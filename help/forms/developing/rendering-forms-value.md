---
title: 按價值呈現Forms
seo-title: Rendering Forms By Value
description: 使用FormsAPI(Java)使用Java API和Web服務API按值呈現表單。
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

# 按價值呈現Forms {#rendering-forms-by-value}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

通常，在設計器中建立的表單設計會參照Forms服務傳遞。 表單設計可以是大的，因此，通過引用來傳遞它們更有效，以避免必須按值封送表單設計位元組。 Forms服務還可以快取表單設計，這樣在快取時，它就不必持續讀取表單設計。

如果表單設計包含UUID屬性，則會快取該屬性。 UUID值對於所有表單設計都是唯一的，用於唯一標識表單。 按值呈現表單時，只有在表單重複使用時才應快取它。 但是，如果表單未重複使用且必須唯一，則可以使用使用AEM FormsAPI設定的快取選項來避免快取表單。

Forms服務還可以解析表單設計中連結內容的位置。 例如，從表單設計中引用的連結影像是相對URL。 連結的內容始終被假定為與窗體設計位置相關。 因此，解析連結內容是通過將相對路徑應用到絕對表單設計位置來確定其位置的問題。

可以按值傳遞窗體設計，而不是通過參照傳遞窗體設計。 動態建立表單設計時，按值傳遞表單設計是有效的；即，當客戶端應用程式在運行時生成建立表單設計的XML時。 在這種情況下，表單設計不會儲存在物理儲存庫中，因為它儲存在記憶體中。 在運行時動態建立表單設計並按值傳遞時，您可以快取表單並提高Forms服務的效能。

**按值傳遞表單的限制**

按值傳遞表單設計時，會應用以下限制：

* 表單設計中不能包含任何相關連結內容。 所有影像和片段必須嵌入到表單設計中，或者必須完全引用。
* 在呈現表單後無法執行伺服器端計算。 如果表單被提交回Forms服務，則資料將被提取並返回，而不需要任何伺服器端計算。
* 由於HTML只能在運行時使用連結的影像，因此無法生成嵌入影像的HTML。 這是因為Forms服務通過從引用的表單設計中檢索影像而支援具有HTML的嵌入影像。 由於按值傳遞的表單設計沒有引用的位置，因此當顯示HTML頁時無法提取嵌入的影像。 因此，影像引用必須是要在HTML中渲染的絕對路徑。

>[!NOTE]
>
>雖然您可以按值呈現不同類型的表單(例如，包含使用權限的HTML表單或表單)，但本節將討論呈現互動式PDF forms。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

要按值呈現表單，請執行以下步驟：

1. 包括項目檔案。
1. 建立Forms客戶端API對象。
1. 參考窗體設計。
1. 按值呈現窗體。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Forms客戶端API對象**

在以寫程式方式將資料導入PDF表單Client API之前，必須建立Data Integration服務客戶端。 建立服務客戶端時，定義調用服務所需的連接設定。

**參考窗體設計**

按值呈現表單時，必須建立 `com.adobe.idp.Document` 包含要呈現的窗體設計的對象。 您可以引用現有XDP檔案，也可以在運行時動態建立窗體設計並填充 `com.adobe.idp.Document` 資料。

>[!NOTE]
>
>本節和相應的快速啟動引用現有XDP檔案。

**按值呈現窗體**

要按值呈現表單，請傳遞 `com.adobe.idp.Document` 包含呈現方法的窗體設計的實例 `inDataDoc` 參數(可以是 `FormsServiceClient` 對象的呈現方法，如 `renderPDFForm`。 `(Deprecated) renderHTMLForm`等)。 此參數值通常保留給與表單合併的資料。 同樣，將空字串值傳遞給 `formQuery` 的下界。 通常，此參數需要一個字串值來指定窗體設計的名稱。

>[!NOTE]
>
>如果要在表單中顯示資料，則必須在 `xfa:datasets` 的子菜單。 有關XFA體系結構的資訊，請轉至 [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf)。

