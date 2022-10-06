---
title: 使用PDF/A檔案
seo-title: Working with PDF/A Documents
description: 使用DocConverter服務確定PDF文檔是否為PDF/A文檔，並將PDF文檔轉換為PDF/A文檔。
seo-description: Use the  DocConverter service to determine if a PDF document is a PDF/A document and convert PDF documents to PDF/A documents.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Developer
exl-id: 966c3554-25df-4467-866e-11c43cc15b58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 0%

---

# 使用PDF/A檔案 {#working-with-pdf-a-documents}

**關於DocConverter服務**

DocConverter服務可將PDF文檔轉換為PDA/A文檔。 您可以使用此服務來完成下列工作：

* 將PDF文檔轉換為PDF/A文檔。 (請參閱 [將文檔轉換為PDF/A文檔](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* 確定PDF文檔是否為PDF/A文檔。 (請參閱 [以程式設計方式決定PDF/符合性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將文檔轉換為PDF/A文檔 {#converting-documents-to-pdf-a-documents}

可以使用DocConverter服務將PDF文檔轉換為PDF/文檔。 由於PDF/A是用於長期保存文檔內容的存檔格式，因此所有字型都被嵌入並且檔案被解壓縮。 因此，PDF/A文檔通常比標準PDF文檔大。 此外，PDF/檔案不包含音訊和視訊內容。 將PDF文檔轉換為PDF/A文檔之前，請確保PDF文檔不是PDF/A文檔。

PDF/A-1規範由兩個符合級別組成，即A和B。這兩個級別之間的主要區別在於邏輯結構（可訪問性）支援，這對於符合級別B不是必需的。無論符合級別如何，PDF/A-1都規定所有字型都嵌入在生成的PDF/A文檔中。 目前驗證（和轉換）僅支援PDF/A-1b。

雖然PDF/A是歸檔PDF文檔的標準，但如果標準PDF文檔滿足您公司的要求，則使用PDF/A進行歸檔並非強制性的。 PDF/A標準的目的是建立一個PDF檔案，用於滿足長期歸檔和文檔保存需求。

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要將PDF文檔轉換為PDF/A文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立DocConvert客戶端
1. 參考PDF文檔以轉換為PDF/A文檔。
1. 設定追蹤資訊。
1. 轉換文檔。
1. 儲存PDF/檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立DocConvert客戶端**

在以寫程式方式執行DocConverter操作之前，必須建立DocConverter客戶端。 如果您使用Java API，請建立 `DocConverterServiceClient` 物件。 如果您使用DocConverter Web服務API，請建立 `DocConverterServiceService` 物件。

**參考PDF文檔以轉換為PDF/文檔**

檢索PDF文檔以轉換為PDF/A文檔。 如果嘗試將PDF文檔(如Acrobat表單)轉換為PDF/A文檔，將導致異常。

**設定追蹤資訊**

您可以設定執行階段選項，以決定在轉換過程中要追蹤多少資訊。 也就是說，可以設定9個不同的級別，以指定DocConverter服務將PDF文檔轉換為PDF/A文檔時跟蹤的資訊量。

**轉換文檔**

建立DocConverter服務客戶端後，請參考要轉換的PDF文檔並設定指定跟蹤多少資訊的運行時選項，可以將PDF文檔轉換為PDF/A文檔。

**儲存PDF/檔案**

您可以將PDF/檔案儲存為PDF檔案。

**另請參閱**

[使用Java API將檔案轉換為PDF/A檔案](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[使用Web服務API將文檔轉換為PDF/A文檔](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式決定PDF/符合性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### 使用Java API將檔案轉換為PDF/A檔案 {#convert-documents-to-pdf-a-documents-using-the-java-api}

使用Java API將PDF檔案轉換為PDF/A檔案：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-docconverter-client.jar。

1. 建立DocConvert客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocConverterServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 參考PDF文檔以轉換為PDF/文檔

   * 建立 `java.io.FileInputStream` 表示要轉換的PDF文檔的對象，方法是使用其建構子並傳遞指定PDF檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 設定追蹤資訊

   * 建立 `PDFAConversionOptionSpec` 物件，使用其建構子。
   * 叫用 `PDFAConversionOptionSpec` 物件 `setLogLevel` 方法，並傳遞指定追蹤層級的字串值。 例如，傳遞值 `FINE`. 如需不同值的相關資訊，請參閱 `setLogLevel` 方法(在 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 轉換文檔

   調用以下命令將PDF文檔轉換為PDF/A文檔 `DocConverterServiceClient` 物件 `toPDFA` 方法並傳遞下列值：

   * 此 `com.adobe.idp.Document` 包含要轉換的PDF文檔的對象
   * 此 `PDFAConversionOptionSpec` 指定跟蹤資訊的對象

   此 `toPDFA` 方法傳回 `PDFAConversionResult` 包含PDF/A文檔的對象。

1. 儲存PDF/檔案

   * 叫用 `PDFAConversionResult` 物件 `getPDFA` 方法。 此方法會傳回 `com.adobe.idp.Document` 表示PDF/A文檔的對象。
   * 建立 `java.io.File` 代表PDF/A檔案的物件。 請確定副檔名為.pdf。
   * 叫用PDF/A資料，將檔案填入 `com.adobe.idp.Document` 物件 `copyToFile` 方法和傳遞 `java.io.File` 物件。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門（SOAP模式）:使用Java API將檔案轉換為PDF/檔案](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將文檔轉換為PDF/A文檔 {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

使用DocConverter API（Web服務）將PDF文檔轉換為PDF/A文檔：

1. 包含項目檔案

   * 建立會使用DocConverter WSDL的Microsoft .NET客戶端程式集。
   * 參考Microsoft .NET客戶端程式集。

1. 建立DocConvert客戶端

   * 使用Microsoft .NET客戶端程式集，建立 `DocConverterServiceService` 對象，方法是調用其預設建構子。
   * 設定 `DocConverterServiceService` 物件 `Credentials` 具有 `System.Net.NetworkCredential` 指定用戶名和密碼值的值。

1. 參考PDF文檔以轉換為PDF/文檔

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存轉換為PDF/PDF文檔的文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子，並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `binaryData` 屬性（包含位元組陣列的內容）。

1. 設定追蹤資訊

   * 建立 `PDFAConversionOptionSpec` 物件，使用其建構子。
   * 指定值以將追蹤層級指定給 `PDFAConversionOptionSpec` 物件 `logLevel` 資料成員。 例如，指派值 `FINE` 到此資料成員。

1. 轉換文檔

   調用以下命令將PDF文檔轉換為PDF/A文檔 `DocConverterServiceService` 物件 `toPDFA` 方法並傳遞下列值：

   * 此 `BLOB` 包含要轉換的PDF文檔的對象
   * 此 `PDFAConversionOptionSpec` 指定跟蹤資訊的對象

   此 `toPDFA` 方法傳回 `PDFAConversionResult` 包含PDF/A文檔的對象。

1. 儲存PDF/檔案

   * 建立 `BLOB` 透過取得PDF的 `PDFAConversionResult` 物件 `PDFADocument` 資料成員。
   * 建立位元組陣列，用於儲存 `BLOB` 使用 `PDFAConversionResult` 物件。 取得 `BLOB` 物件 `binaryData` 資料成員。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式並傳遞字串值，該字串值代表PDF/A檔案的檔案位置。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 以程式設計方式決定PDF/符合性 {#programmatically-determining-pdf-a-compliancy}

可以使用DocConverter服務來確定PDF文檔是否符合PDF/A。 有關PDF/A文檔以及如何將PDF文檔轉換為PDF/A文檔的資訊，請參閱 [將文檔轉換為PDF/A文檔](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

要確定PDF/符合性，請執行以下步驟：

1. 包含專案檔案。
1. 建立DocConvert客戶端
1. 參考用於判斷PDF/符合性的PDF檔案。
1. 設定運行時選項。
1. 檢索有關PDF文檔的資訊。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立DocConvert客戶端**

在以寫程式方式執行DocConverter操作之前，必須建立DocConverter客戶端。 如果您使用Java API，請建立 `DocConverterServiceClient` 物件。 如果您使用DocConverter Web服務API，請建立 `DocConverterServiceService` 物件。

**參考用於確定PDF/符合性的PDF檔案**

必須引用PDF文檔並將其傳遞到DocConverter服務，以確定PDF文檔是否符合PDF/A。

**設定運行時選項**

您可以設定執行階段選項，以決定在轉換過程中要追蹤多少資訊。 也就是說，可以設定9個不同的級別，以指定DocConverter服務將PDF文檔轉換為PDF/A文檔時跟蹤的資訊量。

**檢索有關PDF文檔的資訊**

建立DocConverter服務客戶端、參考PDF文檔並設定運行時選項後，可以確定PDF文檔是否與PDF/A相容。

**另請參閱**

[使用Java API判斷PDF/符合性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[使用網站服務API判斷PDF/符合性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API判斷PDF/符合性 {#determine-pdf-a-compliancy-using-the-java-api}

使用Java API來判斷PDF/符合性：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-docconverter-client.jar。

1. 建立DocConvert客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocConverterServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 參考用於確定PDF/符合性的PDF檔案

   * 建立 `java.io.FileInputStream` 表示要轉換的PDF文檔的對象，方法是使用其建構子並傳遞指定PDF檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 設定運行時選項

   * 建立 `PDFAValidationOptionSpec` 物件，使用其建構子。
   * 通過調用 `PDFAValidationOptionSpec` 物件 `setCompliance` 方法與傳遞 `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * 叫用 `PDFAValidationOptionSpec` 物件 `setLogLevel` 方法，並傳遞指定追蹤層級的字串值。 例如，傳遞值 `FINE`. 如需不同值的相關資訊，請參閱 `setLogLevel` 方法(在 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 檢索有關PDF文檔的資訊

   叫用以判斷PDF/符合性 `DocConverterServiceClient` 物件 `isPDFA` 方法並傳遞下列值：

   * 此 `com.adobe.idp.Document` 包含PDF文檔的對象。
   * 此 `PDFAValidationOptionSpec` 指定運行時選項的對象。

   此 `isPDFA` 方法傳回 `PDFAValidationResult` 包含此操作結果的對象。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門（SOAP模式）:使用Java API判斷PDF/符合性](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API判斷PDF/符合性 {#determine-pdf-a-compliancy-using-the-web-service-api}

使用網站服務API來判斷PDF/符合性：

1. 包含項目檔案

   * 建立會使用DocConverter WSDL的Microsoft .NET客戶端程式集。
   * 參考Microsoft .NET客戶端程式集。

1. 建立DocConvert客戶端

   * 使用Microsoft .NET客戶端程式集，建立 `DocConverterServiceService` 對象，方法是調用其預設建構子。
   * 設定 `DocConverterServiceService` 物件 `Credentials` 具有 `System.Net.NetworkCredential` 指定用戶名和密碼值的值。

1. 參考用於確定PDF/符合性的PDF檔案

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存轉換為PDF/PDF文檔的文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子，並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `binaryData` 屬性（包含位元組陣列的內容）。

1. 設定運行時選項

   * 建立 `PDFAValidationOptionSpec` 物件，使用其建構子。
   * 通過分配 `PDFAValidationOptionSpec` 物件 `compliance` 具有值的資料成員 `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * 指派 `PDFAValidationOptionSpec` 物件 `resultLevel` 具有值的資料成員 `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. 檢索有關PDF文檔的資訊

   叫用以判斷PDF/符合性 `DocConverterServiceService` 物件 `isPDFA` 方法並傳遞下列值：

   * 此 `BLOB` 包含PDF文檔的對象。
   * 此 `PDFAValidationOptionSpec` 包含運行時選項的對象。

   此 `isPDFA` 方法傳回 `PDFAValidationResult` 包含此操作結果的對象。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
