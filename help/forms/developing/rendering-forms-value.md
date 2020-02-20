---
title: 依值轉換表單
seo-title: 依值轉換表單
description: 'null'
seo-description: 'null'
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 依值轉換表單 {#rendering-forms-by-value}

通常，在設計器中建立的表單設計會參照Forms服務來傳遞。 表單設計可以很大，因此，參照傳遞表單設計會更有效率，以避免需要依值來調整表單設計位元組。 Forms服務也可以快取表格設計，如此在快取時，就不需要持續讀取表格設計。

如果表單設計包含UUID屬性，則會快取它。 UUID值對於所有表單設計都是唯一的，用於唯一標識表單。 在依值呈現表格時，只有在重複使用表格時，才應快取表格。 不過，如果表單未重複使用，且必須是唯一的，您可以使用使用AEM Forms API設定的快取選項來避免快取表單。

Forms服務也可以解決連結內容在表單設計中的位置。 例如，從表單設計中參考的連結影像是相對URL。 連結的內容一律假設是與表單設計位置相關。 因此，解析連結內容是透過將相對路徑套用至絕對表單設計位置來決定其位置的問題。

您可以按值傳遞表單設計，而不是參照傳遞表單設計。 當動態建立表單設計時，以值傳遞表單設計是有效率的；也就是說，當用戶端應用程式產生XML，並在執行時期建立表單設計時。 在這種情況下，表單設計不會儲存在物理儲存庫中，因為它儲存在記憶體中。 在執行時期動態建立表單設計並依值傳遞時，您可以快取表單並改善Forms服務的效能。

**依值傳遞表格的限制**

以下限制適用於依值傳遞表單設計時：

* 表單設計中不能包含任何相關的連結內容。 所有影像和片段都必須內嵌在表單設計中，或絕對參考。
* 在轉譯表單後無法執行伺服器端計算。 如果表單已提交回Forms服務，則會擷取並傳回資料，而不需任何伺服器端計算。
* 由於HTML在執行時期只能使用連結的影像，因此無法產生內嵌影像的HTML。 這是因為Forms服務支援從參考的表單設計擷取影像，以HTML格式內嵌影像。 由於依值傳遞的表單設計沒有參考位置，因此當顯示HTML頁面時，無法擷取內嵌影像。 因此，影像參照必須是絕對路徑，才能在HTML中轉譯。

>[!NOTE]
>
>雖然您可以依值來轉換不同類型的表單（例如，包含使用權限的HTML表單或表單），但本節將討論轉換互動式PDF表單。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱「AEM Forms [的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

要按值呈現表單，請執行以下步驟：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 參考表單設計。
1. 依值演算表格。
1. 將表單資料流寫入用戶端網頁瀏覽器。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

您必須先建立資料整合服務用戶端，才能以程式設計方式將資料匯入PDF表單用戶端API。 建立服務客戶端時，您定義調用服務所需的連接設定。

**參考表單設計**

按值呈現表單時，您必須建立包含要呈 `com.adobe.idp.Document` 現的表單設計的物件。 您可以參考現有的XDP檔案，也可以在執行時期動態建立表單設計，並填入 `com.adobe.idp.Document` 該資料。

>[!NOTE]
>
>本節和相應的快速啟動引用現有XDP檔案。

**依值演算表格**

若要依值來轉換表單，請將包含 `com.adobe.idp.Document` 表單設計的例項傳遞至轉換方法的參數 `inDataDoc` (可以是物件的任何轉換方 `FormsServiceClient` 法， `renderPDFForm``(Deprecated) renderHTMLForm`等等)。 此參數值通常保留給與表單合併的資料。 同樣地，將空字串值傳遞至參 `formQuery` 數。 通常，此參數需要一個字串值來指定表單設計的名稱。

>[!NOTE]
>
>如果您想要在表單中顯示資料，則必須在元素中指定 `xfa:datasets` 資料。 如需XFA架構的詳細資訊，請前往 [https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html)。

**將表單資料串流寫入用戶端網頁瀏覽器**

當Forms服務根據值轉換表單時，它會傳回您必須寫入用戶端網頁瀏覽器的表單資料流。 當寫入用戶端網頁瀏覽器時，使用者會看到表單。

**另請參閱**

[使用Java API依值演算表格](#render-a-form-by-value-using-the-java-api)

[使用web service API，依值演算表格](#render-a-form-by-value-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳送至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

[建立轉譯表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API依值演算表格 {#render-a-form-by-value-using-the-java-api}

使用Forms API(Java)依值演算表格：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `FormsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考表單設計

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定XDP檔案位置的字串值，以建立表示要演算之表單設計的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 依值演算表格

   叫用物 `FormsServiceClient` 件的方 `renderPDFForm` 法並傳遞下列值：

   * 空字串值。 （通常，此參數需要一個字串值，它指定表單設計的名稱。）
   * 包 `com.adobe.idp.Document` 含表單設計的物件。 通常，此參數值會保留給與表單合併的資料。
   * 存 `PDFFormRenderSpec` 儲運行時選項的對象。 此為可選參數，您可以指 `null` 定是否不想指定執行時選項。
   * 包 `URLSpec` 含Forms服務所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不想將檔案附加到表單。
   該方 `renderPDFForm` 法返回包 `FormsResult` 含可寫入客戶端Web瀏覽器的表單資料流的對象。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 通過調 `com.adobe.idp.Document` 用對象的方法 `FormsResult` 建立對 `getOutputContent` 像。
   * 通過調用對象的方 `com.adobe.idp.Document` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `com.adobe.idp.Document` 類型。
   * 呼叫 `javax.servlet.ServletOutputStream` 物件的方法，建立用於將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器的物 `getOutputStream` 件。
   * 調用 `java.io.InputStream` 物件的方 `com.adobe.idp.Document` 法以建立物 `getInputStream` 件。
   * 建立位元組陣列並分配對象的大 `InputStream` 小。 叫用 `InputStream` 物件的方 `available` 法，以取得物件的大 `InputStream` 小。
   * 調用物件的方法，並將位元組陣列傳 `InputStream` 遞為引數， `read`以表格資料流填入位元組陣列。
   * 叫用物 `javax.servlet.ServletOutputStream` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[Rendering Forms By Value](/help/forms/developing/rendering-forms.md#rendering-forms-by-value)

[快速入門（SOAP模式）:使用Java API依值演算](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API，依值演算表格 {#render-a-form-by-value-using-the-web-service-api}

使用Forms API(web service)，依值演算表格：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立對 `FormsService` 像並設定驗證值。

1. 參考表單設計

   * 使用其 `java.io.FileInputStream` 建構函式建立物件。 傳遞指定XDP檔案位置的字串值。
   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用於儲存使用密碼加密的PDF檔案。
   * 建立儲存物件內容的位元組 `java.io.FileInputStream` 陣列。 您可以使用物件的方法，來取得物件的大 `java.io.FileInputStream` 小，以判斷位元組陣列的 `available` 大小。
   * 調用物件的方法並傳遞位元組陣列， `java.io.FileInputStream` 以串流資 `read` 料填入位元組陣列。
   * 調用對 `BLOB` 像的方法並傳遞字 `setBinaryData` 節陣列來填充對象。

1. 依值演算表格

   叫用物 `FormsService` 件的方 `renderPDFForm` 法並傳遞下列值：

   * 空字串值。 （通常，此參數需要一個字串值，它指定表單設計的名稱。）
   * 包 `BLOB` 含表單設計的物件。 通常，此參數值會保留給與表單合併的資料。
   * 存 `PDFFormRenderSpec` 儲運行時選項的對象。 此為可選參數，您可以指 `null` 定是否不想指定執行時選項。
   * 包 `URLSpec` 含Forms服務所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不想將檔案附加到表單。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空對象。 這可用來儲存轉譯的PDF表單。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填充的空對象。 （此引數會儲存表單中的頁數。）
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空對象。 （此引數儲存地區值。）
   * 包含 `com.adobe.idp.services.holders.FormsResultHolder` 此操作結果的空對象。
   該方 `renderPDFForm` 法用必 `com.adobe.idp.services.holders.FormsResultHolder` 須寫入客戶端Web瀏覽器的表單資料流填充作為最後一個參數值傳遞的對象。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 獲取 `FormResult` 對象資料成員的 `com.adobe.idp.services.holders.FormsResultHolder` 值以建立 `value` 對象。
   * 呼叫 `BLOB` 物件的方法，以建立包含表 `FormsResult` 單資料的物 `getOutputContent` 件。
   * 通過調用對象的方 `BLOB` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `BLOB` 類型。
   * 呼叫 `javax.servlet.ServletOutputStream` 物件的方法，建立用於將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器的物 `getOutputStream` 件。
   * 建立位元組陣列，並透過叫用物件的方 `BLOB` 法來填入該 `getBinaryData` 陣列。 此任務將對象的內 `FormsResult` 容分配給位元組陣列。
   * 叫用物 `javax.servlet.http.HttpServletResponse` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[依值轉換表單](#rendering-forms-by-value)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
