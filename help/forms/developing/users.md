---
title: 管理用戶
seo-title: Managing Users
description: 使用用戶管理API建立可管理角色、權限和承擔者（可以是用戶或組）以及驗證用戶的客戶端應用程式。
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

# 管理用戶 {#managing-users}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於用戶管理**

您可以使用用戶管理API建立客戶端應用程式，這些應用程式可以管理角色、權限和承擔者（可以是用戶或組），並驗證用戶。 用戶管理API由以下AEM FormsAPI組成：

* 目錄管理器服務API
* 驗證管理器服務API
* 授權管理器服務API

用戶管理使您能夠分配、刪除和確定角色和權限。 它還允許您分配、刪除和查詢域、用戶和組。 最後，您可以使用用戶管理來驗證用戶。

在 [添加用戶](users.md#adding-users) 您將瞭解如何以寫程式方式添加用戶。 本節使用目錄管理器服務API。

在 [刪除用戶](users.md#deleting-users) 您將瞭解如何以寫程式方式刪除用戶。 本節使用目錄管理器服務API。

在 [管理用戶和組](users.md#managing-users-and-groups) 您將瞭解本地用戶和目錄用戶之間的區別，並查看如何使用Java和Web服務API以寫程式方式管理用戶和組的示例。 本節使用目錄管理器服務API。

在 [管理角色和權限](users.md#managing-roles-and-permissions) 您將瞭解系統角色和權限，以及可以通過寫程式方式來補充這些角色和權限的方法，並查看如何使用Java和Web服務API以寫程式方式管理角色和權限的示例。 本節同時使用目錄管理器服務API和授權管理器服務API。

在 [驗證用戶](users.md#authenticating-users) 您將看到如何使用Java和Web服務API以寫程式方式驗證用戶的示例。 本節使用授權管理器服務API。

**瞭解身份驗證過程**

用戶管理提供了內置的身份驗證功能，還讓您能夠將其與自己的身份驗證提供程式連接。 當用戶管理收到驗證請求（例如，用戶嘗試登錄）時，它會將用戶資訊傳遞給驗證提供方進行驗證。 用戶管理在驗證用戶後從驗證提供程式接收結果。

下圖顯示了嘗試登錄的最終用戶、用戶管理和身份驗證提供程式之間的交互。

![mu_mu_umauth進程](assets/mu_mu_umauth_process.png)

下表說明了驗證過程的每個步驟。

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
   <td><p>用戶嘗試登錄到調用用戶管理的服務。 用戶指定用戶名和密碼。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>用戶管理將用戶名和密碼以及配置資訊發送到驗證提供程式。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>驗證提供器連接到用戶儲存並驗證用戶。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>驗證提供程式將結果返回給用戶管理。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>用戶管理允許用戶登錄或拒絕對產品的訪問。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果伺服器時區與客戶端時區不同，當在WebSphere應用程式伺服器群集上使用.NET客戶端在本機SOAP堆棧上使用AEM Forms生成PDF服務的WSDL時，可能會出現以下用戶管理驗證錯誤：

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**瞭解目錄管理**

用戶管理與支援到LDAP目錄的連接的目錄服務提供程式(DirectoryManagerService)打包在一起。 如果您的組織使用非LDAP儲存庫儲存用戶記錄，則可以建立與儲存庫一起使用的您自己的目錄服務提供程式。

目錄服務提供方應用戶管理的請求從用戶儲存中檢索記錄。 用戶管理會定期在資料庫中快取用戶和組記錄以提高效能。

目錄服務提供程式可用於將用戶管理資料庫與用戶儲存同步。 此步驟確保所有用戶目錄資訊以及所有用戶和組記錄都是最新的。

此外， DirectoryManagerService還使您能夠建立和管理域。 域定義不同的用戶基。 域的邊界通常根據組織的結構方式或用戶儲存的設定來定義。 用戶管理域提供身份驗證提供程式和目錄服務提供程式使用的配置設定。

在用戶管理導出的配置XML中，屬性值為 `Domains` 包含為用戶管理定義的每個域的XML元素。 這些元素中的每一個都包含定義與特定服務提供商相關聯的域的各個方面的其他元素。

**瞭解objectSID值**

使用Active Directory時，必須瞭解 `objectSID` 值不是跨多個域的唯一屬性。 此值儲存對象的安全標識符。 在多域環境中（例如，域樹）, `objectSID` 值可以不同。

安 `objectSID` 如果將對象從一個Active Directory域移動到另一個域，則值將更改。 某些對象具有相同 `objectSID` 域中任何位置的值。 例如，BUILTIN\Administrators、BUILTIN\Power Users等組將具有相同的 `objectSID` 無論域如何。 這些 `objectSID` 值是眾所周知的。

## 添加用戶 {#adding-users}

可以使用目錄管理器服務API（Java和Web服務）以寫程式方式將用戶添加到AEM Forms。 添加用戶後，在執行需要用戶的服務操作時可以使用該用戶。 例如，您可以將任務分配給新用戶。

### 步驟摘要 {#summary-of-steps}

要添加用戶，請執行以下步驟：

1. 包括項目檔案。
1. 建立DirectoryManagerService客戶端。
1. 定義用戶資訊。
1. 將用戶添加到AEM Forms。
1. 驗證是否已添加用戶。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務操作之前，請建立目錄管理器服務API客戶端。

**定義用戶資訊**

使用目錄管理器服務API添加新用戶時，請定義該用戶的資訊。 通常，在添加新用戶時，您會定義以下值：

* **域名**:用戶所屬的域(例如， `DefaultDom`)。
* **用戶標識符值**:用戶的標識符值(例如， `wblue`)。
* **主體類型**:用戶類型(例如，可以指定 `USER)`。
* **給定名稱**:用戶的指定名稱(例如， `Wendy`)。
* **姓氏**:用戶的族名(例如， `Blue)`。
* **區域設定**:用戶的區域設定資訊。

**將用戶添加到AEM Forms**

定義用戶資訊後，可將用戶添加到AEM Forms。 要添加用戶，請調用 `DirectoryManagerServiceClient` 對象 `createLocalUser` 的雙曲餘切值。

**驗證是否已添加用戶**

您可以驗證是否添加了用戶以確保未出現任何問題。 使用用戶標識符值查找新用戶。

**另請參閱**

[使用Java API添加用戶](users.md#add-users-using-the-java-api)

[使用Web服務API添加用戶](users.md#add-users-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[刪除用戶](users.md#deleting-users)

### 使用Java API添加用戶 {#add-users-using-the-java-api}

使用目錄管理器服務API(Java)添加用戶：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-usermanager-client.jar。

1. 建立DirectoryManagerServices客戶端。

   建立 `DirectoryManagerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 定義用戶資訊。

   * 建立 `UserImpl` 對象。
   * 通過調用 `UserImpl` 對象 `setDomainName` 的雙曲餘切值。 傳遞指定域名的字串值。
   * 通過調用 `UserImpl` 對象 `setPrincipalType` 的雙曲餘切值。 傳遞指定用戶類型的字串值。 例如，可以指定 `USER`。
   * 通過調用 `UserImpl` 對象 `setUserid` 的雙曲餘切值。 傳遞指定用戶標識符值的字串值。 例如，可以指定 `wblue`。
   * 通過調用 `UserImpl` 對象 `setCanonicalName` 的雙曲餘切值。 傳遞一個指定用戶規範名稱的字串值。 例如，可以指定 `wblue`。
   * 通過調用 `UserImpl` 對象 `setGivenName` 的雙曲餘切值。 傳遞一個字串值，該值指定用戶的指定名稱。 例如，可以指定 `Wendy`。
   * 通過調用 `UserImpl` 對象 `setFamilyName` 的雙曲餘切值。 傳遞一個指定用戶族名的字串值。 例如，可以指定 `Blue`。

   >[!NOTE]
   >
   >調用屬於 `UserImpl` 對象以設定其他值。 例如，可以通過調用 `UserImpl` 對象 `setLocale` 的雙曲餘切值。

1. 將用戶添加到AEM Forms。

   調用 `DirectoryManagerServiceClient` 對象 `createLocalUser` 方法並傳遞以下值：

   * 的 `UserImpl` 表示新用戶的對象
   * 表示用戶密碼的字串值

   的 `createLocalUser` 方法返回指定本地用戶標識符值的字串值。

1. 驗證是否已添加用戶。

   * 建立 `PrincipalSearchFilter` 對象。
   * 通過調用 `PrincipalSearchFilter` 對象 `setUserId` 的雙曲餘切值。 傳遞表示用戶標識符值的字串值。
   * 調用 `DirectoryManagerServiceClient` 對象 `findPrincipals` 方法和通過 `PrincipalSearchFilter` 的雙曲餘切值。 此方法返回 `java.util.List` 實例，其中每個元素都是 `User` 的雙曲餘切值。 迭代 `java.util.List` 實例以查找用戶。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API添加用戶](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API添加用戶 {#add-users-using-the-web-service-api}

使用目錄管理器服務API（Web服務）添加用戶：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保將以下WSDL定義用於服務引用： `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立DirectoryManagerService客戶端。

   * 建立 `DirectoryManagerServiceClient` 對象。
   * 建立 `DirectoryManagerServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 確保指定 `?blob=mtom`。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `DirectoryManagerServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 定義用戶資訊。

   * 建立 `UserImpl` 對象。
   * 通過將字串值分配給 `UserImpl` 對象 `domainName` 的子菜單。
   * 通過將字串值分配給 `UserImpl` 對象 `principalType` 的子菜單。 例如，可以指定 `USER`。
   * 通過將字串值分配給 `UserImpl` 對象 `userid` 的子菜單。
   * 通過將字串值分配給 `UserImpl` 對象 `canonicalName` 的子菜單。
   * 通過將字串值分配給 `UserImpl` 對象 `givenName` 的子菜單。
   * 通過為 `UserImpl` 對象 `familyName` 的子菜單。

1. 將用戶添加到AEM Forms。

   調用 `DirectoryManagerServiceClient` 對象 `createLocalUser` 方法並傳遞以下值：

   * 的 `UserImpl` 表示新用戶的對象
   * 表示用戶密碼的字串值

   的 `createLocalUser` 方法返回指定本地用戶標識符值的字串值。

1. 驗證是否已添加用戶。

   * 建立 `PrincipalSearchFilter` 對象。
   * 通過將表示用戶標識符值的字串值分配給 `PrincipalSearchFilter` 對象 `userId` 的子菜單。
   * 調用 `DirectoryManagerServiceClient` 對象 `findPrincipals` 方法和通過 `PrincipalSearchFilter` 的雙曲餘切值。 此方法返回 `MyArrayOfUser` 集合對象，其中每個元素都是 `User` 的雙曲餘切值。 迭代 `MyArrayOfUser` 以查找用戶。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除用戶 {#deleting-users}

可以使用目錄管理器服務API（Java和Web服務）以寫程式方式從AEM Forms刪除用戶。 刪除用戶後，用戶將不能再用於執行需要用戶的服務操作。 例如，不能將任務分配給已刪除的用戶。

### 步驟摘要 {#summary_of_steps-1}

要刪除用戶，請執行以下步驟：

1. 包括項目檔案。
1. 建立DirectoryManagerService客戶端。
1. 指定要刪除的用戶。
1. 從AEM Forms刪除用戶。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務API操作之前，請建立目錄管理器服務客戶端。

**指定要刪除的用戶**

可以使用用戶的標識符值指定要刪除的用戶。

**從AEM Forms刪除用戶**

要刪除用戶，請調用 `DirectoryManagerServiceClient` 對象 `deleteLocalUser` 的雙曲餘切值。

**另請參閱**

[使用Java API刪除用戶](users.md#delete-users-using-the-java-api)

[使用Web服務API刪除用戶](users.md#delete-users-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加用戶](users.md#adding-users)

### 使用Java API刪除用戶 {#delete-users-using-the-java-api}

使用目錄管理器服務API(Java)刪除用戶：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   建立 `DirectoryManagerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要刪除的用戶。

   * 建立 `PrincipalSearchFilter` 對象。
   * 通過調用 `PrincipalSearchFilter` 對象 `setUserId` 的雙曲餘切值。 傳遞表示用戶標識符值的字串值。
   * 調用 `DirectoryManagerServiceClient` 對象 `findPrincipals` 方法和通過 `PrincipalSearchFilter` 的雙曲餘切值。 此方法返回 `java.util.List` 實例，其中每個元素都是 `User` 的雙曲餘切值。 迭代 `java.util.List` 實例以查找要刪除的用戶。

1. 從AEM Forms刪除用戶。

   調用 `DirectoryManagerServiceClient` 對象 `deleteLocalUser` 方法並傳遞 `User` 對象 `oid` 的子菜單。 調用 `User` 對象 `getOid` 的雙曲餘切值。 使用 `User` 從 `java.util.List` 實例。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API刪除用戶](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[快速啟動（SOAP模式）:使用Java API刪除用戶](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API刪除用戶 {#delete-users-using-the-web-service-api}

使用目錄管理器服務API（Web服務）刪除用戶：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   * 建立 `DirectoryManagerServiceClient` 對象。
   * 建立 `DirectoryManagerServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 確保指定 `blob=mtom.`
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `DirectoryManagerServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 指定要刪除的用戶。

   * 建立 `PrincipalSearchFilter` 對象。
   * 通過將字串值分配給 `PrincipalSearchFilter` 對象 `userId` 的子菜單。
   * 調用 `DirectoryManagerServiceClient` 對象 `findPrincipals` 方法和通過 `PrincipalSearchFilter` 的雙曲餘切值。 此方法返回 `MyArrayOfUser` 集合對象，其中每個元素都是 `User` 的雙曲餘切值。 迭代 `MyArrayOfUser` 以查找用戶。 的 `User` 從 `MyArrayOfUser` 集合對象用於刪除用戶。

1. 從AEM Forms刪除用戶。

   通過傳遞 `User` 對象 `oid` 欄位值 `DirectoryManagerServiceClient` 對象 `deleteLocalUser` 的雙曲餘切值。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立組 {#creating-groups}

可以使用目錄管理器服務API（Java和Web服務）以寫程式方式建立AEM Forms組。 建立組後，可使用該組執行需要組的服務操作。 例如，可以將用戶分配給新組。 (請參閱 [管理用戶和組](users.md#managing-users-and-groups)。)

### 步驟摘要 {#summary_of_steps-2}

要建立組，請執行以下步驟：

1. 包括項目檔案。
1. 建立DirectoryManagerService客戶端。
1. 確定組不存在。
1. 建立組。
1. 對組執行操作。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務操作之前，請建立目錄管理器服務API客戶端。

**確定組是否存在**

建立組時，請確保組不存在於同一域中。 也就是說，兩個組不能在同一域中具有相同的名稱。 要執行此任務，請執行搜索並根據兩個值篩選搜索結果。 將承擔者類型設定為 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` 確保僅返回組。 另外，請確保指定域名。

**建立組**

確定域中不存在組後，請建立組並指定以下屬性：

* **公用名**:組的名稱。
* **域**:添加組的域。
* **說明**:組的說明。

**對組執行操作**

建立組後，可以使用該組執行操作。 例如，可以向組中添加用戶。 要向組添加用戶，請檢索用戶和組的唯一標識符值。 將這些值傳遞給 `addPrincipalToLocalGroup` 的雙曲餘切值。

**另請參閱**

[使用Java API建立組](users.md#create-groups-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加用戶](users.md#adding-users)

[刪除用戶](users.md#deleting-users)

### 使用Java API建立組 {#create-groups-using-the-java-api}

使用目錄管理器服務API(Java)建立組：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   建立 `DirectoryManagerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 確定組是否存在。

   * 建立 `PrincipalSearchFilter` 對象。
   * 通過調用 `PrincipalSearchFilter` 對象 `setPrincipalType` 的雙曲餘切值。 傳遞值 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`。
   * 通過調用 `PrincipalSearchFilter` 對象 `setSpecificDomainName` 的雙曲餘切值。 傳遞指定域名的字串值。
   * 要查找組，請調用 `DirectoryManagerServiceClient` 對象 `findPrincipals` 方法（主體可以是組）。 通過 `PrincipalSearchFilter` 指定主體類型和域名的對象。 此方法返回 `java.util.List` 實例，其中每個元素都是 `Group` 實例。 每個組實例都符合使用 `PrincipalSearchFilter` 的雙曲餘切值。
   * 迭代 `java.util.List` 實例。 對於每個元素，檢索組名稱。 確保組名不等於新組名。

1. 建立組。

   * 如果組不存在，請調用 `Group` 對象 `setCommonName` 方法並傳遞一個指定組名的字串值。
   * 調用 `Group` 對象 `setDescription` 方法，並傳遞一個指定組說明的字串值。
   * 調用 `Group` 對象 `setDomainName` 方法並傳遞一個指定域名的字串值。
   * 調用 `DirectoryManagerServiceClient` 對象 `createLocalGroup` 方法和通過 `Group` 實例。

   的 `createLocalUser` 方法返回指定本地用戶標識符值的字串值。

1. 對組執行操作。

   * 建立 `PrincipalSearchFilter` 對象。
   * 通過調用 `PrincipalSearchFilter` 對象 `setUserId` 的雙曲餘切值。 傳遞表示用戶標識符值的字串值。
   * 調用 `DirectoryManagerServiceClient` 對象 `findPrincipals` 方法和通過 `PrincipalSearchFilter` 的雙曲餘切值。 此方法返回 `java.util.List` 實例，其中每個元素都是 `User` 的雙曲餘切值。 迭代 `java.util.List` 實例以查找用戶。
   * 通過調用 `DirectoryManagerServiceClient` 對象 `addPrincipalToLocalGroup` 的雙曲餘切值。 傳遞的返回值 `User` 對象 `getOid` 的雙曲餘切值。 傳遞的返回值 `Group` 對象 `getOid` 方法(使用 `Group` 表示新組的實例)。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 管理用戶和組 {#managing-users-and-groups}

本主題介紹如何使用(Java)以寫程式方式分配、刪除和查詢域、用戶和組。

>[!NOTE]
>
>配置域時，必須為組和用戶設定唯一標識符。 所選屬性不僅必須在LDAP環境中是唯一的，而且必須是不可變的，不會在目錄中更改。 此屬性還必須是簡單的字串資料類型(Active Directory 2000/2003當前允許的唯一例外是 `"objectsid"`，即二進位值)。 Novell eDirectory屬性 `"GUID"`例如，不是簡單的字串資料類型，因此無法工作。

* 對於Active Directory，使用 `"objectsid"`。
* 對於SunOne，使用 `"nsuniqueid"`。

>[!NOTE]
>
>不支援在LDAP目錄同步進行時建立多個本地用戶和組。 嘗試此進程可能會導致錯誤。

### 步驟摘要 {#summary_of_steps-3}

要管理用戶和組，請執行以下步驟：

1. 包括項目檔案。
1. 建立DirectoryManagerService客戶端。
1. 調用相應的用戶或組操作。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務操作之前，必須建立目錄管理器服務客戶端。 使用Java API，可通過建立 `DirectoryManagerServiceClient` 的雙曲餘切值。 使用Web服務API，可通過建立 `DirectoryManagerServiceService` 的雙曲餘切值。

**調用相應的用戶或組操作**

建立服務客戶端後，可以調用用戶或組管理操作。 服務客戶端允許您分配、刪除和查詢域、用戶和組。 請注意，可以將目錄主體或本地主體添加到本地組，但無法將本地主體添加到目錄組。

**另請參閱**

[使用Java API管理用戶和組](users.md#managing-users-and-groups-using-the-java-api)

[使用Web服務API管理用戶和組](users.md#managing-users-and-groups-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用戶管理器API快速啟動](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理用戶和組 {#managing-users-and-groups-using-the-java-api}

要使用(Java)以寫程式方式管理用戶、組和域，請執行以下任務：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-usermanager-client.jar。 有關這些檔案位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 建立DirectoryManagerService客戶端。

   建立 `DirectoryManagerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。 有關資訊，請參見 [設定連接屬性&#x200B;](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*。*

1. 調用相應的用戶或組操作。

   要查找用戶或組，請調用 `DirectoryManagerServiceClient` 對象查找承擔者的方法（因為承擔者可以是用戶或組）。 在下面的示例中， `findPrincipals` 使用搜索篩選器調用方法( `PrincipalSearchFilter` 對象)。

   由於此情況下的返回值是 `java.util.List` 含 `Principal` 對象，迭代結果並強制轉換 `Principal` 對象 `User` 或 `Group` 對象。

   使用結果 `User` 或 `Group` 對象(兩者均繼承自 `Principal` 介面)，檢索工作流中需要的資訊。 例如，域名和規範名稱值組合起來，可唯一地標識主體。 通過調用 `Principal` 對象 `getDomainName` 和 `getCanonicalName` 方法。

   要刪除本地用戶，請調用 `DirectoryManagerServiceClient` 對象 `deleteLocalUser` 方法並傳遞用戶的標識符。

   要刪除本地組，請調用 `DirectoryManagerServiceClient` 對象 `deleteLocalGroup` 方法並傳遞組的標識符。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API管理用戶和組 {#managing-users-and-groups-using-the-web-service-api}

要使用目錄管理器服務API（Web服務）以寫程式方式管理用戶、組和域，請執行以下任務：

1. 包括項目檔案。

   * 建立一個使用目錄管理器WSDL的Microsoft.NET客戶端程式集。 (請參閱 [使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)
   * 引用Microsoft.NET客戶端程式集。 (請參閱 [建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。)

1. 建立DirectoryManagerService客戶端。

   建立 `DirectoryManagerServiceService` 對象。

1. 調用相應的用戶或組操作。

   要查找用戶或組，請調用 `DirectoryManagerServiceService` 對象查找承擔者的方法（因為承擔者可以是用戶或組）。 在下面的示例中， `findPrincipalsWithFilter` 使用搜索篩選器調用方法( `PrincipalSearchFilter` 對象)。 使用 `PrincipalSearchFilter` 對象，僅當 `isLocal` 屬性設定為 `true`。 此行為與Java API的行為不同。

   >[!NOTE]
   >
   >如果未在搜索篩選器中指定最大結果數(通過 `PrincipalSearchFilter.resultsMax` 欄位)，最多將返回1000個結果。 這與使用Java API時的行為不同，在Java API中，預設最大值為10個結果。 另外，搜索方法如 `findGroupMembers` 除非在搜索篩選器中指定最大結果數(例如，通過 `GroupMembershipSearchFilter.resultsMax` )。 這適用於從 `GenericSearchFilter` 類。 有關詳細資訊，請參見 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

   由於此情況下的返回值是 `object[]` 含 `Principal` 對象，迭代結果並強制轉換 `Principal` 對象 `User` 或 `Group` 對象。

   使用結果 `User` 或 `Group` 對象(兩者均繼承自 `Principal` 介面)，檢索工作流中需要的資訊。 例如，域名和規範名稱值組合起來，可唯一地標識主體。 通過調用 `Principal` 對象 `domainName` 和 `canonicalName` 的下界。

   要刪除本地用戶，請調用 `DirectoryManagerServiceService` 對象 `deleteLocalUser` 方法並傳遞用戶的標識符。

   要刪除本地組，請調用 `DirectoryManagerServiceService` 對象 `deleteLocalGroup` 方法並傳遞組的標識符。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 管理角色和權限 {#managing-roles-and-permissions}

本主題介紹如何使用授權管理器服務API(Java)以寫程式方式分配、刪除和確定角色和權限。

在AEM Forms, *角色* 是一組訪問一個或多個系統級資源的權限。 這些權限是通過用戶管理建立的，並由服務元件強制執行。 例如，管理員可以將「策略集作者」角色分配給一組用戶。 然後，Rights Management將允許具有該角色的組的用戶通過管理控制台建立策略集。

有兩種角色： *預設角色* 和 *自定義角色*。 預設角色(*系統角色* 已經住在AEM Forms。 假定預設角色不能由管理員刪除或修改，因此不可變。 因此，管理員建立的自定義角色可變。

角色使管理權限更容易。 當角色被分配給承擔者時，一組權限被自動分配給該承擔者，並且承擔者的所有特定訪問相關決策都基於該總組分配的權限。

### 步驟摘要 {#summary_of_steps-4}

要管理角色和權限，請執行以下步驟：

1. 包括項目檔案。
1. 建立AuthorizationManagerService客戶端。
1. 調用相應的角色或權限操作。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立AuthorizationManagerService客戶端**

在以寫程式方式執行User Management AuthorizationManagerService操作之前，必須建立AuthorizationManagerService客戶端。 使用Java API，可通過建立 `AuthorizationManagerServiceClient` 的雙曲餘切值。

**調用適當的角色或權限操作**

建立服務客戶端後，可以調用角色或權限操作。 服務客戶端允許您分配、刪除和確定角色和權限。

**另請參閱**

[使用Java API管理角色和權限](users.md#managing-roles-and-permissions-using-the-java-api)

[使用Web服務API管理角色和權限](users.md#managing-roles-and-permissions-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用戶管理器API快速啟動](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理角色和權限 {#managing-roles-and-permissions-using-the-java-api}

要使用授權管理器服務API(Java)管理角色和權限，請執行以下任務：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-usermanager-client.jar。

1. 建立AuthorizationManagerService客戶端。

   建立 `AuthorizationManagerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用相應的角色或權限操作。

   要將角色分配給承擔者，請調用 `AuthorizationManagerServiceClient` 對象 `assignRole` 方法並傳遞以下值：

   * A `java.lang.String` 包含角色標識符的對象
   * 一組 `java.lang.String` 包含主體標識符的對象。

   要從承擔者中刪除角色，請調用 `AuthorizationManagerServiceClient` 對象 `unassignRole` 方法並傳遞以下值：

   * A `java.lang.String` 包含角色標識符的對象。
   * 一組 `java.lang.String` 包含主體標識符的對象。


**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API管理角色和權限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API管理角色和權限 {#managing-roles-and-permissions-using-the-web-service-api}

使用授權管理器服務API（Web服務）管理角色和權限：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立AuthorizationManagerService客戶端。

   * 建立 `AuthorizationManagerServiceClient` 對象。
   * 建立 `AuthorizationManagerServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `AuthorizationManagerServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 調用相應的角色或權限操作。

   要將角色分配給承擔者，請調用 `AuthorizationManagerServiceClient` 對象 `assignRole` 方法並傳遞以下值：

   * A `string` 包含角色標識符的對象
   * A `MyArrayOf_xsd_string` 包含主體標識符的對象。

   要從承擔者中刪除角色，請調用 `AuthorizationManagerServiceService` 對象 `unassignRole` 方法並傳遞以下值：

   * A `string` 包含角色標識符的對象。
   * 一組 `string` 包含主體標識符的對象。


**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 驗證用戶 {#authenticating-users}

本主題介紹如何使用Authentication Manager服務API(Java)來使客戶端應用程式能夠以寫程式方式驗證用戶。

可能需要用戶身份驗證才能與儲存安全資料的企業資料庫或其他企業儲存庫交互。

例如，假設用戶在網頁中輸入用戶名和密碼並將這些值提交到托管Forms的J2EE應用伺服器。 Forms自定義應用程式可以使用身份驗證管理器服務對用戶進行身份驗證。

如果驗證成功，則應用程式訪問安全的企業資料庫。 否則，向用戶發送消息，指出該用戶不是授權用戶。

下圖顯示了應用程式的邏輯流。

![au_au_umauth進程](assets/au_au_umauth_process.png)

下表介紹了此圖中的步驟

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
   <td><p>用戶訪問網站並指定用戶名和密碼。 此資訊將提交到托管AEM Forms的J2EE應用伺服器。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>用戶憑據通過Authentication Manager服務進行身份驗證。 如果用戶憑據有效，則工作流將繼續執行步驟3。 否則，向用戶發送消息，指出該用戶不是授權用戶。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>從安全的企業資料庫檢索用戶資訊和表單設計。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>將用戶資訊與表單設計合併，並將表單呈現給用戶。 </p></td>
  </tr>
 </tbody>
</table>

### 步驟摘要 {#summary_of_steps-5}

要以寫程式方式驗證用戶，請執行以下步驟：

1. 包括項目檔案。
1. 建立AuthenticationManagerService客戶端。
1. 調用驗證操作。
1. 如有必要，請檢索上下文，以便客戶端應用程式可以將其轉發到另一個AEM Forms服務進行身份驗證。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立AuthenticationManagerService客戶端**

在以寫程式方式驗證用戶之前，必須先建立AuthenticationManagerService客戶端。 使用Java API時，建立 `AuthenticationManagerServiceClient` 的雙曲餘切值。

**調用驗證操作**

建立服務客戶端後，可以調用驗證操作。 此操作需要有關用戶的資訊，如用戶的名稱和密碼。 如果用戶未進行身份驗證，則會引發異常。

**檢索驗證上下文**

在對用戶進行身份驗證後，可以在經過身份驗證的用戶中建立上下文。 然後，您可以使用內容調用其他AEM Forms服務。 例如，可以使用上下文建立 `EncryptionServiceClient` 用密碼加密PDF文檔。 確保已驗證的用戶具有名為 `Services User` 需要調用AEM Forms服務。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用戶管理器API快速啟動](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密碼加密PDF文檔](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API驗證用戶 {#authenticate-a-user-using-the-java-api}

使用Authentication Manager服務API(Java)驗證用戶：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-usermanager-client.jar。

1. 建立AuthenticationManagerServices客戶端。

   建立 `AuthenticationManagerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用驗證操作。

   調用 `AuthenticationManagerServiceClient` 對象 `authenticate` 方法並傳遞以下值：

   * A `java.lang.String` 包含用戶名的對象。
   * 位元組陣列(a `byte[]` 對象)。 您可以 `byte[]` 通過調用 `java.lang.String` 對象 `getBytes` 的雙曲餘切值。

   authenticate方法返回 `AuthResult` 對象，其中包含有關已驗證用戶的資訊。

1. 檢索驗證上下文。

   調用 `ServiceClientFactory` 對象 `getContext` 方法，它將返回 `Context` 的雙曲餘切值。

   然後調用 `Context` 對象 `initPrincipal` 方法和通過 `AuthResult`。

### 使用Web服務API驗證用戶 {#authenticate-a-user-using-the-web-service-api}

使用Authentication Manager服務API（Web服務）驗證用戶：

1. 包括項目檔案。

   * 建立使用驗證管理器WSDL的Microsoft.NET客戶端程式集。 (請參閱 [使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)
   * 引用Microsoft.NET客戶端程式集。 (請參閱中的「引用.NET客戶端程式集」 [使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)

1. 建立AuthenticationManagerService客戶端。

   建立 `AuthenticationManagerServiceService` 對象。

1. 調用驗證操作。

   調用 `AuthenticationManagerServiceClient` 對象 `authenticate` 方法並傳遞以下值：

   * A `string` 包含用戶名的對象
   * 位元組陣列(a `byte[]` 對象)。 您可以 `byte[]` 通過轉換對象 `string` 包含對 `byte[]` 陣列。
   * 返回的值將為 `AuthResult` 對象，可用於檢索有關用戶的資訊。 在下面的示例中，通過首先獲取 `AuthResult` 對象 `authenticatedUser` 欄位，然後獲取結果 `User` 對象 `canonicalName` 和 `domainName` 的子菜單。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 以寫程式方式同步用戶 {#programmatically-synchronizing-users}

可以使用用戶管理API以寫程式方式同步用戶。 同步用戶時，您正在使用用戶儲存庫中的用戶資料更新AEM Forms。 例如，假定您向用戶儲存庫添加新用戶。 執行同步操作後，新用戶將成為表AEM單用戶。 此外，不再在用戶儲存庫中的用戶也將從AEM Forms刪除。

下圖顯示了AEM Forms與用戶儲存庫同步。

![ps_ps_umauth同步](assets/ps_ps_umauth_sync.png)

下表介紹了此圖中的步驟

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
   <td><p>客戶端應用程式請求AEM Forms執行同步操作。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Forms執行同步操作。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用戶資訊已更新。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>用戶能夠查看更新的用戶資訊。 </p></td>
  </tr>
 </tbody>
</table>

### 步驟摘要 {#summary_of_steps-6}

要以寫程式方式同步用戶，請執行以下步驟：

1. 包括項目檔案。
1. 建立UserManagerUtilServiceClient客戶端。
1. 指定企業域。
1. 調用驗證操作。
1. 確定同步操作是否完成

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立UserManagerUtilServiceClientClient客戶端**

在以寫程式方式同步用戶之前，必須建立 `UserManagerUtilServiceClient` 的雙曲餘切值。

**指定企業域**

在使用用戶管理API執行同步操作之前，請指定用戶所屬的企業域。 可以指定一個或多個企業域。 在以寫程式方式執行同步操作之前，必須使用管理控制台設定企業域。 (請參閱 [管理幫助](https://www.adobe.com/go/learn_aemforms_admin_63)。)

**調用同步操作**

指定一個或多個企業域後，可以執行同步操作。 執行此操作所花的時間取決於用戶儲存庫中的用戶記錄數。

**確定同步操作是否完成**

以寫程式方式執行同步操作後，可以確定操作是否完成。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用戶管理器API快速啟動](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密碼加密PDF文檔](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API以寫程式方式同步用戶 {#programmatically-synchronizing-users-using-the-java-api}

使用用戶管理API(Java)同步用戶：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-usermanager-client.jar和adobe-usermanager-util-client.jar。

1. 建立UserManagerUtilServiceClient客戶端。

   建立 `UserManagerUtilServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定企業域。

   * 調用 `UserManagerUtilServiceClient` 對象 `scheduleSynchronization` 方法啟動用戶同步操作。
   * 建立 `java.util.Set` 實例 `HashSet` 建構子。 確保指定 `String` 類型。 此 `Java.util.Set` 實例儲存同步操作所應用的域名。
   * 對於要添加的每個域名，調用 `java.util.Set` 對象的add方法並傳遞域名。

1. 調用同步操作。

   調用 `ServiceClientFactory` 對象 `getContext` 方法，它將返回 `Context` 的雙曲餘切值。

   然後調用 `Context` 對象 `initPrincipal` 方法和通過 `AuthResult`。

**另請參閱**

[以寫程式方式同步用戶](users.md#programmatically-synchronizing-users)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
