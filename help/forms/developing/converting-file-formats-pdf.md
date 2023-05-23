---
title: 在檔案格式和PDF之間轉換
seo-title: Converting Between File Formats and PDF
description: 使用「生成PDF」服務將本機檔案格式轉換為PDF。 生成PDF服務還將PDF轉換為其他檔案格式，並優化PDF文檔的大小。
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

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於生成PDF服務**

「生成PDF」服務將本機檔案格式轉換為PDF。 它還將PDF轉換為其他檔案格式，並優化PDF文檔的大小。

「生成PDF」服務使用本機應用程式將以下檔案格式轉換為PDF。 除非另有說明，否則僅支援這些應用程式的德文、法文、英文和日文版本。 *僅Windows* 表示僅支援Windows Server® 2003和Windows Server 2008。

* MicrosoftOffice 2003和2007轉換DOC、DOCX、RTF、TXT、XLS、XLS、PPT、PPTX、VSD、MPPX、XPS和PUB（僅限Windows）

>[!NOTE]
>
>Acrobat® 9.2或更高版本需要將MicrosoftXPS格式轉換為PDF。

* Autodesk AutoCAD 2005、2006、2007、2008和2009轉換DWF、DWG和DXW（僅限英文）
* Corel WordPerfect 12和X4轉換WPD、QPW、SHW（僅英文）
* OpenOffice 2.0、2.4、3.0.1和3.1轉換ODT、ODS、ODP、ODG、ODF、SXW、SXI、SXC、DOC、DOCX、RTF、XLSX、PPT、PPTX、VSD、MPP、MPPX和PUB

>[!NOTE]
>
>生成PDF服務不支援64位版本的OpenOffice。

* Adobe Photoshop® CS2轉換PSD（僅限Windows）

>[!NOTE]
>
>PhotoshopCS3和CS4不受支援，因為它們不支援Windows Server 2003或Windows Server 2008。

* Adobe FrameMaker® 7.2和8轉換FM（僅限Windows）
* AdobePageMaker® 7.0轉換PMD、PM6、P65和PM（僅限Windows）
* 第三方應用程式支援的本機格式（需要開發特定於應用程式的安裝檔案）（僅限Windows）

「生成PDF」服務將以下基於標準的檔案格式轉換為PDF。

* 視頻格式：SWF, FLV（僅限Windows）
* 影像格式：JPEG、JPG、JP2、J2Kí、JPC、J2C、GIF、BMP、TIFF、TIF、PNG、JPF
* HTML（Windows、Sun™ Solaris™和Linux®）

「生成PDF」服務將PDF轉換為以下檔案格式（僅限Windows）:

* 封裝的PostScript(EPS)
* HTML3.2
* HTML4.01，帶CSS 1.0
* DOC(MicrosoftWord格式)
* RTF
* 文本（可訪問和純文字檔案）
* XML
* PDF/A-1a，僅使用DeviceRGB顏色空間
* PDF/A-1b，僅使用DeviceRGB顏色空間

生成PDF服務要求您執行以下管理任務：

* 在托管AEM Forms的電腦上安裝所需的本機應用程式
* 在托管Adobe Acrobat的電腦上安裝Acrobat Pro專業版9.2
* 執行安裝後安裝任務

這些任務在使用JBoss Tunky安裝和部AEM署表單中介紹。

您可以使用「生成PDF」服務完成以下任務：

* 從本機檔案格式轉換為PDF。
* 將HTML文檔轉換為PDF文檔。
* 將PDF文檔轉換為檔案格式。

