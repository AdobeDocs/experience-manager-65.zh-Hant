---
title: 按價值呈現Forms
seo-title: 按價值呈現Forms
description: 使用FormsAPI(Java)，使用Java API和Web服務API，依值來轉換表單。
seo-description: 使用FormsAPI(Java)，使用Java API和Web服務API，依值來轉換表單。
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 0%

---


# 按值呈現Forms{#rendering-forms-by-value}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

通常，在設計人員中建立的表單設計會參照Forms服務來傳遞。 表單設計可以很大，因此，參照傳遞表單設計會更有效率，以避免需要依值來調整表單設計位元組。 Forms服務也可以快取表格設計，如此在快取時，就不需持續讀取表格設計。

如果表單設計包含UUID屬性，則會快取它。 UUID值對於所有表單設計都是唯一的，用於唯一標識表單。 在依值呈現表格時，只有在重複使用表格時，才應快取表格。 不過，如果表單不重複使用且必須是唯一的，您可以使用使用AEM FormsAPI設定的快取選項來避免快取表單。

Forms服務也可以解決表單設計中連結內容的位置。 例如，從表單設計中參考的連結影像是相對URL。 連結的內容一律假設是與表單設計位置相關。 因此，解析連結內容是透過將相對路徑套用至絕對表單設計位置來決定其位置的問題。

您可以按值傳遞表單設計，而不是參照傳遞表單設計。 當動態建立表單設計時，以值傳遞表單設計是有效率的；也就是說，當用戶端應用程式產生XML，並在執行時期建立表單設計時。 在這種情況下，表單設計不會儲存在物理儲存庫中，因為它儲存在記憶體中。 在執行時期動態建立表格設計並依值傳遞時，您可以快取表格並改善Forms服務的效能。

**依值傳遞表格的限制**

以下限制適用於依值傳遞表單設計時：

* 表單設計中不能包含任何相關的連結內容。 所有影像和片段都必須內嵌在表單設計中，或絕對參考。
* 在轉譯表單後無法執行伺服器端計算。 如果表單已提交回Forms服務，則會擷取並傳回資料，毋需伺服器端計算。
* 由於HTML在執行時期只能使用連結的影像，因此無法產生內嵌影像的HTML。 這是因為Forms服務支援從參考的表單設計擷取影像，以HTML格式內嵌影像。 由於依值傳遞的表單設計沒有參考位置，因此當顯示HTML頁面時，無法擷取內嵌影像。 因此，影像參照必須是絕對路徑，才能在HTML中轉譯。

