---
title: 使用已提交的XML資料建立PDF檔案
seo-title: 使用已提交的XML資料建立PDF檔案
description: 'null'
seo-description: 'null'
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用提交的XML資料建立PDF檔案 {#creating-pdf-documents-with-submittedxml-data}

## 使用提交的XML資料建立PDF檔案 {#creating-pdf-documents-with-submitted-xml-data}

讓使用者可填寫互動式表單的網路應用程式，需要將資料送回伺服器。 使用Forms服務，您可以擷取使用者在互動式表單中輸入的表單資料。 然後，您可以將表單資料傳遞至其他AEM Forms服務作業，並使用資料建立PDF檔案。

>[!NOTE]
>
>在您閱讀本內容之前，建議您對處理已提交表單有深入的瞭解。 「處理提交的表單」中涵蓋表單設計與提交XML資料之間的關係等概念。

請考慮下列包含三個AEM Forms服務的工作流程：

* 使用者從網路應用程式提交XML資料至Forms服務。
* Forms服務用於處理提交的表單並提取表單欄位。 可處理表單資料。 例如，可將資料提交至企業資料庫。
* 表單資料會傳送至輸出服務，以建立非互動式PDF檔案。
* 非互動式PDF檔案會儲存在Content Services中（不建議使用）。

下圖提供此工作流程的視覺化表示。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

當使用者從用戶端網頁瀏覽器提交表單後，非互動式PDF檔案會儲存在Content Services（不建議使用）中。 下圖顯示儲存在Content services中的PDF檔案（已過時）。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 步驟摘要 {#summary-of-steps}

若要使用已提交的XML資料建立非互動式PDF檔案並儲存在Content services中的PDF檔案（不建議使用），請執行下列工作：

1. 包含專案檔案。
1. 建立表單、輸出和檔案管理物件。
1. 使用Forms服務擷取表單資料。
1. 使用「輸出」服務建立非互動式PDF檔案。
1. 使用「檔案管理」服務，將PDF表格儲存在Content Services（已過時）中。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立表單、輸出和文檔管理對象**

在以程式設計方式執行Forms服務API操作之前，請先建立Forms Client API物件。 同樣地，由於此工作流會調用「輸出」和「文檔管理」服務，因此請同時建立「輸出客戶端API」對象和「文檔管理客戶端API」對象。

**使用Forms服務擷取表單資料**

擷取已提交至Forms服務的表單資料。 您可以處理提交的資料，以符合您的業務需求。 例如，您可以將表單資料儲存在企業資料庫中。 不過，若要建立非互動式PDF檔案，表單資料會傳遞至「輸出」服務。

**使用「輸出」服務建立非互動式PDF檔案。**

使用「輸出」服務建立以表單設計和XML表單資料為基礎的非互動式PDF檔案。 在工作流程中，會從Forms服務擷取表單資料。

**使用檔案管理服務將PDF表格儲存在Content Services（已過時）**

使用Document Management服務API，將PDF檔案儲存在Content Services（已過時）。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### 使用Java API建立包含已提交XML資料的PDF檔案 {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

使用表單、輸出和檔案管理API(Java)，建立包含已提交XML資料的PDF檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar、adobe-output-client.jar和adobe-contentservices-client.jar。

1. 建立表單、輸出和文檔管理對象

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `FormsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。
   * 使用其 `OutputClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。
   * 使用其 `DocumentManagementServiceClientImpl` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 使用Forms服務擷取表單資料

   * 叫用物 `FormsServiceClient` 件的方 `processFormSubmission` 法並傳遞下列值：

      * 包 `com.adobe.idp.Document` 含表單資料的物件。
      * 指定環境變數的字串值，包括所有相關的HTTP標題。 指定要處理的內容類型，方法是為環境變數指定一或多 `CONTENT_TYPE` 個值。 例如，若要處理XML資料，請為此參數指定下列字串值： `CONTENT_TYPE=text/xml`。
      * 指定標題值的字 `HTTP_USER_AGENT` 串值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 存 `RenderOptionsSpec` 儲運行時選項的對象。
      該方 `processFormSubmission` 法返回包 `FormsResult` 含表單提交結果的對象。

   * 調用物件的方法，以判斷Forms服務是否已完成表 `FormsResult` 單資料的處 `getAction` 理。 如果此方法傳回值 `0`，資料就可供處理。
   * 借由調用物件的方 `com.adobe.idp.Document` 法來建立物件，以 `FormsResult` 擷取表單 `getOutputContent` 資料。 （此物件包含可傳送至Output服務的表單資料。）
   * 通過調 `java.io.InputStream` 用建構子並傳遞對 `java.io.DataInputStream` 像來建立對 `com.adobe.idp.Document` 像。
   * 呼叫 `org.w3c.dom.DocumentBuilderFactory` 靜態物件的方 `org.w3c.dom.DocumentBuilderFactory` 法以建立物 `newInstance` 件。
   * 調用 `org.w3c.dom.DocumentBuilder` 物件的方 `org.w3c.dom.DocumentBuilderFactory` 法以建立物 `newDocumentBuilder` 件。
   * 調用 `org.w3c.dom.Document` 物件的方法並傳 `org.w3c.dom.DocumentBuilder` 遞物件， `parse` 以建立物 `java.io.InputStream` 件。
   * 檢索XML文檔中每個節點的值。 完成此任務的一種方法是建立接受兩個參數的自定義方法：要 `org.w3c.dom.Document` 檢索其值的對象和節點的名稱。 此方法返回表示節點值的字串值。 在此程式後面的代碼示例中，調用此自定義方法 `getNodeText`。 本文給出了該方法的主體。


1. 使用「輸出」服務建立非互動式PDF檔案。

   叫用物件的方法並傳 `OutputClient` 遞下列值， `generatePDFOutput` 以建立PDF檔案：

   * 列舉 `TransformationFormat` 值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。 確保表單設計與從Forms服務擷取的表單資料相容。
   * 指定表單設計所在內容根目錄的字串值。
   * 包 `PDFOutputOptionsSpec` 含PDF執行時期選項的物件。
   * 包含 `RenderOptionsSpec` 演算執行時間選項的物件。
   * 包 `com.adobe.idp.Document` 含XML資料來源的物件，其中包含要與表單設計合併的資料。 請確定此物件是由物件 `FormsResult` 的方法傳 `getOutputContent` 回。
   * 方 `generatePDFOutput` 法返回 `OutputResult` 包含操作結果的對象。
   * 叫用物件的方法，擷取非互 `OutputResult` 動式PDF文 `getGeneratedDoc` 件。 此方法會傳回 `com.adobe.idp.Document` 代表非互動式PDF檔案的例項。

1. 使用檔案管理服務將PDF表格儲存在Content Services（已過時）

   叫用物件的方法並 `DocumentManagementServiceClientImpl` 傳遞下 `storeContent` 列值，以新增內容：

   * 一個字串值，它指定添加內容的儲存。 預設商店為 `SpacesStore`。 此值為必要參數。
   * 一個字串值，它指定添加內容的空間(例如 `/Company Home/Test Directory`)的完全限定路徑。 此值為必要參數。
   * 代表新內容的節點名稱(例如 `MortgageForm.pdf`)。 此值為必要參數。
   * 指定節點類型的字串值。 若要新增內容，例如PDF檔案，請指定 `{https://www.alfresco.org/model/content/1.0}content`。 此值為必要參數。
   * 代 `com.adobe.idp.Document` 表內容的物件。 此值為必要參數。
   * 指定編碼值(例如 `UTF-8`)的字串值。 此值為必要參數。
   * 一 `UpdateVersionType` 個枚舉值，它指定如何處理版本資訊(例如， `UpdateVersionType.INCREMENT_MAJOR_VERSION` 增量內容版本)。 )此值為必要參數。
   * 指定 `java.util.List` 與內容相關的方面的實例。 此值是可選參數，您可以指定 `null`。
   * 儲存 `java.util.Map` 內容屬性的對象。
   該方 `storeContent` 法返回描 `CRCResult` 述內容的對象。 例如， `CRCResult` 您可以使用物件來取得內容的唯一識別碼值。 若要執行此工作，請叫 `CRCResult` 用物件的方 `getNodeUuid` 法。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
