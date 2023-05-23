---
title: 使用SubmittedXML資料建立PDF文檔
seo-title: Creating PDF Documents with SubmittedXML Data
description: 使用Forms服務檢索用戶輸入到互動式表單中的表單資料。 將表單資料傳遞到另一個AEM Forms服務操作，並使用該資料建立PDF文檔。
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

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

## 使用已提交的XML資料建立PDF文檔 {#creating-pdf-documents-with-submitted-xml-data}

使用戶能夠填寫互動式表單的基於Web的應用程式需要將資料提交回伺服器。 使用Forms服務，可以檢索用戶輸入到互動式表單中的表單資料。 然後，您可以將表單資料傳遞給另一個AEM Forms服務操作，並使用該資料建立PDF文檔。

>[!NOTE]
>
>在閱讀此內容之前，建議您對處理已提交表單有深入的瞭解。 表單設計與提交的XML資料之間的關係等概念在處理提交的Forms中得到了介紹。

請考慮以下涉及三個AEM Forms服務的工作流：

* 用戶從基於Web的應用程式向Forms服務提交XML資料。
* Forms服務用於處理提交的表單和提取表單欄位。 可以處理表單資料。 例如，資料可以提交到企業資料庫。
* 表單資料將發送到輸出服務以建立非互動式PDF文檔。
* 非互動式PDF文檔儲存在Content Services（不建議使用）中。

下圖提供了此工作流的可視表示。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

用戶從客戶端Web瀏覽器提交表單後，非互動式PDF文檔將儲存在Content Services（不建議使用）中。 下圖顯示了儲存在Content Services（不建議使用）中的PDF文檔。

![cd_cs_gui](assets/cd_cd_cs_gui.png)

### 步驟摘要 {#summary-of-steps}

要使用已提交的XML資料建立非互動式PDF文檔並將其儲存在Content Services（不建議使用）中的PDF文檔中，請執行以下任務：

1. 包括項目檔案。
1. 建立Forms、輸出和文檔管理對象。
1. 使用Forms服務檢索表單資料。
1. 使用輸出服務建立非互動式PDF文檔。
1. 使用文檔管理服務將PDF表單儲存在Content Services（不建議使用）中。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Forms、輸出和文檔管理對象**

在以寫程式方式執行Forms服務API操作之前，請建立一個Forms客戶端API對象。 同樣，由於此工作流調用輸出和文檔管理服務，因此請同時建立輸出客戶端API對象和文檔管理客戶端API對象。

**使用Forms服務檢索表單資料**

檢索已提交到Forms服務的表單資料。 您可以處理提交的資料以滿足您的業務要求。 例如，您可以將表單資料儲存在企業資料庫中。 但是，要建立非互動式PDF文檔，表單資料將傳遞給Output服務。

**使用輸出服務建立非互動式PDF文檔。**

使用「輸出」服務可建立基於表單設計和XML表單資料的非互動式PDF文檔。 在工作流中，從Forms服務檢索表單資料。

**使用文檔管理服務將PDF窗體儲存在Content Services（不建議使用）中**

使用Document Management服務API將PDF文檔儲存在Content Services（不建議使用）中。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### 使用Java API使用提交的XML資料建立PDF文檔 {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

使用Forms、輸出和文檔管理API(Java)建立具有已提交XML資料的PDF文檔：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar、adobe-output-client.jar和adobe-contentservices-client.jar。

