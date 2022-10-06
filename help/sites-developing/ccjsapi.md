---
title: 用戶端內容Javascript API
seo-title: Client Context Javascript API
description: 用戶端內容的Javascript API
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

# 用戶端內容Javascript API{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

CQ_Analytics.ClientContextMgr物件是單例，包含一組自行註冊的工作階段存放區，並提供註冊、保存和管理工作階段存放區的方法。

延伸CQ_Analytics.PerisentSessionStore。

### 方法 {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

傳回指定名稱的工作階段存放區。 另請參閱 [存取工作階段存放區](/help/sites-developing/client-context.md#accessing-session-stores).

**參數**

* 名稱：字串。 工作階段存放區的名稱。

**傳回**

代表指定名稱之工作階段存放區的CQ_Analytics.SessionStore物件。 傳回 `null` 當指定名稱不存在儲存時。

#### 註冊(sessionstore) {#register-sessionstore}

使用客戶端上下文註冊會話儲存。 完成時觸發storeregister和storeupdate事件。

**參數**

* sessionstore:CQ_Analytics.SessionStore。 要註冊的會話儲存對象。

**傳回**

沒有傳回值。

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

提供監聽工作階段存放區啟動和註冊的方法。 另請參閱 [檢查會話儲存是否已定義並初始化](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### 方法 {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

註冊在初始化會話儲存時調用的回調函式。 對於初始化多次的儲存，指定回呼延遲，使回呼函式只被呼叫一次：

* 當儲存器在先前初始化的延遲期間被初始化時，取消先前的函式調用，並且為當前初始化再次調用函式。
* 如果延遲期間在後續初始化發生之前結束，則會執行兩次回呼函式。

例如，工作階段存放區是以JSON物件為基礎，並透過JSON要求擷取。 可能有下列初始化案例：

* 請求已完成，資料已擷取並載入儲存中。 在此情況下，初始化只進行一次。
* 請求失敗（逾時）。 在此情況下，初始化不會進行，且儲存中沒有資料。
* 儲存區已預先填入預設值（init屬性），但請求失敗（逾時）。 只有一個初始化具有預設值。
* 商店已預先填入。

延遲設為 `true` 或是毫秒，方法會等待再呼叫callback方法。 如果在傳遞延遲之前觸發了另一個初始化事件，則會等待到延遲時間超出，而沒有初始化事件。 這可讓您等候第二個初始化事件觸發，並在最佳情況下呼叫回呼函式。

**參數**

* storeName:字串。 要添加監聽程式的會話儲存的名稱。
* 回呼：函式。 儲存初始化時要呼叫的函式。
* 延遲：布林值或數字。 延遲呼叫回呼函式的時間量（以毫秒為單位）。 的布林值 `true` 使用的預設延遲為 `200 ms`. 的布林值 `false` 或負數不會造成使用延遲。

**傳回**

沒有傳回值。

#### onStoreRegistered(storeName, callback) {#onstoreregistered-storename-callback}

註冊會話儲存區時調用的回調函式。 當商店註冊到 [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**參數**

* storeName:字串。 要添加監聽程式的會話儲存的名稱。
* 回呼：函式。 儲存初始化時要呼叫的函式。

**傳回**

沒有傳回值。

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

包含JSON資料的非持續工作階段存放區。 資料從外部JSONP服務中檢索。 使用 `getInstance` 或 `getRegisteredInstance` 建立此類實例的方法。

延伸CQ_Analytics.JSONStore。

### 屬性 {#properties}

如需繼承的屬性，請參閱CQ_Analytics.JSONStore和CQ_Analytics.SessonStore 。

### 方法 {#methods-2}

如需繼承的方法，另請參閱CQ_Analytics.JSONStore和CQ_Analytics.SessonStore 。

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

建立CQ_Analytics.JSONPStore物件。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName，包含所有大寫字元。 如果未提供storeName，則方法將返回null。
* serviceURL:字串。 JSONP服務的URL
* dynamicData:（選用）物件。 在呼叫回呼函式之前，附加至存放區初始化資料的JSON資料。
* deferLoading:（選用）布林值。 值true可防止在建立對象時調用JSONP服務。 值false會呼叫JSONP服務。
* loadingCallback:（選用）字串。 要調用以處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**傳回**

新的CQ_Analytics.JSONPStore物件；若storeName為null，則為null。

#### getServiceURL() {#getserviceurl}

擷取此物件用來擷取JSON資料的JSONP服務URL。

**參數**

無.

**傳回**

表示服務URL的字串；如果未配置服務URL，則為null。

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

呼叫JSONP服務。 JSONP URL是尾碼為給定回呼函式名稱的服務URL。

**參數**

* serviceURL:（選用）字串。 JSONP服務。 值為null會使用已設定的服務URL。 非空值將JSONP服務設定為用於此對象。 （請參閱setServiceURL。）
* dynamicData:（選用）物件。 在呼叫回呼函式之前，附加至存放區初始化資料的JSON資料。
* 回呼：（選用）字串。 要調用以處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**傳回**

沒有傳回值。

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

建立CQ_Analytics.JSONPStore物件，並使用用戶端內容註冊存放區。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName，包含所有大寫字元。 如果未提供storeName，則方法將返回null。
* serviceURL:（選用）字串。 JSONP服務的URL。
* dynamicData:（選用）物件。 在呼叫回呼函式之前，附加至存放區初始化資料的JSON資料。
* 回呼：（選用）字串。 要調用以處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**傳回**

已註冊的CQ_Analytics.JSONPStore物件。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

設定用於擷取JSON資料的JSONP服務的URL。

**參數**

* serviceURL:字串。 提供JSON資料的JSONP服務的URL

**傳回**

沒有傳回值。

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

JSON物件的容器。 建立此類別的例項，以建立包含JSON資料的非持續工作階段存放區：

`myjsonstore = new CQ_Analytics.JSONStore`

您可以定義一組資料，在初始化時填入儲存。

延伸CQ_Analytics.SessionStore。

### 屬性 {#properties-1}

#### STOREKEY {#storekey}

識別存放區的金鑰。 使用 `getInstance` 方法來擷取此值。

#### 儲存重新命名 {#storename}

商店的名稱。 使用 `getInstance` 方法來擷取此值。

### 方法 {#methods-3}

另請參閱CQ_Analytics.SessionStore ，以了解繼承的方法。

#### 清除() {#clear}

刪除會話儲存資料並刪除所有初始化屬性。

**參數**

無.

**傳回**

沒有傳回值。

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

以指定名稱建立CQ_Analytics.JSONStore物件，並以指定JSON資料初始化（呼叫initJSON方法）。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName，包含所有大寫字元。
* json資料：物件。 包含JSON資料的物件。

**傳回**

CQ_Analytics.JSONStore物件。

#### getJSON() {#getjson}

擷取工作階段存放區的JSON格式資料。

**參數**

無.

**傳回**

代表JSON格式儲存資料的物件。

#### init() {#init}

清除會話儲存，並使用初始化屬性對其進行初始化。 將初始化標幟設為 `true` 然後再引發 `initialize` 和 `update` 事件。

**參數**

無.

**傳回**

沒有傳回資料。

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

從JSON物件中的資料建立初始化屬性。 您可以選擇刪除所有現有的初始化屬性。

屬性名稱衍生自JSON物件中的資料階層。 下列范常式式碼代表JSON物件：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

在此範例中，會在儲存中建立下列屬性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**參數**

* json資料：包含要儲存之資料的JSON物件。
* doNotClear:true值會保留現有的初始化屬性，並新增從JSON物件衍生的屬性。 若值為false，則會先移除現有的初始化屬性，再新增從JSON物件衍生的屬性。

**傳回**

沒有傳回值。

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

以指定名稱建立CQ_Analytics.JSONStore物件，並以指定JSON資料初始化（呼叫initJSON方法）。 新物件會自動註冊至Clickstream雲端管理器。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName，包含所有大寫字元。
* json資料：物件。 包含JSON資料的物件。

**傳回**

CQ_Analytics.JSONStore物件。

## CQ_Analytics.Ovebart {#cq-analytics-observable}

引發事件，並允許其他物件監聽這些事件並做出反應。 擴展此類的類可以引發導致調用偵聽器的事件。

### 方法 {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

為事件註冊偵聽器。 另請參閱 [建立偵聽器以對會話儲存區更新做出反應](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**參數**

* 事件：字串。 要監聽的事件的名稱。
* fct:函式。 發生事件時呼叫的函式。
* 範圍：（選用）物件。 執行處理程式函式的範圍。 處理常式函式的「this」內容。

**傳回**

沒有傳回值。

#### removeListener(event, fct) {#removelistener-event-fct}

移除事件的指定事件處理常式。

**參數**

* 事件：字串。 事件的名稱。
* fct:函式。 事件處理常式。

**傳回**

沒有傳回值。

## CQ_Analyics.PerisentJSONPStore {#cq-analyics-persistedjsonpstore}

從遠端JSONP服務擷取的JSON物件持續存在的容器。

延伸CQ_Analytics.PeristedJSONStore。

### 方法 {#methods-5}

另請參閱CQ_Analytics.PerisentJSONStore ，了解繼承的方法。

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

建立CQ_Analytics.PerisentJSONPStore物件。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName，包含所有大寫字元。 如果未提供storeName，則方法將返回null。
* serviceURL:字串。 JSONP服務的URL
* dynamicData:（選用）物件。 在呼叫回呼函式之前，附加至存放區初始化資料的JSON資料。
* deferLoading:（選用）布林值。 值true可防止在建立對象時調用JSONP服務。 值false會呼叫JSONP服務。
* loadingCallback:（選用）字串。 要調用以處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**傳回**

新的CQ_Analytics.PerisentJSONPStore物件，若storeName為null，則為null。

#### getServiceURL() {#getserviceurl-1}

擷取此物件用來擷取JSON資料的JSONP服務URL。

**參數**

無.

**傳回**

表示服務URL的字串；如果未配置服務URL，則為null。

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

呼叫JSONP服務。 JSONP URL是尾碼為給定回呼函式名稱的服務URL。

**參數**

* serviceURL:（選用）字串。 JSONP服務。 值為null會使用已設定的服務URL。 非空值將JSONP服務設定為用於此對象。 （請參閱setServiceURL。）
* dynamicData:（選用）物件。 在呼叫回呼函式之前，附加至存放區初始化資料的JSON資料。
* 回呼：（選用）字串。 要調用以處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**傳回**

沒有傳回值。

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

建立CQ_Analytics.PerisentJSONPStore物件，並使用用戶端內容註冊存放區。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName，包含所有大寫字元。 如果未提供storeName，則方法將返回null。
* serviceURL:（選用）字串。 JSONP服務的URL。
* dynamicData:（選用）物件。 在呼叫回呼函式之前，附加至存放區初始化資料的JSON資料。
* 回呼：（選用）字串。 要調用以處理JSONP服務返回的JSONP對象的函式的名稱。 回呼函式必須定義單一參數，此參數為CQ_Analytics.JSONPStore物件。

**傳回**

已註冊的CQ_Analytics.PerisentJSONPStore物件。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

設定用於擷取JSON資料的JSONP服務的URL。

**參數**

* serviceURL:字串。 提供JSON資料的JSONP服務的URL

**傳回**

沒有傳回值。

## CQ_Analytics.PerisentJSONStore {#cq-analytics-persistedjsonstore}

JSON物件的持續存在容器。

延伸 `CQ_Analytics.PersistedSessionStore`.

### 屬性 {#properties-2}

#### STOREKEY {#storekey-1}

識別存放區的金鑰。 使用 `getInstance` 方法來擷取此值。

#### 儲存重新命名 {#storename-1}

商店的名稱。 使用 `getInstance` 方法來擷取此值。

### 方法 {#methods-6}

另請參閱CQ_Analytics.PerisentSessionStore ，了解繼承的方法。

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

以指定名稱建立CQ_Analytics.PerisentJSONStore物件，並以指定JSON資料初始化（呼叫initJSON方法）。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName，包含所有大寫字元。
* json資料：物件。 包含JSON資料的物件。

**傳回**

CQ_Analytics.PerisentJSONStore物件。

#### getJSON() {#getjson-1}

擷取工作階段存放區的JSON格式資料。

**參數**

無.

**傳回**

代表JSON格式儲存資料的物件。

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

從JSON物件中的資料建立初始化屬性。 您可以選擇刪除所有現有的初始化屬性。

屬性名稱衍生自JSON物件中的資料階層。 下列范常式式碼代表JSON物件：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

在此範例中，會在儲存中建立下列屬性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**參數**

* json資料：包含要儲存之資料的JSON物件。
* doNotClear:true值會保留現有的初始化屬性，並新增從JSON物件衍生的屬性。 若值為false，則會先移除現有的初始化屬性，再新增從JSON物件衍生的屬性。

**傳回**

沒有傳回值。

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

以指定名稱建立CQ_Analytics.PerisentJSONStore物件，並以指定JSON資料初始化（呼叫initJSON方法）。 新對象會自動註冊到客戶端上下文管理器。

**參數**

* storeName:字串。 用作STORENAME屬性的名稱。 STOREKEY屬性的值設為storeName，包含所有大寫字元。
* json資料：物件。 包含JSON資料的物件。

**傳回**

CQ_Analytics.PerisentJSONStore物件。

## CQ_Analytics.PerisentSessionStore {#cq-analytics-persistedsessionstore}

屬性和值的容器。 資料會使用CQ_Analytics.SessionPersistence來保存。 建立此類的例項以建立持續的工作階段存放區：

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

延伸CQ_Analytics.SessionStore。

### 屬性 {#properties-3}

#### STOREKEY {#storekey-2}

預設值為 `key`.

### 方法 {#methods-7}

如需繼承的方法，請參閱CQ_Analytics.SessionStore 。

繼承的方法 `clear`, `setProperty`, `setProperties`, `removeProperty` 可用來變更儲存資料，除非變更的屬性被標示為notPeristent，否則會自動保存變更。

#### getStoreKey() {#getstorekey}

擷取 `STOREKEY` 屬性。

**參數**

無

**傳回**

的值 `STOREKEY` 屬性。

#### isPerisent(name) {#ispersisted-name}

判斷資料屬性是否持續存在。

**參數**

* 名稱：字串。 屬性的名稱。

**傳回**

的布林值 `true` 如果屬性持續存在，且值為 `false` 如果值不是持續屬性。

#### persist() {#persist}

保存會話儲存。 預設持久性模式使用瀏覽器 `localStorage` 使用 `ClientSidePersistence` 作為名稱( `window.localStorage.set("ClientSidePersistance", store);`)

如果localStorage不可用或不可寫，則該儲存作為窗口的屬性保存。

引發 `persist` 事件。

**參數**

無

**傳回**

沒有傳回值。

#### reset(deferEvent) {#reset-deferevent}

從儲存中移除所有資料屬性，並保存該儲存。 （可選）不會觸發 `udpate` 事件。

**參數**

* deferEvent:若值為true，則會防止 `update` 事件。 值 `false` 會引發更新事件。

**傳回**

沒有傳回值。

#### setNonPeristent(name) {#setnonpersisted-name}

將資料屬性標幟為不持續存在。

**參數**

* 名稱：字串。 不要持續存在的屬性名稱。

**傳回**

無傳回值。

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore代表工作階段存放區。 建立此類的實例以建立會話儲存：

`mystore = new CQ_Analytics.SessionStore`

延伸CQ_Analytics.Vobalt。

### 屬性 {#properties-4}

#### 儲存重新命名 {#storename-2}

工作階段存放區的名稱。 使用getName檢索此屬性的值。

### 方法 {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

將屬性和值添加到會話儲存初始化資料。

使用loadInitProperties將初始化值填充會話儲存資料。

**參數**

* 名稱：字串。 要新增的屬性名稱。
* 值：字串。 要新增的屬性值。

**傳回**

沒有傳回值。

#### 清除() {#clear-1}

從儲存中刪除所有資料屬性。

**參數**

無.

**傳回**

無傳回值。

#### getData(excluded) {#getdata-excluded}

傳回儲存資料。 （可選）從資料中排除名稱屬性。 呼叫 `init` 方法（如果儲存的資料屬性不存在）。

**參數**

已排除：（選用）要從傳回資料中排除的屬性名稱陣列。

**傳回**

屬性的物件及其值。

#### getInitProperty(name) {#getinitproperty-name}

擷取資料屬性的值。

**參數**

* 名稱：字串。 要擷取的資料屬性名稱。

**傳回**

資料屬性的值。 回訪 `null` 如果會話儲存不包含指定名稱的屬性。

#### getName() {#getname}

傳回工作階段存放區的名稱。

**參數**

無.

**傳回**

代表商店名稱的字串值。

#### getProperty(name, raw) {#getproperty-name-raw}

傳回屬性的值。 此值會傳回為原始屬性或XSS篩選的值。 呼叫 `init` 方法（如果儲存的資料屬性不存在）。

**參數**

* 名稱：字串。 要擷取的資料屬性名稱。
* 原始：布林值。 若值為true，系統會傳回原始屬性值。 若值為false，則會將傳回的值設為XSS篩選。

**傳回**

資料屬性的值。

#### getPropertyNames(excluded) {#getpropertynames-excluded}

傳回工作階段存放區包含之屬性的名稱。 呼叫 `init` 方法（如果儲存的資料屬性不存在）。

**參數**

已排除：（選用）要從結果中忽略的屬性名稱陣列。

**傳回**

代表工作階段屬性名稱的字串值陣列。

#### getSessionStore() {#getsessionstore}

傳回附加至目前物件的工作階段存放區。

**參數**

無.

**傳回**

此

#### init() {#init-1}

將存放區標示為已初始化，並引發 `initialize` 事件。

**參數**

無.

**傳回**

沒有傳回值。

#### isInitialized() {#isinitialized}

指示會話儲存是否已初始化。

**參數**

無.

**傳回**

值 `true` 如果儲存已初始化，且 `false` 如果儲存未初始化。

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

將指定對象的屬性添加到會話儲存的初始化資料中。 可選地，對象資料也添加到儲存資料中。

**參數**

* obj:包含可枚舉屬性的對象。
* setValues:若為true，如果存放區資料尚未包含相同名稱的屬性，則obj屬性會新增至工作階段存放區資料。 若為false，則不會將任何資料新增至工作階段存放區資料。

**傳回**

沒有傳回值。

#### removeProperty(name) {#removeproperty-name}

從工作階段存放區移除屬性。 引發 `update` 事件。 呼叫 `init` 方法（如果儲存的資料屬性不存在）。

**參數**

* 名稱：字串。 要移除的屬性名稱。

**傳回**

沒有傳回值。

#### 重設() {#reset}

還原資料儲存的初始值。 預設實作只會移除所有資料。 引發 `update` 事件。

**參數**

無.

**傳回**

沒有傳回值。

#### setProperties(properties) {#setproperties-properties}

設定多個屬性的值。 引發 `update` 事件。 呼叫 `init` 方法（如果儲存的資料屬性不存在）。

**參數**

* 屬性：物件。 包含可枚舉屬性的對象。 每個屬性名稱和值都會新增至商店。

**傳回**

沒有傳回值。

#### setProperty(name, value) {#setproperty-name-value}

設定屬性的值。 引發 `update` 事件。 呼叫 `init` 方法（如果儲存的資料屬性不存在）。

**參數**

* 名稱：字串。 屬性的名稱。
* 值：字串。 屬性值。

**傳回**

沒有傳回值。
