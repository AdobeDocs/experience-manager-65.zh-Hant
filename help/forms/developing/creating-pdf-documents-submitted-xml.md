---
title: 使用SubmittedXML資料建立PDF文檔
seo-title: Creating PDF Documents with SubmittedXML Data
description: 使用Forms服務來擷取使用者在互動式表單中輸入的表單資料。 將表單資料傳遞至其他AEM Forms服務作業，並使用資料建立PDF檔案。
seo-description: Use the Forms service to retrieve the form data that the user entered into an interactive form. Pass the form data to another AEM Forms service operation and create a PDF document using the data.
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
role: Developer
exl-id: d9d5b94a-9d10-4d90-9e10-5142f30ba4a3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 0%

---

# 使用已提交的XML資料建立PDF文檔 {#creating-pdf-documents-with-submittedxml-data}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 使用已提交的XML資料建立PDF文檔 {#creating-pdf-documents-with-submitted-xml-data}

讓使用者能夠填寫互動式表單的網頁型應用程式，需要將資料提交回伺服器。 使用Forms服務，您可以擷取使用者在互動式表單中輸入的表單資料。 然後，您可以將表單資料傳遞至其他AEM Forms服務作業，並使用資料建立PDF檔案。

>[!NOTE]
>
>閱讀此內容之前，建議您對處理已提交表單有紮實的了解。 處理已提交的Forms中涵蓋表單設計與已提交XML資料之間的關係等概念。

請考量下列涉及三個AEM Forms服務的工作流程：

* 用戶從基於Web的應用程式向Forms服務提交XML資料。
* Forms服務可用於處理已提交的表單及擷取表單欄位。 可處理表單資料。 例如，可將資料提交到企業資料庫。
* 表單資料會傳送至輸出服務，以建立非互動式PDF檔案。
* 非互動式PDF檔案會儲存在內容服務中（已淘汰）。

下圖提供此工作流程的視覺表示法。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

