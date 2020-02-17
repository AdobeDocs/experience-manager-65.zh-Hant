---
title: 將PDF轉換為Postscript和影像檔案
seo-title: 將PDF轉換為Postscript和影像檔案
description: 'null'
seo-description: 'null'
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# 將PDF轉換為Postscript和影像檔案 {#converting-pdf-to-postscript-andimage-files}

**關於轉換PDF服務**

「轉換PDF」服務會將PDF檔案轉換為PostScript和多種影像格式（JPEG、JPEG 2000、PNG和TIFF）。 將PDF檔案轉換為PostScript對於在任何PostScript印表機上以伺服器為基礎的無人值守列印十分有用。 在不支援PDF檔案的內容管理系統中封存檔案時，將PDF檔案轉換為多頁TIFF檔案十分實用。

您可以使用「轉換PDF」服務完成下列工作：

* 將PDF檔案轉換為PostScript。
* 將PDF檔案轉換為影像格式。

   ***注意&#x200B;**:如需轉換PDF服務的詳細資訊，請參閱「AEM表[單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。*

## 將PDF檔案轉換為PostScript {#converting-pdf-documents-to-postscript}

本主題說明如何使用轉換PDF服務API（Java和web service），以程式設計方式將PDF檔案轉換為PostScript檔案。 轉換為PostScript檔案的PDF檔案必須是非互動式PDF檔案。 也就是說，如果您嘗試將互動式PDF檔案轉換為PostScript檔案，則會擲回例外。

>[!NOTE]
>
>如需轉換PDF服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

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

您必須先建立「轉換PDF」服務用戶端，才能以程式設計方式執行「轉換PDF」服務作業。 如果您使用Java API，請建立物 `ConvertPdfServiceClient` 件。 如果您使用web service API，請建立物 `ConvertPDFServiceService` 件。

本節使用AEM Forms中引進的Web服務功能。 若要存取新功能，您必須使用屬性來建構您的Proxy物 `lc_version` 件。 (請參閱「使用Web services叫用AEM Forms」中的「使 [用Web Services存取新功能](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)」)。

**參考PDF檔案以轉換為PostScript檔案**

參考您要轉換為PostScript檔案的PDF檔案。 如本主題前面所述，PDF檔案必須是非互動式PDF檔案。 如果您嘗試將互動式PDF檔案轉換為PostScript檔案，則會擲回例外。

**設定轉換執行時期選項**

將PDF檔案轉換為PostScript檔案時，您可以定義執行時期選項，以指定所建立的PostScript類型。 例如，您可以定義第3級PostScript檔案。

通常，產生的PostScript檔案會反映輸入PDF檔案的大小。 如果您選取 `ShrinkToFit` 選項（縮小PostScript檔案的輸出以符合頁面），您將不會看到輸入的PDF檔案與產生的PostScript檔案有任何不同。 只有在 `ShrinkToFit` 您選擇在比輸入PDF檔案小的頁面尺寸上列印時，此選項才會生效。 要選擇較小的頁面大小，請定義選 `PageSize` 項。 此外，建議您將選項設 `RotateAndCenter` 定為 `true` 取得正確的PostScript輸出。

同樣地，如果您選 `ExpandToFit` 取選項（會展開PostScript檔案的輸出以符合頁面大小），則只有在您選擇列印的頁面大小大於輸入的PDF檔案時，此選項才生效。 若要選取較大的頁面大小，請定義 `PageSize` 選項。 此外，建議您將選項設 `RotateAndCenter` 定為 `true` 取得正確的PostScript輸出。

