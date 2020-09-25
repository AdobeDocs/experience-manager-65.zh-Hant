---
title: 將ContextHub新增至頁面及存取商店
description: 將ContextHub新增至您的頁面，以啟用ContextHub功能並連結至ContextHub Javascript程式庫
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# 將ContextHub新增至頁面及存取商店 {#adding-contexthub-to-pages-and-accessing-stores}

將ContextHub新增至您的頁面，以啟用ContextHub功能並連結至ContextHub Javascript程式庫。

ContextHub Javascript API可讓您存取ContextHub管理的上下文資料。 本頁簡要說明API存取和控制上下文資料的主要功能。 依循API參考檔案的連結，以檢視詳細資訊和程式碼範例。

## 將ContextHub新增至頁面元件 {#adding-contexthub-to-a-page-component}

若要啟用ContextHub功能並連結至ContextHub Javascript程式庫，請在頁 `contexthub` 面的區 `head` 段中加入元件。 頁面元件的HTL程式碼應類似下列範例：

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

請注意，您也需要設定ContextHub工具列是否顯示在「預覽」模式中。 請參 [閱顯示和隱藏ContextHub UI](ch-configuring.md#showing-and-hiding-the-contexthub-ui)。

## 關於ContextHub儲存 {#about-contexthub-stores}

使用ContextHub儲存區來保存上下文資料。 ContextHub提供下列類型的商店，這些商店是所有商店類型的基礎：

* [PeristingStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PeristingJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

所有商店類型都是類別的擴 [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) 充名稱。 如需建立新商店類型的詳細資訊，請參 [閱建立自訂商店](ch-extend.md#creating-custom-store-candidates)。 如需範例商店類型的詳細資訊，請參 [閱範例ContextHub商店候選者](ch-samplestores.md)。

### 持久性模式 {#persistence-modes}

Context Hub儲存區使用下列永續性模式之一：

* **本地：** 使用HTML5 localStorage來保存資料。 本機儲存區會跨作業持續存在於瀏覽器上。
* **會話：** 使用HTML5 sessionStorage來保存資料。 會話儲存在瀏覽器會話期間持續存在，並且可用於所有瀏覽器窗口。
* **Cookie:** 使用瀏覽器對Cookie的原生支援來儲存資料。 在HTTP請求中，Cookie資料會傳送至伺服器或從伺服器傳送。
* **Window.name:** 使用window.name屬性來保存資料。
* **記憶體：** 使用Javascript物件來保存資料。

預設情況下，Context Hub使用本地持久性模式。 如果瀏覽器不支援或允許HTML5 localStorage，則會使用「作業」永續性。 如果瀏覽器不支援或允許HTML5 sessionStorage，則會使用Window.name永續性。

### 存放資料 {#store-data}

在內部，將資料表單儲存為樹結構，以便將值添加為主要類型或複雜對象。 添加複雜對象到儲存時，對象屬性在資料樹中形成分支。 例如，下列複雜物件會新增至名為location的空白商店：

```javascript
Object {
   number: 321,
   data: {
      city: "Basel",
      country: "Switzerland",
      details: {
         population: 173330,
         elevation: 260
      }
   }
}
```

儲存資料的樹結構可概念化如下：

```text
/
|- number
|- data
      |- city
      |- country
      |- details
            |- population
            |- elevation
```

樹結構將儲存中的資料項定義為鍵／值對。 在上例中，鍵與 `/number` 值對應， `321`鍵與 `/data/country` 值對應 `Switzerland`。

### 控制物件 {#manipulating-objects}

ContextHub提供用 [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) 於控制Javascript物件的類別。 在您將Javascript物件新增至商店或從商店取得之前，請使用此類別的函式來控制這些物件。

此外，該類 [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) 還提供了一些函式，用於序列化要素的對象，以及將字串解序列化為對象。 使用此類別來處理JSON資料，以支援原生未包含和函式的瀏 `JSON.parse` 覽 `JSON.stringify` 器。

## 與ContextHub商店互動 {#interacting-with-contexthub-stores}

使用 [`ContextHub`](contexthub-api.md#ui-event-constants) Javascript物件以Javascript物件形式取得商店。 在您取得儲存物件後，就可以控制它包含的資料。 使用 [`getAllStores`](contexthub-api.md#getallstores) 或函 [`getStore`](contexthub-api.md#getstore-name) 數獲取儲存。

### 訪問儲存資料 {#accessing-store-data}

Javascript類 [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) 別會定義數種與儲存資料互動的函式。 下列函式可儲存和擷取物件中包含的多個資料項目：

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

個別資料項目會儲存為一組索引鍵／值配對。 要儲存和檢索值，請指定相應的鍵：

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

請注意，自訂商店申請人可定義其他功能，以提供存取儲存資料的功能。

>[!NOTE]
>
>ContextHub預設不會知道目前登入的發佈伺服器上使用過，且ContextHub會將這些使用者視為「匿名」。
>
>您可以載入描述檔存放區，讓ContextHub得知已登入的使用者。 請參閱 [GitHub上的范常式式碼](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js)。

### ContextHub事件 {#contexthub-eventing}

ContextHub包含事件框架，可讓您自動回應儲存事件。 每個儲存對象都 [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) 包含一個可用作儲存的屬性的對 [`eventing`](contexthub-api.md#eventing) 像。 使用 [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) 或 [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) 函式將Javascript函式系結至商店事件。

## 使用內容中樞操控Cookie {#using-context-hub-to-manipulate-cookies}

Context Hub Javascript API提供跨瀏覽器處理Cookie的支援。 命名空間 [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) 定義了用於建立、控制和刪除Cookie的數個函式。

## 確定已解決的ContextHub區段 {#determining-resolved-contexthub-segments}

ContextHub區段引擎可讓您判斷哪些已註冊區段可在目前的上下文中解決。 使用類別的getResolvedSegments函式 [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) 來擷取已解析的區段。 然後，使用 `getName` 類別 `getPath` 的或 [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) 函式來測試區段。

### ContextHub 區段 {#contexthub-segments}

ContextHub區段會安裝在節 `/conf/<site>/settings/wcm/segments` 點下。

以下區段會隨 [WKND教學課程網站安裝。](getting-started.md)

* 夏季
* 冬

用以解決這些區段的規則概述如下：

* 首先， [地理位置](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) ，儲存區用來判斷使用者的緯度。
* 然後，surferinfo商店的月份資 [料項目](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) ，會決定該緯度的季節。

>[!WARNING]
>
>已安裝的區段會作為參考設定提供，以協助您建立專案專屬的設定，因此不應直接使用。

## 除錯ContextHub {#debugging-contexthub}

ContextHub有許多除錯選項，包括產生記錄檔。 如需詳 [細資訊，請參閱設定ContextHub。](ch-configuring.md#logging-debug-messages-for-contexthub)

## 請參閱ContextHub架構概觀 {#see-an-overview-of-the-contexthub-framework}

ContextHub提供 [診斷頁](ch-diagnostics.md) ，您可在其中查看ContextHub框架的概述。
