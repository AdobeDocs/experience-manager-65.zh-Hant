---
title: ContextHub JavaScript API參考
description: 將ContextHub元件新增至頁面後，指令碼即可使用ContextHub JavaScript API
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
feature: Context Hub,Developing,Personalization
exl-id: b472d96f-b1a5-40b7-be2a-52f3396f6884
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '4913'
ht-degree: 0%

---

# ContextHub JavaScript API參考{#contexthub-javascript-api-reference}

ContextHub JavaScript API適用於您的指令碼，當 [ContextHub元件已新增至頁面](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component).

## ContextHub常數 {#contexthub-constants}

ContextHub JavaScript API定義的常數值。

### 事件常數 {#event-constants}

下表列出ContextHub存放區發生的名稱事件。 另請參閱 [contexthub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing).

| 常數 | 說明 | 值 |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | ContextHub的事件名稱空間 | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | 表示所有必要的存放區都已註冊、初始化，且可供使用 | 所有商店就緒 |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | 表示在指定的逾時內並未初始化所有存放區 | 商店 — 部分就緒 |
| ContextHub.Constants.EVENT_STORE_REGISTERED | 註冊存放區時引發 | store-registered |
| ContextHub.Constants.EVENT_STORE_READY | 表示存放區已準備就緒。 註冊後會立即觸發，但JSONP存放區除外（在擷取資料時會觸發）。 | 已備妥 |
| ContextHub.Constants.EVENT_STORE_UPDATED | 在存放區更新其持續性時引發 | 存放區已更新 |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | 持續性容器名稱 | ContextHubPersistence |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | 儲存原始JSON結果的特定持續性索引鍵名稱 | /_/raw-response |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | 儲存特定時間戳記，指出擷取JSON資料的時間 | /_/response-time |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | 儲存上次呼叫期間所使用的特定JSON服務URL | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | 指示ContextHub的UI是否展開 | /_/container-expanded |

### UI事件常數 {#ui-event-constants}

下表列出ContextHub UI中發生的事件名稱。

| **常數** | **說明** | **值** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | 在模式註冊時引發 | ui-mode-registered |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | 在模式取消註冊時引發 | ui-mode-unregistered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | 註冊模式轉譯器時引發 | ui-mode-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | 取消註冊模式轉譯器時引發 | ui-mode-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | 在新增模式時引發 | ui-mode-added |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | 移除模式時引發 | ui-mode-removed |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | 當使用者選取模式時引發 | ui-mode-selected |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | 註冊新模組時引發 | ui-module-registered |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | 模組取消註冊時引發 | ui-module-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | 在註冊模組轉譯器時引發 | ui-module-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | 在模組轉譯器取消註冊時引發 | ui-module-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | 在新增模組時引發 | ui-module-added |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | 移除模組時引發 | ui-module-removed |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | 將UI容器新增至頁面時引發 | ui-container-added |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | 在ContextHub UI開啟時引發 | ui-container-open |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | 在ContextHub UI摺疊時引發 | ui-container-closed |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | 修改屬性時引發 | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | 每次呈現ContextHub UI時引發（例如，在屬性變更後） | ui-rendered |
| ContextHub.Constants.EVENT_UI_INITIALIZED | 當UI容器初始化時引發 | ui已初始化 |
| ContextHub.Constants.ACTIVE_UI_MODE | 指示作用中UI模式 | /_/active-ui-mode |

## ContextHub JavaScript API參考 {#contexthub-javascript-api-reference-2}

ContextHub物件提供所有存放區的存取權。

### 函式(ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

傳回所有已註冊的ContextHub存放區。

此函式沒有引數。

**傳回**

包含所有ContextHub存放區的物件。 每個存放區都是一個物件，使用與該存放區相同的名稱。

**範例**

下列範例會擷取所有存放區，然後擷取地理位置存放區：

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

擷取儲存區做為JavaScript物件。

**引數**

* **名稱：** 存放區登入的名稱。

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

以字串值的形式傳回區段名稱。

#### getPath() {#getpath}

以String值傳回區段定義的存放庫路徑。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

提供ContextHub區段的存取權。

