---
title: 數字簽名和認證文檔
seo-title: Digitally Signing and Certifying Documents
description: 使用簽名服務向PDF文檔添加和刪除數字簽名欄位，檢索PDF文檔中籤名欄位的名稱，修改簽名欄位，數字簽名PDF文檔，驗證PDF文檔中的數字簽名，驗證PDF文檔中的數字簽名，驗證PDF文檔中的所有數字簽名，以及從簽名欄位中刪除數字簽名。
seo-description: Use the Signature service to add and delete digital signature fields to a PDF document, retrieve the names of signature fields located in a PDF document, modify signature fields, digitally sign PDF documents, certify PDF documents, validate digital signatures located in a PDF document, validate all digital signatures located in a PDF document, and remove a digital signature from a signature field.
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '17046'
ht-degree: 0%

---

# 數字簽名和認證文檔 {#digitally-signing-and-certifying-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於簽名服務**

簽章服務可讓您的組織保護其所發送及接收之Adobe PDF檔案的安全與隱私。 此服務使用數位簽名和認證，以確保只有預期的收件者才能更改文檔。 由於安全功能應用於文檔本身，因此文檔在整個生命週期中都保持安全並受到控制。 檔案在離線下載時，以及提交回您的組織時，都會在防火牆之外保持安全。

>[!NOTE]
>
>您可以為簽名服務建立自定義簽名處理程式，該處理程式在調用某些操作(如簽名PDF文檔)時被調用。

**簽名欄位名稱**

某些簽名服務操作要求您指定在其上執行操作的簽名欄位的名稱。 例如，在簽署PDF文檔時，可以指定要簽名的簽名欄位的名稱。 假設簽名欄位的全名為 `form1[0].Form1[0].SignatureField1[0]`. 您可以指定 `SignatureField1[0]` 而非 `form1[0].Form1[0].SignatureField1[0]`.

有時，衝突會導致簽名服務在錯誤的欄位中籤名（或執行需要簽名欄位名稱的其他操作）。 此衝突是名稱的結果 `SignatureField1[0]` 顯示在同一PDF文檔中的兩個或多個位置。 例如，假設PDF文檔包含兩個簽名欄位，名為 `form1[0].Form1[0].SignatureField1[0]` 和 `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` 您可指定 `SignatureField1[0]`. 在這種情況下，簽名服務會簽名它在迭代文檔中的所有簽名欄位時找到的第一個簽名欄位。

如果PDF文檔中有多個簽名欄位，建議您指定簽名欄位的完整名稱。 即，指定 `form1[0].Form1[0].SignatureField1[0]`而非 `SignatureField1[0]`.

您可以使用簽名服務完成以下任務：

