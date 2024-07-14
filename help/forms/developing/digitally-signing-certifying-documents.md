---
title: 數位簽署和認證檔案
description: 使用簽名服務在PDF檔案中新增和刪除數位簽名欄位、擷取PDF檔案中簽名欄位的名稱、修改簽名欄位、數位簽署PDF檔案、認證PDF檔案、驗證PDF檔案中的數位簽名、驗證PDF檔案中的所有數位簽名，以及從簽名欄位中移除數位簽名。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '16917'
ht-degree: 0%

---

# 數位簽署和認證檔案 {#digitally-signing-and-certifying-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於簽章服務**

簽名服務可讓貴組織保護所散發及接收之Adobe PDF檔案的安全性與隱私權。 此服務使用數位簽名和憑證，以確保只有預期的收件者才能變更檔案。 因為安全功能會套用至檔案本身，所以檔案在其整個生命週期中都會保持安全及受控。 當檔案離線下載以及將它送回您的組織時，防火牆外仍會保持安全。

>[!NOTE]
>
>您可以建立自訂簽章處理常式，以便在叫用某些作業(例如簽署PDF檔案)時叫用簽章服務。

**簽章欄位名稱**

某些簽章服務作業需要您指定執行作業的簽章欄位名稱。 例如，在簽署PDF檔案時，您可以指定要簽署的簽名欄位名稱。 假設簽章欄位的完整名稱是`form1[0].Form1[0].SignatureField1[0]`。 您可以指定`SignatureField1[0]`而不是`form1[0].Form1[0].SignatureField1[0]`。

有時衝突會導致簽章服務簽署（或執行其他需要簽章欄位名稱的作業）錯誤的欄位。 此衝突是名稱`SignatureField1[0]`出現在同一PDF檔案中的兩個或多個位置的結果。 例如，假設一個PDF檔案包含兩個名為`form1[0].Form1[0].SignatureField1[0]`和`form1[0].Form1[0].SubForm1[0].SignatureField1[0]`的簽章欄位，而您指定了`SignatureField1[0]`。 在此情況下，簽名服務會在反複處理檔案中的所有簽名欄位時找到第一個簽名欄位簽名。

如果PDF檔案中有多個簽名欄位，建議您指定簽名欄位的完整名稱。 也就是說，請指定`form1[0].Form1[0].SignatureField1[0]`而非`SignatureField1[0]`。

您可以使用簽名服務完成這些工作：

