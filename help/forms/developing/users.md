---
title: 管理使用者
seo-title: 管理使用者
description: 'null'
seo-description: 'null'
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 管理使用者 {#managing-users}

**關於用戶管理**

您可以使用使用者管理API來建立用戶端應用程式，以管理角色、權限和承擔者（可以是使用者或群組），並驗證使用者。 使用者管理API包含下列AEM Forms API:

* 目錄管理器服務API
* Authentication Manager服務API
* 授權管理器服務API

使用者管理可讓您指派、移除和決定角色和權限。 它也可讓您指派、移除和查詢網域、使用者和群組。 最後，您可以使用「使用者管理」來驗證使用者。

在「 [新增使用者](users.md#adding-users) 」中，您將瞭解如何以程式設計方式新增使用者。 本節使用目錄管理器服務API。

在刪 [除用戶](users.md#deleting-users) ，您將瞭解如何以程式設計方式刪除用戶。 本節使用目錄管理器服務API。

在「 [管理使用者和群組](users.md#managing-users-and-groups) 」中，您將瞭解本機使用者和目錄使用者之間的差異，並檢視如何使用Java和web service API以程式設計方式管理使用者和群組的範例。 本節使用目錄管理器服務API。

在「 [管理角色和權限](users.md#managing-roles-and-permissions) 」中，您將瞭解系統角色和權限，以及如何以程式設計方式來增強這些角色和權限，並檢視如何使用Java和web service API以程式設計方式管理角色和權限的範例。 本節同時使用目錄管理器服務API和授權管理器服務API。

在「 [驗證使用者](users.md#authenticating-users) 」中，您會看到如何使用Java和web service API以程式設計方式驗證使用者的範例。 本節使用授權管理器服務API。

**瞭解驗證程式**

使用者管理提供內建的驗證功能，也讓您能夠將它與您自己的驗證提供者連接。 當「使用者管理」收到驗證要求（例如，使用者嘗試登入）時，會將使用者資訊傳遞給驗證提供者以進行驗證。 使用者管理會在驗證使用者後，從驗證提供者接收結果。

下圖顯示嘗試登入的一般使用者、使用者管理與驗證提供者之間的互動。

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

下表說明驗證程式的每個步驟。

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
   <td><p>用戶嘗試登錄調用「用戶管理」的服務。 用戶指定用戶名和口令。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>使用者管理會將使用者名稱和密碼以及設定資訊傳送至驗證提供者。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>認證提供者連接至使用者儲存並驗證使用者。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>驗證提供者會將結果傳回使用者管理。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>使用者管理可讓使用者登入或拒絕產品存取。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果伺服器時區與用戶端時區不同，當在WebSphere應用程式伺服器叢集上使用。NET用戶端在原生SOAP堆疊上使用AEM Forms的WSDL產生PDF服務時，可能會發生下列使用者管理驗證錯誤：

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**瞭解目錄管理**

用戶管理與支援到LDAP目錄的連接的目錄服務提供程式(DirectoryManagerService)一起打包。 如果您的組織使用非LDAP儲存庫來儲存用戶記錄，則可以建立與儲存庫一起使用的自己的目錄服務提供程式。

目錄服務提供者應使用者管理的要求，從使用者存放區擷取記錄。 使用者管理會定期在資料庫中快取使用者和群組記錄，以改善效能。

目錄服務提供程式可用於將用戶管理資料庫與用戶儲存同步。 此步驟可確保所有使用者目錄資訊以及所有使用者和群組記錄都是最新的。

此外， DirectoryManagerService還允許您建立和管理域。 網域會定義不同的使用者群。 域的邊界通常根據組織的結構方式或用戶儲存的設定來定義。 使用者管理網域提供驗證提供者和目錄服務提供者使用的組態設定。

在「用戶管理」導出的配置XML中，屬性值為的根節點包含為「用戶管理」定義的 `Domains` 每個域的XML元素。 這些元素中的每一個都包含其他元素，這些元素定義與特定服務提供商相關聯的域的各個方面。

**瞭解objectSID值**

使用Active Directory時，請務必瞭解值不是 `objectSID` 跨多個網域的唯一屬性。 此值儲存對象的安全標識符。 在多網域環境中（例如，網域樹狀結構），值 `objectSID` 可以不同。

如果 `objectSID` 將對象從一個Active Directory域移動到另一個域，則值將更改。 有些物件在網域的 `objectSID` 任何位置都有相同的值。 例如，BUILTIN\Administrators、BUILTIN\Power Users等群組無論網域為何都 `objectSID` 有相同的值。 這些 `objectSID` 值是眾所周知的。

## 新增使用者 {#adding-users}

您可以使用Directory Manager Service API（Java和web service），以程式設計方式將使用者新增至AEM Forms。 在添加用戶後，在執行需要用戶的服務操作時可以使用該用戶。 例如，您可以指派任務給新用戶。

### 步驟摘要 {#summary-of-steps}

要添加用戶，請執行以下步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService客戶端。
1. 定義使用者資訊。
1. 將使用者新增至AEM Forms。
1. 確認已添加用戶。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務操作之前，請建立目錄管理器服務API客戶端。

**定義使用者資訊**

當您使用目錄管理器服務API添加新用戶時，請為該用戶定義資訊。 通常，在添加新用戶時，您定義以下值：

* **域名**:用戶所屬的域(例如 `DefaultDom`)。
* **使用者識別碼值**:使用者的識別碼值(例如 `wblue`)。
* **主要類型**:使用者類型(例如，您可以指定 `USER)`。
* **指定名稱**:使用者的指定名稱(例如 `Wendy`)。
* **姓氏**:用戶的族名(例如 `Blue)`。
* **地區**:用戶的地區資訊。

**將使用者新增至AEM Forms**

在您定義使用者資訊後，您可以將使用者新增至AEM Forms。 若要新增使用者，請叫 `DirectoryManagerServiceClient` 用物件的方 `createLocalUser` 法。

**確認已添加用戶**

您可以驗證是否已新增使用者，以確保未發生任何問題。 使用使用者識別碼值來尋找新使用者。

**另請參閱**

[使用Java API新增使用者](users.md#add-users-using-the-java-api)

[使用web service API新增使用者](users.md#add-users-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[刪除用戶](users.md#deleting-users)

### 使用Java API新增使用者 {#add-users-using-the-java-api}

使用目錄管理器服務API(Java)添加用戶：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerServices客戶端。

   使用其 `DirectoryManagerServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 定義使用者資訊。

   * 使用其 `UserImpl` 建構函式建立物件。
   * 調用物件的方法，以 `UserImpl` 設定詳細名 `setDomainName` 稱。 傳遞指定網域名稱的字串值。
   * 調用物件的方法，以設 `UserImpl` 定承擔者 `setPrincipalType` 類型。 傳遞指定使用者類型的字串值。 例如，您可以指定 `USER`。
   * 呼叫物件的方法，以設 `UserImpl` 定使用者識別 `setUserid` 碼值。 傳遞指定使用者識別碼值的字串值。 例如，您可以指定 `wblue`。
   * 調用物件的方法，以 `UserImpl` 設定標準 `setCanonicalName` 名稱。 傳遞指定使用者標準名稱的字串值。 例如，您可以指定 `wblue`。
   * 調用物件的方法，以設 `UserImpl` 定指定的 `setGivenName` 名稱。 傳遞指定使用者指定名稱的字串值。 例如，您可以指定 `Wendy`。
   * 通過調用對象的方法 `UserImpl` 來設定族 `setFamilyName` 名。 傳遞指定使用者系列名稱的字串值。 例如，您可以指定 `Blue`。
   >[!NOTE]
   >
   >調用屬於該對象的方 `UserImpl` 法以設定其他值。 例如，您可以叫用物件的方法來設定 `UserImpl` 地區設定 `setLocale` 值。

1. 將使用者新增至AEM Forms。

   叫用物 `DirectoryManagerServiceClient` 件的方 `createLocalUser` 法並傳遞下列值：

   * 代 `UserImpl` 表新用戶的對象
   * 代表使用者密碼的字串值
   該方 `createLocalUser` 法返回一個字串值，它指定本地用戶標識符值。

1. 確認已添加用戶。

   * 使用其 `PrincipalSearchFilter` 建構函式建立物件。
   * 呼叫物件的方法，以設 `PrincipalSearchFilter` 定使用者識別 `setUserId` 碼值。 傳遞代表使用者識別碼值的字串值。
   * 叫用物 `DirectoryManagerServiceClient` 件的方 `findPrincipals` 法並傳遞物 `PrincipalSearchFilter` 件。 此方法傳回 `java.util.List` 例項，其中每個元素都是物 `User` 件。 重複執行個 `java.util.List` 體以找出使用者。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API新增使用者](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API新增使用者 {#add-users-using-the-web-service-api}

使用目錄管理器服務API（web服務）添加用戶：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您對服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立DirectoryManagerService客戶端。

   * 使用其 `DirectoryManagerServiceClient` 預設建構函式建立物件。
   * 使用建 `DirectoryManagerServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。 確定您已指定 `?blob=mtom`。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `DirectoryManagerServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 定義使用者資訊。

   * 使用其 `UserImpl` 建構函式建立物件。
   * 將字串值指派給物件的欄位，以設 `UserImpl` 定demain `domainName` 名稱。
   * 通過為對象欄位指定字串值來設 `UserImpl` 置承擔者類 `principalType` 型。 例如，您可以指定 `USER`。
   * 將字串值指派給物件的欄位，以設 `UserImpl` 定使用者識別 `userid` 碼值。
   * 為物件欄位指派字串值，以設定 `UserImpl` 標準名稱 `canonicalName` 值。
   * 將字串值指派給物件的欄位，以設 `UserImpl` 定指定的名 `givenName` 稱值。
   * 通過為對象欄位指定字串值來設 `UserImpl` 置族名 `familyName` 值。

1. 將使用者新增至AEM Forms。

   叫用物 `DirectoryManagerServiceClient` 件的方 `createLocalUser` 法並傳遞下列值：

   * 代 `UserImpl` 表新用戶的對象
   * 代表使用者密碼的字串值
   該方 `createLocalUser` 法返回一個字串值，它指定本地用戶標識符值。

1. 確認已添加用戶。

   * 使用其 `PrincipalSearchFilter` 建構函式建立物件。
   * 將代表使用者識別碼值的字串值指派至物件的欄位，以設定使用者 `PrincipalSearchFilter` 的使用者識別 `userId` 碼值。
   * 叫用物 `DirectoryManagerServiceClient` 件的方 `findPrincipals` 法並傳遞物 `PrincipalSearchFilter` 件。 此方法會傳回 `MyArrayOfUser` 系列物件，其中每個元素都是 `User` 物件。 重複整個系 `MyArrayOfUser` 列以找出使用者。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除用戶 {#deleting-users}

您可以使用Directory Manager Service API（Java和web service），以程式設計方式從AEM Forms刪除使用者。 刪除用戶後，無法再使用該用戶執行需要用戶的服務操作。 例如，您無法將任務指派給已刪除的用戶。

### 步驟摘要 {#summary_of_steps-1}

要刪除用戶，請執行以下步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService客戶端。
1. 指定要刪除的使用者。
1. 從AEM Forms刪除使用者。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務API操作之前，請建立目錄管理器服務客戶端。

**指定要刪除的使用者**

您可以使用使用者的識別碼值來指定要刪除的使用者。

**從AEM Forms刪除使用者**

若要刪除使用者，請叫 `DirectoryManagerServiceClient` 用物件的方 `deleteLocalUser` 法。

**另請參閱**

[使用Java API刪除使用者](users.md#delete-users-using-the-java-api)

[使用web service API刪除使用者](users.md#delete-users-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增使用者](users.md#adding-users)

### 使用Java API刪除使用者 {#delete-users-using-the-java-api}

使用目錄管理器服務API(Java)刪除用戶：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   使用其 `DirectoryManagerServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 指定要刪除的使用者。

   * 使用其 `PrincipalSearchFilter` 建構函式建立物件。
   * 呼叫物件的方法，以設 `PrincipalSearchFilter` 定使用者識別 `setUserId` 碼值。 傳遞代表使用者識別碼值的字串值。
   * 叫用物 `DirectoryManagerServiceClient` 件的方 `findPrincipals` 法並傳遞物 `PrincipalSearchFilter` 件。 此方法傳回 `java.util.List` 例項，其中每個元素都是物 `User` 件。 重複執行個 `java.util.List` 體以找出要刪除的使用者。

1. 從AEM Forms刪除使用者。

   叫用 `DirectoryManagerServiceClient` 物件的方 `deleteLocalUser` 法並傳遞物件 `User` 欄位的 `oid` 值。 叫用 `User` 物件的方 `getOid` 法。 使用從 `User` 實例檢索的對 `java.util.List` 像。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API刪除用戶](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[快速入門（SOAP模式）:使用Java API刪除用戶](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API刪除使用者 {#delete-users-using-the-web-service-api}

使用目錄管理器服務API（web服務）刪除用戶：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   * 使用其 `DirectoryManagerServiceClient` 預設建構函式建立物件。
   * 使用建 `DirectoryManagerServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。 確定您指定 `blob=mtom.`
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `DirectoryManagerServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 指定要刪除的使用者。

   * 使用其 `PrincipalSearchFilter` 建構函式建立物件。
   * 將字串值指派給物件的欄位，以設 `PrincipalSearchFilter` 定使用者識別 `userId` 碼值。
   * 叫用物 `DirectoryManagerServiceClient` 件的方 `findPrincipals` 法並傳遞物 `PrincipalSearchFilter` 件。 此方法會傳回 `MyArrayOfUser` 系列物件，其中每個元素都是 `User` 物件。 重複整個系 `MyArrayOfUser` 列以找出使用者。 從收 `User` 集對象中檢索 `MyArrayOfUser` 的對象用於刪除用戶。

1. 從AEM Forms刪除使用者。

   將物件的欄位值傳 `User` 遞至物件 `oid` 的方法， `DirectoryManagerServiceClient` 以刪除使 `deleteLocalUser` 用者。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立群組 {#creating-groups}

您可以使用Directory Manager Service API（Java和web service）以程式設計方式建立AEM Forms群組。 建立群組後，您可以使用該群組來執行需要群組的服務作業。 例如，您可以指派使用者至新群組。 (請參 [閱管理使用者和群組](users.md#managing-users-and-groups)。)

### 步驟摘要 {#summary_of_steps-2}

要建立組，請執行以下步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService客戶端。
1. 確定組不存在。
1. 建立群組。
1. 對組執行操作。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務操作之前，請建立目錄管理器服務API客戶端。

**確定組是否存在**

建立群組時，請確定群組不存在於相同網域中。 也就是說，兩個群組在相同網域內不能有相同的名稱。 要執行此任務，請執行搜索並基於兩個值篩選搜索結果。 將承擔者類型設 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` 置為確保僅返回組。 此外，請確定您指定網域名稱。

**建立群組**

確定組不存在於域中後，請建立組並指定以下屬性：

* **CommonName**:群組的名稱。
* **網域**:新增群組的網域。
* **說明**:群組的說明。

**對組執行操作**

建立群組後，您可以使用群組執行動作。 例如，您可以新增使用者至群組。 若要將使用者新增至群組，請擷取使用者和群組的唯一識別碼值。 將這些值傳遞至 `addPrincipalToLocalGroup` 方法。

**另請參閱**

[使用Java API建立群組](users.md#create-groups-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增使用者](users.md#adding-users)

[刪除用戶](users.md#deleting-users)

### 使用Java API建立群組 {#create-groups-using-the-java-api}

使用目錄管理器服務API(Java)建立組：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   使用其 `DirectoryManagerServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 確定組是否存在。

   * 使用其 `PrincipalSearchFilter` 建構函式建立物件。
   * 通過調用對象的對象來 `PrincipalSearchFilter` 設定主體類 `setPrincipalType` 型。 傳遞值 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`。
   * 調用物件的物 `PrincipalSearchFilter` 件來設定 `setSpecificDomainName` 網域。 傳遞指定網域名稱的字串值。
   * 若要尋找群組，請叫 `DirectoryManagerServiceClient` 用物件的 `findPrincipals` 方法（承擔者可以是群組）。 傳遞指 `PrincipalSearchFilter` 定主類型和域名的對象。 此方法會傳回 `java.util.List` 每個元素都是例項的例 `Group` 項。 每個群組例項都符合使用物件所指定的篩 `PrincipalSearchFilter` 選器。
   * 重複執行 `java.util.List` 個體。 對於每個元素，檢索組名。 請確定群組名稱不等於新群組名稱。

1. 建立群組。

   * 如果群組不存在，請叫用物 `Group` 件的方 `setCommonName` 法並傳遞指定群組名稱的字串值。
   * 叫用物 `Group` 件的方 `setDescription` 法，並傳遞指定群組說明的字串值。
   * 叫用物 `Group` 件的方 `setDomainName` 法並傳遞指定網域名稱的字串值。
   * 叫用物 `DirectoryManagerServiceClient` 件的方 `createLocalGroup` 法並傳遞例 `Group` 項。
   該方 `createLocalUser` 法返回一個字串值，它指定本地用戶標識符值。

1. 對組執行操作。

   * 使用其 `PrincipalSearchFilter` 建構函式建立物件。
   * 調用物件的方法，以設 `PrincipalSearchFilter` 定使用者識別 `setUserId` 碼值。 傳遞代表使用者識別碼值的字串值。
   * 叫用物 `DirectoryManagerServiceClient` 件的方 `findPrincipals` 法並傳遞物 `PrincipalSearchFilter` 件。 此方法傳回 `java.util.List` 例項，其中每個元素都是物 `User` 件。 重複執行個 `java.util.List` 體以找出使用者。
   * 叫用物件的方法，將使用者 `DirectoryManagerServiceClient` 新增至群 `addPrincipalToLocalGroup` 組。 傳遞物件方法 `User` 的傳回 `getOid` 值。 傳遞物件方法 `Group` 的傳回值 `getOid` (使用 `Group` 代表新群組的例項)。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Managing Users and Groups {#managing-users-and-groups}

本主題說明如何使用(Java)以程式設計方式指派、移除和查詢網域、使用者和群組。

>[!NOTE]
>
>在設定網域時，您必須為群組和使用者設定唯一識別碼。 所選的屬性不僅在LDAP環境中是唯一的，而且必須是不可變的，不會在目錄中更改。 此屬性也必須是簡單的字串資料類型(Active Directory 2000/2003當前允許的唯一例外是 `"objectsid"`二進位值)。 例如，Novell eDirectory屬 `"GUID"`性不是簡單的字串資料類型，因此不起作用。

* 對於Active Directory，請使用 `"objectsid"`。
* 對於SunOne，請使用 `"nsuniqueid"`。

>[!NOTE]
>
>不支援在LDAP目錄同步進行時建立多個本地用戶和組。 嘗試此程式可能會導致錯誤。

### 步驟摘要 {#summary_of_steps-3}

要管理用戶和組，請執行以下步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService客戶端。
1. 叫用適當的使用者或群組作業。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務操作之前，必須建立目錄管理器服務客戶端。 使用Java API，這是透過建立物件來 `DirectoryManagerServiceClient` 完成。 使用web service API，這是透過建立物件來 `DirectoryManagerServiceService` 完成。

**叫用適當的使用者或群組作業**

建立服務客戶端後，可以調用用戶或組管理操作。 服務客戶端允許您分配、刪除和查詢域、用戶和組。 請注意，可以將目錄承擔者或本地承擔者添加到本地組，但無法將本地承擔者添加到目錄組。

**另請參閱**

[使用Java API管理使用者和群組](users.md#managing-users-and-groups-using-the-java-api)

[使用web service API管理使用者和群組](users.md#managing-users-and-groups-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理使用者和群組 {#managing-users-and-groups-using-the-java-api}

若要使用(Java)以程式設計方式管理使用者、群組和網域，請執行下列工作：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。 如需這些檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 建立DirectoryManagerService客戶端。

   使用其 `DirectoryManagerServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。 有關資訊，請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*。*

1. 叫用適當的使用者或群組作業。

   要查找用戶或組，請調用對象的其中一 `DirectoryManagerServiceClient` 種查找承擔者的方法（因為承擔者可以是用戶或組）。 在下例中，使用 `findPrincipals` 搜尋篩選器（物件）來呼叫 `PrincipalSearchFilter` 方法。

   由於此情況下的返回值是包含 `java.util.List` 對象 `Principal` 的，因此對結果進行迭代，並將對象 `Principal` 轉換為 `User` 或對 `Group` 像。

   使用結果 `User` 或對 `Group` 像（兩者都繼承自介面）, `Principal` 檢索工作流中需要的資訊。 例如，域名和標準名稱值組合在一起可唯一地標識承擔者。 這些是分別呼叫物 `Principal` 件和方法 `getDomainName` 來擷 `getCanonicalName` 取的。

   若要刪除本機使用者，請叫 `DirectoryManagerServiceClient` 用物件的方 `deleteLocalUser` 法並傳遞使用者的識別碼。

   若要刪除本機群組，請叫 `DirectoryManagerServiceClient` 用物件的方 `deleteLocalGroup` 法並傳遞群組的識別碼。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API管理使用者和群組 {#managing-users-and-groups-using-the-web-service-api}

要使用目錄管理器服務API(web service)以寫程式方式管理用戶、組和域，請執行以下任務：

1. 包含專案檔案。

   * 建立一個使用目錄管理器WSDL的Microsoft .NET客戶端元件。 (請參 [閱使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding))。
   * 參考Microsoft .NET客戶端元件。 (請參 [閱建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。)

1. 建立DirectoryManagerService客戶端。

   使用 `DirectoryManagerServiceService` proxy類別的建構函式建立物件。

1. 叫用適當的使用者或群組作業。

   要查找用戶或組，請調用對象的其中一 `DirectoryManagerServiceService` 種查找承擔者的方法（因為承擔者可以是用戶或組）。 在下例中，使用 `findPrincipalsWithFilter` 搜尋篩選器（物件）來呼叫 `PrincipalSearchFilter` 方法。 使用對象時， `PrincipalSearchFilter` 僅在將屬性設定為時才返回本 `isLocal` 地承擔者 `true`。 此行為與Java API的行為不同。

   >[!NOTE]
   >
   >如果未在搜尋篩選器中（透過欄位）指定最 `PrincipalSearchFilter.resultsMax` 大結果數，則最多會傳回1000個結果。 這與使用Java API（預設上限為10個結果）時的行為不同。 此外，搜尋方法( `findGroupMembers` 例如，透過欄位)不會產生任何結果，除非在搜尋篩選中指定最大結果 `GroupMembershipSearchFilter.resultsMax` 數。 這會套用至繼承自類別的所有搜尋篩 `GenericSearchFilter` 選器。 如需詳細資訊，請參 [閱「AEM Forms API參考」](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

   由於此情況下的返回值是包含 `object[]` 對象 `Principal` 的，因此可循環處理結果並將對象 `Principal` 轉換為 `User` 或對 `Group` 像。

   使用結果 `User` 或對 `Group` 像（兩者都繼承自介面）, `Principal` 檢索工作流中需要的資訊。 例如，域名和標準名稱值組合在一起可唯一地標識承擔者。 這些項目會分 `Principal` 別呼叫物件 `domainName` 和 `canonicalName` 欄位來擷取。

   若要刪除本機使用者，請叫 `DirectoryManagerServiceService` 用物件的方 `deleteLocalUser` 法並傳遞使用者的識別碼。

   若要刪除本機群組，請叫 `DirectoryManagerServiceService` 用物件的方 `deleteLocalGroup` 法並傳遞群組的識別碼。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 管理角色和權限 {#managing-roles-and-permissions}

本主題說明如何使用授權管理器服務API(Java)以程式設計方式指派、移除及決定角色和權限。

在AEM Forms中，角 *色是存取一* 或多個系統層級資源的權限群組。 這些權限是透過「使用者管理」建立，並由服務元件強制執行。 例如，管理員可以將「策略集作者」的角色指派給一組用戶。 然後，Rights Management會允許具有該角色的群組使用者透過管理控制台建立原則集。

角色有兩種類型：預 *設角色**和自訂角色*。 預設角色(*系統角色)* 已駐留在AEM Forms中。 假定管理員不能刪除或修改預設角色，因此不可變。 因此，管理員建立的自定義角色可以變更，管理員隨後可以修改或刪除這些角色。

角色可讓管理權限更輕鬆。 將角色分配給承擔者時，會自動將一組權限分配給承擔者，並且承擔者的所有特定訪問相關決策都基於該總指派的權限集。

### 步驟摘要 {#summary_of_steps-4}

要管理角色和權限，請執行以下步驟：

1. 包含專案檔案。
1. 建立AuthorizationManagerService客戶端。
1. 調用適當的角色或權限操作。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立AuthorizationManagerService客戶端**

在以寫程式方式執行User Management AuthorizationManagerService操作之前，必須建立AuthorizationManagerService客戶端。 使用Java API，這是透過建立物件來 `AuthorizationManagerServiceClient` 完成。

**調用適當的角色或權限操作**

建立服務客戶端後，可以調用角色或權限操作。 服務客戶端允許您分配、刪除和確定角色和權限。

**另請參閱**

[使用Java API管理角色和權限](users.md#managing-roles-and-permissions-using-the-java-api)

[使用web service API管理角色和權限](users.md#managing-roles-and-permissions-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理角色和權限 {#managing-roles-and-permissions-using-the-java-api}

要使用Authorization Manager Service API(Java)管理角色和權限，請執行以下任務：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立AuthorizationManagerService客戶端。

   使用其 `AuthorizationManagerServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 調用適當的角色或權限操作。

   要為承擔者指派角色，請調用對 `AuthorizationManagerServiceClient` 像的方 `assignRole` 法並傳遞以下值：

   * 包 `java.lang.String` 含角色標識符的對象
   * 包含主標識符 `java.lang.String` 的對象陣列。
   要從承擔者中刪除角色，請調 `AuthorizationManagerServiceClient` 用對象的方 `unassignRole` 法並傳遞以下值：

   * 包含 `java.lang.String` 角色標識符的對象。
   * 包含主標識符 `java.lang.String` 的對象陣列。


**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API管理角色和權限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API管理角色和權限 {#managing-roles-and-permissions-using-the-web-service-api}

使用Authorization Manager Service API(web service)管理角色和權限：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立AuthorizationManagerService客戶端。

   * 使用其 `AuthorizationManagerServiceClient` 預設建構函式建立物件。
   * 使用建 `AuthorizationManagerServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `AuthorizationManagerServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 調用適當的角色或權限操作。

   要為承擔者指派角色，請調用對 `AuthorizationManagerServiceClient` 像的方 `assignRole` 法並傳遞以下值：

   * 包 `string` 含角色標識符的對象
   * 包 `MyArrayOf_xsd_string` 含主標識符的對象。
   要從承擔者中刪除角色，請調 `AuthorizationManagerServiceService` 用對象的方 `unassignRole` 法並傳遞以下值：

   * 包含 `string` 角色標識符的對象。
   * 包含主標識符 `string` 的對象陣列。


**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 驗證使用者 {#authenticating-users}

本主題說明如何使用Authentication Manager Service API(Java)，讓用戶端應用程式以程式設計方式驗證使用者。

用戶驗證可能需要與儲存安全資料的企業資料庫或其他企業儲存庫交互。

例如，假設使用者在網頁中輸入使用者名稱和密碼，並將值提交至代管表單的J2EE應用程式伺服器。 Forms自訂應用程式可以使用Authentication Manager服務來驗證使用者。

如果驗證成功，應用程式將訪問受保護的企業資料庫。 否則，會傳送訊息給使用者，指出使用者並非授權使用者。

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
   <td><p>用戶訪問網站並指定用戶名和口令。 這項資訊會提交至代管AEM Forms的J2EE應用程式伺服器。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>用戶憑證通過Authentication Manager服務進行驗證。 如果用戶憑據有效，工作流將繼續執行步驟3。 否則，會傳送訊息給使用者，指出使用者並非授權使用者。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>從安全企業資料庫檢索用戶資訊和表單設計。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>使用者資訊會與表單設計合併，表單會轉譯給使用者。 </p></td>
  </tr>
 </tbody>
</table>

### 步驟摘要 {#summary_of_steps-5}

若要以程式設計方式驗證使用者，請執行下列步驟：

1. 包含專案檔案。
1. 建立AuthenticationManagerService客戶端。
1. 叫用驗證操作。
1. 如有必要，請擷取內容，讓用戶端應用程式可將它轉送至其他AEM Forms服務進行驗證。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立AuthenticationManagerService客戶端**

您必須先建立AuthenticationManagerService用戶端，才能以程式設計方式驗證使用者。 使用Java API時，請建立物 `AuthenticationManagerServiceClient` 件。

**叫用驗證操作**

建立服務客戶端後，可以調用驗證操作。 此操作將需要有關使用者的資訊，例如使用者的名稱和密碼。 如果用戶未驗證，則會拋出異常。

**擷取驗證內容**

一旦您驗證了使用者，就可以在已驗證的使用者中建立內容。 然後，您可以使用內容叫用其他AEM Forms服務。 例如，您可以使用內容來建立PDF文 `EncryptionServiceClient` 件並加密使用密碼的檔案。 請確定已驗證的使用者具有名 `Services User` 稱為呼叫AEM Forms服務所需的角色。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密碼加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API驗證使用者 {#authenticate-a-user-using-the-java-api}

使用Authentication Manager Service API(Java)驗證使用者：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立AuthenticationManagerServices客戶端。

   使用其 `AuthenticationManagerServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 叫用驗證操作。

   叫用物 `AuthenticationManagerServiceClient` 件的方 `authenticate` 法並傳遞下列值：

   * 包 `java.lang.String` 含使用者名稱的物件。
   * 包含使用者密 `byte[]` 碼的位元組陣列（物件）。 您可以叫用 `byte[]` 物件的方法 `java.lang.String` 來取得物 `getBytes` 件。
   驗證方法返回包 `AuthResult` 含關於已驗證用戶的資訊的對象。

1. 擷取驗證內容。

   叫用 `ServiceClientFactory` 物件的方 `getContext` 法，以傳回物 `Context` 件。

   然後叫用 `Context` 物件的方 `initPrincipal` 法並傳遞 `AuthResult`。

### 使用web service API驗證使用者 {#authenticate-a-user-using-the-web-service-api}

使用Authentication Manager Service API(web service)驗證用戶：

1. 包含專案檔案。

   * 建立使用驗證管理器WSDL的Microsoft .NET客戶端元件。 (請參 [閱使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding))。
   * 參考Microsoft .NET客戶端元件。 (請參閱使用Base64編碼叫用AEM Forms中的「參 [照。NET用戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)」)。

1. 建立AuthenticationManagerService客戶端。

   使用 `AuthenticationManagerServiceService` proxy類別的建構函式建立物件。

1. 叫用驗證操作。

   叫用物 `AuthenticationManagerServiceClient` 件的方 `authenticate` 法並傳遞下列值：

   * 包 `string` 含使用者名稱的物件
   * 包含使用者密 `byte[]` 碼的位元組陣列（物件）。 您可以使用 `byte[]` 下例中顯示的邏 `string` 輯，將包含口令的對象轉換為 `byte[]` 陣列，以獲得該對象。
   * 傳回的值將是物 `AuthResult` 件，可用來擷取使用者的相關資訊。 在下列範例中，使用者的資訊會先取得物件的欄位， `AuthResult` 然 `authenticatedUser` 後再取得結果物 `User` 件的欄位 `canonicalName` 和 `domainName` 欄位。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 以程式設計方式同步使用者 {#programmatically-synchronizing-users}

您可以使用「使用者管理API」，以程式設計方式同步使用者。 當您同步使用者時，您會使用位於使用者儲存庫中的使用者資料來更新AEM Forms。 例如，假設您向用戶儲存庫添加新用戶。 在您執行同步作業後，新使用者會變成AEM表單使用者。 此外，您的使用者儲存庫中不再有的使用者也會從AEM Forms中移除。

下圖顯示與使用者儲存庫同步的AEM Forms。

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
   <td><p>用戶端應用程式會要求AEM Forms執行同步作業。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Forms會執行同步作業。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者資訊已更新。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>用戶可以查看更新的用戶資訊。 </p></td>
  </tr>
 </tbody>
</table>

### 步驟摘要 {#summary_of_steps-6}

若要以程式設計方式同步使用者，請執行下列步驟：

1. 包含專案檔案。
1. 建立UserManagerUtilServiceClient客戶端。
1. 指定企業網域。
1. 叫用驗證操作。
1. 確定同步操作是否完成

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立UserManagerUtilServiceClientclient**

您必須先建立物件，才能以程式設計方式同步使 `UserManagerUtilServiceClient` 用者。

**指定企業網域**

在使用用戶管理API執行同步操作之前，您應指定用戶所屬的企業域。 您可以指定一或多個企業網域。 在以寫程式方式執行同步操作之前，必須使用管理控制台設定企業域。 (請參閱 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_63)。)

**調用同步操作**

指定一個或多個企業域後，可以執行同步操作。 執行此操作所花費的時間取決於用戶儲存庫中的用戶記錄數。

**確定同步操作是否完成**

在以寫程式方式執行同步操作後，可以確定操作是否完成。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密碼加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API以程式設計方式同步使用者 {#programmatically-synchronizing-users-using-the-java-api}

使用使用者管理API(Java)來同步使用者：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar和adobe-usermanager-util-client.jar。

1. 建立UserManagerUtilServiceClient客戶端。

   使用其 `UserManagerUtilServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 指定企業網域。

   * 叫用 `UserManagerUtilServiceClient` 物件的方 `scheduleSynchronization` 法以啟動使用者同步作業。
   * 使用建 `java.util.Set` 構函式建立例 `HashSet` 項。 請確定您指定 `String` 為資料類型。 此實 `Java.util.Set` 例儲存應用同步操作的域名。
   * 對於要添加的每個域名，請調 `java.util.Set` 用對象的添加方法並傳遞域名。

1. 調用同步操作。

   叫用 `ServiceClientFactory` 物件的方 `getContext` 法，以傳回物 `Context` 件。

   然後叫用 `Context` 物件的方 `initPrincipal` 法並傳遞 `AuthResult`。

**另請參閱**

[以程式設計方式同步使用者](users.md#programmatically-synchronizing-users)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
