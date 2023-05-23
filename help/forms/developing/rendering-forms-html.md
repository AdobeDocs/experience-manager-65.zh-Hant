---
title: 讓Forms成為HTML
seo-title: Rendering Forms as HTML
description: 使用Forms服務將表單作為HTML呈現，以響應來自Web瀏覽器的HTTP請求。 可以使用Java API和Web服務API將表單呈現為HTML。
seo-description: Use the Forms service to render forms as HTML in response to an HTTP request from a web browser. You can use the Java API and Web Service API to render forms as HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4150'
ht-degree: 0%

---

# 讓Forms成為HTML {#rendering-forms-as-html}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

Forms服務將表單呈現為HTML，以響應來自Web瀏覽器的HTTP請求。 將表單呈現為HTML的好處是客戶端Web瀏覽器所在的電腦不需要Adobe Reader、Acrobat或Flash Player(對於表單指南（不建議使用）)。

要將表單渲染為HTML，必須將表單設計另存為XDP檔案。 保存為PDF檔案的窗體設計無法呈現為HTML。 在設計器中開發將呈現為HTML的表單設計時，請考慮以下條件：

* 不要使用對象的邊框屬性在窗體上繪製線條、框或網格。 某些瀏覽器可能與預覽中顯示的邊框完全不同。 對象可能顯示分層或將其他對象推離其預期位置。
* 可以使用線條、矩形和圓定義背景。
* 繪製文本略大於容納文本所需的內容。 某些Web瀏覽器無法清晰顯示文本。

>[!NOTE]
>
>使用 `FormServiceClient` 對象 `(Deprecated) renderHTMLForm` 和 `renderHTMLForm2` 方法，在Internet Explorer或Mozilla Firefox瀏覽器中顯示的呈現的TIFF表單中，HTML影像不可見。 這些瀏覽器不提供對TIFF影像的本機支援。

## HTML頁 {#html-pages}

當將表單設計呈現為HTML表單時，每個第二級子表單呈現為HTML頁（面板）。 可以在設計器中查看子窗體的層次結構。 屬於根子窗體的子子窗體（根子窗體的預設名稱為form1）是面板子窗體。 以下示例顯示了窗體設計的子窗體。

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

當表單設計呈現為HTML表單時，面板不受任何特定頁面大小的限制。 如果具有動態子窗體，則應將其嵌套在面板子窗體中。 動態子表單能夠擴展到無限數量的HTML頁。

當表單呈現為HTML表單時，頁面大小(對於呈現為PDF的分頁表單而言是必需的)沒有任何意義。 因為具有可流式佈局的表單可以擴展到無限數量的HTML頁，所以避免母版頁上的頁腳非常重要。 首頁內容區域下方的頁腳可以覆蓋流經頁面邊界的HTML內容。

必須使用 `xfa.host.pageUp` 和 `xfa.host.pageDown` 的雙曲餘切值。 通過向Forms服務發送表單，並讓Forms服務將表單呈現回客戶端設備（通常是Web瀏覽器）來更改頁面。

>[!NOTE]
>
>將表單發送到Forms服務，然後讓Forms服務將表單呈現回客戶端設備的過程稱為向伺服器的往返跳轉資料。

>[!NOTE]
>
>如果要自定義HTML表單上「HTML數字簽名」按鈕的外觀，必須更改fscdigsig.css檔案（adobe-forms-ds.ear > adobe-forms-ds.war檔案中）中的以下屬性：

**.fsc-ds-ssb**:此樣式表適用於空白符號欄位。

**.fsc-ds-ssv**:此樣式表適用於「有效符號」欄位。

**.fsc-ds-ssc**:此樣式表適用於「有效符號」欄位，但資料已更改。

**.fsc-ds-ssi**:此樣式表適用於無效符號欄位的情況。

**.fsc-ds-pop-bg**:未使用此樣式表屬性。

**.fsc-ds-popup-btn**:未使用此樣式表屬性。

## 運行指令碼 {#running-scripts}

