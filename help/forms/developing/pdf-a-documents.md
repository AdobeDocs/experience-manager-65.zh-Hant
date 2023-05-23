---
title: 使用PDF/A文檔
seo-title: Working with PDF/A Documents
description: 使用DocConverter服務確定PDF文檔是否是PDF/A文檔，並將PDF文檔轉換為PDF/A文檔。
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
ht-degree: 1%

---

# 使用PDF/A文檔 {#working-with-pdf-a-documents}

**關於DocConverter服務**

DocConverter服務可以將PDF文檔轉換為PDA/A文檔。 您可以使用此服務完成以下任務：

* 將PDF文檔轉換為PDF/A文檔。 (請參閱 [將文檔轉換為PDF/A文檔](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。)
* 確定PDF文檔是否是PDF/A文檔。 (請參閱 [以寫程式方式確定PDF/符合性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)。)

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將文檔轉換為PDF/A文檔 {#converting-documents-to-pdf-a-documents}

可以使用DocConverter服務將PDF文檔轉換為PDF/A文檔。 由於PDF/A是文檔內容長期保留的存檔格式，因此所有字型都被嵌入，檔案也未壓縮。 因此，PDF/A 文件通常比標準 PDF 文件大。此外，PDF/A 文件不包含音訊和視訊內容。在將PDF文檔轉換為PDF/A文檔之前，請確保PDF文檔不是PDF/A文檔。

PDF/A-1規格由兩個一致性級別組成，即A和B。兩者之間的主要區別在於邏輯結構（可訪問性）支援，這是一致性級別B不需要的。無論符合級別如何，PDF/A-1都指示所有字型都嵌入到生成的PDF/A文檔中。 此時，驗證（和轉換）中僅支援PDF/A-1b。

雖然PDF/A是存檔PDF文檔的標準，但如果標準PDF文檔滿足您公司的要求，則PDF/A不是強制性的。 PDF/A標準的目的是建立一個PDF檔案，用於長期存檔和文檔保存需要。

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要將PDF文檔轉換為PDF/A文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立DocConvert客戶端
1. 引用PDF文檔以轉換為PDF/A文檔。
1. 設定跟蹤資訊。
1. 轉換文檔。
1. 保存PDF/A文檔。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DocConvert客戶端**

在以寫程式方式執行DocConverter操作之前，必須建立DocConverter客戶端。 如果使用Java API，請建立 `DocConverterServiceClient` 的雙曲餘切值。 如果使用DocConverter Web服務API，請建立 `DocConverterServiceService` 的雙曲餘切值。

**引用PDF文檔以轉換為PDF/文檔**

檢索要轉換為PDF/PDF文檔的文檔。 如果嘗試將PDF文檔(如Acrobat表單)轉換為PDF/A文檔，將導致異常。

**設定跟蹤資訊**

您可以設定運行時選項，該選項確定在轉換過程中跟蹤的資訊量。 也就是說，您可以設定九個不同級別，以指定DocConverter服務在將PDF文檔轉換為PDF/A文檔時跟蹤的資訊量。

**轉換文檔**

在建立DocConverter服務客戶端後，參考要轉換的PDF文檔並設定指定跟蹤多少資訊的運行時選項，您可以將PDF文檔轉換為PDF/A文檔。

**保存PDF/文檔**

可以將PDF/A文檔另存為PDF檔案。

**另請參閱**

[使用Java API將文檔轉換為PDF/A文檔](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[使用Web服務API將文檔轉換為PDF/A文檔](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式確定PDF/符合性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### 使用Java API將文檔轉換為PDF/A文檔 {#convert-documents-to-pdf-a-documents-using-the-java-api}

使用Java API將PDF文檔轉換為PDF/A文檔：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-docconverter-client.jar。

1. 建立DocConvert客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocConverterServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用PDF文檔以轉換為PDF/文檔

   * 建立 `java.io.FileInputStream` 表示要轉換的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定跟蹤資訊

   * 建立 `PDFAConversionOptionSpec` 對象。
   * 通過調用 `PDFAConversionOptionSpec` 對象 `setLogLevel` 方法並傳遞指定跟蹤級別的字串值。 例如，傳遞值 `FINE`。 有關不同值的資訊，請參見 `setLogLevel` 中 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 轉換文檔

   通過調用PDF文檔將PDF文檔轉換為 `DocConverterServiceClient` 對象 `toPDFA` 方法並傳遞以下值：

   * 的 `com.adobe.idp.Document` 包含要轉換的PDF文檔的對象
   * 的 `PDFAConversionOptionSpec` 指定跟蹤資訊的對象

   的 `toPDFA` 方法返回 `PDFAConversionResult` 包含PDF/A文檔的對象。

1. 保存PDF/文檔

   * 通過調用PDF/A文檔 `PDFAConversionResult` 對象 `getPDFA` 的雙曲餘切值。 此方法返回 `com.adobe.idp.Document` 表示PDF/A文檔的對象。
   * 建立 `java.io.File` 表示PDF/A檔案的對象。 確保檔案副檔名為.pdf。
   * 通過調用PDF/A資料來填充檔案 `com.adobe.idp.Document` 對象 `copyToFile` 方法和傳遞 `java.io.File` 的雙曲餘切值。

**另請參閱**

[使用PDF/A文檔](pdf-a-documents.md#working-with-pdf-a-documents)

[快速啟動（SOAP模式）:使用Java API將文檔轉換為PDF/文檔](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將文檔轉換為PDF/A文檔 {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

使用DocConverter API（Web服務）將PDF文檔轉換為PDF/A文檔：

1. 包括項目檔案

   * 建立使用DocConverter WSDL的Microsoft.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立DocConvert客戶端

   * 使用Microsoft.NET客戶端程式集，建立 `DocConverterServiceService` 調用其預設建構子。
   * 設定 `DocConverterServiceService` 對象 `Credentials` 資料成員 `System.Net.NetworkCredential` 指定用戶名和密碼值的值。

1. 引用PDF文檔以轉換為PDF/文檔

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存轉換為PDF/A文檔的PDF文檔。
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值(該字串值表示PDF文檔的檔案位置)和在中開啟檔案的模式來對對象。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `binaryData` 屬性。

1. 設定跟蹤資訊

   * 建立 `PDFAConversionOptionSpec` 對象。
   * 通過將指定跟蹤級別的值分配給 `PDFAConversionOptionSpec` 對象 `logLevel` 資料成員。 例如，分配值 `FINE` 到此資料成員。

1. 轉換文檔

   通過調用PDF文檔將PDF文檔轉換為 `DocConverterServiceService` 對象 `toPDFA` 方法並傳遞以下值：

   * 的 `BLOB` 包含要轉換的PDF文檔的對象
   * 的 `PDFAConversionOptionSpec` 指定跟蹤資訊的對象

   的 `toPDFA` 方法返回 `PDFAConversionResult` 包含PDF/A文檔的對象。

1. 保存PDF/文檔

   * 建立 `BLOB` 通過獲取PDF/A文檔的值來儲存該文檔的對象 `PDFAConversionResult` 對象 `PDFADocument` 資料成員。
   * 建立一個位元組陣列，用於儲存 `BLOB` 使用 `PDFAConversionResult` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `binaryData` 資料成員。
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞表示PDF/A文檔的檔案位置的字串值來對對象。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[使用PDF/A文檔](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 以寫程式方式確定PDF/符合性 {#programmatically-determining-pdf-a-compliancy}

您可以使用DocConverter服務來確定PDF文檔是否符合PDF/A。 有關PDF/A文檔以及如何將PDF文檔轉換為PDF/A文檔的資訊，請參閱 [將文檔轉換為PDF/A文檔](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要確定PDF/符合性，請執行以下步驟：

1. 包括項目檔案。
1. 建立DocConvert客戶端
1. 引用用於確定PDF/符合性的PDF文檔。
1. 設定運行時選項。
1. 檢索有關PDF文檔的資訊。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DocConvert客戶端**

在以寫程式方式執行DocConverter操作之前，必須建立DocConverter客戶端。 如果使用Java API，請建立 `DocConverterServiceClient` 的雙曲餘切值。 如果使用DocConverter Web服務API，請建立 `DocConverterServiceService` 的雙曲餘切值。

**引用用於確定PDF/符合性的PDF文檔**

必須引用PDF文檔並將其傳遞給DocConverter服務，以確定PDF文檔是否符合PDF/A。

**設定運行時選項**

您可以設定運行時選項，該選項確定在轉換過程中跟蹤的資訊量。 也就是說，您可以設定九個不同級別，以指定DocConverter服務在將PDF文檔轉換為PDF/A文檔時跟蹤的資訊量。

**檢索有關PDF文檔的資訊**

在建立DocConverter服務客戶端、引用PDF文檔並設定運行時選項後，您可以確定PDF文檔是否是符合PDF/A的文檔。

**另請參閱**

[使用Java API確定PDF/符合性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[使用Web服務API確定PDF/符合性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API確定PDF/符合性 {#determine-pdf-a-compliancy-using-the-java-api}

使用Java API確定PDF/A相容性：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-docconverter-client.jar。

1. 建立DocConvert客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocConverterServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用用於確定PDF/符合性的PDF文檔

   * 建立 `java.io.FileInputStream` 表示要轉換的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定運行時選項

   * 建立 `PDFAValidationOptionSpec` 對象。
   * 通過調用 `PDFAValidationOptionSpec` 對象 `setCompliance` 方法 `PDFAValidationOptionSpec.Compliance.PDFA_1B`。
   * 通過調用 `PDFAValidationOptionSpec` 對象 `setLogLevel` 方法並傳遞指定跟蹤級別的字串值。 例如，傳遞值 `FINE`。 有關不同值的資訊，請參見 `setLogLevel` 中 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 檢索有關PDF文檔的資訊

   通過調用PDF/符合性 `DocConverterServiceClient` 對象 `isPDFA` 方法並傳遞以下值：

   * 的 `com.adobe.idp.Document` 包含PDF文檔的對象。
   * 的 `PDFAValidationOptionSpec` 指定運行時選項的對象。

   的 `isPDFA` 方法返回 `PDFAValidationResult` 包含此操作結果的對象。

**另請參閱**

[使用PDF/A文檔](pdf-a-documents.md#working-with-pdf-a-documents)

[快速啟動（SOAP模式）:使用Java API確定PDF/符合性](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API確定PDF/符合性 {#determine-pdf-a-compliancy-using-the-web-service-api}

使用Web服務API確定PDF/A相容性：

1. 包括項目檔案

   * 建立使用DocConverter WSDL的Microsoft.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立DocConvert客戶端

   * 使用Microsoft.NET客戶端程式集，建立 `DocConverterServiceService` 調用其預設建構子。
   * 設定 `DocConverterServiceService` 對象 `Credentials` 資料成員 `System.Net.NetworkCredential` 指定用戶名和密碼值的值。

1. 引用用於確定PDF/符合性的PDF文檔

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存轉換為PDF/A文檔的PDF文檔。
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值(該字串值表示PDF文檔的檔案位置)和在中開啟檔案的模式來對對象。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `binaryData` 屬性。

1. 設定運行時選項

   * 建立 `PDFAValidationOptionSpec` 對象。
   * 通過分配 `PDFAValidationOptionSpec` 對象 `compliance` 具有值的資料成員 `PDFAConversionOptionSpec_Compliance.PDFA_1B`。
   * 通過分配 `PDFAValidationOptionSpec` 對象 `resultLevel` 具有值的資料成員 `PDFAValidationOptionSpec_ResultLevel.DETAILED`。

1. 檢索有關PDF文檔的資訊

   通過調用PDF/符合性 `DocConverterServiceService` 對象 `isPDFA` 方法並傳遞以下值：

   * 的 `BLOB` 包含PDF文檔的對象。
   * 的 `PDFAValidationOptionSpec` 包含運行時選項的對象。

   的 `isPDFA` 方法返回 `PDFAValidationResult` 包含此操作結果的對象。

**另請參閱**

[使用PDF/A文檔](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
