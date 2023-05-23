---
title: 建立邀請外部用戶處理程式
description: 建立邀請外部用戶處理程式
role: Developer
exl-id: b0416716-dcc9-4f80-986a-b9660a7c8f6b
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---

# 建立邀請外部用戶處理程式 {#create-invite-external-users-handler}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

您可以為Rights Management服務建立邀請外部用戶處理程式。 邀請外部用戶處理程式使Rights Management服務能夠邀請外部用戶成為Rights Management用戶。 在用戶成為Rights Management用戶後，用戶能夠執行任務，例如開啟受策略保護的PDF文檔。 將邀請外部用戶處理程式部署到AEM Forms後，可以使用管理控制台與其進行交互。

>[!NOTE]
>
>邀請外部用戶處理程式是AEM Forms元件。 在建立邀請外部用戶處理程式之前，建議您熟悉建立元件。

**步驟摘要**

要開發邀請外部用戶處理程式，必須執行以下步驟：

1. 設定開發環境。
1. 定義邀請外部用戶處理程式實現。
1. 定義元件XML檔案。
1. 部署邀請外部用戶處理程式。
1. Test邀請外部用戶處理程式。

## 設定開發環境 {#setting-up-development-environment}

要設定開發環境，必須建立新的Java項目，如Eclipse項目。 支援的Eclipse版本 `3.2.1` 或稍後。

Rights ManagementSPI要求 `edc-server-spi.jar` 要在項目的類路徑中設定的檔案。 如果未引用此JAR檔案，則無法在Java項目中使用Rights ManagementSPI。 此JAR檔案隨AEM FormsSDK一起安裝在 `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` 的子菜單。

除添加 `edc-server-spi.jar` 檔案到項目的類路徑，還必須添加使用Rights Management服務API所需的JAR檔案。 在邀請外部用戶處理程式內使用Rights Management服務API時需要這些檔案。

## 定義邀請外部用戶處理程式實現 {#define-invite-external-users-handler}

要開發邀請外部用戶處理程式，必須建立實現 `com.adobe.edc.server.spi.ersp.InvitedUserProvider` 。 此類包含名為 `invitedUser`,Rights Management服務使用 **添加邀請的用戶** 可通過管理控制台訪問的頁面。

的 `invitedUser` 方法接受 `java.util.List` 實例，包含從 **添加邀請的用戶** 的子菜單。 的 `invitedUser` 方法返回 `InvitedUserProviderResult` 對象，通常是電子郵件地址到用戶對象的映射（不返回空值）。

>[!NOTE]
>
>除了演示如何建立邀請外部用戶處理程式外，本節還使用AEM FormsAPI。

