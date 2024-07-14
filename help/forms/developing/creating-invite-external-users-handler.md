---
title: 建立邀請外部使用者處理常式
description: 瞭解如何建立邀請外部使用者處理常式。 這可讓Rights Management服務邀請外部使用者成為Rights Management使用者。
role: Developer
exl-id: b0416716-dcc9-4f80-986a-b9660a7c8f6b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# 建立邀請外部使用者處理常式 {#create-invite-external-users-handler}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以為Rights Management服務建立「邀請外部使用者」處理常式。 邀請外部使用者處理常式可讓Rights Management服務邀請外部使用者成為Rights Management使用者。 當使用者成為Rights Management使用者後，該使用者便能執行工作，例如開啟受原則保護的PDF檔案。 將邀請外部使用者處理常式部署至AEM Forms後，您可以使用管理主控台與其互動。

>[!NOTE]
>
>邀請外部使用者處理常式是AEM Forms元件。 建立「邀請外部使用者」處理常式之前，建議您先熟悉如何建立元件。

**步驟摘要**

若要開發「邀請外部使用者」處理常式，您必須執行下列步驟：

1. 設定您的開發環境。
1. 定義「邀請外部使用者」處理常式實作。
1. 定義元件XML檔案。
1. 部署邀請外部使用者處理常式。
1. 測試邀請外部使用者處理常式。

## 設定您的開發環境 {#setting-up-development-environment}

若要設定開發環境，您必須建立Java專案，例如Eclipse專案。 支援的Eclipse版本是`3.2.1`或更新版本。

Rights ManagementSPI要求在專案的類別路徑中設定`edc-server-spi.jar`檔案。 如果您未參考此JAR檔案，則無法在Java專案中使用Rights ManagementSPI。 此JAR檔案與AEM Forms SDK一起安裝在`[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi`資料夾中。

除了將`edc-server-spi.jar`檔案新增至專案的類別路徑外，您還必須新增使用Rights Management服務API所需的JAR檔案。 若要在邀請外部使用者處理常式中使用Rights Management服務API，則需要這些檔案。

## 定義邀請外部使用者處理常式實作 {#define-invite-external-users-handler}

若要開發邀請外部使用者處理常式，您必須建立實作`com.adobe.edc.server.spi.ersp.InvitedUserProvider`介面的Java類別。 此類別包含名為`invitedUser`的方法，當Rights Management服務使用可透過管理主控台存取的&#x200B;**新增受邀使用者**&#x200B;頁面提交電子郵件地址時，會叫用此方法。

`invitedUser`方法接受`java.util.List`執行個體，其中包含從&#x200B;**新增受邀使用者**&#x200B;頁面提交的字串型電子郵件地址。 `invitedUser`方法傳回`InvitedUserProviderResult`物件的陣列，這通常是電子郵件地址到User物件的對應（不傳回null）。

>[!NOTE]
>
>除了示範如何建立邀請外部使用者處理常式外，本節也使用AEM Forms API。

邀請外部使用者處理常式的實作包含名為`createLocalPrincipalAccount`的使用者定義方法。 此方法接受將電子郵件地址指定為引數值的字串值。 `createLocalPrincipalAccount`方法假設名為`EDC_EXTERNAL_REGISTERED`的本機網域已存在。 您可以將此網域名稱設定為您想要的任何名稱；但是，對於生產應用程式，您可能想要與企業網域整合。

`createUsers`方法會對每個電子郵件地址反複運算，並建立對應的User物件（`EDC_EXTERNAL_REGISTERED`網域中的本機使用者）。 最後，呼叫`doEmails`方法。 在範例中，此方法會刻意保留為虛設常式。 在生產環境實作中，它會包含應用程式邏輯，以將邀請電子郵件訊息傳送給新建立的使用者。 範例中會保留此功能，以示範實際應用程式的應用程式邏輯流程。

### 定義邀請外部使用者處理常式實作 {#user-handler-implementation}

下列邀請外部使用者處理常式實作會接受從「新增受邀使用者」頁面（可透過管理控制檯存取）提交的電子郵件地址。

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
>此Java類別會儲存為名為InviteExternalUsersSample.java的JAVA檔案。

## 定義授權處理常式的元件XML檔案 {#define-component-xml-authorization-handler}