**將表單資料流寫入客戶端Web瀏覽器**

當Forms服務按值呈現表單時，它將返回您必須寫入客戶端Web瀏覽器的表單資料流。 當寫入客戶端Web瀏覽器時，該表單對用戶可見。

**另請參閱**

[使用Java API按值呈現表單](#render-a-form-by-value-using-the-java-api)

[使用Web服務API按值呈現表單](#render-a-form-by-value-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案轉給Forms](/help/forms/developing/passing-documents-forms-service.md)

[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API按值呈現表單 {#render-a-form-by-value-using-the-java-api}

使用FormsAPI(Java)按值呈現表單：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。

1. 建立Forms客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 參考窗體設計

   * 建立 `java.io.FileInputStream` 表示要呈現的窗體設計的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定XDP檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 按值呈現窗體

   調用 `FormsServiceClient` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 空字串值。 （通常，此參數需要一個字串值來指定窗體設計的名稱。）
   * A `com.adobe.idp.Document` 包含窗體設計的對象。 通常，此參數值是為與表單合併的資料保留的。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 這是可選參數，您可以指定 `null` 選項。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。

   的 `renderPDFForm` 方法返回 `FormsResult` 包含可寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `com.adobe.idp.Document` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `com.adobe.idp.Document` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
   * 建立位元組陣列並分配 `InputStream` 的雙曲餘切值。 調用 `InputStream` 對象 `available` 獲取 `InputStream` 的雙曲餘切值。
   * 通過調用 `InputStream` 對象 `read`方法，並將位元組陣列作為參數傳遞。
   * 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[按價值呈現Forms](/help/forms/developing/rendering-forms.md)

[快速啟動（SOAP模式）:使用Java API按值呈現](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API按值呈現表單 {#render-a-form-by-value-using-the-web-service-api}

使用FormsAPI（Web服務）按值呈現表單：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包括到類路徑中。

1. 建立Forms客戶端API對象

   建立 `FormsService` 對象和設定驗證值。

1. 參考窗體設計

   * 建立 `java.io.FileInputStream` 對象。 傳遞一個指定XDP檔案位置的字串值。
   * 建立 `BLOB` 對象。 的 `BLOB` object用於儲存使用密碼加密的PDF文檔。
   * 建立一個位元組陣列，用於儲存 `java.io.FileInputStream` 的雙曲餘切值。 通過獲取 `java.io.FileInputStream` 對象的大小 `available` 的雙曲餘切值。
   * 通過調用 `java.io.FileInputStream` 對象 `read` 和傳遞位元組陣列。
   * 填充 `BLOB` 通過調用對象 `setBinaryData` 和傳遞位元組陣列。

1. 按值呈現窗體

   調用 `FormsService` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 空字串值。 （通常，此參數需要一個字串值來指定窗體設計的名稱。）
   * A `BLOB` 包含窗體設計的對象。 通常，此參數值是為與表單合併的資料保留的。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 這是可選參數，您可以指定 `null` 選項。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的對象。 這用於儲存渲染的PDF窗體。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的對象。 （此參數儲存表單中的頁數。）
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的對象。 （此參數儲存區域設定值。）
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作結果的對象。

   的 `renderPDFForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個參數值傳遞的對象，其表單資料流必須寫入客戶端web瀏覽器。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `FormResult` 通過獲取 `com.adobe.idp.services.holders.FormsResultHolder` 對象 `value` 資料成員。
   * 建立 `BLOB` 通過調用包含表單資料的對象 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `BLOB` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `BLOB` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立位元組陣列，並通過調用 `BLOB` 對象 `getBinaryData` 的雙曲餘切值。 此任務分配 `FormsResult` 對象。
   * 調用 `javax.servlet.http.HttpServletResponse` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[按價值呈現Forms](#rendering-forms-by-value)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
