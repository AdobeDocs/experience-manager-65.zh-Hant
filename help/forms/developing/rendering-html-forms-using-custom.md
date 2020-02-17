---
title: 使用自訂CSS檔案轉換HTML表格
seo-title: 使用自訂CSS檔案轉換HTML表格
description: 'null'
seo-description: 'null'
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用自訂CSS檔案轉換HTML表格 {#rendering-html-forms-using-custom-css-files}

Forms服務會根據來自網頁瀏覽器的HTTP要求轉譯HTML表格。 轉換HTML表格時，Forms服務可以參考自訂CSS檔案。 您可以建立自訂的CSS檔案，以符合您的業務需求，並在使用Forms服務轉換HTML表格時參考該CSS檔案。

Forms服務會以無訊息方式解析自訂CSS檔案。 也就是說，如果自訂CSS檔案不符合CSS標準，Forms服務不會報告可能遇到的錯誤。 在此情況下，Forms服務會忽略樣式，並繼續使用CSS檔案中的其餘樣式。

下列清單指定自訂CSS檔案支援的樣式：

* **類別級選擇器樣式對**:如果自訂CSS檔案中有選取器，則會使用HTML表單中用作類別樣式的選取器。 未使用的類樣式將被忽略。
* **識別碼層級選擇器——樣式配對**:如果所有識別碼樣式都用於HTML表單，則會使用這些樣式。
* **元素層級選取器——樣式對**:如果所有元素樣式都用於HTML表單，則會使用這些樣式。
* **樣式優先順序**:樣式優先順序（如重要）受支援，可用於自訂CSS檔案。
* **媒體類型**:一個或多個選擇器樣式對可以用@media樣式包住，以定義媒體類型。 Forms服務不檢查是否支援指定的介質類型。 自訂CSS檔案中指定的媒體類型會合併為HTML表單。

您可以使用FormsIVS應用程式擷取範例CSS檔案。 上傳表單，在「測試表單設計」頁面中選取它，然後按一下「產生CSS」。 您不需要在按一下按鈕之前設定HTML轉換類型。 接下來選擇「儲存」。 您可以編輯此CSS檔案，以符合您的業務需求。

>[!NOTE]
>
>在轉換使用自訂CSS檔案的HTML表格之前，請務必對轉換HTML表格有紮實的瞭解。 (請參 [閱「將表單轉換為HTML](/help/forms/developing/rendering-forms-html.md)」)。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱「AEM Forms [的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

若要轉換使用CSS檔案的HTML表格，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms Java API物件。
1. 參考CSS檔案。
1. 演算HTML表格。
1. 將表單資料流寫入用戶端網頁瀏覽器。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms Java API物件**

您必須先建立Forms用戶端物件，才能以程式設計方式執行Forms服務支援的作業。

**參考CSS檔案**

若要轉換使用自訂CSS檔案的HTML表格，請確定您參考現有的CSS檔案。

**轉換HTML表格**

要渲染HTML表單，必須指定在Designer中建立並另存為XDP檔案的表單設計。 您還必須選擇HTML轉換類型。 例如，您可以指定轉換Internet Explorer 5.0或更新版本動態HTML的HTML轉換類型。

轉換HTML表單也需要值，例如轉換其他表單類型所需的URI值。

**將表單資料串流寫入用戶端網頁瀏覽器**

當Forms服務轉譯HTML表單時，它會傳回您必須寫入用戶端網頁瀏覽器的表單資料串流，讓使用者可以看見HTML表單。

**另請參閱**

[使用Java API演算使用CSS檔案的HTML表格](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉換互動式PDF表單](/help/forms/developing/rendering-interactive-pdf-forms.md)

[將表單轉換為HTML](/help/forms/developing/rendering-forms-html.md)

[建立轉譯表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API演算使用CSS檔案的HTML表格 {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

使用Forms API(Java)演算使用自訂CSS檔案的HTML表格：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms Java API物件

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `FormsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考CSS檔案

   * 使用其 `HTMLRenderSpec` 建構函式建立物件。
   * 若要轉換使用自訂CSS檔案的HTML表單，請 `HTMLRenderSpec` 叫用物件的方 `setCustomCSSURI` 法，並傳遞指定CSS檔案位置和名稱的字串值。

1. 轉換HTML表格

   叫用物 `FormsServiceClient` 件的方 `(Deprecated) (Deprecated) renderHTMLForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參照屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定 `TransformTo` HTML首選項類型的枚舉值。 例如，若要轉譯與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表格，請指定 `TransformTo.MSDHTML`。
   * 包 `com.adobe.idp.Document` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞空 `com.adobe.idp.Document` 物件。
   * 儲存 `HTMLRenderSpec` HTML執行時期選項的物件。
   * 指定標題值的字 `HTTP_USER_AGENT` 串值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * 存 `URLSpec` 儲呈現HTML表單所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不要將檔案附加到表單。
   該方 `(Deprecated) renderHTMLForm` 法返回包 `FormsResult` 含必須寫入客戶端Web瀏覽器的表單資料流的對象。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 通過調 `com.adobe.idp.Document` 用對象的方法 `FormsResult` 建立對 `getOutputContent` 像。
   * 通過調用對象的方 `com.adobe.idp.Document` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `com.adobe.idp.Document` 類型。
   * 呼叫 `javax.servlet.ServletOutputStream` 物件的方法，建立用於將表單資料串流寫入用戶端Web `javax.servlet.h\ttp.HttpServletResponse` 瀏覽器的物 `getOutputStream` 件。
   * 調用 `java.io.InputStream` 物件的方 `com.adobe.idp.Document` 法以建立物 `getInputStream` 件。
   * 建立位元組陣列，並借由調用物件的方法並將 `InputStream` 位元組陣列 `read` 傳入為引數，以表單資料流填入。
   * 叫用物 `javax.servlet.ServletOutputStream` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[使用自訂CSS檔案轉換HTML表格](#rendering-html-forms-using-custom-css-files)

[快速入門（SOAP模式）:使用Java API轉換使用CSS檔案的HTML表格](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API演算使用CSS檔案的HTML表格 {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

使用Forms API(web service)演算使用自訂CSS檔案的HTML表格：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 在類路徑中包含Java代理類。

1. 建立Forms Java API物件

   建立對 `FormsService` 像並設定驗證值。

1. 參考CSS檔案

   * 使用其 `HTMLRenderSpec` 建構函式建立物件。
   * 若要轉換使用自訂CSS檔案的HTML表單，請 `HTMLRenderSpec` 叫用物件的方 `setCustomCSSURI` 法，並傳遞指定CSS檔案位置和名稱的字串值。

1. 轉換HTML表格

   叫用物 `FormsService` 件的方 `(Deprecated) renderHTMLForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參照屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定 `TransformTo` HTML首選項類型的枚舉值。 例如，若要轉譯與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表格，請指定 `TransformTo.MSDHTML`。
   * 包 `BLOB` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞 `null`。 (請參 [閱「使用可排程版面預填表單」](/help/forms/developing/rendering-forms-rendering-forms preming-forms-flowable-layouts-premilting.md#preming-forms-with-flowable-layouts)。
   * 儲存 `HTMLRenderSpec` HTML執行時期選項的物件。
   * 指定標題值的字 `HTTP_USER_AGENT` 串值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。 如果您不想設定此值，可以傳遞空字串。
   * 存 `URLSpec` 儲呈現HTML表單所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不要將檔案附加到表單。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填入的空對 `(Deprecated) renderHTMLForm` 像。 此參數值儲存渲染的表單。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填入的空對 `(Deprecated) renderHTMLForm` 像。 此參數儲存輸出XML資料。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填入的空對 `(Deprecated) renderHTMLForm` 像。 此引數會儲存表單中的頁數。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填入的空對 `(Deprecated) renderHTMLForm` 像。 此引數儲存地區值。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填入的空對 `(Deprecated) renderHTMLForm` 像。 此引數儲存所使用的HTML轉換值。
   * 包含 `com.adobe.idp.services.holders.FormsResultHolder` 此操作結果的空對象。
   該方 `(Deprecated) renderHTMLForm` 法用必 `com.adobe.idp.services.holders.FormsResultHolder` 須寫入客戶端Web瀏覽器的表單資料流填充作為最後一個參數值傳遞的對象。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 獲取 `FormResult` 對象資料成員的 `com.adobe.idp.services.holders.FormsResultHolder` 值以建立 `value` 對象。
   * 呼叫 `BLOB` 物件的方法，以建立包含表 `FormsResult` 單資料的物 `getOutputContent` 件。
   * 通過調用對象的方 `BLOB` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `BLOB` 類型。
   * 呼叫 `javax.servlet.ServletOutputStream` 物件的方法，建立用於將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器的物 `getOutputStream` 件。
   * 建立位元組陣列，並透過叫用物件的方 `BLOB` 法來填入該 `getBinaryData` 陣列。 此任務將對象的內 `FormsResult` 容分配給位元組陣列。
   * 叫用物 `javax.servlet.http.HttpServletResponse` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[使用自訂CSS檔案轉換HTML表格](#rendering-html-forms-using-custom-css-files)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
