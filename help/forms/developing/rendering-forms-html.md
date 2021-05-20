---
title: 將Forms轉譯為HTML
seo-title: 將Forms轉譯為HTML
description: 使用Forms服務，回應來自網頁瀏覽器的HTTP要求，將表單轉譯為HTML。 您可以使用Java API和網站服務API，將表單轉譯為HTML。
seo-description: 使用Forms服務，回應來自網頁瀏覽器的HTTP要求，將表單轉譯為HTML。 您可以使用Java API和網站服務API，將表單轉譯為HTML。
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
source-wordcount: '4188'
ht-degree: 0%

---

# 將Forms呈現為HTML {#rendering-forms-as-html}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

Forms服務會回應來自網頁瀏覽器的HTTP要求，將表單轉譯為HTML。 將表單轉譯為HTML的好處是用戶端網頁瀏覽器所在的電腦不需要Adobe Reader、Acrobat或Flash Player(適用於表單指南（已淘汰）)。

若要將表單轉譯為HTML，表單設計必須儲存為XDP檔案。 另存為PDF檔案的表單設計無法呈現為HTML。 在設計工具中開發將呈現為HTML的表單設計時，請考慮下列條件：

* 請勿使用對象的邊框屬性在窗體上繪製線、框或網格。 某些瀏覽器可能無法像預覽中一樣排列邊框。 對象可能呈分層狀態，也可能將其他對象推離其預期位置。
* 您可以使用線、矩形和圓來定義背景。
* 繪製文本比容納文本所需的文本稍大。 有些網頁瀏覽器無法清晰顯示文字。

>[!NOTE]
>
>使用`FormServiceClient`對象的`(Deprecated) renderHTMLForm`和`renderHTMLForm2`方法呈現包含TIFF影像的表單時，在Internet Explorer或Mozilla Firefox瀏覽器中顯示的呈現的HTML表單中看不到TIFF影像。 這些瀏覽器不提供TIFF影像的原生支援。

## HTML頁面{#html-pages}

表單設計轉譯為HTML表單時，每個第二層子表單會轉譯為HTML頁面（面板）。 您可以在設計工具中檢視子表單的階層。 屬於根子表單的子表單（根子表單的預設名稱為form1）是面板子表單。 以下範例顯示表單設計的子表單。

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

當表單設計呈現為HTML表單時，面板不受限於任何特定頁面大小。 如果您有動態子表單，應將其巢狀內嵌在面板子表單中。 動態子表單可以展開至無限數量的HTML頁面。

表單轉譯為HTML表單時，頁面大小（轉譯為PDF的表單為必要頁面）沒有意義。 因為具有可流式版面的表單可以展開為無限數量的HTML頁面，所以請務必避免主版頁面上的頁尾。 主版頁面上內容區域下方的頁尾可能會覆寫流過頁面界限的HTML內容。

您必須使用`xfa.host.pageUp`和`xfa.host.pageDown`方法，在面板之間顯式移動。 您可以將表單傳送至Forms服務，並讓Forms服務將表單轉譯回用戶端裝置（通常是網頁瀏覽器），借此變更頁面。

>[!NOTE]
>
>將表單傳送至Forms服務，然後讓Forms服務將表單轉譯回用戶端裝置的程式，即稱為將資料往返於伺服器。

>[!NOTE]
>
>如果要自訂HTML表單上「HTML數位簽名」按鈕的外觀，必須在fscdigsig.css檔案（在adobe-forms-ds.ear > adobe-forms-ds.war檔案中）中變更下列屬性：

**.fsc-ds-ssb**:此樣式表適用於空白符號欄位。

**.fsc-ds-ssv**:此樣式表適用於有效符號欄位。

**.fsc-ds-ssc**:此樣式表適用於有效符號欄位，但資料已變更。

**.fsc-ds-ssi**:此樣式表適用於無效符號欄位的情況。

**.fsc-ds-popup-bg**:未使用此樣式表屬性。

**.fsc-ds-popup-btn**:未使用此樣式表屬性。

## 運行指令碼{#running-scripts}

