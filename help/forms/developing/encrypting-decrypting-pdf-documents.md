---
title: 加密和解密PDF檔案
seo-title: 加密和解密PDF檔案
description: 'null'
seo-description: 'null'
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# 加密和解密PDF檔案 {#encrypting-and-decrypting-pdf-documents}

**關於加密服務**

加密服務可讓您加密和解密檔案。 當文檔加密時，其內容將變得不可讀。 授權用戶可以解密文檔以獲得對內容的訪問。 如果PDF檔案使用密碼加密，使用者必須先指定開啟的密碼，才能在Adobe reader或Adobe Acrobat中檢視該檔案。 同樣地，如果PDF檔案使用憑證加密，使用者必須使用與用來加密PDF檔案的憑證（私密金鑰）對應的公開金鑰來解密PDF檔案。

您可以使用Encryption服務完成以下任務：

* 使用密碼加密PDF檔案。 (請參 [閱使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)
* 使用憑證加密PDF檔案。 (請參 [閱使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。)
* 從PDF檔案移除密碼加密。 (請參 [閱刪除密碼加密](encrypting-decrypting-pdf-documents.md#removing-password-encryption)。)
* 從PDF檔案移除憑證式加密。 (請參 [閱移除憑證式加密](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption))。
* 解除鎖定PDF檔案，以便執行其他服務作業。 例如，在解除鎖定密碼加密的PDF檔案後，您就可以套用數位簽章。 (請參閱解 [除加密的PDF檔案鎖定](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)。)
* 確定安全PDF檔案的加密類型。 (請參閱 [確定加密類型](encrypting-decrypting-pdf-documents.md#determining-encryption-type)。)

   ***注意&#x200B;**:如需Encryption服務的詳細資訊，請參閱「AEM[表格的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。*

## 使用密碼加密PDF檔案 {#encrypting-pdf-documents-with-a-password}

當您使用密碼加密PDF檔案時，使用者必須指定密碼才能在Adobe Reader或Acrobat中開啟PDF檔案。 此外，在對檔案執行其他AEM Forms作業（例如數位簽署PDF檔案）之前，必須先解除鎖定密碼加密的PDF檔案。

>[!NOTE]
>
>如果您將加密的PDF檔案上傳至AEM Forms存放庫，它將無法解密PDF檔案並擷取XDP內容。 建議您不要在將檔案上傳至AEM Forms儲存庫之前加密檔案。 (請參閱 [編寫資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。)

>[!NOTE]
>
>如需Encryption服務的詳細資訊，請參閱「AEM [表格的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要使用密碼加密PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密客戶端API對象。
1. 取得要加密的PDF檔案。
1. 設定加密運行時選項。
1. 新增密碼。
1. 將加密的PDF檔案儲存為PDF檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

**建立加密客戶端API對象**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。

**取得PDF檔案以加密**

您必須取得未加密的PDF檔案，才能使用密碼來加密檔案。 如果您嘗試保護已加密的PDF檔案，會造成例外。

**設定加密運行時選項**

若要使用密碼加密PDF檔案，請指定4個值，包括2個密碼值。 第一個密碼值用於加密PDF文檔，在開啟PDF文檔時必須指定。 第二個密碼值（稱為主密碼值）用於從PDF文檔中刪除加密。 密碼值區分大小寫，這兩個密碼值不能是相同的值。

您必須指定要加密的PDF檔案資源。 您可以加密整份PDF檔案、除檔案中繼資料外的所有內容，或僅加密檔案的附件。 如果您只加密檔案的附件，當使用者嘗試存取檔案附件時，會提示使用者輸入密碼。

在加密PDF檔案時，您可以指定與安全檔案相關的權限。 透過指定權限，您可以控制開啟密碼加密PDF檔案的使用者可執行的動作。 例如，若要成功擷取表單資料，您必須設定下列權限：

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>權限被指定為 `PasswordEncryptionPermission` 枚舉值。

**新增密碼**

在擷取不安全的PDF檔案並設定加密執行時值後，您可以在PDF檔案中新增密碼。

**將加密的PDF檔案儲存為PDF檔案**

您可以將密碼加密的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[使用web service API加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### 使用Java API加密PDF檔案 {#encrypt-a-pdf-document-using-the-java-api}

使用Encryption API(Java)，以密碼加密PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密用戶端API。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EncryptionServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得要加密的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表要加密之PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 設定加密運行時選項。

   * 通過調用 `PasswordEncryptionOptionSpec` 其建構子建立對象。
   * 指定要加密的PDF檔案資源，方 `PasswordEncryptionOptionSpec` 法是叫用物件的方 `setEncryptOption` 法，並傳 `PasswordEncryptionOption` 遞列舉值，指定要加密的檔案資源。 例如，若要加密整個PDF檔案，包括其中繼資料及其附件，請指定 `PasswordEncryptionOption.ALL`。
   * 使用建 `java.util.List` 構函式建立儲存加密權限的物 `ArrayList` 件。
   * 通過調用對象&#39;s方 `java.util.List` 法並傳遞 `add` 與要設定的權限相對應的枚舉值來指定權限。 例如，若要設定允許使用者複製PDF檔案中資料的權限，請指定 `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`。 （請針對每個要設定的權限重複此步驟）。
   * 調用物件的方法並傳遞列舉值，以指 `PasswordEncryptionOptionSpec` 定Acrobat相容 `setCompatability` 性等級，以指定Acrobat相容性選項。 例如，您可以指定 `PasswordEncryptionCompatability.ACRO_7`。
   * 指定密碼值，讓使用者可以叫用物件的方法，並傳 `PasswordEncryptionOptionSpec` 遞代表 `setDocumentOpenPassword` 開啟密碼的字串值，以開啟加密的PDF檔案。
   * 指定主密碼值，讓使用者透過叫用物件的方法並傳遞代表主密碼的字 `PasswordEncryptionOptionSpec` 串值， `setPermissionPassword` 從PDF檔案移除加密。

1. 新增密碼。

   調用物件的方法並傳 `EncryptionServiceClient` 遞下列值， `encryptPDFUsingPassword` 以加密PDF檔案：

   * 包 `com.adobe.idp.Document` 含要使用密碼加密的PDF文檔的對象。
   * 包 `PasswordEncryptionOptionSpec` 含加密運行時選項的對象。
   此方 `encryptPDFUsingPassword` 法會傳回包 `com.adobe.idp.Document` 含密碼加密PDF檔案的物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法，將物件的內容 `com.adobe.idp.Document` 複製至檔案。 請確定您使用 `com.adobe.idp.Document` 方法傳回的物 `encryptPDFUsingPassword` 件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API加密PDF檔案](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API加密PDF檔案 {#encrypting-a-pdf-document-using-the-web-service-api}

使用Encryption API(web service)，以密碼加密PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立加密客戶端API對象。

   * 使用其 `EncryptionServiceClient` 預設建構函式建立物件。
   * 使用建 `EncryptionServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `EncryptionServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得要加密的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用於儲存使用密碼加密的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元 `BLOB` 組陣列的內容指派給物件的資料成員， `BLOB` 以填入 `MTOM` 物件。

1. 設定加密運行時選項。

   * 使用其 `PasswordEncryptionOptionSpec` 建構函式建立物件。
   * 指定要加密的PDF檔案資源，方法 `PasswordEncryptionOption` 是將列舉值指派 `PasswordEncryptionOptionSpec` 給物件的資 `encryptOption` 料成員。 若要加密整個PDF，包括其中繼資料及其附件，請指派 `PasswordEncryptionOption.ALL` 給此資料成員。
   * 指定Acrobat相容性選項，方 `PasswordEncryptionCompatability` 法是將列舉值指 `PasswordEncryptionOptionSpec` 派給物件的資 `compatability` 料成員。 例如，指派 `PasswordEncryptionCompatability.ACRO_7` 給此資料成員。
   * 指定密碼值，讓使用者指派字串值，代表物件資料成員的開啟密碼，以開啟加密 `PasswordEncryptionOptionSpec` 的PDF `documentOpenPassword` 檔案。
   * 指定密碼值，讓使用者將代表主密碼的字串值指派給物件的資料成員，以移除PDF文 `PasswordEncryptionOptionSpec` 件的 `permissionPassword` 加密。

1. 新增密碼。

   調用物件的方法並傳 `EncryptionServiceClient` 遞下列值， `encryptPDFUsingPassword` 以加密PDF檔案：

   * 包 `BLOB` 含要使用密碼加密的PDF文檔的對象。
   * 包 `PasswordEncryptionOptionSpec` 含加密運行時選項的對象。
   此方 `encryptPDFUsingPassword` 法會傳回包 `BLOB` 含密碼加密PDF檔案的物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示受保護PDF文檔的檔案位置。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `encryptPDFUsingPassword` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 使用憑證加密PDF檔案 {#encrypting-pdf-documents-with-certificates}

憑證式加密可讓您透過公開金鑰技術，為特定收件者加密檔案。 可以為不同的收件者授予不同的檔案權限。 公鑰技術使加密的許多方面成為可能。 演算法可用來產生兩個大數字，稱為 *鍵*，具有下列屬性：

* 一個密鑰用於加密一組資料。 隨後，只能使用其他密鑰解密資料。
* 不可能區分一把鑰匙和另一把鑰匙。

其中一個金鑰可當成使用者的私密金鑰。 請務必僅讓使用者存取此金鑰。 另一個金鑰是使用者的公開金鑰，可與其他人共用。

公開金鑰憑證包含使用者的公開金鑰和識別資訊。 X.509格式用於儲存憑證。 證書通常由證書頒發機構(CA)核發和數位簽名，該機構是一個認可的實體，提供對證書有效性的信任度。 憑證有到期日，之後即不再有效。 此外，證書撤銷清單(CRL)提供在證書到期日前被撤銷的證書資訊。 憑證授權機構會定期發佈CRL。 證書的撤銷狀態也可以通過網路上的線上證書狀態協定(OCSP)來檢索。

>[!NOTE]
>
>如果您將加密的PDF檔案上傳至AEM Forms存放庫，它將無法解密PDF檔案並擷取XDP內容。 建議您不要在將檔案上傳至AEM Forms儲存庫之前加密檔案。 (請參閱 [編寫資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。)

>[!NOTE]
>
>您必須先確保將憑證新增至AEM Forms，才能使用憑證加密PDF檔案。 憑證是使用管理控制台或使用信任管理器API以程式設計方式新增。 (請參 [閱使用Trust Manager API匯入認證](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。)

>[!NOTE]
>
>如需Encryption服務的詳細資訊，請參閱「AEM [表格的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要使用證書加密PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密客戶端API對象。
1. 取得要加密的PDF檔案。
1. 參考憑證。
1. 設定加密運行時選項。
1. 建立憑證加密的PDF檔案。
1. 將加密的PDF檔案儲存為PDF檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

**建立加密客戶端API對象**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java Encryption Service API，請建立物 `EncrytionServiceClient` 件。 如果您使用web service Encryption Service API，請建立物 `EncryptionServiceService` 件。

**取得PDF檔案以加密**

您必須取得未加密的PDF檔案才能加密。 如果您嘗試保護已加密的PDF檔案，則會擲出例外。

**參考憑證**

若要使用憑證來加密PDF檔案，請參考用來加密PDF檔案的憑證。 憑證是。cer檔案、.crt檔案或。pem檔案。 PKCS#12檔案用於儲存具有相應證書的私鑰。

使用憑證加密PDF檔案時，請指定與安全檔案相關的權限。 透過指定權限，您可以控制開啟憑證加密PDF檔案的使用者可執行的動作。

**設定加密運行時選項**

指定要加密的PDF檔案資源。 您可以加密整份PDF檔案、除檔案中繼資料以外的所有內容，或僅加密檔案的附件。

**建立憑證加密的PDF檔案**

擷取不安全的PDF檔案、參考憑證並設定執行時期選項後，您就可以建立憑證加密的PDF檔案。 在PDF檔案加密後，您需要對應的公開金鑰才能解密。

**將加密的PDF檔案儲存為PDF檔案**

您可以將加密的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[使用web service API使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API使用憑證加密PDF檔案 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

使用Encryption API(Java)使用憑證來加密PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密客戶端API對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EncryptionServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得要加密的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表要加密之PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 參考憑證。

   * 使用建 `java.util.List` 構函式建立儲存權限資訊的物件。
   * 調用物件的方法並傳遞列舉值，以指定與 `java.util.List``add``CertificateEncryptionPermissions` 加密檔案相關的權限，該列舉值代表授予開啟安全PDF檔案之使用者的權限。 例如，若要指定所有權限，請傳遞 `CertificateEncryptionPermissions.PKI_ALL_PERM`。
   * 使用其 `Recipient` 建構函式建立物件。
   * 建立一 `java.io.FileInputStream` 個對象，該對象表示通過使用PDF文檔的建構子並傳遞指定證書位置的字串值來加密PDF文檔的證書。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞代表憑證的 `java.io.FileInputStream` 物件，以建立物件。
   * 叫用物 `Recipient` 件的方 `setX509Cert` 法，並傳遞包 `com.adobe.idp.Document` 含憑證的物件。 (此外，對象可 `Recipient`以有Truststore證書別名或LDAP URL作為證書源。)
   * 使用建 `CertificateEncryptionIdentity` 構函式建立儲存權限和憑證資訊的物件。
   * 叫用物 `CertificateEncryptionIdentity` 件的方 `setPerms` 法，並傳遞 `java.util.List` 儲存權限資訊的物件。
   * 叫用物 `CertificateEncryptionIdentity` 件的方 `setRecipient` 法，並傳遞 `Recipient` 儲存憑證資訊的物件。
   * 使用其 `java.util.List` 建構函式建立儲存憑證資訊的物件。
   * 叫用 `java.util.List` 物件的新增方法並傳遞物 `CertificateEncryptionIdentity` 件。 (此 `java.util.List` 物件會作為參數傳遞至 `encryptPDFUsingCertificates` 方法。)

1. 設定加密運行時選項。

   * 通過調用 `CertificateEncryptionOptionSpec` 其建構子建立對象。
   * 指定要加密的PDF檔案資源，方 `CertificateEncryptionOptionSpec` 法是叫用物件的方 `setOption` 法，並傳 `CertificateEncryptionOption` 遞列舉值，指定要加密的檔案資源。 例如，若要加密整個PDF檔案，包括其中繼資料及其附件，請指定 `CertificateEncryptionOption.ALL`。
   * 調用物件的方法並傳遞列舉值，以指 `CertificateEncryptionOptionSpec` 定Acrobat相容 `setCompat` 性等級， `CertificateEncryptionCompatibility` 以指定Acrobat相容性選項。 例如，您可以指定 `CertificateEncryptionCompatibility.ACRO_7`。

1. 建立憑證加密的PDF檔案。

   使用憑證來加密PDF檔案，方法是叫 `EncryptionServiceClient` 用物件的方 `encryptPDFUsingCertificates` 法並傳遞下列值：

   * 包 `com.adobe.idp.Document` 含要加密的PDF文檔的對象。
   * 儲存 `java.util.List` 證書資訊的對象。
   * 包 `CertificateEncryptionOptionSpec` 含加密運行時選項的對象。
   此方 `encryptPDFUsingCertificates` 法會傳回包 `com.adobe.idp.Document` 含憑證加密PDF檔案的物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法，將物件的內容 `com.adobe.idp.Document` 複製至檔案。 請確定您使用 `com.adobe.idp.Document` 方法傳回的物 `encryptPDFUsingCertificates` 件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API使用憑證加密PDF檔案](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API使用憑證加密PDF檔案 {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

使用Encryption API(web service)使用憑證來加密PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立加密客戶端API對象。

   * 使用其 `EncryptionServiceClient` 預設建構函式建立物件。
   * 使用建 `EncryptionServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `EncryptionServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得要加密的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用於儲存使用憑證加密的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 參考憑證。

   * 使用其 `Recipient` 建構函式建立物件。 此對象將儲存證書資訊。
   * 使用其 `BLOB` 建構函式建立物件。 此 `BLOB` 物件會儲存加密PDF檔案的憑證。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示證書的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元 `BLOB` 組陣列的內容指派給物件的資料成員， `BLOB` 以填入 `MTOM` 物件。
   * 將儲存 `BLOB` 憑證的物件指派給物件的 `Recipient` 資料成 `x509Cert` 員。
   * 使用其 `CertificateEncryptionIdentity` 建構函式建立儲存憑證資訊的物件。
   * 將儲存 `Recipient` 憑證的物件指派給物件 `CertificateEncryptionIdentity`的收件者資料成員。
   * 建立 `Object` 陣列並將對 `CertificateEncryptionIdentity` 像指定給陣列的第一個元 `Object` 素。 此 `Object` 陣列會作為參數傳遞至方 `encryptPDFUsingCertificates` 法。

1. 設定加密運行時選項。

   * 使用其 `CertificateEncryptionOptionSpec` 建構函式建立物件。
   * 指定要加密的PDF檔案資源，方法 `CertificateEncryptionOption` 是將列舉值指派 `CertificateEncryptionOptionSpec` 給物件的資 `option` 料成員。 若要加密整個PDF檔案，包括其中繼資料及其附件，請指派 `CertificateEncryptionOption.ALL` 給此資料成員。
   * 指定Acrobat相容性選項，方 `CertificateEncryptionCompatibility` 法是將列舉值指 `CertificateEncryptionOptionSpec` 派給物件的資 `compat` 料成員。 例如，指派 `CertificateEncryptionCompatibility.ACRO_7` 給此資料成員。

1. 建立憑證加密的PDF檔案。

   使用憑證來加密PDF檔案，方法是叫 `EncryptionServiceService` 用物件的方 `encryptPDFUsingCertificates` 法並傳遞下列值：

   * 包 `BLOB` 含要加密的PDF文檔的對象。
   * 儲存 `Object` 憑證資訊的陣列。
   * 包 `CertificateEncryptionOptionSpec` 含加密運行時選項的對象。
   此方 `encryptPDFUsingCertificates` 法會傳回包 `BLOB` 含憑證加密PDF檔案的物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示受保護PDF文檔的檔案位置。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `encryptPDFUsingCertificates` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `binaryData` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除基於證書的加密 {#removing-certificate-based-encryption}

您可從PDF檔案移除憑證式加密，讓使用者在Adobe Reader或Acrobat中開啟PDF檔案。 若要從使用憑證加密的PDF檔案移除加密，必須參考公開金鑰。 從PDF檔案移除加密後，就不再安全。

>[!NOTE]
>
>如需Encryption服務的詳細資訊，請參閱「AEM [表格的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

要從PDF文檔中刪除基於證書的加密，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密服務客戶端。
1. 取得加密的PDF檔案。
1. 刪除加密。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

**建立加密服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java Encryption Service API，請建立物 `EncrytionServiceClient` 件。 如果您使用web service Encryption Service API，請建立物 `EncryptionServiceService` 件。

**取得加密的PDF檔案**

您必須取得加密的PDF檔案，才能移除憑證式加密。 如果您嘗試從未加密的PDF檔案移除加密，則會擲出例外。 同樣地，如果您嘗試從密碼加密的檔案中移除憑證式加密，則會擲出例外。

**刪除加密**

若要從加密的PDF檔案移除憑證式加密，您需要加密的PDF檔案和與用來加密PDF檔案的金鑰相對應的私密金鑰。 從加密的PDF檔案移除憑證式加密時，會指定私密金鑰的別名值。 如需公開金鑰的詳細資訊，請參 [閱使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。

>[!NOTE]
>
>私密金鑰會儲存在AEM Forms信任商店中。 將證書放在那裡時，會指定別名值。

**儲存PDF檔案**

從加密的PDF檔案移除憑證式加密後，您就可將PDF檔案儲存為PDF檔案。 使用者可在Adobe reader或Acrobat中開啟PDF檔案。

**另請參閱**

[使用Java API移除憑證式加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[使用web service API移除憑證式加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API移除憑證式加密 {#remove-certificate-based-encryption-using-the-java-api}

使用Encryption API(Java)從PDF檔案移除憑證式加密：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EncryptionServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得加密的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定加密PDF檔案位置的字串值，建立代表加密PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 刪除加密。

   調用物件的方法並傳遞下列值，以移除PDF `EncryptionServiceClient` 檔案中 `removePDFCertificateSecurity` 的憑證式加密：

   * 包 `com.adobe.idp.Document` 含加密PDF檔案的物件。
   * 一個字串值，它指定與用於加密PDf文檔的密鑰相對應的私鑰的別名。
   此方 `removePDFCertificateSecurity` 法會傳回包 `com.adobe.idp.Document` 含不安全PDF檔案的物件。

1. 儲存PDF檔案。

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法，將物件的內容 `Document` 複製至檔案。 請確定您使用 `com.adobe.idp.Document` 方法傳回的物 `removePDFCredentialSecurity` 件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API移除憑證式加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API移除憑證式加密 {#remove-certificate-based-encryption-using-the-web-service-api}

使用Encryption API(web service)移除憑證式加密：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立加密服務客戶端。

   * 使用其 `EncryptionServiceClient` 預設建構函式建立物件。
   * 使用建 `EncryptionServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `EncryptionServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用來儲存加密的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元 `BLOB` 組陣列的內容指派給物件的資料成員， `BLOB` 以填入 `MTOM` 物件。

1. 刪除加密。

   叫用物 `EncryptionServiceClient` 件的方 `removePDFCertificateSecurity` 法並傳遞下列值：

   * 包含 `BLOB` 代表加密PDF檔案之檔案串流資料的物件。
   * 一個字串值，它指定與用於加密PDf文檔的私鑰相對應的公鑰的別名。
   此方 `removePDFCredentialSecurity` 法會傳回包 `BLOB` 含不安全PDF檔案的物件。

1. 儲存PDF檔案。

   * 調用 `System.IO.FileStream` 其建構函式並傳遞字串值，以建立物件，此字串值代表不安全PDF檔案的檔案位置。
   * 建立一個位元組陣列，該陣列儲存方 `BLOB` 法返回的對象的內 `removePDFPasswordSecurity` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除密碼加密 {#removing-password-encryption}

您可從PDF檔案移除密碼加密，讓使用者在Adobe Reader或Acrobat中開啟PDF檔案，而不需指定密碼。 從PDF檔案移除密碼加密後，檔案就不再安全。

>[!NOTE]
>
>如需Encryption服務的詳細資訊，請參閱「AEM [表格的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

要從PDF文檔中刪除基於密碼的加密，請執行以下步驟：

1. 包含專案檔案
1. 建立加密服務客戶端。
1. 取得加密的PDF檔案。
1. 刪除密碼。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

**建立加密服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java Encryption Service API，請建立物 `EncrytionServiceClient` 件。 如果您使用web service Encryption Service API，請建立物 `EncryptionServiceService` 件。

**取得加密的PDF檔案**

您必須取得加密的PDF檔案，才能移除密碼型加密。 如果您嘗試從未加密的PDF檔案移除加密，則會擲出例外。

**刪除密碼**

若要從加密的PDF檔案移除密碼型加密，您需要加密的PDF檔案和用於從PDF檔案移除加密的主密碼值。 用於開啟密碼加密的PDF文檔的密碼不能用於刪除加密。 當使用密碼加密PDF檔案時，會指定主密碼。 (請參 [閱使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

**儲存PDF檔案**

在Encryption服務移除PDF檔案中以密碼為基礎的加密後，您可以將PDF檔案儲存為PDF檔案。 使用者可以在Adobe Reader或Acrobat中開啟PDF檔案，毋需指定密碼。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API移除密碼型加密 {#remove-password-based-encryption-using-the-java-api}

使用Encryption API(Java)從PDF檔案移除密碼加密：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EncryptionServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得加密的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表加密PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 刪除密碼。

   調用物件的方法並傳遞下列值，以移除PDF `EncryptionServiceClient` 檔案中 `removePDFPasswordSecurity` 的密碼加密：

   * 包 `com.adobe.idp.Document` 含加密PDF檔案的物件。
   * 一個字串值，它指定用於從PDF文檔中刪除加密的主密碼值。
   此方 `removePDFPasswordSecurity` 法會傳回包 `com.adobe.idp.Document` 含不安全PDF檔案的物件。

1. 儲存PDF檔案。

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法，將物件的內容 `Document` 複製至檔案。 請確定您使用 `Document` 方法傳回的物 `removePDFPasswordSecurity` 件。

**另請參閱**

[快速入門（SOAP模式）:使用Java API移除密碼加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### 使用web service API移除密碼加密 {#remove-password-based-encryption-using-the-web-service-api}

使用Encryption API(web service)移除密碼型加密：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立加密服務客戶端。

   * 使用其 `EncryptionServiceClient` 預設建構函式建立物件。
   * 使用建 `EncryptionServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `EncryptionServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 此物 `BLOB` 件用於儲存密碼加密的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元 `BLOB` 組陣列的內容指派給物件的資料成員， `BLOB` 以填入 `MTOM` 物件。

1. 刪除密碼。

   叫用物 `EncryptionServiceService` 件的方 `removePDFPasswordSecurity` 法並傳遞下列值：

   * 包含 `BLOB` 代表加密PDF檔案之檔案串流資料的物件。
   * 一個字串值，它指定用於從PDF文檔中刪除加密的口令值。 此值是在使用密碼加密PDF文檔時指定的。
   此方 `removePDFPasswordSecurity` 法會傳回包 `BLOB` 含不安全PDF檔案的物件。

1. 儲存PDF檔案。

   * 調用 `System.IO.FileStream` 其建構函式並傳遞字串值，以建立物件，此字串值代表不安全PDF檔案的檔案位置。
   * 建立一個位元組陣列，該陣列儲存方 `BLOB` 法返回的對象的內 `removePDFPasswordSecurity` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 解鎖加密的PDF檔案 {#unlocking-encrypted-pdf-documents}

必須先解除鎖定密碼加密或憑證加密的PDF檔案，才能對其執行其他AEM Forms作業。 如果您嘗試對加密的PDF檔案執行操作，將會產生例外。 在解除鎖定加密的PDF檔案後，您可以對其執行一或多個操作。 這些作業可以屬於其他服務，例如Acrobat Reader DC擴充功能服務。

>[!NOTE]
>
>如需Encryption服務的詳細資訊，請參閱「AEM [表格的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

要解除鎖定加密的PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密服務客戶端。
1. 取得加密的PDF檔案。
1. 解除鎖定檔案。
1. 執行AEM Forms作業。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

**建立加密服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java Encryption Service API，請建立物 `EncrytionServiceClient` 件。 如果您使用web service Encryption Service API，請建立物 `EncryptionServiceService` 件。

**取得加密的PDF檔案**

您必須取得加密的PDF檔案，才能解除鎖定。 如果您嘗試解除鎖定未加密的PDF檔案，則會擲出例外。

**解除鎖定檔案**

若要解除鎖定密碼加密的PDF檔案，您需要加密的PDF檔案和用來開啟密碼加密的PDF檔案的密碼值。 此值是在使用密碼加密PDF文檔時指定的。 (請參 [閱使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

若要解除鎖定憑證加密的PDF檔案，您需要加密的PDF檔案，以及與用來加密PDF檔案的私密金鑰相對應的公開金鑰別名值。

**執行AEM Forms作業**

在解除鎖定加密的PDF檔案後，您可以對其執行其他服務操作，例如套用使用權。 此操作屬於Acrobat Reader DC Extensions服務。

**另請參閱**

[使用Java API解除鎖定加密的PDF檔案](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[使用web service API解除鎖定加密的PDF檔案](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API解除鎖定加密的PDF檔案 {#unlock-an-encrypted-pdf-document-using-the-java-api}

使用加密API(Java)解除鎖定加密的PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EncryptionServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得加密的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定加密PDF檔案位置的字串值，建立代表加密PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 解除鎖定檔案。

   叫用物件或方法，以解除 `EncryptionServiceClient` 鎖定加密的 `unlockPDFUsingPassword` PDF `unlockPDFUsingCredential` 檔案。

   若要解除鎖定使用密碼加密的PDF檔案，請叫用方 `unlockPDFUsingPassword` 法並傳遞下列值：

   * 包 `com.adobe.idp.Document` 含密碼加密PDF檔案的物件。
   * 一個字串值，它指定用於開啟密碼加密的PDF文檔的密碼值。 此值是在使用密碼加密PDF文檔時指定的。
   若要解除鎖定使用憑證加密的PDF檔案，請叫用 `unlockPDFUsingCredential` 方法並傳遞下列值：

   * 包 `com.adobe.idp.Document` 含憑證加密PDF檔案的物件。
   * 一個字串值，它指定與用於加密PDF文檔的私鑰相對應的公鑰的別名。
   這些 `unlockPDFUsingPassword` 和 `unlockPDFUsingCredential` 方法都會傳回您傳 `com.adobe.idp.Document` 遞至另一個AEM Forms java方法以執行作業的物件。

1. 執行AEM Forms作業。

   對解除鎖定的PDF檔案執行AEM Forms作業，以符合您的業務需求。 例如，假設您要將使用權套用至解除鎖定的PDF檔案，請將 `com.adobe.idp.Document` 由或方法傳回的物件 `unlockPDFUsingPassword``unlockPDFUsingCredential` 傳遞至物 `ReaderExtensionsServiceClient` 件的方 `applyUsageRights` 法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAP模式）解除加密的PDF檔案鎖定

[將使用權套用至PDF檔案](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API解除鎖定加密的PDF檔案 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

使用Encryption API(web service)解除鎖定加密的PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立加密服務客戶端。

   * 使用其 `EncryptionServiceClient` 預設建構函式建立物件。
   * 使用建 `EncryptionServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `EncryptionServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元 `BLOB` 組陣列的內容指派給物件的資料成員， `BLOB` 以填入 `MTOM` 物件。

1. 解除鎖定檔案。

   叫用物件或方法，以解除 `EncryptionServiceClient` 鎖定加密的 `unlockPDFUsingPassword` PDF `unlockPDFUsingCredential` 檔案。

   若要解除鎖定使用密碼加密的PDF檔案，請叫用方 `unlockPDFUsingPassword` 法並傳遞下列值：

   * 包 `BLOB` 含密碼加密PDF檔案的物件。
   * 一個字串值，它指定用於開啟密碼加密的PDF文檔的密碼值。 此值是在使用密碼加密PDF文檔時指定的。
   若要解除鎖定使用憑證加密的PDF檔案，請叫用 `unlockPDFUsingCredential` 方法並傳遞下列值：

   * 包 `BLOB` 含憑證加密PDF檔案的物件。
   * 一個字串值，它指定與用於加密PDf文檔的私鑰相對應的公鑰的別名。
   這些 `unlockPDFUsingPassword` 和方 `unlockPDFUsingCredential` 法都會傳回您 `com.adobe.idp.Document` 傳遞至其他AEM Forms方法以執行作業的物件。

1. 執行AEM Forms作業。

   對解除鎖定的PDF檔案執行AEM Forms作業，以符合您的業務需求。 例如，假設您要將使用權套用至解除鎖定的PDF檔案，請將 `BLOB` 或方法傳回的物件 `unlockPDFUsingPassword``unlockPDFUsingCredential` 傳遞 `ReaderExtensionsServiceClient` 至物件的方 `applyUsageRights` 法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 確定加密類型 {#determining-encryption-type}

您可以使用Java Encryption Service API或web service Encryption Service API，以程式設計方式決定要保護PDF檔案的加密類型。 有時需要動態判斷PDF檔案是否已加密，若已加密，則需要加密類型。 例如，您可以決定PDF檔案是使用密碼加密或Rights Management原則來保護。

PDF檔案可受下列加密類型保護：

* 密碼加密
* 憑證式加密
* 由Rights Management服務建立的策略
* 另一種加密

>[!NOTE]
>
>如需Encryption服務的詳細資訊，請參閱「AEM [表格的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

要確定保護PDF文檔的加密類型，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密服務客戶端。
1. 取得加密的PDF檔案。
1. 確定加密類型。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

**建立服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java Encryption Service API，請建立物 `EncrytionServiceClient` 件。 如果您使用web service Encryption Service API，請建立物 `EncryptionServiceService` 件。

**取得加密的PDF檔案**

您必須取得PDF檔案，以決定要保護它的加密類型。

**確定加密類型**

您可以決定保護PDF檔案的加密類型。 如果PDF檔案未受保護，則加密服務會通知您PDF檔案未受到保護。

**另請參閱**

[使用Java API確定加密類型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[使用web service API確定加密類型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用原則保護檔案](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### 使用Java API確定加密類型 {#determine-the-encryption-type-using-the-java-api}

使用Encryption API(Java)確定保護PDF檔案的加密類型：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立服務客戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EncryptionServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得加密的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，以建立代表PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 確定加密類型。

   * 調用物件的方法並傳 `EncryptionServiceClient` 遞包含PDF `getPDFEncryption` 檔案的物 `com.adobe.idp.Document` 件，以決定加密類型。 此方法返回對 `EncryptionTypeResult` 像。
   * 叫用 `EncryptionTypeResult` 物件的方 `getEncryptionType` 法。 此方法返回 `EncryptionType` 指定加密類型的枚舉值。 例如，如果PDF檔案受到密碼加密的保護，此方法會傳回 `EncryptionType.PASSWORD`。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API確定加密類型](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API確定加密類型 {#determine-the-encryption-type-using-the-web-service-api}

使用Encryption API(web service)確定保護PDF檔案的加密類型：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立服務客戶端。

   * 使用其 `EncryptionServiceClient` 預設建構函式建立物件。
   * 使用建 `EncryptionServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `EncryptionServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元 `BLOB` 組陣列的內容指派給物件的資料成員， `BLOB` 以填入 `MTOM` 物件。

1. 確定加密類型。

   * 叫用物 `EncryptionServiceClient` 件的方 `getPDFEncryption` 法，並傳 `BLOB` 遞包含PDF檔案的物件。 此方法返回對 `EncryptionTypeResult` 像。
   * 取得物件資 `EncryptionTypeResult` 料方法 `encryptionType` 的值。 例如，如果PDF檔案使用密碼加密進行保護，則此資料成員的值為 `EncryptionType.PASSWORD`。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)