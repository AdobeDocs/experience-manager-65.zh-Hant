---
title: 將表單轉換為HTML
seo-title: 將表單轉換為HTML
description: 'null'
seo-description: 'null'
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
translation-type: tm+mt
source-git-commit: 9f3129aff8a3e389231b0fe0973794e5d34480a0

---


# 將表單轉換為HTML {#rendering-forms-as-html}

Forms服務會回應來自網頁瀏覽器的HTTP要求，將表單轉譯為HTML。 將表單轉譯為HTML的好處是，用戶端網頁瀏覽器所在的電腦不需要Adobe Reader、Acrobat或Flash Player(表單指南（已停用）)。

若要將表單轉換為HTML，表單設計必須儲存為XDP檔案。 儲存為PDF檔案的表單設計無法轉譯為HTML。 在Designer中開發將呈現為HTML的表單設計時，請考慮下列條件：

* 請勿使用物件的邊框屬性在表單上繪製線條、方塊或格線。 有些瀏覽器可能無法像預覽中顯示的一樣排列邊框。 對象可能呈現分層，也可能將其他對象推離其預期位置。
* 您可以使用線條、矩形和圓形來定義背景。
* 繪製文字，稍大於容納文字所需的大小。 有些網頁瀏覽器無法清晰顯示文字。

>[!NOTE]
>
>當使用物件和方法轉譯包含TIFF `FormServiceClient` 影像的表格 `(Deprecated) renderHTMLForm``renderHTMLForm2` 時，在Internet explorer或Mozilla Firefox瀏覽器中顯示的轉譯HTML表格中，不會顯示TIFF影像。 這些瀏覽器不提供TIFF影像的原生支援。

## HTML頁面 {#html-pages}

當表單設計呈現為HTML表單時，每個二級子表單都會呈現為HTML頁面（面板）。 您可以在Designer中檢視子表單的階層。 屬於根子表單的子子表單（根子表單的預設名稱為form1）是面板子表單。 下列範例顯示表單設計的子表單。

