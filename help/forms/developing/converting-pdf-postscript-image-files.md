---
title: 將PDF轉換為Postscript和影像檔案
seo-title: 將PDF轉換為Postscript和影像檔案
description: 使用「轉換PDF」服務，使用Java API和Web Service API，將PDF檔案轉換為PostScript，並轉換為多種影像格式（JPEG、JPEG 2000、PNG和TIFF）。
seo-description: 使用「轉換PDF」服務，使用Java API和Web Service API，將PDF檔案轉換為PostScript，並轉換為多種影像格式（JPEG、JPEG 2000、PNG和TIFF）。
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2847'
ht-degree: 0%

---


# 將PDF轉換為Postscript和影像檔{#converting-pdf-to-postscript-andimage-files}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

**關於轉換PDF服務**

「轉換PDF」服務會將PDF檔案轉換為PostScript和多種影像格式（JPEG、JPEG 2000、PNG和TIFF）。 將PDF檔案轉換為PostScript對於在任何PostScript印表機上以伺服器為基礎的無人值守列印十分有用。 在不支援PDF檔案的內容管理系統中封存檔案時，將PDF檔案轉換為多頁TIFF檔案十分實用。

您可以使用「轉換PDF」服務完成下列工作：

* 將PDF檔案轉換為PostScript。
* 將PDF檔案轉換為影像格式。

