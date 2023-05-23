---
title: 自定義Adobe Analytics框架
seo-title: Customizing the Adobe Analytics Framework
description: 自定義Adobe Analytics框架
seo-description: null
uuid: 444a29c2-3b4e-4d21-adc0-5f317ece2b77
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
exl-id: ab0d4f2e-f761-4510-ba51-4a2dcea49601
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1618'
ht-degree: 0%

---

# 自定義Adobe Analytics框架{#customizing-the-adobe-analytics-framework}

Adobe Analytics框架確定與Adobe Analytics一起跟蹤的資訊。 要自定義預設框架，請使用javascript添加自定義跟蹤、整合Adobe Analytics插件以及更改用於跟蹤的框架中的常規設定。

## 關於生成的Javascript for Framework {#about-the-generated-javascript-for-frameworks}

當頁面與Adobe Analytics框架關聯時，該頁面包括 [對分析模組的引用](/help/sites-administering/adobeanalytics.md)，將自動為頁面生成analytics.sitecalst.js檔案。

頁面中的javascript將建立 `s_gi`對象(s_code.jsAdobe Analytics庫定義的對象)，並為其屬性指定值。 對象實例的名稱為 `s`。 本節中提供的代碼示例對此進行了多次引用 `s` 變數。

以下示例代碼與analytics.sitecalyst.js檔案中的代碼類似：

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

使用自定義Javascript代碼自定義框架時，將更改此檔案的內容。

## 配置Adobe Analytics屬性 {#configuring-adobe-analytics-properties}

Adobe Analytics內有許多預定義變數可在框架上配置。 的 **字元集**。 **cookie生存期**。 **currencyCode** 和 **跟蹤InlineStats** 變數包含在 **常規分析設定** 清單。

![aa-22](assets/aa-22.png)

可以將變數名稱和值添加到清單。 這些預定義變數和您添加的任何變數用於配置 `s` analytics.sitecalst.js檔案中的對象。 以下示例說明如何添加 `prop10` 值屬性 `CONSTANT` 表示在javascript代碼中：

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

請按下列步驟將變數添加到清單：

1. 在您的Adobe Analytics框架頁面上，展開 **常規分析設定** 的子菜單。
1. 在變數清單下，按一下添加項以向清單中添加新變數。
1. 在左側單元格中，輸入變數的名稱，例如 `prop10`。

1. 在右側列中，輸入變數的值，例如 `CONSTANT`。

1. 要刪除變數，請按一下變數旁邊的(-)按鈕。

>[!NOTE]
>
>在輸入變數和值時，確保它們的格式和拼寫正確，或 **不會發送呼叫** 值/變數對正確。 拼寫錯誤的變數和值甚至可以阻止調用的發生。
>
>請咨詢您的Adobe Analytics代表，確保正確設定這些變數。

>[!CAUTION]
>
>此清單中的某些變數 **強制** 以便Adobe Analytics的呼叫能夠正常運行(例如 **currencyCode**。 **字元集**)
>
>因此，即使從框架本身刪除這些內容，在進行Adobe Analytics調用時，它們仍會附加一個預設值。

### 將自定義javascript添加到Adobe Analytics框架 {#adding-custom-javascript-to-an-adobe-analytics-framework}

中的自Javascript框 **常規分析設定** 區域可將自定義代碼添加到Adobe Analytics框架。

![aa-21](assets/aa-21.png)

您添加的代碼將附加到analytics.sitecalst.js檔案。 因此，您可以 `s` 變數，它是 `s_gi` 在中定義的javascript對象 `s_code.js`。 例如，添加以下代碼相當於添加名為 `prop10` 值 `CONSTANT`，是上一節中的示例：

`s.prop10= 'CONSTANT';`

中的代碼 [analytics.sitecalyst.js](/help/sites-developing/extending-analytics-components.md) 檔案(包括Adobe Analytics `s-code.js` 檔案)包含以下代碼：

`if (s.usePlugins) s.doPlugins(s)`

以下過程演示了如何使用javascript框自定義Adobe Analytics跟蹤。 如果您的javascript需要使用Adobe Analytics插件， [整合](/help/sites-administering/adobeanalytics.md) 進AEM去。

