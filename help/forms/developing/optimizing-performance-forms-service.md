---
title: 優化Forms服務的效能
seo-title: Optimizing the Performance of theForms Service
description: 在呈現表單時設定運行時選項，並將XDP檔案儲存在儲存庫中，以優化Forms服務的效能。
seo-description: Set run-time options when rendering a form and store XDP files in the repository to optimize the performance of the Forms service.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 0%

---

# 優化Forms服務的效能 {#optimizing-the-performance-of-theforms-service}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

## 優化Forms服務的效能 {#optimizing-the-performance-of-the-forms-service}

在呈現表單時，可以設定運行時選項，以優化Forms服務的效能。 您可以執行的另一個任務是將XDP檔案儲存在儲存庫中，以提高Forms服務的效能。 但是，本節沒有說明如何執行此任務。 (請參閱 [使用Java客戶端庫調用服務](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)。)

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要在呈現表單時優化Forms服務的效能，請執行以下任務：

1. 包括項目檔案。
1. 建立Forms客戶端API對象。
1. 設定效能運行時選項。
1. 呈現窗體。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Forms客戶端API對象**

在以寫程式方式執行Forms服務客戶端API操作之前，必須建立Forms服務客戶端。 如果使用Java API，請建立 `FormsServiceClient` 的雙曲餘切值。 如果使用FormsWeb服務API，請建立 `FormsService` 的雙曲餘切值。

**設定效能運行時選項**

您可以設定以下效能運行時選項以改進Forms服務的效能：

* **表單快取**:您可以快取在伺服器快取中呈現為PDF的表單。 每個表單在首次生成後被快取。 在隨後的呈現中，如果快取的表單比表單設計的時間戳新，則從快取中檢索表單。 通過快取表單，可以提高Forms服務的效能，因為它不必從儲存庫檢索表單設計。
* 表單參考線（已棄用）的呈現時間可能比其他轉換類型長。 建議您快取表單指南（不建議使用）以提高效能。
* **獨立選項**:如果不要求Forms服務執行伺服器端計算，可以將「獨立」選項設定為 `true`，導致在沒有狀態資訊的情況下呈現表單。 如果要向最終用戶呈現互動式表單，而最終用戶隨後將資訊輸入表單並將表單提交回Forms服務，則需要狀態資訊。 然後，Forms服務執行計算操作，並將表單呈現回用戶，結果以表單顯示。 如果將沒有狀態資訊的表單提交回Forms服務，則只有XML資料可用，且不執行伺服器端計算。
* **線性化PDF**:組織線性化的PDF檔案以在網路環境中實現有效的增量訪問。 該PDF檔案在所有方面都是有效的PDF，並且與所有現有查看器和其他PDF應用程式相容。 即，可以在下載線性化的PDF時查看它。
* 在客戶端上呈現PDF表單時，此選項不會提高效能。
* **GuideRSL選項**:啟用使用運行時共用庫生成表單指南（已棄用）。 這意味著第一個請求將下載較小的SWF檔案，以及儲存在瀏覽器快取中的較大的共用庫。 有關詳細資訊，請參閱Flex文檔中的RSL。
* 您還可以通過在客戶端上生成表單來改進Forms服務的效能。 (請參閱 [在客戶端呈現Forms](/help/forms/developing/rendering-forms-client.md)。)

**呈現窗體**

要在設定效能選項後呈現表單，請使用與呈現不帶效能選項的表單相同的應用程式邏輯。

**將表單資料流寫入客戶端Web瀏覽器**

Forms服務呈現表單後，它將返回必須寫入客戶端Web瀏覽器的表單資料流。 當寫入客戶端Web瀏覽器時，該表單對用戶可見。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[讓Forms成為HTML](/help/forms/developing/rendering-forms-html.md)

[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API優化效能 {#optimize-the-performance-using-the-java-api}

使用FormsAPI(Java)呈現具有優化效能的表單：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。

1. 建立Forms客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 設定效能運行時選項

   * 建立 `PDFFormRenderSpec` 對象。
   * 通過調用 `PDFFormRenderSpec` 對象 `setCacheEnabled` 方法 `true`。
   * 通過調用 `PDFFormRenderSpec` 對象 `setLinearizedPDF` 方法 `true.`

1. 呈現窗體

   調用 `FormsServiceClient` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。
   * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞一個空 `com.adobe.idp.Document` 的雙曲餘切值。
   * A `PDFFormRenderSpec` 用於儲存運行時選項以提高效能的對象。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。

   的 `renderPDFForm` 方法返回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `javax.servlet.ServletOutputStream` 用於將表單資料流發送到客戶端web瀏覽器的對象。
   * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
   * 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
   * 通過調用 `InputStream` 對象 `read`方法，並將位元組陣列作為參數傳遞。
   * 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API優化效能](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API優化效能 {#optimize-the-performance-using-the-web-service-api}

使用FormsAPI（Web服務）呈現具有優化效能的表單：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包括到類路徑中。

1. 建立Forms客戶端API對象

   建立 `FormsService` 對象和設定驗證值。

1. 設定效能運行時選項

   * 建立 `PDFFormRenderSpec` 對象。
   * 通過調用 `PDFFormRenderSpec` 對象 `setCacheEnabled` 方法和傳遞true。
   * 通過調用 `PDFFormRenderSpec` 對象 `setStandAlone` 方法和傳遞true。
   * 通過調用 `PDFFormRenderSpec` 對象 `setLinearizedPDF` 方法和傳遞true。

1. 呈現窗體

   調用 `FormsService` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。
   * A `BLOB` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞 `null`。
   * A `PDFFormRenderSpecc` 儲存運行時選項的對象。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的對象。 這用於儲存渲染的PDF窗體。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的對象。 （此參數將儲存表單中的頁數）。
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的對象。 （此參數將儲存區域設定值）。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作結果的對象。

   的 `renderPDFForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個參數值傳遞的對象，其表單資料流必須寫入客戶端web瀏覽器。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `FormResult` 通過獲取 `com.adobe.idp.services.holders.FormsResultHolder` 對象 `value` 資料成員。
   * 建立 `javax.servlet.ServletOutputStream` 用於將表單資料流發送到客戶端web瀏覽器的對象。
   * 建立 `BLOB` 通過調用包含表單資料的對象 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
   * 建立位元組陣列，並通過調用 `BLOB` 對象 `getBinaryData` 的雙曲餘切值。 此任務分配 `FormsResult` 對象。
   * 調用 `javax.servlet.http.HttpServletResponse` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