表單作者指定指令碼是在伺服器還是客戶端上執行。 Forms服務建立分佈式事件處理環境，用於執行可通過使用 `runAt` 屬性。 有關此屬性或在表單設計中建立指令碼的資訊，請參見 [Forms設計師](https://www.adobe.com/go/learn_aemforms_designer_63_tw)

Forms服務可以在呈現表單時執行指令碼。 因此，可以通過連接到資料庫或客戶端上可能不可用的Web服務來預填充表單中的資料。 也可以設定按鈕的 `Click` 要在伺服器上運行的事件，以便客戶端將往返資料返回到伺服器。 這允許客戶端在用戶與表單交互時運行可能需要伺服器資源的指令碼。 對於HTML表單，只能在伺服器上執行formcalc指令碼。 因此，必須將這些指令碼標籤為在 `server` 或 `both`。

可以通過調用來設計在頁面（面板）之間移動的表單 `xfa.host.pageUp` 和 `xfa.host.pageDown` 的雙曲餘切值。 此指令碼放在按鈕的 `Click` 事件和 `runAt` 屬性設定為 `Both`。 您選擇的原因 `Both` 這樣，Adobe Reader或Acrobat(對於作為PDF呈現的表單)可以更改頁面而不進入伺服器，而HTML表單可以通過將資料往返到伺服器來更改頁面。 即，將表單發送到Forms服務，並將表單呈現為HTML，並顯示新頁面。

建議不要為指令碼變數和表單域指定與項目等名稱相同的名稱。 某些Web瀏覽器（如Internet Explorer）可能無法初始化與表單域同名的變數，該變數會導致指令碼錯誤。 將表單域和指令碼變數賦予不同的名稱是一種很好的做法。

在呈現同時包含頁面導航功能和表單指令碼的HTML表單時（例如，假設指令碼每次呈現表單時都從資料庫中檢索欄位資料），請確保表單指令碼位於form:calculate event而不是form:readyevent中。

位於表單：ready事件中的表單指令碼在表單的初始呈現期間僅執行一次，並且不會執行後續頁檢索。 相反，對於呈現表單的每頁導航，將執行表單：計算事件。

>[!NOTE]
在多頁表單上，如果您移動到其他頁，則JavaScript對頁所做的更改不會保留。

在提交表單之前，可以調用自定義指令碼。 此功能適用於所有可用的瀏覽器。 但是，僅當用戶呈現具有其的HTML窗體時，才可使用 `Output Type` 屬性設定為 `Form Body`。 當 `Output Type` 是 `Full HTML`。 有關配置此功能的步驟，請參閱管理幫助中的「配置表單」。

必須先定義在提交表單之前調用的回調函式，其中函式的名稱為 `_user_onsubmit`。 假定函式不會引發任何異常，或者如果引發異常，則將忽略該異常。 建議將JavaScript函式放在html的head部分；但是，可以在包含指令碼標籤的末尾之前的任何位置聲明它 `xfasubset.js`。

當formserver呈現包含下拉清單的XDP時，除建立下拉清單外，還會建立兩個隱藏的文本欄位。 這些文本欄位儲存下拉清單的資料（一個儲存選項的顯示名稱，另一個儲存選項的值）。 因此，每次用戶提交表單時，都會提交下拉清單的整個資料。 假定您不想每次提交這麼多資料，您可以編寫自定義指令碼來禁用該指令碼。 例如：下拉清單的名稱為 `drpOrderedByStateProv` 它被包裹在子表格標題下。 HTML輸入元素的名稱將 `header[0].drpOrderedByStateProv[0]`。 儲存和提交下拉清單資料的隱藏欄位的名稱具有以下名稱： `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

如果不想發佈資料，可以以下方式禁用這些輸入元素。 `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## XFA子集 {#xfa-subsets}

在建立表單設計以呈現為HTML時，必須將指令碼僅限於JavaScript語言中指令碼的XFA子集。

在客戶端上運行或在客戶端和伺服器上運行的指令碼必須寫入XFA子集。 在伺服器上運行的指令碼可以使用完整的XFA指令碼模型，也可以使用FormCalc。 有關使用JavaScript的資訊，請參見 [Forms設計師](https://www.adobe.com/go/learn_aemforms_designer_63_tw)。

在客戶端上運行指令碼時，只顯示當前面板才能使用指令碼；例如，當顯示面板B時，不能對面板A中的欄位進行指令碼編寫。 在伺服器上運行指令碼時，可以訪問所有面板。

在客戶端上運行的指令碼中使用指令碼對象模型(SOM)表達式時，還必須小心。 在客戶端上運行的指令碼只支援SOM表達式的簡化子集。

## 事件計時 {#event-timing}

XFA子集定義映射到HTML事件的XFA事件。 在計算和驗證事件的定時上，行為稍有不同。 在Web瀏覽器中，當您退出欄位時執行完全計算事件。 更改欄位值時不會自動執行計算事件。 通過調用 `xfa.form.execCalculate` 的雙曲餘切值。

在Web瀏覽器中，驗證事件僅在退出欄位或提交表單時執行。 可以使用 `xfa.form.execValidate` 的雙曲餘切值。

Forms在Web瀏覽器(與Adobe Reader或Acrobat不同)中顯示，符合XFA空test（錯誤或警告）的強制欄位。

* 如果空test產生錯誤，並且您退出欄位而未指定值，則將顯示一個消息框，並且在按一下「確定」後將重新定位到該欄位。
* 如果空test產生警告，並且您在不指定值的情況下退出欄位，則系統將提示您按一下「確定」或「取消」，從而為您提供在不指定值的情況下繼續操作或返回到欄位以輸入值的選項。

有關空test的詳細資訊，請參見 [Forms設計師](https://www.adobe.com/go/learn_aemforms_designer_63_tw)。

## 窗體按鈕 {#form-buttons}

按一下提交按鈕將表單資料發送到Forms服務並表示表單處理的結束。 的 `preSubmit` 可以將事件設定為在客戶端或伺服器上運行。 的 `preSubmit` 事件在表單提交之前運行（如果配置為在客戶端上運行）。 否則， `preSubmit` 事件在提交表單期間在伺服器上運行。 有關 `preSubmit` 事件，請參閱 [Forms設計師](https://www.adobe.com/go/learn_aemforms_designer_63_tw)。

如果按鈕沒有與其關聯的客戶端指令碼，則資料將提交到伺服器，在伺服器上執行計算，並重新生成HTML表單。 如果按鈕包含客戶端指令碼，則資料不會發送到伺服器，客戶端指令碼在Web瀏覽器中執行。

## HTML4.0 Web瀏覽器 {#html-4-0-web-browser}

僅支援HTML4.0的Web瀏覽器不能支援XFA子集客戶端指令碼模型。 在建立表單設計以在4.0HTML和MSDHTML或CSS2HTML中同時工作時，標籤為在客戶端運行的指令碼實際上將在伺服器上運行。 例如，假定用戶按一下位於HTML4.0 Web瀏覽器中顯示的表單上的按鈕。 在這種情況下，表單資料將發送到執行客戶端指令碼的伺服器。

建議將表單邏輯放在計算事件中，這些事件在HTML4.0中的伺服器上運行，在MSDHTML或CSS2HTML的客戶端上運行。

## 維護演示文稿更改 {#maintaining-presentation-changes}

在HTML頁（面板）之間移動時，僅維護資料狀態。 不維護背景顏色或強制欄位設定等設定（如果與初始設定不同）。 要維護演示狀態，必須建立表示欄位的演示狀態的欄位（通常是隱藏的）。 如果將指令碼添加到欄位 `Calculate` 如果根據隱藏欄位值更改演示文稿，則可以在HTML頁（面板）之間來回移動時保留演示文稿狀態。

以下指令碼維護 `fillColor` 值 `hiddenField`。 假定此指令碼位於欄位的 `Calculate` 的子菜單。

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
當嵌套在表單元格內時，靜態對象不會顯示在呈現的HTML表單中。 例如，嵌套在表單元格中的圓和矩形不會顯示在渲染HTML窗體中。 但是，當這些相同的靜態對象位於表之外時，它們會正確顯示。

## 數字簽名HTML表單 {#digitally-signing-html-forms}

如果將表單呈現為以下HTML轉換之一，則不能對包含數字簽名欄位的HTML表單進行簽名：

* AHTML
* HTML4
* 靜態HTML
* 無指令碼XHTML

有關對文檔進行數字簽名的資訊，請參見 [數字簽名和驗證文檔](/help/forms/developing/digitally-signing-certifying-documents.md)

## 呈現符合輔助功能准則的XHTML表單 {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

您可以呈現符合輔助功能准則的完整HTML表單。 即，表單在完整HTML標籤中呈現，而不是在正文標籤(不是完整HTML頁)中呈現HTML表單。

## 驗證表單資料 {#validating-form-data}

建議在將表單呈現為HTML表單時，限制對表單域的驗證規則的使用。 某些驗證規則可能不支援HTML表單。 例如，當MM-DD-YYYY的驗證模式應用於 `Date/Time` 位於作為HTML窗體呈現的窗體設計中的欄位，即使輸入的日期正確，該欄位也無法正常工作。 但是，此驗證模式對於呈現為PDF的表單適用。

>[!NOTE]
有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

要呈現HTML窗體，請執行以下步驟：

1. 包括項目檔案。
1. 建立Forms客戶端API對象。
1. 設定HTML運行時選項。
1. 呈現HTML窗體。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Forms客戶端API對象**

在以寫程式方式將資料導入PDFformClient API之前，必須建立Form Data Integration服務客戶端。 建立服務客戶端時，定義調用服務所需的連接設定。

**設定HTML運行時選項**

在呈現HTML窗體時設定HTML運行時選項。 例如，您可以向HTML表單添加工具欄，以使用戶能夠選擇位於客戶端電腦上的檔案附件或檢索使用HTML表單呈現的檔案附件。 預設情況下，HTML工具欄被禁用。 要將工具欄添加到HTML窗體，必須以寫程式方式設定運行時選項。 預設情況下，HTML工具欄由以下按鈕組成：

* `Home`:提供到應用程式Web根的連結。
* `Upload`:提供用戶介面以選擇要附加到當前窗體的檔案。
* `Download`:提供用於顯示附加檔案的用戶介面。

當HTML表單上顯示HTML工具欄時，用戶最多可以選擇十個要提交的檔案以及表單資料。 提交檔案後，Forms服務可以檢索檔案。

在將表單呈現為HTML時，可以指定用戶代理值。 用戶代理值提供瀏覽器和系統資訊。 這是可選值，您可以傳遞空字串值。 使用Java API快速啟動呈現HTML表單顯示如何獲取用戶代理值並使用它呈現表單為HTML。

通過使用Forms服務客戶端API設定目標URL，可以指定表單資料發佈到的HTTP URL，也可以在XDP表單設計中包含的「提交」按鈕中指定。 如果在表單設計中指定了目標URL，則不要使用Forms服務客戶端API設定值。

>[!NOTE]
使用工具欄呈現HTML窗體是可選的。

>[!NOTE]
如果呈現AHTML表單，建議不要向表單添加工具欄。

**呈現HTML窗體**

要呈現HTML窗體，必須指定在設計器中建立並另存為XDP檔案的窗體設計。 還必須選擇HTML轉換類型。 例如，可以指定為Internet Explorer 5.0或更高版本呈現動態HTML的HTML轉換類型。

呈現HTML表單還需要值，如呈現其他表單類型所需的URI值。

**將表單資料流寫入客戶端Web瀏覽器**

當Forms服務呈現HTML表單時，它將返回您必須寫入客戶端Web瀏覽器的表單資料流。 寫入客戶端Web瀏覽器時，用戶可以看到HTML表單。

**另請參閱**

[使用Java API將表單呈現為HTML](#render-a-form-as-html-using-the-java-api)

[使用Web服務API將表單呈現為HTML](#render-a-form-as-html-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[使用自定義工具欄呈現HTMLForms](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API將表單呈現為HTML {#render-a-form-as-html-using-the-java-api}

使用FormsAPI(Java)呈現HTML表單：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。

1. 建立Forms客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 設定HTML運行時選項

   * 建立 `HTMLRenderSpec` 對象。
   * 要使用工具欄呈現HTML窗體，請調用 `HTMLRenderSpec` 對象 `setHTMLToolbar` 方法和通過 `HTMLToolbar` 枚舉值。 例如，要顯示垂直HTML工具欄，請通過 `HTMLToolbar.Vertical`。
   * 要設定HTML窗體的區域設定值，請調用 `HTMLRenderSpec` 對象 `setLocale` 方法並傳遞一個字串值，該字串值指定區域設定值。 （這是可選設定。）
   * 要在完整HTML標籤內呈現HTML窗體，請調用 `HTMLRenderSpec` 對象 `setOutputType` 方法 `OutputType.FullHTMLTags`。 （這是可選設定。）

   >[!NOTE]
   Forms未在HTML中成功呈現 `StandAlone` 選項 `true` 和 `ApplicationWebRoot` 引用承載AEM Forms的J2EE應用程式伺服器以外的伺服器( `ApplicationWebRoot` 使用 `URLSpec` 傳遞給 `FormsServiceClient` 對象 `(Deprecated) renderHTMLForm` )。 當 `ApplicationWebRoot` 是托管AEM Forms的另一台伺服器，需要將管理控制台中的web根URI值設定為窗體的web應用程式URI值。 可以通過登錄到管理控制台，按一下「服務」>「Forms」，並將Web根URI設定為https://server-name:port/FormServer來完成此操作。 然後，保存設定。

1. 呈現HTML窗體

   調用 `FormsServiceClient` 對象 `(Deprecated) renderHTMLForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `TransformTo` 指定HTML首選項類型的枚舉值。 例如，要呈現與Internet Explorer 5.0或更高版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`。
   * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞一個空 `com.adobe.idp.Document` 的雙曲餘切值。
   * 的 `HTMLRenderSpec` 儲存HTML運行時選項的對象。
   * 一個字串值，它指定 `HTTP_USER_AGENT` 標題值；比如說， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * A `URLSpec` 儲存呈現HTML窗體所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。

   的 `(Deprecated) renderHTMLForm` 方法返回 `FormsResult` 包含可寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `com.adobe.idp.Document` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `com.adobe.idp.Document` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
   * 通過調用 `InputStream` 對象 `read` 方法，並將位元組陣列作為參數傳遞。
   * 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[讓Forms成為HTML](#rendering-forms-as-html)

[快速啟動（SOAP模式）:使用Java API呈現HTML窗體](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API將表單呈現為HTML {#render-a-form-as-html-using-the-web-service-api}

使用FormsAPI（Web服務）呈現HTML表單：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包括到類路徑中。

1. 建立Forms客戶端API對象

   建立 `FormsService` 對象和設定驗證值。

1. 設定HTML運行時選項

   * 建立 `HTMLRenderSpec` 對象。
   * 要使用工具欄呈現HTML窗體，請調用 `HTMLRenderSpec` 對象 `setHTMLToolbar` 方法和通過 `HTMLToolbar` 枚舉值。 例如，要顯示垂直HTML工具欄，請通過 `HTMLToolbar.Vertical`。
   * 要設定HTML窗體的區域設定值，請調用 `HTMLRenderSpec` 對象 `setLocale` 方法並傳遞一個字串值，該字串值指定區域設定值。 有關詳細資訊，請參見 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 要在完整HTML標籤內呈現HTML窗體，請調用 `HTMLRenderSpec` 對象 `setOutputType` 方法 `OutputType.FullHTMLTags`。

   >[!NOTE]
   Forms未在HTML中成功呈現 `StandAlone` 選項 `true` 和 `ApplicationWebRoot` 引用承載AEM Forms的J2EE應用程式伺服器以外的伺服器( `ApplicationWebRoot` 使用 `URLSpec` 傳遞給 `FormsServiceClient` 對象 `(Deprecated) renderHTMLForm` )。 當 `ApplicationWebRoot` 是托管AEM Forms的另一台伺服器，需要將管理控制台中的web根URI值設定為窗體的web應用程式URI值。 可以通過登錄到管理控制台，按一下「服務」>「Forms」，並將Web根URI設定為https://server-name:port/FormServer來完成此操作。 然後，保存設定。

1. 呈現HTML窗體

   調用 `FormsService` 對象 `(Deprecated) renderHTMLForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `TransformTo` 指定HTML首選項類型的枚舉值。 例如，要呈現與Internet Explorer 5.0或更高版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`。
   * A `BLOB` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞 `null`。 (請參閱 [用可流式佈局預填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)。)
   * 的 `HTMLRenderSpec` 儲存HTML運行時選項的對象。
   * 一個字串值，它指定 `HTTP_USER_AGENT` 標題值；比如說， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。 如果不想設定此值，可以傳遞空字串。
   * A `URLSpec` 儲存呈現HTML窗體所需的URI值的對象。 (請參閱 [指定URI值](/help/forms/developing/rendering-interactive-pdf-forms.md)。)
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。 (請參閱 [將檔案附加到窗體](/help/forms/developing/rendering-interactive-pdf-forms.md)。)
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的對象。 此參數值儲存渲染的表單。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的對象。 此參數將儲存輸出XML資料。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的對象。 此參數將儲存窗體中的頁數。
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的對象。 此參數將儲存區域設定值。
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的對象。 此參數將儲存所使用的HTML呈現值。
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

[讓Forms成為HTML](#rendering-forms-as-html)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