邀請外部用戶處理程式的實現包含一個名為 `createLocalPrincipalAccount`。 此方法接受一個字串值，該字串值將電子郵件地址指定為參數值。 的 `createLocalPrincipalAccount` 方法假定本地域(稱為 `EDC_EXTERNAL_REGISTERED`。 您可以將此域名配置為任何您想要的域名；但是，對於生產應用程式，您可能希望與企業域整合。

的 `createUsers` 方法在每個電子郵件地址上迭代並建立相應的用戶對象(本地用戶在 `EDC_EXTERNAL_REGISTERED` 域)。 最後， `doEmails` 調用方法。 此方法被有意地作為存根留在示例中。 在生產實現中，它將包含應用程式邏輯，用於向新建立的用戶發送邀請電子郵件。 在示例中留下來演示一個實際應用的應用邏輯流程。

### 定義邀請外部用戶處理程式實現 {#user-handler-implementation}

以下邀請外部用戶處理程式實現接受通過管理控制台可訪問的「添加邀請的用戶」頁提交的電子郵件地址。

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
>此Java類另存為名為InviteExternalUsersSample.java的JAVA檔案。

## 為授權處理程式定義元件XML檔案 {#define-component-xml-authorization-handler}

必須定義元件XML檔案才能部署邀請外部用戶處理程式元件。 每個元件都存在一個元件XML檔案，並提供有關該元件的元資料。

以下 `component.xml` 檔案用於invite外部用戶處理程式。 請注意，服務名稱 `InviteExternalUsersSample` 此服務公開的操作名為 `invitedUser`。 輸入參數是 `java.util.List` 實例和輸出值是 `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` 實例。

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

## 打包邀請外部用戶處理程式 {#packaging-invite-external-users-handler}

要將邀請外部用戶處理程式部署到AEM Forms，必須將Java項目打包到JAR檔案中。 必須確保邀請外部用戶處理程式的業務邏輯所依賴的外部JAR檔案，如 `edc-server-spi.jar` 和 `adobe-rightsmanagement-client.jar` 檔案也包含在JAR檔案中。 此外，元件XML檔案必須存在。 的 `component.xml` 檔案和外部JAR檔案必須位於JAR檔案的根目錄。

>[!NOTE]
>
>在下圖中， `BootstrapImpl` 類。 本節不討論如何建立 `BootstrapImpl` 類。

下圖顯示了打包到邀請外部用戶處理程式的JAR檔案中的Java項目內容。

![邀請用戶](assets/ci_ci_InviteUsers.png)

答：元件B所需的外部JAR檔案。JAVA檔案

必須將邀請外部用戶處理程式打包到JAR檔案中。 在上圖中，請注意.JAVA檔案已列出。 打包到JAR檔案後，還必須指定相應的.CLASS檔案。 如果沒有.CLASS檔案，授權處理程式將不工作。

>[!NOTE]
>
>將外部授權處理程式打包到JAR檔案後，可以將元件部署到AEM Forms。 在給定時間只能部署一個邀請外部用戶處理程式。

>[!NOTE]
>
>也可以以寫程式方式部署元件。

## 測試邀請外部用戶處理程式 {#testing-invite-external-users-handler}

要test邀請外部用戶處理程式，可以使用管理控制台添加要邀請的外部用戶。

要使用管理控制台添加要邀請的外部用戶，請執行以下操作：

1. 使用Workbench部署邀請外部用戶處理程式的JAR檔案。
1. 重新啟動應用程式伺服器。
1. 登錄到管理控制台。
1. 按一下 **[!UICONTROL 服務]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 配置]** >邀請 **[!UICONTROL 用戶註冊]**。
1. 通過檢查 **[!UICONTROL 啟用邀請的用戶註冊]** 框。 下 **[!UICONTROL 使用內置註冊系統]**&#x200B;按一下 **[!UICONTROL 否]**。 保存設定。
1. 在管理控制台首頁中，按一下 **[!UICONTROL 設定]** > **[!UICONTROL 用戶管理]** > **[!UICONTROL 域管理]**。
1. 按一下 **[!UICONTROL 新建本地域]**。 在以下頁面上，建立名稱和標識符值為 `EDC_EXTERNAL_REGISTERED`。 保存更改。
1. 在管理控制台首頁中，按一下 **[!UICONTROL 服務]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 已邀請和本地用戶]**。 的 **[!UICONTROL 添加邀請的用戶]** 的子菜單。
1. 輸入電子郵件地址（因為當前邀請外部用戶處理程式實際上不發送電子郵件，因此電子郵件地址不必有效）。 按一下&#x200B;**[!UICONTROL 「確定」]**。系統會邀請用戶。
1. 在管理控制台首頁中，按一下 **[!UICONTROL 設定]** > **[!UICONTROL 用戶管理]** > **[!UICONTROL 用戶和組]**。
1. 在 **[!UICONTROL 查找]** 欄位中，輸入您指定的電子郵件地址。 按一下 **[!UICONTROL 查找]**。 您邀請的用戶在本地中顯示為用戶 `EDC_EXTERNAL_REGISTERED` 。

>[!NOTE]
>
>如果停止或卸載元件，則邀請外部用戶處理程式將失敗。
