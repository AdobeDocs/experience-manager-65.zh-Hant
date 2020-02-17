---
title: 使用PDF/A檔案
seo-title: 使用PDF/A檔案
description: 'null'
seo-description: 'null'
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用PDF/A檔案 {#working-with-pdf-a-documents}

**關於DocConverter服務**

DocConverter服務可將PDF檔案轉換為PDA/A檔案。 您可以使用此服務完成以下任務：

* 將PDF檔案轉換為PDF/A檔案。 (請參 [閱將檔案轉換為PDF/A檔案](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。)
* 確定PDF檔案是否為PDF/A檔案。 (請參 [閱程式設計決定PDF/A相容](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)。)

>[!NOTE]
>
>如需DocConverter服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將檔案轉換為PDF/A檔案 {#converting-documents-to-pdf-a-documents}

您可以使用DocConverter服務將PDF檔案轉換為PDF/A檔案。 由於PDF/A是長期保存檔案內容的封存格式，所以所有字型都已內嵌，檔案也未壓縮。 因此，PDF/A檔案通常比標準PDF檔案大。 此外，PDF/A檔案不包含音訊和視訊內容。 在將PDF檔案轉換為PDF/A檔案之前，請確定PDF檔案不是PDF/A檔案。

PDF/A-1規格包含兩個符合等級，即A和B。兩者之間的主要區別在於邏輯結構（可訪問性）支援，而邏輯結構（可訪問性）支援對於符合性級別B不是必需的。無論符合程度如何，PDF/A-1都規定所有字型都內嵌在產生的PDF/A檔案中。 目前，驗證（和轉換）只支援PDF/A-1b。

雖然PDF/A是封存PDF檔案的標準，但如果標準PDF檔案符合您公司的需求，則不必使用PDF/A進行封存。 PDF/A標準的目的，在於建立PDF檔案，以滿足長期封存和檔案保存的需求。

>[!NOTE]
>
>如需DocConverter服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要將PDF檔案轉換為PDF/A檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立DocConvert客戶端
1. 參考PDF檔案以轉換為PDF/A檔案。
1. 設定追蹤資訊。
1. 轉換檔案。
1. 儲存PDF/A檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DocConvert客戶端**

在以寫程式方式執行DocConverter操作之前，必須建立DocConverter客戶端。 如果您使用Java API，請建立物 `DocConverterServiceClient` 件。 如果您使用DocConverter web服務API，請建立對 `DocConverterServiceService` 像。

**參考PDF檔案以轉換為PDF/A檔案**

擷取PDF檔案以轉換為PDF/A檔案。 如果您嘗試將PDF檔案（例如Acrobat表格）轉換為PDF/A檔案，將會造成例外。

**設定追蹤資訊**

您可以設定執行時期選項，以決定在轉換程式期間追蹤的資訊量。 也就是說，您可以設定9個不同的層級，以指定DocConverter服務在將PDF檔案轉換為PDF/A檔案時追蹤的資訊量。

**轉換檔案**

在您建立DocConverter服務用戶端後，請參考PDF檔案以轉換並設定執行時期選項，以指定要追蹤的資訊量，您就可將PDF檔案轉換為PDF/A檔案。

**儲存PDF/A檔案**

您可將PDF/A檔案儲存為PDF檔案。

**另請參閱**

[使用Java API將檔案轉換為PDF/A檔案](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[使用web service API將檔案轉換為PDF/A檔案](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式決定PDF/A相容性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### 使用Java API將檔案轉換為PDF/A檔案 {#convert-documents-to-pdf-a-documents-using-the-java-api}

使用Java API將PDF檔案轉換為PDF/A檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-docconverter-client.jar。

1. 建立DocConvert客戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `DocConverterServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考PDF檔案以轉換為PDF/A檔案

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表PDF檔案的物件以進行轉換。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 設定追蹤資訊

   * 使用其 `PDFAConversionOptionSpec` 建構函式建立物件。
   * 調用物件的方法並傳遞指 `PDFAConversionOptionSpec` 定追蹤層級 `setLogLevel` 的字串值，以設定資訊追蹤層級。 例如，傳遞值 `FINE`。 如需不同值的詳細資訊，請參 `setLogLevel` 閱「 [AEM Forms API參考」中的方法](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 轉換檔案

   調用物件的方法並傳遞下列值，將PDF `DocConverterServiceClient` 檔案轉 `toPDFA` 換為PDF/A檔案：

   * 包 `com.adobe.idp.Document` 含要轉換的PDF檔案的物件
   * 指定 `PDFAConversionOptionSpec` 追蹤資訊的物件
   此方 `toPDFA` 法會傳回 `PDFAConversionResult` 包含PDF/A檔案的物件。

1. 儲存PDF/A檔案

   * 叫用物件的方法，以擷取 `PDFAConversionResult` PDF/A文 `getPDFA` 件。 此方法傳回 `com.adobe.idp.Document` 代表PDF/A檔案的物件。
   * 建立 `java.io.File` 代表PDF/A檔案的物件。 請確定副檔名為。pdf。
   * 調用物件的方法並傳遞物件，以PDF/A `com.adobe.idp.Document` 資料填 `copyToFile` 入檔案 `java.io.File` 中。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門（SOAP模式）:使用Java API將檔案轉換為PDF/A檔案](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API將檔案轉換為PDF/A檔案 {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

使用DocConverter API(web service)將PDF檔案轉換為PDF/A檔案：

1. 包含專案檔案

   * 建立一個使用DocConverter WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立DocConvert客戶端

   * 使用Microsoft .NET客戶端元件，通過調用其缺 `DocConverterServiceService` 省建構子建立對象。
   * 使用指 `DocConverterServiceService` 定用戶名 `Credentials` 和口令值的 `System.Net.NetworkCredential` 值來設定對象的資料成員。

1. 參考PDF檔案以轉換為PDF/A檔案

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存轉換為PDF/A文檔的PDF文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示PDF文檔的檔案位置和開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 賦值其屬性， `binaryData` 使其包含位元組陣列的內容。

1. 設定追蹤資訊

   * 使用其 `PDFAConversionOptionSpec` 建構函式建立物件。
   * 為物件的資料成員指派指定追蹤層級的值，以設定 `PDFAConversionOptionSpec` 資訊追蹤 `logLevel` 層級。 例如，將值指派給 `FINE` 此資料成員。

1. 轉換檔案

   調用物件的方法並傳遞下列值，將PDF `DocConverterServiceService` 檔案轉 `toPDFA` 換為PDF/A檔案：

   * 包 `BLOB` 含要轉換的PDF檔案的物件
   * 指定 `PDFAConversionOptionSpec` 追蹤資訊的物件
   此方 `toPDFA` 法會傳回 `PDFAConversionResult` 包含PDF/A檔案的物件。

1. 儲存PDF/A檔案

   * 取得 `BLOB` 物件資料成員的值，以建立儲存PDF/A `PDFAConversionResult` 檔案的 `PDFADocument` 物件。
   * 建立位元組陣列，該陣列儲存使用對 `BLOB` 像返回的對象的內 `PDFAConversionResult` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `binaryData` 陣列。
   * 調用 `System.IO.FileStream` 其建構函式並傳遞代表PDF/A檔案檔案位置的字串值，以建立物件。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 以程式設計方式決定PDF/A相容性 {#programmatically-determining-pdf-a-compliancy}

您可以使用DocConverter服務來判斷PDF檔案是否與PDF/A相容。 如需有關PDF/A檔案以及如何將PDF檔案轉換為PDF/A檔案的資訊，請參 [閱將檔案轉換為PDF/A檔案](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。

>[!NOTE]
>
>如需DocConverter服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

若要判斷PDF/A相容性，請執行下列步驟：

1. 包含專案檔案。
1. 建立DocConvert客戶端
1. 參考用來判斷PDF/A相容性的PDF檔案。
1. 設定執行時期選項。
1. 擷取PDF檔案的相關資訊。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DocConvert客戶端**

在以寫程式方式執行DocConverter操作之前，必須建立DocConverter客戶端。 如果您使用Java API，請建立物 `DocConverterServiceClient` 件。 如果您使用DocConverter web服務API，請建立對 `DocConverterServiceService` 像。

**參考用來判斷PDF/A相容性的PDF檔案**

必須參考PDF檔案並將其傳遞至DocConverter服務，才能判斷PDF檔案是否與PDF/A相容。

**設定執行時期選項**

您可以設定執行時期選項，以決定在轉換程式期間追蹤的資訊量。 也就是說，您可以設定9個不同的層級，以指定DocConverter服務在將PDF檔案轉換為PDF/A檔案時追蹤的資訊量。

**擷取PDF檔案的相關資訊**

在您建立DocConverter服務用戶端、參考PDF檔案並設定執行時期選項後，您可以判斷PDF檔案是否符合PDF/A規範。

**另請參閱**

[使用Java API判斷PDF/A符合性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[使用web service API判斷PDF/A符合性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API判斷PDF/A符合性 {#determine-pdf-a-compliancy-using-the-java-api}

使用Java API來判斷PDF/A符合性：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-docconverter-client.jar。

1. 建立DocConvert客戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `DocConverterServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考用來判斷PDF/A相容性的PDF檔案

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表PDF檔案的物件以進行轉換。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 設定執行時期選項

   * 使用其 `PDFAValidationOptionSpec` 建構函式建立物件。
   * 調用物件的方法並傳遞， `PDFAValidationOptionSpec` 以設定 `setCompliance` 相容性等級 `PDFAValidationOptionSpec.Compliance.PDFA_1B`。
   * 調用物件的方法並傳遞指 `PDFAValidationOptionSpec` 定追蹤層級 `setLogLevel` 的字串值，以設定資訊追蹤層級。 例如，傳遞值 `FINE`。 如需不同值的詳細資訊，請參 `setLogLevel` 閱「 [AEM Forms API參考」中的方法](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 擷取PDF檔案的相關資訊

   調用物件的方法並傳遞下 `DocConverterServiceClient` 列值，以 `isPDFA` 判斷PDF/A相容性：

   * 包 `com.adobe.idp.Document` 含PDF檔案的物件。
   * 指定 `PDFAValidationOptionSpec` 運行時選項的對象。
   方 `isPDFA` 法返回 `PDFAValidationResult` 包含此操作結果的對象。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門（SOAP模式）:使用Java API判斷PDF/A相容性](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API判斷PDF/A符合性 {#determine-pdf-a-compliancy-using-the-web-service-api}

使用web service API來判斷PDF/A符合性：

1. 包含專案檔案

   * 建立一個使用DocConverter WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立DocConvert客戶端

   * 使用Microsoft .NET客戶端元件，通過調用其缺 `DocConverterServiceService` 省建構子建立對象。
   * 使用指 `DocConverterServiceService` 定用戶名 `Credentials` 和口令值的 `System.Net.NetworkCredential` 值來設定對象的資料成員。

1. 參考用來判斷PDF/A相容性的PDF檔案

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存轉換為PDF/A文檔的PDF文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示PDF文檔的檔案位置和開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 賦值其屬性， `binaryData` 使其包含位元組陣列的內容。

1. 設定執行時期選項

   * 使用其 `PDFAValidationOptionSpec` 建構函式建立物件。
   * 將物件的資料成員指派 `PDFAValidationOptionSpec` 為值，以 `compliance` 設定相容性層級 `PDFAConversionOptionSpec_Compliance.PDFA_1B`。
   * 將物件的資料成員指派 `PDFAValidationOptionSpec` 為值，以 `resultLevel` 設定資訊追蹤層級 `PDFAValidationOptionSpec_ResultLevel.DETAILED`。

1. 擷取PDF檔案的相關資訊

   調用物件的方法並傳遞下 `DocConverterServiceService` 列值，以 `isPDFA` 判斷PDF/A相容性：

   * 包 `BLOB` 含PDF檔案的物件。
   * 包 `PDFAValidationOptionSpec` 含運行時選項的對象。
   方 `isPDFA` 法返回 `PDFAValidationResult` 包含此操作結果的對象。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
