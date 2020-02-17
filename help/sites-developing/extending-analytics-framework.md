---
title: 自訂Adobe Analytics Framework
seo-title: 自訂Adobe Analytics Framework
description: 'null'
seo-description: 'null'
uuid: 444a29c2-3b4e-4d21-adc0-5f317ece2b77
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
translation-type: tm+mt
source-git-commit: 0dc96f07e45ccbfea4edc87431677ada5b1bfa8c

---


# 自訂Adobe Analytics Framework{#customizing-the-adobe-analytics-framework}

Adobe Analytics架構會決定使用Adobe Analytics追蹤的資訊。 若要自訂預設架構，請使用javascript來新增自訂追蹤、整合Adobe Analytics外掛程式，以及變更用於追蹤的架構內的一般設定。

## 關於產生的Javascript for Frameworks {#about-the-generated-javascript-for-frameworks}

當頁面與Adobe Analytics架構關聯，且頁面包含 [Analytics模組的參考時](/help/sites-administering/adobeanalytics.md)，會自動為頁面產生analytics.sitecatalyst.js檔案。

頁面中的javascript會建立 `s_gi`物件（s_code.js Adobe Analytics程式庫所定義的物件），並指派值給其屬性。 對象實例的名稱為 `s`。 本節中顯示的程式碼範例會參照此變數的多 `s` 個。

下列范常式式碼與analytics.sitecatalyst.js檔案中的程式碼類似：

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";

/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

當您使用自訂Javascript程式碼自訂架構時，您會變更此檔案的內容。

## 設定Adobe Analytics屬性 {#configuring-adobe-analytics-properties}

Adobe Analytics中有許多預先定義的變數，可在架構上設定。 預設 **情況下**,Charset **、** CookieLifetime **、** currencyInline ******** 和trackInline變數會納入General Analytics設定清單中。

![aa-22](assets/aa-22.png)

您可以新增變數名稱和值至清單。 這些預先定義的變數和您新增的任何變數，會用來設定analytics.sitecatalyst.js `s` 檔案中物件的屬性。 下列範例說明如何在javascript `prop10` 程式碼中 `CONSTANT` 呈現新增的值屬性：

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.prop10= 'CONSTANT';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";
```

請按下列步驟將變數新增至清單：

1. 在Adobe Analytics架構頁面上，展開「一般 **分析設定** 」區域。
1. 在變數清單下方，按一下「新增項目」，將新變數新增至清單。
1. 在左側儲存格中，輸入變數的名稱，例如 `prop10`。

1. 在右側欄中，輸入變數的值，例如 `CONSTANT`。

1. 若要移除變數，請按一下變數旁的(-)按鈕。

>[!NOTE]
>
>輸入變數和值時，請確定其格式正確且拼寫正確，否 **則呼叫不會隨正確的值** /變數對傳送。 拼錯的變數和值甚至可防止呼叫發生。
>
>請洽詢您的Adobe Analytics代表，以確定這些變數已正確設定。

>[!CAUTION]
>
>此清單中的某些變數是必 **備的** ,Adobe Analytics呼叫才能正常運作(例如 **currencyCode**, **charSet**)
>
>因此，即使從架構本身移除，在進行Adobe Analytics呼叫時，仍會附加預設值。

### 新增自訂javascript至Adobe Analytics Framework {#adding-custom-javascript-to-an-adobe-analytics-framework}

「一般分析設定」區域中的免 **費javascript方塊** ，可讓您將自訂代碼新增至Adobe Analytics架構。

![aa-21](assets/aa-21.png)

您新增的程式碼會附加至analytics.sitecatalyst.js檔案。 因此，您可以存 `s` 取變數，此變數是中定義之 `s_gi` javascript物件的例項 `s_code.js`。 例如，新增下列程式碼等同於新增名為 `prop10` 值 `CONSTANT`的變數，這是上一節的範例：

`s.prop10= 'CONSTANT';`

analytics.sitecatalyst.js檔 [案中的程式碼](/help/sites-developing/extending-analytics-components.md) （包含Adobe Analytics檔案的內容）包含 `s-code.js` 下列程式碼：

`if (s.usePlugins) s.doPlugins(s)`

下列程式示範如何使用javascript方塊來自訂Adobe Analytics追蹤。 如果您的javascript需要使用Adobe Analytics外掛程式，請將 [它們整合](/help/sites-administering/adobeanalytics.md) 至AEM。

1. 將下列javascript程式碼新增至方塊，以便 `s.doPlugins` 執行：

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >如果您想要在Adobe Analytics呼叫中傳送變數，而Adobe Analytics呼叫中的變數已以某種方式自訂，但無法透過基本拖放介面OR透過Adobe Analytics檢視中的內嵌javascript來完成，則需使用此程式碼。
   >
   >如果自訂變數不在s_doPlugins函式外，則在Adobe Analytics呼叫中會以*undefined *傳送這些變數

1. 在 **s_doPlugins函式中新增您的javascript程式碼** 。

下列範例使用共用分隔符號&quot;|&quot;，以階層順序串連在頁面上擷取的資料。

Adobe Analytics架構具有下列設定：

* Adobe `prop2` Analytics變數會對應至網站 `pagedata.sitesection` 屬性。

* Adobe `prop3` Analytics變數會對應至網站 `pagedata.subsection` 屬性。

* 下列程式碼會新增至free-from javascript方塊：

   ```
   s.usePlugins=true;
    function s_doPlugins(s) {
    s.prop1 = s.prop2+'|'+s.prop3;
    }
    s.doPlugins=s_doPlugins;
   ```

* 當瀏覽使用架構的網頁（或在編輯模式中重新載入或預覽頁面）時，會執行對Adobe Analytics的呼叫。

例如，Adobe Analytics會產生下列值：

![aa-20](assets/aa-20.png)

### 新增所有Adobe Analytics架構的全域自訂程式碼 {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

提供整合至所有Adobe Analytics架構的自訂Javascript程式碼。 當頁面的Adobe Analytics架構不含自訂的 [自由格式javascript](/help/sites-administering/adobeanalytics.md),/libs/cq/analytics/components/sitecatalyst/config.js.jsp指令碼產生的javascript會附加至 [](/help/sites-administering/adobeanalytics.md) analytics.sitecatalyst.js檔案。 依預設，指令碼沒有作用，因為它已加上註解。 程式碼也設 `s.usePlugins` 定 `false`為：

```
/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

