---
title: 將ContextHub添加到頁面和訪問儲存
description: 將ContextHub添加到您的頁面以啟用ContextHub功能並連結到ContextHub Javascript庫
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 將ContextHub添加到頁面和訪問儲存 {#adding-contexthub-to-pages-and-accessing-stores}

將ContextHub添加到您的頁面以啟用ContextHub功能並連結到ContextHub Javascript庫。

ContextHub Javascript API提供對ContextHub管理的上下文資料的訪問。 本頁簡要介紹了用於訪問和操作上下文資料的API的主要功能。 按照指向API參考文檔的連結查看詳細資訊和代碼示例。

## 將ContextHub添加到頁面元件 {#adding-contexthub-to-a-page-component}

要啟用ContextHub功能並連結到ContextHub Javascript庫，請包括 `contexthub` 元件 `head` 的子菜單。 頁面元件的HTL代碼應與以下示例類似：

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

請注意，您還需要配置ContextHub工具欄是否顯示在「預覽」模式下。 請參閱 [顯示和隱藏ContextHub UI](ch-configuring.md#showing-and-hiding-the-contexthub-ui)。

## 關於ContextHub儲存 {#about-contexthub-stores}

使用ContextHub儲存保留上下文資料。 ContextHub提供以下類型的儲存，這些儲存構成了所有儲存類型的基礎：

* [持久儲存](contexthub-api.md#contexthub-store-persistedstore)
* [會話儲存](contexthub-api.md#contexthub-store-sessionstore)
* [瓊普斯托雷](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [永續JSONPStore](contexthub-api.md#contexthub-store-persistedstore)

所有儲存類型都是 [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) 類。 有關建立新儲存類型的資訊，請參見 [建立自定義儲存](ch-extend.md#creating-custom-store-candidates)。 有關示例儲存類型的資訊，請參見 [示例ContextHub儲存候選](ch-samplestores.md)。

### 持久性模式 {#persistence-modes}

上下文中心儲存使用以下持久性模式之一：

* **本地：** 使用HTML5 localStorage保留資料。 本地儲存在瀏覽器上跨會話永續。
* **會話：** 使用HTML5 sessionStorage保留資料。 會話儲存在瀏覽器會話的持續時間內被保留，並且可用於所有瀏覽器窗口。
* **Cookie:** 使用瀏覽器對Cookie的本機支援來儲存資料。 在HTTP請求中，Cookie資料會發送到伺服器並從伺服器發送。
* **Window.name:** 使用window.name屬性保留資料。
* **記憶體：** 使用Javascript對象保留資料。

預設情況下，上下文中心使用本地持久性模式。 如果瀏覽器不支援或允許HTML5 localStorage，則使用會話持久性。 如果瀏覽器不支援或允許HTML5sessionStorage，則使用Window.name持久性。

### 存放資料 {#store-data}

在內部，儲存資料形成樹結構，使值能夠添加為主要類型或複雜對象。 將複雜對象添加到儲存時，對象屬性會在資料樹中形成分支。 例如，以下複雜對象將添加到名為location的空儲存中：

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

儲存資料的樹結構可以概念化為：

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

樹結構將儲存中的資料項定義為鍵/值對。 在上例中，鍵 `/number` 與值對應 `321`，以及鍵 `/data/country` 與值對應 `Switzerland`。

### 操作對象 {#manipulating-objects}

ContextHub提供 [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) 用於操作Javascript對象的類。 在將Javascript對象添加到儲存或從儲存獲取這些對象之前，請使用此類的函式來操作它們。

此外， [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) 類提供了將對象序列化為stings和將字串反序列化為對象的函式。 使用此類處理JSON資料以支援本機不包含的瀏覽器 `JSON.parse` 和 `JSON.stringify` 的子菜單。

## 與ContextHub儲存交互 {#interacting-with-contexthub-stores}

使用 [`ContextHub`](contexthub-api.md#ui-event-constants) Javascript對象以Javascript對象形式獲取儲存。 獲得儲存對象後，您就可以處理它包含的資料。 使用 [`getAllStores`](contexthub-api.md#getallstores) 或 [`getStore`](contexthub-api.md#getstore-name) 函式獲取儲存區。

### 訪問儲存資料 {#accessing-store-data}

的 [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) Javascript類定義了幾個用於與儲存資料交互的函式。 以下函式儲存和檢索對象中包含的多個資料項：

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

單個資料項被儲存為一組鍵/值對。 要儲存和檢索值，請指定相應的鍵：

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

請注意，自定義儲存候選項可以定義其他功能，以提供對儲存資料的訪問。

>[!NOTE]
>
>預設情況下，ContextHub不知道當前登錄在發佈伺服器上使用的用戶，ContextHub將這些用戶視為「匿名」。
>
>通過載入配置檔案儲存，可以使ContextHub瞭解登錄的用戶。 請參閱 [此處GitHub上的示例代碼](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js)。

### ContextHub事件 {#contexthub-eventing}

ContextHub包含一個事件框架，使您能夠自動對儲存事件做出反應。 每個儲存對象都包含 [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) 可用作商店的 [`eventing`](contexthub-api.md#eventing) 屬性。 使用 [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) 或 [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) 函式將Javascript函式綁定到儲存事件。

## 使用上下文中心處理Cookie {#using-context-hub-to-manipulate-cookies}

Context Hub Javascript API為處理瀏覽器Cookie提供了跨瀏覽器支援。 的 [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) 命名空間定義了用於建立、操作和刪除cookie的多個函式。

## 確定已解析的ContextHub段 {#determining-resolved-contexthub-segments}

ContextHub段引擎使您能夠確定在當前上下文中解析哪些已註冊段。 使用的getResolvedSegments函式 [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) 類以檢索已解析的段。 然後，使用 `getName` 或 `getPath` 函式 [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) 類到段的test。

### ContextHub 區段 {#contexthub-segments}

ContextHub網段安裝在 `/conf/<site>/settings/wcm/segments` 的下界。

以下段隨 [WKND教程站點。](getting-started.md)

* 夏
* 冬

用於解決這些段的規則概述如下：

* 首先 [地理位置](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) 儲存用於確定用戶的緯度。
* 然後， [surferinfo商店](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) 決定它在那個緯度上的季節。

>[!WARNING]
>
>安裝的段作為參考配置提供，以幫助您為項目構建自己的專用配置，因此不應直接使用。

## 調試ContextHub {#debugging-contexthub}

有許多用於調試ContextHub的選項，包括生成日誌。 請參閱 [配置ContextHub以瞭解詳細資訊。](ch-configuring.md#logging-debug-messages-for-contexthub)

## 請參閱ContextHub框架概述 {#see-an-overview-of-the-contexthub-framework}

ContextHub提供 [診斷頁](ch-diagnostics.md) 其中可以看到ContextHub框架的概述。
