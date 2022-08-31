---
title: 建立「邀請外部用戶」處理程式
description: 建立「邀請外部用戶」處理程式
role: Developer
exl-id: b0416716-dcc9-4f80-986a-b9660a7c8f6b
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---

# 建立「邀請外部用戶」處理程式 {#create-invite-external-users-handler}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以為Rights Management服務建立「邀請外部使用者」處理常式。 「邀請外部使用者」處理常式可讓Rights Management服務邀請外部使用者成為Rights Management使用者。 當用戶成為Rights Management用戶後，用戶能夠執行任務，例如開啟受策略保護的PDF文檔。 將「邀請外部使用者」處理常式部署至AEM Forms後，您就可以使用管理控制台來與其互動。

>[!NOTE]
>
>邀請外部使用者處理常式是AEM Forms元件。 建立「邀請外部使用者」處理常式之前，建議您先熟悉建立元件的方式。

**步驟摘要**

要開發「邀請外部用戶」處理程式，您必須執行以下步驟：

1. 設定您的開發環境。
1. 定義「邀請外部使用者」處理常式實作。
1. 定義元件XML檔案。
1. 部署「邀請外部用戶」處理程式。
1. 測試「邀請外部用戶」處理程式。

## 設定您的開發環境 {#setting-up-development-environment}

若要設定開發環境，您必須建立新的Java專案，例如Eclipse專案。 支援的Eclipse版本為 `3.2.1` 或更新版本。

Rights ManagementSPI要求 `edc-server-spi.jar` 檔案，以在專案的類別路徑中設定。 如果您未參考此JAR檔案，則無法在Java項目中使用Rights ManagementSPI。 此JAR檔案會與AEM Forms SDK一起安裝於 `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` 檔案夾。

除了新增 `edc-server-spi.jar` 檔案至專案的類別路徑，您也必須新增使用Rights Management服務API所需的JAR檔案。 若要在「邀請外部使用者」處理常式中使用Rights Management服務API，需要這些檔案。

## 定義邀請外部使用者處理常式實作 {#define-invite-external-users-handler}

若要開發邀請外部使用者處理常式，您必須建立實作的Java類別 `com.adobe.edc.server.spi.ersp.InvitedUserProvider` 介面。 此類包含名為 `invitedUser`，使用提交電子郵件地址時，Rights Management服務會叫用 **新增受邀的使用者** 可透過管理控制台存取的頁面。

此 `invitedUser` 方法接受 `java.util.List` 例項，包含從 **新增受邀的使用者** 頁面。 此 `invitedUser` 方法傳回陣列 `InvitedUserProviderResult` 對象，通常是電子郵件地址與用戶對象的映射（不返回null）。

>[!NOTE]
>
>除了說明如何建立邀請外部使用者處理常式外，本節也使用AEM Forms API。

邀請外部用戶處理程式的實施包含用戶定義的方法，名為 `createLocalPrincipalAccount`. 此方法接受字串值，該字串值會將電子郵件地址指定為參數值。 此 `createLocalPrincipalAccount` 方法假設存在名為的本地域 `EDC_EXTERNAL_REGISTERED`. 您可以將此域名配置為任何您希望的域名；但是，對於生產應用程式，您可能希望與企業域整合。

此 `createUsers` 方法會反覆顯示每個電子郵件地址，並建立對應的使用者物件( `EDC_EXTERNAL_REGISTERED` 網域)。 最後， `doEmails` 方法。 此方法被有意保留為樣本中的存根。 在生產實作中，它會包含應用程式邏輯，以傳送邀請電子郵件訊息給新建立的使用者。 它留在示例中，以演示實際應用程式的應用程式邏輯流。

### 定義邀請外部使用者處理常式實作 {#user-handler-implementation}

以下邀請外部用戶處理程式實施接受從「添加受邀用戶」頁面提交的電子郵件地址，該頁可通過管理控制台訪問。

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
>此Java類將另存為名為InviteExternalUsersSample.java的JAVA檔案。

## 為授權處理程式定義元件XML檔案 {#define-component-xml-authorization-handler}