1. 建立Forms、輸出和文檔管理對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。
   * 建立 `OutputClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。
   * 建立 `DocumentManagementServiceClientImpl` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 使用Forms服務檢索表單資料

   * 調用 `FormsServiceClient` 對象 `processFormSubmission` 方法並傳遞以下值：

      * 的 `com.adobe.idp.Document` 包含窗體資料的對象。
      * 一個字串值，它指定環境變數，包括所有相關的HTTP標頭。 通過為指定一個或多個值來指定要處理的內容類型 `CONTENT_TYPE` 環境變數。 例如，要處理XML資料，請為此參數指定以下字串值： `CONTENT_TYPE=text/xml`。
      * 一個字串值，它指定 `HTTP_USER_AGENT` 標題值，如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * A `RenderOptionsSpec` 儲存運行時選項的對象。

      的 `processFormSubmission` 方法返回 `FormsResult` 包含表單提交結果的對象。

   * 通過調用 `FormsResult` 對象 `getAction` 的雙曲餘切值。 如果此方法返回值 `0`，資料已準備好處理。
   * 通過建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。 （此對象包含可發送到輸出服務的表單資料。）
   * 建立 `java.io.InputStream` 通過調用 `java.io.DataInputStream` 建構子和傳遞 `com.adobe.idp.Document` 的雙曲餘切值。
   * 建立 `org.w3c.dom.DocumentBuilderFactory` 通過調用靜態 `org.w3c.dom.DocumentBuilderFactory` 對象 `newInstance` 的雙曲餘切值。
   * 建立 `org.w3c.dom.DocumentBuilder` 通過調用 `org.w3c.dom.DocumentBuilderFactory` 對象 `newDocumentBuilder` 的雙曲餘切值。
   * 建立 `org.w3c.dom.Document` 通過調用 `org.w3c.dom.DocumentBuilder` 對象 `parse` 方法和傳遞 `java.io.InputStream` 的雙曲餘切值。
   * 檢索XML文檔中每個節點的值。 完成此任務的一種方法是建立接受兩個參數的自定義方法：這樣 `org.w3c.dom.Document` 對象和要檢索其值的節點的名稱。 此方法返回表示節點值的字串值。 在此流程後面的代碼示例中，此自定義方法被調用 `getNodeText`。 給出了該方法的主體結構。


1. 使用輸出服務建立非互動式PDF文檔。

   通過調用PDF `OutputClient` 對象 `generatePDFOutput` 方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`。
   * 一個字串值，它指定窗體設計的名稱。 確保表單設計與從Forms服務檢索到的表單資料相容。
   * 一個字串值，它指定窗體設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `com.adobe.idp.Document` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。 確保此對象由 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
   * 的 `generatePDFOutput` 方法返回 `OutputResult` 包含操作結果的對象。
   * 通過調用非互動式PDF文檔 `OutputResult` 對象 `getGeneratedDoc` 的雙曲餘切值。 此方法返回 `com.adobe.idp.Document` 表示非互動式PDF文檔的實例。

1. 使用文檔管理服務將PDF窗體儲存在Content Services（不建議使用）中

   通過調用 `DocumentManagementServiceClientImpl` 對象 `storeContent` 方法並傳遞以下值：

   * 一個字串值，它指定添加內容的儲存。 預設儲存為 `SpacesStore`。 此值是必需參數。
   * 一個字串值，它指定添加內容的空間的完全限定路徑(例如， `/Company Home/Test Directory`)。 此值是必需參數。
   * 表示新內容的節點名稱(例如， `MortgageForm.pdf`)。 此值是必需參數。
   * 指定節點類型的字串值。 要添加新內容(如PDF檔案)，請指定 `{https://www.alfresco.org/model/content/1.0}content`。 此值是必需參數。
   * A `com.adobe.idp.Document` 表示內容的對象。 此值是必需參數。
   * 指定編碼值的字串值(例如， `UTF-8`)。 此值是必需參數。
   * 安 `UpdateVersionType` 指定如何處理版本資訊的枚舉值(例如， `UpdateVersionType.INCREMENT_MAJOR_VERSION` 來增加內容版本。 )此值是必需參數。
   * A `java.util.List` 指定與內容相關的方面的實例。 此值是可選參數，您可以指定 `null`。
   * A `java.util.Map` 儲存內容屬性的對象。

   的 `storeContent` 方法返回 `CRCResult` 描述內容的對象。 使用 `CRCResult` 對象，例如，可以獲取內容的唯一標識符值。 要執行此任務，請調用 `CRCResult` 對象 `getNodeUuid` 的雙曲餘切值。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
