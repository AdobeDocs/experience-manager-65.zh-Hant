---
title: 詳細的客戶端上下文
seo-title: Client Context in Detail
description: 「用戶端內容」代表動態組合的使用者資料集合
seo-description: The Client Context represents a dynamically assembled collection of user data
uuid: 95b08fbd-4f50-44a1-80fb-46335fe04a40
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c881ad66-bcc3-4f99-b77f-0944c23e2d29
docset: aem65
feature: Context Hub
exl-id: 38b9a795-1c83-406c-ab13-b4456da938dd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3008'
ht-degree: 0%

---

# 詳細的客戶端上下文{#client-context-in-detail}

>[!NOTE]
>
>客戶端上下文已被ContextHub取代。 請參閱 [相關檔案](/help/sites-developing/contexthub.md) 以取得詳細資訊。

「用戶端內容」代表動態組合的使用者資料集合。 您可以使用資料來判斷在指定情況下要顯示在網頁上的內容（內容定位）。 網站分析和頁面上的任何Javascript也能使用這些資料。

客戶端上下文主要包括以下方面：

* 包含使用者資料的工作階段存放區。
* 顯示使用者資料的UI，並提供模擬使用者體驗的工具。
* A [javascript API](/help/sites-developing/ccjsapi.md) 與工作階段存放區互動。

要建立獨立會話儲存並將其添加到客戶端上下文，或建立與上下文儲存元件綁定的會話儲存。 AEM會安裝數個您可立即使用的內容存放區元件。 您可以將這些元件作為元件的基礎。

如需開啟用戶端內容、設定其顯示的資訊以及模擬使用者體驗的相關資訊，請參閱 [用戶端內容](/help/sites-administering/client-context.md).

## 工作階段存放區 {#session-stores}

「用戶端內容」包含包含使用者資料的各種工作階段存放區。 儲存來自以下來源的資料：

