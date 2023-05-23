---
title: 使用自定義CSS檔案呈現HTMLForms
seo-title: Rendering HTML Forms Using Custom CSS Files
description: 使用Forms服務引用自定義CSS檔案以響應來自Web瀏覽器的HTTP請求來呈現HTML表單。 可以使用Java API和Web服務API呈現使用CSS檔案的HTML表單。
seo-description: Use the Forms service to refer to custom CSS files to render HTML forms in response to an HTTP request from a web browser. You can render an HTML form that uses a CSS file using the Java API and Web Service API.
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
role: Developer
exl-id: 5fa385a7-f030-4c0c-8938-0991d02ef361
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1688'
ht-degree: 0%

---

# 使用自定義CSS檔案呈現HTMLForms {#rendering-html-forms-using-custom-css-files}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

Forms服務響應來自Web瀏覽器的HTTP請求來呈現HTML表單。 呈現HTML表單時，Forms服務可以引用自定義CSS檔案。 使用Forms服務呈現HTML表單時，可以建立自定義CSS檔案以滿足業務要求並引用該CSS檔案。

Forms服務以靜默方式解析自定義CSS檔案。 即，如果自定義CSS檔案不符合CSS標準，Forms服務不會報告可能遇到的錯誤。 在這種情況下，Forms服務將忽略該樣式，並繼續處理CSS檔案中的其餘樣式。

以下清單指定自定義CSS檔案中支援的樣式：

* **類級別選擇器樣式對**:如果自定義CSS檔案中存在，則使用HTML表單中用作類樣式的選擇器。 未使用的類樣式將被忽略。
* **標識符級別選擇器樣式對**:如果在HTML窗體中使用所有標識符樣式，則使用它們。
* **元素級別選擇器樣式對**:如果在HTML窗體中使用了所有元素樣式，則會使用它們。
* **樣式優先順序**:支援樣式優先順序（與重要資訊一樣），可以在自定義CSS檔案中使用。
* **媒體類型**:一個或多個選擇器樣式對可以用@media樣式包裝以定義媒體類型。 Forms服務不檢查是否支援指定的媒體類型。 在自定義CSS檔案中指定的媒體類型將合併到HTML窗體中。

可以使用FormsIVS應用程式檢索示例CSS檔案。 上載表單，在「Test表單設計」頁中選擇它，然後按一下「生成CSS」。 在按一下按鈕之前，不需要設定HTML轉換類型。 下一步選擇「保存」。 您可以編輯此CSS檔案以滿足您的業務要求。

>[!NOTE]
>
>在呈現使用自定義CSS檔案的HTML表單之前，必須對呈現HTML表單有深入的瞭解。 (請參閱 [讓Forms成為HTML](/help/forms/developing/rendering-forms-html.md)。)

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

要呈現使用CSS檔案的HTML表單，請執行以下任務：

1. 包括項目檔案。
1. 建立FormsJava API對象。
1. 引用CSS檔案。
1. 呈現HTML窗體。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立FormsJava API對象**

在以寫程式方式執行Forms服務支援的操作之前，必須建立Forms客戶端對象。

**引用CSS檔案**

要呈現使用自定義CSS檔案的HTML表單，請確保引用現有CSS檔案。

**呈現HTML窗體**

要呈現HTML窗體，必須指定在設計器中建立並另存為XDP檔案的窗體設計。 還必須選擇HTML轉換類型。 例如，可以指定為Internet Explorer 5.0或更高版本呈現動態HTML的HTML轉換類型。

呈現HTML表單還需要值，如呈現其他表單類型所需的URI值。

**將表單資料流寫入客戶端Web瀏覽器**

當Forms服務呈現HTML表單時，它將返回您必須寫入客戶端Web瀏覽器的表單資料流，以使HTML表單對用戶可見。

**另請參閱**