>[!NOTE]
>
>有關生成PDF服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將Word文檔轉換為PDF文檔 {#converting-word-documents-to-pdf-documents}

本節介紹如何使用「生成PDFAPI」以寫程式方式將MicrosoftWord文檔轉換為PDF文檔。

>[!NOTE]
>
>有關其他檔案格式的詳細資訊，請參見 [添加對其他本機檔案格式的支援](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)。

>[!NOTE]
>
>有關生成PDF服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要將MicrosoftWord文檔轉換為PDF文檔，請執行以下任務：

1. 包括項目檔案。
1. 建立生成PDF客戶端。
1. 檢索要轉換為PDF文檔的檔案。
1. 將檔案轉換為PDF文檔。
1. 檢索結果。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立生成PDF客戶端**

在以寫程式方式執行「生成PDF」操作之前，請建立「生成PDF」服務客戶端。 如果使用Java API，請建立 `GeneratePdfServiceClient` 的雙曲餘切值。 如果使用Web服務API，請建立 `GeneratePDFServiceService` 的雙曲餘切值。

**檢索要轉換為PDF文檔的檔案**

檢索要轉換為Microsoft文檔的PDFWord文檔。

**將檔案轉換為PDF文檔**

建立「生成PDF」服務客戶端後，可以調用 `createPDF2` 的雙曲餘切值。 此方法需要有關要轉換的文檔的資訊，包括檔案副檔名。

**檢索結果**

將檔案轉換為PDF文檔後，可以檢索結果。 例如，將Word檔案轉換為PDF文檔後，可以檢索和保存PDF文檔。

**另請參閱**

[使用Java API將Word文檔轉換為PDF文檔](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[使用Web服務API將Word文檔轉換為PDF文檔](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[生成PDF服務API快速啟動](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將Word文檔轉換為PDF文檔 {#convert-word-documents-to-pdf-documents-using-the-java-api}

使用「生成MicrosoftAPI(Java)」將PDFWord文檔轉換為PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-generatepdf-client.jar。

1. 建立生成PDF客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `GeneratePdfServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索要轉換為PDF文檔的檔案。

   * 建立 `java.io.FileInputStream` 表示要使用其建構子轉換的Word檔案的對象。 傳遞指定檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 將檔案轉換為PDF文檔。

   通過調用 `GeneratePdfServiceClient` 對象 `createPDF2` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示要轉換的檔案的對象。
   * A `java.lang.String` 包含檔案副檔名的對象。
   * A `java.lang.String` 包含要在轉換中使用的檔案類型設定的對象。 檔案類型設定為不同檔案類型(如.doc或.xls)提供轉換設定。
   * A `java.lang.String` 包含要使用的PDF設定名稱的對象。 例如，可以指定 `Standard`。
   * A `java.lang.String` 包含要使用的安全設定名稱的對象。
   * 可選 `com.adobe.idp.Document` 包含生成PDF文檔時要應用的設定的對象。
   * 可選 `com.adobe.idp.Document` 包含要應用到PDF文檔的元資料資訊的對象。

   的 `createPDF2` 方法返回 `CreatePDFResult` 包含新PDF文檔和日誌資訊的對象。 日誌檔案通常包含由轉換請求生成的錯誤或警告消息。

1. 檢索結果。

   要獲取PDF文檔，請執行以下操作：

   * 調用 `CreatePDFResult` 對象 `getCreatedDocument` 方法，它返回 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法從上一步建立的對象中提取PDF文檔。

   如果你用 `createPDF2` 方法獲取日誌文檔(不適用於HTML轉換)，請執行以下操作：

   * 調用 `CreatePDFResult` 對象 `getLogDocument` 的雙曲餘切值。 這返回 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法提取日誌文檔。


**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API將MicrosoftWord文檔轉換為PDF文檔](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將Word文檔轉換為PDF文檔 {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

使用生成MicrosoftAPI（Web服務）將Word文檔轉換為PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立生成PDF客戶端。

   * 建立 `GeneratePDFServiceClient` 對象。
   * 建立 `GeneratePDFServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`。) 你不需要 `lc_version` 屬性。 但是，請指定 `?blob=mtom`。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `GeneratePDFServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 檢索要轉換為PDF文檔的檔案。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存要轉換為PDF文檔的檔案。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示要轉換的檔案的位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過為對象分配 `MTOM` 屬性位元組陣列的內容。

1. 將檔案轉換為PDF文檔。

   通過調用 `GeneratePDFServiceService` 對象 `CreatePDF2` 方法並傳遞以下值：

   * A `BLOB` 表示要轉換的檔案的對象。
   * 包含檔案副檔名的字串。
   * A `java.lang.String` 包含要在轉換中使用的檔案類型設定的對象。 檔案類型設定為不同檔案類型(如.doc或.xls)提供轉換設定。
   * 包含要使用的PDF設定的字串對象。 可以指定 `Standard`。
   * 包含要使用的安全設定的字串對象。 可以指定 `No Security`。
   * 可選 `BLOB` 包含生成PDF文檔時要應用的設定的對象。
   * 可選 `BLOB` 包含要應用到PDF文檔的元資料資訊的對象。
   * 類型的輸出參數 `BLOB` 是由 `CreatePDF2` 的雙曲餘切值。 的 `CreatePDF2` 方法使用轉換的文檔填充此對象。 （此參數值僅對於Web服務調用是必需的）。
   * 類型的輸出參數 `BLOB` 是由 `CreatePDF2` 的雙曲餘切值。 的 `CreatePDF2` 方法使用日誌文檔填充此對象。 （此參數值僅對於Web服務調用是必需的）。

1. 檢索結果。

   * 通過分配已轉換的PDF文檔 `BLOB` 對象 `MTOM` 欄位。 位元組陣列表示已轉換的PDF文檔。 確保使用 `BLOB` 用作輸出參數的對象 `createPDF2` 的雙曲餘切值。
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示轉換的PDF文檔的檔案位置。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將HTML文檔轉換為PDF文檔 {#converting-html-documents-to-pdf-documents}

本節介紹如何使用「生成PDFAPI」以寫程式方式將HTML文檔轉換為PDF文檔。

>[!NOTE]
>
>有關生成PDF服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要將HTML文檔轉換為PDF文檔，請執行以下任務：

1. 包括項目檔案。
1. 建立生成PDF客戶端。
1. 檢索要轉換為HTML文檔的PDF內容。
1. 將HTML內容轉換為PDF文檔。
1. 檢索結果。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立生成PDF客戶端**

在以寫程式方式執行「生成PDF」操作之前，必須建立「生成PDF」服務客戶端。 如果使用Java API，請建立 `GeneratePdfServiceClient` 的雙曲餘切值。 如果使用Web服務API，請建立 `GeneratePDFServiceService`。

**檢索要轉換為HTML文檔的PDF內容**

要轉換為HTML文檔的引用PDF內容。 您可以引用HTML內容，如可使用URL訪問的HTML檔案或HTML內容。

**將HTML內容轉換為PDF文檔**

建立服務客戶端後，可以調用相應的PDF建立操作。 此操作需要有關要轉換的文檔的資訊，包括目標文檔的路徑。

**檢索結果**

將HTML內容轉換為PDF文檔後，可以檢索結果並保存PDF文檔。

**另請參閱**

[使用Java API將HTML內容轉換為PDF文檔](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[使用Web服務API將HTML內容轉換為PDF文檔](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[生成PDF服務API快速啟動](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將HTML內容轉換為PDF文檔 {#convert-html-content-to-a-pdf-document-using-the-java-api}

使用「生成HTMLAPI(Java)」將PDF文檔轉換為PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-generatepdf-client.jar。

1. 建立生成PDF客戶端。

   建立 `GeneratePdfServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 檢索要轉換為HTML文檔的PDF內容。

   通過建立字串變數並指定指向HTML內容的URL來檢索HTML內容。

1. 將HTML內容轉換為PDF文檔。

   調用 `GeneratePdfServiceClient` 對象 `htmlToPDF2` 方法並傳遞以下值：

   * A `java.lang.String` 包含要轉換的HTML檔案的URL的對象。
   * A `java.lang.String` 包含要在轉換中使用的檔案類型設定的對象。 檔案類型設定可以包括顯示級別。
   * A `java.lang.String` 包含要使用的安全設定名稱的對象。
   * 可選 `com.adobe.idp.Document` 包含生成PDF文檔時要應用的設定的對象。 如果未提供此資訊，則根據前三個參數自動選擇設定。
   * 可選 `com.adobe.idp.Document` 包含要應用到PDF文檔的元資料資訊的對象。

1. 檢索結果。

   的 `htmlToPDF2` 方法返回 `HtmlToPdfResult` 包含已生成的新PDF文檔的對象。 要獲取新建立的PDF文檔，請執行以下操作：

   * 調用 `HtmlToPdfResult` 對象 `getCreatedDocument` 的雙曲餘切值。 這返回 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法從上一步建立的對象中提取PDF文檔。

**另請參閱**

[將HTML文檔轉換為PDF文檔](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[快速啟動（SOAP模式）:使用Java API將HTML內容轉換為PDF文檔](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[快速啟動（SOAP模式）:使用Java API將HTML內容轉換為PDF文檔](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將HTML內容轉換為PDF文檔 {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

使用「生成HTMLAPI（Web服務）」將PDF內容轉換為PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立生成PDF客戶端。

   * 建立 `GeneratePDFServiceClient` 對象。
   * 建立 `GeneratePDFServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`。) 你不需要 `lc_version` 屬性。 但是，請指定 `?blob=mtom`。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `GeneratePDFServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 檢索要轉換為HTML文檔的PDF內容。

   通過建立字串變數並指定指向HTML內容的URL來檢索HTML內容。

1. 將HTML內容轉換為PDF文檔。

   通過調用HTML內容將PDF內容轉換為 `GeneratePDFServiceService` 對象 `HtmlToPDF2` 方法並傳遞以下值：

   * 包含要轉換的HTML內容的字串。
   * A `java.lang.String` 包含要在轉換中使用的檔案類型設定的對象。
   * 包含要使用的安全設定的字串對象。
   * 可選 `BLOB` 包含生成PDF文檔時要應用的設定的對象。
   * 可選 `BLOB` 包含要應用到PDF文檔的元資料資訊的對象。
   * 類型的輸出參數 `BLOB` 是由 `CreatePDF2` 的雙曲餘切值。 的 `CreatePDF2` 方法使用轉換的文檔填充此對象。 （此參數值僅對於Web服務調用是必需的）。

1. 檢索結果。

   * 通過分配已轉換的PDF文檔 `BLOB` 對象 `MTOM` 欄位。 位元組陣列表示已轉換的PDF文檔。 確保使用 `BLOB` 用作輸出參數的對象 `HtmlToPDF2` 的雙曲餘切值。
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示轉換的PDF文檔的檔案位置。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[將HTML文檔轉換為PDF文檔](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將PDF文檔轉換為非影像格式 {#converting-pdf-documents-to-non-image-formats}

本節介紹如何使用「生成PDFJava API」和Web服務API以寫程式方式將PDF文檔轉換為RTF檔案，這是非影像格式的示例。 其他非影像格式包括HTML、文本、DOC和EPS。 將PDF文檔轉換為RTF時，確保PDF文檔不包含表單元素，如提交按鈕。 表單元素不會轉換。

>[!NOTE]
>
>有關生成PDF服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

要將PDF文檔轉換為任何受支援的類型，請執行以下步驟：

1. 包括項目檔案。
1. 建立生成PDF客戶端。
1. 檢索要轉換的PDF文檔。
1. 轉換PDF文檔。
1. 保存已轉換的檔案。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立生成PDF客戶端**

在以寫程式方式執行「生成PDF」操作之前，必須建立「生成PDF」服務客戶端。 如果使用Java API，請建立 `GeneratePdfServiceClient` 的雙曲餘切值。 如果使用Web服務API，請建立 `GeneratePDFServiceService` 的雙曲餘切值。

**檢索要轉換的PDF文檔**

檢索要轉換為非影像格式的PDF文檔。

**轉換PDF文檔**

建立服務客戶端後，可以調用PDF導出操作。 此操作需要有關要轉換的文檔的資訊，包括目標文檔的路徑。

**保存轉換的檔案**

保存已轉換的檔案。 例如，如果將PDF文檔轉換為RTF檔案，請將轉換後的文檔保存為RTF檔案。

**另請參閱**

[使用Java API將PDF文檔轉換為RTF檔案](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[使用Web服務API將PDF文檔轉換為RTF檔案](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[生成PDF服務API快速啟動](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF文檔轉換為RTF檔案 {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

使用「生成PDFAPI(Java)」將PDF文檔轉換為RTF檔案：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-generatepdf-client.jar。

1. 建立生成PDF客戶端。

   建立 `GeneratePdfServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 檢索要轉換的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示要使用其建構子轉換的PDF文檔的對象。 傳遞一個字串值，指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 轉換PDF文檔。

   調用 `GeneratePdfServiceClient` 對象 `exportPDF2` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示要轉換的PDF檔案的對象。
   * A `java.lang.String` 包含要轉換的檔案名稱的對象。
   * A `java.lang.String` 包含Adobe PDF設定名稱的對象。
   * A `ConvertPDFFormatType` 指定轉換的目標檔案類型的對象。
   * 可選 `com.adobe.idp.Document` 包含生成PDF文檔時要應用的設定的對象。

   的 `exportPDF2` 方法返回 `ExportPDFResult` 包含已轉換檔案的對象。

1. 轉換PDF文檔。

   要獲取新建立的檔案，請執行以下操作：

   * 調用 `ExportPDFResult` 對象 `getConvertedDocument` 的雙曲餘切值。 這返回 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法提取新文檔。

**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API將HTML內容轉換為PDF文檔](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將PDF文檔轉換為RTF檔案 {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

使用生成PDFAPI（Web服務）將PDF文檔轉換為RTF檔案：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立生成PDf客戶端。

   * 建立 `GeneratePDFServiceClient` 對象。
   * 建立 `GeneratePDFServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`。) 你不需要 `lc_version` 屬性。 但是，請指定 `?blob=mtom`。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `GeneratePDFServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 檢索要轉換的PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存轉換的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過為對象分配 `MTOM` 屬性位元組陣列的內容。

1. 轉換PDF文檔。

   調用 `GeneratePDFServiceServiceWse` 對象 `ExportPDF2` 方法並傳遞以下值：

   * A `BLOB` 表示要轉換的PDF檔案的對象。
   * 包含要轉換的檔案路徑名的字串。
   * A `java.lang.String` 指定檔案位置的對象。
   * 一個字串對象，它指定轉換的目標檔案類型。 指定 `RTF`。
   * 可選 `BLOB` 包含生成PDF文檔時要應用的設定的對象。
   * 類型的輸出參數 `BLOB` 是由 `ExportPDF2` 的雙曲餘切值。 的 `ExportPDF2` 方法使用轉換的文檔填充此對象。 （此參數值僅對於Web服務調用是必需的）。

1. 保存已轉換的檔案。

   * 通過分配 `BLOB` 對象 `MTOM` 欄位。 位元組陣列表示轉換的RTF文檔。 確保使用 `BLOB` 用作輸出參數的對象 `ExportPDF2` 的雙曲餘切值。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞表示RTF檔案位置的字串值。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 添加對其他本機檔案格式的支援 {#adding-support-for-additional-native-file-formats}

本節介紹如何添加對其他本機檔案格式的支援。 它概述了生成PDF服務與本機應用程式之間的交互，本機應用程式用於將本機檔案格式轉換為PDF。

本節還將介紹以下內容：

* 如何修改生成PDF服務對本機應用程式的響應，該產品已用於將本機檔案格式轉換為PDF
* 生成PDF服務、生成PDF服務應用程式監視器(AppMon)元件和本機應用程式(如MicrosoftWord)之間的交互
* XML文法在這些交互中所起的作用

### 元件交互 {#component-interactions}

「生成PDF」服務通過調用與檔案格式關聯的應用程式，然後與應用程式交互以使用預設打印機打印文檔來轉換本機檔案格式。 預設打印機必須設定為Adobe PDF打印機。

此圖顯示了與本機應用程式支援相關的元件和驅動程式。 還提到了影響交互的XML文法。

用於本機檔案轉換的元件交互

此文檔使用術語 *本機應用程式* 指示用於生成本機檔案格式的應用程式，如MicrosoftWord。

*AppMon* 是與本機應用程式交互的企業元件，與用戶在該應用程式顯示的對話框中導航的方式相同。 AppMon用於指示應用程式(如MicrosoftWord)開啟和打印檔案的XML文法涉及以下順序任務：

1. 通過選擇「檔案」>「開啟」開啟檔案
1. 確保出現「開啟」對話框；否則，處理錯誤
1. 在「檔案名」欄位中提供檔案名，然後按一下「開啟」按鈕
1. 確保檔案實際開啟
1. 通過選擇「檔案」>「打印」開啟「打印」對話框
1. 確保顯示「打印」對話框

AppMon使用標準Win32 API與第三方應用程式進行交互，以便傳輸UI事件，如按鍵和滑鼠按一下，這對控制這些應用程式以從它們中生成PDF檔案非常有用。

由於這些Win32 API的限制，AppMon無法將這些UI事件分派到某些特定類型的窗口，如浮動菜單欄（在某些應用程式中如TextPad），以及某些類型的對話框，這些對話框的內容無法使用Win32 API檢索。

易於直觀地識別浮動菜單欄；但是，僅僅通過視覺檢查就可能無法識別特殊類型的對話。 您需要第三方應用程式，如MicrosoftSpy++(MicrosoftVisual C++開發環境的一部分)或其等效的WinID(可以免費從 [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID))，以檢查對話框以確定AppMon是否能夠使用標準Win32 API與其進行交互。

如果WinID能夠提取對話框內容，如文本、子窗口、窗口類ID等，則AppMon也可以執行同樣操作。

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
   <td><p>包括PDF設定、安全設定和檔案類型設定。 </p><p>檔案類型設定將檔案副檔名與相應的本機應用程式相關聯。 檔案類型設定還指定用於打印本機檔案的本機應用程式設定。 </p></td>
   <td><p>要更改已支援的本機應用程式的設定，系統管理員將在管理控制台中設定「檔案類型設定」。 </p><p>要添加對新本機檔案格式的支援，必須手動編輯該檔案。 (請參閱 <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">添加或修改對本機檔案格式的支援</a>。) </p></td>
  </tr>
  <tr>
   <td><p>指令碼 </p></td>
   <td><p>指定生成PDF服務與本機應用程式之間的交互。 此類交互通常指導應用程式將檔案打印到Adobe PDF驅動程式。 </p><p>該指令碼包含指導本機應用程式開啟特定對話框的說明，這些說明為這些對話框中的欄位和按鈕提供特定的響應。 </p></td>
   <td><p>「生成PDF」服務包括所有受支援的本機應用程式的指令碼檔案。 可以使用XML編輯應用程式修改這些檔案。</p><p>要添加對新本機應用程式的支援，必須建立新指令碼檔案。 (請參閱 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">為本機應用程式建立或修改附加對話框XML檔案</a>。) </p></td>
  </tr>
  <tr>
   <td><p>一般對話框說明 </p></td>
   <td><p>指定如何響應多個應用程式通用的對話框。 這些對話框由作業系統、幫助程式應用程式（如PDFMaker）和驅動程式生成。 </p><p>包含此資訊的檔案為appmon.global.en_US.xml。</p></td>
   <td><p>不要修改此檔案。 </p></td>
  </tr>
  <tr>
   <td><p>特定於應用程式的對話框說明</p></td>
   <td><p>指定如何響應特定於應用程式的對話框。 </p><p>包含此資訊的檔案是appmon。<i>「[appname]」</i>。對話框。<i>「[區域設定]」</i>.xml（例如appmon.word.en_US.xml）。</p></td>
   <td><p>不要修改此檔案。 </p><p>要添加新本機應用程式的對話框說明，請參見 <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">為本機應用程式建立或修改附加對話框XML檔案</a>。</p></td>
  </tr>
  <tr>
   <td><p>其他特定於應用程式的對話框說明 </p></td>
   <td><p>指定特定於應用程式的對話框說明的替代和添加。 本節介紹了此類資訊的示例。 </p><p>包含此資訊的檔案是appmon。<i>「[appname]」</i>.addition（.添加）<i>「[區域設定]」</i>.xml。 示例為appmon.addition.en_US.xml。</p></td>
   <td><p>可以使用XML編輯應用程式建立和修改此類型的檔案。 (請參閱 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">為本機應用程式建立或修改附加對話框XML檔案</a>。) </p><p><strong>重要</strong>:您必須為伺服器將支援的每個本機應用程式建立其他特定於應用程式的對話框說明。 </p></td>
  </tr>
 </tbody>
</table>

### 關於指令碼和對話框XML檔案 {#about-the-script-and-dialog-xml-files}

指令碼XML檔案指導「生成PDF」服務在應用程式對話框中導航，與用戶在應用程式對話框中導航的方式相同。 指令碼XML檔案還通過執行諸如按鈕、選擇或取消選擇複選框或選擇菜單項等操作來指示「生成PDF」服務響應對話框。

相反，對話框XML檔案只是響應在指令碼XML檔案中使用的操作類型相同的對話框。

#### 對話框和窗口元素術語 {#dialog-box-and-window-element-terminology}

本節和下一節根據所描述的透視，對對話框及其包含的元件使用不同的術語。 對話框元件是按鈕、欄位和組合框等項。

當本節和下一節從用戶的角度描述對話框及其元件時，術語如 *對話框*。 *按鈕*。 *場*, *組合框* 的子菜單。

當本節和下一節從對話框及其內部表示的角度描述對話框及其元件時，術語 *窗口元素* 的子菜單。 窗口元素的內部表示是層次，其中每個窗口元素實例由標籤標識。 窗口元素實例還描述了其物理特徵和行為。

從用戶的角度來看，對話框及其元件顯示的行為不同，其中某些對話框元素在激活之前會被隱藏。 從內部表示的角度看，不存在此類行為問題。 例如，對話框的內部表示形式與其包含的元件的內部表示形式類似，但是這些元件嵌套在對話框中除外。

本節介紹提供AppMon的說明的XML元素。 這些元素的名稱如 `dialog` 元素和 `window` 的子菜單。 此文檔使用單位間隔字型來區分XML元素。 的 `dialog` 元素標識XML指令碼檔案可能導致顯示的對話框，有意或無意。 的 `window` 元素標識窗口元素（對話框或對話框的元件）。

#### 層次結構 {#hierarchy}

此圖顯示了指令碼和對話框XML的層次結構。 指令碼XML檔案符合script.xsd架構，該架構包括（在XML意義下）window.xsd架構。 同樣，對話框XML檔案符合dialogs.xsd架構，該架構還包括window.xsd架構。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

指令碼和對話框XML的層次結構

#### 編寫XML檔案指令碼 {#script-xml-files}

A *指令碼XML檔案* 指定一系列步驟，這些步驟指導本機應用程式導航到某些窗口元素，然後為這些元素提供響應。 大多數響應是文本或擊鍵，與用戶向相應對話框中的欄位、組合框或按鈕提供的輸入相對應。

「生成PDF」服務對指令碼XML檔案的支援旨在引導本機應用程式打印本機檔案。 但是，指令碼XML檔案可用於完成用戶在與本機應用程式對話框交互時可以執行的任何任務。

指令碼XML檔案中的步驟按順序執行，而不存在任何分支機會。 支援的唯一條件test是超時/重試，這會導致在特定時間段內和經過特定次數的重試後，如果某個步驟未成功完成，則指令碼將終止。

除了順序步驟之外，步驟內的指令也按順序執行。 必須確保步驟和說明反映用戶執行這些相同步驟的順序。

指令碼XML檔案中的每個步驟都標識在成功執行步驟指令時預期會出現的窗口元素。 如果在執行指令碼步驟時出現意外對話框，則生成PDF服務將按下一節中所述搜索對話框XML檔案。

#### 對話框XML檔案 {#dialog-xml-files}

運行本機應用程式時會顯示不同的對話框，無論本機應用程式處於可見或不可見模式，都會顯示這些對話框。 對話框可由作業系統或應用程式本身生成。 當本機應用程式在「生成PDF」服務的控制下運行時，系統和本機應用程式對話框將顯示在不可見的窗口中。

A *對話框XML檔案* 指定生成PDF服務對系統或本機應用程式對話框的響應方式。 對話框XML檔案允許生成PDF服務以便於轉換過程的方式響應未提示的對話框。

當系統或本機應用程式顯示當前正在執行的指令碼XML檔案未處理的對話框時，生成PDF服務將按此順序搜索該對話框XML檔案，當它發現匹配項時停止：

* 應用程式。`[appname]`.其他。`[locale]`.xml
* 應用程式。`[appname]`。`[locale]`.xml（不要修改此檔案。）
* appmon.global.`[locale]`.xml（不要修改此檔案。）

如果「生成PDF」服務發現對話框的匹配項，則它會通過發送為對話框指定的擊鍵或其他操作來取消該對話框。 如果對話框的指令指定了中止消息，則生成PDF服務終止當前正在執行的作業並生成錯誤消息。 將在 `abortMessage` 指令碼XML語法中的元素。

如果「生成PDF」服務遇到先前列出的任何檔案中都未描述的對話框，則「生成PDF」服務會將該對話框的標題合併到日誌檔案條目中。 當前正在執行的作業最終超時。 然後，可以使用日誌檔案中的資訊在本機應用程式的附加對話框XML檔案中編寫新說明。

### 添加或修改對本機檔案格式的支援 {#adding-or-modifying-support-for-a-native-file-format}

本節介紹為支援其他本機檔案格式或修改對已受支援的本機檔案格式的支援而必須執行的任務。

在添加或修改支援之前，必須完成以下任務。

#### 選擇用於標識窗口元素的工具 {#choosing-a-tool-for-identifying-window-elements}

對話框和指令碼XML檔案要求您標識對話框或指令碼元素所響應的窗口元素（對話框、欄位或其他對話框元件）。 例如，在指令碼為本機應用程式調用菜單後，指令碼必須標識該菜單上要應用擊鍵或操作的窗口元素。

通過標題欄中顯示的標題，您可以輕鬆識別對話框。 但是，必須使用諸如MicrosoftSpy++之類的工具來標識較低級別的窗口元素。 低層窗口元素可以通過各種屬性來識別，這些屬性並不明顯。 另外，每個本地應用程式可以不同地標識其窗口元素。 因此，有多種方法來識別窗口元素。 以下是考慮窗口要素標識的建議順序：

1. 標題本身（如果它唯一）
1. 控制項ID，它對於給定對話框可能唯一，也可能不唯一
1. 類名，可能唯一，也可能不唯一

這三個屬性的任何一個或組合都可用於標識窗口。

如果屬性無法標識標題，則可以通過使用窗口元素相對於其父項的索引來標識窗口元素。 安 *索引* 指定窗口元素相對於其同級窗口元素的位置。 通常，索引是標識組合框的唯一方法。

請注意以下問題：

* MicrosoftSpy++使用&amp;號來標識字幕的熱鍵來顯示字幕。 例如，Spy++將一個「打印」對話框的標題顯示為 `Pri&nt`，表示熱鍵為 *n*。 指令碼和對話框XML檔案中的標題必須省略「和」。
* 部分字幕包括換行符。 生成PDF服務無法標識換行符。 如果標題包含換行符，則包含足夠的標題以將其與其他菜單項區分，然後對省略的部分使用規則運算式。 示例為( `^Long caption title$`)。 (請參閱 [在標題屬性中使用規則運算式](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes)。)
* 對保留的XML字元使用字元實體（也稱為轉義序列）。 例如，使用 `&` 對於和號， `<` 和 `>` 小於和大於符號， `&apos;` 撇號和 `&quot;` 的下界。

如果計畫使用對話框或指令碼XML檔案，則應安裝應用程式MicrosoftSpy++。

#### 取消對話框和指令碼檔案的打包 {#unpackaging-the-dialog-and-script-files}

對話框和指令碼檔案位於appmondata.jar檔案中。 在可以修改其中任何檔案或添加新指令碼或對話框檔案之前，必須取消打包此JAR檔案。 例如，假定要添加對EditPlus應用程式的支援。 您可以建立兩個XML檔案，名為appmon.editplus.script.en_US.xml和appmon.editplus.script.addition.en_US.xml。 必須將這些XML指令碼添加到adobe-appmondata.jar檔案的兩個位置，如下所述：

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon。 adobe-livecycle-native-jboss-x86_win32.ear檔案位於的導出資料夾中 `[AEM forms install directory]\configurationManager`。 (如果AEM Forms部署在另一台J2EE應用伺服器上，請將adobe-livecycle-native-jboss-x86_win32.ear檔案替換為與J2EE應用伺服器對應的EAR檔案。)
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon （adobe-appmondata.jar檔案位於adobe-generatepdf-dsc.jar檔案內）。 adobe-generatepdf-dsc.jar檔案位於 `[AEM forms install directory]\deploy` 的子菜單。

將這些XML檔案添加到adobe-appmondata.jar檔案後，必須重新部署GeneratePDF元件。 要將對話框和指令碼XML檔案添加到adobe-appmondata.jar檔案，請執行以下任務：

1. 使用WinZip或WinRAR等工具，開啟adobe-liveccycle-native-jboss-x86_win32.earfile > adobe-Native2PDFvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFvc-native.jar\bin > adobe-appmondatajar檔案。
1. 將對話框和指令碼XML檔案添加到appmondata.jar檔案，或修改此檔案中的現有XML檔案。 (請參閱 [為本機應用程式建立或修改指令碼XML檔案](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)和 [為本機應用程式建立或修改附加對話框XML檔案](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)。)
1. 使用WinZip或WinRAR等工具，開啟adobe-generatepdf-dsc.jar > adobe-appmondata.jar。
1. 將對話框和指令碼XML檔案添加到appmondata.jar檔案，或修改此檔案中的現有XML檔案。 (請參閱 [為本機應用程式建立或修改指令碼XML檔案](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)和 [為本機應用程式建立或修改附加對話框XML檔案](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)。) 將XML檔案添加到adobe-appmondata.jar檔案後，將新的adobe-appmondata.jar檔案放入adobe-generatepdf-dsc.jar檔案。
1. 如果添加了對附加本機檔案格式的支援，請建立提供應用程式路徑的系統環境變數(請參見 [建立環境變數以定位本機應用程式](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application)。)

**重新部署GeneratePDF元件**

1. 登錄到Workbench。
1. 選擇 **窗口** > **顯示視圖** > **元件**。 此操作將「元件」視圖添加到工作台。
1. 按一下右鍵「生成PDF」元件，然後選擇 **停止元件**。
1. 元件停止後，按一下右鍵並選擇「卸載元件」將其刪除。
1. 按一下右鍵 **元件** 表徵圖 **安裝元件**。
1. 瀏覽並選擇修改的adobe-generatepdf-dsc.jar檔案，然後按一下「開啟」。 請注意，在GeneratePDF元件旁邊會出現一個紅方。
1. 展開GeneratePDF元件，選擇「服務描述符」，然後按一下右鍵「生成PDF服務」，然後選擇「激活服務」。
1. 在出現的配置對話框中，輸入適用的配置值。 如果將這些值留空，則使用預設配置值。
1. 按一下右鍵「生成PDF」，然後選擇「啟動元件」。
1. 展開Active Services。 如果服務名稱正在運行，則其旁邊會顯示綠色箭頭。 否則，服務處於停止狀態。
1. 如果服務處於停止狀態，請按一下右鍵服務名並選擇啟動服務。

### 為本機應用程式建立或修改指令碼XML檔案 {#creating-or-modifying-a-script-xml-file-for-a-native-application}

如果要將檔案定向到新的本機應用程式，必須為該應用程式建立指令碼XML檔案。 如果要修改生成PDF服務與已受支援的本機應用程式交互的方式，則必須修改該應用程式的指令碼。

該指令碼包含在本機應用程式的窗口元素中導航並提供對這些元素特定響應的說明。 包含此資訊的檔案是 `appmon.`[應用名稱]&quot; `.script.`[區域]`.xml`。 示例為appmon.notepad.script.en_US.xml。

#### 標識指令碼必須執行的步驟 {#identifying-steps-the-script-must-execute}

使用本機應用程式，確定必須導航的窗口元素以及打印文檔時必須執行的每個響應。 請注意任何響應產生的對話框。 這些步驟將類似於以下步驟：

1. 選擇「檔案」>「開啟」。
1. 指定路徑，然後按一下「開啟」。
1. 在菜單欄上選擇「檔案」>「打印」。
1. 指定打印機所需的屬性。
1. 選擇打印並等待「另存為」對話框出現。 生成PDF服務需要「另存為」對話框來指定PDF檔案的目標。

#### 標識標題屬性中指定的對話框 {#identifying-the-dialogs-specified-in-caption-attributes}

使用MicrosoftSpy++獲取本機應用程式中窗口元素屬性的標識。 您必須具有這些標識才能編寫指令碼。

#### 在標題屬性中使用規則運算式 {#using-regular-expressions-in-caption-attributes}

可以在標題規範中使用規則運算式。 生成PDF服務使用 `java.util.regex.Matcher` 類以支援規則運算式。 該實用程式支援中所述的規則運算式 `java.util.regex.Pattern`。

**在記事本標題中將檔案名置於記事本前面的規則運算式**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**規則運算式將打印與打印設定區分開來**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### 對窗口和窗口排序清單元素 {#ordering-the-window-and-windowlist-elements}

您必須訂購 `window` 和 `windowList` 元素：

* 當多個 `window` 元素在中顯示為子項 `windowList` 或 `dialog` 元素，排序 `window` 按降序排列的元素，其長度 `caption` 指示順序中位置的名稱。
* 當多個 `windowList` 元素出現在 `window` 元素，排序 `windowList` 按降序排列的元素，其長度 `caption` 第一個屬性 `indexes/`指示順序中位置的元素。

**對對話框檔案中的窗口元素排序**

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

**對windowList元素中的窗口元素排序**

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

### 為本機應用程式建立或修改附加對話框XML檔案 {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

如果為先前不支援的本機應用程式建立指令碼，則還必須為該應用程式建立一個附加對話框XML檔案。 AppMon使用的每個本機應用程式必須只有一個附加的對話框XML檔案。 即使不需要未經請求的對話框，也需要附加的對話框XML檔案。 附加對話框必須至少有一個 `window` 元素，即使 `window` 元素只是佔位符。

>[!NOTE]
>
>在這方面，&quot;附加&quot;一詞是指 `appmon.[applicationname].addition.[locale].xml` 的子菜單。 此類檔案指定對話框XML檔案的替代和添加。

您還可以為以下目的修改本機應用程式的附加對話框XML檔案：

* 覆蓋具有不同響應的應用程式的對話框XML檔案
* 向該應用程式的對話框XML檔案中未定址的對話框添加響應

標識其他對話框的檔案名XML檔案為 `appmon.[appname].addition.[locale].xml`。 示例為appmon.excel.addition.en_US.xml。

附加對話框XML檔案的名稱必須使用格式 `appmon.[applicationname].addition.[locale].xml`，也請參見Wiki頁。 *應用程式名* 必須與XML配置檔案和指令碼中使用的應用程式名稱完全匹配。

>[!NOTE]
>
>native2pdfconfig.xml配置檔案中指定的所有通用應用程式都沒有主對話框XML檔案。 節 [添加或修改對本機檔案格式的支援](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) 描述了此類規範。

您必須訂購 `windowList` 在 `window` 的子菜單。 (請參閱 [對窗口和窗口排序清單元素](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements)。)

### 修改常規對話框XML檔案 {#modifying-the-general-dialog-xml-file}

您可以修改常規對話框XML檔案以響應由系統生成的對話框或響應多個應用程式共同的對話框。

#### 在XML配置檔案中添加檔案類型項 {#adding-a-filetype-entry-in-the-xml-configuration-file}

此過程說明如何更新生成PDF服務配置檔案以將檔案類型與本機應用程式關聯。 要更新此配置檔案，必須使用管理控制台將配置資料導出到檔案。 配置資料的預設檔案名為native2pdfconfig.xml。

**更新生成PDF服務配置檔案**

1. 選擇 **首頁** > **服務** > **Adobe PDF發電機** > **配置檔案**，然後選擇 **導出配置**。
1. 修改 `filetype-settings` native2pdfconfig.xml檔案中的元素。
1. 選擇 **首頁** > **服務** > **Adobe PDF發電機** >**配置檔案**，然後選擇 **導入配置**。 配置資料將導入到「生成PDF」服務中，以替換以前的設定。

>[!NOTE]
>
>應用程式的名稱被指定為 `GenericApp` 元素 `name` 屬性。 此值必須與為該應用程式開發的指令碼中指定的相應名稱完全匹配。 同樣， `GenericApp` 元素 `displayName` 屬性應與相應指令碼的 `expectedWindow` 窗口標題。 在解析出現在 `displayName` 或 `caption` 屬性。

在此示例中，修改了生成PDF服務提供的預設配置資料，以指定應使用記事本(而不是MicrosoftWord)來處理檔案副檔名為.txt的檔案。 在此修改之前，將MicrosoftWord指定為應處理此類檔案的本機應用程式。

**將文本檔案定向到記事本(native2pdfconfig.xml)的修改**

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

#### 建立環境變數以定位本機應用程式 {#creating-an-environment-variable-to-locate-the-native-application}

建立一個環境變數，指定本地應用程式執行檔的位置。 變數必須使用格式 `[applicationname]_PATH`，也請參見Wiki頁。 *應用程式名* 必須與XML配置檔案和指令碼中使用的應用程式名稱完全匹配，其中路徑包含以雙引號表示的執行檔的路徑。 此環境變數的示例為 `Photoshop_PATH`。

建立新PDF變數後，必須重新啟動部署了生成環境服務的伺服器。

**在Windows XP環境中建立系統變數**

1. 選擇 **控制面板>系統**。
1. 在「系統屬性」對話框中，按一下 **高級** 按鈕 **環境變數**。
1. 在「環境變數」(Environment Variables)對話框的「系統變數」(System Variables)下，按一下 **新建**。
1. 在「新建系統變數」(New System Variable)對話框中， **變數名稱** 框中，鍵入使用格式的名稱 `[applicationname]_PATH`。
1. 在 **變數值** 框中，鍵入應用程式的執行檔的完整路徑和檔案名，然後按一下 **確定**。 例如，鍵入： `c:\windows\Notepad.exe`
1. 在「環境變數」(Environment Variables)對話框中，按一下 **確定**。

**從命令行建立系統變數**

1. 在命令行窗口中，使用以下格式鍵入變數定義：

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   例如，鍵入： `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. 啟動新命令行提示，使系統變數生效。

#### XML檔案 {#xml-files}

AEM Forms包含XML檔案示例，這些檔案使生成PDF服務使用記事本處理任何檔案副檔名為.txt的檔案。 此代碼包含在此部分中。 此外，還必須進行本節中介紹的其他修改。

#### 附加對話框XML檔案 {#additional-dialog-xml-file}

此示例包含記事本應用程式的附加對話框。 除了「生成PDF」服務指定的對話框之外，還可以使用這些對話框。

**記事本對話框(appmon.notepad.addition.en_US.xml)**

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

此示例指定生成PDF服務如何使用Adobe PDF打印機與記事本交互以打印檔案。

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