>[!NOTE]
>
>如需您可設定之執行時期值的詳細資訊，請參閱 `ToPSOptionsSpec`[AEM Forms API參考中的類別參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**將PDF檔案轉換為PostScript檔案**

在您建立服務用戶端並設定執行時期選項後，就可以叫用PostScript轉換作業。 此操作將需要有關要轉換的文檔的資訊，包括目標文檔的首選PostScript級別。

**儲存PostScript檔案**

將PDF檔案轉換為PostScript後，您可將輸出儲存為PostScript檔案。

**另請參閱**

[使用Java API將PDF檔案轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[使用web service API將PDF檔案轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速入門](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF檔案轉換為PS {#convert-a-pdf-document-to-ps-using-the-java-api}

使用「轉換PDF服務API(Java)」將PDF檔案轉換為PostScript:

1. 包含專案檔案。

   將用戶端JAR檔案（例如adobe-convertpdf-client.jar）加入Java專案的類別路徑中。

1. 建立轉換PDF用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `ConvertPdfServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考PDF檔案以轉換為PostScript檔案。

   * 使用 `java.io.FileInputStream` 其建構函式建立物件，並傳遞指定PDF檔案轉換位置的字串值。
   * 使用 `com.adobe.idp.Document` 建構函式建立儲存PDF檔案的物 `com.adobe.idp.Document` 件。 傳遞包 `java.io.FileInputStream` 含PDF檔案的物件。

1. 設定轉換執行時期選項。

   * 通過調用 `ToPSOptionsSpec` 其建構子建立對象。
   * 通過調用屬於對象的適當方法來設定運行時 `ToPSOptionsSpec` 選項。 例如，若要定義所建立的PostScript層級，請叫 `ToPSOptionsSpec` 用物件的 `setPsLevel` 方法，並傳遞指定 `PSLevel` PostScript層級的列舉值。 如需您可設定的所有執行時期值的詳細資訊，請參閱 `ToPSOptionsSpec`[AEM Forms API參考中的類別參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 將PDF檔案轉換為PostScript檔案。

   叫用物 `ConvertPdfServiceClient`件的方 `toPS2` 法並傳遞下列值：

   * 表示 `com.adobe.idp.Document` 要轉換為PostScript檔案的PDF檔案的物件。
   * 指定 `ToPSOptionsSpec` PostScript執行時間選項的物件。
   此方 `toPS2` 法會傳回包 `Document` 含新PostScript檔案的物件。

1. 儲存PostScript檔案。

   * 建立物 `java.io.File` 件，並確定副檔名為。ps。
   * 叫用 `Document` 物件的方 `copyToFile` 法，將物件的內容複製至檔案(請確定您使用 `Document` 由方法傳回的物 `Document``toPS2` 件)。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API將PDF檔案轉換為PostScript](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API將PDF檔案轉換為PS {#convert-a-pdf-document-to-ps-using-the-web-service-api}

使用「轉換PDF服務API」(web service)將PDF檔案轉換為PostScript:

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立轉換PDF用戶端。

   * 使用其 `ConvertPdfServiceClient` 預設建構函式建立物件。
   * 使用建 `ConvertPdfServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`。)您不需要使用屬 `lc_version` 性。 不過，請指定 `?blob=mtom`。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `ConvertPdfServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 參考PDF檔案以轉換為PostScript檔案。

   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用於儲存轉換為PostScript檔案的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示要轉換的PDF文檔的檔案位置，以及在中開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，並將位元組陣列、 `System.IO.FileStream` 起始位置 `Read` 和串流長度傳遞給讀取，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 設定轉換執行時期選項。

   * 通過調用 `ToPSOptionsSpec` 其建構子建立對象。
   * 為物件的資料成員指派值，以設定 `ToPSOptionsSpec` 執行時期選項。 例如，若要定義所建立的PostScript層級，請為物 `PSLevel` 件的資料成 `ToPSOptionsSpec` 員指派列舉 `psLevel` 值。

1. 將PDF檔案轉換為PostScript檔案。

   叫用物 `GeneratePDFServiceService` 件的方 `toPS2` 法並傳遞下列值：

   * 表示 `BLOB` 要轉換為PostScript檔案的PDF檔案的物件
   * 指定 `ToPSOptionsSpec` 運行時選項的對象
   轉換完成後，請存取PostScript檔案的物件屬性，以擷取代表PostScript文 `BLOB` 件的二進位 `MTOM` 資料。 這會傳回一個位元組陣列，您可將其寫出至PostScript檔案。

1. 儲存PostScript檔案。

   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞代表PS檔案檔案位置的字串值。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `encryptPDFUsingPassword` 容。 取得物件欄位的值，以填入 `BLOB` 位元組陣 `MTOM` 列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PostScript檔案。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將PDF檔案轉換為影像格式 {#converting-pdf-documents-to-image-formats}

您可以使用「轉換PDF」服務，以程式設計方式將PDF檔案轉換為影像格式，包括JPEG、JPEG 2000、TIFF和PNG。 將PDF檔案轉換為影像檔案後，您就可將PDF檔案當成影像檔案使用。 例如，您可以將映像放置在企業內容管理系統中以進行儲存。

當將PDF檔案轉換為影像時，「轉換PDF」服務會針對檔案中的每個頁面建立個別的影像。 也就是說，如果檔案有20頁，「轉換PDF」服務會建立20個影像檔。 將PDF檔案轉換為影像格式時，您可以為PDF檔案內的每個頁面建立個別影像，或為整個PDF檔案建立單一影像檔。

>[!NOTE]
>
>如需轉換PDF服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

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

您必須先建立「轉換PDF」服務用戶端，才能以程式設計方式執行「轉換PDF」服務作業。 如果您使用Java API，請建立物 `ConvertPdfServiceClient` 件。 如果您使用web service API，請建立物 `ConvertPDFServiceService` 件。

**擷取要轉換的PDF檔案**

您必須擷取PDF檔案才能轉換為影像。 您無法將互動式PDF檔案轉換為影像。 如果您嘗試這麼做，則會擲回例外。 若要將互動式PDF檔案轉換為影像檔，您必須先平面化PDF檔案，才能進行轉換。 (請參閱 [平面化PDF檔案](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)。)

**設定執行時期選項**

您必須設定執行時期選項，例如影像格式和解析度值。 如需執行時間值的詳細資訊，請參閱 `ToImageOptionsSpec`[AEM Forms API參考中的類別參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**將PDF轉換為影像**

建立服務用戶端並設定執行時期選項後，您就可以將PDF檔案轉換為影像。 會傳回包含影像的系列物件。

**從系列擷取影像檔案**

您可以從轉換PDF服務傳回的系列物件擷取影像檔案。 系列中的每個元素都是 `com.adobe.idp.Document` 例項(或您使 `BLOB` 用web services時的例項)，您可將其儲存為影像檔案，例如JPG檔案。

影像檔案的格式取決於執 `ImageConvertFormat` 行時選項。 也就是說，如果您將執行 `ImageConvertFormat` 時期選項設為 `ImageConvertFormat.JPEG`，您可將影像檔儲存為JPG檔案。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速入門](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF檔案轉換為影像檔 {#convert-a-pdf-document-to-image-files-using-the-java-api}

使用「轉換PDF服務API」(Java)，將PDF檔案轉換為影像格式：

1. 包含專案檔案。

   將用戶端JAR檔案（例如adobe-convertpdf-client.jar）加入Java專案的類別路徑中。

1. 建立轉換PDF用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `ConvertPdfServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 擷取要轉換的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 設定執行時期選項。

   * 使用其 `ToImageOptionsSpec` 建構函式建立物件。
   * 根據需要調用屬於此對象的方法。 例如，通過調用方法並傳遞指定格 `setImageConvertFormat` 式類型的枚舉 `ImageConvertFormat` 值來設定影像類型。
   >[!NOTE]
   >
   >必須 `ImageConvertFormat` 設定枚舉值。

1. 將PDF轉換為影像。

   叫用物 `ConvertPdfServiceClient` 件的方 `toImage2` 法並傳遞下列值：

   * 表示 `com.adobe.idp.Document` 要轉換的PDF檔案的物件。
   * 包 `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` 含目標影像格式各種首選項的對象。
   該方 `toImage2` 法返回包 `java.util.List` 含影像的對象。 系列中的每個元素都是例 `com.adobe.idp.Document` 項。

1. 從系列擷取影像檔案。

   重複物件 `java.util.List` 以判斷影像是否存在。 每個元素都是 `com.adobe.idp.Document` 例項。 調用物件的方法並傳 `com.adobe.idp.Document` 遞物件， `copyToFile` 以儲存影 `java.io.File` 像。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將PDF檔案轉換為JPEG檔案](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 使用web service API將PDF檔案轉換為影像檔 {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

使用「轉換PDF服務API」(web service)，將PDF檔案轉換為影像格式：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立轉換PDF用戶端。

   * 使用其 `ConvertPdfServiceClient` 預設建構函式建立物件。
   * 使用建 `ConvertPdfServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`。)您不需要使用屬 `lc_version` 性。 不過，請指定 `?blob=mtom`。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `ConvertPdfServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 擷取要轉換的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 此 `BLOB` 物件用來儲存PDF表格。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，指定PDF表單的位置和開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 透過取得物件的屬性，判斷位 `System.IO.FileStream` 元組陣列的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 設定執行時期選項。

   * 使用其 `ToImageOptionsSpec` 建構函式建立物件。
   * 根據需要調用屬於此對象的方法。 例如，通過調用方法並傳遞指定格 `setImageConvertFormat` 式類型的枚 `ImageConvertFormat` 舉值來設定影像類型。
   >[!NOTE]
   >
   >必須 `ImageConvertFormat` 設定枚舉值。

1. 將PDF轉換為影像。

   叫用物 `ConvertPDFServiceService` 件的方 `toImage2` 法並傳遞下列值：

   * 表示 `BLOB` 要轉換的檔案的對象
   * 包 `ToImageOptionsSpec` 含目標影像格式各種首選項的對象
   該方 `toImage2` 法返回包 `MyArrayOfBLOB` 含新建映像檔案的對象。

1. 從系列擷取影像檔案。

   * 透過取得物件欄位的 `MyArrayOfBLOB` 值，判斷物件中的元素 `Count` 數。 每個元素都 `BLOB` 是包含影像的物件。
   * 重複物件 `MyArrayOfBLOB` 並儲存每個影像檔。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
