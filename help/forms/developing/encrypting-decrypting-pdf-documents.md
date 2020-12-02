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
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3
workflow-type: tm+mt
source-wordcount: '8118'
ht-degree: 0%

---


# 加密和解密PDF檔案{#encrypting-and-decrypting-pdf-documents}

**關於加密服務**

加密服務可讓您加密和解密檔案。 當文檔加密時，其內容將變得不可讀。 授權用戶可以解密文檔以獲得對內容的訪問。 如果PDF檔案使用密碼加密，使用者必須先指定開啟的密碼，才能在Adobe Reader或Adobe Acrobat中檢視該檔案。 同樣地，如果PDF檔案使用憑證加密，使用者必須使用與用來加密PDF檔案的憑證（私密金鑰）對應的公開金鑰來解密PDF檔案。

您可以使用Encryption服務完成以下任務：

* 使用密碼加密PDF檔案。 （請參閱[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)）。
* 使用憑證加密PDF檔案。 （請參閱[使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)）。
* 從PDF檔案移除密碼加密。 （請參閱[刪除密碼加密](encrypting-decrypting-pdf-documents.md#removing-password-encryption)。）
* 從PDF檔案移除憑證式加密。 （請參閱[刪除基於證書的加密](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)。）
* 解除鎖定PDF檔案，以便執行其他服務作業。 例如，在解除鎖定密碼加密的PDF檔案後，您就可以套用數位簽章。 （請參閱[解除加密的PDF檔案鎖定](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)）。
* 確定安全PDF檔案的加密類型。 （請參閱[確定加密類型](encrypting-decrypting-pdf-documents.md#determining-encryption-type)。）

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 使用密碼{#encrypting-pdf-documents-with-a-password}加密PDF檔案

當您使用密碼加密PDF檔案時，使用者必須指定密碼才能在Adobe Reader或Acrobat中開啟PDF檔案。 此外，在對檔案執行其他AEM Forms作業（例如數位簽署PDF檔案）之前，必須先解除鎖定密碼加密的PDF檔案。

>[!NOTE]
>
>如果您將加密的PDF檔案上傳至AEM Forms存放庫，它將無法解密PDF檔案並擷取XDP內容。 建議您不要在將檔案上傳至AEM Forms儲存庫之前加密檔案。 （請參閱[編寫資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。）

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

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
>權限指定為`PasswordEncryptionPermission`枚舉值。

**新增密碼**

在擷取不安全的PDF檔案並設定加密執行時值後，您可以在PDF檔案中新增密碼。

**將加密的PDF檔案儲存為PDF檔案**

您可以將密碼加密的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[使用web service API加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### 使用Java API {#encrypt-a-pdf-document-using-the-java-api}加密PDF檔案

使用Encryption API(Java)，以密碼加密PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密用戶端API。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`EncryptionServiceClient`對象。

1. 取得要加密的PDF檔案。

   * 建立`java.io.FileInputStream`對象，該對象表示要加密的PDF文檔，方法是使用其建構子並傳遞指定PDF文檔位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定加密運行時選項。

   * 通過調用`PasswordEncryptionOptionSpec`對象的建構子建立&lt;a0/>對象。
   * 調用`PasswordEncryptionOptionSpec`物件的`setEncryptOption`方法並傳遞指定要加密之檔案資源的`PasswordEncryptionOption`列舉值，以指定要加密的PDF檔案資源。 例如，若要加密整個PDF檔案，包括其中繼資料及其附件，請指定`PasswordEncryptionOption.ALL`。
   * 使用`ArrayList`建構函式建立儲存加密權限的`java.util.List`物件。
   * 通過調用`java.util.List`對象「s `add`」方法並傳遞與要設定的權限相對應的枚舉值來指定權限。 例如，若要設定允許使用者複製PDF檔案中資料的權限，請指定`PasswordEncryptionPermission.PASSWORD_EDIT_COPY`。 （請針對每個要設定的權限重複此步驟）。
   * 調用`PasswordEncryptionOptionSpec`物件的`setCompatability`方法並傳遞指定Acrobat相容性等級的列舉值，以指定Acrobat相容性選項。 例如，您可以指定`PasswordEncryptionCompatability.ACRO_7`。
   * 指定密碼值，讓使用者呼叫`PasswordEncryptionOptionSpec`物件的`setDocumentOpenPassword`方法並傳遞代表開啟密碼的字串值，以開啟加密的PDF檔案。
   * 指定主密碼值，讓使用者透過叫用`PasswordEncryptionOptionSpec`物件的`setPermissionPassword`方法並傳遞代表主密碼的字串值，從PDF檔案移除加密。

1. 新增密碼。

   叫用`EncryptionServiceClient`物件的`encryptPDFUsingPassword`方法並傳遞下列值，以加密PDF檔案：

   * 包含要使用密碼加密的PDF文檔的`com.adobe.idp.Document`對象。
   * 包含加密運行時選項的`PasswordEncryptionOptionSpec`對象。

   `encryptPDFUsingPassword`方法會傳回包含密碼加密PDF檔案的`com.adobe.idp.Document`物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案。 請確定您使用`encryptPDFUsingPassword`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API加密PDF檔案](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#encrypting-a-pdf-document-using-the-web-service-api}加密PDF檔案

使用Encryption API(web service)，以密碼加密PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立加密客戶端API對象。

   * 使用其預設建構子建立`EncryptionServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得要加密的PDF檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存使用密碼加密的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元組陣列的內容分配給`BLOB`對象的`MTOM`資料成員，以填充`BLOB`對象。

1. 設定加密運行時選項。

   * 使用其建構子建立`PasswordEncryptionOptionSpec`對象。
   * 為`PasswordEncryptionOptionSpec`物件的`encryptOption`資料成員指派`PasswordEncryptionOption`列舉值，以指定要加密的PDF檔案資源。 若要加密整個PDF，包括其中繼資料及其附件，請指派`PasswordEncryptionOption.ALL`給此資料成員。
   * 為`PasswordEncryptionOptionSpec`物件的`compatability`資料成員指派`PasswordEncryptionCompatability`列舉值，以指定Acrobat相容性選項。 例如，將`PasswordEncryptionCompatability.ACRO_7`指派給此資料成員。
   * 指定密碼值，讓使用者為`PasswordEncryptionOptionSpec`物件的`documentOpenPassword`資料成員指派代表開啟密碼的字串值，以開啟加密的PDF檔案。
   * 指定密碼值，讓使用者將代表主密碼的字串值指派給`PasswordEncryptionOptionSpec`物件的`permissionPassword`資料成員，以移除PDF檔案的加密。

1. 新增密碼。

   叫用`EncryptionServiceClient`物件的`encryptPDFUsingPassword`方法並傳遞下列值，以加密PDF檔案：

   * 包含要使用密碼加密的PDF文檔的`BLOB`對象。
   * 包含加密運行時選項的`PasswordEncryptionOptionSpec`對象。

   `encryptPDFUsingPassword`方法會傳回包含密碼加密PDF檔案的`BLOB`物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立&lt;a0/>對象，該字串值表示受保護PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存`encryptPDFUsingPassword`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立&lt;a0/>對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 使用憑證{#encrypting-pdf-documents-with-certificates}加密PDF檔案

憑證式加密可讓您透過公開金鑰技術，為特定收件者加密檔案。 可以為不同的收件者授予不同的檔案權限。 公鑰技術使加密的許多方面成為可能。 演算法用來產生兩個大數字，稱為&#x200B;*keys*，具有以下屬性：

* 一個密鑰用於加密一組資料。 隨後，只能使用其他密鑰解密資料。
* 不可能區分一把鑰匙和另一把鑰匙。

其中一個金鑰可當成使用者的私密金鑰。 請務必僅讓使用者存取此金鑰。 另一個金鑰是使用者的公開金鑰，可與其他人共用。

公開金鑰憑證包含使用者的公開金鑰和識別資訊。 X.509格式用於儲存憑證。 證書通常由證書頒發機構(CA)核發和數位簽名，該機構是一個認可的實體，提供對證書有效性的信任度。 憑證有到期日，之後即不再有效。 此外，證書撤銷清單(CRL)提供在證書到期日前被撤銷的證書資訊。 憑證授權機構會定期發佈CRL。 證書的撤銷狀態也可以通過網路上的聯機證書狀態協定(OCSP)來檢索。

>[!NOTE]
>
>如果您將加密的PDF檔案上傳至AEM Forms存放庫，它將無法解密PDF檔案並擷取XDP內容。 建議您不要在將檔案上傳至AEM Forms儲存庫之前加密檔案。 （請參閱[編寫資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。）

>[!NOTE]
>
>您必須先確保將憑證新增至AEM Forms，才能使用憑證加密PDF檔案。 憑證是使用管理控制台或使用信任管理器API以程式設計方式新增。 （請參閱[使用Trust Manager API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)匯入認證。）

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}摘要

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
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application Server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application Server上，則為必需）

**建立加密客戶端API對象**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java Encryption Service API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務Encryption Service API，請建立`EncryptionServiceService`對象。

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

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}使用憑證加密PDF檔案

使用Encryption API(Java)使用憑證來加密PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密客戶端API對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`EncryptionServiceClient`對象。

1. 取得要加密的PDF檔案。

   * 建立`java.io.FileInputStream`對象，該對象表示要加密的PDF文檔，方法是使用其建構子並傳遞指定PDF文檔位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 參考憑證。

   * 使用`java.util.List`的建構函式建立可儲存權限資訊的&lt;a0/>物件。
   * 調用`java.util.List`物件的`add`方法並傳遞`CertificateEncryptionPermissions`列舉值，以指定與加密檔案相關的權限，此列舉值代表授予開啟安全PDF檔案之使用者的權限。 例如，若要指定所有權限，請傳遞`CertificateEncryptionPermissions.PKI_ALL_PERM`。
   * 使用其建構子建立`Recipient`對象。
   * 建立`java.io.FileInputStream`對象，該對象表示通過使用其建構子並傳遞指定證書位置的字串值來加密PDF文檔的證書。
   * 使用其建構子並傳遞代表證書的`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。
   * 叫用`Recipient`物件的`setX509Cert`方法，並傳遞包含憑證的`com.adobe.idp.Document`物件。 （此外，`Recipient`物件可以有Truststore憑證別名或LDAP URL做為憑證來源）。
   * 使用`CertificateEncryptionIdentity`的建構函式建立可儲存權限和憑證資訊的&lt;a0/>物件。
   * 叫用`CertificateEncryptionIdentity`物件的`setPerms`方法，並傳遞儲存權限資訊的`java.util.List`物件。
   * 叫用`CertificateEncryptionIdentity`物件的`setRecipient`方法，並傳遞儲存憑證資訊的`Recipient`物件。
   * 使用`java.util.List`的建構函式建立儲存憑證資訊的&lt;a0/>物件。
   * 叫用`java.util.List`物件的add方法並傳遞`CertificateEncryptionIdentity`物件。 （此`java.util.List`對象作為參數傳遞給`encryptPDFUsingCertificates`方法。）

1. 設定加密運行時選項。

   * 通過調用`CertificateEncryptionOptionSpec`對象的建構子建立&lt;a0/>對象。
   * 調用`CertificateEncryptionOptionSpec`物件的`setOption`方法並傳遞指定要加密之檔案資源的`CertificateEncryptionOption`列舉值，以指定要加密的PDF檔案資源。 例如，若要加密整個PDF檔案，包括其中繼資料及其附件，請指定`CertificateEncryptionOption.ALL`。
   * 調用`CertificateEncryptionOptionSpec`物件的`setCompat`方法並傳遞指定Acrobat相容性等級的`CertificateEncryptionCompatibility`列舉值，以指定Acrobat相容性選項。 例如，您可以指定`CertificateEncryptionCompatibility.ACRO_7`。

1. 建立憑證加密的PDF檔案。

   使用憑證來加密PDF檔案，方法是叫用`EncryptionServiceClient`物件的`encryptPDFUsingCertificates`方法並傳遞下列值：

   * 包含要加密的PDF文檔的`com.adobe.idp.Document`對象。
   * 儲存證書資訊的`java.util.List`對象。
   * 包含加密運行時選項的`CertificateEncryptionOptionSpec`對象。

   `encryptPDFUsingCertificates`方法會傳回包含憑證加密PDF檔案的`com.adobe.idp.Document`物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案。 請確定您使用`encryptPDFUsingCertificates`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API使用憑證加密PDF檔案](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}使用憑證加密PDF檔案

使用Encryption API(web service)使用憑證來加密PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立加密客戶端API對象。

   * 使用其預設建構子建立`EncryptionServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得要加密的PDF檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存使用憑證加密的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的&lt;a1/>屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 參考憑證。

   * 使用其建構子建立`Recipient`對象。 此對象將儲存證書資訊。
   * 使用其建構子建立`BLOB`對象。 此`BLOB`物件會儲存加密PDF檔案的憑證。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立&lt;a0/>對象，該字串值表示證書的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元組陣列的內容分配給`BLOB`對象的`MTOM`資料成員，以填充`BLOB`對象。
   * 將儲存憑證的`BLOB`物件指派給`Recipient`物件的`x509Cert`資料成員。
   * 使用`CertificateEncryptionIdentity`的建構函式建立儲存憑證資訊的&lt;a0/>物件。
   * 將儲存憑證的`Recipient`物件指派給`CertificateEncryptionIdentity`物件的收件者資料成員。
   * 建立`Object`陣列，並將`CertificateEncryptionIdentity`對象分配給`Object`陣列的第一個元素。 此`Object`陣列作為參數傳遞給`encryptPDFUsingCertificates`方法。

1. 設定加密運行時選項。

   * 使用其建構子建立`CertificateEncryptionOptionSpec`對象。
   * 為`CertificateEncryptionOptionSpec`物件的`option`資料成員指派`CertificateEncryptionOption`列舉值，以指定要加密的PDF檔案資源。 要加密整個PDF文檔，包括其元資料及其附件，請將`CertificateEncryptionOption.ALL`分配給此資料成員。
   * 為`CertificateEncryptionOptionSpec`物件的`compat`資料成員指派`CertificateEncryptionCompatibility`列舉值，以指定Acrobat相容性選項。 例如，將`CertificateEncryptionCompatibility.ACRO_7`指派給此資料成員。

1. 建立憑證加密的PDF檔案。

   使用憑證來加密PDF檔案，方法是叫用`EncryptionServiceService`物件的`encryptPDFUsingCertificates`方法並傳遞下列值：

   * 包含要加密的PDF文檔的`BLOB`對象。
   * 儲存證書資訊的`Object`陣列。
   * 包含加密運行時選項的`CertificateEncryptionOptionSpec`對象。

   `encryptPDFUsingCertificates`方法會傳回包含憑證加密PDF檔案的`BLOB`物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立&lt;a0/>對象，該字串值表示受保護PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存`encryptPDFUsingCertificates`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象`binaryData`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立&lt;a0/>對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除基於證書的加密{#removing-certificate-based-encryption}

您可從PDF檔案移除憑證式加密，讓使用者在Adobe Reader或Acrobat中開啟PDF檔案。 若要從使用憑證加密的PDF檔案移除加密，必須參考公開金鑰。 從PDF檔案移除加密後，就不再安全。

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-2}摘要

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
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application Server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application Server上，則為必需）

**建立加密服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java Encryption Service API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務Encryption Service API，請建立`EncryptionServiceService`對象。

**取得加密的PDF檔案**

您必須取得加密的PDF檔案，才能移除憑證式加密。 如果您嘗試從未加密的PDF檔案移除加密，則會擲出例外。 同樣地，如果您嘗試從密碼加密的檔案中移除憑證式加密，則會擲出例外。

**刪除加密**

若要從加密的PDF檔案移除憑證式加密，您需要加密的PDF檔案和與用來加密PDF檔案的金鑰相對應的私密金鑰。 從加密的PDF檔案移除憑證式加密時，會指定私密金鑰的別名值。 如需公開金鑰的詳細資訊，請參閱[使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。

>[!NOTE]
>
>私密金鑰會儲存在AEM Forms信任商店中。 將證書放在那裡時，會指定別名值。

**儲存PDF檔案**

從加密的PDF檔案移除憑證式加密後，您就可將PDF檔案儲存為PDF檔案。 使用者可在Adobe Reader或Acrobat中開啟PDF檔案。

**另請參閱**

[使用Java API移除憑證式加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[使用web service API移除憑證式加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API {#remove-certificate-based-encryption-using-the-java-api}移除憑證式加密

使用Encryption API(Java)從PDF檔案移除憑證式加密：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`EncryptionServiceClient`對象。

1. 取得加密的PDF檔案。

   * 使用其建構函式並傳遞指定加密PDF檔案位置的字串值，建立代表加密PDF檔案的`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 刪除加密。

   調用`EncryptionServiceClient`物件的`removePDFCertificateSecurity`方法並傳遞下列值，以移除PDF檔案中的憑證式加密：

   * 包含加密PDF文檔的`com.adobe.idp.Document`對象。
   * 一個字串值，它指定與用於加密PDf文檔的密鑰相對應的私鑰的別名。

   `removePDFCertificateSecurity`方法傳回包含不安全PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`方法，將`Document`物件的內容複製至檔案。 請確定您使用`removePDFCredentialSecurity`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API移除憑證式加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#remove-certificate-based-encryption-using-the-web-service-api}移除憑證式加密

使用Encryption API(web service)移除憑證式加密：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立加密服務客戶端。

   * 使用其預設建構子建立`EncryptionServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存加密的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元組陣列的內容分配給`BLOB`對象的`MTOM`資料成員，以填充`BLOB`對象。

1. 刪除加密。

   叫用`EncryptionServiceClient`物件的`removePDFCertificateSecurity`方法並傳遞下列值：

   * `BLOB`物件，包含代表加密PDF檔案的檔案串流資料。
   * 一個字串值，它指定與用於加密PDf文檔的私鑰相對應的公鑰的別名。

   `removePDFCredentialSecurity`方法傳回包含不安全PDF檔案的`BLOB`物件。

1. 儲存PDF檔案。

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立&lt;a0/>對象，該字串值表示不安全PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存`removePDFPasswordSecurity`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立&lt;a0/>對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除密碼加密{#removing-password-encryption}

您可從PDF檔案移除密碼加密，讓使用者在Adobe Reader或Acrobat中開啟PDF檔案，而不需指定密碼。 從PDF檔案移除密碼加密後，檔案就不再安全。

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-3}摘要

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

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java Encryption Service API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務Encryption Service API，請建立`EncryptionServiceService`對象。

**取得加密的PDF檔案**

您必須取得加密的PDF檔案，才能移除密碼型加密。 如果您嘗試從未加密的PDF檔案移除加密，則會擲出例外。

**刪除密碼**

若要從加密的PDF檔案移除密碼型加密，您需要加密的PDF檔案和用於從PDF檔案移除加密的主密碼值。 用於開啟密碼加密的PDF文檔的密碼不能用於刪除加密。 當使用密碼加密PDF檔案時，會指定主密碼。 （請參閱[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)）。

**儲存PDF檔案**

在Encryption服務移除PDF檔案中以密碼為基礎的加密後，您可以將PDF檔案儲存為PDF檔案。 使用者可以在Adobe Reader或Acrobat中開啟PDF檔案，毋需指定密碼。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#remove-password-based-encryption-using-the-java-api}移除密碼加密

使用Encryption API(Java)從PDF檔案移除密碼加密：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`EncryptionServiceClient`對象。

1. 取得加密的PDF檔案。

   * 使用其建構函式並傳遞指定PDF檔案位置的字串值，建立代表加密PDF檔案的`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 刪除密碼。

   調用`EncryptionServiceClient`物件的`removePDFPasswordSecurity`方法並傳遞下列值，以移除PDF檔案中以密碼為基礎的加密：

   * `com.adobe.idp.Document`物件，其中包含加密的PDF檔案。
   * 一個字串值，它指定用於從PDF文檔中刪除加密的主密碼值。

   `removePDFPasswordSecurity`方法傳回包含不安全PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`方法，將`Document`物件的內容複製至檔案。 請確定您使用`removePDFPasswordSecurity`方法傳回的`Document`物件。

**另請參閱**

[快速入門（SOAP模式）:使用Java API移除密碼加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### 使用web service API {#remove-password-based-encryption-using-the-web-service-api}刪除基於密碼的加密

使用Encryption API(web service)移除密碼型加密：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立加密服務客戶端。

   * 使用其預設建構子建立`EncryptionServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存密碼加密的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元組陣列的內容分配給`BLOB`對象的`MTOM`資料成員，以填充`BLOB`對象。

1. 刪除密碼。

   叫用`EncryptionServiceService`物件的`removePDFPasswordSecurity`方法並傳遞下列值：

   * `BLOB`物件，包含代表加密PDF檔案的檔案串流資料。
   * 一個字串值，它指定用於從PDF文檔中刪除加密的口令值。 此值是在使用密碼加密PDF文檔時指定的。

   `removePDFPasswordSecurity`方法傳回包含不安全PDF檔案的`BLOB`物件。

1. 儲存PDF檔案。

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立&lt;a0/>對象，該字串值表示不安全PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存`removePDFPasswordSecurity`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立&lt;a0/>對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 解鎖加密的PDF檔案{#unlocking-encrypted-pdf-documents}

必須先解除鎖定密碼加密或憑證加密的PDF檔案，才能對其執行其他AEM Forms作業。 如果您嘗試對加密的PDF檔案執行操作，將會產生例外。 在解除鎖定加密的PDF檔案後，您可以對其執行一或多個操作。 這些作業可以屬於其他服務，例如Acrobat Reader DC擴充功能服務。

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-4}摘要

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
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application Server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application Server上，則為必需）

**建立加密服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java Encryption Service API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務Encryption Service API，請建立`EncryptionServiceService`對象。

**取得加密的PDF檔案**

您必須取得加密的PDF檔案，才能解除鎖定。 如果您嘗試解除鎖定未加密的PDF檔案，則會擲出例外。

**解除鎖定檔案**

若要解除鎖定密碼加密的PDF檔案，您需要加密的PDF檔案和用來開啟密碼加密的PDF檔案的密碼值。 此值是在使用密碼加密PDF文檔時指定的。 （請參閱[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)）。

若要解除鎖定憑證加密的PDF檔案，您需要加密的PDF檔案，以及與用來加密PDF檔案的私密金鑰相對應的公開金鑰別名值。

**執行AEM Forms作業**

在解除鎖定加密的PDF檔案後，您可以對其執行其他服務操作，例如套用使用權。 此操作屬於Acrobat Reader DC Extensions服務。

**另請參閱**

[使用Java API解除鎖定加密的PDF檔案](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[使用web service API解除鎖定加密的PDF檔案](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API {#unlock-an-encrypted-pdf-document-using-the-java-api}解除鎖定加密的PDF檔案

使用加密API(Java)解除鎖定加密的PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`EncryptionServiceClient`對象。

1. 取得加密的PDF檔案。

   * 使用其建構函式並傳遞指定加密PDF檔案位置的字串值，建立代表加密PDF檔案的`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 解除鎖定檔案。

   叫用`EncryptionServiceClient`物件的`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法，解除鎖定加密的PDF檔案。

   要解鎖使用密碼加密的PDF文檔，請調用`unlockPDFUsingPassword`方法並傳遞以下值：

   * `com.adobe.idp.Document`物件，其中包含密碼加密的PDF檔案。
   * 一個字串值，它指定用於開啟密碼加密的PDF文檔的密碼值。 此值是在使用密碼加密PDF文檔時指定的。

   要解鎖使用證書加密的PDF文檔，請調用`unlockPDFUsingCredential`方法並傳遞以下值：

   * `com.adobe.idp.Document`物件，其中包含憑證加密的PDF檔案。
   * 一個字串值，它指定與用於加密PDF文檔的私鑰相對應的公鑰的別名。

   `unlockPDFUsingPassword`和`unlockPDFUsingCredential`方法都會傳回您傳遞至其他AEM Forms Java方法以執行作業的`com.adobe.idp.Document`物件。

1. 執行AEM Forms作業。

   對解除鎖定的PDF檔案執行AEM Forms作業，以符合您的業務需求。 例如，假設您要將使用權限套用至解除鎖定的PDF檔案，請將`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法傳回的`com.adobe.idp.Document`物件傳遞至`ReaderExtensionsServiceClient`物件的`applyUsageRights`方法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAP模式）解除加密的PDF檔案鎖定

[將使用權套用至PDF檔案](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#unlock-an-encrypted-pdf-document-using-the-web-service-api}解除鎖定加密的PDF檔案

使用Encryption API(web service)解除鎖定加密的PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立加密服務客戶端。

   * 使用其預設建構子建立`EncryptionServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其建構子建立`BLOB`對象。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元組陣列的內容分配給`BLOB`對象的`MTOM`資料成員，以填充`BLOB`對象。

1. 解除鎖定檔案。

   叫用`EncryptionServiceClient`物件的`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法，解除鎖定加密的PDF檔案。

   要解鎖使用密碼加密的PDF文檔，請調用`unlockPDFUsingPassword`方法並傳遞以下值：

   * `BLOB`物件，其中包含密碼加密的PDF檔案。
   * 一個字串值，它指定用於開啟密碼加密的PDF文檔的密碼值。 此值是在使用密碼加密PDF文檔時指定的。

   要解鎖使用證書加密的PDF文檔，請調用`unlockPDFUsingCredential`方法並傳遞以下值：

   * `BLOB`物件，其中包含憑證加密的PDF檔案。
   * 一個字串值，它指定與用於加密PDf文檔的私鑰相對應的公鑰的別名。

   `unlockPDFUsingPassword`和`unlockPDFUsingCredential`方法都會傳回您傳遞至其他AEM Forms方法以執行作業的`com.adobe.idp.Document`物件。

1. 執行AEM Forms作業。

   對解除鎖定的PDF檔案執行AEM Forms作業，以符合您的業務需求。 例如，假設您要將使用權限套用至解除鎖定的PDF檔案，請將`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法傳回的`BLOB`物件傳遞至`ReaderExtensionsServiceClient`物件的`applyUsageRights`方法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 確定加密類型{#determining-encryption-type}

您可以使用Java Encryption Service API或web service Encryption Service API，以程式設計方式決定要保護PDF檔案的加密類型。 有時需要動態判斷PDF檔案是否已加密，若已加密，則需要加密類型。 例如，您可以決定PDF檔案是使用密碼加密或Rights Management原則來保護。

PDF檔案可受下列加密類型保護：

* 密碼加密
* 憑證式加密
* 由Rights Management服務建立的策略
* 另一種加密

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-5}摘要

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
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application Server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application Server上，則為必需）

**建立服務客戶端**

要以寫程式方式執行加密服務操作，必須建立加密服務客戶端。 如果您使用Java Encryption Service API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務Encryption Service API，請建立`EncryptionServiceService`對象。

**取得加密的PDF檔案**

您必須取得PDF檔案，以決定要保護它的加密類型。

**確定加密類型**

您可以決定保護PDF檔案的加密類型。 如果PDF檔案未受保護，則加密服務會通知您PDF檔案未受到保護。

**另請參閱**

[使用Java API確定加密類型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[使用web service API確定加密類型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用原則保護檔案](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### 使用Java API {#determine-the-encryption-type-using-the-java-api}確定加密類型

使用Encryption API(Java)確定保護PDF檔案的加密類型：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-encryption-client.jar。

1. 建立服務客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`EncryptionServiceClient`對象。

1. 取得加密的PDF檔案。

   * 使用PDF檔案的建構函式並傳遞指定PDF檔案位置的字串值，建立代表PDF檔案的`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 確定加密類型。

   * 調用`EncryptionServiceClient`物件的`getPDFEncryption`方法並傳遞包含PDF檔案的`com.adobe.idp.Document`物件，以判斷加密類型。 此方法返回`EncryptionTypeResult`對象。
   * 叫用`EncryptionTypeResult`物件的`getEncryptionType`方法。 此方法傳回指定加密類型的`EncryptionType`列舉值。 例如，如果PDF檔案受到密碼加密的保護，此方法會傳回`EncryptionType.PASSWORD`。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API確定加密類型](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#determine-the-encryption-type-using-the-web-service-api}確定加密類型

使用Encryption API(web service)確定保護PDF檔案的加密類型：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立服務客戶端。

   * 使用其預設建構子建立`EncryptionServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`EncryptionServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用其建構子建立`BLOB`對象。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 將位元組陣列的內容分配給`BLOB`對象的`MTOM`資料成員，以填充`BLOB`對象。

1. 確定加密類型。

   * 叫用`EncryptionServiceClient`物件的`getPDFEncryption`方法，並傳遞包含PDF檔案的`BLOB`物件。 此方法返回`EncryptionTypeResult`對象。
   * 取得`EncryptionTypeResult`物件的`encryptionType`資料方法的值。 例如，如果PDF檔案使用密碼加密進行保護，則此資料成員的值為`EncryptionType.PASSWORD`。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)