### 函式(ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

傳回在目前內容中解析的區段。 此函式沒有引數。

**傳回**

ContextHub.SegmentEngine.Segment物件的陣列。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub存放區的基底類別。

### 屬性(ContextHub.Store.Core) {#properties-contexthub-store-core}

#### 事件 {#eventing}

A [contexthub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 物件。 將此物件用於繫結函式，以儲存事件。 如需有關預設值和初始化的資訊，請參閱 [init(name，config)](/help/sites-developing/contexthub-api.md#init-name-config).

#### 名稱 {#name}

存放區的名稱。

#### persistence {#persistence}

contexthub.Utils.Persistence物件。 如需有關預設值和初始化的資訊，請參閱 `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### 函式(ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree， options) {#addallitems-tree-options}

將資料物件或陣列與存放區資料合併。 物件或陣列中的每個索引鍵/值組都會新增到存放區(透過 `setItem` 函式)：

* **物件：** 金鑰為屬性名稱。
* **陣列：** 索引鍵是陣列索引。

請注意，值可以是物件。

**引數**

* **樹狀結構：** （物件或陣列）要新增至存放區的資料。
* **選項：** （物件）傳遞至setItem函式之選項的選用物件。 如需詳細資訊，請參閱 `options` 引數： [setItem(key，value，options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options).

**傳回**

A `boolean` 值：

* 值 `true` 表示儲存的資料物件。
* 值 `false` 表示資料存放區未變更。

#### addReference(key， anotherKey) {#addreference-key-anotherkey}

建立從一個索引鍵到另一個索引鍵的參照。 索引鍵不能參考自身。

**引數**

* **索引鍵：** 參考的金鑰 `anotherKey`.

* **另一個索引鍵：** 所參考的金鑰 `key`.

**傳回**

A `boolean` 值：

* 值 `true` 表示已新增參照。
* 值 `false` 表示未新增參照。

#### announceReadiness() {#announcereadiness}

觸發 `ready` 此商店的事件。 此函式沒有引數且未傳回任何值。

#### clean() {#clean}

從存放區移除所有資料。 函式沒有引數也沒有傳回值。

#### getItem(key) {#getitem-key}

傳回與索引鍵相關聯的值。

**引數**

* **索引鍵：** （字串）要傳回值的索引鍵。

**傳回**

代表索引鍵值的物件。

#### getKeys(includeInternals) {#getkeys-includeinternals}

從存放區擷取金鑰。 您可以選擇擷取ContextHub架構內部使用的金鑰。

**引數**

* **includeinternals：** 值 `true` 在結果中包含內部使用的索引鍵。 這些鍵以底線(「_」)字元開頭。 預設值為 `false`。

**傳回**

索引鍵名稱陣列( `string` 值)。

#### getReferences() {#getreferences}

從存放區擷取參考。

**傳回**

使用參照索引鍵做為參照索引鍵的索引的陣列：

* 參照索引鍵對應至 `key` 的引數 `addReference` 函式。

* 參照的索引鍵對應至 `anotherKey` 的引數 `addReference` 函式。

#### getTree(includeInternals) {#gettree-includeinternals}

從存放區擷取資料樹狀結構。 您可以選擇加入ContextHub架構在內部使用的索引鍵/值組。

**引數**

* `includeInternals:` 值 `true` 在結果中包含內部使用的索引鍵/值配對。 此資料的鍵值以底線(「_」)字元開頭。 預設值為 `false`。

**傳回**

代表資料樹的物件。 鍵是物件的屬性名稱。

#### init(name， config) {#init-name-config}

初始化存放區。

* 將存放區資料設定為空白物件。
* 將存放區參考設定為空白物件。
* eventChannel為資料：*名稱*，其中 *名稱* 是存放區名稱。

* storeDataKey為/store/*名稱*，其中 *名稱* 是存放區名稱。

**引數**

* **名稱：** 存放區的名稱。
* **設定：** 包含組態屬性的物件：

   * eventDeferring：預設值為32。
   * 事件： [contexthub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 物件。 預設值是ContextHub.eventing物件使用的值。
   * 持續性：此存放區的ContextHub.Utils.Persistence物件。 預設值為ContextHub.persistence物件。

#### isEventingPaused() {#iseventingpaused}

決定是否暫停此存放區的事件。

**傳回**

布林值：

* `true`：事件已暫停，因此不會為此存放區觸發任何事件。
* `false`：事件不會暫停，因此會為此存放區觸發事件。

#### pauseEventing() {#pauseeventing}

暫停存放區的事件，以免觸發任何事件。 此函式不需要引數也未傳回任何值。

#### removeItem(key， options) {#removeitem-key-options}

從存放區移除索引鍵/值組。

移除索引鍵時，函式會觸發 `data` 事件。 事件資料包含存放區名稱、已移除的機碼名稱、已移除的值、機碼的新值(null)以及「移除」的動作型別。

或者，您可以防止觸發 `data` 事件。

**引數**

* **索引鍵：** （字串）要移除的金鑰名稱。
* **選項：** （物件）選項的物件。 下列物件屬性有效：

   * 靜音：值 `true` 防止觸發 `data` 事件。 預設值為 `false`。

**傳回**

A `boolean` 值：

* 值 `true` 表示索引鍵/值配對已移除。
* 值 `false` 表示資料存放區未變更，因為在存放區中找不到索引鍵。

#### removeReference(key) {#removereference-key}

從存放區移除參照。

**引數**

* **索引鍵：** 要移除的索引鍵參考。 此引數對應至 `key` 的引數 `addReference` 函式。

**傳回**

A `boolean` 值：

* 值 `true` 表示參照已移除。
* 值 `false` 表示金鑰無效，且存放區未變更。

#### reset(keepRemainingData) {#reset-keepremainingdata}

重設存放區儲存資料的初始值。 或者，您也可以從存放區移除所有其他資料。 當存放區重設時，此存放區的事件已暫停。 此函式未傳回任何值。

初始值是在用來具現化存放區物件的設定物件的initialValues屬性中提供。

**引數**

* **keepRemainingData：** （布林值） true值會持續儲存非初始資料。 如果值為false，則會移除初始值以外的所有資料。

重設存放區儲存資料的初始值。 或者，您也可以從存放區移除所有其他資料。 當存放區重設時，此存放區的事件已暫停。 此函式未傳回任何值。

初始值是在用來具現化存放區物件的設定物件的initialValues屬性中提供。

**引數**

* keepRemainingData： （布林值） true值會持續儲存非初始資料。 如果值為false，則會移除初始值以外的所有資料。

#### resolveReference(key， retry) {#resolvereference-key-retry}

擷取參照的索引鍵。 或者，您可以指定用於解析最佳比對的反複專案數。

**引數**

* **索引鍵：** （字串）要解析參考的索引鍵。 這個 `key` 引數對應至 `key` 的引數 `addReference` 函式。

* **重試：** （數目）要使用的反複專案數。

**傳回**

A `string` 代表參考索引鍵的值。 如果未解析任何參照，則 `key` 引數會傳回。

#### resumeEventing() {#resumeeventing}

繼續此存放區的事件，以便觸發事件。 此函式不定義任何引數也不傳回任何值。

#### setItem(key， value， options) {#setitem-key-value-options}

將索引鍵/值配對新增至存放區。

觸發 `data` 只有在索引鍵的值不同於目前為索引鍵儲存的值時，才會發生事件。 您可以選擇避免觸發 `data` 事件。

事件資料包括商店名稱、金鑰、先前的值、新值和動作型別 `set`.

**引數**

* **索引鍵：** （字串）金鑰的名稱。
* **選項：** （物件）選項的物件。 下列物件屬性有效：

   * 靜音：值 `true` 防止觸發 `data` 事件。 預設值為 `false`。

* **值：** （物件）要與索引鍵關聯的值。

**傳回**

A `boolean` 值：

* 值 `true` 表示儲存的資料物件。
* 值 `false` 表示資料存放區未變更。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

包含JSON資料的存放區。 資料會從外部JSONP服務擷取，或選擇性地從傳回JSON資料的服務擷取。 使用指定服務詳細資料 [`init`](/help/sites-developing/contexthub-api.md#init-name-config) 建立此類別的執行個體時執行函式。

存放區使用記憶體內部持續性（JavaScript變數）。 存放區資料僅在頁面存留期內可用。

ContextHub.Store.JSONPStore擴展 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 並繼承該類別的功能。

### 函式(ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig， override) {#configureservice-serviceconfig-override}

設定連線至此物件所使用JSONP服務的詳細資訊。 您可以更新或取代現有設定。 函式不會傳回任何值。

**引數**

* **serviceConfig：** 包含下列屬性的物件：

   * 主機： （字串）伺服器名稱或IP位址。
   * jsonp： （布林值） true值表示服務是JSONP服務，否則為false。 若為True，則{callback： &quot;ContextHub.Callbacks.*物件名稱*}物件已新增至service.params物件。
   * params： （物件）以物件屬性表示的URL引數。 引數名稱為屬性名稱，引數值為屬性值。
   * path： （字串）服務的路徑。
   * port： (Number)服務的連線埠號碼。
   * secure： （字串或布林值）決定用於服務URL的通訊協定：

      * 自動： //
      * true： https://
      * false： https://

* **覆寫：** （布林值）。 值 `true` 導致現有的服務設定被以下屬性取代： `serviceConfig`. 值 `false` 會導致現有的服務設定屬性與的屬性合併 `serviceConfig`.

#### getRawResponse() {#getrawresponse}

傳回自上次呼叫JSONP服務後快取的原始回應。 函式不需要引數。

**傳回**

代表原始回應的物件。

#### getServiceDetails() {#getservicedetails}

擷取此ContextHub.Store.JSONPStore物件的服務物件。 服務物件包含建立服務URL所需的所有資訊。

**傳回**

具有下列屬性的物件：

* **主機：** （字串）伺服器名稱或IP位址。
* **jsonp：** （布林值） true值表示服務是JSONP服務，否則為false。 若為True，則{callback： &quot;ContextHub.Callbacks.*物件名稱*}物件已新增至service.params物件。

* **引數：** （物件） URL引數以物件屬性表示。 引數名稱為屬性名稱，引數值為屬性值。
* **路徑：** （字串）服務的路徑。
* **連線埠：** （號碼）服務的連線埠號碼。
* **安全：** （字串或布林值）決定用於服務URL的通訊協定：

   * 自動： //
   * true： https://
   * false： https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

擷取JSONP服務的URL。

**引數**

* **解析：** （布林值）決定是否在URL中包含解析的引數。 值 `true` 解析的引數，以及 `false` 不會。

**傳回**

A `string` 代表服務URL的值。

#### init(name， config) {#init-name-config-1}

初始化ContextHub.Store.JSONPStore物件。

**引數**

* **名稱：** （字串）存放區的名稱。
* **設定：** （物件）包含服務屬性的物件。 JSONPStore物件使用 `service` 物件來建構JSONP服務的URL：

   * eventDeferring： 32。
   * 事件：此存放區的ContextHub.Utils.Eventing物件。 預設值為 `ContextHub.eventing` 物件。
   * 持續性：此存放區的ContextHub.Utils.Persistence物件。 預設會使用記憶體持續性（JavaScript物件）。
   * 服務： （物件）

      * 主機： （字串）伺服器名稱或IP位址。
      * jsonp： （布林值） true值表示服務是JSONP服務，否則為false。 若為True，則 `{callback: "ContextHub.Callbacks.*Object.name*}`物件已新增至 `service.params`.
      * params： （物件）以物件屬性表示的URL引數。 引數名稱和值分別是物件屬性名稱和值。
      * path： （字串）服務的路徑。
      * port： (Number)服務的連線埠號碼。
      * secure： （字串或布林值）決定用於服務URL的通訊協定：

         * 自動： //
         * true： https://
         * false： https://

      * 逾時： （數字）逾時前等待JSONP服務回應的時間（以毫秒為單位）。
      * ttl：呼叫JSONP服務之間的最小時間量（以毫秒為單位）。 (請參閱 [queryservice](/help/sites-developing/contexthub-api.md#queryservice-reload) 函式)。

#### queryService（重新載入） {#queryservice-reload}

查詢遠端JSONP服務並快取回應。 如果自上次呼叫此函式後經過的時間少於 `config.service.ttl`，則不會呼叫服務，且快取的回應不會變更。 您可以選擇強制呼叫服務。 此 `config.service.ttl`屬性是在呼叫 [init](/help/sites-developing/contexthub-api.md#init-name-config) 初始化存放區的函式。

查詢完成時觸發就緒事件。 如果未設定JSONP服務URL，則函式不會執行任何動作。

**引數**

* **重新載入：** （布林值） true值會移除快取回應，並強制呼叫JSONP服務。

#### 重設 {#reset}

重設存放區儲存資料的初始值，然後呼叫JSONP服務。 或者，您也可以從存放區移除所有其他資料。 初始值重設時，此存放區的事件已暫停。 此函式未傳回任何值。

初始值是在用來具現化存放區物件的設定物件的initialValues屬性中提供。

**引數**

* **keepRemainingData：** （布林值） true值會持續儲存非初始資料。 如果值為false，則會移除初始值以外的所有資料。

#### resolveParameter(f) {#resolveparameter-f}

解析指定的引數。

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersistedJSONPStore擴展 [contexthub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) 因此它會繼承該類別的所有函式。 不過，從JSONP服務擷取的資料會根據ContextHub持續性的設定持續存在。 (請參閱 [持續性模式](/help/sites-developing/ch-adding.md#persistence-modes).)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PersistedStore延伸 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 因此它會繼承該類別的所有函式。 此存放區中的資料會根據ContextHub持續性的設定持續儲存。

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore延伸 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 因此它會繼承該類別的所有函式。 此存放區中的資料是使用記憶體內持續性（JavaScript物件）來持續儲存。

## ContextHub.UI {#contexthub-ui}

管理UI模組和UI模組轉譯器。

### 函式(ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType， renderer， dontRender) {#registerrenderer-moduletype-renderer-dontrender}

向ContextHub註冊UI模組轉譯器。 註冊轉譯器後，它可用於 [建立使用者介面模組](ch-configuring.md#adding-a-ui-module). 請在以下情況下使用此函式： [擴充ContextHub.UI.BaseModuleRenderer](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) 以建立自訂UI模組轉譯器。

**引數**

* **模組型別：** （字串） UI模組轉譯器的識別碼。 如果轉譯器已使用指定的值註冊，則在註冊此轉譯器之前會先取消註冊現有的轉譯器。
* **轉譯器：** （字串）轉譯UI模組的類別名稱。
* **不要呈現：** （布林值）設為 `true` 以防止在註冊轉譯器後轉譯ContextHub UI。 預設值為 `false`。

**範例**

下列範例會將轉譯器註冊為contexthub.browserinfo模組型別。

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

與Cookie互動的公用程式類別。

### 函式(ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists（鍵） {#exists-key}

判斷Cookie是否存在。

**引數**

* **索引鍵：** A `String` 包含您正在測試之Cookie的金鑰。

**傳回**

A `boolean` true值表示Cookie存在。

**範例**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

傳回索引鍵符合篩選器的所有Cookie。

**引數**

* （可選） **篩選：** 比對Cookie金鑰的條件。 若要傳回所有Cookie，請勿指定任何值。 支援的型別如下：

   * 字串：字串會與Cookie金鑰比較。
   * 陣列：陣列中的每個專案都是一個篩選器。
   * RegExp物件：物件的測試函式用於比對Cookie金鑰。
   * 函式：測試Cookie金鑰以符合專案的函式。 函式必須以Cookie金鑰為引數，如果測試確認相符，則傳回true。

**傳回**

Cookie的物件。 物件屬性是Cookie金鑰，金鑰值是Cookie值。

**範例**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

傳回Cookie值。

**引數**

* **索引鍵：** 您要取值的Cookie金鑰。

**傳回**

Cookie值，或 `null` 如果找不到索引鍵的Cookie。

**範例**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

傳回符合篩選條件的現有Cookie索引鍵陣列。

**引數**

* **篩選：** 比對Cookie金鑰的條件。 支援的型別如下：

   * 字串：字串會與Cookie金鑰比較。
   * 陣列：陣列中的每個專案都是一個篩選器。
   * RegExp物件：物件的測試函式用於比對Cookie金鑰。
   * 函式：測試Cookie金鑰以符合專案的函式。 函式必須以Cookie金鑰為引數，並傳回 `true` 如果測試確認相符。

**傳回**

字串陣列，其中每個字串是符合篩選器的Cookie索引鍵。

**範例**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key， options) {#removeitem-key-options-1}

移除Cookie。 若要移除Cookie，此值會設為空字串，而到期日期會設為目前日期之前的日期。

**引數**

* **索引鍵：** A `String` 代表要移除之Cookie索引鍵的值。

* **選項：** 包含用於設定Cookie屬性的屬性值的物件。 請參閱 ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` 函式以取得資訊。 此 `expires` 屬性沒有作用。

**傳回**

此函式未傳回值。

**範例**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key， value， options) {#setitem-key-value-options-1}

建立指定索引鍵和值的Cookie，並將Cookie新增至目前檔案。 您可以選擇指定用來設定Cookie屬性的選項。

**引數**

* **索引鍵：** 包含Cookie金鑰的字串。
* **值：** 包含Cookie值的字串。
* **選項：** （選用）物件，包含下列任何可設定Cookie屬性的屬性：

   * 過期： A `date` 或 `number` 指定Cookie過期時間的值。 日期值會指定絕對到期時間。 數字（以天為單位）會將到期時間設定為目前時間加上數字。 預設值為 `undefined`。
   * 安全： A `boolean` 值，指定 `Secure` Cookie的屬性。 預設值為 `false`。
   * 路徑： A `String` 要做為的值 `Path` Cookie的屬性。 預設值為 `undefined`。

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

移除符合指定篩選器的所有Cookie。 Cookie會使用getKeys函式來比對，並使用removeItem函式來移除。

**引數**

* **篩選：** 此 `filter` 要在呼叫中使用的引數 `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` 函式。

* **選項：** 此 `options` 要在呼叫中使用的引數 `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` 函式。

**傳回**

此函式未傳回值。

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

可讓您將函式繫結和解除繫結至ContextHub存放區事件。 使用存取存放區的ContextHub.Utils.Eventing物件 [事件](/help/sites-developing/contexthub-api.md#eventing) 存放區的屬性。

### 函式(ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name， selector) {#off-name-selector}

從事件中取消繫結函式。

**引數**

* **名稱：** 此 [事件的名稱](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 您正在解除繫結函式的連結。

* **選擇器：** 識別繫結的選擇器。 (請參閱 `selector` 的引數 [於](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) 和 [一次](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) 函式)。

**傳回**

此函式未傳回任何值。

#### on(name， handler， selector， triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

將函式繫結至事件。 每次事件發生時都會呼叫函式。 或者，可以為過去發生的事件（在建立繫結之前）呼叫函式。

**引數**

* **名稱：** （字串） [事件的名稱](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 您要將函式繫結到其中。

* **處理常式：** （函式）繫結至事件的函式。
* **選擇器：** （字串）繫結的唯一識別碼。 如果您要使用 `off` 函式以移除繫結。

* **triggerForPastEvents：** （布林值）指出是否應該針對過去發生的事件執行處理常式。 值 `true` 呼叫過去事件的處理常式。 值 `false` 呼叫未來事件的處理常式。 預設值為 `true`。

**傳回**

當 `triggerForPastEvents` 引數為 `true`，此函式傳回 `boolean` 指出該事件是否過去發生的值：

* `true`：該事件發生在過去，且將會呼叫處理常式。
* `false`：此事件過去未發生。

如果 `triggerForPastEvents` 是 `false`，此函式不會傳回任何值。

**範例**

下列範例會將函式繫結至地理位置存放區的資料事件。 函式會使用存放區中Latitude資料專案的值填入頁面上的元素。

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

#### once(name， handler， selector， triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

將函式繫結至事件。 函式只會在第一次發生事件時呼叫一次。 您可以選擇在建立繫結之前，為過去發生的事件呼叫函式。

**引數**

* **名稱：** （字串） [事件的名稱](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 您要將函式繫結到其中。

* **處理常式：** （函式）繫結至事件的函式。
* **選擇器：** （字串）繫結的唯一識別碼。 如果您要使用 `off` 函式以移除繫結。

* **triggerForPastEvents：** （布林值）指出是否應該針對過去發生的事件執行處理常式。 值 `true` 呼叫過去事件的處理常式。 值 `false` 呼叫未來事件的處理常式。 預設值為 `true`。

**傳回**

當 `triggerForPastEvents` 引數為 `true`，此函式傳回 `boolean` 指出該事件是否過去發生的值：

* `true`：該事件發生在過去，且將會呼叫處理常式。
* `false`：此事件過去未發生。

如果 `triggerForPastEvents` 是 `false`，此函式不會傳回任何值。

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

一種公用程式類別，可讓物件繼承另一個物件的屬性和方法。

### 函式(ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child， parent) {#inherit-child-parent}

讓物件繼承另一個物件的屬性和方法。

**引數**

* **子項：** （物件）繼承的物件。
* **父系：** （物件）定義繼承之屬性和方法的物件。

## ContextHub.Utils.JSON {#contexthub-utils-json}

提供將物件序列化為JSON格式並將JSON字串還原序列化為物件的函式。

### 函式(ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

將字串值剖析為JSON並將其轉換為Javascript物件。

**引數**

* **資料：** JSON格式的字串值。

**傳回**

javascript物件。

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

將JavaScript值和物件序列化為JSON格式的字串值。

**引數**

* **資料：** 要序列化的值或物件。 此函式支援布林值、陣列、數字、字串和日期值。

**傳回**

序列化字串值。 時間 `data` 是R `egExp` 值，此函式傳回空白物件。 時間 `data` 為函式，傳回 `undefined`.

**範例**

下列程式碼會傳回 `"{'city':'Basel','country':'Switzerland','population':'173330'}":`

```
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

此類別有助於處理要儲存或從ContextHub存放區擷取的資料物件。

### 函式(ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

建立資料物件的復本，並從第二個物件將資料樹新增至該復本。 函式會傳回覆本，而不會修改任何原始物件。 當兩個物件的資料樹包含相同的索引鍵時，第二個物件的值會覆寫第一個物件的值。

**引數**

* **樹狀結構：** 複製的物件。
* **secondTree：** 與的復本合併的物件 `tree` 物件。

**傳回**

包含合併資料的物件。

#### cleanup() {#cleanup}

建立物件的復本，尋找並移除資料樹狀結構中不含任何值、空值或未定義值的專案，然後傳回覆本。

**引數**

* **樹狀結構：** 要清除的物件。

**傳回**

已清除的樹狀結構復本。

#### getItem() {#getitem}

從物件擷取索引鍵的值。

**引數**

* **樹狀結構：** 資料物件。
* **索引鍵：** 您要擷取之值的索引鍵。

**傳回**

和索引鍵對應的值。 當索引鍵具有子索引鍵時，此函式會傳回複雜的物件。 當索引鍵值的型別為 `undefined`， `null` 會傳回。

**範例**

請考量下列JavaScript物件：

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

下列範常式式碼會傳回值 `260`：

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

下列範常式式碼會擷取具有子索引鍵之索引鍵的值：

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

此函式傳回以下物件：

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

從物件的資料樹狀結構中擷取所有索引鍵。 您可以選擇只擷取特定鍵的子系鍵。 您也可以選擇指定擷取之索引鍵的排序順序。

**引數**

* **樹狀結構：** 要從中擷取資料樹狀結構索引鍵的物件。
* **父系：** （選擇性）資料樹狀結構中要擷取子專案索引鍵的專案索引鍵。
* **訂購：** （選用）決定傳回索引鍵排序順序的函式。 (請參閱 [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) ，位於Mozilla Developer Network。)

**傳回**

索引鍵陣列。

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

此 `ContextHub.Utils.JSON.tree.getKeys(myObject);` 指令碼傳回下列陣列：

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

建立指定物件的復本，從資料樹狀結構中移除指定的分支，並傳回修改後的復本。

**引數**

* 樹：資料物件。
* key：要移除的索引鍵。

**傳回**

移除金鑰的原始資料物件復本。

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

以下範例指令碼會從資料樹狀結構中移除/one/two/three/four分支：

```
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

此函式傳回以下物件：

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanizeKey(key) {#sanitizekey-key}

清理字串值，使其可用作索引鍵。 若要清除字串，此函式會執行下列動作：

* 將多個連續正斜線減少為單一斜線。
* 移除字串開頭和結尾的空格。
* 將結果分割成以斜線分隔的字串陣列。

使用結果陣列建立可用的索引鍵。  **引數**

* **索引鍵：** 此 `string` 以整理。

**傳回**

陣列 `string` 值，其中每個字串都是 `key` 以斜線分隔。 代表已清除的金鑰。 如果經過清理的陣列長度為零，此函式會傳回 `null`.

**範例**

下列程式碼會清理字串以產生陣列 `["this", "is", "a", "path"]`，然後產生金鑰 `"/this/is/a/path"` 從陣列：

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree， key， value) {#setitem-tree-key-value}

將索引鍵/值配對新增至物件復本的資料樹狀結構。 如需資料樹狀結構的相關資訊，請參閱 [持續性](/help/sites-developing/contexthub.md#persistence).

**引數**

* 樹：資料物件。
* key：與要新增的值產生關聯的索引鍵。 索引鍵是資料樹狀結構中專案的路徑。 此函式呼叫 `ContextHub.Utils.JSON.tree.sanitize` 以在新增金鑰之前對其進行處理。
* value：要新增至資料樹狀結構的值。

**傳回**

「 」的副本 `tree` 物件，包括 `key`/ `value` 配對。

**範例**

考量下列JavaScript程式碼：

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

myObject物件具有下列值：

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

可讓您註冊候選商店並取得已註冊的候選商店。

### 函式(ContextHub.Utils.storeCategors) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

傳回註冊為候選商店的商店型別。 擷取特定存放區型別或所有存放區型別的已註冊候選者。

**引數**

* **storeType：** （字串）存放區型別的名稱。 請參閱 `storeType` 的引數 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 函式。

**傳回**

存放區型別的物件。 物件屬性是存放區型別名稱，而屬性值是已登入的存放區候選陣列。

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

從註冊的候選者中傳回存放區型別。 如果登入了多個相同名稱的存放區型別，此函式會傳回具有最高優先順序的存放區型別。

**引數**

* storeType： （字串）存放區候選的名稱。 請參閱 `storeType` 的引數 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 函式。

**傳回**

代表已登入的存放區候選者的物件。 如果未登入要求的存放區型別，則會擲回錯誤。

#### getSupportedStoreTypes() {#getsupportedstoretypes}

傳回註冊為候選商店的商店型別名稱。 此函式不需要引數。

**傳回**

字串值的陣列，其中每個字串是用來登入存放區候選的存放區型別。 請參閱 `storeType` 的引數 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 函式。

#### registerStoreCandidate(store， storeType， priority， applies) {#registerstorecandidate-store-storetype-priority-applies}

使用名稱和優先順序將存放區物件註冊為存放區候選。

優先順序是指示同名存放區之重要性的數字。 當使用與已登入的候選商店相同的名稱登入候選商店時，會使用具有較高優先順序的候選商店。 註冊存放區候選時，只有當優先順序高於同名已註冊存放區候選時，才會註冊存放區。

**引數**

* **商店：** （物件）要註冊為存放區候選者的存放區物件。
* **storeType：** （字串）候選商店的名稱。 在建立存放區候選的執行個體時，需要此值。
* **優先順序：** （數字）商店候選者的優先順序。
* **套用：** （函式）要呼叫的函式，用於評估存放區在目前環境中的適用性。 函式必須傳回 `true` 如果存放區適用，且 `false` 否則。 預設值是傳回true的函式： `function() {return true;}`

**範例**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
