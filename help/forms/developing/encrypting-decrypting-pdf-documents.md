---
title: 加密和解密PDF文檔
seo-title: Encrypting and Decrypting PDF Documents
description: 使用加密服務對文檔進行加密和解密。 加密服務任務包括用密碼加密PDF文檔、用證書加密PDF文檔、從PDF文檔中刪除基於密碼的加密、從PDF文檔中刪除基於證書的加密、解鎖PDF文檔以便能夠執行其他服務操作以及確定安全PDF文檔的加密類型。
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

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於加密服務**

加密服務允許您加密和解密文檔。 當文檔被加密時，其內容將變得不可讀。 授權用戶可解密文檔以獲得對內容的訪問。 如果PDF文檔使用密碼進行加密，則用戶必須指定開啟的密碼，然後才能在Adobe Reader或Adobe Acrobat查看該文檔。 同樣，如果PDF文檔用證書加密，則用戶必須使用與用於加密PDF文檔的證書（私鑰）對應的公鑰來解密PDF文檔。

您可以使用加密服務完成以下任務：

* 使用密碼加密PDF文檔。 (請參閱 [使用密碼加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)
* 使用證書加密PDF文檔。 (請參閱 [使用證書加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。)
* 從PDF文檔中刪除基於密碼的加密。 (請參閱 [刪除密碼加密](encrypting-decrypting-pdf-documents.md#removing-password-encryption)。)
* 從PDF文檔中刪除基於證書的加密。 (請參閱 [刪除基於證書的加密](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)。)
* 解鎖PDF文檔，以便可以執行其他服務操作。 例如，在解鎖密碼加密的PDF文檔後，您可以對其應用數字簽名。 (請參閱 [解鎖加密PDF文檔](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)。)
* 確定安全PDF文檔的加密類型。 (請參閱 [確定加密類型](encrypting-decrypting-pdf-documents.md#determining-encryption-type)。)

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 使用密碼加密PDF文檔 {#encrypting-pdf-documents-with-a-password}

使用密碼加密PDF文檔時，用戶必須指定密碼才能在Adobe Reader或Acrobat開啟PDF文檔。 此外，在對文檔執行諸如對PDF文檔進行數字簽名的另一個AEM Forms操作之前，必須解鎖密碼加密的PDF文檔。

>[!NOTE]
>
>如果將加密的PDF文檔上載到AEM Forms儲存庫，則無法解密PDF文檔並提取XDP內容。 建議在將文檔上載到AEM Forms儲存庫之前不要對其進行加密。 (請參閱 [編寫資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。)

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要使用密碼加密PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立加密客戶端API對象。
1. 獲取要加密的PDF文檔。
1. 設定加密運行時選項。
1. 添加密碼。
1. 將加密的PDF文檔另存為PDF檔案。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

**建立加密客戶端API對象**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。

**獲取要加密的PDF文檔**

必須獲取未加密的PDF文檔，才能使用密碼對文檔進行加密。 如果嘗試保護已加密的PDF文檔，將導致異常。

**設定加密運行時選項**

要使用口令加密PDF文檔，請指定四個值，包括兩個口令值。 第一個密碼值用於加密PDF文檔，並且在開啟PDF文檔時必須指定。 第二個口令值（稱為主口令值）用於從PDF文檔中刪除加密。 密碼值區分大小寫，這兩個密碼值不能是相同的值。

必須指定要加密的PDF文檔資源。 您可以加密整個PDF文檔、除文檔元資料之外的所有內容，或僅加密文檔的附件。 如果僅加密文檔的附件，則當用戶嘗試訪問檔案附件時，系統會提示用戶輸入密碼。

加密PDF文檔時，可以指定與安全文檔關聯的權限。 通過指定權限，您可以控制開啟密碼加密PDF文檔的用戶允許執行的操作。 例如，要成功提取表單資料，必須設定以下權限：

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>權限指定為 `PasswordEncryptionPermission` 枚舉值。

**添加密碼**

檢索不安全的PDF文檔並設定加密運行時值後，可以向PDF文檔添加密碼。

**將加密的PDF文檔另存為PDF檔案**

可以將密碼加密的PDF文檔另存為PDF檔案。

**另請參閱**

[使用Java API加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[使用Web服務API加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速啟動](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用證書加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### 使用Java API加密PDF文檔 {#encrypt-a-pdf-document-using-the-java-api}

使用Encryption API(Java)使用口令加密PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-encryption-client.jar。

1. 建立加密客戶端API。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取要加密的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示要加密的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定加密運行時選項。

   * 建立 `PasswordEncryptionOptionSpec` 調用其建構子。
   * 通過調用要加密的PDF文檔資源 `PasswordEncryptionOptionSpec` 對象 `setEncryptOption` 方法和通過 `PasswordEncryptionOption` 指定要加密的文檔資源的枚舉值。 例如，要加密整個PDF文檔，包括其元資料及其附件，請指定 `PasswordEncryptionOption.ALL`。
   * 建立 `java.util.List` 使用 `ArrayList` 建構子。
   * 通過調用 `java.util.List` 對象s `add` 方法，並傳遞與要設定的權限對應的枚舉值。 例如，要設定允許用戶複製位於PDF文檔中的資料的權限，請指定 `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`。 （對要設定的每個權限重複此步驟）。
   * 通過調用 `PasswordEncryptionOptionSpec` 對象 `setCompatability` 方法，並傳遞指定Acrobat相容性級別的枚舉值。 例如，可以指定 `PasswordEncryptionCompatability.ACRO_7`。
   * 指定口令值，該口令值允許用戶通過調用 `PasswordEncryptionOptionSpec` 對象 `setDocumentOpenPassword` 方法，並傳遞表示開啟口令的字串值。
   * 指定主密碼值，該值允許用戶通過調用PDF文檔刪除加密 `PasswordEncryptionOptionSpec` 對象 `setPermissionPassword` 和傳遞表示主密碼的字串值。

1. 添加密碼。

   通過調用PDF文檔 `EncryptionServiceClient` 對象 `encryptPDFUsingPassword` 方法並傳遞以下值：

   * 的 `com.adobe.idp.Document` 包含要用密碼加密的PDF文檔的對象。
   * 的 `PasswordEncryptionOptionSpec` 包含加密運行時選項的對象。

   的 `encryptPDFUsingPassword` 方法返回 `com.adobe.idp.Document` 包含密碼加密PDF文檔的對象。

1. 將加密的PDF文檔另存為PDF檔案。

   * 建立 `java.io.File` 並確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象。 確保使用 `com.adobe.idp.Document` 返回的對象 `encryptPDFUsingPassword` 的雙曲餘切值。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API加密PDF文檔](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API加密PDF文檔 {#encrypting-a-pdf-document-using-the-web-service-api}

使用Encryption API（Web服務）使用密碼加密PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立加密客戶端API對象。

   * 建立 `EncryptionServiceClient` 對象。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `EncryptionServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取要加密的PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` object用於儲存使用密碼加密的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 對象，方法是將位元組陣列的內容分配給 `BLOB` 對象 `MTOM` 資料成員。

1. 設定加密運行時選項。

   * 建立 `PasswordEncryptionOptionSpec` 對象。
   * 通過分配PDF文檔資源來指定要加密的 `PasswordEncryptionOption` 枚舉值 `PasswordEncryptionOptionSpec` 對象 `encryptOption` 資料成員。 要加密整個PDF，包括其元資料及其附件，請分配 `PasswordEncryptionOption.ALL` 到此資料成員。
   * 通過指定 `PasswordEncryptionCompatability` 枚舉值 `PasswordEncryptionOptionSpec` 對象 `compatability` 資料成員。 例如，分配 `PasswordEncryptionCompatability.ACRO_7` 到此資料成員。
   * 指定口令值，該口令值允許用戶通過將表示開啟口令的字串值分配給 `PasswordEncryptionOptionSpec` 對象 `documentOpenPassword` 資料成員。
   * 指定口令值，該口令值允許用戶通過為PDF文檔指定表示主口令的字串值來刪除加密 `PasswordEncryptionOptionSpec` 對象 `permissionPassword` 資料成員。

1. 添加密碼。

   通過調用PDF文檔 `EncryptionServiceClient` 對象 `encryptPDFUsingPassword` 方法並傳遞以下值：

   * 的 `BLOB` 包含要用密碼加密的PDF文檔的對象。
   * 的 `PasswordEncryptionOptionSpec` 包含加密運行時選項的對象。

   的 `encryptPDFUsingPassword` 方法返回 `BLOB` 包含密碼加密PDF文檔的對象。

1. 將加密的PDF文檔另存為PDF檔案。

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示安全PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `encryptPDFUsingPassword` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 使用證書加密PDF文檔 {#encrypting-pdf-documents-with-certificates}

基於證書的加密允許您通過公鑰技術為特定收件人加密文檔。 可以為文檔授予不同的權限。 公鑰技術使加密的許多方面成為可能。 算法用於生成兩個大數，稱為 *鍵*，具有以下屬性：

* 一個密鑰用於加密一組資料。 隨後，只能使用其他密鑰解密資料。
* 一把鑰匙和另一把鑰匙是無法區分的。

其中一個密鑰用作用戶的私鑰。 只有用戶才能訪問此密鑰，這一點非常重要。 另一個密鑰是用戶的公鑰，可以與他人共用。

公鑰證書包含用戶的公鑰和標識資訊。 X.509格式用於儲存證書。 證書通常由證書頒發機構(CA)頒發和數字簽名，該機構是一個被認可的實體，提供對證書有效性的信任度。 證書的到期日期已過，在此日期之後，證書不再有效。 此外，證書吊銷清單(CRL)提供了在證書過期之前已吊銷的證書的資訊。 CRL由證書頒發機構定期發佈。 還可以通過網路通過線上證書狀態協定(OCSP)檢索證書的吊銷狀態。

>[!NOTE]
>
>如果將加密的PDF文檔上載到AEM Forms儲存庫，則無法解密PDF文檔並提取XDP內容。 建議在將文檔上載到AEM Forms儲存庫之前不要對其進行加密。 (請參閱 [編寫資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。)

>[!NOTE]
>
>在使用證書加密PDF文檔之前，必須確保將證書添加到AEM Forms。 證書是使用管理控制台或使用Trust Manager API以寫程式方式添加的。 (請參閱 [使用Trust Manager API導入憑據](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。)

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要使用證書加密PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立加密客戶端API對象。
1. 獲取要加密的PDF文檔。
1. 引用證書。
1. 設定加密運行時選項。
1. 建立證書加密的PDF文檔。
1. 將加密的PDF文檔另存為PDF檔案。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

**建立加密客戶端API對象**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果使用Java加密服務API，請建立 `EncrytionServiceClient` 的雙曲餘切值。 如果使用Web服務加密服務API，請建立 `EncryptionServiceService` 的雙曲餘切值。

**獲取要加密的PDF文檔**

必須獲取未加密的PDF文檔才能加密。 如果嘗試保護已加密的PDF文檔，則會引發異常。

**引用證書**

要使用證書加密PDF文檔，請引用用於加密PDF文檔的證書。 證書是.cer檔案、.crt檔案或.pem檔案。 PKCS#12檔案用於儲存具有相應證書的私鑰。

使用證書加密PDF文檔時，指定與安全文檔關聯的權限。 通過指定權限，您可以控制開啟證書加密PDF文檔的用戶可以執行的操作。

**設定加密運行時選項**

指定要加密的PDF文檔資源。 您可以加密整個PDF文檔、除文檔元資料之外的所有內容，或僅加密文檔的附件。

**建立證書加密的PDF文檔**

檢索不安全的PDF文檔、引用證書並設定運行時選項後，可以建立證書加密的PDF文檔。 PDF文檔被加密後，需要相應的公鑰來解密它。

**將加密的PDF文檔另存為PDF檔案**

可以將加密的PDF文檔另存為PDF檔案。

**另請參閱**

[使用Java API使用證書加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[使用Web服務API使用證書加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速啟動](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API使用證書加密PDF文檔 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

使用Encryption API(Java)使用證書加密PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-encryption-client.jar。

1. 建立加密客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取要加密的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示要加密的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 引用證書。

   * 建立 `java.util.List` 使用其建構子儲存權限資訊的對象。
   * 通過調用 `java.util.List` 對象 `add` 方法和通過 `CertificateEncryptionPermissions` 表示授予開啟安全PDF文檔的用戶的權限的枚舉值。 例如，要指定所有權限，請傳遞 `CertificateEncryptionPermissions.PKI_ALL_PERM`。
   * 建立 `Recipient` 對象。
   * 建立 `java.io.FileInputStream` 對象，該對象表示使用PDF文檔的建構子並傳遞一個字串值，指定證書的位置，用於加密該文檔。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 表示證書的對象。
   * 調用 `Recipient` 對象 `setX509Cert` 方法和通過 `com.adobe.idp.Document` 包含證書的對象。 (此外，本集團 `Recipient`對象可以將Truststore證書別名或LDAP URL作為證書源。)
   * 建立 `CertificateEncryptionIdentity` 使用其建構子儲存權限和證書資訊的對象。
   * 調用 `CertificateEncryptionIdentity` 對象 `setPerms` 方法和通過 `java.util.List` 儲存權限資訊的對象。
   * 調用 `CertificateEncryptionIdentity` 對象 `setRecipient` 方法和通過 `Recipient` 儲存證書資訊的對象。
   * 建立 `java.util.List` 使用其建構子儲存證書資訊的對象。
   * 調用 `java.util.List` 對象的add方法並傳遞 `CertificateEncryptionIdentity` 的雙曲餘切值。 (此 `java.util.List` 對象作為參數傳遞給 `encryptPDFUsingCertificates` )。

1. 設定加密運行時選項。

   * 建立 `CertificateEncryptionOptionSpec` 調用其建構子。
   * 通過調用要加密的PDF文檔資源 `CertificateEncryptionOptionSpec` 對象 `setOption` 方法和通過 `CertificateEncryptionOption` 指定要加密的文檔資源的枚舉值。 例如，要加密整個PDF文檔，包括其元資料及其附件，請指定 `CertificateEncryptionOption.ALL`。
   * 通過調用 `CertificateEncryptionOptionSpec` 對象 `setCompat` 方法和通過 `CertificateEncryptionCompatibility` 指定Acrobat相容性級別的枚舉值。 例如，可以指定 `CertificateEncryptionCompatibility.ACRO_7`。

1. 建立證書加密的PDF文檔。

   通過調用PDF `EncryptionServiceClient` 對象 `encryptPDFUsingCertificates` 方法並傳遞以下值：

   * 的 `com.adobe.idp.Document` 包含要加密的PDF文檔的對象。
   * 的 `java.util.List` 儲存證書資訊的對象。
   * 的 `CertificateEncryptionOptionSpec` 包含加密運行時選項的對象。

   的 `encryptPDFUsingCertificates` 方法返回 `com.adobe.idp.Document` 包含證書加密PDF文檔的對象。

1. 將加密的PDF文檔另存為PDF檔案。

   * 建立 `java.io.File` 對象，並確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象。 確保使用 `com.adobe.idp.Document` 返回的對象 `encryptPDFUsingCertificates` 的雙曲餘切值。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API使用證書加密PDF文檔](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API使用證書加密PDF文檔 {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

使用加密API（Web服務）使用證書加密PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立加密客戶端API對象。

   * 建立 `EncryptionServiceClient` 對象。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `EncryptionServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取要加密的PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存用證書加密的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 引用證書。

   * 建立 `Recipient` 對象。 此對象將儲存證書資訊。
   * 建立 `BLOB` 對象。 此 `BLOB` 對象將儲存加密PDF文檔的證書。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示證書的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 對象，方法是將位元組陣列的內容分配給 `BLOB` 對象 `MTOM` 資料成員。
   * 分配 `BLOB` 將證書儲存到 `Recipient` 對象 `x509Cert` 資料成員。
   * 建立 `CertificateEncryptionIdentity` 使用其建構子儲存證書資訊的對象。
   * 分配 `Recipient` 將證書儲存到 `CertificateEncryptionIdentity`對象的收件人資料成員。
   * 建立 `Object` 陣列並分配 `CertificateEncryptionIdentity` 對象到 `Object` 陣列。 此 `Object` 陣列作為參數傳遞給 `encryptPDFUsingCertificates` 的雙曲餘切值。

1. 設定加密運行時選項。

   * 建立 `CertificateEncryptionOptionSpec` 對象。
   * 通過分配PDF文檔資源來指定要加密的 `CertificateEncryptionOption` 枚舉值 `CertificateEncryptionOptionSpec` 對象 `option` 資料成員。 要加密整個PDF文檔，包括其元資料及其附件，請分配 `CertificateEncryptionOption.ALL` 到此資料成員。
   * 通過指定 `CertificateEncryptionCompatibility` 枚舉值 `CertificateEncryptionOptionSpec` 對象 `compat` 資料成員。 例如，分配 `CertificateEncryptionCompatibility.ACRO_7` 到此資料成員。

1. 建立證書加密的PDF文檔。

   通過調用PDF `EncryptionServiceService` 對象 `encryptPDFUsingCertificates` 方法並傳遞以下值：

   * 的 `BLOB` 包含要加密的PDF文檔的對象。
   * 的 `Object` 儲存證書資訊的陣列。
   * 的 `CertificateEncryptionOptionSpec` 包含加密運行時選項的對象。

   的 `encryptPDFUsingCertificates` 方法返回 `BLOB` 包含證書加密PDF文檔的對象。

1. 將加密的PDF文檔另存為PDF檔案。

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示安全PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `encryptPDFUsingCertificates` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除基於證書的加密 {#removing-certificate-based-encryption}

可以從PDF文檔中刪除基於證書的加密，以便用戶可以在Adobe Reader或Acrobat開啟PDF文檔。 要從使用證書加密的PDF文檔中刪除加密，必須引用公鑰。 從PDF文檔中刪除加密後，它不再安全。

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

要從PDF文檔中刪除基於證書的加密，請執行以下步驟：

1. 包括項目檔案。
1. 建立加密服務客戶端。
1. 獲取加密的PDF文檔。
1. 刪除加密。
1. 將PDF文檔另存為PDF檔案。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

**建立加密服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果使用Java加密服務API，請建立 `EncrytionServiceClient` 的雙曲餘切值。 如果使用Web服務加密服務API，請建立 `EncryptionServiceService` 的雙曲餘切值。

**獲取加密的PDF文檔**

必須獲取加密的PDF文檔才能刪除基於證書的加密。 如果嘗試從未加密的PDF文檔中刪除加密，則會引發異常。 同樣，如果嘗試從密碼加密文檔中刪除基於證書的加密，則會引發異常。

**刪除加密**

要從加密的PDF文檔中刪除基於證書的加密，您需要加密的PDF文檔和與用於加密PDF文檔的密鑰對應的私鑰。 在從加密的PDF文檔中刪除基於證書的加密時指定私鑰的別名值。 有關公鑰的資訊，請參見 [使用證書加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。

>[!NOTE]
>
>私鑰儲存在AEM Forms信託商店中。 將證書放在那裡時，將指定別名值。

**保存PDF文檔**

在從加密的PDF文檔中刪除基於證書的加密後，可以將PDF文檔另存為PDF檔案。 用戶可以在Adobe Reader或Acrobat開啟PDF文檔。

**另請參閱**

[使用Java API刪除基於證書的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[使用Web服務API刪除基於證書的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速啟動](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API刪除基於證書的加密 {#remove-certificate-based-encryption-using-the-java-api}

使用Encryption API(Java)從PDF文檔中刪除基於證書的加密：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取加密的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示加密PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定加密PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 刪除加密。

   通過調用PDF文檔來刪除基於證書的加密 `EncryptionServiceClient` 對象 `removePDFCertificateSecurity` 方法並傳遞以下值：

   * 的 `com.adobe.idp.Document` 包含加密PDF文檔的對象。
   * 一個字串值，它指定與用於加密PDf文檔的密鑰相對應的私鑰的別名。

   的 `removePDFCertificateSecurity` 方法返回 `com.adobe.idp.Document` 包含不安全PDF文檔的對象。

1. 保存PDF文檔。

   * 建立 `java.io.File` 並確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象。 確保使用 `com.adobe.idp.Document` 返回的對象 `removePDFCredentialSecurity` 的雙曲餘切值。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API刪除基於證書的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API刪除基於證書的加密 {#remove-certificate-based-encryption-using-the-web-service-api}

使用Encryption API（Web服務）刪除基於證書的加密：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立加密服務客戶端。

   * 建立 `EncryptionServiceClient` 對象。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `EncryptionServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取加密的PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存加密的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 對象，方法是將位元組陣列的內容分配給 `BLOB` 對象 `MTOM` 資料成員。

1. 刪除加密。

   調用 `EncryptionServiceClient` 對象 `removePDFCertificateSecurity` 方法並傳遞以下值：

   * 的 `BLOB` 包含表示加密PDF文檔的檔案流資料的對象。
   * 一個字串值，它指定與用於加密PDf文檔的私鑰相對應的公鑰的別名。

   的 `removePDFCredentialSecurity` 方法返回 `BLOB` 包含不安全PDF文檔的對象。

1. 保存PDF文檔。

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示不安全PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `removePDFPasswordSecurity` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除密碼加密 {#removing-password-encryption}

可以從PDF文檔中刪除基於密碼的加密，以便用戶可以在Adobe Reader或Acrobat開啟PDF文檔，而無需指定密碼。 從PDF文檔中刪除基於密碼的加密後，文檔不再安全。

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

要從PDF文檔中刪除基於密碼的加密，請執行以下步驟：

1. 包括項目檔案
1. 建立加密服務客戶端。
1. 獲取加密的PDF文檔。
1. 刪除密碼。
1. 將PDF文檔另存為PDF檔案。

**包括項目檔案**

將必要的檔案包括到您的開發項目中。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

**建立加密服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果使用Java加密服務API，請建立 `EncrytionServiceClient` 的雙曲餘切值。 如果使用Web服務加密服務API，請建立 `EncryptionServiceService` 的雙曲餘切值。

**獲取加密的PDF文檔**

必須獲取加密的PDF文檔才能刪除基於密碼的加密。 如果嘗試從未加密的PDF文檔中刪除加密，則會引發異常。

**刪除密碼**

要從加密的PDF文檔中刪除基於密碼的加密，您需要加密的PDF文檔和用於從PDF文檔中刪除加密的主密碼值。 用於開啟密碼加密PDF文檔的密碼不能用於刪除加密。 使用密碼對PDF文檔進行加密時指定主密碼。 (請參閱 [使用密碼加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

**保存PDF文檔**

在加密服務從PDF文檔中刪除基於密碼的加密後，您可以將PDF文檔另存為PDF檔案。 用戶可以在Adobe Reader或Acrobat開啟PDF文檔，而無需指定密碼。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速啟動](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API刪除基於密碼的加密 {#remove-password-based-encryption-using-the-java-api}

使用Encryption API(Java)從PDF文檔中刪除基於密碼的加密：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取加密的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示加密PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 刪除密碼。

   通過調用PDF文檔來刪除基於密碼的加密 `EncryptionServiceClient` 對象 `removePDFPasswordSecurity` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 包含加密PDF文檔的對象。
   * 一個字串值，它指定用於從PDF文檔中刪除加密的主密碼值。

   的 `removePDFPasswordSecurity` 方法返回 `com.adobe.idp.Document` 包含不安全PDF文檔的對象。

1. 保存PDF文檔。

   * 建立 `java.io.File` 對象，並確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象。 確保使用 `Document` 返回的對象 `removePDFPasswordSecurity` 的雙曲餘切值。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API刪除基於密碼的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### 使用Web服務API刪除基於密碼的加密 {#remove-password-based-encryption-using-the-web-service-api}

使用Encryption API（Web服務）刪除基於密碼的加密：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立加密服務客戶端。

   * 建立 `EncryptionServiceClient` 對象。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `EncryptionServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取加密的PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存密碼加密的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 對象，方法是將位元組陣列的內容分配給 `BLOB` 對象 `MTOM` 資料成員。

1. 刪除密碼。

   調用 `EncryptionServiceService` 對象 `removePDFPasswordSecurity` 方法並傳遞以下值：

   * 的 `BLOB` 包含表示加密PDF文檔的檔案流資料的對象。
   * 一個字串值，它指定用於從PDF文檔中刪除加密的密碼值。 使用密碼加密PDF文檔時指定此值。

   的 `removePDFPasswordSecurity` 方法返回 `BLOB` 包含不安全PDF文檔的對象。

1. 保存PDF文檔。

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示不安全PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `removePDFPasswordSecurity` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 解鎖加密PDF文檔 {#unlocking-encrypted-pdf-documents}

必須解鎖密碼加密或證書加密的PDF文檔，然後才能對其執行其他AEM Forms操作。 如果嘗試對加密的PDF文檔執行操作，將生成異常。 解鎖加密的PDF文檔後，可以對其執行一個或多個操作。 這些操作可以屬於其他服務，如Acrobat Reader DC分機處。

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

要解鎖加密的PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立加密服務客戶端。
1. 獲取加密的PDF文檔。
1. 解鎖文檔。
1. 執行AEM Forms操作。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

**建立加密服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果使用Java加密服務API，請建立 `EncrytionServiceClient` 的雙曲餘切值。 如果使用Web服務加密服務API，請建立 `EncryptionServiceService` 的雙曲餘切值。

**獲取加密的PDF文檔**

必須獲取加密的PDF文檔才能將其解鎖。 如果嘗試解鎖未加密的PDF文檔，則會引發異常。

**解鎖文檔**

要解鎖密碼加密的PDF文檔，您需要加密的PDF文檔和用於開啟密碼加密的PDF文檔的密碼值。 使用密碼加密PDF文檔時指定此值。 (請參閱 [使用密碼加密PDF文檔](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

要解鎖證書加密的PDF文檔，您需要加密的PDF文檔和與用於加密PDF文檔的私鑰對應的公鑰的別名值。

**執行AEM Forms操作**

解鎖加密的PDF文檔後，您可以對其執行其他服務操作，如對其應用使用權限。 此操作屬於Acrobat Reader DC分機服務。

**另請參閱**

[使用Java API解鎖加密的PDF文檔](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[使用Web服務API解鎖加密的PDF文檔](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速啟動](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API解鎖加密的PDF文檔 {#unlock-an-encrypted-pdf-document-using-the-java-api}

使用Encryption API(Java)解鎖加密的PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取加密的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示加密PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定加密PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 解鎖文檔。

   通過調用 `EncryptionServiceClient` 對象 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 的雙曲餘切值。

   要解鎖使用密碼加密的PDF文檔，請調用 `unlockPDFUsingPassword` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 包含密碼加密PDF文檔的對象。
   * 一個字串值，它指定用於開啟密碼加密的PDF文檔的密碼值。 使用密碼加密PDF文檔時指定此值。

   要解鎖使用證書加密的PDF文檔，請調用 `unlockPDFUsingCredential` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 包含證書加密PDF文檔的對象。
   * 一個字串值，它指定與用於加密PDF文檔的私鑰相對應的公鑰的別名。

   的 `unlockPDFUsingPassword` 和 `unlockPDFUsingCredential` 方法都返回 `com.adobe.idp.Document` 傳遞給另一個AEM FormsJava方法以執行操作的對象。

1. 執行AEM Forms操作。

   對解鎖的PDF文檔執行AEM Forms操作，以滿足您的業務要求。 例如，假定要將使用權限應用於未鎖定的PDF文檔，請將 `com.adobe.idp.Document` 由其中一個 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 方法 `ReaderExtensionsServiceClient` 對象 `applyUsageRights` 的雙曲餘切值。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API解鎖加密PDF文檔](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAP模式）

[將使用權限應用於PDF文檔](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API解鎖加密的PDF文檔 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

使用Encryption API（Web服務）解鎖加密PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立加密服務客戶端。

   * 建立 `EncryptionServiceClient` 對象。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `EncryptionServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取加密的PDF文檔。

   * 建立 `BLOB` 對象。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 對象，方法是將位元組陣列的內容分配給 `BLOB` 對象 `MTOM` 資料成員。

1. 解鎖文檔。

   通過調用 `EncryptionServiceClient` 對象 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 的雙曲餘切值。

   要解鎖使用密碼加密的PDF文檔，請調用 `unlockPDFUsingPassword` 方法並傳遞以下值：

   * A `BLOB` 包含密碼加密PDF文檔的對象。
   * 一個字串值，它指定用於開啟密碼加密的PDF文檔的密碼值。 使用密碼加密PDF文檔時指定此值。

   要解鎖使用證書加密的PDF文檔，請調用 `unlockPDFUsingCredential` 方法並傳遞以下值：

   * A `BLOB` 包含證書加密PDF文檔的對象。
   * 一個字串值，它指定與用於加密PDf文檔的私鑰相對應的公鑰的別名。

   的 `unlockPDFUsingPassword` 和 `unlockPDFUsingCredential` 方法都返回 `com.adobe.idp.Document` 傳遞給另一個AEM Forms方法以執行操作的對象。

1. 執行AEM Forms操作。

   對解鎖的PDF文檔執行AEM Forms操作，以滿足您的業務要求。 例如，假定要將使用權限應用於未鎖定的PDF文檔，請將 `BLOB` 由其中一個 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 方法 `ReaderExtensionsServiceClient` 對象 `applyUsageRights` 的雙曲餘切值。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 確定加密類型 {#determining-encryption-type}

可以通過使用Java加密服務API或Web服務加密服務API以寫程式方式確定保護PDF文檔的加密類型。 有時需要動態確定PDF文檔是否已加密，如果加密，則需要確定加密類型。 例如，您可以確定PDF文檔是使用基於密碼的加密還是使用Rights Management策略進行保護。

PDF文檔可以受以下加密類型的保護：

* 基於密碼的加密
* 基於證書的加密
* 由Rights Management服務建立的策略
* 另一種加密類型

>[!NOTE]
>
>有關加密服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

要確定保護PDF文檔的加密類型，請執行以下步驟：

1. 包括項目檔案。
1. 建立加密服務客戶端。
1. 獲取加密的PDF文檔。
1. 確定加密類型。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

**建立服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果使用Java加密服務API，請建立 `EncrytionServiceClient` 的雙曲餘切值。 如果使用Web服務加密服務API，請建立 `EncryptionServiceService` 的雙曲餘切值。

**獲取加密的PDF文檔**

必須獲取PDF文檔，才能確定保護該文檔的加密類型。

**確定加密類型**

您可以確定保護PDF文檔的加密類型。 如果PDF文檔未受保護，則加密服務會通知您PDF文檔未受保護。

**另請參閱**

[使用Java API確定加密類型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[使用Web服務API確定加密類型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速啟動](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用策略保護文檔](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### 使用Java API確定加密類型 {#determine-the-encryption-type-using-the-java-api}

使用Encryption API(Java)確定保護PDF文檔的加密類型：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-encryption-client.jar。

1. 建立服務客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EncryptionServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取加密的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 確定加密類型。

   * 通過調用 `EncryptionServiceClient` 對象 `getPDFEncryption` 方法和傳遞 `com.adobe.idp.Document` 包含PDF文檔的對象。 此方法返回 `EncryptionTypeResult` 的雙曲餘切值。
   * 調用 `EncryptionTypeResult` 對象 `getEncryptionType` 的雙曲餘切值。 此方法返回 `EncryptionType` 指定加密類型的枚舉值。 例如，如果PDF文檔使用基於密碼的加密進行保護，則此方法將返回 `EncryptionType.PASSWORD`。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API確定加密類型](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API確定加密類型 {#determine-the-encryption-type-using-the-web-service-api}

使用Encryption API（Web服務）確定保護PDF文檔的加密類型：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立服務客戶端。

   * 建立 `EncryptionServiceClient` 對象。
   * 建立 `EncryptionServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `EncryptionServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取加密的PDF文檔。

   * 建立 `BLOB` 對象。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 對象，方法是將位元組陣列的內容分配給 `BLOB` 對象 `MTOM` 資料成員。

1. 確定加密類型。

   * 調用 `EncryptionServiceClient` 對象 `getPDFEncryption` 方法和通過 `BLOB` 包含PDF文檔的對象。 此方法返回 `EncryptionTypeResult` 的雙曲餘切值。
   * 獲取的值 `EncryptionTypeResult` 對象 `encryptionType` 資料方法。 例如，如果PDF文檔使用基於密碼的加密進行保護，則此資料成員的值為 `EncryptionType.PASSWORD`。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
