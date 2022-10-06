---
title: 加密和解密PDF文檔
seo-title: Encrypting and Decrypting PDF Documents
description: 使用加密服務對文檔進行加密和解密。 該加密服務任務包括用密碼加密PDF文檔、用證書加密PDF文檔、從PDF文檔中刪除基於密碼的加密、從PDF文檔中刪除基於證書的加密、解鎖PDF文檔以便執行其他服務操作，以及確定安全PDF文檔的加密類型。
seo-description: Use the Encryption service to encrypt and decrypt documents. The Encryption service tasks include encrypting a PDF document with a password, encrypting a PDF document with a certificate, removing password-based encryption from a PDF document, removing certificate-based encryption from a PDF document, unlocking the PDF document so that other service operations can be performed, and determining the encryption type of a secured PDF document.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '8189'
ht-degree: 0%

---

# 加密和解密PDF文檔 {#encrypting-and-decrypting-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於加密服務**

加密服務可讓您加密和解密檔案。 文檔被加密後，其內容將變得不可讀。 授權用戶可以解密該文檔以獲得對內容的訪問。 如果使用密碼加密PDF文檔，則用戶必須指定開啟的密碼，然後才能在Adobe Reader或Adobe Acrobat中查看該文檔。 同樣，如果PDF文檔使用證書加密，則用戶必須使用與用於加密PDF文檔的證書（私鑰）相對應的公鑰對PDF文檔進行解密。

您可以使用加密服務完成以下任務：