>[!NOTE]
>
>如需轉換PDF服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PDF檔案轉換為PostScript {#converting-pdf-documents-to-postscript}

本主題說明如何使用轉換PDF服務API（Java和web service），以程式設計方式將PDF檔案轉換為PostScript檔案。 轉換為PostScript檔案的PDF檔案必須是非互動式PDF檔案。 也就是說，如果您嘗試將互動式PDF檔案轉換為PostScript檔案，則會擲回例外。

>[!NOTE]
>
>如需轉換PDF服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

若要將PDF檔案轉換為PostScript檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立轉換PDF服務用戶端。
1. 參考PDF檔案以轉換為PostScript檔案。
1. 設定轉換執行時期選項。
1. 將PDF檔案轉換為PostScript檔案。
1. 儲存PostScript檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立轉換PDF用戶端**

您必須先建立「轉換PDF」服務用戶端，才能以程式設計方式執行「轉換PDF」服務作業。 如果您使用Java API，請建立`ConvertPdfServiceClient`物件。 如果您使用web service API，請建立`ConvertPDFServiceService`物件。

本節使用AEM Forms推出的web service功能。 若要存取新功能，您必須使用`lc_version`屬性來建構您的Proxy物件。 (請參閱[使用Web Services](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)叫用AEM Forms中的「使用Web服務訪問新功能」。)

**參考PDF檔案以轉換為PostScript檔案**

參考您要轉換為PostScript檔案的PDF檔案。 如本主題前面所述，PDF檔案必須是非互動式PDF檔案。 如果您嘗試將互動式PDF檔案轉換為PostScript檔案，則會擲回例外。

**設定轉換執行時期選項**

將PDF檔案轉換為PostScript檔案時，您可以定義執行時期選項，以指定所建立的PostScript類型。 例如，您可以定義第3級PostScript檔案。

通常，產生的PostScript檔案會反映輸入PDF檔案的大小。 如果您選取`ShrinkToFit`選項（會縮小PostScript檔案的輸出以符合頁面），您將看不到輸入的PDF檔案與產生的PostScript檔案之間的差異。 `ShrinkToFit`選項只有在您選擇在比輸入PDF檔案小的頁面大小上列印時才生效。 要選擇較小的頁面大小，請定義`PageSize`選項。 此外，建議您將`RotateAndCenter`選項設為`true`以取得正確的PostScript輸出。

同樣地，如果您選取`ExpandToFit`選項（會展開PostScript檔案的輸出以符合頁面大小），則只有在您選擇列印的頁面大小大於輸入的PDF檔案時，才會生效。 要選擇較大的頁面大小，請定義`PageSize`選項。 此外，建議您將`RotateAndCenter`選項設為`true`以取得正確的PostScript輸出。

>[!NOTE]
>
>有關可設定的運行時值的資訊，請參閱[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToPSOptionsSpec`類參考。

**將PDF檔案轉換為PostScript檔案**

在您建立服務用戶端並設定執行時期選項後，就可以叫用PostScript轉換作業。 此操作將需要有關要轉換的文檔的資訊，包括目標文檔的首選PostScript級別。

**儲存PostScript檔案**

將PDF檔案轉換為PostScript後，您可將輸出儲存為PostScript檔案。

**另請參閱**

[使用Java API將PDF檔案轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[使用web service API將PDF檔案轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速入門](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API {#convert-a-pdf-document-to-ps-using-the-java-api}將PDF檔案轉換為PS

使用「轉換PDF服務API(Java)」將PDF檔案轉換為PostScript:

1. 包含專案檔案。

   將用戶端JAR檔案（例如adobe-convertpdf-client.jar）加入Java專案的類別路徑中。

1. 建立轉換PDF用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`ConvertPdfServiceClient`對象。

1. 參考PDF檔案以轉換為PostScript檔案。

   * 使用其建構函式建立`java.io.FileInputStream`物件，並傳遞指定要轉換之PDF檔案位置的字串值。
   * 使用`com.adobe.idp.Document`建構函式建立儲存PDF檔案的`com.adobe.idp.Document`物件。 傳遞包含PDF檔案的`java.io.FileInputStream`物件。

1. 設定轉換執行時期選項。

   * 通過調用`ToPSOptionsSpec`對象的建構子建立對象。
   * 通過調用屬於`ToPSOptionsSpec`對象的相應方法來設定運行時選項。 例如，若要定義所建立的PostScript層級，請叫用`ToPSOptionsSpec`物件的`setPsLevel`方法，並傳遞指定PostScript層級的`PSLevel`列舉值。 有關可設定的所有運行時值的資訊，請參閱[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToPSOptionsSpec`類參考。

1. 將PDF檔案轉換為PostScript檔案。

   叫用`ConvertPdfServiceClient`物件的`toPS2`方法並傳遞下列值：

   * `com.adobe.idp.Document`物件，代表要轉換為PostScript檔案的PDF檔案。
   * `ToPSOptionsSpec`物件，指定PostScript執行時期選項。

   `toPS2`方法返回包含新PostScript文檔的`Document`對象。

1. 儲存PostScript檔案。

   * 建立`java.io.File`物件，並確定副檔名為。ps。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製至檔案（請確定您使用`toPS2`方法傳回的`Document`物件）。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API將PDF檔案轉換為PostScript](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#convert-a-pdf-document-to-ps-using-the-web-service-api}將PDF檔案轉換為PS

使用「轉換PDF服務API」(web service)將PDF檔案轉換為PostScript:

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立轉換PDF用戶端。

   * 使用其預設建構子建立`ConvertPdfServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`ConvertPdfServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）。 您不需要使用`lc_version`屬性。 不過，請指定`?blob=mtom`。
   * 獲取`ConvertPdfServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考PDF檔案以轉換為PostScript檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存轉換為PostScript檔案的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要轉換的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並將位元組陣列、開始位置和串流長度傳遞給讀取，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 設定轉換執行時期選項。

   * 通過調用`ToPSOptionsSpec`對象的建構子建立對象。
   * 為`ToPSOptionsSpec`物件的資料成員指派值，以設定執行時期選項。 例如，若要定義所建立的PostScript層級，請為`ToPSOptionsSpec`物件的`psLevel`資料成員指派`PSLevel`列舉值。

1. 將PDF檔案轉換為PostScript檔案。

   叫用`GeneratePDFServiceService`物件的`toPS2`方法並傳遞下列值：

   * `BLOB`物件，代表要轉換為PostScript檔案的PDF檔案
   * 指定運行時選項的`ToPSOptionsSpec`對象

   轉換完成後，請存取其`BLOB`物件的`MTOM`屬性，以擷取代表PostScript檔案的二進位資料。 這會傳回一個位元組陣列，您可將其寫出至PostScript檔案。

1. 儲存PostScript檔案。

   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞代表PS檔案檔案位置的字串值。
   * 建立一個位元組陣列，用於儲存`encryptPDFUsingPassword`方法返回的`BLOB`對象的資料內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PostScript檔案。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將PDF檔案轉換為影像格式{#converting-pdf-documents-to-image-formats}

您可以使用「轉換PDF」服務，以程式設計方式將PDF檔案轉換為影像格式，包括JPEG、JPEG 2000、TIFF和PNG。 將PDF檔案轉換為影像檔案後，您就可將PDF檔案當成影像檔案使用。 例如，您可以將映像放置在企業內容管理系統中以進行儲存。

當將PDF檔案轉換為影像時，「轉換PDF」服務會針對檔案中的每個頁面建立個別的影像。 也就是說，如果檔案有20頁，「轉換PDF」服務會建立20個影像檔。 將PDF檔案轉換為影像格式時，您可以為PDF檔案內的每個頁面建立個別影像，或為整個PDF檔案建立單一影像檔。

>[!NOTE]
>
>如需轉換PDF服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}摘要

若要將PDF檔案轉換為任何支援的類型，請執行下列步驟：

1. 包含專案檔案。
1. 建立轉換PDF服務用戶端。
1. 擷取要轉換的PDF檔案。
1. 設定執行時期選項。
1. 將PDF轉換為影像。
1. 從系列擷取影像檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立轉換PDF用戶端**

您必須先建立「轉換PDF」服務用戶端，才能以程式設計方式執行「轉換PDF」服務作業。 如果您使用Java API，請建立`ConvertPdfServiceClient`物件。 如果您使用web service API，請建立`ConvertPDFServiceService`物件。

**擷取要轉換的PDF檔案**

您必須擷取PDF檔案才能轉換為影像。 您無法將互動式PDF檔案轉換為影像。 如果您嘗試這麼做，則會擲回例外。 若要將互動式PDF檔案轉換為影像檔，您必須先平面化PDF檔案，才能進行轉換。 （請參閱[平面化PDF檔案](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)。）

**設定執行時期選項**

您必須設定執行時期選項，例如影像格式和解析度值。 有關運行時值的資訊，請參閱[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToImageOptionsSpec`類參考。

**將PDF轉換為影像**

建立服務用戶端並設定執行時期選項後，您就可以將PDF檔案轉換為影像。 會傳回包含影像的系列物件。

**從系列擷取影像檔案**

您可以從轉換PDF服務傳回的系列物件擷取影像檔案。 系列中的每個元素都是一個`com.adobe.idp.Document`例項（若您使用web services，則為`BLOB`例項），您可將其儲存為影像檔案，例如JPG檔案。

影像檔案的格式取決於`ImageConvertFormat`執行時期選項。 也就是說，如果您將`ImageConvertFormat`執行時期選項設為`ImageConvertFormat.JPEG`，則可將影像檔案儲存為JPG檔案。

**另請參閱**

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速入門](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API {#convert-a-pdf-document-to-image-files-using-the-java-api}將PDF檔案轉換為影像檔

使用「轉換PDF服務API」(Java)，將PDF檔案轉換為影像格式：

1. 包含專案檔案。

   將用戶端JAR檔案（例如adobe-convertpdf-client.jar）加入Java專案的類別路徑中。

1. 建立轉換PDF用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`ConvertPdfServiceClient`對象。

1. 擷取要轉換的PDF檔案。

   * 使用PDF檔案的建構函式並傳遞指定PDF檔案位置的字串值，建立代表要轉換之PDF檔案的`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定執行時期選項。

   * 使用其建構子建立`ToImageOptionsSpec`對象。
   * 根據需要調用屬於此對象的方法。 例如，通過調用`setImageConvertFormat`方法並傳遞指定格式類型的`ImageConvertFormat`枚舉值來設定影像類型。

   >[!NOTE]
   >
   >必須設定`ImageConvertFormat`枚舉值。

1. 將PDF轉換為影像。

   叫用`ConvertPdfServiceClient`物件的`toImage2`方法並傳遞下列值：

   * 代表要轉換的PDF檔案的`com.adobe.idp.Document`物件。
   * `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec`物件，包含目標影像格式的各種偏好設定。

   `toImage2`方法返回包含影像的`java.util.List`對象。 系列中的每個元素都是`com.adobe.idp.Document`例項。

1. 從系列擷取影像檔案。

   重複`java.util.List`物件，以判斷影像是否存在。 每個元素都是`com.adobe.idp.Document`實例。 調用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`物件，以儲存影像。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將PDF檔案轉換為JPEG檔案](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 使用web service API {#convert-a-pdf-document-to-image-files-using-the-web-service-api}將PDF檔案轉換為影像檔

使用「轉換PDF服務API」(web service)，將PDF檔案轉換為影像格式：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立轉換PDF用戶端。

   * 使用其預設建構子建立`ConvertPdfServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`ConvertPdfServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）。 您不需要使用`lc_version`屬性。 不過，請指定`?blob=mtom`。
   * 獲取`ConvertPdfServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取要轉換的PDF檔案。

   * 使用其建構子建立`BLOB`對象。 此`BLOB`物件用來儲存PDF表單。
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，指定PDF表單的位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 取得`System.IO.FileStream`物件的`Length`屬性，以決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 設定執行時期選項。

   * 使用其建構子建立`ToImageOptionsSpec`對象。
   * 根據需要調用屬於此對象的方法。 例如，通過調用`setImageConvertFormat`方法並傳遞指定格式類型的`ImageConvertFormat`枚舉值來設定影像類型。

   >[!NOTE]
   >
   >必須設定`ImageConvertFormat`枚舉值。

1. 將PDF轉換為影像。

   叫用`ConvertPDFServiceService`物件的`toImage2`方法並傳遞下列值：

   * `BLOB`物件，代表要轉換的檔案
   * `ToImageOptionsSpec`物件，包含目標影像格式的各種偏好設定

   `toImage2`方法返回包含新建映像檔案的`MyArrayOfBLOB`對象。

1. 從系列擷取影像檔案。

   * 通過獲取`Count`欄位的值，確定`MyArrayOfBLOB`對象中的元素數。 每個元素都是包含影像的`BLOB`物件。
   * 重複`MyArrayOfBLOB`物件並儲存每個影像檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
