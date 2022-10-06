---
title: 將PDF轉換為Postscript和影像檔案
seo-title: Converting PDF to Postscript andImage Files
description: 使用「轉換PDF」服務，使用Java API和Web服務API，將PDF文檔轉換為PostScript和多種影像格式(JPEG、JPEG2000、PNG和TIFF)。
seo-description: Use the Convert PDF service to convert PDF documents to PostScript and to a number of image formats (JPEG, JPEG 2000, PNG, and TIFF) using the Java API and Web Service API.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2809'
ht-degree: 0%

---

# 將PDF轉換為Postscript和影像檔案 {#converting-pdf-to-postscript-andimage-files}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於轉換PDF服務**

「轉換PDF」服務將PDF文檔轉換為PostScript和多種影像格式(JPEG、JPEG2000、PNG和TIFF)。 將PDF文檔轉換為PostScript對於在任何PostScript打印機上基於伺服器的無人值守打印非常有用。 將PDF文檔轉換為多頁TIFF檔案對於在不支援PDF文檔的內容管理系統中歸檔文檔非常實用。

您可以使用「轉換PDF」服務來完成下列工作：

* 將PDF文檔轉換為PostScript。
* 將PDF文檔轉換為影像格式。

>[!NOTE]
>
>如需「轉換PDF」服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將PDF文檔轉換為PostScript {#converting-pdf-documents-to-postscript}

本主題說明如何使用「轉換PDF服務API」（Java和Web服務），以程式設計方式將PDF檔案轉換為PostScript檔案。 轉換為PostScript檔案的PDF文檔必須是非互動式PDF文檔。 也就是說，如果嘗試將互動式PDF文檔轉換為PostScript檔案，則會引發異常。

>[!NOTE]
>
>如需「轉換PDF」服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要將PDF文檔轉換為PostScript檔案，請執行以下步驟：

1. 包含專案檔案。
1. 建立轉換PDF服務客戶端。
1. 參考PDF文檔以轉換為PostScript檔案。
1. 設定轉換執行時間選項。
1. 將PDF文檔轉換為PostScript檔案。
1. 儲存PostScript檔案。

**包含項目檔案**

將必要的檔案納入您的開發專案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立轉換PDF客戶端**

在以寫程式方式執行「轉換PDF」服務操作之前，必須建立「轉換PDF」服務客戶端。 如果您使用Java API，請建立 `ConvertPdfServiceClient` 物件。 如果您使用網站服務API，請建立 `ConvertPDFServiceService` 物件。

本節使用AEM Forms中推出的網站服務功能。 若要存取新功能，您必須使用 `lc_version` 屬性。 (請參閱以下主題中的「使用網站服務存取新功能」： [使用Web服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**參考PDF文檔以轉換為PostScript檔案**

參考要轉換為PostScript檔案的PDF文檔。 如本主題前面所述，PDF文檔必須是非互動式PDF文檔。 如果嘗試將互動式PDF文檔轉換為PostScript檔案，則會引發異常。

**設定轉換執行時間選項**

將PDF文檔轉換為PostScript檔案時，您可以定義運行時選項，以指定所建立的PostScript類型。 例如，您可以定義第3層PostScript檔案。

一般而言，產生的PostScript檔案會反映輸入PDF檔案的大小。 如果您選取 `ShrinkToFit` 選項（該選項會縮小PostScript檔案的輸出以適合頁面），您將不會看到輸入PDF文檔與生成的PostScript檔案之間的差異。 此 `ShrinkToFit` 選項只有在選擇打印的頁面大小比輸入PDF文檔小時才生效。 若要選取較小的頁面大小，請定義 `PageSize` 選項。 此外，建議您將 `RotateAndCenter` 選項 `true` 以獲得正確的PostScript輸出。

同樣地，若您選取 `ExpandToFit` 選項（它擴展了PostScript檔案的輸出以適合頁面大小），只有當您選擇打印的頁面大小比輸入PDF文檔大時，它才生效。 若要選取較大的頁面大小，請定義 `PageSize` 選項。 此外，建議您將 `RotateAndCenter` 選項 `true` 以獲得正確的PostScript輸出。

>[!NOTE]
>
>如需可設定的執行階段值相關資訊，請參閱 `ToPSOptionsSpec` 類引用 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**將PDF文檔轉換為PostScript檔案**

建立服務客戶端並設定運行時選項後，可以調用PostScript轉換操作。 此操作需要有關要轉換的文檔的資訊，包括目標文檔的首選PostScript級別。

**儲存PostScript檔案**

將PDF文檔轉換為PostScript後，可以將輸出另存為PostScript檔案。

**另請參閱**

[使用Java API將PDF文檔轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[使用Web服務API將PDF文檔轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速入門](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF文檔轉換為PS {#convert-a-pdf-document-to-ps-using-the-java-api}

使用「轉換PDF服務API」(Java)將PDF文檔轉換為PostScript:

1. 包含專案檔案。

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-convertpdf-client.jar。

1. 建立轉換PDF客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `ConvertPdfServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 參考PDF文檔以轉換為PostScript檔案。

   * 建立 `java.io.FileInputStream` 對象，使用其建構子並傳遞一個字串值，該字串值指定要轉換的PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 用於儲存PDF文檔的對象，方法是使用 `com.adobe.idp.Document` 建構子。 傳遞 `java.io.FileInputStream` 包含PDF文檔的對象。

1. 設定轉換執行時間選項。

   * 建立 `ToPSOptionsSpec` 對象，方法是調用其建構子。
   * 調用屬於的適當方法，以設定執行時選項 `ToPSOptionsSpec` 物件。 例如，要定義已建立的PostScript級別，請調用 `ToPSOptionsSpec` 物件 `setPsLevel` 方法和傳遞 `PSLevel` 指定PostScript級別的枚舉值。 如需可設定之所有執行階段值的相關資訊，請參閱 `ToPSOptionsSpec` 類引用 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 將PDF文檔轉換為PostScript檔案。

   叫用 `ConvertPdfServiceClient`物件 `toPS2` 方法，並傳遞下列值：

   * A `com.adobe.idp.Document` 表示要轉換為PostScript檔案的PDF文檔的對象。
   * A `ToPSOptionsSpec` 指定PostScript運行時選項的對象。

   此 `toPS2` 方法傳回 `Document` 包含新PostScript文檔的對象。

1. 儲存PostScript檔案。

   * 建立 `java.io.File` 物件，並確定副檔名為.ps。
   * 叫用 `Document` 物件 `copyToFile` 複製內容的方法 `Document` 物件(請確定您使用 `Document` 由傳回的物件 `toPS2` 方法)。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API將PDF檔案轉換為PostScript](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將PDF文檔轉換為PS {#convert-a-pdf-document-to-ps-using-the-web-service-api}

使用「轉換PDF服務API」（Web服務）將PDF文檔轉換為PostScript:

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立轉換PDF客戶端。

   * 建立 `ConvertPdfServiceClient` 物件，使用其預設建構函式。
   * 建立 `ConvertPdfServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 不過，請指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `ConvertPdfServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參考PDF文檔以轉換為PostScript檔案。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存轉換為PostScript檔案的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子，並傳遞一個字串值，該字串值表示要轉換的PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法及傳遞位元組陣列、起始位置及資料流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 設定轉換執行時間選項。

   * 建立 `ToPSOptionsSpec` 對象，方法是調用其建構子。
   * 為 `ToPSOptionsSpec` 對象的資料成員。 例如，若要定義所建立的PostScript層級，請指派 `PSLevel` 枚舉值 `ToPSOptionsSpec` 物件 `psLevel` 資料成員。

1. 將PDF文檔轉換為PostScript檔案。

   叫用 `GeneratePDFServiceService` 物件 `toPS2` 方法，並傳遞下列值：

   * A `BLOB` 表示要轉換為PostScript檔案的PDF文檔的對象
   * A `ToPSOptionsSpec` 指定運行時選項的對象

   轉換完成後，通過訪問PostScript文檔來提取代表該文檔的二進位資料 `BLOB` 物件 `MTOM` 屬性。 這會傳回位元組陣列，您可將其寫出至PostScript檔案。

1. 儲存PostScript檔案。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞代表PS檔案檔案位置的字串值。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `encryptPDFUsingPassword` 方法。 取得 `BLOB` 物件 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將PDF文檔轉換為影像格式 {#converting-pdf-documents-to-image-formats}

您可以使用「轉換PDF」服務，以寫程式方式將PDF文檔轉換為影像格式，包括JPEG、JPEG2000、TIFF和PNG。 通過將PDF文檔轉換為影像檔案，可以將PDF文檔用作影像檔案。 例如，您可以將映像放置在企業內容管理系統中以進行儲存。

將PDF文檔轉換為影像時，「轉換PDF」服務將為文檔中的每個頁面建立單獨的影像。 也就是說，如果文檔有20頁，則「轉換PDF」服務將建立20個影像檔案。 將PDF文檔轉換為影像格式時，可以為PDF文檔內的每個頁面建立單個影像，也可以為整個PDF文檔建立單個影像檔案。

>[!NOTE]
>
>如需「轉換PDF」服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

要將PDF文檔轉換為任何支援的類型，請執行以下步驟：

1. 包含專案檔案。
1. 建立轉換PDF服務客戶端。
1. 檢索要轉換的PDF文檔。
1. 設定運行時選項。
1. 將PDF轉換為影像。
1. 從集合中擷取影像檔案。

**包含項目檔案**

將必要的檔案納入您的開發專案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立轉換PDF客戶端**

在以寫程式方式執行「轉換PDF」服務操作之前，必須建立「轉換PDF」服務客戶端。 如果您使用Java API，請建立 `ConvertPdfServiceClient` 物件。 如果您使用網站服務API，請建立 `ConvertPDFServiceService` 物件。

**檢索要轉換的PDF文檔**

必須檢索PDF文檔才能轉換為影像。 無法將互動式PDF文檔轉換為影像。 如果嘗試執行此操作，則會擲回例外。 要將互動式PDF文檔轉換為影像檔案，必須先平面化PDF文檔，然後再進行轉換。 (請參閱 [拼合PDF文檔](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**設定運行時選項**

必須設定運行時選項，如影像格式和解析度值。 如需執行時值的相關資訊，請參閱 `ToImageOptionsSpec` 類引用 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**將PDF轉換為影像**

建立服務客戶端並設定運行時選項後，可以將PDF文檔轉換為影像。 會傳回包含影像的集合物件。

**從集合中擷取影像檔案**

您可以從轉換PDF服務傳回的集合物件擷取影像檔案。 集合中的每個元素都是 `com.adobe.idp.Document` 例項(或 `BLOB` 例項（若您使用web服務），可儲存為影像檔案，例如JPG檔案。

影像檔案的格式取決於 `ImageConvertFormat` 執行時選項。 也就是說，若您設定 `ImageConvertFormat` 運行時選項 `ImageConvertFormat.JPEG`，您可以將影像檔案儲存為JPG檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速入門](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF檔案轉換為影像檔案 {#convert-a-pdf-document-to-image-files-using-the-java-api}

使用「轉換PDF服務API(Java)」將PDF文檔轉換為影像格式：

1. 包含專案檔案。

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-convertpdf-client.jar。

1. 建立轉換PDF客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `ConvertPdfServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索要轉換的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示要轉換的PDF文檔的對象，方法是使用其建構子並傳遞指定PDF文檔位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 設定運行時選項。

   * 建立 `ToImageOptionsSpec` 物件，使用其建構子。
   * 根據需要調用屬於此對象的方法。 例如，借由叫用 `setImageConvertFormat` 方法並傳遞 `ImageConvertFormat` 指定格式類型的枚舉值。

   >[!NOTE]
   >
   >設定 `ImageConvertFormat` 枚舉值是必需的。

1. 將PDF轉換為影像。

   叫用 `ConvertPdfServiceClient` 物件 `toImage2` 方法，並傳遞下列值：

   * A `com.adobe.idp.Document` 表示要轉換的PDF檔案的對象。
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` 包含有關目標影像格式的各種首選項的對象。

   此 `toImage2` 方法傳回 `java.util.List` 包含影像的物件。 集合中的每個元素都是 `com.adobe.idp.Document` 例項。

1. 從集合中擷取影像檔案。

   重複 `java.util.List` 物件，以判斷影像是否存在。 每個元素都是 `com.adobe.idp.Document` 例項。 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法和傳遞 `java.io.File` 物件。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將PDF檔案轉換為JPEG檔案](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 使用Web服務API將PDF文檔轉換為影像檔案 {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

使用「轉換PDF服務API（Web服務）」將PDF文檔轉換為影像格式：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立轉換PDF客戶端。

   * 建立 `ConvertPdfServiceClient` 物件，使用其預設建構函式。
   * 建立 `ConvertPdfServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 不過，請指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `ConvertPdfServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 檢索要轉換的PDF文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 物件可用來儲存PDF表單。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，指定PDF表單的位置，以及在中開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 透過取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 設定運行時選項。

   * 建立 `ToImageOptionsSpec` 物件，使用其建構子。
   * 根據需要調用屬於此對象的方法。 例如，借由叫用 `setImageConvertFormat` 方法並傳遞 `ImageConvertFormat` 指定格式類型的枚舉值。

   >[!NOTE]
   >
   >設定 `ImageConvertFormat` 枚舉值是必需的。

1. 將PDF轉換為影像。

   叫用 `ConvertPDFServiceService` 物件 `toImage2` 方法，並傳遞下列值：

   * A `BLOB` 表示要轉換的檔案的對象
   * A `ToImageOptionsSpec` 包含有關目標影像格式的各種首選項的對象

   此 `toImage2` 方法傳回 `MyArrayOfBLOB` 包含新建立的影像檔案的對象。

1. 從集合中擷取影像檔案。

   * 決定 `MyArrayOfBLOB` 物件，方法是取得其值 `Count` 欄位。 每個元素都是 `BLOB` 包含影像的物件。
   * 重複 `MyArrayOfBLOB` 物件，並儲存每個影像檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