analytics.sitecatalyst.js檔案中的程式碼（包含Adobe Analytics s_code.js檔案的內容）包含下列程式碼：

if(s.usePlugins)s.doPlugins(s)

因此，您的javascript應設 `s.usePlugins` 定為 `true` 執行函式中的 `s_doPlugins` 任何程式碼。 若要自訂程式碼，請使用您自己的javascript來覆蓋config.js.jsp檔案。 如果您的javascript需要使用Adobe Analytics外掛程式，請將 [它們整合](/help/sites-administering/adobeanalytics.md) 至AEM。

>[!NOTE]
>
>請勿編輯/libs/cq/analytics/components/sitecatalyst/config.js.jsp檔案。 某些AEM升級或維護工作可以重新安裝原始檔案，移除您所做的變更。

1. 在CRXDE Lite中，建立/apps/cq/analytics/components檔案夾結構：

   1. 以滑鼠右鍵按一下/apps檔案夾，然後按一下「建立>建立檔案夾」。
   1. 指定 `cq` 為資料夾名稱，然後按一下「確定」。
   1. 同樣地，請建立 `analytics` 和資 `components` 料夾。

1. 按一下右鍵剛建立的 `components` 資料夾，然後按一下「建立」(Create)>「建立元件」(Create Component)。 指定下列屬性值：

   * 標籤: `sitecatalyst`
   * 標題: `sitecatalyst`
   * 超級類型: `/libs/cq/analytics/components/sitecatalyst`
   * 群組: `hidden`

1. 重複按一下「Next（下一步）」 ，直到啟用「OK（確定）」按鈕，然後按一下「OK（確定）」。

   sitecatalyst元件包含自動建立的sitecatalyst.jsp檔案。

1. 以滑鼠右鍵按一下sitecatalyst.jsp檔案，然後按一下「刪除」。

1. 以滑鼠右鍵按一下sitecatalyst元件，然後按一下「建立>建立檔案」。 指定名稱， `config.js.jsp` 然後按一下「確定」。

   config.js.jsp檔案會自動開啟以供編輯。

1. 將下列文字新增至檔案，然後按一下「全部儲存」:

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   /apps/cq/analytics/components/sitecatalyst/config.js.jsp指令碼產生的javascript程式碼現在會插入使用Adobe Analytics架構的所有頁面的analytics.sitecatalyst.js檔案。

