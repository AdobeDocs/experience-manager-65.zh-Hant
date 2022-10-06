---
title: ContextHub Javascript API參考資料
seo-title: ContextHub Javascript API Reference
description: 將ContextHub元件新增至頁面時，您的指令碼即可使用ContextHub Javascript API
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

# ContextHub Javascript API參考資料{#contexthub-javascript-api-reference}

當 [頁面已新增ContextHub元件](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component).

## ContextHub常數 {#contexthub-constants}

ContextHub Javascript API定義的常數值。

### 事件常數 {#event-constants}

下表列出ContextHub儲存區發生的名稱事件。 另請參閱 [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing).

| 常數 | 說明 | 值 |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | ContextHub的事件命名空間 | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | 指示所有必需儲存庫都已註冊、初始化並準備好使用 | 全店就緒 |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | 指出並非所有儲存都已在指定逾時內初始化 | 部分就緒 |
| ContextHub.Constants.EVENT_STORE_REGISTERED | 在註冊商店時引發 | 儲存註冊 |
| ContextHub.Constants.EVENT_STORE_READY | 指出存放區已準備就緒。 註冊後會立即觸發，但JSONP商店除外，擷取資料時會在此觸發)。 | 存放就緒 |
| ContextHub.Constants.EVENT_STORE_UPDATED | 商店更新其持續性時引發 | 商店更新 |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | 永續性容器名稱 | ContextHubPersistence |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | 儲儲存存原始JSON結果的特定永續性金鑰名稱 | /_/raw回應 |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | 儲存指出JSON資料擷取時的特定時間戳記 | /_/回應時間 |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | 儲存上次呼叫期間使用的JSON服務特定URL | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | 指出ContextHub的UI是否已展開 | /_/容器擴展 |

### UI事件常數 {#ui-event-constants}

下表列出ContextHub UI發生的事件名稱。

| **常數** | **說明** | **值** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | 註冊模式時引發 | ui-mode-registered |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | 未註冊模式時引發 | ui-mode-unecroved |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | 註冊模式轉譯器時引發 | ui-mode-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | 未註冊模式轉譯器時引發 | ui-mode-renderer-unecroved |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | 新增模式時引發 | ui-mode-added |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | 移除模式時引發 | ui-mode-removed |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | 使用者選取模式時觸發 | ui-mode-selected |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | 註冊新模組時引發 | ui模組已註冊 |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | 未註冊模組時引發 | ui-module-uneclover |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | 註冊模組轉譯器時引發 | ui-module-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | 未註冊模組轉譯器時引發 | ui-module-renderer-unregersted |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | 新增模組時引發 | ui-module-added |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | 移除模組時觸發 | ui-module-removed |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | 將UI容器新增至頁面時引發 | ui-container-added |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | 開啟ContextHub UI時觸發 | ui-container-opened |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | 折疊ContextHub UI時觸發 | ui-container-closed |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | 修改屬性時觸發 | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | 每次轉譯ContextHub UI時（例如在屬性變更後）觸發 | ui呈現 |
| ContextHub.Constants.EVENT_UI_INITIALIZED | 初始化UI容器時觸發 | ui初始化 |
| ContextHub.Constants.ACTIVE_UI_MODE | 指示活動UI模式 | /_/active-ui模式 |

## ContextHub Javascript API參考資料 {#contexthub-javascript-api-reference-2}

ContextHub物件可讓您存取所有存放區。

### 函式(ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

傳回所有已註冊的ContextHub存放區。

此函式沒有參數。

**傳回**

包含所有ContextHub存放區的物件。 每個商店都是一個使用與商店相同名稱的對象。

**範例**

下列範例會擷取所有商店，然後擷取地理位置商店：

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

以Javascript物件擷取商店。

**參數**

* **名稱：** 該商店的註冊名稱。

**傳回**

代表存放區的物件。

**範例**

下列範例會擷取地理位置存放區：

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

代表ContextHub區段。 使用ContextHub.SegmentEngine.SegmentManager來取得區段。