* 使用密碼加密PDF文檔。 (請參閱 [使用密碼加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* 使用憑證加密PDF檔案。 (請參閱 [使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* 從PDF文檔中刪除基於密碼的加密。 (請參閱 [刪除密碼加密](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* 從PDF文檔中刪除基於證書的加密。 (請參閱 [刪除基於證書的加密](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* 解鎖PDF文檔，以便執行其他服務操作。 例如，在解除鎖定密碼加密的PDF文檔後，您可以對其應用數字簽名。 (請參閱 [解鎖加密的PDF文檔](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* 確定安全PDF文檔的加密類型。 (請參閱 [確定加密類型](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 使用密碼加密PDF文檔 {#encrypting-pdf-documents-with-a-password}

使用密碼加密PDF文檔時，用戶必須指定密碼以在Adobe Reader或Acrobat中開啟PDF文檔。 此外，在可以對文檔執行其他AEM Forms操作(例如對PDF文檔進行數字簽名)之前，必須解鎖密碼加密的PDF文檔。

>[!NOTE]
>
>如果您將加密的PDF檔案上傳至AEM Forms存放庫，該檔案將無法解密PDF檔案並擷取XDP內容。 建議您不要在將檔案上傳至AEM Forms存放庫前加密檔案。 (請參閱 [編寫資源](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要使用密碼加密PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密客戶端API對象。
1. 獲取要加密的PDF文檔。
1. 設定加密運行時選項。
1. 新增密碼。
1. 將加密的PDF文檔另存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

**建立加密客戶端API對象**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。

**獲取要加密的PDF文檔**

您必須獲取未加密的PDF文檔，才能使用密碼加密文檔。 如果您嘗試保護已加密的PDF文檔，則會導致異常。

**設定加密運行時選項**

要使用密碼加密PDF文檔，請指定四個值，包括兩個密碼值。 第一個密碼值用於加密PDF文檔，在開啟PDF文檔時必須指定。 第二個口令值（名為主口令值）用於從PDF文檔中刪除加密。 密碼值區分大小寫，且這兩個密碼值不能是相同的值。

必須指定要加密的PDF文檔資源。 您可以加密整個PDF文檔，除文檔元資料外的所有內容，或僅加密文檔的附件。 如果僅加密文檔的附件，則當用戶嘗試訪問檔案附件時，將提示用戶輸入密碼。

加密PDF文檔時，您可以指定與安全文檔關聯的權限。 通過指定權限，您可以控制開啟密碼加密PDF文檔的用戶可以執行的操作。 例如，若要成功擷取表單資料，您必須設定下列權限：

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>權限指定為 `PasswordEncryptionPermission` 枚舉值。

**新增密碼**

檢索不安全的PDF文檔並設定加密運行時值後，可以向PDF文檔添加密碼。

**將加密的PDF文檔另存為PDF檔案**

您可以將密碼加密的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[使用Web服務API加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### 使用Java API加密PDF檔案 {#encrypt-a-pdf-document-using-the-java-api}

使用加密API(Java)以密碼加密PDF文檔：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密客戶端API。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 獲取要加密的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示要加密的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 設定加密運行時選項。

   * 建立 `PasswordEncryptionOptionSpec` 對象，方法是調用其建構子。
   * 通過調用 `PasswordEncryptionOptionSpec` 物件 `setEncryptOption` 方法和傳遞 `PasswordEncryptionOption` 指定要加密的文檔資源的枚舉值。 例如，要加密整個PDF文檔，包括其元資料和附件，請指定 `PasswordEncryptionOption.ALL`.
   * 建立 `java.util.List` 使用 `ArrayList` 建構子。
   * 叫用 `java.util.List` 物件s `add` 方法，並傳遞符合您要設定之權限的列舉值。 例如，若要設定允許使用者複製PDF檔案中資料的權限，請指定 `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. （對要設定的每個權限重複此步驟）。
   * 叫用「 」以指定Acrobat相容性選項 `PasswordEncryptionOptionSpec` 物件 `setCompatability` 方法，並傳遞指定Acrobat相容性層級的列舉值。 例如，您可以指定 `PasswordEncryptionCompatability.ACRO_7`.
   * 指定密碼值，該密碼值允許用戶通過調用 `PasswordEncryptionOptionSpec` 物件 `setDocumentOpenPassword` 方法，並傳遞代表開啟密碼的字串值。
   * 指定主密碼值，該值允許用戶通過調用 `PasswordEncryptionOptionSpec` 物件 `setPermissionPassword` 方法，並傳遞代表主密碼的字串值。

1. 新增密碼。

   叫用以加密PDF檔案 `EncryptionServiceClient` 物件 `encryptPDFUsingPassword` 方法並傳遞下列值：

   * 此 `com.adobe.idp.Document` 包含要使用密碼加密的PDF文檔的對象。
   * 此 `PasswordEncryptionOptionSpec` 包含加密運行時選項的對象。

   此 `encryptPDFUsingPassword` 方法傳回 `com.adobe.idp.Document` 包含密碼加密PDF文檔的對象。

1. 將加密的PDF文檔另存為PDF檔案。

   * 建立 `java.io.File` 物件，並確定副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 物件。 請確定您使用 `com.adobe.idp.Document` 由傳回的物件 `encryptPDFUsingPassword` 方法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API加密PDF檔案](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API加密PDF文檔 {#encrypting-a-pdf-document-using-the-web-service-api}

使用加密API（Web服務）使用密碼加密PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立加密客戶端API對象。

   * 建立 `EncryptionServiceClient` 物件，使用其預設建構函式。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `EncryptionServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 獲取要加密的PDF文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存使用密碼加密的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示要加密的PDF文檔的檔案位置以及要開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，方法是將位元組陣列的內容指派給 `BLOB` 物件 `MTOM` 資料成員。

1. 設定加密運行時選項。

   * 建立 `PasswordEncryptionOptionSpec` 物件，使用其建構子。
   * 指定要加密的PDF文檔資源，方法是分配 `PasswordEncryptionOption` 枚舉值 `PasswordEncryptionOptionSpec` 物件 `encryptOption` 資料成員。 若要加密整個PDF，包括其中繼資料和附件，請指派 `PasswordEncryptionOption.ALL` 到此資料成員。
   * 指定Acrobat相容性選項，方法是指派 `PasswordEncryptionCompatability` 枚舉值 `PasswordEncryptionOptionSpec` 物件 `compatability` 資料成員。 例如，指派 `PasswordEncryptionCompatability.ACRO_7` 到此資料成員。
   * 指定密碼值，該密碼值允許用戶通過為分配代表開啟的密碼的字串值來開啟加密的PDF文檔 `PasswordEncryptionOptionSpec` 物件 `documentOpenPassword` 資料成員。
   * 指定密碼值，該密碼值允許用戶通過為PDF文檔分配代表主密碼的字串值來從密碼文檔中刪除加密 `PasswordEncryptionOptionSpec` 物件 `permissionPassword` 資料成員。

1. 新增密碼。

   叫用以加密PDF檔案 `EncryptionServiceClient` 物件 `encryptPDFUsingPassword` 方法並傳遞下列值：

   * 此 `BLOB` 包含要使用密碼加密的PDF文檔的對象。
   * 此 `PasswordEncryptionOptionSpec` 包含加密運行時選項的對象。

   此 `encryptPDFUsingPassword` 方法傳回 `BLOB` 包含密碼加密PDF文檔的對象。

1. 將加密的PDF文檔另存為PDF檔案。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示安全PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `encryptPDFUsingPassword` 方法。 取得 `BLOB` 物件 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 使用憑證加密PDF檔案 {#encrypting-pdf-documents-with-certificates}

憑證式加密可讓您透過公開金鑰技術為特定收件者加密檔案。 可以為文檔授予不同的收件者權限。 公鑰技術使加密的許多方面成為可能。 演算法可產生兩個大數，稱為 *鍵*，其中包含下列屬性：

* 一個密鑰用於加密一組資料。 隨後，只能使用其他密鑰來解密資料。
* 一個鍵和另一個鍵是無法區分的。

其中一個金鑰作為使用者的私密金鑰。 只有使用者才能存取此金鑰，這一點很重要。 另一個密鑰是使用者的公開密鑰，可與其他人共用。

公鑰證書包含用戶的公鑰和標識資訊。 X.509格式用於儲存憑證。 證書通常由證書頒發機構(CA)頒發並數字簽名，該機構是一個公認的實體，提供對證書有效性的信心度量。 憑證有到期日，之後即無效。 此外，證書吊銷清單(CRL)還提供有關在證書到期日之前被吊銷的證書的資訊。 證書頒發機構定期發佈CRL。 通過網路的線上證書狀態協定(OCSP)也可以檢索證書的吊銷狀態。

>[!NOTE]
>
>如果您將加密的PDF檔案上傳至AEM Forms存放庫，該檔案將無法解密PDF檔案並擷取XDP內容。 建議您不要在將檔案上傳至AEM Forms存放庫前加密檔案。 (請參閱 [編寫資源](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>您必須先確定將憑證新增至AEM Forms，才能使用憑證加密PDF檔案。 使用管理控制台或使用信任管理器API以程式設計方式新增憑證。 (請參閱 [使用信任管理器API導入憑據](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

要使用證書加密PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密客戶端API對象。
1. 獲取要加密的PDF文檔。
1. 參考憑證。
1. 設定加密運行時選項。
1. 建立憑證加密的PDF檔案。
1. 將加密的PDF文檔另存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

**建立加密客戶端API對象**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java加密服務API，請建立 `EncrytionServiceClient` 物件。 如果您使用Web服務加密服務API，請建立 `EncryptionServiceService` 物件。

**獲取要加密的PDF文檔**

您必須取得未加密的PDF檔案才能加密。 如果您嘗試保護已加密的PDF文檔，則會引發異常。

**參考憑證**

若要使用憑證加密PDF檔案，請參考用來加密PDF檔案的憑證。 憑證是.cer檔案、.crt檔案或.pem檔案。 PKCS#12檔案用於儲存具有相應證書的私鑰。

使用證書加密PDF文檔時，請指定與安全文檔相關聯的權限。 通過指定權限，您可以控制開啟證書加密PDF文檔的用戶可以執行的操作。

**設定加密運行時選項**

指定要加密的PDF文檔資源。 您可以加密整個PDF文檔、除文檔元資料之外的所有內容，或僅加密文檔的附件。

**建立憑證加密的PDF檔案**

擷取不安全的PDF檔案、參考憑證並設定執行時選項後，您可以建立憑證加密的PDF檔案。 PDF檔案加密後，您需要對應的公開金鑰才能解密。

**將加密的PDF文檔另存為PDF檔案**

您可以將加密的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[使用Web服務API使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API使用憑證加密PDF檔案 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

使用加密API(Java)使用憑證加密PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 獲取要加密的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示要加密的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 參考憑證。

   * 建立 `java.util.List` 使用其建構子儲存權限資訊的物件。
   * 通過調用 `java.util.List` 物件 `add` 方法和傳遞 `CertificateEncryptionPermissions` 表示授予開啟安全PDF文檔的用戶的權限的枚舉值。 例如，若要指定所有權限，請傳遞 `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * 建立 `Recipient` 物件，使用其建構子。
   * 建立 `java.io.FileInputStream` 表示用於加密PDF文檔的證書的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定證書的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 代表憑證的物件。
   * 叫用 `Recipient` 物件 `setX509Cert` 方法並傳遞 `com.adobe.idp.Document` 包含憑證的物件。 (此外，本 `Recipient`對象可以有Truststore證書別名或LDAP URL作為證書源。)
   * 建立 `CertificateEncryptionIdentity` 使用其建構子儲存權限和憑證資訊的物件。
   * 叫用 `CertificateEncryptionIdentity` 物件 `setPerms` 方法並傳遞 `java.util.List` 儲存權限資訊的物件。
   * 叫用 `CertificateEncryptionIdentity` 物件 `setRecipient` 方法並傳遞 `Recipient` 儲存憑證資訊的物件。
   * 建立 `java.util.List` 使用其建構子儲存憑證資訊的物件。
   * 叫用 `java.util.List` 物件的add方法，並傳遞 `CertificateEncryptionIdentity` 物件。 (此 `java.util.List` 物件會以參數的形式傳遞至 `encryptPDFUsingCertificates` 方法)。

1. 設定加密運行時選項。

   * 建立 `CertificateEncryptionOptionSpec` 對象，方法是調用其建構子。
   * 通過調用 `CertificateEncryptionOptionSpec` 物件 `setOption` 方法和傳遞 `CertificateEncryptionOption` 指定要加密的文檔資源的枚舉值。 例如，要加密整個PDF文檔，包括其元資料和附件，請指定 `CertificateEncryptionOption.ALL`.
   * 叫用「 」以指定Acrobat相容性選項 `CertificateEncryptionOptionSpec` 物件 `setCompat` 方法和傳遞 `CertificateEncryptionCompatibility` 指定Acrobat相容級別的枚舉值。 例如，您可以指定 `CertificateEncryptionCompatibility.ACRO_7`.

1. 建立憑證加密的PDF檔案。

   使用憑證加密PDF檔案，方法是叫用 `EncryptionServiceClient` 物件 `encryptPDFUsingCertificates` 方法並傳遞下列值：

   * 此 `com.adobe.idp.Document` 包含要加密的PDF文檔的對象。
   * 此 `java.util.List` 儲存憑證資訊的物件。
   * 此 `CertificateEncryptionOptionSpec` 包含加密運行時選項的對象。

   此 `encryptPDFUsingCertificates` 方法傳回 `com.adobe.idp.Document` 包含證書加密PDF文檔的對象。

1. 將加密的PDF文檔另存為PDF檔案。

   * 建立 `java.io.File` 物件，並確定副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 物件。 請確定您使用 `com.adobe.idp.Document` 由傳回的物件 `encryptPDFUsingCertificates` 方法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API使用憑證加密PDF檔案](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API使用憑證加密PDF檔案 {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

使用加密API（Web服務）使用憑證加密PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立加密客戶端API對象。

   * 建立 `EncryptionServiceClient` 物件，使用其預設建構函式。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `EncryptionServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 獲取要加密的PDF文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存使用證書加密的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示要加密的PDF文檔的檔案位置以及要開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性（包含位元組陣列的內容）。

1. 參考憑證。

   * 建立 `Recipient` 物件，使用其建構子。 此物件將儲存憑證資訊。
   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 物件會儲存加密PDF檔案的憑證。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式並傳遞字串值，該字串值代表憑證的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，方法是將位元組陣列的內容指派給 `BLOB` 物件 `MTOM` 資料成員。
   * 指派 `BLOB` 將憑證儲存至 `Recipient` 物件 `x509Cert` 資料成員。
   * 建立 `CertificateEncryptionIdentity` 使用其建構子儲存憑證資訊的物件。
   * 指派 `Recipient` 將憑證儲存至 `CertificateEncryptionIdentity`對象的收件人資料成員。
   * 建立 `Object` 陣列，並指派 `CertificateEncryptionIdentity` 物件至 `Object` 陣列。 此 `Object` 陣列會以參數的形式傳遞至 `encryptPDFUsingCertificates` 方法。

1. 設定加密運行時選項。

   * 建立 `CertificateEncryptionOptionSpec` 物件，使用其建構子。
   * 指定要加密的PDF文檔資源，方法是分配 `CertificateEncryptionOption` 枚舉值 `CertificateEncryptionOptionSpec` 物件 `option` 資料成員。 要加密整個PDF文檔，包括其元資料和附件，請分配 `CertificateEncryptionOption.ALL` 到此資料成員。
   * 指定Acrobat相容性選項，方法是指派 `CertificateEncryptionCompatibility` 枚舉值 `CertificateEncryptionOptionSpec` 物件 `compat` 資料成員。 例如，指派 `CertificateEncryptionCompatibility.ACRO_7` 到此資料成員。

1. 建立憑證加密的PDF檔案。

   使用憑證加密PDF檔案，方法是叫用 `EncryptionServiceService` 物件 `encryptPDFUsingCertificates` 方法並傳遞下列值：

   * 此 `BLOB` 包含要加密的PDF文檔的對象。
   * 此 `Object` 儲存憑證資訊的陣列。
   * 此 `CertificateEncryptionOptionSpec` 包含加密運行時選項的對象。

   此 `encryptPDFUsingCertificates` 方法傳回 `BLOB` 包含證書加密PDF文檔的對象。

1. 將加密的PDF文檔另存為PDF檔案。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示安全PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `encryptPDFUsingCertificates` 方法。 取得 `BLOB` 物件 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除基於證書的加密 {#removing-certificate-based-encryption}

可從PDF檔案中移除憑證式加密，讓使用者能在Adobe Reader或Acrobat中開啟PDF檔案。 若要從使用憑證加密的PDF檔案中移除加密，必須參考公開金鑰。 從PDF文檔中刪除加密後，加密將不再安全。

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-2}

要從PDF文檔中刪除基於證書的加密，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密服務客戶端。
1. 取得加密的PDF檔案。
1. 刪除加密。
1. 將PDF文檔另存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

**建立加密服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java加密服務API，請建立 `EncrytionServiceClient` 物件。 如果您使用Web服務加密服務API，請建立 `EncryptionServiceService` 物件。

**取得加密的PDF檔案**

您必須取得加密的PDF檔案，才能移除憑證式加密。 如果嘗試從未加密的PDF文檔中刪除加密，則會引發異常。 同樣，如果嘗試從密碼加密的文檔中刪除基於證書的加密，則會引發異常。

**刪除加密**

要從加密的PDF文檔中刪除基於證書的加密，您需要加密的PDF文檔和與用於加密PDF文檔的密鑰相對應的私鑰。 從加密的PDF文檔中刪除基於證書的加密時，指定私鑰的別名值。 如需公開金鑰的相關資訊，請參閱 [使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>私密金鑰儲存在AEM Forms信託存放區。 將證書放在該處時，將指定別名值。

**保存PDF文檔**

從加密的PDF文檔中刪除基於證書的加密後，您可以將PDF文檔另存為PDF檔案。 使用者可以在Adobe Reader或Acrobat中開啟PDF檔案。

**另請參閱**

[使用Java API移除憑證式加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[使用Web服務API刪除基於證書的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API移除憑證式加密 {#remove-certificate-based-encryption-using-the-java-api}

使用加密API(Java)從PDF文檔中刪除基於證書的加密：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 取得加密的PDF檔案。

   * 建立 `java.io.FileInputStream` 表示加密PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定加密PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 刪除加密。

   通過調用 `EncryptionServiceClient` 物件 `removePDFCertificateSecurity` 方法並傳遞下列值：

   * 此 `com.adobe.idp.Document` 包含加密PDF文檔的對象。
   * 一個字串值，它指定與用於加密PDf文檔的密鑰對應的私鑰的別名。

   此 `removePDFCertificateSecurity` 方法傳回 `com.adobe.idp.Document` 包含不安全PDF文檔的對象。

1. 保存PDF文檔。

   * 建立 `java.io.File` 物件，並確定副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 複製內容的方法 `Document` 物件。 請確定您使用 `com.adobe.idp.Document` 由傳回的物件 `removePDFCredentialSecurity` 方法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API移除憑證式加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API刪除基於證書的加密 {#remove-certificate-based-encryption-using-the-web-service-api}

使用加密API（Web服務）刪除基於證書的加密：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立加密服務客戶端。

   * 建立 `EncryptionServiceClient` 物件，使用其預設建構函式。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `EncryptionServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得加密的PDF檔案。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存加密的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，方法是將位元組陣列的內容指派給 `BLOB` 物件 `MTOM` 資料成員。

1. 刪除加密。

   叫用 `EncryptionServiceClient` 物件 `removePDFCertificateSecurity` 方法，並傳遞下列值：

   * 此 `BLOB` 包含代表加密PDF文檔的檔案流資料的對象。
   * 一個字串值，它指定與用於加密PDf文檔的私鑰相對應的公鑰的別名。

   此 `removePDFCredentialSecurity` 方法傳回 `BLOB` 包含不安全PDF文檔的對象。

1. 保存PDF文檔。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示不安全PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `removePDFPasswordSecurity` 方法。 取得 `BLOB` 物件 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除密碼加密 {#removing-password-encryption}

可以從PDF文檔中刪除基於密碼的加密，這樣用戶就可以在Adobe Reader或Acrobat中開啟PDF文檔，而無需指定密碼。 從PDF文檔中刪除基於密碼的加密後，該文檔將不再安全。

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-3}

要從PDF文檔中刪除基於密碼的加密，請執行以下步驟：

1. 包含項目檔案
1. 建立加密服務客戶端。
1. 取得加密的PDF檔案。
1. 刪除密碼。
1. 將PDF文檔另存為PDF檔案。

**包含項目檔案**

將必要的檔案納入您的開發專案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

**建立加密服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java加密服務API，請建立 `EncrytionServiceClient` 物件。 如果您使用Web服務加密服務API，請建立 `EncryptionServiceService` 物件。

**取得加密的PDF檔案**

必須獲取加密的PDF文檔，才能刪除基於密碼的加密。 如果嘗試從未加密的PDF文檔中刪除加密，則會引發異常。

**刪除密碼**

要從加密的PDF文檔中刪除基於密碼的加密，您需要加密的PDF文檔和用於從PDF文檔中刪除加密的主密碼值。 用於開啟密碼加密的PDF文檔的密碼不能用於刪除加密。 使用密碼加密PDF文檔時，指定主密碼。 (請參閱 [使用密碼加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**保存PDF文檔**

在PDF服務從PDF文檔中刪除基於密碼的加密後，您可以將加密文檔另存為PDF檔案。 使用者無需指定密碼，即可開啟Adobe Reader或Acrobat中的PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API刪除基於密碼的加密 {#remove-password-based-encryption-using-the-java-api}

使用加密API(Java)從PDF文檔中刪除基於密碼的加密：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 取得加密的PDF檔案。

   * 建立 `java.io.FileInputStream` 表示加密PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 刪除密碼。

   通過調用以下內容，從PDF文檔中刪除基於密碼的加密 `EncryptionServiceClient` 物件 `removePDFPasswordSecurity` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 包含加密PDF文檔的對象。
   * 一個字串值，它指定用於從PDF文檔中刪除加密的主密碼值。

   此 `removePDFPasswordSecurity` 方法傳回 `com.adobe.idp.Document` 包含不安全PDF文檔的對象。

1. 保存PDF文檔。

   * 建立 `java.io.File` 物件，並確定副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 複製內容的方法 `Document` 物件。 請確定您使用 `Document` 由傳回的物件 `removePDFPasswordSecurity` 方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API刪除基於密碼的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### 使用Web服務API刪除基於密碼的加密 {#remove-password-based-encryption-using-the-web-service-api}

使用加密API（Web服務）刪除基於密碼的加密：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立加密服務客戶端。

   * 建立 `EncryptionServiceClient` 物件，使用其預設建構函式。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `EncryptionServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得加密的PDF檔案。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存密碼加密的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，方法是將位元組陣列的內容指派給 `BLOB` 物件 `MTOM` 資料成員。

1. 刪除密碼。

   叫用 `EncryptionServiceService` 物件 `removePDFPasswordSecurity` 方法，並傳遞下列值：

   * 此 `BLOB` 包含代表加密PDF文檔的檔案流資料的對象。
   * 一個字串值，它指定用於從PDF文檔中刪除加密的密碼值。 使用密碼加密PDF文檔時，將指定此值。

   此 `removePDFPasswordSecurity` 方法傳回 `BLOB` 包含不安全PDF文檔的對象。

1. 保存PDF文檔。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示不安全PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `removePDFPasswordSecurity` 方法。 取得 `BLOB` 物件 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 解鎖加密的PDF文檔 {#unlocking-encrypted-pdf-documents}

必須先解除密碼加密或憑證加密的PDF檔案鎖定，然後才能對其執行其他AEM Forms操作。 如果嘗試對加密的PDF文檔執行操作，將生成異常。 解鎖加密的PDF文檔後，可以對其執行一個或多個操作。 這些作業可屬於其他服務，例如Acrobat Reader DC擴充功能服務。

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-4}

要解鎖加密的PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密服務客戶端。
1. 取得加密的PDF檔案。
1. 解鎖文檔。
1. 執行AEM Forms操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

**建立加密服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java加密服務API，請建立 `EncrytionServiceClient` 物件。 如果您使用Web服務加密服務API，請建立 `EncryptionServiceService` 物件。

**取得加密的PDF檔案**

您必須取得加密的PDF檔案才能將其解鎖。 如果嘗試解鎖未加密的PDF文檔，則會引發異常。

**解鎖文檔**

要解鎖密碼加密的PDF文檔，您需要加密的PDF文檔和用於開啟密碼加密的PDF文檔的密碼值。 使用密碼加密PDF文檔時，將指定此值。 (請參閱 [使用密碼加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

要解鎖證書加密的PDF文檔，您需要加密的PDF文檔和與用於加密PDF文檔的私鑰相對應的公鑰的別名值。

**執行AEM Forms操作**

加密的PDF文檔解除鎖定後，您可以對其執行其他服務操作，如應用使用權限。 此操作屬於Acrobat Reader DC擴充功能服務。

**另請參閱**

[使用Java API解除鎖定加密的PDF檔案](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[使用Web服務API解鎖加密的PDF文檔](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API解除鎖定加密的PDF檔案 {#unlock-an-encrypted-pdf-document-using-the-java-api}

使用加密API(Java)解鎖加密的PDF文檔：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 取得加密的PDF檔案。

   * 建立 `java.io.FileInputStream` 表示加密PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定加密PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 解鎖文檔。

   叫用 `EncryptionServiceClient` 物件 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 方法。

   要解鎖使用密碼加密的PDF文檔，請調用 `unlockPDFUsingPassword` 方法，並傳遞下列值：

   * A `com.adobe.idp.Document` 包含密碼加密PDF文檔的對象。
   * 一個字串值，它指定用於開啟密碼加密的PDF文檔的密碼值。 使用密碼加密PDF文檔時，將指定此值。

   若要解鎖使用憑證加密的PDF檔案，請叫用 `unlockPDFUsingCredential` 方法，並傳遞下列值：

   * A `com.adobe.idp.Document` 包含憑證加密PDF檔案的物件。
   * 一個字串值，它指定與用於加密PDF文檔的私鑰對應的公鑰的別名。

   此 `unlockPDFUsingPassword` 和 `unlockPDFUsingCredential` 方法都會傳回 `com.adobe.idp.Document` 物件，而您要傳遞至其他AEM Forms Java方法以執行操作。

1. 執行AEM Forms操作。

   對解鎖的PDF文檔執行AEM Forms操作，以滿足您的業務要求。 例如，假設您要將使用權限套用至解除鎖定的PDF檔案，請將 `com.adobe.idp.Document` 由 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 方法 `ReaderExtensionsServiceClient` 物件 `applyUsageRights` 方法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API解鎖加密的PDF文檔](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAP模式）

[將使用權應用於PDF文檔](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API解鎖加密的PDF文檔 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

使用加密API（Web服務）解鎖加密的PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立加密服務客戶端。

   * 建立 `EncryptionServiceClient` 物件，使用其預設建構函式。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `EncryptionServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得加密的PDF檔案。

   * 建立 `BLOB` 物件，使用其建構子。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，方法是將位元組陣列的內容指派給 `BLOB` 物件 `MTOM` 資料成員。

1. 解鎖文檔。

   叫用 `EncryptionServiceClient` 物件 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 方法。

   要解鎖使用密碼加密的PDF文檔，請調用 `unlockPDFUsingPassword` 方法，並傳遞下列值：

   * A `BLOB` 包含密碼加密PDF文檔的對象。
   * 一個字串值，它指定用於開啟密碼加密的PDF文檔的密碼值。 使用密碼加密PDF文檔時，將指定此值。

   若要解鎖使用憑證加密的PDF檔案，請叫用 `unlockPDFUsingCredential` 方法，並傳遞下列值：

   * A `BLOB` 包含憑證加密PDF檔案的物件。
   * 一個字串值，它指定與用於加密PDf文檔的私鑰相對應的公鑰的別名。

   此 `unlockPDFUsingPassword` 和 `unlockPDFUsingCredential` 方法都會傳回 `com.adobe.idp.Document` 物件，您傳遞至其他AEM Forms方法以執行操作。

1. 執行AEM Forms操作。

   對解鎖的PDF文檔執行AEM Forms操作，以滿足您的業務要求。 例如，假設您要將使用權限套用至解除鎖定的PDF檔案，請將 `BLOB` 由 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 方法 `ReaderExtensionsServiceClient` 物件 `applyUsageRights` 方法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 確定加密類型 {#determining-encryption-type}

您可以使用Java加密服務API或Web服務加密服務API，以程式設計方式確定要保護PDF文檔的加密類型。 有時需要動態確定PDF文檔是否加密，如果加密，則需要確定加密類型。 例如，您可以確定PDF文檔是使用基於密碼的加密保護還是使用Rights Management策略。

PDF文檔可以受以下加密類型的保護：

* 基於密碼的加密
* 基於證書的加密
* 由Rights Management服務建立的策略
* 另一種加密

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-5}

要確定保護PDF文檔的加密類型，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密服務客戶端。
1. 取得加密的PDF檔案。
1. 確定加密類型。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

**建立服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java加密服務API，請建立 `EncrytionServiceClient` 物件。 如果您使用Web服務加密服務API，請建立 `EncryptionServiceService` 物件。

**取得加密的PDF檔案**

必須獲取PDF文檔，以確定要保護加密的類型。

**確定加密類型**

您可以確定保護PDF文檔的加密類型。 如果PDF文檔未受保護，則加密服務會通知您PDF文檔未受保護。

**另請參閱**

[使用Java API確定加密類型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[使用Web服務API確定加密類型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用策略保護文檔](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### 使用Java API確定加密類型 {#determine-the-encryption-type-using-the-java-api}

使用加密API(Java)確定保護PDF文檔的加密類型：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立服務客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 取得加密的PDF檔案。

   * 建立 `java.io.FileInputStream` 表示PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 確定加密類型。

   * 通過調用 `EncryptionServiceClient` 物件 `getPDFEncryption` 方法和傳遞 `com.adobe.idp.Document` 包含PDF文檔的對象。 此方法會傳回 `EncryptionTypeResult` 物件。
   * 叫用 `EncryptionTypeResult` 物件 `getEncryptionType` 方法。 此方法會傳回 `EncryptionType` 指定加密類型的枚舉值。 例如，如果PDF文檔受基於密碼的加密保護，則此方法將返回 `EncryptionType.PASSWORD`.

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API確定加密類型](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API確定加密類型 {#determine-the-encryption-type-using-the-web-service-api}

使用加密API（Web服務）確定保護PDF文檔的加密類型：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立服務客戶端。

   * 建立 `EncryptionServiceClient` 物件，使用其預設建構函式。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `EncryptionServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得加密的PDF檔案。

   * 建立 `BLOB` 物件，使用其建構子。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，方法是將位元組陣列的內容指派給 `BLOB` 物件 `MTOM` 資料成員。

1. 確定加密類型。

   * 叫用 `EncryptionServiceClient` 物件 `getPDFEncryption` 方法並傳遞 `BLOB` 包含PDF文檔的對象。 此方法會傳回 `EncryptionTypeResult` 物件。
   * 取得 `EncryptionTypeResult` 物件 `encryptionType` 資料方法。 例如，如果PDF文檔受基於密碼的加密保護，則此資料成員的值為 `EncryptionType.PASSWORD`.

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
