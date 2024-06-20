---
title: 使用PDF/A檔案
description: 使用DocConverter服務來判斷PDF檔案是否為PDF/A檔案，並將PDF檔案轉換為PDF/A檔案。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 966c3554-25df-4467-866e-11c43cc15b58
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 1%

---

# 使用PDF/A檔案 {#working-with-pdf-a-documents}

**關於DocConverter服務**

DocConverter服務可以將PDF檔案轉換為PDA/A檔案。 您可以使用此服務完成這些工作：

* 將PDF檔案轉換為PDF/A檔案。 (請參閱 [將檔案轉換為PDF/A檔案](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* 決定PDF檔案是否為PDF/A檔案。 (請參閱 [以程式設計方式決定PDF/合規性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>如需DocConverter服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將檔案轉換為PDF/A檔案 {#converting-documents-to-pdf-a-documents}

您可以使用DocConverter服務將PDF檔案轉換為PDF/A檔案。 由於PDF/A是用於長期儲存檔案內容的封存格式，因此所有字型全都內嵌且檔案都未壓縮。 因此，PDF/A 文件通常比標準 PDF 文件大。此外，PDF/檔案不包含音訊和視訊內容。 將PDF檔案轉換為PDF/A檔案之前，請確定PDF檔案不是PDF/A檔案。

PDF/A-1規格包含兩個一致性層次，即A與B。兩者之間的主要差異在於邏輯結構（協助工具）支援，這是符合性層級B所不需要的。無論符合性層級為何，PDF/A-1會指定所有字型都內嵌在產生的PDF/A檔案中。 目前，驗證（和轉換）僅支援PDF/A-1b。

雖然PDF/A是封存PDF檔案的標準，但如果標準PDF檔案符合貴公司的要求，則不強制使用PDF/A進行封存。 PDF/A標準的目的是建立適合長期封存和檔案儲存需求的PDF檔案。

>[!NOTE]
>
>如需DocConverter服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要將PDF檔案轉換為PDF/A檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立DocConvert使用者端
1. 參照要轉換成PDF/A檔案的PDF檔案。
1. 設定追蹤資訊。
1. 轉換檔案。
1. 儲存PDF/檔案。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

有關這些JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立DocConvert使用者端**

您必須先建立DocConverter使用者端，才能以程式設計方式執行DocConverter作業。 如果您使用Java API，請建立 `DocConverterServiceClient` 物件。 如果您使用DocConverter Web服務API，請建立 `DocConverterServiceService` 物件。

**參照要轉換成PDF/A檔案的PDF檔案**

擷取PDF檔案以轉換為PDF/A檔案。 如果您嘗試將PDF檔案(例如Acrobat表單)轉換為PDF/A檔案，則會造成例外狀況。

**設定追蹤資訊**

您可以設定執行階段選項，以決定在轉換過程中要追蹤多少資訊。 也就是說，您可以設定九個不同層級，以指定DocConverter服務將PDF檔案轉換為PDF/A檔案時追蹤的資訊量。

**轉換檔案**

建立DocConverter服務使用者端後，參照要轉換的PDF檔案，並設定指定要追蹤多少資訊的執行階段選項，您可以將PDF檔案轉換為PDF/A檔案。

**儲存PDF/檔案**

您可以將PDF/A檔案儲存為PDF檔案。

**另請參閱**

[使用Java API將檔案轉換為PDF/A檔案](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[使用網站服務API將檔案轉換為PDF/A檔案](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式決定PDF/合規性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### 使用Java API將檔案轉換為PDF/A檔案 {#convert-documents-to-pdf-a-documents-using-the-java-api}

使用Java API將PDF檔案轉換為PDF/A檔案：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-docconverter-client.jar。

1. 建立DocConvert使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `DocConverterServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參照要轉換成PDF/A檔案的PDF檔案

   * 建立 `java.io.FileInputStream` 物件，代表要轉換的PDF檔案，使用它的建構函式，並傳遞字串值，指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 設定追蹤資訊

   * 建立 `PDFAConversionOptionSpec` 物件（使用其建構函式）。
   * 透過叫用 `PDFAConversionOptionSpec` 物件的 `setLogLevel` 方法並傳遞指定追蹤層級的字串值。 例如，傳遞值 `FINE`. 如需不同值的詳細資訊，請參閱 `setLogLevel` 中的方法 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 轉換檔案

   PDF PDF透過叫用 `DocConverterServiceClient` 物件的 `toPDFA` 方法並傳遞下列值：

   * 此 `com.adobe.idp.Document` 包含要轉換之PDF檔案的物件
   * 此 `PDFAConversionOptionSpec` 指定追蹤資訊的物件

   此 `toPDFA` 方法傳回 `PDFAConversionResult` 包含PDF/檔案之物件。

1. 儲存PDF/檔案

   * 透過叫用「 」擷取PDF/檔案 `PDFAConversionResult` 物件的 `getPDFA` 方法。 此方法會傳回 `com.adobe.idp.Document` 代表PDF/A檔案的物件。
   * 建立 `java.io.File` 代表PDF/A檔案的物件。 確認副檔名為.pdf。
   * 請叫用「 」，將PDF/A資料填入檔案中 `com.adobe.idp.Document` 物件的 `copyToFile` 方法並傳遞 `java.io.File` 物件。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門(SOAP模式)：使用Java API將檔案轉換為PDF/檔案](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將檔案轉換為PDF/A檔案 {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

使用DocConverter API （Web服務）將PDF檔案轉換為PDF/A檔案：

1. 包含專案檔案

   * 建立使用DocConverter WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立DocConvert使用者端

   * 使用Microsoft .NET使用者端元件，建立 `DocConverterServiceService` 物件（透過叫用其預設建構函式）。
   * 設定 `DocConverterServiceService` 物件的 `Credentials` 具有的資料成員 `System.Net.NetworkCredential` 指定使用者名稱和密碼值的值。

1. 參照要轉換成PDF/A檔案的PDF檔案

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存已轉換為PDF/A檔案的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法為叫用其建構函式，並傳遞代表PDF檔案檔案位置的字串值，以及用來開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 透過叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `binaryData` 包含位元組陣列內容的屬性。

1. 設定追蹤資訊

   * 建立 `PDFAConversionOptionSpec` 物件（使用其建構函式）。
   * 將指定追蹤層級的值指派給，以設定資訊追蹤層級 `PDFAConversionOptionSpec` 物件的 `logLevel` 資料成員。 例如，指派值 `FINE` 至此資料成員。

1. 轉換檔案

   PDF PDF透過叫用 `DocConverterServiceService` 物件的 `toPDFA` 方法並傳遞下列值：

   * 此 `BLOB` 包含要轉換之PDF檔案的物件
   * 此 `PDFAConversionOptionSpec` 指定追蹤資訊的物件

   此 `toPDFA` 方法傳回 `PDFAConversionResult` 包含PDF/檔案之物件。

1. 儲存PDF/檔案

   * 建立 `BLOB` PDF物件，透過取得 `PDFAConversionResult` 物件的 `PDFADocument` 資料成員。
   * 建立位元組陣列，儲存 `BLOB` 使用傳回的物件 `PDFAConversionResult` 物件。 透過取得 `BLOB` 物件的 `binaryData` 資料成員。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF/A檔案檔案位置的字串值。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式，然後傳遞 `System.IO.FileStream` 物件。
   * 透過叫用將位元組陣列的內容寫入PDF檔案 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 以程式設計方式決定PDF/合規性 {#programmatically-determining-pdf-a-compliancy}

您可以使用DocConverter服務來判斷PDF檔案是否符合PDF/A規範。 有關PDF/A檔案以及如何將PDF檔案轉換為PDF/A檔案的資訊，請參閱 [將檔案轉換為PDF/A檔案](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>如需DocConverter服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

若要判斷PDF/A相容性，請執行下列步驟：

1. 包含專案檔案。
1. 建立DocConvert使用者端
1. 參考用來判斷PDF/A相容性的PDF檔案。
1. 設定執行階段選項。
1. 擷取PDF檔案的相關資訊。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

有關這些JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立DocConvert使用者端**

您必須先建立DocConverter使用者端，才能以程式設計方式執行DocConverter作業。 如果您使用Java API，請建立 `DocConverterServiceClient` 物件。 如果您使用DocConverter Web服務API，請建立 `DocConverterServiceService` 物件。

**參考用於判斷PDF/A合規性的PDF檔案**

必須參考PDF檔案並將其傳遞到DocConverter服務，以確定PDF檔案是否符合PDF/A規範。

**設定執行階段選項**

您可以設定執行階段選項，以決定在轉換過程中要追蹤多少資訊。 也就是說，您可以設定九個不同的層級，指定當DocConverter服務將PDF檔案轉換為PDF/A檔案時，它會追蹤多少資訊。

**擷取PDF檔案的相關資訊**

建立DocConverter服務使用者端、參考PDF檔案並設定執行階段選項之後，您可以決定PDF檔案是否符合PDF/A規範。

**另請參閱**

[使用Java API判斷PDF/A合規性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[使用網站服務API判斷PDF/A合規性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API判斷PDF/A合規性 {#determine-pdf-a-compliancy-using-the-java-api}

使用Java API判斷PDF/A合規性：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-docconverter-client.jar。

1. 建立DocConvert使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `DocConverterServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考用於判斷PDF/A合規性的PDF檔案

   * 建立 `java.io.FileInputStream` 物件，代表要轉換的PDF檔案，使用它的建構函式，並傳遞字串值，指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 設定執行階段選項

   * 建立 `PDFAValidationOptionSpec` 物件（使用其建構函式）。
   * 透過叫用 `PDFAValidationOptionSpec` 物件的 `setCompliance` 方法和傳遞 `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * 透過叫用 `PDFAValidationOptionSpec` 物件的 `setLogLevel` 方法並傳遞指定追蹤層級的字串值。 例如，傳遞值 `FINE`. 如需不同值的詳細資訊，請參閱 `setLogLevel` 中的方法 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 擷取PDF檔案的相關資訊

   透過叫用「 」來判斷PDF/A相容性 `DocConverterServiceClient` 物件的 `isPDFA` 方法並傳遞下列值：

   * 此 `com.adobe.idp.Document` 包含PDF檔案的物件。
   * 此 `PDFAValidationOptionSpec` 指定執行階段選項的物件。

   此 `isPDFA` 方法傳回 `PDFAValidationResult` 包含此作業結果的物件。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門(SOAP模式)：使用Java API判斷PDF/A合規性](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API判斷PDF/A合規性 {#determine-pdf-a-compliancy-using-the-web-service-api}

使用Web服務API來判斷PDF/A相容性：

1. 包含專案檔案

   * 建立使用DocConverter WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立DocConvert使用者端

   * 使用Microsoft .NET使用者端元件，建立 `DocConverterServiceService` 物件（透過叫用其預設建構函式）。
   * 設定 `DocConverterServiceService` 物件的 `Credentials` 具有的資料成員 `System.Net.NetworkCredential` 指定使用者名稱和密碼值的值。

1. 參考用於判斷PDF/A合規性的PDF檔案

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存已轉換為PDF/A檔案的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法為叫用其建構函式，並傳遞代表PDF檔案檔案位置的字串值，以及用來開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 透過叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `binaryData` 包含位元組陣列內容的屬性。

1. 設定執行階段選項

   * 建立 `PDFAValidationOptionSpec` 物件（使用其建構函式）。
   * 透過指定來設定規範遵循等級 `PDFAValidationOptionSpec` 物件的 `compliance` 具有值的資料成員 `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * 透過指派以下專案來設定資訊追蹤等級 `PDFAValidationOptionSpec` 物件的 `resultLevel` 具有值的資料成員 `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. 擷取PDF檔案的相關資訊

   透過叫用「 」來判斷PDF/A相容性 `DocConverterServiceService` 物件的 `isPDFA` 方法並傳遞下列值：

   * 此 `BLOB` 包含PDF檔案的物件。
   * 此 `PDFAValidationOptionSpec` 包含執行階段選項的物件。

   此 `isPDFA` 方法傳回 `PDFAValidationResult` 包含此作業結果的物件。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
