---
title: 加密和解密PDF檔案
seo-title: 加密和解密PDF檔案
description: 使用加密服務對文檔進行加密和解密。 加密服務任務包括使用密碼加密PDF文檔、使用證書加密PDF文檔、從PDF文檔中刪除基於密碼的加密、從PDF文檔中刪除基於證書的加密、解鎖PDF文檔以便執行其他服務操作，以及確定安全PDF文檔的加密類型。
seo-description: 使用加密服務對文檔進行加密和解密。 加密服務任務包括使用密碼加密PDF文檔、使用證書加密PDF文檔、從PDF文檔中刪除基於密碼的加密、從PDF文檔中刪除基於證書的加密、解鎖PDF文檔以便執行其他服務操作，以及確定安全PDF文檔的加密類型。
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
source-wordcount: '8258'
ht-degree: 0%

---

# 加密和解密PDF文檔{#encrypting-and-decrypting-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於加密服務**

加密服務可讓您加密和解密檔案。 文檔被加密後，其內容將變得不可讀。 授權用戶可以解密該文檔以獲得對內容的訪問。 如果PDF檔案使用密碼加密，使用者必須先指定開啟的密碼，才能在Adobe Reader或Adobe Acrobat中檢視該檔案。 同樣，如果PDF文檔用證書加密，則用戶必須用與用於加密PDF文檔的證書（私鑰）對應的公鑰解密PDF文檔。

您可以使用加密服務完成以下任務：