當用戶從客戶端Web瀏覽器提交表單後，非互動式PDF文檔將儲存在內容服務中（已廢止）。 下圖顯示儲存在「內容服務」中的PDF檔案（已過時）。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 步驟摘要 {#summary-of-steps}

要使用已提交的XML資料建立非互動式PDF文檔，並將其儲存在Content Services的PDF文檔中（已廢止），請執行以下任務：

1. 包含專案檔案。
1. 建立Forms、輸出和文檔管理對象。
1. 使用Forms服務擷取表單資料。
1. 使用輸出服務建立非互動式PDF文檔。
1. 使用檔案管理服務將PDF表單儲存在內容服務（已淘汰）。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms、輸出和文檔管理對象**

在以程式設計方式執行Forms服務API操作之前，請先建立Forms用戶端API物件。 同樣，由於此工作流調用了輸出和文檔管理服務，因此請同時建立輸出客戶端API對象和文檔管理客戶端API對象。

**使用Forms服務擷取表單資料**

擷取已提交至Forms服務的表單資料。 您可以處理提交的資料，以符合您的業務需求。 例如，您可以將表單資料儲存在企業資料庫中。 但是，要建立非互動式PDF文檔，表單資料將傳遞到輸出服務。

**使用輸出服務建立非互動式PDF文檔。**

使用輸出服務建立基於表單設計和XML表單資料的非互動式PDF文檔。 在工作流程中，表單資料會從Forms服務中擷取。

**使用檔案管理服務將PDF表單儲存在內容服務（已淘汰）中**

使用檔案管理服務API將PDF檔案儲存在內容服務中（已過時）。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### 使用Java API建立PDF文檔，該文檔包含已提交的XML資料 {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

使用Forms、輸出和文檔管理API(Java)建立具有已提交XML資料的PDF文檔：

1. 包含項目檔案

   在您的Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar、adobe-output-client.jar和adobe-contentservices-client.jar。

1. 建立Forms、輸出和文檔管理對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。
   * 建立 `OutputClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。
   * 建立 `DocumentManagementServiceClientImpl` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 使用Forms服務擷取表單資料

   * 叫用 `FormsServiceClient` 物件 `processFormSubmission` 方法，並傳遞下列值：

      * 此 `com.adobe.idp.Document` 包含表單資料的物件。
      * 指定環境變數的字串值，包括所有相關的HTTP標題。 指定要處理的內容類型，方法是為 `CONTENT_TYPE` 環境變數。 例如，要處理XML資料，請為此參數指定以下字串值： `CONTENT_TYPE=text/xml`.
      * 指定 `HTTP_USER_AGENT` 標題值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` 儲存運行時選項的對象。

      此 `processFormSubmission` 方法傳回 `FormsResult` 包含表單提交結果的物件。

   * 判斷Forms服務是否已借由叫用 `FormsResult` 物件 `getAction` 方法。 如果此方法傳回值 `0`，則資料已準備好供處理。
   * 透過建立 `com.adobe.idp.Document` 對象，方法是調用 `FormsResult` 物件 `getOutputContent` 方法。 （此物件包含可傳送至輸出服務的表單資料。）
   * 建立 `java.io.InputStream` 對象，方法是調用 `java.io.DataInputStream` 建構子和傳遞 `com.adobe.idp.Document` 物件。
   * 建立 `org.w3c.dom.DocumentBuilderFactory` 物件，方法是呼叫靜態 `org.w3c.dom.DocumentBuilderFactory` 物件 `newInstance` 方法。
   * 建立 `org.w3c.dom.DocumentBuilder` 對象，方法是調用 `org.w3c.dom.DocumentBuilderFactory` 物件 `newDocumentBuilder` 方法。
   * 建立 `org.w3c.dom.Document` 對象，方法是調用 `org.w3c.dom.DocumentBuilder` 物件 `parse` 方法和傳遞 `java.io.InputStream` 物件。
   * 檢索XML文檔中每個節點的值。 完成此工作的一種方式是建立接受兩個參數的自訂方法：the `org.w3c.dom.Document` 對象和要檢索其值的節點的名稱。 此方法會傳回代表節點值的字串值。 在此程式後的程式碼範例中，此自訂方法稱為 `getNodeText`. 此方法的內文如所示。


1. 使用輸出服務建立非互動式PDF文檔。

   通過調用 `OutputClient` 物件 `generatePDFOutput` 方法並傳遞下列值：

   * A `TransformationFormat` 列舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`.
   * 指定表單設計名稱的字串值。 確認表單設計與從Forms服務擷取的表單資料相容。
   * 一個字串值，它指定表單設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 此 `com.adobe.idp.Document` 包含要與表單設計合併的資料的XML資料源的對象。 請確定此物件是由 `FormsResult` 物件 `getOutputContent` 方法。
   * 此 `generatePDFOutput` 方法傳回 `OutputResult` 包含操作結果的對象。
   * 通過調用 `OutputResult` 物件 `getGeneratedDoc` 方法。 此方法會傳回 `com.adobe.idp.Document` 代表非互動式PDF檔案的例項。

1. 使用檔案管理服務將PDF表單儲存在內容服務（已淘汰）中

   叫用 `DocumentManagementServiceClientImpl` 物件 `storeContent` 方法並傳遞下列值：

   * 一個字串值，它指定添加內容的儲存區。 預設商店為 `SpacesStore`. 此值是必要參數。
   * 一個字串值，它指定添加內容的空間的完全限定路徑(例如， `/Company Home/Test Directory`)。 此值是必要參數。
   * 代表新內容的節點名稱(例如 `MortgageForm.pdf`)。 此值是必要參數。
   * 指定節點類型的字串值。 若要新增內容(例如PDF檔案)，請指定 `{https://www.alfresco.org/model/content/1.0}content`. 此值是必要參數。
   * A `com.adobe.idp.Document` 代表內容的物件。 此值是必要參數。
   * 指定編碼值的字串值(例如 `UTF-8`)。 此值是必要參數。
   * 安 `UpdateVersionType` 指定如何處理版本資訊的枚舉值(例如， `UpdateVersionType.INCREMENT_MAJOR_VERSION` 來增加內容版本。 )此值是必填參數。
   * A `java.util.List` 指定與內容相關的方面的實例。 此值是選用參數，您可以指定 `null`.
   * A `java.util.Map` 儲存內容屬性的物件。

   此 `storeContent` 方法傳回 `CRCResult` 描述內容的物件。 使用 `CRCResult` 物件，例如，您可以取得內容的唯一識別碼值。 要執行此任務，請調用 `CRCResult` 物件 `getNodeUuid` 方法。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