必須定義元件XML檔案，才能部署邀請外部用戶處理程式元件。 每個元件都存在一個元件XML檔案，並提供有關該元件的元資料。

以下 `component.xml` 檔案用於邀請外部用戶處理程式。 請注意，服務名稱為 `InviteExternalUsersSample` 此服務公開的操作已命名 `invitedUser`. 輸入參數為 `java.util.List` instance和輸出值是 `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` 例項。

### 為邀請外部用戶處理程式定義元件XML檔案 {#component-xml-invite-external-users-handler}

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

## 封裝邀請外部使用者處理常式 {#packaging-invite-external-users-handler}

若要將邀請外部使用者處理常式部署至AEM Forms，您必須將Java專案封裝至JAR檔案。 您必須確保邀請外部用戶處理程式的業務邏輯所依賴的外部JAR檔案，例如 `edc-server-spi.jar` 和 `adobe-rightsmanagement-client.jar` 檔案也包含在JAR檔案中。 此外，元件XML檔案必須存在。 此 `component.xml` 檔案和外部JAR檔案必須位於JAR檔案的根目錄中。

>[!NOTE]
>
>在下圖中， `BootstrapImpl` 會顯示類別。 本節不討論如何建立 `BootstrapImpl` 類別。

下圖顯示封裝到邀請外部用戶處理程式的JAR檔案中的Java項目內容。

![邀請使用者](assets/ci_ci_InviteUsers.png)

A.元件B. JAVA檔案所需的外部JAR檔案

必須將邀請外部用戶處理程式打包到JAR檔案中。 在上圖中，請注意.JAVA檔案已列出。 打包到JAR檔案後，還必須指定相應的.CLASS檔案。 若沒有.CLASS檔案，授權處理常式將無法運作。

>[!NOTE]
>
>將外部授權處理程式封裝為JAR檔案後，您就可將元件部署至AEM Forms。 指定時間只能部署一個邀請外部用戶處理程式。

>[!NOTE]
>
>您也可以以程式設計方式部署元件。

## 測試邀請外部使用者處理常式 {#testing-invite-external-users-handler}

若要測試邀請外部使用者處理常式，您可以使用管理控制台來新增要邀請的外部使用者。

若要使用管理控制台新增要邀請的外部使用者：

1. 使用Workbench部署邀請外部用戶處理常式的JAR檔案。
1. 重新啟動應用程式伺服器。
1. 登入管理控制台。
1. 按一下 **[!UICONTROL 服務]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 設定]** >受邀 **[!UICONTROL 用戶註冊]**.
1. 通過檢查 **[!UICONTROL 啟用邀請的用戶註冊]** 框。 在 **[!UICONTROL 使用內置註冊系統]**，按一下 **[!UICONTROL 否]**. 儲存您的設定。
1. 在管理控制台首頁，按一下 **[!UICONTROL 設定]** > **[!UICONTROL 使用者管理]** > **[!UICONTROL 網域管理]**.
1. 按一下 **[!UICONTROL 新本地域]**. 在以下頁面中，建立名稱和標識符值為 `EDC_EXTERNAL_REGISTERED`. 儲存您的變更。
1. 在管理控制台首頁，按一下 **[!UICONTROL 服務]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 受邀和本地用戶]**. 此 **[!UICONTROL 添加邀請的用戶]** 頁。
1. 輸入電子郵件地址（因為目前的邀請外部使用者處理常式實際上並未傳送電子郵件訊息，因此電子郵件地址不必有效）。 按一下&#x200B;**[!UICONTROL 「確定」]**。系統會邀請使用者加入系統。
1. 在管理控制台首頁，按一下 **[!UICONTROL 設定]** > **[!UICONTROL 使用者管理]** > **[!UICONTROL 使用者和群組]**.
1. 在 **[!UICONTROL 查找]** 欄位，輸入您指定的電子郵件地址。 按一下 **[!UICONTROL 查找]**. 您邀請的使用者會以使用者身分顯示在本機 `EDC_EXTERNAL_REGISTERED` 網域。

>[!NOTE]
>
>如果停止或解除安裝元件，則邀請外部使用者處理常式會失敗。