尋找元件XML檔案，以部署Invite外部使用者處理常式元件。 每個元件都有元件XML檔案，並提供有關元件的中繼資料。

下列`component.xml`檔案用於邀請外部使用者處理常式。 請注意，服務名稱為`InviteExternalUsersSample`，此服務公開的操作名稱為`invitedUser`。 輸入引數是`java.util.List`執行個體，而輸出值是`com.adobe.edc.server.spi.esrp.InvitedUserProviderResult`執行個體的陣列。

### 定義邀請外部使用者處理常式的元件XML檔案 {#component-xml-invite-external-users-handler}

```as3
<component xmlns="https://adobe.com/idp/dsc/component/document"> 
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

## 正在封裝邀請外部使用者處理常式 {#packaging-invite-external-users-handler}

若要將邀請外部使用者處理常式部署到AEM Forms，您必須將Java專案封裝到JAR檔案中。 請確定JAR檔案中也包含Invite外部使用者處理常式商業邏輯所依賴的外部JAR檔案，例如`edc-server-spi.jar`和`adobe-rightsmanagement-client.jar`檔案。 此外，元件XML檔案也必須存在。 `component.xml`檔案和外部JAR檔案必須位於JAR檔案的根目錄。

>[!NOTE]
>
>在下圖中，顯示`BootstrapImpl`類別。 本節未討論如何建立`BootstrapImpl`類別。

下圖顯示封裝至邀請外部使用者處理常式的JAR檔案中的Java專案內容。

![邀請使用者](assets/ci_ci_InviteUsers.png)

A.元件所需的外部JAR檔案B. JAVA檔案

將邀請外部使用者處理常式封裝到JAR檔案中。 在上圖中，請注意已列出.JAVA檔案。 封裝成JAR檔案後，也必須指定對應的.CLASS檔案。 如果沒有.CLASS檔案，授權處理常式將無法運作。

>[!NOTE]
>
>將外部授權處理常式封裝成JAR檔案後，您就可以將元件部署到AEM Forms。 一次只能部署一個邀請外部使用者處理常式。

>[!NOTE]
>
>您也可以以程式設計方式部署元件。

## 測試邀請外部使用者處理常式 {#testing-invite-external-users-handler}

若要測試邀請外部使用者處理常式，您可以使用管理控制檯來新增要邀請的外部使用者。

若要使用管理主控台新增要邀請的外部使用者：

1. 使用Workbench部署邀請外部使用者處理常式的JAR檔案。
1. 重新啟動應用程式伺服器。

   >[!NOTE]
   >
   > 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

1. 登入管理主控台。
1. 按一下&#x200B;**[!UICONTROL 服務]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 組態]** >已邀請&#x200B;**[!UICONTROL 使用者註冊]**。
1. 勾選&#x200B;**[!UICONTROL 啟用受邀使用者註冊]**&#x200B;方塊，以啟用受邀使用者註冊。 在&#x200B;**[!UICONTROL 使用內建註冊系統]**&#x200B;下，按一下&#x200B;**[!UICONTROL 否]**。 儲存您的設定。
1. 從管理主控台首頁，按一下&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 使用者管理]** > **[!UICONTROL 網域管理]**。
1. 按一下&#x200B;**[!UICONTROL 新增本機網域]**。 在下列頁面中，建立名稱與識別碼值為`EDC_EXTERNAL_REGISTERED`的網域。 儲存您的變更。
1. 從管理主控台首頁，按一下&#x200B;**[!UICONTROL 服務]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 受邀和本機使用者]**。 出現「**[!UICONTROL 新增受邀使用者]**」頁面。
1. 輸入電子郵件地址（由於目前的邀請外部使用者處理常式並不會實際傳送電子郵件訊息，因此電子郵件地址不一定有效）。 按一下&#x200B;**[!UICONTROL 確定]**。 使用者受邀加入系統。
1. 從管理主控台首頁，按一下&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 使用者管理]** > **[!UICONTROL 使用者和群組]**。
1. 在&#x200B;**[!UICONTROL 尋找]**&#x200B;欄位中，輸入您指定的電子郵件地址。 按一下&#x200B;**[!UICONTROL 尋找]**。 您邀請的使用者會顯示為本機`EDC_EXTERNAL_REGISTERED`網域中的使用者。

>[!NOTE]
>
>如果停止或解除安裝元件，邀請外部使用者處理常式會失敗。
