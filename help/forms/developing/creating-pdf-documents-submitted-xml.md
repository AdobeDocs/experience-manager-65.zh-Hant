---
title: 使用已提交的XML資料建立PDF檔案
seo-title: 使用已提交的XML資料建立PDF檔案
description: 使用Forms服務來擷取使用者在互動式表單中輸入的表單資料。 將表單資料傳遞至另一個AEM Forms服務作業，並使用資料建立PDF檔案。
seo-description: 使用Forms服務來擷取使用者在互動式表單中輸入的表單資料。 將表單資料傳遞至另一個AEM Forms服務作業，並使用資料建立PDF檔案。
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 0%

---


# 使用已提交的XML資料建立PDF檔案{#creating-pdf-documents-with-submittedxml-data}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

## 使用已提交的XML資料建立PDF檔案{#creating-pdf-documents-with-submitted-xml-data}

讓使用者可填寫互動式表單的網路應用程式，需要將資料送回伺服器。 使用Forms服務，您可以擷取使用者在互動式表單中輸入的表單資料。 然後，您可以將表單資料傳遞至另一個AEM Forms服務作業，並使用資料建立PDF檔案。

>[!NOTE]
>
>在您閱讀本內容之前，建議您對處理已提交表單有深入的瞭解。 表單設計與已提交XML資料之間的關係等概念，在處理已提交的Forms中有說明。

請考慮下列涉及三項AEM Forms服務的工作流程：

* 使用者從網路應用程式將XML資料提交至Forms服務。
* Forms服務用於處理提交的表單並提取表單欄位。 可處理表單資料。 例如，可將資料提交至企業資料庫。
* 表單資料會傳送至輸出服務，以建立非互動式PDF檔案。
* 非互動式PDF檔案會儲存在Content Services中（不建議使用）。

下圖提供此工作流程的視覺化表示。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

