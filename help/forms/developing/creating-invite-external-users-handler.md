---
title: 建立邀請外部使用者處理常式
description: 建立邀請外部使用者處理常式
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---


# 建立邀請外部使用者處理常式{#create-invite-external-users-handler}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

您可以為Rights Management服務建立邀請外部用戶處理程式。 邀請外部用戶處理程式可讓Rights Management服務邀請外部用戶成為Rights Management用戶。 當使用者成為Rights Management使用者後，使用者就可以執行工作，例如開啟受原則保護的PDF檔案。 在邀請外部使用者處理常式部署至AEM Forms後，您可以使用管理主控台與其互動。

>[!NOTE]
>
>邀請外部使用者處理常式是AEM Forms元件。 在您建立邀請外部使用者處理常式之前，建議您熟悉建立元件。

**步驟摘要**

要開發邀請外部用戶處理程式，必須執行以下步驟：

1. 設定您的開發環境。
1. 定義邀請外部使用者處理常式實作。
1. 定義元件XML檔案。
1. 部署邀請外部使用者處理常式。
1. 測試邀請外部使用者處理常式。

## 設定您的開發環境{#setting-up-development-environment}

若要設定您的開發環境，您必須建立新的Java專案，例如Eclipse專案。 支援的Eclipse版本為`3.2.1`或更新版本。

Rights ManagementSPI要求在項目的類路徑中設定`edc-server-spi.jar`檔案。 如果未引用此JAR檔案，則不能在Java項目中使用Rights ManagementSPI。 此JAR檔案隨`[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi`資料夾中的AEM FormsSDK一起安裝。

除了將`edc-server-spi.jar`檔案新增至專案的類別路徑外，您還必須新增使用Rights Management服務API所需的JAR檔案。 在邀請外部用戶處理程式中使用Rights Management服務API時，需要這些檔案。

## 定義邀請外部用戶處理程式實施{#define-invite-external-users-handler}

要開發邀請外部用戶處理程式，必須建立實現`com.adobe.edc.server.spi.ersp.InvitedUserProvider`介面的Java類。 此類包含名為`invitedUser`的方法，當使用&#x200B;**新增已邀請的使用者**&#x200B;頁面提交電子郵件地址時，Rights Management服務會叫用此方法。

`invitedUser`方法接受`java.util.List`實例，該實例包含從&#x200B;**添加邀請的用戶**&#x200B;頁提交的字串型電子郵件地址。 `invitedUser`方法返回`InvitedUserProviderResult`對象的陣列，通常是電子郵件地址與用戶對象的映射（不返回null）。

>[!NOTE]
>
>除了示範如何建立邀請外部使用者處理常式外，本節也使用AEM FormsAPI。

邀請外部用戶處理程式的實現包含名為`createLocalPrincipalAccount`的用戶定義方法。 此方法接受一個字串值，該字串值指定電子郵件地址為參數值。 `createLocalPrincipalAccount`方法假定存在名為`EDC_EXTERNAL_REGISTERED`的本地域。 您可以將此域名配置為任何您希望的域名；但是，對於生產應用程式，您可能想要與企業網域整合。

`createUsers`方法會重複每個電子郵件地址，並建立對應的使用者物件（`EDC_EXTERNAL_REGISTERED`網域中的本機使用者）。 最後，調用`doEmails`方法。 此方法被有意保留為樣本中的樁模組。 在生產實作中，它會包含應用程式邏輯，以傳送邀請電子郵件訊息給新建立的使用者。 它留在範例中，以示範實際應用程式的應用程式邏輯流程。

### 定義邀請外部用戶處理程式實施{#user-handler-implementation}

下列邀請外部使用者處理常式實作接受從「新增已邀請的使用者」頁面提交的電子郵件地址，此頁面可透過管理控制台存取。