```as3
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

當表單設計轉譯為HTML表單時，面板不會受限於任何特定頁面大小。 如果您有動態子表單，則應將其巢狀內嵌在面板子表單中。 動態子表單可以展開成無限數目的HTML頁面。

當表單轉譯為HTML表單時，頁面大小（轉譯為PDF的表單需要編頁）沒有意義。 因為具有可排列版面的表單可以展開為無限數目的HTML頁面，所以請務必避免主版頁面的頁尾。 主版頁面內容區域下方的頁尾可覆寫流過頁面邊界的HTML內容。

您必須使用和方法，在面板之間顯式 `xfa.host.pageUp` 移動 `xfa.host.pageDown` 面板。 您可以將表單傳送至Forms服務，並讓Forms服務將表單轉譯回用戶端裝置（通常是網頁瀏覽器），以變更頁面。

>[!NOTE]
>
>將表單傳送至Forms服務，然後讓Forms服務將表單轉譯回用戶端裝置的程式，稱為將資料轉譯回伺服器的程式。

>[!NOTE]
>
>如果您想要自訂HTML表單上「HTML數位簽章」按鈕的外觀，您必須變更fscdigsig.css檔案（在adobe-forms-ds.ear > adobe-forms-ds.war檔案中）中的下列屬性：

**.fsc-ds-ssb**:此樣式表適用於空白符號欄位的情況。

**.fsc-ds-ssv**:此樣式表適用於「有效符號」欄位的情況。

**.fsc-ds-ssc**:此樣式表適用於「有效符號」欄位，但資料已變更的情況。

**.fsc-ds-ssi**:此樣式表適用於無效符號欄位的情況。

**.fsc-ds-popup-bg**:不使用此樣式表屬性。

**.fsc-ds-popup-btn**:不使用此樣式表屬性。

## 運行指令碼 {#running-scripts}

表單作者指定指令碼是在伺服器上還是在客戶端上執行。 Forms服務建立分佈式事件處理環境，用於執行表單智慧，該智慧可通過使用屬性在客戶端和伺服器之間分 `runAt` 布。 如需此屬性或在表單設計中建立指令碼的詳細資訊，請參閱 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Forms服務可在呈現表單時執行指令碼。 因此，您可以將資料預先填入表單，方法是將資料連接至資料庫或用戶端上可能無法使用的web services。 您也可以設定在伺服器上執 `Click` 行按鈕的事件，讓用戶端將往返資料傳送至伺服器。 這允許客戶端在用戶與表單交互時運行可能需要伺服器資源（如企業資料庫）的指令碼。 對於HTML表單，表單計算指令碼只能在伺服器上執行。 因此，您必須標籤這些指令碼才能在或 `server` 運行 `both`。

您可以透過呼叫和方法，設計在頁面（面板）之間移動 `xfa.host.pageUp` 的表 `xfa.host.pageDown` 單。 此指令檔會置於按鈕的事 `Click` 件中，而屬 `runAt` 性會設為 `Both`。 您選擇的原 `Both` 因是，讓Adobe Reader或Acrobat（針對以PDF格式轉譯的表單）可以變更頁面，而不需前往伺服器，而HTML表單可以將資料往返於伺服器，以變更頁面。 也就是說，表單會傳送至Forms服務，而表單會呈現為HTML並顯示新頁面。

建議您不要為指令碼變數和表單欄位指定相同的名稱，例如項目。 某些Web瀏覽器（例如Internet Explorer）可能無法初始化與表單欄位同名的變數，而造成指令碼錯誤。 建議您為表單欄位和指令碼變數指定不同的名稱。

在呈現同時包含頁面導覽功能和表單指令碼的HTML表單時（例如，假設指令碼在每次轉譯表單時都會從資料庫擷取欄位資料），請確定表單指令碼位於form:calculate事件中，而非form:readyevent中。

位於form:ready事件中的表單指令碼在表單的初始呈現期間僅執行一次，且不會針對後續的頁面擷取執行。 相反地，會針對每個轉譯表單的頁面導覽執行表單：calculate事件。

>[!NOTE]
在多頁表單中，如果您移至不同的頁面，JavaScript對頁面所做的變更不會保留。

您可以在提交表單之前叫用自訂指令碼。 此功能適用於所有可用的瀏覽器。 不過，只有當使用者轉譯HTML表單時，其屬性才 `Output Type` 能使用它 `Form Body`。 當是時，它將無法 `Output Type` 運作 `Full HTML`。 如需設定此功能的步驟，請參閱管理說明中的設定表單。

您必須先定義回呼函式，在提交表單之前先加以呼叫，其中函式的名稱為 `_user_onsubmit`。 假定該函式不會拋出任何例外，或者如果有，則會忽略該例外。 建議將JavaScript函式置於html的head區段中；但是，您可以在包含的指令碼標籤結束之前的任何地方宣告它 `xfasubset.js`。

當formserver轉譯包含下拉式清單的XDP時，除了建立下拉式清單外，還會建立兩個隱藏的文字欄位。 這些文字欄位會儲存下拉式清單的資料（一個儲存選項的顯示名稱，另一個儲存選項的值）。 因此，每當使用者提交表單時，下拉式清單的整個資料都會提交。 假設您不想每次都提交那麼多資料，您可以編寫自訂指令碼來停用該功能。 例如：下拉式清單的名稱是， `drpOrderedByStateProv` 並會包住子表單標題下。 HTML輸入元素的名稱將為 `header[0].drpOrderedByStateProv[0]`。 儲存並送出下拉式清單資料的隱藏欄位名稱具有以下名稱： `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

