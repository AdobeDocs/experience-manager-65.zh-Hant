---
title: 數字簽名和認證文檔
seo-title: 數字簽名和認證文檔
description: 使用簽名服務可向PDF文檔添加和刪除數字簽名欄位、檢索PDF文檔中的簽名欄位名稱、修改簽名欄位、數字簽名PDF文檔、認證PDF文檔、驗證PDF文檔中的數字簽名、驗證PDF文檔中的所有數字簽名，以及從簽名欄位中刪除數字簽名。
seo-description: 使用簽名服務可向PDF文檔添加和刪除數字簽名欄位、檢索PDF文檔中的簽名欄位名稱、修改簽名欄位、數字簽名PDF文檔、認證PDF文檔、驗證PDF文檔中的數字簽名、驗證PDF文檔中的所有數字簽名，以及從簽名欄位中刪除數字簽名。
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '17113'
ht-degree: 0%

---

# 數字簽名和認證文檔{#digitally-signing-and-certifying-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於簽名服務**

簽章服務可讓您的組織保護其所發送及接收之Adobe PDF檔案的安全與隱私。 此服務使用數位簽名和認證，以確保只有預期的收件者才能更改文檔。 由於安全功能應用於文檔本身，因此文檔在整個生命週期中都保持安全並受到控制。 檔案在離線下載時，以及提交回您的組織時，都會在防火牆之外保持安全。

>[!NOTE]
>
>您可以為簽名服務建立自定義簽名處理程式，該處理程式在調用某些操作（如簽名PDF文檔）時被調用。

**簽名欄位名稱**

某些簽名服務操作要求您指定在其上執行操作的簽名欄位的名稱。 例如，在簽署PDF文檔時，您指定要簽名的簽名欄位的名稱。 假設簽名欄位的全名為`form1[0].Form1[0].SignatureField1[0]`。 您可以指定`SignatureField1[0]`而非`form1[0].Form1[0].SignatureField1[0]`。

有時，衝突會導致簽名服務在錯誤的欄位中籤名（或執行需要簽名欄位名稱的其他操作）。 此衝突是名稱`SignatureField1[0]`出現在同一PDF文檔中兩個或多個位置的結果。 例如，假設PDF文檔包含名為`form1[0].Form1[0].SignatureField1[0]`和`form1[0].Form1[0].SubForm1[0].SignatureField1[0]`的兩個簽名欄位，並且您指定了`SignatureField1[0]`。 在這種情況下，簽名服務會簽名它在迭代文檔中的所有簽名欄位時找到的第一個簽名欄位。

如果PDF文檔中有多個簽名欄位，建議您指定簽名欄位的完整名稱。 即指定`form1[0].Form1[0].SignatureField1[0]`而非`SignatureField1[0]`。

您可以使用簽名服務完成以下任務：