[使用Java API呈現使用CSS檔案的HTML窗體](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[讓Forms成為HTML](/help/forms/developing/rendering-forms-html.md)

[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API呈現使用CSS檔案的HTML窗體 {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

使用FormsAPI(Java)呈現使用自定義CSS檔案的HTML表單：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。

1. 建立FormsJava API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用CSS檔案

   * 建立 `HTMLRenderSpec` 對象。
   * 要呈現使用自定義CSS檔案的HTML窗體，請調用 `HTMLRenderSpec` 對象 `setCustomCSSURI` 方法並傳遞一個字串值，該字串值指定CSS檔案的位置和名稱。

1. 呈現HTML窗體

   調用 `FormsServiceClient` 對象 `(Deprecated) (Deprecated) renderHTMLForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `TransformTo` 指定HTML首選項類型的枚舉值。 例如，要呈現與Internet Explorer 5.0或更高版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`。
   * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞一個空 `com.adobe.idp.Document` 的雙曲餘切值。
   * 的 `HTMLRenderSpec` 儲存HTML運行時選項的對象。
   * 一個字串值，它指定 `HTTP_USER_AGENT` 標題值，如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * A `URLSpec` 儲存呈現HTML窗體所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。

   的 `(Deprecated) renderHTMLForm` 方法返回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `com.adobe.idp.Document` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `com.adobe.idp.Document` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.h\ttp.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
   * 通過調用 `InputStream` 對象 `read` 方法，並將位元組陣列作為參數傳遞。
   * 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[使用自定義CSS檔案呈現HTMLForms](#rendering-html-forms-using-custom-css-files)

[快速啟動（SOAP模式）:使用Java API呈現使用CSS檔案的HTML窗體](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API呈現使用CSS檔案的HTML窗體 {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

使用FormsAPI（Web服務）呈現使用自定義CSS檔案的HTML表單：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 在類路徑中包括Java代理類。

1. 建立FormsJava API對象

   建立 `FormsService` 對象和設定驗證值。

1. 引用CSS檔案

   * 建立 `HTMLRenderSpec` 對象。
   * 要呈現使用自定義CSS檔案的HTML窗體，請調用 `HTMLRenderSpec` 對象 `setCustomCSSURI` 方法並傳遞一個字串值，該字串值指定CSS檔案的位置和名稱。

1. 呈現HTML窗體

   調用 `FormsService` 對象 `(Deprecated) renderHTMLForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `TransformTo` 指定HTML首選項類型的枚舉值。 例如，要呈現與Internet Explorer 5.0或更高版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`。
   * A `BLOB` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞 `null`。 (請參閱 [用可流式佈局預填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
   * 的 `HTMLRenderSpec` 儲存HTML運行時選項的對象。
   * 一個字串值，它指定 `HTTP_USER_AGENT` 標題值，如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。 如果不想設定此值，可以傳遞空字串。
   * A `URLSpec` 儲存呈現HTML窗體所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 填充的對象 `(Deprecated) renderHTMLForm` 的雙曲餘切值。 此參數值儲存渲染的表單。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 填充的對象 `(Deprecated) renderHTMLForm` 的雙曲餘切值。 此參數儲存輸出XML資料。
   * 空 `javax.xml.rpc.holders.LongHolder` 填充的對象 `(Deprecated) renderHTMLForm` 的雙曲餘切值。 此參數儲存窗體中的頁數。
   * 空 `javax.xml.rpc.holders.StringHolder` 填充的對象 `(Deprecated) renderHTMLForm` 的雙曲餘切值。 此參數儲存區域設定值。
   * 空 `javax.xml.rpc.holders.StringHolder` 填充的對象 `(Deprecated) renderHTMLForm` 的雙曲餘切值。 此參數儲存所使用的HTML呈現值。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作結果的對象。

   的 `(Deprecated) renderHTMLForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個參數值傳遞的對象，其表單資料流必須寫入客戶端web瀏覽器。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `FormResult` 通過獲取 `com.adobe.idp.services.holders.FormsResultHolder` 對象 `value` 資料成員。
   * 建立 `BLOB` 通過調用包含表單資料的對象 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `BLOB` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `BLOB` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立位元組陣列，並通過調用 `BLOB` 對象 `getBinaryData` 的雙曲餘切值。 此任務分配 `FormsResult` 對象。
   * 調用 `javax.servlet.http.HttpServletResponse` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[使用自定義CSS檔案呈現HTMLForms](#rendering-html-forms-using-custom-css-files)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