如果您不想張貼資料，可以以下列方式停用這些輸入元素。 `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```as3
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```as3
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## XFA子集 {#xfa-subsets}

當建立表單設計以呈現為HTML時，您必須將指令碼限制為XFA子集，以取得javascript語言的指令碼。

在客戶端上運行或在客戶端和伺服器上同時運行的指令碼必須寫入XFA子集。 在伺服器上運行的指令碼可以使用完整的XFA指令碼模型，也可以使用FormCalc。 如需使用JavaScript的詳細資訊，請參 [閱Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

在用戶端上執行指令碼時，只有目前顯示的面板可以使用指令碼；例如，當顯示面板B時，您無法對面板A中的欄位編寫指令碼。 在伺服器上執行指令碼時，可存取所有面板。

在用戶端上執行的指令碼中使用指令碼物件模型(SOM)運算式時，您也必須小心。 在客戶端上運行的指令碼只支援簡化的SOM表達式子集。

## 事件時間 {#event-timing}

XFA子集定義映射至HTML事件的XFA事件。 在計算和驗證事件的時間上，行為略有不同。 在Web瀏覽器中，當您退出欄位時，會執行完整計算事件。 當您變更欄位值時，不會自動執行計算事件。 您可以呼叫方法，強制計算事 `xfa.form.execCalculate` 件。

在Web瀏覽器中，驗證事件僅在退出欄位或送出表格時執行。 您可以使用方法強制驗證事 `xfa.form.execValidate` 件。

在網頁瀏覽器（與Adobe Reader或Acrobat相反）中顯示的表格符合必填欄位的XFA空值測試（錯誤或警告）。

* 如果空測試產生錯誤，而您退出欄位而未指定值，則會顯示訊息方塊，並在按一下「確定」後將您重新定位至欄位。
* 如果空測試產生警告，而您退出欄位而未指定值，系統會提示您按一下「確定」或「取消」，提供不指定值或返回欄位以輸入值的選項。

如需空值測試的詳細資訊，請參閱 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

## 表單按鈕 {#form-buttons}

按一下提交按鈕會傳送表單資料至Forms服務，並代表表單處理結束。 事 `preSubmit` 件可設為在用戶端或伺服器上執行。 如果 `preSubmit` 事件設定為在用戶端上執行，則事件會在表單提交之前執行。 否則，事 `preSubmit` 件會在表單提交期間在伺服器上執行。 如需事件的詳細資 `preSubmit` 訊，請參 [閱Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

如果按鈕沒有與其關聯的用戶端指令碼，則資料會提交至伺服器，並在伺服器上執行計算，然後重新產生HTML表格。 如果按鈕包含用戶端指令碼，資料不會傳送至伺服器，而用戶端指令碼會在網頁瀏覽器中執行。

## HTML 4.0網頁瀏覽器 {#html-4-0-web-browser}

僅支援HTML 4.0的網頁瀏覽器無法支援XFA子集用戶端指令碼模型。 當建立表格設計以便在HTML 4.0和MSDHTML或CSS2HTML中運作時，標示為在用戶端執行的指令碼會實際在伺服器上執行。 例如，假設使用者按了位於HTML 4.0網頁瀏覽器中顯示之表單上的按鈕。 在這種情況下，表單資料會傳送至執行用戶端指令碼的伺服器。

建議您將表單邏輯放入計算事件中，這些事件在HTML 4.0的伺服器上執行，在MSDHTML或CSS2HTML的用戶端上執行。

## 維護簡報變更 {#maintaining-presentation-changes}

當您在HTML頁面（面板）之間移動時，只會保留資料的狀態。 不會保留背景顏色或強制欄位設定等設定（如果與初始設定不同）。 若要維持簡報狀態，您必須建立代表欄位簡報狀態的欄位（通常是隱藏的）。 如果您新增指令碼至欄位事件，並根據隱藏欄位值變更簡報，則當您在HTML頁面（面板）之間來回移動時，可以保留簡報狀態。 `Calculate`

以下指令碼會 `fillColor` 根據的值維護欄位 `hiddenField`。 假設此指令檔位於欄位的事 `Calculate` 件。

```as3
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
當嵌套在表格儲存格內時，靜態物件不會顯示在轉譯的HTML表單中。 例如，嵌套在表格儲存格內的圓形和矩形不會顯示在演算HTML表單內。 但是，這些相同的靜態對象在位於表之外時會正確顯示。

## 數位簽署HTML表格 {#digitally-signing-html-forms}

如果表單呈現為下列HTML轉換，則無法簽署包含數位簽名欄位的HTML表單：

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

如需有關數位簽署檔案的詳細資訊，請參 [閱數位簽署和認證檔案](/help/forms/developing/digitally-signing-certifying-documents.md)

## 呈現符合協助工具方針的XHTML表單 {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

您可以轉換符合協助工具方針的完整HTML表格。 也就是說，表單會呈現在完整HTML標籤中，而非呈現在內文標籤（非完整HTML頁面）中的HTML表單。

## 驗證表單資料 {#validating-form-data}

建議您在將表單轉譯為HTML表單時，限制對表單欄位的驗證規則使用。 HTML表格可能不支援某些驗證規則。 例如，當MM-DD-YYYY的驗證模式套用至表格設計中的欄位（以HTML表格呈現）時，即使日期已正確輸入，它仍無法正常運作。 `Date/Time` 不過，此驗證模式適用於轉譯為PDF的表單。

