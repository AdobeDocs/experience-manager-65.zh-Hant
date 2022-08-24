---
title: 將PDF轉換為Postscript和Image檔案
seo-title: Converting PDF to Postscript andImage Files
description: 使用「轉換PDF」服務，可以使用Java API和Web服務API將PDF文檔轉換為PostScript和多種影像格式(JPEG、JPEG2000、PNG和TIFF)。
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

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於轉換PDF服務**

「轉換PDF」服務將PDF文檔轉換為PostScript和多種影像格式(JPEG、JPEG2000、PNG和TIFF)。 將PDF文檔轉換為PostScript對於在任何PostScript打印機上基於伺服器的無人參與打印都非常有用。 將PDF文檔轉換為多頁TIFF檔案在不支援PDF文檔的內容管理系統中存檔文檔時非常實用。

您可以使用轉換PDF服務完成以下任務：

* 將PDF文檔轉換為PostScript。
* 將PDF文檔轉換為影像格式。

>[!NOTE]
>
>有關轉換PDF服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PDF文檔轉換為PostScript {#converting-pdf-documents-to-postscript}

本主題介紹如何使用轉換PDF服務API（Java和Web服務）以寫程式方式將PDF文檔轉換為PostScript檔案。 轉換為PostScript檔案的PDF文檔必須是非互動式PDF文檔。 即，如果嘗試將互動式PDF文檔轉換為PostScript檔案，則會引發異常。

>[!NOTE]
>
>有關轉換PDF服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要將PDF文檔轉換為PostScript檔案，請執行以下步驟：

1. 包括項目檔案。
1. 建立轉換PDF服務客戶端。
1. 引用PDF文檔以轉換為PostScript檔案。
1. 設定轉換運行時選項。
1. 將PDF文檔轉換為PostScript檔案。
1. 保存PostScript檔案。

**包括項目檔案**

將必要的檔案包括到您的開發項目中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立轉換PDF客戶端**

在以寫程式方式執行轉換PDF服務操作之前，必須建立轉換PDF服務客戶端。 如果使用Java API，請建立 `ConvertPdfServiceClient` 的雙曲餘切值。 如果使用Web服務API，請建立 `ConvertPDFServiceService` 的雙曲餘切值。

本節使用在AEM Forms引入的Web服務功能。 要訪問新功能，必須使用 `lc_version` 屬性。 (請參閱中的「使用Web服務訪問新功能」 [使用Web服務調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)。)

**引用PDF文檔以轉換為PostScript檔案**

引用要轉換為PostScript檔案的PDF文檔。 如本主題前面所述，PDF文檔必須是非互動式PDF文檔。 如果嘗試將互動式PDF文檔轉換為PostScript檔案，則會引發異常。

**設定轉換運行時選項**

將PDF文檔轉換為PostScript檔案時，可以定義指定所建立的PostScript類型的運行時選項。 例如，可以定義級別3的PostScript檔案。

通常，生成的PostScript檔案將反映輸入PDF文檔的大小。 如果選擇 `ShrinkToFit` 選項（它收縮PostScript檔案的輸出以適合頁面），您將看不到輸入PDF文檔與生成的PostScript檔案之間的差異。 的 `ShrinkToFit` 選項僅在選擇以比輸入PDF文檔小的頁面大小打印時生效。 要選擇較小的頁面大小，請定義 `PageSize` 的雙曲餘切值。 此外，建議您 `RotateAndCenter` 選項 `true` 獲取正確的PostScript輸出。

同樣，如果您選擇 `ExpandToFit` 選項（將展開PostScript檔案的輸出以適合頁面），僅當選擇在比輸入PDF文檔大的頁面大小上打印時才生效。 要選擇較大的頁面大小，請定義 `PageSize` 的雙曲餘切值。 此外，建議您 `RotateAndCenter` 選項 `true` 獲取正確的PostScript輸出。

>[!NOTE]
>
>有關可設定的運行時值的資訊，請參閱 `ToPSOptionsSpec` 類引用 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**將PDF文檔轉換為PostScript檔案**

建立服務客戶端並設定運行時選項後，可以調用PostScript轉換操作。 此操作將需要有關要轉換的文檔的資訊，包括目標文檔的首選PostScript級別。

**保存PostScript檔案**

將PDF文檔轉換為PostScript後，可將輸出另存為PostScript檔案。

**另請參閱**

[使用Java API將PDF文檔轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[使用Web服務API將PDF文檔轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速啟動](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF文檔轉換為PS {#convert-a-pdf-document-to-ps-using-the-java-api}

使用「轉換PDF服務API(Java)」將PDF文檔轉換為PostScript:

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-convertpdf-client.jar。

1. 建立轉換PDF客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `ConvertPdfServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用PDF文檔以轉換為PostScript檔案。

   * 建立 `java.io.FileInputStream` 對象，並傳遞一個字串值，該字串值指定要轉換的PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用PDF `com.adobe.idp.Document` 建構子。 通過 `java.io.FileInputStream` 包含PDF文檔的對象。

1. 設定轉換運行時選項。

   * 建立 `ToPSOptionsSpec` 調用其建構子。
   * 通過調用屬於 `ToPSOptionsSpec` 的雙曲餘切值。 例如，要定義所建立的PostScript級別，請調用 `ToPSOptionsSpec` 對象 `setPsLevel` 方法和通過 `PSLevel` 指定PostScript級別的枚舉值。 有關可設定的所有運行時值的資訊，請參閱 `ToPSOptionsSpec` 類引用 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 將PDF文檔轉換為PostScript檔案。

   調用 `ConvertPdfServiceClient`對象 `toPS2` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示要轉換為PostScript檔案的PDF文檔的對象。
   * A `ToPSOptionsSpec` 指定PostScript運行時選項的對象。

   的 `toPS2` 方法返回 `Document` 包含新PostScript文檔的對象。

1. 保存PostScript檔案。

   * 建立 `java.io.File` 對象，並確保檔案副檔名為.ps。
   * 調用 `Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象到檔案(確保 `Document` 返回的對象 `toPS2` )。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API將PDF文檔轉換為PostScript](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將PDF文檔轉換為PS {#convert-a-pdf-document-to-ps-using-the-web-service-api}

使用「轉換PDF服務API（Web服務）」將PDF文檔轉換為PostScript:

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立轉換PDF客戶端。

   * 建立 `ConvertPdfServiceClient` 對象。
   * 建立 `ConvertPdfServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`。) 你不需要 `lc_version` 屬性。 但是，請指定 `?blob=mtom`。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `ConvertPdfServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用PDF文檔以轉換為PostScript檔案。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存轉換為PostScript檔案的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示要轉換的PDF文檔的檔案位置，以及在中開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置、流長度等傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 設定轉換運行時選項。

   * 建立 `ToPSOptionsSpec` 調用其建構子。
   * 通過為 `ToPSOptionsSpec` 對象的資料成員。 例如，要定義所建立的PostScript級別，請分配 `PSLevel` 枚舉值 `ToPSOptionsSpec` 對象 `psLevel` 資料成員。

1. 將PDF文檔轉換為PostScript檔案。

   調用 `GeneratePDFServiceService` 對象 `toPS2` 方法並傳遞以下值：

   * A `BLOB` 表示要轉換為PostScript檔案的PDF文檔的對象
   * A `ToPSOptionsSpec` 指定運行時選項的對象

   轉換完成後，通過訪問代表PostScript文檔的二進位資料 `BLOB` 對象 `MTOM` 屬性。 這將返回一個位元組陣列，您可以將其寫出到PostScript檔案。

1. 保存PostScript檔案。

   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個表示PS檔案的檔案位置的字串值。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `encryptPDFUsingPassword` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 的子菜單。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將PDF文檔轉換為影像格式 {#converting-pdf-documents-to-image-formats}

可以使用「轉換PDF」服務以寫程式方式將PDF文檔轉換為影像格式，包括JPEG、JPEG2000、TIFF和PNG。 通過將PDF文檔轉換為影像檔案，可以將PDF文檔用作影像檔案。 例如，可以將映像放在企業內容管理系統中進行儲存。

將PDF文檔轉換為影像時，「轉換PDF」服務將為文檔中的每個頁面建立單獨的影像。 即，如果文檔有20頁，則轉換PDF服務將建立20個影像檔案。 將PDF文檔轉換為影像格式時，可以為PDF文檔內的每個頁面建立單個影像，或為整個PDF文檔建立單個影像檔案。

>[!NOTE]
>
>有關轉換PDF服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要將PDF文檔轉換為任何受支援的類型，請執行以下步驟：

1. 包括項目檔案。
1. 建立轉換PDF服務客戶端。
1. 檢索要轉換的PDF文檔。
1. 設定運行時選項。
1. 將PDF轉換為影像。
1. 從集合中檢索影像檔案。

**包括項目檔案**

將必要的檔案包括到您的開發項目中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立轉換PDF客戶端**

在以寫程式方式執行轉換PDF服務操作之前，必須建立轉換PDF服務客戶端。 如果使用Java API，請建立 `ConvertPdfServiceClient` 的雙曲餘切值。 如果使用Web服務API，請建立 `ConvertPDFServiceService` 的雙曲餘切值。

**檢索要轉換的PDF文檔**

必須檢索PDF文檔才能轉換為影像。 無法將互動式PDF文檔轉換為影像。 如果嘗試執行此操作，則會引發異常。 要將互動式PDF文檔轉換為影像檔案，必須先平整PDF文檔，然後才能轉換它。 (請參閱 [拼合PDF文檔](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)。)

**設定運行時選項**

必須設定運行時選項，如影像格式和解析度值。 有關運行時值的資訊，請參見 `ToImageOptionsSpec` 類引用 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**將PDF轉換為影像**

在建立服務客戶端並設定運行時選項後，可以將PDF文檔轉換為影像。 返回包含影像的集合對象。

**從集合中檢索影像檔案**

可以從ConvertPDF服務返回的集合對象檢索影像檔案。 集合中的每個元素都是 `com.adobe.idp.Document` 實例(或 `BLOB` 實例（如果您使用Web服務），則可以另存為影像檔案，如JPG檔案。

影像檔案的格式取決於 `ImageConvertFormat` 運行時選項。 也就是說，如果你 `ImageConvertFormat` 運行時選項到 `ImageConvertFormat.JPEG`，可以將影像檔案另存為JPG檔案。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速啟動](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF文檔轉換為影像檔案 {#convert-a-pdf-document-to-image-files-using-the-java-api}

使用「轉換PDF服務API(Java)」將PDF文檔轉換為影像格式：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-convertpdf-client.jar。

1. 建立轉換PDF客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `ConvertPdfServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索要轉換的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示要轉換的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定運行時選項。

   * 建立 `ToImageOptionsSpec` 對象。
   * 根據需要調用屬於此對象的方法。 例如，通過調用 `setImageConvertFormat` 方法和傳遞 `ImageConvertFormat` 指定格式類型的枚舉值。

   >[!NOTE]
   >
   >設定 `ImageConvertFormat` 枚舉值是必需的。

1. 將PDF轉換為影像。

   調用 `ConvertPdfServiceClient` 對象 `toImage2` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示要轉換的PDF檔案的對象。
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` 包含有關目標影像格式的各種首選項的對象。

   的 `toImage2` 方法返回 `java.util.List` 包含影像的對象。 集合中的每個元素都是 `com.adobe.idp.Document` 實例。

1. 從集合中檢索影像檔案。

   迭代 `java.util.List` 確定影像是否存在的對象。 每個元素都是 `com.adobe.idp.Document` 實例。 通過調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法和通過 `java.io.File` 的雙曲餘切值。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API將PDF文檔轉換為JPEG檔案](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 使用Web服務API將PDF文檔轉換為影像檔案 {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

使用「轉換PDF服務API（Web服務）」將PDF文檔轉換為影像格式：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立轉換PDF客戶端。

   * 建立 `ConvertPdfServiceClient` 對象。
   * 建立 `ConvertPdfServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`。) 你不需要 `lc_version` 屬性。 但是，請指定 `?blob=mtom`。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `ConvertPdfServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 檢索要轉換的PDF文檔。

   * 建立 `BLOB` 對象。 此 `BLOB` 對象用於儲存PDF窗體。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值指定PDF表單的位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 設定運行時選項。

   * 建立 `ToImageOptionsSpec` 對象。
   * 根據需要調用屬於此對象的方法。 例如，通過調用 `setImageConvertFormat` 方法和傳遞 `ImageConvertFormat` 指定格式類型的枚舉值。

   >[!NOTE]
   >
   >設定 `ImageConvertFormat` 枚舉值是必需的。

1. 將PDF轉換為影像。

   調用 `ConvertPDFServiceService` 對象 `toImage2` 方法並傳遞以下值：

   * A `BLOB` 表示要轉換的檔案的對象
   * A `ToImageOptionsSpec` 包含有關目標影像格式的各種首選項的對象

   的 `toImage2` 方法返回 `MyArrayOfBLOB` 包含新建立的影像檔案的對象。

1. 從集合中檢索影像檔案。

   * 確定 `MyArrayOfBLOB` 通過獲取其值 `Count` 的子菜單。 每個元素都是 `BLOB` 包含影像的對象。
   * 迭代 `MyArrayOfBLOB` 對象並保存每個影像檔案。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
