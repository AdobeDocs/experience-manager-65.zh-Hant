---
title: 處理已提交的Forms
seo-title: Handling Submitted Forms
description: 使用Forms服務檢索以交互形式輸入的已提交資料。 用戶可以以XML、PDF和URL UTF-16格式提交表單資料。
seo-description: Use the Forms service to retrieve the submitted data entered in an interactive form. The user can submit the form data in XML, PDF, and URL UTF-16 formats.
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2904'
ht-degree: 0%

---

# 處理已提交的Forms {#handling-submitted-forms}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

使用戶能夠填寫互動式表單的基於Web的應用程式需要將資料提交回伺服器。 使用Forms服務，可以檢索用戶輸入到互動式表單中的資料。 檢索資料後，您可以處理資料以滿足業務要求。 例如，可以將資料儲存在資料庫中，將資料發送到另一個應用程式，將資料發送到另一個服務，將資料合併到表單設計中，在Web瀏覽器中顯示資料，等等。

表單資料以XML或PDF資料的形式提交到Forms服務，這是在設計器中設定的選項。 以XML形式提交的表單使您能夠提取單個欄位資料值。 即，可以提取用戶在表單中輸入的每個表單域的值。 作為PDF資料提交的表單是二進位資料，而不是XML資料。 您可以將表單另存為PDF檔案，或將表單發送到其他服務。 如果要從以XML形式提交的表單中提取資料，然後使用表單資料建立PDF文檔，請調用另一個AEM Forms操作。 (請參閱 [使用已提交的XML資料建立PDF文檔](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

下圖顯示要提交到名為Java Servlet的 `HandleData` 的子菜單。

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

下表說明了圖中的步驟。

<table>
 <thead>
  <tr>
   <th><p>步驟</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>用戶填寫互動式表單，然後按一下表單的「提交」按鈕。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>資料已提交到 <code>HandleData</code> 作為XML資料的Java Servlet。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>的 <code>HandleData</code> Java Servlet包含用於檢索資料的應用程式邏輯。</p></td>
  </tr>
 </tbody>
</table>

## 處理已提交的XML資料 {#handling-submitted-xml-data}

當表單資料以XML形式提交時，可以檢索表示已提交資料的XML資料。 所有表單域都以XML架構中的節點形式顯示。 節點值與用戶填入的值相對應。 請考慮一個借出表單，在該表單中，每個欄位都作為XML資料中的節點顯示。 每個節點的值與用戶填入的值相對應。 假定用戶使用以下表單中顯示的資料填充貸款表單。

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

下圖顯示了使用Forms服務客戶端API檢索的相應XML資料。

![hs_hs_loandata](assets/hs_hs_loandata.png)

貸款窗體中的欄位。 可以使用Java XML類檢索這些值。

>[!NOTE]
>
>必須在設計器中正確配置表單設計，才能將資料作為XML資料提交。 要正確配置表單設計以提交XML資料，請確保將表單設計上的「提交」按鈕設定為提交XML資料。 有關設定「提交」按鈕以提交XML資料的資訊，請參閱 [AEM Forms設計師](https://www.adobe.com/go/learn_aemforms_designer_63_tw)。

## 處理已提交的PDF資料 {#handling-submitted-pdf-data}

考慮調用Forms服務的Web應用程式。 在Forms服務將互動式PDF表單呈現給客戶端web瀏覽器之後，用戶填寫表單並將其作為PDF資料提交回來。 當Forms服務接收到PDF資料時，它可以將PDF資料發送到另一服務或將其保存為PDF檔案。 下圖顯示了應用程式的邏輯流。

![hs_hs_saving表單](assets/hs_hs_savingforms.png)

下表介紹了此圖中的步驟。

<table>
 <thead>
  <tr>
   <th><p>步驟</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>網頁包含訪問調用Forms服務的Java Servlet的連結。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Forms服務向客戶端Web瀏覽器呈現互動式PDF表單。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用戶填寫互動式表單，然後按一下提交按鈕。 表格作為PDF資料提交回Forms服務。 此選項在設計器中設定。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms服務將PDF資料保存為PDF檔案。 </p></td>
  </tr>
 </tbody>
</table>

## 處理已提交的URL UTF-16資料 {#handling-submitted-url-utf-16-data}

如果表單資料以URL UTF-16資料提交，則客戶端電腦需要Adobe Reader或Acrobat 8.1或更高版本。 此外，如果表單設計包含具有URL編碼資料(HTTP Post)的提交按鈕，且資料編碼選項為UTF-16，則必須在文本編輯器（如記事本）中修改表單設計。 可以將編碼選項設定為 `UTF-16LE` 或 `UTF-16BE` 按鈕。 設計器不提供此功能。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

要處理已提交的表單，請執行以下任務：

1. 包括項目檔案。
1. 建立Forms客戶端API對象。
1. 檢索表單資料。
1. 確定表單提交是否包含檔案附件。
1. 處理提交的資料。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Forms客戶端API對象**

在以寫程式方式執行Forms服務客戶端API操作之前，必須建立Forms服務客戶端。 如果使用Java API，請建立 `FormsServiceClient` 的雙曲餘切值。 如果使用FormsWeb服務API，請建立 `FormsService` 的雙曲餘切值。

**檢索表單資料**

要檢索已提交的表單資料，請調用 `FormsServiceClient` 對象 `processFormSubmission` 的雙曲餘切值。 調用此方法時，必須指定已提交表單的內容類型。 當資料從客戶端Web瀏覽器提交到Forms服務時，它可以作為XML或PDF資料提交。 要檢索輸入到表單域中的資料，可以將資料作為XML資料提交。

還可以通過設定以下運行時選項從作為PDF資料提交的表單中檢索表單域：

* 將以下值傳遞給 `processFormSubmission` 方法： `CONTENT_TYPE=application/pdf`。
* 設定 `RenderOptionsSpec` 對象 `PDFToXDP` 值 `true`
* 設定 `RenderOptionsSpec` 對象 `ExportDataFormat` 值 `XMLData`

在調用 `processFormSubmission` 的雙曲餘切值。 以下清單指定了適用的內容類型值：

* **文本/xml**:表示PDF表單將表單資料提交為XML時要使用的內容類型。
* **應用程式/x-www格式 — urlencoded**:表示HTML表單以XML形式提交資料時要使用的內容類型。
* **應用程式/pdf**:表示PDF表單將資料提交為PDF時要使用的內容類型。

>[!NOTE]
>
>您將注意到「處理已提交的Forms」部分有三個相應的快速開始。 使用Java API快速啟動將作為PDF提交的處理PDF forms演示了如何處理提交的PDF資料。 此快速啟動中指定的內容類型為 `application/pdf`。 使用Java API快速啟動將作為XML提交的處理PDF forms演示如何處理從PDF表單提交的已提交XML資料。 此快速啟動中指定的內容類型為 `text/xml`。 同樣，使用Java API快速啟動作為XML提交的處理HTML表單演示了如何處理從HTML表單提交的已提交XML資料。 此快速啟動中指定的內容類型是application/x-www-form-urlencoded。

您可以檢索已發佈到Forms服務的表單資料並確定其處理狀態。 即，當資料提交給Forms處時，並不一定意味著Forms處理完資料，準備處理資料。 例如，資料可以提交到Forms服務，以便執行計算。 計算完成後，表單將呈現給用戶，並顯示計算結果。 在處理提交的資料之前，建議您確定Forms服務是否已完成處理資料。

Forms服務返回以下值，以指示它是否已完成資料處理：

* **0（提交）:** 已提交資料已準備好進行處理。
* **1（計算）:** Forms服務對資料執行了計算操作，結果必須返還給用戶。
* **2（驗證）:** Forms服務已驗證表單資料，結果必須返還給用戶。
* **3（下一個）:** 當前頁面已更改，結果必須寫入客戶端應用程式。
* **4（上一個）**):當前頁面已更改，結果必須寫入客戶端應用程式。

>[!NOTE]
>
>計算和驗證必須返回給用戶。 (請參閱 [計算表單資料](/help/forms/developing/calculating-form-data.md#calculating-form-data)。

**確定表單提交是否包含檔案附件**

Forms提交給Forms服務可包含檔案附件。 例如，使用Acrobat的內置附件窗格，用戶可以選擇要連同表單一起提交的檔案附件。 此外，用戶還可以使用HTML工具欄選擇檔案附件，該工具欄用HTML檔案呈現。

在確定表單是否包含檔案附件後，您可以處理資料。 例如，可以將檔案附件保存到本地檔案系統。

>[!NOTE]
>
>必須將表單作為PDF資料提交，以檢索檔案附件。 如果表單以XML資料形式提交，則檔案附件不會提交。

**處理提交的資料**

根據已提交資料的內容類型，您可以從已提交的XML資料中提取單個表單欄位值，或將已提交的PDF資料另存為PDF檔案（或將其發送到其他服務）。 要提取單個表單域，請將提交的XML資料轉換為XML資料源，然後使用 `org.w3c.dom` 類。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案轉給Forms](/help/forms/developing/passing-documents-forms-service.md)

[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API處理提交的表單 {#handle-submitted-forms-using-the-java-api}

使用FormsAPI(Java)處理提交的表單：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。

1. 建立Forms客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索表單資料

   * 要檢索已發佈到Java Servlet的表單資料，請建立 `com.adobe.idp.Document` 使用其建構子調用對象 `javax.servlet.http.HttpServletResponse` 對象 `getInputStream` 方法。
   * 建立 `RenderOptionsSpec` 對象。 通過調用 `RenderOptionsSpec` 對象 `setLocale` 方法，並傳遞指定區域設定值的字串值。

   >[!NOTE]
   >
   >您可以通過調用Forms服務從提交的PDF內容建立XDP或XML資料 `RenderOptionsSpec` 對象 `setPDF2XDP` 方法 `true` 還有 `setXMLData` 傳 `true`。 然後，您可以調用 `FormsResult` 對象 `getOutputXML` 用於檢索與XDP/XML資料對應的XML資料的方法。 ( `FormsResult` 對象由 `processFormSubmission` 方法，下一步中將說明。)

   * 調用 `FormsServiceClient` 對象 `processFormSubmission` 方法並傳遞以下值：

      * 的 `com.adobe.idp.Document` 包含窗體資料的對象。
      * 一個字串值，它指定包括所有相關HTTP標頭的環境變數。 指定要處理的內容類型。 要處理XML資料，請為此參數指定以下字串值： `CONTENT_TYPE=text/xml`。 要處理PDF資料，請為此參數指定以下字串值： `CONTENT_TYPE=application/pdf`。
      * 一個字串值，它指定 `HTTP_USER_AGENT` 標題值，例如。 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。此參數值是可選的。
      * A `RenderOptionsSpec` 儲存運行時選項的對象。

      的 `processFormSubmission` 方法返回 `FormsResult` 包含表單提交結果的對象。

   * 通過調用 `FormsResult` 對象 `getAction` 的雙曲餘切值。 如果此方法返回值 `0`，資料已準備好處理。



1. 確定表單提交是否包含檔案附件

   * 調用 `FormsResult` 對象 `getAttachments` 的雙曲餘切值。 此方法返回 `java.util.List` 包含隨窗體提交的檔案的對象。
   * 迭代 `java.util.List` 對象，以確定是否存在檔案附件。 如果存在檔案附件，則每個元素都是 `com.adobe.idp.Document` 實例。 通過調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法和通過 `java.io.File` 的雙曲餘切值。

   >[!NOTE]
   >
   >此步驟僅在表單作為PDF提交時才適用。

1. 處理提交的資料

   * 如果資料內容類型為 `application/vnd.adobe.xdp+xml` 或 `text/xml`，建立應用程式邏輯以檢索XML資料值。

      * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
      * 建立 `java.io.InputStream` 通過調用 `java.io.DataInputStream` 建構子和傳遞 `com.adobe.idp.Document` 的雙曲餘切值。
      * 建立 `org.w3c.dom.DocumentBuilderFactory` 通過調用靜態 `org.w3c.dom.DocumentBuilderFactory` 對象 `newInstance` 的雙曲餘切值。
      * 建立 `org.w3c.dom.DocumentBuilder` 通過調用 `org.w3c.dom.DocumentBuilderFactory` 對象 `newDocumentBuilder` 的雙曲餘切值。
      * 建立 `org.w3c.dom.Document` 通過調用 `org.w3c.dom.DocumentBuilder` 對象 `parse` 方法和傳遞 `java.io.InputStream` 的雙曲餘切值。
      * 檢索XML文檔中每個節點的值。 完成此任務的一種方法是建立接受兩個參數的自定義方法：這樣 `org.w3c.dom.Document` 對象和要檢索其值的節點的名稱。 此方法返回表示節點值的字串值。 在此流程後面的代碼示例中，此自定義方法被調用 `getNodeText`。 給出了該方法的主體結構。
   * 如果資料內容類型為 `application/pdf`，建立應用程式邏輯以將提交的PDF資料另存為PDF檔案。

      * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
      * 建立 `java.io.File` 對象。 請確保將PDF指定為檔案副檔名。
      * 通過調用PDF檔案 `com.adobe.idp.Document` 對象 `copyToFile` 方法和傳遞 `java.io.File` 的雙曲餘切值。


**另請參閱**

[快速啟動（SOAP模式）:使用Java API處理作為XML提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[快速啟動（SOAP模式）:使用Java API處理作為XML提交的HTML表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[快速啟動（SOAP模式）:使用Java API處理作為PDF提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API處理已提交的PDF資料 {#handle-submitted-pdf-data-using-the-web-service-api}

使用FormsAPI（Web服務）處理提交的表單：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包括到類路徑中。

1. 建立Forms客戶端API對象

   建立 `FormsService` 對象和設定驗證值。

1. 檢索表單資料

   * 要檢索已發佈到Java Servlet的表單資料，請建立 `BLOB` 對象。
   * 建立 `java.io.InputStream` 通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getInputStream` 的雙曲餘切值。
   * 建立 `java.io.ByteArrayOutputStream` 對象，使用其建構子並傳遞 `java.io.InputStream` 的雙曲餘切值。
   * 複製 `java.io.InputStream` 對象 `java.io.ByteArrayOutputStream` 的雙曲餘切值。
   * 通過調用 `java.io.ByteArrayOutputStream` 對象 `toByteArray` 的雙曲餘切值。
   * 填充 `BLOB` 通過調用對象 `setBinaryData` 方法，並將位元組陣列作為參數傳遞。
   * 建立 `RenderOptionsSpec` 對象。 通過調用 `RenderOptionsSpec` 對象 `setLocale` 方法，並傳遞指定區域設定值的字串值。
   * 調用 `FormsService` 對象 `processFormSubmission` 方法並傳遞以下值：

      * 的 `BLOB` 包含窗體資料的對象。
      * 一個字串值，它指定包括所有相關HTTP標頭的環境變數。 指定要處理的內容類型。 要處理XML資料，請為此參數指定以下字串值： `CONTENT_TYPE=text/xml`。 要處理PDF資料，請為此參數指定以下字串值： `CONTENT_TYPE=application/pdf`。
      * 一個字串值，它指定 `HTTP_USER_AGENT` 標題值；比如說， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * A `RenderOptionsSpec` 儲存運行時選項的對象。
      * 空 `BLOBHolder` 由方法填充的對象。
      * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的對象。
      * 空 `BLOBHolder` 由方法填充的對象。
      * 空 `BLOBHolder` 由方法填充的對象。
      * 空 `javax.xml.rpc.holders.ShortHolder` 由方法填充的對象。
      * 空 `MyArrayOf_xsd_anyTypeHolder` 由方法填充的對象。 此參數用於儲存隨表單一起提交的檔案附件。
      * 空 `FormsResultHolder` 由方法填充且已提交表單的對象。

      的 `processFormSubmission` 方法填充 `FormsResultHolder` 參數。

   * 通過調用 `FormsResult` 對象 `getAction` 的雙曲餘切值。 如果此方法返回值 `0`，表單資料已準備好處理。 你可以 `FormsResult` 通過獲取 `FormsResultHolder` 對象 `value` 資料成員。


1. 確定表單提交是否包含檔案附件

   獲取的值 `MyArrayOf_xsd_anyTypeHolder` 對象 `value` 資料成員( `MyArrayOf_xsd_anyTypeHolder` 對象已傳遞給 `processFormSubmission` )。 此資料成員返回 `Objects`。 在 `Object` 陣列是 `Object`與隨表單一起提交的檔案相對應。 您可以獲取陣列中的每個元素並將其轉換為 `BLOB` 的雙曲餘切值。

1. 處理提交的資料

   * 如果資料內容類型為 `application/vnd.adobe.xdp+xml` 或 `text/xml`，建立應用程式邏輯以檢索XML資料值。

      * 建立 `BLOB` 通過調用 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
      * 通過調用 `BLOB` 對象 `getBinaryData` 的雙曲餘切值。
      * 建立 `java.io.InputStream` 通過調用 `java.io.ByteArrayInputStream` 建構子和傳遞位元組陣列。
      * 建立 `org.w3c.dom.DocumentBuilderFactory` 通過調用靜態 `org.w3c.dom.DocumentBuilderFactory` 對象 `newInstance` 的雙曲餘切值。
      * 建立 `org.w3c.dom.DocumentBuilder` 通過調用 `org.w3c.dom.DocumentBuilderFactory` 對象 `newDocumentBuilder` 的雙曲餘切值。
      * 建立 `org.w3c.dom.Document` 通過調用 `org.w3c.dom.DocumentBuilder` 對象 `parse` 方法和傳遞 `java.io.InputStream` 的雙曲餘切值。
      * 檢索XML文檔中每個節點的值。 完成此任務的一種方法是建立接受兩個參數的自定義方法：這樣 `org.w3c.dom.Document` 對象和要檢索其值的節點的名稱。 此方法返回表示節點值的字串值。 在此流程後面的代碼示例中，此自定義方法被調用 `getNodeText`。 給出了該方法的主體結構。
   * 如果資料內容類型為 `application/pdf`，建立應用程式邏輯以將提交的PDF資料另存為PDF檔案。

      * 建立 `BLOB` 通過調用 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
      * 通過調用 `BLOB` 對象 `getBinaryData` 的雙曲餘切值。
      * 建立 `java.io.File` 對象。 請確保將PDF指定為檔案副檔名。
      * 建立 `java.io.FileOutputStream` 使用其建構子並傳遞對象 `java.io.File` 的雙曲餘切值。
      * 通過調用PDF檔案 `java.io.FileOutputStream` 對象 `write` 和傳遞位元組陣列。


**另請參閱**

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
