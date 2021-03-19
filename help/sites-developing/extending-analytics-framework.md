---
title: 定制Adobe Analytics框架
seo-title: 定制Adobe Analytics框架
description: 定制Adobe Analytics框架
seo-description: 'null'
uuid: 444a29c2-3b4e-4d21-adc0-5f317ece2b77
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 0%

---


# 自定義Adobe Analytics框架{#customizing-the-adobe-analytics-framework}

Adobe Analytics框架決定了Adobe Analytics所跟蹤的資訊。 若要自訂預設架構，請使用javascript來新增自訂追蹤、整合Adobe Analytics外掛程式，以及變更用於追蹤的架構內的一般設定。

## 關於為架構{#about-the-generated-javascript-for-frameworks}產生的javascript

當頁面與Adobe Analytics架構相關聯，且頁面包含對Analytics模組](/help/sites-administering/adobeanalytics.md)的[參考時，會自動為頁面產生analytics.sitecatalyst.js檔案。

頁面中的javascript會建立`s_gi`物件(s_code.jsAdobe Analytics程式庫所定義)，並指派值給其屬性。 對象實例的名稱為`s`。 本節中顯示的程式碼範例會參照此`s`變數。

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

## 配置Adobe Analytics屬性{#configuring-adobe-analytics-properties}

Adobe Analytics內有許多預先定義的變數可在架構上設定。 預設會將&#x200B;**charset**、**cookieLifetime**、**currencyCode**&#x200B;和&#x200B;**trackInlineStats**&#x200B;變數包含在「一般分析設定&#x200B;**」清單中。**

![aa-22](assets/aa-22.png)

您可以新增變數名稱和值至清單。 這些預先定義的變數和您新增的任何變數可用來設定analytics.sitecatalyst.js檔案中`s`物件的屬性。 下列範例說明在javascript程式碼中如何呈現值`CONSTANT`的新增`prop10`屬性：

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

1. 在您的Adobe Analytics框架頁面上，展開「一般分析設定」區域。****
1. 在變數清單下方，按一下「新增項目」，將新變數新增至清單。
1. 在左側儲存格中，輸入變數的名稱，例如`prop10`。

1. 在右側欄中，輸入變數的值，例如`CONSTANT`。

1. 若要移除變數，請按一下變數旁的(-)按鈕。

>[!NOTE]
>
>輸入變數和值時，請確定其格式正確且拼字正確，或&#x200B;**呼叫不會以正確的值／變數對傳送。**&#x200B;拼錯的變數和值甚至可防止呼叫發生。
>
>請洽詢您的Adobe Analytics代表，以確定這些變數已正確設定。

>[!CAUTION]
>
>此清單中的某些變數為&#x200B;**mandatory**，以讓Adobe Analytics呼叫正常運作(例如&#x200B;**currencyCode**, **charSet**)
>
>因此，即使從框架本身移除它們，在進行Adobe Analytics調用時，它們仍將附加一個預設值。

### 新增自訂javascript至Adobe Analytics架構{#adding-custom-javascript-to-an-adobe-analytics-framework}

**一般分析設定**&#x200B;區域中的free-from javascript方塊可讓您將自訂代碼新增至Adobe Analytics架構。

![aa-21](assets/aa-21.png)

您新增的程式碼會附加至analytics.sitecatalyst.js檔案。 因此，您可以訪問`s`變數，該變數是`s_code.js`中定義的`s_gi`javascript對象的實例。 例如，新增下列程式碼等同於新增值`CONSTANT`的`prop10`變數，這是上一節的範例：

`s.prop10= 'CONSTANT';`

[analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md)檔案(包含Adobe Analytics`s-code.js`檔案的內容)中的程式碼包含下列程式碼：

`if (s.usePlugins) s.doPlugins(s)`

下列程式示範如何使用javascript方塊來自訂Adobe Analytics追蹤。 如果您的javascript需要使用Adobe Analytics外掛程式，請[將它們](/help/sites-administering/adobeanalytics.md)整合至AEM。

1. 將下列javascript程式碼新增至方塊，以便執行`s.doPlugins`:

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >如果您想要在Adobe Analytics呼叫中傳送變數，而這些變數是以某種方式自訂，無法透過基本拖放介面OR透過Adobe Analytics檢視的內嵌javascript來完成，則此程式碼是必要的。
   >
   >如果自訂變數不在s_doPlugins函式外，則在Adobe Analytics呼叫中會以*undefined *傳送這些變數

1. 在&#x200B;**s_doPlugins**&#x200B;函式中新增您的javascript程式碼。

下列範例使用共用分隔符號&quot;|&quot;，以階層順序串連在頁面上擷取的資料。

Adobe Analytics框架具有以下配置：

* `prop2`Adobe Analytics變數會對應至`pagedata.sitesection`網站屬性。

* `prop3`Adobe Analytics變數會對應至`pagedata.subsection`網站屬性。

* 下列程式碼會新增至free-from javascript方塊：

   ```
   s.usePlugins=true;
    function s_doPlugins(s) {
    s.prop1 = s.prop2+'|'+s.prop3;
    }
    s.doPlugins=s_doPlugins;
   ```

* 當瀏覽使用框架的網頁時（或在編輯模式中重新載入或預覽頁面），將執行對Adobe Analytics的呼叫。

例如，下列值會在Adobe Analytics產生：

![aa-20](assets/aa-20.png)

### 為所有Adobe Analytics框架添加全局自定義代碼{#adding-global-custom-code-for-all-adobe-analytics-frameworks}

提供整合在所有Adobe Analytics架構中的自訂Javascript程式碼。 當頁面的Adobe Analytics架構不含自訂[自由格式javascript](/help/sites-administering/adobeanalytics.md)時，/libs/cq/analytics/components/sitecatalyst/config.js.jsp指令碼產生的javascript會附加至[analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md)檔案。 依預設，指令碼沒有作用，因為它已加上註解。 代碼還將`s.usePlugins`設定為`false` :

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

analytics.sitecatalyst.js檔案(包含Adobe Analyticss_code.js檔案的內容)中的程式碼包含下列程式碼：

if(s.usePlugins)s.doPlugins(s)

因此，您的javascript應將`s.usePlugins`設為`true`，以便執行`s_doPlugins`函式中的任何程式碼。 若要自訂程式碼，請使用您自己的javascript來覆蓋config.js.jsp檔案。 如果您的javascript需要使用Adobe Analytics外掛程式，請[將它們](/help/sites-administering/adobeanalytics.md)整合至AEM。

>[!NOTE]
>
>請勿編輯/libs/cq/analytics/components/sitecatalyst/config.js.jsp檔案。 某些AEM升級或維護任務可以重新安裝原始檔案，刪除您的更改。

1. 在CRXDE Lite中，建立/apps/cq/analytics/components檔案夾結構：

   1. 以滑鼠右鍵按一下/apps檔案夾，然後按一下「建立>建立檔案夾」。
   1. 指定`cq`作為資料夾名稱，然後按一下「確定」。
   1. 同樣地，請建立`analytics`和`components`資料夾。

1. 按一下右鍵剛建立的`components`資料夾，然後按一下「建立」>「建立元件」。 指定下列屬性值：

   * 標籤: `sitecatalyst`
   * 標題: `sitecatalyst`
   * 超級類型: `/libs/cq/analytics/components/sitecatalyst`
   * 群組: `hidden`

1. 重複按一下「Next（下一步）」 ，直到啟用「OK（確定）」按鈕，然後按一下「OK（確定）」。

   sitecatalyst元件包含自動建立的sitecatalyst.jsp檔案。

1. 以滑鼠右鍵按一下sitecatalyst.jsp檔案，然後按一下「刪除」。

1. 以滑鼠右鍵按一下sitecatalyst元件，然後按一下「建立>建立檔案」。 指定名稱`config.js.jsp`，然後按一下「確定」。

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

1. 在`s_doPlugins`函式中新增您要執行的javascript程式碼，然後按一下「全部儲存」。

>[!CAUTION]
>
>如果頁面架構的自由格式javascript中有任何文字（甚至僅限空白字元），則會忽略config.js.jsp。

### 在AEM{#using-adobe-analytics-plugins-in-aem}中使用Adobe Analytics插件

取得Adobe Analytics外掛程式的javascript程式碼，並將它們整合至您的Adobe Analytics架構AEM。 將程式碼新增至`sitecatalyst.plugins`類別的用戶端程式庫資料夾，以便自訂javascript程式碼可使用。

例如，如果您整合`getQueryParams`外掛程式，則可從自訂javascript的`s_doPlugins`函式呼叫外掛程式。 當觸發Adobe Analytics呼叫時，下列范常式式碼會從反向連結的URL傳送&#x200B;**&quot;pid&quot;**&#x200B;中的查詢字串，作為&#x200B;**eVar1**。

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

安AEM裝下列Adobe Analytics插件，以便預設使用它們：

* getQueryParam()
* getPreviousValue()
* split()

/libs/cq/analytics/clientlibs/sitecatalyst/plugins用戶端程式庫資料夾會將這些外掛程式包含在sitecatalyst.plugins類別中。

>[!NOTE]
>
>為外掛程式建立新的用戶端程式庫資料夾。 請勿將外掛程式新增至`/libs/cq/analytics/clientlibs/sitecatalyst/plugins`資料夾。 此做法可確保在重新安裝或升級任務期間不會覆寫您對`sitecatalyst.plugins`類AEM別的貢獻。

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

請按下列步驟獲取插件代碼、將代碼儲存在儲存庫AEM中，並將代碼添加到客戶端庫資料夾中。

1. 使用您的Adobe Analytics帳戶登入[sc.omniture.com](https://sc.omniture.com)。
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
>支援外掛程式的名稱也需要新增至&#x200B;**js.txt**。