>[!NOTE]
如需Forms服務的詳細資訊，請參閱「AEM Forms [的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

要渲染HTML表單，請執行以下步驟：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 設定HTML執行時期選項。
1. 演算HTML表格。
1. 將表單資料流寫入用戶端網頁瀏覽器。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

您必須先建立表單資料整合服務用戶端，才能以程式設計方式將資料匯入PDF formClient API。 建立服務客戶端時，您定義調用服務所需的連接設定。

**設定HTML執行時期選項**

您可在轉換HTML表單時設定HTML執行時期選項。 例如，您可以將工具列新增至HTML表格，讓使用者選取位於用戶端電腦上的檔案附件，或擷取使用HTML表格轉譯的檔案附件。 依預設，會停用HTML工具列。 若要將工具列新增至HTML表格，您必須以程式設計方式設定執行時期選項。 依預設，HTML工具列包含下列按鈕：

* `Home`:提供應用程式Web根目錄的連結。
* `Upload`:提供用戶介面以選擇要附加到當前表單的檔案。
* `Download`:提供用於顯示附加檔案的用戶介面。

當HTML工具列出現在HTML表格上時，使用者最多可以選取10個檔案以及表格資料一起提交。 提交檔案後，Forms服務就可以擷取檔案。

將表單轉譯為HTML時，您可以指定使用者代理值。 用戶代理值提供瀏覽器和系統資訊。 這是可選值，您可以傳遞空字串值。 使用Java API快速開始演算HTML表單，說明如何取得使用者代理值，並使用它將表單轉換為HTML。

表單資料張貼位置的HTTP URL可使用Forms Service Client API設定目標URL，或可在XDP表單設計中的「提交」按鈕中指定。 如果在表單設計中指定目標URL，請勿使用Forms Service Client API設定值。

>[!NOTE]
使用工具列轉換HTML表格是選用的。

>[!NOTE]
如果您演算AHTML表格，建議您不要新增工具列至表格。

**轉換HTML表格**

要渲染HTML表單，必須指定在Designer中建立並另存為XDP檔案的表單設計。 您還必須選擇HTML轉換類型。 例如，您可以指定轉換Internet Explorer 5.0或更新版本動態HTML的HTML轉換類型。

轉換HTML表單也需要值，例如轉換其他表單類型所需的URI值。

**將表單資料串流寫入用戶端網頁瀏覽器**

當Forms服務轉譯HTML表單時，它會傳回您必須寫入用戶端網頁瀏覽器的表單資料流。 當寫入用戶端網頁瀏覽器時，使用者會看到HTML表格。

**另請參閱**

[使用Java API將表單轉換為HTML](#render-a-form-as-html-using-the-java-api)

[使用web service API將表單轉換為HTML](#render-a-form-as-html-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉換互動式PDF表單](/help/forms/developing/rendering-interactive-pdf-forms.md)

[使用自訂工具列來轉換HTML表格](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[建立轉譯表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API將表單轉換為HTML {#render-a-form-as-html-using-the-java-api}

使用Forms API(Java)演算HTML表格：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `FormsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 設定HTML執行時期選項

   * 使用其 `HTMLRenderSpec` 建構函式建立物件。
   * 若要使用工具列來轉換HTML表格，請叫 `HTMLRenderSpec` 用物件的方 `setHTMLToolbar` 法並傳遞 `HTMLToolbar` 列舉值。 例如，若要顯示垂直HTML工具列，請傳遞 `HTMLToolbar.Vertical`。
   * 若要設定HTML表單的地區設定值，請叫用 `HTMLRenderSpec` 物件的方 `setLocale` 法，並傳遞指定地區設定值的字串值。 （這是選用設定。）
   * 若要在完整HTML標籤中轉譯HTML表格，請叫 `HTMLRenderSpec` 用物件的方 `setOutputType` 法並傳遞 `OutputType.FullHTMLTags`。 （這是選用設定。）
   >[!NOTE]
   當選項為且引用代管AEM Forms的J2EE應用程式伺服器以外的伺服器( `StandAlone` 值是使用傳遞至物件方法的物件 `true` 來指定)時， `ApplicationWebRoot` HTML中無法成功轉譯 `ApplicationWebRoot` 表 `URLSpec``FormsServiceClient``(Deprecated) renderHTMLForm` 格。 當是 `ApplicationWebRoot` 代管AEM Forms的另一個伺服器時，管理主控台中的Web根URI值必須設定為表單的Web應用程式URI值。 您可登入管理主控台，按一下「服務>表單」，並將Web根URI設為https://server-name:port/FormServer。 然後，儲存您的設定。

1. 轉換HTML表格

   叫用物 `FormsServiceClient` 件的方 `(Deprecated) renderHTMLForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參照屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定 `TransformTo` HTML首選項類型的枚舉值。 例如，若要轉譯與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表格，請指定 `TransformTo.MSDHTML`。
   * 包 `com.adobe.idp.Document` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞空 `com.adobe.idp.Document` 物件。
   * 儲存 `HTMLRenderSpec` HTML執行時期選項的物件。
   * 指定標題值的 `HTTP_USER_AGENT` 字串值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * 存 `URLSpec` 儲呈現HTML表單所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不想將檔案附加到表單。
   該方 `(Deprecated) renderHTMLForm` 法返回包 `FormsResult` 含可寫入客戶端Web瀏覽器的表單資料流的對象。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 通過調 `com.adobe.idp.Document` 用對象的方法 `FormsResult` 建立對 `getOutputContent` 像。
   * 通過調用對象的方 `com.adobe.idp.Document` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `com.adobe.idp.Document` 類型。
   * 呼叫 `javax.servlet.ServletOutputStream` 物件的方法，建立用於將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器的物 `getOutputStream` 件。
   * 調用 `java.io.InputStream` 物件的方 `com.adobe.idp.Document` 法以建立物 `getInputStream` 件。
   * 建立位元組陣列，並借由調用物件的方法並將 `InputStream` 位元組陣列 `read` 傳入為引數，以表單資料流填入。
   * 叫用物 `javax.servlet.ServletOutputStream` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[將表單轉換為HTML](#rendering-forms-as-html)

[快速入門（SOAP模式）:使用Java API轉換HTML表格](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API將表單轉換為HTML {#render-a-form-as-html-using-the-web-service-api}

使用Forms API(web service)演算HTML表格：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立對 `FormsService` 像並設定驗證值。

1. 設定HTML執行時期選項

   * 使用其 `HTMLRenderSpec` 建構函式建立物件。
   * 若要使用工具列來轉換HTML表格，請叫 `HTMLRenderSpec` 用物件的方 `setHTMLToolbar` 法並傳遞 `HTMLToolbar` 列舉值。 例如，若要顯示垂直HTML工具列，請傳遞 `HTMLToolbar.Vertical`。
   * 若要設定HTML表單的地區設定值，請叫用 `HTMLRenderSpec` 物件的方 `setLocale` 法，並傳遞指定地區設定值的字串值。 如需詳細資訊，請參 [閱「AEM Forms API參考」](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 若要在完整HTML標籤中轉譯HTML表格，請叫 `HTMLRenderSpec` 用物件的方 `setOutputType` 法並傳遞 `OutputType.FullHTMLTags`。
   >[!NOTE]
   當選項為且引用代管AEM Forms的J2EE應用程式伺服器以外的伺服器( `StandAlone` 值是使用傳遞至物件方法的物件 `true` 來指定)時， `ApplicationWebRoot` HTML中無法成功轉譯 `ApplicationWebRoot` 表 `URLSpec``FormsServiceClient``(Deprecated) renderHTMLForm` 格。 當是 `ApplicationWebRoot` 代管AEM Forms的另一個伺服器時，管理主控台中的Web根URI值必須設定為表單的Web應用程式URI值。 您可登入管理主控台，按一下「服務>表單」，並將Web根URI設為https://server-name:port/FormServer。 然後，儲存您的設定。

1. 轉換HTML表格

   叫用物 `FormsService` 件的方 `(Deprecated) renderHTMLForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參照屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定 `TransformTo` HTML首選項類型的枚舉值。 例如，若要轉譯與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表格，請指定 `TransformTo.MSDHTML`。
   * 包 `BLOB` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞 `null`。 (請參 [閱使用可排程版面預填表單](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)。)
   * 儲存 `HTMLRenderSpec` HTML執行時期選項的物件。
   * 指定標題值的 `HTTP_USER_AGENT` 字串值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。 如果您不想設定此值，可以傳遞空字串。
   * 存 `URLSpec` 儲呈現HTML表單所需URI值的對象。 (請參 [閱指定URI值](/help/forms/developing/rendering-interactive-pdf-forms.md)。)
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不想將檔案附加到表單。 (請參 [閱將檔案附加至表單](/help/forms/developing/rendering-interactive-pdf-forms.md)。)
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空對象。 此參數值儲存渲染的表單。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空對象。 此參數將儲存輸出的XML資料。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填充的空對象。 此引數將儲存表單中的頁數。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空對象。 此引數將儲存地區值。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空對象。 此引數將儲存所使用的HTML轉換值。
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

[將表單轉換為HTML](#rendering-forms-as-html)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

