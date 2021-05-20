---
title: 將PDF轉換為Postscript和Image檔案
seo-title: 將PDF轉換為Postscript和Image檔案
description: 使用「轉換PDF」服務，使用Java API和Web服務API將PDF文檔轉換為PostScript，並轉換為多種影像格式（JPEG、JPEG 2000、PNG和TIFF）。
seo-description: 使用「轉換PDF」服務，使用Java API和Web服務API將PDF文檔轉換為PostScript，並轉換為多種影像格式（JPEG、JPEG 2000、PNG和TIFF）。
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2846'
ht-degree: 0%

---

# 將PDF轉換為Postscript和影像檔案{#converting-pdf-to-postscript-andimage-files}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於轉換PDF服務**

「轉換PDF」服務將PDF文檔轉換為PostScript和多種影像格式（JPEG、JPEG 2000、PNG和TIFF）。 將PDF文檔轉換為PostScript對於在任何PostScript打印機上基於伺服器的無人值守打印非常有用。 將PDF檔案轉換為多頁TIFF檔案，在不支援PDF檔案的內容管理系統中封存檔案時非常實用。

您可以使用「轉換PDF」服務來完成下列工作：

* 將PDF檔案轉換為PostScript。
* 將PDF文檔轉換為影像格式。

>[!NOTE]
>
>如需轉換PDF服務的詳細資訊，請參閱[AEM Forms適用的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PDF文檔轉換為PostScript {#converting-pdf-documents-to-postscript}

本主題說明如何使用「轉換PDF服務API（Java和Web服務）」，以程式設計方式將PDF檔案轉換為PostScript檔案。 轉換為PostScript檔案的PDF文檔必須是非互動式PDF文檔。 也就是說，如果嘗試將互動式PDF檔案轉換為PostScript檔案，則會引發例外狀況。

>[!NOTE]
>
>如需轉換PDF服務的詳細資訊，請參閱[AEM Forms適用的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}的摘要

要將PDF文檔轉換為PostScript檔案，請執行以下步驟：

1. 包含專案檔案。
1. 建立轉換PDF服務用戶端。
1. 參考要轉換為PostScript檔案的PDF文檔。
1. 設定轉換執行時間選項。
1. 將PDF文檔轉換為PostScript檔案。
1. 儲存PostScript檔案。

**包含項目檔案**

將必要的檔案納入您的開發專案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立轉換PDF用戶端**

必須先建立「轉換PDF」服務客戶端，才能以寫程式方式執行「轉換PDF」服務操作。 如果您使用Java API，請建立`ConvertPdfServiceClient`物件。 如果您使用Web服務API，請建立`ConvertPDFServiceService`物件。

本節使用AEM Forms中推出的網站服務功能。 若要存取新功能，您必須使用`lc_version`屬性來建構您的Proxy物件。 (請參閱[使用網站服務叫用AEM Forms中的「使用網站服務存取新功能」。)](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

**參考要轉換為PostScript檔案的PDF文檔**

參考要轉換為PostScript檔案的PDF文檔。 如本主題前面所述，PDF文檔必須是非互動式PDF文檔。 如果嘗試將互動式PDF檔案轉換為PostScript檔案，則會引發例外狀況。

**設定轉換執行時間選項**

將PDF文檔轉換為PostScript檔案時，您可以定義運行時選項，以指定所建立的PostScript類型。 例如，您可以定義第3層PostScript檔案。

一般而言，產生的PostScript檔案會反映輸入PDF檔案的大小。 如果選擇`ShrinkToFit`選項（該選項會縮小PostScript檔案的輸出以適合頁面），則輸入的PDF文檔與生成的PostScript檔案之間將不會出現差異。 `ShrinkToFit`選項只有在您選擇在比輸入PDF文檔小的頁面大小上打印時才生效。 若要選取較小的頁面大小，請定義`PageSize`選項。 此外，建議將`RotateAndCenter`選項設定為`true`以獲得正確的PostScript輸出。

同樣，如果選擇`ExpandToFit`選項（展開PostScript檔案的輸出以適合頁面），則只有在選擇打印的頁面大小比輸入的PDF文檔大時，該選項才生效。 若要選取較大的頁面大小，請定義`PageSize`選項。 此外，建議將`RotateAndCenter`選項設定為`true`以獲得正確的PostScript輸出。

>[!NOTE]
>
>如需可設定之執行階段值的詳細資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToPSOptionsSpec`類別參考。

**將PDF文檔轉換為PostScript檔案**

建立服務客戶端並設定運行時選項後，可以調用PostScript轉換操作。 此操作需要有關要轉換的文檔的資訊，包括目標文檔的首選PostScript級別。

**儲存PostScript檔案**

將PDF文檔轉換為PostScript後，可以將輸出另存為PostScript檔案。

**另請參閱**

[使用Java API將PDF檔案轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[使用Web服務API將PDF檔案轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速入門](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API {#convert-a-pdf-document-to-ps-using-the-java-api}將PDF文檔轉換為PS

使用「轉換PDF服務API(Java)」將PDF文檔轉換為PostScript:

1. 包含專案檔案。

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-convertpdf-client.jar。

1. 建立轉換PDF用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`ConvertPdfServiceClient`物件。

1. 參考要轉換為PostScript檔案的PDF文檔。

   * 使用其建構子建立`java.io.FileInputStream`物件，並傳遞字串值，指定要轉換的PDF檔案的位置。
   * 使用`com.adobe.idp.Document`建構子建立`com.adobe.idp.Document`物件以儲存PDF檔案。 傳遞包含PDF檔案的`java.io.FileInputStream`物件。

1. 設定轉換執行時間選項。

   * 調用`ToPSOptionsSpec`對象的建構子以建立對象。
   * 通過調用屬於`ToPSOptionsSpec`對象的適當方法來設定運行時選項。 例如，要定義已建立的PostScript級別，請調用`ToPSOptionsSpec`對象的`setPsLevel`方法，並傳遞指定PostScript級別的`PSLevel`枚舉值。 如需可設定之所有執行階段值的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToPSOptionsSpec`類別參考。

1. 將PDF文檔轉換為PostScript檔案。

   調用`ConvertPdfServiceClient`對象的`toPS2`方法並傳遞以下值：

   * 代表要轉換為PostScript檔案的PDF文檔的`com.adobe.idp.Document`對象。
   * `ToPSOptionsSpec`對象，指定PostScript運行時選項。

   `toPS2`方法返回包含新PostScript文檔的`Document`對象。

1. 儲存PostScript檔案。

   * 建立`java.io.File`物件，並確定副檔名為.ps。
   * 調用`Document`對象的`copyToFile`方法，將`Document`對象的內容複製到檔案（確保使用`toPS2`方法返回的`Document`對象）。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API將PDF檔案轉換為PostScript](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#convert-a-pdf-document-to-ps-using-the-web-service-api}將PDF文檔轉換為PS

使用「轉換PDF服務API（Web服務）」將PDF文檔轉換為PostScript:

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立轉換PDF用戶端。

   * 使用其預設建構子建立`ConvertPdfServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`ConvertPdfServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）。 您不需要使用`lc_version`屬性。 但請指定`?blob=mtom`。
   * 獲取`ConvertPdfServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考要轉換為PostScript檔案的PDF文檔。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存轉換為PostScript檔案的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要轉換的PDF文檔的檔案位置，以及在中開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、起始位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 設定轉換執行時間選項。

   * 調用`ToPSOptionsSpec`對象的建構子以建立對象。
   * 通過為`ToPSOptionsSpec`對象的資料成員分配值來設定運行時選項。 例如，要定義已建立的PostScript級別，請將`PSLevel`枚舉值分配給`ToPSOptionsSpec`對象的`psLevel`資料成員。

1. 將PDF文檔轉換為PostScript檔案。

   調用`GeneratePDFServiceService`對象的`toPS2`方法並傳遞以下值：

   * 代表要轉換為PostScript檔案的PDF文檔的`BLOB`對象
   * 指定運行時選項的`ToPSOptionsSpec`對象

   轉換完成後，通過訪問其`BLOB`對象的`MTOM`屬性來提取表示PostScript文檔的二進位資料。 這會傳回位元組陣列，您可將其寫出至PostScript檔案。

1. 儲存PostScript檔案。

   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞代表PS檔案檔案位置的字串值。
   * 建立位元組陣列，用於儲存`encryptPDFUsingPassword`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象的`MTOM`欄位的值，填入位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PostScript檔案。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將PDF文檔轉換為影像格式{#converting-pdf-documents-to-image-formats}

您可以使用「轉換PDF」服務，以寫程式方式將PDF文檔轉換為影像格式，包括JPEG、JPEG 2000、TIFF和PNG。 通過將PDF文檔轉換為影像檔案，可以將PDF文檔用作影像檔案。 例如，您可以將映像放置在企業內容管理系統中以進行儲存。

將PDF文檔轉換為影像時，「轉換PDF」服務會為文檔中的每一頁建立單獨的影像。 也就是說，如果文檔有20頁，則「轉換PDF」服務將建立20個影像檔案。 將PDF文檔轉換為影像格式時，可以為PDF文檔內的每頁建立單個影像，也可以為整個PDF文檔建立單個影像檔案。

>[!NOTE]
>
>如需轉換PDF服務的詳細資訊，請參閱[AEM Forms適用的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}的摘要

要將PDF文檔轉換為任何支援的類型，請執行以下步驟：

1. 包含專案檔案。
1. 建立轉換PDF服務用戶端。
1. 檢索要轉換的PDF文檔。
1. 設定運行時選項。
1. 將PDF轉換為影像。
1. 從集合中擷取影像檔案。

**包含項目檔案**

將必要的檔案納入您的開發專案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立轉換PDF用戶端**

必須先建立「轉換PDF」服務客戶端，才能以寫程式方式執行「轉換PDF」服務操作。 如果您使用Java API，請建立`ConvertPdfServiceClient`物件。 如果您使用Web服務API，請建立`ConvertPDFServiceService`物件。

**檢索要轉換的PDF文檔**

必須檢索PDF文檔才能轉換為影像。 無法將互動式PDF文檔轉換為影像。 如果嘗試執行此操作，則會擲回例外。 要將互動式PDF文檔轉換為影像檔案，必須先平面化PDF文檔，然後再轉換。 （請參閱[拼合PDF文檔](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)。）

**設定運行時選項**

必須設定運行時選項，如影像格式和解析度值。 有關運行時值的資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToImageOptionsSpec`類參考。

**將PDF轉換為影像**

建立服務客戶端並設定運行時選項後，可以將PDF文檔轉換為影像。 會傳回包含影像的集合物件。

**從集合中擷取影像檔案**

您可以從轉換PDF服務傳回的集合物件擷取影像檔案。 集合中的每個元素都是一個`com.adobe.idp.Document`例項（如果您使用Web服務，則為`BLOB`例項），可儲存為影像檔案，例如JPG檔案。

影像檔案的格式取決於`ImageConvertFormat`運行時選項。 也就是說，如果將`ImageConvertFormat`運行時選項設定為`ImageConvertFormat.JPEG`，則可以將影像檔案另存為JPG檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速入門](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API {#convert-a-pdf-document-to-image-files-using-the-java-api}將PDF文檔轉換為影像檔案

使用「轉換PDF服務API(Java)」將PDF文檔轉換為影像格式：

1. 包含專案檔案。

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-convertpdf-client.jar。

1. 建立轉換PDF用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`ConvertPdfServiceClient`物件。

1. 檢索要轉換的PDF文檔。

   * 建立一個`java.io.FileInputStream`對象，該對象表示要轉換的PDF文檔，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定運行時選項。

   * 使用其建構子建立`ToImageOptionsSpec`物件。
   * 根據需要調用屬於此對象的方法。 例如，通過調用`setImageConvertFormat`方法並傳遞指定格式類型的`ImageConvertFormat`枚舉值來設定影像類型。

   >[!NOTE]
   >
   >必須設定`ImageConvertFormat`枚舉值。

1. 將PDF轉換為影像。

   調用`ConvertPdfServiceClient`對象的`toImage2`方法並傳遞以下值：

   * 代表要轉換的PDF檔案的`com.adobe.idp.Document`物件。
   * `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec`物件，包含關於目標影像格式的各種偏好設定。

   `toImage2`方法返回包含影像的`java.util.List`對象。 集合中的每個元素都是`com.adobe.idp.Document`例項。

1. 從集合中擷取影像檔案。

   逐一查看`java.util.List`物件，以判斷影像是否存在。 每個元素都是`com.adobe.idp.Document`例項。 叫用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`物件，以儲存影像。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將PDF文檔轉換為JPEG檔案](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 使用Web服務API {#convert-a-pdf-document-to-image-files-using-the-web-service-api}將PDF文檔轉換為影像檔案

使用「轉換PDF服務API（Web服務）」將PDF文檔轉換為影像格式：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立轉換的PDF客戶端。

   * 使用其預設建構子建立`ConvertPdfServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`ConvertPdfServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）。 您不需要使用`lc_version`屬性。 但請指定`?blob=mtom`。
   * 獲取`ConvertPdfServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 檢索要轉換的PDF文檔。

   * 使用其建構子建立`BLOB`物件。 此`BLOB`物件用於儲存PDF表單。
   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，指定PDF表單的位置以及在中開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性來確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 設定運行時選項。

   * 使用其建構子建立`ToImageOptionsSpec`物件。
   * 根據需要調用屬於此對象的方法。 例如，通過調用`setImageConvertFormat`方法並傳遞指定格式類型的`ImageConvertFormat`枚舉值來設定影像類型。

   >[!NOTE]
   >
   >必須設定`ImageConvertFormat`枚舉值。

1. 將PDF轉換為影像。

   調用`ConvertPDFServiceService`對象的`toImage2`方法並傳遞以下值：

   * 表示要轉換的檔案的`BLOB`對象
   * `ToImageOptionsSpec`對象，包含有關目標影像格式的各種首選項

   `toImage2`方法返回包含新建立的影像檔案的`MyArrayOfBLOB`對象。

1. 從集合中擷取影像檔案。

   * 通過獲取`Count`欄位的值，確定`MyArrayOfBLOB`對象中的元素數。 每個元素都是包含影像的`BLOB`物件。
   * 逐一查看`MyArrayOfBLOB`物件，並儲存每個影像檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