* 將數字簽名欄位添加和刪除到PDF文檔。 (請參閱 [添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields).)
* 檢索位於PDF文檔中的簽名欄位的名稱。 (請參閱 [檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* 修改簽名欄位。 (請參閱 [修改簽名欄位](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* 數位簽署PDF檔案。 (請參閱 [數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* 認證PDF檔案。 (請參閱 [認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* 驗證PDF文檔中的數字簽名。 (請參閱 [驗證數字簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* 驗證PDF文檔中的所有數字簽名。 (請參閱 [驗證多個數字簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* 從簽名欄位中刪除數字簽名。 (請參閱 [移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>有關簽名服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)...

## 添加簽名欄位 {#adding-signature-fields}

數字簽名出現在簽名欄位中，簽名欄位是包含簽名的圖形表示的表單欄位。 簽名欄位可以是可見的或不可見的。 簽名者可以使用預先存在的簽名欄位，或以寫程式方式添加簽名欄位。 無論是哪種情況，簽名欄位都必須存在，才能簽名PDF文檔。

您可以使用簽名服務Java API或簽名Web服務API，以寫程式方式添加簽名欄位。 可以向PDF文檔添加多個簽名欄位；但是，每個簽名欄位名稱必須是唯一的。

>[!NOTE]
>
>某些PDF文檔類型不允許您以寫程式方式添加簽名欄位。 有關簽名服務和添加簽名欄位的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要向PDF文檔添加簽名欄位，請執行以下步驟：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 獲取添加簽名欄位的PDF文檔。
1. 添加簽名欄位。
1. 將PDF文檔另存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**獲取添加簽名欄位的PDF文檔**

必須獲取添加簽名欄位的PDF文檔。

**添加簽名欄位**

要成功將簽名欄位添加到PDF文檔，請指定用於標識簽名欄位位置的坐標值。 （如果添加不可見的簽名欄位，則這些值不是必需值。） 此外，還可以指定在將簽名應用到簽名欄位後，PDF文檔中的哪些欄位被鎖定。

**將PDF文檔另存為PDF檔案**

簽名服務將簽名欄位添加到PDF文檔後，您可以將文檔另存為PDF檔案，以便用戶可以在Acrobat或Adobe Reader中開啟該文檔。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API新增簽名欄位 {#add-signature-fields-using-the-java-api}

使用簽名API(Java)添加簽名欄位：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 獲取添加簽名欄位的PDF文檔

   * 建立 `java.io.FileInputStream` 表示簽名欄位添加到的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 添加簽名欄位

   * 建立 `PositionRectangle` 使用其建構子指定簽名欄位位置的對象。 在建構子中，指定坐標值。
   * 如果需要，請建立 `FieldMDPOptions` 指定在將數字簽名應用於簽名欄位時鎖定的欄位的對象。
   * 通過調用 `SignatureServiceClient` 物件 `addSignatureField` 方法並傳遞下列值：

      * A `com.adobe.idp`. `Document` 表示添加簽名欄位的PDF文檔的對象。
      * 指定簽名欄位名稱的字串值。
      * A `java.lang.Integer` 代表新增簽名欄位的頁碼的值。
      * A `PositionRectangle` 指定簽名欄位位置的對象。
      * A `FieldMDPOptions` 指定PDF文檔中在將數字簽名應用到簽名欄位後鎖定的欄位的對象。 此參數值為選用值，您可以傳遞 `null`.
   * A `PDFSeedValueOptions` 指定各種運行時值的對象。 此參數值為選用值，您可以傳遞 `null`.

      此 `addSignatureField` 方法傳回 `com.adobe.idp`. `Document` 表示包含簽名欄位的PDF文檔的對象。
   >[!NOTE]
   >
   >您可以叫用 `SignatureServiceClient` 物件 `addInvisibleSignatureField` 添加不可見簽名欄位的方法。

1. 將PDF文檔另存為PDF檔案

   * 建立 `java.io.File` 物件，並確定副檔名為.pdf。
   * 叫用 `com.adobe.idp`. `Document` 物件 `copyToFile` 複製內容的方法 `Document` 物件。 請確定您使用 `com.adobe.idp`. `Document` 由傳回的物件 `addSignatureField` 方法。

**另請參閱**

[簽名服務API快速入門](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 使用Web服務API添加簽名欄位 {#add-signature-fields-using-the-web-service-api}

要使用簽名API（Web服務）添加簽名欄位：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 物件，使用其預設建構函式。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 獲取添加簽名欄位的PDF文檔

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存將包含簽名欄位的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性（包含位元組陣列的內容）。

1. 添加簽名欄位

   通過調用 `SignatureServiceClient` 物件 `addSignatureField` 方法並傳遞下列值：

   * A `BLOB` 表示添加簽名欄位的PDF文檔的對象。
   * 指定簽名欄位名稱的字串值。
   * 一個整數值，表示要向其添加簽名欄位的頁碼。
   * A `PositionRect` 指定簽名欄位位置的對象。
   * A `FieldMDPOptions` 指定PDF文檔中在將數字簽名應用到簽名欄位後鎖定的欄位的對象。 此參數值為選用值，您可以傳遞 `null`.
   * A `PDFSeedValueOptions` 指定各種運行時值的對象。 此參數值為選用值，您可以傳遞 `null`.

   此 `addSignatureField` 方法傳回 `BLOB` 表示包含簽名欄位的PDF文檔的對象。

1. 將PDF文檔另存為PDF檔案

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示將包含簽名欄位的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `addSignatureField` 方法。 取得 `BLOB` 物件 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢索簽名欄位名稱 {#retrieving-signature-field-names}

您可以檢索位於要簽名或認證的PDF文檔中的所有簽名欄位的名稱。 如果您不確定位於PDF文檔中的簽名欄位名稱，或要驗證名稱，可以用寫程式方式檢索它們。 簽名服務返回簽名欄位的完全限定名稱，例如 `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>有關簽名服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟摘要 {#summary_of_steps-1}

要檢索簽名欄位名稱，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 獲取包含簽名欄位的PDF文檔。
1. 檢索簽名欄位名稱。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**獲取包含簽名欄位的PDF文檔**

檢索包含簽名欄位的PDF文檔。

**檢索簽名欄位名稱**

檢索包含一個或多個簽名欄位的PDF文檔後，可以檢索簽名欄位名稱。

**另請參閱**

[使用Java API檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[使用Web服務API檢索簽名欄位](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API檢索簽名欄位名稱 {#retrieve-signature-field-names-using-the-java-api}

使用簽名API(Java)檢索簽名欄位名稱：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 獲取包含簽名欄位的PDF文檔

   * 建立 `java.io.FileInputStream` 表示包含簽名欄位的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 檢索簽名欄位名稱

   * 通過調用 `SignatureServiceClient` 物件 `getSignatureFieldList` 方法和傳遞 `com.adobe.idp.Document` 包含包含簽名欄位的PDF文檔的對象。 此方法會傳回 `java.util.List` 物件，其中每個元素包含 `PDFSignatureField` 物件。 使用此對象，可以獲取有關簽名欄位的其他資訊，如簽名欄位是否可見。
   * 重複 `java.util.List` 用於確定是否存在簽名欄位名稱的對象。 對於PDF文檔中的每個簽名欄位，您可以獲得單獨的 `PDFSignatureField` 物件。 要獲取簽名欄位的名稱，請調用 `PDFSignatureField` 物件 `getName` 方法。 此方法會傳回指定簽名欄位名稱的字串值。

**另請參閱**

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[快速入門（SOAP模式）:使用Java API檢索簽名欄位名稱](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API檢索簽名欄位 {#retrieve-signature-field-using-the-web-service-api}

使用簽名API（Web服務）檢索簽名欄位名稱：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 物件，使用其預設建構函式。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 獲取包含簽名欄位的PDF文檔

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存包含簽名欄位的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 欄位位位元組陣列內容。

1. 檢索簽名欄位名稱

   * 通過調用以檢索簽名欄位名稱 `SignatureServiceClient` 物件 `getSignatureFieldList` 方法和傳遞 `BLOB` 包含包含簽名欄位的PDF文檔的對象。 此方法會傳回 `MyArrayOfPDFSignatureField` 每個元素包含的集合物件 `PDFSignatureField` 物件。
   * 重複 `MyArrayOfPDFSignatureField` 用於確定是否存在簽名欄位名稱的對象。 對於PDF文檔中的每個簽名欄位，您可以獲取 `PDFSignatureField` 物件。 要獲取簽名欄位的名稱，請調用 `PDFSignatureField` 物件 `getName` 方法。 此方法會傳回指定簽名欄位名稱的字串值。

**另請參閱**

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改簽名欄位 {#modifying-signature-fields}

您可以使用Java API和Web服務API修改PDF檔案中的簽名欄位。 修改簽名欄位涉及操作其簽名欄位鎖定字典值或種子值字典值。

A *欄位鎖字典* 指定簽名欄位時鎖定的欄位清單。 鎖定的欄位可防止使用者對欄位進行變更。 A *種子值字典* 包含在應用簽名時使用的約束資訊。 例如，您可以變更權限，以控制可能發生的動作，而不使簽名失效。

通過修改現有簽名欄位，您可以對PDF文檔進行更改以反映不斷變化的業務需求。 例如，新業務要求可能需要在文檔簽名後鎖定所有文檔欄位。

本節說明如何通過修改欄位鎖定字典和種子值字典值來修改簽名欄位。 對簽名欄位鎖定字典所做的更改會導致簽名欄位時PDF文檔中的所有欄位被鎖定。 對種子值字典所做的更改禁止對文檔進行特定類型的更改。

>[!NOTE]
>
>有關簽名服務和修改簽名欄位的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-2}

要修改PDF文檔中的簽名欄位，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 獲取包含要修改的簽名欄位的PDF文檔。
1. 設定字典值。
1. 修改簽名欄位。
1. 將PDF文檔另存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包括LiveCycleJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**獲取包含要修改的簽名欄位的PDF文檔**

檢索包含要修改的簽名欄位的PDF文檔。

**設定字典值**

要修改簽名欄位，請將值分配給其欄位鎖定字典或種子值字典。 指定簽名欄位鎖定字典值包括指定簽名欄位時鎖定的PDF文檔欄位。 （本節探討如何鎖定所有欄位。）

可設定下列種子值字典值：

* **修訂檢查**:指定在將簽名應用到簽名欄位時是否執行吊銷檢查。
* **憑證選項**:為證書種子值字典指定值。 建議您先熟悉憑證種子值字典，再指定憑證選項。 (請參閱 [PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **摘要選項**:指派用於簽署的摘要演算法。 有效值為SHA1、SHA256、SHA384、SHA512和RIPEMD160。
* **篩選**:指定與簽名欄位一起使用的篩選器。 例如，您可以使用Adobe.PPKLite篩選器。 (請參閱 [PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **標幟選項**:指定與此簽名欄位關聯的標誌值。 值1表示簽署者只能為條目使用指定值。 值0表示允許其他值。 位位置如下：

   * **1（篩選）:** 用於簽名欄位的簽名處理程式
   * **2（子篩選）:** 指出簽署時可使用之可接受編碼的名稱陣列
   * **3(V)**:用於簽名欄位的簽名處理程式的最低所需版本號
   * **4（理由）:** 字串的陣列，指定簽署檔案的可能原因
   * **5(PDFLegalWarnings):** 指定可能的法律證明的字串陣列

* **法律證明**:認證文檔時，會自動掃描特定類型的內容，這些內容可能使文檔的可見內容模糊或產生誤導。 例如，注釋可能會遮蔽對於了解正在認證的內容非常重要的文本。 掃描過程會生成警告，指示是否存在此類內容。 它也提供可能已產生警告之內容的額外說明。
* **權限**:指定可用於PDF文檔而不使簽名失效的權限。
* **原因**:指定必須簽署此文檔的原因。
* **時間戳記**:指定時間戳選項。 例如，您可以設定所使用時間戳記伺服器的URL。
* **版本**:指定用於簽名欄位的簽名處理程式的最小版本號。

**修改簽名欄位**

建立簽名服務客戶端後，檢索包含要修改的簽名欄位的PDF文檔，並設定字典值，您可以指示簽名服務修改簽名欄位。 然後，簽名服務返回包含已修改簽名欄位的PDF文檔。 原始PDF文檔不受影響。

**將PDF文檔另存為PDF檔案**

將包含已修改簽名欄位的PDF文檔保存為PDF檔案，以便用戶可以在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[簽名服務API快速入門](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API修改簽名欄位 {#modify-signature-fields-using-the-java-api}

使用簽名API(Java)修改簽名欄位：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 獲取包含要修改的簽名欄位的PDF文檔

   * 建立 `java.io.FileInputStream` 表示包含要修改的簽名欄位的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 設定字典值

   * 建立 `PDFSignatureFieldProperties` 物件，使用其建構子。 A `PDFSignatureFieldProperties` 對象儲存簽名欄位鎖字典和種子值字典資訊。
   * 建立 `PDFSeedValueOptionSpec` 物件，使用其建構子。 此物件可讓您設定種子值字典值。
   * 禁止通過調用 `PDFSeedValueOptionSpec` 物件 `setMdpValue` 方法和傳遞 `MDPPermissions.NoChanges` 枚舉值。
   * 建立 `FieldMDPOptionSpec` 物件，使用其建構子。 此對象允許您設定簽名欄位鎖定字典值。
   * 調用以鎖定PDF文檔中的所有欄位 `FieldMDPOptionSpec` 物件 `setMdpValue` 方法和傳遞 `FieldMDPAction.ALL` 枚舉值。
   * 調用 `PDFSignatureFieldProperties` 物件 `setSeedValue` 方法和傳遞 `PDFSeedValueOptionSpec` 物件。
   * 通過調用 `PDFSignatureFieldProperties`物件 `setFieldMDP` 方法和傳遞 `FieldMDPOptionSpec` 物件。

   >[!NOTE]
   >
   >若要查看您可設定的所有種子值字典值，請參閱 `PDFSeedValueOptionSpec` 類別參考。 (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. 修改簽名欄位

   調用 `SignatureServiceClient` 物件 `modifySignatureField` 方法並傳遞下列值：

   * 此 `com.adobe.idp.Document` 儲存包含要修改的簽名欄位的PDF文檔的對象
   * 指定簽名欄位名稱的字串值
   * 此 `PDFSignatureFieldProperties` 儲存簽名欄位鎖字典和種子值字典資訊的對象

   此 `modifySignatureField` 方法傳回 `com.adobe.idp.Document` 儲存包含已修改簽名欄位的PDF文檔的對象。

1. 將PDF文檔另存為PDF檔案

   * 建立 `java.io.File` 物件，並確定副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 物件。 請確定您使用 `com.adobe.idp.Document` 物件 `modifySignatureField` 方法傳回。

### 使用Web服務API修改簽名欄位 {#modify-signature-fields-using-the-web-service-api}

使用簽名API（Web服務）修改簽名欄位：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 物件，使用其預設建構函式。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 獲取包含要修改的簽名欄位的PDF文檔

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存包含要修改的簽名欄位的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性位元組陣列的內容。

1. 設定字典值

   * 建立 `PDFSignatureFieldProperties` 物件，使用其建構子。 該對象儲存簽名欄位鎖字典和種子值字典資訊。
   * 建立 `PDFSeedValueOptionSpec` 物件，使用其建構子。 此物件可讓您設定種子值字典值。
   * 通過指定 `MDPPermissions.NoChanges` 枚舉值 `PDFSeedValueOptionSpec` 物件 `mdpValue` 資料成員。
   * 建立 `FieldMDPOptionSpec` 物件，使用其建構子。 此對象允許您設定簽名欄位鎖定字典值。
   * 通過指定 `FieldMDPAction.ALL` 枚舉值 `FieldMDPOptionSpec` 物件 `mdpValue` 資料成員。
   * 通過分配 `PDFSeedValueOptionSpec` 物件 `PDFSignatureFieldProperties` 物件 `seedValue` 資料成員。
   * 通過分配 `FieldMDPOptionSpec` 物件 `PDFSignatureFieldProperties` 物件 `fieldMDP` 資料成員。

   >[!NOTE]
   >
   >若要查看您可設定的所有種子值字典值，請參閱 `PDFSeedValueOptionSpec` 類別參考。 (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 修改簽名欄位

   調用 `SignatureServiceClient` 物件 `modifySignatureField` 方法並傳遞下列值：

   * 此 `BLOB` 儲存包含要修改的簽名欄位的PDF文檔的對象
   * 指定簽名欄位名稱的字串值
   * 此 `PDFSignatureFieldProperties` 儲存簽名欄位鎖字典和種子值字典資訊的對象

   此 `modifySignatureField` 方法傳回 `BLOB` 儲存包含已修改簽名欄位的PDF文檔的對象。

1. 將PDF文檔另存為PDF檔案

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示將包含簽名欄位的PDF文檔的檔案位置，以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `BLOB` 物件 `addSignatureField` 方法會傳回。 取得 `BLOB` 物件 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數位簽署PDF檔案 {#digitally-signing-pdf-documents}

數字簽名可以應用於PDF文檔，以提供一定的安全級別。 數字簽名（如手寫簽名）提供了一種手段，使簽名者能夠識別自己，並對文檔進行聲明。 用於數字簽名文檔的技術有助於確保簽名者和接收者都清楚簽名的內容，並確信文檔自簽名後沒有更改。

PDF檔案採用公鑰技術簽署。 簽名者有兩個密鑰：公鑰和私鑰。 私密金鑰儲存在使用者的憑證中，且在簽署時必須可用。 公開金鑰儲存在使用者的憑證中，收件者必須能使用該憑證來驗證簽名。 有關已撤銷證書的資訊可在由證書頒發機構(CA)分發的證書吊銷清單(CRL)和線上證書狀態協定(OCSP)響應中找到。 簽名時間可從稱為時間戳頒發機構的可信源獲得。

>[!NOTE]
>
>您必須確定將憑證新增至AEM Forms，才能以數位方式簽署PDF檔案。 使用管理控制台或使用信任管理器API以程式設計方式新增憑證。 (請參閱 [使用信任管理器API導入憑據](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

您可以以程式設計方式數位簽署PDF檔案。 以數位方式簽署PDF檔案時，您必須參考AEM Forms中存在的安全憑證。 憑據是用於簽名的私鑰。

簽名服務在簽名PDF文檔時執行以下步驟：

1. 簽名服務通過傳遞請求中指定的別名從Truststore中檢索憑據。
1. Truststore將搜索指定的憑據。
1. 憑證會傳回至簽章服務，並用來簽署檔案。 系統會根據別名快取憑證，以備日後請求之用。

有關處理安全憑據的資訊，請參閱 *安裝和部署AEM Forms* 應用程式伺服器指南。

>[!NOTE]
>
>簽名和認證文檔之間存在差異。 (請參閱 [認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>並非所有PDF檔案都支援簽署。 有關簽名服務和數字簽名文檔的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>簽名服務不支援具有嵌入PDF資料的XDP檔案作為操作的輸入，例如驗證文檔。 此動作會導致簽名服務擲出 `PDFOperationException`. 若要解決此問題，請使用PDF公用程式服務，將XDP檔案轉換為PDF檔案，然後將轉換的PDF檔案傳遞至簽名服務操作。 (請參閱 [使用PDF實用程式](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**密碼nShield HSM憑據**

使用nCipher nShield HSM憑據來簽名或認證PDF文檔時，必須重新啟動部署在AEM Forms上的J2EE應用程式伺服器，才能使用新憑據。 但是，您可以設定配置值，從而使簽名或認證操作正常工作，而不重新啟動J2EE應用程式伺服器。

您可以在位於/opt/nfast/cknfastrc(或c:\nfast\cknfastrc)的cknfastrc檔案中添加以下配置值：

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將此配置值添加到cknfastrc檔案後，即可使用新憑據，而無需重新啟動J2EE應用程式伺服器。

**簽名不受信任**

在認證和簽署同一PDF文檔時，如果不信任認證簽名，則在Acrobat或Adobe Reader中開啟PDF文檔時，第一個簽名將出現一個黃色三角形。 必須信任認證簽名才能避免這種情況。

**簽署以XFA為基礎的表單的檔案**

如果您嘗試使用簽章服務API簽署以XFA為基礎的表單，資料可能會從 `View` `Signed` `Version` 位於Acrobat。 例如，請考量下列工作流程：

* 使用Designer建立的XDP檔案，可以合併包含簽名欄位的表單設計和包含表單資料的XML資料。 您可使用Forms服務產生互動式PDF檔案。
* 您使用簽名服務API簽署PDF文檔。

### 步驟摘要 {#summary_of_steps-3}

要數字簽署PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名服務客戶端。
1. 取得要簽署的PDF檔案。
1. 簽署PDF檔案。
1. 將已簽名的PDF文檔另存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**取得要簽署的PDF檔案**

要簽名PDF文檔，必須獲取包含簽名欄位的PDF文檔。 如果PDF文檔不包含簽名欄位，則無法簽名。 簽名欄位可通過使用Designer或以寫程式方式添加。

**簽署PDF檔案**

在簽署PDF文檔時，您可以設定簽名服務使用的運行時選項。 您可以設定下列選項：

* 外觀選項
* 吊銷檢查
* 時間戳值

通過使用 `PDFSignatureAppearanceOptionSpec` 物件。 例如，您可以叫用 `PDFSignatureAppearanceOptionSpec` 物件 `setShowDate` 方法與傳遞 `true`.

您還可以指定是否執行吊銷檢查，該檢查確定用於數字簽名PDF文檔的證書是否已被吊銷。 要執行吊銷檢查，可以指定以下值之一：

* **無檢查**:不執行吊銷檢查。
* **BestEffort**:始終嘗試檢查是否吊銷鏈中的所有證書。 如果檢查中出現任何問題，則假定吊銷有效。 如果發生任何失敗，請假設憑證未撤銷。
* **CheckIfAvailable:** 如果可取消資訊，則檢查是否吊銷鏈中的所有證書。 如果檢查中出現任何問題，則假定吊銷無效。 如果發生任何失敗，假設憑證已撤銷且無效。 （這是預設值。）
* **AlwaysCheck**:檢查是否撤銷鏈中的所有證書。 如果任何證書中沒有吊銷資訊，則假定吊銷無效。

要對證書執行吊銷檢查，可以使用 `CRLOptionSpec` 物件。 但是，如果要執行吊銷檢查，並且您沒有為CRL伺服器指定URL，則簽名服務將從證書中獲取該URL。

在執行吊銷檢查時，可以使用聯機證書狀態協定(OCSP)伺服器，而不使用CRL伺服器。 通常，當使用OCSP伺服器而不是CRL伺服器時，執行吊銷檢查的速度會更快。 (請參閱「線上憑證狀態通訊協定」，網址為 [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

您可以使用Adobe應用程式和服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器首先在Adobe應用程式和服務中設定，則檢查OCSP伺服器，然後檢查CRL伺服器。 （請參閱AAC說明中的「使用信任存放區管理憑證和憑證」）。

如果指定不執行吊銷檢查，則簽名服務不會檢查用於簽名或證明文檔的證書是否已被吊銷。 即忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>雖然可以在證書中指定CRL或OCSP伺服器，但可以使用 `CRLOptionSpec` 和 `OCSPOptionSpec` 物件。 例如，要覆蓋CRL伺服器，可以調用 `CRLOptionSpec` 物件 `setLocalURI` 方法。

時間戳是指跟蹤已簽名或已認證文檔被修改的時間的過程。 文檔簽名後，即使文檔所有者也不應修改它。 時間戳有助於強制簽署或認證文檔的有效性。 您可以使用 `TSPOptionSpec` 物件。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務中逐個瀏覽各個部分並進行相應的快速啟動，使用撤銷檢查。 由於沒有指定CRL或OCSP伺服器資訊，因此從用於對PDF文檔進行數字簽名的證書中獲取伺服器資訊。

若要成功簽署PDF檔案，您可以指定將包含數位簽名的簽名欄位的完全限定名稱，例如 `form1[0].#subform[1].SignatureField3[3]`. 使用XFA表單欄位時，也可以使用簽名欄位的部分名稱： `SignatureField3[3]`.

您還必須參考安全憑據以數字簽名PDF文檔。 要引用安全憑據，請指定別名。 別名是對實際憑據的引用，該憑據可能位於PKCS#12檔案中（副檔名為.pfx），或硬體安全模組(HSM)中。 有關安全憑據的資訊，請參見 *安裝和部署AEM Forms* 應用程式伺服器指南。

**保存已簽名的PDF文檔**

簽章服務對PDF檔案進行數位簽署後，您可以將其儲存為PDF檔案，讓使用者能在Acrobat或Adobe Reader中開啟該檔案。

**另請參閱**

[使用Java API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[使用網站服務API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### 使用Java API數位簽署PDF檔案 {#digitally-sign-pdf-documents-using-the-java-api}

使用簽章API(Java)以數位方式簽署PDF檔案：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 取得要簽署的PDF檔案

   * 建立 `java.io.FileInputStream` 用其建構子並傳遞指定PDF文檔位置的字串值來表示要數字簽名的PDF文檔的對象。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 簽署PDF檔案

   叫用PDF檔案 `SignatureServiceClient` 物件 `sign` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 表示要簽名的PDF文檔的對象。
   * 表示將包含數字簽名的簽名欄位的名稱的字串值。
   * A `Credential` 表示用於對PDF文檔進行數字簽名的憑據的對象。 建立 `Credential` 對象，方法是調用 `Credential` 對象的靜態 `getInstance` 方法，並傳遞指定與安全憑據對應的別名值的字串值。
   * A `HashAlgorithm` 指定靜態資料成員的對象，該靜態資料成員表示用於摘要PDF文檔的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 來使用SHA1演算法。
   * 代表PDF檔案進行數位簽署原因的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數字簽名外觀的對象。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * A `java.lang.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。
   * 安 `OCSPOptionSpec` 儲存線上證書狀態協定(OCSP)支援首選項的對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`.
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援偏好設定的物件。 此參數為選用參數，可以是 `null`. 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   此 `sign` 方法傳回 `com.adobe.idp.Document` 表示簽名PDF文檔的對象。

1. 保存已簽名的PDF文檔

   * 建立 `java.io.File` 物件，並確定副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法和傳遞 `java.io.File`複製 `Document` 物件。 請確定您使用 `com.adobe.idp.Document` 由傳回的物件 `sign` 方法。

**另請參閱**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[快速入門（SOAP模式）:使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API數位簽署PDF檔案 {#digitally-signing-pdf-documents-using-the-web-service-api}

使用簽名API（Web服務）對PDF文檔進行數字簽名：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 物件，使用其預設建構函式。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得要簽署的PDF檔案

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存已簽名的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示要簽名的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性位元組陣列的內容。

1. 簽署PDF檔案

   叫用PDF檔案 `SignatureServiceClient` 物件 `sign` 方法並傳遞下列值：

   * A `BLOB` 表示要簽名的PDF文檔的對象。
   * 表示將包含數字簽名的簽名欄位的名稱的字串值。
   * A `Credential` 表示用於對PDF文檔進行數字簽名的憑據的對象。 建立 `Credential` 對象，使用其建構子，並通過為 `Credential` 物件 `alias` 屬性。
   * A `HashAlgorithm` 指定靜態資料成員的對象，該靜態資料成員表示用於摘要PDF文檔的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 來使用SHA1演算法。
   * 一個布林值，指定是否使用哈希算法。
   * 代表PDF檔案進行數位簽署原因的字串值。
   * 代表簽署者位置的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數字簽名外觀的對象。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * A `System.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。 如果完成了此吊銷檢查，則它嵌入到簽名中。 預設為 `false`。
   * 安 `OCSPOptionSpec` 儲存線上證書狀態協定(OCSP)支援首選項的對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`. 如需此物件的相關資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援偏好設定的物件。 此參數為選用參數，可以是 `null`.

   此 `sign` 方法傳回 `BLOB` 表示簽名PDF文檔的對象。

1. 保存已簽名的PDF文檔

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `sign` 方法。 取得 `BLOB` 物件 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數位簽署互動式Forms {#digitally-signing-interactive-forms}

您可以簽署Forms服務建立的互動式表單。 例如，請考量下列工作流程：

* 您可以合併使用Designer建立的基於XFA的PDF表單，以及使用Forms服務在XML文檔中找到的表單資料。 Forms伺服器會轉譯互動式表單。
* 您使用簽名服務API簽署互動式表單。

結果為數位簽署的互動式PDF表單。 簽署以XFA表單為基礎的PDF表單時，請確定您將PDF檔案儲存為Adobe靜態PDF表單。 如果您嘗試簽署儲存為「PDF動態PDF」表單的Adobe表單，則會發生例外狀況。 因為您正在簽署從Forms服務傳回的表單，請確定表單包含簽名欄位。

>[!NOTE]
>
>您必須確定已將憑證新增至AEM Forms，才能數位簽署互動式表單。 使用管理控制台或使用信任管理器API以程式設計方式新增憑證。 (請參閱 [使用信任管理器API導入憑據](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

使用Forms服務API時，請設定 `GenerateServerAppearance` 運行時選項 `true`. 此執行階段選項可確保在Acrobat或Adobe Reader中開啟時，伺服器上產生的表單外觀仍有效。 建議您在使用Forms API產生要簽署的互動式表單時，設定此執行階段選項。

>[!NOTE]
>
>閱讀數位簽署互動式Forms前，建議您先熟悉簽署PDF檔案。 (請參閱 [數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### 步驟摘要 {#summary_of_steps-4}

若要以數位方式簽署Forms服務傳回的互動式表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms和簽名客戶端。
1. 使用Forms服務取得互動式表單。
1. 簽署互動式表單。
1. 將已簽名的PDF文檔另存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立Forms和簽名客戶端**

因為此工作流同時調用Forms和簽名服務，請同時建立Forms服務客戶端和簽名服務客戶端。

**使用Forms服務取得互動式表單**

您可以使用Forms服務取得要簽署的互動式PDF表單。 從AEM Forms開始，您可以 `com.adobe.idp.Document` 物件至包含要呈現的表單的Forms服務。 此方法的名稱為 `renderPDFForm2`. 此方法會傳回 `com.adobe.idp.Document` 包含要簽名的表單的對象。 你可以通過 `com.adobe.idp.Document` 執行個體。

同樣地，如果您使用網站服務，則可以傳遞 `BLOB` Forms服務傳回至簽名服務的例項。

>[!NOTE]
>
>與「數位簽署互動式Forms」區段相關聯的快速入門會叫用 `renderPDFForm2` 方法。

**簽署互動式表單**

在簽署PDF文檔時，您可以設定簽名服務使用的運行時選項。 您可以設定下列選項：

* 外觀選項
* 吊銷檢查
* 時間戳值

通過使用 `PDFSignatureAppearanceOptionSpec` 物件。 例如，您可以叫用 `PDFSignatureAppearanceOptionSpec` 物件 `setShowDate` 方法與傳遞 `true`.

**保存已簽名的PDF文檔**

簽名服務對PDF文檔進行數字簽名後，您可以將其另存為PDF檔案。 PDF檔案可在Acrobat或Adobe Reader中開啟。

**另請參閱**

[使用Java API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[使用網站服務API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[轉譯互動式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### 使用Java API數位簽署互動式表單 {#digitally-sign-an-interactive-form-using-the-java-api}

使用Forms和簽名API(Java)以數位方式簽署互動式表單：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar和adobe-forms-client.jar。

1. 建立Forms和簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。
   * 建立 `FormsServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 使用Forms服務取得互動式表單

   * 建立 `java.io.FileInputStream` 代表PDF檔案的物件，可使用其建構函式傳遞至Forms服務。 傳遞指定PDF文檔位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。
   * 建立 `java.io.FileInputStream` 表示包含表單資料的XML檔案的物件，可透過其建構函式傳遞至Forms服務。 傳遞指定XML檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。
   * 建立 `PDFFormRenderSpec` 用於設定運行時選項的對象。 叫用 `PDFFormRenderSpec` 物件 `setGenerateServerAppearance` 方法和傳遞 `true`.
   * 叫用 `FormsServiceClient` 物件 `renderPDFForm2` 方法，並傳遞下列值：

      * A `com.adobe.idp.Document` 包含要呈現的PDF表單的對象。
      * A `com.adobe.idp.Document` 包含要與表單合併資料的物件。
      * A `PDFFormRenderSpec` 儲存運行時選項的對象。
      * A `URLSpec` 包含Forms服務所需URI值的物件。 您可以指定 `null` ，以取得此參數值。
      * A `java.util.HashMap` 儲存檔案附件的物件。 這是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。

      此 `renderPDFForm2` 方法傳回 `FormsResult` 包含表單資料流的物件

   * 叫用以擷取PDF表單 `FormsResult` 物件 `getOutputContent` 方法。 此方法會傳回 `com.adobe.idp.Document` 代表互動式表單的物件。


1. 簽署互動式表單

   叫用PDF檔案 `SignatureServiceClient` 物件 `sign` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 表示要簽名的PDF文檔的對象。 請確定此物件為 `com.adobe.idp.Document` 從Forms服務取得的物件。
   * 表示簽名欄位名稱的字串值。
   * A `Credential` 表示用於對PDF文檔進行數字簽名的憑據的對象。 建立 `Credential` 對象，方法是調用 `Credential` 對象的靜態 `getInstance` 方法。 傳遞一個字串值，該字串值指定與安全憑據對應的別名值。
   * A `HashAlgorithm` 指定靜態資料成員的對象，該靜態資料成員表示用於摘要PDF文檔的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 來使用SHA1演算法。
   * 代表PDF檔案進行數位簽署原因的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數字簽名外觀的對象。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * A `java.lang.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。
   * 安 `OCSPPreferences` 儲存線上證書狀態協定(OCSP)支援首選項的對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`.
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援偏好設定的物件。 此參數為選用參數，可以是 `null`.

   此 `sign` 方法傳回 `com.adobe.idp.Document` 表示簽名PDF文檔的對象。

1. 保存已簽名的PDF文檔

   * 建立 `java.io.File` 物件，並確定副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法和傳遞 `java.io.File`複製 `Document` 物件。 請確定您使用 `com.adobe.idp.Document` 物件 `sign` 方法傳回。

**另請參閱**

[數位簽署互動式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[快速入門（SOAP模式）:使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API數位簽署互動式表單 {#digitally-sign-an-interactive-form-using-the-web-service-api}

使用Forms和簽名API（網站服務）數位簽署互動式表單：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 由於此客戶端應用程式調用了兩個AEM Forms服務，因此請建立兩個服務引用。 為與簽名服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   為與Forms服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   因為 `BLOB` 資料類型是兩個服務參考的共同類型，完全限定 `BLOB` 資料類型。 在相應的Web服務快速入門中，所有 `BLOB` 例項已完全限定。

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Forms和簽名客戶端

   * 建立 `SignatureServiceClient` 物件，使用其預設建構函式。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >對Forms服務用戶端重複這些步驟。

1. 使用Forms服務取得互動式表單

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存已簽名的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示要簽名的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性位元組陣列的內容。
   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 物件可用來儲存表單資料。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示包含表單資料的XML檔案的檔案位置，以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性位元組陣列的內容。
   * 建立 `PDFFormRenderSpec` 用於設定運行時選項的對象。 指派值 `true` 到 `PDFFormRenderSpec` 物件 `generateServerAppearance` 欄位。
   * 叫用 `FormsServiceClient` 物件 `renderPDFForm2` 方法，並傳遞下列值：

      * A `BLOB` 包含要呈現的PDF表單的對象。
      * A `BLOB` 包含要與表單合併資料的物件。
      * A `PDFFormRenderSpec` 儲存運行時選項的對象。
      * A `URLSpec` 包含Forms服務所需URI值的物件。 您可以指定 `null` ，以取得此參數值。
      * A `java.util.HashMap` 儲存檔案附件的物件。 這是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。
      * 長輸出參數，用於儲存表單中的頁數。
      * 用於地區設定值的字串輸出參數。
      * A `FormResult` 值，此為用於儲存互動式表單的輸出參數。
   * 叫用PDF表單 `FormsResult` 物件 `outputContent` 欄位。 此欄位會儲存 `BLOB` 代表互動式表單的物件。


1. 簽署互動式表單

   叫用PDF檔案 `SignatureServiceClient` 物件 `sign` 方法並傳遞下列值：

   * A `BLOB` 表示要簽名的PDF文檔的對象。 使用 `BLOB` 由Forms服務傳回的例項。
   * 表示簽名欄位名稱的字串值。
   * A `Credential` 表示用於對PDF文檔進行數字簽名的憑據的對象。 建立 `Credential` 對象，使用其建構子，並通過為 `Credential` 物件 `alias` 屬性。
   * A `HashAlgorithm` 指定靜態資料成員的對象，該靜態資料成員表示用於摘要PDF文檔的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 來使用SHA1演算法。
   * 一個布林值，指定是否使用哈希算法。
   * 代表PDF檔案進行數位簽署原因的字串值。
   * 代表簽署者位置的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數字簽名外觀的對象。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * A `System.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。 如果完成了此吊銷檢查，則它嵌入到簽名中。 預設為 `false`。
   * 安 `OCSPPreferences` 儲存線上證書狀態協定(OCSP)支援首選項的對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`. 如需此物件的相關資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援偏好設定的物件。 此參數為選用參數，可以是 `null`.

   此 `sign` 方法傳回 `BLOB` 表示簽名PDF文檔的對象。

1. 保存已簽名的PDF文檔

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `sign` 方法。 取得 `BLOB` 物件 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[數位簽署互動式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 認證PDF檔案 {#certifying-pdf-documents}

您可以使用一種稱為認證簽名的特定簽名類型對PDF文檔進行認證，從而保護文檔安全。 經認證的簽名與數字簽名在以下方面有區別：

* 它必須是應用於PDF文檔的第一個簽名；也就是說，在應用經認證的簽名時，文檔中的任何其他簽名欄位必須未簽名。 在PDF文檔中僅允許一個經認證的簽名。 如果要簽名和認證PDF文檔，則必須在簽名前對其進行認證。 認證PDF檔案後，您可以數位簽署其他簽名欄位。
* 文檔的作者或創作者可以指定文檔可以以某些方式修改，而不使經認證的簽名失效。 例如，該文檔可允許填寫表單或注釋。 如果作者指定不允許進行特定修改，Acrobat會限制使用者以此方式修改檔案。 如果進行了此類修改（例如使用其他應用程式），則經認證的簽名無效，並且Acrobat在用戶開啟文檔時發出警告。 （使用未經認證的簽名時，不會阻止修改，且正常的編輯操作不會使原始簽名無效。）
* 在簽名時，將掃描文檔以查找可能使文檔內容模糊或具有誤導性的特定內容類型。 例如，注釋可能會遮蔽頁面上對於了解正在認證的內容非常重要的文字。 可以提供關於此類內容的說明（法律證明）。

您可以使用簽名服務Java API或簽名Web服務API，以寫程式方式為PDF文檔進行認證。 驗證PDF文檔時，必須引用憑據服務中存在的安全憑據。 有關安全憑據的資訊，請參見 *安裝和部署AEM Forms* 應用程式伺服器指南。

>[!NOTE]
>
>在認證和簽署同一PDF文檔時，如果不信任認證簽名，則在Acrobat或Adobe Reader中開啟PDF文檔時，第一個簽名簽名旁會出現一個黃色三角形。 必須信任認證簽名才能避免這種情況。

>[!NOTE]
>
>使用nCipher nShield HSM憑據來簽名或認證PDF文檔時，必須重新啟動部署了AEM Forms的J2EE應用程式伺服器，才能使用新憑據。 但是，您可以設定配置值，從而使簽名或認證操作正常工作，而不重新啟動J2EE應用程式伺服器。

您可以在位於/opt/nfast/cknfastrc(或c:\nfast\cknfastrc)的cknfastrc檔案中添加以下配置值：

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將此配置值添加到cknfastrc檔案後，即可使用新憑據，而無需重新啟動J2EE應用程式伺服器。

>[!NOTE]
>
>有關簽名服務和證明文檔的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-5}

要驗證PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 取得PDF檔案以進行認證。
1. 驗證PDF文檔。
1. 將認證的PDF文檔另存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名客戶端**

在以寫程式方式執行簽名操作之前，必須建立簽名客戶端。

**取得PDF檔案以進行認證**

要驗證PDF文檔，必須獲取包含簽名欄位的PDF文檔。 如果PDF文檔不包含簽名欄位，則無法對其進行認證。 簽名欄位可通過使用Designer或以寫程式方式添加。 有關以寫程式方式添加簽名欄位的資訊，請參見 [添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields).

**認證PDF檔案**

要成功認證PDF文檔，您需要以下由簽名服務使用的輸入值來認證PDF文檔：

* **PDF檔案**:包含簽名欄位的PDF文檔，該簽名欄位是包含經認證簽名的圖形表示的表單欄位。 PDF文檔必須包含簽名欄位，才能進行認證。 簽名欄位可通過使用Designer或以寫程式方式添加。 (請參閱 [添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **簽名欄位名稱**:經認證的簽名欄位的完全限定名稱。 以下是範例值： `form1[0].#subform[1].SignatureField3[3]`. 使用XFA表單欄位時，也可以使用簽名欄位的部分名稱： `SignatureField3[3]`. 如果為欄位名稱傳遞了空值，則動態建立並認證不可見的簽名欄位。
* **安全憑據**:用於驗證PDF文檔的憑據。 此安全憑據包含密碼和別名，該密碼和別名必須與位於憑據服務中的憑據中顯示的別名匹配。 別名是對實際憑據的引用，該憑據可能位於PKCS#12檔案中（副檔名為.pfx）或硬體安全模組(HSM)中。
* **雜湊演算法**:用於摘要PDF檔案的雜湊演算法。
* **簽名原因**:顯示在Acrobat或Adobe Reader中的值，讓其他使用者了解PDF檔案獲得認證的原因。
* **簽署者的位置**:憑據指定的簽名者的位置。
* **聯絡資訊**:簽名者的聯繫資訊，如地址和電話號碼。
* **權限資訊**:控制最終用戶可以在文檔上執行的操作而不導致認證簽名無效的權限。 例如，您可以設定權限，使得對PDF文檔的任何更改都會導致經認證的簽名無效。
* **法律解釋**:認證文檔時，會自動掃描特定類型的內容，這些內容可能使文檔的內容模糊或產生誤導。 例如，注釋可能會遮蔽頁面上對於了解正在認證的內容非常重要的文字。 掃描過程會生成有關這些類型內容的警告。 此值提供可能已產生警告之內容的額外說明。
* **外觀選項**:控制認證簽名外觀的選項。 例如，認證的簽名可以顯示日期資訊。
* **吊銷檢查**:該值指定是否對簽名者的證書執行吊銷檢查。 預設設定為 `false` 表示未執行吊銷檢查。
* **OCSP設定**:聯機證書狀態協定(OCSP)支援的設定，該協定提供有關用於驗證PDF文檔的憑據的狀態的資訊。 例如，您可以指定伺服器的URL，該URL提供有關用於登錄到PDF文檔的憑據的資訊。
* **CRL設定**:完成吊銷檢查時，證書吊銷清單(CRL)首選項的設定。 例如，您可以指定始終檢查憑據是否被吊銷。
* **時間戳**:定義應用於認證簽名的時間戳資訊的設定。 時間戳表示特定資料是在某個時間之前建立的。 此知識有助於在簽署者與驗證者之間建立信任關係。

**將認證的PDF文檔另存為PDF檔案**

簽章服務認證PDF檔案後，您可以將其儲存為PDF檔案，讓使用者能在Acrobat或Adobe Reader中開啟該檔案。

**另請參閱**

[使用Java API驗證PDF檔案](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[使用Web服務API驗證PDF文檔](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API驗證PDF檔案 {#certify-pdf-documents-using-the-java-api}

使用簽名API(Java)驗證PDF文檔：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 取得PDF檔案以進行認證

   * 建立 `java.io.FileInputStream` 表示要認證的PDF文檔的對象，使用其建構子並傳遞指定PDF文檔位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 認證PDF檔案

   叫用以驗證PDF檔案 `SignatureServiceClient` 物件 `certify` 方法並傳遞下列值：

   * 此 `com.adobe.idp.Document` 表示要認證的PDF文檔的對象。
   * 表示將包含簽名的簽名欄位的名稱的字串值。
   * A `Credential` 表示用於驗證PDF文檔的憑據的對象。 建立 `Credential` 對象，方法是調用 `Credential` 對象的靜態 `getInstance` 方法，並傳遞指定與安全憑據對應的別名值的字串值。
   * A `HashAlgorithm` 指定靜態資料成員的對象，該靜態資料成員表示用於摘要PDF文檔的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 來使用SHA1演算法。
   * 表示PDF文檔被認證原因的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * A `MDPPermissions` 對象，指定可在PDF文檔上執行的使簽名失效的操作。
   * A `PDFSignatureAppearanceOptions` 控制認證簽名外觀的對象。 如果需要，通過調用方法(如 `setShowDate`.
   * 字串值，可說明使簽名無效的動作。
   * A `java.lang.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。 如果完成了此吊銷檢查，則它嵌入到簽名中。 預設為 `false`。
   * A `java.lang.Boolean` 指定是否鎖定要認證的簽名欄位的對象。 如果欄位被鎖定，則簽名欄位被標籤為只讀，其屬性無法修改，並且沒有必需權限的任何人無法清除該欄位。 預設為 `false`。
   * 安 `OCSPPreferences` 儲存線上證書狀態協定(OCSP)支援首選項的對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`. 有關此對象的資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援偏好設定的物件。 例如，在您建立 `TSPPreferences` 物件，您可以叫用 `TSPPreferences` 物件 `setTspServerURL` 方法。 此參數為選用參數，可以是 `null`. 如需詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

   此 `certify` 方法傳回 `com.adobe.idp.Document` 表示經認證的PDF文檔的對象。

1. 將認證的PDF文檔另存為PDF檔案

   * 建立 `java.io.File` 物件，並確定副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 物件。

**另請參閱**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[快速入門（SOAP模式）:使用Java API驗證PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API驗證PDF文檔 {#certify-pdf-documents-using-the-web-service-api}

使用簽名API（Web服務）驗證PDF文檔：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 物件，使用其預設建構函式。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得PDF檔案以進行認證

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存經認證的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示要認證的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 資料成員是位元組陣列的內容。

1. 認證PDF檔案

   叫用以驗證PDF檔案 `SignatureServiceClient` 物件 `certify` 方法並傳遞下列值：

   * 此 `BLOB` 表示要認證的PDF文檔的對象。
   * 表示將包含簽名的簽名欄位的名稱的字串值。
   * A `Credential` 表示用於驗證PDF文檔的憑據的對象。 建立 `Credential` 對象（使用其建構子），並通過為 `Credential` 物件 `alias` 屬性。
   * A `HashAlgorithm` 指定靜態資料成員的對象，該靜態資料成員表示用於摘要PDF文檔的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 來使用SHA1演算法。
   * 一個布林值，指定是否使用哈希算法。
   * 表示PDF文檔被認證原因的字串值。
   * 代表簽署者位置的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * 安 `MDPPermissions` 對象的靜態資料成員，該成員指定可對使簽名無效的PDF文檔執行的操作。
   * 一個布林值，它指定是否使用 `MDPPermissions` 以上一個參數值傳遞的物件。
   * 一個字串值，說明使簽名無效的操作。
   * A `PDFSignatureAppearanceOptions` 控制認證簽名外觀的對象。 建立 `PDFSignatureAppearanceOptions` 物件，使用其建構子。 可以通過設定簽名的一個資料成員來修改簽名的外觀。
   * A `System.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。 如果完成了此吊銷檢查，則它嵌入到簽名中。 預設為 `false`。
   * A `System.Boolean` 指定是否鎖定要認證的簽名欄位的對象。 如果欄位被鎖定，則簽名欄位被標籤為只讀，其屬性無法修改，並且沒有必需權限的任何人無法清除該欄位。 預設為 `false`。
   * A `System.Boolean` 指定是否鎖定簽名欄位的對象。 就是說，如果你通過 `true` 轉入上一個參數，然後傳入 `true` 到此參數。
   * 安 `OCSPPreferences` 用於儲存線上證書狀態協定(OCSP)支援首選項的對象，該協定提供有關用於驗證PDF文檔的憑據的狀態的資訊。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`.
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援偏好設定的物件。 例如，在您建立 `TSPPreferences` 物件，您可以設定 `TSPPreferences` 物件 `tspServerURL` 資料成員。 此參數為選用參數，可以是 `null`.

   此 `certify` 方法傳回 `BLOB` 表示經認證的PDF文檔的對象。

1. 將認證的PDF文檔另存為PDF檔案

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示將包含經認證的PDF文檔的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `certify` 方法。 取得 `BLOB` 物件 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證數字簽名 {#verifying-digital-signatures}

數字簽名可以被驗證以確保簽名的PDF文檔未被修改，並且數字簽名有效。 驗證數字簽名時，您可以檢查簽名的狀態和簽名的屬性，如簽名者的身份。 信任數字簽名之前，建議您驗證它。 驗證數字簽名時，請參考包含數字簽名的PDF文檔。

假設簽名者的身份未知。 在Acrobat中開啟PDF檔案時，警告訊息會指出簽署者的身分不明，如下圖所示。

![vd_vd_verifsig](assets/vd_vd_verifysig.png)

同樣，當以寫程式方式驗證數字簽名時，可以確定簽名者的身份狀態。 例如，如果您驗證上圖所示檔案中的數位簽名，結果會是簽名者的身份未知。

>[!NOTE]
>
>有關簽名服務和驗證數字簽名的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-6}

要驗證數字簽名，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 獲取包含要驗證的簽名的PDF文檔。
1. 設定PKI運行時選項。
1. 驗證數字簽名。
1. 確定簽名的狀態。
1. 確定簽名者的身份。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，請建立簽名服務客戶端。

**獲取包含要驗證的簽名的PDF文檔**

要驗證用於數字簽名或認證PDF文檔的簽名，請獲取包含簽名的PDF文檔。

**設定PKI運行時選項**

設定簽名服務在驗證PDF文檔中籤名時使用的以下PKI運行時選項：

* 驗證時間
* 吊銷檢查
* 時間戳值

作為設定這些選項的一部分，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），以指出要使用目前時間。 如需不同時間值的相關資訊，請參閱 `VerificationTime` 枚舉值 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

您還可以指定是否在驗證過程中執行吊銷檢查。 例如，您可以執行吊銷檢查以確定證書是否被吊銷。 有關吊銷檢查選項的資訊，請參見 `RevocationCheckStyle` 枚舉值 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

要對證書執行吊銷檢查，請使用 `CRLOptionSpec` 物件。 但是，如果您未指定URL到CRL伺服器，則簽名服務將從證書中獲取該URL。

在執行吊銷檢查時，可以使用聯機證書狀態協定(OCSP)伺服器，而不使用CRL伺服器。 通常，當使用OCSP伺服器而不是CRL伺服器時，執行吊銷檢查的速度會更快。 (請參閱 [聯機證書狀態協定](https://tools.ietf.org/html/rfc2560).)

您可以通過使用Adobe應用程式和服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器首先在Adobe應用程式和服務中設定，則檢查OCSP伺服器，然後檢查CRL伺服器。

如果您未執行吊銷檢查，則簽名服務不檢查證書是否被吊銷。 即忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用 `CRLOptionSpec` 和 `OCSPOptionSpec` 物件。 例如，要覆蓋CRL伺服器，可以調用 `CRLOptionSpec` 物件 `setLocalURI` 方法。

時間戳是跟蹤已簽名或經認證的文檔被修改的時間的過程。 文檔簽名後，任何人都無法修改它。 時間戳有助於強制簽署或認證文檔的有效性。 您可以使用 `TSPOptionSpec` 物件。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務快速啟動中，驗證時間設定為 `VerificationTime.CURRENT_TIME` 並且吊銷檢查設定為 `RevocationCheckStyle.BestEffort`. 由於未指定CRL或OCSP伺服器資訊，因此從證書中獲取伺服器資訊。

**驗證數字簽名**

要成功驗證簽名，請指定包含簽名的簽名欄位的完全限定名稱，例如 `form1[0].#subform[1].SignatureField3[3]`. 使用XFA表單欄位時，您也可以使用簽名欄位的部分名稱： `SignatureField3`.

預設情況下，簽名服務將文檔在驗證後簽名的時間限制為65分鐘。 如果用戶嘗試在當前時間驗證簽名，並且簽名時間晚於當前時間並且在65分鐘內，則簽名服務不會建立驗證錯誤。

>[!NOTE]
>
>有關驗證簽名時需要的其他值，請參見 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**確定簽名的狀態**

作為驗證數字簽名的一部分，您可以檢查簽名的狀態。

**確定簽名者的身份**

您可以決定簽署者的身分，其可以是下列其中一個值：

* **未知**:此簽名者未知，因為無法執行簽名者驗證。
* **受信任**:此簽名者是受信任的。
* **不受信任**:不信任此簽名者。

**另請參閱**

[使用Java API驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[使用Web服務API驗證數字簽名](#verify-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API驗證數位簽名 {#verify-digital-signatures-using-the-java-api}

使用簽名服務API(Java)驗證數字簽名：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 獲取包含要驗證的簽名的PDF文檔

   * 建立 `java.io.FileInputStream` 表示包含要使用其建構子驗證的簽名的PDF文檔的對象。 傳遞指定PDF文檔位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 設定PKI運行時選項

   * 建立 `PKIOptions` 物件，使用其建構子。
   * 調用 `PKIOptions` 物件 `setVerificationTime` 方法和傳遞 `VerificationTime` 指定驗證時間的枚舉值。
   * 通過調用 `PKIOptions` 物件 `setRevocationCheckStyle` 方法和傳遞 `RevocationCheckStyle` 指定是否執行吊銷檢查的枚舉值。

1. 驗證數字簽名

   叫用 `SignatureServiceClient` 物件 `verify2` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 包含數字簽名或認證的PDF文檔的對象。
   * 表示包含要驗證的簽名的簽名欄位名稱的字串值。
   * A `PKIOptions` 包含PKI運行時選項的對象。
   * A `VerifySPIOptions` 包含SPI資訊的實例。 您可以指定 `null` 的URL。

   此 `verify2` 方法傳回 `PDFSignatureVerificationInfo` 包含可用於驗證數字簽名的資訊的對象。

1. 確定簽名的狀態

   * 通過調用 `PDFSignatureVerificationInfo` 物件 `getStatus` 方法。 此方法會傳回 `SignatureStatus` 指定簽名狀態的對象。 例如，如果未修改簽名的PDF文檔，則此方法將返回 `SignatureStatus.DocumentSigNoChanges`.

1. 確定簽名者的身份

   * 叫用 `PDFSignatureVerificationInfo` 物件 `getSigner` 方法。 此方法會傳回 `IdentityInformation` 物件。
   * 叫用 `IdentityInformation` 物件 `getStatus` 確定簽名者身份的方法。 此方法會傳回 `IdentityStatus` 指定身分的枚舉值。 例如，如果簽名者受信任，則此方法會傳回 `IdentityStatus.TRUSTED`.

**另請參閱**

[驗證數字簽名](#verify-digital-signatures-using-the-java-api)

[快速入門（SOAP模式）:使用Java API驗證數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API驗證數字簽名 {#verify-digital-signatures-using-the-web-service-api}

使用簽名服務API（Web服務）驗證數字簽名：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 物件，使用其預設建構函式。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 獲取包含要驗證的簽名的PDF文檔

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存包含要驗證的數字或認證簽名的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性位元組陣列的內容。

1. 設定PKI運行時選項

   * 建立 `PKIOptions` 物件，使用其建構子。
   * 通過分配 `PKIOptions` 物件 `verificationTime` 資料成員 `VerificationTime` 指定驗證時間的枚舉值。
   * 通過分配 `PKIOptions` 物件 `revocationCheckStyle` 資料成員 `RevocationCheckStyle` 指定是否執行吊銷檢查的枚舉值。

1. 驗證數字簽名

   叫用 `SignatureServiceClient` 物件 `verify2` 方法並傳遞下列值：

   * 此 `BLOB` 包含數字簽名或認證的PDF文檔的對象。
   * 表示包含要驗證的簽名的簽名欄位名稱的字串值。
   * A `PKIOptions` 包含PKI運行時選項的對象。
   * A `VerifySPIOptions` 包含SPI資訊的實例。 您可以指定 `null` 的URL。

   此 `verify2` 方法傳回 `PDFSignatureVerificationInfo` 包含可用於驗證數字簽名的資訊的對象。

1. 確定簽名的狀態

   通過獲取 `PDFSignatureVerificationInfo` 物件 `status` 資料成員。 此資料成員儲存 `SignatureStatus` 指定簽名狀態的對象。 例如，如果修改了已簽名的PDF文檔，則 `status` 資料成員儲存值 `SignatureStatus.DocumentSigNoChanges`.

1. 確定簽名者的身份

   * 通過檢索 `PDFSignatureVerificationInfo` 物件 `signer` 資料成員。 此成員返回 `IdentityInformation` 物件。
   * 擷取 `IdentityInformation` 物件 `status` 確定簽名者身份的資料成員。 此資料成員返回 `IdentityStatus` 指定身分的枚舉值。 例如，如果簽名者受信任，則此成員返回 `IdentityStatus.TRUSTED`.

**另請參閱**

[驗證數字簽名](#verify-digital-signatures-using-the-java-api)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證多個數字簽名 {#verifying-multiple-digital-signatures}

AEM Forms提供驗證位於PDF檔案中的所有數位簽名的方法。 假設PDF文檔包含多個數字簽名，因為業務流程需要多個簽名者的簽名。 例如，考慮一項金融交易，該交易既需要貸款官的簽名，又需要經理的簽名。 您可以使用簽名服務Java API或Web服務API來驗證PDF文檔中的所有簽名。 驗證多個數字簽名時，您可以檢查每個簽名的狀態和屬性。 信任數字簽名之前，建議您驗證它。 建議您熟悉驗證單一數位簽名。

>[!NOTE]
>
>有關簽名服務和驗證數字簽名的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-7}

要驗證多個數字簽名，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 獲取包含要驗證的簽名的PDF文檔。
1. 設定PKI運行時選項。
1. 檢索所有數字簽名。
1. 逐一查看所有簽名。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，請建立簽名服務客戶端。

**獲取包含要驗證的簽名的PDF文檔**

要驗證用於數字簽名或認證PDF文檔的簽名，請獲取包含簽名的PDF文檔。

**設定PKI運行時選項**

設定簽名服務在驗證PDF文檔中的所有簽名時使用的以下PKI運行時選項：

* 驗證時間
* 吊銷檢查
* 時間戳值

作為設定這些選項的一部分，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），以指出要使用目前時間。 如需不同時間值的相關資訊，請參閱 `VerificationTime` 枚舉值 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

您還可以指定是否在驗證過程中執行吊銷檢查。 例如，您可以執行吊銷檢查以確定證書是否被吊銷。 有關吊銷檢查選項的資訊，請參見 `RevocationCheckStyle` 枚舉值 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

要對證書執行吊銷檢查，請使用 `CRLOptionSpec` 物件。 但是，如果您沒有為CRL伺服器指定URL，則簽名服務將從證書中獲取該URL。

在執行吊銷檢查時，可以使用聯機證書狀態協定(OCSP)伺服器，而不使用CRL伺服器。 通常，使用OCSP伺服器（而不是CRL伺服器）時，執行吊銷檢查的速度會更快。 (請參閱 [聯機證書狀態協定](https://tools.ietf.org/html/rfc2560).)

您可以通過使用Adobe應用程式和服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是先在Adobe應用程式和服務中設定的，則會檢查OCSP伺服器，然後檢查CRL伺服器。

如果您未執行吊銷檢查，則簽名服務不檢查證書是否被吊銷。 即忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用 `CRLOptionSpec` 和 `OCSPOptionSpec` 物件。 例如，要覆蓋CRL伺服器，可以調用 `CRLOptionSpec` 物件 `setLocalURI` 方法。

時間戳是跟蹤已簽名或經認證的文檔被修改的時間的過程。 文檔簽名後，任何人都無法修改它。 時間戳有助於強制簽署或認證文檔的有效性。 您可以使用 `TSPOptionSpec` 物件。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務快速啟動中，驗證時間設定為 `VerificationTime.CURRENT_TIME` 並且吊銷檢查設定為 `RevocationCheckStyle.BestEffort`. 由於未指定CRL或OCSP伺服器資訊，因此從證書中獲取伺服器資訊。

**檢索所有數字簽名**

要驗證PDF文檔中的所有數字簽名，請從PDF文檔中檢索數字簽名。 所有簽名都在清單中返回。 作為驗證數字簽名的一部分，請檢查簽名的狀態。

>[!NOTE]
>
>與驗證單個數字簽名時不同，驗證多個簽名時不需要指定簽名欄位名稱。

**重複查看所有簽名**

逐個反覆檢查每個簽名。 即對於每個簽名，驗證數字簽名，並檢查簽名者的身份和每個簽名的狀態。 (請參閱 [驗證數字簽名](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>如果要求是整個文檔，則無需重複執行所有簽名。

**另請參閱**

[使用Java API驗證多個數位簽名](#verify-digital-signatures-using-the-java-api)

[使用Web服務API驗證多個數字簽名](#verify-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API驗證多個數位簽名 {#verify-multiple-digital-signatures-using-the-java-api}

使用簽名服務API(Java)驗證多個數字簽名：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 獲取包含要驗證的簽名的PDF文檔

   * 建立 `java.io.FileInputStream` 表示包含多個數字簽名的PDF文檔的對象，要使用其建構子進行驗證。 傳遞指定PDF文檔位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 設定PKI運行時選項

   * 建立 `PKIOptions` 物件，使用其建構子。
   * 調用 `PKIOptions` 物件 `setVerificationTime` 方法和傳遞 `VerificationTime` 指定驗證時間的枚舉值。
   * 通過調用 `PKIOptions` 物件 `setRevocationCheckStyle` 方法和傳遞 `RevocationCheckStyle` 指定是否執行吊銷檢查的枚舉值。

1. 檢索所有數字簽名

   叫用 `SignatureServiceClient` 物件 `verifyPDFDocument` 方法，並傳遞下列值：

   * A `com.adobe.idp.Document` 包含包含多個數字簽名的PDF文檔的對象。
   * A `PKIOptions` 包含PKI運行時選項的對象。
   * A `VerifySPIOptions` 包含SPI資訊的實例。 您可以指定 `null` 的URL。

   此 `verifyPDFDocument` 方法傳回 `PDFDocumentVerificationInfo` 包含PDF文檔中所有數字簽名資訊的對象。

1. 重複查看所有簽名

   * 叫用 `PDFDocumentVerificationInfo` 物件 `getVerificationInfos` 方法。 此方法會傳回 `java.util.List` 其中每個元素都是 `PDFSignatureVerificationInfo` 物件。 使用 `java.util.Iterator` 物件，以逐一查看簽名清單。
   * 使用 `PDFSignatureVerificationInfo` 對象，您可以通過調用 `PDFSignatureVerificationInfo` 物件 `getStatus` 方法。 此方法會傳回 `SignatureStatus` 靜態資料成員通知您簽名的狀態的對象。 例如，如果簽名未知，則此方法返回 `SignatureStatus.DocumentSignatureUnknown`.

**另請參閱**

[驗證多個數字簽名](#verifying-multiple-digital-signatures)

[快速入門（SOAP模式）:使用Java API驗證多個數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[驗證數字簽名](#verify-digital-signatures-using-the-java-api)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API驗證多個數字簽名 {#verifying-multiple-digital-signatures-using-the-web-service-api}

使用簽名服務API（Web服務）驗證多個數字簽名：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 物件，使用其預設建構函式。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 獲取包含要驗證的簽名的PDF文檔

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象儲存包含多個數字簽名以驗證的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性位元組陣列的內容。

1. 設定PKI運行時選項

   * 建立 `PKIOptions` 物件，使用其建構子。
   * 通過分配 `PKIOptions` 物件 `verificationTime` 資料成員 `VerificationTime` 指定驗證時間的枚舉值。
   * 通過分配 `PKIOptions` 物件 `revocationCheckStyle` 資料成員 `RevocationCheckStyle` 指定是否執行吊銷檢查的枚舉值。

1. 檢索所有數字簽名

   叫用 `SignatureServiceClient` 物件 `verifyPDFDocument` 方法，並傳遞下列值：

   * A `BLOB` 包含包含多個數字簽名的PDF文檔的對象。
   * A `PKIOptions` 包含PKI運行時選項的對象。
   * A `VerifySPIOptions` 包含SPI資訊的實例。 可以為此參數指定null。

   此 `verifyPDFDocument` 方法傳回 `PDFDocumentVerificationInfo` 包含PDF文檔中所有數字簽名資訊的對象。

1. 重複查看所有簽名

   * 透過取得 `PDFDocumentVerificationInfo` 物件 `verificationInfos` 資料成員。 此資料成員返回 `Object` 陣列，其中每個元素都是 `PDFSignatureVerificationInfo` 物件。
   * 使用 `PDFSignatureVerificationInfo` 對象，您可以通過獲取 `PDFSignatureVerificationInfo` 物件 `status` 資料成員。 此資料成員返回 `SignatureStatus` 靜態資料成員通知您簽名的狀態的對象。 例如，如果簽名未知，則此方法返回 `SignatureStatus.DocumentSignatureUnknown`.

**另請參閱**

[驗證多個數字簽名](#verifying-multiple-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 移除數位簽名 {#removing-digital-signatures}

必須先從簽名欄位中刪除數字簽名，然後才能應用較新的數字簽名。 無法覆蓋數字簽名。 如果嘗試將數字簽名應用到包含簽名的簽名欄位，則會發生異常。

>[!NOTE]
>
>有關簽名服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-8}

要從簽名欄位中刪除數字簽名，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 獲取包含要刪除的簽名的PDF文檔。
1. 從簽名欄位中刪除數字簽名。
1. 將PDF文檔另存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**獲取包含要刪除的簽名的PDF文檔**

要從PDF文檔中刪除簽名，必須獲取包含簽名的PDF文檔。

**從簽名欄位中刪除數字簽名**

要成功從PDF文檔中刪除數字簽名，必須指定包含數字簽名的簽名欄位的名稱。 此外，您必須擁有移除數位簽名的權限；否則，會發生例外。

**將PDF文檔另存為PDF檔案**

簽名服務從簽名欄位中刪除數字簽名後，您可以將PDF文檔另存為PDF檔案，以便用戶可以在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[使用Java API移除數位簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[使用Web服務API刪除數字簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API移除數位簽名 {#remove-digital-signatures-using-the-java-api}

使用簽名API(Java)刪除數字簽名：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 獲取包含要刪除的簽名的PDF文檔

   * 建立 `java.io.FileInputStream` 表示包含要刪除的簽名的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 從簽名欄位中刪除數字簽名

   叫用 `SignatureServiceClient` 物件 `clearSignatureField` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 表示包含要刪除的簽名的PDF文檔的對象。
   * 一個字串值，它指定包含數字簽名的簽名欄位的名稱。

   此 `clearSignatureField` 方法傳回 `com.adobe.idp.Document` 表示從中刪除數字簽名的PDF文檔的對象。

1. 將PDF文檔另存為PDF檔案

   * 建立 `java.io.File` 物件，並確定副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法。 傳遞 `java.io.File` 要複製 `com.adobe.idp.Document` 物件。 請確定您使用 `Document` 由傳回的物件 `clearSignatureField` 方法。

**另請參閱**

[移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[快速入門（SOAP模式）:使用Java API移除數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API刪除數字簽名 {#remove-digital-signatures-using-the-web-service-api}

使用簽名API（Web服務）刪除數字簽名：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 物件，使用其預設建構函式。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 獲取包含要刪除的簽名的PDF文檔

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存包含要刪除的數字簽名的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性（包含位元組陣列的內容）。

1. 從簽名欄位中刪除數字簽名

   叫用 `SignatureServiceClient` 物件 `clearSignatureField` 方法並傳遞下列值：

   * A `BLOB` 包含簽名PDF文檔的對象。
   * 一個字串值，它表示包含要刪除的數字簽名的簽名欄位的名稱。

   此 `clearSignatureField` 方法傳回 `BLOB` 表示從中刪除數字簽名的PDF文檔的對象。

1. 將PDF文檔另存為PDF檔案

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子，並傳遞一個字串值，該字串值表示包含空簽名欄位的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `sign` 方法。 取得 `BLOB` 物件 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
