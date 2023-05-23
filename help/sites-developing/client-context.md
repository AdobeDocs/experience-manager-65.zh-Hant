---
title: 客戶端上下文詳細資訊
seo-title: Client Context in Detail
description: 客戶端上下文表示動態裝配的用戶資料集合
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

# 客戶端上下文詳細資訊{#client-context-in-detail}

>[!NOTE]
>
>客戶端上下文已被ContextHub取代。 請參閱 [相關文檔](/help/sites-developing/contexthub.md) 的雙曲餘切值。

客戶端上下文表示動態組裝的用戶資料集合。 您可以使用資料確定在給定情況（內容目標）下要在網頁上顯示的內容。 該資料也可用於網站分析和頁面上的任何javascript。

客戶端上下文主要包括以下方面：

* 包含用戶資料的會話儲存。
* 顯示用戶資料並提供模擬用戶體驗工具的UI。
* A [javascript API](/help/sites-developing/ccjsapi.md) 用於與會話儲存交互。

建立獨立會話儲存並將其添加到客戶端上下文，或建立與上下文儲存元件關聯的會話儲存。 安AEM裝幾個可立即使用的上下文儲存元件。 您可以將這些元件用作元件的基礎。

有關開啟客戶端上下文、配置其顯示的資訊以及模擬用戶體驗的資訊，請參見 [客戶端上下文](/help/sites-administering/client-context.md)。

## 會話儲存 {#session-stores}

客戶端上下文包括包含用戶資料的各種會話儲存。 儲存資料來自以下源：