### 函式(ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

以字串值傳回區段名稱。

#### getPath() {#getpath}

以字串值傳回區段定義的存放庫路徑。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

提供ContextHub區段的存取權。

### 函式(ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

傳回在目前內容中解析的區段。 此函式沒有參數。

**傳回**

ContextHub.SegmentEngine.Segment物件的陣列。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub儲存庫的基類。

### 屬性(ContextHub.Store.Core) {#properties-contexthub-store-core}

#### 事件 {#eventing}

A [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 物件。 使用此對象來綁定函式以儲存事件。 有關預設值和初始化的資訊，請參閱 [init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).

#### 名稱 {#name}

商店的名稱。

#### 持續性 {#persistence}

ContextHub.Utils.Persistence物件。 有關預設值和初始化的資訊，請參閱 `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### 函式(ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

將資料對象或陣列與儲存資料合併。 物件或陣列中的每個索引鍵/值組會新增至儲存區(透過 `setItem` 函式):

* **對象：** 鍵是屬性名稱。
* **陣列：** 鍵是陣列索引。

請注意，值可以是物件。

**參數**

* **樹：** （物件或陣列）要新增至存放區的資料。
* **選項：** （物件）傳遞至setItem函式的選項物件。 如需詳細資訊，請參閱 `options` 參數 [setItem(key,value,options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options).

**傳回**

A `boolean` 值：

* 值 `true` 指示已儲存資料對象。
* 值 `false` 表示資料儲存區未變更。

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

建立從一個鍵到另一個鍵的引用。 鍵無法引用本身。

**參數**

* **索引鍵：** 參考的鍵 `anotherKey`.

* **另一個鍵：** 參考的索引鍵 `key`.

**傳回**

A `boolean` 值：

* 值 `true` 表示已添加引用。
* 值 `false` 表示未添加任何引用。

#### announceReadiness() {#announcereadiness}

觸發 `ready` 事件。 此函式沒有參數且未傳回值。

#### clean() {#clean}

從儲存中移除所有資料。 函式沒有參數，也沒有傳回值。

#### getItem(key) {#getitem-key}

傳回與索引鍵相關聯的值。

**參數**

* **索引鍵：** （字串）要傳回值的索引鍵。

**傳回**

代表索引鍵值的物件。

#### getKeys(includeInternals) {#getkeys-includeinternals}

從商店中擷取金鑰。 您可以選擇擷取ContextHub架構內部使用的索引鍵。

**參數**

* **includeInternals:** 值 `true` 結果中包含內部使用的索引鍵。 這些鍵以下划線(&quot;_&quot;)字元開頭。 預設值為 `false`。

**傳回**

密鑰名稱的陣列( `string` 值)。

#### getReferences() {#getreferences}

從商店中檢索引用。

**傳回**

使用引用鍵作為引用鍵索引的陣列：

* 引用與 `key` 參數 `addReference` 函式。

* 引用的鍵與 `anotherKey` 參數 `addReference` 函式。

#### getTree(includeInternals) {#gettree-includeinternals}

從儲存中檢索資料樹。 您可以選擇包含ContextHub架構內部使用的索引鍵/值組。

**參數**

* `includeInternals:` 值 `true` 在結果中包含內部使用的索引鍵/值組。 此資料的鍵以下划線(&quot;_&quot;)字元開頭。 預設值為 `false`。

**傳回**

表示資料樹的對象。 鍵是對象的屬性名稱。

#### init(name, config) {#init-name-config}

初始化儲存。

* 將儲存資料設定為空對象。
* 設定對空對象的儲存引用。
* eventChannel是資料：*名稱*，其中 *名稱* 是商店名稱。

* storeDataKey是/store/*名稱*，其中 *名稱* 是商店名稱。

**參數**

* **名稱：** 商店的名稱。
* **設定：** 包含配置屬性的對象：

   * eventDeferring:預設值為32。
   * 事件：此 [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 此儲存的對象。 預設值為ContextHub.eventing物件使用的。
   * 持續性：此儲存的ContextHub.Utils.Persistence物件。 預設值為ContextHub.persistence物件。

#### isEventingPaused() {#iseventingpaused}

判斷是否暫停此商店的事件。

**傳回**

布林值：

* `true`:事件已暫停，因此不會為此存放區觸發任何事件。
* `false`:事件不會暫停，因此會針對此存放區觸發事件。

#### pauseEventing() {#pauseeventing}

暫停儲存的事件，以便不觸發任何事件。 此函式不需要參數且不傳回值。

#### removeItem(key, options) {#removeitem-key-options}

從存放區移除金鑰/值組。

移除金鑰時，函式會觸發 `data` 事件。 事件資料包括儲存名稱、已移除的金鑰名稱、已移除的值、金鑰的新值(null)，以及「remove」的動作類型。

（可選）您可以防止 `data` 事件。

**參數**

* **索引鍵：** （字串）要移除的金鑰名稱。
* **選項：** （物件）選項的物件。 以下對象屬性有效：

   * 靜默：值 `true` 防止 `data` 事件。 預設值為 `false`。

**傳回**

A `boolean` 值：

* 值 `true` 表示已移除索引鍵/值組。
* 值 `false` 表示資料儲存區未變更，因為在儲存區中找不到金鑰。

#### removeReference(key) {#removereference-key}

從儲存中刪除引用。

**參數**

* **索引鍵：** 要刪除的鍵引用。 此參數對應於 `key` 參數 `addReference` 函式。

**傳回**

A `boolean` 值：

* 值 `true` 表示已刪除引用。
* 值 `false` 指出金鑰無效且存放區未變更。

#### reset(keepRemainingData) {#reset-keepremainingdata}

重設儲存的持續資料的初始值。 您可以選擇從存放區移除所有其他資料。 重設存放區時，此存放區的事件會暫停。 此函式不會傳回任何值。

初始值會提供在用於實例化儲存對象的配置對象的initialValues屬性中。

**參數**

* **keepRemainingData:** （布林值）true值會導致非初始資料持續存在。 值為false會移除除初始值以外的所有資料。

重設儲存的持續資料的初始值。 您可以選擇從存放區移除所有其他資料。 重設存放區時，此存放區的事件會暫停。 此函式不會傳回任何值。

初始值會提供在用於實例化儲存對象的配置對象的initialValues屬性中。

**參數**

* keepRemainingData:（布林值）true值會導致非初始資料持續存在。 值為false會移除除初始值以外的所有資料。

#### resolveReference(key, retry) {#resolvereference-key-retry}

擷取參考的金鑰。 或者，您可以指定用於解析最佳匹配的迭代次數。

**參數**

* **索引鍵：** （字串）要解析引用的鍵。 此 `key` 參數與 `key` 參數 `addReference` 函式。

* **重試：** （數量）要使用的迭代次數。

**傳回**

A `string` 代表參考索引鍵的值。 如果未解析任何引用，則 `key` 參數。

#### resumeEventing() {#resumeeventing}

繼續此存放區的事件，以觸發事件。 此函式不定義參數，也不傳回值。

#### setItem(key, value, options) {#setitem-key-value-options}

將索引鍵/值組新增至商店。

觸發 `data` 事件，條件是索引鍵的值與目前儲存用於索引鍵的值不同。 您可以選擇防止 `data` 事件。

事件資料包含的儲存名稱、索引鍵、先前的值、新值，以及 `set`.

**參數**

* **索引鍵：** （字串）金鑰的名稱。
* **選項：** （物件）選項的物件。 以下對象屬性有效：

   * 靜默：值 `true` 防止 `data` 事件。 預設值為 `false`。

* **值：** （物件）要與索引鍵關聯的值。

**傳回**

A `boolean` 值：

* 值 `true` 指示已儲存資料對象。
* 值 `false` 表示資料儲存區未變更。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

包含JSON資料的商店。 資料會從外部JSONP服務中擷取，或選擇性地從傳回JSON資料的服務中擷取。 使用 [ `init`](/help/sites-developing/contexthub-api.md#init-name-config) 函式。

存放區會使用記憶體中的持續時間（Javascript變數）。 儲存資料僅在頁面存留期期間可用。

ContextHub.Store.JSONPStore延伸 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 並繼承該類的函式。

### 函式(ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

配置用於連接到此對象使用的JSONP服務的詳細資訊。 您可以更新或取代現有設定。 函式不會傳回任何值。

**參數**

* **serviceConfig:** 包含下列屬性的物件：

   * 主機：（字串）伺服器名稱或IP位址。
   * jsonp:（布林值）值true表示服務是JSONP服務，否則為false。 若為true，則{callback:&quot;ContextHub.回呼。*Object.name*}物件已新增至service.params物件。
   * params:（物件）URL參數以物件屬性表示。 參數名稱是屬性名稱，參數值是屬性值。
   * 路徑：（字串）服務的路徑。
   * 埠：（數字）服務的埠號。
   * 安全：（字串或布林值）決定要用於服務URL的通訊協定：

      * auto: //
      * true:https://
      * false:https://

* **覆蓋：** （布林值）。 值 `true` 導致現有服務配置被 `serviceConfig`. 值 `false` 導致現有服務配置屬性與 `serviceConfig`.

#### getRawResponse() {#getrawresponse}

傳回自上次呼叫JSONP服務以來所快取的原始回應。 函式不需要參數。

**傳回**

代表原始回應的物件。

#### getServiceDetails() {#getservicedetails}

檢索此ContextHub.Store.JSONPStore對象的服務對象。 服務物件包含建立服務URL所需的所有資訊。

**傳回**

具有下列屬性的物件：

* **主機：** （字串）伺服器名稱或IP位址。
* **jsonp:** （布林值）值true表示服務是JSONP服務，否則為false。 若為true，則{callback:&quot;ContextHub.回呼。*Object.name*}物件已新增至service.params物件。

* **params:** （物件）URL參數以物件屬性表示。 參數名稱是屬性名稱，參數值是屬性值。
* **路徑：** （字串）服務的路徑。
* **埠：** （數字）服務的埠號。
* **安全：** （字串或布林值）決定要用於服務URL的通訊協定：

   * 自動：/
   * true:https://
   * false:https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

擷取JSONP服務的URL。

**參數**

* **解決：** （布林值）判斷是否要在URL中包含已解析的參數。 值 `true` 解析參數，和 `false` 不會。

**傳回**

A `string` 代表服務URL的值。

#### init(name, config) {#init-name-config-1}

初始化ContextHub.Store.JSONPStore對象。

**參數**

* **名稱：** （字串）商店名稱。
* **設定：** （物件）包含服務屬性的物件。 JSONPStore物件使用 `service` 物件，以建構JSONP服務的URL:

   * eventDeferring:32.
   * 事件：此儲存區的ContextHub.Utils.Eventing物件。 預設值為 `ContextHub.eventing` 物件。
   * 持續性：此儲存的ContextHub.Utils.Persistence物件。 預設會使用記憶體持續性（Javascript物件）。
   * 服務：（物件）

      * 主機：（字串）伺服器名稱或IP位址。
      * jsonp:（布林值）值true表示服務是JSONP服務，否則為false。 若為true，則 `{callback: "ContextHub.Callbacks.*Object.name*}`物件已新增至 `service.params`.
      * params:（物件）URL參數以物件屬性表示。 參數名稱和值分別是對象屬性名稱和值。
      * 路徑：（字串）服務的路徑。
      * 埠：（數字）服務的埠號。
      * 安全：（字串或布林值）決定要用於服務URL的通訊協定：

         * 自動：/
         * true:https://
         * false:https://
      * 逾時：（數字）等待JSONP服務在超時前響應的時間長度（以毫秒為單位）。
      * ttl:在兩次JSONP服務呼叫之間傳遞的最小時間量（毫秒）。 (請參閱 [queryService](/help/sites-developing/contexthub-api.md#queryservice-reload) 函式)。


#### queryService(reload) {#queryservice-reload}

查詢遠程JSONP服務並快取響應。 如果自上次呼叫此函式以來的時間量小於 `config.service.ttl`，則不會呼叫服務，且不會變更快取回應。 您可以視需要強制呼叫服務。 此 `config.service.ttl`在呼叫 [init](/help/sites-developing/contexthub-api.md#init-name-config) 函式來初始化儲存。

查詢完成時觸發就緒事件。 如果未設定JSONP服務URL，函式則不會執行任何動作。

**參數**

* **重新載入：** （布林值）值true會移除快取回應，並強制呼叫JSONP服務。

#### 重設 {#reset}

重設儲存區持續資料的初始值，然後呼叫JSONP服務。 您可以選擇從存放區移除所有其他資料。 初始值重設時，此存放區的事件會暫停。 此函式不會傳回任何值。

初始值會提供在用於實例化儲存對象的配置對象的initialValues屬性中。

**參數**

* **keepRemainingData:** （布林值）true值會導致非初始資料持續存在。 值為false會移除除初始值以外的所有資料。

#### resolveParameter(f) {#resolveparameter-f}

解析給定參數。

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PerisentJSONPStore延伸 [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) 因此它繼承該類的所有函式。 不過，從JSONP服務擷取的資料會根據ContextHub持續性的設定而持續保存。 (請參閱 [持續性模式](/help/sites-developing/ch-adding.md#persistence-modes).)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PerisentStore延伸 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 因此它繼承該類的所有函式。 此存放區中的資料會根據ContextHub持續性的設定而保存。

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore延伸 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 因此它繼承該類的所有函式。 此存放區中的資料會使用記憶體中的持續性（Javascript物件）來保存。

## ContextHub.UI {#contexthub-ui}

管理UI模組和UI模組轉譯器。

### 函式(ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRenderer) {#registerrenderer-moduletype-renderer-dontrender}

向ContextHub註冊UI模組轉譯器。 註冊轉譯器後，可將其用於 [建立UI模組](ch-configuring.md#adding-a-ui-module). 若您是 [延伸ContextHub.UI.BaseModuleRenderer](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) 建立自訂UI模組轉譯器。

**參數**

* **moduleType:** （字串）UI模組轉譯器的識別碼。 如果已使用指定值註冊了渲染器，則在註冊此渲染器之前，將先註冊現有的渲染器。
* **轉譯程式：** （字串）轉譯UI模組的類別名稱。
* **dontRender:** （布林值）設為 `true` 以防止在註冊轉譯器後轉譯ContextHub UI。 預設值為 `false`。

**範例**

以下範例將轉譯器註冊為contexthub.browserinfo模組類型。

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

與Cookie互動的公用程式類別。

### 函式(ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

判斷Cookie是否存在。

**參數**

* **索引鍵：** A `String` 包含您要測試之cookie的金鑰。

**傳回**

A `boolean` 值true表示cookie存在。

**範例**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

傳回所有具有符合篩選器之索引鍵的Cookie。

**參數**

* （可選） **篩選：** 比對Cookie金鑰的條件。 若要傳回所有Cookie，請指定任何值。 支援下列類型：

   * 字串：字串會與Cookie金鑰比較。
   * 陣列：陣列中的每個項目都是篩選器。
   * RegExp物件：物件的測試函式可用來比對Cookie金鑰。
   * 函式：測試Cookie金鑰是否相符的函式。 如果測試確認相符，函式必須將Cookie金鑰當作參數，並傳回true。

**傳回**

Cookie的物件。 物件屬性是Cookie索引鍵，而索引鍵值是Cookie值。

**範例**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

傳回Cookie值。

**參數**

* **索引鍵：** 您要其值的Cookie金鑰。

**傳回**

Cookie值，或 `null` 若找不到金鑰的cookie。

**範例**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

傳回符合篩選器之現有Cookie的索引鍵陣列。

**參數**

* **篩選：** 比對Cookie金鑰的條件。 支援下列類型：

   * 字串：字串會與Cookie金鑰比較。
   * 陣列：陣列中的每個項目都是篩選器。
   * RegExp物件：物件的測試函式可用來比對Cookie金鑰。
   * 函式：測試Cookie金鑰是否相符的函式。 函式必須將Cookie金鑰當作參數並傳回 `true` 如果測試確認相符。

**傳回**

字串的陣列，其中每個字串是符合篩選條件之Cookie的索引鍵。

**範例**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

移除Cookie。 若要移除Cookie，值會設為空白字串，而到期日會設為目前日期的前一天。

**參數**

* **索引鍵：** A `String` 代表要移除之cookie之索引鍵的值。

* **選項：** 包含用於設定Cookie屬性之屬性值的物件。 請參閱 ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` 函式以取得相關資訊。 此 `expires` 屬性沒有作用。

**傳回**

此函式不會傳回值。

**範例**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

建立指定索引鍵和值的Cookie，並將Cookie新增至目前的檔案。 您可以選擇指定用以設定Cookie屬性的選項。

**參數**

* **索引鍵：** 包含Cookie索引鍵的字串。
* **值：** 包含Cookie值的字串。
* **選項：** （選用）物件，包含下列任何設定Cookie屬性的屬性：

   * 過期：A `date` 或 `number` 值，指定cookie何時過期。 日期值指定到期的絕對時間。 數字（以天為單位）會將到期時間設為目前時間加上數字。 預設值為 `undefined`。
   * 安全：A `boolean` 指定值 `Secure` 屬性。 預設值為 `false`。
   * 路徑：A `String` 值 `Path` 屬性。 預設值為 `undefined`。

**傳回**

具有設定值的Cookie。

**範例**

```
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### 消失（篩選，選項） {#vanish-filter-options}

移除符合指定篩選器的所有Cookie。 使用getKeys函式來比對Cookie，並使用removeItem函式來移除。

**參數**

* **篩選：** 此 `filter` 要在對 `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` 函式。

* **選項：** 此 `options` 要在對 `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` 函式。

**傳回**

此函式不會傳回值。

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

可讓您將函式系結和解除系結至ContextHub儲存事件。 使用訪問儲存的ContextHub.Utils.Eventing對象 [事件](/help/sites-developing/contexthub-api.md#eventing) 商店的屬性。

### 函式(ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off（名稱，選取器） {#off-name-selector}

從事件中取消綁定函式。

**參數**

* **名稱：** 此 [事件名稱](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 您要為其解除函式系結的項目。

* **選取器：** 標識綁定的選擇器。 (請參閱 `selector` 參數 [on](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) 和 [once](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) 函式)。

**傳回**

此函式不會傳回任何值。

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

將函式綁定到事件。 每次發生事件時都會呼叫函式。 可選地，在建立綁定之前，可以為過去發生的事件調用函式。

**參數**

* **名稱：** （字串） [事件名稱](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 您要與其系結函式。

* **處理常式：** （函式）要系結至事件的函式。
* **選取器：** （字串）系結的唯一識別碼。 如果要使用 `off` 函式來移除系結。

* **triggerForPastEvents:** （布林值）指出是否應針對過去發生的事件執行處理常式。 值 `true` 呼叫過去事件的處理常式。 值 `false` 為未來事件找了手。 預設值為 `true`。

**傳回**

當 `triggerForPastEvents` 引數 `true`，此函式會傳回 `boolean` 指出事件是否發生在過去的值：

* `true`:事件在過去發生，將呼叫處理常式。
* `false`:事件過去未發生。

若 `triggerForPastEvents` is `false`，此函式不會傳回任何值。

**範例**

以下範例將函式系結至地理位置存放區的資料事件。 函式會以商店中緯度資料項目的值填入頁面上的元素。

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

#### once(name, handler, selector, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

將函式綁定到事件。 對於事件的首次出現，函式只會呼叫一次。 或者，可以在建立綁定之前，為過去發生的事件調用函式。

**參數**

* **名稱：** （字串） [事件名稱](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 您要與其系結函式。

* **處理常式：** （函式）要系結至事件的函式。
* **選取器：** （字串）系結的唯一識別碼。 如果要使用 `off` 函式來移除系結。

* **triggerForPastEvents:** （布林值）指出是否應針對過去發生的事件執行處理常式。 值 `true` 呼叫過去事件的處理常式。 值 `false` 為未來事件找了手。 預設值為 `true`。

**傳回**

當 `triggerForPastEvents` 引數 `true`，此函式會傳回 `boolean` 指出事件是否發生在過去的值：

* `true`:事件在過去發生，將呼叫處理常式。
* `false`:事件過去未發生。

若 `triggerForPastEvents` is `false`，此函式不會傳回任何值。

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

允許對象繼承另一個對象的屬性和方法的實用程式類。

### 函式(ContextHub.Utils.inheritation) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

使對象繼承另一個對象的屬性和方法。

**參數**

* **子項：** （對象）繼承的對象。
* **父級：** （物件）定義繼承的屬性和方法的物件。

## ContextHub.Utils.JSON {#contexthub-utils-json}

提供將物件序列化為JSON格式，以及將JSON字串反序列化為物件的函式。

### 函式(ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

將字串值剖析為JSON，並將其轉換為Javascript物件。

**參數**

* **資料：** JSON格式的字串值。

**傳回**

Javascript物件。

**範例**

程式碼 `ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");` 傳回下列物件：

```
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

將Javascript值和物件序列化為JSON格式的字串值。

**參數**

* **資料：** 要序列化的值或對象。 此函式支援布林值、陣列、數字、字串和日期值。

**傳回**

序列化字串值。 當 `data` 是R `egExp` 值，此函式會傳回空白物件。 當 `data` 是函式，傳回 `undefined`.

**範例**

以下程式碼會傳回 `"{'city':'Basel','country':'Switzerland','population':'173330'}":`

```
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

此類便於操作要儲存或從ContextHub儲存中檢索的資料對象。

### 函式(ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

建立資料對象的副本，並從第二個對象添加到資料樹中。 函式返回副本，不修改任何一個原始對象。 當兩個對象的資料樹包含相同的鍵時，第二對象的值覆蓋第一對象的值。

**參數**

* **樹：** 複製的物件。
* **secondTree:** 與 `tree` 物件。

**傳回**

包含合併資料的物件。

#### cleanup() {#cleanup}

建立對象的副本，查找並刪除資料樹中不包含值、空值或未定義的項，並返回副本。

**參數**

* **樹：** 要清除的物件。

**傳回**

已清理的樹的副本。

#### getItem() {#getitem}

從物件中擷取金鑰的值。

**參數**

* **樹：** 資料物件。
* **索引鍵：** 您要擷取之值的索引鍵。

**傳回**

與鍵對應的值。 當索引鍵具有子索引鍵時，此函式會傳回複雜物件。 鍵的值類型為 `undefined`, `null` 的URL。

**範例**

請考量下列Javascript物件：

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

下列范常式式碼會傳回值 `260`:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

下列范常式式碼會擷取具有子項之索引鍵的值：

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

函式會傳回下列物件：

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

從對象的資料樹中檢索所有鍵。 或者，您只能檢索特定鍵子項的鍵。 您也可以選擇指定擷取索引鍵的排序順序。

**參數**

* **樹：** 要從中檢索資料樹鍵的對象。
* **父級：** （可選）要檢索子項的鍵的資料樹中項的鍵。
* **訂購：** （選用）決定傳回索引鍵排序順序的函式。 (請參閱 [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) （位於Mozilla開發人員網路上）。

**傳回**

鍵的陣列。

**範例**

請考量下列物件：

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

此 `ContextHub.Utils.JSON.tree.getKeys(myObject);` script會傳回下列陣列：

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

建立給定對象的副本，從資料樹中刪除指定的分支，並返回修改的副本。

**參數**

* 樹：資料物件。
* 索引鍵：要刪除的鍵。

**傳回**

已移除鍵的原始資料物件復本。

**範例**

請考量下列物件：

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

函式會傳回下列物件：

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

清除字串值，以便用作索引鍵。 若要處理字串，此函式會執行下列動作：

* 將多個連續正斜線減少為單斜線。
* 從字串的開頭和結尾移除空格。
* 將結果分割為由斜線標定的字串陣列。

使用產生的陣列建立可用密鑰。  **參數**

* **索引鍵：** 此 `string` 處理。

**傳回**

陣列 `string` 每個字串是 `key` 用斜線劃分的。 代表已淨化的金鑰。 如果清理的陣列長度為零，則此函式將返回 `null`.

**範例**

下列程式碼會處理字串以產生陣列 `["this", "is", "a", "path"]`，然後產生金鑰 `"/this/is/a/path"` 從陣列：

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

將索引鍵/值組新增至物件復本的資料樹。 如需資料樹的相關資訊，請參閱 [持久性](/help/sites-developing/contexthub.md#persistence).

**參數**

* 樹：資料物件。
* 索引鍵：與要新增的值相關聯的鍵。 索引鍵是資料樹中項目的路徑。 此函式呼叫 `ContextHub.Utils.JSON.tree.sanitize` 先處理金鑰再新增。
* 值：要添加到資料樹的值。

**傳回**

此 `tree` 包含 `key`/ `value` 配對。

**範例**

請考量下列Javascript程式碼：

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

myObject物件具有以下值：

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

使您可以註冊儲存候選項，並獲取註冊的儲存候選項。

### 函式(ContextHub.Utils.storeCandiates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandiates(storeType) {#getregisteredcandidates-storetype}

返回註冊為儲存候選項的儲存類型。 檢索特定儲存類型或所有儲存類型的註冊證書。

**參數**

* **storeType:** （字串）商店類型的名稱。 請參閱 `storeType` 參數 [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 函式。

**傳回**

儲存類型的物件。 對象屬性是儲存類型名稱，而屬性值是已註冊儲存候選項的陣列。

#### getStoreFromCapdiations(storeType) {#getstorefromcandidates-storetype}

從註冊候選項返回儲存類型。 如果註冊了多個同名的儲存類型，則函式將返回具有最高優先順序的儲存類型。

**參數**

* storeType:（字串）商店候選名稱。 請參閱 `storeType` 參數 [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 函式。

**傳回**

表示註冊儲存候選項的對象。 如果未註冊請求的儲存類型，則會引發錯誤。

#### getSupportedStoreTypes() {#getsupportedstoretypes}

返回註冊為儲存候選項的儲存類型的名稱。 此函式不需要參數。

**傳回**

字串值的陣列，其中每個字串是註冊儲存候選項的儲存類型。 請參閱 `storeType` 參數 [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 函式。

#### registerStoreCanditad(store, storeType, priority, applies) {#registerstorecandidate-store-storetype-priority-applies}

使用名稱和優先順序將儲存對象註冊為儲存候選項。

優先順序是指出同名商店重要性的數字。 當使用與已註冊的儲存候選相同的名稱註冊儲存候選時，使用優先順序較高的候選。 當註冊儲存候選時，僅當優先順序高於同名註冊儲存候選時，才註冊儲存。

**參數**

* **商店：** （對象）要註冊為儲存候選項的儲存對象。
* **storeType:** （字串）商店候選名稱。 建立商店候選項的例項時，需要此值。
* **優先順序：** （數字）商店候選的優先順序。
* **套用：** （函式）用以叫用的函式，會評估儲存在目前環境中的可用性。 函式必須傳回 `true` 如果商店適用， `false` 否則。 預設值是傳回true的函式： `function() {return true;}`

**範例**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
