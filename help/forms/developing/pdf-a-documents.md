---
title: 使用PDF/A檔案
seo-title: 使用PDF/A檔案
description: 使用DocConverter服務來判斷PDF檔案是否為PDF/A檔案，並將PDF檔案轉換為PDF/A檔案。
seo-description: 使用DocConverter服務來判斷PDF檔案是否為PDF/A檔案，並將PDF檔案轉換為PDF/A檔案。
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2387'
ht-degree: 0%

---


# 使用PDF/A檔案{#working-with-pdf-a-documents}

**關於DocConverter服務**

DocConverter服務可將PDF檔案轉換為PDA/A檔案。 您可以使用此服務完成以下任務：

* 將PDF檔案轉換為PDF/A檔案。 （請參閱[將檔案轉換為PDF/A檔案](pdf-a-documents.md#converting-documents-to-pdf-a-documents)）。
* 確定PDF檔案是否為PDF/A檔案。 （請參閱[程式設計決定PDF/A相容性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)）。

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將檔案轉換為PDF/A檔案{#converting-documents-to-pdf-a-documents}

您可以使用DocConverter服務將PDF檔案轉換為PDF/A檔案。 由於PDF/A是長期保存檔案內容的封存格式，所以所有字型都已內嵌，檔案也未壓縮。 因此，PDF/A檔案通常比標準PDF檔案大。 此外，PDF/A檔案不包含音訊和視訊內容。 在將PDF檔案轉換為PDF/A檔案之前，請確定PDF檔案不是PDF/A檔案。

PDF/A-1規格包含兩個符合等級，即A和B。兩者之間的主要區別在於邏輯結構（可訪問性）支援，而邏輯結構（可訪問性）支援對於符合性級別B不是必需的。無論符合程度如何，PDF/A-1都規定所有字型都內嵌在產生的PDF/A檔案中。 目前，驗證（和轉換）只支援PDF/A-1b。

雖然PDF/A是封存PDF檔案的標準，但如果標準PDF檔案符合您公司的需求，則不必使用PDF/A進行封存。 PDF/A標準的目的，在於建立PDF檔案，以滿足長期封存和檔案保存的需求。

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

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
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

有關這些JAR檔案位置的資訊，請參見[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DocConvert客戶端**

在以寫程式方式執行DocConverter操作之前，必須建立DocConverter客戶端。 如果您使用Java API，請建立`DocConverterServiceClient`物件。 如果您使用DocConverter Web服務API，請建立`DocConverterServiceService`對象。

**參考PDF檔案以轉換為PDF/A檔案**

擷取PDF檔案以轉換為PDF/A檔案。 如果您嘗試將PDF檔案(例如Acrobat表格)轉換為PDF/A檔案，將會造成例外。

**設定追蹤資訊**

您可以設定執行時期選項，以決定在轉換程式期間追蹤的資訊量。 也就是說，您可以設定9個不同的層級，以指定DocConverter服務在將PDF檔案轉換為PDF/A檔案時追蹤的資訊量。

**轉換檔案**

在您建立DocConverter服務用戶端後，請參考PDF檔案以轉換並設定執行時期選項，以指定要追蹤的資訊量，您就可將PDF檔案轉換為PDF/A檔案。

**儲存PDF/A檔案**

您可將PDF/A檔案儲存為PDF檔案。

**另請參閱**

[使用Java API將檔案轉換為PDF/A檔案](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[使用web service API將檔案轉換為PDF/A檔案](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式決定PDF/A相容性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### 使用Java API {#convert-documents-to-pdf-a-documents-using-the-java-api}將檔案轉換為PDF/A檔案

使用Java API將PDF檔案轉換為PDF/A檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-docconverter-client.jar。

1. 建立DocConvert客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`DocConverterServiceClient`對象。

1. 參考PDF檔案以轉換為PDF/A檔案

   * 使用PDF檔案的建構函式並傳遞指定PDF檔案位置的字串值，建立代表要轉換之PDF檔案的`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定追蹤資訊

   * 使用其建構子建立`PDFAConversionOptionSpec`對象。
   * 調用`PDFAConversionOptionSpec`物件的`setLogLevel`方法並傳遞指定追蹤層級的字串值，以設定資訊追蹤層級。 例如，傳遞值`FINE`。 有關不同值的資訊，請參見[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`setLogLevel`方法。

1. 轉換檔案

   調用`DocConverterServiceClient`物件的`toPDFA`方法並傳遞下列值，將PDF檔案轉換為PDF/A檔案：

   * 包含要轉換的PDF文檔的`com.adobe.idp.Document`對象
   * 指定追蹤資訊的`PDFAConversionOptionSpec`物件

   `toPDFA`方法返回包含PDF/A文檔的`PDFAConversionResult`對象。

1. 儲存PDF/A檔案

   * 叫用`PDFAConversionResult`物件的`getPDFA`方法，擷取PDF/A檔案。 此方法會傳回代表PDF/A檔案的`com.adobe.idp.Document`物件。
   * 建立代表PDF/A檔案的`java.io.File`物件。 請確定副檔名為。pdf。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`物件，以PDF/A資料填入檔案。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門（SOAP模式）:使用Java API將檔案轉換為PDF/A檔案](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#convert-documents-to-pdf-a-documents-using-the-web-service-api}將檔案轉換為PDF/A檔案

使用DocConverter API(web service)將PDF檔案轉換為PDF/A檔案：

1. 包含專案檔案

   * 建立一個使用DocConverter WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立DocConvert客戶端

   * 使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`DocConverterServiceService`對象。
   * 將`DocConverterServiceService`物件的`Credentials`資料成員設定為`System.Net.NetworkCredential`值，以指定使用者名稱和密碼值。

1. 參考PDF檔案以轉換為PDF/A檔案

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存轉換為PDF/A檔案的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`binaryData`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 設定追蹤資訊

   * 使用其建構子建立`PDFAConversionOptionSpec`對象。
   * 為`PDFAConversionOptionSpec`物件的`logLevel`資料成員指派指定追蹤層級的值，以設定資訊追蹤層級。 例如，將值`FINE`分配給此資料成員。

1. 轉換檔案

   調用`DocConverterServiceService`物件的`toPDFA`方法並傳遞下列值，將PDF檔案轉換為PDF/A檔案：

   * 包含要轉換的PDF文檔的`BLOB`對象
   * 指定追蹤資訊的`PDFAConversionOptionSpec`物件

   `toPDFA`方法返回包含PDF/A文檔的`PDFAConversionResult`對象。

1. 儲存PDF/A檔案

   * 透過取得`PDFAConversionResult`物件`PDFADocument`資料成員的值，建立儲存PDF/A檔案的`BLOB`物件。
   * 建立一個位元組陣列，用於儲存使用`PDFAConversionResult`對象返回的`BLOB`對象的內容。 獲取`BLOB`對象`binaryData`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示PDF/A文檔的檔案位置。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 以程式設計方式決定PDF/A相容性{#programmatically-determining-pdf-a-compliancy}

您可以使用DocConverter服務來判斷PDF檔案是否與PDF/A相容。 如需有關PDF/A檔案以及如何將PDF檔案轉換為PDF/A檔案的詳細資訊，請參閱[將檔案轉換為PDF/A檔案](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}摘要

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
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

有關這些JAR檔案位置的資訊，請參見[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DocConvert客戶端**

在以寫程式方式執行DocConverter操作之前，必須建立DocConverter客戶端。 如果您使用Java API，請建立`DocConverterServiceClient`物件。 如果您使用DocConverter Web服務API，請建立`DocConverterServiceService`對象。

**參考用來判斷PDF/A相容性的PDF檔案**

必須參考PDF檔案並將其傳遞至DocConverter服務，才能判斷PDF檔案是否與PDF/A相容。

**設定執行時期選項**

您可以設定執行時期選項，以決定在轉換程式期間追蹤的資訊量。 也就是說，您可以設定9個不同的層級，以指定DocConverter服務在將PDF檔案轉換為PDF/A檔案時追蹤的資訊量。

**擷取PDF檔案的相關資訊**

在您建立DocConverter服務用戶端、參考PDF檔案並設定執行時期選項後，您可以判斷PDF檔案是否符合PDF/A規範。

**另請參閱**

[使用Java API判斷PDF/A符合性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[使用web service API判斷PDF/A符合性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#determine-pdf-a-compliancy-using-the-java-api}判斷PDF/A相容性

使用Java API來判斷PDF/A符合性：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-docconverter-client.jar。

1. 建立DocConvert客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`DocConverterServiceClient`對象。

1. 參考用來判斷PDF/A相容性的PDF檔案

   * 使用PDF檔案的建構函式並傳遞指定PDF檔案位置的字串值，建立代表要轉換之PDF檔案的`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定執行時期選項

   * 使用其建構子建立`PDFAValidationOptionSpec`對象。
   * 調用`PDFAValidationOptionSpec`物件的`setCompliance`方法並傳遞`PDFAValidationOptionSpec.Compliance.PDFA_1B`，以設定相容性層級。
   * 調用`PDFAValidationOptionSpec`物件的`setLogLevel`方法並傳遞指定追蹤層級的字串值，以設定資訊追蹤層級。 例如，傳遞值`FINE`。 有關不同值的資訊，請參見[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`setLogLevel`方法。

1. 擷取PDF檔案的相關資訊

   調用`DocConverterServiceClient`物件的`isPDFA`方法並傳遞下列值，以判斷PDF/A相容性：

   * 包含PDF文檔的`com.adobe.idp.Document`對象。
   * 指定運行時選項的`PDFAValidationOptionSpec`對象。

   `isPDFA`方法返回包含此操作結果的`PDFAValidationResult`對象。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門（SOAP模式）:使用Java API判斷PDF/A相容性](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#determine-pdf-a-compliancy-using-the-web-service-api}判斷PDF/A相容性

使用web service API來判斷PDF/A符合性：

1. 包含專案檔案

   * 建立一個使用DocConverter WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立DocConvert客戶端

   * 使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`DocConverterServiceService`對象。
   * 將`DocConverterServiceService`物件的`Credentials`資料成員設定為`System.Net.NetworkCredential`值，以指定使用者名稱和密碼值。

1. 參考用來判斷PDF/A相容性的PDF檔案

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存轉換為PDF/A檔案的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`binaryData`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 設定執行時期選項

   * 使用其建構子建立`PDFAValidationOptionSpec`對象。
   * 通過將`PDFAValidationOptionSpec`對象的`compliance`資料成員分配為值`PDFAConversionOptionSpec_Compliance.PDFA_1B`來設定法規遵從性級別。
   * 將`PDFAValidationOptionSpec`物件的`resultLevel`資料成員指派為值`PDFAValidationOptionSpec_ResultLevel.DETAILED`，以設定資訊追蹤層級。

1. 擷取PDF檔案的相關資訊

   調用`DocConverterServiceService`物件的`isPDFA`方法並傳遞下列值，以判斷PDF/A相容性：

   * 包含PDF文檔的`BLOB`對象。
   * 包含運行時選項的`PDFAValidationOptionSpec`對象。

   `isPDFA`方法返回包含此操作結果的`PDFAValidationResult`對象。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
