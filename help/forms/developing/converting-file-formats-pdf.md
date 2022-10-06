---
title: 在檔案格式和PDF之間轉換
seo-title: Converting Between File Formats and PDF
description: 使用「生成PDF」服務將本機檔案格式轉換為PDF。 生成PDF服務還將PDF轉換為其他檔案格式並優化PDF文檔的大小。
seo-description: Use the Generate PDF service to convert native file formats to PDF. Generate PDF service also converts PDF to other file formats and optimizes the size of PDF documents.
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
role: Developer
exl-id: 10535740-e3c2-4347-a88f-86706ad699b4
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '7850'
ht-degree: 0%

---

# 在檔案格式和PDF之間轉換 {#converting-between-file-formatsand-pdf}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於產生PDF服務**

「生成PDF」服務將本機檔案格式轉換為PDF。 它還將PDF轉換為其他檔案格式，並優化PDF文檔的大小。

「生成PDF」服務使用本機應用程式將下列檔案格式轉換為PDF。 除非另有說明，否則僅支援這些應用程式的德文、法文、英文和日文版本。 *僅限Windows* 表示僅支援Windows Server® 2003和Windows Server 2008。

* Microsoft Office 2003和2007，轉換DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PPTX、VSD、MPP、MPPX、XPS和PUB（僅限Windows）

>[!NOTE]
>
>Acrobat® 9.2或更新版本需要將Microsoft XPS格式轉換為PDF。

* Autodesk AutoCAD 2005、2006、2007、2008和2009，以轉換DWF、DWG和DXW（僅英語）
* Corel WordPerfect 12和X4轉換WPD、QPW、SHW（僅英語）
* OpenOffice 2.0、2.4、3.0.1和3.1，以轉換ODT、ODS、ODP、ODF、SXW、SXI、SXC、SXD、DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PTX、VSD、MP、MPX和PUB

>[!NOTE]
>
>生成PDF服務不支援64位版本的OpenOffice。

* Adobe Photoshop® CS2轉換PSD（僅限Windows）

>[!NOTE]
>
>Photoshop CS3和CS4不受支援，因為它們不支援Windows Server 2003或Windows Server 2008。

* Adobe FrameMaker® 7.2和8以轉換FM（僅限Windows）
* AdobePageMaker® 7.0以轉換PMD、PM6、P65和PM（僅限Windows）
* 協力廠商應用程式支援的原生格式（需要開發應用程式專用的設定檔案）（僅限Windows）

「生成PDF」服務將以下基於標準的檔案格式轉換為PDF。

* 視頻格式：SWF, FLV（僅限Windows）
* 影像格式：JPEG,JPG, JP2, J2Kí, JPC, J2C,GIF, BMP,TIFF, TIF, PNG, JPF
* HTML(Windows、Sun™ Solaris™和Linux®)

「生成PDF」服務將PDF轉換為以下檔案格式（僅限Windows）:

* 封裝的PostScript(EPS)
* HTML3.2
* HTML4.01搭配CSS 1.0
* DOC(Microsoft Word格式)
* RTF
* 文本（可訪問和純文字檔案）
* XML
* PDF/A-1a，僅使用DeviceRGB色域
* PDF/A-1b，僅使用DeviceRGB色域

生成PDF服務要求您執行以下管理任務：

* 在托管AEM Forms的電腦上安裝所需的原生應用程式
* 在托管AEM Forms的電腦上安裝Adobe Acrobat Professional或Acrobat Pro Extended 9.2
* 執行安裝後安裝任務

使用JBoss Tunklying安裝和部署AEM表單中介紹了這些任務。

您可以使用「產生PDF」服務來完成下列工作：

* 從原生檔案格式轉換為PDF。
* 將HTML文檔轉換為PDF文檔。
* 將PDF文檔轉換為檔案格式。

