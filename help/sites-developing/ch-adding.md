---
title: 將ContextHub新增至頁面並存取存放區
description: 將ContextHub新增至您的頁面，以啟用ContextHub功能並連結至ContextHub JavaScript資料庫
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# 將ContextHub新增至頁面並存取存放區 {#adding-contexthub-to-pages-and-accessing-stores}

將ContextHub新增至您的頁面，以啟用ContextHub功能並連結至ContextHub JavaScript資料庫。

ContextHub JavaScript API可讓您存取ContextHub管理的內容資料。 本頁面簡要說明用於存取及操控內容資料的API的主要功能。 請依照API參考檔案的連結檢視詳細資訊和程式碼範例。

## 將ContextHub新增至頁面元件 {#adding-contexthub-to-a-page-component}

若要啟用ContextHub功能並連結至ContextHub JavaScript資料庫，請在頁面的`head`區段中包含`contexthub`元件。 頁面元件的HTL程式碼應類似下列範例：

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

請注意，您還需要設定ContextHub工具列是否以「預覽」模式顯示。 請參閱[顯示和隱藏ContextHub UI](ch-configuring.md#showing-and-hiding-the-contexthub-ui)。

## 關於ContextHub存放區 {#about-contexthub-stores}

使用ContextHub存放區來儲存內容資料。 ContextHub提供下列型別的存放區，這些存放區是所有存放區型別的基礎：

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [工作階段存放區](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

所有存放區型別都是[`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core)類別的延伸。 如需有關建立存放區型別的資訊，請參閱[建立自訂存放區](ch-extend.md#creating-custom-store-candidates)。 如需有關範例存放區型別的資訊，請參閱[範例ContextHub存放區候選者](ch-samplestores.md)。

### 持續性模式 {#persistence-modes}

Context Hub存放區會使用下列其中一個持續性模式：

* **本機：**&#x200B;使用HTML5 localStorage保留資料。 本機儲存體會跨工作階段儲存在瀏覽器上。
* **工作階段：**&#x200B;使用HTML5 sessionStorage來儲存資料。 工作階段存放區會在瀏覽器工作階段期間持續保留，並可供所有瀏覽器視窗使用。
* **Cookie：**&#x200B;使用瀏覽器原生支援的Cookie來儲存資料。 Cookie資料會以HTTP要求傳送至伺服器，或從伺服器傳送。
* **Window.name：**&#x200B;使用window.name屬性來儲存資料。
* **記憶體：**&#x200B;使用JavaScript物件來儲存資料。

Context Hub預設會使用本機持續性模式。 如果瀏覽器不支援或允許HTML5 localStorage，則會使用工作階段持續性。 如果瀏覽器不支援或允許HTML5 sessionStorage，則會使用Window.name持續性。

### 存放資料 {#store-data}

在內部，以樹狀結構儲存資料，可讓值新增為主要型別或複雜物件。 當您將複雜物件加入至儲存區時，物件屬性會在資料樹狀結構中形成分支。 例如，下列複雜物件會新增至名為location的空白存放區：

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

存放區資料的樹狀結構可依據下列方式進行概念化：

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

樹狀結構會將存放區中的資料專案定義為索引鍵/值組。 在上述範例中，索引鍵`/number`對應到值`321`，而索引鍵`/data/country`對應到值`Switzerland`。

### 操控物件 {#manipulating-objects}

ContextHub提供[`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree)類別以操控JavaScript物件。 在您將JavaScript物件新增至存放區之前，或是從存放區取得之後，請使用此類別的函式來操控這些物件。

此外，[`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json)類別也提供將物件序列化為字串，以及將字串還原為物件的功能。 使用此類別來處理JSON資料，以支援本身不包含`JSON.parse`和`JSON.stringify`函式的瀏覽器。

## 與ContextHub存放區互動 {#interacting-with-contexthub-stores}

使用[`ContextHub`](contexthub-api.md#ui-event-constants) JavaScript物件來取得儲存區作為JavaScript物件。 取得存放區物件後，您就可以控制其中包含的資料。 使用[`getAllStores`](contexthub-api.md#getallstores)或[`getStore`](contexthub-api.md#getstore-name)函式取得存放區。

### 存取存放區資料 {#accessing-store-data}

[`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) JavaScript類別定義了數個與存放區資料互動的功能。 以下函式儲存和擷取物件中包含的多個資料專案：

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

個別資料專案會儲存為一組索引鍵/值組。 若要儲存和擷取值，請指定對應的索引鍵：

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

請注意，自訂商店候選者可以定義其他函式，以提供對商店資料的存取權。

>[!NOTE]
>
>ContextHub預設不會知道發佈伺服器上目前使用的登入，並且ContextHub會將此類使用者視為「匿名」。
>
>您可以載入設定檔存放區，讓ContextHub知道登入的使用者。 請參閱這裡](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js)的GitHub上的[範常式式碼。

### ContextHub事件 {#contexthub-eventing}

ContextHub包括事件架構，可讓您自動對儲存事件做出反應。 每個存放區物件都包含一個[`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing)物件，可作為存放區的[`eventing`](contexthub-api.md#eventing)屬性使用。 使用[`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents)或[`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents)函式將JavaScript函式繫結到存放區事件。

## 使用Context Hub操作Cookie {#using-context-hub-to-manipulate-cookies}

Context Hub JavaScript API提供處理瀏覽器Cookie的跨瀏覽器支援。 [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie)名稱空間定義了數個用於建立、處理和刪除Cookie的功能。

## 決定已解析的ContextHub區段 {#determining-resolved-contexthub-segments}

ContextHub區段引擎可讓您決定要在目前前後關聯中解析哪些已註冊區段。 使用[`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager)類別的getResolvedSegments函式來擷取已解析的區段。 然後，使用[`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment)類別的`getName`或`getPath`函式來測試區段。

### ContextHub 區段 {#contexthub-segments}

ContextHub區段安裝在`/conf/<site>/settings/wcm/segments`節點下方。

[WKND教學課程網站已安裝下列區段。](getting-started.md)

* 夏天
* 冬天

用於解析這些區段的規則概述如下：

* 首先，[地理位置](ch-samplestores.md#contexthub-geolocation-sample-store-candidate)存放區是用來決定使用者的緯度。
* 然後[surferinfo存放區](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate)的月份資料專案會決定它在該緯度的哪個季節。

>[!WARNING]
>
>提供的已安裝區段可作為參考設定，協助您為專案建立自己的專用設定。 請勿直接使用，

## 偵錯ContextHub {#debugging-contexthub}

偵錯ContextHub有數個選項，包括產生記錄檔。 如需詳細資訊，請參閱[設定ContextHub。](ch-configuring.md#logging-debug-messages-for-contexthub)

## 請參閱ContextHub架構的概觀 {#see-an-overview-of-the-contexthub-framework}

ContextHub提供[診斷頁面](ch-diagnostics.md)，您可在其中檢視ContextHub架構的概觀。
