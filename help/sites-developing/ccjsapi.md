---
title: 客戶端上下文Javascript API
seo-title: Client Context Javascript API
description: 客戶端上下文的Javascript API
seo-description: The Javascript API for Client Context
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
feature: Context Hub
exl-id: 24bdf9fc-71e6-4b99-9dad-0f41a5e36b98
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3153'
ht-degree: 2%

---

# 客戶端上下文Javascript API{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

CQ_Analytics.ClientContextMgr對象是一個單據，它包含一組自註冊的會話儲存，並提供了註冊、保留和管理會話儲存的方法。

擴展CQ_Analytics.PeristedSessionStore。

### 方法 {#methods}

#### getRegisteredStore（名稱） {#getregisteredstore-name}

返回指定名稱的會話儲存。 另請參閱 [訪問會話儲存](/help/sites-developing/client-context.md#accessing-session-stores)。

**參數**

* 名稱：字串。 會話儲存的名稱。

**返回**

表示給定名稱的會話儲存的CQ_Analytics.SessionStore對象。 返回 `null` 當不存在給定名稱的儲存時。

#### 註冊（會話儲存） {#register-sessionstore}

使用客戶端上下文註冊會話儲存。 完成時觸發儲存寄存器和儲存更新事件。

**參數**

* 會話儲存：CQ_Analytics.SessionStore。 要註冊的會話儲存對象。

**返回**

沒有返回值。

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

提供監聽會話儲存激活和註冊的方法。 另請參閱 [檢查是否定義並初始化會話儲存](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized)。

### 方法 {#methods-1}

#### onStoreInitialized（storeName，回調，延遲） {#onstoreinitialized-storename-callback-delay}

註冊在初始化會話儲存時調用的回調函式。 對於多次初始化的儲存，請指定回調延遲，以便只調用一次回調函式：

* 當儲存器在先前初始化的延遲期間被初始化時，取消先前函式調用，並且再次調用該函式以用於當前初始化。
* 如果延遲期在後續初始化之前結束，則執行兩次回調函式。

例如，會話儲存基於JSON對象，並通過JSON請求檢索。 以下初始化方案可能：

* 請求完成，資料被檢索並載入到儲存中。 在這種情況下，初始化只發生一次。
* 請求失敗（超時）。 在這種情況下，不會進行初始化，並且儲存中沒有資料。
* 儲存預填充了預設值（init屬性），但請求失敗（超時）。 只有一個初始化，其中包含預設值。
* 商店已預裝。

當延遲設定為 `true` 或者，方法在調用回調方法之前等待。 如果在延遲傳遞之前觸發了另一個初始化事件，則它將等到延遲時間被超過而沒有初始化事件。 這允許等待觸發第二個初始化事件，並在最佳情況下調用回調函式。

**參數**

* 儲存名稱：字串。 要添加監聽程式的會話儲存的名稱。
* 回調：函式。 在儲存初始化時調用的函式。
* 延遲：布爾或數字。 延遲調用回調函式的時間（毫秒）。 布爾值 `true` 使用預設延遲 `200 ms`。 布爾值 `false` 或者負數不導致使用延遲。

**返回**

沒有返回值。

#### onStoreRegistered（storeName，回調） {#onstoreregistered-storename-callback}

註冊在註冊會話儲存時調用的回調函式。 當儲存註冊到 [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr)。

**參數**

* 儲存名稱：字串。 要添加監聽程式的會話儲存的名稱。
* 回調：函式。 在儲存初始化時調用的函式。

**返回**

沒有返回值。

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

包含JSON資料的非永續會話儲存。 從外部JSONP服務檢索資料。 使用 `getInstance` 或 `getRegisteredInstance` 方法建立此類的實例。

擴展CQ_Analytics.JSONStore。

### 屬性 {#properties}

有關繼承的屬性，請參見CQ_Analytics.JSONStore和CQ_Analytics.SessonStore。

### 方法 {#methods-2}

有關繼承的方法，請參見CQ_Analytics.JSONStore和CQ_Analytics.SessonStore。

#### getInstance(storeName、serviceURL、dynamicData、deferLoading、loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

建立CQ_Analytics.JSONPStore對象。

**參數**

* 儲存名稱：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設定為storeName並包含所有大寫字元。 如果未提供storeName，則此方法返回null。
* 服務URL:字串。 JSONP服務的URL
* 動態資料：（可選）對象。 在調用回調函式之前要追加到儲存的初始化資料的JSON資料。
* deferLoading:（可選）布爾型。 值為true可防止在建立對象時調用JSONP服務。 值false將導致調用JSONP服務。
* 載入回調：（可選）字串。 要調用處理JSONP服務返回的JSONP對象的函式的名稱。 回調函式必須定義CQ_Analytics.JSONPStore對象的單個參數。

**返回**

新的CQ_Analytics.JSONPStore對象，或如果storeName為null，則為null。

#### getServiceURL() {#getserviceurl}

檢索此對象用於檢索JSON資料的JSONP服務的URL。

**參數**

無。

**返回**

表示服務URL的字串；如果未配置服務URL，則為null。

#### load（serviceURL、dynamicData、回調） {#load-serviceurl-dynamicdata-callback}

呼叫JSONP服務。 JSONP URL是帶給回調函式名稱尾碼的服務URL。

**參數**

* 服務URL:（可選）字串。 JSONP服務。 值為null時，將使用已配置的服務URL。 非空值設定要用於此對象的JSONP服務。 （請參閱setServiceURL。）
* 動態資料：（可選）對象。 在調用回調函式之前要追加到儲存的初始化資料的JSON資料。
* 回調：（可選）字串。 要調用處理JSONP服務返回的JSONP對象的函式的名稱。 回調函式必須定義CQ_Analytics.JSONPStore對象的單個參數。

**返回**

沒有返回值。

#### registerNewInstance（storeName、serviceURL、dynamicData、回調） {#registernewinstance-storename-serviceurl-dynamicdata-callback}

建立CQ_Analytics.JSONPStore對象，並在客戶端上下文中註冊儲存。

**參數**

* 儲存名稱：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設定為storeName並包含所有大寫字元。 如果未提供storeName，則此方法返回null。
* 服務URL:（可選）字串。 JSONP服務的URL。
* 動態資料：（可選）對象。 在調用回調函式之前要追加到儲存的初始化資料的JSON資料。
* 回調：（可選）字串。 要調用處理JSONP服務返回的JSONP對象的函式的名稱。 回調函式必須定義CQ_Analytics.JSONPStore對象的單個參數。

**返回**

已註冊的CQ_Analytics.JSONPStore對象。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

設定JSONP服務的URL以用於檢索JSON資料。

**參數**

* 服務URL:字串。 提供JSON資料的JSONP服務的URL

**返回**

沒有返回值。

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

JSON對象的容器。 建立此類的實例以建立包含JSON資料的非永續會話儲存：

`myjsonstore = new CQ_Analytics.JSONStore`

您可以定義一組資料，這些資料在初始化時填充儲存。

擴展CQ_Analytics.SessionStore。

### 屬性 {#properties-1}

#### 儲存鍵 {#storekey}

標識儲存的密鑰。 使用 `getInstance` 方法來檢索此值。

#### 儲存更名 {#storename}

商店的名稱。 使用 `getInstance` 方法來檢索此值。

### 方法 {#methods-3}

另請參見CQ_Analytics.SessionStore以瞭解繼承的方法。

#### 清除() {#clear}

刪除會話儲存資料並刪除所有初始化屬性。

**參數**

無。

**返回**

沒有返回值。

#### getInstance(storeName、jsonData) {#getinstance-storename-jsondata}

使用給定名稱建立CQ_Analytics.JSONStore對象，並使用給定JSON資料進行初始化（調用initJSON方法）。

**參數**

* 儲存名稱：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設定為storeName並包含所有大寫字元。
* json資料：對象。 包含JSON資料的對象。

**返回**

CQ_Analytics.JSONStore對象。

#### getJSON() {#getjson}

以JSON格式檢索會話儲存的資料。

**參數**

無。

**返回**

以JSON格式表示儲存資料的對象。

#### init() {#init}

清除會話儲存並使用initialization屬性初始化它。 將初始化標誌設定為 `true` 然後放火 `initialize` 和 `update` 事件。

**參數**

無。

**返回**

未返回資料。

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

從JSON對象中的資料建立初始化屬性。 您可以選擇刪除所有現有的初始化屬性。

屬性的名稱是從JSON對象中資料的層次中派生的。 以下示例代碼表示JSON對象：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

在此示例中，在儲存中建立了以下屬性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**參數**

* json資料：包含要儲存的資料的JSON對象。
* 不清除：值為true將保留現有初始化屬性，並添加從JSON對象派生的屬性。 如果值為false，則在添加從JSON對象派生的屬性之前刪除現有的初始化屬性。

**返回**

沒有返回值。

#### registerNewInstance(storeName、jsonData) {#registernewinstance-storename-jsondata}

使用給定名稱建立CQ_Analytics.JSONStore對象，並使用給定JSON資料進行初始化（調用initJSON方法）。 新對象將自動註冊到Clickstream雲管理器。

**參數**

* 儲存名稱：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設定為storeName並包含所有大寫字元。
* json資料：對象。 包含JSON資料的對象。

**返回**

CQ_Analytics.JSONStore對象。

## CQ_Analytics.可觀察 {#cq-analytics-observable}

激發事件並允許其他對象偵聽這些事件並做出反應。 擴展此類的類可以觸發導致調用偵聽器的事件。

### 方法 {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

為事件註冊偵聽器。 另請參閱 [建立偵聽器以對會話儲存更新做出響應](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update)。

**參數**

* 事件：字串。 要監聽的事件的名稱。
* fct:函式。 發生事件時調用的函式。
* 範圍：（可選）對象。 執行處理程式函式的範圍。 處理程式函式的「this」上下文。

**返回**

沒有返回值。

#### removeListener(event, fct) {#removelistener-event-fct}

刪除事件的給定事件處理程式。

**參數**

* 事件：字串。 事件的名稱。
* fct:函式。 事件處理程式。

**返回**

沒有返回值。

## CQ_Analycis.PeristedJSONPStore {#cq-analyics-persistedjsonpstore}

從遠程JSONP服務檢索的JSON對象的永續容器。

擴展CQ_Analytics.PeristedJSONStore。

### 方法 {#methods-5}

另請參見CQ_Analytics.PeristedJSONStore以瞭解繼承的方法。

#### getInstance(storeName、serviceURL、dynamicData、deferLoading、loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

建立CQ_Analytics.PersiedJSONPStore對象。

**參數**

* 儲存名稱：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設定為storeName並包含所有大寫字元。 如果未提供storeName，則此方法返回null。
* 服務URL:字串。 JSONP服務的URL
* 動態資料：（可選）對象。 在調用回調函式之前要追加到儲存的初始化資料的JSON資料。
* deferLoading:（可選）布爾型。 值為true可防止在建立對象時調用JSONP服務。 值false將導致調用JSONP服務。
* 載入回調：（可選）字串。 要調用處理JSONP服務返回的JSONP對象的函式的名稱。 回調函式必須定義CQ_Analytics.JSONPStore對象的單個參數。

**返回**

新的CQ_Analytics.PersiedJSONPStore對象，如果storeName為null，則為null。

#### getServiceURL() {#getserviceurl-1}

檢索此對象用於檢索JSON資料的JSONP服務的URL。

**參數**

無。

**返回**

表示服務URL的字串；如果未配置服務URL，則為null。

#### load（serviceURL、dynamicData、回調） {#load-serviceurl-dynamicdata-callback-1}

呼叫JSONP服務。 JSONP URL是帶給回調函式名稱尾碼的服務URL。

**參數**

* 服務URL:（可選）字串。 JSONP服務。 值為null時，將使用已配置的服務URL。 非空值設定要用於此對象的JSONP服務。 （請參閱setServiceURL。）
* 動態資料：（可選）對象。 在調用回調函式之前要追加到儲存的初始化資料的JSON資料。
* 回調：（可選）字串。 要調用處理JSONP服務返回的JSONP對象的函式的名稱。 回調函式必須定義CQ_Analytics.JSONPStore對象的單個參數。

**返回**

沒有返回值。

#### registerNewInstance（storeName、serviceURL、dynamicData、回調） {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

建立CQ_Analytics.PersiedJSONPStore對象，並將儲存註冊到客戶端上下文。

**參數**

* 儲存名稱：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設定為storeName並包含所有大寫字元。 如果未提供storeName，則此方法返回null。
* 服務URL:（可選）字串。 JSONP服務的URL。
* 動態資料：（可選）對象。 在調用回調函式之前要追加到儲存的初始化資料的JSON資料。
* 回調：（可選）字串。 要調用處理JSONP服務返回的JSONP對象的函式的名稱。 回調函式必須定義CQ_Analytics.JSONPStore對象的單個參數。

**返回**

已註冊的CQ_Analytics.PeristedJSONPStore對象。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

設定JSONP服務的URL以用於檢索JSON資料。

**參數**

* 服務URL:字串。 提供JSON資料的JSONP服務的URL

**返回**

沒有返回值。

## CQ_Analytics.PeristedJSONStore {#cq-analytics-persistedjsonstore}

JSON對象的永續容器。

擴展 `CQ_Analytics.PersistedSessionStore`。

### 屬性 {#properties-2}

#### 儲存鍵 {#storekey-1}

標識儲存的密鑰。 使用 `getInstance` 方法來檢索此值。

#### 儲存更名 {#storename-1}

商店的名稱。 使用 `getInstance` 方法來檢索此值。

### 方法 {#methods-6}

另請參見CQ_Analytics.PeristedSessionStore以瞭解繼承的方法。

#### getInstance(storeName、jsonData) {#getinstance-storename-jsondata-1}

建立具有給定名稱的CQ_Analytics.PeristedJSONStore對象，並使用給定的JSON資料進行初始化（調用initJSON方法）。

**參數**

* 儲存名稱：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設定為storeName並包含所有大寫字元。
* json資料：對象。 包含JSON資料的對象。

**返回**

CQ_Analytics.PeristedJSONStore對象。

#### getJSON() {#getjson-1}

以JSON格式檢索會話儲存的資料。

**參數**

無。

**返回**

以JSON格式表示儲存資料的對象。

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

從JSON對象中的資料建立初始化屬性。 您可以選擇刪除所有現有的初始化屬性。

屬性的名稱是從JSON對象中資料的層次中派生的。 以下示例代碼表示JSON對象：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

在此示例中，在儲存中建立了以下屬性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**參數**

* json資料：包含要儲存的資料的JSON對象。
* 不清除：值為true將保留現有初始化屬性，並添加從JSON對象派生的屬性。 如果值為false，則在添加從JSON對象派生的屬性之前刪除現有的初始化屬性。

**返回**

沒有返回值。

#### registerNewInstance(storeName、jsonData) {#registernewinstance-storename-jsondata-1}

建立具有給定名稱的CQ_Analytics.PeristedJSONStore對象，並使用給定的JSON資料進行初始化（調用initJSON方法）。 新對象將自動註冊到「客戶端上下文管理器」。

**參數**

* 儲存名稱：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設定為storeName並包含所有大寫字元。
* json資料：對象。 包含JSON資料的對象。

**返回**

CQ_Analytics.PeristedJSONStore對象。

## CQ_Analytics.PeristedSessionStore {#cq-analytics-persistedsessionstore}

屬性和值的容器。 資料是使用CQ_Analytics.SessionPersistence保留的。 建立此類的實例以建立永續會話儲存：

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

擴展CQ_Analytics.SessionStore。

### 屬性 {#properties-3}

#### 儲存鍵 {#storekey-2}

預設值為 `key`.

### 方法 {#methods-7}

有關繼承的方法，請參見CQ_Analytics.SessionStore。

當繼承的方法 `clear`。 `setProperty`。 `setProperties`。 `removeProperty` 用於更改儲存資料，除非已更改的屬性被標籤為notPersided，否則這些更改將自動保留。

#### getStoreKey() {#getstorekey}

檢索 `STOREKEY` 屬性。

**參數**

無

**返回**

的值 `STOREKEY` 屬性。

#### isPersided(name) {#ispersisted-name}

確定是否保留資料屬性。

**參數**

* 名稱：字串。 屬性的名稱。

**返回**

布爾值 `true` 如果屬性永續，並且 `false` 如果值不是持久屬性。

#### persist() {#persist}

保留會話儲存。 預設持久性模式使用瀏覽器 `localStorage` 使用 `ClientSidePersistence` 名稱( `window.localStorage.set("ClientSidePersistance", store);`)

如果localStorage不可用或不可寫，則儲存將保留為窗口的屬性。

激發 `persist` 事件。

**參數**

無

**返回**

沒有返回值。

#### reset(deferEvent) {#reset-deferevent}

從儲存中刪除所有資料屬性並保留儲存。 （可選）不觸發 `udpate` 事件。

**參數**

* deferEvent:值為true可防止 `update` 激發事件。 值 `false` 導致更新事件觸發。

**返回**

沒有返回值。

#### setNonPersided（名稱） {#setnonpersisted-name}

將資料屬性標籤為未永續。

**參數**

* 名稱：字串。 不要永續的屬性的名稱。

**返回**

無返回值。

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore表示會話儲存。 建立此類的實例以建立會話儲存：

`mystore = new CQ_Analytics.SessionStore`

擴展CQ_Analytics.Ovebable。

### 屬性 {#properties-4}

#### 儲存更名 {#storename-2}

會話儲存的名稱。 使用getName檢索此屬性的值。

### 方法 {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

向會話儲存初始化資料添加屬性和值。

使用loadInitProperties用初始化值填充會話儲存資料。

**參數**

* 名稱：字串。 要添加的屬性的名稱。
* 值：字串。 要添加的屬性的值。

**返回**

沒有返回值。

#### 清除() {#clear-1}

從儲存中刪除所有資料屬性。

**參數**

無。

**返回**

無返回值。

#### getData（排除） {#getdata-excluded}

返回儲存資料。 （可選）從資料中排除名稱屬性。 呼叫 `init` 方法。

**參數**

排除：（可選）要從返回的資料中排除的屬性名稱陣列。

**返回**

屬性及其值的對象。

#### getInitProperty(name) {#getinitproperty-name}

檢索資料屬性的值。

**參數**

* 名稱：字串。 要檢索的資料屬性的名稱。

**返回**

資料屬性的值。 返回 `null` 如果會話儲存不包含給定名稱的屬性。

#### getName() {#getname}

返回會話儲存的名稱。

**參數**

無。

**返回**

表示儲存名稱的字串值。

#### getProperty（名稱，原始） {#getproperty-name-raw}

返回屬性的值。 該值作為原始屬性或XSS篩選的值返回。 呼叫 `init` 方法。

**參數**

* 名稱：字串。 要檢索的資料屬性的名稱。
* 原始：布爾型。 如果值為true，則返回原始屬性值。 值為false將導致返回的值被XSS篩選。

**返回**

資料屬性的值。

#### getPropertyNames（排除） {#getpropertynames-excluded}

返回會話儲存包含的屬性的名稱。 呼叫 `init` 方法。

**參數**

排除：（可選）要從結果中忽略的屬性名稱陣列。

**返回**

表示會話屬性名稱的字串值陣列。

#### getSessionStore() {#getsessionstore}

返回附加到當前對象的會話儲存。

**參數**

無。

**返回**

這個

#### init() {#init-1}

將儲存標籤為已初始化並觸發 `initialize` 的子菜單。

**參數**

無。

**返回**

沒有返回值。

#### isInitialized() {#isinitialized}

指示是否初始化會話儲存。

**參數**

無。

**返回**

值 `true` 如果儲存已初始化，並且 `false` 的子菜單。

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

將給定對象的屬性添加到會話儲存的初始化資料。 可選地，對象資料也被添加到儲存資料中。

**參數**

* obj:包含可枚舉屬性的對象。
* setValues:如果為true，則如果儲存資料未包含同名的屬性，則obj屬性將添加到會話儲存資料。 如果為false，則不向會話儲存資料添加任何資料。

**返回**

沒有返回值。

#### removeProperty(name) {#removeproperty-name}

從會話儲存中刪除屬性。 激發 `update` 事件。 呼叫 `init` 方法。

**參數**

* 名稱：字串。 要刪除的屬性的名稱。

**返回**

沒有返回值。

#### 重設() {#reset}

恢復資料儲存的初始值。 預設實現只是刪除所有資料。 激發 `update` 事件。

**參數**

無。

**返回**

沒有返回值。

#### setProperties（屬性） {#setproperties-properties}

設定多個屬性的值。 激發 `update` 事件。 呼叫 `init` 方法。

**參數**

* 屬性：對象。 包含可枚舉屬性的對象。 每個屬性名稱和值都添加到儲存中。

**返回**

沒有返回值。

#### setProperty(name, value) {#setproperty-name-value}

設定屬性的值。 激發 `update` 事件。 呼叫 `init` 方法。

**參數**

* 名稱：字串。 屬性的名稱。
* 值：字串。 屬性值。

**返回**

沒有返回值。
