---
title: 基於片段呈現Forms
seo-title: Rendering Forms Based on Fragments
description: 使用Forms服務可呈現基於使用設計器建立的片段的表單。
seo-description: Use the Forms service to render forms that are based on fragments created using Designer.
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
role: Developer
exl-id: febf5350-3fc5-48c0-8bc5-198daff15936
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 0%

---

# 基於片段呈現Forms {#rendering-forms-based-on-fragments}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

## 基於片段呈現Forms {#rendering-forms-based-on-fragments-inner}

Forms服務可以基於您使用設計器建立的片段來呈現表單。 A *片段* 是表單的可重用部分，並另存為可插入到多個表單設計中的獨立XDP檔案。 例如，片段可以包括地址塊或合法文本。

使用碎片簡化並加快了大量形式的建立和維護。 建立新窗體時，將插入對所需片段的引用，該片段將出現在窗體中。 片段引用包含指向物理XDP檔案的子窗體。 有關基於片段建立表單設計的資訊，請參見 [Forms設計師](https://www.adobe.com/go/learn_aemforms_designer_63_tw)

片段可以包括多個子形式，這些子形式被包裝在選擇子形式集中。 選擇子表單集基於來自資料連接的資料流控制子表單的顯示。 您可以使用條件語句來確定集合中的子窗體出現在傳遞的窗體中。 例如，集合中的每個子表單可以包括特定地理位置的資訊，並且可以基於用戶的位置來確定所顯示的子表單。

A *指令碼片段* 包含可重用的JavaScript函式或值，這些函式或值與任何特定對象（如日期分析器或Web服務調用）分開儲存。 這些片段包括一個指令碼對象，該對象在「層次」元件面板中顯示為變數的子項。 無法從其他對象的屬性（如驗證、計算或初始化等事件指令碼）的指令碼建立片段。

以下是使用碎片的優勢：

* **內容重用**:可以使用片段在多個窗體設計中重用內容。 當您需要在多個表單中使用某些相同的內容時，使用片段比複製或重新建立內容更快、更簡單。 使用片段還確保表單設計中經常使用的部分在所有引用表單中具有一致的內容和外觀。
* **全局更新**:您可以使用片段在一個檔案中僅對多個表單進行一次全局更改。 您可以更改片段中的內容、指令碼對象、資料綁定、佈局或樣式，引用該片段的所有XDP表單都將反映更改。
* 例如，許多表單中的公用元素可能是地址塊，其中包含國家/地區的下拉清單對象。 如果需要更新下拉清單對象的值，必須開啟許多表單才能進行更改。 如果將地址塊包括在片段中，則只需開啟一個片段檔案即可進行更改。
* 要更新PDF窗體中的片段，必須在設計器中重新保存窗體。
* **共用表單建立**:可以使用片段在多個資源之間共用表單的建立。 具有指令碼編寫專業知識或其他高級功能的表單開發人員可以開發和共用利用指令碼和動態屬性的片段。 表單設計人員可以使用這些片段來佈局表單設計，並確保表單的所有部分在由多人設計的多個表單上具有一致的外觀和功能。

### 用碎片裝配的形狀設計 {#assembling-a-form-design-assembled-using-fragments}

您可以基於多個碎片將表單設計裝配到Forms服務。 要匯集多個片段，請使用匯編器服務。 要查看使用Assemble服務建立由其他Forms服務（Output服務）使用的窗體設計的示例，請參見 [使用片段建立PDF文檔](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)。 您可以使用Forms服務執行相同的工作流，而不是使用輸出服務。

使用匯編器服務時，您正在傳遞使用片段裝配的表單設計。 建立的窗體設計不引用其他片段。 相比之下，本主題討論的是通過表格設計，將其他片段引入Forms服務。 但是，表單設計不是由匯編器裝配的。 它是在設計器中建立的。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關建立基於Web的應用程式以基於片段呈現表單的資訊，請參見 [建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)。

### 步驟摘要 {#summary-of-steps}

要基於片段呈現表單，請執行以下任務：

1. 包括項目檔案。
1. 建立Forms客戶端API對象。
1. 指定URI值。
1. 呈現窗體。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Forms客戶端API對象**

在以寫程式方式執行Forms服務客戶端API操作之前，必須建立Forms服務客戶端。

**指定URI值**

要成功呈現基於片段的表單，必須確保Forms服務能夠找到表單設計引用的表單和片段（XDP檔案）。 例如，假定表單名為PO.xdp，並且此表單使用兩個名為FooterUS.xdp和FooterCanada.xdp的片段。 在這種情況下，Forms服務必須能夠找到所有三個XDP檔案。

通過將表單放置在一個位置，將片段放置在另一個位置，可以組織表單及其片段，或將所有XDP檔案放置在同一位置。 在本節中，假定所有XDP檔案都位於AEM Forms儲存庫中。 有關將XDP檔案放在AEM Forms儲存庫中的資訊，請參見 [編寫資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。

在基於片段呈現表單時，必須僅引用表單本身，而不是片段。 例如，必須引用PO.xdp，而不是FooterUS.xdp或FooterCanada.xdp。 確保將碎片放置在Forms服務可以找到它們的位置。

**呈現窗體**

基於片段的表單可以以與非碎片表單相同的方式呈現。 也就是說，您可以將表單渲染為「PDF」、「HTML」或「表單參考線」（不建議使用）。 本節中的示例將基於片段的表單渲染為互動式PDF表單。 (請參閱 [呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)。)

**將表單資料流寫入客戶端Web瀏覽器**

當Forms服務呈現表單時，它將返回必須寫入客戶端Web瀏覽器的表單資料流。 當寫入客戶端Web瀏覽器時，該表單對用戶可見。

**另請參閱**

[使用Java API基於片段呈現表單](#render-forms-based-on-fragments-using-the-java-api)

[使用Web服務API基於片段呈現表單](#render-forms-based-on-fragments-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API基於片段呈現表單 {#render-forms-based-on-fragments-using-the-java-api}

使用FormsAPI(Java)基於片段呈現表單：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。

1. 建立Forms客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 指定URI值

   * 建立 `URLSpec` 使用其建構子儲存URI值的對象。
   * 調用 `URLSpec` 對象 `setApplicationWebRoot` 方法，並傳遞一個表示應用程式web根的字串值。
   * 調用 `URLSpec` 對象 `setContentRootURI` 方法並傳遞一個字串值，該字串值指定內容根URI值。 確保表單設計和片段位於內容根URI中。 否則，Forms服務會引發異常。 要引用儲存庫，請指定 `repository://`。
   * 調用 `URLSpec` 對象 `setTargetURL` 方法並傳遞一個字串值，該字串值指定將表單資料發佈到的目標URL值。 如果在表單設計中定義目標URL，則可以傳遞空字串。 您還可以指定表單發送到的URL以執行計算。

1. 呈現窗體

   調用 `FormsServiceClient` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞一個空 `com.adobe.idp.Document` 的雙曲餘切值。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。
   * A `URLSpec` 包含Forms服務基於片段呈現表單所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。

   的 `renderPDFForm` 方法返回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `com.adobe.idp.Document` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `com.adobe.idp.Document` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
   * 通過調用 `InputStream` 對象 `read`方法，並將位元組陣列作為參數傳遞。
   * 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[基於片段呈現Forms](#rendering-forms-based-on-fragments)

[快速啟動（SOAP模式）:使用Java API基於片段呈現表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API基於片段呈現表單 {#render-forms-based-on-fragments-using-the-web-service-api}

使用FormsAPI（Web服務）基於片段呈現表單：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包括到類路徑中。

1. 建立Forms客戶端API對象

   建立 `FormsService` 對象和設定驗證值。

1. 指定URI值

   * 建立 `URLSpec` 使用其建構子儲存URI值的對象。
   * 調用 `URLSpec` 對象 `setApplicationWebRoot` 方法，並傳遞一個表示應用程式web根的字串值。
   * 調用 `URLSpec` 對象 `setContentRootURI` 方法並傳遞一個字串值，該字串值指定內容根URI值。 確保表單設計位於內容根URI中。 否則，Forms服務會引發異常。 要引用儲存庫，請指定 `repository://`。
   * 調用 `URLSpec` 對象 `setTargetURL` 方法並傳遞一個字串值，該字串值指定將表單資料發佈到的目標URL值。 如果在表單設計中定義目標URL，則可以傳遞空字串。 您還可以指定表單發送到的URL以執行計算。

1. 呈現窗體

   調用 `FormsService` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `BLOB` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞 `null`。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 請注意，如果輸入文檔是PDF文檔，則無法設定標籤PDF選項。 如果輸入檔案是XDP檔案，則可以設定標籤PDF選項。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的對象。 此參數用於儲存渲染的表單。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的對象。 此參數將儲存窗體中的頁數。
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的對象。 此參數將儲存區域設定值。
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

[基於片段呈現Forms](#rendering-forms-based-on-fragments)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