```as3
package com.adobe.livecycle.samples.inviteexternalusers.provider; 
 
import com.adobe.edc.server.spi.ersp.*; 
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
import com.adobe.idp.um.api.*; 
import com.adobe.idp.um.api.infomodel.*; 
import com.adobe.idp.um.api.impl.UMBaseLibrary; 
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient; 
 
import java.util.ArrayList; 
import java.util.Iterator; 
import java.util.List; 
 
public class InviteExternalUsersSample implements InvitedUserProvider 
{ 
       private ServiceClientFactory _factory = null; 
 
       private User createLocalPrincipalAccount(String email_address) throws Exception 
       { 
    String ret = null; 
 
    //  Assume the local domain already exists! 
    String domain = "EDC_EXTERNAL_REGISTERED"; 
         
    List aliases = new ArrayList(); 
    aliases.add( email_address ); 
         
    User local_user = UMBaseLibrary.createUser( email_address, domain, email_address ); 
    local_user.setCommonName( email_address ); 
    local_user.setEmail( email_address ); 
    local_user.setEmailAliases( aliases ); 
         
    //  You may wish to disable the local user until, for example, his registration is processed by a confirmation link 
    //local_user.setDisabled( true ); 
 
    DirectoryManager directory_manager = new DirectoryManagerServiceClient( _factory ); 
    String ret_oid = directory_manager.createLocalUser( local_user, null ); 
     
    if( ret_oid == null ) 
    { 
        throw new Exception( "FAILED TO CREATE PRINCIPAL FOR EMAIL ADDRESS: " + email_address ); 
    } 
 
    return local_user; 
       } 
 
       protected User[] createUsers( List emails ) throws Exception 
       { 
    ArrayList ret_users = new ArrayList(); 
 
    _factory = ServiceClientFactory.createInstance(); 
 
    Iterator iter = emails.iterator(); 
 
    while( iter.hasNext() ) 
    { 
        String current_email = (String)iter.next(); 
 
        ret_users.add( createLocalPrincipalAccount( current_email ) ); 
    } 
 
    return (User[])ret_users.toArray( new User[0] ); 
       } 
 
       protected void doInvitations(List emails) 
       { 
    //  Here you may choose to send the users who were created an invitation email 
    //  This step is completely optional, depending on your requirements.   
       } 
 
       public InvitedUserProviderResult[] invitedUser(List emails) 
       { 
    //  This sample demonstrates the workflow for inviting a user via email 
 
    try 
    { 
 
        User[] principals = createUsers(emails); 
 
        InvitedUserProviderResult[] result = new InvitedUserProviderResult[principals.length]; 
        for( int i = 0; i < principals.length; i++ ) 
        { 
        result[i] = new InvitedUserProviderResult(); 
 
        result[i].setEmail( (String)emails.get( i ) ); 
        result[i].setUser( principals[i] ); 
        } 
 
        doInvitations(emails); 
 
        System.out.println( "SUCCESSFULLY INVITED " + result.length + " USERS" ); 
 
        return result; 
 
    } 
    catch( Exception e ) 
    { 
        System.out.println( "FAILED TO INVITE USERS FOR INVITE USERS SAMPLE" ); 
        e.printStackTrace(); 
 
        return new InvitedUserProviderResult[0]; 
    } 
       } 
}
 
```

>[!NOTE]
>
>此Java類會儲存為名為InviteExternalUsersSample.java的JAVA檔案。

## 為授權處理程式{#define-component-xml-authorization-handler}定義元件XML檔案

您必須定義元件XML檔案，才能部署邀請外部使用者處理常式元件。 每個元件都有元件XML檔案，並提供有關元件的中繼資料。

以下`component.xml`檔案用於邀請外部使用者處理常式。 請注意，服務名為`InviteExternalUsersSample` ，此服務公開的操作名為`invitedUser`。 輸入參數是`java.util.List`實例，輸出值是`com.adobe.edc.server.spi.esrp.InvitedUserProviderResult`實例的陣列。

### 為邀請外部用戶處理程式{#component-xml-invite-external-users-handler}定義元件XML檔案

```as3
<component xmlns="http://adobe.com/idp/dsc/component/document"> 
<component-id>com.adobe.livecycle.samples.inviteexternalusers</component-id> 
<version>1.0</version> 
<bootstrap-class>com.adobe.livecycle.samples.inviteexternalusers.provider.BootstrapImpl</bootstrap-class> 
<descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
<services> 
<service name="InviteExternalUsersSample"> 
<specifications> 
<specification spec-id="com.adobe.edc.server.spi.ersp.InvitedUserProvider"/> 
</specifications> 
<specification-version>1.0</specification-version> 
<implementation-class>com.adobe.livecycle.samples.inviteexternalusers.provider.InviteExternalUsersSample</implementation-class> 
<auto-deploy category-id="Samples" service-id="InviteExternalUsersSample" major-version="1" minor-version="0"/> 
<operations> 
<operation name="invitedUser"> 
<input-parameter name="input" type="java.util.List" required="true"/> 
<output-parameter name="result" type="com.adobe.edc.server.spi.esrp.InvitedUserProviderResult[]"/> 
</operation> 
</operations> 
</service> 
</services> 
</component> 
```

