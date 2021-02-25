---
title: 數位簽署和認證檔案
seo-title: 數位簽署和認證檔案
description: 使用簽名服務將數位簽名欄位新增及刪除至PDF檔案、擷取PDF檔案中的簽名欄位名稱、修改簽名欄位、數位簽署PDF檔案、認證PDF檔案、驗證PDF檔案中的數位簽名、驗證PDF檔案中的所有數位簽名，以及從簽名欄位移除數位簽名。
seo-description: 使用簽名服務將數位簽名欄位新增及刪除至PDF檔案、擷取PDF檔案中的簽名欄位名稱、修改簽名欄位、數位簽署PDF檔案、認證PDF檔案、驗證PDF檔案中的數位簽名、驗證PDF檔案中的所有數位簽名，以及從簽名欄位移除數位簽名。
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '17113'
ht-degree: 0%

---


# 數位簽署和認證檔案{#digitally-signing-and-certifying-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於簽名服務**

簽名服務可讓貴組織保護其發送及接收之Adobe PDF檔案的安全性和隱私權。 本服務使用數位簽章和認證，以確保只有預期的收件者才能變更檔案。 由於安全性功能會套用至檔案本身，因此檔案在整個生命週期中都會保持安全並受到控制。 檔案在防火牆外、離線下載時，以及送出回您的組織時，都能保有安全。

>[!NOTE]
>
>您可以為「簽名」服務建立自訂的簽名處理常式，該處理常式會在呼叫特定作業（例如簽署PDF檔案）時被叫用。

**簽名欄位名**

某些簽名服務操作要求您指定執行操作的簽名欄位的名稱。 例如，在簽署PDF檔案時，您可以指定要簽署的簽名欄位名稱。 假設簽名欄位的全名為`form1[0].Form1[0].SignatureField1[0]`。 您可以指定`SignatureField1[0]`而非`form1[0].Form1[0].SignatureField1[0]`。

有時衝突會導致簽名服務在錯誤欄位中籤名（或執行另一個需要簽名欄位名稱的操作）。 此衝突是名稱`SignatureField1[0]`出現在同一PDF檔案中兩個或多個位置的結果。 例如，假設PDF檔案包含兩個名為`form1[0].Form1[0].SignatureField1[0]`和`form1[0].Form1[0].SubForm1[0].SignatureField1[0]`的簽名欄位，而您指定`SignatureField1[0]`。 在這種情況下，簽章服務會簽署它在重複檔案中所有簽名欄位時所找到的第一個簽名欄位。

如果PDF檔案中有多個簽名欄位，建議您指定簽名欄位的完整名稱。 也就是說，請指定`form1[0].Form1[0].SignatureField1[0]`而非`SignatureField1[0]`。

您可以使用簽名服務完成下列工作：