* 新增和刪除數位簽名欄位至PDF檔案。 （請參閱[新增簽章欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。）
* 擷取PDF檔案中簽名欄位的名稱。 （請參閱[擷取簽章欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)。）
* 修改簽名欄位。 （請參閱[修改簽章欄位](digitally-signing-certifying-documents.md#modifying-signature-fields)。）
* 數位簽署PDF檔案。 (請參閱[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)
* 認證PDF檔案。 (請參閱[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)。)
* 驗證PDF檔案中的數位簽章。 （請參閱[驗證數位簽章](digitally-signing-certifying-documents.md#verifying-digital-signatures)。）
* 驗證PDF檔案中的所有數位簽章。 （請參閱[驗證多個數位簽章](digitally-signing-certifying-documents.md#verifying-digital-signatures)。）
* 從簽名欄位中移除數位簽名。 （請參閱[移除數位簽章](digitally-signing-certifying-documents.md#removing-digital-signatures)。）

>[!NOTE]
>
>如需有關簽章服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 新增簽名欄位 {#adding-signature-fields}

數位簽章會出現在簽章欄位中，這些欄位是包含簽章圖形表示的表單欄位。 簽章欄位可以顯示或隱藏。 簽名者可以使用預先存在的簽名欄位，也可以以程式設計方式新增簽名欄位。 在任何一種情況下，簽章欄位都必須存在，才能簽署PDF檔案。

您可以使用簽名服務Java API或簽名網站服務API，以程式設計方式新增簽名欄位。 您可以將多個簽章欄位新增至PDF檔案；但是，每個簽章欄位名稱必須是唯一的。

>[!NOTE]
>
>有些PDF檔案型別不允許您以程式設計方式新增簽名欄位。 如需有關簽章服務和新增簽章欄位的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要將簽名欄位新增至PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得新增簽名欄位的PDF檔案。
1. 新增簽名欄位。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立簽章使用者端**

您必須先建立簽名服務使用者端，才能以程式設計方式執行簽名服務作業。

**取得已新增簽名欄位的PDF檔案**

取得新增簽名欄位的PDF檔案。

**新增簽名欄位**

若要成功將簽名欄位新增到PDF檔案中，請指定可識別簽名欄位位置的座標值。 （如果您新增隱藏的簽章欄位，這些值並非必要值。） 此外，您可以指定PDF檔案中的哪些欄位會在簽名套用至簽名欄位後鎖定。

**將PDF檔案儲存為PDF檔案**

簽名服務將簽名欄位新增到PDF檔案後，您可以將檔案儲存為PDF檔案，以便使用者可以在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API新增簽名欄位 {#add-signature-fields-using-the-java-api}

使用簽名API (Java)新增簽名欄位：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽章使用者端

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`SignatureServiceClient`物件。

1. 取得新增簽名欄位的PDF檔案

   * 使用它的建構函式，並傳遞指定PDF檔案位置的字串值，來建立代表要新增簽名欄位的PDF檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 新增簽名欄位

   * 使用它的建構函式建立指定簽章欄位位置的`PositionRectangle`物件。 在建構函式中，指定座標值。
   * 如果需要，請建立`FieldMDPOptions`物件，指定將數位簽章套用至簽章欄位時所鎖定的欄位。
   * 透過叫用`SignatureServiceClient`物件的`addSignatureField`方法並傳遞下列值，將簽章欄位新增至PDF檔案：

      * `com.adobe.idp`。 `Document`物件，代表加入簽名欄位的PDF檔案。
      * 字串值，指定簽名欄位的名稱。
      * 代表新增簽名欄位之頁碼的`java.lang.Integer`值。
      * 指定簽章欄位位置的`PositionRectangle`物件。
      * `FieldMDPOptions`物件，指定PDF檔案中在數位簽章套用至簽章欄位後鎖定的欄位。 此引數值是選用的，您可以傳遞`null`。

   * 指定各種執行階段值的`PDFSeedValueOptions`物件。 此引數值是選用的，您可以傳遞`null`。

     `addSignatureField`方法傳回`com.adobe.idp`。 `Document`物件代表包含簽名欄位的PDF檔案。

   >[!NOTE]
   >
   >您可以叫用`SignatureServiceClient`物件的`addInvisibleSignatureField`方法，以新增隱藏的簽章欄位。

1. 將PDF檔案儲存為PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`com.adobe.idp`。 `Document`物件的`copyToFile`方法，以將`Document`物件的內容複製到檔案。 確定您使用`com.adobe.idp`。 `addSignatureField`方法傳回的`Document`物件。

**另請參閱**

[簽名服務API快速啟動](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 使用Web服務API新增簽名欄位 {#add-signature-fields-using-the-web-service-api}

若要使用Signature API （Web服務）新增簽名欄位：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立簽章使用者端

   * 使用預設建構函式建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`SignatureServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得新增簽名欄位的PDF檔案

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存將包含簽章欄位的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表PDF檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派物件的`MTOM`屬性，填入`BLOB`物件。

1. 新增簽名欄位

   呼叫`SignatureServiceClient`物件的`addSignatureField`方法並傳遞下列值，以將簽章欄位新增至PDF檔案：

   * `BLOB`物件，代表加入簽名欄位的PDF檔案。
   * 字串值，指定簽名欄位名稱。
   * 整數值，代表新增簽名欄位的頁碼。
   * 指定簽章欄位位置的`PositionRect`物件。
   * `FieldMDPOptions`物件，指定PDF檔案中在數位簽章套用至簽章欄位後鎖定的欄位。 此引數值是選用的，您可以傳遞`null`。
   * 指定各種執行階段值的`PDFSeedValueOptions`物件。 此引數值是選用的，您可以傳遞`null`。

   `addSignatureField`方法傳回`BLOB`物件，該物件代表包含簽名欄位的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表將包含簽章欄位的PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存`addSignatureField`方法傳回的`BLOB`物件的內容。 取得`BLOB`物件的`binaryData`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 正在擷取簽章欄位名稱 {#retrieving-signature-field-names}

您可以擷取所有簽名欄位的名稱，這些欄位位於您要簽署或認證的PDF檔案中。 如果您不確定PDF檔案中的簽名欄位名稱，或者您想要驗證這些名稱，則可以使用程式擷取它們。 簽章服務傳回簽章欄位的完整名稱，例如`form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

>[!NOTE]
>
>如需有關簽章服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟摘要 {#summary_of_steps-1}

若要擷取簽名欄位名稱，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得包含簽名欄位的PDF檔案。
1. 擷取簽章欄位名稱。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如需關於這些JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽章使用者端**

您必須先建立簽名服務使用者端，才能以程式設計方式執行簽名服務作業。

**取得包含簽章欄位的PDF檔案**

擷取包含簽名欄位的PDF檔案。

**擷取簽章欄位名稱**

擷取包含一或多個簽名欄位的PDF檔案後，即可擷取簽名欄位名稱。

**另請參閱**

[使用Java API擷取簽名欄位名稱](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[使用Web服務API擷取簽名欄位](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API擷取簽名欄位名稱 {#retrieve-signature-field-names-using-the-java-api}

使用簽名API (Java)擷取簽名欄位名稱：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽章使用者端

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`SignatureServiceClient`物件。

1. 取得包含簽名欄位的PDF檔案

   * 使用它的建構函式並傳遞指定PDF檔案位置的字串值，建立代表包含簽名欄位的PDF檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 擷取簽章欄位名稱

   * 叫用`SignatureServiceClient`物件的`getSignatureFieldList`方法，並傳遞包含簽章欄位之PDF檔案的`com.adobe.idp.Document`物件，以擷取簽章欄位名稱。 此方法會傳回`java.util.List`物件，其中每個元素都包含`PDFSignatureField`物件。 使用此物件，您可以取得有關簽名欄位的其他資訊，例如它是否可見。
   * 逐一檢視`java.util.List`物件，以判斷是否有簽章欄位名稱。 對於PDF檔案中的每一個簽章欄位，您可以取得個別的`PDFSignatureField`物件。 若要取得簽章欄位的名稱，請叫用`PDFSignatureField`物件的`getName`方法。 此方法會傳回指定簽名欄位名稱的字串值。

**另請參閱**

[正在擷取簽章欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[快速入門(SOAP模式)：使用Java API擷取簽名欄位名稱](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API擷取簽名欄位 {#retrieve-signature-field-using-the-web-service-api}

使用簽名API （Web服務）擷取簽名欄位名稱：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立簽章使用者端

   * 使用預設建構函式建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`SignatureServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含簽名欄位的PDF檔案

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存包含簽章欄位的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表PDF檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將位元組陣列內容指派給物件的`MTOM`欄位，以填入`BLOB`物件。

1. 擷取簽章欄位名稱

   * 叫用`SignatureServiceClient`物件的`getSignatureFieldList`方法，並傳遞包含簽章欄位之PDF檔案的`BLOB`物件，以擷取簽章欄位名稱。 此方法會傳回`MyArrayOfPDFSignatureField`集合物件，其中每個元素都包含`PDFSignatureField`物件。
   * 逐一檢視`MyArrayOfPDFSignatureField`物件，以判斷是否有簽章欄位名稱。 對於PDF檔案中的每個簽章欄位，您可以取得`PDFSignatureField`物件。 若要取得簽章欄位的名稱，請叫用`PDFSignatureField`物件的`getName`方法。 此方法會傳回指定簽名欄位名稱的字串值。

**另請參閱**

[正在擷取簽章欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改簽章欄位 {#modifying-signature-fields}

您可以使用Java API和Web服務API來修改PDF檔案中的簽名欄位。 修改簽章欄位涉及處理其簽章欄位鎖定字典值或種子值字典值。

*欄位鎖定字典*&#x200B;指定簽署簽章欄位時鎖定的欄位清單。 鎖定的欄位可防止使用者變更欄位。 *種子值字典*&#x200B;包含套用簽章時使用的限制資訊。 例如，您可以變更在不使簽名失效的情況下控制可能發生的動作的許可權。

透過修改現有簽名欄位，您可以變更PDF檔案以反映不斷變化的業務需求。 例如，新業務需求可能需要在簽署檔案後鎖定所有檔案欄位。

本節說明如何透過修改欄位鎖定字典和種子值字典值來修改簽名欄位。 簽名欄位簽署時，對簽名欄位鎖定字典所做的變更會導致PDF檔案中的所有欄位被鎖定。 對種子值字典所做的變更會禁止對檔案進行特定型別的變更。

>[!NOTE]
>
>如需有關簽章服務和修改簽章欄位的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

若要修改PDF檔案中的簽名欄位，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得包含要修改之簽名欄位的PDF檔案。
1. 設定字典值。
1. 修改簽章欄位。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如需關於這些JAR檔案位置的資訊，請參閱[包含LiveCycleJava程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽章使用者端**

您必須先建立簽名服務使用者端，才能以程式設計方式執行簽名服務作業。

**取得包含要修改之簽章欄位的PDF檔案**

擷取包含要修改之簽名欄位的PDF檔案。

**設定字典值**

若要修改簽章欄位，請將值指派給其欄位鎖定字典或種子值字典。 指定簽章欄位鎖定字典值涉及指定簽章欄位簽署時鎖定的PDF檔案欄位。 （本節將討論如何鎖定所有欄位。）

可以設定以下種子值字典值：

* **修訂檢查**：指定簽章套用至簽章欄位時，是否執行撤銷檢查。
* **憑證選項**：指派值給憑證種子值字典。 在指定憑證選項之前，建議您先熟悉憑證種子值字典。 (請參閱[PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。)
* **摘要選項**：指派用於簽署的摘要演演算法。 有效值為SHA1、SHA256、SHA384、SHA512和RIPEMD160。
* **篩選器**：指定用於簽章欄位的篩選器。 例如，您可以使用Adobe.PPKLite篩選器。 (請參閱[PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。)
* **標幟選項**：指定與此簽章欄位關聯的標幟值。 值1表示簽署者必須僅使用專案的指定值。 值為0表示允許使用其他值。 以下是Bit位置：

   * **1（篩選器）：**&#x200B;用來簽署簽章欄位的簽章處理常式
   * **2 (SubFilter)：**&#x200B;表示簽署時可使用的編碼之名稱陣列
   * **3 (V)**：簽章處理常式簽署簽章欄位所需的最低版本號碼
   * **4 （原因）：**&#x200B;指定簽署檔案可能原因的字串陣列
   * **5 (PDFLegalWarnings)：**&#x200B;指定可能合法證明的字串陣列

* **法律證明**：當檔案通過認證時，會自動掃描特定型別的內容，使檔案的可見內容模糊或誤導。 例如，註解可能會模糊文字，而這些文字對於瞭解認證內容非常重要。 掃描程式會產生警告，指出此型別的內容是否存在。 此外，也為可能產生警告的內容提供額外說明。
* **許可權**：指定可在PDF檔案上使用而不使簽章失效的許可權。
* **原因**：指定必須簽署此檔案的原因。
* **時間戳記**：指定時間戳記選項。 例如，您可以設定所使用之時間戳記伺服器的URL。
* **版本**：指定要用來簽署簽章欄位的簽章處理常式的最小版本號碼。

**修改簽章欄位**

建立「簽名」服務使用者端、擷取包含要修改之簽名欄位的PDF檔案，以及設定說明值之後，您可以指示「簽名」服務修改簽名欄位。 接著，Signature服務會傳回包含修改過之簽名欄位的PDF檔案。 原始PDF檔案不受影響。

**將PDF檔案儲存為PDF檔案**

將包含已修改簽名欄位的PDF檔案儲存為PDF檔案，以便使用者可以在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[簽名服務API快速啟動](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API修改簽名欄位 {#modify-signature-fields-using-the-java-api}

使用簽名API (Java)修改簽名欄位：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽章使用者端

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`SignatureServiceClient`物件。

1. 取得包含要修改之簽名欄位的PDF檔案

   * 建立`java.io.FileInputStream`物件，代表包含要修改之簽章欄位的PDF檔案，方法是使用其建構函式，並傳遞指定PDF檔案位置的字串值。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定字典值

   * 使用物件的建構函式建立`PDFSignatureFieldProperties`物件。 `PDFSignatureFieldProperties`物件儲存簽章欄位鎖定字典和種子值字典資訊。
   * 使用物件的建構函式建立`PDFSeedValueOptionSpec`物件。 此物件可讓您設定種子值字典值。
   * 叫用`PDFSeedValueOptionSpec`物件的`setMdpValue`方法並傳遞`MDPPermissions.NoChanges`列舉值，不允許變更PDF檔案。
   * 使用物件的建構函式建立`FieldMDPOptionSpec`物件。 此物件可讓您設定簽章欄位鎖定字典值。
   * 呼叫`FieldMDPOptionSpec`物件的`setMdpValue`方法並傳遞`FieldMDPAction.ALL`列舉值，以鎖定PDF檔案中的所有欄位。
   * 透過叫用`PDFSignatureFieldProperties`物件的`setSeedValue`方法並傳遞`PDFSeedValueOptionSpec`物件來設定種子值字典資訊。
   * 透過叫用`PDFSignatureFieldProperties`物件的`setFieldMDP`方法並傳遞`FieldMDPOptionSpec`物件來設定簽章欄位鎖定字典資訊。

   >[!NOTE]
   >
   >若要檢視所有可設定的種子值字典值，請參閱`PDFSeedValueOptionSpec`類別參考。 (請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

1. 修改簽章欄位

   呼叫`SignatureServiceClient`物件的`modifySignatureField`方法並傳遞下列值，以修改簽章欄位：

   * 儲存包含要修改之簽章欄位的PDF檔案的`com.adobe.idp.Document`物件
   * 字串值，指定簽名欄位的名稱
   * 儲存簽章欄位鎖定字典和種子值字典資訊的`PDFSignatureFieldProperties`物件

   `modifySignatureField`方法傳回`com.adobe.idp.Document`物件，該物件儲存包含修改簽名欄位的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案。 請確定您使用的是`modifySignatureField`方法傳回的`com.adobe.idp.Document`物件。

### 使用Web服務API修改簽名欄位 {#modify-signature-fields-using-the-web-service-api}

使用簽名API （Web服務）修改簽名欄位：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立簽章使用者端

   * 使用預設建構函式建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`SignatureServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含要修改之簽名欄位的PDF檔案

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存包含要修改之簽章欄位的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表PDF檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將物件的`MTOM`屬性指派給位元組陣列的內容，以填入`BLOB`物件。

1. 設定字典值

   * 使用物件的建構函式建立`PDFSignatureFieldProperties`物件。 此物件儲存簽章欄位鎖定字典和種子值字典資訊。
   * 使用物件的建構函式建立`PDFSeedValueOptionSpec`物件。 此物件可讓您設定種子值字典值。
   * 將`MDPPermissions.NoChanges`列舉值指派給`PDFSeedValueOptionSpec`物件的`mdpValue`資料成員，不允許變更PDF檔案。
   * 使用物件的建構函式建立`FieldMDPOptionSpec`物件。 此物件可讓您設定簽章欄位鎖定字典值。
   * 將`FieldMDPAction.ALL`列舉值指派給`FieldMDPOptionSpec`物件的`mdpValue`資料成員，以鎖定PDF檔案中的所有欄位。
   * 將`PDFSeedValueOptionSpec`物件指派給`PDFSignatureFieldProperties`物件的`seedValue`資料成員，以設定種子值字典資訊。
   * 將`FieldMDPOptionSpec`物件指派給`PDFSignatureFieldProperties`物件的`fieldMDP`資料成員，以設定簽章欄位鎖定字典資訊。

   >[!NOTE]
   >
   >若要檢視所有可設定的種子值字典值，請參閱`PDFSeedValueOptionSpec`類別參考。 (請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 修改簽章欄位

   呼叫`SignatureServiceClient`物件的`modifySignatureField`方法並傳遞下列值，以修改簽章欄位：

   * 儲存包含要修改之簽章欄位的PDF檔案的`BLOB`物件
   * 字串值，指定簽名欄位的名稱
   * 儲存簽章欄位鎖定字典和種子值字典資訊的`PDFSignatureFieldProperties`物件

   `modifySignatureField`方法傳回`BLOB`物件，該物件儲存包含修改簽名欄位的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立`System.IO.FileStream`物件，方法是叫用其建構函式，並傳遞代表將包含簽章欄位之PDF檔案的檔案位置的字串值，以及開啟檔案的模式。
   * 建立位元組陣列，儲存`addSignatureField`方法傳回的`BLOB`物件內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數位簽署PDF檔案 {#digitally-signing-pdf-documents}

數位簽章可套用至PDF檔案，以提供安全等級。 數位簽章（例如手寫簽章）提供簽署者識別自己及就檔案發表宣告的方法。 用於數位簽署檔案的技術有助於確保簽署者和收件者都清楚已簽署的內容，並且確信檔案在簽署後未曾變更。

PDF檔案是以公開金鑰技術簽署。 簽署者有兩個金鑰：公開金鑰和私密金鑰。 私密金鑰會儲存在使用者的認證中，在簽署時必須可供使用。 公開金鑰儲存在使用者的憑證中，收件人必須可以使用它來驗證簽名。 憑證撤銷清單(CRL)和由憑證授權單位(CA)發佈的線上憑證狀態通訊協定(OCSP)回應中，可提供撤銷憑證的相關資訊。 簽署時間可從信任的來源（稱為時間戳記授權單位）取得。

>[!NOTE]
>
>您必須確定將憑證新增到AEM Forms，才能數位簽署PDF檔案。 使用管理控制檯或以程式設計方式使用信任管理員API新增憑證。 （請參閱[使用信任管理員API匯入認證](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。）

您可以用程式設計方式對PDF檔案進行數位簽署。 數位簽署PDF檔案時，您必須參考AEM Forms中存在的保全性認證。 認證是用於簽署的私密金鑰。

簽章服務會在簽署PDF檔案時執行下列步驟：

1. 簽章服務會傳遞要求中指定的別名，從信任存放區擷取認證。
1. 信任庫會搜尋指定的認證。
1. 認證會傳回至簽章服務，並用來簽署檔案。 也會針對別名快取認證，以供日後請求使用。

如需有關處理安全性認證的資訊，請參閱應用程式伺服器的&#x200B;*安裝和部署AEM Forms*&#x200B;指南。

>[!NOTE]
>
>簽署和認證檔案之間存在差異。 (請參閱[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)。)

>[!NOTE]
>
>並非所有PDF檔案都支援簽署。 如需有關簽章服務和數位簽署檔案的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>簽章服務不支援內嵌PDF資料的XDP檔案做為作業的輸入，例如憑證檔案。 此動作會導致簽章服務擲回`PDFOperationException`。 若要解決此問題，請使用PDF公用程式服務，將XDP檔案轉換為PDF檔案，然後將轉換的PDF檔案傳遞至簽名服務作業。 (請參閱[使用PDF公用程式](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)。)

**nCipher nShield HSM認證**

使用nCipher nShield HSM認證簽署或認證PDF檔案時，必須重新啟動AEM Forms部署所在的J2EE應用程式伺服器，才能使用新的認證。 不過，您可以設定組態值，讓簽署或認證作業正常運作，而不需重新啟動J2EE應用程式伺服器。

您可以在位於/opt/nfast/cknfastrc （或c：\nfast\cknfastrc）的cknfastrc檔案中新增下列組態值：

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將這個組態值新增至cknfastrc檔案之後，便可以使用新的認證而不需重新啟動J2EE應用程式伺服器。

    >[！NOTE]
    >
    >建議使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

**簽章不受信任**

在認證和簽署相同的PDF檔案時，如果認證簽名不受信任，則在Acrobat或Adobe Reader中開啟PDF檔案時，第一個簽名旁邊會出現一個黃色三角形。 必須信任憑證簽章以避免這種情況。

**簽署以XFA為基礎的表單**

如果您嘗試使用簽章服務API簽署以XFA為基礎的表單，Acrobat中的`View` `Signed` `Version`可能遺漏資料。 例如，請考量下列工作流程：

* 使用Designer建立的XDP檔案，合併包含簽名欄位的表單設計以及包含表單資料的XML資料。 您可以使用Forms服務產生互動式PDF檔案。
* 您使用簽名服務API簽署PDF檔案。

### 步驟摘要 {#summary_of_steps-3}

若要數位簽署PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章服務使用者端。
1. 取得要簽署的PDF檔案。
1. 簽署PDF檔案。
1. 將已簽署的PDF檔案儲存為PDF檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立簽章使用者端**

您必須先建立簽名服務使用者端，才能以程式設計方式執行簽名服務作業。

**取得PDF檔案以簽署**

若要簽署PDF檔案，您必須取得包含簽名欄位的PDF檔案。 如果PDF檔案不包含簽名欄位，則無法簽署。 可使用Designer或以程式設計方式新增簽名欄位。

**簽署PDF檔案**

簽署PDF檔案時，您可以設定簽名服務使用的執行階段選項。 您可以設定下列選項：

* 外觀選項
* 撤銷檢查
* 時間戳記值

您使用`PDFSignatureAppearanceOptionSpec`物件來設定外觀選項。 例如，您可以叫用`PDFSignatureAppearanceOptionSpec`物件的`setShowDate`方法並傳遞`true`，在簽章中顯示日期。

您也可以指定是否要執行撤銷檢查，以判斷用於數位簽署PDF檔案的憑證是否已撤銷。 若要執行撤銷檢查，您可以指定下列其中一個值：

* **NoCheck**：不執行撤銷檢查。
* **BestEffort**：一律嘗試檢查鏈結中所有憑證的撤銷。 如果檢查時發生任何問題，系統就會將撤銷視為有效。 如果發生任何失敗，則假設未撤銷憑證。
* **CheckIfAvailable：**&#x200B;如果撤銷資訊可用，請檢查鏈結中所有憑證的撤銷。 如果檢查時發生任何問題，系統就會將撤銷視為無效。 如果發生任何失敗，假設憑證被撤銷且無效。 （這是預設值。）
* **AlwaysCheck**：檢查鏈結中所有憑證的撤銷。 如果任何憑證中都沒有撤銷資訊，則會假設撤銷無效。

若要對憑證執行撤銷檢查，您可以使用`CRLOptionSpec`物件來指定憑證撤銷清單(CRL)伺服器的URL。 不過，如果您要執行撤銷檢查但未指定CRL伺服器的URL，則簽章服務會從憑證取得該URL。

執行撤銷檢查時，您可以使用線上憑證狀態通訊協定(OCSP)伺服器，而不使用CRL伺服器。 通常在使用OCSP伺服器而非CRL伺服器時，撤銷檢查的執行速度會更快。 (請參閱[https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560)上的「線上憑證狀態通訊協定」。)

您可以使用Adobe應用程式和服務來設定Signature服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是先在Adobe應用程式和服務中設定，則會檢查OCSP伺服器，然後檢查CRL伺服器。 （請參閱AAC說明中的「使用信任存放區管理憑證和認證」）。

如果您指定不執行撤銷檢查，則簽名服務不會檢查用於簽署或證明檔案的憑證是否已撤銷。 也就是說，會忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>雖然可以在憑證中指定CRL或OCSP伺服器，但您可以使用`CRLOptionSpec`和`OCSPOptionSpec`物件來覆寫憑證中指定的URL。 例如，若要覆寫CRL伺服器，您可以叫用`CRLOptionSpec`物件的`setLocalURI`方法。

時間戳記是指追蹤已簽署或已驗證檔案修改時間的程式。 檔案一旦簽署，即不應修改，即使檔案擁有者亦然。 時間戳記有助於加強已簽署或已驗證檔案的有效性。 您可以使用`TSPOptionSpec`物件來設定時間戳記選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務逐步瀏覽區段及對應的快速啟動中，會使用撤銷檢查。 因為未指定CRL或OCSP伺服器資訊，所以伺服器資訊會從用來數位簽署PDF檔案的憑證取得。

若要成功簽署PDF檔案，您可以指定包含數位簽章之簽章欄位的完整名稱，例如`form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，也可以使用簽章欄位的部分名稱： `SignatureField3[3]`。

您也必須參考安全性認證，才能數位簽署PDF檔案。 若要參照安全性認證，請指定別名。 別名是實際認證的參考，可能位於PKCS#12檔案（具有.pfx副檔名）或硬體安全模組(HSM)中。 如需安全性認證的相關資訊，請參閱應用程式伺服器的&#x200B;*安裝和部署AEM Forms*&#x200B;指南。

**儲存已簽署的PDF檔案**

簽名服務以數位方式簽署PDF檔案後，您可以將檔案儲存為PDF檔案，讓使用者在Acrobat或Adobe Reader中開啟檔案。

**另請參閱**

[使用Java API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[使用Web服務API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

[正在擷取簽章欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### 使用Java API數位簽署PDF檔案 {#digitally-sign-pdf-documents-using-the-java-api}

使用簽名API (Java)以數位方式簽署PDF檔案：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名使用者端

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`SignatureServiceClient`物件。

1. 取得要簽署的PDF檔案

   * 建立一個`java.io.FileInputStream`物件，代表要以數位方式簽署的PDF檔案，使用它的建構函式並傳遞一個字串值來指定PDF檔案的位置。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 簽署PDF檔案

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值以簽署PDF檔案：

   * 代表要簽署的PDF檔案的`com.adobe.idp.Document`物件。
   * 字串值，代表將包含數位簽章之簽章欄位的名稱。
   * `Credential`物件，代表用於數位簽署PDF檔案的認證。 呼叫`Credential`物件的靜態`getInstance`方法，並傳遞字串值（指定與安全性認證對應的別名值），以建立`Credential`物件。
   * `HashAlgorithm`物件，指定代表用來摘要PDF檔案的雜湊演演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演演算法。
   * 字串值，代表PDF檔案經過數位簽署的原因。
   * 代表簽署者聯絡資訊的字串值。
   * 控制數位簽章外觀的`PDFSignatureAppearanceOptions`物件。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * `java.lang.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。
   * 儲存線上憑證狀態通訊協定(OCSP)支援之偏好設定的`OCSPOptionSpec`物件。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。
   * 儲存憑證撤銷清單(CRL)偏好設定的`CRLPreferences`物件。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。
   * 儲存時間戳記提供者(TSP)支援之偏好設定的`TSPPreferences`物件。 此引數是選用的，可以是`null`。 如需詳細資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

   `sign`方法傳回代表已簽署PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存已簽署的PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`以將`Document`物件的內容複製到檔案。 確定您使用的是`sign`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[快速入門(SOAP模式)：使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API數位簽署PDF檔案 {#digitally-signing-pdf-documents-using-the-web-service-api}

若要使用Signature API （Web服務）數位簽署PDF檔案：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立簽名使用者端

   * 使用預設建構函式建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`SignatureServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得要簽署的PDF檔案

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存已簽署的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表要簽署之PDF檔案的檔案位置，以及開啟檔案的模式之字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將物件的`MTOM`屬性指派給位元組陣列的內容，以填入`BLOB`物件。

1. 簽署PDF檔案

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值以簽署PDF檔案：

   * 代表要簽署的PDF檔案的`BLOB`物件。
   * 字串值，代表將包含數位簽章之簽章欄位的名稱。
   * `Credential`物件，代表用於數位簽署PDF檔案的認證。 使用物件的建構函式建立`Credential`物件，並指定別名給`Credential`物件的`alias`屬性。
   * `HashAlgorithm`物件，指定代表用來摘要PDF檔案的雜湊演演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演演算法。
   * Boolean值，指定是否使用雜湊演演算法。
   * 字串值，代表PDF檔案經過數位簽署的原因。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * 控制數位簽章外觀的`PDFSignatureAppearanceOptions`物件。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * `System.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。 若完成此撤銷檢查，則會內嵌於簽章中。 預設為 `false`。
   * 儲存線上憑證狀態通訊協定(OCSP)支援之偏好設定的`OCSPOptionSpec`物件。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。 如需此物件的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 儲存憑證撤銷清單(CRL)偏好設定的`CRLPreferences`物件。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。
   * 儲存時間戳記提供者(TSP)支援之偏好設定的`TSPPreferences`物件。 此引數是選用的，可以是`null`。

   `sign`方法傳回代表已簽署PDF檔案的`BLOB`物件。

1. 儲存已簽署的PDF檔案

   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表已簽署PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存`sign`方法傳回的`BLOB`物件的內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數位簽署互動式Forms {#digitally-signing-interactive-forms}

您可以簽署Forms服務建立的互動式表單。 例如，請考量下列工作流程：

* 您可以使用Forms服務，在XML檔案中合併使用Designer建立的XFAPDF表單和表單資料。 Forms伺服器會呈現互動式表單。
* 您可以使用Signature service API簽署互動式表單。

結果會產生數位簽署的互動式PDF表單。 在簽署以XFA表單為基礎的PDF表單時，請確定您將PDF檔案儲存為Adobe靜態PDF表單。 如果您嘗試簽署儲存為「PDF動態PDF」表單的Adobe表單，會發生例外狀況。 由於您簽署的是從Forms服務傳回的表單，因此請確定表單包含簽名欄位。

>[!NOTE]
>
>您必須確定將憑證新增至AEM Forms，才能數位簽署互動式表單。 使用管理控制檯或以程式設計方式使用信任管理員API新增憑證。 （請參閱[使用信任管理員API匯入認證](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。）

使用Forms服務API時，將`GenerateServerAppearance`執行階段選項設定為`true`。 此執行階段選項可確保伺服器上產生的表單外觀，在Acrobat或Adobe Reader中開啟時仍然有效。 產生互動式表單以使用Forms API簽署時，建議您設定此執行階段選項。

>[!NOTE]
>
>閱讀「數位簽署互動式Forms」前，建議您先熟悉簽署PDF檔案。 (請參閱[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)

### 步驟摘要 {#summary_of_steps-4}

若要以數位方式簽署Forms服務傳回的互動式表單，請執行以下工作：

1. 包含專案檔案。
1. 建立Forms和簽名使用者端。
1. 使用Forms服務取得互動式表單。
1. 簽署互動式表單。
1. 將已簽署的PDF檔案儲存為PDF檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如需關於這些JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立Forms和簽章使用者端**

由於此工作流程會同時叫用Forms和簽名服務，因此請建立Forms服務使用者端和簽名服務使用者端。

**使用Forms服務取得互動式表單**

您可以使用Forms服務來取得要簽署的互動式PDF表單。 自AEM Forms起，您可以將`com.adobe.idp.Document`物件傳遞至包含要轉譯之表單的Forms服務。 這個方法的名稱為`renderPDFForm2`。 此方法傳回包含要簽署的表單的`com.adobe.idp.Document`物件。 您可以將此`com.adobe.idp.Document`執行個體傳遞至簽章服務。

同樣地，如果您使用Web服務，您可以傳遞Forms服務傳回至簽名服務的`BLOB`執行個體。

>[!NOTE]
>
>與數位簽署互動式Forms區段相關的快速入門會叫用`renderPDFForm2`方法。

**簽署互動式表單**

簽署PDF檔案時，您可以設定Signature service使用的執行階段選項。 您可以設定下列選項：

* 外觀選項
* 撤銷檢查
* 時間戳記值

您使用`PDFSignatureAppearanceOptionSpec`物件來設定外觀選項。 例如，您可以叫用`PDFSignatureAppearanceOptionSpec`物件的`setShowDate`方法並傳遞`true`，在簽章中顯示日期。

**儲存已簽署的PDF檔案**

簽章服務以數位方式簽署PDF檔案後，您可以將其儲存為PDF檔案。 PDF檔案可在Acrobat或Adobe Reader中開啟。

**另請參閱**

[使用Java API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[使用網站服務API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[呈現互動式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### 使用Java API數位簽署互動式表單 {#digitally-sign-an-interactive-form-using-the-java-api}

使用Forms和簽名API (Java)數位簽署互動式表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar和adobe-forms-client.jar。

1. 建立Forms和簽名使用者端

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`SignatureServiceClient`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`FormsServiceClient`物件。

1. 使用Forms服務取得互動式表單

   * 使用建構函式建立代表PDF檔案以傳遞至Forms服務的`java.io.FileInputStream`物件。 傳遞字串值，指定PDF檔案的位置。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。
   * 建立一個`java.io.FileInputStream`物件，代表包含表單資料的XML檔案，以使用它的建構函式傳遞至Forms服務。 傳遞指定XML檔案位置的字串值。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。
   * 建立用來設定執行階段選項的`PDFFormRenderSpec`物件。 叫用`PDFFormRenderSpec`物件的`setGenerateServerAppearance`方法並傳遞`true`。
   * 叫用`FormsServiceClient`物件的`renderPDFForm2`方法，並傳遞下列值：

      * 包含要轉譯之PDF表單的`com.adobe.idp.Document`物件。
      * 包含要與表單合併之資料的`com.adobe.idp.Document`物件。
      * 儲存執行階段選項的`PDFFormRenderSpec`物件。
      * 包含Forms服務所需URI值的`URLSpec`物件。 您可以為此引數值指定`null`。
      * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。

     `renderPDFForm2`方法傳回包含表單資料流的`FormsResult`物件

   * 透過叫用`FormsResult`物件的`getOutputContent`方法擷取PDF表單。 此方法會傳回代表互動式表單的`com.adobe.idp.Document`物件。

1. 簽署互動式表單

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值以簽署PDF檔案：

   * 代表要簽署的PDF檔案的`com.adobe.idp.Document`物件。 確定此物件是從Forms服務取得的`com.adobe.idp.Document`物件。
   * 代表已簽署之簽名欄位名稱的字串值。
   * `Credential`物件，代表用於數位簽署PDF檔案的認證。 呼叫`Credential`物件的靜態`getInstance`方法，以建立`Credential`物件。 傳遞字串值，指定與安全性認證對應的別名值。
   * `HashAlgorithm`物件，指定代表用來摘要PDF檔案的雜湊演演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演演算法。
   * 字串值，代表PDF檔案經過數位簽署的原因。
   * 代表簽署者聯絡資訊的字串值。
   * 控制數位簽章外觀的`PDFSignatureAppearanceOptions`物件。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * `java.lang.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。
   * 儲存線上憑證狀態通訊協定(OCSP)支援之偏好設定的`OCSPPreferences`物件。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。
   * 儲存憑證撤銷清單(CRL)偏好設定的`CRLPreferences`物件。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。
   * 儲存時間戳記提供者(TSP)支援之偏好設定的`TSPPreferences`物件。 此引數是選用的，可以是`null`。

   `sign`方法傳回代表已簽署PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存已簽署的PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`以將`Document`物件的內容複製到檔案。 請確定您使用的是`sign`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[數位簽署互動式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[快速入門(SOAP模式)：使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API數位簽署互動式表單 {#digitally-sign-an-interactive-form-using-the-web-service-api}

使用Forms和簽名API （Web服務）數位簽署互動式表單：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 由於此使用者端應用程式會叫用兩個AEM Forms服務，請建立兩個服務參考。 使用下列WSDL定義作為與Signature服務關聯的服務參考： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   使用下列WSDL定義作為與Forms服務相關聯的服務參考： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   因為`BLOB`資料型別是兩個服務參考的共同型別，使用它時，請完全限定`BLOB`資料型別。 在對應的Web服務快速入門中，所有`BLOB`執行個體都是完全合格的。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Forms和簽名使用者端

   * 使用預設建構函式建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`SignatureServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >對Forms服務使用者端重複這些步驟。

1. 使用Forms服務取得互動式表單

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存已簽署的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表要簽署之PDF檔案的檔案位置，以及開啟檔案的模式之字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將物件的`MTOM`屬性指派給位元組陣列的內容，以填入`BLOB`物件。
   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存表單資料。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表包含表單資料之XML檔案的檔案位置，以及開啟檔案的模式。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將物件的`MTOM`屬性指派給位元組陣列的內容，以填入`BLOB`物件。
   * 建立用來設定執行階段選項的`PDFFormRenderSpec`物件。 將值`true`指派給`PDFFormRenderSpec`物件的`generateServerAppearance`欄位。
   * 叫用`FormsServiceClient`物件的`renderPDFForm2`方法，並傳遞下列值：

      * 包含要轉譯之PDF表單的`BLOB`物件。
      * 包含要與表單合併之資料的`BLOB`物件。
      * 儲存執行階段選項的`PDFFormRenderSpec`物件。
      * 包含Forms服務所需URI值的`URLSpec`物件。 您可以為此引數值指定`null`。
      * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。
      * 用來儲存表單頁數的長輸出引數。
      * 用於地區設定值的字串輸出引數。
      * `FormResult`值是用來儲存互動式表單的輸出引數。

   * 叫用`FormsResult`物件的`outputContent`欄位以擷取PDF表單。 此欄位儲存代表互動式表單的`BLOB`物件。

1. 簽署互動式表單

   叫用`SignatureServiceClient`物件的`sign`方法並傳遞下列值以簽署PDF檔案：

   * 代表要簽署的PDF檔案的`BLOB`物件。 使用Forms服務傳回的`BLOB`執行個體。
   * 代表已簽署之簽名欄位名稱的字串值。
   * `Credential`物件，代表用於數位簽署PDF檔案的認證。 使用物件的建構函式建立`Credential`物件，並指定別名給`Credential`物件的`alias`屬性。
   * `HashAlgorithm`物件，指定代表用來摘要PDF檔案的雜湊演演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演演算法。
   * Boolean值，指定是否使用雜湊演演算法。
   * 字串值，代表PDF檔案經過數位簽署的原因。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * 控制數位簽章外觀的`PDFSignatureAppearanceOptions`物件。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * `System.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。 若完成此撤銷檢查，則會內嵌於簽章中。 預設為 `false`。
   * 儲存線上憑證狀態通訊協定(OCSP)支援之偏好設定的`OCSPPreferences`物件。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。 如需此物件的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 儲存憑證撤銷清單(CRL)偏好設定的`CRLPreferences`物件。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。
   * 儲存時間戳記提供者(TSP)支援之偏好設定的`TSPPreferences`物件。 此引數是選用的，可以是`null`。

   `sign`方法傳回代表已簽署PDF檔案的`BLOB`物件。

1. 儲存已簽署的PDF檔案

   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表已簽署PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存`sign`方法傳回的`BLOB`物件的內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[數位簽署互動式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 認證PDF檔案 {#certifying-pdf-documents}

您可以使用稱為認證簽名的特定簽名型別來認證PDF檔案，以保護檔案安全。 認證簽名與數位簽名的區別如下：

* 它必須是套用至PDF檔案的第一個簽章；也就是說，在套用已驗證簽章時，檔案中的任何其他簽章欄位都必須未簽署。 PDF檔案中只允許一個認證簽章。 如果您要簽署和認證PDF檔案，則必須在簽署之前進行認證。 在認證PDF檔案後，您可以數位簽署其他簽名欄位。
* 檔案的作者或建立者可以指定檔案可以某些方式修改，而不會使認證的簽名失效。 例如，檔案可能允許填寫表格或加上註解。 如果作者指定不允許特定修改，Acrobat會限制使用者不得以這種方式修改檔案。 如果已進行此類修改（例如使用其他應用程式），則認證簽名無效，Acrobat會在使用者開啟檔案時發出警告。 （若為未驗證的簽章，則不會防止修改，且一般的編輯作業不會使原始簽章失效。）
* 簽署時，會掃描檔案是否有特定型別的內容，可能會使檔案的內容含糊或產生誤導。 例如，註解可能會遮蔽頁面上的一些文字，而這些文字對於瞭解正在認證的內容非常重要。 可提供此類內容的說明（法律證明）。

您可以使用簽名服務Java API或簽名Web服務API，以程式設計方式認證PDF檔案。 在認證PDF檔案時，您必須參考「認證」服務中存在的安全性認證。 如需安全性認證的相關資訊，請參閱應用程式伺服器的&#x200B;*安裝和部署AEM Forms*&#x200B;指南。

>[!NOTE]
>
>當認證和簽署相同的PDF檔案時，如果認證簽名不受信任，當您在Acrobat或Adobe Reader中開啟PDF檔案時，第一個簽名簽名旁邊會出現一個黃色三角形。 必須信任憑證簽章以避免這種情況。

>[!NOTE]
>
>使用nCipher nShield HSM認證簽署或認證PDF檔案時，必須重新啟動部署AEM Forms的J2EE應用程式伺服器，才能使用新的認證。 不過，您可以設定組態值，讓簽署或認證作業正常運作，而不需重新啟動J2EE應用程式伺服器。

您可以在位於/opt/nfast/cknfastrc （或c：\nfast\cknfastrc）的cknfastrc檔案中新增下列組態值：

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將這個組態值新增至cknfastrc檔案之後，便可以使用新的認證而不需重新啟動J2EE應用程式伺服器。

>[!NOTE]
>
>如需有關簽章服務與認證檔案的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

若要認證PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得要認證的PDF檔案。
1. 認證PDF檔案。
1. 將認證的PDF檔案儲存為PDF檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如需關於這些JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽章使用者端**

您必須先建立簽名使用者端，才能以程式設計方式執行簽名作業。

**取得PDF檔案以認證**

若要認證PDF檔案，您必須取得包含簽名欄位的PDF檔案。 如果PDF檔案不包含簽名欄位，則無法認證該檔案。 可使用Designer或以程式設計方式新增簽名欄位。 如需以程式設計方式新增簽名欄位的資訊，請參閱[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。

**認證PDF檔案**

若要成功認證PDF檔案，您需要以下供簽名服務用來認證PDF檔案的輸入值：

* **PDF檔案**：包含簽章欄位的PDF檔案，此表單欄位包含已驗證簽章的圖形表示。 PDF檔案必須包含簽名欄位，才能加以認證。 可使用Designer或以程式設計方式新增簽名欄位。 （請參閱[新增簽章欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。）
* **簽章欄位名稱**：已驗證的簽章欄位的完整名稱。 下列值為範例： `form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，也可以使用簽章欄位的部分名稱： `SignatureField3[3]`。 如果為欄位名稱傳遞null值，則會動態建立並認證不可見的簽章欄位。
* **安全性認證**：用於認證PDF檔案的認證。 此安全性認證包含密碼和別名，必須與Credential服務內認證中顯示的別名相符。 別名是實際認證的參考，可能位於PKCS#12檔案（具有.pfx副檔名）或硬體安全模組(HSM)中。
* **雜湊演演算法**：用於摘要PDF檔案的雜湊演演算法。
* **簽署原因**：顯示在Acrobat或Adobe Reader中的值，讓其他使用者知道PDF檔案經過認證的原因。
* **簽署者的位置**：認證所指定的簽署者位置。
* **連絡資訊**：簽署者的連絡資訊，例如地址和電話號碼。
* **許可權資訊**：控制一般使用者可以在檔案上執行的動作，而不會造成認證簽名無效的許可權。 例如，您可以設定許可權，這樣對PDF檔案所做的任何變更都會導致認證簽名無效。
* **法律說明**：當檔案通過認證時，會自動掃描特定型別的內容，使檔案內容模糊或誤導。 例如，註解可能會遮蔽頁面上的一些文字，而這些文字對於瞭解正在認證的內容非常重要。 掃描程式會產生有關這些內容型別的警告。 此值提供可能產生警告之內容的額外說明。
* **外觀選項**：控制認證簽章外觀的選項。 例如，已驗證的簽章可以顯示日期資訊。
* **撤銷檢查**：此值指定是否對簽署者的憑證執行撤銷檢查。 `false`的預設設定表示未完成撤銷檢查。
* **OCSP設定**： Online Certificate Status Protocol (OCSP)支援的設定，提供認證PDF檔案所使用的認證狀態相關資訊。 例如，您可以指定伺服器的URL，以提供您用來登入PDF檔案的認證相關資訊。
* **CRL設定**：憑證撤銷清單(CRL)偏好設定的設定（如果已完成撤銷檢查）。 例如，您可以指定一律檢查認證是否被撤銷。
* **時間戳記**：定義套用至已驗證簽章之時間戳記資訊的設定。 時間戳記表示特定資料是在特定時間之前建立的。 此知識有助於在簽署者和驗證者之間建立信任關係。

**將認證的PDF檔案儲存為PDF檔案**

簽名服務驗證PDF檔案後，您可以將它儲存為PDF檔案，以便使用者在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[使用Java API認證PDF檔案](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[使用網站服務API認證PDF檔案](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API認證PDF檔案 {#certify-pdf-documents-using-the-java-api}

使用簽名API (Java)認證PDF檔案：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽章使用者端

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`SignatureServiceClient`物件。

1. 取得PDF檔案以認證

   * 建立代表要認證之PDF檔案的`java.io.FileInputStream`物件，方法是使用其建構函式，並傳遞指定PDF檔案位置的字串值。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 認證PDF檔案

   透過叫用`SignatureServiceClient`物件的`certify`方法並傳遞下列值來認證PDF檔案：

   * 代表要認證之PDF檔案的`com.adobe.idp.Document`物件。
   * 字串值，代表將包含簽章之簽章欄位的名稱。
   * `Credential`物件，代表用來認證PDF檔案的認證。 呼叫`Credential`物件的靜態`getInstance`方法，並傳遞字串值（指定與安全性認證對應的別名值），以建立`Credential`物件。
   * `HashAlgorithm`物件，指定代表用於摘要PDF檔案的雜湊演演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演演算法。
   * 代表驗證PDF檔案之原因的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * `MDPPermissions`物件，指定可在使簽章失效的PDF檔案上執行的動作。
   * 控制認證簽章外觀的`PDFSignatureAppearanceOptions`物件。 如有需要，請叫用方法（例如`setShowDate`）來修改簽章的外觀。
   * 字串值，說明哪些動作會使簽章失效。
   * `java.lang.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。 若完成此撤銷檢查，則會內嵌於簽章中。 預設為 `false`。
   * 指定正在認證的簽章欄位是否已鎖定的`java.lang.Boolean`物件。 如果欄位已鎖定，則簽章欄位會標示為唯讀，其屬性無法修改，且沒有必要許可權的任何人都無法清除。 預設為 `false`。
   * 儲存線上憑證狀態通訊協定(OCSP)支援之偏好設定的`OCSPPreferences`物件。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。 如需此物件的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 儲存憑證撤銷清單(CRL)偏好設定的`CRLPreferences`物件。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。
   * 儲存時間戳記提供者(TSP)支援之偏好設定的`TSPPreferences`物件。 例如，在您建立`TSPPreferences`物件後，可以叫用`TSPPreferences`物件的`setTspServerURL`方法來設定TSP伺服器的URL。 此引數是選用的，可以是`null`。 如需詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

   `certify`方法傳回代表認證PDF檔案的`com.adobe.idp.Document`物件。

1. 將認證的PDF檔案儲存為PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案。

**另請參閱**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[快速入門(SOAP模式)：使用Java API認證PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API認證PDF檔案 {#certify-pdf-documents-using-the-web-service-api}

使用簽名API （Web服務）認證PDF檔案：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立簽章使用者端

   * 使用預設建構函式建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`SignatureServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得PDF檔案以認證

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存已認證的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表要認證之PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將其`MTOM`資料成員指派給位元組陣列的內容，以填入`BLOB`物件。

1. 認證PDF檔案

   透過叫用`SignatureServiceClient`物件的`certify`方法並傳遞下列值來認證PDF檔案：

   * 代表要認證之PDF檔案的`BLOB`物件。
   * 字串值，代表將包含簽章之簽章欄位的名稱。
   * `Credential`物件，代表用來認證PDF檔案的認證。 使用物件的建構函式建立`Credential`物件，並指定別名給`Credential`物件的`alias`屬性。
   * `HashAlgorithm`物件，指定代表用於摘要PDF檔案的雜湊演演算法的靜態資料成員。 例如，您可以指定`HashAlgorithm.SHA1`來使用SHA1演演算法。
   * Boolean值，指定是否使用雜湊演演算法。
   * 代表驗證PDF檔案之原因的字串值。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * `MDPPermissions`物件的靜態資料成員，指定可在PDF檔案上執行的使簽章失效的動作。
   * Boolean值，指定是否使用作為前一個引數值傳遞的`MDPPermissions`物件。
   * 字串值，說明哪些動作會使簽章失效。
   * 控制認證簽章外觀的`PDFSignatureAppearanceOptions`物件。 使用物件的建構函式建立`PDFSignatureAppearanceOptions`物件。 您可以藉由設定其中一個資料成員來修改簽章的外觀。
   * `System.Boolean`物件，指定是否對簽署者的憑證執行撤銷檢查。 若完成此撤銷檢查，則會內嵌於簽章中。 預設為 `false`。
   * 指定正在認證的簽章欄位是否已鎖定的`System.Boolean`物件。 如果欄位已鎖定，則簽章欄位會標示為唯讀，其屬性無法修改，且沒有必要許可權的任何人都無法清除。 預設為 `false`。
   * 指定簽章欄位是否已鎖定的`System.Boolean`物件。 也就是說，如果您將`true`傳遞給上一個引數，則將`true`傳遞給此引數。
   * 儲存線上憑證狀態通訊協定(OCSP)支援之偏好設定的`OCSPPreferences`物件，可提供用於認證PDF檔案之認證的狀態相關資訊。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。
   * 儲存憑證撤銷清單(CRL)偏好設定的`CRLPreferences`物件。 如果未完成撤銷檢查，則不會使用此引數，您可以指定`null`。
   * 儲存時間戳記提供者(TSP)支援之偏好設定的`TSPPreferences`物件。 例如，建立`TSPPreferences`物件後，您可以設定`TSPPreferences`物件的`tspServerURL`資料成員來設定TSP的URL。 此引數是選用的，可以是`null`。

   `certify`方法傳回代表認證PDF檔案的`BLOB`物件。

1. 將認證的PDF檔案儲存為PDF檔案

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞字串值，該值代表PDF檔案的檔案位置，其中將包含認證的PDF檔案以及開啟檔案的模式。
   * 建立位元組陣列，儲存`certify`方法傳回的`BLOB`物件的內容。 取得`BLOB`物件的`binaryData`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證數位簽章 {#verifying-digital-signatures}

可以驗證數位簽章，以確保已簽署的PDF檔案未被修改且數位簽章有效。 驗證數位簽章時，您可以檢查簽章的狀態和簽章的屬性，例如簽署者的身分。 在信任數位簽名之前，建議您先驗證它。 驗證數位簽名時，請參考包含數位簽名的PDF檔案。

假設簽署者的身分不明。 當您在Acrobat中開啟PDF檔案時，會出現警告訊息，指出簽署者的身分不明，如下圖所示。

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

同樣地，當您以程式設計方式驗證數位簽名時，您可以判斷簽名者的身分狀態。 例如，如果您驗證上圖所示檔案中的數位簽章，則結果會是簽署者的身分不明。

>[!NOTE]
>
>如需有關簽章服務和驗證數位簽章的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-6}

若要驗證數位簽名，請執行以下工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得包含要驗證之簽名的PDF檔案。
1. 設定PKI執行階段選項。
1. 驗證數位簽章。
1. 決定簽章的狀態。
1. 判斷簽署者的身分。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如需關於這些JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽章使用者端**

在您以程式設計方式執行簽章服務作業之前，請先建立簽章服務使用者端。

**取得包含簽章的PDF檔案以進行驗證**

若要驗證用於數位簽署或認證PDF檔案的簽章，請取得包含簽章的PDF檔案。

**設定PKI執行階段選項**

設定Signature service在PDF檔案中驗證簽名時所使用的PKI執行階段選項：

* 驗證時間
* 撤銷檢查
* 時間戳記值

在設定這些選項時，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），以指示使用目前時間。 如需不同時間值的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`VerificationTime`列舉值。

您也可以指定是否執行撤銷檢查作為驗證程式的一部分。 例如，您可以執行撤銷檢查來決定是否撤銷憑證。 如需有關撤銷檢查選項的資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`RevocationCheckStyle`列舉值。

若要對憑證執行撤銷檢查，請使用`CRLOptionSpec`物件指定憑證撤銷清單(CRL)伺服器的URL。 不過，如果您未指定CRL伺服器的URL，則簽章服務會從憑證中取得該URL。

執行撤銷檢查時，您可以使用線上憑證狀態通訊協定(OCSP)伺服器，而不使用CRL伺服器。 通常，當使用OCSP伺服器而非CRL伺服器時，撤銷檢查的執行速度會更快。 （請參閱[線上憑證狀態通訊協定](https://tools.ietf.org/html/rfc2560)。）

您可以使用Adobe應用程式和服務來設定Signature服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是先在Adobe應用程式和服務中設定，則會檢查OCSP伺服器，然後檢查CRL伺服器。

如果您未執行撤銷檢查，Signature service就不會檢查憑證是否已撤銷。 也就是說，會忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用`CRLOptionSpec`和`OCSPOptionSpec`物件來覆寫憑證中指定的URL。 例如，若要覆寫CRL伺服器，您可以叫用`CRLOptionSpec`物件的`setLocalURI`方法。

時間戳記是追蹤已簽署或已驗證檔案修改時間的程式。 簽署檔案後，沒有人可以修改它。 時間戳記有助於加強已簽署或已驗證檔案的有效性。 您可以使用`TSPOptionSpec`物件來設定時間戳記選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務快速啟動中，驗證時間設為`VerificationTime.CURRENT_TIME`，撤銷檢查設為`RevocationCheckStyle.BestEffort`。 因為未指定CRL或OCSP伺服器資訊，所以會從憑證取得伺服器資訊。

**驗證數位簽章**

若要成功驗證簽章，請指定包含簽章之簽章欄位的完整名稱，例如`form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，您也可以使用簽名欄位的部分名稱： `SignatureField3`。

依預設，簽名服務將驗證後檔案可簽署的時間限製為65分鐘。 如果使用者嘗試在目前時間驗證簽名，且簽署時間晚於目前時間且在65分鐘內，則簽名服務不會建立驗證錯誤。

>[!NOTE]
>
>如需驗證簽章時所需的其他值，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**決定簽章的狀態**

在驗證數位簽名時，您可以檢查簽名的狀態。

**決定簽署者的身分**

您可以決定簽署者的身分，身分可以是下列其中一個值：

* **未知**：此簽署者不明，因為無法執行簽署者驗證。
* **信任**：此簽署者受信任。
* **不受信任**：此簽署者不受信任。

**另請參閱**

[使用Java API驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[使用網站服務API驗證數位簽名](#verify-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API驗證數位簽名 {#verify-digital-signatures-using-the-java-api}

使用簽名服務API (Java)驗證數位簽名：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽章使用者端

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`SignatureServiceClient`物件。

1. 取得包含要驗證之簽名的PDF檔案

   * 建立一個`java.io.FileInputStream`物件，代表包含要使用其建構函式驗證的簽章的PDF檔案。 傳遞字串值，指定PDF檔案的位置。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定PKI執行階段選項

   * 使用物件的建構函式建立`PKIOptions`物件。
   * 透過叫用`PKIOptions`物件的`setVerificationTime`方法並傳遞指定驗證時間的`VerificationTime`列舉值來設定驗證時間。
   * 透過叫用`PKIOptions`物件的`setRevocationCheckStyle`方法並傳遞指定是否執行撤銷檢查的`RevocationCheckStyle`列舉值來設定撤銷檢查選項。

1. 驗證數位簽名

   叫用`SignatureServiceClient`物件的`verify2`方法並傳遞下列值以驗證簽章：

   * 包含數位簽署或認證的PDF檔案的`com.adobe.idp.Document`物件。
   * 字串值，代表包含要驗證之簽章的簽章欄位名稱。
   * 包含PKI執行階段選項的`PKIOptions`物件。
   * 包含SPI資訊的`VerifySPIOptions`執行個體。 您可以為此引數指定`null`。

   `verify2`方法傳回`PDFSignatureVerificationInfo`物件，其中包含可用來驗證數位簽章的資訊。

1. 決定簽章的狀態

   * 透過叫用`PDFSignatureVerificationInfo`物件的`getStatus`方法來判斷簽章的狀態。 此方法會傳回指定簽章狀態的`SignatureStatus`物件。 例如，如果未修改已簽署的PDF檔案，此方法會傳回`SignatureStatus.DocumentSigNoChanges`。

1. 判斷簽署者的身分

   * 透過叫用`PDFSignatureVerificationInfo`物件的`getSigner`方法來判斷簽署者的身分。 此方法傳回`IdentityInformation`物件。
   * 叫用`IdentityInformation`物件的`getStatus`方法以判斷簽署者的身分。 此方法會傳回指定識別的`IdentityStatus`列舉值。 例如，如果簽署者受到信任，此方法會傳回`IdentityStatus.TRUSTED`。

**另請參閱**

[驗證數位簽章](#verify-digital-signatures-using-the-java-api)

[快速入門(SOAP模式)：使用Java API驗證數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API驗證數位簽名 {#verify-digital-signatures-using-the-web-service-api}

使用簽名服務API （Web服務）驗證數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立簽章使用者端

   * 使用預設建構函式建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`SignatureServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含要驗證之簽名的PDF檔案

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存包含要驗證的數位或認證簽名的PDF檔案。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表已簽署PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 將物件的`MTOM`屬性指派給位元組陣列的內容，以填入`BLOB`物件。

1. 設定PKI執行階段選項

   * 使用物件的建構函式建立`PKIOptions`物件。
   * 將`PKIOptions`物件的`verificationTime`資料成員指派給指定驗證時間的`VerificationTime`列舉值，以設定驗證時間。
   * 將`PKIOptions`物件的`revocationCheckStyle`資料成員指派給指定是否要執行撤銷檢查的`RevocationCheckStyle`列舉值，以設定撤銷檢查選項。

1. 驗證數位簽名

   叫用`SignatureServiceClient`物件的`verify2`方法並傳遞下列值以驗證簽章：

   * 包含數位簽署或認證的PDF檔案的`BLOB`物件。
   * 字串值，代表包含要驗證之簽章的簽章欄位名稱。
   * 包含PKI執行階段選項的`PKIOptions`物件。
   * 包含SPI資訊的`VerifySPIOptions`執行個體。 您可以為此引數指定`null`。

   `verify2`方法傳回`PDFSignatureVerificationInfo`物件，其中包含可用來驗證數位簽章的資訊。

1. 決定簽章的狀態

   取得`PDFSignatureVerificationInfo`物件的`status`資料成員的值，以判斷簽章的狀態。 此資料成員儲存指定簽章狀態的`SignatureStatus`物件。 例如，如果已簽署的PDF檔案被修改，`status`資料成員會儲存值`SignatureStatus.DocumentSigNoChanges`。

1. 判斷簽署者的身分

   * 擷取`PDFSignatureVerificationInfo`物件的`signer`資料成員的值，以判斷簽署者的身分。 此成員傳回`IdentityInformation`物件。
   * 擷取`IdentityInformation`物件的`status`資料成員，以判斷簽署者的身分。 此資料成員傳回指定識別的`IdentityStatus`列舉值。 例如，如果簽署者受到信任，則此成員會傳回`IdentityStatus.TRUSTED`。

**另請參閱**

[驗證數位簽章](#verify-digital-signatures-using-the-java-api)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證多個數位簽名 {#verifying-multiple-digital-signatures}

AEM Forms提供驗證PDF檔案中所有數位簽名的方法。 假設PDF檔案包含多個數位簽名，因為業務流程需要來自多個簽名者的簽名。 例如，假設金融交易需要貸款專員和經理的簽名。 您可以使用簽名服務Java API或Web服務API來驗證PDF檔案中的所有簽名。 驗證多個數位簽名時，您可以檢查每個簽名的狀態和屬性。 在您信任數位簽名之前，建議您先驗證它。 建議您熟悉如何驗證單一數位簽名。

>[!NOTE]
>
>如需有關簽章服務和驗證數位簽章的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-7}

若要驗證多個數位簽名，請執行以下工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得包含要驗證之簽名的PDF檔案。
1. 設定PKI執行階段選項。
1. 擷取所有數位簽名。
1. 逐一檢視所有簽章。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如需關於這些JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽章使用者端**

在您以程式設計方式執行簽章服務作業之前，請先建立簽章服務使用者端。

**取得包含簽章的PDF檔案以進行驗證**

若要驗證用於數位簽署或認證PDF檔案的簽章，請取得包含簽章的PDF檔案。

**設定PKI執行階段選項**

設定Signature service在驗證PDF檔案中所有簽名時所使用的PKI執行階段選項：

* 驗證時間
* 撤銷檢查
* 時間戳記值

在設定這些選項時，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），以指示使用目前時間。 如需不同時間值的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`VerificationTime`列舉值。

您也可以指定是否執行撤銷檢查作為驗證程式的一部分。 例如，您可以執行撤銷檢查來決定是否撤銷憑證。 如需有關撤銷檢查選項的資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`RevocationCheckStyle`列舉值。

若要對憑證執行撤銷檢查，請使用`CRLOptionSpec`物件指定憑證撤銷清單(CRL)伺服器的URL。 不過，如果您未指定CRL伺服器的URL，則簽章服務會從憑證中取得該URL。

執行撤銷檢查時，您可以使用線上憑證狀態通訊協定(OCSP)伺服器，而不使用CRL伺服器。 通常在使用OCSP伺服器而非CRL伺服器時，撤銷檢查的執行速度會更快。 （請參閱[線上憑證狀態通訊協定](https://tools.ietf.org/html/rfc2560)。）

您可以使用Adobe應用程式和服務來設定Signature服務使用的CRL和OCSP伺服器順序。 例如，如果先在Adobe應用程式和服務中設定OCSP伺服器，則會檢查OCSP伺服器，然後檢查CRL伺服器。

如果您未執行撤銷檢查，Signature service就不會檢查憑證是否已撤銷。 也就是說，會忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用`CRLOptionSpec`和`OCSPOptionSpec`物件來覆寫憑證中指定的URL。 例如，若要覆寫CRL伺服器，您可以叫用`CRLOptionSpec`物件的`setLocalURI`方法。

時間戳記是追蹤已簽署或已驗證檔案修改時間的程式。 簽署檔案後，沒有人可以修改它。 時間戳記有助於加強已簽署或已驗證檔案的有效性。 您可以使用`TSPOptionSpec`物件來設定時間戳記選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務快速啟動中，驗證時間設為`VerificationTime.CURRENT_TIME`，撤銷檢查設為`RevocationCheckStyle.BestEffort`。 因為未指定CRL或OCSP伺服器資訊，所以會從憑證取得伺服器資訊。

**擷取所有數位簽章**

若要驗證PDF檔案中的所有數位簽名，請從PDF檔案中擷取數位簽名。 所有簽名都會傳回清單中。 在驗證數位簽章時，請檢查簽章的狀態。

>[!NOTE]
>
>與驗證單一數位簽名不同，當您驗證多個簽名時，您不需要指定簽名欄位名稱。

**反複檢查所有簽章**

逐一檢視每個簽章。 亦即，針對每個簽名，驗證數位簽名，並檢查簽名者的身分和每個簽名的狀態。 （請參閱[驗證數位簽章](#verify-digital-signatures-using-the-java-api)。）

>[!NOTE]
>
>如果要求是整個檔案，則不需要反複檢查所有簽名。

**另請參閱**

[使用Java API驗證多個數位簽名](#verify-digital-signatures-using-the-java-api)

[使用網站服務API驗證多個數位簽名](#verify-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API驗證多個數位簽名 {#verify-multiple-digital-signatures-using-the-java-api}

使用簽名服務API (Java)驗證多個數位簽名：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽章使用者端

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`SignatureServiceClient`物件。

1. 取得包含要驗證之簽名的PDF檔案

   * 建立一個`java.io.FileInputStream`物件，代表包含多個數位簽章的PDF檔案，以使用它的建構函式進行驗證。 傳遞字串值，指定PDF檔案的位置。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定PKI執行階段選項

   * 使用物件的建構函式建立`PKIOptions`物件。
   * 透過叫用`PKIOptions`物件的`setVerificationTime`方法並傳遞指定驗證時間的`VerificationTime`列舉值來設定驗證時間。
   * 透過叫用`PKIOptions`物件的`setRevocationCheckStyle`方法並傳遞指定是否執行撤銷檢查的`RevocationCheckStyle`列舉值來設定撤銷檢查選項。

1. 擷取所有數位簽名

   叫用`SignatureServiceClient`物件的`verifyPDFDocument`方法，並傳遞下列值：

   * 包含包含包含多個數位簽章之PDF檔案的`com.adobe.idp.Document`物件。
   * 包含PKI執行階段選項的`PKIOptions`物件。
   * 包含SPI資訊的`VerifySPIOptions`執行個體。 您可以為此引數指定`null`。

   `verifyPDFDocument`方法傳回`PDFDocumentVerificationInfo`物件，其中包含PDF檔案中所有數位簽章的相關資訊。

1. 逐一檢視所有簽章

   * 透過叫用`PDFDocumentVerificationInfo`物件的`getVerificationInfos`方法來重複處理所有簽章。 此方法會傳回`java.util.List`物件，其中每個元素都是`PDFSignatureVerificationInfo`物件。 使用`java.util.Iterator`物件來反複檢查簽章清單。
   * 您可以使用`PDFSignatureVerificationInfo`物件來執行工作，例如透過叫用`PDFSignatureVerificationInfo`物件的`getStatus`方法來判斷簽章的狀態。 此方法會傳回`SignatureStatus`物件，其靜態資料成員會通知您簽章的狀態。 例如，如果簽章不明，此方法會傳回`SignatureStatus.DocumentSignatureUnknown`。

**另請參閱**

[驗證多個數位簽名](#verifying-multiple-digital-signatures)

[快速入門(SOAP模式)：使用Java API驗證多個數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[驗證數位簽章](#verify-digital-signatures-using-the-java-api)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API驗證多個數位簽名 {#verifying-multiple-digital-signatures-using-the-web-service-api}

使用簽名服務API （Web服務）驗證多個數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立簽章使用者端

   * 使用預設建構函式建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`SignatureServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含要驗證之簽名的PDF檔案

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件儲存含有多個要驗證的數位簽名的PDF檔案。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表PDF檔案檔案位置和開啟檔案模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 將物件的`MTOM`屬性指派給位元組陣列的內容，以填入`BLOB`物件。

1. 設定PKI執行階段選項

   * 使用物件的建構函式建立`PKIOptions`物件。
   * 將`PKIOptions`物件的`verificationTime`資料成員指派給指定驗證時間的`VerificationTime`列舉值，以設定驗證時間。
   * 將`PKIOptions`物件的`revocationCheckStyle`資料成員指派給指定是否要執行撤銷檢查的`RevocationCheckStyle`列舉值，以設定撤銷檢查選項。

1. 擷取所有數位簽名

   叫用`SignatureServiceClient`物件的`verifyPDFDocument`方法，並傳遞下列值：

   * 包含包含包含多個數位簽章之PDF檔案的`BLOB`物件。
   * 包含PKI執行階段選項的`PKIOptions`物件。
   * 包含SPI資訊的`VerifySPIOptions`執行個體。 您可以為此引數指定null。

   `verifyPDFDocument`方法傳回`PDFDocumentVerificationInfo`物件，其中包含PDF檔案中所有數位簽章的相關資訊。

1. 逐一檢視所有簽章

   * 透過取得`PDFDocumentVerificationInfo`物件的`verificationInfos`資料成員來反複檢查所有簽章。 此資料成員傳回`Object`陣列，其中每個元素都是`PDFSignatureVerificationInfo`物件。
   * 使用`PDFSignatureVerificationInfo`物件，您可以透過取得`PDFSignatureVerificationInfo`物件的`status`資料成員來執行判斷簽章狀態等工作。 此資料成員傳回`SignatureStatus`物件，其靜態資料成員會通知您簽章的狀態。 例如，如果簽章不明，此方法會傳回`SignatureStatus.DocumentSignatureUnknown`。

**另請參閱**

[驗證多個數位簽名](#verifying-multiple-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 移除數位簽章 {#removing-digital-signatures}

必須先從簽名欄位中移除數位簽名，才能套用更新的數位簽名。 無法覆寫數位簽章。 如果您嘗試將數位簽章套用至包含簽章的簽章欄位，會發生例外狀況。

>[!NOTE]
>
>如需有關簽章服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-8}

若要從簽名欄位中移除數位簽名，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得包含要移除之簽名的PDF檔案。
1. 從簽名欄位中移除數位簽名。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如需關於這些JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽章使用者端**

您必須先建立簽名服務使用者端，才能以程式設計方式執行簽名服務作業。

**取得包含要移除之簽章的PDF檔案**

若要從PDF檔案中移除簽名，您必須取得包含簽名的PDF檔案。

**從簽章欄位移除數位簽章**

若要成功從PDF檔案中移除數位簽名，您必須指定包含數位簽名的簽名欄位名稱。 此外，您必須擁有移除數位簽章的許可權；否則，會發生例外狀況。

**將PDF檔案儲存為PDF檔案**

簽名服務從簽名欄位中移除數位簽名後，您可以將PDF檔案儲存為PDF檔案，以便使用者可以在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[使用Java API移除數位簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[使用網站服務API移除數位簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API移除數位簽名 {#remove-digital-signatures-using-the-java-api}

使用簽名API (Java)移除數位簽名：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽章使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`SignatureServiceClient`物件。

1. 取得包含要移除之簽名的PDF檔案

   * 建立`java.io.FileInputStream`物件，代表包含要移除之簽章的PDF檔案，方法是使用其建構函式，並傳遞指定PDF檔案位置的字串值。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 從簽名欄位中移除數位簽名

   叫用`SignatureServiceClient`物件的`clearSignatureField`方法並傳遞下列值，從簽章欄位中移除數位簽章：

   * 一個`com.adobe.idp.Document`物件，代表包含要移除之簽章的PDF檔案。
   * 字串值，指定包含數位簽章之簽章欄位的名稱。

   `clearSignatureField`方法傳回`com.adobe.idp.Document`物件，該物件代表已從其中移除數位簽名的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法。 傳遞`java.io.File`物件以將`com.adobe.idp.Document`物件的內容複製到檔案。 確定您使用的是`clearSignatureField`方法傳回的`Document`物件。

**另請參閱**

[移除數位簽章](digitally-signing-certifying-documents.md#removing-digital-signatures)

[快速入門(SOAP模式)：使用Java API移除數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API移除數位簽名 {#remove-digital-signatures-using-the-web-service-api}

使用簽名API （Web服務）移除數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立簽章使用者端

   * 使用預設建構函式建立`SignatureServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`SignatureServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`SignatureServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含要移除之簽名的PDF檔案

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存包含要移除的數位簽名的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表已簽署PDF檔案的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派物件的`MTOM`屬性，填入`BLOB`物件。

1. 從簽名欄位中移除數位簽名

   透過叫用`SignatureServiceClient`物件的`clearSignatureField`方法並傳遞下列值來移除數位簽章：

   * 包含已簽署PDF檔案的`BLOB`物件。
   * 字串值，代表包含要移除之數位簽章的簽章欄位名稱。

   `clearSignatureField`方法傳回`BLOB`物件，該物件代表已從其中移除數位簽名的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立`System.IO.FileStream`物件，方法是叫用其建構函式，並傳遞代表包含空白簽章欄位的PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存`sign`方法傳回的`BLOB`物件的內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[移除數位簽章](digitally-signing-certifying-documents.md#removing-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