* 將數位簽名欄位添加和刪除到PDF文檔。 （請參閱[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。）
* 檢索位於PDF文檔中的簽名欄位的名稱。 （請參閱[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)。）
* 修改簽名欄位。 （請參閱[修改簽名欄位](digitally-signing-certifying-documents.md#modifying-signature-fields)。）
* 數位簽署PDF檔案。 （請參閱[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。）
* 認證PDF檔案。 （請參閱[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)。）
* 驗證PDF檔案中的數位簽名。 （請參閱[驗證數字簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures)。）
* 驗證PDF檔案中的所有數位簽名。 （請參閱[驗證多個數字簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures)。）
* 從簽名欄位中刪除數字簽名。 （請參閱[刪除數字簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)。）

>[!NOTE]
>
>有關簽名服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 添加簽名欄位{#adding-signature-fields}

數字簽名出現在簽名欄位中，簽名欄位是包含簽名的圖形表示的表單欄位。 簽名欄位可以是可見的或不可見的。 簽名者可以使用預先存在的簽名欄位，或以寫程式方式添加簽名欄位。 無論是哪種情況，簽名欄位都必須存在，才能簽名PDF文檔。

您可以使用簽名服務Java API或簽名Web服務API，以寫程式方式添加簽名欄位。 您可以在PDF檔案中新增多個簽名欄位；但是，每個簽名欄位名稱必須是唯一的。

>[!NOTE]
>
>有些PDF檔案類型不可讓您以程式設計方式新增簽名欄位。 有關簽名服務和添加簽名欄位的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}的摘要

要將簽名欄位添加到PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 取得已新增簽名欄位的PDF檔案。
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

**取得已新增簽名欄位的PDF檔案**

您必須取得已新增簽名欄位的PDF檔案。

**添加簽名欄位**

要成功將簽名欄位添加到PDF文檔，請指定用於標識簽名欄位位置的坐標值。 （如果添加不可見的簽名欄位，則這些值不是必需值。） 此外，還可以指定在將簽名應用到簽名欄位後，PDF文檔中的哪些欄位被鎖定。

**將PDF檔案另存為PDF檔案**

簽名服務將簽名欄位添加到PDF文檔後，您可以將文檔另存為PDF檔案，以便用戶可以在Acrobat或Adobe Reader中開啟該文檔。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API {#add-signature-fields-using-the-java-api}添加簽名欄位

使用簽名API(Java)添加簽名欄位：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`SignatureServiceClient`物件。

1. 取得已新增簽名欄位的PDF檔案

   * 建立`java.io.FileInputStream`對象，該對象表示PDF文檔，通過使用其建構子並傳遞指定PDF文檔位置的字串值，將簽名欄位添加到該文檔中。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 添加簽名欄位

   * 建立`PositionRectangle`對象，該對象使用其建構子指定簽名欄位位置。 在建構子中，指定坐標值。
   * 如果需要，請建立`FieldMDPOptions`對象，該對象指定當將數字簽名應用到簽名欄位時鎖定的欄位。
   * 叫用`SignatureServiceClient`物件的`addSignatureField`方法並傳遞下列值，將簽名欄位新增至PDF檔案：

      * A `com.adobe.idp`. `Document` 表示添加簽名欄位的PDF文檔的對象。
      * 指定簽名欄位名稱的字串值。
      * `java.lang.Integer`值，代表新增簽名欄位的頁碼。
      * `PositionRectangle`對象，它指定簽名欄位的位置。
      * `FieldMDPOptions`對象，指定在將數字簽名應用到簽名欄位後鎖定的PDF文檔中的欄位。 此參數值為選用值，您可以傳遞`null`。
   * 指定各種運行時值的`PDFSeedValueOptions`對象。 此參數值為選用值，您可以傳遞`null`。

      `addSignatureField`方法返回`com.adobe.idp`。 `Document` 表示包含簽名欄位的PDF文檔的對象。
   >[!NOTE]
   >
   >可以調用`SignatureServiceClient`對象的`addInvisibleSignatureField`方法以添加不可見的簽名欄位。

1. 將PDF檔案另存為PDF檔案

   * 建立`java.io.File`物件，並確認副檔名為.pdf。
   * 叫用`com.adobe.idp`。 `Document` 對象的方 `copyToFile` 法，將對象的內容復 `Document` 制到檔案。確保使用`com.adobe.idp`。 `Document` 方法傳回的物 `addSignatureField` 件。

**另請參閱**

[簽名服務API快速入門](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 使用Web服務API {#add-signature-fields-using-the-web-service-api}添加簽名欄位

要使用簽名API（Web服務）添加簽名欄位：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 使用其預設建構子建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得已新增簽名欄位的PDF檔案

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存將包含簽名欄位的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 添加簽名欄位

   叫用`SignatureServiceClient`物件的`addSignatureField`方法並傳遞下列值，將簽名欄位新增至PDF檔案：

   * `BLOB`物件，代表新增簽名欄位的PDF檔案。
   * 指定簽名欄位名稱的字串值。
   * 一個整數值，表示要向其添加簽名欄位的頁碼。
   * `PositionRect`對象，它指定簽名欄位的位置。
   * `FieldMDPOptions`對象，指定在將數字簽名應用到簽名欄位後鎖定的PDF文檔中的欄位。 此參數值為選用值，您可以傳遞`null`。
   * 指定各種運行時值的`PDFSeedValueOptions`對象。 此參數值為選用值，您可以傳遞`null`。

   `addSignatureField`方法返回一個`BLOB`對象，該對象表示包含簽名欄位的PDF文檔。

1. 將PDF檔案另存為PDF檔案

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示將包含簽名欄位和開啟檔案的模式的PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存`addSignatureField`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象的`binaryData`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢索簽名欄位名稱{#retrieving-signature-field-names}

您可以檢索位於要簽名或認證的PDF文檔中的所有簽名欄位的名稱。 如果您不確定位於PDF文檔中的簽名欄位名稱，或要驗證名稱，可以用寫程式方式檢索它們。 簽名服務返回簽名欄位的完全限定名稱，如`form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

>[!NOTE]
>
>如需簽章服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟{#summary_of_steps-1}的摘要

要檢索簽名欄位名稱，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 取得包含簽名欄位的PDF檔案。
1. 檢索簽名欄位名稱。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參閱[包括AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**取得包含簽名欄位的PDF檔案**

檢索包含簽名欄位的PDF文檔。

**檢索簽名欄位名稱**

檢索包含一個或多個簽名欄位的PDF文檔後，可以檢索簽名欄位名稱。

**另請參閱**

[使用Java API檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[使用Web服務API檢索簽名欄位](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API {#retrieve-signature-field-names-using-the-java-api}檢索簽名欄位名稱

使用簽名API(Java)檢索簽名欄位名稱：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`SignatureServiceClient`物件。

1. 取得包含簽名欄位的PDF檔案

   * 建立`java.io.FileInputStream`對象，該對象表示包含簽名欄位的PDF文檔，方法是使用其建構子並傳遞指定PDF文檔位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 檢索簽名欄位名稱

   * 調用`SignatureServiceClient`對象的`getSignatureFieldList`方法並傳遞包含簽名欄位的PDF文檔的`com.adobe.idp.Document`對象，以檢索簽名欄位名稱。 此方法會傳回`java.util.List`物件，其中每個元素都包含`PDFSignatureField`物件。 使用此對象，可以獲取有關簽名欄位的其他資訊，如簽名欄位是否可見。
   * 逐一查看`java.util.List`對象，以確定是否存在簽名欄位名稱。 對於PDF文檔中的每個簽名欄位，可以獲得單獨的`PDFSignatureField`對象。 要獲取簽名欄位的名稱，請調用`PDFSignatureField`對象的`getName`方法。 此方法會傳回指定簽名欄位名稱的字串值。

**另請參閱**

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[快速入門（SOAP模式）:使用Java API檢索簽名欄位名稱](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#retrieve-signature-field-using-the-web-service-api}檢索簽名欄位

使用簽名API（Web服務）檢索簽名欄位名稱：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 使用其預設建構子建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含簽名欄位的PDF檔案

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存包含簽名欄位的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列內容，以填入`BLOB`物件。

1. 檢索簽名欄位名稱

   * 調用`SignatureServiceClient`對象的`getSignatureFieldList`方法並傳遞`BLOB`對象（該對象包含包含簽名欄位的PDF文檔），以檢索簽名欄位名稱。 此方法會傳回`MyArrayOfPDFSignatureField`集合物件，其中每個元素都包含`PDFSignatureField`物件。
   * 逐一查看`MyArrayOfPDFSignatureField`對象，以確定是否存在簽名欄位名稱。 對於PDF文檔中的每個簽名欄位，可以獲取`PDFSignatureField`對象。 要獲取簽名欄位的名稱，請調用`PDFSignatureField`對象的`getName`方法。 此方法會傳回指定簽名欄位名稱的字串值。

**另請參閱**

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改簽名欄位{#modifying-signature-fields}

您可以使用Java API和Web服務API修改PDF檔案中的簽名欄位。 修改簽名欄位涉及操作其簽名欄位鎖定字典值或種子值字典值。

*欄位鎖定字典*&#x200B;指定簽名欄位時鎖定的欄位清單。 鎖定的欄位可防止使用者對欄位進行變更。 *種子值字典*&#x200B;包含在應用簽名時使用的約束資訊。 例如，您可以變更權限，以控制可能發生的動作，而不使簽名失效。

通過修改現有簽名欄位，您可以對PDF文檔進行更改以反映不斷變化的業務需求。 例如，新業務要求可能需要在文檔簽名後鎖定所有文檔欄位。

本節說明如何通過修改欄位鎖定字典和種子值字典值來修改簽名欄位。 對簽名欄位鎖定字典所做的更改會導致簽名欄位時PDF文檔中的所有欄位被鎖定。 對種子值字典所做的更改禁止對文檔進行特定類型的更改。

>[!NOTE]
>
>有關簽名服務和修改簽名欄位的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-2}的摘要

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

有關這些JAR檔案的位置的資訊，請參閱[包括LiveCycleJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**獲取包含要修改的簽名欄位的PDF文檔**

檢索包含要修改的簽名欄位的PDF文檔。

**設定字典值**

要修改簽名欄位，請將值分配給其欄位鎖定字典或種子值字典。 指定簽名欄位鎖定字典值包括指定簽名欄位時鎖定的PDF文檔欄位。 （本節探討如何鎖定所有欄位。）

可設定下列種子值字典值：

* **修訂檢查**:指定在將簽名應用到簽名欄位時是否執行吊銷檢查。
* **憑證選項**:為證書種子值字典指定值。建議您先熟悉憑證種子值字典，再指定憑證選項。 （請參閱[PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。）
* **摘要選項**:指派用於簽署的摘要演算法。有效值為SHA1、SHA256、SHA384、SHA512和RIPEMD160。
* **篩選**:指定與簽名欄位一起使用的篩選器。例如，您可以使用Adobe.PPKLite篩選器。 （請參閱[PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。）
* **標幟選項**:指定與此簽名欄位關聯的標誌值。值1表示簽署者只能為條目使用指定值。 值0表示允許其他值。 位位置如下：

   * **1（篩選器）:** 用於簽名簽名欄位的簽名處理程式
   * **2(SubFilter):** 指出簽署時可使用之可接受編碼的名稱陣列
   * **3(V)**:用於簽名欄位的簽名處理程式的最低所需版本號
   * **4（原因）:** 字串的陣列，指定簽署檔案的可能原因
   * **5(PDFLegalWarnings):** 一系列字串，可指定可能的法律證明

* **法律證明**:認證文檔時，會自動掃描特定類型的內容，這些內容可能使文檔的可見內容模糊或產生誤導。例如，注釋可能會遮蔽對於了解正在認證的內容非常重要的文本。 掃描過程會生成警告，指示是否存在此類內容。 它也提供可能已產生警告之內容的額外說明。
* **權限**:指定可在PDF文檔上使用的權限，而不使簽名失效。
* **原因**:指定必須簽署此文檔的原因。
* **時間戳**:指定時間戳選項。例如，您可以設定所使用時間戳記伺服器的URL。
* **版本**:指定用於簽名欄位的簽名處理程式的最小版本號。

**修改簽名欄位**

建立簽名服務客戶端後，檢索包含要修改的簽名欄位的PDF文檔，並設定字典值，您可以指示簽名服務修改簽名欄位。 然後，簽名服務將返回包含已修改簽名欄位的PDF文檔。 原始PDF文檔不受影響。

**將PDF檔案另存為PDF檔案**

將包含已修改簽名欄位的PDF文檔保存為PDF檔案，以便用戶在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[簽名服務API快速入門](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API {#modify-signature-fields-using-the-java-api}修改簽名欄位

使用簽名API(Java)修改簽名欄位：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`SignatureServiceClient`物件。

1. 獲取包含要修改的簽名欄位的PDF文檔

   * 建立`java.io.FileInputStream`對象，該對象表示包含要修改的簽名欄位的PDF文檔，方法是使用其建構子並傳遞指定PDF文檔位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定字典值

   * 使用其建構子建立`PDFSignatureFieldProperties`物件。 `PDFSignatureFieldProperties`對象儲存簽名欄位鎖字典和種子值字典資訊。
   * 使用其建構子建立`PDFSeedValueOptionSpec`物件。 此物件可讓您設定種子值字典值。
   * 叫用`PDFSeedValueOptionSpec`物件的`setMdpValue`方法並傳遞`MDPPermissions.NoChanges`分項清單，禁止變更PDF檔案。
   * 使用其建構子建立`FieldMDPOptionSpec`物件。 此對象允許您設定簽名欄位鎖定字典值。
   * 叫用`FieldMDPOptionSpec`物件的`setMdpValue`方法並傳遞`FieldMDPAction.ALL`分項清單，以鎖定PDF檔案中的所有欄位。
   * 調用`PDFSignatureFieldProperties`對象的`setSeedValue`方法並傳遞`PDFSeedValueOptionSpec`對象，以設定種子值字典資訊。
   * 調用`PDFSignatureFieldProperties`對象的`setFieldMDP`方法並傳遞`FieldMDPOptionSpec`對象，設定簽名欄位鎖定字典資訊。

   >[!NOTE]
   >
   >要查看可以設定的所有種子值字典值，請參閱`PDFSeedValueOptionSpec`類引用。 (請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

1. 修改簽名欄位

   調用`SignatureServiceClient`對象的`modifySignatureField`方法並傳遞以下值，修改簽名欄位：

   * `com.adobe.idp.Document`對象，用於儲存包含要修改的簽名欄位的PDF文檔
   * 指定簽名欄位名稱的字串值
   * 儲存簽名欄位鎖定字典和種子值字典資訊的`PDFSignatureFieldProperties`對象

   `modifySignatureField`方法返回一個`com.adobe.idp.Document`對象，該對象儲存包含已修改簽名欄位的PDF文檔。

1. 將PDF檔案另存為PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案。 請確定您使用`modifySignatureField`方法傳回的`com.adobe.idp.Document`物件。

### 使用Web服務API {#modify-signature-fields-using-the-web-service-api}修改簽名欄位

使用簽名API（Web服務）修改簽名欄位：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 使用其預設建構子建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 獲取包含要修改的簽名欄位的PDF文檔

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存包含要修改的簽名欄位的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為位元組陣列的內容指派其`MTOM`屬性，以填入`BLOB`物件。

1. 設定字典值

   * 使用其建構子建立`PDFSignatureFieldProperties`物件。 該對象儲存簽名欄位鎖字典和種子值字典資訊。
   * 使用其建構子建立`PDFSeedValueOptionSpec`物件。 此物件可讓您設定種子值字典值。
   * 通過將`MDPPermissions.NoChanges`枚舉值分配給`PDFSeedValueOptionSpec`對象的`mdpValue`資料成員，禁止對PDF文檔進行更改。
   * 使用其建構子建立`FieldMDPOptionSpec`物件。 此對象允許您設定簽名欄位鎖定字典值。
   * 將`FieldMDPAction.ALL`枚舉值分配給`FieldMDPOptionSpec`對象的`mdpValue`資料成員，以鎖定PDF文檔中的所有欄位。
   * 將`PDFSeedValueOptionSpec`對象分配給`PDFSignatureFieldProperties`對象的`seedValue`資料成員，以設定種子值字典資訊。
   * 通過將`FieldMDPOptionSpec`對象分配給`PDFSignatureFieldProperties`對象的`fieldMDP`資料成員，設定簽名欄位鎖定字典資訊。

   >[!NOTE]
   >
   >要查看可以設定的所有種子值字典值，請參閱`PDFSeedValueOptionSpec`類引用。 (請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 修改簽名欄位

   調用`SignatureServiceClient`對象的`modifySignatureField`方法並傳遞以下值，修改簽名欄位：

   * `BLOB`對象，用於儲存包含要修改的簽名欄位的PDF文檔
   * 指定簽名欄位名稱的字串值
   * 儲存簽名欄位鎖定字典和種子值字典資訊的`PDFSignatureFieldProperties`對象

   `modifySignatureField`方法返回一個`BLOB`對象，該對象儲存包含已修改簽名欄位的PDF文檔。

1. 將PDF檔案另存為PDF檔案

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示將包含簽名欄位的PDF文檔的檔案位置，以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存`addSignatureField`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 以數字方式簽署PDF文檔{#digitally-signing-pdf-documents}

數位簽名可套用至PDF檔案，以提供一定的安全性。 數字簽名（如手寫簽名）提供了一種手段，使簽名者能夠識別自己，並對文檔進行聲明。 用於數字簽名文檔的技術有助於確保簽名者和接收者都清楚簽名的內容，並確信文檔自簽名後沒有更改。

PDF檔案採用公開金鑰技術簽署。 簽名者有兩個密鑰：公鑰和私鑰。 私密金鑰儲存在使用者的憑證中，且在簽署時必須可用。 公開金鑰儲存在使用者的憑證中，收件者必須能使用該憑證來驗證簽名。 有關已撤銷證書的資訊可在由證書頒發機構(CA)分發的證書吊銷清單(CRL)和線上證書狀態協定(OCSP)響應中找到。 簽名時間可從稱為時間戳頒發機構的可信源獲得。

>[!NOTE]
>
>您必須確定將憑證新增至AEM Forms，才能數位簽署PDF檔案。 使用管理控制台或使用信任管理器API以程式設計方式新增憑證。 （請參閱[使用信任管理器API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)導入憑據。）

您可以以數位方式簽署PDF檔案。 以數位方式簽署PDF檔案時，您必須參考AEM Forms中存在的安全憑證。 憑據是用於簽名的私鑰。

簽署PDF檔案時，簽名服務會執行下列步驟：

1. 簽名服務通過傳遞請求中指定的別名從Truststore中檢索憑據。
1. Truststore將搜索指定的憑據。
1. 憑證會傳回至簽章服務，並用來簽署檔案。 系統會根據別名快取憑證，以供日後請求使用。

有關處理安全憑據的資訊，請參閱應用程式伺服器的&#x200B;*安裝和部署AEM Forms*&#x200B;指南。

>[!NOTE]
>
>簽名和認證文檔之間存在差異。 （請參閱[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)。）

>[!NOTE]
>
>並非所有PDF檔案都支援簽署。 有關簽名服務和數字簽名文檔的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>簽章服務不支援含有內嵌PDF資料的XDP檔案作為操作的輸入，例如認證檔案。 此動作會導致簽名服務擲出`PDFOperationException`。 若要解決此問題，請使用PDF公用程式服務將XDP檔案轉換為PDF檔案，然後將轉換的PDF檔案傳遞至簽名服務操作。 （請參閱[使用PDF實用程式](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)。）

**密碼nShield HSM憑據**

使用nCipher nShield HSM憑據來簽名或認證PDF文檔時，必須重新啟動部署了AEM Forms的J2EE應用程式伺服器，才能使用新憑據。 但是，您可以設定配置值，從而使簽名或認證操作正常工作，而不重新啟動J2EE應用程式伺服器。

您可以在位於/opt/nfast/cknfastrc(或c:\nfast\cknfastrc)的cknfastrc檔案中添加以下配置值：

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將此配置值添加到cknfastrc檔案後，即可使用新憑據，而無需重新啟動J2EE應用程式伺服器。

**簽名不受信任**

在認證和簽署相同的PDF檔案時，如果不信任認證簽名，在Acrobat或Adobe Reader中開啟PDF檔案時，會針對第一個簽名顯示黃色三角形。 必須信任認證簽名才能避免這種情況。

**簽署以XFA為基礎的表單的檔案**

如果您嘗試使用簽章服務API簽署以XFA為基礎的表單，位於Acrobat的`View` `Signed` `Version`中可能會遺失資料。 例如，請考量下列工作流程：

* 使用Designer建立的XDP檔案，可以合併包含簽名欄位的表單設計和包含表單資料的XML資料。 您可使用Forms服務產生互動式PDF檔案。
* 您使用簽名服務API簽署PDF檔案。

### 步驟{#summary_of_steps-3}的摘要

若要數位簽署PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名服務客戶端。
1. 取得要簽署的PDF檔案。
1. 簽署PDF檔案。
1. 將簽署的PDF檔案儲存為PDF檔案。

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

要簽署PDF文檔，必須獲取包含簽名欄位的PDF文檔。 如果PDF文檔不包含簽名欄位，則無法簽名。 簽名欄位可通過使用Designer或以寫程式方式添加。

**簽署PDF檔案**

簽署PDF檔案時，您可以設定簽名服務使用的執行階段選項。 您可以設定下列選項：

* 外觀選項
* 吊銷檢查
* 時間戳值

可使用`PDFSignatureAppearanceOptionSpec`對象來設定外觀選項。 例如，您可以叫用`PDFSignatureAppearanceOptionSpec`物件的`setShowDate`方法並傳遞`true`，以顯示簽章內的日期。

您也可以指定是否執行吊銷檢查，以確定用於數字簽署PDF文檔的證書是否已被吊銷。 要執行吊銷檢查，可以指定以下值之一：

* **無檢查**:不執行吊銷檢查。
* **BestEffort**:始終嘗試檢查是否吊銷鏈中的所有證書。如果檢查中出現任何問題，則假定吊銷有效。 如果發生任何失敗，請假設憑證未撤銷。
* **CheckIfAvailable:** 如果可取消資訊，則檢查是否吊銷鏈中的所有證書。如果檢查中出現任何問題，則假定吊銷無效。 如果發生任何失敗，假設憑證已撤銷且無效。 （這是預設值。）
* **AlwaysCheck**:檢查是否撤銷鏈中的所有證書。如果任何證書中沒有吊銷資訊，則假定吊銷無效。

要對證書執行吊銷檢查，可以使用`CRLOptionSpec`對象指定證書吊銷清單(CRL)伺服器的URL。 但是，如果要執行吊銷檢查，並且您沒有為CRL伺服器指定URL，則簽名服務將從證書中獲取該URL。

在執行吊銷檢查時，可以使用聯機證書狀態協定(OCSP)伺服器，而不使用CRL伺服器。 通常，當使用OCSP伺服器而不是CRL伺服器時，執行吊銷檢查的速度會更快。 (請參閱[https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560)上的「線上證書狀態協定」。)

您可以使用Adobe應用程式和服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器首先在Adobe應用程式和服務中設定，則檢查OCSP伺服器，然後檢查CRL伺服器。 （請參閱AAC說明中的「使用信任存放區管理憑證和憑證」）。

如果指定不執行吊銷檢查，則簽名服務不會檢查用於簽名或證明文檔的證書是否已被吊銷。 即忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>雖然可以在證書中指定CRL或OCSP伺服器，但可以使用`CRLOptionSpec`和`OCSPOptionSpec`對象來覆蓋在證書中指定的URL。 例如，要覆蓋CRL伺服器，可以調用`CRLOptionSpec`對象的`setLocalURI`方法。

時間戳是指跟蹤已簽名或已認證文檔被修改的時間的過程。 文檔簽名後，即使文檔所有者也不應修改它。 時間戳有助於強制簽署或認證文檔的有效性。 可以使用`TSPOptionSpec`對象設定時間戳選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務中逐個瀏覽各個部分並進行相應的快速啟動，使用撤銷檢查。 由於沒有指定CRL或OCSP伺服器資訊，因此從用於數字簽署PDF文檔的證書中獲取伺服器資訊。

若要成功簽署PDF檔案，您可以指定將包含數位簽名的簽名欄位的完全限定名稱，例如`form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，也可以使用簽名欄位的部分名稱：`SignatureField3[3]`。

您還必須參考安全憑證以數位簽署PDF檔案。 要引用安全憑據，請指定別名。 別名是對實際憑據的引用，該憑據可能位於PKCS#12檔案中（副檔名為.pfx），或硬體安全模組(HSM)中。 有關安全憑據的資訊，請參閱應用程式伺服器的&#x200B;*安裝和部署AEM Forms*&#x200B;指南。

**儲存已簽署的PDF檔案**

簽名服務對PDF檔案進行數位簽署後，您可以將其儲存為PDF檔案，讓使用者能在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[使用Java API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[使用網站服務API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### 使用Java API {#digitally-sign-pdf-documents-using-the-java-api}數位簽署PDF檔案

使用簽章API(Java)以數位方式簽署PDF檔案：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`SignatureServiceClient`物件。

1. 取得要簽署的PDF檔案

   * 建立`java.io.FileInputStream`對象，該對象使用其建構子並傳遞指定PDF文檔位置的字串值，來表示要數字簽名的PDF文檔。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 簽署PDF檔案

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值，以簽署PDF檔案：

   * 代表要簽署的PDF文檔的`com.adobe.idp.Document`對象。
   * 表示將包含數字簽名的簽名欄位的名稱的字串值。
   * `Credential`物件，代表用於數位簽署PDF檔案的憑證。 通過調用`Credential`對象的靜態`getInstance`方法並傳遞指定與安全憑據對應的別名值的字串值，建立`Credential`對象。
   * `HashAlgorithm`物件，指定代表要用於摘要PDF檔案的雜湊演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 代表PDF檔案因數位簽署的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * 控制數字簽名外觀的`PDFSignatureAppearanceOptions`對象。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * `java.lang.Boolean`對象，指定是否對簽名者的證書執行吊銷檢查。
   * `OCSPOptionSpec`物件，可儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。
   * 儲存證書吊銷清單(CRL)首選項的`CRLPreferences`對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，用於儲存時間戳提供程式(TSP)支援的偏好設定。 此參數為選用參數，可以是`null`。 如需詳細資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

   `sign`方法返回一個`com.adobe.idp.Document`對象，該對象表示已簽名的PDF文檔。

1. 儲存已簽署的PDF檔案

   * 建立`java.io.File`物件，並確認副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，並傳遞`java.io.File`以將`Document`對象的內容複製到檔案。 請確定您使用`sign`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[快速入門（SOAP模式）:使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#digitally-signing-pdf-documents-using-the-web-service-api}以數位方式簽署PDF檔案

若要使用簽名API（網站服務）以數位方式簽署PDF檔案：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 使用其預設建構子建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得要簽署的PDF檔案

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存已簽名的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要簽名的PDF文檔的檔案位置以及要在其中開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為位元組陣列的內容指派其`MTOM`屬性，以填入`BLOB`物件。

1. 簽署PDF檔案

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值，以簽署PDF檔案：

   * 代表要簽署的PDF文檔的`BLOB`對象。
   * 表示將包含數字簽名的簽名欄位的名稱的字串值。
   * `Credential`物件，代表用於數位簽署PDF檔案的憑證。 使用其建構子建立`Credential`對象，並通過為`Credential`對象的`alias`屬性指定值來指定別名。
   * `HashAlgorithm`物件，指定代表要用於摘要PDF檔案的雜湊演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 一個布林值，指定是否使用哈希算法。
   * 代表PDF檔案因數位簽署的字串值。
   * 代表簽署者位置的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * 控制數字簽名外觀的`PDFSignatureAppearanceOptions`對象。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * `System.Boolean`對象，指定是否對簽名者的證書執行吊銷檢查。 如果完成了此吊銷檢查，則它嵌入到簽名中。 預設值為`false`。
   * `OCSPOptionSpec`物件，可儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。 如需此物件的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 儲存證書吊銷清單(CRL)首選項的`CRLPreferences`對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，用於儲存時間戳提供程式(TSP)支援的偏好設定。 此參數為選用參數，可以是`null`。

   `sign`方法返回一個`BLOB`對象，該對象表示已簽名的PDF文檔。

1. 儲存已簽署的PDF檔案

   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存`sign`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 以數位方式簽署互動式Forms {#digitally-signing-interactive-forms}

您可以簽署Forms服務建立的互動式表單。 例如，請考量下列工作流程：

* 您可以合併使用Designer建立的基於XFA的PDF表單，以及使用Forms服務在XML文檔中找到的表單資料。 Forms伺服器會轉譯互動式表單。
* 您使用簽名服務API簽署互動式表單。

結果會是以數位簽署的互動式PDF表單。 簽署以XFA表單為基礎的PDF表單時，請務必將PDF檔案儲存為Adobe靜態PDF表單。 如果您嘗試簽署儲存為Adobe動態PDF表單的PDF表單，會發生例外狀況。 因為您正在簽署從Forms服務傳回的表單，請確定表單包含簽名欄位。

>[!NOTE]
>
>您必須確定已將憑證新增至AEM Forms，才能數位簽署互動式表單。 使用管理控制台或使用信任管理器API以程式設計方式新增憑證。 （請參閱[使用信任管理器API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)導入憑據。）

使用Forms服務API時，將`GenerateServerAppearance`執行時間選項設為`true`。 此執行階段選項可確保在Acrobat或Adobe Reader中開啟時，伺服器上產生的表單外觀仍有效。 建議您在使用Forms API產生要簽署的互動式表單時，設定此執行階段選項。

>[!NOTE]
>
>閱讀數位簽署互動式Forms前，建議您先熟悉簽署PDF檔案的方式。 （請參閱[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。）

### 步驟{#summary_of_steps-4}的摘要

若要以數位方式簽署Forms服務傳回的互動式表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms和簽名客戶端。
1. 使用Forms服務取得互動式表單。
1. 簽署互動式表單。
1. 將簽署的PDF檔案儲存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參閱[包括AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立Forms和簽名客戶端**

因為此工作流同時調用Forms和簽名服務，請同時建立Forms服務客戶端和簽名服務客戶端。

**使用Forms服務取得互動式表單**

您可以使用Forms服務取得互動式PDF表單進行簽署。 自AEM Forms起，您可以將`com.adobe.idp.Document`物件傳遞至包含要呈現表單的Forms服務。 此方法的名稱為`renderPDFForm2`。 此方法會傳回`com.adobe.idp.Document`物件，其中包含要簽署的表單。 您可以將此`com.adobe.idp.Document`實例傳遞到簽名服務。

同樣地，如果您使用Web服務，則可以傳遞Forms服務返回簽名服務的`BLOB`實例。

>[!NOTE]
>
>與「數字簽名互動式Forms」部分關聯的快速啟動調用`renderPDFForm2`方法。

**簽署互動式表單**

簽署PDF檔案時，您可以設定簽章服務使用的執行階段選項。 您可以設定下列選項：

* 外觀選項
* 吊銷檢查
* 時間戳值

可使用`PDFSignatureAppearanceOptionSpec`對象來設定外觀選項。 例如，您可以叫用`PDFSignatureAppearanceOptionSpec`物件的`setShowDate`方法並傳遞`true`，以顯示簽章內的日期。

**儲存已簽署的PDF檔案**

簽名服務對PDF文檔進行數字簽名後，您可以將其另存為PDF檔案。 可在Acrobat或Adobe Reader中開啟PDF檔案。

**另請參閱**

[使用Java API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[使用網站服務API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[轉譯互動式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### 使用Java API {#digitally-sign-an-interactive-form-using-the-java-api}數位簽署互動式表單

使用Forms和簽名API(Java)以數位方式簽署互動式表單：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar和adobe-forms-client.jar。

1. 建立Forms和簽名客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`SignatureServiceClient`物件。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`FormsServiceClient`物件。

1. 使用Forms服務取得互動式表單

   * 建立`java.io.FileInputStream`物件，透過其建構函式，代表要傳遞至Forms服務的PDF檔案。 傳遞指定PDF文檔位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。
   * 建立`java.io.FileInputStream`物件，該物件代表包含表單資料的XML檔案，可透過其建構函式傳遞至Forms服務。 傳遞指定XML檔案位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。
   * 建立用於設定運行時選項的`PDFFormRenderSpec`對象。 調用`PDFFormRenderSpec`對象的`setGenerateServerAppearance`方法並傳遞`true`。
   * 調用`FormsServiceClient`對象的`renderPDFForm2`方法並傳遞以下值：

      * `com.adobe.idp.Document`物件，包含要呈現的PDF表單。
      * `com.adobe.idp.Document`物件，包含要與表單合併的資料。
      * 儲存運行時選項的`PDFFormRenderSpec`對象。
      * `URLSpec`物件，包含Forms服務所需的URI值。 您可以為此參數值指定`null`。
      * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。

      `renderPDFForm2`方法返回包含表單資料流的`FormsResult`對象

   * 叫用`FormsResult`物件的`getOutputContent`方法，擷取PDF表單。 此方法會傳回代表互動式表單的`com.adobe.idp.Document`物件。


1. 簽署互動式表單

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值，以簽署PDF檔案：

   * 代表要簽署的PDF文檔的`com.adobe.idp.Document`對象。 請確定此物件為從Forms服務取得的`com.adobe.idp.Document`物件。
   * 表示簽名欄位名稱的字串值。
   * `Credential`物件，代表用於數位簽署PDF檔案的憑證。 調用`Credential`對象的靜態`getInstance`方法，建立`Credential`對象。 傳遞一個字串值，該字串值指定與安全憑據對應的別名值。
   * `HashAlgorithm`物件，指定代表要用於摘要PDF檔案的雜湊演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 代表PDF檔案因數位簽署的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * 控制數字簽名外觀的`PDFSignatureAppearanceOptions`對象。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * `java.lang.Boolean`對象，指定是否對簽名者的證書執行吊銷檢查。
   * `OCSPPreferences`物件，可儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。
   * 儲存證書吊銷清單(CRL)首選項的`CRLPreferences`對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，用於儲存時間戳提供程式(TSP)支援的偏好設定。 此參數為選用參數，可以是`null`。

   `sign`方法返回一個`com.adobe.idp.Document`對象，該對象表示已簽名的PDF文檔。

1. 儲存已簽署的PDF檔案

   * 建立`java.io.File`物件，並確認副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，並傳遞`java.io.File`以將`Document`對象的內容複製到檔案。 請確定您使用`sign`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[數位簽署互動式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[快速入門（SOAP模式）:使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API {#digitally-sign-an-interactive-form-using-the-web-service-api}數位簽署互動式表單

使用Forms和簽名API（網站服務）數位簽署互動式表單：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET項目。 由於此客戶端應用程式調用了兩個AEM Forms服務，因此請建立兩個服務引用。 為與簽名服務關聯的服務引用使用以下WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   為與Forms服務關聯的服務引用使用以下WSDL定義：`http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   因為`BLOB`資料類型對兩個服務引用都是通用的，因此在使用`BLOB`資料類型時，請完全限定該資料類型。 在相應的Web服務快速入門中，所有`BLOB`實例都完全限定。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立Forms和簽名客戶端

   * 使用其預設建構子建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >對Forms服務用戶端重複這些步驟。

1. 使用Forms服務取得互動式表單

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存已簽名的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要簽名的PDF文檔的檔案位置以及要在其中開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為位元組陣列的內容指派其`MTOM`屬性，以填入`BLOB`物件。
   * 使用其建構子建立`BLOB`物件。 `BLOB`物件用於儲存表單資料。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示包含表單資料的XML檔案的檔案位置，以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為位元組陣列的內容指派其`MTOM`屬性，以填入`BLOB`物件。
   * 建立用於設定運行時選項的`PDFFormRenderSpec`對象。 將值`true`指派給`PDFFormRenderSpec`物件的`generateServerAppearance`欄位。
   * 調用`FormsServiceClient`對象的`renderPDFForm2`方法並傳遞以下值：

      * `BLOB`物件，包含要呈現的PDF表單。
      * `BLOB`物件，包含要與表單合併的資料。
      * 儲存運行時選項的`PDFFormRenderSpec`對象。
      * `URLSpec`物件，包含Forms服務所需的URI值。 您可以為此參數值指定`null`。
      * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。
      * 長輸出參數，用於儲存表單中的頁數。
      * 用於地區設定值的字串輸出參數。
      * `FormResult`值，是用於儲存互動式表單的輸出參數。
   * 叫用`FormsResult`物件的`outputContent`欄位，以擷取PDF表單。 此欄位儲存代表互動式表單的`BLOB`物件。


1. 簽署互動式表單

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值，以簽署PDF檔案：

   * 代表要簽署的PDF文檔的`BLOB`對象。 使用Forms服務傳回的`BLOB`例項。
   * 表示簽名欄位名稱的字串值。
   * `Credential`物件，代表用於數位簽署PDF檔案的憑證。 使用其建構子建立`Credential`對象，並通過為`Credential`對象的`alias`屬性指定值來指定別名。
   * `HashAlgorithm`物件，指定代表要用於摘要PDF檔案的雜湊演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 一個布林值，指定是否使用哈希算法。
   * 代表PDF檔案因數位簽署的字串值。
   * 代表簽署者位置的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * 控制數字簽名外觀的`PDFSignatureAppearanceOptions`對象。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * `System.Boolean`對象，指定是否對簽名者的證書執行吊銷檢查。 如果完成了此吊銷檢查，則它嵌入到簽名中。 預設值為`false`。
   * `OCSPPreferences`物件，可儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。 如需此物件的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 儲存證書吊銷清單(CRL)首選項的`CRLPreferences`對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，用於儲存時間戳提供程式(TSP)支援的偏好設定。 此參數為選用參數，可以是`null`。

   `sign`方法返回一個`BLOB`對象，該對象表示已簽名的PDF文檔。

1. 儲存已簽署的PDF檔案

   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存`sign`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[數位簽署互動式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 認證PDF文檔{#certifying-pdf-documents}

您可以使用稱為認證簽名的特定簽名類型對PDF文檔進行認證，以保護該文檔的安全。 經認證的簽名與數字簽名在以下方面有區別：

* 必須是套用至PDF檔案的第一個簽名；也就是說，在應用經認證的簽名時，文檔中的任何其他簽名欄位必須未簽名。 PDF文檔中僅允許一個經認證的簽名。 如果您想要簽署和認證PDF檔案，則必須在簽署前進行認證。 認證PDF檔案後，您可以數位簽署其他簽名欄位。
* 文檔的作者或創作者可以指定文檔可以以某些方式修改，而不使經認證的簽名失效。 例如，該文檔可允許填寫表單或注釋。 如果作者指定不允許進行特定修改，Acrobat會限制使用者以此方式修改檔案。 如果進行了此類修改（例如使用其他應用程式），則經認證的簽名無效，並且Acrobat在用戶開啟文檔時發出警告。 （使用未經認證的簽名時，不會阻止修改，且正常的編輯操作不會使原始簽名無效。）
* 在簽名時，將掃描文檔以查找可能使文檔內容模糊或具有誤導性的特定內容類型。 例如，注釋可能會遮蔽頁面上對於了解正在認證的內容非常重要的文字。 可以提供關於此類內容的說明（法律證明）。

您可以使用簽名服務Java API或簽名網站服務API，以程式設計方式為PDF文檔進行認證。 認證PDF檔案時，必須參考憑證服務中存在的安全憑證。 有關安全憑據的資訊，請參閱應用程式伺服器的&#x200B;*安裝和部署AEM Forms*&#x200B;指南。

>[!NOTE]
>
>在認證和簽署相同的PDF檔案時，如果不信任認證簽名，當您在Acrobat或Adobe Reader中開啟PDF檔案時，第一個簽名簽名旁會出現一個黃色三角形。 必須信任認證簽名才能避免這種情況。

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
>有關簽名服務和證明文檔的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-5}的摘要

要認證PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 取得PDF檔案以進行認證。
1. 認證PDF檔案。
1. 將認證的PDF檔案儲存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參閱[包括AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名操作之前，必須建立簽名客戶端。

**取得PDF檔案以進行認證**

若要認證PDF檔案，您必須取得包含簽名欄位的PDF檔案。 如果PDF檔案不包含簽名欄位，則無法認證它。 簽名欄位可通過使用Designer或以寫程式方式添加。 有關以寫程式方式添加簽名欄位的資訊，請參閱[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。

**認證PDF檔案**

要成功認證PDF文檔，您需要以下由簽名服務使用的輸入值來認證PDF文檔：

* **PDF文檔**:包含簽名欄位的PDF文檔，該表單欄位包含經認證簽名的圖形表示。PDF檔案必須包含簽名欄位，才能獲得認證。 簽名欄位可通過使用Designer或以寫程式方式添加。 （請參閱[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。）
* **簽名欄位名稱**:經認證的簽名欄位的完全限定名稱。以下是範例值：`form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，也可以使用簽名欄位的部分名稱：`SignatureField3[3]`。 如果為欄位名稱傳遞了空值，則動態建立並認證不可見的簽名欄位。
* **安全憑據**:用於認證PDF文檔的憑據。此安全憑據包含密碼和別名，該密碼和別名必須與位於憑據服務中的憑據中顯示的別名匹配。 別名是對實際憑據的引用，該憑據可能位於PKCS#12檔案中（副檔名為.pfx）或硬體安全模組(HSM)中。
* **雜湊演算法**:用於摘要PDF檔案的雜湊演算法。
* **簽署**&#x200B;的原因：顯示在Acrobat或Adobe Reader中的值，讓其他使用者了解PDF檔案獲得認證的原因。
* **簽署者的位置**:憑據指定的簽名者的位置。
* **聯絡資訊**:簽名者的聯繫資訊，如地址和電話號碼。
* **權限資訊**:控制最終用戶可以在文檔上執行的操作而不導致認證簽名無效的權限。例如，您可以設定權限，使得對PDF文檔的任何更改都會導致經認證的簽名無效。
* **法律解釋**:認證文檔時，會自動掃描特定類型的內容，這些內容可能使文檔的內容模糊或產生誤導。例如，注釋可能會遮蔽頁面上對於了解正在認證的內容非常重要的文字。 掃描過程會生成有關這些類型內容的警告。 此值提供可能已產生警告之內容的額外說明。
* **外觀選項**:控制認證簽名外觀的選項。例如，認證的簽名可以顯示日期資訊。
* **吊銷檢查**:該值指定是否對簽名者的證書執行吊銷檢查。預設設定`false`表示未完成吊銷檢查。
* **OCSP設定**:線上憑證狀態通訊協定(OCSP)支援的設定，提供用於認證PDF檔案之憑證狀態的相關資訊。例如，您可以指定伺服器的URL，該URL提供有關用於登錄PDF文檔的憑據的資訊。
* **CRL設定**:完成吊銷檢查時，證書吊銷清單(CRL)首選項的設定。例如，您可以指定始終檢查憑據是否被吊銷。
* **時間戳記**:定義應用於認證簽名的時間戳資訊的設定。時間戳表示特定資料是在某個時間之前建立的。 此知識有助於在簽署者與驗證者之間建立信任關係。

**將經認證的PDF檔案儲存為PDF檔案**

簽章服務認證PDF檔案後，您可以將其儲存為PDF檔案，讓使用者能在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[使用Java API認證PDF檔案](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[使用Web服務API認證PDF檔案](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API {#certify-pdf-documents-using-the-java-api}認證PDF文檔

使用簽名API(Java)認證PDF文檔：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`SignatureServiceClient`物件。

1. 取得PDF檔案以進行認證

   * 使用PDF文檔的建構子並傳遞指定PDF文檔位置的字串值，建立一個`java.io.FileInputStream`對象，該對象表示要認證的PDF文檔。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 認證PDF檔案

   叫用`SignatureServiceClient`物件的`certify`方法並傳遞下列值，以驗證PDF檔案：

   * 代表要認證的PDF檔案的`com.adobe.idp.Document`物件。
   * 表示將包含簽名的簽名欄位的名稱的字串值。
   * `Credential`物件，代表用來認證PDF檔案的憑證。 通過調用`Credential`對象的靜態`getInstance`方法並傳遞指定與安全憑據對應的別名值的字串值，建立`Credential`對象。
   * `HashAlgorithm`物件，指定代表用於摘要PDF檔案的雜湊演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 代表PDF檔案獲得認證原因的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * `MDPPermissions`物件，指定可在PDF檔案上執行的使簽名失效的動作。
   * 控制認證簽名外觀的`PDFSignatureAppearanceOptions`對象。 如果需要，通過調用方法（如`setShowDate`）來修改簽名的外觀。
   * 字串值，可說明使簽名無效的動作。
   * `java.lang.Boolean`對象，指定是否對簽名者的證書執行吊銷檢查。 如果完成了此吊銷檢查，則它嵌入到簽名中。 預設值為`false`。
   * `java.lang.Boolean`對象，它指定是否鎖定要認證的簽名欄位。 如果欄位被鎖定，則簽名欄位被標籤為只讀，其屬性無法修改，並且沒有必需權限的任何人無法清除該欄位。 預設值為`false`。
   * `OCSPPreferences`物件，可儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。 如需此物件的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 儲存證書吊銷清單(CRL)首選項的`CRLPreferences`對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，用於儲存時間戳提供程式(TSP)支援的偏好設定。 例如，建立`TSPPreferences`物件後，您可以叫用`TSPPreferences`物件的`setTspServerURL`方法，以設定TSP伺服器的URL。 此參數為選用參數，可以是`null`。 如需詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

   `certify`方法返回一個`com.adobe.idp.Document`對象，該對象表示經認證的PDF文檔。

1. 將經認證的PDF檔案儲存為PDF檔案

   * 建立`java.io.File`物件，並確認副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案。

**另請參閱**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[快速入門（SOAP模式）:使用Java API驗證PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#certify-pdf-documents-using-the-web-service-api}認證PDF文檔

使用簽名API（Web服務）認證PDF文檔：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 使用其預設建構子建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得PDF檔案以進行認證

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存經認證的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要認證的PDF文檔的檔案位置以及要在其中開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`資料成員分配位元組陣列的內容，以填充`BLOB`對象。

1. 認證PDF檔案

   叫用`SignatureServiceClient`物件的`certify`方法並傳遞下列值，以驗證PDF檔案：

   * 代表要認證的PDF檔案的`BLOB`物件。
   * 表示將包含簽名的簽名欄位的名稱的字串值。
   * `Credential`物件，代表用來認證PDF檔案的憑證。 使用其建構子建立`Credential`對象，並通過為`Credential`對象的`alias`屬性指定值來指定別名。
   * `HashAlgorithm`物件，指定代表用於摘要PDF檔案的雜湊演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演算法。
   * 一個布林值，指定是否使用哈希算法。
   * 代表PDF檔案獲得認證原因的字串值。
   * 代表簽署者位置的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * `MDPPermissions`對象的靜態資料成員，該成員指定可在使簽名無效的PDF文檔上執行的操作。
   * 一個布爾值，它指定是否使用傳遞為前一個參數值的`MDPPermissions`對象。
   * 一個字串值，說明使簽名無效的操作。
   * 控制認證簽名外觀的`PDFSignatureAppearanceOptions`對象。 使用其建構子建立`PDFSignatureAppearanceOptions`物件。 可以通過設定簽名的一個資料成員來修改簽名的外觀。
   * `System.Boolean`對象，指定是否對簽名者的證書執行吊銷檢查。 如果完成了此吊銷檢查，則它嵌入到簽名中。 預設值為`false`。
   * `System.Boolean`對象，它指定是否鎖定要認證的簽名欄位。 如果欄位被鎖定，則簽名欄位被標籤為只讀，其屬性無法修改，並且沒有必需權限的任何人無法清除該欄位。 預設值為`false`。
   * `System.Boolean`對象，指定是否鎖定簽名欄位。 也就是說，如果將`true`傳遞至上一個參數，則將`true`傳遞至此參數。
   * `OCSPPreferences`物件，用於儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定，可提供用於認證PDF檔案之憑證狀態的相關資訊。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。
   * 儲存證書吊銷清單(CRL)首選項的`CRLPreferences`對象。 如果未完成吊銷檢查，則不使用此參數，您可以指定`null`。
   * `TSPPreferences`物件，用於儲存時間戳提供程式(TSP)支援的偏好設定。 例如，建立`TSPPreferences`對象後，可以通過設定`TSPPreferences`對象的`tspServerURL`資料成員來設定TSP的URL。 此參數為選用參數，可以是`null`。

   `certify`方法返回一個`BLOB`對象，該對象表示經認證的PDF文檔。

1. 將經認證的PDF檔案儲存為PDF檔案

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示將包含經認證的PDF文檔的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存`certify`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象的`binaryData`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證數字簽名{#verifying-digital-signatures}

數字簽名可以驗證，以確保已簽名的PDF文檔未被修改，並且數字簽名有效。 驗證數字簽名時，您可以檢查簽名的狀態和簽名的屬性，如簽名者的身份。 信任數字簽名之前，建議您驗證它。 驗證數字簽名時，請參考包含數字簽名的PDF文檔。

假設簽名者的身份未知。 在Acrobat中開啟PDF檔案時，警告訊息會指出簽署者的身分不明，如下圖所示。

![vd_vd_verifsig](assets/vd_vd_verifysig.png)

同樣，當以寫程式方式驗證數字簽名時，可以確定簽名者的身份狀態。 例如，如果您驗證上圖所示檔案中的數位簽名，結果會是簽名者的身份未知。

>[!NOTE]
>
>有關簽名服務和驗證數字簽名的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-6}的摘要

要驗證數字簽名，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 取得包含要驗證之簽名的PDF檔案。
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

有關這些JAR檔案的位置的資訊，請參閱[包括AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，請建立簽名服務客戶端。

**取得包含要驗證之簽名的PDF檔案**

要驗證用於數字簽名或認證PDF文檔的簽名，請獲取包含簽名的PDF文檔。

**設定PKI運行時選項**

設定簽名服務在驗證PDF文檔中的簽名時使用的以下PKI運行時選項：

* 驗證時間
* 吊銷檢查
* 時間戳值

作為設定這些選項的一部分，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），以指出要使用目前時間。 如需不同時間值的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`VerificationTime`列舉值。

您還可以指定是否在驗證過程中執行吊銷檢查。 例如，您可以執行吊銷檢查以確定證書是否被吊銷。 有關吊銷檢查選項的資訊，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`RevocationCheckStyle`枚舉值。

要對證書執行吊銷檢查，請使用`CRLOptionSpec`對象指定證書吊銷清單(CRL)伺服器的URL。 但是，如果您未指定URL到CRL伺服器，則簽名服務將從證書中獲取該URL。

在執行吊銷檢查時，可以使用聯機證書狀態協定(OCSP)伺服器，而不使用CRL伺服器。 通常，當使用OCSP伺服器而不是CRL伺服器時，執行吊銷檢查的速度會更快。 （請參閱[線上證書狀態協定](https://tools.ietf.org/html/rfc2560)。）

您可以通過使用Adobe應用程式和服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器首先在Adobe應用程式和服務中設定，則檢查OCSP伺服器，然後檢查CRL伺服器。

如果您未執行吊銷檢查，則簽名服務不檢查證書是否被吊銷。 即忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用`CRLOptionSpec`和`OCSPOptionSpec`物件來覆寫憑證中指定的URL。 例如，要覆蓋CRL伺服器，可以調用`CRLOptionSpec`對象的`setLocalURI`方法。

時間戳是跟蹤已簽名或經認證的文檔被修改的時間的過程。 文檔簽名後，任何人都無法修改它。 時間戳有助於強制簽署或認證文檔的有效性。 可以使用`TSPOptionSpec`對象設定時間戳選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務快速啟動中，驗證時間被設定為`VerificationTime.CURRENT_TIME`，吊銷檢查被設定為`RevocationCheckStyle.BestEffort`。 由於未指定CRL或OCSP伺服器資訊，因此從證書中獲取伺服器資訊。

**驗證數字簽名**

要成功驗證簽名，請指定包含簽名的簽名欄位的完全限定名稱，例如`form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，您也可以使用簽名欄位的部分名稱：`SignatureField3`。

預設情況下，簽名服務將文檔在驗證後簽名的時間限制為65分鐘。 如果用戶嘗試在當前時間驗證簽名，並且簽名時間晚於當前時間並且在65分鐘內，則簽名服務不會建立驗證錯誤。

>[!NOTE]
>
>有關驗證簽名時需要的其他值，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

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

### 使用Java API {#verify-digital-signatures-using-the-java-api}驗證數字簽名

使用簽名服務API(Java)驗證數字簽名：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`SignatureServiceClient`物件。

1. 取得包含要驗證之簽名的PDF檔案

   * 建立`java.io.FileInputStream`對象，該對象表示包含要使用其建構子驗證的簽名的PDF文檔。 傳遞指定PDF文檔位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定PKI運行時選項

   * 使用其建構子建立`PKIOptions`物件。
   * 通過調用`PKIOptions`對象的`setVerificationTime`方法並傳遞指定驗證時間的`VerificationTime`枚舉值來設定驗證時間。
   * 通過調用`PKIOptions`對象的`setRevocationCheckStyle`方法並傳遞指定是否執行吊銷檢查的`RevocationCheckStyle`枚舉值來設定吊銷檢查選項。

1. 驗證數字簽名

   調用`SignatureServiceClient`對象的`verify2`方法並傳遞以下值以驗證簽名：

   * `com.adobe.idp.Document`物件，包含數位簽署或認證的PDF檔案。
   * 表示包含要驗證的簽名的簽名欄位名稱的字串值。
   * 包含PKI運行時選項的`PKIOptions`對象。
   * 包含SPI資訊的`VerifySPIOptions`實例。 您可以為此參數指定`null`。

   `verify2`方法返回一個`PDFSignatureVerificationInfo`對象，該對象包含可用於驗證數字簽名的資訊。

1. 確定簽名的狀態

   * 調用`PDFSignatureVerificationInfo`對象的`getStatus`方法來確定簽名的狀態。 此方法返回指定簽名狀態的`SignatureStatus`對象。 例如，如果未修改已簽名的PDF文檔，此方法將返回`SignatureStatus.DocumentSigNoChanges`。

1. 確定簽名者的身份

   * 調用`PDFSignatureVerificationInfo`對象的`getSigner`方法，確定簽署者的身份。 此方法會傳回`IdentityInformation`物件。
   * 調用`IdentityInformation`對象的`getStatus`方法以確定簽名者的身份。 此方法會傳回指定身分的`IdentityStatus`列舉值。 例如，如果簽名者受信任，則此方法將返回`IdentityStatus.TRUSTED`。

**另請參閱**

[驗證數字簽名](#verify-digital-signatures-using-the-java-api)

[快速入門（SOAP模式）:使用Java API驗證數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#verify-digital-signatures-using-the-web-service-api}驗證數字簽名

使用簽名服務API（Web服務）驗證數字簽名：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 使用其預設建構子建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含要驗證之簽名的PDF檔案

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存包含要驗證的數字簽名或認證簽名的PDF文檔。
   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為位元組陣列的內容指派其`MTOM`屬性，以填入`BLOB`物件。

1. 設定PKI運行時選項

   * 使用其建構子建立`PKIOptions`物件。
   * 通過為`PKIOptions`對象的`verificationTime`資料成員分配指定驗證時間的`VerificationTime`枚舉值來設定驗證時間。
   * 通過為`PKIOptions`對象的`revocationCheckStyle`資料成員分配指定是否執行吊銷檢查的`RevocationCheckStyle`枚舉值來設定吊銷檢查選項。

1. 驗證數字簽名

   調用`SignatureServiceClient`對象的`verify2`方法並傳遞以下值以驗證簽名：

   * `BLOB`物件，包含數位簽名或認證的PDF檔案。
   * 表示包含要驗證的簽名的簽名欄位名稱的字串值。
   * 包含PKI運行時選項的`PKIOptions`對象。
   * 包含SPI資訊的`VerifySPIOptions`實例。 您可以為此參數指定`null`。

   `verify2`方法返回一個`PDFSignatureVerificationInfo`對象，該對象包含可用於驗證數字簽名的資訊。

1. 確定簽名的狀態

   通過獲取`PDFSignatureVerificationInfo`對象的`status`資料成員的值來確定簽名的狀態。 此資料成員儲存指定簽名狀態的`SignatureStatus`對象。 例如，如果修改了帶簽名的PDF文檔，`status`資料成員將儲存值`SignatureStatus.DocumentSigNoChanges`。

1. 確定簽名者的身份

   * 通過檢索`PDFSignatureVerificationInfo`對象的`signer`資料成員的值來確定簽名者的身份。 此成員返回`IdentityInformation`對象。
   * 檢索`IdentityInformation`對象的`status`資料成員以確定簽名者的身份。 此資料成員返回指定標識的`IdentityStatus`枚舉值。 例如，如果簽名者受信任，則此成員返回`IdentityStatus.TRUSTED`。

**另請參閱**

[驗證數字簽名](#verify-digital-signatures-using-the-java-api)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證多個數字簽名{#verifying-multiple-digital-signatures}

AEM Forms提供驗證PDF檔案中所有數位簽名的方法。 假設PDF檔案包含多個數位簽名，因為業務流程需要多個簽名者的簽名。 例如，考慮一項金融交易，該交易既需要貸款官的簽名，又需要經理的簽名。 您可以使用簽名服務Java API或Web服務API來驗證PDF文檔中的所有簽名。 驗證多個數字簽名時，您可以檢查每個簽名的狀態和屬性。 信任數字簽名之前，建議您驗證它。 建議您熟悉驗證單一數位簽名。

>[!NOTE]
>
>有關簽名服務和驗證數字簽名的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-7}的摘要

要驗證多個數字簽名，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 取得包含要驗證之簽名的PDF檔案。
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

有關這些JAR檔案的位置的資訊，請參閱[包括AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，請建立簽名服務客戶端。

**獲取包含要驗證的簽名的PDF文檔**

要驗證用於數字簽名或認證PDF文檔的簽名，請獲取包含簽名的PDF文檔。

**設定PKI運行時選項**

設定簽名服務在驗證PDF文檔中的所有簽名時使用的以下PKI運行時選項：

* 驗證時間
* 吊銷檢查
* 時間戳值

作為設定這些選項的一部分，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），以指出要使用目前時間。 如需不同時間值的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`VerificationTime`列舉值。

您還可以指定是否在驗證過程中執行吊銷檢查。 例如，您可以執行吊銷檢查以確定證書是否被吊銷。 有關吊銷檢查選項的資訊，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`RevocationCheckStyle`枚舉值。

要對證書執行吊銷檢查，請使用`CRLOptionSpec`對象指定證書吊銷清單(CRL)伺服器的URL。 但是，如果您沒有為CRL伺服器指定URL，則簽名服務將從證書中獲取該URL。

在執行吊銷檢查時，可以使用聯機證書狀態協定(OCSP)伺服器，而不使用CRL伺服器。 通常，使用OCSP伺服器（而不是CRL伺服器）時，執行吊銷檢查的速度會更快。 （請參閱[線上證書狀態協定](https://tools.ietf.org/html/rfc2560)。）

您可以通過使用Adobe應用程式和服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是先在Adobe應用程式和服務中設定的，則會檢查OCSP伺服器，然後檢查CRL伺服器。

如果您未執行吊銷檢查，則簽名服務不檢查證書是否被吊銷。 即忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用`CRLOptionSpec`和`OCSPOptionSpec`物件來覆寫憑證中指定的URL。 例如，要覆蓋CRL伺服器，可以調用`CRLOptionSpec`對象的`setLocalURI`方法。

時間戳是跟蹤已簽名或經認證的文檔被修改的時間的過程。 文檔簽名後，任何人都無法修改它。 時間戳有助於強制簽署或認證文檔的有效性。 您可以使用`TSPOptionSpec`物件來設定時間戳記選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務快速啟動中，驗證時間被設定為`VerificationTime.CURRENT_TIME`，吊銷檢查被設定為`RevocationCheckStyle.BestEffort`。 由於未指定CRL或OCSP伺服器資訊，因此從證書中獲取伺服器資訊。

**檢索所有數字簽名**

要驗證PDF文檔中的所有數字簽名，請從PDF文檔中檢索數字簽名。 所有簽名都在清單中返回。 作為驗證數字簽名的一部分，請檢查簽名的狀態。

>[!NOTE]
>
>與驗證單個數字簽名時不同，驗證多個簽名時不需要指定簽名欄位名稱。

**重複查看所有簽名**

逐個反覆檢查每個簽名。 即對於每個簽名，驗證數字簽名，並檢查簽名者的身份和每個簽名的狀態。 （請參閱[驗證數字簽名](#verify-digital-signatures-using-the-java-api)。）

>[!NOTE]
>
>如果要求是整個文檔，則無需重複執行所有簽名。

**另請參閱**

[使用Java API驗證多個數位簽名](#verify-digital-signatures-using-the-java-api)

[使用Web服務API驗證多個數字簽名](#verify-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#verify-multiple-digital-signatures-using-the-java-api}驗證多個數字簽名

使用簽名服務API(Java)驗證多個數字簽名：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`SignatureServiceClient`物件。

1. 獲取包含要驗證的簽名的PDF文檔

   * 建立`java.io.FileInputStream`對象，該對象表示包含多個數字簽名的PDF文檔，以使用其建構子進行驗證。 傳遞指定PDF文檔位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定PKI運行時選項

   * 使用其建構子建立`PKIOptions`物件。
   * 通過調用`PKIOptions`對象的`setVerificationTime`方法並傳遞指定驗證時間的`VerificationTime`枚舉值來設定驗證時間。
   * 通過調用`PKIOptions`對象的`setRevocationCheckStyle`方法並傳遞指定是否執行吊銷檢查的`RevocationCheckStyle`枚舉值來設定吊銷檢查選項。

1. 檢索所有數字簽名

   調用`SignatureServiceClient`對象的`verifyPDFDocument`方法並傳遞以下值：

   * `com.adobe.idp.Document`物件，包含包含多個數位簽名的PDF檔案。
   * 包含PKI運行時選項的`PKIOptions`對象。
   * 包含SPI資訊的`VerifySPIOptions`實例。 您可以為此參數指定`null`。

   `verifyPDFDocument`方法返回`PDFDocumentVerificationInfo`對象，該對象包含有關位於PDF文檔中的所有數字簽名的資訊。

1. 重複查看所有簽名

   * 調用`PDFDocumentVerificationInfo`對象的`getVerificationInfos`方法，查看所有簽名。 此方法會傳回`java.util.List`物件，其中每個元素都是`PDFSignatureVerificationInfo`物件。 使用`java.util.Iterator`物件來反覆查看簽名清單。
   * 使用`PDFSignatureVerificationInfo`對象，可以通過調用`PDFSignatureVerificationInfo`對象的`getStatus`方法來執行諸如確定簽名狀態之類的任務。 此方法會傳回`SignatureStatus`物件，其靜態資料成員會通知您簽名的狀態。 例如，如果簽名未知，則此方法返回`SignatureStatus.DocumentSignatureUnknown`。

**另請參閱**

[驗證多個數字簽名](#verifying-multiple-digital-signatures)

[快速入門（SOAP模式）:使用Java API驗證多個數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[驗證數字簽名](#verify-digital-signatures-using-the-java-api)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#verifying-multiple-digital-signatures-using-the-web-service-api}驗證多個數字簽名

使用簽名服務API（Web服務）驗證多個數字簽名：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 使用其預設建構子建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 獲取包含要驗證的簽名的PDF文檔

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象儲存包含要驗證的多個數字簽名的PDF文檔。
   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為位元組陣列的內容指派其`MTOM`屬性，以填入`BLOB`物件。

1. 設定PKI運行時選項

   * 使用其建構子建立`PKIOptions`物件。
   * 通過為`PKIOptions`對象的`verificationTime`資料成員分配指定驗證時間的`VerificationTime`枚舉值來設定驗證時間。
   * 通過為`PKIOptions`對象的`revocationCheckStyle`資料成員分配指定是否執行吊銷檢查的`RevocationCheckStyle`枚舉值來設定吊銷檢查選項。

1. 檢索所有數字簽名

   調用`SignatureServiceClient`對象的`verifyPDFDocument`方法並傳遞以下值：

   * `BLOB`物件，包含包含多個數位簽名的PDF檔案。
   * 包含PKI運行時選項的`PKIOptions`對象。
   * 包含SPI資訊的`VerifySPIOptions`實例。 可以為此參數指定null。

   `verifyPDFDocument`方法返回`PDFDocumentVerificationInfo`對象，該對象包含有關位於PDF文檔中的所有數字簽名的資訊。

1. 重複查看所有簽名

   * 獲取`PDFDocumentVerificationInfo`對象的`verificationInfos`資料成員，重複所有簽名。 此資料成員返回`Object`陣列，其中每個元素都是`PDFSignatureVerificationInfo`對象。
   * 使用`PDFSignatureVerificationInfo`對象，可以通過獲取`PDFSignatureVerificationInfo`對象的`status`資料成員來執行諸如確定簽名狀態之類的任務。 此資料成員返回一個`SignatureStatus`對象，其靜態資料成員會通知您簽名的狀態。 例如，如果簽名未知，則此方法返回`SignatureStatus.DocumentSignatureUnknown`。

**另請參閱**

[驗證多個數字簽名](#verifying-multiple-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除數字簽名{#removing-digital-signatures}

必須先從簽名欄位中刪除數字簽名，然後才能應用較新的數字簽名。 無法覆蓋數字簽名。 如果嘗試將數字簽名應用到包含簽名的簽名欄位，則會發生異常。

>[!NOTE]
>
>如需簽章服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-8}的摘要

要從簽名欄位中刪除數字簽名，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名客戶端。
1. 取得包含要移除之簽名的PDF檔案。
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

有關這些JAR檔案的位置的資訊，請參閱[包括AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**取得包含要移除之簽名的PDF檔案**

要從PDF文檔中刪除簽名，必須獲取包含簽名的PDF文檔。

**從簽名欄位中刪除數字簽名**

要成功從PDF文檔中刪除數字簽名，必須指定包含數字簽名的簽名欄位的名稱。 此外，您必須擁有移除數位簽名的權限；否則，會發生例外。

**將PDF檔案另存為PDF檔案**

簽章服務從簽名欄位移除數位簽名後，您可以將PDF檔案儲存為PDF檔案，讓使用者能在Acrobat或Adobe Reader中開啟該檔案。

**另請參閱**

[使用Java API移除數位簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[使用Web服務API刪除數字簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API {#remove-digital-signatures-using-the-java-api}刪除數字簽名

使用簽名API(Java)刪除數字簽名：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`SignatureServiceClient`物件。

1. 取得包含要移除之簽名的PDF檔案

   * 建立`java.io.FileInputStream`對象，該對象表示包含要刪除的簽名的PDF文檔，方法是使用其建構子並傳遞指定PDF文檔位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 從簽名欄位中刪除數字簽名

   調用`SignatureServiceClient`對象的`clearSignatureField`方法並傳遞以下值，從簽名欄位中刪除數字簽名：

   * `com.adobe.idp.Document`物件，代表包含要移除之簽名的PDF檔案。
   * 一個字串值，它指定包含數字簽名的簽名欄位的名稱。

   `clearSignatureField`方法返回一個`com.adobe.idp.Document`對象，該對象表示從中刪除數字簽名的PDF文檔。

1. 將PDF檔案另存為PDF檔案

   * 建立`java.io.File`物件，並確認副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法。 傳遞`java.io.File`物件，將`com.adobe.idp.Document`物件的內容複製到檔案。 請確定您使用`clearSignatureField`方法傳回的`Document`物件。

**另請參閱**

[移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[快速入門（SOAP模式）:使用Java API移除數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#remove-digital-signatures-using-the-web-service-api}刪除數字簽名

使用簽名API（Web服務）刪除數字簽名：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立簽名客戶端

   * 使用其預設建構子建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`SignatureServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含要移除之簽名的PDF檔案

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存包含要刪除的數字簽名的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 從簽名欄位中刪除數字簽名

   調用`SignatureServiceClient`對象的`clearSignatureField`方法並傳遞以下值，以刪除數字簽名：

   * `BLOB`物件，包含已簽署的PDF檔案。
   * 一個字串值，它表示包含要刪除的數字簽名的簽名欄位的名稱。

   `clearSignatureField`方法返回一個`BLOB`對象，該對象表示從中刪除數字簽名的PDF文檔。

1. 將PDF檔案另存為PDF檔案

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示包含空簽名欄位的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存`sign`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
