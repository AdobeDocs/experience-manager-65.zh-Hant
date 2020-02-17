---
title: 用戶端內容詳細說明
seo-title: 用戶端內容詳細說明
description: 「用戶端內容」代表動態組合的使用者資料集合
seo-description: 「用戶端內容」代表動態組合的使用者資料集合
uuid: 95b08fbd-4f50-44a1-80fb-46335fe04a40
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c881ad66-bcc3-4f99-b77f-0944c23e2d29
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 用戶端內容詳細說明{#client-context-in-detail}

>[!NOTE]
>
>ContextHub已取代用戶端內容。 如需詳細資訊， [請參閱相關](/help/sites-developing/contexthub.md) 檔案。

「用戶端內容」代表動態組合的使用者資料集合。 您可以使用資料來判斷在特定情況（內容定位）下要在網頁上顯示的內容。 此資料也可用於網站分析，以及頁面上的任何javascript。

Client Context主要包含下列方面：

* 包含使用者資料的作業存放區。
* 顯示使用者資料並提供工具以模擬使用者體驗的UI。
* 用於 [與作業存放區互動的Javascript](/help/sites-developing/ccjsapi.md) API。

若要建立獨立作業存放區並將其新增至「用戶端內容」，或建立系結至「內容存放區」元件的作業存放區。 AEM會安裝數個您可立即使用的Context Store元件。 您可以將這些元件當做元件的基礎。

如需有關開啟「用戶端內容」、設定其顯示的資訊以及模擬使用者體驗的詳細資訊，請參閱「用戶 [端內容」](/help/sites-administering/client-context.md)。

## 會話儲存 {#session-stores}

「用戶端內容」包含包含使用者資料的各種作業儲存區。 儲存來自下列來源的資料：

* 用戶端網頁瀏覽器。
* 伺服器(請參 [閱JSONP商店](/help/sites-administering/client-context.md#main-pars-variable-8) ，以儲存來自第三方來源的資訊)

Client Context架構提供 [javascript API](/help/sites-developing/ccjsapi.md) ，您可用來與作業存放區互動，以讀取和寫入使用者資料，以及監聽和回應儲存事件。 您也可以針對您用於內容定位或其他目的的使用者資料建立工作階段儲存。

會話儲存資料仍保留在客戶端上。 客戶端上下文不會將資料寫回伺服器。 若要傳送資料至伺服器，請使用表單或開發自訂javascript。

每個作業存放區都是屬性值配對的集合。 會話儲存表示（任何類型）的資料集合，其概念含義可由設計人員和／或開發人員決定。 下列範例javascript程式碼定義一個物件，代表作業階段儲存可能包含的描述檔資料：

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

作業存放區可跨瀏覽器作業持續存留，或僅適用於建立作業的瀏覽器作業。

>[!NOTE]
>
>商店永續性使用瀏覽器儲存或Cookie( `SessionPersistence` Cookie)。 瀏覽器儲存空間更常見。
>
>當瀏覽器關閉並重新開啟時，作業存放區可載入來自持續存放區的值。 然後需要清除瀏覽器快取，才能移除舊值。

### 上下文商店元件 {#context-store-components}

上下文儲存元件是可新增至「用戶端內容」的CQ元件。 通常，上下文儲存元件顯示來自與其關聯的會話儲存的資料。 但是，上下文儲存元件顯示的資訊不限於會話儲存資料。

上下文商店元件可包含下列項目：

* 定義客戶端上下文中外觀的JSP指令碼。
* 用於在Sidekick中列出元件的屬性。
* 編輯用於配置元件實例的對話框。
* 初始化作業存放區的Javascript。

有關可添加到上下文儲存庫的已安裝上下文儲存庫元件的說明，請參 [閱可用客戶端上下文元件](/help/sites-administering/client-context.md#available-client-context-components)。

>[!NOTE]
>
>「頁面資料」不再以預設元件的形式出現在用戶端內容中。 如果需要，可以通過編輯客戶機上下文、添加 **Generic Store Properties** （通用商店屬性）元件來添加此內容，然後將其配置為將 **Store定義為**`pagedata`。

### 目標內容傳送 {#targeted-content-delivery}

描述檔資訊也用於傳送目 [標內容](/help/sites-authoring/content-targeting-touch.md)。

![clientcontext_targetedcontentdeliveryclientcontext](assets/clientcontext_targetedcontentdelivery.png) _ ![targetedcontentdeliverydetail](assets/clientcontext_targetedcontentdeliverydetail.png)

## 新增用戶端內容至頁面 {#adding-client-context-to-a-page}

將「用戶端內容」元件加入網頁的正文區段，以啟用「用戶端內容」。 客戶端上下文元件節點的路徑為 `/libs/cq/personalization/components/clientcontext`。 若要包含此元件，請將下列程式碼新增至頁面元件的JSP檔案，該檔案位於頁面元 `body` 素的正下方：

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

clientcontext元件會使頁面載入實作「用戶端內容」的用戶端程式庫。

* 用戶端內容javascript API。
* 支援工作階段儲存、事件管理等的Client Context架構。
* 定義的區段。
* 為每個已添加到客戶端上下文的上下文儲存元件生成的init.js指令碼。
* （僅限作者例項）用戶端內容UI。

用戶端內容UI僅適用於作者例項。

## 擴充用戶端內容 {#extending-client-context}

若要擴充用戶端內容，請建立作業存放區並選擇性地顯示儲存資料：

* 為您針對內容定位和網頁分析所需的使用者資料建立工作階段商店。
* 建立內容儲存區元件，讓管理員可設定關聯的工作階段儲存區，並在「用戶端內容」中顯示儲存資料，以便進行測試。

>[!NOTE]
>
>如果您有（或建立）可 `JSONP` 以提供資料的服務，您只需使用內容儲存元件，並將 `JSONP` 它對應至JSONP服務。 這將處理會話儲存。

### 建立會話儲存 {#creating-a-session-store}

為需要添加到客戶端上下文並從中檢索的資料建立會話儲存。 通常，您使用以下過程建立會話儲存：

1. 建立屬性值為的客戶端 `categories` 庫資料夾 `personalization.stores.kernel`。 Client Context會自動載入此類別的用戶端程式庫。

1. 配置客戶端庫資料夾，使其與客戶端庫資料夾 `personalization.core.kernel` 具有相關性。 用戶 `personalization.core.kernel` 端程式庫提供用戶端內容javascript API。

1. 新增建立和初始化作業存放區的javascript。

將javascript包含在personalization.stores.kernel客戶程式庫中，會在載入Client Context架構時建立商店。

>[!NOTE]
>
>如果您要建立作為內容儲存元件一部分的作業儲存區，則可以選擇將javascript置於元件的init.js.jsp檔案中。 在這種情況下，只有將元件添加到「客戶端上下文」中時，才會建立會話儲存。

#### 會話儲存的類型 {#types-of-session-stores}

作業存放區會在瀏覽器作業期間建立並可用，或保存在瀏覽器儲存區或Cookie中。 Client Context javascript API定義了數個表示兩種資料儲存類型的類別：

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`:這些物件僅位於頁面DOM中。 資料會建立並保存在頁面的存留期間。
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`:這些物件位於頁面DOM中，並會持續存在瀏覽器儲存或Cookie中。 資料可跨頁和跨使用者作業使用。

API也提供這些類別的擴充功能，這些類別專門用來儲存JSON資料或JSONP資料：

* 僅會話對象： [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore)[和CQ_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore)。

* 持久對象： [CQ_Analytics.PeristingJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore)[和CQ_Analytics.PeristingJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore)。

#### 建立會話儲存對象 {#creating-the-session-store-object}

用戶端程式庫資料夾的javascript會建立並初始化工作階段商店。 然後，必須使用上下文商店管理員註冊作業商店。 下列範例會建立並注 [冊CQ_Analytics.SessionStore物件](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 。

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

若要儲存JSON資料，下列範例會建立並註冊 [CQ_Analytics.JSONStore物件](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 。

```
if (!CQ_Analytics.myJSONStore) {
    CQ_Analytics.myJSONStore = CQ_Analytics.JSONStore.registerNewInstance("myjsonstore",{});
}
```

### 建立上下文儲存元件 {#creating-a-context-store-component}

建立內容儲存元件，以在「用戶端內容」中呈現工作階段儲存資料。 建立後，您可將內容存放區元件拖曳至「用戶端內容」，以從作業存放區轉譯資料。 上下文商店元件包含下列項目：

* 用於呈現資料的JSP指令碼。
* 編輯對話框。
* 用於初始化會話儲存的JSP指令碼。
* （可選）用於建立會話儲存的客戶端庫資料夾。 如果元件使用現有會話儲存，則不需要包括客戶端庫資料夾。

#### 擴充提供的內容儲存元件 {#extending-the-provided-context-store-components}

AEM提供一般商店和一般商店屬性上下文商店元件，您可加以擴充。 儲存資料的結構決定了擴展的元件：

* 屬性——值對：延伸元 `GenericStoreProperties` 件。 此元件會自動呈現屬性值對的儲存區。 提供數個互動點：

   * `prolog.jsp` 和 `epilog.jsp`:元件互動功能，可讓您在元件轉換之前或之後新增伺服器端邏輯。

* 複雜資料：延伸元 `GenericStore` 件。 然後，您的作業商店將需要「轉譯器」方法，每次需要轉譯元件時都會呼叫此方法。 轉換程式函式是使用兩個參數來呼叫：

   * `@param {String} store`
要演算的商店

   * `@param {String} divId`
必須呈現商店的div的ID。

>[!NOTE]
>
>所有客戶端上下文元件都是通用儲存或通用儲存屬性元件的擴展。 資料夾中已安裝數個 `/libs/cq/personalization/components/contextstores` 範例。

#### 在Sidekick中設定外觀 {#configuring-the-appearance-in-sidekick}

編輯「用戶端內容」時，內容儲存元件會顯示在Sidekick中。 與所有元件一樣，客戶 `componentGroup` 端上下文 `jcr:title` 元件的組和屬性決定了元件的組和名稱。

預設會在Sidekick中顯 `componentGroup` 示屬性值 `Client Context` 為的所有元件。 如果對屬性使用不同的值， `componentGroup` 則必須使用「設計」模式手動將元件添加到Sidekick。

#### 上下文商店元件例項 {#context-store-component-instances}

將上下文儲存元件添加到「客戶端上下文」時，將在下面建立一個代表元件實例的節點 `/etc/clientcontext/default/content/jcr:content/stores`。 此節點包含使用元件的編輯對話框配置的屬性值。

初始化「客戶端上下文」時，會處理這些節點。

#### 初始化關聯的會話儲存 {#initializing-the-associated-session-store}

將init.js.jsp檔案新增至元件，以產生Javascript程式碼，以初始化上下文儲存區元件所使用的工作階段儲存區。 例如，使用初始化指令碼檢索元件的配置屬性，並使用這些屬性填充會話儲存。

當在作者和發佈例項的頁面載入時初始化「用戶端內容」時，產生的Javascript會新增至頁面。 此JSP在載入和呈現上下文儲存元件實例之前執行。

代碼必須將檔案的MIME類型設定為 `text/javascript`，否則不執行。

>[!CAUTION]
>
>init.js.jsp指令碼會在作者和發佈例項上執行，但前提是上下文儲存元件已新增至用戶端內容。

以下過程建立init.js.jsp指令碼檔案並添加設定正確MIME類型的代碼。 執行儲存初始化的代碼將遵循。

1. 按一下右鍵上下文儲存元件節點，然後按一下「建立」(Create)>「建立檔案」(Create File)。
1. 在「名稱」欄位中，輸入 `init.js.jsp` 並按一下「確定」。
1. 在頁面頂端，新增下列程式碼，然後按一下「全部儲存」。

   ```java
   <%@page contentType="text/javascript" %>
   ```

### 為一般儲存屬性元件呈現會話儲存資料 {#rendering-session-store-data-for-genericstoreproperties-components}

使用一致的格式，在「用戶端內容」中顯示工作階段儲存資料。

#### 顯示屬性資料 {#displaying-property-data}

個人化標籤庫提 `personalization:storePropertyTag` 供顯示工作階段商店中屬性值的標籤。 若要使用標籤，請在JSP檔案中加入下列程式碼行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

標籤具有下列格式：

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

屬 `propertyName` 性是要顯示之商店屬性的名稱。 屬 `store` 性是註冊商店的名稱。 下列範例標籤會顯示商店 `authorizableId` 屬性的 `profile` 值：

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### HTML結構 {#html-structure}

personalization.ui用戶端資料庫檔案夾(/etc/clientlibs/foundation/personalization/ui/themes/default)提供「用戶端內容」用來設定HTML程式碼格式的CSS樣式。 下列程式碼說明用於顯示儲存資料的建議結構：

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

上下文 `/libs/cq/personalization/components/contextstores/profiledata` 儲存元件使用此結構來顯示來自配置檔案會話儲存的資料。 類別 `cq-cc-thumbnail` 會放置縮圖影像。 類 `cq-cc-store-property-level*x*` 格式化字母數字資料：

* level0、level1和level2是垂直分佈的，並使用白字型。
* level3及任何其他層級均以水準分佈，並使用較深色背景的白色字型。

![chlimage_1-4](assets/chlimage_1-4.png)

### 為通用儲存元件呈現會話儲存資料 {#rendering-session-store-data-for-genericstore-components}

若要使用一般商店元件來轉換商店資料，您必須：

* 將personalization:storeRendererTag標籤新增至元件JSP指令碼，以識別作業商店的名稱。
* 在會話儲存類上實現渲染器方法。

#### 識別Genericstore會話儲存 {#identifying-the-genericstore-session-store}

個人化標籤庫提 `personalization:storePropertyTag` 供顯示工作階段商店中屬性值的標籤。 若要使用標籤，請在JSP檔案中加入下列程式碼行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

標籤具有下列格式：

```java
<personalization:storeRendererTag store="store_name"/>
```

#### 實現會話儲存渲染器方法 {#implementing-the-session-store-renderer-method}

然後，您的作業商店將需要「轉譯器」方法，每次需要轉譯元件時都會呼叫此方法。 轉換程式函式是使用兩個參數來呼叫：

* @param {String}商店要轉譯的商店
* 必須轉譯商店的div的@param {String} divId。

## 與會話儲存交互 {#interacting-with-session-stores}

使用javascript與作業存放區互動。

### 訪問會話儲存 {#accessing-session-stores}

獲取會話儲存對象以讀取或寫入資料到儲存。 [CQ_Analytics.ClientContextMgr](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) ，可根據商店名稱提供對商店的存取。 取得後，請使用 [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 或 [](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore) CQ_Analytics.PeristedSessionStore的方法與儲存資料互動。

下面的示例獲取存 `profile` 儲，然後從儲存 `formattedName` 中檢索屬性。

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

工作階段會儲存觸發事件，因此可以新增監聽器並根據這些事件觸發事件。

會話儲存器是基於模式 `Observable` 構建的。 它們可 [ 以擴 `CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable) 展提供方 ` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)` 法。

下面的示例將偵聽程式添加到會 `update` 話儲存的 `profile` 事件中。

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

### 檢查是否已定義並初始化會話儲存 {#checking-that-a-session-store-is-defined-and-initialized}

會話儲存在載入並用資料初始化之前不可用。 下列因素可能會影響作業存放區可用性的時間：

* 頁面載入
* JavaScript載入
* JavaScript執行時間
* XHR請求的回應時間
* 會話儲存的動態更改

使用 [CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils) 物件的 [onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback) 和 [](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay) onStoreInitialized方法，只有在工作階段儲存可用時才可存取。 這些方法可讓您註冊回應作業註冊和初始化事件的事件接聽程式。

>[!CAUTION]
>
>如果您依賴其他商店，則需要迎合從未註冊商店的情況。

下面的示例使用 `onStoreRegistered` 會話儲存的 `profile` 事件。 在註冊儲存時，會向會話儲存的事 `update` 件添加偵聽器。 更新商店時，頁面上的元 `<div class="welcome">` 素內容會以商店的名稱更 `profile` 新。

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

### 從作業永續性Cookie中排除屬性 {#excluding-a-property-from-the-sessionpersistence-cookie}

若要防止某個屬 `PersistedSessionStore` 性持續存在(亦即從 `sessionpersistence` Cookie中排除它)，請將屬性新增至持續作業商店的非持續屬性清單。

請參閱 ` [CQ_Analytics.PersistedSessionStore.setNonPersisted(propertyName)](/help/sites-developing/ccjsapi.md#setnonpersisted-name)`

```
CQ_Analytics.ClientContextUtils.onStoreRegistered("surferinfo", function(store) {
  //this will exclude the browser, OS and resolution properties of the surferinfo session store from the
  store.setNonPersisted("browser");
  store.setNonPersisted("OS");
  store.setNonPersisted("resolution");
});
```

## 配置設備滑塊 {#configuring-the-device-slider}

### 條件 {#conditions}

目前頁面必須有對應的行動頁面；這只有在頁面有LiveCopy設定為行動轉出設定（包含）時 `rolloutconfig.path.toLowerCase` 才 `mobile`決定。

#### 設定 {#configuration}

從案頭頁面切換至其行動裝置頁面時：

* 已載入行動頁面的DOM。
* 包含內 `div` 容的主（必要）會擷取並插入目前的案頭頁面。

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

## 範例：建立自訂內容商店元件 {#example-creating-a-custom-context-store-component}

在此示例中，您建立上下文儲存元件，該元件從外部服務中檢索資料並將其儲存在會話儲存中：

* 延伸一般儲存屬性元件。
* 使用CQ_Analytics.JSONPStore javascript物件初始化商店。
* 呼叫JSONP服務以擷取資料並將其新增至商店。
* 在用戶端內容中轉譯資料。

### 新增geoloc元件 {#add-the-geoloc-component}

建立CQ應用程式並新增geoloc元件。

1. 在您的網頁瀏覽器(https://localhost:4502/crx/de)中開啟CRXDE[Lite](https://localhost:4502/crx/de)。
1. 按一下右鍵資料夾， `/apps` 然後按一下「建立」>「建立資料夾」。 指定名稱，然 `myapp` 後按一下「確定」。
1. 同樣地，在下 `myapp`面建立名為的資料夾 `contextstores`。&quot;
1. 按一下右鍵資料夾， `/apps/myapp/contextstores` 然後按一下「建立」(Create)>「建立元件」(Create Component)。 指定下列屬性值，然後按一下「下一步」:

   * 標籤：geoloc
   * 標題：位置商店
   * 超級類型：cq/personalization/components/contextstores/genericstoreproperties
   * 群組：用戶端內容

1. 在「建立元件」對話方塊中，按一下每頁的「下一步」，直到啟用「確定」按鈕，然後按一下「確定」。
1. 按一下「全部儲存」。

### 建立geoloc編輯對話框 {#create-the-geoloc-edit-dialog}

上下文儲存區元件需要編輯對話方塊。 geoloc edit對話框將包含一條靜態消息，指出沒有要配置的屬性。

1. 按一下右鍵該節 `/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog` 點，然後按一下複製。
1. 按一下右鍵該節 `/apps/myapp/contextstores/geoloc` 點，然後按一下貼上。
1. 刪除/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items節點下的所有子節點：

   * 商店
   * 屬性
   * 縮圖

1. 按一下右鍵該節 `/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items` 點，然後按一下建立>建立節點。 指定下列屬性值，然後按一下「確定」:

   * 名稱：靜態
   * 類型：cq:Widget

1. 將以下屬性添加到節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | cls | 字串 | x-form-fieldset-description |
   | 文字 | 字串 | geoloc元件不需要配置。 |
   | xtype | 字串 | 靜態 |

1. 按一下「全部儲存」。

   ![chlimage_1-5](assets/chlimage_1-5.png)

### 建立初始化指令碼 {#create-the-initialization-script}

將init.js.jsp檔案新增至geoloc元件，並使用它來建立作業存放區、擷取位置資料，並將它新增至存放區。

init.js.jsp檔案會在頁面載入用戶端內容時執行。 目前，用戶端內容javascript API已載入，可供您的指令碼使用。

1. 按一下右鍵/apps/myapp/contextstores/geoloc節點，然後按一下「建立」>「建立檔案」。 指定init.js.jsp的名稱，然後按一下「確定」。
1. 將下列程式碼新增至頁面頂端，然後按一下「全部儲存」。

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

### 呈現geoloc會話儲存資料 {#render-the-geoloc-session-store-data}

將代碼添加到geoloc元件的JSP檔案中，以在Client context中呈現儲存資料。

![chlimage_1-6](assets/chlimage_1-6.png)

1. 在CRXDE Lite中，開啟檔 `/apps/myapp/contextstores/geoloc/geoloc.jsp` 案。
1. 在存根程式碼下方新增下列HTML程式碼：

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

1. 按一下「全部儲存」。

### 將元件新增至用戶端內容 {#add-the-component-to-client-context}

將Location Store元件新增至Client Context，以便在頁面載入時初始化它。

1. 在作者例項(https://localhost:4502/content/geometrixx-outdoors/en.html)上開啟Geometrixx Outdoors首[頁](https://localhost:4502/content/geometrixx-outdoors/en.html)。
1. 按一下Ctrl-Alt-c(windows)或control-option-c(Mac)以開啟「用戶端內容」。
1. 按一下「用戶端內容」頂端的編輯圖示，以開啟「用戶端內容設計器」。

   ![](do-not-localize/chlimage_1.png)

1. 將Location Store元件拖曳至Client Context。

### 請參閱用戶端內容中的位置資訊 {#see-the-location-information-in-client-context}

以編輯模式開啟Geometrixx Outdoors首頁，然後開啟Client Context以檢視Location Store元件的資料。

1. 開啟Geometrixx Outdoors網站的英文頁面。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))
1. 要開啟「客戶端上下文」，請按Ctrl-Alt-c(windows)或control-option-c(Mac)。

## 建立自訂用戶端內容 {#creating-a-customized-client-context}

要建立第二個客戶機上下文，您需要複製分支：

`/etc/clientcontext/default`

* 子資料夾：
   `/content`
將包含自訂用戶端內容的內容。

* 資料夾：
   `/contextstores`
允許您為上下文儲存庫定義不同的配置。

若要使用自訂的用戶端內容，請`path`以用戶端內容元件的設計樣式編輯屬性，如頁面範本所示。 例如，作為以下的標準位置：
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
