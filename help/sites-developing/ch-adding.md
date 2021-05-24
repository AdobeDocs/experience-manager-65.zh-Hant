---
title: 新增ContextHub至頁面及存取商店
description: 將ContextHub新增至您的頁面以啟用ContextHub功能並連結至ContextHub Javascript資料庫
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 將ContextHub新增至頁面並存取儲存{#adding-contexthub-to-pages-and-accessing-stores}

將ContextHub新增至您的頁面以啟用ContextHub功能並連結至ContextHub Javascript資料庫。

ContextHub Javascript API可讓您存取ContextHub管理的內容資料。 本頁簡要說明API存取及控制內容資料的主要功能。 請依照API參考檔案的連結，查看詳細資訊和程式碼範例。

## 將ContextHub新增至頁面元件{#adding-contexthub-to-a-page-component}

若要啟用ContextHub功能並連結至ContextHub Javascript程式庫，請在頁面的`head`區段中加入`contexthub`元件。 您頁面元件的HTL程式碼應類似下列範例：

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

請注意，您也需要設定ContextHub工具列是否顯示在「預覽」模式中。 請參閱[顯示和隱藏ContextHub UI](ch-configuring.md#showing-and-hiding-the-contexthub-ui)。

## 關於ContextHub儲存{#about-contexthub-stores}

使用ContextHub存放區來保留內容資料。 ContextHub提供下列儲存類型，這些儲存類型構成所有儲存類型的基礎：

* [PerisentStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PerisentJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

所有儲存類型都是[`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core)類的副檔名。 有關建立新商店類型的資訊，請參閱[建立自定義商店](ch-extend.md#creating-custom-store-candidates)。 如需範例存放區類型的相關資訊，請參閱[範例ContextHub存放區候選項](ch-samplestores.md)。

### 持久性模式{#persistence-modes}

Context Hub存放區使用下列其中一種持續性模式：

* **本機：** 使用HTML5 localStorage來保存資料。本機儲存會跨工作階段保存在瀏覽器上。
* **工作階段：** 使用HTML5 sessionStorage來保存資料。工作階段儲存在瀏覽器工作階段期間持續存在，且可供所有瀏覽器視窗使用。
* **Cookie:** 使用瀏覽器對資料儲存Cookie的原生支援。Cookie資料會在HTTP要求中傳送至伺服器，或從伺服器傳送。
* **Window.name:** 使用window.name屬性來保存資料。
* **記憶體：** 使用Javascript物件來保存資料。

預設情況下，Context Hub使用本地持久性模式。 如果瀏覽器不支援或允許HTML5 localStorage，則會使用工作階段持續性。 如果瀏覽器不支援或允許HTML5 sessionStorage，則會使用Window.name持續性。

### 存放資料 {#store-data}

在內部，將資料儲存為樹結構，以便將值添加為主要類型或複雜對象。 添加要儲存的複雜對象時，對象屬性在資料樹中形成分支。 例如，下列複雜物件會新增至名為位置的空白存放區：

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

儲存資料的樹狀結構可概念化如下：

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

樹結構將儲存中的資料項目定義為索引鍵/值組。 在上例中，鍵`/number`與值`321`對應，鍵`/data/country`與值`Switzerland`對應。

### 操作對象{#manipulating-objects}

ContextHub提供[`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree)類別，用於操作Javascript對象。 在將Javascript對象添加到儲存區之前，或在從儲存區獲取Javascript對象之後，使用此類的函式。

此外，[`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json)類還提供了將對象序列化為字串，並將字串反序列化為對象的函式。 使用此類別處理JSON資料，以支援原生不包含`JSON.parse`和`JSON.stringify`函式的瀏覽器。

## 與ContextHub商店互動{#interacting-with-contexthub-stores}

使用[`ContextHub`](contexthub-api.md#ui-event-constants) Javascript物件來取得儲存作為Javascript物件。 取得儲存物件後，您就可以控制其包含的資料。 使用[`getAllStores`](contexthub-api.md#getallstores)或[`getStore`](contexthub-api.md#getstore-name)函式來取得存放區。

### 訪問儲存資料{#accessing-store-data}

[`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) Javascript類定義了與儲存資料交互的多個函式。 以下函式儲存和檢索對象中包含的多個資料項：

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

個別資料項目會儲存為一組索引鍵/值組。 要儲存和檢索值，請指定相應的鍵：

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

請注意，自訂存放區候選項可定義其他功能，以提供存取儲存資料的權限。

>[!NOTE]
>
>ContextHub預設不會知道目前在發佈伺服器上使用的登入，且ContextHub會將這類使用者視為「匿名」。
>
>您可以載入設定檔存放區，讓ContextHub得知已登入的使用者。 請在此處](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js)參閱GitHub上的[范常式式碼。

### ContextHub事件{#contexthub-eventing}

ContextHub包含事件架構，可讓您自動回應以儲存事件。 每個儲存對象都包含一個[`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing)對象，該對象可用作儲存的[`eventing`](contexthub-api.md#eventing)屬性。 使用[`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents)或[`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents)函式將Javascript函式系結至儲存事件。

## 使用內容中樞來操控Cookie {#using-context-hub-to-manipulate-cookies}

Context Hub Javascript API提供跨瀏覽器支援，可處理瀏覽器Cookie。 [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie)命名空間定義了用於建立、操作和刪除Cookie的多個函式。

## 確定解析的ContextHub區段{#determining-resolved-contexthub-segments}

ContextHub區段引擎可讓您判斷目前內容中要解析的已註冊區段。 使用[`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager)類的getResolvedSegments函式來檢索已解析的段。 然後，使用[`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment)類的`getName`或`getPath`函式來測試段。

### ContextHub 區段 {#contexthub-segments}

ContextHub區段會安裝在`/conf/<site>/settings/wcm/segments`節點下。

下列區段隨[WKND教學課程網站一起安裝。](getting-started.md)

* 夏季
* 冬季

用以解決這些區段的規則摘要如下：

* 首先，使用[geolocation](ch-samplestores.md#contexthub-geolocation-sample-store-candidate)商店來判斷使用者的緯度。
* 然後，[surferinfo商店](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate)的月份資料項決定該緯度的季數。

>[!WARNING]
>
>安裝的區段會作為參考設定提供，協助您為專案建立專屬的設定，因此不應直接使用。

## 調試ContextHub {#debugging-contexthub}

有許多選項可用來偵錯ContextHub，包括產生記錄檔。 如需詳細資訊，請參閱[設定ContextHub 。](ch-configuring.md#logging-debug-messages-for-contexthub)

## 請參閱ContextHub架構概述{#see-an-overview-of-the-contexthub-framework}

ContextHub提供[診斷頁面](ch-diagnostics.md) ，您可在其中看到ContextHub架構的概觀。