## 封裝邀請外部使用者處理常式{#packaging-invite-external-users-handler}

若要將邀請外部使用者處理常式部署至AEM Forms，您必須將Java專案封裝至JAR檔案。 您必須確保邀請外部用戶處理程式的業務邏輯所依賴的外部JAR檔案（如`edc-server-spi.jar`和`adobe-rightsmanagement-client.jar`檔案）也包含在JAR檔案中。 此外，元件XML檔案也必須存在。 `component.xml`檔案和外部JAR檔案必須位於JAR檔案的根目錄中。

>[!NOTE]
>
>在下圖中，顯示`BootstrapImpl`類。 本節不討論如何建立`BootstrapImpl`類。

下圖顯示封裝在邀請外部使用者處理常式的JAR檔案中的Java專案內容。

![邀請使用者](assets/ci_ci_InviteUsers.png)

答：元件B所需的外部JAR檔案。JAVA檔案

您必須將邀請外部用戶處理程式打包到JAR檔案中。 在上圖中，請注意。JAVA檔案已列出。 打包到JAR檔案後，還必須指定相應的。CLASS檔案。 沒有。CLASS檔案，授權處理程式將無法工作。

>[!NOTE]
>
>將外部授權處理常式封裝到JAR檔案後，您就可將元件部署至AEM Forms。 指定時間只能部署一個邀請外部使用者處理常式。

>[!NOTE]
>
>您也可以以程式設計方式部署元件。

## 測試邀請外部用戶處理程式{#testing-invite-external-users-handler}

若要測試邀請外部使用者處理常式，您可以使用管理控制台新增要邀請的外部使用者。

若要使用管理控制台新增要邀請的外部使用者：

1. 使用Workbench部署邀請外部使用者處理常式的JAR檔案。
1. 重新啟動應用程式伺服器。
1. 登入管理控制台。
1. 按一下「**[!UICONTROL 服務]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 配置]** >已邀請&#x200B;**[!UICONTROL 用戶註冊]**」。
1. 選中&#x200B;**[!UICONTROL 啟用邀請的用戶註冊]**&#x200B;框，以啟用邀請的用戶註冊。 在&#x200B;**[!UICONTROL 使用內置註冊系統]**&#x200B;下，按一下&#x200B;**[!UICONTROL 否]**。 儲存您的設定。
1. 在管理控制台首頁，按一下「設定&#x200B;**** > **[!UICONTROL 使用者管理]** > **[!UICONTROL 網域管理]**」。
1. 按一下&#x200B;**[!UICONTROL 新建本地域]**。 在以下頁面上，建立名稱和標識符值為`EDC_EXTERNAL_REGISTERED`的域。 儲存您的變更。
1. 在管理控制台首頁中，按一下「**[!UICONTROL 服務]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 已邀請和本地用戶]**」。 此時將顯示&#x200B;**[!UICONTROL 添加邀請的用戶]**&#x200B;頁。
1. 輸入電子郵件地址（因為目前的邀請外部使用者處理常式實際上不會傳送電子郵件訊息，所以電子郵件地址不一定有效）。 按一下&#x200B;**[!UICONTROL 「確定」]**。系統會邀請用戶。
1. 在管理控制台首頁中，按一下「設定&#x200B;**** > **[!UICONTROL 使用者管理]** > **[!UICONTROL 使用者和群組]**」。
1. 在&#x200B;**[!UICONTROL Find]**&#x200B;欄位中，輸入您指定的電子郵件地址。 按一下&#x200B;**[!UICONTROL 查找]**。 您邀請的使用者會以使用者身分出現在本機`EDC_EXTERNAL_REGISTERED`網域中。

>[!NOTE]
>
>如果停止或解除安裝元件，則邀請外部使用者處理常式會失敗。
