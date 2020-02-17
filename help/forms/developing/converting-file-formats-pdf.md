---
title: 在檔案格式與PDF之間轉換
seo-title: 在檔案格式與PDF之間轉換
description: 'null'
seo-description: 'null'
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 在檔案格式與PDF之間轉換 {#converting-between-file-formatsand-pdf}

**關於產生PDF服務**

「產生PDF」服務可將原始檔案格式轉換為PDF。 此外，它還可將PDF轉換為其他檔案格式，並最佳化PDF檔案的大小。

「產生PDF」服務使用原生應用程式將下列檔案格式轉換為PDF。 除非另有指示，否則僅支援這些應用程式的德文、法文、英文和日文版本。 *僅Windows* 表示僅支援Windows Server® 2003和Windows Server 2008。

* 轉換DOC、DOCX、RTF、TXT、XLS、XLS、PPT、PPTX、PPTX、VSD、MPP、MPPX、XPS和PUB的Microsoft Office 2003和2007（僅限Windows）

   **注意**:需要有Acrobat® 9.2或更新版本才能將Microsoft XPS格式轉換為PDF。*

* Autodesk autoCAD 2005、2006、2007、2008和2009可轉換DWF、DWG和DXW（僅提供英文版）
* Corel wordPerfect 12和X4可轉換WPD、QPW、SHW（僅提供英文版）
* OpenOffice 2.0、2.4、3.0.1和3.1，以轉換ODT、ODS、ODP、ODG、ODF、SXW、SXI、SXC、SXD、DOC、RTF、TXT、XLSX、PPT、PPTtx、VSD、MPP、MPPX和PUB

   ***注意&#x200B;**:「產生PDF」服務不支援64位元版本的OpenOffice。*

* 轉換PSD的Adobe Photoshop® CS2（僅限Windows）

   *注&#x200B;**意**:不支援Photoshop CS3和CS4，因為它們不支援Windows Server 2003或Windows Server 2008。*

* Adobe FrameMaker® 7.2和8可轉換FM（僅限Windows）
* Adobe pageMaker® 7.0可轉換PMD、PM6、P65和PM（僅限Windows）
* 協力廠商應用程式支援的原生格式（需要針對應用程式開發特定的設定檔案）（僅限Windows）

「產生PDF」服務會將下列標準檔案格式轉換為PDF。

* 視訊格式：SWF、FLV（僅限Windows）
* 影像格式：JPEG、JPG、JP2、J2Kí、JPC、J2C、GIF、BMP、TIFF、TIF、PNG、JPF
* HTML（Windows、Sun™ Solaris™和Linux®）

「產生PDF」服務會將PDF轉換為下列檔案格式（僅限Windows）:

* 封裝的PostScript(EPS)
* HTML3.2
* HTML 4.01含CSS 1.0
* DOC（Microsoft word格式）
* RTF
* 文字（可存取和純文字）
* XML
* 僅使用DeviceRGB色域的PDF/A-1a
* 僅使用DeviceRGB色域的PDF/A-1b

「產生PDF」服務需要您執行下列管理工作：

* 在代管AEM Forms的電腦上安裝必要的原生應用程式
* 在代管AEM Forms的電腦上安裝Adobe Acrobat Professional或Acrobat Pro Extended 9.2
* 執行安裝後安裝任務

這些工作在使用JBoss Tunkly安裝和部署AEM表單中有說明。

您可以使用「產生PDF」服務完成下列工作：

* 從原始檔案格式轉換為PDF。
* 將HTML檔案轉換為PDF檔案。
* 將PDF檔案轉換為檔案格式。

>[!NOTE]
>
>如需「產生PDF」服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將Word檔案轉換為PDF檔案 {#converting-word-documents-to-pdf-documents}

本節說明如何使用「產生PDF API」，以程式設計方式將Microsoft word檔案轉換為PDF檔案。

>[!NOTE]
>
>有關其他檔案格式的詳細資訊，請參 [閱添加對其他原生檔案格式的支援](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)。

>[!NOTE]
>
>如需「產生PDF」服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要將Microsoft word檔案轉換為PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立產生PDF用戶端。
1. 擷取檔案以轉換為PDF檔案。
1. 將檔案轉換為PDF檔案。
1. 擷取結果。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立產生PDF用戶端**

在以程式設計方式執行「產生PDF」作業之前，請先建立「產生PDF」服務用戶端。 如果您使用Java API，請建立物 `GeneratePdfServiceClient` 件。 如果您使用web service API，請建立物 `GeneratePDFServiceService` 件。

**擷取檔案以轉換為PDF檔案**

擷取Microsoft word檔案以轉換為PDF檔案。

**將檔案轉換為PDF檔案**

建立「產生PDF」服務用戶端後，您可以叫用該 `createPDF2` 方法。 此方法需要轉換檔案的相關資訊，包括副檔名。

**擷取結果**

將檔案轉換為PDF檔案後，您就可以擷取結果。 例如，將Word檔案轉換為PDF檔案後，您就可以擷取並儲存PDF檔案。

**另請參閱**

[使用Java API將Word檔案轉換為PDF檔案](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[使用web service API將Word檔案轉換為PDF檔案](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[產生PDF服務API快速入門](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將Word檔案轉換為PDF檔案 {#convert-word-documents-to-pdf-documents-using-the-java-api}

使用「產生PDF API(Java)」將Microsoft word檔案轉換為PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-generatepdf-client.jar。

1. 建立產生PDF用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `GeneratePdfServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 擷取檔案以轉換為PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式建立代表Word檔案的物件。 傳遞指定檔案位置的字串值。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 將檔案轉換為PDF檔案。

   調用物件的方法並傳遞下列值， `GeneratePdfServiceClient` 將檔案 `createPDF2` 轉換為PDF檔案：

   * 代 `com.adobe.idp.Document` 表要轉換的檔案的對象。
   * 包 `java.lang.String` 含副檔名的物件。
   * 包 `java.lang.String` 含要用於轉換的檔案類型設定的對象。 檔案類型設定為不同檔案類型（如。doc或。xls）提供轉換設定。
   * 包 `java.lang.String` 含要使用的PDF設定名稱的物件。 例如，您可以指定 `Standard`。
   * 包 `java.lang.String` 含要使用的安全設定名稱的對象。
   * 可選物 `com.adobe.idp.Document` 件，包含產生PDF檔案時要套用的設定。
   * 可選物 `com.adobe.idp.Document` 件，包含要套用至PDF檔案的中繼資料資訊。
   此方 `createPDF2` 法會傳回 `CreatePDFResult` 包含新PDF檔案和記錄檔資訊的物件。 日誌檔案通常包含由轉換請求生成的錯誤或警告消息。

1. 擷取結果。

   若要取得PDF檔案，請執行下列動作：

   * 叫用 `CreatePDFResult` 物件的方 `getCreatedDocument` 法，以傳回物 `com.adobe.idp.Document` 件。
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法，從先前步驟中建立的物件擷取PDF檔案。
   如果您使用 `createPDF2` 方法來取得記錄檔（不適用於HTML轉換），請執行下列動作：

   * 叫用 `CreatePDFResult` 物件的方 `getLogDocument` 法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法以擷取記錄檔。


**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API將Microsoft word檔案轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API將Word檔案轉換為PDF檔案 {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

使用「產生PDF API(web service)」將Microsoft word檔案轉換為PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立產生PDF用戶端。

   * 使用其 `GeneratePDFServiceClient` 預設建構函式建立物件。
   * 使用建 `GeneratePDFServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`。)您不需要使用屬 `lc_version` 性。 不過，請指定 `?blob=mtom`。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `GeneratePDFServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 擷取檔案以轉換為PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 物 `BLOB` 件用來儲存您要轉換為PDF檔案的檔案。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，代表要轉換之檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為 `BLOB` 其屬性指定字 `MTOM` 節陣列的內容來填充對象。

1. 將檔案轉換為PDF檔案。

   調用物件的方法並傳遞下列值， `GeneratePDFServiceService` 將檔案 `CreatePDF2` 轉換為PDF檔案：

   * 表示 `BLOB` 要轉換的檔案的對象。
   * 包含副檔名的字串。
   * 包 `java.lang.String` 含要用於轉換的檔案類型設定的對象。 檔案類型設定為不同檔案類型（如。doc或。xls）提供轉換設定。
   * 包含要使用的PDF設定的字串物件。 您可以指定 `Standard`。
   * 包含要使用的安全設定的字串對象。 您可以指定 `No Security`。
   * 可選物 `BLOB` 件，包含產生PDF檔案時要套用的設定。
   * 可選物 `BLOB` 件，包含要套用至PDF檔案的中繼資料資訊。
   * 由方法填 `BLOB` 入的輸出參 `CreatePDF2` 數。 該方 `CreatePDF2` 法使用轉換的文檔填充此對象。 （此參數值僅適用於Web服務調用）。
   * 由方法填 `BLOB` 入的輸出參 `CreatePDF2` 數。 方 `CreatePDF2` 法使用日誌文檔填充此對象。 （此參數值僅適用於Web服務調用）。

1. 擷取結果。

   * 將物件欄位指派給位元組陣列， `BLOB` 以擷取轉 `MTOM` 換的PDF檔案。 位元組陣列代表已轉換的PDF檔案。 請確定您使 `BLOB` 用用作方法輸出參數的對 `createPDF2` 像。
   * 調用 `System.IO.FileStream` 其建構函式並傳遞字串值，以建立物件，此字串值代表已轉換PDF檔案的檔案位置。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將HTML檔案轉換為PDF檔案 {#converting-html-documents-to-pdf-documents}

本節說明如何使用「產生PDF API」，以程式設計方式將HTML檔案轉換為PDF檔案。

>[!NOTE]
>
>如需「產生PDF」服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要將HTML文檔轉換為PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立產生PDF用戶端。
1. 擷取HTML內容以轉換為PDF檔案。
1. 將HTML內容轉換為PDF檔案。
1. 擷取結果。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立產生PDF用戶端**

您必須先建立「產生PDF」服務用戶端，才能以程式設計方式執行「產生PDF」操作。 如果您使用Java API，請建立物 `GeneratePdfServiceClient` 件。 如果您使用web service API，請建立 `GeneratePDFServiceService`。

**擷取HTML內容以轉換為PDF檔案**

參考您要轉換為PDF檔案的HTML內容。 您可以參考HTML內容，例如HTML檔案或可使用URL存取的HTML內容。

**將HTML內容轉換為PDF檔案**

建立服務用戶端後，您可以叫用適當的PDF建立作業。 此操作需要有關要轉換的文檔的資訊，包括目標文檔的路徑。

**擷取結果**

將HTML內容轉換為PDF檔案後，您可以擷取結果並儲存PDF檔案。

**另請參閱**

[使用Java API將HTML內容轉換為PDF檔案](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[使用web service API將HTML內容轉換為PDF檔案](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[產生PDF服務API快速入門](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將HTML內容轉換為PDF檔案 {#convert-html-content-to-a-pdf-document-using-the-java-api}

使用「產生PDF API(Java)」將HTML檔案轉換為PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-generatepdf-client.jar。

1. 建立產生PDF用戶端。

   使用其 `GeneratePdfServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 擷取HTML內容以轉換為PDF檔案。

   建立字串變數並指派指向HTML內容的URL，以擷取HTML內容。

1. 將HTML內容轉換為PDF檔案。

   叫用物 `GeneratePdfServiceClient` 件的方 `htmlToPDF2` 法並傳遞下列值：

   * 包 `java.lang.String` 含要轉換之HTML檔案URL的物件。
   * 包 `java.lang.String` 含要用於轉換的檔案類型設定的對象。 檔案類型設定可包含色階。
   * 包 `java.lang.String` 含要使用的安全設定名稱的對象。
   * 可選物 `com.adobe.idp.Document` 件，包含產生PDF檔案時要套用的設定。 如果未提供此資訊，則會根據前三個參數自動選擇設定。
   * 可選物 `com.adobe.idp.Document` 件，包含要套用至PDF檔案的中繼資料資訊。

1. 擷取結果。

   此方 `htmlToPDF2` 法會傳回 `HtmlToPdfResult` 包含已產生之新PDF檔案的物件。 若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用 `HtmlToPdfResult` 物件的方 `getCreatedDocument` 法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法，從先前步驟中建立的物件擷取PDF檔案。

**另請參閱**

[將HTML檔案轉換為PDF檔案](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[快速入門（SOAP模式）:使用Java API將HTML內容轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）:使用Java API將HTML內容轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API將HTML內容轉換為PDF檔案 {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

使用「產生PDF API」(web service)，將HTML內容轉換為PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立產生PDF用戶端。

   * 使用其 `GeneratePDFServiceClient` 預設建構函式建立物件。
   * 使用建 `GeneratePDFServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`。)您不需要使用屬 `lc_version` 性。 不過，請指定 `?blob=mtom`。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `GeneratePDFServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 擷取HTML內容以轉換為PDF檔案。

   建立字串變數並指派指向HTML內容的URL，以擷取HTML內容。

1. 將HTML內容轉換為PDF檔案。

   調用物件的方法，將HTML內容轉 `GeneratePDFServiceService` 換為PDF `HtmlToPDF2` 檔案，並傳遞下列值：

   * 包含要轉換之HTML內容的字串。
   * 包 `java.lang.String` 含要用於轉換的檔案類型設定的對象。
   * 包含要使用的安全設定的字串對象。
   * 可選物 `BLOB` 件，包含產生PDF檔案時要套用的設定。
   * 可選物 `BLOB` 件，包含要套用至PDF檔案的中繼資料資訊。
   * 由方法填 `BLOB` 入的輸出參 `CreatePDF2` 數。 該方 `CreatePDF2` 法使用轉換的文檔填充此對象。 （此參數值僅適用於Web服務調用）。

1. 擷取結果。

   * 將物件欄位指派給位元組陣列， `BLOB` 以擷取轉 `MTOM` 換的PDF檔案。 位元組陣列代表已轉換的PDF檔案。 請確定您使 `BLOB` 用用作方法輸出參數的對 `HtmlToPDF2` 像。
   * 調用 `System.IO.FileStream` 其建構函式並傳遞字串值，以建立物件，此字串值代表已轉換PDF檔案的檔案位置。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[將HTML檔案轉換為PDF檔案](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將PDF檔案轉換為非影像格式 {#converting-pdf-documents-to-non-image-formats}

本節說明如何使用「產生PDF Java API」和web service API，以程式設計方式將PDF檔案轉換為RTF檔案（非影像格式的範例）。 其他非影像格式包括HTML、文字、DOC和EPS。 將PDF檔案轉換為RTF時，請確定PDF檔案不包含表單元素，例如提交按鈕。 表單元素不會轉換。

>[!NOTE]
>
>如需「產生PDF」服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

若要將PDF檔案轉換為任何支援的類型，請執行下列步驟：

1. 包含專案檔案。
1. 建立產生PDF用戶端。
1. 擷取要轉換的PDF檔案。
1. 轉換PDF檔案。
1. 保存已轉換的檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立產生PDF用戶端**

您必須先建立「產生PDF」服務用戶端，才能以程式設計方式執行「產生PDF」操作。 如果您使用Java API，請建立物 `GeneratePdfServiceClient` 件。 如果您使用web service API，請建立物 `GeneratePDFServiceService` 件。

**擷取要轉換的PDF檔案**

擷取PDF檔案以轉換為非影像格式。

**轉換PDF檔案**

建立服務用戶端後，您可以叫用PDF匯出作業。 此操作需要有關要轉換的文檔的資訊，包括目標文檔的路徑。

**儲存轉換的檔案**

保存已轉換的檔案。 例如，如果將PDF文檔轉換為RTF檔案，請將轉換的文檔保存為RTF檔案。

**另請參閱**

[使用Java API將PDF檔案轉換為RTF檔案](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[使用web service API將PDF檔案轉換為RTF檔案](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[產生PDF服務API快速入門](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF檔案轉換為RTF檔案 {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

使用「產生PDF API(Java)」將PDF檔案轉換為RTF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-generatepdf-client.jar。

1. 建立產生PDF用戶端。

   使用其 `GeneratePdfServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 擷取要轉換的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式建立代表PDF檔案的物件以進行轉換。 傳遞指定PDF檔案位置的字串值。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 轉換PDF檔案。

   叫用物 `GeneratePdfServiceClient` 件的方 `exportPDF2` 法並傳遞下列值：

   * 表示 `com.adobe.idp.Document` 要轉換的PDF檔案的物件。
   * 包 `java.lang.String` 含要轉換的檔案名的對象。
   * 包 `java.lang.String` 含Adobe PDF設定名稱的物件。
   * 指定 `ConvertPDFFormatType` 轉換的目標檔案類型的對象。
   * 可選物 `com.adobe.idp.Document` 件，包含產生PDF檔案時要套用的設定。
   該方 `exportPDF2` 法返回包 `ExportPDFResult` 含已轉換檔案的對象。

1. 轉換PDF檔案。

   要獲取新建立的檔案，請執行以下操作：

   * 叫用 `ExportPDFResult` 物件的方 `getConvertedDocument` 法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法以擷取新檔案。

**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API將HTML內容轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API將PDF檔案轉換為RTF檔案 {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

使用「產生PDF API(web service)」將PDF檔案轉換為RTF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立生成PDf客戶端。

   * 使用其 `GeneratePDFServiceClient` 預設建構函式建立物件。
   * 使用建 `GeneratePDFServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`。)您不需要使用屬 `lc_version` 性。 不過，請指定 `?blob=mtom`。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `GeneratePDFServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 擷取要轉換的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存已轉換的PDF文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為 `BLOB` 其屬性指定字 `MTOM` 節陣列的內容來填充對象。

1. 轉換PDF檔案。

   叫用物 `GeneratePDFServiceServiceWse` 件的方 `ExportPDF2` 法並傳遞下列值：

   * 表示 `BLOB` 要轉換的PDF檔案的物件。
   * 包含要轉換的檔案路徑名的字串。
   * 指定 `java.lang.String` 檔案位置的對象。
   * 指定轉換目標檔案類型的字串對象。 指定 `RTF`。
   * 可選物 `BLOB` 件，包含產生PDF檔案時要套用的設定。
   * 由方法填 `BLOB` 入的輸出參 `ExportPDF2` 數。 該方 `ExportPDF2` 法使用轉換的文檔填充此對象。 （此參數值僅適用於Web服務調用）。

1. 保存已轉換的檔案。

   * 將對象欄位指定給位元組數 `BLOB` 組，以檢 `MTOM` 索已轉換的RTF文檔。 位元組陣列表示轉換的RTF文檔。 請確定您使 `BLOB` 用用作方法輸出參數的對 `ExportPDF2` 像。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞代表RTF檔案位置的字串值。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入RTF檔案。

**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 新增對其他原生檔案格式的支援 {#adding-support-for-additional-native-file-formats}

本節說明如何新增對其他原生檔案格式的支援。 它概述了「產生PDF」服務與本服務用來將原始檔案格式轉換為PDF之原生應用程式之間的互動。

本節還說明以下內容：

* 如何修改「產生PDF」服務對本產品已用來將原生檔案格式轉換為PDF之原生應用程式的回應
* 產生PDF服務、產生PDF服務應用程式監視程式(AppMon)元件與原生應用程式（例如Microsoft Word）之間的互動
* XML文法在這些互動中所扮演的角色

### 元件互動 {#component-interactions}

「產生PDF」服務會叫用與檔案格式相關的應用程式，然後與應用程式互動，以使用預設印表機列印檔案，以轉換原生檔案格式。 預設印表機必須設為Adobe PDF印表機。

此圖顯示與原生應用程式支援相關的元件和驅動程式。 同時也提到影響互動的XML文字。

原生檔案轉換的元件互動

本檔案使用「原生應 *用程式」一詞* ，指出用來產生原生檔案格式（例如Microsoft Word）的應用程式。

*AppMon是企業元件* ，與原生應用程式互動的方式，與使用者在應用程式顯示的對話方塊中導覽的方式相同。 AppMon用來指示應用程式（例如Microsoft Word）開啟和列印檔案的XML文字會包含下列循序工作：

1. 通過選擇「檔案」>「開啟」開啟檔案
1. 確保「開啟」對話框出現；否則，處理錯誤
1. 在「檔案名」欄位中提供檔案名，然後按一下「開啟」按鈕
1. 確保檔案實際開啟
1. 通過選擇「檔案」>「打印」開啟「打印」對話框
1. 確保「打印」對話框出現

AppMon使用標準的Win32 API與協力廠商應用程式互動，以便傳輸UI事件，例如按鍵和滑鼠點按，這對於控制這些應用程式以從它們產生PDF檔案非常有用。

由於這些Win32 API的限制，AppMon無法將這些UI事件分派到某些特定類型的視窗，例如浮動式選單列（在TextPad等應用程式中），以及某些使用Win32 API無法擷取其內容的對話方塊。

可以很容易地以視覺化方式識別浮動的菜單欄；但是，可能無法只透過視覺檢查來識別特殊類型的對話框。 您需要協力廠商應用程式(例如Microsoft Spy++（Microsoft Visual C++開發環境的一部分）或其相當的WinID(可從 [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)免費下載)來檢查對話方塊，以判斷AppMon是否能使用標準Win32 API與它互動。

如果WinID能夠擷取對話方塊內容，例如文字、子視窗、視窗類別ID等，AppMon也可以這麼做。

此表列出了打印原始檔案格式時使用的資訊類型。

<table>
 <thead>
  <tr>
   <th><p>資訊類型</p></th>
   <th><p>說明</p></th>
   <th><p>修改／建立與本機檔案相關的條目 </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>管理設定 </p></td>
   <td><p>包含PDF設定、安全性設定和檔案類型設定。 </p><p>檔案類型設定將檔案副檔名與相應的本地應用程式關聯。 檔案類型設定還指定用於打印本地檔案的本地應用程式設定。 </p></td>
   <td><p>若要變更已支援之原生應用程式的設定，系統管理員會在管理控制台中設定「檔案類型設定」。 </p><p>若要新增對新原生檔案格式的支援，您必須手動編輯檔案。 (請參 <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">閱添加或修改對原生檔案格式的支援</a>。) </p></td>
  </tr>
  <tr>
   <td><p>指令碼 </p></td>
   <td><p>指定「產生PDF」服務與原生應用程式之間的互動。 這類互動通常會引導應用程式將檔案列印至Adobe PDF驅動程式。 </p><p>此指令碼包含指示原生應用程式開啟特定對話方塊，以及針對這些對話方塊中的欄位和按鈕提供特定回應的指示。 </p></td>
   <td><p>「產生PDF」服務包含所有支援原生應用程式的指令碼檔案。 您可以使用XML編輯應用程式修改這些檔案。</p><p>若要新增對新原生應用程式的支援，您必須建立新的指令碼檔案。 (請參 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">閱為原生應用程式建立或修改其他對話XML檔案</a>。) </p></td>
  </tr>
  <tr>
   <td><p>一般對話方塊指示 </p></td>
   <td><p>指定如何回應多個應用程式共用的對話方塊。 這些對話方塊是由作業系統、輔助應用程式（例如PDFMaker）和驅動程式產生。 </p><p>包含此資訊的檔案為appmon.global.en_US.xml。</p></td>
   <td><p>請勿修改此檔案。 </p></td>
  </tr>
  <tr>
   <td><p>應用程式特定對話方塊指示</p></td>
   <td><p>指定如何回應應用程式特定的對話方塊。 </p><p>包含此資訊的檔案是appmon。<i>[appname]</i>.dialog。<i>[locale]</i>.xml（例如appmon.word.en_US.xml）。</p></td>
   <td><p>請勿修改此檔案。 </p><p>要為新的本地應用程式添加對話框說明，請參 <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">閱建立或修改本地應用程式的其他對話框XML檔案</a>。</p></td>
  </tr>
  <tr>
   <td><p>其他應用程式特定對話方塊指示 </p></td>
   <td><p>指定對特定應用程式對話框指令的覆蓋和添加。 本節介紹了此類資訊的示例。 </p><p>包含此資訊的檔案是appmon。<i>[appname]</i>.addition。<i>[locale]</i>.xml。 例如appmon.addition.en_US.xml。</p></td>
   <td><p>可使用XML編輯應用程式來建立和修改此類檔案。 (請參 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">閱為原生應用程式建立或修改其他對話XML檔案</a>。) </p><p><strong>重要</strong>:您必須針對您的伺服器將支援的每個原生應用程式建立其他應用程式特定對話框指示。 </p></td>
  </tr>
 </tbody>
</table>

### 關於指令碼和對話框XML檔案 {#about-the-script-and-dialog-xml-files}

指令碼XML檔案會引導「產生PDF」服務以使用者在應用程式對話方塊中導覽的方式，在應用程式對話方塊中導覽。 指令碼XML檔案也會指示「產生PDF」服務執行按鈕、選取或取消選取核取方塊或選取功能表項目等動作，以回應對話方塊。

相反地，對話框XML檔案只對對話框做出響應，其操作類型與指令碼XML檔案中使用的操作類型相同。

#### 對話框和窗口元素術語 {#dialog-box-and-window-element-terminology}

本節和下一節會根據所描述的透視，對對話方塊及其所包含的元件使用不同的術語。 對話框元件是按鈕、欄位和組合框等項。

當本節和下一節從用戶的角度介紹對話框及其元件時，會使用 *對話框*、 *button*、 *field*、 ** combobox等術語。

當本節和下一節從其內部表示的角度描述對話框及其元件時，將使用術語 *窗口元素* 。 窗口元素的內部表示是層次，其中每個窗口元素實例都由標籤標識。 窗口元素實例還描述了其物理特性和行為。

從使用者的角度來看，對話方塊及其元件會顯示不同的行為，其中有些對話方塊元素會隱藏直到啟動為止。 從內部代表的角度看，不存在此類行為問題。 例如，對話框的內部表示形式與其包含的元件的內部表示形式類似，但該對話框中的元件是嵌套的。

本節說明提供AppMon指示的XML元素。 這些元素具有元素和元 `dialog` 素等名 `window` 稱。 本檔案使用單位間隔字型來區分XML元素。 元 `dialog` 素會識別XML指令檔可能導致顯示的對話方塊，不論是有意或無意。 元素 `window` 標識窗口元素（對話框或對話框的元件）。

#### 階層 {#hierarchy}

此圖顯示了指令碼和對話框XML的層次結構。 指令碼XML檔案符合script.xsd架構，該架構包括（在XML意義下）window.xsd架構。 同樣地，對話框XML檔案符合dialogs.xsd架構，該架構還包括window.xsd架構。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

指令碼和對話框XML的層次

#### 指令碼XML檔案 {#script-xml-files}

指令 *碼XML檔案指定一系列步驟* ，以引導原生應用程式導覽至特定視窗元素，然後提供這些元素的回應。 大部分回應是文字或按鍵輸入，這些回應會對應使用者在對應對話方塊中提供的欄位、組合方塊或按鈕。

「產生PDF」服務支援指令碼XML檔案的目的，在於引導原生應用程式列印原生檔案。 不過，指令碼XML檔案可用來完成使用者在與原生應用程式對話方塊互動時可執行的任何工作。

指令碼XML檔案中的步驟會依順序執行，而不會產生任何分支的機會。 唯一支援的條件測試是逾時／重試，當某個步驟在特定時段內和特定重試次數之後未成功完成時，會導致指令碼終止。

除了循序步驟外，步驟中的指令也依順序執行。 您必須確保步驟和說明反映使用者執行這些相同步驟的順序。

指令碼XML檔案中的每個步驟都會識別在成功執行步驟指示時預期會出現的視窗元素。 如果在執行指令碼步驟時出現非預期的對話方塊，「產生PDF」服務會依下節所述搜尋對話XML檔案。

#### 對話框XML檔案 {#dialog-xml-files}

執行原生應用程式會顯示不同的對話方塊，不論原生應用程式是在可見或不可見模式下，都會顯示對話方塊。 對話方塊可由作業系統或應用程式本身產生。 當原生應用程式在「產生PDF」服務的控制下執行時，系統和原生應用程式對話方塊會顯示在不可見的視窗中。

對話 *框XML檔案* ，指定生成PDF服務對系統或本地應用程式對話框的響應方式。 對話方塊XML檔案可讓「產生PDF」服務以方便轉換程式的方式回應未提示的對話方塊。

當系統或原生應用程式顯示目前執行的指令碼XML檔案未處理的對話方塊時，「產生PDF」服務會依此順序搜尋對話方塊XML檔案，在找到相符項目時停止：

* appmon。*[appname]*.additional.*[locale]*.xml
* appmon。*[appname]。[locale]*.xml（請勿修改此檔案）。
* appmon.global。*[locale]*.xml（請勿修改此檔案）。

如果「產生PDF」服務找到對話方塊的符合項，則會傳送對話方塊的按鍵動作或其他動作，以關閉該對話方塊。 如果對話框的說明指定了中止消息，則生成PDF服務將終止當前正在執行的作業並生成錯誤消息。 將在指令碼XML語法的元素中 `abortMessage` 指定此類中止消息。

如果「產生PDF」服務遇到任何先前列出的檔案中未說明的對話方塊，「產生PDF」服務會將對話方塊的標題整合至記錄檔項目中。 當前執行的作業最終超時。 然後，您可以使用日誌檔案中的資訊在本地應用程式的附加對話框XML檔案中編寫新的說明。

### 添加或修改對本機檔案格式的支援 {#adding-or-modifying-support-for-a-native-file-format}

本節介紹支援其他原生檔案格式或修改對已支援的原生檔案格式的支援時必須執行的任務。

您必須先完成下列工作，才能新增或修改支援。

#### 選擇用於標識窗口元素的工具 {#choosing-a-tool-for-identifying-window-elements}

對話框和指令碼XML檔案要求您標識對話框或指令碼元素所響應的窗口元素（對話框、欄位或其他對話框元件）。 例如，在指令碼調用本地應用程式的菜單後，指令碼必須標識該菜單上要應用擊鍵或操作的窗口元素。

您可以透過對話框標題列中顯示的標題輕鬆識別對話框。 不過，您必須使用Microsoft Spy++等工具來識別較低層級的視窗元素。 低層窗口元素可以通過多種屬性來識別，這些屬性並不明顯。 此外，每個原生應用程式可以不同地識別其視窗元素。 因此，有多種識別視窗元素的方式。 以下是考慮窗口元素標識的建議順序：

1. 標題本身（如果是唯一）
1. 控制ID，它對於指定對話框可能唯一，也可能不唯一
1. 類別名稱，可能唯一，也可能不唯一

這三個屬性的任意一個或組合可用於標識窗口。

如果屬性無法識別標題，則可以改為使用相對於父項的索引來識別窗口元素。 索 *引指* 定窗口元素相對於其同級窗口元素的位置。 索引通常是識別組合框的唯一方法。

請注意下列問題：

* Microsoft Spy++使用&amp;符號(&amp;)來識別標題的熱鍵，以顯示標題。 例如，Spy++將一個「打印」對話框的標題顯示為 `Pri&nt`，這表示熱鍵為 *n*。 指令碼和對話框XML檔案中的標題必須省略&amp;符號。
* 有些標題包含分行符號。 「產生PDF」服務無法識別分行符號。 如果標題包含分行符號，請包含足夠的標題以區隔其他功能表項目，然後對省略的部分使用規則運算式。 例如( `^Long caption title$`)。]. (請參閱 [在標題屬性中使用規則運算式](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes)。)
* 對保留的XML字元使用字元實體（也稱為轉義序列）。 例如，對於 `&` &amp;符號， `<` 對於 `>` 小於和大於符號，對於撇號 `&apos;` ，對於 `&quot;` 引號。

如果您打算使用對話方塊或XML檔案指令碼，則應安裝應用程式Microsoft Spy++。

#### 取消對話框和指令碼檔案的封裝 {#unpackaging-the-dialog-and-script-files}

對話框和指令碼檔案駐留在appmondata.jar檔案中。 在可以修改這些檔案或添加新指令碼或對話框檔案之前，必須先取消打包此JAR檔案。 例如，假設您要新增對EditPlus應用程式的支援。 您可以建立兩個XML檔案，名為appmon.editplus.script.en_US.xml和appmon.editplus.script.addition.en_US.xml。 這些XML指令碼必須新增至位於兩個位置的adobe-appmondata.jar檔案，如下所述：

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon。 adobe-livecycle-native-jboss-x86_win32.ear檔案位於匯出資料夾中，網址為 `[AEM forms install directory]\configurationManager`。 （如果AEM Forms已部署在其他J2EE應用程式伺服器上，請將adobe-livecycle-native-jboss-x86_win32.ear檔案取代為與您的J2EE應用程式伺服器對應的EAR檔案。）
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon （adobe-appmondata.jar檔案位於adobe-generatepdf-dsc.jar檔案中）。 adobe-generatepdf-dsc.jar檔案位於 *[AEM forms install directory]*\deploy資料夾中。

將這些XML檔案新增至adobe-appmondata.jar檔案後，您必須重新部署GeneratePDF元件。 若要將對話方塊和指令碼XML檔案新增至adobe-appmondata.jar檔案，請執行下列工作：

1. 使用WinZip或WinRAR等工具，開啟adobe-livecycle-native.jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar檔案。
1. 將對話方塊和指令碼XML檔案新增至appmondata.jar檔案，或修改此檔案中現有的XML檔案。 (請參 [閱為本地應用程式建立或修改指令碼XML文](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)件， [以及為本地應用程式建立或修改其他對話框XML檔案](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)。)
1. 使用WinZip或WinRAR等工具，開啟adobe-generatepdf-dsc.jar > adobe-appmondata.jar。
1. 將對話方塊和指令碼XML檔案新增至appmondata.jar檔案，或修改此檔案中現有的XML檔案。 (請參 [閱為本地應用程式建立或修改指令碼XML文](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)件， [以及為本地應用程式建立或修改其他對話框XML檔案](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)。)將XML檔案新增至adobe-appmondata.jar檔案後，請將新的adobe-appmondata.jar檔案置入adobe-generatepdf-dsc.jar檔案。
1. 如果您新增了對其他原生檔案格式的支援，請建立提供應用程式路徑的系統環境變數(請參閱建立環境變數以找出原生應用程式 [](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application))。

**重新部署GeneratePDF元件**

1. 登入工作台。
1. 選擇「 **窗口** 」>「 **顯示視圖** 」 **>「組**&#x200B;件」。 此動作會將「元件」檢視新增至「工作台」。
1. 按一下右鍵GeneratePDF元件，然後選擇「停 **止元件」**。
1. 當元件停止時，按一下右鍵並選擇「卸載元件」將其刪除。
1. 按一下右鍵「組 **件** 」表徵圖，然後選擇「 **安裝元件」**。
1. 瀏覽並選取已修改的adobe-generatepdf-dsc.jar檔案，然後按一下「開啟」。 請注意，GeneratePDF元件旁會出現紅方。
1. 展開GeneratePDF元件，選擇「服務描述符」，然後按一下右鍵「生成PDF服務」並選擇「激活服務」。
1. 在出現的配置對話框中，輸入適用的配置值。 如果將這些值留空，則會使用預設組態值。
1. 在「產生PDF」上按一下滑鼠右鍵，然後選取「開始元件」。
1. 展開「活動服務」。 如果服務名正在運行，則服務名旁邊將顯示綠色箭頭。 否則，服務處於停止狀態。
1. 如果服務處於停止狀態，請按一下右鍵服務名，然後選擇啟動服務。

### 為本地應用程式建立或修改指令碼XML檔案 {#creating-or-modifying-a-script-xml-file-for-a-native-application}

如果要將檔案定向到新的本地應用程式，則必須為該應用程式建立指令碼XML檔案。 如果您想要修改「產生PDF」服務與已受支援的原生應用程式互動的方式，您必須修改該應用程式的指令碼。

此指令碼包含導覽原生應用程式視窗元素的指示，並提供這些元素的特定回應。 包含此資訊的檔案是appmon。*[appname]*.script。*[locale]*.xml。 例如appmon.notepad.script.en_US.xml。

#### 標識指令碼必須執行的步驟 {#identifying-steps-the-script-must-execute}

使用原生應用程式，確定您必須瀏覽的視窗元素以及列印檔案時必須執行的每個回應。 請注意任何回應所產生的對話方塊。 這些步驟將類似於下列步驟：

1. 選擇「檔案」>「開啟」。
1. 指定路徑，然後按一下「開啟」。
1. 在菜單欄上選擇「檔案」>「打印」。
1. 指定打印機所需的屬性。
1. 選擇「打印」並等待「另存為」對話框出現。 「產生PDF」服務需要「另存新檔」對話方塊，才能指定PDF檔案的目的地。

#### 標識標題屬性中指定的對話框 {#identifying-the-dialogs-specified-in-caption-attributes}

使用Microsoft Spy++獲取本地應用程式中窗口元素屬性的身份。 您必須具備這些身分才能編寫指令碼。

#### 在標題屬性中使用規則運算式 {#using-regular-expressions-in-caption-attributes}

您可以在標題規格中使用規則運算式。 「產生PDF」服務使用類 `java.util.regex.Matcher` 別來支援規則運算式。 該實用程式支援中所述的規則運算式 `java.util.regex.Pattern`。 (請至Java網站： [https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html](https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html)。)

**在記事本橫幅中，包含前置於記事本的檔案名的規則運算式**

```as3
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**規則運算式區分列印與列印設定**

```as3
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### 排序窗口和窗口清單元素 {#ordering-the-window-and-windowlist-elements}

您必須按如 `window` 下方 `windowList` 式訂購和元素：

* 當多個 `window` 元素在或元素中顯示為子項時， `windowList` 請依遞減順序排列這些元素，並使用名稱的長度 `dialog``window``caption` 來指示順序中的位置。
* 當元素 `windowList` 中出現多個元素 `window` 時，請依遞減順序排列這些元素，第一個元素的屬 `windowList` 性長度會 `caption``indexes/`指示順序中的位置。

**對對話框檔案中的窗口元素進行排序**

```as3
 <!-- The caption attribute in the following window element is 40 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <window caption="Unexpected Failure in DebugActiveProcess">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Adobe Acrobat - License Agreement">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Microsoft Visual.*Runtime Library">
     <…>
 </window>

 <!-- The caption attribute in the following window element is 28 characters long. It is the shortest caption in this example, so its parent window element appears after the others. -->
 <window caption="Adobe Acrobat - Registration">
     <…>
 </window>
```

**在窗口中對窗口元素排序清單元素**

```as3
 <!-- The caption attribute in the following indexes element is 56 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <windowList>
     <window caption="Can&apos;t exit design mode because.* cannot be created"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
 <windowList>
     <window caption="Do you want to continue loading the project?"/>
     <window className="Button" caption="No" action="press"/>
 </windowList>
 <windowList>
     <window caption="The macros in this project are disabled"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
```

### 為本地應用程式建立或修改其他對話框XML檔案 {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

如果您為先前不支援的原生應用程式建立指令碼，您也必須為該應用程式建立額外的對話XML檔案。 AppMon使用的每個原生應用程式都只能有一個額外的對話XML檔案。 即使不需要任何未經請求的對話方塊，也需要額外的對話XML檔案。 其他對話方塊至少必須有一個元素， `window` 即使該元素僅 `window` 是預留位置。

>[!NOTE]
>
>在此背景下，「附加」一詞表示應用程式的內容。[applicationname].addition。[locale].xml檔案。 此類檔案指定對話XML檔案的覆蓋和添加。

您也可以針對下列用途修改原生應用程式的其他對話XML檔案：

* 若要覆寫具有不同回應之應用程式的對話XML檔案
* 向該應用程式的對話框XML檔案中未定址的對話框添加響應

此時會套用用以識別其他dialogXML檔案的檔案名稱。*[appname]*.addition。*[locale]*.xml。 例如appmon.excel.addition.en_US.xml。

其他對話框XML檔案的名稱必須使用格式appmon。*[applicationname]*.addition。*[locale]*.xml，其中 *applicationname* 必須與XML配置檔案和指令碼中使用的應用程式名稱完全匹配。

>[!NOTE]
>
>native2pdfconfig.xml配置檔案中指定的所有通用應用程式都沒有主對話框XML檔案。 添加或修 [改對本地檔案格式的支援一節介紹了此類規範](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) 。

您必須排序 `windowList` 元素，這些元素在元素中顯示為子 `window` 項。 (請參 [閱排序窗口和窗口清單元素](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements)。)

### 修改常規對話框XML檔案 {#modifying-the-general-dialog-xml-file}

您可以修改常規對話框XML檔案，以響應由系統生成的對話框，或響應多個應用程式通用的對話框。

#### 在XML配置檔案中添加檔案類型條目 {#adding-a-filetype-entry-in-the-xml-configuration-file}

此程式說明如何更新「產生PDF」服務設定檔，將檔案類型與原生應用程式建立關聯。 要更新此配置檔案，必須使用管理控制台將配置資料導出到檔案。 設定資料的預設檔案名稱為native2pdfconfig.xml。

**更新「產生PDF」服務設定檔**

1. 選擇「 **首頁** 」>「 **服務** 」>「 **Adobe PDF Generator** 」>「配置檔案」，然後選 ********&#x200B;擇「導出配置檔案」來配置配置配置。
1. 視需 `filetype-settings` 要修改native2pdfconfig.xml檔案中的元素。
1. 選擇「 **首頁** 」>「 **服務** 」>「 **Adobe PDF Generator** 」>「配置檔案導入」，然&#x200B;********&#x200B;後選擇「導入配置配置」。 設定資料會匯入「產生PDF」服務，取代先前的設定。

>[!NOTE]
>
>應用程式的名稱會指定為元素屬 `GenericApp` 性的值 `name` 。 此值必須完全符合您為該應用程式開發的指令碼中指定的對應名稱。 同樣地，元 `GenericApp` 素的屬 `displayName` 性應完全符合對應指令碼的視窗 `expectedWindow` 標題。 在解析出現在或屬性中的任何規則運算式後，會評估此 `displayName` 等等 `caption` 效性。

在此示例中，Generate PDF服務提供的預設配置資料已修改，以指定應使用記事本（而非Microsoft Word）來處理檔案副檔名為。txt的檔案。 在進行此修改之前，Microsoft word已指定為應處理此類檔案的原生應用程式。

**將文字檔案導向記事本的修改(native2pdfconfig.xml)**

```as3
 <filetype-settings>

 <!-- Some native app file types were omitted for brevity. -->
 <!-- The following GenericApp element specifies Notepad as the native application that should be used to process files that have a txt file name extension. -->
             <GenericApp
                 extensions="txt"
                 name="Notepad" displayName=".*Notepad"/>
             <GenericApp
                 extensions="wpd"
                 name="WordPerfect" displayName="Corel WordPerfect"/>
             <GenericApp extensions="pmd,pm6,p65,pm"
                 name="PageMaker" displayName="Adobe PageMaker"/>
             <GenericApp extensions="fm"
                 name="FrameMaker" displayName="Adobe FrameMaker"/>
             <GenericApp extensions="psd"
                 name="Photoshop" displayName="Adobe Photoshop"/>
         </settings>
     </filetype-settings>
```

#### 建立環境變數以查找本機應用程式 {#creating-an-environment-variable-to-locate-the-native-application}

建立一個環境變數，指定本地應用程式執行檔的位置。 變數必須使用格式 *[applicationname]*_PATH，其中 *applicationname* 必須與XML配置檔案和指令碼中使用的應用程式名稱完全匹配，並且路徑包含以雙引號表示的執行檔的路徑。 這樣的環境變數的示例為 `Photoshop_PATH`。

建立新環境變數後，您必須重新啟動部署「產生PDF」服務的伺服器。

**在Windows XP環境中建立系統變數**

1. 選擇「 **控制面板」>「系統**」。
1. 在「系統屬性」對話框中，按一下「高 **級** 」頁籤，然後按一下「 **環境變數」**。
1. 在「環境變數」(Environment Variables)對話框的「系統變數」(System Variables)下，按一下「 **新建**」(New)。
1. 在「新建系統變數」對話框的「變 **量名稱** 」框中，鍵入使用格式 *[applicationname]*_PATH的名稱。
1. 在「變 **量值** 」方塊中，輸入應用程式可執行檔的完整路徑和檔案名稱，然後按一下「 **確定」**。 例如，鍵入： `c:\windows\Notepad.exe`
1. 在「環境變數」對話框中，按一下「確 **定」**。

**從命令行建立系統變數**

1. 在命令行窗口中，使用以下格式鍵入變數定義：

   ```as3
            [applicationname]_PATH=[Full path name]
   ```

   例如，鍵入： `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. 啟動新的命令行提示，使系統變數生效。

#### XML檔案 {#xml-files}

AEM Forms包含範例XML檔案，可讓「產生PDF」服務使用記事本處理任何副檔名為。txt的檔案。 本節包含此代碼。 此外，您必須進行本節所述的其他修改。

#### 其他對話框XML檔案 {#additional-dialog-xml-file}

此示例包含記事本應用程式的其他對話框。 除了「產生PDF」服務所指定的對話方塊外，這些對話方塊也可以。

**記事本對話方塊(appmon.notepad.addition.en_US.xml)**

```as3
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### 指令碼XML檔案 {#script-xml-file}

此範例指定「產生PDF」服務如何與記事本互動，以使用Adobe PDF印表機列印檔案。

**記事本指令碼XML檔案(appmon.notepad.script.en_US.xml)**

```as3
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!--
*
* ADOBE CONFIDENTIAL
* ___________________
* Copyright 2004 - 2005 Adobe Systems Incorporated
* All Rights Reserved.
*
* NOTICE:  All information contained herein is, and remains
* the property of Adobe Systems Incorporated and its suppliers,
* if any.  The intellectual and technical concepts contained
* herein are proprietary to Adobe Systems Incorporated and its
* suppliers and may be covered by U.S. and Foreign Patents,
* patents in process, and are protected by trade secret or copyright law.
* Dissemination of this information or reproduction of this material
* is strictly forbidden unless prior written permission is obtained
* from Adobe Systems Incorporated.
*-->

<!-- This file automates printing of text files via notepad to Adobe PDF printer. In order to see the complete hierarchy we recommend using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps-->

<application name="Notepad" version="9.0" locale="en_US" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="scripts.xsd">

    <!-- In this step we wait for the application window to appear -->
    <step>
        <expectedWindow>
            <window caption=".*Notepad"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the application window and send File->Open menu bar, menu item commands and the expectation is the windows Open dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Open...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Open window and then select the 'Edit' widget and input the source path followed by clicking on the 'Open' button . The expectation of this 'action' is that the Open dialog will disappear -->
    <step>
        <acquiredWindow>
            <window caption="Open">
                <windowList>
                    <window className="ComboBoxEx32">
                        <windowList>
                            <window className="ComboBox">
                                <windowList>
                                <window className="Edit" action="inputSourcePath"/>
                                </windowList>
                            </window>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="Open" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open" action="disappear"/>
        </expectedWindow>
        <pause value="30"/>
    </step>

    <!-- In this step, we acquire the application window and send File->Print menu bar, menu item commands and the expectation is the windows Print dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Print...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print">
        </window>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Print dialog and click on the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General">
                        <windowList>
                            <window className="Button" caption="Preferences" action="press"/>
                        </windowList>
                    </window>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which  has the caption '"View Adobe PDF results' and we click on the button OK. The expectation is that 'Printing Preferences' dialog disappears. -->
    <step>
        <acquiredWindow>
            <window caption="Printing Preferences">
                <windowList>
                    <window caption="Adobe PDF Settings">
                        <windowList>
                            <window className="Button" caption="View Adobe PDF results" action="uncheck"/>
                        </windowList>
                        <windowList>
                            <window className="Button" caption="Ask to Replace existing PDF file" action="uncheck"/>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="OK" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the 'Print' dialog and click on the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General"/>
                    <window className="Button" caption="^Print$" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print" action="disappear"/>
        </expectedWindow>
    </step>
    <step>
        <expectedWindow>
            <window caption="Save PDF File As"/>
        </expectedWindow>
    </step>
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click on the Save button. The expectation is that the dialog disappears-->
    <step>
        <acquiredWindow>
            <window caption="Save PDF File As">
                <windowList>
                    <window className="Edit" action="inputDestinationPath"/>
                </windowList>
                <windowList>
                    <window className="Button" caption="Save" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Save PDF File As" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- We can always set a retry count or a maximum time for a step. In case we surpass these limitations, PDF Generator generates this abort message and terminates processing. -->
    <abortMessage msg="15078"/>
</application>
```

