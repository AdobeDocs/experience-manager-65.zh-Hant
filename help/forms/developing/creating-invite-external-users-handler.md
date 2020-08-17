---
title: 建立邀請外部使用者處理常式
description: 建立邀請外部使用者處理常式
translation-type: tm+mt
source-git-commit: 92e5cc0b1934dad641357a22894e70a3660b774a
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---


# 建立邀請外部使用者處理常式 {#create-invite-external-users-handler}

您可以為Rights Management服務建立邀請外部使用者處理常式。 邀請外部使用者處理常式可讓Rights Management服務邀請外部使用者成為Rights Management使用者。 當使用者成為Rights Management使用者後，使用者就可以執行工作，例如開啟受原則保護的PDF檔案。 將「邀請外部使用者處理常式」部署至AEM Forms後，您可以使用管理主控台與其互動。

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

## 設定您的開發環境 {#setting-up-development-environment}

若要設定您的開發環境，您必須建立新的Java專案，例如Eclipse專案。 支援的Eclipse版本為或 `3.2.1` 更新版本。

Rights Management SPI要求在 `edc-server-spi.jar` 專案的類別路徑中設定檔案。 如果未引用此JAR檔案，則不能在Java項目中使用Rights Management SPI。 此JAR檔案會隨AEM Forms SDK一起安裝在檔案夾 `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` 中。

除了將檔案新 `edc-server-spi.jar` 增至專案的類別路徑外，您還必須新增使用Rights Management Service API所需的JAR檔案。 在邀請外部使用者處理常式中使用Rights Management Service API時，需要這些檔案。

## 定義邀請外部使用者處理常式實作 {#define-invite-external-users-handler}

若要開發邀請外部使用者處理常式，您必須建立實作介面的Java `com.adobe.edc.server.spi.ersp.InvitedUserProvider` 類別。 此類包含名為的方法 `invitedUser`，當使用「新增已邀請的使用者」頁面提交電子郵件地址時，Rights Management服務會叫用此方法。此頁面可透過 **** 管理主控台存取。

該方 `invitedUser` 法接受例項 `java.util.List` ，該例項包含從「新增已邀請的使用者」頁面提交的字串 **型電子郵件地址** 。 該方 `invitedUser` 法返回一組對象， `InvitedUserProviderResult` 通常是電子郵件地址與用戶對象的映射（不返回空值）。

>[!NOTE]
>
>除了示範如何建立邀請外部使用者處理常式外，本節也使用AEM Forms API。

邀請外部用戶處理程式的實現包含名為的用戶定義方法 `createLocalPrincipalAccount`。 此方法接受一個字串值，該字串值指定電子郵件地址為參數值。 該方 `createLocalPrincipalAccount` 法假定本地域的存在是預先存在的，稱為 `EDC_EXTERNAL_REGISTERED`。 您可以將此域名配置為任何您希望的域名；但是，對於生產應用程式，您可能想要與企業網域整合。

該方 `createUsers` 法會重複每個電子郵件地址，並建立對應的使用者物件(網域中的本機 `EDC_EXTERNAL_REGISTERED` 使用者)。 最後，對該方 `doEmails` 法進行了調用。 此方法被有意保留為樣本中的樁模組。 在生產實作中，它會包含應用程式邏輯，以傳送邀請電子郵件訊息給新建立的使用者。 它留在範例中，以示範實際應用程式的應用程式邏輯流程。

### 定義邀請外部使用者處理常式實作 {#user-handler-implementation}

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

## 為授權處理程式定義元件XML檔案 {#define-component-xml-authorization-handler}

您必須定義元件XML檔案，才能部署邀請外部使用者處理常式元件。 每個元件都有元件XML檔案，並提供有關元件的中繼資料。

下列檔 `component.xml` 案用於邀請外部使用者處理常式。 請注意，服務名 `InviteExternalUsersSample` 稱為，此服務提供的操作名為 `invitedUser`。 輸入參數是實 `java.util.List` 例，輸出值是實例的陣 `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` 列。