1. 將以下Javascript代碼添加到框中，以便 `s.doPlugins` 執行：

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >如果要在Adobe Analytics調用中發送變數，而這些變數以某種方式自定義，但無法通過基本拖放介面OR通過Adobe Analytics視圖中的內嵌javascript完成。
   >
   >如果自定義變數在s_doPlugins函式之外，則在Adobe Analytics調用中，它們將作為*undefined *發送

1. 將您的Javascript代碼添加到 **s_do插件** 的子菜單。

以下示例使用公共分隔符「|」按層次順序連接在頁面上捕獲的資料。

Adobe Analytics框架具有以下配置：

* 的 `prop2` Adobe Analytics變數映射到 `pagedata.sitesection` 站點屬性。

* 的 `prop3` Adobe Analytics變數映射到 `pagedata.subsection` 站點屬性。

* 以下代碼將添加到「自由Javascript」框中：

   ```
   s.usePlugins=true;
    function s_doPlugins(s) {
    s.prop1 = s.prop2+'|'+s.prop3;
    }
    s.doPlugins=s_doPlugins;
   ```

* 訪問使用框架的網頁（或在編輯模式下重新載入或預覽頁面）時，將執行對Adobe Analytics的調用。

例如，在Adobe Analytics中生成以下值：

![a-20](assets/aa-20.png)

### 為所有Adobe Analytics框架添加全局自定義代碼 {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

提供整合到所有Adobe Analytics框架的自定義Javascript代碼。 當頁面的Adobe Analytics框架不包含自定義 [自由格式javascript](/help/sites-administering/adobeanalytics.md)，將/libs/cq/analytics/components/sitecatalyst/config.js.jsp指令碼生成的javascript附加到 [analytics.sitecalyst.js](/help/sites-administering/adobeanalytics.md) 的子菜單。 預設情況下，指令碼無效，因為指令碼被注釋掉。 代碼還設定 `s.usePlugins` 至 `false`:

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

analytics.sitecalyst.js檔案(包括Adobe Analyticss_code.js檔案的內容)中的代碼包含以下代碼：

if(s.usePlugins)s.doPlugins

因此，應設定Javascript `s.usePlugins` 至 `true` 所以任何代碼 `s_doPlugins` 函式。 要自定義代碼，請將config.js.jsp檔案與使用您自己的javascript的檔案重疊。 如果您的javascript需要使用Adobe Analytics插件， [整合](/help/sites-administering/adobeanalytics.md) 進AEM去。

>[!NOTE]
>
>不要編輯/libs/cq/analytics/components/sitecatalyst/config.js.jsp檔案。 某些AEM升級或維護任務可以重新安裝原始檔案，刪除您所做的更改。

1. 在CRXDE Lite中，建立/apps/cq/analytics/components資料夾結構：

   1. 按一下右鍵/apps資料夾，然後按一下「建立」>「建立資料夾」。
   1. 指定 `cq` 資料夾名稱，然後按一下「確定」。
   1. 同樣，建立 `analytics` 和 `components` 資料夾。

1. 按一下右鍵 `components` 建立的資料夾，然後按一下「建立」>「建立元件」。 指定以下屬性值：

   * 標籤: `sitecatalyst`
   * 標題: `sitecatalyst`
   * 超級類型: `/libs/cq/analytics/components/sitecatalyst`
   * 群組: `hidden`

1. 重複按一下「Next（下一步）」 ，直到啟用「OK（確定）」按鈕，然後按一下「OK（確定）」。

   sitecalyst元件包含自動建立的sitecalyst.jsp檔案。

1. 按一下右鍵sitecalyst.jsp檔案，然後按一下「刪除」。

1. 按一下右鍵sitecalyst元件，然後按一下「建立」>「建立檔案」。 指定名稱 `config.js.jsp` 然後按一下「OK（確定）」。

   config.js.jsp檔案將自動開啟以供編輯。

1. 將以下文本添加到檔案，然後按一下「全部保存」：

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   /apps/cq/analytics/components/sitecatalyst/config.js.jsp指令碼生成的javascript代碼現在插入analytics.sitecatalst.js檔案中，用於所有使用Adobe Analytics框架的頁。