當使用者從用戶端網頁瀏覽器提交表單後，非互動式PDF檔案會儲存在Content Services（不建議使用）中。 下圖顯示儲存在Content Services中的PDF檔案（已過時）。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 步驟{#summary-of-steps}摘要

若要使用已提交的XML資料建立非互動式PDF檔案並儲存在Content Services中的PDF檔案（不建議使用），請執行下列工作：

1. 包含專案檔案。
1. 建立Forms、輸出和檔案管理物件。
1. 使用Forms服務擷取表單資料。
1. 使用「輸出」服務建立非互動式PDF檔案。
1. 使用「檔案管理」服務，將PDF表格儲存在Content Services（已過時）中。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms、輸出和文檔管理對象**

在以程式設計方式執行Forms服務API操作之前，請先建立Forms客戶端API對象。 同樣地，由於此工作流會調用「輸出」和「文檔管理」服務，因此請同時建立「輸出客戶端API」對象和「文檔管理客戶端API」對象。

**使用Forms服務檢索表單資料**

擷取已提交至Forms服務的表單資料。 您可以處理提交的資料，以符合您的業務需求。 例如，您可以將表單資料儲存在企業資料庫中。 不過，若要建立非互動式PDF檔案，表單資料會傳遞至「輸出」服務。

**使用「輸出」服務建立非互動式PDF檔案。**

使用「輸出」服務建立以表單設計和XML表單資料為基礎的非互動式PDF檔案。 在工作流中，從Forms服務檢索表單資料。

**使用檔案管理服務將PDF表格儲存在Content Services（已過時）**

使用Document Management服務API，將PDF檔案儲存在Content Services（已過時）。

**另請參閱**

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### 使用Java API {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}建立包含已提交XML資料的PDF檔案

使用Forms、輸出和檔案管理API(Java)，使用提交的XML資料建立PDF檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar、adobe-output-client.jar和adobe-contentservices-client.jar。

1. 建立Forms、輸出和文檔管理對象

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormsServiceClient`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`OutputClient`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`DocumentManagementServiceClientImpl`對象。

1. 使用Forms服務檢索表單資料

   * 叫用`FormsServiceClient`物件的`processFormSubmission`方法並傳遞下列值：

      * 包含表單資料的`com.adobe.idp.Document`物件。
      * 指定環境變數的字串值，包括所有相關的HTTP標題。 通過為`CONTENT_TYPE`環境變數指定一個或多個值，指定要處理的內容類型。 例如，若要處理XML資料，請為此參數指定下列字串值：`CONTENT_TYPE=text/xml`。
      * 指定`HTTP_USER_AGENT`標題值的字串值，例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 儲存運行時選項的`RenderOptionsSpec`對象。

      `processFormSubmission`方法返回包含表單提交結果的`FormsResult`對象。

   * 調用`FormsResult`物件的`getAction`方法，以判斷Forms服務是否已完成表單資料的處理。 如果此方法返回值`0`，則資料已準備就緒可供處理。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`com.adobe.idp.Document`物件來擷取表單資料。 （此物件包含可傳送至Output服務的表單資料。）
   * 通過調用`java.io.DataInputStream`建構子並傳遞`com.adobe.idp.Document`對象來建立`java.io.InputStream`對象。
   * 呼叫靜態`org.w3c.dom.DocumentBuilderFactory`物件的`newInstance`方法，以建立`org.w3c.dom.DocumentBuilderFactory`物件。
   * 調用`org.w3c.dom.DocumentBuilderFactory`物件的`newDocumentBuilder`方法，以建立`org.w3c.dom.DocumentBuilder`物件。
   * 通過調用`org.w3c.dom.DocumentBuilder`對象的`parse`方法並傳遞`java.io.InputStream`對象來建立`org.w3c.dom.Document`對象。
   * 檢索XML文檔中每個節點的值。 完成此任務的一種方法是建立接受兩個參數的自定義方法：`org.w3c.dom.Document`對象和要檢索其值的節點的名稱。 此方法返回表示節點值的字串值。 在此程式後面的代碼示例中，此自定義方法稱為`getNodeText`。 本文給出了該方法的主體。


1. 使用「輸出」服務建立非互動式PDF檔案。

   呼叫`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。 確保表單設計與從Forms服務檢索的表單資料相容。
   * 指定表單設計所在內容根目錄的字串值。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `com.adobe.idp.Document`物件，包含XML資料來源，其中包含要與表單設計合併的資料。 請確定此物件是由`FormsResult`物件的`getOutputContent`方法傳回。
   * `generatePDFOutput`方法返回包含操作結果的`OutputResult`對象。
   * 叫用`OutputResult`物件的`getGeneratedDoc`方法，擷取非互動式PDF檔案。 此方法會傳回代表非互動式PDF檔案的`com.adobe.idp.Document`例項。

1. 使用檔案管理服務將PDF表格儲存在Content Services（已過時）

   叫用`DocumentManagementServiceClientImpl`物件的`storeContent`方法並傳遞下列值，以新增內容：

   * 一個字串值，它指定添加內容的儲存。 預設商店為`SpacesStore`。 此值為必要參數。
   * 一個字串值，它指定添加內容的空間的完全限定路徑（例如`/Company Home/Test Directory`）。 此值為必要參數。
   * 代表新內容的節點名稱（例如`MortgageForm.pdf`）。 此值為必要參數。
   * 指定節點類型的字串值。 若要新增內容，例如PDF檔案，請指定`{https://www.alfresco.org/model/content/1.0}content`。 此值為必要參數。
   * 代表內容的`com.adobe.idp.Document`物件。 此值為必要參數。
   * 指定編碼值的字串值（例如`UTF-8`）。 此值為必要參數。
   * `UpdateVersionType`列舉值，指定如何處理版本資訊（例如`UpdateVersionType.INCREMENT_MAJOR_VERSION`）以增加內容版本。 )此值為必要參數。
   * 一個`java.util.List`實例，它指定與內容相關的方面。 此值是可選參數，您可以指定`null`。
   * 儲存內容屬性的`java.util.Map`對象。

   `storeContent`方法返回描述內容的`CRCResult`對象。 例如，您可以使用`CRCResult`物件，取得內容的唯一識別碼值。 要執行此任務，請調用`CRCResult`對象的`getNodeUuid`方法。

**另請參閱**

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
