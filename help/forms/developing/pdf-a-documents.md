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
feature: Adaptive Forms,Document Services,APIs & Integrations
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '2398'
ht-degree: 1%
---
# 使用PDF/A檔案 {#working-with-pdf-a-documents}

**關於DocConverter服務**

DocConverter服務可以將PDF檔案轉換為PDA/A檔案。 您可以使用此服務完成這些工作：

* 將PDF檔案轉換為PDF/A檔案。 （請參閱[將檔案轉換為PDF/A檔案](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。）
* 判斷PDF檔案是否為PDF/A檔案。 （請參閱[以程式設計方式決定PDF/A合規性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)。）

>[!NOTE]
>
>如需DocConverter服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將檔案轉換為PDF/A檔案 {#converting-documents-to-pdf-a-documents}

您可以使用DocConverter服務將PDF檔案轉換為PDF/A檔案。 由於PDF/A是用於長期儲存檔案內容的封存格式，因此所有字型全都內嵌且檔案都未壓縮。 因此，PDF/A 文件通常比標準 PDF 文件大。 此外，PDF/A 文件不包含音訊和視訊內容。 將PDF檔案轉換為PDF/A檔案之前，請確定PDF檔案不是PDF/A檔案。

PDF/A-1規格包含兩個一致性層級，即A和B。兩者之間的主要差異在於邏輯結構（協助工具）支援，合規性層級B不需要此支援。無論合規性層級為何，PDF/A-1都會指定所有字型都內嵌在產生的PDF/A檔案中。 目前，驗證（和轉換）中僅支援PDF/A-1b。

雖然PDF/A是封存PDF檔案的標準，但若標準PDF/A檔案符合貴公司的需求，則不強制使用PDF/A進行封存。 PDF/A標準的目的是建立適合長期封存和檔案儲存需求的PDF檔案。

支援的PDF/A合規性標準包括PDF/A-1a、1b、2a、2b、3a和3b。

>[!NOTE]
>
>如需DocConverter服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要將PDF檔案轉換為PDF/A檔案，請執行以下步驟：

1. 包含專案檔案。
1. 建立DocConvert使用者端
1. 參考要轉換成PDF/A檔案的PDF檔案。
1. 設定追蹤資訊。
1. 轉換檔案。
1. 儲存PDF/A檔案。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar （如果將AEM Forms部署在JBoss Application Server上，則為必要）
* jbossall-client.jar （如果AEM Forms部署在JBoss Application Server上，則為必要）

如需關於這些JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DocConvert使用者端**

您必須先建立DocConverter使用者端，才能以程式設計方式執行DocConverter作業。 如果您使用Java API，請建立`DocConverterServiceClient`物件。 如果您使用DocConverter Web服務API，請建立`DocConverterServiceService`物件。

**參考PDF檔案以轉換為PDF/A檔案**

擷取PDF檔案以轉換為PDF/A檔案。 如果您嘗試將PDF檔案（例如Acrobat表單）轉換為PDF/A檔案，則會造成例外狀況。

**設定追蹤資訊**

您可以設定執行階段選項，以決定在轉換過程中要追蹤多少資訊。 也就是說，您可以設定九個不同層級，以指定DocConverter服務將PDF檔案轉換為PDF/A檔案時追蹤的資訊量。

**轉換檔案**

建立DocConverter服務使用者端後，參照PDF檔案以轉換並設定執行階段選項（指定追蹤的資訊量），即可將PDF檔案轉換為PDF/A檔案。

**儲存PDF/A檔案**

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

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocConverterServiceClient`物件。

1. 參照要轉換成PDF/A檔案的PDF檔案

   * 建立代表要轉換之PDF檔案的`java.io.FileInputStream`物件，方法為使用其建構函式，並傳遞指定PDF檔案位置的字串值。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定追蹤資訊

   * 使用物件的建構函式建立`PDFAConversionOptionSpec`物件。
   * 透過叫用`PDFAConversionOptionSpec`物件的`setLogLevel`方法並傳遞指定追蹤層級的字串值來設定資訊追蹤層級。 例如，傳遞值`FINE`。 如需不同值的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`setLogLevel`方法。

1. 轉換檔案

   呼叫`DocConverterServiceClient`物件的`toPDFA`方法並傳遞下列值，以將PDF檔案轉換為PDF/A檔案：

   * 包含要轉換之PDF檔案的`com.adobe.idp.Document`物件
   * 指定追蹤資訊的`PDFAConversionOptionSpec`物件

   `toPDFA`方法傳回包含PDF/A檔案的`PDFAConversionResult`物件。

1. 儲存PDF/A檔案

   * 叫用`PDFAConversionResult`物件的`getPDFA`方法擷取PDF/A檔案。 此方法會傳回代表PDF/A檔案的`com.adobe.idp.Document`物件。
   * 建立代表PDF/A檔案的`java.io.File`物件。 確認副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`物件，以使用PDF/A資料填入檔案。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門（SOAP模式）：使用Java API將檔案轉換為PDF/A檔案](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將檔案轉換為PDF/A檔案 {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

使用DocConverter API （Web服務）將PDF檔案轉換為PDF/A檔案：

1. 包含專案檔案

   * 建立使用DocConverter WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立DocConvert使用者端

   * 使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`DocConverterServiceService`物件。
   * 將`DocConverterServiceService`物件的`Credentials`資料成員設定為指定使用者名稱和密碼值的`System.Net.NetworkCredential`值。

1. 參照要轉換成PDF/A檔案的PDF檔案

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存已轉換為PDF/A檔案的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表PDF檔案檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派物件的`binaryData`屬性，填入`BLOB`物件。

1. 設定追蹤資訊

   * 使用物件的建構函式建立`PDFAConversionOptionSpec`物件。
   * 指派值指定追蹤層級給`PDFAConversionOptionSpec`物件的`logLevel`資料成員，以設定資訊追蹤層級。 例如，將值`FINE`指派給此資料成員。

1. 轉換檔案

   呼叫`DocConverterServiceService`物件的`toPDFA`方法並傳遞下列值，以將PDF檔案轉換為PDF/A檔案：

   * 包含要轉換之PDF檔案的`BLOB`物件
   * 指定追蹤資訊的`PDFAConversionOptionSpec`物件

   `toPDFA`方法傳回包含PDF/A檔案的`PDFAConversionResult`物件。

1. 儲存PDF/A檔案

   * 取得`PDFAConversionResult`物件之`PDFADocument`資料成員的值，建立儲存PDF/A檔案的`BLOB`物件。
   * 建立位元組陣列，儲存使用`PDFAConversionResult`物件傳回的`BLOB`物件的內容。 取得`BLOB`物件的`binaryData`資料成員的值，以填入位元組陣列。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表PDF/A檔案檔案位置的字串值。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 以程式設計方式決定PDF/合規性 {#programmatically-determining-pdf-a-compliancy}

您可以使用DocConverter服務來判斷PDF檔案是否符合PDF/A標準。 如需PDF/A檔案以及如何將PDF檔案轉換為PDF/A檔案的相關資訊，請參閱[將檔案轉換為PDF/A檔案](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。

>[!NOTE]
>
>如需DocConverter服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

若要判斷PDF/A合規性，請執行以下步驟：

1. 包含專案檔案。
1. 建立DocConvert使用者端
1. 參考用來判斷PDF/A合規性的PDF檔案。
1. 設定執行階段選項。
1. 擷取PDF檔案的相關資訊。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar （如果將AEM Forms部署在JBoss Application Server上，則為必要）
* jbossall-client.jar （如果AEM Forms部署在JBoss Application Server上，則為必要）

如需關於這些JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立DocConvert使用者端**

您必須先建立DocConverter使用者端，才能以程式設計方式執行DocConverter作業。 如果您使用Java API，請建立`DocConverterServiceClient`物件。 如果您使用DocConverter Web服務API，請建立`DocConverterServiceService`物件。

**參考用來判斷PDF/A相容性的PDF檔案**

必須參考PDF檔案並傳遞給DocConverter服務，才能判斷PDF檔案是否符合PDF/A規範。

**設定執行階段選項**

您可以設定執行階段選項，以決定在轉換過程中要追蹤多少資訊。 也就是說，您可以設定九個不同等級，指定當DocConverter服務將PDF檔案轉換為PDF/A檔案時，它會追蹤多少資訊。

**擷取PDF檔案的相關資訊**

建立DocConverter服務使用者端、參考PDF檔案並設定執行階段選項後，您可以判斷PDF檔案是否符合PDF/A規範。

**另請參閱**

[使用Java API判斷PDF/A合規性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[使用網站服務API判斷PDF/A合規性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API判斷PDF/A合規性 {#determine-pdf-a-compliancy-using-the-java-api}

使用Java API判斷PDF/A相容性：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-docconverter-client.jar。

1. 建立DocConvert使用者端

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocConverterServiceClient`物件。

1. 參考用來判斷PDF/A合規性的PDF檔案

   * 建立代表要轉換之PDF檔案的`java.io.FileInputStream`物件，方法為使用其建構函式，並傳遞指定PDF檔案位置的字串值。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定執行階段選項

   * 使用物件的建構函式建立`PDFAValidationOptionSpec`物件。
   * 透過叫用`PDFAValidationOptionSpec`物件的`setCompliance`方法並傳遞`PDFAValidationOptionSpec.Compliance.PDFA_1B`來設定規範遵循層級。
   * 透過叫用`PDFAValidationOptionSpec`物件的`setLogLevel`方法並傳遞指定追蹤層級的字串值來設定資訊追蹤層級。 例如，傳遞值`FINE`。 如需不同值的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`setLogLevel`方法。

1. 擷取PDF檔案的相關資訊

   呼叫`DocConverterServiceClient`物件的`isPDFA`方法並傳遞下列值，以判斷PDF/A相容性：

   * 包含PDF檔案的`com.adobe.idp.Document`物件。
   * 指定執行階段選項的`PDFAValidationOptionSpec`物件。

   `isPDFA`方法傳回包含此作業結果的`PDFAValidationResult`物件。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入門（SOAP模式）：使用Java API判斷PDF/A合規性](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API判斷PDF/A合規性 {#determine-pdf-a-compliancy-using-the-web-service-api}

使用網站服務API判斷PDF/A合規性：

1. 包含專案檔案

   * 建立使用DocConverter WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立DocConvert使用者端

   * 使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`DocConverterServiceService`物件。
   * 將`DocConverterServiceService`物件的`Credentials`資料成員設定為指定使用者名稱和密碼值的`System.Net.NetworkCredential`值。

1. 參考用來判斷PDF/A合規性的PDF檔案

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存已轉換為PDF/A檔案的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表PDF檔案檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派物件的`binaryData`屬性，填入`BLOB`物件。

1. 設定執行階段選項

   * 使用物件的建構函式建立`PDFAValidationOptionSpec`物件。
   * 以值`PDFAConversionOptionSpec_Compliance.PDFA_1B`指派`PDFAValidationOptionSpec`物件的`compliance`資料成員來設定規範遵循層級。
   * 使用值`PDFAValidationOptionSpec_ResultLevel.DETAILED`指派`PDFAValidationOptionSpec`物件的`resultLevel`資料成員，以設定資訊追蹤層級。

1. 擷取PDF檔案的相關資訊

   呼叫`DocConverterServiceService`物件的`isPDFA`方法並傳遞下列值，以判斷PDF/A相容性：

   * 包含PDF檔案的`BLOB`物件。
   * 包含執行階段選項的`PDFAValidationOptionSpec`物件。

   `isPDFA`方法傳回包含此作業結果的`PDFAValidationResult`物件。

**另請參閱**

[使用PDF/A檔案](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
