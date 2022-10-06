---
title: 管理使用者
seo-title: Managing Users
description: 使用用戶管理API建立可管理角色、權限和承擔者（可以是用戶或組）以及驗證用戶的用戶端應用程式。
seo-description: Use the User Management API to create client applications that can manage roles, permissions, and principals (which can be users or groups), as well as authenticate users.
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '6228'
ht-degree: 0%

---

# 管理使用者 {#managing-users}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於使用者管理**

您可以使用使用者管理API來建立可管理角色、權限和承擔者（可以是使用者或群組），以及驗證使用者的用戶端應用程式。 使用者管理API包含下列AEM Forms API:

* 目錄管理器服務API
* Authentication Manager服務API
* 授權管理器服務API

使用者管理可讓您指派、移除和決定角色和權限。 它也可讓您指派、移除和查詢網域、使用者和群組。 最後，您可以使用「使用者管理」來驗證使用者。

在 [新增使用者](users.md#adding-users) 您將了解如何以程式設計方式新增使用者。 本節使用目錄管理器服務API。

在 [刪除用戶](users.md#deleting-users) 您將了解如何以程式設計方式刪除使用者。 本節使用目錄管理器服務API。

在 [管理使用者和群組](users.md#managing-users-and-groups) 您將了解本機使用者和目錄使用者之間的差異，並參閱範例，了解如何使用Java和網站服務API，以程式設計方式管理使用者和群組。 本節使用目錄管理器服務API。

在 [管理角色和權限](users.md#managing-roles-and-permissions) 您將了解系統角色和權限，以及您可以以程式設計方式來增強這些角色和權限，並參閱如何使用Java和網站服務API以程式設計方式管理角色和權限的範例。 本節同時使用目錄管理器服務API和授權管理器服務API。

在 [驗證使用者](users.md#authenticating-users) 您將看到如何使用Java和網站服務API，以程式設計方式驗證使用者的範例。 本節使用授權管理器服務API。

**了解驗證程式**

「使用者管理」提供內建的驗證功能，也可讓您將其與自己的驗證提供者連線。 當「使用者管理」收到驗證請求時（例如，使用者嘗試登入），會將使用者資訊傳遞給驗證提供者以進行驗證。 用戶管理在驗證用戶後從驗證提供程式接收結果。

下圖顯示嘗試登入的一般使用者、使用者管理和驗證提供者之間的互動。

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

下表說明了身份驗證過程的每個步驟。

<table>
 <thead>
  <tr>
   <th><p>步驟</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>用戶嘗試登錄調用「用戶管理」的服務。 用戶指定用戶名和密碼。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>User Management會將使用者名稱和密碼以及設定資訊傳送至驗證提供者。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>驗證提供者連接到用戶儲存並驗證用戶。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>驗證提供程式將結果返回給用戶管理。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>使用者管理可讓使用者登入或拒絕產品的存取權。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果伺服器時區與客戶端時區不同，當在WebSphere應用程式伺服器群集上使用.NET客戶端在本機SOAP堆棧上使用AEM Forms生成PDF服務的WSDL時，可能會發生以下用戶管理驗證錯誤：

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**了解目錄管理**

用戶管理與支援到LDAP目錄的連接的目錄服務提供程式(DirectoryManagerService)一起打包。 如果貴組織使用非LDAP儲存庫來儲存用戶記錄，則可以建立與儲存庫一起使用的您自己的目錄服務提供程式。

目錄服務提供程式應用戶管理的請求從用戶儲存中檢索記錄。 「用戶管理」定期在資料庫中快取用戶和組記錄，以提高效能。

目錄服務提供程式可用於將用戶管理資料庫與用戶儲存同步。 此步驟可確保所有使用者目錄資訊以及所有使用者和群組記錄都為最新狀態。

此外， DirectoryManagerService還允許您建立和管理域。 網域會定義不同的使用者基礎。 網域的界限通常會根據組織的結構方式或使用者存放區的設定方式來定義。 用戶管理域提供身份驗證提供程式和目錄服務提供程式使用的配置設定。

在「用戶管理」導出的配置XML中，具有屬性值的根節點 `Domains` 包含為「用戶管理」定義的每個域的XML元素。 這些元素中的每個都包含其他元素，這些元素定義與特定服務提供商關聯的域的各個方面。

**了解objectSID值**

使用Active Directory時，請務必了解 `objectSID` 值不是跨多個網域的唯一屬性。 此值儲存對象的安全標識符。 在多個網域環境中（例如，網域樹狀結構）, `objectSID` 值可以不同。

安 `objectSID` 如果對象從一個Active Directory域移動到另一個域，則值將更改。 某些物件具有相同 `objectSID` 值。 例如，BUILDIN\Administrators、BUILDIN\Power Users等組具有相同的 `objectSID` 值（無論網域為何）。 這些 `objectSID` 值是眾所周知的。

## 新增使用者 {#adding-users}

您可以使用目錄管理器服務API（Java和Web服務），以寫程式方式將用戶添加到AEM Forms。 新增使用者後，當執行需要使用者的服務作業時，即可使用該使用者。 例如，您可以將任務指派給新使用者。

### 步驟摘要 {#summary-of-steps}

要添加用戶，請執行以下步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService客戶端。
1. 定義使用者資訊。
1. 新增使用者至AEM Forms。
1. 確認已新增使用者。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務操作之前，請建立目錄管理器服務API客戶端。

**定義使用者資訊**

使用目錄管理器服務API添加新用戶時，請為該用戶定義資訊。 通常，新增使用者時，您會定義下列值：

* **域名**:使用者所屬的網域(例如 `DefaultDom`)。
* **使用者識別碼值**:使用者的識別碼值(例如 `wblue`)。
* **主體類型**:使用者的類型(例如，您可以指定 `USER)`.
* **指定名稱**:使用者的指定名稱(例如 `Wendy`)。
* **姓**:用戶的家族名稱(例如 `Blue)`.
* **地區**:用戶的地區資訊。

**新增使用者至AEM Forms**

定義使用者資訊後，即可將使用者新增至AEM Forms。 若要新增使用者，請叫用 `DirectoryManagerServiceClient` 物件 `createLocalUser` 方法。

**確認已新增使用者**

您可以確認已新增使用者，以確保未發生任何問題。 使用使用者識別碼值來找出新使用者。

**另請參閱**

[使用Java API新增使用者](users.md#add-users-using-the-java-api)

[使用網站服務API新增使用者](users.md#add-users-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[刪除用戶](users.md#deleting-users)

### 使用Java API新增使用者 {#add-users-using-the-java-api}

使用目錄管理器服務API(Java)添加用戶：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerServices客戶端。

   建立 `DirectoryManagerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 定義使用者資訊。

   * 建立 `UserImpl` 物件，使用其建構子。
   * 叫用 `UserImpl` 物件 `setDomainName` 方法。 傳遞指定網域名稱的字串值。
   * 通過調用 `UserImpl` 物件 `setPrincipalType` 方法。 傳遞指定使用者類型的字串值。 例如，您可以指定 `USER`.
   * 叫用 `UserImpl` 物件 `setUserid` 方法。 傳遞指定使用者識別碼值的字串值。 例如，您可以指定 `wblue`.
   * 叫用 `UserImpl` 物件 `setCanonicalName` 方法。 傳遞指定使用者標準名稱的字串值。 例如，您可以指定 `wblue`.
   * 叫用 `UserImpl` 物件 `setGivenName` 方法。 傳遞指定使用者指定名稱的字串值。 例如，您可以指定 `Wendy`.
   * 通過調用 `UserImpl` 物件 `setFamilyName` 方法。 傳遞一個字串值，該字串值指定用戶的姓。 例如，您可以指定 `Blue`.

   >[!NOTE]
   >
   >調用屬於 `UserImpl` 物件來設定其他值。 例如，可以通過調用 `UserImpl` 物件 `setLocale` 方法。

1. 新增使用者至AEM Forms。

   叫用 `DirectoryManagerServiceClient` 物件 `createLocalUser` 方法，並傳遞下列值：

   * 此 `UserImpl` 代表新使用者的物件
   * 代表使用者密碼的字串值

   此 `createLocalUser` 方法返回指定本地用戶標識符值的字串值。

1. 確認已新增使用者。

   * 建立 `PrincipalSearchFilter` 物件，使用其建構子。
   * 叫用 `PrincipalSearchFilter` 物件 `setUserId` 方法。 傳遞代表使用者識別碼值的字串值。
   * 叫用 `DirectoryManagerServiceClient` 物件 `findPrincipals` 方法並傳遞 `PrincipalSearchFilter` 物件。 此方法會傳回 `java.util.List` 例項，其中每個元素都 `User` 物件。 重複 `java.util.List` 例項來尋找使用者。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API新增使用者](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API新增使用者 {#add-users-using-the-web-service-api}

使用目錄管理器服務API（Web服務）添加用戶：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確保為服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立DirectoryManagerService客戶端。

   * 建立 `DirectoryManagerServiceClient` 物件，使用其預設建構函式。
   * 建立 `DirectoryManagerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時，會使用此屬性。 請確定您指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DirectoryManagerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 定義使用者資訊。

   * 建立 `UserImpl` 物件，使用其建構子。
   * 將字串值指派給 `UserImpl` 物件 `domainName` 欄位。
   * 通過為 `UserImpl` 物件 `principalType` 欄位。 例如，您可以指定 `USER`.
   * 將字串值指派給 `UserImpl` 物件 `userid` 欄位。
   * 將字串值指派給 `UserImpl` 物件 `canonicalName` 欄位。
   * 將字串值指派給 `UserImpl` 物件 `givenName` 欄位。
   * 通過為 `UserImpl` 物件 `familyName` 欄位。

1. 新增使用者至AEM Forms。

   叫用 `DirectoryManagerServiceClient` 物件 `createLocalUser` 方法，並傳遞下列值：

   * 此 `UserImpl` 代表新使用者的物件
   * 代表使用者密碼的字串值

   此 `createLocalUser` 方法返回指定本地用戶標識符值的字串值。

1. 確認已新增使用者。

   * 建立 `PrincipalSearchFilter` 物件，使用其建構子。
   * 為 `PrincipalSearchFilter` 物件 `userId` 欄位。
   * 叫用 `DirectoryManagerServiceClient` 物件 `findPrincipals` 方法並傳遞 `PrincipalSearchFilter` 物件。 此方法會傳回 `MyArrayOfUser` 集合物件，其中每個元素都是 `User` 物件。 重複 `MyArrayOfUser` 集合，以找出使用者。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除用戶 {#deleting-users}

您可以使用目錄管理器服務API（Java和Web服務），以程式設計方式從AEM Forms中刪除用戶。 刪除用戶後，無法再使用該用戶執行需要用戶的服務操作。 例如，您不能將任務分配給已刪除的用戶。

### 步驟摘要 {#summary_of_steps-1}

要刪除用戶，請執行以下步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService客戶端。
1. 指定要刪除的使用者。
1. 從AEM Forms刪除使用者。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務API操作之前，請建立目錄管理器服務客戶端。

**指定要刪除的使用者**

您可以使用使用者的識別碼值來指定要刪除的使用者。

**從AEM Forms刪除使用者**

若要刪除使用者，請叫用 `DirectoryManagerServiceClient` 物件 `deleteLocalUser` 方法。

**另請參閱**

[使用Java API刪除使用者](users.md#delete-users-using-the-java-api)

[使用網站服務API刪除使用者](users.md#delete-users-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增使用者](users.md#adding-users)

### 使用Java API刪除使用者 {#delete-users-using-the-java-api}

使用目錄管理器服務API(Java)刪除用戶：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   建立 `DirectoryManagerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要刪除的使用者。

   * 建立 `PrincipalSearchFilter` 物件，使用其建構子。
   * 叫用 `PrincipalSearchFilter` 物件 `setUserId` 方法。 傳遞代表使用者識別碼值的字串值。
   * 叫用 `DirectoryManagerServiceClient` 物件 `findPrincipals` 方法並傳遞 `PrincipalSearchFilter` 物件。 此方法會傳回 `java.util.List` 例項，其中每個元素都 `User` 物件。 重複 `java.util.List` 例項來尋找要刪除的使用者。

1. 從AEM Forms刪除使用者。

   叫用 `DirectoryManagerServiceClient` 物件 `deleteLocalUser` 方法，並傳遞 `User` 物件 `oid` 欄位。 叫用 `User` 物件 `getOid` 方法。 使用 `User` 從 `java.util.List` 例項。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速入門（EJB模式）:使用Java API刪除使用者](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[快速入門（SOAP模式）:使用Java API刪除使用者](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API刪除使用者 {#delete-users-using-the-web-service-api}

使用目錄管理器服務API（Web服務）刪除用戶：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   * 建立 `DirectoryManagerServiceClient` 物件，使用其預設建構函式。
   * 建立 `DirectoryManagerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時，會使用此屬性。 請確定您指定 `blob=mtom.`
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DirectoryManagerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 指定要刪除的使用者。

   * 建立 `PrincipalSearchFilter` 物件，使用其建構子。
   * 將字串值指派給 `PrincipalSearchFilter` 物件 `userId` 欄位。
   * 叫用 `DirectoryManagerServiceClient` 物件 `findPrincipals` 方法並傳遞 `PrincipalSearchFilter` 物件。 此方法會傳回 `MyArrayOfUser` 集合物件，其中每個元素都是 `User` 物件。 重複 `MyArrayOfUser` 集合，以找出使用者。 此 `User` 從 `MyArrayOfUser` 集合物件可用來刪除使用者。

1. 從AEM Forms刪除使用者。

   將 `User` 物件 `oid` 欄位值 `DirectoryManagerServiceClient` 物件 `deleteLocalUser` 方法。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立群組 {#creating-groups}

您可以使用目錄管理器服務API（Java和Web服務）以寫程式方式建立AEM Forms組。 建立群組後，您可以使用該群組執行需要群組的服務操作。 例如，您可以指派使用者至新群組。 (請參閱 [管理使用者和群組](users.md#managing-users-and-groups).)

### 步驟摘要 {#summary_of_steps-2}

要建立組，請執行以下步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService客戶端。
1. 確定組不存在。
1. 建立群組。
1. 對組執行操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務操作之前，請建立目錄管理器服務API客戶端。

**確定組是否存在**

建立群組時，請確定群組不存在於相同的網域中。 也就是說，兩個群組在相同網域內不能有相同的名稱。 要執行此任務，請執行搜索並根據兩個值篩選搜索結果。 將主體類型設定為 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` 以確保只傳回群組。 同時，請務必指定網域名稱。

**建立群組**

在您確定該組不存在於域中後，請建立該組並指定以下屬性：

* **CommonName**:群組的名稱。
* **網域**:新增群組的網域。
* **說明**:群組的說明。

**對組執行操作**

建立群組後，您可以使用群組執行動作。 例如，您可以新增使用者至群組。 若要將使用者新增至群組，請擷取該使用者和群組的唯一識別碼值。 將這些值傳遞至 `addPrincipalToLocalGroup` 方法。

**另請參閱**

[使用Java API建立群組](users.md#create-groups-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增使用者](users.md#adding-users)

[刪除用戶](users.md#deleting-users)

### 使用Java API建立群組 {#create-groups-using-the-java-api}

使用目錄管理器服務API(Java)建立組：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   建立 `DirectoryManagerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 確定組是否存在。

   * 建立 `PrincipalSearchFilter` 物件，使用其建構子。
   * 通過調用 `PrincipalSearchFilter` 物件 `setPrincipalType` 物件。 傳遞值 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * 叫用 `PrincipalSearchFilter` 物件 `setSpecificDomainName` 物件。 傳遞指定網域名稱的字串值。
   * 要查找組，請調用 `DirectoryManagerServiceClient` 物件 `findPrincipals` 方法（主體可以是組）。 傳遞 `PrincipalSearchFilter` 指定主體類型和域名的對象。 此方法會傳回 `java.util.List` 例項，其中每個元素都是 `Group` 例項。 每個群組例項都符合使用 `PrincipalSearchFilter` 物件。
   * 重複 `java.util.List` 例項。 對於每個元素，擷取群組名稱。 確保組名不等於新組名。

1. 建立群組。

   * 如果群組不存在，請叫用 `Group` 物件 `setCommonName` 方法，並傳遞指定群組名稱的字串值。
   * 叫用 `Group` 物件 `setDescription` 方法，並傳遞指定群組說明的字串值。
   * 叫用 `Group` 物件 `setDomainName` 方法，並傳遞指定網域名稱的字串值。
   * 叫用 `DirectoryManagerServiceClient` 物件 `createLocalGroup` 方法並傳遞 `Group` 例項。

   此 `createLocalUser` 方法返回指定本地用戶標識符值的字串值。

1. 對組執行操作。

   * 建立 `PrincipalSearchFilter` 物件，使用其建構子。
   * 叫用 `PrincipalSearchFilter` 物件 `setUserId` 方法。 傳遞代表使用者識別碼值的字串值。
   * 叫用 `DirectoryManagerServiceClient` 物件 `findPrincipals` 方法並傳遞 `PrincipalSearchFilter` 物件。 此方法會傳回 `java.util.List` 例項，其中每個元素都 `User` 物件。 重複 `java.util.List` 例項來尋找使用者。
   * 叫用 `DirectoryManagerServiceClient` 物件 `addPrincipalToLocalGroup` 方法。 傳遞的傳回值 `User` 物件 `getOid` 方法。 傳遞的傳回值 `Group` 對象 `getOid` 方法(使用 `Group` 代表新群組的例項)。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 管理使用者和群組 {#managing-users-and-groups}

本主題說明如何使用(Java)以程式設計方式指派、移除和查詢網域、使用者和群組。

>[!NOTE]
>
>設定網域時，您必須為群組和使用者設定唯一識別碼。 所選屬性不僅在LDAP環境中是唯一的，而且也必須是不可變的，並且在目錄中不會更改。 此屬性也必須是簡單的字串資料類型(Active Directory 2000/2003當前允許的唯一例外是 `"objectsid"`，此為二進位值)。 Novell eDirectory屬性 `"GUID"`，例如不是簡單的字串資料類型，因此無法運作。

* 對於Active Directory，請使用 `"objectsid"`.
* 對於SunOne，請使用 `"nsuniqueid"`.

>[!NOTE]
>
>不支援在LDAP目錄同步正在進行時建立多個本地用戶和組。 嘗試此程式可能會導致錯誤。

### 步驟摘要 {#summary_of_steps-3}

要管理用戶和組，請執行以下步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService客戶端。
1. 調用相應的用戶或組操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務操作之前，必須建立目錄管理器服務客戶端。 使用Java API，您可借由建立 `DirectoryManagerServiceClient` 物件。 有了Web服務API，您可以建立 `DirectoryManagerServiceService` 物件。

**調用相應的用戶或組操作**

建立服務客戶端後，您就可以調用用戶或組管理操作。 服務客戶端允許您分配、刪除和查詢域、用戶和組。 請注意，可以將目錄主體或本地主體添加到本地組，但無法將本地主體添加到目錄組。

**另請參閱**

[使用Java API管理使用者和群組](users.md#managing-users-and-groups-using-the-java-api)

[使用網站服務API管理使用者和群組](users.md#managing-users-and-groups-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理使用者和群組 {#managing-users-and-groups-using-the-java-api}

要使用(Java)以寫程式方式管理用戶、組和域，請執行以下任務：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。 如需這些檔案的位置資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. 建立DirectoryManagerService客戶端。

   建立 `DirectoryManagerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。 如需詳細資訊，請參閱 [設定連接屬性&#x200B;](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. 調用相應的用戶或組操作。

   要查找用戶或組，請調用 `DirectoryManagerServiceClient` 對象查找主體的方法（因為主體可以是用戶或組）。 在以下範例中， `findPrincipals` 方法(使用搜尋篩選器 `PrincipalSearchFilter` 物件)。

   由於在此情況下，傳回值是 `java.util.List` 包含 `Principal` 對象，迭代查看結果並轉換 `Principal` 對象 `User` 或 `Group` 對象。

   使用結果 `User` 或 `Group` 對象(兩者均繼承自 `Principal` 介面)，擷取您在工作流程中需要的資訊。 例如，域名和規範名稱值組合在一起，可唯一標識主體。 這些會透過叫用 `Principal` 物件 `getDomainName` 和 `getCanonicalName` 方法。

   若要刪除本機使用者，請叫用 `DirectoryManagerServiceClient` 物件 `deleteLocalUser` 方法，並傳遞使用者的識別碼。

   若要刪除本機群組，請叫用 `DirectoryManagerServiceClient` 物件 `deleteLocalGroup` 方法，並傳遞群組的識別碼。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API管理使用者和群組 {#managing-users-and-groups-using-the-web-service-api}

要使用目錄管理器服務API（Web服務）以寫程式方式管理用戶、組和域，請執行以下任務：

1. 包含專案檔案。

   * 建立一個使用目錄管理器WSDL的Microsoft .NET客戶端程式集。 (請參閱 [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * 參考Microsoft .NET客戶端程式集。 (請參閱 [建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. 建立DirectoryManagerService客戶端。

   建立 `DirectoryManagerServiceService` 對象，使用代理類的建構子。

1. 調用相應的用戶或組操作。

   要查找用戶或組，請調用 `DirectoryManagerServiceService` 對象查找主體的方法（因為主體可以是用戶或組）。 在以下範例中， `findPrincipalsWithFilter` 方法(使用搜尋篩選器 `PrincipalSearchFilter` 物件)。 使用 `PrincipalSearchFilter` 對象，只有在 `isLocal` 屬性設為 `true`. 此行為與Java API的發生方式不同。

   >[!NOTE]
   >
   >如果未在搜尋篩選器中指定結果的最大數量(透過 `PrincipalSearchFilter.resultsMax` 欄位)，最多將傳回1000個結果。 這與使用Java API時的行為不同，Java API的預設上限為10個結果。 此外，搜尋方法如 `findGroupMembers` 除非在搜尋篩選器中指定結果的最大數量(例如，透過 `GroupMembershipSearchFilter.resultsMax` 欄位)。 這會套用至繼承自 `GenericSearchFilter` 類別。 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   由於在此情況下，傳回值是 `object[]` 包含 `Principal` 對象，迭代查看結果並轉換 `Principal` 對象 `User` 或 `Group` 對象。

   使用結果 `User` 或 `Group` 對象(兩者均繼承自 `Principal` 介面)，擷取您在工作流程中需要的資訊。 例如，域名和規範名稱值組合在一起，可唯一標識主體。 這些會透過叫用 `Principal` 物件 `domainName` 和 `canonicalName` 欄位。

   若要刪除本機使用者，請叫用 `DirectoryManagerServiceService` 物件 `deleteLocalUser` 方法，並傳遞使用者的識別碼。

   若要刪除本機群組，請叫用 `DirectoryManagerServiceService` 物件 `deleteLocalGroup` 方法，並傳遞群組的識別碼。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 管理角色和權限 {#managing-roles-and-permissions}

本主題說明如何使用授權管理器服務API(Java)，以程式設計方式指派、移除及決定角色和權限。

在AEM Forms, *角色* 是一組存取一或多個系統層級資源的權限。 這些權限是透過「使用者管理」建立，並由服務元件強制執行。 例如，管理員可以將「策略集作者」的角色分配給一組用戶。 然後，Rights Management將允許具有該角色的組的用戶通過管理控制台建立策略集。

角色有兩種類型： *預設角色* 和 *自訂角色*. 預設角色(*系統角色)* 已經住在AEM Forms了。 假定管理員不能刪除或修改預設角色，因此不可變。 因此，管理員建立的自定義角色可變，管理員隨後可修改或刪除這些角色。

角色可讓您更輕鬆管理權限。 當角色被分配給承擔者時，一組權限被自動分配給該承擔者，並且承擔者的所有與訪問相關的特定決策都基於該整體分配的權限集。

### 步驟摘要 {#summary_of_steps-4}

要管理角色和權限，請執行以下步驟：

1. 包含專案檔案。
1. 建立AuthorizationManagerService客戶端。
1. 調用相應的角色或權限操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立AuthorizationManagerService客戶端**

在以寫程式方式執行用戶管理授權管理器服務操作之前，必須建立授權管理器服務客戶端。 使用Java API，您可以建立 `AuthorizationManagerServiceClient` 物件。

**調用適當的角色或權限操作**

建立服務客戶端後，您就可以調用角色或權限操作。 服務客戶端允許您分配、刪除和確定角色和權限。

**另請參閱**

[使用Java API管理角色和權限](users.md#managing-roles-and-permissions-using-the-java-api)

[使用網站服務API管理角色和權限](users.md#managing-roles-and-permissions-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理角色和權限 {#managing-roles-and-permissions-using-the-java-api}

要使用授權管理器服務API(Java)管理角色和權限，請執行以下任務：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立AuthorizationManagerService客戶端。

   建立 `AuthorizationManagerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用相應的角色或權限操作。

   要將角色分配給承擔者，請調用 `AuthorizationManagerServiceClient` 物件 `assignRole` 方法，並傳遞下列值：

   * A `java.lang.String` 包含角色標識符的對象
   * 陣列 `java.lang.String` 包含主標識符的對象。

   要從主體中刪除角色，請調用 `AuthorizationManagerServiceClient` 物件 `unassignRole` 方法，並傳遞下列值：

   * A `java.lang.String` 包含角色標識符的對象。
   * 陣列 `java.lang.String` 包含主標識符的對象。


**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API管理角色和權限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API管理角色和權限 {#managing-roles-and-permissions-using-the-web-service-api}

使用授權管理器服務API（Web服務）管理角色和權限：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立AuthorizationManagerService客戶端。

   * 建立 `AuthorizationManagerServiceClient` 物件，使用其預設建構函式。
   * 建立 `AuthorizationManagerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時，會使用此屬性。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `AuthorizationManagerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 調用相應的角色或權限操作。

   要將角色分配給承擔者，請調用 `AuthorizationManagerServiceClient` 物件 `assignRole` 方法，並傳遞下列值：

   * A `string` 包含角色標識符的對象
   * A `MyArrayOf_xsd_string` 包含主標識符的對象。

   要從主體中刪除角色，請調用 `AuthorizationManagerServiceService` 物件 `unassignRole` 方法，並傳遞下列值：

   * A `string` 包含角色標識符的對象。
   * 陣列 `string` 包含主標識符的對象。


**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 驗證使用者 {#authenticating-users}

本主題說明如何使用Authentication Manager服務API(Java)，讓用戶端應用程式以程式設計方式驗證使用者。

與儲存安全資料的企業資料庫或其他企業儲存庫交互可能需要用戶身份驗證。

例如，假設使用者在網頁中輸入使用者名稱和密碼，並將值提交至托管Forms的J2EE應用程式伺服器。 Forms自訂應用程式可使用Authentication Manager服務驗證使用者。

如果驗證成功，則應用程式訪問安全企業資料庫。 否則，會傳送訊息給使用者，指出該使用者不是授權使用者。

下圖顯示應用程式的邏輯流程。

![au_au_umauth_process](assets/au_au_umauth_process.png)

下表說明此圖中的步驟

<table>
 <thead>
  <tr>
   <th><p>步驟</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>用戶訪問網站並指定用戶名和密碼。 此資訊會提交至托管AEM Forms的J2EE應用程式伺服器。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>使用者憑證會透過Authentication Manager服務進行驗證。 如果用戶憑據有效，工作流將繼續到步驟3。 否則，會傳送訊息給使用者，指出該使用者不是授權使用者。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>從安全企業資料庫中檢索用戶資訊和表單設計。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>使用者資訊與表單設計合併，表單轉譯給使用者。 </p></td>
  </tr>
 </tbody>
</table>

### 步驟摘要 {#summary_of_steps-5}

要以寫程式方式驗證用戶，請執行以下步驟：

1. 包含專案檔案。
1. 建立AuthenticationManagerService客戶端。
1. 調用驗證操作。
1. 如有必要，請擷取內容，讓用戶端應用程式可將其轉送至其他AEM Forms服務進行驗證。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立AuthenticationManagerService客戶端**

在以寫程式方式對用戶進行身份驗證之前，必須建立AuthenticationManagerService客戶端。 使用Java API時，請建立 `AuthenticationManagerServiceClient` 物件。

**調用驗證操作**

建立服務客戶端後，您就可以調用驗證操作。 此操作將需要有關用戶的資訊，如用戶名和密碼。 如果用戶未進行身份驗證，則會引發異常。

**擷取驗證內容**

一旦您驗證了使用者，您就可以根據已驗證的使用者建立內容。 然後，您可以使用內容叫用其他AEM Forms服務。 例如，您可以使用內容來建立 `EncryptionServiceClient` 使用密碼加密PDF文檔。 確保已驗證的使用者具有 `Services User` 叫用AEM Forms服務時所需的URL。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密碼加密PDF文檔](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API驗證使用者 {#authenticate-a-user-using-the-java-api}

使用Authentication Manager服務API(Java)驗證用戶：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立AuthenticationManagerServices客戶端。

   建立 `AuthenticationManagerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用驗證操作。

   叫用 `AuthenticationManagerServiceClient` 物件 `authenticate` 方法，並傳遞下列值：

   * A `java.lang.String` 包含使用者名稱的物件。
   * 位元組陣列(a `byte[]` 物件)，包含使用者的密碼。 您可以取得 `byte[]` 對象，方法是調用 `java.lang.String` 物件 `getBytes` 方法。

   驗證方法會傳回 `AuthResult` 物件，包含已驗證使用者的相關資訊。

1. 擷取驗證內容。

   叫用 `ServiceClientFactory` 物件 `getContext` 方法，將返回 `Context` 物件。

   然後叫用 `Context` 物件 `initPrincipal` 方法並傳遞 `AuthResult`.

### 使用網站服務API驗證使用者 {#authenticate-a-user-using-the-web-service-api}

使用Authentication Manager服務API（Web服務）驗證用戶：

1. 包含專案檔案。

   * 建立會使用驗證管理器WSDL的Microsoft .NET客戶端程式集。 (請參閱 [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * 參考Microsoft .NET客戶端程式集。 (請參閱 [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. 建立AuthenticationManagerService客戶端。

   建立 `AuthenticationManagerServiceService` 對象，使用代理類的建構子。

1. 調用驗證操作。

   叫用 `AuthenticationManagerServiceClient` 物件 `authenticate` 方法，並傳遞下列值：

   * A `string` 包含用戶名的對象
   * 位元組陣列(a `byte[]` 物件)，包含使用者的密碼。 您可以取得 `byte[]` 透過轉換 `string` 包含密碼的對象 `byte[]` 陣列，使用下列範例中的邏輯。
   * 傳回的值將是 `AuthResult` 物件，可用來擷取使用者的相關資訊。 在以下範例中，使用者的資訊是先取得 `AuthResult` 物件 `authenticatedUser` 欄位，並隨後獲得結果 `User` 物件 `canonicalName` 和 `domainName` 欄位。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 以程式設計方式同步使用者 {#programmatically-synchronizing-users}

您可以使用使用者管理API，以程式設計方式同步使用者。 同步使用者時，您會將AEM Forms與位於使用者存放庫中的使用者資料更新。 例如，假設您將新使用者新增至您的使用者存放庫。 執行同步操作後，新的使用者會變成AEM表單使用者。 此外，您的使用者存放庫中不再有的使用者，也會從AEM Forms中移除。

下圖顯示AEM Forms與使用者存放庫同步。

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

下表說明此圖中的步驟

<table>
 <thead>
  <tr>
   <th><p>步驟</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>用戶端應用程式要求AEM Forms執行同步作業。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Forms執行同步操作。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>更新使用者資訊。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>使用者可檢視更新的使用者資訊。 </p></td>
  </tr>
 </tbody>
</table>

### 步驟摘要 {#summary_of_steps-6}

要以寫程式方式同步用戶，請執行以下步驟：

1. 包含專案檔案。
1. 建立UserManagerUtilServiceClient客戶端。
1. 指定企業網域。
1. 調用驗證操作。
1. 確定同步操作是否完成

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立UserManagerUtilServiceClientclient**

您必須先建立 `UserManagerUtilServiceClient` 物件。

**指定企業網域**

在使用用戶管理API執行同步操作之前，請指定用戶所屬的企業域。 您可以指定一或多個企業網域。 在以寫程式方式執行同步操作之前，必須使用管理控制台來設定企業域。 (請參閱 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_63).)

**調用同步操作**

指定一個或多個企業域後，可以執行同步操作。 執行此操作所花的時間取決於位於用戶儲存庫中的用戶記錄數。

**確定同步操作是否完成**

以寫程式方式執行同步操作後，可以確定操作是否完成。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密碼加密PDF文檔](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API以程式設計方式同步使用者 {#programmatically-synchronizing-users-using-the-java-api}

使用「使用者管理API」(Java)同步使用者：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar和adobe-usermanager-util-client.jar。

1. 建立UserManagerUtilServiceClient客戶端。

   建立 `UserManagerUtilServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定企業網域。

   * 叫用 `UserManagerUtilServiceClient` 物件 `scheduleSynchronization` 啟動用戶同步操作的方法。
   * 建立 `java.util.Set` 例項，使用 `HashSet` 建構子。 請確定您指定 `String` 作為資料類型。 此 `Java.util.Set` 實例儲存同步操作要應用的域名。
   * 對於要添加的每個域名，調用 `java.util.Set` 物件的add方法，並傳遞網域名稱。

1. 調用同步操作。

   叫用 `ServiceClientFactory` 物件 `getContext` 方法，將返回 `Context` 物件。

   然後叫用 `Context` 物件 `initPrincipal` 方法並傳遞 `AuthResult`.

**另請參閱**

[以程式設計方式同步使用者](users.md#programmatically-synchronizing-users)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
