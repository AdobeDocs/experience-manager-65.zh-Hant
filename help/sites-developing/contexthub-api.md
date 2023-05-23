---
title: ContextHub Javascript API參考
seo-title: ContextHub Javascript API Reference
description: 將ContextHub元件添加到頁面後，ContextHub Javascript API可用於指令碼
seo-description: The ContextHub Javascript API is available to your scripts when the ContextHub component has been added to the page
uuid: 296d6c8e-517f-4837-9e86-ae571ea8aa17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 90605f41-1861-4891-a7c8-b8b5918cd5c6
feature: Context Hub
exl-id: b472d96f-b1a5-40b7-be2a-52f3396f6884
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '5006'
ht-degree: 2%

---

# ContextHub Javascript API參考{#contexthub-javascript-api-reference}

ContextHub Javascript API可用於指令碼 [ContextHub元件已添加到頁面](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component)。

## ContextHub常數 {#contexthub-constants}

ContextHub Javascript API定義的常數值。

### 事件常數 {#event-constants}

下表列出了ContextHub儲存區發生的名稱事件。 另請參閱 [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing)。

| 常數 | 說明 | 值 |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | ContextHub的事件命名空間 | 甲 |
| ContextHub.Constants.EVENT_ALL_STORES_READY | 指示已註冊、初始化並準備使用所有必需儲存 | 全儲存就緒 |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | 指示並非所有儲存都在給定超時內初始化 | 部分就緒 |
| ContextHub.Constants.EVENT_STORE_REGISTERED | 註冊商店時激發 | 儲存註冊 |
| ContextHub.Constants.EVENT_STORE_READY | 指示儲存已準備就緒。 它在註冊後立即觸發，JSONP儲存除外，在JSONP儲存中，資料被讀取時觸發)。 | 儲存就緒 |
| ContextHub.Constants.EVENT_STORE_UPDATED | 當儲存更新其持久性時激發 | 儲存更新 |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | 持久性容器名稱 | 上下文集線器持久性 |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | 儲存原始JSON結果的特定持久性密鑰名稱 | /_/原始響應 |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | 儲存指示何時讀取JSON資料的特定時間戳 | /_/響應時間 |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | 儲存上次調用期間使用的JSON服務的特定URL | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | 指示是否展開ContextHub的UI | /_/容器擴展 |

### UI事件常數 {#ui-event-constants}

下表列出了ContextHub UI發生的事件的名稱。

| **常數** | **說明** | **值** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | 註冊模式時激發 | ui模式註冊 |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | 未註冊模式時激發 | ui-mode-unregested |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | 註冊模式呈現器時激發 | ui-mode-renderer-regited |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | 未註冊模式呈現器時激發 | ui-mode-renderer-unregested |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | 添加新模式時激發 | ui-mode-added |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | 刪除模式時激發 | ui-mode-removed |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | 當用戶選擇模式時激發 | ui-mode選定 |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | 註冊新模組時激發 | ui模組註冊 |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | 未註冊模組時激發 | ui-module-unregested |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | 註冊模組呈現器時激發 | ui模組呈現器註冊 |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | 未註冊模組呈現器時激發 | ui-module-renderer-unregested |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | 添加新模組時激發 | 添加的ui模組 |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | 刪除模組時激發 | ui模組已刪除 |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | 將UI容器添加到頁面時激發 | 添加ui容器 |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | 開啟ContextHub UI時激發 | ui容器已開啟 |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | 折疊ContextHub UI時激發 | ui容器封閉 |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | 修改屬性時激發 | ui屬性已修改 |
| ContextHub.Constants.EVENT_UI_RENDERED | 每次呈現ContextHub UI時激發（例如在屬性更改後） | ui呈現 |
| ContextHub.Constants.EVENT_UI_INITIALIZED | 初始化UI容器時激發 | ui初始化 |
| ContextHub.Constants.ACTIVE_UI_MODE | 指示活動UI模式 | /_/active-ui模式 |

## ContextHub Javascript API參考 {#contexthub-javascript-api-reference-2}

ContextHub對象提供對所有儲存的訪問。

### 函式(ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