>[!NOTE]
>
>如需產生PDF服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將Word文檔轉換為PDF文檔 {#converting-word-documents-to-pdf-documents}

本節說明如何使用「產生PDFAPI」，以程式設計方式將Microsoft Word檔案轉換為PDF檔案。

>[!NOTE]
>
>如需其他檔案格式的詳細資訊，請參閱 [新增對其他原生檔案格式的支援](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats).

>[!NOTE]
>
>如需產生PDF服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要將Microsoft Word文檔轉換為PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立「生成PDF」客戶端。
1. 檢索要轉換為PDF文檔的檔案。
1. 將檔案轉換為PDF文檔。
1. 檢索結果。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立生成PDF客戶端**

在以寫程式方式執行「生成PDF」操作之前，請建立「生成PDF」服務客戶端。 如果您使用Java API，請建立 `GeneratePdfServiceClient` 物件。 如果您使用網站服務API，請建立 `GeneratePDFServiceService` 物件。

**檢索要轉換為PDF文檔的檔案**

檢索Microsoft Word文檔以轉換為PDF文檔。

**將檔案轉換為PDF文檔**

建立「生成PDF」服務客戶端後，可以調用 `createPDF2` 方法。 此方法需要有關要轉換的文檔的資訊，包括副檔名。

**擷取結果**

將檔案轉換為PDF文檔後，可以檢索結果。 例如，將Word檔案轉換為PDF文檔後，可以檢索並保存PDF文檔。

**另請參閱**

[使用Java API將Word文檔轉換為PDF文檔](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[使用Web服務API將Word文檔轉換為PDF文檔](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[產生PDF服務API快速入門](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將Word文檔轉換為PDF文檔 {#convert-word-documents-to-pdf-documents-using-the-java-api}

使用「產生MicrosoftAPI(Java)」將PDF Word檔案轉換為PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-generatepdf-client.jar。

1. 建立「生成PDF」客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `GeneratePdfServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索要轉換為PDF文檔的檔案。

   * 建立 `java.io.FileInputStream` 使用其建構子表示要轉換的Word檔案的對象。 傳遞指定檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 將檔案轉換為PDF文檔。

   調用 `GeneratePdfServiceClient` 物件 `createPDF2` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 表示要轉換的檔案的對象。
   * A `java.lang.String` 包含副檔名的物件。
   * A `java.lang.String` 包含要用於轉換的檔案類型設定的物件。 檔案類型設定提供不同檔案類型(如.doc或.xls)的轉換設定。
   * A `java.lang.String` 包含要使用的PDF設定名稱的物件。 例如，您可以指定 `Standard`.
   * A `java.lang.String` 包含要使用的安全設定名稱的對象。
   * 可選 `com.adobe.idp.Document` 包含在生成PDF文檔時要應用的設定的對象。
   * 可選 `com.adobe.idp.Document` 包含要應用到PDF文檔的元資料資訊的對象。

   此 `createPDF2` 方法傳回 `CreatePDFResult` 包含新PDF文檔和日誌資訊的對象。 記錄檔通常包含轉換請求產生的錯誤或警告訊息。

1. 檢索結果。

   要獲取PDF文檔，請執行以下操作：

   * 叫用 `CreatePDFResult` 物件 `getCreatedDocument` 方法，返回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法，從上一步中建立的物件中擷取PDF檔案。

   如果您使用 `createPDF2` 要獲取日誌文檔的方法(不適用於HTML轉換)，請執行以下操作：

   * 叫用 `CreatePDFResult` 物件 `getLogDocument` 方法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法來擷取記錄檔。


**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API將Microsoft Word檔案轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將Word文檔轉換為PDF文檔 {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

使用「產生MicrosoftAPI」（Web服務）將PDF Word檔案轉換為PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立「生成PDF」客戶端。

   * 建立 `GeneratePDFServiceClient` 物件，使用其預設建構函式。
   * 建立 `GeneratePDFServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 不過，請指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `GeneratePDFServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 檢索要轉換為PDF文檔的檔案。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存要轉換為PDF文檔的檔案。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示要轉換的檔案的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過為其分配 `MTOM` 屬性位元組陣列的內容。

1. 將檔案轉換為PDF文檔。

   調用 `GeneratePDFServiceService` 物件 `CreatePDF2` 方法並傳遞下列值：

   * A `BLOB` 表示要轉換的檔案的物件。
   * 包含副檔名的字串。
   * A `java.lang.String` 包含要用於轉換的檔案類型設定的物件。 檔案類型設定提供不同檔案類型(如.doc或.xls)的轉換設定。
   * 包含要使用的PDF設定的字串物件。 您可以指定 `Standard`.
   * 包含要使用的安全設定的字串對象。 您可以指定 `No Security`.
   * 可選 `BLOB` 包含在生成PDF文檔時要應用的設定的對象。
   * 可選 `BLOB` 包含要應用到PDF文檔的元資料資訊的對象。
   * 類型的輸出參數 `BLOB` 由 `CreatePDF2` 方法。 此 `CreatePDF2` 方法會以轉換的檔案填入此物件。 （此參數值僅對於Web服務調用是必需的）。
   * 類型的輸出參數 `BLOB` 由 `CreatePDF2` 方法。 此 `CreatePDF2` 方法會以記錄檔填入此物件。 （此參數值僅對於Web服務調用是必需的）。

1. 檢索結果。

   * 通過分配 `BLOB` 物件 `MTOM` 欄位至位元組陣列。 位元組陣清單示轉換的PDF文檔。 請確定您使用 `BLOB` 用作 `createPDF2` 方法。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示已轉換PDF文檔的檔案位置。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將HTML文檔轉換為PDF文檔 {#converting-html-documents-to-pdf-documents}

本節說明如何使用「產生PDFAPI」，以程式設計方式將HTML檔案轉換為PDF檔案。

>[!NOTE]
>
>如需產生PDF服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

要將HTML文檔轉換為PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立「生成PDF」客戶端。
1. 檢索要轉換為HTML文檔的PDF內容。
1. 將HTML內容轉換為PDF文檔。
1. 檢索結果。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立生成PDF客戶端**

在以寫程式方式執行「生成PDF」操作之前，必須建立「生成PDF」服務客戶端。 如果您使用Java API，請建立 `GeneratePdfServiceClient` 物件。 如果您使用網站服務API，請建立 `GeneratePDFServiceService`.

**檢索要轉換為HTML文檔的PDF內容**

參考要轉換為HTML文檔的PDF內容。 您可以參考HTML內容，例如HTML檔案或HTML內容，可透過URL存取。

**將HTML內容轉換為PDF文檔**

建立服務客戶端後，可以調用相應的PDF建立操作。 此操作需要有關要轉換的文檔的資訊，包括目標文檔的路徑。

**擷取結果**

將HTML內容轉換為PDF文檔後，可以檢索結果並保存PDF文檔。

**另請參閱**

[使用Java API將HTML內容轉換為PDF檔案](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[使用Web服務API將HTML內容轉換為PDF文檔](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[產生PDF服務API快速入門](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將HTML內容轉換為PDF檔案 {#convert-html-content-to-a-pdf-document-using-the-java-api}

使用「生成HTMLAPI(Java)」將PDF文檔轉換為PDF文檔：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-generatepdf-client.jar。

1. 建立「生成PDF」客戶端。

   建立 `GeneratePdfServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 檢索要轉換為HTML文檔的PDF內容。

   建立字串變數並指派指向HTML內容的URL，以擷取HTML內容。

1. 將HTML內容轉換為PDF文檔。

   叫用 `GeneratePdfServiceClient` 物件 `htmlToPDF2` 方法，並傳遞下列值：

   * A `java.lang.String` 包含要轉換的HTML檔案URL的物件。
   * A `java.lang.String` 包含要用於轉換的檔案類型設定的物件。 檔案類型設定可以包含尖峰層級。
   * A `java.lang.String` 包含要使用的安全設定名稱的對象。
   * 可選 `com.adobe.idp.Document` 包含在生成PDF文檔時要應用的設定的對象。 如果未提供此資訊，則會根據前三個參數自動選擇設定。
   * 可選 `com.adobe.idp.Document` 包含要應用到PDF文檔的元資料資訊的對象。

1. 檢索結果。

   此 `htmlToPDF2` 方法傳回 `HtmlToPdfResult` 包含已生成的新PDF文檔的對象。 要獲取新建立的PDF文檔，請執行以下操作：

   * 叫用 `HtmlToPdfResult` 物件 `getCreatedDocument` 方法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法，從上一步中建立的物件中擷取PDF檔案。

**另請參閱**

[將HTML文檔轉換為PDF文檔](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[快速入門（SOAP模式）:使用Java API將HTML內容轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）:使用Java API將HTML內容轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將HTML內容轉換為PDF文檔 {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

使用「產生HTMLAPI」（網站服務）將PDF內容轉換為PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立「生成PDF」客戶端。

   * 建立 `GeneratePDFServiceClient` 物件，使用其預設建構函式。
   * 建立 `GeneratePDFServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 不過，請指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `GeneratePDFServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 檢索要轉換為HTML文檔的PDF內容。

   建立字串變數並指派指向HTML內容的URL，以擷取HTML內容。

1. 將HTML內容轉換為PDF文檔。

   調用以下命令，將HTML內容轉換為PDF文檔 `GeneratePDFServiceService` 物件 `HtmlToPDF2` 方法，並傳遞下列值：

   * 包含要轉換的HTML內容的字串。
   * A `java.lang.String` 包含要用於轉換的檔案類型設定的物件。
   * 包含要使用的安全設定的字串對象。
   * 可選 `BLOB` 包含在生成PDF文檔時要應用的設定的對象。
   * 可選 `BLOB` 包含要應用到PDF文檔的元資料資訊的對象。
   * 類型的輸出參數 `BLOB` 由 `CreatePDF2` 方法。 此 `CreatePDF2` 方法會以轉換的檔案填入此物件。 （此參數值僅對於Web服務調用是必需的）。

1. 檢索結果。

   * 通過分配 `BLOB` 物件 `MTOM` 欄位至位元組陣列。 位元組陣清單示轉換的PDF文檔。 請確定您使用 `BLOB` 用作 `HtmlToPDF2` 方法。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示已轉換PDF文檔的檔案位置。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[將HTML文檔轉換為PDF文檔](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將PDF文檔轉換為非影像格式 {#converting-pdf-documents-to-non-image-formats}

本節介紹如何使用生成PDFJava API和Web服務API，以寫程式方式將PDF文檔轉換為RTF檔案，這是非影像格式的示例。 其他非影像格式包括HTML、文字、DOC和EPS。 將PDF文檔轉換為RTF時，請確保PDF文檔不包含表單元素，如提交按鈕。 表單元素不會轉換。

>[!NOTE]
>
>如需產生PDF服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-2}

要將PDF文檔轉換為任何支援的類型，請執行以下步驟：

1. 包含專案檔案。
1. 建立「生成PDF」客戶端。
1. 檢索要轉換的PDF文檔。
1. 轉換PDF文檔。
1. 儲存轉換的檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立生成PDF客戶端**

在以寫程式方式執行「生成PDF」操作之前，必須建立「生成PDF」服務客戶端。 如果您使用Java API，請建立 `GeneratePdfServiceClient` 物件。 如果您使用網站服務API，請建立 `GeneratePDFServiceService` 物件。

**檢索要轉換的PDF文檔**

檢索PDF文檔以轉換為非影像格式。

**轉換PDF文檔**

建立服務客戶端後，可以調用PDF導出操作。 此操作需要有關要轉換的文檔的資訊，包括目標文檔的路徑。

**儲存轉換的檔案**

儲存轉換的檔案。 例如，如果將PDF文檔轉換為RTF檔案，請將轉換的文檔保存為RTF檔案。

**另請參閱**

[使用Java API將PDF文檔轉換為RTF檔案](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[使用Web服務API將PDF文檔轉換為RTF檔案](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[產生PDF服務API快速入門](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF文檔轉換為RTF檔案 {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

使用生成PDFAPI(Java)將PDF文檔轉換為RTF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-generatepdf-client.jar。

1. 建立「生成PDF」客戶端。

   建立 `GeneratePdfServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 檢索要轉換的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示要使用其建構子轉換的PDF文檔的對象。 傳遞指定PDF文檔位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 轉換PDF文檔。

   叫用 `GeneratePdfServiceClient` 物件 `exportPDF2` 方法，並傳遞下列值：

   * A `com.adobe.idp.Document` 表示要轉換的PDF檔案的對象。
   * A `java.lang.String` 包含要轉換的檔案名稱的對象。
   * A `java.lang.String` 包含Adobe PDF設定名稱的物件。
   * A `ConvertPDFFormatType` 指定轉換目標檔案類型的對象。
   * 可選 `com.adobe.idp.Document` 包含在生成PDF文檔時要應用的設定的對象。

   此 `exportPDF2` 方法傳回 `ExportPDFResult` 包含轉換檔案的物件。

1. 轉換PDF文檔。

   要獲取新建立的檔案，請執行以下步驟：

   * 叫用 `ExportPDFResult` 物件 `getConvertedDocument` 方法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法來擷取新檔案。

**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API將HTML內容轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將PDF文檔轉換為RTF檔案 {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

使用生成PDFAPI（Web服務）將PDF文檔轉換為RTF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立生成PDf客戶端。

   * 建立 `GeneratePDFServiceClient` 物件，使用其預設建構函式。
   * 建立 `GeneratePDFServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 不過，請指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `GeneratePDFServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 檢索要轉換的PDF文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存轉換的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過為其分配 `MTOM` 屬性位元組陣列的內容。

1. 轉換PDF文檔。

   叫用 `GeneratePDFServiceServiceWse` 物件 `ExportPDF2` 方法，並傳遞下列值：

   * A `BLOB` 表示要轉換的PDF檔案的對象。
   * 包含要轉換的檔案路徑名的字串。
   * A `java.lang.String` 指定檔案位置的對象。
   * 指定轉換目標檔案類型的字串對象。 指定 `RTF`.
   * 可選 `BLOB` 包含在生成PDF文檔時要應用的設定的對象。
   * 類型的輸出參數 `BLOB` 由 `ExportPDF2` 方法。 此 `ExportPDF2` 方法會以轉換的檔案填入此物件。 （此參數值僅對於Web服務調用是必需的）。

1. 儲存轉換的檔案。

   * 通過分配 `BLOB` 物件 `MTOM` 欄位至位元組陣列。 位元組陣清單示轉換的RTF文檔。 請確定您使用 `BLOB` 用作 `ExportPDF2` 方法。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞表示RTF檔案位置的字串值。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 新增對其他原生檔案格式的支援 {#adding-support-for-additional-native-file-formats}

本節說明如何新增對其他原生檔案格式的支援。 它概述了生成PDF服務與本服務用於將本機檔案格式轉換為PDF的本機應用程式之間的交互。

本節也說明下列內容：

* 如何修改生成PDF服務提供給本機應用程式的響應，而本產品已使用這些響應將本機檔案格式轉換為PDF
* 「生成PDF」服務、「生成PDF服務應用程式監視器」(AppMon)元件和本機應用程式(如Microsoft Word)之間的交互
* XML語法在這些交互中所扮演的角色

### 元件互動 {#component-interactions}

「生成PDF」服務通過調用與檔案格式關聯的應用程式，然後與應用程式交互以使用預設打印機打印文檔來轉換本機檔案格式。 預設打印機必須設定為Adobe PDF打印機。

此圖顯示了與本機應用程式支援相關的元件和驅動程式。 它還提到影響交互的XML文法。

原生檔案轉換的元件互動

本檔案使用 *原生應用程式* 指示用於產生原生檔案格式的應用程式，如Microsoft Word。

*AppMon* 是企業元件，與原生應用程式互動的方式與使用者瀏覽該應用程式所顯示對話方塊的方式相同。 AppMon用來指示應用程式(如Microsoft Word)開啟和打印涉及以下順序任務的檔案的XML語法：

1. 選取「檔案」>「開啟」以開啟檔案
1. 確保顯示「開啟」對話框；否則，處理錯誤
1. 在「檔案名」欄位中提供檔案名，然後按一下「開啟」按鈕
1. 確保檔案實際開啟
1. 通過選擇「檔案」>「打印」開啟「打印」對話框
1. 確保顯示「打印」對話框

AppMon使用標準的Win32 API與第三方應用程式交互，以傳輸UI事件，如按鍵和滑鼠點擊，這對控制這些應用程式以從它們生成PDF檔案非常有用。

由於這些Win32 API的限制，AppMon無法將這些UI事件發送到某些特定類型的窗口，如浮動菜單欄（在TextPad等應用程式中找到），以及某些類型的對話框，其內容無法使用Win32 API檢索。

直觀地識別浮動菜單條很容易；但是，可能無法僅通過視覺檢查來確定特殊類型的對話。 您需要第三方應用程式，如Microsoft Spy++(Microsoft Visual C++開發環境的一部分)或其等效的WinID（可免費從以下位置下載） [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID))來檢查對話方塊，以判斷AppMon是否能使用標準Win32 API與其互動。

如果WinID能夠提取對話框內容，如文本、子窗口、窗口類ID等，則AppMon也能夠提取這些內容。

此表列出了打印本機檔案格式時使用的資訊類型。

<table>
 <thead>
  <tr>
   <th><p>資訊類型</p></th>
   <th><p>說明</p></th>
   <th><p>修改/建立與本機檔案相關的條目 </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>管理設定 </p></td>
   <td><p>包括PDF設定、安全設定和檔案類型設定。 </p><p>檔案類型設定將檔案名副檔名與相應的本機應用程式關聯。 檔案類型設定還指定用於打印本機檔案的本機應用程式設定。 </p></td>
   <td><p>要更改已支援的本機應用程式的設定，系統管理員在管理控制台中設定「檔案類型設定」。 </p><p>若要新增對新原生檔案格式的支援，您必須手動編輯檔案。 (請參閱 <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">添加或修改對本機檔案格式的支援</a>.) </p></td>
  </tr>
  <tr>
   <td><p>指令碼 </p></td>
   <td><p>指定「生成PDF」服務與本機應用程式之間的交互。 這類交互通常指導應用程式將檔案打印到Adobe PDF驅動程式。 </p><p>該指令碼包含指導本機應用程式開啟特定對話框的說明，以及對這些對話框中的欄位和按鈕提供特定響應的說明。 </p></td>
   <td><p>「生成PDF」服務包含所有受支援本機應用程式的指令碼檔案。 您可以使用XML編輯應用程式修改這些檔案。</p><p>要添加對新本機應用程式的支援，必須建立新的指令碼檔案。 (請參閱 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">為本機應用程式建立或修改其他對話框XML檔案</a>.) </p></td>
  </tr>
  <tr>
   <td><p>一般對話方塊指示 </p></td>
   <td><p>指定如何響應多個應用程式共用的對話框。 這些對話框由作業系統、輔助應用程式（如PDFMaker）和驅動程式生成。 </p><p>包含此資訊的檔案為appmon.global.en_US.xml。</p></td>
   <td><p>請勿修改此檔案。 </p></td>
  </tr>
  <tr>
   <td><p>特定於應用程式的對話框說明</p></td>
   <td><p>指定如何響應特定於應用程式的對話框。 </p><p>包含此資訊的檔案為appmon。<i>'[appname]'</i>對話框。<i>'[locale]'</i>.xml（例如appmon.word.en_US.xml）。</p></td>
   <td><p>請勿修改此檔案。 </p><p>要為新的本機應用程式添加對話框說明，請參閱 <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">為本機應用程式建立或修改其他對話框XML檔案</a>.</p></td>
  </tr>
  <tr>
   <td><p>其他特定於應用程式的對話框說明 </p></td>
   <td><p>指定應用程式特定對話框指令的覆蓋和添加。 本節提供此類資訊的示例。 </p><p>包含此資訊的檔案為appmon。<i>'[appname]'</i>新增。<i>'[locale]'</i>.xml。 例如appmon.addition.en_US.xml。</p></td>
   <td><p>可使用XML編輯應用程式建立和修改此類型的檔案。 (請參閱 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">為本機應用程式建立或修改其他對話框XML檔案</a>.) </p><p><strong>重要</strong>:您必須為伺服器將支援的每個本機應用程式建立其他特定於應用程式的對話方塊指示。 </p></td>
  </tr>
 </tbody>
</table>

### 關於指令碼和對話框XML檔案 {#about-the-script-and-dialog-xml-files}

指令碼XML檔案指示「生成PDF」服務導航應用程式對話框，與用戶導航應用程式對話框的方式相同。 指令碼XML檔案還指示「生成」PDF服務通過執行按鈕、選擇或取消選擇複選框或選擇菜單項等操作來響應對話框。

相反地，對話框XML檔案只是以指令碼XML檔案中使用的相同類型的操作響應對話框。

#### 對話框和窗口元素術語 {#dialog-box-and-window-element-terminology}

本節和下一節將根據所描述的透視，對對話框及其包含的元件使用不同的術語。 對話框元件是按鈕、欄位和組合框等項。

當本節和下一節從用戶的角度描述對話框及其元件時，如 *對話框*, *按鈕*, *欄位*，和 *組合框* 中所有規則的URL區段。

當本節和下一節從其內部表示的角度描述對話框及其元件時，該術語 *視窗元素* 中所有規則的URL區段。 窗口元素的內部表示是層次，其中每個窗口元素實例由標籤標識。 窗口元素實例還描述了其物理特性和行為。

從用戶的角度來看，對話框及其元件顯示不同的行為，其中某些對話框元素在激活之前處於隱藏狀態。 從內部代表的角度看，不存在此類行為問題。 例如，對話框的內部表示與包含的元件相似，但該元件在對話框內嵌套除外。

本節介紹為AppMon提供說明的XML元素。 這些元素的名稱如 `dialog` 元素和 `window` 元素。 本文檔使用單行字型來區分XML元素。 此 `dialog` 元素標識XML指令碼檔案可能導致顯示的對話框，有意或無意。 此 `window` 元素標識窗口元素（對話框或對話框的元件）。

#### 階層 {#hierarchy}

此圖表顯示指令碼和對話框XML的層次結構。 指令碼XML檔案符合script.xsd架構，該架構包括（在XML意義中）window.xsd架構。 同樣地，對話框XML檔案符合dialogs.xsd架構，其中也包含window.xsd架構。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

指令碼和對話框XML的層次

#### 指令碼XML檔案 {#script-xml-files}

A *指令碼XML檔案* 指定一系列步驟，這些步驟引導本地應用程式導航到某些窗口元素，然後提供對這些元素的響應。 大多數響應是文本或擊鍵，它們與用戶在相應對話框中提供的欄位、組合框或按鈕的輸入相對應。

「生成PDF」服務對指令碼XML檔案的支援目的是指導本機應用程式打印本機檔案。 但是，指令碼XML檔案可用於完成用戶在與本機應用程式的對話框交互時可以執行的任何任務。

指令碼XML檔案中的步驟會依序執行，不會有任何分支的機會。 唯一支援的條件式測試是超時/重試，如果某個步驟在特定時間段內和特定重試次數之後未成功完成，則會導致指令碼終止。

除了循序步驟之外，步驟內的指令也依序執行。 您必須確保步驟和指示反映使用者執行這些步驟的順序。

指令碼XML檔案中的每個步驟都標識了如果成功執行了步驟的指令，則預期會出現的窗口元素。 如果執行指令碼步驟時出現意外的對話框，則生成PDF服務將按下一節中所述搜索對話框XML檔案。

#### 對話框XML檔案 {#dialog-xml-files}

運行本地應用程式會顯示不同的對話框，無論本地應用程式處於可見模式還是不可見模式，都會顯示這些對話框。 對話框可由作業系統或應用程式本身生成。 當本機應用程式在「生成PDF」服務的控制下運行時，系統和本機應用程式對話框將顯示在不可見窗口中。

A *對話框XML檔案* 指定「生成PDF」服務如何響應系統或本機應用程式對話框。 對話框XML檔案允許生成PDF服務以有助於轉換過程的方式響應未提示的對話框。

當系統或本機應用程式顯示一個當前執行的指令碼XML檔案未處理的對話框時，生成PDF服務將按此順序搜索對話框XML檔案，當它找到匹配項時停止：

* appmon。`[appname]`其他。`[locale]`.xml
* appmon。`[appname]`。`[locale]`.xml（請勿修改此檔案。）
* appmon.global.`[locale]`.xml（請勿修改此檔案。）

如果「生成PDF」服務找到對話框的匹配項，則通過發送為對話框指定的擊鍵或其他操作將其關閉。 如果對話框的指令指定了中止消息，則生成PDF服務將終止當前執行的作業並生成錯誤消息。 此類中止訊息將在 `abortMessage` 元素。

如果「生成PDF」服務遇到的對話框未在先前列出的任何檔案中描述，則生成PDF服務會將對話框的標題併入日誌檔案條目中。 當前執行的作業最終超時。 然後，您可以使用日誌檔案中的資訊，在本機應用程式的其他對話框XML檔案中合成新指令。

### 添加或修改對本機檔案格式的支援 {#adding-or-modifying-support-for-a-native-file-format}

本節介紹為支援其他本機檔案格式或修改對已支援本機檔案格式的支援而必須執行的任務。

您必須先完成下列工作，才能新增或修改支援。

#### 選擇用於標識窗口元素的工具 {#choosing-a-tool-for-identifying-window-elements}

對話框和指令碼XML檔案要求您標識對話框或指令碼元素要響應的窗口元素（對話框、欄位或其他對話框元件）。 例如，在指令碼調用本地應用程式的菜單後，指令碼必須標識該菜單上要應用擊鍵或操作的窗口元素。

通過標題欄中顯示的標題，可以輕鬆識別對話框。 但是，必須使用Microsoft Spy++等工具來標識較低級別的窗口元素。 可以通過各種屬性來識別較低級別的窗口元素，這些屬性並不明顯。 此外，每個本機應用程式可以不同地識別其窗口元素。 因此，有多種方式可識別視窗元素。 以下是考慮窗口元素標識的建議順序：

1. 註解本身（如果它是唯一的）
1. 控制ID，它對於指定對話框可能唯一，也可能不唯一
1. 類名，可能唯一，也可能不唯一

這三個屬性的任何一個或組合都可以用來識別視窗。

如果屬性無法識別標題，則可以改為使用相對於其父項的索引來識別窗口元素。 安 *索引* 指定窗口元素相對於其同級窗口元素的位置。 索引通常是標識組合框的唯一方法。

請注意下列問題：

* Microsoft Spy++使用&amp;符號來識別字幕的熱鍵，從而顯示字幕。 例如，Spy++將一個「打印」對話框的標題顯示為 `Pri&nt`，表示快捷鍵為 *n*. 指令碼和對話框XML檔案中的標題必須忽略&amp;符號。
* 有些字幕包括分行。 「生成PDF」服務無法標識分行。 如果標題包括分行符，則包括足夠的標題以將其與其他菜單項區分，然後對省略的部分使用規則表達式。 例如( `^Long caption title$`)。 (請參閱 [在註解屬性中使用規則運算式](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes).)
* 對保留的XML字元使用字元實體（也稱為轉義序列）。 例如，使用 `&` 對於&amp;符號， `<` 和 `>` 小於和大於符號， `&apos;` 撇號和 `&quot;` 引號。

如果您打算使用對話框或指令碼XML檔案，則應安裝應用程式Microsoft Spy++。

#### 取消對對話框和指令碼檔案的打包 {#unpackaging-the-dialog-and-script-files}

對話方塊和指令碼檔案位於appmondata.jar檔案中。 在可以修改其中任何檔案或添加新指令碼或對話框檔案之前，必須取消包裝此JAR檔案。 例如，假設您要添加對EditPlus應用程式的支援。 建立兩個XML檔案，名為appmon.editplus.script.en_US.xml和appmon.editplus.script.addition.en_US.xml。 必須將這些XML指令碼新增至adobe-appmondata.jar檔案中的兩個位置，如下所指定：

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon。 adobe-livecycle-native-jboss-x86_win32.ear檔案位於的匯出資料夾中 `[AEM forms install directory]\configurationManager`. (如果AEM Forms部署在其他J2EE應用程式伺服器上，請以與您的J2EE應用程式伺服器對應的EAR檔案取代adobe-livecycle-native-jboss-x86_win32.ear檔案。)
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon （adobe-appmondata.jar檔案位於adobe-generatepdf-dsc.jar檔案內）。 adobe-generatepdf-dsc.jar檔案位於 `[AEM forms install directory]\deploy` 檔案夾。

將這些XML檔案新增至adobe-appmondata.jar檔案後，您必須重新部署GeneratePDF元件。 若要將對話方塊和指令碼XML檔案新增至adobe-appmondata.jar檔案，請執行下列工作：

1. 使用WinZip或WinRAR等工具，開啟adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar檔案。
1. 將對話框和指令碼XML檔案添加到appmondata.jar檔案中，或修改此檔案中的現有XML檔案。 (請參閱 [為本機應用程式建立或修改指令碼XML檔案](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)和 [為本機應用程式建立或修改其他對話框XML檔案](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).)
1. 使用WinZip或WinRAR等工具，開啟adobe-generatepdf-dsc.jar > adobe-appmondata.jar。
1. 將對話框和指令碼XML檔案添加到appmondata.jar檔案中，或修改此檔案中的現有XML檔案。 (請參閱 [為本機應用程式建立或修改指令碼XML檔案](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)和 [為本機應用程式建立或修改其他對話框XML檔案](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).) 將XML檔案新增至adobe-appmondata.jar檔案後，請將新的adobe-appmondata.jar檔案放入adobe-generatepdf-dsc.jar檔案中。
1. 如果添加了對其他本機檔案格式的支援，請建立提供應用程式路徑的系統環境變數(請參閱 [建立環境變數以找出原生應用程式](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application).)

**重新部署GeneratePDF元件**

1. 登入Workbench。
1. 選擇 **視窗** > **顯示視圖** > **元件**. 此動作會將「元件」檢視新增至Workbench。
1. 按一下右鍵GeneratePDF元件，然後選擇 **停止元件**.
1. 元件停止後，按一下右鍵並選擇「卸載元件」將其刪除。
1. 以滑鼠右鍵按一下 **元件** 圖示並選取 **安裝元件**.
1. 瀏覽並選取修改的adobe-generatepdf-dsc.jar檔案，然後按一下「開啟」。 請注意， GeneratePDF元件旁會出現一個紅方。
1. 展開GeneratePDF元件，選擇服務描述符，然後按一下右鍵GeneratePDFService並選擇激活服務。
1. 在顯示的設定對話方塊中，輸入適用的設定值。 若將這些值保留為空白，則會使用預設設定值。
1. 按一下右鍵「生成PDF」，然後選擇「啟動元件」。
1. 展開「活動服務」。 服務名稱（如果正在運行）旁會出現綠色箭頭。 否則，服務處於停止狀態。
1. 如果服務處於停止狀態，請按一下右鍵服務名稱，然後選擇啟動服務。

### 為本機應用程式建立或修改指令碼XML檔案 {#creating-or-modifying-a-script-xml-file-for-a-native-application}

如果要將檔案導向到新的本機應用程式，必須為該應用程式建立指令碼XML檔案。 如果要修改生成PDF服務與已支援的本機應用程式交互的方式，則必須修改該應用程式的指令碼。

指令碼包含在本機應用程式的窗口元素中導航的指令，並為這些元素提供特定響應。 包含此資訊的檔案為 `appmon.`[appname]&quot; `.script.`[地區]`.xml`. 例如appmon.notepad.script.en_US.xml。

#### 識別指令碼必須執行的步驟 {#identifying-steps-the-script-must-execute}

使用本機應用程式確定必須導航的窗口元素以及必須執行的打印文檔的每個響應。 請注意任何回應產生的對話方塊。 步驟將類似於以下步驟：

1. 選擇「檔案」>「開啟」。
1. 指定路徑，然後按一下「開啟」。
1. 在菜單欄上選擇檔案>打印。
1. 指定打印機所需的屬性。
1. 選擇「打印」並等待「另存為」對話框出現。 「生成PDF」服務需要「另存新檔」對話框來指定PDF檔案的目標。

#### 標識在字幕屬性中指定的對話框 {#identifying-the-dialogs-specified-in-caption-attributes}

使用Microsoft Spy++獲取本機應用程式中窗口元素屬性的標識。 您必須有這些身分才能編寫指令碼。

#### 在註解屬性中使用規則運算式 {#using-regular-expressions-in-caption-attributes}

您可以在註解規格中使用規則運算式。 產生PDF服務使用 `java.util.regex.Matcher` 類別來支援規則運算式。 該公用程式支援下列章節所述的規則運算式： `java.util.regex.Pattern`.

**在記事本橫幅中，可容納在記事本前面的檔案名的規則運算式**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**規則運算式區分打印和打印設定**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### 對窗口和windowList元素排序 {#ordering-the-window-and-windowlist-elements}

您必須訂購 `window` 和 `windowList` 元素，如下所示：

* 多個 `window` 元素在 `windowList` 或 `dialog` 元素，排序 `window` 元素，長度由 `caption` 表示順序中位置的名稱。
* 多個 `windowList` 元素會出現在 `window` 元素，排序 `windowList` 元素，長度由 `caption` 第一個屬性 `indexes/`表示順序中位置的元素。

**對對話框檔案中的窗口元素進行排序**

```xml
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

**在windowList元素內排序窗口元素**

```xml
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

### 為本機應用程式建立或修改其他對話框XML檔案 {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

如果為以前不支援的本機應用程式建立指令碼，則還必須為該應用程式建立一個附加的對話框XML檔案。 AppMon使用的每個本機應用程式都只能有一個額外的對話XML檔案。 即使沒有未請求的對話框，也需要附加的對話框XML檔案。 其他對話框必須至少有一個 `window` 元素，即使 `window` 元素只是預留位置。

>[!NOTE]
>
>在此情境中，「額外」一詞表示 `appmon.[applicationname].addition.[locale].xml` 檔案。 此類檔案指定對話XML檔案的覆蓋和添加。

您還可以為以下目的修改本機應用程式的其他對話框XML檔案：

* 用不同的響應覆蓋應用程式的對話框XML檔案
* 向該應用程式的對話框XML檔案中未定址的對話框添加響應

標識其他dialogXML檔案的檔案名為 `appmon.[appname].addition.[locale].xml`. 例如appmon.excel.addition.en_US.xml。

其他對話框XML檔案的名稱必須使用格式 `appmon.[applicationname].addition.[locale].xml`，其中 *應用程式名稱* 必須與XML配置檔案和指令碼中使用的應用程式名稱完全匹配。

>[!NOTE]
>
>native2pdfconfig.xml配置檔案中指定的所有通用應用程式都沒有主對話框XML檔案。 區段 [添加或修改對本機檔案格式的支援](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) 描述了這些規範。

您必須訂購 `windowList` 在 `window` 元素。 (請參閱 [對窗口和windowList元素排序](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements).)

### 修改常規對話框XML檔案 {#modifying-the-general-dialog-xml-file}

可以修改常規對話框XML檔案以響應系統生成的對話框或響應多個應用程式共同的對話框。

#### 在XML配置檔案中添加檔案類型條目 {#adding-a-filetype-entry-in-the-xml-configuration-file}

此過程說明如何更新生成PDF服務配置檔案，以將檔案類型與本機應用程式關聯。 要更新此配置檔案，必須使用管理控制台將配置資料導出到檔案。 配置資料的預設檔案名為native2pdfconfig.xml。

**更新生成PDF服務配置檔案**

1. 選擇 **首頁** > **服務** > **Adobe PDF Generator** > **組態檔**，然後選取 **匯出設定**.
1. 修改 `filetype-settings` 元素（視需要）。
1. 選擇 **首頁** > **服務** > **Adobe PDF Generator** >**組態檔**，然後選取 **匯入設定**. 配置資料將導入「生成PDF」服務，替換先前的設定。

>[!NOTE]
>
>應用程式的名稱會指定為 `GenericApp` 元素 `name` 屬性。 此值必須與您在為該應用程式開發的指令碼中指定的對應名稱完全相符。 同樣， `GenericApp` 元素 `displayName` 屬性應完全符合對應指令碼的 `expectedWindow` 窗口標題。 解析任何出現在 `displayName` 或 `caption` 屬性。

在此示例中，已修改「生成PDF」服務提供的預設配置資料，以指定應使用記事本(而不是Microsoft Word)來處理副檔名為.txt的檔案。 在此修改前，已將Microsoft Word指定為應處理此類檔案的原生應用程式。

**將文本檔案導向到記事本(native2pdfconfig.xml)的修改**

```xml
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

#### 建立環境變數以找出原生應用程式 {#creating-an-environment-variable-to-locate-the-native-application}

建立環境變數，指定本機應用程式執行檔的位置。 變數必須使用格式 `[applicationname]_PATH`，其中 *應用程式名稱* 必須與XML配置檔案和指令碼中使用的應用程式名稱完全匹配，且其中路徑包含雙引號中執行檔的路徑。 此類環境變數的範例為 `Photoshop_PATH`.

建立新環境變數後，必須重新啟動部署了「生成PDF」服務的伺服器。

**在Windows XP環境中建立系統變數**

1. 選擇 **控制面板>系統**.
1. 在「系統屬性」(System Properties)對話框中，按一下 **進階** ，然後按一下 **環境變數**.
1. 在「環境變數」對話框中的「系統變數」下，按一下 **新增**.
1. 在「新建系統變數」(New System Variable)對話框中， **變數名稱** 框中，鍵入使用格式的名稱 `[applicationname]_PATH`.
1. 在 **變數值** 框中，鍵入應用程式執行檔的完整路徑和檔案名，然後按一下 **確定**. 例如，輸入： `c:\windows\Notepad.exe`
1. 在「環境變數」對話方塊中，按一下 **確定**.

**從命令列建立系統變數**

1. 在命令列視窗中，使用以下格式輸入變數定義：

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   例如，輸入： `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. 啟動新的命令行提示，使系統變數生效。

#### XML檔案 {#xml-files}

AEM Forms包含範例XML檔案，這些檔案會導致「產生PDF」服務使用記事本來處理任何副檔名為.txt的檔案。 本節包含此程式碼。 此外，您必須進行本節所述的其他修改。

#### 其他對話框XML檔案 {#additional-dialog-xml-file}

此示例包含記事本應用程式的其他對話框。 除了「生成PDF」服務指定的對話框之外，還可以使用這些對話框。

**記事對話框(appmon.notepad.addition.en_US.xml)**

```xml
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### 指令碼XML檔案 {#script-xml-file}

此示例指定生成PDF服務應如何與記事本交互，以使用Adobe PDF打印機打印檔案。

**記事本指令碼XML檔案(appmon.notepad.script.en_US.xml)**

```xml
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
