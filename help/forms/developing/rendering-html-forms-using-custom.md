---
title: 使用自訂CSS檔案轉譯HTML Forms
seo-title: 使用自訂CSS檔案轉譯HTML Forms
description: 使用Forms服務參照自訂CSS檔案，以回應來自網頁瀏覽器的HTTP要求而轉譯HTML表單。 您可以使用Java API和網站服務API來轉譯使用CSS檔案的HTML表單。
seo-description: 使用Forms服務參照自訂CSS檔案，以回應來自網頁瀏覽器的HTTP要求而轉譯HTML表單。 您可以使用Java API和網站服務API來轉譯使用CSS檔案的HTML表單。
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
source-wordcount: '1738'
ht-degree: 0%

---

# 使用自訂CSS檔案{#rendering-html-forms-using-custom-css-files}呈現HTMLForms

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

Forms服務會回應來自網頁瀏覽器的HTTP要求而轉譯HTML表單。 轉譯HTML表單時，Forms服務可參考自訂CSS檔案。 您可以建立自訂CSS檔案，以符合您的業務需求，並在使用Forms服務轉譯HTML表單時參考該CSS檔案。

Forms服務會以靜默方式解析自訂CSS檔案。 也就是說，如果自訂CSS檔案不符合CSS標準，Forms服務不會報告可能遇到的錯誤。 在此情況下，Forms服務會忽略樣式，並繼續處理CSS檔案中剩餘的樣式。

下列清單指定自訂CSS檔案支援的樣式：

* **類別層級選取器樣式配對**:如果自訂CSS檔案中存在，則會使用HTML表單中作為類別樣式使用的選取器。未使用的類樣式被忽略。
* **識別碼層級選取器樣式配對**:如果在HTML表單中使用了所有識別碼樣式，則會使用這些樣式。
* **元素層級選取器樣式配對**:如果在HTML表單中使用所有元素樣式，則會使用這些樣式。
* **樣式優先順序**:樣式優先順序（如重要）受支援，可用於自訂CSS檔案。
* **媒體類型**:一或多個選取器樣式組可以包裝@media樣式以定義媒體類型。Forms服務不會檢查指定的媒體類型是否受支援。 自訂CSS檔案中指定的媒體類型會合併為HTML表單。

您可以使用FormsIVS應用程式擷取範例CSS檔案。 上傳表單，在「測試表單設計」頁面中選取該表單，然後按一下「產生CSS」。 在按一下按鈕之前，您不需要設定HTML轉換類型。 下一步選擇「保存」。 您可以編輯此CSS檔案以符合您的業務需求。