1. 新增您要在函式中執行的Javascript程式碼，然後按一 `s_doPlugins` 下「全部儲存」。

>[!CAUTION]
>
>如果頁面架構的自由格式javascript中有任何文字（甚至僅限空白字元），則會忽略config.js.jsp。

### 在AEM中使用Adobe Analytics外掛程式 {#using-adobe-analytics-plugins-in-aem}

取得Adobe Analytics外掛程式的javascript程式碼，並將它們整合在AEM的Adobe Analytics架構中。 將程式碼新增至類別的用戶端程式庫資料夾， `sitecatalyst.plugins` 以便自訂javascript程式碼可使用這些程式碼。

例如，如果您整合外掛程 `getQueryParams` 式，則可從自訂javascript的函式 `s_doPlugins` 呼叫外掛程式。 當觸發Adobe Analytics呼叫時，下列范常式式碼 **會從反向連結的URL將查詢字串「pid」** ( **pid**)傳送為eVar1。

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM會安裝下列Adobe Analytics外掛程式，以便依預設提供：

* getQueryParam()
* getPreviousValue()
* split()

/libs/cq/analytics/clientlibs/sitecatalyst/plugins用戶端程式庫資料夾會將這些外掛程式包含在sitecatalyst.plugins類別中。

>[!NOTE]
>
>為外掛程式建立新的用戶端程式庫資料夾。 請勿將外掛程式新增至資 `/libs/cq/analytics/clientlibs/sitecatalyst/plugins` 料夾。 此做法可確保您在AEM重新安裝 `sitecatalyst.plugins` 或升級工作期間不會覆寫您對類別的貢獻。

請按下列步驟為外掛程式建立用戶端程式庫資料夾。 您只需執行此程式一次。 若要將外掛程式新增至用戶端程式庫資料夾，請使用後續的程式。

1. 在網頁瀏覽器中，開啟CRXDE Lite。 ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. 按一下右鍵/apps/my-app/clientlibs資料夾，然後按一下「建立」>「建立節點」。 輸入以下屬性值，然後按一下「確定」:

   * 名稱：用戶端程式庫資料夾的名稱，例如my-plugins

   * 類型：cq:ClientLibraryFolder

1. 選取您剛建立的用戶端程式庫資料夾，並使用右下方的屬性列來新增下列屬性：

   * 名稱：類別
   * 類型：字串
   * 值：sitecatalyst.plugins
   * 多重：已選取
   在「編輯」窗口中按一下「確定」以確認屬性值。

1. 按一下右鍵剛建立的客戶端庫資料夾，然後按一下「建立」>「建立檔案」。 對於檔案名稱，請輸入js.txt，然後按一下「確定」。

1. 按一下「全部儲存」。

請依照下列程式來取得外掛程式程式碼、將程式碼儲存在AEM儲存庫中，並將程式碼新增至您的用戶端程式庫檔案夾。

1. 使用您 [的Adobe Analytics帳戶登入sc.omniture](https://sc.omniture.com) .com。
1. 在登陸頁面上，請至「說明>說明首頁」。
1. 在左側的目錄中，按一下「實施外掛程式」。
1. 按一下您要新增的外掛程式連結，當頁面開啟時，找出外掛程式的javascript原始碼，然後選取程式碼並加以複製。

1. 在用戶端程式庫資料夾上按一下滑鼠右鍵，然後按一下「建立>建立檔案」。 對於檔案名稱，輸入您要整合的外掛程式名稱，後面接著。js，然後按一下「確定」。 例如，如果您要整合getQueryParam外掛程式，請為檔案命名getQueryParam.js。

   當您建立檔案時，檔案會開啟以供編輯。

1. 將外掛程式javascript程式碼貼入檔案中，按一下「全部儲存」，然後關閉檔案。

1. 從用戶端程式庫資料夾開啟js.txt檔案。

1. 在新行中，新增包含外掛程式的檔案名稱，例如getQueryParam.js。 然後，按一下「全部儲存」並關閉檔案。

>[!NOTE]
>
>使用外掛程式時，請確定也整合任何支援外掛程式，否則外掛程式javascript將無法識別它對支援外掛程式中函式所進行的呼叫。 例如，getPreviousValue()外掛程式需要split()外掛程式才能正常運作。
>
>支援外掛程式的名稱也需要新 **增至js.txt** 。
