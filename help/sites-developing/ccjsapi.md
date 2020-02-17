---
title: 用戶端內容Javascript API
seo-title: 用戶端內容Javascript API
description: 用戶端內容的Javascript API
seo-description: 用戶端內容的Javascript API
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 用戶端內容Javascript API{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

CQ_Analytics.ClientContextMgr物件是包含一組自行註冊的工作階段儲存區的單例，並提供註冊、保存和管理工作階段儲存區的方法。

擴充CQ_Analytics.PeristedSessionStore。

### Methods {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

傳回指定名稱的作業存放區。 另請參閱 [訪問會話儲存](/help/sites-developing/client-context.md#accessing-session-stores)。

**參數**

* 名稱：字串。 會話儲存的名稱。

**退貨**

CQ_Analytics.SessionStore物件，代表指定名稱的作業存放區。 當指 `null` 定名稱不存在儲存時返回。

#### register(sessionstore) {#register-sessionstore}

使用用戶端內容註冊會話儲存。 完成時觸發儲存寄存器和儲存更新事件。

**參數**

* sessionstore:CQ_Analytics.SessionStore。 要註冊的會話儲存對象。

**退貨**

無返回值。

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

提供監聽作業商店啟動和註冊的方法。 另請參 [閱檢查會話儲存是否已定義和初始化](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized)。

### Methods {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

註冊在初始化會話儲存時調用的回調函式。 對於已初始化多次的儲存，請指定回調延遲，使回調函式只被調用一次：

* 當儲存器在先前初始化的延遲期間被初始化時，前一個函式調用被取消，並且該函式被再次調用以用於當前初始化。
* 如果延遲期在後續初始化之前過期，則會執行兩次回呼函式。

例如，作業商店是以JSON物件為基礎，並透過JSON請求擷取。 可能出現下列初始化情形：

* 請求完成，資料被檢索並載入到儲存中。 在這種情況下，初始化只進行一次。
* 請求失敗（逾時）。 在這種情況下，不會進行初始化，並且儲存中沒有資料。
* 商店已預先填入預設值（init屬性），但請求失敗（逾時）。 只有一個初始化具有預設值。
* 商店已預先填入。

當延遲設為或 `true` 毫秒數時，方法會在呼叫回呼方法之前等待。 如果在傳遞延遲之前觸發另一個初始化事件，則會等到延遲時間超過而未發生初始化事件。 這可讓您等候觸發第二個初始化事件，並在最佳情況下呼叫回呼函式。

**參數**

* storeName:字串。 要添加監聽程式的會話儲存的名稱。
* 回呼：函式。 在儲存初始化時調用的函式。
* 延遲：布爾值或數字。 延遲呼叫回呼函式的時間量（以毫秒為單位）。 布爾值使 `true` 用預設延遲 `200 ms`。 布爾值或負 `false` 數不會導致使用延遲。

**退貨**

無返回值。

#### onStoreRegistered(storeName, callback) {#onstoreregistered-storename-callback}

註冊在註冊會話儲存時調用的回調函式。 註冊事件發生在將商店註冊到 [CQ_Analytics.ClientContextMgr時](#cq-analytics-clientcontextmgr)。

**參數**

* storeName:字串。 要添加監聽程式的會話儲存的名稱。
* 回呼：函式。 在儲存初始化時調用的函式。

**退貨**

無返回值。

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

包含JSON資料的非持續作業商店。 從外部JSONP服務檢索資料。 使用 `getInstance` 或 `getRegisteredInstance` 方法建立此類的實例。

擴充CQ_Analytics.JSONStore。

### 屬性 {#properties}

如需繼承的屬性，請參閱CQ_Analytics.JSONStore和CQ_Analytics.SessonStore。

### Methods {#methods-2}

另請參閱CQ_Analytics.JSONStore和CQ_Analytics.SessonStore以取得繼承的方法。

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

建立CQ_Analytics.JSONPStore物件。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值會設為storeName，其中包含所有大寫字元。 如果未提供storeName，則方法返回null。
* serviceURL:字串。 JSONP服務的URL
* dynamicData:（可選）物件。 在呼叫回呼函式前附加至商店初始化資料的JSON資料。
* deferLoading:（選用）布林值。 值true可防止在建立對象時調用JSONP服務。 值false會導致調用JSONP服務。
* loadingCallback:（選用）字串。 調用處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**退貨**

新的CQ_Analytics.JSONPStore物件，若storeName為null，則為null。

#### getServiceURL() {#getserviceurl}

擷取此物件用來擷取JSON資料的JSONP服務URL。

**參數**

無.

**退貨**

代表服務URL的字串，若未設定服務URL，則為null。

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

呼叫JSONP服務。 JSONP URL是服務URL的尾碼，其中包含給定回呼函式名稱。

**參數**

* serviceURL:（選用）字串。 JSONP服務。 值null會使用已配置的服務URL。 非空值設定要用於此對象的JSONP服務。 （請參閱setServiceURL。）
* dynamicData:（可選）物件。 在呼叫回呼函式前附加至商店初始化資料的JSON資料。
* 回呼：（選用）字串。 調用處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**退貨**

無返回值。

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

建立CQ_Analytics.JSONPStore物件，並使用用戶端內容註冊商店。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值會設為storeName，其中包含所有大寫字元。 如果未提供storeName，則方法返回null。
* serviceURL:（選用）字串。 JSONP服務的URL。
* dynamicData:（可選）物件。 在呼叫回呼函式前附加至商店初始化資料的JSON資料。
* 回呼：（選用）字串。 調用處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**退貨**

已註冊的CQ_Analytics.JSONPStore物件。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

設定JSONP服務的URL以用於擷取JSON資料。

**參數**

* serviceURL:字串。 提供JSON資料的JSONP服務URL

**退貨**

無返回值。

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

JSON物件的容器。 建立此類別的例項，以建立包含JSON資料的非持續作業商店：

`myjsonstore = new CQ_Analytics.JSONStore`

您可以定義一組資料，在初始化時填入儲存。

擴充CQ_Analytics.SessionStore。

### 屬性 {#properties-1}

#### STOREKEY {#storekey}

識別商店的金鑰。 使用方 `getInstance` 法來擷取此值。

#### STORENAME {#storename}

商店名稱。 使用方 `getInstance` 法來擷取此值。

### Methods {#methods-3}

另請參閱CQ_Analytics.SessionStore以取得繼承的方法。

#### 清除() {#clear}

刪除會話儲存資料並刪除所有初始化屬性。

**參數**

無.

**退貨**

無返回值。

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

建立具有指定名稱的CQ_Analytics.JSONStore物件，並以指定的JSON資料初始化（呼叫initJSON方法）。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值會設為storeName，其中包含所有大寫字元。
* jsonData:物件。 包含JSON資料的物件。

**退貨**

CQ_Analytics.JSONStore物件。

#### getJSON() {#getjson}

擷取JSON格式作業存放區的資料。

**參數**

無.

**退貨**

以JSON格式表示儲存資料的物件。

#### init() {#init}

清除會話儲存，並使用初始化屬性對其進行初始化。 將初始化標幟設 `true` 為，然後觸發 `initialize` 和 `update` 事件。

**參數**

無.

**退貨**

沒有傳回的資料。

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

從JSON物件中的資料建立初始化屬性。 您可以選擇移除所有現有的初始化屬性。

屬性名稱是從JSON物件中的資料階層衍生而來。 下列范常式式碼代表JSON物件：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

在此範例中，會在商店中建立下列屬性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**參數**

* jsonData:包含要儲存之資料的JSON物件。
* doNotClear:值true會保留現有的初始化屬性，並新增從JSON物件衍生的屬性。 值false會先移除現有的初始化屬性，再新增從JSON物件衍生的屬性。

**退貨**

無返回值。

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

建立具有指定名稱的CQ_Analytics.JSONStore物件，並以指定的JSON資料初始化（呼叫initJSON方法）。 新物件會自動在Clickstream Cloud Manager中註冊。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值會設為storeName，其中包含所有大寫字元。
* jsonData:物件。 包含JSON資料的物件。

**退貨**

CQ_Analytics.JSONStore物件。

## CQ_Analytics.可觀察 {#cq-analytics-observable}

引發事件，並允許其他物件監聽這些事件並做出反應。 擴充此類別的類別可觸發導致呼叫聆聽者的事件。

### Methods {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

註冊事件的偵聽器。 另請參 [閱建立偵聽器以對會話儲存更新做出反應](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update)。

**參數**

* 事件：字串。 要監聽的事件的名稱。
* fct:函式。 發生事件時呼叫的函式。
* 範圍：（可選）物件。 執行處理程式函式的範圍。 handler函式的&quot;this&quot;上下文。

**退貨**

無返回值。

#### removeListener(event, fct) {#removelistener-event-fct}

移除事件的指定事件處理常式。

**參數**

* 事件：字串。 事件的名稱。
* fct:函式。 事件處理常式。

**退貨**

無返回值。

## CQ_Analyics.PeristingJSONPStore {#cq-analyics-persistedjsonpstore}

從遠端JSONP服務擷取之JSON物件的持續容器。

擴充CQ_Analytics.PeristedJSONStore。

### Methods {#methods-5}

另請參閱CQ_Analytics.PeristingJSONStore以取得繼承的方法。

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

建立CQ_Analytics.PersiantJSONPStore物件。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值會設為storeName，其中包含所有大寫字元。 如果未提供storeName，則方法返回null。
* serviceURL:字串。 JSONP服務的URL
* dynamicData:（可選）物件。 在呼叫回呼函式前附加至商店初始化資料的JSON資料。
* deferLoading:（選用）布林值。 值true可防止在建立對象時調用JSONP服務。 值false會導致調用JSONP服務。
* loadingCallback:（選用）字串。 調用處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**退貨**

新的CQ_Analytics.PeristedJSONPStore物件，若storeName為null，則為null。

#### getServiceURL() {#getserviceurl-1}

擷取此物件用來擷取JSON資料的JSONP服務URL。

**參數**

無.

**退貨**

代表服務URL的字串，若未設定服務URL，則為null。

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

呼叫JSONP服務。 JSONP URL是服務URL的尾碼，其中包含給定回呼函式名稱。

**參數**

* serviceURL:（選用）字串。 JSONP服務。 值null會使用已配置的服務URL。 非空值設定要用於此對象的JSONP服務。 （請參閱setServiceURL。）
* dynamicData:（可選）物件。 在呼叫回呼函式前附加至商店初始化資料的JSON資料。
* 回呼：（選用）字串。 調用處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**退貨**

無返回值。

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

建立CQ_Analytics.PeristedJSONPStore物件，並使用用戶端內容註冊商店。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值會設為storeName，其中包含所有大寫字元。 如果未提供storeName，則方法返回null。
* serviceURL:（選用）字串。 JSONP服務的URL。
* dynamicData:（可選）物件。 在呼叫回呼函式前附加至商店初始化資料的JSON資料。
* 回呼：（選用）字串。 調用處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**退貨**

已註冊的CQ_Analytics.PeristedJSONPStore物件。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

設定JSONP服務的URL以用於擷取JSON資料。

**參數**

* serviceURL:字串。 提供JSON資料的JSONP服務URL

**退貨**

無返回值。

## CQ_Analytics.PeristingJSONStore {#cq-analytics-persistedjsonstore}

JSON物件的持續容器。

延伸 `CQ_Analytics.PersistedSessionStore`。

### 屬性 {#properties-2}

#### STOREKEY {#storekey-1}

識別商店的金鑰。 使用方 `getInstance` 法來擷取此值。

#### STORENAME {#storename-1}

商店名稱。 使用方 `getInstance` 法來擷取此值。

### Methods {#methods-6}

另請參閱CQ_Analytics.PeristedSessionStore以取得繼承的方法。

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

建立具有指定名稱的CQ_Analytics.PeristandJSONStore物件，並以指定的JSON資料初始化（呼叫initJSON方法）。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值會設為storeName，其中包含所有大寫字元。
* jsonData:物件。 包含JSON資料的物件。

**退貨**

CQ_Analytics.PeristingJSONStore物件。

#### getJSON() {#getjson-1}

擷取JSON格式作業存放區的資料。

**參數**

無.

**退貨**

以JSON格式表示儲存資料的物件。

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

從JSON物件中的資料建立初始化屬性。 您可以選擇移除所有現有的初始化屬性。

屬性名稱是從JSON物件中的資料階層衍生而來。 下列范常式式碼代表JSON物件：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

在此範例中，會在商店中建立下列屬性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**參數**

* jsonData:包含要儲存之資料的JSON物件。
* doNotClear:值true會保留現有的初始化屬性，並新增從JSON物件衍生的屬性。 值false會先移除現有的初始化屬性，再新增從JSON物件衍生的屬性。

**退貨**

無返回值。

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

建立具有指定名稱的CQ_Analytics.PeristandJSONStore物件，並以指定的JSON資料初始化（呼叫initJSON方法）。 新對象會自動向「客戶端上下文管理器」註冊。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值會設為storeName，其中包含所有大寫字元。
* jsonData:物件。 包含JSON資料的物件。

**退貨**

CQ_Analytics.PeristingJSONStore物件。

## CQ_Analytics.PeristedSessionStore {#cq-analytics-persistedsessionstore}

屬性和值的容器。 資料會使用CQ_Analytics.SessionPersistence來保存。 建立此類別的例項，以建立持續作業商店：

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

擴充CQ_Analytics.SessionStore。

### 屬性 {#properties-3}

#### STOREKEY {#storekey-2}

預設值為 `key`.

### Methods {#methods-7}

如需繼承的方法，請參閱CQ_Analytics.SessionStore。

當繼承的方 `clear`法 `setProperty`、 `setProperties`、、用來變 `removeProperty` 更儲存資料時，變更會自動持續，除非變更的屬性被標幟為notPeristend。

#### getStoreKey() {#getstorekey}

檢索屬 `STOREKEY` 性。

**參數**

無

**退貨**

屬性的 `STOREKEY` 值。

#### isPersiant(name) {#ispersisted-name}

判斷資料屬性是否持續存在。

**參數**

* 名稱：字串。 屬性的名稱。

**退貨**

Boolean值： `true` if屬性持續存在，值： `false` if值不是持續屬性。

#### persist() {#persist}

持續存在會話儲存。 預設永續性模式使用瀏 `localStorage` 覽器 `ClientSidePersistence` 作為名稱( `window.localStorage.set("ClientSidePersistance", store);`)

如果localStorage不可用或不可寫，則儲存會作為窗口的屬性保存。

完成時 `persist` 觸發事件。

**參數**

無

**退貨**

無返回值。

#### reset(deferEvent) {#reset-deferevent}

從儲存中刪除所有資料屬性並保留儲存。 （可選）不會在完成 `udpate` 時觸發事件。

**參數**

* deferEvent:值true可防止引 `update` 發事件。 值會引 `false` 發更新事件。

**退貨**

無返回值。

#### setNonPersiant(name) {#setnonpersisted-name}

將資料屬性標示為未持續存在。

**參數**

* 名稱：字串。 不持續的屬性名稱。

**退貨**

無返回值。

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore代表作業商店。 建立此類的實例以建立會話儲存：

`mystore = new CQ_Analytics.SessionStore`

擴充CQ_Analytics.Ovetable。

### 屬性 {#properties-4}

#### STORENAME {#storename-2}

會話儲存的名稱。 使用getName檢索此屬性的值。

### Methods {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

將屬性和值添加到會話儲存初始化資料。

使用loadInitProperties將會話儲存資料填入初始化值。

**參數**

* 名稱：字串。 要添加的屬性的名稱。
* 值：字串。 要添加的屬性值。

**退貨**

無返回值。

#### 清除() {#clear-1}

從儲存中刪除所有資料屬性。

**參數**

無.

**退貨**

無返回值。

#### getData（已排除） {#getdata-excluded}

傳回儲存資料。 （可選）從資料中排除名稱屬性。 如果存 `init` 儲的data屬性不存在，則調用方法。

**參數**

excluded:（選用）要從傳回資料中排除的屬性名稱陣列。

**退貨**

屬性及其值的對象。

#### getInitProperty(name) {#getinitproperty-name}

擷取資料屬性的值。

**參數**

* 名稱：字串。 要檢索的資料屬性的名稱。

**退貨**

資料屬性的值。 如果 `null` 會話儲存不包含給定名稱的屬性，則返回。

#### getName() {#getname}

返回會話儲存的名稱。

**參數**

無.

**退貨**

代表商店名稱的字串值。

#### getProperty(name, raw) {#getproperty-name-raw}

傳回屬性的值。 值會傳回為原始屬性或XSS篩選的值。 如果存 `init` 儲的data屬性不存在，則調用方法。

**參數**

* 名稱：字串。 要檢索的資料屬性的名稱。
* 原始：布林。 值true會傳回原始屬性值。 值false會使傳回的值經過XSS篩選。

**退貨**

資料屬性的值。

#### getPropertyNames(excluded) {#getpropertynames-excluded}

返回會話儲存所包含的屬性的名稱。 如果存 `init` 儲的data屬性不存在，則調用方法。

**參數**

excluded:（可選）要從結果中忽略的屬性名稱陣列。

**退貨**

代表會話屬性名稱的字串值陣列。

#### getSessionStore() {#getsessionstore}

返回附加到當前對象的會話儲存。

**參數**

無.

**退貨**

this

#### init() {#init-1}

將商店標示為已初始化，並引發 `initialize` 事件。

**參數**

無.

**退貨**

無返回值。

#### isInitialized() {#isinitialized}

指示會話儲存是否已初始化。

**參數**

無.

**退貨**

如果儲存 `true` 被初始化，則值為；如果儲存未 `false` 被初始化，則值為。

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

將給定對象的屬性添加到會話儲存的初始化資料。 或者，對象資料也被添加到儲存資料中。

**參數**

* obj:包含可枚舉屬性的對象。
* setValues:如果為true，則如果儲存資料尚未包含同名的屬性，則obj屬性將添加到會話儲存資料。 若為false，則不會將任何資料新增至作業儲存資料。

**退貨**

無返回值。

#### removeProperty(name) {#removeproperty-name}

從會話儲存中刪除屬性。 完成時 `update` 觸發事件。 如果存 `init` 儲的data屬性不存在，則調用方法。

**參數**

* 名稱：字串。 要移除的屬性名稱。

**退貨**

無返回值。

#### 重設() {#reset}

恢復資料儲存的初始值。 預設實作只會移除所有資料。 完成時 `update` 觸發事件。

**參數**

無.

**退貨**

無返回值。

#### setProperties(properties) {#setproperties-properties}

設定多個屬性的值。 完成時 `update` 觸發事件。 如果存 `init` 儲的data屬性不存在，則調用方法。

**參數**

* 屬性：物件。 包含可枚舉屬性的對象。 每個屬性名稱和值都會新增至商店。

**退貨**

無返回值。

#### setProperty(name, value) {#setproperty-name-value}

設定屬性的值。 完成時 `update` 觸發事件。 如果存 `init` 儲的data屬性不存在，則調用方法。

**參數**

* 名稱：字串。 屬性的名稱。
* 值：字串。 屬性值。

**退貨**

無返回值。
