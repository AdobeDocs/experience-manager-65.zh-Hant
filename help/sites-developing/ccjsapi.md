---
title: Client Context JavaScript API
description: 瞭解Adobe Experience Manager中適用於Client Context的JavaScript API。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
feature: Context Hub
exl-id: 24bdf9fc-71e6-4b99-9dad-0f41a5e36b98
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '3106'
ht-degree: 0%

---

# Client Context JavaScript API{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

CQ_Analytics.ClientContextMgr物件是包含一組自我註冊工作階段存放區的單一物件，並提供註冊、持續和管理工作階段存放區的方法。

擴充CQ_Analytics.PersistedSessionStore。

### 方法 {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

傳回指定名稱的工作階段存放區。 另請參閱 [存取工作階段存放區](/help/sites-developing/client-context.md#accessing-session-stores).

**引數**

* name：字串。 工作階段存放區的名稱。

**傳回**

CQ_Analytics.SessionStore物件，代表指定名稱的工作階段存放區。 傳回 `null` 當指定的名稱不存在存放區時。

#### register(sessionstore) {#register-sessionstore}

向Client Context註冊工作階段存放區。 完成時引發storeregister和storeupdate事件。

**引數**

* sessionstore： CQ_Analytics.SessionStore。 要註冊的工作階段存放區物件。

**傳回**

沒有傳回值。

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

提供監聽工作階段存放區啟用和註冊的方法。 另請參閱 [正在檢查工作階段存放區是否已定義及初始化](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### 方法 {#methods-1}

#### onStoreInitialized(storeName， callback， delay) {#onstoreinitialized-storename-callback-delay}

註冊當工作階段存放區初始化時所呼叫的回呼函式。 對於已初始化多次的存放區，請指定回呼延遲，使回呼函式只呼叫一次：

* 當在上一個初始化的延遲期間內初始化存放區時，會取消上一個函式呼叫，並為目前初始化再次呼叫函式。
* 如果延遲期間在後續初始化發生之前過期，則會執行兩次回呼函式。

例如，工作階段存放區是以JSON物件為基礎，並透過JSON要求擷取。 可能的初始化案例如下：

* 要求完成，擷取資料並載入存放區。 在這種情況下，初始化會進行一次。
* 請求失敗（逾時）。 在這種情況下，不會進行初始化，而且存放區中沒有資料。
* 存放區已預先填入預設值（初始屬性），但請求失敗（逾時）。 只有一個預設值的初始化。
* 系統會預先填入存放區。

當延遲設定為 `true` 或幾毫秒後，方法會先等候再呼叫回呼方法。 如果在傳遞延遲之前觸發另一個初始化事件，則會等到超過延遲時間再觸發初始化事件。 這可讓等候觸發第二個初始化事件，並在最佳情況下呼叫回呼函式。

**引數**

* storeName：字串。 要新增監聽器的工作階段存放區名稱。
* callback：函式。 在存放區初始化時要呼叫的函式。
* 延遲：布林值或數字。 延遲呼叫回呼函式的時間長度，以毫秒為單位。 布林值 `true` 使用預設的延遲 `200 ms`. 布林值 `false` 或負數會造成無延遲使用。

**傳回**

沒有傳回值。

#### onStoreRegistered(storeName， callback) {#onstoreregistered-storename-callback}

註冊在註冊工作階段存放區時所呼叫的回呼函式。 註冊存放區時，會發生註冊事件 [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**引數**

* storeName：字串。 要新增監聽器的工作階段存放區名稱。
* callback：函式。 在存放區初始化時要呼叫的函式。

**傳回**

沒有傳回值。

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

包含JSON資料的非持續性工作階段存放區。 資料會從外部JSONP服務擷取。 使用 `getInstance` 或 `getRegisteredInstance` 方法以建立此類別的實體。

擴充CQ_Analytics.JSONStore。

### 屬性 {#properties}

如需繼承的屬性，請參閱CQ_Analytics.JSONStore和CQ_Analytics.SessionStore 。

### 方法 {#methods-2}

另請參閱CQ_Analytics.JSONStore和CQ_Analytics.SessionStore以瞭解繼承的方法。

#### getInstance(storeName， serviceURL， dynamicData， deferLoading， loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

建立CQ_Analytics.JSONPStore物件。

**引數**

* storeName：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName （包含所有大寫字元）。 如果未提供storeName，方法會傳回null。
* serviceURL：字串。 JSONP服務的URL
* dynamicData： （選用）物件。 JSON資料，用於在呼叫回呼函式之前附加至存放區的初始化資料。
* deferLoading： （選用）布林值。 如果值為true，則在建立物件時不會呼叫JSONP服務。 false值會導致呼叫JSONP服務。
* loadingCallback： （選用）字串。 呼叫用於處理JSONP服務傳回之JSONP物件的函式名稱。 回呼函式必須定義單一引數，即CQ_Analytics.JSONPStore物件。

**傳回**

新的CQ_Analytics.JSONPStore物件，或如果storeName為null則為null。

#### getServiceURL() {#getserviceurl}

擷取此物件用於擷取JSON資料的JSONP服務URL。

**引數**

無。

**傳回**

代表服務URL的字串；若未設定服務URL，則為null。

#### load(serviceURL， dynamicData， callback) {#load-serviceurl-dynamicdata-callback}

呼叫JSONP服務。 JSONP URL是尾碼為給定回呼函式名稱的服務URL。

**引數**

* serviceURL： （選用）字串。 要呼叫的JSONP服務。 如果值為null，則會使用已設定的服務URL。 非null值會設定JSONP服務用於此物件。 （請參閱setServiceURL。）
* dynamicData： （選用）物件。 JSON資料，用於在呼叫回呼函式之前附加至存放區的初始化資料。
* callback： （選用）字串。 呼叫用於處理JSONP服務傳回之JSONP物件的函式名稱。 回呼函式必須定義單一引數，即CQ_Analytics.JSONPStore物件。

**傳回**

沒有傳回值。

#### registerNewInstance(storeName， serviceURL， dynamicData， callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

建立CQ_Analytics.JSONPStore物件，並將存放區註冊到Client Context。

**引數**

* storeName：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName （包含所有大寫字元）。 如果未提供storeName，方法會傳回null。
* serviceURL： （選用）字串。 JSONP服務的URL。
* dynamicData： （選用）物件。 JSON資料，用於在呼叫回呼函式之前附加至存放區的初始化資料。
* callback： （選用）字串。 呼叫用於處理JSONP服務傳回之JSONP物件的函式名稱。 回呼函式必須定義單一引數，即CQ_Analytics.JSONPStore物件。

**傳回**

已註冊的CQ_Analytics.JSONPStore物件。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

設定用於擷取JSON資料的JSONP服務URL。

**引數**

* serviceURL：字串。 提供JSON資料的JSONP服務的URL

**傳回**

沒有傳回值。

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

JSON物件的容器。 建立此類別的例項，以建立包含JSON資料的非持續性工作階段存放區：

`myjsonstore = new CQ_Analytics.JSONStore`

您可以定義一組資料，在初始化時填入存放區。

擴充CQ_Analytics.SessionStore。

### 屬性 {#properties-1}

#### STOREKEY {#storekey}

用來識別存放區的金鑰。 使用 `getInstance` 方法以擷取此值。

#### STORENAME {#storename}

存放區的名稱。 使用 `getInstance` 方法以擷取此值。

### 方法 {#methods-3}

如需繼承的方法，另請參閱CQ_Analytics.SessionStore 。

#### clear() {#clear}

移除工作階段存放區資料，並移除所有初始化屬性。

**引數**

無。

**傳回**

沒有傳回值。

#### getInstance(storeName， jsonData) {#getinstance-storename-jsondata}

以指定名稱建立CQ_Analytics.JSONStore物件，並以指定JSON資料初始化（呼叫initJSON方法）。

**引數**

* storeName：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName （包含所有大寫字元）。
* jsonData：物件。 包含JSON資料的物件。

**傳回**

cq_Analytics.JSONStore物件。

#### getJSON() {#getjson}

擷取工作階段存放區的JSON格式資料。

**引數**

無。

**傳回**

以JSON格式表示存放區資料的物件。

#### init() {#init}

清除工作階段存放區，並使用初始化屬性將其初始化。 將初始化旗標設為 `true` 然後觸發 `initialize` 和 `update` 事件。

**引數**

無。

**傳回**

沒有傳回的資料。

#### initJSON(jsonData， doNotClear) {#initjson-jsondata-donotclear}

從JSON物件中的資料建立初始化屬性。 您可以選擇移除所有現有的初始化屬性。

屬性的名稱衍生自JSON物件中的資料階層。 以下範常式式碼代表JSON物件：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

在此範例中，會在存放區中建立下列屬性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**引數**

* jsonData： JSON物件，包含要儲存的資料。
* doNotClear： true值會保留現有的初始化屬性，並新增衍生自JSON物件的屬性。 若值為false，會先移除現有的初始化屬性，再新增衍生自JSON物件的屬性。

**傳回**

沒有傳回值。

#### registerNewInstance(storeName， jsonData) {#registernewinstance-storename-jsondata}

以指定名稱建立CQ_Analytics.JSONStore物件，並以指定JSON資料初始化（呼叫initJSON方法）。 新物件會自動向Clickstream Cloud Manager註冊。

**引數**

* storeName：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName （包含所有大寫字元）。
* jsonData：物件。 包含JSON資料的物件。

**傳回**

cq_Analytics.JSONStore物件。

## CQ_Analytics.Observable {#cq-analytics-observable}

引發事件並允許其他物件接聽這些事件並做出反應。 擴充此類別的類別可能會引發事件，進而導致呼叫接聽程式。

### 方法 {#methods-4}

#### addListener(event， fct， scope) {#addlistener-event-fct-scope}

註冊事件的監聽器。 另請參閱 [建立監聽器以回應工作階段存放區更新](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**引數**

* 事件：字串。 要監聽的事件名稱。
* fct：函式。 發生事件時所呼叫的函式。
* 範圍： （選用）物件。 執行處理常式函式的範圍。 處理常式函式的「this」內容。

**傳回**

沒有傳回值。

#### removeListener(event， fct) {#removelistener-event-fct}

移除事件的指定事件處理常式。

**引數**

* 事件：字串。 事件的名稱。
* fct：函式。 事件處理常式。

**傳回**

沒有傳回值。

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

從遠端JSONP服務擷取之JSON物件的持續容器。

擴充CQ_Analytics.PersistedJSONStore。

### 方法 {#methods-5}

如需繼承方法，另請參閱CQ_Analytics.PersistedJSONStore 。

#### getInstance(storeName， serviceURL， dynamicData， deferLoading， loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

建立CQ_Analytics.PersistedJSONPStore物件。

**引數**

* storeName：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName （包含所有大寫字元）。 如果未提供storeName，方法會傳回null。
* serviceURL：字串。 JSONP服務的URL
* dynamicData： （選用）物件。 JSON資料，用於在呼叫回呼函式之前附加至存放區的初始化資料。
* deferLoading： （選用）布林值。 如果值為true，則在建立物件時不會呼叫JSONP服務。 false值會導致呼叫JSONP服務。
* loadingCallback： （選用）字串。 呼叫用於處理JSONP服務傳回之JSONP物件的函式名稱。 回呼函式必須定義單一引數，即CQ_Analytics.JSONPStore物件。

**傳回**

新的CQ_Analytics.PersistedJSONPStore物件，或Null （如果storeName為Null）。

#### getServiceURL() {#getserviceurl-1}

擷取此物件用於擷取JSON資料的JSONP服務URL。

**引數**

無。

**傳回**

代表服務URL的字串；若未設定服務URL，則為null。

#### load(serviceURL， dynamicData， callback) {#load-serviceurl-dynamicdata-callback-1}

呼叫JSONP服務。 JSONP URL是尾碼為給定回呼函式名稱的服務URL。

**引數**

* serviceURL： （選用）字串。 要呼叫的JSONP服務。 如果值為null，則會使用已設定的服務URL。 非null值會設定JSONP服務用於此物件。 （請參閱setServiceURL。）
* dynamicData： （選用）物件。 JSON資料，用於在呼叫回呼函式之前附加至存放區的初始化資料。
* callback： （選用）字串。 呼叫用於處理JSONP服務傳回之JSONP物件的函式名稱。 回呼函式必須定義單一引數，即CQ_Analytics.JSONPStore物件。

**傳回**

沒有傳回值。

#### registerNewInstance(storeName， serviceURL， dynamicData， callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

建立CQ_Analytics.PersistedJSONPStore物件，並將存放區註冊到Client Context。

**引數**

* storeName：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName （包含所有大寫字元）。 如果未提供storeName，方法會傳回null。
* serviceURL： （選用）字串。 JSONP服務的URL。
* dynamicData： （選用）物件。 JSON資料，用於在呼叫回呼函式之前附加至存放區的初始化資料。
* callback： （選用）字串。 呼叫用於處理JSONP服務傳回之JSONP物件的函式名稱。 回呼函式必須定義單一引數，即CQ_Analytics.JSONPStore物件。

**傳回**

已登入的CQ_Analytics.PersistedJSONPStore物件。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

設定用於擷取JSON資料的JSONP服務URL。

**引數**

* serviceURL：字串。 提供JSON資料的JSONP服務的URL

**傳回**

沒有傳回值。

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

JSON物件的持續容器。

延伸 `CQ_Analytics.PersistedSessionStore`.

### 屬性 {#properties-2}

#### STOREKEY {#storekey-1}

用來識別存放區的金鑰。 使用 `getInstance` 方法以擷取此值。

#### STORENAME {#storename-1}

存放區的名稱。 使用 `getInstance` 方法以擷取此值。

### 方法 {#methods-6}

另請參閱CQ_Analytics.PersistedSessionStore以瞭解繼承的方法。

#### getInstance(storeName， jsonData) {#getinstance-storename-jsondata-1}

以指定名稱建立CQ_Analytics.PersistedJSONStore物件，並以指定JSON資料初始化（呼叫initJSON方法）。

**引數**

* storeName：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName （包含所有大寫字元）。
* jsonData：物件。 包含JSON資料的物件。

**傳回**

cq_Analytics.PersistedJSONStore物件。

#### getJSON() {#getjson-1}

擷取工作階段存放區的JSON格式資料。

**引數**

無。

**傳回**

以JSON格式表示存放區資料的物件。

#### initJSON(jsonData， doNotClear) {#initjson-jsondata-donotclear-1}

從JSON物件中的資料建立初始化屬性。 您可以選擇移除所有現有的初始化屬性。

屬性的名稱衍生自JSON物件中的資料階層。 以下範常式式碼代表JSON物件：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

在此範例中，會在存放區中建立下列屬性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**引數**

* jsonData： JSON物件，包含要儲存的資料。
* doNotClear： true值會保留現有的初始化屬性，並新增衍生自JSON物件的屬性。 若值為false，會先移除現有的初始化屬性，再新增衍生自JSON物件的屬性。

**傳回**

沒有傳回值。

#### registerNewInstance(storeName， jsonData) {#registernewinstance-storename-jsondata-1}

以指定名稱建立CQ_Analytics.PersistedJSONStore物件，並以指定JSON資料初始化（呼叫initJSON方法）。 新物件會自動註冊到Client Context Manager。

**引數**

* storeName：字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName （包含所有大寫字元）。
* jsonData：物件。 包含JSON資料的物件。

**傳回**

cq_Analytics.PersistedJSONStore物件。

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

屬性和值的容器。 資料會使用CQ_Analytics.SessionPersistence持續儲存。 建立此類別的執行個體以建立持續的工作階段存放區：

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

擴充CQ_Analytics.SessionStore。

### 屬性 {#properties-3}

#### STOREKEY {#storekey-2}

預設值為 `key`.

### 方法 {#methods-7}

如需繼承的方法，請參閱CQ_Analytics.SessionStore 。

當繼承方法時 `clear`， `setProperty`， `setProperties`， `removeProperty` 可用來變更存放區資料，除非已變更的屬性標示為notPersisted，否則變更會自動持續存在。

#### getStoreKey() {#getstorekey}

擷取 `STOREKEY` 屬性。

**引數**

無

**傳回**

的值 `STOREKEY` 屬性。

#### isPersisted(name) {#ispersisted-name}

決定是否保留資料屬性。

**引數**

* name：字串。 屬性的名稱。

**傳回**

布林值 `true` 如果屬性持續存在，且值為 `false` 如果值不是持續屬性。

#### persist() {#persist}

儲存工作階段存放區。 預設的持續性模式使用瀏覽器 `localStorage` 使用 `ClientSidePersistence` 作為名稱( `window.localStorage.set("ClientSidePersistance", store);`)

如果localStorage無法使用或無法寫入，則會將存放區保留為視窗的屬性。

觸發 `persist` 完成時的事件。

**引數**

無

**傳回**

沒有傳回值。

#### reset(deferEvent) {#reset-deferevent}

從存放區移除所有資料屬性，並保留存放區。 選擇性地不觸發 `udpate` 完成時的事件。

**引數**

* deferevent： true值會防止 `update` 事件中防止觸發。 值 `false` 會導致更新事件引發。

**傳回**

沒有傳回值。

#### setNonPersisted(name) {#setnonpersisted-name}

將資料屬性標示為未保留。

**引數**

* name：字串。 不持續存在的屬性名稱。

**傳回**

沒有傳回值。

## cq_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore代表工作階段存放區。 建立此類別的執行個體以建立工作階段存放區：

`mystore = new CQ_Analytics.SessionStore`

擴充CQ_Analytics.Observable。

### 屬性 {#properties-4}

#### STORENAME {#storename-2}

工作階段存放區的名稱。 使用getName擷取此屬性的值。

### 方法 {#methods-8}

#### addInitProperty(name， value) {#addinitproperty-name-value}

將屬性和值新增至工作階段存放區初始化資料。

使用loadInitProperties以初始化值填入工作階段存放區資料。

**引數**

* name：字串。 要新增的屬性名稱。
* 值：字串。 要新增的屬性值。

**傳回**

沒有傳回值。

#### clear() {#clear-1}

從存放區移除所有資料屬性。

**引數**

無。

**傳回**

沒有傳回值。

#### getData(excluded) {#getdata-excluded}

傳回存放區資料。 可選擇性地從資料中排除名稱屬性。 呼叫 `init` 方法（如果存放區的資料屬性不存在）。

**引數**

已排除： （選用）要從傳回資料排除的屬性名稱陣列。

**傳回**

屬性及其值的物件。

#### getInitProperty(name) {#getinitproperty-name}

擷取資料屬性的值。

**引數**

* name：字串。 要擷取的資料屬性的名稱。

**傳回**

資料屬性的值。 回訪 `null` 如果工作階段存放區不包含指定名稱的屬性。

#### getName() {#getname}

傳回工作階段存放區的名稱。

**引數**

無。

**傳回**

代表存放區名稱的字串值。

#### getProperty(name， raw) {#getproperty-name-raw}

傳回屬性的值。 值會傳回為原始屬性或XSS篩選值。 呼叫 `init` 方法（如果存放區的資料屬性不存在）。

**引數**

* name：字串。 要擷取的資料屬性的名稱。
* 原始：布林值。 true值會傳回原始屬性值。 false值會導致傳回的值經過XSS篩選。

**傳回**

資料屬性的值。

#### getPropertyNames（已排除） {#getpropertynames-excluded}

傳回工作階段存放區包含的屬性名稱。 呼叫 `init` 方法（如果存放區的資料屬性不存在）。

**引數**

已排除： （選用）要從結果中忽略的屬性名稱陣列。

**傳回**

代表工作階段屬性名稱的String值陣列。

#### getSessionStore() {#getsessionstore}

傳回附加到目前物件的工作階段存放區。

**引數**

無。

**傳回**

此

#### init() {#init-1}

將存放區標示為已初始化，並引發 `initialize` 事件。

**引數**

無。

**傳回**

沒有傳回值。

#### isInitialized() {#isinitialized}

指出工作階段存放區是否已初始化。

**引數**

無。

**傳回**

值 `true` 如果已初始化存放區，且值為 `false` 如果存放區未初始化。

#### Loadinitproperties(obj， setValues) {#loadinitproperties-obj-setvalues}

將指定物件的屬性新增至工作階段存放區的初始化資料。 也可以將物件資料新增至存放區資料。

**引數**

* 物件：包含可列舉屬性的物件。
* setValues：為true時，如果存放區資料尚未包含相同名稱的屬性，則會將物件屬性新增至工作階段存放區資料。 為false時，不會將任何資料新增至工作階段存放區資料。

**傳回**

沒有傳回值。

#### removeProperty(name) {#removeproperty-name}

從工作階段存放區移除屬性。 觸發 `update` 完成時的事件。 呼叫 `init` 方法（如果存放區的資料屬性不存在）。

**引數**

* name：字串。 要移除的屬性名稱。

**傳回**

沒有傳回值。

#### reset() {#reset}

還原資料存放區的初始值。 預設實施只會移除所有資料。 觸發 `update` 完成時的事件。

**引數**

無。

**傳回**

沒有傳回值。

#### setProperties(properties) {#setproperties-properties}

設定多個屬性的值。 觸發 `update` 完成時的事件。 呼叫 `init` 方法（如果存放區的資料屬性不存在）。

**引數**

* 屬性：物件。 包含可列舉屬性的物件。 每個屬性名稱和值都會新增至存放區。

**傳回**

沒有傳回值。

#### setProperty(name， value) {#setproperty-name-value}

設定屬性的值。 觸發 `update` 完成時的事件。 呼叫 `init` 方法（如果存放區的資料屬性不存在）。

**引數**

* name：字串。 屬性的名稱。
* 值：字串。 屬性值。

**傳回**

沒有傳回值。
