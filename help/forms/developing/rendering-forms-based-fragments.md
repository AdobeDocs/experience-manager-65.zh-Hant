---
title: 根據片段轉譯Forms
seo-title: Rendering Forms Based on Fragments
description: 使用Forms服務來轉譯以Designer所建立片段為基礎的表單。
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

# 根據片段轉譯Forms {#rendering-forms-based-on-fragments}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 根據片段轉譯Forms {#rendering-forms-based-on-fragments-inner}

Forms服務可呈現以您使用Designer建立之片段為基礎的表單。 A *片段* 是表單的可重複使用部分，並儲存為可插入到多個表單設計中的個別XDP檔案。 例如，片段可以包含地址塊或法律文字。

使用片段可簡化及加速大量表單的建立與維護作業。 建立新表單時，您會插入對所需片段的參考，片段會出現在表單中。 片段參考包含指向物理XDP檔案的子表單。 如需根據片段建立表單設計的相關資訊，請參閱 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

片段可以包括包裝在選擇子表單集中的多個子表單。 選擇子表單集基於來自資料連接的資料流控制子表單的顯示。 您可以使用條件陳述式來判斷傳送的表單中，會出現集內的子表單。 例如，集合中的每個子表單可以包括特定地理位置的資訊，並且可以根據用戶的位置確定顯示的子表單。

A *指令碼片段* 包含可重複使用的JavaScript函式或值，這些函式或值與任何特定對象（如日期解析器或Web服務調用）分開儲存。 這些片段包含單一指令碼物件，在階層浮動視窗中顯示為變數的子項。 無法從屬於其他物件屬性的指令碼建立片段，例如驗證、計算或初始化等事件指令碼。

以下是使用片段的優點：

* **內容重複使用**:您可以使用片段來重複使用多個表單設計中的內容。 當您需要在多個表單中使用某些相同內容時，使用片段比複製或重新建立內容更快更簡單。 使用片段也可確保經常使用的表單設計部分在所有參考表單中具有一致的內容和外觀。
* **全域更新**:您只能在一個檔案中使用片段對多個表單進行一次全域變更。 您可以變更片段中的內容、指令碼物件、資料系結、版面或樣式，而所有參考片段的XDP表單將反映變更。
* 例如，許多表單中的通用元素可能是地址塊，其中包含國家/地區的下拉式清單物件。 如果需要更新下拉式清單物件的值，您必須開啟許多表單才能進行變更。 如果您將地址塊包含在片段中，則只需開啟一個片段檔案即可進行變更。
* 若要更新PDF表單中的片段，您必須在Designer中重新儲存表單。
* **共用表單建立**:您可以使用片段，在多個資源間共用表單的建立作業。 具備指令碼或其他Designer進階功能的表單開發人員可開發及共用片段，以運用指令碼和動態屬性。 表單設計人員可以使用這些片段來設計表單設計，並確保表單的所有部分在由多人設計的多個表單中具有一致的外觀和功能。

### 裝配使用碎片裝配的表單設計 {#assembling-a-form-design-assembled-using-fragments}

您可以根據多個片段組合表單設計以傳遞至Forms服務。 要組合多個片段，請使用組合器服務。 若要查看使用Assemble服務建立供其他Forms服務（輸出服務）使用的表單設計的範例，請參閱 [使用片段建立PDF檔案](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). 您可以使用Forms服務來執行相同的工作流程，而不使用輸出服務。

使用組合器服務時，您正在傳遞使用片段組合的表單設計。 建立的表單設計不會參考其他片段。 相反地，本主題探討如何將參考其他片段的表單設計傳遞至Forms服務。 但是，表單設計不是由組合器裝配的。 是在Designer中建立的。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>如需建立以網頁為基礎的應用程式，以根據片段轉譯表單的相關資訊，請參閱 [建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md).

### 步驟摘要 {#summary-of-steps}

若要根據片段轉譯表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 指定URI值。
1. 轉譯表單。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API作業。

**指定URI值**

若要根據片段成功轉譯表單，您必須確定Forms服務可以找到表單設計所參考的表單和片段（XDP檔案）。 例如，假設表單名為PO.xdp，且此表單使用名為FooterUS.xdp和FooterCanada.xdp的兩個片段。 在此情況下，Forms服務必須能夠找到所有三個XDP檔案。