1. 添加要在中執行的Javascript代碼 `s_doPlugins` ，然後按一下「全部保存」。

>[!CAUTION]
>
>如果頁面框架的自由格式javascript中存在任何文本（甚至僅包含空白），則將忽略config.js.jsp。

### 使用Adobe Analytics插件AEM {#using-adobe-analytics-plugins-in-aem}

獲取Adobe Analytics插件的javascript代碼，並將它們整合到您的Adobe Analytics框架AEM中。 將代碼添加到類別的客戶端庫資料夾中 `sitecatalyst.plugins` 以便它們可用於您的自定義javascript代碼。

例如，如果將 `getQueryParams` 插件，可從 `s_doPlugins` 自定義javascript的函式。 以下示例代碼將查詢字串 **&quot;pid&quot;** 從引用者的URL **eVar1**，當觸發Adobe Analytics呼叫時。

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

安AEM裝以下Adobe Analytics插件，以便預設情況下可用：

* getQueryParam()
* getPreviousValue()
* split()

/libs/cq/analytics/clientlibs/sitecatalyst/plugins客戶端庫資料夾將這些插件包含在sitecalst.plugins類別中。

>[!NOTE]
>
>為插件建立新的客戶端庫資料夾。 不向 `/libs/cq/analytics/clientlibs/sitecatalyst/plugins` 的子菜單。 此練習可確保您對 `sitecatalyst.plugins` 在重新安裝或升級任AEM務期間不會覆蓋類別。

請按下列步驟為插件建立客戶端庫資料夾。 您只需執行一次此過程。 要將插件添加到客戶端庫資料夾，請使用後續過程。

1. 在Web瀏覽器中，開啟CRXDE Lite。 ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. 按一下右鍵/apps/my-app/clientlibs資料夾，然後按一下「建立」>「建立節點」。 輸入以下屬性值，然後按一下確定：

   * 名稱：客戶端庫資料夾的名稱，如my-plugins

   * 類型：cq:ClientLibraryFolder

1. 選擇剛建立的客戶端庫資料夾，然後使用右下方的屬性欄添加以下屬性：

   * 名稱：類別
   * 類型：字串
   * 值：催化劑插件
   * 多：選定

   在「編輯」窗口中按一下「確定」以確認屬性值。

1. 按一下右鍵剛建立的客戶端庫資料夾，然後按一下「建立」>「建立檔案」。 對於檔案名，鍵入js.txt，然後按一下「確定」。

1. 按一下「全部保存」。

請按下列步驟獲取插件代碼，將代碼儲存在存AEM儲庫中，然後將代碼添加到客戶端庫資料夾中。

1. 登錄到 [sc.omniture.com](https://sc.omniture.com) 用你的Adobe Analytics賬戶。
1. 在登錄頁上，轉至「幫助」>「幫助首頁」。
1. 在左側的目錄中，按一下「Implementation Plug-ins（實現插件）」。
1. 按一下要添加的插件的連結，當該頁開啟時，找到插件的Javascript原始碼，然後選擇該代碼並複製它。

1. 按一下右鍵客戶端庫資料夾，然後按一下「建立」>「建立檔案」。 對於檔案名，鍵入要整合的插件的名稱，後跟.js，然後按一下「確定」。 例如，如果要整合getQueryParam插件，請將檔案命名為getQueryParam.js。

   建立檔案時，該檔案將開啟以進行編輯。

1. 將插件Javascript代碼貼上到檔案中，按一下「全部保存」，然後關閉檔案。

1. 從客戶端庫資料夾開啟js.txt檔案。

1. 在新行中，添加包含插件的檔案的名稱，例如getQueryParam.js。 然後，按一下「全部保存」並關閉檔案。

>[!NOTE]
>
>使用插件時，請確保也整合了任何支援插件，否則插件javascript將無法識別它對支援插件中的函式所進行的調用。 例如，getPreviousValue()插件要求split()插件正常運行。
>
>需要將支援插件的名稱添加到 **js.txt** 也是。