返回所有已註冊的ContextHub儲存。

此函式沒有參數。

**返回**

包含所有ContextHub儲存的對象。 每個儲存都是與儲存使用相同名稱的對象。

**範例**

下面的示例檢索所有儲存，然後檢索地理位置儲存：

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore（名稱） {#getstore-name}

將儲存檢索為Javascript對象。

**參數**

* **名稱：** 註冊商店的名稱。

**返回**

表示儲存的對象。

**範例**

下面的示例檢索地理位置儲存：

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

表示ContextHub段。 使用ContextHub.SegmentEngine.SegmentManager獲取段。

### 函式(ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

返回段的名稱，作為字串值。

#### getPath() {#getpath}

返回段定義的儲存庫路徑作為字串值。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

提供對ContextHub段的訪問。

### 函式(ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

返回在當前上下文中解析的段。 此函式沒有參數。

**返回**

ContextHub.SegmentEngine.Segment對象的陣列。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub儲存的基類。

### 屬性(ContextHub.Store.Core) {#properties-contexthub-store-core}

#### 事件 {#eventing}

A [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 的雙曲餘切值。 使用此對象綁定函式來儲存事件。 有關預設值和初始化的資訊，請參見 [init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config)。

#### 名稱 {#name}

商店的名稱。

#### 持久性 {#persistence}

ContextHub.Utils.Persistence對象。 有關預設值和初始化的資訊，請參見 `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### 函式(ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems（樹，選項） {#addallitems-tree-options}

將資料對象或陣列與儲存資料合併。 對象或陣列中的每個鍵/值對都添加到儲存中(通過 `setItem` ):

* **對象：** 鍵是屬性名稱。
* **陣列：** 鍵是陣列索引。

請注意，值可以是對象。

**參數**

* **樹：** （對象或陣列）要添加到儲存中的資料。
* **選項：** （對象）傳遞給setItem函式的選項的可選對象。 有關資訊，請參見 `options` 參數 [setItem(key,value,options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options)。

**返回**

A `boolean` 值：

* 值 `true` 表示已儲存資料對象。
* 值 `false` 指示資料儲存未更改。

#### addReference(key, atherKey) {#addreference-key-anotherkey}

建立從一個鍵到另一個鍵的引用。 鍵不能引用自身。

**參數**

* **鍵：** 引用的鍵 `anotherKey`。

* **另一個鍵：** 它們被引用的鍵 `key`。

**返回**

A `boolean` 值：

* 值 `true` 表示已添加引用。
* 值 `false` 表示未添加引用。

#### annowsReadiness() {#announcereadiness}

觸發 `ready` 此商店的事件。 此函式沒有參數，並且不返回值。

#### clean() {#clean}

從儲存中刪除所有資料。 該函式沒有參數且沒有返回值。

#### getItem(key) {#getitem-key}

返回與鍵關聯的值。

**參數**

* **鍵：** （字串）要返回值的鍵。

**返回**

表示鍵值的對象。

#### getKeys(includeInternals) {#getkeys-includeinternals}

從儲存中檢索密鑰。 （可選）可以檢索ContextHub框架內部使用的鍵。

**參數**

* **包括內部：** 值 `true` 包括結果中的內部使用鍵。 這些鍵以下划線(&quot;_&quot;)字元開頭。 預設值為 `false`。

**返回**

鍵名陣列( `string` 值)。

#### getReferences() {#getreferences}

從儲存檢索引用。

**返回**

使用引用鍵作為引用鍵的索引的陣列：

* 引用鍵與 `key` 參數 `addReference` 的子菜單。

* 引用的鍵與 `anotherKey` 參數 `addReference` 的子菜單。

#### getTree(includeInternals) {#gettree-includeinternals}

從儲存中檢索資料樹。 （可選）您可以包括ContextHub框架內部使用的鍵/值對。

**參數**

* `includeInternals:` 值 `true` 包括結果中內部使用的鍵/值對。 此資料的鍵以下划線(&quot;_&quot;)字元開頭。 預設值為 `false`。

**返回**

表示資料樹的對象。 鍵是對象的屬性名稱。

#### init(name, config) {#init-name-config}

初始化儲存。

* 將儲存資料設定為空對象。
* 設定對空對象的儲存引用。
* eventChannel是資料：*名稱*，也請參見Wiki頁。 *名稱* 是商店名稱。

* storeDataKey是/store/*名稱*，也請參見Wiki頁。 *名稱* 是商店名稱。

**參數**

* **名稱：** 商店的名稱。
* **配置：** 包含配置屬性的對象：

   * 事件延遲：預設值為32。
   * 事件：的 [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 此儲存的對象。 預設值為ContextHub.eventing對象使用的值。
   * 持久性：此儲存的ContextHub.Utils.Persistence對象。 預設值為ContextHub.persistence對象。

#### isEventingPaused() {#iseventingpaused}

確定此儲存是否暫停了事件。

**返回**

布爾值：

* `true`:事件暫停，因此不會觸發此儲存的事件。
* `false`:事件不會暫停，因此會觸發此儲存的事件。

#### pauseEventing() {#pauseeventing}

暫停儲存的事件，以便不觸發任何事件。 此函式不需要任何參數，也不返回任何值。

#### removeItem（key，選項） {#removeitem-key-options}

從儲存中刪除密鑰/值對。

刪除鍵後，該函式將觸發 `data` 的子菜單。 事件資料包括儲存名稱、已刪除的鍵的名稱、已刪除的值、鍵的新值（空）以及「remove」的操作類型。

（可選）您可以防止觸發 `data` 的子菜單。

**參數**

* **鍵：** （字串）要刪除的鍵的名稱。
* **選項：** （對象）選項的對象。 以下對象屬性有效：

   * 靜默：值 `true` 防止觸發 `data` 的子菜單。 預設值為 `false`。

**返回**

A `boolean` 值：

* 值 `true` 指示已刪除密鑰/值對。
* 值 `false` 指示資料儲存區未更改，因為在儲存區中找不到密鑰。

#### removeReference(key) {#removereference-key}

從儲存中刪除引用。

**參數**

* **鍵：** 要刪除的鍵引用。 此參數與 `key` 參數 `addReference` 的子菜單。

**返回**

A `boolean` 值：

* 值 `true` 表示已刪除引用。
* 值 `false` 表示密鑰無效，且儲存未更改。

#### reset(keepRemainingData) {#reset-keepremainingdata}

重置儲存的永續資料的初始值。 （可選）可以從儲存中刪除所有其他資料。 當儲存被重置時，此儲存的事件暫停。 此函式不返回值。

用於實例化儲存對象的config對象的initialValues屬性中提供了初始值。

**參數**

* **keepRemainingData:** （布爾值）值為true將保留非初始資料。 如果值為false，則除初始值外，所有資料都將被刪除。

重置儲存的永續資料的初始值。 （可選）可以從儲存中刪除所有其他資料。 當儲存被重置時，此儲存的事件暫停。 此函式不返回值。

用於實例化儲存對象的config對象的initialValues屬性中提供了初始值。

**參數**

* keepRemainingData:（布爾值）值為true將保留非初始資料。 如果值為false，則除初始值外，所有資料都將被刪除。

#### resolveReference(key, retry) {#resolvereference-key-retry}

檢索引用的鍵。 （可選）可以指定用於解析最佳匹配的迭代次數。

**參數**

* **鍵：** （字串）用於解析引用的鍵。 此 `key` 參數與 `key` 參數 `addReference` 的子菜單。

* **重試：** （數字）要使用的迭代數。

**返回**

A `string` 表示引用鍵的值。 如果未解析引用，則 `key` 參數。

#### resumeEventing() {#resumeeventing}

恢復此儲存的事件，以便觸發事件。 此函式不定義任何參數，也不返回任何值。

#### setItem(key、value、options) {#setitem-key-value-options}

向儲存添加密鑰/值對。

觸發 `data` 僅當鍵的值與當前為鍵儲存的值不同時，才會發生事件。 您可以選擇防止觸發 `data` 的子菜單。

事件資料包括儲存名稱、鍵、上一個值、新值和操作類型 `set`。

**參數**

* **鍵：** （字串）鍵的名稱。
* **選項：** （對象）選項的對象。 以下對象屬性有效：

   * 靜默：值 `true` 防止觸發 `data` 的子菜單。 預設值為 `false`。

* **值：** （對象）要與鍵關聯的值。

**返回**

A `boolean` 值：

* 值 `true` 表示已儲存資料對象。
* 值 `false` 指示資料儲存未更改。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

包含JSON資料的儲存。 從外部JSONP服務中檢索資料，或從返回JSON資料的服務（可選）中檢索資料。 使用 [ `init`](/help/sites-developing/contexthub-api.md#init-name-config) 函式。

儲存使用記憶體中持久性（Javascript變數）。 儲存資料僅在頁面的生命週期內可用。

ContextHub.Store.JSONPStore擴展 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 並繼承了該類的功能。

### 函式(ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

配置用於連接到此對象使用的JSONP服務的詳細資訊。 您可以更新或替換現有配置。 該函式不返回值。

**參數**

* **服務配置：** 包含以下屬性的對象：

   * 主機：（字串）伺服器名稱或IP地址。
   * jsonp:（布爾值）值為true表示服務是JSONP服務，否則為false。 如果為true，則{callback:&quot;ContextHub.Callbacks。*對象名稱*}對象已添加到service.params對象。
   * params:（對象）表示為對象屬性的URL參數。 參數名是屬性名，參數值是屬性值。
   * 路徑：（字串）服務的路徑。
   * 埠：（編號）服務的埠號。
   * 安全：（字串或布爾值）確定用於服務URL的協定：

      * auto: //
      * 真：https://
      * false:https://

* **覆蓋：** （布爾型）。 值 `true` 導致現有服務配置被 `serviceConfig`。 值 `false` 導致現有服務配置屬性與 `serviceConfig`。

#### getRawResponse() {#getrawresponse}

返回自上次調用JSONP服務後快取的原始響應。 該函式不需要參數。

**返回**

表示原始響應的對象。

#### getServiceDetails() {#getservicedetails}

檢索此ContextHub.Store.JSONPStore對象的服務對象。 服務對象包含建立服務URL所需的所有資訊。

**返回**

具有以下屬性的對象：

* **主機：** （字串）伺服器名稱或IP地址。
* **jsonp:** （布爾值）值為true表示服務是JSONP服務，否則為false。 如果為true，則{callback:&quot;ContextHub.Callbacks。*對象名稱*}對象已添加到service.params對象。

* **params:** （對象）表示為對象屬性的URL參數。 參數名是屬性名，參數值是屬性值。
* **路徑：** （字串）服務的路徑。
* **埠：** （編號）服務的埠號。
* **安全：** （字串或布爾值）確定用於服務URL的協定：

   * auto: //
   * 真：https://
   * false:https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

檢索JSONP服務的URL。

**參數**

* **解決：** （布爾值）確定是否在URL中包含已解析的參數。 值 `true` 解析參數，和 `false` 不會。

**返回**

A `string` 表示服務URL的值。

#### init(name, config) {#init-name-config-1}

初始化ContextHub.Store.JSONPStore對象。

**參數**

* **名稱：** （字串）儲存的名稱。
* **配置：** （對象）包含service屬性的對象。 JSONPStore對象使用 `service` 構建JSONP服務的URL的對象：

   * 事件延遲：32.
   * 事件：此儲存的ContextHub.Utils.Eventing對象。 預設值為 `ContextHub.eventing` 的雙曲餘切值。
   * 持久性：此儲存的ContextHub.Utils.Persistence對象。 預設情況下，使用記憶體持久性（Javascript對象）。
   * 服務：（對象）

      * 主機：（字串）伺服器名稱或IP地址。
      * jsonp:（布爾值）值為true表示服務是JSONP服務，否則為false。 如果為真， `{callback: "ContextHub.Callbacks.*Object.name*}`對象添加到 `service.params`。
      * params:（對象）表示為對象屬性的URL參數。 參數名稱和值分別是對象屬性名稱和值。
      * 路徑：（字串）服務的路徑。
      * 埠：（編號）服務的埠號。
      * 安全：（字串或布爾值）確定用於服務URL的協定：

         * auto: //
         * 真：https://
         * false:https://
      * 超時：（數字）等待JSONP服務在超時之前響應的時間（毫秒）。
      * ttl:在JSONP服務調用之間傳遞的最小時間（毫秒）。 (請參閱 [查詢服務](/help/sites-developing/contexthub-api.md#queryservice-reload) )的正平方根。


#### queryService(reload) {#queryservice-reload}

查詢遠程JSONP服務並快取響應。 如果自上次調用此函式以來的時間量小於 `config.service.ttl`，未調用服務且未更改快取響應。 （可選）您可以強制調用服務。 的 `config.service.ttl`調用屬性時設定 [初始化](/help/sites-developing/contexthub-api.md#init-name-config) 函式初始化儲存。

查詢完成後觸發就緒事件。 如果未設定JSONP服務URL，則函式將不執行任何操作。

**參數**

* **重裝：** （布爾值）值為true將刪除快取響應並強制調用JSONP服務。

#### 重設 {#reset}

重置儲存的永續資料的初始值，然後調用JSONP服務。 （可選）可以從儲存中刪除所有其他資料。 重置初始值時，此儲存的事件暫停。 此函式不返回值。

用於實例化儲存對象的config對象的initialValues屬性中提供了初始值。

**參數**

* **keepRemainingData:** （布爾值）值為true將保留非初始資料。 如果值為false，則除初始值外，所有資料都將被刪除。

#### resolveParameter(f) {#resolveparameter-f}

解析給定參數。

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PeristedJSONPStore擴展 [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) 因此它繼承了該類的所有功能。 但是，根據ContextHub持久性的配置，從JSONP服務中檢索到的資料被保留。 (請參閱 [持久性模式](/help/sites-developing/ch-adding.md#persistence-modes)。)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PersiedStore擴展 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 因此它繼承了該類的所有功能。 此儲存中的資料根據ContextHub持久性的配置進行保留。

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore擴展 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 因此它繼承了該類的所有功能。 此儲存中的資料使用記憶體持久性（Javascript對象）永續。

## ContextHub.UI {#contexthub-ui}

管理UI模組和UI模組呈現器。

### 函式(ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType、renderer、dontRender) {#registerrenderer-moduletype-renderer-dontrender}

在ContextHub中註冊UI模組呈現器。 註冊呈現器後，它可用於 [建立UI模組](ch-configuring.md#adding-a-ui-module)。 在您 [擴展ContextHub.UI.BaseModuleRenderer](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) 建立自定義UI模組呈現器。

**參數**

* **moduleType:** （字串）UI模組呈現器的標識符。 如果已使用指定值註冊了呈現器，則在註冊此呈現器之前，將註銷現有呈現器。
* **渲染器：** （字串）呈現UI模組的類的名稱。
* **dontRender:** （布爾值）設定為 `true` 來防止在註冊呈現器後呈現ContextHub UI。 預設值為 `false`。

**範例**

以下示例將呈現器註冊為contexthub.browserinfo模組類型。

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

用於與Cookie交互的實用程式類。

### 函式(ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

確定Cookie是否存在。

**參數**

* **鍵：** A `String` 包含您正在測試的cookie的密鑰。

**返回**

A `boolean` 值為true表示cookie存在。

**範例**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems（篩選器） {#getallitems-filter}

返回所有具有與篩選器匹配的鍵的Cookie。

**參數**

* （可選） **篩選器：** 匹配Cookie鍵的條件。 要返回所有Cookie，請不指定值。 支援以下類型：

   * 字串：將字串與Cookie鍵進行比較。
   * 陣列：陣列中的每個項都是篩選器。
   * RegExp對象：對象的test函式用於匹配cookie鍵。
   * 函式：test匹配的Cookie鍵的函式。 函式必須將cookie鍵作為參數，如果test確認匹配，則返回true。

**返回**

Cookie的對象。 對象屬性是cookie鍵，鍵值是cookie值。

**範例**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

返回Cookie值。

**參數**

* **鍵：** 要為其賦值的Cookie的鍵。

**返回**

Cookie值，或 `null` 找不到該密鑰的cookie。

**範例**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

返回與篩選器匹配的現有Cookie的鍵陣列。

**參數**

* **篩選器：** 匹配Cookie鍵的條件。 支援以下類型：

   * 字串：將字串與Cookie鍵進行比較。
   * 陣列：陣列中的每個項都是篩選器。
   * RegExp對象：對象的test函式用於匹配cookie鍵。
   * 函式：test匹配的Cookie鍵的函式。 函式必須將cookie鍵作為參數並返回 `true` test確認匹配。

**返回**

字串陣列，其中每個字串是與篩選器匹配的cookie的鍵。

**範例**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem（key，選項） {#removeitem-key-options-1}

刪除Cookie。 要刪除Cookie，將值設定為空字串，並將到期日期設定為當前日期之前的日期。

**參數**

* **鍵：** A `String` 表示要刪除的cookie的鍵的值。

* **選項：** 包含用於配置Cookie屬性的屬性值的對象。 查看 ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` 的子菜單。 的 `expires` 屬性無效。

**返回**

此函式不返回值。

**範例**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key、value、options) {#setitem-key-value-options-1}

建立給定鍵和值的cookie，並將cookie添加到當前文檔。 或者，您可以指定配置Cookie屬性的選項。

**參數**

* **鍵：** 包含Cookie的鍵的字串。
* **值：** 包含cookie值的字串。
* **選項：** （可選）包含以下任何配置Cookie屬性的屬性的對象：

   * 過期：A `date` 或 `number` 指定cookie到期時間的值。 日期值指定到期的絕對時間。 數字（以天為單位）將到期時間設定為當前時間加上數字。 預設值為 `undefined`。
   * 安全：A `boolean` 指定值 `Secure` Cookie的屬性。 預設值為 `false`。
   * 路徑：A `String` 值 `Path` Cookie的屬性。 預設值為 `undefined`。

**返回**

具有設定值的cookie。

**範例**

```
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### 消失（篩選器，選項） {#vanish-filter-options}

刪除與給定篩選器匹配的所有Cookie。 使用getKeys函式匹配Cookie，並使用removeItem函式刪除Cookie。

**參數**

* **篩選器：** 的 `filter` 調用中使用的參數 `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` 的子菜單。

* **選項：** 的 `options` 調用中使用的參數 `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` 的子菜單。

**返回**

此函式不返回值。

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

使您能夠將函式綁定和解除綁定到ContextHub儲存事件。 使用 [事件](/help/sites-developing/contexthub-api.md#eventing) 商店的屬性。

### 函式(ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off（名稱，選擇器） {#off-name-selector}

將函式與事件解除綁定。

**參數**

* **名稱：** 的 [事件名稱](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 要解除函式綁定的函式。

* **選擇器：** 標識綁定的選擇器。 (請參閱 `selector` 參數 [上](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) 和 [一次](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) )的正平方根。

**返回**

此函式不返回值。

#### on(name、handler、selector、triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

將函式綁定到事件。 每次事件發生時都會調用該函式。 可選地，可以在建立綁定之前為過去發生的事件調用該函式。

**參數**

* **名稱：** （字串） [事件名稱](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 將函式綁定到的。

* **處理程式：** （函式）綁定到事件的函式。
* **選擇器：** （字串）綁定的唯一標識符。 如果要使用 `off` 函式以刪除綁定。

* **triggerForPastEvents:** （布爾值）指示是否應為過去發生的事件執行處理程式。 值 `true` 為過去的事件調用處理程式。 值 `false` 為未來的事件打電話。 預設值為 `true`。

**返回**

當 `triggerForPastEvents` 參數 `true`，此函式返回 `boolean` 指示事件是否發生在過去的值：

* `true`:過去發生的事件將調用處理程式。
* `false`:此事件過去未發生。

如果 `triggerForPastEvents` 是 `false`，此函式不返回值。

**範例**

以下示例將函式綁定到地理位置儲存的資料事件。 該函式使用儲存中緯度資料項的值填充頁面上的元素。

```
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(name、handler、selector、triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

將函式綁定到事件。 該函式只調用一次，用於事件的首次出現。 可選地，可以在建立綁定之前為過去發生的事件調用該函式。

**參數**

* **名稱：** （字串） [事件名稱](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 將函式綁定到的。

* **處理程式：** （函式）綁定到事件的函式。
* **選擇器：** （字串）綁定的唯一標識符。 如果要使用 `off` 函式以刪除綁定。

* **triggerForPastEvents:** （布爾值）指示是否應為過去發生的事件執行處理程式。 值 `true` 為過去的事件調用處理程式。 值 `false` 為未來的事件打電話。 預設值為 `true`。

**返回**

當 `triggerForPastEvents` 參數 `true`，此函式返回 `boolean` 指示事件是否發生在過去的值：

* `true`:過去發生的事件將調用處理程式。
* `false`:此事件過去未發生。

如果 `triggerForPastEvents` 是 `false`，此函式不返回值。

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

使對象能夠繼承另一個對象的屬性和方法的實用程式類。

### 函式(ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

使對象繼承另一個對象的屬性和方法。

**參數**

* **子項：** （對象）繼承的對象。
* **父項：** （對象）定義繼承的屬性和方法的對象。

## ContextHub.Utils.JSON {#contexthub-utils-json}

提供用於將對象序列化為JSON格式並將JSON字串反序列化為對象的函式。

### 函式(ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

將字串值解析為JSON，並將其轉換為javascript對象。

**參數**

* **資料：** JSON格式的字串值。

**返回**

Javascript對象。

**範例**

代碼 `ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");` 返回以下對象：

```
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify（資料） {#stringify-data}

將Javascript值和對象序列化為JSON格式的字串值。

**參數**

* **資料：** 要序列化的值或對象。 此函式支援布爾值、陣列值、數字值、字串值和日期值。

**返回**

序列化字串值。 當 `data` 是R `egExp` 值，此函式返回空對象。 當 `data` 是函式，返回 `undefined`。

**範例**

以下代碼返回 `"{'city':'Basel','country':'Switzerland','population':'173330'}":`

```
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

此類便於對要儲存或從ContextHub儲存中檢索的資料對象進行操作。

### 函式(ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

建立資料對象的副本，並從第二個對象添加資料樹。 該函式返回副本，並且不修改任何一個原始對象。 當兩個對象的資料樹包含相同的鍵時，第二對象的值覆蓋第一對象的值。

**參數**

* **樹：** 複製的對象。
* **第二樹：** 與的副本合併的對象 `tree` 的雙曲餘切值。

**返回**

包含合併資料的對象。

#### cleanup() {#cleanup}

建立對象的副本，查找並刪除資料樹中不包含值、空值或未定義值的項，並返回副本。

**參數**

* **樹：** 要清理的對象。

**返回**

已清除的樹副本。

#### getItem() {#getitem}

從鍵的對象中檢索值。

**參數**

* **樹：** 資料對象。
* **鍵：** 要檢索的值的鍵。

**返回**

與鍵相關的值。 當鍵具有子鍵時，此函式將返回一個複雜對象。 鍵的值類型為 `undefined`。 `null` 的子菜單。

**範例**

請考慮以下Javascript對象：

```
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

以下示例代碼返回值 `260`:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

下面的示例代碼檢索具有子項的鍵的值：

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

函式返回以下對象：

```
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

從對象的資料樹中檢索所有鍵。 或者，您只能檢索特定鍵的子項的鍵。 您還可以根據需要指定檢索到的鍵的排序順序。

**參數**

* **樹：** 要從中檢索資料樹鍵的對象。
* **父項：** （可選）要檢索其子項的鍵的資料樹中項的鍵。
* **訂單：** （可選）確定返回鍵排序順序的函式。 (請參閱 [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 在Mozilla Developer Network上。)

**返回**

鍵陣列。

**範例**

請考慮以下對象：

```
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

的 `ContextHub.Utils.JSON.tree.getKeys(myObject);` 指令碼返回以下陣列：

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

建立給定對象的副本，從資料樹中刪除指定的分支，並返回修改的副本。

**參數**

* 樹：資料對象。
* 鍵：要刪除的鍵。

**返回**

刪除了鍵的原始資料對象的副本。

**範例**

請考慮以下對象：

```
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

以下示例指令碼從資料樹中刪除/one/two/three/four分支：

```
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

函式返回以下對象：

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### 消毒密鑰（密鑰） {#sanitizekey-key}

清除字串值，使其可用作鍵。 要清理字串，此函式將執行以下操作：

* 將多個連續的正斜槓減為單個斜槓。
* 從字串的開頭和結尾刪除空格。
* 將結果拆分為用斜槓劃分的字串陣列。

使用結果陣列建立可用鍵。  **參數**

* **鍵：** 的 `string` 去消毒。

**返回**

一組 `string` 值，其中每個字串是 `key` 用斜線劃分的。 表示已清理的密鑰。 如果清理後的陣列的長度為零，則此函式將返回 `null`。

**範例**

以下代碼將清理字串以生成陣列 `["this", "is", "a", "path"]`，然後生成密鑰 `"/this/is/a/path"` 從陣列：

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem（樹、鍵、值） {#setitem-tree-key-value}

將鍵/值對添加到對象副本的資料樹中。 有關資料樹的資訊，請參見 [持久性](/help/sites-developing/contexthub.md#persistence)。

**參數**

* 樹：資料對象。
* 鍵：與要添加的值關聯的鍵。 鍵是資料樹中項的路徑。 此函式調用 `ContextHub.Utils.JSON.tree.sanitize` 在添加密鑰之前先對其進行清理。
* 值：要添加到資料樹的值。

**返回**

副本 `tree` 包括 `key`/ `value` 對。

**範例**

請考慮以下Javascript代碼：

```
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

myObject對象具有以下值：

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

使您能夠註冊儲存候選並獲取已註冊的儲存候選。

### 函式(ContextHub.Utils.storeCandiates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandites(storeType) {#getregisteredcandidates-storetype}

返回註冊為儲存候選的儲存類型。 檢索特定儲存類型或所有儲存類型的註冊證書。

**參數**

* **storeType:** （字串）儲存類型的名稱。 查看 `storeType` 參數 [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 的子菜單。

**返回**

儲存類型的對象。 對象屬性是儲存類型名稱，屬性值是已註冊的儲存候選項陣列。

#### getStoreFromCadients(storeType) {#getstorefromcandidates-storetype}

從註冊的候選項返回儲存類型。 如果註冊了多個具有相同名稱的儲存類型，該函式將返回優先順序最高的儲存類型。

**參數**

* storeType:（字串）儲存候選項的名稱。 查看 `storeType` 參數 [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 的子菜單。

**返回**

表示註冊儲存候選對象的對象。 如果未註冊請求的儲存類型，則會引發錯誤。

#### getSupportedStoreTypes() {#getsupportedstoretypes}

返回註冊為儲存候選的儲存類型的名稱。 此函式不需要參數。

**返回**

字串值的陣列，其中每個字串是註冊儲存候選的儲存類型。 查看 `storeType` 參數 [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 的子菜單。

#### registerStoreCanditade(store、storeType、priority、applies) {#registerstorecandidate-store-storetype-priority-applies}

使用名稱和優先順序將儲存對象註冊為儲存候選對象。

優先順序是指示同名儲存的重要性的數字。 當使用與已註冊的儲存候選者相同的名稱註冊儲存候選者時，使用具有較高優先順序的候選者。 當註冊儲存候選時，僅當優先順序高於同名註冊的儲存候選時，才註冊儲存。

**參數**

* **商店：** （對象）要註冊為儲存候選的儲存對象。
* **storeType:** （字串）儲存候選項的名稱。 建立儲存候選實例時需要此值。
* **優先順序：** （數字）儲存候選項的優先順序。
* **應用：** （函式）用於調用的函式，用於評估儲存在當前環境中的可應用性。 函式必須返回 `true` 如果商店適用， `false` 否則。 預設值是返回true的函式： `function() {return true;}`

**範例**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
