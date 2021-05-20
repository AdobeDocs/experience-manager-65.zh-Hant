---
title: 管理使用者
seo-title: 管理使用者
description: 使用用戶管理API建立可管理角色、權限和承擔者（可以是用戶或組）以及驗證用戶的用戶端應用程式。
seo-description: 使用用戶管理API建立可管理角色、權限和承擔者（可以是用戶或組）以及驗證用戶的用戶端應用程式。
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6257'
ht-degree: 0%

---

# 管理用戶{#managing-users}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於使用者管理**

您可以使用使用者管理API來建立可管理角色、權限和承擔者（可以是使用者或群組），以及驗證使用者的用戶端應用程式。 使用者管理API包含下列AEM Forms API:

* 目錄管理器服務API
* Authentication Manager服務API
* 授權管理器服務API

使用者管理可讓您指派、移除和決定角色和權限。 它也可讓您指派、移除和查詢網域、使用者和群組。 最後，您可以使用「使用者管理」來驗證使用者。

在[新增使用者](users.md#adding-users)中，您將了解如何以程式設計方式新增使用者。 本節使用目錄管理器服務API。

在[刪除用戶](users.md#deleting-users)中，您將了解如何以程式設計方式刪除用戶。 本節使用目錄管理器服務API。

在[管理用戶和組](users.md#managing-users-and-groups)中，您將了解本地用戶和目錄用戶之間的差異，並查看如何使用Java和Web服務API以寫程式方式管理用戶和組的示例。 本節使用目錄管理器服務API。

在[管理角色和權限](users.md#managing-roles-and-permissions)中，您將了解系統角色和權限，以及可以以寫程式方式增強這些角色和權限的方法，並查看如何使用Java和Web服務API以寫程式方式管理角色和權限的示例。 本節同時使用目錄管理器服務API和授權管理器服務API。

在[驗證使用者](users.md#authenticating-users)中，您會看到如何使用Java和Web服務API以程式設計方式驗證使用者的範例。 本節使用授權管理器服務API。

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
>如果伺服器時區與客戶端時區不同，在使用WebSphere應用程式伺服器群集上的.NET客戶端在本機SOAP堆棧上使用AEM Forms生成PDF服務的WSDL時，可能會發生以下用戶管理驗證錯誤：

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**了解目錄管理**

用戶管理與支援到LDAP目錄的連接的目錄服務提供程式(DirectoryManagerService)一起打包。 如果貴組織使用非LDAP儲存庫來儲存用戶記錄，則可以建立與儲存庫一起使用的您自己的目錄服務提供程式。

目錄服務提供程式應用戶管理的請求從用戶儲存中檢索記錄。 「用戶管理」定期在資料庫中快取用戶和組記錄，以提高效能。

目錄服務提供程式可用於將用戶管理資料庫與用戶儲存同步。 此步驟可確保所有使用者目錄資訊以及所有使用者和群組記錄都為最新狀態。

此外， DirectoryManagerService還允許您建立和管理域。 網域會定義不同的使用者基礎。 網域的界限通常會根據組織的結構方式或使用者存放區的設定方式來定義。 用戶管理域提供身份驗證提供程式和目錄服務提供程式使用的配置設定。

在「用戶管理」導出的配置XML中，屬性值為`Domains`的根節點包含為「用戶管理」定義的每個域的XML元素。 這些元素中的每個都包含其他元素，這些元素定義與特定服務提供商關聯的域的各個方面。

**了解objectSID值**

使用Active Directory時，請務必了解`objectSID`值不是跨多個域的唯一屬性。 此值儲存對象的安全標識符。 在多個網域環境中（例如，網域樹狀結構）,`objectSID`值可以不同。

如果對象從一個Active Directory域移動到另一個域，`objectSID`值將更改。 域中的任何位置都有相同的`objectSID`值。 例如，BUILDIN\Administrators、BUILDIN\Power Users等組無論域如何都會有相同的`objectSID`值。 這些`objectSID`值眾所周知。

## 添加用戶{#adding-users}

您可以使用目錄管理器服務API（Java和Web服務），以寫程式方式將用戶添加到AEM Forms。 新增使用者後，當執行需要使用者的服務作業時，即可使用該使用者。 例如，您可以將任務指派給新使用者。

### 步驟{#summary-of-steps}的摘要

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
* **主要類型**:使用者的類型(例如，您可以指 `USER)`定。
* **指定名稱**:使用者的指定名稱(例如 `Wendy`)。
* **姓**:用戶的家族名稱(例如 `Blue)`。
* **地區**:用戶的地區資訊。

**新增使用者至AEM Forms**

定義使用者資訊後，即可將使用者新增至AEM Forms。 若要新增使用者，請叫用`DirectoryManagerServiceClient`物件的`createLocalUser`方法。

**確認已新增使用者**

您可以確認已新增使用者，以確保未發生任何問題。 使用使用者識別碼值來找出新使用者。

**另請參閱**

[使用Java API新增使用者](users.md#add-users-using-the-java-api)

[使用網站服務API新增使用者](users.md#add-users-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[刪除用戶](users.md#deleting-users)

### 使用Java API {#add-users-using-the-java-api}添加用戶

使用目錄管理器服務API(Java)添加用戶：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerServices客戶端。

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`DirectoryManagerServiceClient`物件。

1. 定義使用者資訊。

   * 使用其建構子建立`UserImpl`物件。
   * 調用`UserImpl`對象的`setDomainName`方法來設定demain名稱。 傳遞指定網域名稱的字串值。
   * 通過調用`UserImpl`對象的`setPrincipalType`方法來設定主類型。 傳遞指定使用者類型的字串值。 例如，您可以指定`USER`。
   * 調用`UserImpl`對象的`setUserid`方法，以設定用戶標識符值。 傳遞指定使用者識別碼值的字串值。 例如，您可以指定`wblue`。
   * 叫用`UserImpl`物件的`setCanonicalName`方法，以設定標準名稱。 傳遞指定使用者標準名稱的字串值。 例如，您可以指定`wblue`。
   * 調用`UserImpl`對象的`setGivenName`方法來設定給定名稱。 傳遞指定使用者指定名稱的字串值。 例如，您可以指定`Wendy`。
   * 調用`UserImpl`對象的`setFamilyName`方法來設定族名。 傳遞一個字串值，該字串值指定用戶的姓。 例如，您可以指定`Blue`。

   >[!NOTE]
   >
   >調用屬於`UserImpl`對象的方法以設定其他值。 例如，可以通過調用`UserImpl`對象的`setLocale`方法來設定區域設定值。

1. 新增使用者至AEM Forms。

   調用`DirectoryManagerServiceClient`對象的`createLocalUser`方法並傳遞以下值：

   * 代表新用戶的`UserImpl`對象
   * 代表使用者密碼的字串值

   `createLocalUser`方法返回一個字串值，該字串值指定本地用戶標識符值。

1. 確認已新增使用者。

   * 使用其建構子建立`PrincipalSearchFilter`物件。
   * 調用`PrincipalSearchFilter`對象的`setUserId`方法，以設定用戶標識符值。 傳遞代表使用者識別碼值的字串值。
   * 調用`DirectoryManagerServiceClient`對象的`findPrincipals`方法並傳遞`PrincipalSearchFilter`對象。 此方法會傳回`java.util.List`例項，其中每個元素都是`User`物件。 逐一查看`java.util.List`實例以查找用戶。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API新增使用者](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#add-users-using-the-web-service-api}添加用戶

使用目錄管理器服務API（Web服務）添加用戶：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 請確保為服務引用使用以下WSDL定義：`http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立DirectoryManagerService客戶端。

   * 使用其預設建構子建立`DirectoryManagerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`DirectoryManagerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 請務必指定`?blob=mtom`。
   * 獲取`DirectoryManagerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`DirectoryManagerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 定義使用者資訊。

   * 使用其建構子建立`UserImpl`物件。
   * 通過為`UserImpl`對象的`domainName`欄位指定字串值來設定demain名稱。
   * 通過為`UserImpl`對象的`principalType`欄位指定字串值來設定主類型。 例如，您可以指定`USER`。
   * 將字串值分配給`UserImpl`對象的`userid`欄位，以設定用戶標識符值。
   * 將字串值分配給`UserImpl`對象的`canonicalName`欄位，以設定標準名稱值。
   * 為`UserImpl`對象的`givenName`欄位指定字串值，以設定給定的名稱值。
   * 通過為`UserImpl`對象的`familyName`欄位指定字串值來設定族名值。

1. 新增使用者至AEM Forms。

   調用`DirectoryManagerServiceClient`對象的`createLocalUser`方法並傳遞以下值：

   * 代表新用戶的`UserImpl`對象
   * 代表使用者密碼的字串值

   `createLocalUser`方法返回一個字串值，該字串值指定本地用戶標識符值。

1. 確認已新增使用者。

   * 使用其建構子建立`PrincipalSearchFilter`物件。
   * 通過為`PrincipalSearchFilter`對象的`userId`欄位分配表示用戶標識符值的字串值來設定用戶的用戶標識符值。
   * 調用`DirectoryManagerServiceClient`對象的`findPrincipals`方法並傳遞`PrincipalSearchFilter`對象。 此方法會傳回`MyArrayOfUser`集合物件，其中每個元素都是`User`物件。 逐一查看`MyArrayOfUser`集合，以找到使用者。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除用戶{#deleting-users}

您可以使用目錄管理器服務API（Java和Web服務），以程式設計方式從AEM Forms中刪除用戶。 刪除用戶後，無法再使用該用戶執行需要用戶的服務操作。 例如，您不能將任務分配給已刪除的用戶。

### 步驟{#summary_of_steps-1}的摘要

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

要刪除用戶，請調用`DirectoryManagerServiceClient`對象的`deleteLocalUser`方法。

**另請參閱**

[使用Java API刪除使用者](users.md#delete-users-using-the-java-api)

[使用網站服務API刪除使用者](users.md#delete-users-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增使用者](users.md#adding-users)

### 使用Java API {#delete-users-using-the-java-api}刪除用戶

使用目錄管理器服務API(Java)刪除用戶：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`DirectoryManagerServiceClient`物件。

1. 指定要刪除的使用者。

   * 使用其建構子建立`PrincipalSearchFilter`物件。
   * 調用`PrincipalSearchFilter`對象的`setUserId`方法，以設定用戶標識符值。 傳遞代表使用者識別碼值的字串值。
   * 調用`DirectoryManagerServiceClient`對象的`findPrincipals`方法並傳遞`PrincipalSearchFilter`對象。 此方法會傳回`java.util.List`例項，其中每個元素都是`User`物件。 逐一查看`java.util.List`實例，以找到要刪除的用戶。

1. 從AEM Forms刪除使用者。

   調用`DirectoryManagerServiceClient`對象的`deleteLocalUser`方法，並傳遞`User`對象的`oid`欄位的值。 調用`User`對象的`getOid`方法。 使用從`java.util.List`實例檢索的`User`對象。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速入門（EJB模式）:使用Java API刪除使用者](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[快速入門（SOAP模式）:使用Java API刪除使用者](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#delete-users-using-the-web-service-api}刪除用戶

使用目錄管理器服務API（Web服務）刪除用戶：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   * 使用其預設建構子建立`DirectoryManagerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`DirectoryManagerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 確保指定`blob=mtom.`
   * 獲取`DirectoryManagerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`DirectoryManagerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 指定要刪除的使用者。

   * 使用其建構子建立`PrincipalSearchFilter`物件。
   * 將字串值分配給`PrincipalSearchFilter`對象的`userId`欄位，以設定用戶標識符值。
   * 調用`DirectoryManagerServiceClient`對象的`findPrincipals`方法並傳遞`PrincipalSearchFilter`對象。 此方法會傳回`MyArrayOfUser`集合物件，其中每個元素都是`User`物件。 逐一查看`MyArrayOfUser`集合，以找到使用者。 從`MyArrayOfUser`集合物件擷取的`User`物件用於刪除使用者。

1. 從AEM Forms刪除使用者。

   將`User`物件的`oid`欄位值傳遞至`DirectoryManagerServiceClient`物件的`deleteLocalUser`方法，以刪除使用者。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立組{#creating-groups}

您可以使用目錄管理器服務API（Java和Web服務）以寫程式方式建立AEM Forms組。 建立群組後，您可以使用該群組執行需要群組的服務操作。 例如，您可以指派使用者至新群組。 （請參閱[管理使用者和群組](users.md#managing-users-and-groups)。）

### 步驟{#summary_of_steps-2}的摘要

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

有關這些JAR檔案的位置的資訊，請參閱[包括AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務操作之前，請建立目錄管理器服務API客戶端。

**確定組是否存在**

建立群組時，請確定群組不存在於相同的網域中。 也就是說，兩個群組在相同網域內不能有相同的名稱。 要執行此任務，請執行搜索並根據兩個值篩選搜索結果。 將主體類型設定為`com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`以確保只返回組。 同時，請務必指定網域名稱。

**建立群組**

在您確定網域中不存在群組後，請建立群組並指定下列屬性：

* **CommonName**:群組的名稱。
* **網域**:新增群組的網域。
* **說明**:群組的說明。

**對組執行操作**

建立群組後，您可以使用群組執行動作。 例如，您可以新增使用者至群組。 若要將使用者新增至群組，請擷取該使用者和群組的唯一識別碼值。 將這些值傳遞至`addPrincipalToLocalGroup`方法。

**另請參閱**

[使用Java API建立群組](users.md#create-groups-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增使用者](users.md#adding-users)

[刪除用戶](users.md#deleting-users)

### 使用Java API {#create-groups-using-the-java-api}建立群組

使用目錄管理器服務API(Java)建立組：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService客戶端。

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`DirectoryManagerServiceClient`物件。

1. 確定組是否存在。

   * 使用其建構子建立`PrincipalSearchFilter`物件。
   * 調用`PrincipalSearchFilter`對象的`setPrincipalType`對象，以設定主類型。 傳遞值`com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`。
   * 調用`PrincipalSearchFilter`對象的`setSpecificDomainName`對象以設定域。 傳遞指定網域名稱的字串值。
   * 要查找組，請調用`DirectoryManagerServiceClient`對象的`findPrincipals`方法（主體可以是組）。 傳遞`PrincipalSearchFilter`對象，該對象指定主體類型和域名。 此方法會傳回`java.util.List`例項，其中每個元素都是`Group`例項。 每個組實例都符合使用`PrincipalSearchFilter`對象指定的篩選器。
   * 逐一查看`java.util.List`實例。 對於每個元素，擷取群組名稱。 確保組名不等於新組名。

1. 建立群組。

   * 如果組不存在，請調用`Group`對象的`setCommonName`方法，並傳遞指定組名的字串值。
   * 調用`Group`對象的`setDescription`方法並傳遞指定組說明的字串值。
   * 調用`Group`對象的`setDomainName`方法並傳遞指定域名的字串值。
   * 調用`DirectoryManagerServiceClient`對象的`createLocalGroup`方法並傳遞`Group`實例。

   `createLocalUser`方法返回一個字串值，該字串值指定本地用戶標識符值。

1. 對組執行操作。

   * 使用其建構子建立`PrincipalSearchFilter`物件。
   * 調用`PrincipalSearchFilter`對象的`setUserId`方法，以設定用戶標識符值。 傳遞代表使用者識別碼值的字串值。
   * 調用`DirectoryManagerServiceClient`對象的`findPrincipals`方法並傳遞`PrincipalSearchFilter`對象。 此方法會傳回`java.util.List`例項，其中每個元素都是`User`物件。 逐一查看`java.util.List`實例以查找用戶。
   * 叫用`DirectoryManagerServiceClient`物件的`addPrincipalToLocalGroup`方法，將使用者新增至群組。 傳遞`User`物件`getOid`方法的傳回值。 傳遞`Group`對象`getOid`方法的返回值（使用代表新組的`Group`實例）。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 管理用戶和組{#managing-users-and-groups}

本主題說明如何使用(Java)以程式設計方式指派、移除和查詢網域、使用者和群組。

>[!NOTE]
>
>設定網域時，您必須為群組和使用者設定唯一識別碼。 所選屬性不僅在LDAP環境中是唯一的，而且也必須是不可變的，並且在目錄中不會更改。 此屬性還必須是簡單的字串資料類型(Active Directory 2000/2003當前允許的唯一例外是`"objectsid"`，這是二進位值)。 例如，Novell eDirectory屬性`"GUID"`不是簡單的字串資料類型，因此將無法工作。

* 對於Active Directory，請使用`"objectsid"`。
* 對於SunOne，請使用`"nsuniqueid"`。

>[!NOTE]
>
>不支援在LDAP目錄同步正在進行時建立多個本地用戶和組。 嘗試此程式可能會導致錯誤。

### 步驟{#summary_of_steps-3}的摘要

要管理用戶和組，請執行以下步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService客戶端。
1. 調用相應的用戶或組操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立DirectoryManagerService客戶端**

在以寫程式方式執行目錄管理器服務操作之前，必須建立目錄管理器服務客戶端。 使用Java API，您可以建立`DirectoryManagerServiceClient`物件來完成此作業。 使用Web服務API，可建立`DirectoryManagerServiceService`物件來完成此操作。

**調用相應的用戶或組操作**

建立服務客戶端後，您就可以調用用戶或組管理操作。 服務客戶端允許您分配、刪除和查詢域、用戶和組。 請注意，可以將目錄主體或本地主體添加到本地組，但無法將本地主體添加到目錄組。

**另請參閱**

[使用Java API管理使用者和群組](users.md#managing-users-and-groups-using-the-java-api)

[使用網站服務API管理使用者和群組](users.md#managing-users-and-groups-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API {#managing-users-and-groups-using-the-java-api}管理使用者和群組

要使用(Java)以寫程式方式管理用戶、組和域，請執行以下任務：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。 有關這些檔案的位置資訊，請參閱[包含AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 建立DirectoryManagerService客戶端。

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`DirectoryManagerServiceClient`物件。 有關資訊，請參閱[設定連接屬性&#x200B;](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*。*

1. 調用相應的用戶或組操作。

   要查找用戶或組，請調用`DirectoryManagerServiceClient`對象的方法之一以查找主體（因為主體可以是用戶或組）。 在以下範例中，使用搜尋篩選器（`PrincipalSearchFilter`物件）呼叫`findPrincipals`方法。

   由於此情況下的返回值是包含`Principal`對象的`java.util.List`，請反覆查看結果，並將`Principal`對象轉換為`User`或`Group`對象。

   使用結果的`User`或`Group`對象（兩者均繼承自`Principal`介面），檢索工作流中需要的資訊。 例如，域名和規範名稱值組合在一起，可唯一標識主體。 這些參數是通過分別調用`Principal`對象的`getDomainName`和`getCanonicalName`方法來檢索的。

   若要刪除本地用戶，請調用`DirectoryManagerServiceClient`對象的`deleteLocalUser`方法並傳遞用戶的標識符。

   要刪除本地組，請調用`DirectoryManagerServiceClient`對象的`deleteLocalGroup`方法，並傳遞組的標識符。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#managing-users-and-groups-using-the-web-service-api}管理用戶和組

要使用目錄管理器服務API（Web服務）以寫程式方式管理用戶、組和域，請執行以下任務：

1. 包含專案檔案。

   * 建立一個Microsoft .NET客戶端程式集，該程式集將使用目錄管理器WSDL。 (請參閱[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)
   * 參考Microsoft .NET客戶端程式集。 （請參閱[建立使用Base64編碼](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)的.NET客戶端程式集。）

1. 建立DirectoryManagerService客戶端。

   使用代理類的建構子建立`DirectoryManagerServiceService`對象。

1. 調用相應的用戶或組操作。

   要查找用戶或組，請調用`DirectoryManagerServiceService`對象的方法之一以查找主體（因為主體可以是用戶或組）。 在以下範例中，使用搜尋篩選器（`PrincipalSearchFilter`物件）呼叫`findPrincipalsWithFilter`方法。 使用`PrincipalSearchFilter`對象時，僅當`isLocal`屬性設定為`true`時，才返回本地主體。 此行為與Java API的發生方式不同。

   >[!NOTE]
   >
   >如果未在搜尋篩選器中指定結果數上限（透過`PrincipalSearchFilter.resultsMax`欄位），則最多將傳回1000個結果。 這與使用Java API時的行為不同，Java API的預設上限為10個結果。 此外，除非在搜尋篩選器中指定結果的最大數量（例如，透過`GroupMembershipSearchFilter.resultsMax`欄位），否則`findGroupMembers`等搜尋方法不會產生任何結果。 這適用於繼承自`GenericSearchFilter`類的所有搜索篩選器。 如需詳細資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

   由於此情況下的返回值是包含`Principal`對象的`object[]`，請反覆查看結果，並將`Principal`對象轉換為`User`或`Group`對象。

   使用結果的`User`或`Group`對象（兩者均繼承自`Principal`介面），檢索工作流中需要的資訊。 例如，域名和規範名稱值組合在一起，可唯一標識主體。 這些欄位是通過分別調用`Principal`對象的`domainName`和`canonicalName`欄位來檢索的。

   若要刪除本地用戶，請調用`DirectoryManagerServiceService`對象的`deleteLocalUser`方法並傳遞用戶的標識符。

   要刪除本地組，請調用`DirectoryManagerServiceService`對象的`deleteLocalGroup`方法，並傳遞組的標識符。

**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 管理角色和權限{#managing-roles-and-permissions}

本主題說明如何使用授權管理器服務API(Java)，以程式設計方式指派、移除及決定角色和權限。

在AEM Forms中，*role*&#x200B;是一組存取一或多個系統層級資源的權限。 這些權限是透過「使用者管理」建立，並由服務元件強制執行。 例如，管理員可以將「策略集作者」的角色分配給一組用戶。 然後，Rights Management將允許具有該角色的組的用戶通過管理控制台建立策略集。

角色有兩種類型：*預設角色*&#x200B;和&#x200B;*自訂角色*。 預設角色（*系統角色）*&#x200B;已駐留在AEM Forms中。 假定管理員不能刪除或修改預設角色，因此不可變。 因此，管理員建立的自定義角色可變，管理員隨後可修改或刪除這些角色。

角色可讓您更輕鬆管理權限。 當角色被分配給承擔者時，一組權限被自動分配給該承擔者，並且承擔者的所有與訪問相關的特定決策都基於該整體分配的權限集。

### 步驟{#summary_of_steps-4}的摘要

要管理角色和權限，請執行以下步驟：

1. 包含專案檔案。
1. 建立AuthorizationManagerService客戶端。
1. 調用相應的角色或權限操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立AuthorizationManagerService客戶端**

在以寫程式方式執行用戶管理授權管理器服務操作之前，必須建立授權管理器服務客戶端。 使用Java API，您可以建立`AuthorizationManagerServiceClient`物件來完成此作業。

**調用適當的角色或權限操作**

建立服務客戶端後，您就可以調用角色或權限操作。 服務客戶端允許您分配、刪除和確定角色和權限。

**另請參閱**

[使用Java API管理角色和權限](users.md#managing-roles-and-permissions-using-the-java-api)

[使用網站服務API管理角色和權限](users.md#managing-roles-and-permissions-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API {#managing-roles-and-permissions-using-the-java-api}管理角色和權限

要使用授權管理器服務API(Java)管理角色和權限，請執行以下任務：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立AuthorizationManagerService客戶端。

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`AuthorizationManagerServiceClient`物件。

1. 調用相應的角色或權限操作。

   要將角色分配給承擔者，請調用`AuthorizationManagerServiceClient`對象的`assignRole`方法並傳遞以下值：

   * 包含角色標識符的`java.lang.String`對象
   * 包含主標識符的`java.lang.String`對象的陣列。

   要從主體中刪除角色，請調用`AuthorizationManagerServiceClient`對象的`unassignRole`方法並傳遞以下值：

   * 包含角色標識符的`java.lang.String`對象。
   * 包含主標識符的`java.lang.String`對象的陣列。


**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API管理角色和權限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#managing-roles-and-permissions-using-the-web-service-api}管理角色和權限

使用授權管理器服務API（Web服務）管理角色和權限：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立AuthorizationManagerService客戶端。

   * 使用其預設建構子建立`AuthorizationManagerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`AuthorizationManagerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。
   * 獲取`AuthorizationManagerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 調用相應的角色或權限操作。

   要將角色分配給承擔者，請調用`AuthorizationManagerServiceClient`對象的`assignRole`方法並傳遞以下值：

   * 包含角色標識符的`string`對象
   * 包含主標識符的`MyArrayOf_xsd_string`對象。

   要從主體中刪除角色，請調用`AuthorizationManagerServiceService`對象的`unassignRole`方法並傳遞以下值：

   * 包含角色標識符的`string`對象。
   * 包含主標識符的`string`對象的陣列。


**另請參閱**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 驗證用戶{#authenticating-users}

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
   <td><p>3</p></td>
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

### 步驟{#summary_of_steps-5}的摘要

要以寫程式方式驗證用戶，請執行以下步驟：

1. 包含專案檔案。
1. 建立AuthenticationManagerService客戶端。
1. 調用驗證操作。
1. 如有必要，請擷取內容，讓用戶端應用程式可將其轉送至其他AEM Forms服務進行驗證。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立AuthenticationManagerService客戶端**

在以寫程式方式對用戶進行身份驗證之前，必須建立AuthenticationManagerService客戶端。 使用Java API時，請建立`AuthenticationManagerServiceClient`物件。

**調用驗證操作**

建立服務客戶端後，您就可以調用驗證操作。 此操作將需要有關用戶的資訊，如用戶名和密碼。 如果用戶未進行身份驗證，則會引發異常。

**擷取驗證內容**

一旦您驗證了使用者，您就可以根據已驗證的使用者建立內容。 然後，您可以使用內容叫用其他AEM Forms服務。 例如，您可以使用上下文建立`EncryptionServiceClient`並使用密碼加密PDF文檔。 確認已驗證的使用者具有叫用AEM Forms服務所需的角色`Services User`。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密碼加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#authenticate-a-user-using-the-java-api}驗證用戶

使用Authentication Manager服務API(Java)驗證用戶：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立AuthenticationManagerServices客戶端。

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`AuthenticationManagerServiceClient`物件。

1. 調用驗證操作。

   調用`AuthenticationManagerServiceClient`對象的`authenticate`方法並傳遞以下值：

   * 包含用戶名的`java.lang.String`對象。
   * 包含使用者密碼的位元組陣列（`byte[]`物件）。 您可以調用`java.lang.String`對象的`getBytes`方法來獲取`byte[]`對象。

   驗證方法返回`AuthResult`對象，該對象包含有關已驗證用戶的資訊。

1. 擷取驗證內容。

   調用`ServiceClientFactory`對象的`getContext`方法，該方法將返回`Context`對象。

   然後調用`Context`對象的`initPrincipal`方法並傳遞`AuthResult`。

### 使用Web服務API {#authenticate-a-user-using-the-web-service-api}驗證用戶

使用Authentication Manager服務API（Web服務）驗證用戶：

1. 包含專案檔案。

   * 建立一個Microsoft .NET客戶端程式集，該程式集將使用身份驗證管理器WSDL。 (請參閱[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)
   * 參考Microsoft .NET客戶端程式集。 (請參閱[使用Base64編碼叫用AEM Forms中的「參考.NET客戶端程式集」。)](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

1. 建立AuthenticationManagerService客戶端。

   使用代理類的建構子建立`AuthenticationManagerServiceService`對象。

1. 調用驗證操作。

   調用`AuthenticationManagerServiceClient`對象的`authenticate`方法並傳遞以下值：

   * 包含用戶名的`string`對象
   * 包含使用者密碼的位元組陣列（`byte[]`物件）。 您可以使用以下示例中所示的邏輯將包含密碼的`string`對象轉換為`byte[]`陣列，從而獲得`byte[]`對象。
   * 傳回的值將是`AuthResult`物件，可用來擷取使用者的相關資訊。 在以下示例中，首先獲取`AuthResult`對象的`authenticatedUser`欄位，然後獲取結果的`User`對象的`canonicalName`和`domainName`欄位，以檢索用戶的資訊。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 以寫程式方式同步用戶{#programmatically-synchronizing-users}

您可以使用使用者管理API，以程式設計方式同步使用者。 同步使用者時，您會將AEM Forms與位於使用者存放庫中的使用者資料更新。 例如，假設您將新使用者新增至您的使用者存放庫。 執行同步操作後，新使用者會變成AEM表單使用者。 此外，您的使用者存放庫中不再有的使用者，也會從AEM Forms中移除。

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
   <td><p>3</p></td>
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

### 步驟{#summary_of_steps-6}的摘要

要以寫程式方式同步用戶，請執行以下步驟：

1. 包含專案檔案。
1. 建立UserManagerUtilServiceClient客戶端。
1. 指定企業網域。
1. 調用驗證操作。
1. 確定同步操作是否完成

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立UserManagerUtilServiceClientclient**

必須先建立`UserManagerUtilServiceClient`對象，才能以寫程式方式同步用戶。

**指定企業網域**

在使用用戶管理API執行同步操作之前，請指定用戶所屬的企業域。 您可以指定一或多個企業網域。 在以寫程式方式執行同步操作之前，必須使用管理控制台來設定企業域。 （請參閱[管理幫助](https://www.adobe.com/go/learn_aemforms_admin_63)。）

**調用同步操作**

指定一個或多個企業域後，可以執行同步操作。 執行此操作所花的時間取決於位於用戶儲存庫中的用戶記錄數。

**確定同步操作是否完成**

以寫程式方式執行同步操作後，可以確定操作是否完成。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密碼加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#programmatically-synchronizing-users-using-the-java-api}以程式設計方式同步使用者

使用「使用者管理API」(Java)同步使用者：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-usermanager-client.jar和adobe-usermanager-util-client.jar。

1. 建立UserManagerUtilServiceClient客戶端。

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`UserManagerUtilServiceClient`物件。

1. 指定企業網域。

   * 調用`UserManagerUtilServiceClient`對象的`scheduleSynchronization`方法以啟動用戶同步操作。
   * 使用`HashSet`建構子建立`java.util.Set`例項。 請確保指定`String`作為資料類型。 此`Java.util.Set`實例儲存同步操作應用的域名。
   * 對於要添加的每個域名，調用`java.util.Set`對象的add方法並傳遞域名。

1. 調用同步操作。

   調用`ServiceClientFactory`對象的`getContext`方法，該方法將返回`Context`對象。

   然後調用`Context`對象的`initPrincipal`方法並傳遞`AuthResult`。

**另請參閱**

[以程式設計方式同步使用者](users.md#programmatically-synchronizing-users)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