* 使用密碼加密PDF檔案。 （請參閱[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。）
* 使用憑證加密PDF檔案。 （請參閱[使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。）
* 從PDF文檔中刪除基於密碼的加密。 （請參閱[刪除密碼加密](encrypting-decrypting-pdf-documents.md#removing-password-encryption)。）
* 從PDF檔案中移除憑證式加密。 （請參閱[刪除基於證書的加密](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)。）
* 解除鎖定PDF檔案，以便執行其他服務操作。 例如，在解除鎖定密碼加密的PDF文檔後，您可以對其應用數字簽名。 （請參閱[解鎖加密的PDF文檔](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)。）
* 確定安全PDF文檔的加密類型。 （請參閱[確定加密類型](encrypting-decrypting-pdf-documents.md#determining-encryption-type)。）

>[!NOTE]
>
>有關加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 使用密碼{#encrypting-pdf-documents-with-a-password}加密PDF文檔

使用密碼加密PDF檔案時，使用者必須指定密碼，才能在Adobe Reader或Acrobat中開啟PDF檔案。 此外，在可以在文檔上執行其他AEM Forms操作（如對PDF文檔進行數字簽名）之前，必須解鎖密碼加密的PDF文檔。

>[!NOTE]
>
>如果您將加密的PDF檔案上傳至AEM Forms存放庫，該檔案將無法解密PDF檔案並擷取XDP內容。 建議您不要在將檔案上傳至AEM Forms存放庫前加密檔案。 （請參閱[寫入資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。）

>[!NOTE]
>
>有關加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}的摘要

要使用密碼加密PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密客戶端API對象。
1. 取得要加密的PDF檔案。
1. 設定加密運行時選項。
1. 新增密碼。
1. 將加密的PDF檔案儲存為PDF檔案。

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

**取得PDF檔案以加密**

您必須取得未加密的PDF檔案，才能使用密碼加密檔案。 如果您嘗試保護已加密的PDF檔案，會造成例外狀況。

**設定加密運行時選項**

要使用密碼加密PDF文檔，請指定四個值，包括兩個密碼值。 第一個密碼值用於加密PDF文檔，在開啟PDF文檔時必須指定。 第二個密碼值（名為主密碼值）用於從PDF文檔中刪除加密。 密碼值區分大小寫，且這兩個密碼值不能是相同的值。

必須指定要加密的PDF文檔資源。 您可以加密整個PDF文檔，除文檔元資料外的所有內容，或僅加密文檔的附件。 如果僅加密文檔的附件，則當用戶嘗試訪問檔案附件時，將提示用戶輸入密碼。

加密PDF文檔時，您可以指定與安全文檔關聯的權限。 通過指定權限，您可以控制開啟密碼加密的PDF文檔的用戶可以執行的操作。 例如，若要成功擷取表單資料，您必須設定下列權限：

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>權限指定為`PasswordEncryptionPermission`枚舉值。

**新增密碼**

檢索不安全的PDF文檔並設定加密運行時值後，可以向PDF文檔添加密碼。

**將加密的PDF檔案儲存為PDF檔案**

您可以將密碼加密的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[使用Web服務API加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### 使用Java API {#encrypt-a-pdf-document-using-the-java-api}加密PDF文檔

使用Encryption API(Java)以密碼加密PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密客戶端API。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`EncryptionServiceClient`物件。

1. 取得要加密的PDF檔案。

   * 建立`java.io.FileInputStream`對象，該對象使用其建構子並傳遞指定PDF文檔位置的字串值來表示要加密的PDF文檔。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定加密運行時選項。

   * 調用`PasswordEncryptionOptionSpec`對象的建構子以建立對象。
   * 通過調用`PasswordEncryptionOptionSpec`對象的`setEncryptOption`方法並傳遞指定要加密的文檔資源的`PasswordEncryptionOption`枚舉值，指定要加密的PDF文檔資源。 例如，要加密整個PDF文檔，包括其元資料和附件，請指定`PasswordEncryptionOption.ALL`。
   * 使用`ArrayList`建構子建立`java.util.List`物件以儲存加密權限。
   * 通過調用`java.util.List`對象s `add`方法並傳遞與要設定的權限相對應的枚舉值來指定權限。 例如，要設定允許用戶複製PDF文檔中資料的權限，請指定`PasswordEncryptionPermission.PASSWORD_EDIT_COPY`。 （對要設定的每個權限重複此步驟）。
   * 叫用`PasswordEncryptionOptionSpec`物件的`setCompatability`方法並傳遞指定Acrobat相容性層級的列舉值，以指定Acrobat相容性選項。 例如，您可以指定`PasswordEncryptionCompatability.ACRO_7`。
   * 指定密碼值，通過調用`PasswordEncryptionOptionSpec`對象的`setDocumentOpenPassword`方法並傳遞代表開啟密碼的字串值，允許用戶開啟加密的PDF文檔。
   * 指定主密碼值，該值允許用戶通過調用`PasswordEncryptionOptionSpec`對象的`setPermissionPassword`方法並傳遞代表主密碼的字串值來從PDF文檔中刪除加密。

1. 新增密碼。

   叫用`EncryptionServiceClient`物件的`encryptPDFUsingPassword`方法並傳遞下列值，以加密PDF檔案：

   * 包含要使用密碼加密的PDF文檔的`com.adobe.idp.Document`對象。
   * 包含加密運行時選項的`PasswordEncryptionOptionSpec`對象。

   `encryptPDFUsingPassword`方法返回包含密碼加密PDF文檔的`com.adobe.idp.Document`對象。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 建立`java.io.File`物件，並確認副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案。 請確定您使用`encryptPDFUsingPassword`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API加密PDF檔案](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#encrypting-a-pdf-document-using-the-web-service-api}加密PDF文檔

使用加密API（Web服務）以密碼加密PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立加密客戶端API對象。

   * 使用其預設建構子建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得要加密的PDF檔案。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存使用密碼加密的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`對象的`MTOM`資料成員，以填入`BLOB`對象。

1. 設定加密運行時選項。

   * 使用其建構子建立`PasswordEncryptionOptionSpec`物件。
   * 為`PasswordEncryptionOptionSpec`對象的`encryptOption`資料成員分配`PasswordEncryptionOption`枚舉值，以指定要加密的PDF文檔資源。 要加密整個PDF，包括其元資料及其附件，請將`PasswordEncryptionOption.ALL`分配給此資料成員。
   * 將`PasswordEncryptionCompatability`枚舉值指派給`PasswordEncryptionOptionSpec`物件的`compatability`資料成員，以指定Acrobat相容性選項。 例如，將`PasswordEncryptionCompatability.ACRO_7`分配給此資料成員。
   * 指定密碼值，該密碼值允許用戶通過為`PasswordEncryptionOptionSpec`對象的`documentOpenPassword`資料成員分配代表開啟密碼的字串值來開啟加密的PDF文檔。
   * 指定密碼值，該密碼值允許用戶通過為`PasswordEncryptionOptionSpec`對象的`permissionPassword`資料成員分配表示主密碼的字串值來從PDF文檔中刪除加密。

1. 新增密碼。

   叫用`EncryptionServiceClient`物件的`encryptPDFUsingPassword`方法並傳遞下列值，以加密PDF檔案：

   * 包含要使用密碼加密的PDF文檔的`BLOB`對象。
   * 包含加密運行時選項的`PasswordEncryptionOptionSpec`對象。

   `encryptPDFUsingPassword`方法返回包含密碼加密PDF文檔的`BLOB`對象。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示安全PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存`encryptPDFUsingPassword`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 使用憑證{#encrypting-pdf-documents-with-certificates}加密PDF檔案

憑證式加密可讓您透過公開金鑰技術為特定收件者加密檔案。 可以為文檔授予不同的收件者權限。 公鑰技術使加密的許多方面成為可能。 演算法可產生兩個大數字，稱為&#x200B;*keys*，其屬性如下：

* 一個密鑰用於加密一組資料。 隨後，只能使用其他密鑰來解密資料。
* 一個鍵和另一個鍵是無法區分的。

其中一個金鑰作為使用者的私密金鑰。 只有使用者才能存取此金鑰，這一點很重要。 另一個密鑰是使用者的公開密鑰，可與其他人共用。

公鑰證書包含用戶的公鑰和標識資訊。 X.509格式用於儲存憑證。 證書通常由證書頒發機構(CA)頒發並數字簽名，該機構是一個公認的實體，提供對證書有效性的信心度量。 憑證有到期日，之後即無效。 此外，證書吊銷清單(CRL)還提供有關在證書到期日之前被吊銷的證書的資訊。 證書頒發機構定期發佈CRL。 通過網路的線上證書狀態協定(OCSP)也可以檢索證書的吊銷狀態。

>[!NOTE]
>
>如果您將加密的PDF檔案上傳至AEM Forms存放庫，該檔案將無法解密PDF檔案並擷取XDP內容。 建議您不要在將檔案上傳至AEM Forms存放庫前加密檔案。 （請參閱[寫入資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。）

>[!NOTE]
>
>您必須先確定將憑證新增至AEM Forms，才能使用憑證加密PDF檔案。 使用管理控制台或使用信任管理器API以程式設計方式新增憑證。 （請參閱[使用信任管理器API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)導入憑據。）

>[!NOTE]
>
>有關加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}的摘要

要使用證書加密PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立加密客戶端API對象。
1. 取得要加密的PDF檔案。
1. 參考憑證。
1. 設定加密運行時選項。
1. 建立憑證加密的PDF檔案。
1. 將加密的PDF檔案儲存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

**建立加密客戶端API對象**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java加密服務API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務加密服務API，請建立`EncryptionServiceService`對象。

**取得PDF檔案以加密**

您必須取得未加密的PDF檔案才能加密。 如果您嘗試保護已加密的PDF檔案，則會擲回例外狀況。

**參考憑證**

若要使用憑證加密PDF檔案，請參考用來加密PDF檔案的憑證。 憑證是.cer檔案、.crt檔案或.pem檔案。 PKCS#12檔案用於儲存具有相應證書的私鑰。

使用憑證加密PDF檔案時，請指定與安全檔案相關聯的權限。 通過指定權限，您可以控制開啟證書加密PDF文檔的用戶可以執行的操作。

**設定加密運行時選項**

指定要加密的PDF檔案資源。 您可以加密整個PDF文檔、除文檔元資料外的所有內容，或僅加密文檔的附件。

**建立憑證加密的PDF檔案**

擷取不安全的PDF檔案、參考憑證和設定執行時選項後，您就可以建立憑證加密的PDF檔案。 PDF檔案加密後，您需要對應的公開金鑰才能解密。

**將加密的PDF檔案儲存為PDF檔案**

您可以將加密的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[使用Web服務API使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}使用憑證加密PDF檔案

使用Encryption API(Java)以憑證加密PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密客戶端API對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`EncryptionServiceClient`物件。

1. 取得要加密的PDF檔案。

   * 建立`java.io.FileInputStream`對象，該對象使用其建構子並傳遞指定PDF文檔位置的字串值來表示要加密的PDF文檔。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 參考憑證。

   * 建立`java.util.List`對象，該對象使用其建構子儲存權限資訊。
   * 通過調用`java.util.List`對象的`add`方法並傳遞`CertificateEncryptionPermissions`枚舉值來指定與加密文檔相關聯的權限，該枚舉值表示授予開啟安全PDF文檔的用戶的權限。 例如，要指定所有權限，請傳遞`CertificateEncryptionPermissions.PKI_ALL_PERM`。
   * 使用其建構子建立`Recipient`物件。
   * 建立`java.io.FileInputStream`對象，該對象表示用於加密PDF文檔的證書，方法是使用其建構子並傳遞一個字串值，該字串值指定證書的位置。
   * 使用其建構函式並傳遞代表憑證的`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。
   * 調用`Recipient`對象的`setX509Cert`方法，並傳遞包含證書的`com.adobe.idp.Document`對象。 （此外，`Recipient`對象可以具有Truststore證書別名或LDAP URL作為證書源。）
   * 建立`CertificateEncryptionIdentity`物件，使用其建構子儲存權限和憑證資訊。
   * 調用`CertificateEncryptionIdentity`對象的`setPerms`方法，並傳遞儲存權限資訊的`java.util.List`對象。
   * 調用`CertificateEncryptionIdentity`對象的`setRecipient`方法，並傳遞儲存證書資訊的`Recipient`對象。
   * 建立`java.util.List`物件，使用其建構子儲存憑證資訊。
   * 調用`java.util.List`對象的add方法並傳遞`CertificateEncryptionIdentity`對象。 （此`java.util.List`物件會以參數形式傳遞至`encryptPDFUsingCertificates`方法。）

1. 設定加密運行時選項。

   * 調用`CertificateEncryptionOptionSpec`對象的建構子以建立對象。
   * 通過調用`CertificateEncryptionOptionSpec`對象的`setOption`方法並傳遞指定要加密的文檔資源的`CertificateEncryptionOption`枚舉值，指定要加密的PDF文檔資源。 例如，要加密整個PDF文檔，包括其元資料和附件，請指定`CertificateEncryptionOption.ALL`。
   * 叫用`CertificateEncryptionOptionSpec`物件的`setCompat`方法並傳遞指定Acrobat相容性層級的`CertificateEncryptionCompatibility`列舉值，以指定Acrobat相容性選項。 例如，您可以指定`CertificateEncryptionCompatibility.ACRO_7`。

1. 建立憑證加密的PDF檔案。

   叫用`EncryptionServiceClient`物件的`encryptPDFUsingCertificates`方法並傳遞下列值，以憑證加密PDF檔案：

   * 包含要加密的PDF文檔的`com.adobe.idp.Document`對象。
   * 儲存證書資訊的`java.util.List`對象。
   * 包含加密運行時選項的`CertificateEncryptionOptionSpec`對象。

   `encryptPDFUsingCertificates`方法返回包含證書加密PDF文檔的`com.adobe.idp.Document`對象。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案。 請確定您使用`encryptPDFUsingCertificates`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API使用憑證加密PDF檔案](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}使用憑證加密PDF檔案

使用加密API（網站服務）以憑證加密PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立加密客戶端API對象。

   * 使用其預設建構子建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得要加密的PDF檔案。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存使用證書加密的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 參考憑證。

   * 使用其建構子建立`Recipient`物件。 此物件將儲存憑證資訊。
   * 使用其建構子建立`BLOB`物件。 此`BLOB`物件將儲存加密PDF檔案的憑證。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示證書的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`對象的`MTOM`資料成員，以填入`BLOB`對象。
   * 將儲存證書的`BLOB`對象分配給`Recipient`對象的`x509Cert`資料成員。
   * 建立`CertificateEncryptionIdentity`物件，使用其建構子儲存憑證資訊。
   * 將儲存憑證的`Recipient`物件指派給`CertificateEncryptionIdentity`物件的收件者資料成員。
   * 建立`Object`陣列，並將`CertificateEncryptionIdentity`物件指派給`Object`陣列的第一個元素。 此`Object`陣列會以參數的形式傳遞至`encryptPDFUsingCertificates`方法。

1. 設定加密運行時選項。

   * 使用其建構子建立`CertificateEncryptionOptionSpec`物件。
   * 為`CertificateEncryptionOptionSpec`對象的`option`資料成員分配`CertificateEncryptionOption`枚舉值，以指定要加密的PDF文檔資源。 要加密整個PDF文檔，包括其元資料及其附件，請將`CertificateEncryptionOption.ALL`分配給此資料成員。
   * 將`CertificateEncryptionCompatibility`枚舉值指派給`CertificateEncryptionOptionSpec`物件的`compat`資料成員，以指定Acrobat相容性選項。 例如，將`CertificateEncryptionCompatibility.ACRO_7`分配給此資料成員。

1. 建立憑證加密的PDF檔案。

   叫用`EncryptionServiceService`物件的`encryptPDFUsingCertificates`方法並傳遞下列值，以憑證加密PDF檔案：

   * 包含要加密的PDF文檔的`BLOB`對象。
   * 儲存證書資訊的`Object`陣列。
   * 包含加密運行時選項的`CertificateEncryptionOptionSpec`對象。

   `encryptPDFUsingCertificates`方法返回包含證書加密PDF文檔的`BLOB`對象。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示安全PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存`encryptPDFUsingCertificates`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象的`binaryData`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除基於證書的加密{#removing-certificate-based-encryption}

可從PDF檔案中移除憑證式加密，讓使用者能在Adobe Reader或Acrobat中開啟PDF檔案。 若要從使用憑證加密的PDF檔案中移除加密，必須參考公開金鑰。 從PDF檔案移除加密後，加密將不再安全。

>[!NOTE]
>
>有關加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-2}的摘要

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

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java加密服務API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務加密服務API，請建立`EncryptionServiceService`對象。

**取得加密的PDF檔案**

您必須取得加密的PDF檔案，才能移除憑證式加密。 如果嘗試從未加密的PDF文檔中刪除加密，則會引發異常。 同樣，如果嘗試從密碼加密的文檔中刪除基於證書的加密，則會引發異常。

**刪除加密**

若要從加密的PDF檔案中移除憑證式加密，您需要加密的PDF檔案和與用來加密PDF檔案的金鑰相對應的私密金鑰。 從加密的PDF檔案中移除憑證式加密時，會指定私密金鑰的別名值。 如需公開金鑰的相關資訊，請參閱[使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。

>[!NOTE]
>
>私密金鑰儲存在AEM Forms信託存放區。 將證書放在該處時，將指定別名值。

**儲存PDF檔案**

從加密的PDF檔案中移除憑證式加密後，您可以將PDF檔案儲存為PDF檔案。 使用者可以在Adobe Reader或Acrobat中開啟PDF檔案。

**另請參閱**

[使用Java API移除憑證式加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[使用Web服務API刪除基於證書的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API {#remove-certificate-based-encryption-using-the-java-api}刪除基於證書的加密

使用加密API(Java)從PDF檔案中移除憑證式加密：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`EncryptionServiceClient`物件。

1. 取得加密的PDF檔案。

   * 使用加密的PDF文檔的建構子並傳遞指定加密的PDF文檔位置的字串值，建立代表加密的PDF文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 刪除加密。

   調用`EncryptionServiceClient`對象的`removePDFCertificateSecurity`方法並傳遞以下值，從PDF文檔中刪除基於證書的加密：

   * 包含加密PDF文檔的`com.adobe.idp.Document`對象。
   * 一個字串值，它指定與用於加密PDf文檔的密鑰對應的私鑰的別名。

   `removePDFCertificateSecurity`方法返回包含不安全PDF文檔的`com.adobe.idp.Document`對象。

1. 保存PDF文檔。

   * 建立`java.io.File`物件，並確認副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`Document`對象的內容複製到檔案。 請確定您使用`removePDFCredentialSecurity`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API移除憑證式加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#remove-certificate-based-encryption-using-the-web-service-api}刪除基於證書的加密

使用加密API（Web服務）刪除基於證書的加密：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立加密服務客戶端。

   * 使用其預設建構子建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存加密的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`對象的`MTOM`資料成員，以填入`BLOB`對象。

1. 刪除加密。

   調用`EncryptionServiceClient`對象的`removePDFCertificateSecurity`方法並傳遞以下值：

   * `BLOB`物件，包含代表加密PDF檔案的檔案資料流資料。
   * 一個字串值，它指定與用於加密PDf文檔的私鑰相對應的公鑰的別名。

   `removePDFCredentialSecurity`方法返回包含不安全PDF文檔的`BLOB`對象。

1. 保存PDF文檔。

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示不安全PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存`removePDFPasswordSecurity`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除密碼加密{#removing-password-encryption}

可從PDF檔案中移除密碼加密，讓使用者無須指定密碼即可在Adobe Reader或Acrobat中開啟PDF檔案。 從PDF檔案移除密碼加密後，檔案將不再安全。

>[!NOTE]
>
>有關加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-3}的摘要

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

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java加密服務API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務加密服務API，請建立`EncryptionServiceService`對象。

**取得加密的PDF檔案**

您必須取得加密的PDF檔案，才能移除密碼加密。 如果嘗試從未加密的PDF文檔中刪除加密，則會引發異常。

**刪除密碼**

要從加密的PDF文檔中刪除基於密碼的加密，您需要加密的PDF文檔和用於從PDF文檔中刪除加密的主密碼值。 用於開啟密碼加密的PDF文檔的密碼不能用於刪除加密。 使用密碼加密PDF文檔時，指定主密碼。 （請參閱[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。）

**儲存PDF檔案**

加密服務從PDF文檔中刪除基於密碼的加密後，您可以將PDF文檔另存為PDF檔案。 使用者無需指定密碼，即可在Adobe Reader或Acrobat中開啟PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#remove-password-based-encryption-using-the-java-api}刪除基於密碼的加密

使用加密API(Java)從PDF文檔中刪除基於密碼的加密：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`EncryptionServiceClient`物件。

1. 取得加密的PDF檔案。

   * 使用加密的PDF文檔的建構子並傳遞一個指定PDF文檔位置的字串值，建立一個`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 刪除密碼。

   調用`EncryptionServiceClient`對象的`removePDFPasswordSecurity`方法並傳遞以下值，從PDF文檔中刪除基於密碼的加密：

   * 包含加密PDF文檔的`com.adobe.idp.Document`對象。
   * 一個字串值，它指定用於從PDF文檔中刪除加密的主密碼值。

   `removePDFPasswordSecurity`方法返回包含不安全PDF文檔的`com.adobe.idp.Document`對象。

1. 保存PDF文檔。

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`Document`對象的內容複製到檔案。 請確定您使用`removePDFPasswordSecurity`方法傳回的`Document`物件。

**另請參閱**

[快速入門（SOAP模式）:使用Java API刪除基於密碼的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### 使用Web服務API {#remove-password-based-encryption-using-the-web-service-api}刪除基於密碼的加密

使用加密API（Web服務）刪除基於密碼的加密：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立加密服務客戶端。

   * 使用其預設建構子建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存密碼加密的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`對象的`MTOM`資料成員，以填入`BLOB`對象。

1. 刪除密碼。

   調用`EncryptionServiceService`對象的`removePDFPasswordSecurity`方法並傳遞以下值：

   * `BLOB`物件，包含代表加密PDF檔案的檔案資料流資料。
   * 一個字串值，它指定用於從PDF文檔中刪除加密的密碼值。 使用密碼加密PDF檔案時，會指定此值。

   `removePDFPasswordSecurity`方法返回包含不安全PDF文檔的`BLOB`對象。

1. 保存PDF文檔。

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示不安全PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存`removePDFPasswordSecurity`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 解鎖加密的PDF文檔{#unlocking-encrypted-pdf-documents}

必須先解除密碼加密或憑證加密的PDF檔案的鎖定，才能對其執行其他AEM Forms操作。 如果嘗試對加密的PDF文檔執行操作，將生成異常。 解鎖加密的PDF文檔後，可以對其執行一個或多個操作。 這些作業可屬於其他服務，例如Acrobat Reader DC擴充功能服務。

>[!NOTE]
>
>有關加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-4}的摘要

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

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java加密服務API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務加密服務API，請建立`EncryptionServiceService`對象。

**取得加密的PDF檔案**

您必須取得加密的PDF檔案才能解鎖。 如果嘗試解鎖未加密的PDF文檔，則會引發異常。

**解鎖文檔**

要解鎖密碼加密的PDF文檔，您需要加密的PDF文檔和用於開啟密碼加密的PDF文檔的密碼值。 使用密碼加密PDF檔案時，會指定此值。 （請參閱[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。）

若要解鎖憑證加密的PDF檔案，您需要加密的PDF檔案，以及與用於加密PDF檔案的私密金鑰相對應的公開金鑰的別名值。

**執行AEM Forms操作**

解除鎖定加密的PDF文檔後，您可以對其執行其他服務操作，如應用使用權限。 此操作屬於Acrobat Reader DC擴充功能服務。

**另請參閱**

[使用Java API解除鎖定加密的PDF檔案](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[使用Web服務API解鎖加密的PDF檔案](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API {#unlock-an-encrypted-pdf-document-using-the-java-api}解鎖加密的PDF文檔

使用加密API(Java)解鎖加密的PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`EncryptionServiceClient`物件。

1. 取得加密的PDF檔案。

   * 使用加密的PDF文檔的建構子並傳遞指定加密的PDF文檔位置的字串值，建立代表加密的PDF文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 解鎖文檔。

   叫用`EncryptionServiceClient`物件的`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法，解鎖加密的PDF檔案。

   要解鎖使用密碼加密的PDF文檔，請調用`unlockPDFUsingPassword`方法並傳遞以下值：

   * `com.adobe.idp.Document`物件，包含密碼加密的PDF檔案。
   * 一個字串值，它指定用於開啟密碼加密的PDF文檔的密碼值。 使用密碼加密PDF檔案時，會指定此值。

   若要解鎖使用憑證加密的PDF檔案，請叫用`unlockPDFUsingCredential`方法，並傳遞下列值：

   * `com.adobe.idp.Document`物件，包含憑證加密的PDF檔案。
   * 一個字串值，它指定與用於加密PDF文檔的私鑰對應的公鑰的別名。

   `unlockPDFUsingPassword`和`unlockPDFUsingCredential`方法都會傳回您傳遞至其他AEM Forms Java方法以執行操作的`com.adobe.idp.Document`物件。

1. 執行AEM Forms操作。

   對解鎖的PDF檔案執行AEM Forms操作，以符合您的業務需求。 例如，假設要將使用權應用於未鎖定的PDF文檔，請將`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法返回的`com.adobe.idp.Document`對象傳遞至`ReaderExtensionsServiceClient`對象的`applyUsageRights`方法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API解除鎖定加密的PDF檔案](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAP模式）

[將使用權套用至PDF檔案](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#unlock-an-encrypted-pdf-document-using-the-web-service-api}解鎖加密的PDF文檔

使用加密API（Web服務）解鎖加密的PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立加密服務客戶端。

   * 使用其預設建構子建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其建構子建立`BLOB`物件。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`對象的`MTOM`資料成員，以填入`BLOB`對象。

1. 解鎖文檔。

   叫用`EncryptionServiceClient`物件的`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法，解鎖加密的PDF檔案。

   要解鎖使用密碼加密的PDF文檔，請調用`unlockPDFUsingPassword`方法並傳遞以下值：

   * `BLOB`物件，包含密碼加密的PDF檔案。
   * 一個字串值，它指定用於開啟密碼加密的PDF文檔的密碼值。 使用密碼加密PDF檔案時，會指定此值。

   若要解鎖使用憑證加密的PDF檔案，請叫用`unlockPDFUsingCredential`方法，並傳遞下列值：

   * `BLOB`物件，包含憑證加密的PDF檔案。
   * 一個字串值，它指定與用於加密PDf文檔的私鑰相對應的公鑰的別名。

   `unlockPDFUsingPassword`和`unlockPDFUsingCredential`方法都會傳回您傳遞至其他AEM Forms方法以執行操作的`com.adobe.idp.Document`物件。

1. 執行AEM Forms操作。

   對解鎖的PDF檔案執行AEM Forms操作，以符合您的業務需求。 例如，假設您要將使用權限應用於未鎖定的PDF文檔，請將`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法返回的`BLOB`對象傳遞至`ReaderExtensionsServiceClient`對象的`applyUsageRights`方法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 確定加密類型{#determining-encryption-type}

您可以使用Java加密服務API或Web服務加密服務API，以程式設計方式確定要保護PDF文檔的加密類型。 有時需要動態判斷PDF檔案是否已加密，若已加密，則需加密類型。 例如，您可以確定PDF文檔是使用基於密碼的加密保護還是Rights Management策略。

PDF檔案可受下列加密類型保護：

* 基於密碼的加密
* 基於證書的加密
* 由Rights Management服務建立的策略
* 另一種加密

>[!NOTE]
>
>有關加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-5}的摘要

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

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java加密服務API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務加密服務API，請建立`EncryptionServiceService`對象。

**取得加密的PDF檔案**

您必須取得PDF檔案，才能判斷要保護加密的類型。

**確定加密類型**

您可以確定要保護PDF文檔的加密類型。 如果PDF檔案未受到保護，加密服務會通知您PDF檔案未受到保護。

**另請參閱**

[使用Java API確定加密類型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[使用Web服務API確定加密類型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用策略保護文檔](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### 使用Java API {#determine-the-encryption-type-using-the-java-api}確定加密類型

使用加密API(Java)確定保護PDF文檔的加密類型：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立服務客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`EncryptionServiceClient`物件。

1. 取得加密的PDF檔案。

   * 使用PDF文檔的建構子並傳遞指定PDF文檔位置的字串值，建立代表PDF文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 確定加密類型。

   * 調用`EncryptionServiceClient`對象的`getPDFEncryption`方法並傳遞包含PDF文檔的`com.adobe.idp.Document`對象，以確定加密類型。 此方法會傳回`EncryptionTypeResult`物件。
   * 調用`EncryptionTypeResult`對象的`getEncryptionType`方法。 此方法會傳回指定加密類型的`EncryptionType`列舉值。 例如，如果PDF文檔受基於密碼的加密保護，則此方法將返回`EncryptionType.PASSWORD`。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API確定加密類型](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#determine-the-encryption-type-using-the-web-service-api}確定加密類型

使用加密API（Web服務）確定保護PDF文檔的加密類型：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立服務客戶端。

   * 使用其預設建構子建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其建構子建立`BLOB`物件。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示加密PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`對象的`MTOM`資料成員，以填入`BLOB`對象。

1. 確定加密類型。

   * 調用`EncryptionServiceClient`對象的`getPDFEncryption`方法，並傳遞包含PDF文檔的`BLOB`對象。 此方法會傳回`EncryptionTypeResult`物件。
   * 獲取`EncryptionTypeResult`對象的`encryptionType`資料方法的值。 例如，如果PDF文檔受基於密碼的加密保護，則此資料成員的值為`EncryptionType.PASSWORD`。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
