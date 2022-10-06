---
title: 依值呈現Forms
seo-title: Rendering Forms By Value
description: 使用Forms API(Java)，透過Java API和網站服務API來依值轉譯表單。
seo-description: Use the Forms API (Java) to render a form by value using the Java API and Web Service API.
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 0%

---

# 依值呈現Forms {#rendering-forms-by-value}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

通常，在Designer中建立的表單設計會參照Forms服務而傳遞。 表單設計可能很大，因此，參照傳遞這些設計會更有效率，以避免必須依值匯整表單設計位元組。 Forms服務也可以快取表單設計，這樣在快取時，就不需要持續讀取表單設計。

如果表單設計包含UUID屬性，則會快取該屬性。 UUID值對於所有表單設計都是唯一的，可用來唯一識別表單。 依值轉譯表單時，只有在重複使用表單時，才應快取該表單。 不過，如果表單未重複使用且必須是唯一的，則可使用使用AEM Forms API設定的快取選項，來避免快取表單。

Forms服務也可以解析連結內容在表單設計中的位置。 例如，從表單設計內參照的連結影像為相對URL。 連結的內容一律視為相對於表單設計位置。 因此，通過將相對路徑應用於絕對表單設計位置來確定連結內容的位置是一個問題。

您可以按值傳遞表單設計，而不是通過參照傳遞表單設計。 動態建立表單設計時，依值傳遞表單設計會很有效率；也就是說，當客戶端應用程式生成在運行時建立表單設計的XML時。 在這種情況下，表單設計不會儲存在物理儲存庫中，因為它儲存在記憶體中。 在執行階段以動態方式建立表單設計並依值傳遞時，您可以快取表單並改善Forms服務的效能。

**依值傳遞表單的限制**

表單設計依值傳遞時，會套用下列限制：

* 表單設計內不能有相對連結的內容。 所有影像和片段必須內嵌在表單設計中，或絕對參照。
* 轉譯表單後，就無法執行伺服器端計算。 如果表單已提交回Forms服務，則會擷取資料並加以傳回，而不需進行任何伺服器端計算。
* 由於HTML在執行時只能使用連結的影像，因此無法產生含有內嵌影像的HTML。 這是因為Forms服務可從參考的表單設計擷取影像，以支援內嵌具有HTML的影像。 由於按值傳遞的表單設計沒有參考的位置，因此在顯示HTML頁面時無法擷取內嵌影像。 因此，影像參照必須是絕對路徑，才能以HTML呈現。