>[!NOTE]
>
>在轉譯使用自訂CSS檔案的HTML表單之前，請務必對轉譯HTML表單有充分的了解。 (請參閱[將Forms呈現為HTML](/help/forms/developing/rendering-forms-html.md)。)

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟{#summary-of-steps}的摘要

要呈現使用CSS檔案的HTML表單，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms Java API物件。
1. 參考CSS檔案。
1. 轉譯HTML表單。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms Java API物件**

您必須先建立Forms用戶端物件，才能以程式設計方式執行Forms服務支援的操作。

**參考CSS檔案**

若要呈現使用自訂CSS檔案的HTML表單，請確定您參考現有的CSS檔案。

**轉譯HTML表單**

要呈現HTML表單，必須指定在「設計器」中建立並另存為XDP檔案的表單設計。 您也必須選取HTML轉換類型。 例如，您可以指定HTML轉換類型，為Internet Explorer 5.0或更新版本轉譯動態HTML。

呈現HTML表單還需要值，如呈現其他表單類型所需的URI值。

**將表單資料流寫入客戶端Web瀏覽器**

Forms服務轉譯HTML表單時，會傳回表單資料流，您必須將此資料流寫入用戶端網頁瀏覽器，才能讓使用者看到HTML表單。

**另請參閱**

[使用Java API轉譯使用CSS檔案的HTML表單](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉譯互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[將Forms轉譯為HTML](/help/forms/developing/rendering-forms-html.md)

[建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API {#render-an-html-form-that-uses-a-css-file-using-the-java-api}呈現使用CSS檔案的HTML表單

使用Forms API(Java)演算使用自訂CSS檔案的HTML表單：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms Java API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`FormsServiceClient`物件。

1. 參考CSS檔案

   * 使用其建構子建立`HTMLRenderSpec`物件。
   * 要呈現使用自定義CSS檔案的HTML表單，請調用`HTMLRenderSpec`對象的`setCustomCSSURI`方法並傳遞一個字串值，該字串值指定CSS檔案的位置和名稱。

1. 轉譯HTML表單

   調用`FormsServiceClient`對象的`(Deprecated) (Deprecated) renderHTMLForm`方法並傳遞以下值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定HTML首選項類型的`TransformTo`枚舉值。 例如，要呈現與Internet Explorer 5.0或更高版本的動態HTML相容的HTML表單，請指定`TransformTo.MSDHTML`。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`com.adobe.idp.Document`物件。
   * 儲存HTML運行時選項的`HTMLRenderSpec`對象。
   * 指定`HTTP_USER_AGENT`標題值（如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`）的字串值。
   * `URLSpec`物件，用於儲存呈現HTML表單所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。

   `(Deprecated) renderHTMLForm`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 調用`FormsResult`對象s `getOutputContent`方法，建立`com.adobe.idp.Document`對象。
   * 調用`getContentType`方法，獲取`com.adobe.idp.Document`對象的內容類型。
   * 通過調用`setContentType`方法並傳遞`com.adobe.idp.Document`對象的內容類型來設定`javax.servlet.http.HttpServletResponse`對象的內容類型。
   * 通過調用`javax.servlet.h\ttp.HttpServletResponse`對象的`getOutputStream`方法，建立用於將表單資料流寫入客戶端Web瀏覽器的`javax.servlet.ServletOutputStream`對象。
   * 調用`com.adobe.idp.Document`對象的`getInputStream`方法，建立`java.io.InputStream`對象。
   * 叫用`InputStream`物件的`read`方法，並將位元組陣列傳遞為引數，借此建立位元組陣列，並填入表單資料流。
   * 調用`javax.servlet.ServletOutputStream`對象的`write`方法，將表單資料流發送到客戶端Web瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[使用自訂CSS檔案轉譯HTML Forms](#rendering-html-forms-using-custom-css-files)

[快速入門（SOAP模式）:使用Java API轉譯使用CSS檔案的HTML表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}呈現使用CSS檔案的HTML表單

使用Forms API（網站服務）轉譯使用自訂CSS檔案的HTML表單：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 在類路徑中包含Java代理類。

1. 建立Forms Java API物件

   建立`FormsService`物件並設定驗證值。

1. 參考CSS檔案

   * 使用其建構子建立`HTMLRenderSpec`物件。
   * 要呈現使用自定義CSS檔案的HTML表單，請調用`HTMLRenderSpec`對象的`setCustomCSSURI`方法並傳遞一個字串值，該字串值指定CSS檔案的位置和名稱。

1. 轉譯HTML表單

   調用`FormsService`對象的`(Deprecated) renderHTMLForm`方法並傳遞以下值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定HTML首選項類型的`TransformTo`枚舉值。 例如，要呈現與Internet Explorer 5.0或更高版本的動態HTML相容的HTML表單，請指定`TransformTo.MSDHTML`。
   * `BLOB`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞`null`。 (請參閱[使用可流動配置預填Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
   * 儲存HTML運行時選項的`HTMLRenderSpec`對象。
   * 指定`HTTP_USER_AGENT`標題值（如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`）的字串值。 如果您不想設定此值，可以傳遞空白字串。
   * `URLSpec`物件，用於儲存呈現HTML表單所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。
   * 由`(Deprecated) renderHTMLForm`方法填入的空`com.adobe.idp.services.holders.BLOBHolder`物件。 此參數值儲存呈現的表單。
   * 由`(Deprecated) renderHTMLForm`方法填入的空`com.adobe.idp.services.holders.BLOBHolder`物件。 此參數儲存輸出XML資料。
   * 由`(Deprecated) renderHTMLForm`方法填入的空`javax.xml.rpc.holders.LongHolder`物件。 此引數會儲存表單中的頁數。
   * 由`(Deprecated) renderHTMLForm`方法填入的空`javax.xml.rpc.holders.StringHolder`物件。 此參數儲存地區設定值。
   * 由`(Deprecated) renderHTMLForm`方法填入的空`javax.xml.rpc.holders.StringHolder`物件。 此引數會儲存所使用的HTML呈現值。
   * 將包含此操作結果的空`com.adobe.idp.services.holders.FormsResultHolder`對象。

   `(Deprecated) renderHTMLForm`方法會以必須寫入用戶端網頁瀏覽器的表單資料流填入作為最後一個引數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 獲取`com.adobe.idp.services.holders.FormsResultHolder`對象的`value`資料成員的值，以建立`FormResult`對象。
   * 調用`FormsResult`對象的`getOutputContent`方法，建立包含表單資料的`BLOB`對象。
   * 調用`getContentType`方法，獲取`BLOB`對象的內容類型。
   * 通過調用`setContentType`方法並傳遞`BLOB`對象的內容類型來設定`javax.servlet.http.HttpServletResponse`對象的內容類型。
   * 通過調用`javax.servlet.http.HttpServletResponse`對象的`getOutputStream`方法，建立用於將表單資料流寫入客戶端Web瀏覽器的`javax.servlet.ServletOutputStream`對象。
   * 建立位元組陣列，並調用`BLOB`對象的`getBinaryData`方法來填入。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 調用`javax.servlet.http.HttpServletResponse`對象的`write`方法，將表單資料流發送到客戶端Web瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[使用自訂CSS檔案轉譯HTML Forms](#rendering-html-forms-using-custom-css-files)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
