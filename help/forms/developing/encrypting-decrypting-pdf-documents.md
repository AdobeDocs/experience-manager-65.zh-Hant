---
title: 加密和解密PDF檔案
description: 使用加密服務來加密和解密檔案。 加密服務工作包括使用密碼加密PDF檔案、使用憑證加密PDF檔案、從PDF檔案中移除密碼式加密、從PDF檔案中移除憑證式加密、解鎖PDF檔案以便可以執行其他服務操作，以及決定安全PDF檔案的加密型別。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '8133'
ht-degree: 0%

---

# 加密和解密PDF檔案 {#encrypting-and-decrypting-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於加密服務**

加密服務可讓您加密和解密檔案。 檔案加密後，其內容會變得無法讀取。 授權的使用者可以解密檔案以取得內容的存取權。 如果PDF檔案已使用密碼加密，使用者必須先指定開啟的密碼，才能在Adobe Reader或Adobe Acrobat中檢視檔案。 同樣地，如果PDF檔案已使用憑證加密，使用者必須使用與用於加密PDF檔案的憑證（私密金鑰）相對應的公開金鑰來解密PDF檔案。

您可以使用加密服務完成這些工作：

* 使用密碼加密PDF檔案。 (請參閱[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)
* 使用憑證加密PDF檔案。 (請參閱[使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。)
* 從PDF檔案中移除密碼式加密。 （請參閱[移除密碼加密](encrypting-decrypting-pdf-documents.md#removing-password-encryption)。）
* 從PDF檔案中移除憑證式加密。 （請參閱[移除憑證式加密](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)。）
* 解鎖PDF檔案，以便執行其他服務操作。 例如，在解除鎖定以密碼加密的PDF檔案後，您可以對其套用數位簽名。 (請參閱[解除鎖定加密的PDF檔案](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)。)
* 判斷安全PDF檔案的加密型別。 （請參閱[決定加密型別](encrypting-decrypting-pdf-documents.md#determining-encryption-type)。）

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 使用密碼加密PDF檔案 {#encrypting-pdf-documents-with-a-password}

當您使用密碼加密PDF檔案時，使用者必須指定密碼，才能在Adobe Reader或Acrobat中開啟PDF檔案。 此外，必須先解除鎖定密碼加密的PDF檔案，才能對檔案執行其他AEM Forms操作(例如數位簽署PDF檔案)。

>[!NOTE]
>
>如果您將加密的PDF檔案上傳到AEM Forms存放庫，它將無法解密PDF檔案並擷取XDP內容。 建議您在將檔案上傳至AEM Forms存放庫之前，不要對其進行加密。 （請參閱[寫入資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。）

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要使用密碼加密PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立加密使用者端API物件。
1. 取得要加密的PDF檔案。
1. 設定加密執行階段選項。
1. 新增密碼。
1. 將加密的PDF檔案儲存為PDF檔案。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立加密使用者端API物件**

若要以程式設計方式執行「加密」服務作業，您必須建立「加密」服務使用者端。

**取得要加密的PDF檔案**

取得未加密的PDF檔案，以使用密碼加密檔案。 如果您嘗試保護已加密的PDF檔案，則會造成例外狀況。

**設定加密執行階段選項**

若要使用密碼加密PDF檔案，請指定四個值，包括兩個密碼值。 第一個密碼值是用來加密PDF檔案，且必須在開啟PDF檔案時指定。 第二個密碼值（稱為主密碼值）可用來從PDF檔案中移除加密。 密碼值區分大小寫，且這兩個密碼值不能相同。

指定要加密的PDF檔案資源。 您可以加密整個PDF檔案，除了檔案的中繼資料以外的所有內容，或只是檔案的附件。 如果您只加密檔案的附件，則當使用者嘗試存取檔案附件時，系統會提示使用者輸入密碼。

加密PDF檔案時，您可以指定與受保護檔案相關聯的許可權。 透過指定許可權，您可以控制允許開啟密碼加密PDF檔案的使用者執行的動作。 例如，若要成功擷取表單資料，您必須設定下列許可權：

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>許可權指定為`PasswordEncryptionPermission`列舉值。

**新增密碼**

擷取不安全的PDF檔案並設定加密執行階段值後，即可將密碼新增至PDF檔案。

**將加密的PDF檔案儲存為PDF檔案**

您可以將密碼加密的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[使用網站服務API加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### 使用Java API加密PDF檔案 {#encrypt-a-pdf-document-using-the-java-api}

使用加密API (Java)以密碼加密PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密使用者端API。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`EncryptionServiceClient`物件。

1. 取得要加密的PDF檔案。

   * 建立代表要加密之PDF檔案的`java.io.FileInputStream`物件，方法是使用其建構函式，並傳遞指定PDF檔案位置的字串值。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定加密執行階段選項。

   * 透過叫用它的建構函式來建立`PasswordEncryptionOptionSpec`物件。
   * 透過叫用`PasswordEncryptionOptionSpec`物件的`setEncryptOption`方法並傳遞指定要加密的檔案資源的`PasswordEncryptionOption`列舉值來指定要加密的PDF檔案資源。 例如，若要加密整個PDF檔案，包括其中繼資料及其附件，請指定`PasswordEncryptionOption.ALL`。
   * 使用`ArrayList`建構函式建立儲存加密許可權的`java.util.List`物件。
   * 透過叫用`java.util.List`物件的`add`方法並傳遞對應到您要設定的許可權的列舉值來指定許可權。 例如，若要設定允許使用者複製PDF檔案中資料的許可權，請指定`PasswordEncryptionPermission.PASSWORD_EDIT_COPY`。 （對每個要設定的許可權重複此步驟）。
   * 呼叫`PasswordEncryptionOptionSpec`物件的`setCompatability`方法，並傳遞指定Acrobat相容性層級的列舉值，以指定Acrobat相容性選項。 例如，您可以指定`PasswordEncryptionCompatability.ACRO_7`。
   * 指定密碼值，讓使用者可以透過叫用`PasswordEncryptionOptionSpec`物件的`setDocumentOpenPassword`方法並傳遞代表開啟密碼的字串值來開啟加密的PDF檔案。
   * 指定主要密碼值，讓使用者可以呼叫`PasswordEncryptionOptionSpec`物件的`setPermissionPassword`方法，並傳遞代表主要密碼的字串值，從PDF檔案移除加密。

1. 新增密碼。

   透過叫用`EncryptionServiceClient`物件的`encryptPDFUsingPassword`方法並傳遞下列值來加密PDF檔案：

   * 包含要以密碼加密之PDF檔案的`com.adobe.idp.Document`物件。
   * 包含加密執行階段選項的`PasswordEncryptionOptionSpec`物件。

   `encryptPDFUsingPassword`方法傳回包含密碼加密PDF檔案的`com.adobe.idp.Document`物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案。 確定您使用的是`encryptPDFUsingPassword`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門(SOAP模式)：使用Java API加密PDF檔案](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)


[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API加密PDF檔案 {#encrypting-a-pdf-document-using-the-web-service-api}

使用加密API （Web服務）以密碼加密PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立加密使用者端API物件。

   * 使用預設建構函式建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`EncryptionServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得要加密的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存以密碼加密的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表要加密之PDF檔案的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`物件的`MTOM`資料成員，以填入`BLOB`物件。

1. 設定加密執行階段選項。

   * 使用物件的建構函式建立`PasswordEncryptionOptionSpec`物件。
   * 指定`PasswordEncryptionOption`列舉值給`PasswordEncryptionOptionSpec`物件的`encryptOption`資料成員，以指定要加密的PDF檔案資源。 若要加密整個PDF，包括其中繼資料及其附件，請將`PasswordEncryptionOption.ALL`指派給此資料成員。
   * 將`PasswordEncryptionCompatability`列舉值指派給`PasswordEncryptionOptionSpec`物件的`compatability`資料成員，以指定Acrobat相容性選項。 例如，將`PasswordEncryptionCompatability.ACRO_7`指派給此資料成員。
   * 指定密碼值，讓使用者藉由指定字串值來開啟加密的PDF檔案，該字串值代表`PasswordEncryptionOptionSpec`物件之`documentOpenPassword`資料成員的開啟密碼。
   * 指定密碼值，可讓使用者透過將代表主密碼的字串值指派給`PasswordEncryptionOptionSpec`物件的`permissionPassword`資料成員，從PDF檔案中移除加密。

1. 新增密碼。

   透過叫用`EncryptionServiceClient`物件的`encryptPDFUsingPassword`方法並傳遞下列值來加密PDF檔案：

   * 包含要以密碼加密之PDF檔案的`BLOB`物件。
   * 包含加密執行階段選項的`PasswordEncryptionOptionSpec`物件。

   `encryptPDFUsingPassword`方法傳回包含密碼加密PDF檔案的`BLOB`物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表受保護PDF檔案檔案位置的字串值。
   * 建立位元組陣列，儲存`encryptPDFUsingPassword`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 使用憑證加密PDF檔案 {#encrypting-pdf-documents-with-certificates}

憑證式加密可讓您透過公開金鑰技術為特定收件者加密檔案。 可以為各種收件者提供該檔案的不同許可權。 公開金鑰技術可讓加密的許多方面成為可能。 演演算法是用來產生兩個大數字，稱為&#x200B;*金鑰*，它們具有以下屬性：

* 一個金鑰用來加密一組資料。 接著，只能使用另一個金鑰來解密資料。
* 無法區分一個金鑰。

其中一個金鑰會作為使用者的私密金鑰。 重要的是，只有使用者才能存取此金鑰。 另一個金鑰是使用者的公開金鑰，可與其他人共用。

公開金鑰憑證包含使用者的公開金鑰和識別資訊。 X.509格式用於儲存憑證。 憑證通常由憑證授權單位(CA)簽發並以數位方式簽署，該授權單位是公認的實體，可衡量憑證的有效性。 憑證有到期日，到期日之後便不再有效。 此外，憑證撤銷清單(CRL)也提供在到期日之前被撤銷的憑證的相關資訊。 憑證授權單位會定期發佈CRL。 憑證的撤銷狀態也可以透過網路上的線上憑證狀態通訊協定(OCSP)來擷取。

>[!NOTE]
>
>如果您將加密的PDF檔案上傳到AEM Forms存放庫，它將無法解密PDF檔案並擷取XDP內容。 建議您在將檔案上傳至AEM Forms存放庫之前，不要對其進行加密。 （請參閱[寫入資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。）

>[!NOTE]
>
>您必須確定將憑證新增至AEM Forms，才能使用憑證加密PDF檔案。 使用管理控制檯或以程式設計方式使用信任管理員API新增憑證。 （請參閱[使用信任管理員API匯入認證](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。）

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

若要使用憑證加密PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立加密使用者端API物件。
1. 取得要加密的PDF檔案。
1. 參考憑證。
1. 設定加密執行階段選項。
1. 建立憑證加密的PDF檔案。
1. 將加密的PDF檔案儲存為PDF檔案。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

**建立加密使用者端API物件**

若要以程式設計方式執行「加密」服務作業，您必須建立「加密」服務使用者端。 如果您使用Java加密服務API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務加密服務API，請建立`EncryptionServiceService`物件。

**取得要加密的PDF檔案**

取得未加密的PDF檔案以進行加密。 如果您嘗試保護已加密的PDF檔案，則會擲回例外狀況。

**參考憑證**

若要使用憑證加密PDF檔案，請參考用來加密PDF檔案的憑證。 憑證是.cer檔案、.crt檔案或.pem檔案。 PKCS#12檔案可用來儲存具有對應憑證的私密金鑰。

使用憑證加密PDF檔案時，請指定與安全檔案相關聯的許可權。 透過指定許可權，您可以控制開啟憑證加密PDF檔案的使用者可以執行的動作。

**設定加密執行階段選項**

指定要加密的PDF檔案資源。 您可以加密整個PDF檔案，除了檔案中繼資料以外的所有內容，或僅加密檔案的附件。

**建立憑證加密的PDF檔案**

擷取不安全的PDF檔案後，參照憑證並設定執行階段選項，即可建立憑證加密的PDF檔案。 PDF檔案加密後，您需要對應的公開金鑰才能將其解密。

**將加密的PDF檔案儲存為PDF檔案**

您可以將加密的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API以憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[使用Web服務API以憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API以憑證加密PDF檔案 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

使用加密API (Java)加密包含憑證的PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密使用者端API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`EncryptionServiceClient`物件。

1. 取得要加密的PDF檔案。

   * 建立代表要加密之PDF檔案的`java.io.FileInputStream`物件，方法是使用其建構函式，並傳遞指定PDF檔案位置的字串值。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 參考憑證。

   * 使用它的建構函式建立儲存許可權資訊的`java.util.List`物件。
   * 透過叫用`java.util.List`物件的`add`方法並傳遞代表許可權的`CertificateEncryptionPermissions`列舉值(已授與開啟安全PDF檔案的使用者)，來指定與加密檔案相關聯的許可權。 例如，若要指定所有許可權，請傳遞`CertificateEncryptionPermissions.PKI_ALL_PERM`。
   * 使用物件的建構函式建立`Recipient`物件。
   * 建立`java.io.FileInputStream`物件，代表使用它的建構函式來加密PDF檔案的憑證，並傳遞指定憑證位置的字串值。
   * 使用它的建構函式並傳遞代表憑證的`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。
   * 叫用`Recipient`物件的`setX509Cert`方法，並傳遞包含憑證的`com.adobe.idp.Document`物件。 （此外，`Recipient`物件可以有Truststore憑證別名或LDAP URL做為憑證來源。）
   * 使用它的建構函式建立儲存許可權和憑證資訊的`CertificateEncryptionIdentity`物件。
   * 叫用`CertificateEncryptionIdentity`物件的`setPerms`方法，並傳遞儲存許可權資訊的`java.util.List`物件。
   * 叫用`CertificateEncryptionIdentity`物件的`setRecipient`方法，並傳遞儲存憑證資訊的`Recipient`物件。
   * 使用它的建構函式建立儲存憑證資訊的`java.util.List`物件。
   * 叫用`java.util.List`物件的新增方法並傳遞`CertificateEncryptionIdentity`物件。 （此`java.util.List`物件會作為引數傳遞至`encryptPDFUsingCertificates`方法。）

1. 設定加密執行階段選項。

   * 透過叫用它的建構函式來建立`CertificateEncryptionOptionSpec`物件。
   * 透過叫用`CertificateEncryptionOptionSpec`物件的`setOption`方法並傳遞指定要加密的檔案資源的`CertificateEncryptionOption`列舉值來指定要加密的PDF檔案資源。 例如，若要加密整個PDF檔案，包括其中繼資料及其附件，請指定`CertificateEncryptionOption.ALL`。
   * 呼叫`CertificateEncryptionOptionSpec`物件的`setCompat`方法，並傳遞指定Acrobat相容性層級的`CertificateEncryptionCompatibility`列舉值，以指定Acrobat相容性選項。 例如，您可以指定`CertificateEncryptionCompatibility.ACRO_7`。

1. 建立憑證加密的PDF檔案。

   透過叫用`EncryptionServiceClient`物件的`encryptPDFUsingCertificates`方法並傳遞下列值，使用憑證加密PDF檔案：

   * 包含要加密之PDF檔案的`com.adobe.idp.Document`物件。
   * 儲存憑證資訊的`java.util.List`物件。
   * 包含加密執行階段選項的`CertificateEncryptionOptionSpec`物件。

   `encryptPDFUsingCertificates`方法傳回包含憑證加密PDF檔案的`com.adobe.idp.Document`物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案。 確定您使用的是`encryptPDFUsingCertificates`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門(SOAP模式)：使用Java API使用憑證加密PDF檔案](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API以憑證加密PDF檔案 {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

使用加密API （Web服務）加密包含憑證的PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立加密使用者端API物件。

   * 使用預設建構函式建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`EncryptionServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得要加密的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存已使用憑證加密的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表要加密之PDF檔案的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派物件的`MTOM`屬性，填入`BLOB`物件。

1. 參考憑證。

   * 使用物件的建構函式建立`Recipient`物件。 此物件將儲存憑證資訊。
   * 使用物件的建構函式建立`BLOB`物件。 此`BLOB`物件將儲存加密PDF檔案的憑證。
   * 建立`System.IO.FileStream`物件，方法是叫用其建構函式，並傳遞代表憑證的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`物件的`MTOM`資料成員，以填入`BLOB`物件。
   * 將儲存憑證的`BLOB`物件指派給`Recipient`物件的`x509Cert`資料成員。
   * 使用它的建構函式建立儲存憑證資訊的`CertificateEncryptionIdentity`物件。
   * 將儲存憑證的`Recipient`物件指派給`CertificateEncryptionIdentity`物件的收件者資料成員。
   * 建立`Object`陣列並將`CertificateEncryptionIdentity`物件指派給`Object`陣列的第一個元素。 此`Object`陣列已作為引數傳遞至`encryptPDFUsingCertificates`方法。

1. 設定加密執行階段選項。

   * 使用物件的建構函式建立`CertificateEncryptionOptionSpec`物件。
   * 指定`CertificateEncryptionOption`列舉值給`CertificateEncryptionOptionSpec`物件的`option`資料成員，以指定要加密的PDF檔案資源。 若要加密整個PDF檔案，包括其中繼資料及其附件，請將`CertificateEncryptionOption.ALL`指派給此資料成員。
   * 將`CertificateEncryptionCompatibility`列舉值指派給`CertificateEncryptionOptionSpec`物件的`compat`資料成員，以指定Acrobat相容性選項。 例如，將`CertificateEncryptionCompatibility.ACRO_7`指派給此資料成員。

1. 建立憑證加密的PDF檔案。

   透過叫用`EncryptionServiceService`物件的`encryptPDFUsingCertificates`方法並傳遞下列值，使用憑證加密PDF檔案：

   * 包含要加密之PDF檔案的`BLOB`物件。
   * 儲存憑證資訊的`Object`陣列。
   * 包含加密執行階段選項的`CertificateEncryptionOptionSpec`物件。

   `encryptPDFUsingCertificates`方法傳回包含憑證加密PDF檔案的`BLOB`物件。

1. 將加密的PDF檔案儲存為PDF檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表受保護PDF檔案檔案位置的字串值。
   * 建立位元組陣列，儲存`encryptPDFUsingCertificates`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`binaryData`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 移除憑證式加密 {#removing-certificate-based-encryption}

憑證式加密可以從PDF檔案中移除，以便使用者可以在Adobe Reader或Acrobat中開啟PDF檔案。 若要從使用憑證加密的PDF檔案中移除加密，必須參考公開金鑰。 從PDF檔案中移除加密後，就不再安全了。

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

若要從PDF檔案中移除憑證式加密，請執行下列步驟：

1. 包含專案檔案。
1. 建立加密服務使用者端。
1. 取得加密的PDF檔案。
1. 移除加密。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

**建立加密服務使用者端**

若要以程式設計方式執行「加密」服務作業，您必須建立「加密」服務使用者端。 如果您使用Java加密服務API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務加密服務API，請建立`EncryptionServiceService`物件。

**取得加密的PDF檔案**

取得加密的PDF檔案以移除憑證式加密。 如果您嘗試從未加密的PDF檔案中移除加密，則會擲回例外狀況。 同樣地，如果您嘗試從密碼加密的檔案移除憑證式加密，則會擲回例外狀況。

**移除加密**

若要從加密的PDF檔案中移除憑證式加密，您需要加密的PDF檔案以及與用於加密PDF檔案的金鑰對應的私密金鑰。 從加密的PDF檔案中移除憑證式加密時，會指定私密金鑰的別名值。 如需公開金鑰的相關資訊，請參閱[使用憑證加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。

>[!NOTE]
>
>私密金鑰會儲存在AEM Forms信任存放區。 將憑證放在那裡時，會指定別名值。

**儲存PDF檔案**

從加密的PDF檔案中移除憑證式加密之後，您可以將PDF檔案儲存為PDF檔案。 使用者可以在Adobe Reader或Acrobat中開啟PDF檔案。

**另請參閱**

[使用Java API移除憑證式加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[使用Web服務API移除憑證式加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API移除憑證式加密 {#remove-certificate-based-encryption-using-the-java-api}

使用加密API (Java)從PDF檔案中移除憑證式加密：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`EncryptionServiceClient`物件。

1. 取得加密的PDF檔案。

   * 使用加密PDF檔案的建構函式，並傳遞指定加密PDF檔案位置的字串值，來建立代表加密檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 移除加密。

   叫用`EncryptionServiceClient`物件的`removePDFCertificateSecurity`方法並傳遞下列值，以從PDF檔案移除憑證式加密：

   * 包含加密PDF檔案的`com.adobe.idp.Document`物件。
   * 字串值，指定與用來加密PDf檔案的金鑰對應的私密金鑰別名。

   `removePDFCertificateSecurity`方法傳回包含不安全PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案。 確定您使用的是`removePDFCredentialSecurity`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門(SOAP模式)：使用Java API移除憑證式加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API移除憑證式加密 {#remove-certificate-based-encryption-using-the-web-service-api}

使用加密API （Web服務）移除憑證式加密：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立加密服務使用者端。

   * 使用預設建構函式建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`EncryptionServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存加密的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表加密PDF檔案的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`物件的`MTOM`資料成員，以填入`BLOB`物件。

1. 移除加密。

   叫用`EncryptionServiceClient`物件的`removePDFCertificateSecurity`方法，並傳遞下列值：

   * 包含代表加密PDF檔案的檔案資料流資料的`BLOB`物件。
   * 字串值，指定與用來加密PDf檔案的私密金鑰對應的公開金鑰別名。

   `removePDFCredentialSecurity`方法傳回包含不安全PDF檔案的`BLOB`物件。

1. 儲存PDF檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表不安全PDF檔案檔案位置的字串值。
   * 建立位元組陣列，儲存`removePDFPasswordSecurity`方法傳回的`BLOB`物件的內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 移除密碼加密 {#removing-password-encryption}

密碼式加密可以從PDF檔案中移除，因此使用者不必指定密碼，即可在Adobe Reader或Acrobat中開啟PDF檔案。 從PDF檔案中移除密碼式加密後，檔案就不再安全。

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

若要從PDF檔案中移除密碼式加密，請執行下列步驟：

1. 包含專案檔案
1. 建立加密服務使用者端。
1. 取得加密的PDF檔案。
1. 移除密碼。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立加密服務使用者端**

若要以程式設計方式執行「加密」服務作業，您必須建立「加密」服務使用者端。 如果您使用Java加密服務API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務加密服務API，請建立`EncryptionServiceService`物件。

**取得加密的PDF檔案**

取得加密的PDF檔案以移除密碼式加密。 如果您嘗試從未加密的PDF檔案中移除加密，則會擲回例外狀況。

**移除密碼**

若要從加密的PDF檔案移除密碼式加密，您需要加密的PDF檔案以及用來從PDF檔案移除加密的主密碼值。 用來開啟以密碼加密的PDF檔案的密碼無法用來移除加密。 使用密碼加密PDF檔案時，會指定主密碼。 (請參閱[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

**儲存PDF檔案**

在「加密」服務從PDF檔案中移除密碼式加密之後，您可以將PDF檔案儲存為PDF檔案。 使用者無須指定密碼，即可在Adobe Reader或Acrobat中開啟PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API移除密碼式加密 {#remove-password-based-encryption-using-the-java-api}

使用加密API (Java)從PDF檔案中移除密碼型加密：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`EncryptionServiceClient`物件。

1. 取得加密的PDF檔案。

   * 使用加密PDF檔案的建構函式，並傳遞指定PDF檔案位置的字串值，來建立代表加密檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 移除密碼。

   呼叫`EncryptionServiceClient`物件的`removePDFPasswordSecurity`方法，並傳遞下列值，以從PDF檔案移除密碼式加密：

   * 包含加密PDF檔案的`com.adobe.idp.Document`物件。
   * 字串值，指定用來從PDF檔案中移除加密的主密碼值。

   `removePDFPasswordSecurity`方法傳回包含不安全PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案。 確定您使用的是`removePDFPasswordSecurity`方法傳回的`Document`物件。

**另請參閱**

[快速入門(SOAP模式)：使用Java API移除密碼式加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### 使用Web服務API移除密碼式加密 {#remove-password-based-encryption-using-the-web-service-api}

使用加密API （Web服務）移除密碼式加密：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立加密服務使用者端。

   * 使用預設建構函式建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`EncryptionServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存密碼加密的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表加密PDF檔案的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`物件的`MTOM`資料成員，以填入`BLOB`物件。

1. 移除密碼。

   叫用`EncryptionServiceService`物件的`removePDFPasswordSecurity`方法，並傳遞下列值：

   * 包含代表加密PDF檔案的檔案資料流資料的`BLOB`物件。
   * 字串值，指定用來從PDF檔案中移除加密的密碼值。 使用密碼加密PDF檔案時，會指定此值。

   `removePDFPasswordSecurity`方法傳回包含不安全PDF檔案的`BLOB`物件。

1. 儲存PDF檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表不安全PDF檔案檔案位置的字串值。
   * 建立位元組陣列，儲存`removePDFPasswordSecurity`方法傳回的`BLOB`物件的內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 解除鎖定加密的PDF檔案 {#unlocking-encrypted-pdf-documents}

必須先解鎖密碼加密或憑證加密的PDF檔案，才能對其執行其他AEM Forms操作。 如果您嘗試在加密的PDF檔案上執行作業，將會產生例外。 解除鎖定加密的PDF檔案後，您可以對其執行一或多個操作。 這些作業可能屬於其他服務，例如Acrobat Reader DC擴充功能服務。

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

若要解除鎖定加密的PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立加密服務使用者端。
1. 取得加密的PDF檔案。
1. 解鎖檔案。
1. 執行AEM Forms作業。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

**建立加密服務使用者端**

若要以程式設計方式執行「加密」服務作業，您必須建立「加密」服務使用者端。 如果您使用Java加密服務API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務加密服務API，請建立`EncryptionServiceService`物件。

**取得加密的PDF檔案**

取得加密的PDF檔案以解除鎖定。 如果您嘗試解除鎖定未加密的PDF檔案，則會擲回例外狀況。

**解除鎖定檔案**

若要解除鎖定以密碼加密的PDF檔案，您需要加密的PDF檔案以及用於開啟以密碼加密的PDF檔案的密碼值。 使用密碼加密PDF檔案時，會指定此值。 (請參閱[使用密碼加密PDF檔案](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

若要解除鎖定憑證加密的PDF檔案，您需要加密的PDF檔案，以及與用來加密PDF檔案的私密金鑰對應的公開金鑰別名值。

**執行AEM Forms作業**

解除鎖定加密的PDF檔案後，您可以對其執行其他服務操作，例如對其套用使用許可權。 此作業屬於Acrobat Reader DC擴充功能服務。

**另請參閱**

[使用Java API解除鎖定加密的PDF檔案](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[使用網站服務API解除鎖定加密的PDF檔案](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API解除鎖定加密的PDF檔案 {#unlock-an-encrypted-pdf-document-using-the-java-api}

使用加密API (Java)解鎖加密的PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-encryption-client.jar。

1. 建立加密服務使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`EncryptionServiceClient`物件。

1. 取得加密的PDF檔案。

   * 使用加密PDF檔案的建構函式，並傳遞指定加密PDF檔案位置的字串值，來建立代表加密檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 解鎖檔案。

   透過叫用`EncryptionServiceClient`物件的`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法，解除鎖定加密的PDF檔案。

   若要解除鎖定使用密碼加密的PDF檔案，請叫用`unlockPDFUsingPassword`方法，並傳遞下列值：

   * 包含密碼加密PDF檔案的`com.adobe.idp.Document`物件。
   * 字串值，指定用來開啟密碼加密PDF檔案的密碼值。 使用密碼加密PDF檔案時，會指定此值。

   若要解除鎖定使用憑證加密的PDF檔案，請叫用`unlockPDFUsingCredential`方法並傳遞下列值：

   * 包含憑證加密PDF檔案的`com.adobe.idp.Document`物件。
   * 字串值，指定與用來加密PDF檔案的私密金鑰對應的公開金鑰別名。

   `unlockPDFUsingPassword`和`unlockPDFUsingCredential`方法都會傳回您傳遞給其他AEM Forms Java方法以執行作業的`com.adobe.idp.Document`物件。

1. 執行AEM Forms作業。

   在未鎖定的PDF檔案上執行AEM Forms作業，以符合您的業務需求。 例如，假設您要將使用許可權套用至未鎖定的PDF檔案，請將`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法傳回的`com.adobe.idp.Document`物件傳遞至`ReaderExtensionsServiceClient`物件的`applyUsageRights`方法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門(SOAP模式)：使用Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (SOAP模式)解除鎖定加密的PDF檔案

[將使用許可權套用至PDF檔案](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API解除鎖定加密的PDF檔案 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

使用加密API （Web服務）解除鎖定加密的PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立加密服務使用者端。

   * 使用預設建構函式建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`EncryptionServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表加密PDF檔案的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`物件的`MTOM`資料成員，以填入`BLOB`物件。

1. 解鎖檔案。

   透過叫用`EncryptionServiceClient`物件的`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法，解除鎖定加密的PDF檔案。

   若要解除鎖定使用密碼加密的PDF檔案，請叫用`unlockPDFUsingPassword`方法，並傳遞下列值：

   * 包含密碼加密PDF檔案的`BLOB`物件。
   * 字串值，指定用來開啟密碼加密PDF檔案的密碼值。 使用密碼加密PDF檔案時，會指定此值。

   若要解除鎖定使用憑證加密的PDF檔案，請叫用`unlockPDFUsingCredential`方法並傳遞下列值：

   * 包含憑證加密PDF檔案的`BLOB`物件。
   * 字串值，指定與用來加密PDf檔案的私密金鑰對應的公開金鑰別名。

   `unlockPDFUsingPassword`和`unlockPDFUsingCredential`方法都會傳回您傳遞給其他AEM Forms方法以執行作業的`com.adobe.idp.Document`物件。

1. 執行AEM Forms作業。

   在未鎖定的PDF檔案上執行AEM Forms作業，以符合您的業務需求。 例如，假設您要將使用許可權套用至解除鎖定的PDF檔案，請將`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法傳回的`BLOB`物件傳遞至`ReaderExtensionsServiceClient`物件的`applyUsageRights`方法。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 決定加密型別 {#determining-encryption-type}

您可以使用Java Encryption Service API或Web服務Encryption Service API，以程式設計方式判斷保護PDF檔案的加密型別。 有時候，必須動態判斷PDF檔案是否已加密，若是，則需判斷加密型別。 例如，您可以決定PDF檔案是使用密碼式加密還是Rights Management原則來保護。

PDF檔案可受下列加密型別保護：

* 密碼式加密
* 憑證式加密
* 由Rights Management服務建立的原則
* 另一種加密型別

>[!NOTE]
>
>如需加密服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

若要判斷保護PDF檔案的加密型別，請執行下列步驟：

1. 包含專案檔案。
1. 建立加密服務使用者端。
1. 取得加密的PDF檔案。
1. 決定加密型別。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

**建立服務使用者端**

若要以程式設計方式執行「加密」服務作業，您必須建立「加密」服務使用者端。 如果您使用Java加密服務API，請建立`EncrytionServiceClient`物件。 如果您使用Web服務加密服務API，請建立`EncryptionServiceService`物件。

**取得加密的PDF檔案**

取得PDF檔案，以判斷要保護的加密型別。

**決定加密型別**

您可以決定保護PDF檔案的加密型別。 如果PDF檔案未受保護，則加密服務會通知您PDF檔案未受保護。

**另請參閱**

[使用Java API判斷加密型別](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[使用Web服務API判斷加密型別](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服務API快速入門](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用原則保護檔案](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### 使用Java API判斷加密型別 {#determine-the-encryption-type-using-the-java-api}

使用加密API (Java)判斷保護PDF檔案的加密型別：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-encryption-client.jar。

1. 建立服務使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`EncryptionServiceClient`物件。

1. 取得加密的PDF檔案。

   * 使用它的建構函式並傳遞指定PDF檔案位置的字串值，建立代表PDF檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 決定加密型別。

   * 透過叫用`EncryptionServiceClient`物件的`getPDFEncryption`方法並傳遞包含PDF檔案的`com.adobe.idp.Document`物件來決定加密型別。 此方法傳回`EncryptionTypeResult`物件。
   * 叫用`EncryptionTypeResult`物件的`getEncryptionType`方法。 此方法會傳回指定加密型別的`EncryptionType`列舉值。 例如，如果PDF檔案受到密碼式加密的保護，此方法會傳回`EncryptionType.PASSWORD`。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入門(SOAP模式)：使用Java API決定加密型別](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API判斷加密型別 {#determine-the-encryption-type-using-the-web-service-api}

使用加密API （Web服務）來判斷保護PDF檔案的加密型別：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立服務使用者端。

   * 使用預設建構函式建立`EncryptionServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`EncryptionServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`EncryptionServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得加密的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表加密PDF檔案的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將位元組陣列的內容指派給`BLOB`物件的`MTOM`資料成員，以填入`BLOB`物件。

1. 決定加密型別。

   * 叫用`EncryptionServiceClient`物件的`getPDFEncryption`方法，並傳遞包含PDF檔案的`BLOB`物件。 此方法傳回`EncryptionTypeResult`物件。
   * 取得`EncryptionTypeResult`物件之`encryptionType`資料方法的值。 例如，如果PDF檔案受到密碼式加密的保護，則此資料成員的值為`EncryptionType.PASSWORD`。

**另請參閱**

[步驟摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