* 將數位簽章欄位新增及刪除至PDF檔案。 （請參閱[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。）
* 擷取PDF檔案中的簽名欄位名稱。 （請參閱[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)。）
* 修改簽名欄位。 （請參閱[修改簽名欄位](digitally-signing-certifying-documents.md#modifying-signature-fields)。）
* 數位簽署PDF檔案。 （請參閱[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)）。
* 認證PDF檔案。 （請參閱[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)。）
* 驗證PDF檔案中的數位簽名。 （請參閱[驗證數位簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures)）。
* 驗證PDF檔案中的所有數位簽名。 （請參閱[驗證多個數位簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures)）。
* 從簽名欄位移除數位簽名。 （請參閱[移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)）。

>[!NOTE]
>
>如需簽名服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 添加簽名欄位{#adding-signature-fields}

數位簽名會出現在簽名欄位中，這些欄位是包含簽名圖形表示的表格欄位。 簽名欄位可以是可見或不可見的。 簽署者可以使用預先存在的簽名欄位，或以程式設計方式新增簽名欄位。 在這兩種情況下，簽名欄位必須存在，才能簽署PDF檔案。

您可以使用簽名服務Java API或簽名網站服務API，以程式設計方式新增簽名欄位。 您可以在PDF檔案中新增多個簽名欄位；但是，每個簽名欄位名必須是唯一的。

>[!NOTE]
>
>有些PDF檔案類型不允許您以程式設計方式新增簽名欄位。 如需有關「簽名」服務和新增簽名欄位的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

若要將簽名欄位新增至PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得新增簽名欄位的PDF檔案。
1. 新增簽名欄位。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

**建立簽名用戶端**

您必須先建立簽名服務用戶端，才能以程式設計方式執行簽名服務作業。

**取得新增簽名欄位的PDF檔案**

您必須取得新增簽名欄位的PDF檔案。

**新增簽名欄位**

若要成功將簽名欄位新增至PDF檔案，請指定用以識別簽名欄位位置的坐標值。 （如果您新增不可見的簽名欄位，則不需要這些值。） 此外，您也可以指定在將簽名套用至簽名欄位後，PDF檔案中的哪些欄位會被鎖定。

**將PDF檔案儲存為PDF檔案**

在簽章服務新增簽名欄位至PDF檔案後，您可以將檔案儲存為PDF檔案，讓使用者在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API {#add-signature-fields-using-the-java-api}新增簽名欄位

使用簽名API(Java)新增簽名欄位：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`SignatureServiceClient`對象。

1. 取得新增簽名欄位的PDF檔案

   * 建立`java.io.FileInputStream`物件，此物件代表PDF檔案，並使用其建構函式並傳遞指定PDF檔案位置的字串值，將簽名欄位新增至該PDF檔案。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 新增簽名欄位

   * 使用`PositionRectangle`物件的建構函式，建立指定簽名欄位位置的物件。 在建構函式中，指定坐標值。
   * 如果需要，請建立`FieldMDPOptions`對象，該對象指定將數字簽名應用於簽名欄位時鎖定的欄位。
   * 叫用`SignatureServiceClient`物件的`addSignatureField`方法並傳遞下列值，將簽名欄位新增至PDF檔案：

      * A `com.adobe.idp`. `Document` 物件，代表新增簽名欄位的PDF檔案。
      * 指定簽名欄位名稱的字串值。
      * `java.lang.Integer`值，代表新增簽名欄位的頁碼。
      * `PositionRectangle`物件，指定簽名欄位的位置。
      * `FieldMDPOptions`物件，指定在數位簽章套用至簽名欄位後鎖定的PDF檔案欄位。 此參數值是可選的，您可以傳遞`null`。
   * `PDFSeedValueOptions`物件，指定各種執行時間值。 此參數值是可選的，您可以傳遞`null`。

      `addSignatureField`方法返回`com.adobe.idp`。 `Document` 物件，代表包含簽名欄位的PDF檔案。
   >[!NOTE]
   >
   >您可以叫用`SignatureServiceClient`物件的`addInvisibleSignatureField`方法，以新增不可見的簽名欄位。

1. 將PDF檔案儲存為PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 叫用`com.adobe.idp`。 `Document` 物件的方 `copyToFile` 法，將物件的內容復 `Document` 制至檔案。請確定您使用`com.adobe.idp`。 `Document` 由方法返回的對 `addSignatureField` 像。

**另請參閱**

[簽章服務API快速入門](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 使用web service API {#add-signature-fields-using-the-web-service-api}新增簽名欄位

若要使用簽名API(web service)新增簽名欄位：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立簽名用戶端

   * 使用其預設建構子建立`SignatureServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得新增簽名欄位的PDF檔案

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存包含簽名欄位的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 新增簽名欄位

   叫用`SignatureServiceClient`物件的`addSignatureField`方法並傳遞下列值，將簽名欄位新增至PDF檔案：

   * `BLOB`物件，代表新增簽名欄位的PDF檔案。
   * 指定簽名欄位名稱的字串值。
   * 一個整數值，它表示要向其添加簽名欄位的頁碼。
   * `PositionRect`物件，指定簽名欄位的位置。
   * `FieldMDPOptions`物件，指定在數位簽章套用至簽名欄位後鎖定的PDF檔案欄位。 此參數值是可選的，您可以傳遞`null`。
   * `PDFSeedValueOptions`物件，指定各種執行時間值。 此參數值是可選的，您可以傳遞`null`。

   `addSignatureField`方法返回一個`BLOB`對象，該對象表示包含簽名欄位的PDF文檔。

1. 將PDF檔案儲存為PDF檔案

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示將包含簽名欄位的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存`addSignatureField`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象`binaryData`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢索簽名欄位名稱{#retrieving-signature-field-names}

您可以擷取位於要簽署或認證之PDF檔案中之所有簽名欄位的名稱。 如果您不確定PDF檔案中的簽名欄位名稱，或想要驗證名稱，則可以以程式設計方式擷取這些名稱。 簽名服務會傳回簽名欄位的完全限定名稱，例如`form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

>[!NOTE]
>
>如需簽名服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟{#summary_of_steps-1}摘要

要檢索簽名欄位名稱，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得包含簽名欄位的PDF檔案。
1. 擷取簽名欄位名稱。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

您必須先建立簽名服務用戶端，才能以程式設計方式執行簽名服務作業。

**取得包含簽名欄位的PDF檔案**

擷取包含簽名欄位的PDF檔案。

**擷取簽名欄位名稱**

在擷取包含一或多個簽名欄位的PDF檔案後，可以擷取簽名欄位名稱。

**另請參閱**

[使用Java API擷取簽名欄位名稱](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[使用web service API擷取簽名欄位](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API {#retrieve-signature-field-names-using-the-java-api}擷取簽名欄位名稱

使用簽名API(Java)擷取簽名欄位名稱：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`SignatureServiceClient`對象。

1. 取得包含簽名欄位的PDF檔案

   * 使用PDF檔案的建構函式並傳遞指定PDF檔案位置的字串值，以建立`java.io.FileInputStream`物件來表示包含簽名欄位的PDF檔案。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 擷取簽名欄位名稱

   * 叫用`SignatureServiceClient`物件的`getSignatureFieldList`方法並傳遞包含簽名欄位之PDF檔案的`com.adobe.idp.Document`物件，以擷取簽名欄位名稱。 此方法返回`java.util.List`對象，其中每個元素都包含`PDFSignatureField`對象。 使用此對象，您可以獲取有關簽名欄位的其他資訊，如簽名欄位是否可見。
   * 重複`java.util.List`物件，以判斷是否有簽名欄位名稱。 對於PDF文檔中的每個簽名欄位，您可以獲取單獨的`PDFSignatureField`對象。 若要取得簽名欄位的名稱，請叫用`PDFSignatureField`物件的`getName`方法。 此方法傳回指定簽名欄位名稱的字串值。

**另請參閱**

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[快速入門（SOAP模式）:使用Java API檢索簽名欄位名稱](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#retrieve-signature-field-using-the-web-service-api}擷取簽名欄位

使用簽名API(web service)擷取簽名欄位名稱：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立簽名用戶端

   * 使用其預設建構子建立`SignatureServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含簽名欄位的PDF檔案

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存包含簽名欄位的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列內容，填充`BLOB`對象。

1. 擷取簽名欄位名稱

   * 叫用`SignatureServiceClient`物件的`getSignatureFieldList`方法並傳遞`BLOB`物件（該物件包含包含簽名欄位的PDF檔案），以擷取簽名欄位名稱。 此方法返回`MyArrayOfPDFSignatureField`集合對象，其中每個元素都包含`PDFSignatureField`對象。
   * 重複`MyArrayOfPDFSignatureField`物件，以判斷是否有簽名欄位名稱。 對於PDF文檔中的每個簽名欄位，您可以獲取`PDFSignatureField`對象。 若要取得簽名欄位的名稱，請叫用`PDFSignatureField`物件的`getName`方法。 此方法傳回指定簽名欄位名稱的字串值。

**另請參閱**

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改簽名欄位{#modifying-signature-fields}

您可以使用Java API和web service API修改PDF檔案中的簽名欄位。 修改簽名欄位涉及操作其簽名欄位鎖定字典值或種子值字典值。

*欄位鎖定字典*&#x200B;指定簽名欄位簽名時鎖定的欄位清單。 鎖定的欄位可防止使用者變更欄位。 *種子值字典*&#x200B;包含在應用簽名時使用的約束資訊。 例如，您可以變更權限，以控制發生動作，而不會使簽名無效。

修改現有的簽名欄位，您就可以變更PDF檔案，以反映不斷變更的業務需求。 例如，新業務要求可能要求在簽署檔案後鎖定所有檔案欄位。

本節說明如何通過修改欄位鎖定字典和種子值字典值來修改簽名欄位。 對簽名欄位鎖定字典所做的變更，會在簽名欄位時鎖定PDF檔案中的所有欄位。 對種子值字典所做的更改禁止對文檔進行特定類型的更改。

>[!NOTE]
>
>如需有關「簽名服務」和修改簽名欄位的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-2}摘要

要修改PDF文檔中的簽名欄位，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得包含要修改之簽名欄位的PDF檔案。
1. 設定字典值。
1. 修改簽名欄位。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

有關這些JAR檔案位置的資訊，請參見[ Including LiveCycle Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

您必須先建立簽名服務用戶端，才能以程式設計方式執行簽名服務作業。

**取得包含要修改之簽名欄位的PDF檔案**

擷取包含要修改之簽名欄位的PDF檔案。

**設定字典值**

要修改簽名欄位，請為其欄位鎖定字典或種子值字典指定值。 指定簽名欄位鎖定字典值涉及指定簽名欄位時鎖定的PDF文檔欄位。 （本節討論如何鎖定所有欄位。）

可以設定以下種子值字典值：

* **修訂檢查**:指定在將簽名應用到簽名欄位時是否執行撤銷檢查。
* **憑證選項**:為證書種子值字典指定值。在指定憑證選項之前，建議您熟悉憑證種子值字典。 （請參閱[PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。）
* **摘要選項**:指派用於簽署的摘要演算法。有效值為SHA1、SHA256、SHA384、SHA512和RIPEMD160。
* **篩選**:指定與簽名欄位一起使用的篩選器。例如，您可以使用Adobe.PPKLite篩選器。 （請參閱[PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。）
* **標籤選項**:指定與此簽名欄位關聯的標籤值。值1表示簽署者只能使用指定的值來輸入項目。 值0表示允許其他值。 以下是位元位置：

   * **1（篩選器）:** 用於簽署簽名欄位的簽名處理常式
   * **2(SubFilter):** 表示簽署時使用之可接受編碼的名稱陣列
   * **3(V)**:用於簽署簽名欄位之簽名處理常式的最低必要版本號碼
   * **4（原因）：指** 定簽署檔案之可能原因的字串陣列
   * **5(PDFLegalWarnings)：指** 定可能的法律證明的字串陣列

* **法律證明**:當檔案獲得認證時，會自動掃描特定類型的內容，這些內容可能會使檔案的可見內容模糊或產生誤導。例如，註解可以遮蔽對瞭解認證內容很重要的文字。 掃描過程生成指示存在此類內容的警告。 此外，也會針對可能產生警告的內容提供其他說明。
* **權限**:指定可在PDF檔案上使用而不會使簽名無效的權限。
* **原因**:指定必須簽署此檔案的原因。
* **時間戳**:指定時間戳記選項。例如，您可以設定所使用之時間戳記伺服器的URL。
* **版本**:指定用於簽署簽名欄位的簽名處理程式的最小版本號。

**修改簽名欄位**

在您建立簽名服務用戶端後，請擷取包含要修改之簽名欄位的PDF檔案，並設定字典值，您可以指示簽名服務修改簽名欄位。 然後，簽名服務會傳回包含已修改簽名欄位的PDF檔案。 原始PDF檔案不受影響。

**將PDF檔案儲存為PDF檔案**

將包含已修改簽名欄位的PDF檔案儲存為PDF檔案，讓使用者可以在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[簽章服務API快速入門](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API {#modify-signature-fields-using-the-java-api}修改簽名欄位

使用簽名API(Java)修改簽名欄位：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`SignatureServiceClient`對象。

1. 取得包含要修改之簽名欄位的PDF檔案

   * 建立`java.io.FileInputStream`對象，該對象表示要修改的PDF文檔，方法是使用其建構子並傳遞指定PDF文檔位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定字典值

   * 使用其建構子建立`PDFSignatureFieldProperties`對象。 `PDFSignatureFieldProperties`對象儲存簽名欄位鎖定字典和種子值字典資訊。
   * 使用其建構子建立`PDFSeedValueOptionSpec`對象。 此物件可讓您設定種子值字典值。
   * 叫用`PDFSeedValueOptionSpec`物件的`setMdpValue`方法並傳遞`MDPPermissions.NoChanges`列舉值，以禁止變更PDF檔案。
   * 使用其建構子建立`FieldMDPOptionSpec`對象。 此物件可讓您設定簽名欄位鎖定字典值。
   * 叫用`FieldMDPOptionSpec`物件的`setMdpValue`方法並傳遞`FieldMDPAction.ALL`列舉值，以鎖定PDF檔案中的所有欄位。
   * 調用`PDFSignatureFieldProperties`物件的`setSeedValue`方法並傳遞`PDFSeedValueOptionSpec`物件，以設定種子值字典資訊。
   * 調用`PDFSignatureFieldProperties`物件的`setFieldMDP`方法並傳遞`FieldMDPOptionSpec`物件，以設定簽名欄位鎖定字典資訊。

   >[!NOTE]
   >
   >要查看您可以設定的所有種子值字典值，請參閱`PDFSeedValueOptionSpec`類參考。 （請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)）。

1. 修改簽名欄位

   調用`SignatureServiceClient`物件的`modifySignatureField`方法並傳遞下列值，以修改簽名欄位：

   * `com.adobe.idp.Document`物件，它儲存包含要修改之簽名欄位的PDF檔案
   * 指定簽名欄位名稱的字串值
   * 儲存簽名欄位鎖定字典和種子值字典資訊的`PDFSignatureFieldProperties`對象

   `modifySignatureField`方法返回一個`com.adobe.idp.Document`對象，該對象儲存包含已修改簽名欄位的PDF文檔。

1. 將PDF檔案儲存為PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案。 請確定您使用`modifySignatureField`方法傳回的`com.adobe.idp.Document`物件。

### 使用web service API {#modify-signature-fields-using-the-web-service-api}修改簽名欄位

使用簽名API(web service)修改簽名欄位：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立簽名用戶端

   * 使用其預設建構子建立`SignatureServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含要修改之簽名欄位的PDF檔案

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存包含要修改之簽名欄位的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 設定字典值

   * 使用其建構子建立`PDFSignatureFieldProperties`對象。 該對象儲存簽名欄位鎖定字典和種子值字典資訊。
   * 使用其建構子建立`PDFSeedValueOptionSpec`對象。 此物件可讓您設定種子值字典值。
   * 將`MDPPermissions.NoChanges`列舉值指派給`PDFSeedValueOptionSpec`物件的`mdpValue`資料成員，以禁止變更PDF檔案。
   * 使用其建構子建立`FieldMDPOptionSpec`對象。 此物件可讓您設定簽名欄位鎖定字典值。
   * 將`FieldMDPAction.ALL`列舉值指派給`FieldMDPOptionSpec`物件的`mdpValue`資料成員，以鎖定PDF檔案中的所有欄位。
   * 將`PDFSeedValueOptionSpec`物件指派給`PDFSignatureFieldProperties`物件的`seedValue`資料成員，以設定種子值字典資訊。
   * 將`FieldMDPOptionSpec`物件指派給`PDFSignatureFieldProperties`物件的`fieldMDP`資料成員，以設定簽名欄位鎖定字典資訊。

   >[!NOTE]
   >
   >要查看您可以設定的所有種子值字典值，請參閱`PDFSeedValueOptionSpec`類參考。 （請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)）。

1. 修改簽名欄位

   調用`SignatureServiceClient`物件的`modifySignatureField`方法並傳遞下列值，以修改簽名欄位：

   * `BLOB`物件，它儲存包含要修改之簽名欄位的PDF檔案
   * 指定簽名欄位名稱的字串值
   * 儲存簽名欄位鎖定字典和種子值字典資訊的`PDFSignatureFieldProperties`對象

   `modifySignatureField`方法返回一個`BLOB`對象，該對象儲存包含已修改簽名欄位的PDF文檔。

1. 將PDF檔案儲存為PDF檔案

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示將包含簽名欄位的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存`addSignatureField`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數位簽署PDF檔案{#digitally-signing-pdf-documents}

數位簽章可套用至PDF檔案，以提供更高的安全性。 數位簽章（如手寫簽章）提供簽署者識別自己並對檔案進行陳述的方式。 以數位方式簽署檔案的技術有助於確保簽署者和收件者都清楚已簽署的內容，並確信檔案自簽署後未變更。

PDF檔案是透過公開金鑰技術簽署。 簽章者有兩個密鑰：公鑰和私鑰。 私密金鑰會儲存在使用者的憑證中，當簽署時，該憑證必須可供使用。 公開金鑰會儲存在使用者的憑證中，而收件者必須能使用此憑證來驗證簽名。 有關已撤銷證書的資訊可在證書撤銷清單(CRL)和由證書頒發機構(CA)分發的線上證書狀態協定(OCSP)響應中找到。 簽署時間可從稱為時間戳記授權機構的受信任來源取得。

>[!NOTE]
>
>您必須先確定將憑證新增至AEM Forms，才能數位簽署PDF檔案。 憑證是使用管理控制台或使用信任管理器API以程式設計方式新增。 （請參閱[使用Trust Manager API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)匯入認證。）

您可以以程式設計方式數位簽署PDF檔案。 在數位簽署PDF檔案時，您必須參考AEM Forms中的安全憑證。 憑證是用於簽署的私密金鑰。

簽署PDF檔案時，簽名服務會執行下列步驟：

1. 簽名服務通過傳遞請求中指定的別名從Truststore檢索憑據。
1. Truststore會搜尋指定的憑證。
1. 憑證會傳回給簽章服務，並用來簽署檔案。 此憑證也會根據別名快取，以供日後請求使用。

如需有關處理安全性憑證的詳細資訊，請參閱應用程式伺服器的&#x200B;*安裝與部署AEM Forms*&#x200B;指南。

>[!NOTE]
>
>簽署和認證檔案之間有差異。 （請參閱[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)。）

>[!NOTE]
>
>並非所有PDF檔案都支援簽署。 如需簽章服務和數位簽署檔案的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>簽章服務不支援將內嵌PDF資料的XDP檔案輸入至作業，例如認證檔案。 此動作會導致簽名服務拋出`PDFOperationException`。 若要解決此問題，請使用PDF公用程式服務將XDP檔案轉換為PDF檔案，然後將轉換的PDF檔案傳遞至簽名服務作業。 （請參閱[使用PDF公用程式](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)）。

**nCypher nShield HSM憑證**

當使用nCypher nShield HSM憑證來簽署或認證PDF檔案時，必須重新啟動AEM Forms所部署的J2EE應用程式伺服器，才能使用新憑證。 不過，您可以設定設定值，讓簽署或認證作業運作正常，而不需重新啟動J2EE應用程式伺服器。

您可以在cknfastrc檔案中新增下列組態值，該檔案位於/opt/nfast/cknfastrc(或c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將此配置值添加到cknfastrc檔案後，無需重新啟動J2EE應用程式伺服器即可使用新憑據。

**不信任簽名**

在認證和簽署相同PDF檔案時，如果不信任認證簽名，在Acrobat或Adobe Reader中開啟PDF檔案時，第一個簽名會出現黃色三角形。 為避免這種情況，認證簽名必須受到信任。

**簽署以XFA為基礎的表格檔案**

如果您嘗試使用簽名服務API簽署以XFA為基礎的表單，Acrobat中的`View` `Signed` `Version`可能會遺失資料。 例如，請考慮下列工作流程：

* 使用Designer建立的XDP檔案，可以合併包含簽名欄位的表單設計和包含表單資料的XML資料。 您可使用Forms服務產生互動式PDF檔案。
* 您使用簽名服務API簽署PDF檔案。

### 步驟{#summary_of_steps-3}摘要

若要數位簽署PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名服務用戶端。
1. 取得要簽署的PDF檔案。
1. 簽署PDF檔案。
1. 將簽署的PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

**建立簽名用戶端**

您必須先建立簽名服務用戶端，才能以程式設計方式執行簽名服務作業。

**取得PDF檔案以簽署**

若要簽署PDF檔案，您必須取得包含簽名欄位的PDF檔案。 如果PDF檔案不包含簽名欄位，則無法簽署。 可使用設計工具或程式設計方式新增簽名欄位。

**簽署PDF檔案**

在簽署PDF檔案時，您可以設定簽章服務使用的執行時期選項。 您可以設定下列選項：

* 外觀選項
* 撤銷檢查
* 時間戳記值

您可使用`PDFSignatureAppearanceOptionSpec`物件來設定外觀選項。 例如，您可以叫用`PDFSignatureAppearanceOptionSpec`物件的`setShowDate`方法並傳遞`true`，以顯示簽名中的日期。

您也可以指定是否執行撤銷檢查，以判斷用於數位簽署PDF檔案的憑證是否已被撤銷。 要執行撤銷檢查，您可以指定以下值之一：

* **NoCheck**:請勿執行撤銷檢查。
* **BestEffort**:請務必檢查是否撤銷鏈中的所有證書。如果檢查中發生任何問題，則假定撤銷有效。 如果發生任何失敗，請假定憑證未被撤銷。
* **CheckIfAvailable：如果** 有撤銷資訊，請檢查是否撤銷鏈中的所有憑證。如果檢查中發生任何問題，則假定撤銷無效。 如果發生任何故障，請假定憑證已撤銷且無效。 （這是預設值。）
* **AlwaysCheck**:檢查是否撤銷鏈中的所有證書。如果撤銷資訊未出現在任何憑證中，則假定撤銷無效。

要對證書執行撤銷檢查，可以使用`CRLOptionSpec`對象指定證書撤銷清單(CRL)伺服器的URL。 但是，如果您要執行撤銷檢查，而您未指定CRL伺服器的URL，則簽名服務會從憑證取得URL。

執行撤銷檢查時，您可以使用線上認證狀態通訊協定(OCSP)伺服器，而不是使用CRL伺服器。 通常在使用OCSP伺服器而非CRL伺服器時，會更快地執行撤銷檢查。 (請參閱[https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560)的「Online Certificate Status Protocol」（聯機證書狀態協定）。

您可以使用Adobe應用程式與服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是先在Adobe Applications and Services中設定，則會檢查OCSP伺服器，接著檢查CRL伺服器。 （請參閱AAC說明中的「使用信任商店管理憑證和認證」）。

如果您指定不執行撤銷檢查，則簽章服務不會檢查用來簽署或認證檔案的憑證是否已被撤銷。 即，忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>雖然CRL或OCSP伺服器可在憑證中指定，但您仍可使用`CRLOptionSpec`和`OCSPOptionSpec`物件來覆寫憑證中指定的URL。 例如，若要覆寫CRL伺服器，您可以叫用`CRLOptionSpec`物件的`setLocalURI`方法。

時間戳記是指追蹤已簽署或已認證檔案修改時間的程式。 簽署檔案後，即使檔案擁有者也不應修改檔案。 時間戳記有助於強制簽署或認證檔案的有效性。 可以使用`TSPOptionSpec`對象設定時間戳選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和web服務中，通過各個部分和相應的快速啟動，使用撤銷檢查。 由於未指定CRL或OCSP伺服器資訊，因此伺服器資訊是從用於數位簽署PDF檔案的憑證中取得。

若要成功簽署PDF檔案，您可以指定包含數位簽名的簽名欄位的完全限定名稱，例如`form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，也可以使用簽名欄位的部分名稱：`SignatureField3[3]`。

您也必須參考安全憑證才能數位簽署PDF檔案。 要引用安全憑據，請指定別名。 別名是對PKCS#12檔案（副檔名為。pfx）或硬體安全模組(HSM)中實際憑據的引用。 如需安全性憑證的詳細資訊，請參閱應用程式伺服器的&#x200B;*安裝與部署AEM Forms*&#x200B;指南。

**儲存已簽署的PDF檔案**

在簽名服務數位簽署PDF檔案後，您可以將它儲存為PDF檔案，讓使用者在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[使用Java API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[使用web service API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### 使用Java API {#digitally-sign-pdf-documents-using-the-java-api}數位簽署PDF檔案

使用簽名API(Java)數位簽署PDF檔案：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`SignatureServiceClient`對象。

1. 取得PDF檔案以簽署

   * 使用PDF檔案的建構函式並傳遞指定PDF檔案位置的字串值，以建立代表PDF檔案的`java.io.FileInputStream`物件來進行數位簽署。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 簽署PDF檔案

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值，以簽署PDF檔案：

   * `com.adobe.idp.Document`物件，代表要簽署的PDF檔案。
   * 一個字串值，代表將包含數位簽名之簽名欄位的名稱。
   * `Credential`物件，代表用於數位簽署PDF檔案的憑證。 通過調用`Credential`對象的靜態`getInstance`方法並傳遞一個字串值來建立`Credential`對象，該字串值指定與安全憑據對應的別名值。
   * `HashAlgorithm`物件，指定代表雜湊演算法的靜態資料成員，用於摘要PDF檔案。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 一個字串值，代表PDF檔案數位簽章的原因。
   * 代表簽署者聯絡資訊的字串值。
   * 控制數位簽名外觀的`PDFSignatureAppearanceOptions`物件。 例如，您可使用此物件將自訂標誌新增至數位簽名。
   * `java.lang.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。
   * `OCSPOptionSpec`物件，儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。
   * `CRLPreferences`物件，可儲存憑證撤銷清單(CRL)偏好設定。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，可儲存時間戳記提供者(TSP)支援的偏好設定。 此參數為可選參數，可以是`null`。 如需詳細資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

   `sign`方法會傳回代表已簽署PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存已簽署的PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`，將`Document`物件的內容複製至檔案。 請確定您使用`sign`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[快速入門（SOAP模式）:使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#digitally-signing-pdf-documents-using-the-web-service-api}數位簽署PDF檔案

若要使用簽名API(web service)數位簽署PDF檔案：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立簽名用戶端

   * 使用其預設建構子建立`SignatureServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得PDF檔案以簽署

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存已簽署的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要簽名的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 簽署PDF檔案

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值，以簽署PDF檔案：

   * `BLOB`物件，代表要簽署的PDF檔案。
   * 一個字串值，代表將包含數位簽名之簽名欄位的名稱。
   * `Credential`物件，代表用於數位簽署PDF檔案的憑證。 使用其建構函式建立`Credential`物件，並透過為`Credential`物件的`alias`屬性指派值來指定別名。
   * `HashAlgorithm`物件，指定代表雜湊演算法的靜態資料成員，用於摘要PDF檔案。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 一個布爾值，它指定是否使用散列算法。
   * 一個字串值，代表PDF檔案數位簽章的原因。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * 控制數位簽名外觀的`PDFSignatureAppearanceOptions`物件。 例如，您可使用此物件將自訂標誌新增至數位簽名。
   * `System.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。 如果完成此撤銷檢查，則會將其嵌入簽名中。 預設值為`false`。
   * `OCSPOptionSpec`物件，儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。 如需此物件的詳細資訊，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * `CRLPreferences`物件，可儲存憑證撤銷清單(CRL)偏好設定。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，可儲存時間戳記提供者(TSP)支援的偏好設定。 此參數為可選參數，可以是`null`。

   `sign`方法會傳回代表已簽署PDF檔案的`BLOB`物件。

1. 儲存已簽署的PDF檔案

   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，代表已簽署PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存`sign`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數位簽署互動式表單{#digitally-signing-interactive-forms}

您可以簽署Forms服務所建立的互動式表單。 例如，請考慮下列工作流程：

* 您可以合併使用Designer建立的以XFA為基礎的PDF表單，以及使用Forms服務在XML檔案中的表單資料。 Forms伺服器會轉譯互動式表單。
* 您可使用簽名服務API簽署互動式表單。

結果是以數位簽章的互動式PDF表單。 在簽署以XFA表單為基礎的PDF表單時，請確定您將PDF檔案儲存為Adobe Static PDF表單。 如果您嘗試簽署儲存為Adobe動態PDF表單的PDF表單，就會發生例外。 由於您正在簽署從Forms服務傳回的表單，請確定表單包含簽名欄位。

>[!NOTE]
>
>您必須先確定將憑證新增至AEM Forms，才能數位簽署互動式表單。 憑證是使用管理控制台或使用信任管理器API以程式設計方式新增。 （請參閱[使用Trust Manager API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)匯入認證。）

使用Forms Service API時，將`GenerateServerAppearance`執行時間選項設為`true`。 此執行時期選項可確保在Acrobat或Adobe Reader中開啟時，伺服器上產生的表格外觀仍然有效。 建議您在使用Forms API產生要簽署的互動式表單時，設定這個執行時期選項。

>[!NOTE]
>
>在閱讀數位簽署互動式表單之前，建議您熟悉簽署PDF檔案。 （請參閱[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)）。

### 步驟{#summary_of_steps-4}摘要

若要數位簽署Forms服務傳回的互動式表單，請執行下列工作：

1. 包含專案檔案。
1. 建立表單和簽名用戶端。
1. 使用Forms服務取得互動式表單。
1. 簽署互動式表單。
1. 將簽署的PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立表單和簽名用戶端**

由於此工作流程會同時叫用Forms和Signature services，因此請同時建立Forms服務用戶端和Signature服務用戶端。

**使用Forms服務取得互動式表單**

您可以使用Forms服務取得要簽署的互動式PDF表單。 從AEM Forms開始，您可以將`com.adobe.idp.Document`物件傳遞至包含要轉譯的表單的Forms服務。 此方法的名稱為`renderPDFForm2`。 此方法會傳回包含要簽署之表單的`com.adobe.idp.Document`物件。 您可以將此`com.adobe.idp.Document`實例傳遞至簽名服務。

同樣地，如果您使用web services，則可以將Forms服務返回的`BLOB`實例傳遞給Signature服務。

>[!NOTE]
>
>與「數位簽署互動式表單」區段關聯的快速入門會叫用`renderPDFForm2`方法。

**簽署互動式表單**

在簽署PDF檔案時，您可以設定簽章服務使用的執行時期選項。 您可以設定下列選項：

* 外觀選項
* 撤銷檢查
* 時間戳記值

您可使用`PDFSignatureAppearanceOptionSpec`物件來設定外觀選項。 例如，您可以叫用`PDFSignatureAppearanceOptionSpec`物件的`setShowDate`方法並傳遞`true`，以顯示簽名中的日期。

**儲存已簽署的PDF檔案**

在簽名服務數位簽署PDF檔案後，您就可將它儲存為PDF檔案。 PDF檔案可在Acrobat或Adobe Reader中開啟。

**另請參閱**

[使用Java API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[使用web service API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[轉換互動式PDF表單](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### 使用Java API {#digitally-sign-an-interactive-form-using-the-java-api}數位簽署互動式表單

使用表單與簽名API(Java)數位簽署互動式表單：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar和adobe-forms-client.jar。

1. 建立表單和簽名用戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`SignatureServiceClient`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormsServiceClient`對象。

1. 使用Forms服務取得互動式表單

   * 建立`java.io.FileInputStream`物件，以代表PDF檔案，並使用其建構函式傳遞至Forms服務。 傳遞指定PDF檔案位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。
   * 建立`java.io.FileInputStream`對象，該對象表示包含表單資料的XML文檔，並使用其建構子傳遞給Forms服務。 傳遞指定XML檔案位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。
   * 建立用於設定運行時選項的`PDFFormRenderSpec`對象。 叫用`PDFFormRenderSpec`物件的`setGenerateServerAppearance`方法並傳遞`true`。
   * 叫用`FormsServiceClient`物件的`renderPDFForm2`方法並傳遞下列值：

      * `com.adobe.idp.Document`物件，其中包含要轉譯的PDF表格。
      * `com.adobe.idp.Document`物件，包含要與表單合併的資料。
      * 儲存運行時選項的`PDFFormRenderSpec`對象。
      * `URLSpec`物件，包含Forms服務所需的URI值。 您可以指定此參數值的`null`。
      * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。

      `renderPDFForm2`方法返回包含表單資料流的`FormsResult`對象

   * 叫用`FormsResult`物件的`getOutputContent`方法，擷取PDF表格。 此方法傳回代表互動式表單的`com.adobe.idp.Document`物件。


1. 簽署互動式表單

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值，以簽署PDF檔案：

   * `com.adobe.idp.Document`物件，代表要簽署的PDF檔案。 請確定此對象是從Forms服務獲取的`com.adobe.idp.Document`對象。
   * 一個字串值，代表已簽署的簽名欄位名稱。
   * `Credential`物件，代表用於數位簽署PDF檔案的憑證。 通過調用`Credential`對象的靜態`getInstance`方法建立`Credential`對象。 傳遞一個字串值，該字串值指定與安全憑據對應的別名值。
   * `HashAlgorithm`物件，指定代表雜湊演算法的靜態資料成員，用於摘要PDF檔案。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 一個字串值，代表PDF檔案數位簽章的原因。
   * 代表簽署者聯絡資訊的字串值。
   * 控制數位簽名外觀的`PDFSignatureAppearanceOptions`物件。 例如，您可使用此物件將自訂標誌新增至數位簽名。
   * `java.lang.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。
   * `OCSPPreferences`物件，儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。
   * `CRLPreferences`物件，可儲存憑證撤銷清單(CRL)偏好設定。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，可儲存時間戳記提供者(TSP)支援的偏好設定。 此參數為可選參數，可以是`null`。

   `sign`方法會傳回代表已簽署PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存已簽署的PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`，將`Document`物件的內容複製至檔案。 請確定您使用`sign`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[快速入門（SOAP模式）:使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#digitally-sign-an-interactive-form-using-the-web-service-api}數位簽署互動式表單

使用表單與簽名API(web service)數位簽署互動式表單：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 由於此用戶端應用程式會叫用兩個AEM Forms服務，因此請建立兩個服務參考。 對與簽名服務關聯的服務引用使用以下WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   對與Forms服務關聯的服務引用使用以下WSDL定義：`http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   由於`BLOB`資料類型對於兩個服務引用都很常見，因此使用`BLOB`資料類型時可完全限定資料類型。 在相應的Web服務快速啟動中，所有`BLOB`實例都完全限定。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立表單和簽名用戶端

   * 使用其預設建構子建立`SignatureServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >對Forms服務客戶端重複這些步驟。

1. 使用Forms服務取得互動式表單

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存已簽署的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要簽名的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`屬性指定位元組陣列的內容來填充`BLOB`對象。
   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存表單資料。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含表單資料的XML檔案的檔案位置，以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`屬性指定位元組陣列的內容來填充`BLOB`對象。
   * 建立用於設定運行時選項的`PDFFormRenderSpec`對象。 將值`true`指派至`PDFFormRenderSpec`物件的`generateServerAppearance`欄位。
   * 叫用`FormsServiceClient`物件的`renderPDFForm2`方法並傳遞下列值：

      * `BLOB`物件，其中包含要轉譯的PDF表格。
      * `BLOB`物件，包含要與表單合併的資料。
      * 儲存運行時選項的`PDFFormRenderSpec`對象。
      * `URLSpec`物件，包含Forms服務所需的URI值。 您可以指定此參數值的`null`。
      * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。
      * 用於儲存表單中頁數的長輸出參數。
      * 用於地區值的字串輸出參數。
      * `FormResult`值，此值是用於儲存互動式表單的輸出參數。
   * 叫用`FormsResult`物件的`outputContent`欄位，以重新建立PDF表格。 此欄位儲存代表互動式表單的`BLOB`對象。


1. 簽署互動式表單

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值，以簽署PDF檔案：

   * `BLOB`物件，代表要簽署的PDF檔案。 使用Forms服務傳回的`BLOB`例項。
   * 一個字串值，代表已簽署的簽名欄位名稱。
   * `Credential`物件，代表用於數位簽署PDF檔案的憑證。 使用其建構函式建立`Credential`物件，並透過為`Credential`物件的`alias`屬性指派值來指定別名。
   * `HashAlgorithm`物件，指定代表雜湊演算法的靜態資料成員，用於摘要PDF檔案。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 一個布爾值，它指定是否使用散列算法。
   * 一個字串值，代表PDF檔案數位簽章的原因。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * 控制數位簽名外觀的`PDFSignatureAppearanceOptions`物件。 例如，您可使用此物件將自訂標誌新增至數位簽名。
   * `System.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。 如果完成此撤銷檢查，則會將其嵌入簽名中。 預設值為`false`。
   * `OCSPPreferences`物件，儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。 如需此物件的詳細資訊，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * `CRLPreferences`物件，可儲存憑證撤銷清單(CRL)偏好設定。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，可儲存時間戳記提供者(TSP)支援的偏好設定。 此參數為可選參數，可以是`null`。

   `sign`方法會傳回代表已簽署PDF檔案的`BLOB`物件。

1. 儲存已簽署的PDF檔案

   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，代表已簽署PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存`sign`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 認證PDF檔案{#certifying-pdf-documents}

您可以使用稱為認證簽名的特定簽名類型來認證PDF檔案，以保全PDF檔案。 認證簽名與數位簽名的區別在於：

* 它必須是套用至PDF檔案的第一個簽名；也就是說，在套用認證簽名時，檔案中的任何其他簽名欄位都必須未簽署。 在PDF檔案中僅允許使用一個認證簽名。 如果您想要簽署和認證PDF檔案，您必須先取得認證，才能簽署。 在認證PDF檔案後，您可以數位簽署其他簽名欄位。
* 文檔的作者或發起者可以指定文檔可以通過某些方式進行修改，而不使經認證的簽名失效。 例如，檔案可能允許填寫表單或加上註解。 如果作者指定不允許進行某些修改，Acrobat會限制使用者以此方式修改檔案。 如果進行此類修改，例如使用其他應用程式，認證的簽名無效，當使用者開啟檔案時，Acrobat會發出警告。 （使用未認證的簽名時，不會防止修改，而一般的編輯作業也不會使原始簽名無效。）
* 在簽署時，會掃描檔案，以找出可能導致檔案內容模糊或誤導的特定內容類型。 例如，註解可能會遮蔽頁面上對瞭解所認證內容很重要的部分文字。 可以提供有關此類內容的說明（法律證明）。

您可以使用簽名服務Java API或簽名網站服務API，以程式設計方式認證PDF檔案。 認證PDF檔案時，您必須參考憑證服務中的安全憑證。 如需安全性憑證的詳細資訊，請參閱應用程式伺服器的&#x200B;*安裝與部署AEM Forms*&#x200B;指南。

>[!NOTE]
>
>當認證並簽署相同的PDF檔案時，如果不信任認證簽名，當您在Acrobat或Adobe Reader中開啟PDF檔案時，第一個簽名旁會出現黃色三角形。 必須信任認證簽名才能避免這種情況。

>[!NOTE]
>
>當使用nCypher nShield HSM憑證來簽署或認證PDF檔案時，必須重新啟動部署AEM Forms的J2EE應用程式伺服器，才能使用新憑證。 不過，您可以設定設定值，讓簽署或認證作業運作正常，而不需重新啟動J2EE應用程式伺服器。

您可以在cknfastrc檔案中新增下列組態值，該檔案位於/opt/nfast/cknfastrc(或c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將此配置值添加到cknfastrc檔案後，無需重新啟動J2EE應用程式伺服器即可使用新憑據。

>[!NOTE]
>
>如需簽章服務和認證檔案的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-5}摘要

若要認證PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得PDF檔案以進行認證。
1. 認證PDF檔案。
1. 將認證的PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

您必須先建立「簽名」用戶端，才能以程式設計方式執行「簽名」操作。

**取得PDF檔案以取得認證**

若要認證PDF檔案，您必須取得包含簽名欄位的PDF檔案。 如果PDF檔案不包含簽名欄位，則無法取得認證。 可使用設計工具或程式設計方式新增簽名欄位。 有關以寫程式方式添加簽名欄位的資訊，請參閱[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。

**認證PDF檔案**

若要成功認證PDF檔案，您需要下列由簽章服務用來認證PDF檔案的輸入值：

* **PDF檔案**:包含簽名欄位的PDF文檔，該欄位是包含已認證簽名的圖形表示的表單欄位。PDF檔案必須先包含簽名欄位，才能取得認證。 可使用設計工具或程式設計方式新增簽名欄位。 （請參閱[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。）
* **簽名欄位名稱**:經認證的簽名欄位的全限定名稱。以下是一個示例：`form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，也可以使用簽名欄位的部分名稱：`SignatureField3[3]`。 如果為欄位名稱傳遞空值，則會動態建立並認證不可見的簽名欄位。
* **安全憑證**:用於認證PDF檔案的憑證。此安全憑證包含密碼和別名，這些密碼和別名必須與位於憑證服務中的憑證中顯示的別名相符。 別名是對PKCS#12檔案（副檔名為。pfx）或硬體安全模組(HSM)中實際憑據的引用。
* **雜湊算法**:用於摘要PDF檔案的雜湊演算法。
* **簽署原因**:顯示在Acrobat或Adobe Reader中的值，讓其他使用者知道PDF檔案獲得認證的原因。
* **簽署者的位置**:憑證指定之簽署者的位置。
* **聯絡資訊**:簽署者的聯絡資訊，例如地址和電話號碼。
* **權限資訊**:控制一般使用者可在檔案上執行動作而不導致認證簽名無效的權限。例如，您可以設定權限，如此對PDF檔案所做的任何變更，都會導致認證的簽名無效。
* **法律解釋**:當檔案獲得認證時，會自動掃描特定類型的內容，這些內容可能會使檔案的內容模糊或產生誤導。例如，註解可能會遮蔽頁面上對瞭解所認證內容很重要的部分文字。 掃描過程生成關於這些類型內容的警告。 此值提供可能產生警告之內容的額外說明。
* **外觀選項**:控制認證簽名外觀的選項。例如，認證的簽名可顯示日期資訊。
* **撤銷檢查**:此值指定是否對簽署者的憑證執行撤銷檢查。預設的`false`設定表示不會執行撤銷檢查。
* **OCSP設定**:線上認證狀態通訊協定(OCSP)支援的設定，提供用來認證PDF檔案之憑證狀態的相關資訊。例如，您可以指定伺服器的URL，以提供您用來登入PDF檔案之憑證的相關資訊。
* **CRL設定**:完成撤銷檢查時，證書撤銷清單(CRL)首選項的設定。例如，您可以指定一律檢查憑證是否已撤銷。
* **時間戳記**:定義套用至認證簽名之時間戳記資訊的設定。時間戳表示特定資料在某個時間之前建立。 這項知識有助於在簽署者與驗證者之間建立信任關係。

**將認證的PDF檔案儲存為PDF檔案**

在簽章服務認證PDF檔案後，您可以將它儲存為PDF檔案，讓使用者在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[使用Java API認證PDF檔案](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[使用web service API認證PDF檔案](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API {#certify-pdf-documents-using-the-java-api}認證PDF檔案

使用簽名API(Java)認證PDF檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`SignatureServiceClient`對象。

1. 取得PDF檔案以取得認證

   * 使用PDF檔案的建構函式並傳遞指定PDF檔案位置的字串值，建立代表PDF檔案的`java.io.FileInputStream`物件以進行認證。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 認證PDF檔案

   叫用`SignatureServiceClient`物件的`certify`方法並傳遞下列值，以認證PDF檔案：

   * 代表要認證的PDF檔案的`com.adobe.idp.Document`物件。
   * 一個字串值，它表示將包含簽名的簽名欄位的名稱。
   * `Credential`物件，代表用來認證PDF檔案的憑證。 通過調用`Credential`對象的靜態`getInstance`方法並傳遞一個字串值來建立`Credential`對象，該字串值指定與安全憑據對應的別名值。
   * `HashAlgorithm`物件，指定代表用於摘要PDF檔案之雜湊演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 一個字串值，代表PDF檔案獲得認證的原因。
   * 代表簽署者聯絡資訊的字串值。
   * `MDPPermissions`物件，指定可在PDF檔案上執行使簽名無效的動作。
   * 控制已認證簽名外觀的`PDFSignatureAppearanceOptions`物件。 如果需要，請通過調用方法（如`setShowDate`）修改簽名的外觀。
   * 字串值，可說明哪些動作使簽名無效。
   * `java.lang.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。 如果完成此撤銷檢查，則會將其嵌入簽名中。 預設值為`false`。
   * 一個`java.lang.Boolean`對象，它指定是否鎖定要認證的簽名欄位。 如果欄位已鎖定，則簽名欄位會標示為唯讀，其屬性無法修改，而且沒有必要權限的任何人也無法清除。 預設值為`false`。
   * `OCSPPreferences`物件，儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。 如需此物件的詳細資訊，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * `CRLPreferences`物件，可儲存憑證撤銷清單(CRL)偏好設定。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，可儲存時間戳記提供者(TSP)支援的偏好設定。 例如，在建立`TSPPreferences`物件後，您可以叫用`TSPPreferences`物件的`setTspServerURL`方法來設定TSP伺服器的URL。 此參數為可選參數，可以是`null`。 如需詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

   `certify`方法會傳回代表已認證PDF檔案的`com.adobe.idp.Document`物件。

1. 將認證的PDF檔案儲存為PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案。

**另請參閱**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[快速入門（SOAP模式）:使用Java API認證PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#certify-pdf-documents-using-the-web-service-api}認證PDF檔案

使用簽名API(web service)認證PDF檔案：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立簽名用戶端

   * 使用其預設建構子建立`SignatureServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得PDF檔案以取得認證

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存已認證的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要認證的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過將`MTOM`資料成員的位元組陣列內容分配給`BLOB`對象，以填充對象。

1. 認證PDF檔案

   叫用`SignatureServiceClient`物件的`certify`方法並傳遞下列值，以認證PDF檔案：

   * 代表要認證的PDF檔案的`BLOB`物件。
   * 一個字串值，它表示將包含簽名的簽名欄位的名稱。
   * `Credential`物件，代表用來認證PDF檔案的憑證。 使用其建構函式建立`Credential`物件，並指定別名，方法是為`Credential`物件的`alias`屬性指定值。
   * `HashAlgorithm`物件，指定代表用於摘要PDF檔案之雜湊演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 一個布爾值，它指定是否使用散列算法。
   * 一個字串值，代表PDF檔案獲得認證的原因。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * `MDPPermissions`物件的靜態資料成員，指定可對PDF檔案執行使簽名無效的動作。
   * 一個布爾值，它指定是否使用作為前一個參數值傳遞的`MDPPermissions`對象。
   * 一個字串值，它解釋哪些操作使簽名無效。
   * 控制已認證簽名外觀的`PDFSignatureAppearanceOptions`物件。 使用其建構子建立`PDFSignatureAppearanceOptions`對象。 您可以通過設定簽名的一個資料成員來修改簽名的外觀。
   * `System.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。 如果完成此撤銷檢查，則會將其嵌入簽名中。 預設值為`false`。
   * 一個`System.Boolean`對象，它指定是否鎖定要認證的簽名欄位。 如果欄位已鎖定，則簽名欄位會標示為唯讀，其屬性無法修改，而且沒有必要權限的任何人也無法清除。 預設值為`false`。
   * `System.Boolean`物件，指定簽名欄位是否已鎖定。 也就是說，如果將`true`傳遞至上一個參數，則將`true`傳遞至此參數。
   * `OCSPPreferences`物件，儲存線上認證狀態通訊協定(OCSP)支援的偏好設定，提供用於認證PDF檔案之憑證狀態的相關資訊。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。
   * `CRLPreferences`物件，可儲存憑證撤銷清單(CRL)偏好設定。 如果未完成撤銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，可儲存時間戳記提供者(TSP)支援的偏好設定。 例如，在建立`TSPPreferences`物件後，您可以設定`TSPPreferences`物件的`tspServerURL`資料成員，以設定TSP的URL。 此參數為可選參數，可以是`null`。

   `certify`方法會傳回代表已認證PDF檔案的`BLOB`物件。

1. 將認證的PDF檔案儲存為PDF檔案

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示將包含已認證PDF文檔的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存`certify`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象`binaryData`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證數字簽名{#verifying-digital-signatures}

數位簽章可進行驗證，以確保已簽署的PDF檔案未修改，且數位簽章有效。 在驗證數位簽章時，您可以檢查簽名的狀態和簽名的屬性，例如簽章者的身分。 在信任數位簽名之前，建議您先進行驗證。 在驗證數位簽名時，請參考包含數位簽名的PDF檔案。

假設簽章者的身分不明。 當您在Acrobat中開啟PDF檔案時，會出現警告訊息，指出簽署者的身分不明，如下圖所示。

![vd_vd_verifisig](assets/vd_vd_verifysig.png)

同樣地，當您以程式設計方式驗證數位簽章時，您也可以決定簽署者身分的狀態。 例如，如果您驗證上圖所示檔案中的數位簽名，結果會是簽章者的身分不明。

>[!NOTE]
>
>如需簽名服務和驗證數位簽名的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-6}摘要

若要驗證數位簽名，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得包含要驗證之簽名的PDF檔案。
1. 設定PKI執行時期選項。
1. 驗證數位簽名。
1. 確定簽名的狀態。
1. 決定簽署者的身分。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

在您以程式設計方式執行簽名服務操作之前，請先建立簽名服務用戶端。

**取得包含簽章的PDF檔案以驗證**

若要驗證用於數位簽署或認證PDF檔案的簽名，請取得包含簽名的PDF檔案。

**設定PKI執行時期選項**

在PDF檔案中驗證簽名時，請設定簽名服務使用的這些PKI執行時期選項：

* 驗證時間
* 撤銷檢查
* 時間戳記值

在設定這些選項時，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），指出使用目前時間。 如需不同時間值的詳細資訊，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`VerificationTime`列舉值。

您也可以指定是否在驗證程式中執行撤銷檢查。 例如，您可以執行撤銷檢查，以判斷憑證是否已撤銷。 如需撤銷檢查選項的詳細資訊，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`RevocationCheckStyle`列舉值。

要對證書執行撤銷檢查，請使用`CRLOptionSpec`對象指定證書撤銷清單(CRL)伺服器的URL。 但是，如果您未指定CRL伺服器的URL，則簽名服務會從憑證取得URL。

執行撤銷檢查時，您可以使用線上認證狀態通訊協定(OCSP)伺服器，而不是使用CRL伺服器。 通常，與CRL伺服器相比，使用OCSP伺服器時，撤銷檢查的執行速度更快。 （請參閱[線上證書狀態協定](https://tools.ietf.org/html/rfc2560)。）

您可以使用Adobe應用程式與服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是先在Adobe Applications and Services中設定，則會檢查OCSP伺服器，接著檢查CRL伺服器。

如果您未執行撤銷檢查，「簽名服務」不會檢查憑證是否已撤銷。 即，忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用`CRLOptionSpec`和`OCSPOptionSpec`物件來覆寫憑證中指定的URL。 例如，若要覆寫CRL伺服器，您可以叫用`CRLOptionSpec`物件的`setLocalURI`方法。

時間戳記是追蹤已簽署或已認證檔案修改時間的程式。 簽署檔案後，任何人都無法修改它。 時間戳記有助於強制簽署或認證檔案的有效性。 可以使用`TSPOptionSpec`對象設定時間戳選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和web服務快速啟動中，驗證時間被設定為`VerificationTime.CURRENT_TIME`，撤銷檢查被設定為`RevocationCheckStyle.BestEffort`。 由於未指定CRL或OCSP伺服器資訊，因此從證書中獲取伺服器資訊。

**驗證數位簽名**

要成功驗證簽名，請指定包含簽名的簽名欄位的完全限定名稱，例如`form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，您也可以使用簽名欄位的部分名稱：`SignatureField3`。

依預設，簽章服務會將檔案在驗證後可簽署的時間限制為65分鐘。 如果使用者嘗試在目前時間驗證簽名，而簽署時間晚於目前時間且在65分鐘內，則簽名服務不會建立驗證錯誤。

>[!NOTE]
>
>如需您在驗證簽名時需要的其他值，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**確定簽名的狀態**

在驗證數位簽名時，您可以檢查簽名的狀態。

**決定簽署者的身分**

您可以決定簽章者的身分，這可以是下列其中一個值：

* **未知**:此簽署者未知，因為無法執行簽署者驗證。
* **受信任**:此簽署者是受信任的。
* **不受信任**:此簽署者不受信任。

**另請參閱**

[使用Java API驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[使用web service API驗證數位簽名](#verify-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#verify-digital-signatures-using-the-java-api}驗證數位簽名

使用簽名服務API(Java)驗證數位簽名：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`SignatureServiceClient`對象。

1. 取得包含簽章的PDF檔案以驗證

   * 建立`java.io.FileInputStream`物件，代表包含要使用其建構函式驗證之簽名的PDF檔案。 傳遞指定PDF檔案位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定PKI執行時期選項

   * 使用其建構子建立`PKIOptions`對象。
   * 調用`PKIOptions`物件的`setVerificationTime`方法並傳遞指定驗證時間的`VerificationTime`列舉值，以設定驗證時間。
   * 通過調用`PKIOptions`對象的`setRevocationCheckStyle`方法並傳遞指定是否執行撤銷檢查的`RevocationCheckStyle`枚舉值來設定撤銷檢查選項。

1. 驗證數位簽名

   調用`SignatureServiceClient`物件的`verify2`方法並傳遞下列值，以驗證簽名：

   * `com.adobe.idp.Document`物件，包含數位簽章或認證的PDF檔案。
   * 一個字串值，代表包含要驗證之簽名的簽名欄位名稱。
   * 包含PKI運行時選項的`PKIOptions`對象。
   * 包含SPI資訊的`VerifySPIOptions`實例。 您可以指定此參數的`null`。

   `verify2`方法返回`PDFSignatureVerificationInfo`對象，該對象包含可用於驗證數字簽名的資訊。

1. 確定簽名的狀態

   * 叫用`PDFSignatureVerificationInfo`物件的`getStatus`方法，以判斷簽名的狀態。 此方法返回指定簽名狀態的`SignatureStatus`對象。 例如，如果未修改已簽署的PDF檔案，此方法會傳回`SignatureStatus.DocumentSigNoChanges`。

1. 決定簽署者的身分

   * 叫用`PDFSignatureVerificationInfo`物件的`getSigner`方法，以決定簽署者的身分。 此方法返回`IdentityInformation`對象。
   * 叫用`IdentityInformation`物件的`getStatus`方法，以判斷簽署者的身分。 此方法返回一個`IdentityStatus`枚舉值，該值指定標識。 例如，如果簽署者受信任，此方法會傳回`IdentityStatus.TRUSTED`。

**另請參閱**

[驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[快速入門（SOAP模式）:使用Java API驗證數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#verify-digital-signatures-using-the-web-service-api}驗證數位簽名

使用簽名服務API(web service)驗證數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立簽名用戶端

   * 使用其預設建構子建立`SignatureServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含簽章的PDF檔案以驗證

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存包含數位或認證簽名以進行驗證的PDF檔案。
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，代表已簽署PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 設定PKI執行時期選項

   * 使用其建構子建立`PKIOptions`對象。
   * 通過為`PKIOptions`對象的`verificationTime`資料成員分配指定驗證時間的`VerificationTime`枚舉值來設定驗證時間。
   * 通過為`PKIOptions`對象的`revocationCheckStyle`資料成員分配指定是否執行撤銷檢查的`RevocationCheckStyle`枚舉值來設定撤銷檢查選項。

1. 驗證數位簽名

   調用`SignatureServiceClient`物件的`verify2`方法並傳遞下列值，以驗證簽名：

   * `BLOB`物件包含數位簽章或認證的PDF檔案。
   * 一個字串值，代表包含要驗證之簽名的簽名欄位名稱。
   * 包含PKI運行時選項的`PKIOptions`對象。
   * 包含SPI資訊的`VerifySPIOptions`實例。 您可以指定此參數的`null`。

   `verify2`方法返回`PDFSignatureVerificationInfo`對象，該對象包含可用於驗證數字簽名的資訊。

1. 確定簽名的狀態

   取得`PDFSignatureVerificationInfo`物件`status`資料成員的值，以判斷簽章的狀態。 此資料成員儲存一個`SignatureStatus`對象，該對象指定簽名的狀態。 例如，如果修改了已簽名的PDF文檔，`status`資料成員將儲存值`SignatureStatus.DocumentSigNoChanges`。

1. 決定簽署者的身分

   * 擷取`PDFSignatureVerificationInfo`物件`signer`資料成員的值，以判斷簽署者的身分。 此成員返回`IdentityInformation`對象。
   * 擷取`IdentityInformation`物件的`status`資料成員，以判斷簽章者的身分。 此資料成員返回一個`IdentityStatus`枚舉值，該枚舉值指定標識。 例如，如果簽署者受信任，此成員會傳回`IdentityStatus.TRUSTED`。

**另請參閱**

[驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證多個數字簽名{#verifying-multiple-digital-signatures}

AEM Forms提供驗證PDF檔案中所有數位簽名的方式。 假設PDF檔案包含多個數位簽名，因為業務流程需要多個簽署者的簽名。 例如，請考慮要求貸款主管和經理簽名的財務交易。 您可以使用簽名服務Java API或web service API來驗證PDF檔案中的所有簽名。 驗證多個數位簽名時，您可以檢查每個簽名的狀態和屬性。 在您信任數位簽名之前，建議您先進行驗證。 建議您熟悉驗證單一數位簽名。

>[!NOTE]
>
>如需簽名服務和驗證數位簽名的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-7}摘要

若要驗證多個數位簽名，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得包含要驗證之簽名的PDF檔案。
1. 設定PKI執行時期選項。
1. 擷取所有數位簽名。
1. 重複所有簽名。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

在您以程式設計方式執行簽名服務操作之前，請先建立簽名服務用戶端。

**取得包含簽名的PDF檔案，以驗證**

若要驗證用於數位簽署或認證PDF檔案的簽名，請取得包含簽名的PDF檔案。

**設定PKI執行時期選項**

設定簽章服務在驗證PDF檔案中所有簽名時使用的這些PKI執行時期選項：

* 驗證時間
* 撤銷檢查
* 時間戳記值

在設定這些選項時，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），指出使用目前時間。 如需不同時間值的詳細資訊，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`VerificationTime`列舉值。

您也可以指定是否在驗證程式中執行撤銷檢查。 例如，您可以執行撤銷檢查，以判斷憑證是否已撤銷。 如需撤銷檢查選項的詳細資訊，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`RevocationCheckStyle`列舉值。

要對證書執行撤銷檢查，請使用`CRLOptionSpec`對象指定證書撤銷清單(CRL)伺服器的URL。 但是，如果您未指定CRL伺服器的URL，則簽名服務會從憑證取得URL。

執行撤銷檢查時，您可以使用線上認證狀態通訊協定(OCSP)伺服器，而不是使用CRL伺服器。 通常，使用OCSP伺服器而非CRL伺服器時，撤銷檢查的執行速度會更快。 （請參閱[線上證書狀態協定](https://tools.ietf.org/html/rfc2560)。）

您可以使用Adobe應用程式與服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是先在Adobe Applications and Services中設定，則會檢查OCSP伺服器，接著檢查CRL伺服器。

如果您未執行撤銷檢查，「簽名服務」不會檢查憑證是否已撤銷。 即，忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用`CRLOptionSpec`和`OCSPOptionSpec`物件來覆寫憑證中指定的URL。 例如，若要覆寫CRL伺服器，您可以叫用`CRLOptionSpec`物件的`setLocalURI`方法。

時間戳記是追蹤已簽署或已認證檔案修改時間的程式。 簽署檔案後，任何人都無法修改它。 時間戳記有助於強制簽署或認證檔案的有效性。 您可以使用`TSPOptionSpec`物件來設定時間戳記選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和web服務快速啟動中，驗證時間被設定為`VerificationTime.CURRENT_TIME`，撤銷檢查被設定為`RevocationCheckStyle.BestEffort`。 由於未指定CRL或OCSP伺服器資訊，因此從證書中獲取伺服器資訊。

**擷取所有數位簽名**

若要確認PDF檔案中的所有數位簽名，請從PDF檔案擷取數位簽名。 所有簽名都會在清單中傳回。 在驗證數位簽名時，請檢查簽名的狀態。

>[!NOTE]
>
>與驗證單一數位簽名不同，當您驗證多個簽名時，不需要指定簽名欄位名稱。

**重複所有簽名**

逐一重複每個簽名。 也就是說，對於每個簽名，請驗證數位簽名，並檢查簽章者的身分和每個簽名的狀態。 （請參閱[驗證數位簽名](#verify-digital-signatures-using-the-java-api)）。

>[!NOTE]
>
>如果要求是整份檔案，則不需要重複所有簽名。

**另請參閱**

[使用Java API驗證多個數位簽名](#verify-digital-signatures-using-the-java-api)

[使用web service API驗證多個數位簽名](#verify-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#verify-multiple-digital-signatures-using-the-java-api}驗證多個數位簽名

使用簽名服務API(Java)驗證多個數位簽名：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`SignatureServiceClient`對象。

1. 取得包含簽名的PDF檔案，以驗證

   * 建立`java.io.FileInputStream`物件，代表包含多個數位簽章的PDF檔案，以使用其建構函式進行驗證。 傳遞指定PDF檔案位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定PKI執行時期選項

   * 使用其建構子建立`PKIOptions`對象。
   * 調用`PKIOptions`物件的`setVerificationTime`方法並傳遞指定驗證時間的`VerificationTime`列舉值，以設定驗證時間。
   * 通過調用`PKIOptions`對象的`setRevocationCheckStyle`方法並傳遞指定是否執行撤銷檢查的`RevocationCheckStyle`枚舉值來設定撤銷檢查選項。

1. 擷取所有數位簽名

   叫用`SignatureServiceClient`物件的`verifyPDFDocument`方法並傳遞下列值：

   * `com.adobe.idp.Document`物件，包含包含多個數位簽名的PDF檔案。
   * 包含PKI運行時選項的`PKIOptions`對象。
   * 包含SPI資訊的`VerifySPIOptions`實例。 您可以指定此參數的`null`。

   `verifyPDFDocument`方法會傳回`PDFDocumentVerificationInfo`物件，其中包含PDF檔案中所有數位簽名的相關資訊。

1. 重複所有簽名

   * 叫用`PDFDocumentVerificationInfo`物件的`getVerificationInfos`方法，以重複所有簽名。 此方法返回`java.util.List`對象，其中每個元素都是`PDFSignatureVerificationInfo`對象。 使用`java.util.Iterator`物件來重複簽名清單。
   * 使用`PDFSignatureVerificationInfo`物件，您可以呼叫`PDFSignatureVerificationInfo`物件的`getStatus`方法，以執行例如判斷簽章狀態等工作。 此方法返回`SignatureStatus`對象，其靜態資料成員會通知您有關簽名的狀態。 例如，如果簽名未知，此方法會傳回`SignatureStatus.DocumentSignatureUnknown`。

**另請參閱**

[驗證多個數位簽名](#verifying-multiple-digital-signatures)

[快速入門（SOAP模式）:使用Java API驗證多個數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#verifying-multiple-digital-signatures-using-the-web-service-api}驗證多個數位簽名

使用簽名服務API(web service)驗證多個數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立簽名用戶端

   * 使用其預設建構子建立`SignatureServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含簽名的PDF檔案，以驗證

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件會儲存包含多個數位簽章以進行驗證的PDF檔案。
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，代表PDF檔案的檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 設定PKI執行時期選項

   * 使用其建構子建立`PKIOptions`對象。
   * 通過為`PKIOptions`對象的`verificationTime`資料成員分配指定驗證時間的`VerificationTime`枚舉值來設定驗證時間。
   * 通過為`PKIOptions`對象的`revocationCheckStyle`資料成員分配`RevocationCheckStyle`枚舉值來設定撤銷檢查選項，該枚舉值指定是否執行撤銷檢查。

1. 擷取所有數位簽名

   叫用`SignatureServiceClient`物件的`verifyPDFDocument`方法並傳遞下列值：

   * `BLOB`物件，包含包含多個數位簽名的PDF檔案。
   * 包含PKI運行時選項的`PKIOptions`對象。
   * 包含SPI資訊的`VerifySPIOptions`實例。 您可以為此參數指定null。

   `verifyPDFDocument`方法會傳回`PDFDocumentVerificationInfo`物件，其中包含PDF檔案中所有數位簽名的相關資訊。

1. 重複所有簽名

   * 取得`PDFDocumentVerificationInfo`物件的`verificationInfos`資料成員，以重複所有簽名。 此資料成員返回`Object`陣列，其中每個元素都是`PDFSignatureVerificationInfo`對象。
   * 使用`PDFSignatureVerificationInfo`物件，您可以取得`PDFSignatureVerificationInfo`物件的`status`資料成員，以執行如決定簽名狀態等工作。 此資料成員返回`SignatureStatus`對象，其靜態資料成員會通知您有關簽名的狀態。 例如，如果簽名未知，此方法會傳回`SignatureStatus.DocumentSignatureUnknown`。

**另請參閱**

[驗證多個數位簽名](#verifying-multiple-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除數字簽名{#removing-digital-signatures}

必須先從簽名欄位移除數位簽名，才能套用較新的數位簽名。 無法覆寫數位簽名。 如果您嘗試將數位簽名套用至包含簽名的簽名欄位，則會發生例外。

>[!NOTE]
>
>如需簽名服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-8}摘要

若要從簽名欄位移除數位簽名，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得包含要移除之簽名的PDF檔案。
1. 從簽名欄位移除數位簽名。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

您必須先建立簽名服務用戶端，才能以程式設計方式執行簽名服務作業。

**取得包含要移除之簽名的PDF檔案**

若要從PDF檔案移除簽名，您必須取得包含簽名的PDF檔案。

**從簽名欄位移除數位簽名**

若要成功從PDF檔案移除數位簽章，您必須指定包含數位簽章的簽名欄位名稱。 此外，您必須擁有移除數位簽名的權限；否則，會發生例外。

**將PDF檔案儲存為PDF檔案**

在簽名服務從簽名欄位移除數位簽名後，您可以將PDF檔案儲存為PDF檔案，讓使用者在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[使用Java API移除數位簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[使用web service API移除數位簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API {#remove-digital-signatures-using-the-java-api}移除數位簽名

使用簽名API(Java)移除數位簽名：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`SignatureServiceClient`對象。

1. 取得包含要移除之簽名的PDF檔案

   * 建立`java.io.FileInputStream`物件，以代表包含要移除之簽名的PDF檔案，方法是使用其建構函式並傳遞指定PDF檔案位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 從簽名欄位移除數位簽名

   叫用`SignatureServiceClient`物件的`clearSignatureField`方法並傳遞下列值，從簽名欄位移除數位簽名：

   * `com.adobe.idp.Document`物件，代表包含要移除之簽名的PDF檔案。
   * 一個字串值，它指定包含數字簽名的簽名欄位的名稱。

   `clearSignatureField`方法會傳回`com.adobe.idp.Document`物件，代表移除數位簽名的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法。 傳遞`java.io.File`物件，將`com.adobe.idp.Document`物件的內容複製至檔案。 請確定您使用`clearSignatureField`方法傳回的`Document`物件。

**另請參閱**

[移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[快速入門（SOAP模式）:使用Java API移除數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#remove-digital-signatures-using-the-web-service-api}移除數位簽名

使用簽名API(web service)移除數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立簽名用戶端

   * 使用其預設建構子建立`SignatureServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含要移除之簽名的PDF檔案

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存包含要移除之數位簽名的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 從簽名欄位移除數位簽名

   叫用`SignatureServiceClient`物件的`clearSignatureField`方法並傳遞下列值，以移除數位簽章：

   * `BLOB`物件，其中包含已簽署的PDF檔案。
   * 一個字串值，代表包含要移除之數位簽名之簽名欄位的名稱。

   `clearSignatureField`方法會傳回`BLOB`物件，代表移除數位簽名的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示包含空簽名欄位的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存`sign`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