您可以將表單放在一個位置，並將片段放在另一個位置，借此組織表單及其片段，或將所有XDP檔案放在相同位置。 就本節而言，假設所有XDP檔案都位於AEM Forms存放庫。 如需將XDP檔案放入AEM Forms存放庫的相關資訊，請參閱 [編寫資源](/help/forms/developing/aem-forms-repository.md#writing-resources).

根據片段轉譯表單時，您只能參考表單本身，不能參考片段。 例如，您必須參考PO.xdp，而非FooterUS.xdp或FooterCanada.xdp。 請確定您將片段放置在Forms服務可找到的位置。

**轉譯表單**

基於片段的表單可以與非碎片表單相同的方式呈現。 也就是說，您可以將表單轉譯為「PDF」、「HTML」或「表單指南」（已廢止）。 本節中的範例會根據片段轉譯表單，作為互動式PDF表單。 (請參閱 [轉譯互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**將表單資料流寫入客戶端Web瀏覽器**

Forms服務轉譯表單時，會傳回您必須寫入用戶端網頁瀏覽器的表單資料流。 寫入客戶端Web瀏覽器時，用戶可以看到該表單。

**另請參閱**

[使用Java API根據片段呈現表單](#render-forms-based-on-fragments-using-the-java-api)

[使用網站服務API根據片段轉譯表單](#render-forms-based-on-fragments-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉譯互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API根據片段呈現表單 {#render-forms-based-on-fragments-using-the-java-api}

使用Forms API(Java)根據片段轉譯表單：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 指定URI值

   * 建立 `URLSpec` 使用其建構子儲存URI值的物件。
   * 叫用 `URLSpec` 物件 `setApplicationWebRoot` 方法，並傳遞代表應用程式網頁根的字串值。
   * 叫用 `URLSpec` 物件 `setContentRootURI` 方法，並傳遞指定內容根URI值的字串值。 請確定表單設計和片段位於內容根URI中。 否則，Forms服務會擲回例外狀況。 要引用儲存庫，請指定 `repository://`.
   * 叫用 `URLSpec` 物件 `setTargetURL` 方法，並傳遞字串值，指定表單資料張貼到的目標URL值。 如果您在表單設計中定義目標URL，則可以傳遞空字串。 您也可以指定表單要傳送到哪個URL，以執行計算。

1. 轉譯表單

   叫用 `FormsServiceClient` 物件 `renderPDFForm` 方法，並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` 包含要與表單合併資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。
   * A `URLSpec` 包含Forms服務根據片段轉譯表單所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 這是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 對象，方法是調用 `FormsResult` 物件s `getOutputContent` 方法。
   * 取得 `com.adobe.idp.Document` 對象 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 對象的內容類型，方法是調用 `setContentType` 方法，並傳遞 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 物件 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 對象，方法是調用 `com.adobe.idp.Document` 物件 `getInputStream` 方法。
   * 叫用 `InputStream` 物件 `read`方法，並將位元組陣列傳遞為引數。
   * 叫用 `javax.servlet.ServletOutputStream` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[根據片段轉譯Forms](#rendering-forms-based-on-fragments)

[快速入門（SOAP模式）:使用Java API根據片段轉譯表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API根據片段轉譯表單 {#render-forms-based-on-fragments-using-the-web-service-api}

使用Forms API（網站服務）根據片段轉譯表單：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立 `FormsService` 對象和設定驗證值。

1. 指定URI值

   * 建立 `URLSpec` 使用其建構子儲存URI值的物件。
   * 叫用 `URLSpec` 物件 `setApplicationWebRoot` 方法，並傳遞代表應用程式網頁根的字串值。
   * 叫用 `URLSpec` 物件 `setContentRootURI` 方法，並傳遞指定內容根URI值的字串值。 確保表單設計位於內容根URI中。 否則，Forms服務會擲回例外狀況。 要引用儲存庫，請指定 `repository://`.
   * 叫用 `URLSpec` 物件 `setTargetURL` 方法，並傳遞字串值，指定表單資料張貼到的目標URL值。 如果您在表單設計中定義目標URL，則可以傳遞空字串。 您也可以指定表單要傳送到哪個URL，以執行計算。

1. 轉譯表單

   叫用 `FormsService` 物件 `renderPDFForm` 方法，並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` 包含要與表單合併資料的物件。 如果您不想合併資料，請傳遞 `null`.
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 請注意，如果輸入文檔是PDF文檔，則無法設定標籤的PDF選項。 如果輸入檔案是XDP檔案，則可以設定標籤的PDF選項。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 這是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 由方法填入的物件。 此參數用於儲存已呈現的表單。
   * 空白 `javax.xml.rpc.holders.LongHolder` 由方法填入的物件。 此引數會以表單儲存頁數。
   * 空白 `javax.xml.rpc.holders.StringHolder` 由方法填入的物件。 此參數將儲存區域設定值。
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

[根據片段轉譯Forms](#rendering-forms-based-on-fragments)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