### 為邀請外部用戶處理程式定義元件XML檔案 {#component-xml-invite-external-users-handler}

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

## 封裝邀請外部使用者處理常式 {#packaging-invite-external-users-handler}

若要將邀請外部使用者處理常式部署至AEM Forms，您必須將Java專案封裝至JAR檔案。 您必須確保邀請外部用戶處理程式的業務邏輯所依賴的外部JAR檔案(如 `edc-server-spi.jar` 和 `adobe-rightsmanagement-client.jar` 檔案)也包含在JAR檔案中。 此外，元件XML檔案也必須存在。 文 `component.xml` 件和外部JAR檔案必須位於JAR檔案的根目錄。

>[!NOTE]
>
>在下圖中，顯示 `BootstrapImpl` 了類。 本節不討論如何建立類 `BootstrapImpl` 別。

下圖顯示封裝在邀請外部使用者處理常式的JAR檔案中的Java專案內容。

![邀請使用者](assets/ci_ci_InviteUsers.png)

答：元件B所需的外部JAR檔案。JAVA檔案

您必須將邀請外部用戶處理程式打包到JAR檔案中。 在上圖中，請注意。JAVA檔案已列出。 打包到JAR檔案後，還必須指定相應的。CLASS檔案。 沒有。CLASS檔案，授權處理程式將無法工作。

>[!NOTE]
>
>將外部授權處理常式封裝至JAR檔案後，您就可將元件部署至AEM Forms。 指定時間只能部署一個邀請外部使用者處理常式。

>[!NOTE]
>
>您也可以以程式設計方式部署元件。

## 測試邀請外部使用者處理常式 {#testing-invite-external-users-handler}

若要測試邀請外部使用者處理常式，您可以使用管理控制台新增要邀請的外部使用者。

若要使用管理控制台新增要邀請的外部使用者：

1. 使用Workbench部署邀請外部使用者處理常式的JAR檔案。
1. 重新啟動應用程式伺服器。
1. 登入管理控制台。
1. 按一 **[!UICONTROL 下「服務]** > **[!UICONTROL Rights Management]** >設 **[!UICONTROL 定]** >邀請的使 ****&#x200B;用者註冊」。
1. 勾選「啟用邀請的使用者註冊」方塊， **[!UICONTROL 以啟用邀請的使用者註冊]** 。 在「 **[!UICONTROL 使用內建註冊系統]**」下，單 **[!UICONTROL 擊否]**。 儲存您的設定。
1. 在管理控制台首頁中，按一下「 **[!UICONTROL 設定]** >使 **[!UICONTROL 用者管理]** >網 **[!UICONTROL 域管理]**」。
1. 按一 **[!UICONTROL 下「新增本機網域]**」。 在以下頁面上，建立名稱和識別碼值為的網域 `EDC_EXTERNAL_REGISTERED`。 儲存您的變更。
1. 在管理控制台首頁中，按一下「 **[!UICONTROL 服務]** > **[!UICONTROL Rights Management]** >已邀 **[!UICONTROL 請和本機使用者」]**。 此時將 **[!UICONTROL 顯示「添加邀請的用戶]** 」頁。
1. 輸入電子郵件地址（因為目前的邀請外部使用者處理常式實際上不會傳送電子郵件訊息，所以電子郵件地址不一定有效）。 按一下&#x200B;**[!UICONTROL 「確定」]**。系統會邀請用戶。
1. 在管理控制台首頁，按一下「 **[!UICONTROL 設定]** >使 **[!UICONTROL 用者管理]** >使 **[!UICONTROL 用者和群組]**」。
1. 在「尋 **[!UICONTROL 找]** 」欄位中，輸入您指定的電子郵件地址。 按一 **[!UICONTROL 下「尋找]**」。 您邀請的使用者會以使用者的身分出現在本機網 `EDC_EXTERNAL_REGISTERED` 域中。

>[!NOTE]
>
>如果停止或解除安裝元件，則邀請外部使用者處理常式會失敗。