表單作者會指定指令碼是在伺服器上還是在用戶端上執行。 Forms服務會建立分佈式事件處理環境，以執行可使用`runAt`屬性在用戶端與伺服器之間分佈的表單智慧。 如需此屬性或在表單設計內建立指令碼的相關資訊，請參閱[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Forms服務可在表單轉譯時執行指令碼。 因此，您可以連接到資料庫或客戶端上可能不可用的Web服務，用資料預填表單。 您也可以設定按鈕的`Click`事件以在伺服器上執行，以便客戶端將行程資料往返到伺服器。 這允許客戶端在用戶與表單交互時運行可能需要伺服器資源的指令碼，如企業資料庫。 對於HTML表單，只能在伺服器上執行表單計算指令碼。 因此，必須將這些指令碼標籤為在`server`或`both`運行。

您可以借由呼叫`xfa.host.pageUp`和`xfa.host.pageDown`方法來設計在頁面（面板）之間移動的表單。 此指令碼被放在按鈕的`Click`事件中，並且`runAt`屬性被設定為`Both`。 您選擇`Both`的原因是，Adobe Reader或Acrobat（針對以PDF呈現的表單）可以變更頁面而不前往伺服器，而HTML表單可借由將資料往返於伺服器來變更頁面。 也就是說，表單會傳送至Forms服務，且表單會以HTML格式呈現，並顯示新頁面。

建議您不要為指令碼變數和表單欄位指定與項目等相同的名稱。 某些網頁瀏覽器（例如Internet Explorer）可能無法初始化與表單欄位同名的變數，而導致指令碼錯誤發生。 將表單欄位和指令碼變數命名為不同名稱是很好的作法。

呈現同時包含頁面導覽功能和表單指令碼的HTML表單時（例如，假設指令碼每次呈現表單時都從資料庫中擷取欄位資料），請確定表單指令碼位於form:calculate事件中，而非form:readyevent中。

位於form:ready事件中的表單指令碼在表單初始呈現期間只會執行一次，且不會針對後續的頁面擷取執行。 相反地，會針對轉譯表單的每個頁面導覽執行form:calculate事件。

>[!NOTE]
在多頁表單中，如果您移至不同頁面，則JavaScript對頁面所做的變更不會保留。

您可以在提交表單前叫用自訂指令碼。 此功能適用於所有可用的瀏覽器。 不過，只有當使用者轉譯其`Output Type`屬性設為`Form Body`的HTML表單時，才能使用它。 當`Output Type`為`Full HTML`時，將無法運作。 如需設定此功能的步驟，請參閱管理說明中的設定表單。

您必須先定義呼叫的回呼函式，再提交表單，其中函式的名稱為`_user_onsubmit`。 假設函式不會擲回任何例外，或若有，則會忽略例外。 建議將JavaScript函式放置在html的head區段中；不過，您可以在包含`xfasubset.js`的指令碼標籤結尾之前的任何地方進行宣告。

當formserver轉譯包含下拉式清單的XDP時，除了建立下拉式清單外，還會建立兩個隱藏的文字欄位。 這些文本欄位儲存下拉清單的資料（一個儲存選項的顯示名稱，另一個儲存選項的值）。 因此，每次使用者提交表單時，都會提交下拉式清單的整個資料。 假設您不想每次提交太多資料，您可以撰寫自訂指令碼來停用該功能。 例如：下拉式清單的名稱為`drpOrderedByStateProv`，並會包裝在子表單標題下。 HTML輸入元素的名稱為`header[0].drpOrderedByStateProv[0]`。 儲存並提交下拉式清單資料的隱藏欄位名稱具有下列名稱：`header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

如果您不想張貼資料，可以透過下列方式停用這些輸入元素。`var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

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

## XFA子集{#xfa-subsets}

建立表單設計以呈現為HTML時，您必須針對JavaScript語言的指令碼，將指令碼限制為XFA子集。

在用戶端上執行或同時在用戶端和伺服器上執行的指令碼，必須寫入XFA子集內。 在伺服器上運行的指令碼可以使用完整的XFA指令碼模型，也可以使用FormCalc。 如需使用JavaScript的相關資訊，請參閱[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

在用戶端上執行指令碼時，只有顯示的目前面板才可使用指令碼；例如，當面板B顯示時，您無法對面板A中的欄位進行指令碼編寫。 在伺服器上執行指令碼時，可存取所有面板。

在客戶端上運行的指令碼內使用指令碼對象模型(SOM)表達式時，您也必須小心。 在客戶端上運行的指令碼僅支援簡化的SOM表達式子集。

## 事件計時{#event-timing}

XFA子集會定義對應至HTML事件的XFA事件。 計算和驗證事件的時間上的行為稍有不同。 在網頁瀏覽器中，當您退出欄位時，會執行完整計算事件。 當您變更欄位值時，不會自動執行計算事件。 您可以呼叫`xfa.form.execCalculate`方法以強制執行計算事件。

在Web瀏覽器中，驗證事件僅在退出欄位或提交表單時執行。 您可以使用`xfa.form.execValidate`方法來強制驗證事件。

顯示在網頁瀏覽器中的Forms(與Adobe Reader或Acrobat相反)符合必填欄位的XFA空值測試（錯誤或警告）。

* 如果空測試產生錯誤，而您退出欄位而未指定值，則會顯示消息框，並在按一下「確定」後重新定位到該欄位。
* 如果空測試產生警告，而您退出欄位時未指定值，則系統提示您按一下「確定」或「取消」，為您提供繼續操作而不指定值或返回欄位以輸入值的選項。

有關Null測試的詳細資訊，請參閱[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

## 表單按鈕{#form-buttons}

按一下提交按鈕會將表單資料傳送至Forms服務，並代表表單處理結束。 `preSubmit`事件可設定為在客戶端或伺服器上運行。 如果將`preSubmit`事件配置為在客戶端上運行，則該事件在表單提交之前運行。 否則，在表單提交期間， `preSubmit`事件會在伺服器上執行。 如需`preSubmit`事件的詳細資訊，請參閱[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

如果按鈕沒有與其相關聯的用戶端指令碼，則會將資料提交到伺服器，在伺服器上執行計算，並重新生成HTML表單。 如果按鈕包含用戶端指令碼，則資料不會傳送至伺服器，且用戶端指令碼會在Web瀏覽器中執行。

## HTML 4.0網頁瀏覽器{#html-4-0-web-browser}

僅支援HTML 4.0的網頁瀏覽器無法支援XFA子集用戶端指令碼模型。 建立表單設計以在HTML 4.0和MSDHTML或CSS2HTML中運作時，標示為在用戶端執行的指令碼實際上會在伺服器上執行。 例如，假設使用者按一下位於HTML 4.0網頁瀏覽器中所顯示表單上的按鈕。 在此情況下，表單資料會傳送至執行用戶端指令碼的伺服器。

建議您將表單邏輯放入計算事件中，該事件在HTML 4.0的伺服器上執行，並在MSDHTML或CSS2HTML的用戶端上執行。

## 維護演示文稿更改{#maintaining-presentation-changes}

當您在HTML頁面（面板）之間移動時，只會保留資料的狀態。 背景顏色或必填欄位設定等設定不會保留（如果與初始設定不同）。 要維護呈現狀態，必須建立表示欄位呈現狀態的欄位（通常隱藏）。 如果向欄位的`Calculate`事件新增指令碼，該事件會根據隱藏的欄位值來變更簡報，則當您在HTML頁面（面板）之間來回移動時，可以保留簡報狀態。

以下指令碼根據`hiddenField`的值維護欄位的`fillColor`。 假設此指令碼位於欄位的`Calculate`事件中。

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
巢狀內嵌在表格儲存格內時，呈現的HTML表單中不會顯示靜態物件。 例如，嵌套在表格單元格內的圓形和矩形不會顯示在渲染HTML表單內。 但是，如果位於表之外，則會正確顯示這些相同的靜態對象。

## 數位簽署HTML表單{#digitally-signing-html-forms}

如果表單呈現為以下HTML轉換之一，則無法對包含數字簽名欄位的HTML表單進行簽名：

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

有關對文檔進行數字簽名的資訊，請參閱[數字簽名和認證文檔](/help/forms/developing/digitally-signing-certifying-documents.md)

## 呈現符合協助工具指南的XHTML表單{#rendering-an-accessibility-guidelines-compliant-xhtml-form}

您可以呈現符合協助工具准則的完整HTML表單。 也就是說，表單會在完整HTML標籤中呈現，而非在內文標籤中呈現的HTML表單（不是完整的HTML頁面）。

## 驗證表單資料{#validating-form-data}

將表單轉譯為HTML表單時，建議您限制使用表單欄位驗證規則。 HTML表單可能不支援某些驗證規則。 例如，將MM-DD-YYYY的驗證模式套用至`Date/Time`欄位（位於以HTML表單呈現的表單設計中）時，即使正確輸入日期，它仍無法正常運作。 不過，此驗證模式適用於以PDF呈現的表單。

>[!NOTE]
如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟{#summary-of-steps}的摘要

要呈現HTML表單，請執行以下步驟：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 設定HTML運行時選項。
1. 轉譯HTML表單。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms用戶端API物件**

您必須先建立「表單資料整合服務」用戶端，才能以程式設計方式將資料匯入PDF formClient API。 建立服務客戶端時，您定義調用服務所需的連接設定。

**設定HTML運行時選項**

在轉譯HTML表單時，您可以設定HTML執行階段選項。 例如，您可以將工具欄添加到HTML表單中，以便用戶選擇位於客戶端電腦上的檔案附件或檢索使用HTML表單呈現的檔案附件。 HTML工具列預設為停用。 若要將工具列新增至HTML表單，您必須以程式設計方式設定執行階段選項。 預設情況下， HTML工具欄由以下按鈕組成：

* `Home`:提供應用程式Web根目錄的連結。
* `Upload`:提供一個用戶介面，用於選擇要附加到當前表單的檔案。
* `Download`:提供用於顯示附加檔案的用戶介面。

當HTML表單上出現HTML工具列時，使用者最多可以選取10個要連同表單資料一起提交的檔案。 提交檔案後，Forms服務便可擷取檔案。

將表單轉譯為HTML時，您可以指定使用者代理程式值。 用戶代理值提供瀏覽器和系統資訊。 這是選用值，您可以傳遞空字串值。 「使用Java API呈現HTML表單」快速入門會說明如何取得使用者代理程式值，並使用它將表單轉譯為HTML。

表單資料張貼位置的HTTP URL可透過使用Forms服務用戶端API設定目標URL來指定，或可在XDP表單設計中的「提交」按鈕中指定。 如果在表單設計中指定目標URL，則請勿使用Forms服務用戶端API設定值。

>[!NOTE]
使用工具列轉譯HTML表單為選用。

>[!NOTE]
如果您轉譯AHTML表單，建議您不要將工具列新增至表單。

**轉譯HTML表單**

要呈現HTML表單，必須指定在「設計器」中建立並另存為XDP檔案的表單設計。 您也必須選取HTML轉換類型。 例如，您可以指定HTML轉換類型，為Internet Explorer 5.0或更新版本轉譯動態HTML。

呈現HTML表單還需要值，如呈現其他表單類型所需的URI值。

**將表單資料流寫入客戶端Web瀏覽器**

Forms服務轉譯HTML表單時，會傳回您必須寫入用戶端網頁瀏覽器的表單資料流。 寫入客戶端Web瀏覽器時，用戶可看到HTML表單。

**另請參閱**

[使用Java API將表單轉譯為HTML](#render-a-form-as-html-using-the-java-api)

[使用網站服務API將表單轉譯為HTML](#render-a-form-as-html-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉譯互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[使用自訂工具列轉譯HTML Forms](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API {#render-a-form-as-html-using-the-java-api}將表單轉譯為HTML

使用Forms API(Java)呈現HTML表單：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`FormsServiceClient`物件。

1. 設定HTML運行時選項

   * 使用其建構子建立`HTMLRenderSpec`物件。
   * 若要使用工具列呈現HTML表單，請叫用`HTMLRenderSpec`物件的`setHTMLToolbar`方法，並傳遞`HTMLToolbar`列舉值。 例如，要顯示垂直HTML工具欄，請傳遞`HTMLToolbar.Vertical`。
   * 要設定HTML表單的區域設定值，請調用`HTMLRenderSpec`對象的`setLocale`方法並傳遞指定區域設定值的字串值。 （此為選用設定。）
   * 若要在完整HTML標籤內呈現HTML表單，請叫用`HTMLRenderSpec`物件的`setOutputType`方法，並傳遞`OutputType.FullHTMLTags`。 （此為選用設定。）

   >[!NOTE]
   當`StandAlone`選項為`true`且`ApplicationWebRoot`參考托管AEM Forms的J2EE應用程式伺服器以外的伺服器時，未在HTML中成功呈現Forms（`ApplicationWebRoot`值是使用傳遞至`FormsServiceClient`物件的`(Deprecated) renderHTMLForm`方法的`URLSpec`物件指定的）。 當`ApplicationWebRoot`是托管AEM Forms的另一台伺服器時，管理控制台中的Web根URI值必須設定為表單的Web應用程式URI值。 您可以登入管理控制台，按一下「服務> Forms」，然後將Web根URI設為https://server-name:port/FormServer ，即可完成此操作。 然後，儲存您的設定。

1. 轉譯HTML表單

   調用`FormsServiceClient`對象的`(Deprecated) renderHTMLForm`方法並傳遞以下值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定HTML首選項類型的`TransformTo`枚舉值。 例如，要呈現與Internet Explorer 5.0或更高版本的動態HTML相容的HTML表單，請指定`TransformTo.MSDHTML`。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`com.adobe.idp.Document`物件。
   * 儲存HTML運行時選項的`HTMLRenderSpec`對象。
   * 指定`HTTP_USER_AGENT`標題值的字串值；例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * `URLSpec`物件，用於儲存呈現HTML表單所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。

   `(Deprecated) renderHTMLForm`方法返回一個`FormsResult`對象，該對象包含可寫入客戶端Web瀏覽器的表單資料流。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 調用`FormsResult`對象s `getOutputContent`方法，建立`com.adobe.idp.Document`對象。
   * 調用`getContentType`方法，獲取`com.adobe.idp.Document`對象的內容類型。
   * 通過調用`setContentType`方法並傳遞`com.adobe.idp.Document`對象的內容類型來設定`javax.servlet.http.HttpServletResponse`對象的內容類型。
   * 通過調用`javax.servlet.http.HttpServletResponse`對象的`getOutputStream`方法，建立用於將表單資料流寫入客戶端Web瀏覽器的`javax.servlet.ServletOutputStream`對象。
   * 調用`com.adobe.idp.Document`對象的`getInputStream`方法，建立`java.io.InputStream`對象。
   * 叫用`InputStream`物件的`read`方法，並將位元組陣列傳遞為引數，借此建立位元組陣列，並填入表單資料流。
   * 調用`javax.servlet.ServletOutputStream`對象的`write`方法，將表單資料流發送到客戶端Web瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[將Forms轉譯為HTML](#rendering-forms-as-html)

[快速入門（SOAP模式）:使用Java API轉譯HTML表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API {#render-a-form-as-html-using-the-web-service-api}將表單轉譯為HTML

使用Forms API（網站服務）轉譯HTML表單：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`物件並設定驗證值。

1. 設定HTML運行時選項

   * 使用其建構子建立`HTMLRenderSpec`物件。
   * 若要使用工具列呈現HTML表單，請叫用`HTMLRenderSpec`物件的`setHTMLToolbar`方法，並傳遞`HTMLToolbar`列舉值。 例如，要顯示垂直HTML工具欄，請傳遞`HTMLToolbar.Vertical`。
   * 要設定HTML表單的區域設定值，請調用`HTMLRenderSpec`對象的`setLocale`方法並傳遞指定區域設定值的字串值。 如需詳細資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 若要在完整HTML標籤內呈現HTML表單，請叫用`HTMLRenderSpec`物件的`setOutputType`方法，並傳遞`OutputType.FullHTMLTags`。

   >[!NOTE]
   當`StandAlone`選項為`true`且`ApplicationWebRoot`參考托管AEM Forms的J2EE應用程式伺服器以外的伺服器時，未在HTML中成功呈現Forms（`ApplicationWebRoot`值是使用傳遞至`FormsServiceClient`物件的`(Deprecated) renderHTMLForm`方法的`URLSpec`物件指定的）。 當`ApplicationWebRoot`是托管AEM Forms的另一台伺服器時，管理控制台中的Web根URI值必須設定為表單的Web應用程式URI值。 您可以登入管理控制台，按一下「服務> Forms」，然後將Web根URI設為https://server-name:port/FormServer ，即可完成此操作。 然後，儲存您的設定。

1. 轉譯HTML表單

   調用`FormsService`對象的`(Deprecated) renderHTMLForm`方法並傳遞以下值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定HTML首選項類型的`TransformTo`枚舉值。 例如，要呈現與Internet Explorer 5.0或更高版本的動態HTML相容的HTML表單，請指定`TransformTo.MSDHTML`。
   * `BLOB`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞`null`。 (請參閱[使用可流動配置預填Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)。)
   * 儲存HTML運行時選項的`HTMLRenderSpec`對象。
   * 指定`HTTP_USER_AGENT`標題值的字串值；例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。 如果您不想設定此值，可以傳遞空白字串。
   * `URLSpec`物件，用於儲存呈現HTML表單所需的URI值。 （請參閱[指定URI值](/help/forms/developing/rendering-interactive-pdf-forms.md)。）
   * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。 （請參閱[將檔案附加到表單](/help/forms/developing/rendering-interactive-pdf-forms.md)。）
   * 由方法填入的空`com.adobe.idp.services.holders.BLOBHolder`物件。 此參數值儲存呈現的表單。
   * 由方法填入的空`com.adobe.idp.services.holders.BLOBHolder`物件。 此參數將儲存輸出XML資料。
   * 由方法填入的空`javax.xml.rpc.holders.LongHolder`物件。 此引數會以表單儲存頁數。
   * 由方法填入的空`javax.xml.rpc.holders.StringHolder`物件。 此參數將儲存區域設定值。
   * 由方法填入的空`javax.xml.rpc.holders.StringHolder`物件。 此引數將儲存使用的HTML呈現值。
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

[將Forms轉譯為HTML](#rendering-forms-as-html)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
