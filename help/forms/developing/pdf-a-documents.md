---
title: 使用PDF/A檔案
seo-title: 使用PDF/A檔案
description: 使用DocConverter服務確定PDF文檔是否為PDF/A文檔，並將PDF文檔轉換為PDF/A文檔。
seo-description: 使用DocConverter服務確定PDF文檔是否為PDF/A文檔，並將PDF文檔轉換為PDF/A文檔。
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
source-wordcount: '2386'
ht-degree: 0%

---

# 使用PDF/A文檔{#working-with-pdf-a-documents}

**關於DocConverter服務**

DocConverter服務可將PDF文檔轉換為PDA/A文檔。 您可以使用此服務來完成下列工作：

* 將PDF檔案轉換為PDF/A檔案。 （請參閱[將文檔轉換為PDF/A文檔](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。）
* 確定PDF文檔是否為PDF/A文檔。 （請參閱[以程式設計方式決定PDF/A相容性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)。）

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將文檔轉換為PDF/A文檔{#converting-documents-to-pdf-a-documents}

您可以使用DocConverter服務將PDF文檔轉換為PDF/A文檔。 由於PDF/A是用於長期保存文檔內容的存檔格式，因此所有字型都會嵌入並解壓縮檔案。 因此，PDF/A文檔通常比標準PDF文檔大。 此外，PDF/A檔案不包含音訊和視訊內容。 在將PDF文檔轉換為PDF/A文檔之前，請確保PDF文檔不是PDF/A文檔。

PDF/A-1規範由兩個一致性級別組成，即A和B。這兩個級別的主要區別在於邏輯結構（可訪問性）支援，這對於一致性級別B不是必要的。無論一致性級別如何，PDF/A-1都規定所有字型都嵌入生成的PDF/A文檔中。 目前驗證（和轉換）僅支援PDF/A-1b。

雖然PDF/A是封存PDF檔案的標準，但如果標準PDF檔案符合貴公司的需求，則使用PDF/A進行封存並非強制性。 PDF/A標準的用途是建立PDF檔案，以滿足長期的封存和檔案保存需求。

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}的摘要

要將PDF文檔轉換為PDF/A文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立DocConvert客戶端
1. 參考要轉換為PDF/A文檔的PDF文檔。
1. 設定追蹤資訊。
1. 轉換文檔。
1. 儲存PDF/A檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

有關這些JAR檔案的位置的資訊，請參閱[包括AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DocConvert客戶端**

在以寫程式方式執行DocConverter操作之前，必須建立DocConverter客戶端。 如果您使用Java API，請建立`DocConverterServiceClient`物件。 如果使用DocConverter Web服務API，請建立`DocConverterServiceService`對象。

**參考要轉換為PDF/A文檔的PDF文檔**

檢索要轉換為PDF/A文檔的PDF文檔。 如果您嘗試將PDF檔案(如Acrobat表單)轉換為PDF/A檔案，將會造成例外狀況。

**設定追蹤資訊**

您可以設定執行階段選項，以決定在轉換過程中要追蹤多少資訊。 也就是說，您可以設定9個不同的級別，以指定DocConverter服務在將PDF文檔轉換為PDF/A文檔時跟蹤的資訊量。

**轉換文檔**

建立DocConverter服務客戶端後，請參考PDF文檔以轉換並設定運行時間選項，該選項指定跟蹤的資訊量，您可以將PDF文檔轉換為PDF/A文檔。

**儲存PDF/A檔案**

您可以將PDF/A檔案儲存為PDF檔案。

**另請參閱**

[使用Java API將檔案轉換為PDF/A檔案](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[使用Web服務API將文檔轉換為PDF/A文檔](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式決定PDF/A相容性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### 使用Java API {#convert-documents-to-pdf-a-documents-using-the-java-api}將文檔轉換為PDF/A文檔

使用Java API將PDF檔案轉換為PDF/A檔案：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-docconverter-client.jar。

1. 建立DocConvert客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`DocConverterServiceClient`物件。

1. 參考要轉換為PDF/A文檔的PDF文檔

   * 建立`java.io.FileInputStream`對象，該對象使用其建構子並傳遞指定PDF檔案位置的字串值來表示要轉換的PDF文檔。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定追蹤資訊

   * 使用其建構子建立`PDFAConversionOptionSpec`物件。
   * 叫用`PDFAConversionOptionSpec`物件的`setLogLevel`方法並傳遞指定追蹤層級的字串值，以設定資訊追蹤層級。 例如，傳遞值`FINE`。 如需不同值的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`setLogLevel`方法。

1. 轉換文檔

   調用`DocConverterServiceClient`對象的`toPDFA`方法並傳遞以下值，將PDF文檔轉換為PDF/A文檔：

   * 包含要轉換的PDF文檔的`com.adobe.idp.Document`對象
   * 指定追蹤資訊的`PDFAConversionOptionSpec`物件

   `toPDFA`方法返回包含PDF/A文檔的`PDFAConversionResult`對象。

1. 儲存PDF/A檔案

   * 調用`PDFAConversionResult`對象的`getPDFA`方法來檢索PDF/A文檔。 此方法會傳回代表PDF/A檔案的`com.adobe.idp.Document`物件。
   * 建立代表PDF/A檔案的`java.io.File`物件。 請確定副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`物件，以PDF/A資料填入檔案。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門（SOAP模式）:使用Java API將檔案轉換為PDF/A檔案](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#convert-documents-to-pdf-a-documents-using-the-web-service-api}將文檔轉換為PDF/A文檔

使用DocConverter API（Web服務）將PDF文檔轉換為PDF/A文檔：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集將使用DocConverter WSDL。
   * 參考Microsoft .NET客戶端程式集。

1. 建立DocConvert客戶端

   * 使用Microsoft .NET客戶端程式集，通過調用其預設建構子來建立`DocConverterServiceService`對象。
   * 將`DocConverterServiceService`對象的`Credentials`資料成員設定為`System.Net.NetworkCredential`值，該值指定用戶名和密碼值。

1. 參考要轉換為PDF/A文檔的PDF文檔

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存轉換為PDF/A文檔的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`binaryData`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 設定追蹤資訊

   * 使用其建構子建立`PDFAConversionOptionSpec`物件。
   * 通過為`PDFAConversionOptionSpec`對象的`logLevel`資料成員指定跟蹤級別的值來設定資訊跟蹤級別。 例如，將值`FINE`分配給此資料成員。

1. 轉換文檔

   調用`DocConverterServiceService`對象的`toPDFA`方法並傳遞以下值，將PDF文檔轉換為PDF/A文檔：

   * 包含要轉換的PDF文檔的`BLOB`對象
   * 指定追蹤資訊的`PDFAConversionOptionSpec`物件

   `toPDFA`方法返回包含PDF/A文檔的`PDFAConversionResult`對象。

1. 儲存PDF/A檔案

   * 通過獲取`PDFAConversionResult`對象的`PDFADocument`資料成員的值，建立儲存PDF/A文檔的`BLOB`對象。
   * 建立位元組陣列，用於儲存通過使用`PDFAConversionResult`對象返回的`BLOB`對象的內容。 獲取`BLOB`對象的`binaryData`資料成員的值，以填充位元組陣列。
   * 叫用`System.IO.FileStream`物件的建構函式並傳遞代表PDF/A檔案位置的字串值，以建立物件。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 以程式設計方式確定PDF/A相容性{#programmatically-determining-pdf-a-compliancy}

您可以使用DocConverter服務來確定PDF文檔是否與PDF/A相容。 有關PDF/A文檔以及如何將PDF文檔轉換為PDF/A文檔的資訊，請參閱[將文檔轉換為PDF/A文檔](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。

>[!NOTE]
>
>有關DocConverter服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}的摘要

若要判斷PDF/A相容性，請執行下列步驟：

1. 包含專案檔案。
1. 建立DocConvert客戶端
1. 參考用來判斷PDF/A相容性的PDF檔案。
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

有關這些JAR檔案的位置的資訊，請參閱[包括AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DocConvert客戶端**

在以寫程式方式執行DocConverter操作之前，必須建立DocConverter客戶端。 如果您使用Java API，請建立`DocConverterServiceClient`物件。 如果使用DocConverter Web服務API，請建立`DocConverterServiceService`對象。

**參考用於判斷PDF/A相容性的PDF檔案**

必須參考PDF文檔並將其傳遞到DocConverter服務，以確定PDF文檔是否與PDF/A相容。

**設定運行時選項**

您可以設定執行階段選項，以決定在轉換過程中要追蹤多少資訊。 也就是說，您可以設定9個不同的級別，以指定DocConverter服務在將PDF文檔轉換為PDF/A文檔時跟蹤的資訊量。

**檢索有關PDF文檔的資訊**

建立DocConverter服務客戶端、參考PDF文檔並設定運行時選項後，可以確定PDF文檔是否與PDF/A相容。

**另請參閱**

[使用Java API判斷PDF/A合規性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[使用網站服務API決定PDF/A合規性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#determine-pdf-a-compliancy-using-the-java-api}確定PDF/A合規性

使用Java API判斷PDF/A是否符合：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-docconverter-client.jar。

1. 建立DocConvert客戶端

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`DocConverterServiceClient`物件。

1. 參考用於判斷PDF/A相容性的PDF檔案

   * 建立`java.io.FileInputStream`對象，該對象使用其建構子並傳遞指定PDF檔案位置的字串值來表示要轉換的PDF文檔。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定運行時選項

   * 使用其建構子建立`PDFAValidationOptionSpec`物件。
   * 調用`PDFAValidationOptionSpec`對象的`setCompliance`方法並傳遞`PDFAValidationOptionSpec.Compliance.PDFA_1B`來設定符合性級別。
   * 叫用`PDFAValidationOptionSpec`物件的`setLogLevel`方法並傳遞指定追蹤層級的字串值，以設定資訊追蹤層級。 例如，傳遞值`FINE`。 如需不同值的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`setLogLevel`方法。

1. 檢索有關PDF文檔的資訊

   叫用`DocConverterServiceClient`物件的`isPDFA`方法並傳遞下列值，以判斷PDF/A符合性：

   * 包含PDF文檔的`com.adobe.idp.Document`對象。
   * 指定運行時選項的`PDFAValidationOptionSpec`對象。

   `isPDFA`方法返回包含此操作結果的`PDFAValidationResult`對象。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門（SOAP模式）:使用Java API判斷PDF/A符合性](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#determine-pdf-a-compliancy-using-the-web-service-api}確定PDF/A合規性

使用網站服務API來判斷PDF/A是否符合：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集將使用DocConverter WSDL。
   * 參考Microsoft .NET客戶端程式集。

1. 建立DocConvert客戶端

   * 使用Microsoft .NET客戶端程式集，通過調用其預設建構子來建立`DocConverterServiceService`對象。
   * 將`DocConverterServiceService`對象的`Credentials`資料成員設定為`System.Net.NetworkCredential`值，該值指定用戶名和密碼值。

1. 參考用於判斷PDF/A相容性的PDF檔案

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存轉換為PDF/A文檔的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`binaryData`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 設定運行時選項

   * 使用其建構子建立`PDFAValidationOptionSpec`物件。
   * 通過為`PDFAValidationOptionSpec`對象的`compliance`資料成員分配值`PDFAConversionOptionSpec_Compliance.PDFA_1B`來設定符合性級別。
   * 通過為`PDFAValidationOptionSpec`對象的`resultLevel`資料成員分配值`PDFAValidationOptionSpec_ResultLevel.DETAILED`來設定資訊跟蹤級別。

1. 檢索有關PDF文檔的資訊

   叫用`DocConverterServiceService`物件的`isPDFA`方法並傳遞下列值，以判斷PDF/A符合性：

   * 包含PDF文檔的`BLOB`對象。
   * 包含運行時選項的`PDFAValidationOptionSpec`對象。

   `isPDFA`方法返回包含此操作結果的`PDFAValidationResult`對象。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