>[!NOTE]
>
>雖然您可以依值呈現不同類型的表單(例如，包含使用權限的HTML表單或表單)，但本節會討論轉譯互動式PDF forms。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步驟摘要 {#summary-of-steps}

要按值呈現表單，請執行以下步驟：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 參考表單設計。
1. 按值呈現表單。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms用戶端API物件**

您必須先建立資料整合服務用戶端，才能以程式設計方式將資料匯入PDF表單用戶端API。 建立服務客戶端時，您定義調用服務所需的連接設定。

**參考表單設計**

依值呈現表單時，您必須建立 `com.adobe.idp.Document` 包含要呈現的表單設計的對象。 您可以參考現有的XDP檔案，或在執行階段以動態方式建立表單設計並填入 `com.adobe.idp.Document` 資料。

>[!NOTE]
>
>本節和對應的快速入門參考現有的XDP檔案。

**按值呈現表單**

若要依值呈現表單，請傳遞 `com.adobe.idp.Document` 包含表單設計到呈現方法的 `inDataDoc` 參數(可以是 `FormsServiceClient` 物件的呈現方法，例如 `renderPDFForm`, `(Deprecated) renderHTMLForm`等)。 此參數值通常會為與表單合併的資料保留。 同樣地，將空字串值傳遞至 `formQuery` 參數。 通常，此參數需要一個字串值，該字串值指定表單設計的名稱。

>[!NOTE]
>
>如果您想在表單中顯示資料，必須在 `xfa:datasets` 元素。 如需XFA架構的相關資訊，請前往 [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**將表單資料流寫入客戶端Web瀏覽器**

Forms服務依值轉譯表單時，會傳回您必須寫入用戶端網頁瀏覽器的表單資料流。 寫入客戶端Web瀏覽器時，用戶可以看到該表單。

**另請參閱**

[使用Java API依值呈現表單](#render-a-form-by-value-using-the-java-api)

[使用網站服務API依值呈現表單](#render-a-form-by-value-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

[建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API依值呈現表單 {#render-a-form-by-value-using-the-java-api}

使用Forms API(Java)依值轉譯表單：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 參考表單設計

   * 建立 `java.io.FileInputStream` 表示要呈現的表單設計的物件，方法是使用其建構子並傳遞指定XDP檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 按值呈現表單

   叫用 `FormsServiceClient` 物件 `renderPDFForm` 方法，並傳遞下列值：

   * 空字串值。 （通常，此參數需要一個字串值，該字串值指定表單設計的名稱。）
   * A `com.adobe.idp.Document` 包含表單設計的物件。 通常，此參數值會保留給與表單合併的資料。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 這是選用參數，您可以指定 `null` 如果您不想指定執行時選項。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 這是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含可寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 對象，方法是調用 `FormsResult` 物件s `getOutputContent` 方法。
   * 取得 `com.adobe.idp.Document` 對象 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 對象的內容類型，方法是調用 `setContentType` 方法，並傳遞 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 物件 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 對象，方法是調用 `com.adobe.idp.Document` 物件 `getInputStream` 方法。
   * 建立位元組陣列，並分配 `InputStream` 物件。 叫用 `InputStream` 物件 `available` 取得 `InputStream` 物件。
   * 叫用 `InputStream` 物件 `read`方法，並將位元組陣列傳遞為引數。
   * 叫用 `javax.servlet.ServletOutputStream` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[依值呈現Forms](/help/forms/developing/rendering-forms.md)

[快速入門（SOAP模式）:使用Java API根據值呈現](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API依值呈現表單 {#render-a-form-by-value-using-the-web-service-api}

使用Forms API（網站服務），依值轉譯表單：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立 `FormsService` 對象和設定驗證值。

1. 參考表單設計

   * 建立 `java.io.FileInputStream` 物件，使用其建構子。 傳遞指定XDP檔案位置的字串值。
   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存使用密碼加密的PDF文檔。
   * 建立位元組陣列，用於儲存 `java.io.FileInputStream` 物件。 您可以取得 `java.io.FileInputStream` 對象的大小(使用 `available` 方法。
   * 叫用 `java.io.FileInputStream` 物件 `read` 方法，並傳遞位元組陣列。
   * 填入 `BLOB` 對象 `setBinaryData` 方法，並傳遞位元組陣列。

1. 按值呈現表單

   叫用 `FormsService` 物件 `renderPDFForm` 方法，並傳遞下列值：

   * 空字串值。 （通常，此參數需要一個字串值，該字串值指定表單設計的名稱。）
   * A `BLOB` 包含表單設計的物件。 通常，此參數值會保留給與表單合併的資料。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 這是選用參數，您可以指定 `null` 如果您不想指定執行時選項。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 這是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 由方法填入的物件。 這可用來儲存呈現的PDF表單。
   * 空白 `javax.xml.rpc.holders.LongHolder` 由方法填入的物件。 （此引數會儲存表單中的頁數。）
   * 空白 `javax.xml.rpc.holders.StringHolder` 由方法填入的物件。 （此參數儲存地區設定值。）
   * 空白 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作結果的對象。

   此 `renderPDFForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個引數值傳遞的物件，具有必須寫入用戶端網頁瀏覽器的表單資料流。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `FormResult` 物件，方法是取得 `com.adobe.idp.services.holders.FormsResultHolder` 物件 `value` 資料成員。
   * 建立 `BLOB` 包含表單資料的物件，方法是叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得 `BLOB` 對象 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 對象的內容類型，方法是調用 `setContentType` 方法，並傳遞 `BLOB` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 物件 `getOutputStream` 方法。
   * 建立位元組陣列，並叫用 `BLOB` 物件 `getBinaryData` 方法。 此任務分配 `FormsResult` 位元組陣列的物件。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[依值呈現Forms](#rendering-forms-by-value)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