>[!NOTE]
>
>雖然您可以依值來呈現不同類型的表單（例如，包含使用權限的HTML表單或表單），但本節將討論轉譯互動式PDF forms。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟{#summary-of-steps}摘要

要按值呈現表單，請執行以下步驟：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 參考表單設計。
1. 依值演算表格。
1. 將表單資料流寫入用戶端網頁瀏覽器。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

您必須先建立資料整合服務用戶端，才能以程式設計方式將資料匯入PDF表單用戶端API。 建立服務客戶端時，您定義調用服務所需的連接設定。

**參考表單設計**

按值呈現表單時，必須建立`com.adobe.idp.Document`對象，該對象包含要渲染的表單設計。 您可以參考現有的XDP檔案，也可以在執行時期動態建立表單設計，並將該資料填入`com.adobe.idp.Document`。

>[!NOTE]
>
>本節和相應的快速啟動引用現有XDP檔案。

**依值演算表格**

若要依值呈現表單，請將包含表單設計的`com.adobe.idp.Document`例項傳遞至呈現方法的`inDataDoc`參數（可以是`FormsServiceClient`物件的任何呈現方法，例如`renderPDFForm`、`(Deprecated) renderHTMLForm`等）。 此參數值通常保留給與表單合併的資料。 同樣地，將空字串值傳遞至`formQuery`參數。 通常，此參數需要一個字串值，它指定表單設計的名稱。

>[!NOTE]
>
>如果要在表單中顯示資料，必須在`xfa:datasets`元素中指定資料。 有關XFA體系結構的資訊，請轉至[https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html)。

**將表單資料串流寫入用戶端網頁瀏覽器**

當Forms服務根據值轉換表單時，它會傳回您必須寫入用戶端網頁瀏覽器的表單資料流。 當寫入用戶端網頁瀏覽器時，使用者會看到表單。

**另請參閱**

[使用Java API依值演算表格](#render-a-form-by-value-using-the-java-api)

[使用web service API，依值演算表格](#render-a-form-by-value-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳遞至Forms](/help/forms/developing/passing-documents-forms-service.md)

[建立轉譯Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API {#render-a-form-by-value-using-the-java-api}依值演算表格

使用FormsAPI(Java)，依值演算表格：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormsServiceClient`對象。

1. 參考表單設計

   * 建立`java.io.FileInputStream`對象，該對象表示要渲染的表單設計，方法是使用其建構子並傳遞指定XDP檔案位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 依值演算表格

   叫用`FormsServiceClient`物件的`renderPDFForm`方法並傳遞下列值：

   * 空字串值。 （通常，此參數需要一個字串值，它指定表單設計的名稱。）
   * 包含表單設計的`com.adobe.idp.Document`物件。 通常，此參數值會保留給與表單合併的資料。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。 此為可選參數，如果您不想指定執行時選項，可以指定`null`。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。

   `renderPDFForm`方法返回`FormsResult`對象，該對象包含可寫入客戶端Web瀏覽器的表單資料流。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 通過調用`FormsResult`對象「s `getOutputContent`」方法建立`com.adobe.idp.Document`對象。
   * 通過調用`getContentType`方法獲取`com.adobe.idp.Document`對象的內容類型。
   * 調用`setContentType`方法並傳遞`com.adobe.idp.Document`物件的內容類型，以設定`javax.servlet.http.HttpServletResponse`物件的內容類型。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立`javax.servlet.ServletOutputStream`物件，用來將表單資料串流寫入用戶端Web瀏覽器。
   * 調用`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 建立位元組陣列並分配`InputStream`對象的大小。 調用`InputStream`物件的`available`方法，以取得`InputStream`物件的大小。
   * 調用`InputStream`物件的`read`方法，並將位元組陣列傳入為引數，以表格資料流填入位元組陣列。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**另請參閱**

[按價值呈現Forms](/help/forms/developing/rendering-forms.md)

[快速入門（SOAP模式）:使用Java API依值演算](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#render-a-form-by-value-using-the-web-service-api}依值呈現表格

使用FormsAPI(web service)，依值轉換表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`對象並設定驗證值。

1. 參考表單設計

   * 使用其建構子建立`java.io.FileInputStream`對象。 傳遞指定XDP檔案位置的字串值。
   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存使用密碼加密的PDF檔案。
   * 建立儲存`java.io.FileInputStream`對象內容的位元組陣列。 您可以使用`available`方法來取得`java.io.FileInputStream`物件的大小，以判斷位元組陣列的大小。
   * 調用`java.io.FileInputStream`物件的`read`方法並傳遞位元組陣列，以串流資料填入位元組陣列。
   * 調用`setBinaryData`方法並傳遞位元組陣列，以填充`BLOB`對象。

1. 依值演算表格

   叫用`FormsService`物件的`renderPDFForm`方法並傳遞下列值：

   * 空字串值。 （通常，此參數需要一個字串值，它指定表單設計的名稱。）
   * 包含表單設計的`BLOB`物件。 通常，此參數值會保留給與表單合併的資料。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。 此為可選參數，如果您不想指定執行時選項，可以指定`null`。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`對象。 這可用來儲存轉譯的PDF表單。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`對象。 （此引數會儲存表單中的頁數。）
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`對象。 （此引數儲存地區值。）
   * 空的`com.adobe.idp.services.holders.FormsResultHolder`對象，將包含此操作的結果。

   `renderPDFForm`方法會以必須寫入用戶端網頁瀏覽器的表單資料流填入作為最後一個參數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 獲取`com.adobe.idp.services.holders.FormsResultHolder`對象`value`資料成員的值，建立`FormResult`對象。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 通過調用`getContentType`方法獲取`BLOB`對象的內容類型。
   * 調用`setContentType`方法並傳遞`BLOB`物件的內容類型，以設定`javax.servlet.http.HttpServletResponse`物件的內容類型。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立`javax.servlet.ServletOutputStream`物件，用來將表單資料串流寫入用戶端Web瀏覽器。
   * 建立位元組陣列，並呼叫`BLOB`物件的`getBinaryData`方法以填入它。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**另請參閱**

[按價值呈現Forms](#rendering-forms-by-value)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