* 客戶端Web瀏覽器。
* 伺服器(請參閱 [JSONP商店](/help/sites-administering/client-context.md#main-pars-variable-8) 用於儲存來自第三方源的資訊)

客戶端上下文框架提供 [javascript API](/help/sites-developing/ccjsapi.md) 可用來與工作階段存放區互動，以讀取和寫入使用者資料，以及接聽和回應儲存事件。 您也可以為您用於內容定位或其他目的的使用者資料建立工作階段存放區。

會話儲存資料仍保留在客戶端上。 客戶端上下文不會將資料寫回伺服器。 若要將資料傳送至伺服器，請使用表單或開發自訂javascript。

每個工作階段存放區都是屬性值組的集合。 工作階段存放區代表資料（任何類型）的集合，其概念意義可由設計人員和/或開發人員決定。 以下範例javascript程式碼定義一個物件，代表工作階段存放區可能包含的設定檔資料：

```
{
  age: 20,
  authorizableId: "aparker@geometrixx.info",
  birthday: "27 Feb 1992",
  email: "aparker@geometrixx.info",
  formattedName: "Alison Parker",
  gender: "female",
  path: "/home/users/geometrixx/aparker@geometrixx.info/profile"
}
```

工作階段存放區可持續存在於各瀏覽器工作階段之間，或僅能存留於建立工作階段的瀏覽器工作階段。

>[!NOTE]
>
>儲存持續性使用瀏覽器儲存或Cookie( `SessionPersistence` cookie)。 瀏覽器儲存更常見。
>
>當瀏覽器關閉並重新開啟時，工作階段存放區可以載入來自持續存放區的值。 然後需要清除瀏覽器快取以移除舊值。

### 內容存放區元件 {#context-store-components}

內容存放區元件是CQ元件，可新增至用戶端內容。 通常，上下文儲存元件會顯示來自與其關聯之工作階段存放區的資料。 不過，上下文儲存元件顯示的資訊不限於工作階段儲存資料。

內容存放區元件可包含下列項目：

* 定義客戶端上下文中外觀的JSP指令碼。
* 用於在Sidekick中列出元件的屬性。
* 編輯配置元件實例的對話框。
* 初始化會話儲存的Javascript。

如需可新增至上下文存放區之已安裝上下文存放區元件的說明，請參閱 [可用的客戶端上下文元件](/help/sites-administering/client-context.md#available-client-context-components).

>[!NOTE]
>
>頁面資料不再是在用戶端內容中作為預設元件。 如有需要，您可以編輯用戶端內容並新增 **一般儲存屬性** 元件，然後進行設定以定義 **商店** as `pagedata`.

### 目標內容傳送 {#targeted-content-delivery}

設定檔資訊也用於傳送 [目標內容](/help/sites-authoring/content-targeting-touch.md).

![clientcontext_targetedcontentdelivery](assets/clientcontext_targetedcontentdelivery.png) ![clientcontext_targetedcontentdeliverydetail](assets/clientcontext_targetedcontentdeliverydetail.png)

## 將用戶端內容新增至頁面 {#adding-client-context-to-a-page}

將「用戶端內容」元件加入網頁內文區段，以啟用「用戶端內容」。 客戶端上下文元件節點的路徑為 `/libs/cq/personalization/components/clientcontext`. 要包括元件，請將以下代碼添加到頁面元件的JSP檔案中，該檔案位於 `body` 頁面的元素：

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

clientcontext元件會導致頁面載入實作用戶端內容的用戶端程式庫。

* 用戶端內容javascript API。
* 支援工作階段存放區、事件管理等的用戶端內容架構。
* 定義的區段。
* 為每個已新增至用戶端內容的上下文儲存元件產生的init.js指令碼。
* （僅限製作例項）用戶端內容UI。

用戶端內容UI僅適用於製作執行個體。

## 擴展客戶端上下文 {#extending-client-context}

若要擴充用戶端內容，請建立工作階段存放區並選擇性地顯示存放區資料：

* 為內容鎖定目標和網頁分析所需的使用者資料建立工作階段存放區。
* 建立上下文儲存元件，使管理員能夠配置相關的會話儲存，並顯示在客戶端上下文中儲存資料以用於測試。

>[!NOTE]
>
>如果您有（或建立） `JSONP` 提供資料的服務，您只需使用 `JSONP` 上下文儲存元件，並將其對應至JSONP服務。 這將處理工作階段存放區。

### 建立工作階段存放區 {#creating-a-session-store}

為需要添加到客戶端上下文並從中檢索的資料建立會話儲存。 一般而言，您可使用下列程式來建立工作階段存放區：

1. 建立具有 `categories` 屬性值 `personalization.stores.kernel`. 客戶端上下文會自動載入此類別的客戶端庫。

1. 配置客戶端庫資料夾，使其與 `personalization.core.kernel` 客戶端庫資料夾。 此 `personalization.core.kernel` 用戶端程式庫提供用戶端內容javascript API。

1. 添加建立和初始化會話儲存的javascript。

在personalization.stores.kernel用戶端程式庫中包含javascript，會在載入用戶端內容架構時建立儲存。

>[!NOTE]
>
>如果您要在內容存放區元件中建立工作階段存放區，您也可以將javascript放置在元件的init.js.jsp檔案中。 在此情況下，只有將元件新增至用戶端內容時，才會建立工作階段存放區。

#### 工作階段存放區類型 {#types-of-session-stores}

工作階段存放區是在瀏覽器工作階段期間建立且可用，或保存在瀏覽器儲存或Cookie中。 用戶端內容javascript API定義了代表這兩種資料存放區類型的數個類別：

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`:這些物件僅位於頁面DOM中。 資料會在頁面的存留期間建立並保存。
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`:這些物件位於頁面DOM中，且會保存在瀏覽器儲存區或Cookie中。 資料可在各頁面和使用者工作階段之間使用。

API也提供這些類別的擴充功能，這些類別專門用於儲存JSON資料或JSONP資料：

* 僅會話對象： [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore) 和 [CQ_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore).

* 保存的對象： [CQ_Analytics.PerisentJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore) 和 [CQ_Analytics.PerisentJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore).

#### 建立會話儲存對象 {#creating-the-session-store-object}

用戶端程式庫資料夾的javascript會建立並初始化工作階段存放區。 然後，必須使用上下文儲存管理器註冊會話儲存。 下面的示例建立並註冊 [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 物件。

```
//Create the session store
if (!CQ_Analytics.MyStore) {
    CQ_Analytics.MyStore = new CQ_Analytics.SessionStore();
    CQ_Analytics.MyStore.STOREKEY = "MYSTORE";
    CQ_Analytics.MyStore.STORENAME = "mystore";
    CQ_Analytics.MyStore.data={};
}
//register the session store
if (CQ_Analytics.ClientContextMgr){
    CQ_Analytics.ClientContextMgr.register(CQ_Analytics.MyStore)
}
```

若要儲存JSON資料，下列範例會建立並註冊 [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 物件。

```
if (!CQ_Analytics.myJSONStore) {
    CQ_Analytics.myJSONStore = CQ_Analytics.JSONStore.registerNewInstance("myjsonstore",{});
}
```

### 建立上下文儲存元件 {#creating-a-context-store-component}

建立上下文儲存元件以在客戶端上下文中呈現會話儲存資料。 建立後，您可以將內容存放區元件拖曳至「用戶端內容」，從工作階段存放區轉譯資料。 內容存放區元件包含下列項目：

* 用於呈現資料的JSP指令碼。
* 編輯對話方塊。
* 用於初始化會話儲存的JSP指令碼。
* （可選）建立工作階段存放區的用戶端程式庫資料夾。 如果元件使用現有的工作階段存放區，則不需要包含用戶端程式庫資料夾。

#### 擴充提供的內容存放區元件 {#extending-the-provided-context-store-components}

AEM提供您可擴充的一般儲存和一般儲存屬性內容儲存元件。 儲存資料的結構會決定您擴充的元件：

* 屬性值配對：擴充 `GenericStoreProperties` 元件。 此元件會自動轉譯屬性值配對的儲存。 提供了多個交互點：

   * `prolog.jsp` 和 `epilog.jsp`:元件互動可讓您在元件呈現之前或之後新增伺服器端邏輯。

* 複雜資料：擴充 `GenericStore` 元件。 接著，您的工作階段存放區將需要「轉譯器」方法，每次需要轉譯元件時都會呼叫此方法。 會使用兩個參數呼叫轉譯器函式：

   * `@param {String} store`
要呈現的商店

   * `@param {String} divId`
必須轉譯商店的div的ID。

>[!NOTE]
>
>所有客戶端上下文元件都是通用儲存或通用儲存屬性元件的擴展。 在 `/libs/cq/personalization/components/contextstores` 檔案夾。

#### 在Sidekick中配置外觀 {#configuring-the-appearance-in-sidekick}

編輯用戶端內容時，內容存放區元件會顯示在Sidekick中。 與所有元件一樣， `componentGroup` 和 `jcr:title` 客戶端上下文元件的屬性決定元件的組和名稱。

具有 `componentGroup` 屬性值 `Client Context` 預設會顯示在Sidekick中。 如果您對 `componentGroup` 屬性，您必須使用「設計」模式，手動將元件新增至Sidekick。

#### 內容儲存元件例項 {#context-store-component-instances}

將上下文儲存元件添加到客戶端上下文時，將在下面建立一個表示元件實例的節點 `/etc/clientcontext/default/content/jcr:content/stores`. 此節點包含使用元件的編輯對話框配置的屬性值。

初始化客戶端上下文時，將處理這些節點。

#### 初始化關聯的會話儲存 {#initializing-the-associated-session-store}

將init.js.jsp檔案新增至元件，以產生Javascript程式碼，初始化內容存放區元件所使用的工作階段存放區。 例如，使用初始化指令碼來檢索元件的配置屬性，並使用它們來填充會話儲存。

在製作和發佈例項的頁面載入上初始化「用戶端內容」時，產生的Javascript會新增至頁面。 此JSP在載入和呈現上下文儲存元件實例之前執行。

程式碼必須將檔案的mime類型設定為 `text/javascript`，或未執行。

>[!CAUTION]
>
>init.js.jsp指令碼會在製作和發佈例項上執行，但僅限於將內容存放區元件新增至用戶端內容時。

以下過程將建立init.js.jsp指令碼檔案並添加設定正確mime類型的代碼。 執行儲存初始化的程式碼會隨之執行。

1. 按一下右鍵上下文儲存元件節點，然後按一下「建立」>「建立檔案」。
1. 在「名稱」欄位中，輸入 `init.js.jsp` 然後按一下「確定」。
1. 在頁面頂端新增下列程式碼，然後按一下「儲存全部」 。

   ```java
   <%@page contentType="text/javascript" %>
   ```

### 呈現一般儲存屬性元件的工作階段儲存資料 {#rendering-session-store-data-for-genericstoreproperties-components}

使用一致格式在「用戶端內容」中顯示工作階段儲存資料。

#### 顯示屬性資料 {#displaying-property-data}

個人化taglib提供 `personalization:storePropertyTag` 標籤，顯示工作階段存放區中屬性的值。 要使用標籤，請在JSP檔案中包括以下代碼行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

標籤的格式如下：

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

此 `propertyName` 屬性是要顯示的儲存屬性的名稱。 此 `store` 屬性是已註冊儲存的名稱。 下列範例標籤會顯示 `authorizableId` 屬性 `profile` 商店：

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### HTML結構 {#html-structure}

personalization.ui用戶端資料庫資料夾(/etc/clientlibs/foundation/personalization/ui/themes/default)提供用戶端內容用來設定HTML程式碼格式的CSS樣式。 下列程式碼說明用於顯示儲存資料的建議結構：

```xml
<div class="cq-cc-store">
   <div class="cq-cc-thumbnail">
      <div class="cq-cc-store-property">
           <!-- personalization:storePropertyTag for the store thumbnail image goes here -->
      </div>
   </div>
   <div class="cq-cc-content">
       <div class="cq-cc-store-property cq-cc-store-property-level0">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level1">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level2">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level3">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
   </div>
   <div class="cq-cc-clear"></div>
</div>
```

此 `/libs/cq/personalization/components/contextstores/profiledata` 上下文儲存元件使用此結構來顯示來自設定檔工作階段存放區的資料。 此 `cq-cc-thumbnail` 類別會放置縮圖影像。 此 `cq-cc-store-property-level*x*` 類格式化字母數字資料：

* level0、level1和level2垂直分佈，使用白字型。
* 級別3和任何其他級別水準分佈，並使用背景較深的白字型。

![chlimage_1-4](assets/chlimage_1-4.png)

### 呈現一般儲存元件的會話儲存資料 {#rendering-session-store-data-for-genericstore-components}

若要使用一般存放區元件呈現存放區資料，您需要：

* 將personalization:storeRendererTag標籤新增至元件JSP指令碼，以識別工作階段存放區的名稱。
* 在工作階段存放區類別上實作轉譯器方法。

#### 標識一般儲存會話儲存 {#identifying-the-genericstore-session-store}

個人化taglib提供 `personalization:storePropertyTag` 標籤，顯示工作階段存放區中屬性的值。 要使用標籤，請在JSP檔案中包括以下代碼行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

標籤的格式如下：

```java
<personalization:storeRendererTag store="store_name"/>
```

#### 實作工作階段存放區轉譯器方法 {#implementing-the-session-store-renderer-method}

接著，您的工作階段存放區將需要「轉譯器」方法，每次需要轉譯元件時都會呼叫此方法。 會使用兩個參數呼叫轉譯器函式：

* @param {String}儲存要呈現的儲存
* @param必須轉譯儲存的div的{String} divId。

## 與工作階段存放區互動 {#interacting-with-session-stores}

使用javascript與工作階段存放區互動。

### 存取工作階段存放區 {#accessing-session-stores}

獲取會話儲存對象以讀取或寫入儲存資料。 [CQ_Analytics.ClientContextMgr](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) 根據商店名稱提供對商店的訪問。 取得後，請使用 [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 或 [CQ_Analytics.PerisentSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore) 與儲存資料互動。

下列範例會取得 `profile` 儲存，然後擷取 `formattedName` 屬性。

```
function getName(){
   var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
   if(profilestore){
      return profilestore.getProperty("formattedName", false);
   } else {
      return null;
   }
}
```

### 建立偵聽器以響應會話儲存更新 {#creating-a-listener-to-react-to-a-session-store-update}

工作階段會儲存引發事件，因此可以根據這些事件來新增接聽程式和觸發事件。

工作階段存放區是建置在 `Observable` 模式。 它們延伸 [ `CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable) 提供 ` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)` 方法。

下面的示例將監聽程式添加到 `update` 事件 `profile` 工作階段存放區。

```
var profileStore = ClientContextMgr.getRegisteredStore("profile");
if( profileStore ) {
  //callback execution context
  var executionContext = this;

  //add "update" event listener to store
  profileStore.addListener("update",function(store, property) {
    //do something on store update

  },executionContext);
}
```

### 檢查會話儲存是否已定義並初始化 {#checking-that-a-session-store-is-defined-and-initialized}

工作階段存放區必須先載入並透過資料初始化，才能使用。 下列因素可能會影響工作階段存放區可用性的時間：

* 頁面載入
* JavaScript載入
* JavaScript執行時間
* XHR請求的回應時間
* 工作階段存放區的動態變更

使用 [CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils) 物件 [onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback) 和 [onStoreInitialized](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay) 僅在會話儲存可用時訪問這些儲存的方法。 這些方法可讓您註冊對工作階段註冊和初始化事件做出反應的事件偵聽器。

>[!CAUTION]
>
>如果您依賴其他商店，則需要針對從未註冊商店的情況進行服務。

下列範例使用 `onStoreRegistered` 事件 `profile` 工作階段存放區。 註冊儲存時，會將監聽程式新增至 `update` 工作階段存放區的事件。 更新商店時， `<div class="welcome">` 頁面上的元素會以 `profile` 儲存。

```
//listen for the store registration
CQ_Analytics.ClientContextUtils.onStoreRegistered("profile", listen);

//listen for the store's update event
function listen(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
    profilestore.addListener("update",insertName);
}

//insert the welcome message
function insertName(){
 $("div.welcome").text("Welcome "+getName());
}

//obtain the name from the profile store
function getName(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
 if(profilestore){
  return profilestore.getProperty("formattedName", false);
    } else {
        return null;
    }
}
```

### 將屬性排除在工作階段持續性Cookie之外 {#excluding-a-property-from-the-sessionpersistence-cookie}

防止 `PersistedSessionStore` 不持續(亦即將其從 `sessionpersistence` cookie)，將屬性新增至持續工作階段存放區的非持續屬性清單。

請參閱 ` [CQ_Analytics.PersistedSessionStore.setNonPersisted(propertyName)](/help/sites-developing/ccjsapi.md#setnonpersisted-name)`

```
CQ_Analytics.ClientContextUtils.onStoreRegistered("surferinfo", function(store) {
  //this will exclude the browser, OS and resolution properties of the surferinfo session store from the
  store.setNonPersisted("browser");
  store.setNonPersisted("OS");
  store.setNonPersisted("resolution");
});
```

## 配置設備滑桿 {#configuring-the-device-slider}

### 條件 {#conditions}

目前頁面必須有對應的行動頁面；唯有頁面已以行動轉出設定設定( `rolloutconfig.path.toLowerCase` 包含 `mobile`)。

#### 設定 {#configuration}

從案頭頁面切換至行動裝置對應頁面時：

* 行動頁面的DOM已載入。
* 主要 `div` （必要），會擷取並插入目前的案頭頁面中。

* 需要載入的CSS和內文類別需要手動設定。

例如：

```
window.CQMobileSlider["geometrixx-outdoors"] = {
  //CSS used by desktop that need to be removed when mobile
  DESKTOP_CSS: [
    "/etc/designs/${app}/clientlibs_desktop_v1.css"
  ],

  //CSS used by mobile that need to be removed when desktop
  MOBILE_CSS: [
    "/etc/designs/${app}/clientlibs_mobile_v1.css"
  ],

  //id of the content that needs to be removed when mobile
  DESKTOP_MAIN_ID: "main",

  //id of the content that needs to be removed when desktop
  MOBILE_MAIN_ID: "main",

  //body classes used by desktop that need to be removed when mobile
  DESKTOP_BODY_CLASS: [
    "page"
  ],

  //body classes used by mobile that need to be removed when desktop
  MOBILE_BODY_CLASS: [
    "page-mobile"
  ]
};
```

## 範例：建立自訂內容存放區元件 {#example-creating-a-custom-context-store-component}

在此範例中，您會建立內容存放區元件，從外部服務擷取資料，並將其儲存在工作階段存放區中：

* 擴展genericstoreproperties元件。
* 使用CQ_Analytics.JSONPStore Javascript物件初始化儲存。
* 呼叫JSONP服務以擷取資料並將其新增至儲存。
* 在用戶端內容中轉譯資料。

### 新增geoloc元件 {#add-the-geoloc-component}

建立CQ應用程式並新增geoloc元件。

1. 在網頁瀏覽器中開啟CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 以滑鼠右鍵按一下 `/apps` ，然後按一下「建立」>「建立資料夾」。 指定名稱 `myapp` 然後按一下「確定」。
1. 同樣地，如下 `myapp`，建立名為 `contextstores`.&quot;
1. 以滑鼠右鍵按一下 `/apps/myapp/contextstores` 資料夾，然後按一下「建立>建立元件」。 指定下列屬性值，然後按一下「下一步」：

   * 標籤：geoloc
   * 標題：位置商店
   * 超類型：cq/personalization/components/contextstores/genericstoreproperties
   * 組：用戶端內容

1. 在「建立元件」對話框中，按一下每頁上的「下一步」，直到啟用「確定」按鈕，然後按一下「確定」。
1. 按一下「全部儲存」 。

### 建立Geoloc編輯對話框 {#create-the-geoloc-edit-dialog}

上下文儲存元件需要編輯對話方塊。 geoloc編輯對話方塊將包含靜態訊息，指出沒有要設定的屬性。

1. 以滑鼠右鍵按一下 `/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog` 節點，然後按一下「複製」。
1. 以滑鼠右鍵按一下 `/apps/myapp/contextstores/geoloc` 節點，然後按一下「貼上」。
1. 刪除/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items節點下的所有子節點：

   * 商店
   * 屬性
   * 縮圖

1. 以滑鼠右鍵按一下 `/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items` 節點，然後按一下「建立>建立節點」。 指定下列屬性值，然後按一下「確定」：

   * 名稱：靜態
   * 類型：cq:Widget

1. 將下列屬性新增至節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | cls | 字串 | x-form-fieldset-description |
   | text | 字串 | geoloc元件不需要設定。 |
   | xtype | 字串 | 靜態 |

1. 按一下「全部儲存」 。

   ![chlimage_1-5](assets/chlimage_1-5.png)

### 建立初始化指令碼 {#create-the-initialization-script}

將init.js.jsp檔案新增至geoloc元件，並使用它建立工作階段存放區、擷取位置資料，並將其新增至存放區。

init.js.jsp檔案會在頁面載入用戶端內容時執行。 此時，用戶端內容javascript API已載入，可供您的指令碼使用。

1. 以滑鼠右鍵按一下/apps/myapp/contextstores/geoloc節點，然後按一下「建立>建立檔案」。 指定init.js.jsp的名稱，然後按一下確定。
1. 將下列程式碼新增至頁面頂端，然後按一下「儲存全部」 。

   ```java
   <%@page contentType="text/javascript;charset=utf-8" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   log.info("***** initializing geolocstore ****");
   String store = "locstore";
   String jsonpurl = "https://api.wipmania.com/jsonp?callback=${callback}";
   
   %>
   var locstore = CQ_Analytics.StoreRegistry.getStore("<%= store %>");
   if(!locstore){
    locstore = CQ_Analytics.JSONPStore.registerNewInstance("<%= store %>", "<%= jsonpurl %>",{});
   }
   <% log.info(" ***** done initializing geoloc ************"); %>
   ```

### 呈現geoloc工作階段存放區資料 {#render-the-geoloc-session-store-data}

將代碼添加到geoloc元件的JSP檔案中，以在客戶端上下文中呈現儲存資料。

![chlimage_1-6](assets/chlimage_1-6.png)

1. 在CRXDE Lite中，開啟 `/apps/myapp/contextstores/geoloc/geoloc.jsp` 檔案。
1. 在存根代碼下添加以下HTML代碼：

   ```xml
   <%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
   <div class="cq-cc-store">
      <div class="cq-cc-content">
          <div class="cq-cc-store-property cq-cc-store-property-level0">
              Continent: <personalization:storePropertyTag propertyName="address/continent" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level1">
              Country: <personalization:storePropertyTag propertyName="address/country" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level2">
              City: <personalization:storePropertyTag propertyName="address/city" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level3">
              Latitude: <personalization:storePropertyTag propertyName="latitude" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level4">
              Longitude: <personalization:storePropertyTag propertyName="longitude" store="locstore"/>
          </div>
      </div>
       <div class="cq-cc-clear"></div>
   </div>
   ```

1. 按一下「全部儲存」 。

### 將元件新增至用戶端內容 {#add-the-component-to-client-context}

將Location Store元件新增至用戶端內容，以便在頁面載入時初始化元件。

1. 在製作執行個體上開啟Geometrixx Outdoors首頁([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 按一下Ctrl-Alt-c(windows)或control-option-c(Mac)以開啟「用戶端內容」。
1. 按一下「客戶端上下文」頂部的編輯表徵圖以開啟「客戶端上下文設計器」。

   ![](do-not-localize/chlimage_1.png)

1. 將「位置儲存」元件拖曳至「用戶端內容」。

### 請參閱用戶端內容中的位置資訊 {#see-the-location-information-in-client-context}

以編輯模式開啟Geometrixx Outdoors首頁，然後開啟用戶端內容以查看位置儲存元件中的資料。

1. 開啟Geometrixx Outdoors網站的英文頁面。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))
1. 若要開啟「用戶端內容」，請按Ctrl-Alt-c(windows)或control-option-c(Mac)。

## 建立自訂用戶端內容 {#creating-a-customized-client-context}

若要建立第二個用戶端內容，您需要複製分支：

`/etc/clientcontext/default`

* 子資料夾：
   `/content`
將包含自訂用戶端內容的內容。

* 資料夾：
   `/contextstores`
可讓您為內容存放區定義不同的設定。

若要使用自訂的用戶端內容，請編輯屬性
`path`
（如頁面範本中所包含）。 例如，作為的標準位置：
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