* 客戶端Web瀏覽器。
* 伺服器(請參見 [JSONP商店](/help/sites-administering/client-context.md#main-pars-variable-8) 用於儲存來自第三方源的資訊)

客戶端上下文框架提供 [javascript API](/help/sites-developing/ccjsapi.md) 用於與會話儲存交互以讀取和寫入用戶資料，以及偵聽和響應儲存事件。 您還可以為用於內容目標或其他目的的用戶資料建立會話儲存。

會話儲存資料仍保留在客戶端上。 客戶端上下文不會將資料寫回伺服器。 要向伺服器發送資料，請使用表單或開發自定義javascript。

每個會話儲存都是屬性值對的集合。 會話儲存表示（任何類型）的資料集合，其概念意義可由設計者和/或開發者決定。 下面的示例javascript代碼定義一個對象，該對象表示會話儲存可能包含的配置檔案資料：

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

會話儲存可以跨瀏覽器會話永續，或者只能對建立會話的瀏覽器會話永續。

>[!NOTE]
>
>儲存持久性使用瀏覽器儲存或Cookie( `SessionPersistence` cookie)。 瀏覽器儲存更常見。
>
>當瀏覽器關閉並重新開啟時，會話儲存可以從持久儲存中載入這些值。 然後需要清除瀏覽器快取以刪除舊值。

### 上下文儲存元件 {#context-store-components}

上下文儲存元件是可添加到「客戶端上下文」的CQ元件。 通常，上下文儲存元件顯示來自與它們關聯的會話儲存的資料。 但是，上下文儲存元件顯示的資訊並不限於會話儲存資料。

上下文儲存元件可以包括以下項：

* 定義客戶端上下文中外觀的JSP指令碼。
* 用於在Sidekick中列出元件的屬性。
* 編輯用於配置元件實例的對話框。
* 初始化會話儲存的Javascript。

有關可添加到上下文儲存的已安裝上下文儲存元件的說明，請參閱 [可用的客戶端上下文元件](/help/sites-administering/client-context.md#available-client-context-components)。

>[!NOTE]
>
>頁面資料不再作為預設元件存在於客戶端上下文中。 如果需要，可以通過編輯客戶端上下文和添加 **常規儲存屬性** 元件，然後配置它以定義 **儲存** 如 `pagedata`。

### 目標內容交付 {#targeted-content-delivery}

配置檔案資訊也用於傳遞 [目標內容](/help/sites-authoring/content-targeting-touch.md)。

![客戶端context_target內容傳遞](assets/clientcontext_targetedcontentdelivery.png) ![客戶端context_targetcontentdementdetail](assets/clientcontext_targetedcontentdeliverydetail.png)

## 將客戶端上下文添加到頁面 {#adding-client-context-to-a-page}

將「客戶端上下文」元件包含到網頁的正文部分以啟用「客戶端上下文」。 客戶端上下文元件節點的路徑為 `/libs/cq/personalization/components/clientcontext`。 要包括該元件，請將以下代碼添加到頁面元件的JSP檔案中，該檔案位於 `body` 頁面元素：

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

客戶端上下文元件使頁面載入實現客戶端上下文的客戶端庫。

* 客戶端上下文javascript API。
* 支援會話儲存、事件管理等的客戶端上下文框架。
* 定義的段。
* 為已添加到客戶端上下文的每個上下文儲存元件生成的init.js指令碼。
* （僅作者實例）客戶端上下文UI。

客戶端上下文UI僅在作者實例上可用。

## 擴展客戶端上下文 {#extending-client-context}

要擴展客戶端上下文，請建立會話儲存，並可選地顯示儲存資料：

* 為內容目標和Web分析所需的用戶資料建立會話儲存。
* 建立上下文儲存元件，使管理員能夠配置關聯的會話儲存，並在客戶端上下文中顯示儲存資料以用於測試目的。

>[!NOTE]
>
>如果您有（或建立） `JSONP` 提供資料的服務，您只需使用 `JSONP` 上下文儲存元件並將其映射到JSONP服務。 這將處理會話儲存。

### 建立會話儲存 {#creating-a-session-store}

為需要添加到客戶端上下文並從其檢索的資料建立會話儲存。 通常，您可以使用以下過程建立會話儲存：

1. 建立具有 `categories` 屬性值 `personalization.stores.kernel`。 客戶端上下文自動載入此類別的客戶端庫。

1. 配置客戶端庫資料夾，使其與 `personalization.core.kernel` 客戶端庫資料夾。 的 `personalization.core.kernel` 客戶端庫提供客戶端上下文javascript API。

1. 添加建立和初始化會話儲存的javascript。

在personalization.stores.kernel客戶端庫中包括javascript，將導致在載入客戶端上下文框架時建立儲存。

>[!NOTE]
>
>如果建立會話儲存作為上下文儲存元件的一部分，則可以將javascript放置在元件的init.js.jsp檔案中。 在這種情況下，只有將元件添加到「客戶端上下文」時，才會建立會話儲存。

#### 會話儲存的類型 {#types-of-session-stores}

會話儲存在瀏覽器會話期間建立並可用，或保留在瀏覽器儲存或cookie中。 Client Context Javascript API定義了幾個類，它們表示兩種類型的資料儲存：

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`:這些對象僅駐留在頁面DOM中。 建立資料並在頁面的生命週期中保留資料。
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`:這些對象駐留在頁面DOM中，並保留在瀏覽器儲存或Cookie中。 資料可跨頁和跨用戶會話使用。

API還提供了這些類的擴展，這些類專用於儲存JSON資料或JSONP資料：

* 僅會話對象： [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore) 和 [CQ_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore)。

* 永續對象： [CQ_Analytics.PeristedJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore) 和 [CQ_Analytics.PeristedJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore)。

#### 建立會話儲存對象 {#creating-the-session-store-object}

客戶端庫資料夾的javascript會建立並初始化會話儲存。 然後，必須使用上下文儲存管理器註冊會話儲存。 下面的示例建立並註冊 [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 的雙曲餘切值。

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

為儲存JSON資料，以下示例建立並註冊 [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 的雙曲餘切值。

```
if (!CQ_Analytics.myJSONStore) {
    CQ_Analytics.myJSONStore = CQ_Analytics.JSONStore.registerNewInstance("myjsonstore",{});
}
```

### 建立上下文儲存元件 {#creating-a-context-store-component}

建立上下文儲存元件以在客戶端上下文中呈現會話儲存資料。 建立後，您可以將上下文儲存元件拖到客戶端上下文上，以從會話儲存中呈現資料。 上下文儲存元件由以下項組成：

* 用於呈現資料的JSP指令碼。
* 編輯對話框。
* 用於初始化會話儲存的JSP指令碼。
* （可選）建立會話儲存的客戶端庫資料夾。 如果元件使用現有會話儲存，則無需包括客戶端庫資料夾。

#### 擴展提供的上下文儲存元件 {#extending-the-provided-context-store-components}

提AEM供可擴展的genericstore和genericstoreproperties上下文儲存元件。 儲存資料的結構決定了擴展的元件：

* 屬性 — 值對：擴展 `GenericStoreProperties` 元件。 此元件自動呈現屬性值對的儲存。 提供了幾個交互點：

   * `prolog.jsp` 和 `epilog.jsp`:元件交互，允許您在元件呈現之前或之後添加伺服器端邏輯。

* 複雜資料：擴展 `GenericStore` 元件。 然後，會話儲存將需要「呈現器」方法，每次需要呈現元件時都會調用該方法。 使用兩個參數調用呈現器函式：

   * `@param {String} store`
要呈現的儲存

   * `@param {String} divId`
必須呈現儲存的div的ID。

>[!NOTE]
>
>所有客戶端上下文元件都是通用儲存或通用儲存屬性元件的擴展。 在 `/libs/cq/personalization/components/contextstores` 的子菜單。

#### 在Sidekick中配置外觀 {#configuring-the-appearance-in-sidekick}

編輯「客戶端上下文」時，上下文儲存元件將顯示在Sidek中。 與所有元件一樣， `componentGroup` 和 `jcr:title` 客戶機上下文元件的屬性決定該元件的組和名稱。

具有 `componentGroup` 屬性值 `Client Context` 預設情況下顯示在Sidekick中。 如果為 `componentGroup` 屬性，必須使用「設計」模式將元件手動添加到Sidekick。

#### 上下文儲存元件實例 {#context-store-component-instances}

將上下文儲存元件添加到客戶端上下文時，將在下面建立表示元件實例的節點 `/etc/clientcontext/default/content/jcr:content/stores`。 此節點包含使用元件的編輯對話框配置的屬性值。

初始化客戶端上下文時，將處理這些節點。

#### 初始化關聯的會話儲存 {#initializing-the-associated-session-store}

將init.js.jsp檔案添加到元件中以生成Javascript代碼，該代碼初始化上下文儲存元件使用的會話儲存。 例如，使用初始化指令碼檢索元件的配置屬性，並使用這些屬性填充會話儲存。

當在作者實例和發佈實例的頁面載入上初始化客戶端上下文時，生成的javascript將添加到頁面。 在載入和呈現上下文儲存元件實例之前，將執行此JSP。

代碼必須將檔案的mime類型設定為 `text/javascript`或未執行。

>[!CAUTION]
>
>init.js.jsp指令碼在作者和發佈實例上執行，但前提是上下文儲存元件已添加到客戶端上下文。

以下過程建立init.js.jsp指令碼檔案並添加設定正確MIME類型的代碼。 執行儲存初始化的代碼將跟隨。

1. 按一下右鍵上下文儲存元件節點，然後按一下「建立」>「建立檔案」。
1. 在「名稱」(Name)欄位中，鍵入 `init.js.jsp` 然後按一下「OK（確定）」。
1. 在頁面頂部，添加以下代碼，然後按一下「全部保存」。

   ```java
   <%@page contentType="text/javascript" %>
   ```

### 呈現生成儲存屬性元件的會話儲存資料 {#rendering-session-store-data-for-genericstoreproperties-components}

使用一致的格式在客戶端上下文中顯示會話儲存資料。

#### 顯示屬性資料 {#displaying-property-data}

個性化標籤庫提供 `personalization:storePropertyTag` 標籤，用於顯示會話儲存的屬性值。 要使用標籤，請在JSP檔案中包括以下代碼行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

標籤具有以下格式：

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

的 `propertyName` attribute是要顯示的儲存屬性的名稱。 的 `store` attribute是註冊儲存的名稱。 以下示例標籤顯示 `authorizableId` 屬性 `profile` 商店：

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### HTML結構 {#html-structure}

personalization.ui客戶端庫資料夾(/etc/clientlibs/foundation/personalization/ui/themes/default)提供了Client Context用於格式化HTML代碼的CSS樣式。 以下代碼說明了用於顯示儲存資料的建議結構：

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

的 `/libs/cq/personalization/components/contextstores/profiledata` 上下文儲存元件使用此結構來顯示配置檔案會話儲存中的資料。 的 `cq-cc-thumbnail` 類會放置縮略圖。 的 `cq-cc-store-property-level*x*` 類格式化字母數字資料：

* level0、level1和level2垂直分佈，並使用白色字型。
* 水準3和任何附加的水準水準分佈，並使用帶有較深背景的白色字型。

![chlimage_1-4](assets/chlimage_1-4.png)

### 呈現一般儲存元件的會話儲存資料 {#rendering-session-store-data-for-genericstore-components}

要使用genericstore元件呈現儲存資料，您需要：

* 將personalization:storeRendererTag標籤添加到元件JSP指令碼，以標識會話儲存的名稱。
* 在會話儲存類上實現呈現器方法。

#### 標識一般儲存會話儲存 {#identifying-the-genericstore-session-store}

個性化標籤庫提供 `personalization:storePropertyTag` 標籤，用於顯示會話儲存的屬性值。 要使用標籤，請在JSP檔案中包括以下代碼行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

標籤具有以下格式：

```java
<personalization:storeRendererTag store="store_name"/>
```

#### 實現會話儲存呈現器方法 {#implementing-the-session-store-renderer-method}

然後，會話儲存將需要「呈現器」方法，每次需要呈現元件時都會調用該方法。 使用兩個參數調用呈現器函式：

* @param {String}儲存要呈現的儲存
* @param {字串}必須呈現儲存的div的divId。

## 與會話儲存交互 {#interacting-with-session-stores}

使用javascript與會話儲存交互。

### 訪問會話儲存 {#accessing-session-stores}

獲取會話儲存對象以讀取資料或將資料寫入儲存。 [CQ_Analytics.ClientContextMgr](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) 提供基於儲存名的對儲存的訪問。 獲取後，使用 [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 或 [CQ_Analytics.PeristedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore) 與儲存資料交互。

下面的示例獲取 `profile` 然後檢索 `formattedName` 商店裡的財產。

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

會話儲存觸發事件，因此可以添加偵聽器並基於這些事件觸發事件。

會話儲存建立在 `Observable` 的上界。 它們延伸 [ `CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable) 提供 ` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)` 的雙曲餘切值。

下面的示例將監聽器添加到 `update` 事件 `profile` 會話儲存。

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

### 檢查是否定義並初始化了會話儲存 {#checking-that-a-session-store-is-defined-and-initialized}

在載入會話儲存並使用資料初始化它們之前，會話儲存不可用。 以下因素會影響會話儲存可用性的時間安排：

* 頁面載入
* JavaScript載入
* JavaScript執行時間
* XHR請求的響應時間
* 對會話儲存的動態更改

使用 [CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils) 對象 [onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback) 和 [onStoreInitialized](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay) 方法，僅在會話儲存可用時訪問它們。 這些方法使您能夠註冊對會話註冊和初始化事件做出反應的事件偵聽器。

>[!CAUTION]
>
>如果你依賴另一家商店，你需要照顧商店從未註冊的情況。

以下示例使用 `onStoreRegistered` 事件 `profile` 會話儲存。 註冊儲存後，會將偵聽器添加到 `update` 會話儲存的事件。 更新儲存時， `<div class="welcome">` 將使用 `profile` 商店。

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

### 從會話持久性Cookie中排除屬性 {#excluding-a-property-from-the-sessionpersistence-cookie}

防止 `PersistedSessionStore` 從保留(即從 `sessionpersistence` cookie)，將屬性添加到永續會話儲存的非永續屬性清單中。

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

當前頁面必須有相應的移動頁面；僅當頁面配置了LiveCopy時，才會確定( `rolloutconfig.path.toLowerCase` 包含 `mobile`)。

#### 設定 {#configuration}

從案頭頁面切換到其移動對等頁面時：

* 已載入移動頁面的DOM。
* 主 `div` （必需），它包含內容，被提取並注入到當前案頭頁面中。

* 需要載入的CSS和正文類需要手動配置。

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

## 示例：建立自定義上下文儲存元件 {#example-creating-a-custom-context-store-component}

在本示例中，您建立一個上下文儲存元件，該元件從外部服務檢索資料並將其儲存在會話儲存中：

* 擴展genericstoreproperties元件。
* 使用CQ_Analytics.JSONPStore Javascript對象初始化儲存。
* 調用JSONP服務以檢索資料並將其添加到儲存中。
* 在客戶端上下文中呈現資料。

### 添加geoloc元件 {#add-the-geoloc-component}

建立CQ應用程式並添加geoloc元件。

1. 在Web瀏覽器中開啟CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 按一下右鍵 `/apps` 資料夾，然後按一下「建立」>「建立資料夾」。 指定名稱 `myapp` 然後按一下「OK（確定）」。
1. 同樣，下面 `myapp`，建立名為 `contextstores`。&quot;
1. 按一下右鍵 `/apps/myapp/contextstores` 資料夾，然後按一下「建立」(Create)>「建立元件」(Create Component)。 指定以下屬性值，然後按一下「下一步」：

   * 標籤：地質
   * 標題：位置儲存
   * 超級類型：cq/個性化/元件/上下文儲存/一般儲存屬性
   * 組：客戶端上下文

1. 在「建立元件」對話框中，按一下每頁上的「下一步」，直到啟用「確定」按鈕，然後按一下「確定」。
1. 按一下「全部保存」。

### 建立地理位置線編輯對話框 {#create-the-geoloc-edit-dialog}

上下文儲存元件需要編輯對話框。 geoloc編輯對話框將包含一條靜態消息，該消息指示沒有要配置的屬性。

1. 按一下右鍵 `/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog` ，然後按一下「複製」。
1. 按一下右鍵 `/apps/myapp/contextstores/geoloc` ，然後按一下「貼上」。
1. 刪除/apps/myapp/contextstores/geoloc/dialog/items/tab1/items節點下的所有子節點：

   * 商店
   * 屬性
   * 縮略圖

1. 按一下右鍵 `/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items` 節點，然後按一下「建立」>「建立節點」。 指定以下屬性值，然後按一下確定：

   * 名稱：靜態
   * 類型：cq：小部件

1. 將以下屬性添加到節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | CL | 字串 | x-form-fieldset-description |
   | text | 字串 | geoloc元件不需要配置。 |
   | x類型 | 字串 | 靜態 |

1. 按一下「全部保存」。

   ![chlimage_1-5](assets/chlimage_1-5.png)

### 建立初始化指令碼 {#create-the-initialization-script}

將init.js.jsp檔案添加到geoloc元件，並使用它建立會話儲存、檢索位置資料並將其添加到儲存。

當頁面載入客戶端上下文時，將執行init.js.jsp檔案。 此時，客戶端上下文javascript API已載入，並且可用於您的指令碼。

1. 按一下右鍵/apps/myapp/contextstores/geoloc節點，然後按一下「建立」>「建立檔案」。 指定init.js.jsp的名稱，然後按一下「確定」。
1. 將以下代碼添加到頁面頂部，然後按一下「全部保存」。

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

將代碼添加到geoloc元件的JSP檔案中，以在「客戶端上下文」中呈現儲存資料。

![chlimage_1-6](assets/chlimage_1-6.png)

1. 在CRXDE Lite中，開啟 `/apps/myapp/contextstores/geoloc/geoloc.jsp` 的子菜單。
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

1. 按一下「全部保存」。

### 將元件添加到客戶端上下文 {#add-the-component-to-client-context}

將「位置儲存」元件添加到「客戶端上下文」，以便在載入頁面時對其進行初始化。

1. 開啟作者實例上的Geometrixx Outdoors首頁([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 按一下Ctrl-Alt-c（窗口）或control-option-c(Mac)以開啟客戶端上下文。
1. 按一下「客戶端上下文」頂部的編輯表徵圖以開啟「客戶端上下文設計器」。

   ![](do-not-localize/chlimage_1.png)

1. 將「位置儲存」元件拖到「客戶端上下文」。

### 請參閱客戶端上下文中的位置資訊 {#see-the-location-information-in-client-context}

在編輯模式下開啟Geometrixx Outdoors首頁，然後開啟客戶端上下文，查看位置儲存元件中的資料。

1. 開啟Geometrixx Outdoors網站的英文頁。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))
1. 要開啟客戶端上下文，請按Ctrl-Alt-c（窗口）或control-option-c(Mac)。

## 建立自定義客戶端上下文 {#creating-a-customized-client-context}

要建立第二個客戶端上下文，您需要複製分支：

`/etc/clientcontext/default`

* 子資料夾：
   `/content`
將包含自定義客戶端上下文的內容。

* 資料夾：
   `/contextstores`
允許您為上下文儲存定義不同的配置。

要使用自定義的客戶端上下文，請編輯屬性
`path`
在頁面模板中包含的客戶端上下文元件的設計樣式中。 例如，作為以下項的標準位置：
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
