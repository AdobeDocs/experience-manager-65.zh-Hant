---
title: 使用和擴充Widget（傳統UI）
seo-title: Using and Extending Widgets (Classic UI)
description: AEM網頁型介面使用AJAX和其他現代瀏覽器技術，讓作者直接在網頁上編輯和格式化內容
seo-description: AEM's web-based interface uses AJAX and other modern browser technologies to enable WYSIWYG editing and formatting of content by authors right on the web page
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4934'
ht-degree: 0%

---

# 使用和擴充Widget（傳統UI）{#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>本頁面說明傳統UI中Widget的使用方式，該UI已於AEM 6.4中淘汰。
>
>Adobe建議您運用現代 [觸控式UI](/help/sites-developing/touch-ui-concepts.md) 根據 [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) 和 [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

Adobe Experience Manager的網頁型介面使用AJAX和其他現代瀏覽器技術，讓作者直接在網頁上編輯和格式化內容。

Adobe Experience Manager(AEM)使用 [ExtJS](https://www.sencha.com/) widget程式庫，提供精良的使用者介面元素，可在所有最重要的瀏覽器上運作，並可建立案頭級UI體驗。

這些Widget包含在AEM中，除了供AEM本身使用外，也可供使用AEM建立的任何網站使用。

如需AEM中所有可用小工具的完整參考，請參閱 [介面工具集API檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html) 或 [現有xtype清單](/help/sites-developing/xtypes.md). 此外，也提供許多範例，說明如何使用ExtJS架構，位於 [森沙](https://www.sencha.com/products/extjs/examples/) 站點，框架的所有者。

本頁面提供如何使用和擴充Widget的相關分析。 它首先描述如何 [在頁面中包含用戶端代碼](#including-the-client-sided-code-in-a-page). 接著，它會說明已建立的一些範例元件，以說明一些基本用途和擴充功能。 這些元件可在 **使用ExtJS Widget** 封裝 **封裝共用**.

套件包含下列範例：

* [基本對話方塊](#basic-dialogs) 使用現成的Widget建置。
* [動態對話方塊](#dynamic-dialogs) 使用現成可用的Widget和自訂的JavaScript邏輯建置。
* 對話方塊 [自訂小工具](#custom-widgets).
* A [樹面板](#tree-overview) 在指定路徑下顯示JCR樹。
* A [網格面板](#grid-overview) 以表格格式顯示資料。

>[!NOTE]
>
>Adobe Experience Manager的傳統UI建置於 [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## 在頁面中包括用戶端代碼 {#including-the-client-sided-code-in-a-page}

客戶端javascript和樣式表代碼應放置在客戶端庫中。

要建立客戶端庫：

1. 在下方建立節點 `/apps/<project>` ，並搭配下列屬性：

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[混合：可鎖定]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * 類別=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widget]&quot;

   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. 在下 `clientlib` 建立 `css` 和 `js` 資料夾(nt:folder)。

1. 在下 `clientlib` 建立 `css.txt` 和 `js.txt` 檔案(nt:files)。 這些.txt檔案會列出程式庫中包含的檔案。

1. 編輯 `js.txt`:它需要從「 `#base=js`「 」，接著CQ用戶端程式庫服務要匯總的檔案清單，例如：

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. 編輯 `css.txt`:它需要從「 `#base=css`「 」，接著CQ用戶端程式庫服務要匯總的檔案清單，例如：

   ```
   #base=css
    components.css
   ```

1. 在 `js` 資料夾中，放置屬於程式庫的javascript檔案。

1. 在 `css` 資料夾，放置 `.css` 檔案和css檔案使用的資源(例如 `my_icon.png`)。

>[!NOTE]
>
>以前介紹的樣式表的處理是可選的。

要將客戶端庫包含在頁面元件jsp中：

* 要同時包括javascript代碼和樣式表，請執行以下操作：
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
where 
`<category-nameX>` 是用戶端程式庫的名稱。

* 僅包含javascript程式碼：
   `<ui:includeClientLib js="<category-name>"/>`

如需更多詳細資訊，請參閱 [&lt;ui:includeclientlib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 標籤。

在某些情況下，用戶端程式庫應僅能以製作模式使用，且應以發佈模式排除。 具體實現如下：

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### 範例快速入門 {#getting-started-with-the-samples}

若要遵循本頁的教學課程，請安裝以下的套件： **使用ExtJS Widget** 在本機AEM例項中，並建立要包含元件的範例頁面。 若要這麼做：

1. 在您的AEM例項中，下載以下的套件： **使用ExtJS Widget(v01)** 從「包共用」安裝包。 它會建立專案 `extjstraining` low `/apps` 儲存庫中。
1. 將包含指令碼(js)和樣式表(css)的用戶端程式庫包含在geometrixx頁jsp的head標籤中，因為您會將範例元件包含在的新頁面中 **Geometrixx** 分支：in **CRXDE Lite** 開啟檔案 `/apps/geometrixx/components/page/headlibs.jsp` 並新增 `cq.extjstraining` 類別至現有 `<ui:includeClientLib>` 標籤，如下所示：
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. 在 **Geometrixx** 分支 `/content/geometrixx/en/products` 然後叫它 **使用ExtJS Widget**.
1. 進入設計模式，然後新增群組的所有元件，稱為 **使用ExtJS Widget** 設計Geometrixx
1. 在編輯模式中返回：組成部分 **使用ExtJS Widget** 可在Sidekick中使用。

>[!NOTE]
>
>本頁的範例以Geometrixx範例內容為基礎，這些內容已由We.Retail取代，不再隨AEM提供。 請參閱檔案 [We.Retail參考實作](/help/sites-developing/we-retail.md#we-retail-geometrixx) 以了解如何下載和安裝Geometrixx。

### 基本對話方塊 {#basic-dialogs}

對話方塊通常用於編輯內容，但也只能顯示資訊。 檢視完整對話方塊的簡單方式，是存取其json格式的表示法。 若要這麼做，請將瀏覽器指向：

`https://localhost:4502/<path-to-dialog>.-1.json`

的第一個元件 **使用ExtJS Widget** sidekick中的群組稱為 **1. 對話基本知識** 和包含四個基本對話方塊，這些對話方塊是使用現成可用的Widget建置，而不使用自訂的Javascript邏輯。 對話方塊儲存於下方 `/apps/extjstraining/components/dialogbasics`. 基本對話方塊為：

* 完整對話方塊( `full` 節點):它顯示一個包含3個頁簽的窗口，每個頁簽都包含2個文本欄位。
* 「單一面板」對話方塊( `singlepanel` 節點):它會顯示一個包含1個標籤的視窗，其中包含2個文字欄位。
* 「多面板」對話框( `multipanel` 節點):其顯示與「完整」對話方塊相同，但建置方式不同。
* 設計對話方塊( `design` 節點):它顯示一個包含2個頁簽的窗口。 第一個頁簽具有文本欄位、下拉菜單和可折疊的文本區域。 第二個頁簽具有一個欄位集，其中包含4個文本欄位，另一個可折疊欄位集，其中包含2個文本欄位。

納入 **1. 對話基本知識** 元件（在範例頁面中）:

1. 新增 **1. 對話基本知識** 元件至範例頁面(從 **使用ExtJS Widget** 標籤 **Sidekick**.
1. 元件會顯示標題、部分文字和 **屬性** 連結：按一下連結以顯示儲存庫中儲存的段落的屬性。 再按一下連結以隱藏屬性。

元件顯示如下：

![chlimage_1-60](assets/chlimage_1-60.png)

#### 範例1:完整對話方塊 {#example-full-dialog}

此 **完整** 對話框顯示一個窗口，其中包含三個頁簽，每個頁簽都包含兩個文本欄位。 這是 **對話基本知識** 元件。 其特點是：

* 由節點定義：節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* 顯示3個頁簽(節點類型= `cq:Panel`)。
* 每個索引標籤有2個文字欄位(節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/full`
* 會以JSON格式呈現，方法是要求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

對話方塊顯示如下：

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 範例2:單一面板對話方塊 {#example-single-panel-dialog}

此 **單一面板** 對話框顯示一個窗口，其中一個頁簽包含兩個文本欄位。 其特點是：

* 顯示1個頁簽(節點類型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* 索引標籤有2個文字欄位(節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* 優於 **完整對話方塊** 就是需要的配置較少。
* 建議使用：顯示資訊或只有幾個欄位的簡單對話框。

若要使用「單一面板」對話方塊：

1. 取代 **對話基本知識** 元件 **單一面板** 對話框：
   1. 在 **CRXDE Lite**，刪除節點： `/apps/extjstraining/components/dialogbasics/dialog`
   1. 按一下 **全部儲存** 以儲存變更。
   1. 複製節點： `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. 將複製的節點貼到下方： `/apps/extjstraining/components/dialogbasics`
   1. 選取節點： `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`重新命名 `dialog`.
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 範例3:多面板對話方塊 {#example-multi-panel-dialog}

此 **多面板** 對話框的顯示與 **完整** 但對話的構建方式不同。 其特點是：

* 由節點定義(節點類型= `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)。
* 顯示3個頁簽(節點類型= `cq:Panel`)。
* 每個索引標籤有2個文字欄位(節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/multipanel`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* 優於 **完整對話方塊** 就是它有簡化的結構。
* 建議使用：對話框。

要使用「多面板」對話框，請執行以下操作：

1. 取代 **對話基本知識** 元件 **多面板** 對話框：請依照 [範例2:單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 範例4:豐富對話方塊 {#example-rich-dialog}

此 **Rich** 對話框顯示一個包含兩個頁簽的窗口。 第一個頁簽具有文本欄位、下拉菜單和可折疊的文本區域。 第二個頁簽有一個欄位集，包含四個文本欄位，一個可折疊欄位集包含兩個文本欄位。 其特點是：

* 由節點定義(節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 顯示2個頁簽(節點類型= `cq:Panel`)。
* 第一個索引標籤具有 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 帶有 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 和 ` [selection](/help/sites-developing/xtypes.md#selection)` 包含3個選項的介面工具集和可折疊 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 帶 ` [textarea](/help/sites-developing/xtypes.md#textarea)` 介面工具集。
* 第二個索引標籤具有 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 4件小工具 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 小工具和可折疊 `dialogfieldset` 2 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 小工具。
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/rich`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

若要使用 **Rich** 對話框：

1. 取代 **對話基本知識** 元件 **Rich** 對話框：請依照 [範例2:單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### 動態對話方塊 {#dynamic-dialogs}

的第二個元件 **使用ExtJS Widget** sidekick中的群組稱為 **2. 動態對話方塊** 包含三個使用現成可用小工具建立的動態對話方塊，以及 **使用自訂的javascript邏輯**. 對話方塊儲存於下方 `/apps/extjstraining/components/dynamicdialogs`. 動態對話方塊為：

* 切換頁簽對話框( `switchtabs` 節點):它會顯示一個包含兩個索引標籤的視窗。 第一個索引標籤有一個選項選項，包含三個選項：選取選項時，會顯示與選項相關的索引標籤。 第二個索引標籤有兩個文字欄位。
* 任意對話框( `arbitrary` 節點):它會顯示一個包含一個索引標籤的視窗。 索引標籤有一個欄位，可拖放或上傳資產，以及一個欄位，可顯示容納頁面和資產的相關資訊（如果參考了該頁面）。
* 切換欄位對話方塊( `togglefield` 節點):它會顯示一個包含一個索引標籤的視窗。 索引標籤中有核取方塊：勾選此欄位時，會顯示包含兩個文字欄位的欄位集。

若要包含 **2. 動態對話方塊** 元件：

1. 新增 **2. 動態對話方塊** 元件至範例頁面(從 **使用ExtJS Widget** 標籤 **Sidekick**.
1. 元件會顯示標題、部分文字和 **屬性** 連結：按一下以顯示儲存庫中儲存的段落的屬性。 再按一下以隱藏屬性。

元件顯示如下：

![chlimage_1-61](assets/chlimage_1-61.png)

#### 範例1:切換頁簽對話框 {#example-switch-tabs-dialog}

此 **切換標籤** 對話框顯示一個包含兩個頁簽的窗口。 第一個索引標籤有一個選項選項，包含三個選項：選取選項時，會顯示與選項相關的索引標籤。 第二個索引標籤有兩個文字欄位。

其主要特點是：

* 由節點定義(節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 顯示2個頁簽(節點類型= `cq:Panel`):1選擇頁簽，第2個頁簽取決於第1個頁簽（3個選項）中的選擇。
* 有3個可選頁簽(節點類型= `cq:Panel`)，每個欄位都有2個文字欄位(節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。 一次只會顯示一個選用索引標籤。
* 由 `switchtabs` 節點位於：
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

此邏輯是透過事件接聽程式和Javascript程式碼來實作，如下所示：

* 對話框節點具有「 `beforeshow`&quot;在顯示對話框之前隱藏所有可選頁簽的偵聽器：
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`

   `dialog.items.get(0)` 獲取包含「選擇」面板和3個可選面板的表。
* 此 `Ejst.x2` 物件是在 `exercises.js` 檔案位置：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在 `Ejst.x2.manageTabs()` 方法，作為 `index` 為–1時，會隱藏所有可選索引標籤（從1到3）。
* 選擇頁簽有2個監聽器：一個在載入對話框時顯示選定頁簽(&quot; `loadcontent`&quot; event)，以及變更選取項目時顯示所選索引標籤的索引標籤(&quot; `selectionchanged`「事件):
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* 在 `Ejst.x2.showTab()` 方法：
   `field.findParentByType('tabpanel')` 獲取包含所有頁簽( `field` 代表選取介面工具集)
   `field.getValue()` 獲取選取項的值，例如：tab2
   `Ejst.x2.manageTabs()` 顯示所選頁簽。
* 每個可選頁簽都有一個監聽器，它隱藏「 `render`&quot;事件：
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* 在 `Ejst.x2.hideTab()` 方法：
   `tabPanel` 是包含所有標籤的表格面板
   `index` 是可選頁簽的索引
   `tabPanel.hideTabStripItem(index)` 隱藏索引標籤

其顯示如下：

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 範例2:任意對話 {#example-arbitrary-dialog}

對話方塊通常會顯示基礎元件的內容。 此處描述的對話方塊稱為 **任意** 對話方塊，從不同元件提取內容。

此 **任意** 對話框顯示一個帶有一個頁簽的窗口。 索引標籤有兩個欄位：一個用於拖放或上傳資產，一個用於顯示容納頁面和資產的相關資訊（若已參考）。

其主要特點是：

* 由節點定義(節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 顯示1個表格介面工具集(節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)，具有1個面板(節點類型= `cq:Panel`)
* 面板具有smartfile介面工具集(節點類型= `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`)和擁有者介面工具集(節點類型= `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* 由 `arbitrary` 節點位於：
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

此邏輯是透過事件接聽程式和Javascript程式碼來實作，如下所示：

* 所有權繪製小部件具有「 `loadcontent`&quot;在載入內容時顯示包含元件的頁面和smartfile介面工具集引用的資產資訊的偵聽器：
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`

   `field` 是使用ownerdraw對象設定的
   `path` 是以元件的內容路徑設定(例如：/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs)
* 此 `Ejst.x2` 物件是在 `exercises.js` 檔案位置：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在 `Ejst.x2.showInfo()` 方法：
   `pagePath` 是包含元件的頁面路徑
   `pageInfo` 以json格式代表頁面屬性
   `reference` 是參考資產的路徑
   `metadata` 以json格式表示資產的中繼資料
   `ownerdraw.getEl().update(html);` 在對話方塊中顯示已建立的html

若要使用 **任意** 對話框：

1. 取代 **動態對話方塊** 元件 **任意** 對話框：請依照 [範例2:單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 範例3:切換欄位對話方塊 {#example-toggle-fields-dialog}

此 **切換欄位** 對話框顯示一個帶有一個頁簽的窗口。 索引標籤中有核取方塊：勾選此欄位時，會顯示包含兩個文字欄位的欄位集。

其主要特點是：

* 由節點定義(節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 顯示1個表格介面工具集(節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`)，具有1個面板(節點類型= `cq:Panel`)。
* 此面板具有選取/核取方塊Widget(節點類型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`)和可折疊的對話欄位集widget(節點類型= `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`)，預設為隱藏，包含2個文字欄位小工具(節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。
* 由 `togglefields` 節點位於：
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

此邏輯是透過事件接聽程式和Javascript程式碼來實作，如下所示：

* 「選擇」頁簽有2個監聽器：顯示內容載入時的dialogfieldset的對話欄位集(&quot; `loadcontent`&quot; event)，以及在更改選項時顯示對話框欄位集(&quot; `selectionchanged`「事件):
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* 此 `Ejst.x2` 物件是在 `exercises.js` 檔案位置：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在 `Ejst.x2.toggleFieldSet()` 方法：
   `box` 是選取物件
   `panel` 是包含選取項目和dialogfieldset小工具的面板
   `fieldSet` 是dialogfieldset對象
   `show` 是根據「 `show`&#39;是否顯示dialogfieldset

若要使用 **切換欄位** 對話框：

1. 取代 **動態對話方塊** 元件 **切換欄位** 對話框：請依照 [範例2:單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### 自訂介面工具集 {#custom-widgets}

AEM隨附的現成可用Widget應涵蓋大部分使用案例。 不過，有時可能需要建立自訂Widget，以滿足專案特定需求。 可通過擴展現有小部件來建立自定義小部件。 為協助您開始進行此類自訂， **使用ExtJS Widget** 套件包含三個使用三個不同自訂小工具的對話方塊：

* 多欄位對話方塊( `multifield` 節點)顯示一個包含一個頁簽的窗口。 索引標籤具有自訂的多欄位介面工具集，其中包含兩個欄位：一個下拉式功能表，其中包含兩個選項和一個文字欄位。 因為是以現成可用的為基礎 `multifield` 介面工具集（只有一個文本欄位），它具有 `multifield` 介面工具集。
* 樹瀏覽對話框( `treebrowse` 節點)顯示一個窗口，其中一個頁簽包含路徑瀏覽小工具：按一下箭頭時，會向上開啟一個窗口，您可以在其中瀏覽層次並選擇項目。 然後，項目的路徑會新增至路徑欄位，並在對話方塊關閉時持續保存。
* RTF編輯器外掛程式對話方塊( `rteplugin` 節點)，將自訂按鈕新增至RTF編輯器，以將一些自訂文字插入主要文字。 它包含 `richtext` 介面工具集(RTE)和自訂功能的介面工具集（透過RTE外掛程式機制新增）。

自訂Widget和外掛程式會包含在 **3. 自訂介面工具集** 的 **使用ExtJS Widget** 包。 若要將此元件包含至範例頁面：

1. 新增 **3. 自訂介面工具集** 元件至範例頁面(從 **使用ExtJS Widget** 標籤 **Sidekick**.
1. 元件會顯示標題、部分文字，以及按一下 **屬性** 連結，儲存在儲存庫中的段落的屬性。 再按一下會隱藏屬性。
元件顯示如下：

![chlimage_1-62](assets/chlimage_1-62.png)

#### 範例1:自訂多欄位介面工具集 {#example-custom-multifield-widget}

此 **自訂多欄位** 基於介面工具集的對話框顯示一個窗口，其中包含一個頁簽。 索引標籤具有自訂的多欄位介面工具集，與具有一個欄位的標準介面工具集不同，它有兩個欄位：一個下拉式功能表，其中包含兩個選項和一個文字欄位。

此 **自訂多欄位** 基於介面工具集的對話框：

* 由節點定義(節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 顯示1個表格介面工具集(節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)包含面板(節點類型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 面板具有 `multifield` widget（節點類型） `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`)。
* 此 `multifield` 介面工具集的欄位設定(節點類型= `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`)，此變數以自訂xtype &#39;為基礎 `ejstcustom`&#39;:
   * &#39; `fieldconfig`&#39;是 ` [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)` 物件。
   * &#39; `optionsProvider`&#39;是 `ejstcustom` 介面工具集。 已使用 `Ejst.x3.provideOptions` 定義於 `exercises.js` at:
      `/apps/extjstraining/clientlib/js/exercises.js`
和會傳回2個選項。
* 由 `multifield` 節點位於：
   `/apps/extjstraining/components/customwidgets/multifield`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

自訂多欄位介面工具集(xtype = `ejstcustom`):

* 是Javascript物件，稱為 `Ejst.CustomWidget`.
* 定義於 `CustomWidget.js` javascript檔案：
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* 將 ` [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)` 介面工具集。
* 有3個欄位： `hiddenField` （文本欄位）, `allowField` (ComboBox)和 `otherField` （文本欄位）
* 覆寫 `CQ.Ext.Component#initComponent` 若要新增3個欄位：
   * `allowField` 是 [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) 「select」類型的對象。 optionsProvider是Selection對象的配置，在對話框中定義的CustomWidget的optionsProvider配置已實例化
   * `otherField` 是 [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) 物件
* 覆寫方法 `setValue`, `getValue` 和 `getRawValue` of [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField) 若要以下格式設定及擷取CustomWidget的值：
   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`。
* 將自身註冊為「 `ejstcustom`&#39; xtype:
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

此 **自訂多欄位** 介面工具集對話方塊的顯示如下：

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 範例2:自訂樹狀瀏覽介面工具集 {#example-custom-treebrowse-widget}

自訂 **樹狀瀏覽** 基於介面工具集的對話框顯示一個窗口，其中包含一個包含自定義路徑瀏覽介面工具集的頁簽：按一下箭頭時，會向上開啟一個窗口，您可以在其中瀏覽層次並選擇項目。 然後，項目的路徑會新增至路徑欄位，並在對話方塊關閉時持續保存。

自定義樹瀏覽對話框：

* 由節點定義(節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 顯示1個表格介面工具集(節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)包含面板(節點類型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 面板具有自訂Widget(節點類型= `cq:Widget`, xtype = `ejstbrowse`)
* 由 `treebrowse` 節點位於：
   `/apps/extjstraining/components/customwidgets/treebrowse`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

自訂樹狀瀏覽介面工具集(xtype = `ejstbrowse`):

* 是Javascript物件，稱為 `Ejst.CustomWidget`.
* 定義於 `CustomBrowseField.js` javascript檔案：
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* 延伸 ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* 定義名為的瀏覽窗口 `browseWindow`.
* 覆寫 ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` 按一下箭頭時顯示瀏覽窗口。
* 定義 [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) 物件：
   * 它會呼叫註冊於的servlet以取得其資料 `/bin/wcm/siteadmin/tree.json`.
   * 其根為「 `apps/extjstraining`」。
* 定義 `window` 對象( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`):
   * 根據預先定義的面板。
   * 有 **確定** 按鈕，設定所選路徑的值並隱藏面板。
* 窗戶固定在 **路徑** 欄位。
* 所選路徑將從瀏覽欄位傳遞到上的窗口 `show` 事件。
* 將自身註冊為「 `ejstbrowse`&#39; xtype:
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

若要使用 **自訂樹狀瀏覽** 基於介面工具集的對話框：

1. 取代 **自訂介面工具集** 元件 **自訂樹狀瀏覽** 對話框：請依照 [範例2:單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 範例3:RTF編輯器(RTE)外掛程式 {#example-rich-text-editor-rte-plug-in}

此 **RTF編輯器(RTE)外掛程式** 「基於」對話方塊是以RTF編輯器為基礎的對話方塊，其中提供自訂按鈕，可在方括弧內插入某些自訂文字。 自訂文字可由某些伺服器端邏輯剖析（此範例中未實作），例如新增在指定路徑上定義的一些文字：

此 **RTE外掛程式** 基於對話框：

* 由rtplugin節點定義：
   `/apps/extjstraining/components/customwidgets/rteplugin`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* 此 `rtePlugins` 節點具有子節點 `inserttext` (節點類型= `nt:unstructured`)，以外掛程式命名。 其屬性稱為 `features`，定義RTE可使用的外掛程式功能。

RTE外掛程式：

* 是Javascript物件，稱為 `Ejst.InsertTextPlugin`.
* 定義於 `InsertTextPlugin.js` javascript檔案：
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* 將 ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` 物件。
* 下列方法會定義 ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` 物件，且在實作外掛程式中遭覆寫：
   * `getFeatures()` 會傳回外掛程式可用之所有功能的陣列。
   * `initializeUI()` 將新按鈕添加到RTE工具欄。
   * `notifyPluginConfig()` 當按鈕暫留時顯示標題和文字。
   * `execute()` 按一下按鈕並執行外掛程式動作時，會呼叫：它顯示一個窗口，用於定義要包括的文本。
* `insertText()` 使用對應的對話框對象插入文本 `Ejst.InsertTextPlugin.Dialog` （請參閱之後）。
* `executeInsertText()` 由呼叫 `apply()` 對話方塊的方法，會在 **確定** 按鈕。
* 將自身註冊為「 `inserttext`&#39;插件：
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* the `Ejst.InsertTextPlugin.Dialog` object定義按一下外掛程式按鈕時開啟的對話方塊。 對話方塊由面板、表單、文字欄位和2個按鈕(**確定** 和 **取消**)。

若要使用 **RTF編輯器(RTE)外掛程式** 基於對話框：

1. 取代 **自訂介面工具集** 元件 **RTF編輯器(RTE)外掛程式** 基於對話框：請依照 [範例2:單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件。
1. 按一下右側的最後一個圖示（四個箭頭的圖示）。 輸入路徑並按一下 **確定**:路徑會顯示在方括弧內([ ])。
1. 按一下 **確定** 來關閉RTF編輯器。

此 **RTF編輯器(RTE)外掛程式** 基於對話方塊的顯示如下：

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>此範例僅顯示如何實作邏輯的用戶端部分：佔位符(*[文字]*)，則會在伺服器端明確剖析（例如在元件JSP中）。

### 樹概述 {#tree-overview}

現成可用 ` [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` 物件提供樹狀結構資料的樹狀結構UI表示。 包含在 **使用ExtJS Widget** 套件會示範如何使用 `TreePanel` 對象，在指定路徑下顯示JCR樹。 窗口本身可以停靠/取消停靠。 在此示例中，窗口邏輯嵌入到元件jsp中， &lt;script>&lt;/script> 標籤。

若要包含 **樹概述** 元件至範例頁面：

1. 新增 **4. 樹概述** 元件至範例頁面(從 **使用ExtJS Widget** 標籤 **Sidekick**.
1. 元件隨即顯示：
   * 標題，帶有文字
   * a **屬性** 連結：按一下以顯示儲存庫中儲存的段落的屬性。 再按一下以隱藏屬性。
   * 浮動視窗，內含存放庫的樹狀表示，可展開。

元件顯示如下：

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

樹概述元件：

* 定義於：
   `/apps/extjstraining/components/treeoverview`

* 其對話框用於設定窗口的大小，以及固定/取消固定窗口（請參閱下面的詳細資訊）。

元件jsp:

* 從儲存庫中檢索寬度、高度和停靠屬性。
* 顯示樹概述資料格式的一些文本。
* 在javascript標籤之間，將視窗邏輯嵌入元件jsp中。
* 定義於：
   `apps/extjstraining/components/treeoverview/content.jsp`

元件jsp中嵌入的javascript代碼：

* 定義 `tree` 對象，方法是嘗試從頁中檢索樹窗口。
* 如果顯示樹的窗口不存在， `treePanel` ([CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel))已建立：
   * `treePanel` 包含用於建立視窗的資料。
   * 通過調用在註冊的servlet來檢索資料：
      `/bin/wcm/siteadmin/tree.json`
* 此 `beforeload` 偵聽器確保已載入點擊的節點。
* 此 `root` 對象設定路徑 `apps/extjstraining` 作為樹根。
* `tree` ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`)，則會根據預先定義 `treePanel`，及顯示為：
   `tree.show();`
* 如果窗口已存在，則根據從儲存庫檢索到的寬度、高度和停靠屬性顯示該窗口。

元件對話方塊：

* 顯示1個頁簽，其中包含2個欄位，用於設定樹概覽窗口的大小（寬度和高度），以及1個欄位用於固定/取消固定窗口
* 由節點定義(節點類型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 面板具有大小欄位小部件(節點類型= `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`)和選取介面工具集(節點類型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = `radio`)，包含2個選項(true/false)
* 由對話方塊節點在下列位置定義：
   `/apps/extjstraining/components/treeoverview/dialog`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* 顯示如下：

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### 格線概述 {#grid-overview}

「網格面板」以行和列的表格格式表示資料。 由下列部分組成：

* 商店：保存資料記錄（列）的模型。
* 欄模型：柱子的組成。
* 檢視：封裝用戶介面。
* 選取模型：選取行為。

包含在 **使用ExtJS Widget** 套件會顯示如何以表格格式顯示資料：

* 範例1使用靜態資料。
* 範例2使用從存放庫擷取的資料。

要將「網格概述」元件包含到示例頁，請執行以下操作：

1. 新增 **5。 格線概述** 元件至範例頁面(從 **使用ExtJS Widget** 標籤 **Sidekick**.
1. 元件隨即顯示：
   * 帶有文本的標題
   * a **屬性** 連結：按一下以顯示儲存庫中儲存的段落的屬性。 再按一下以隱藏屬性。
   * 包含表格格式的資料的浮動視窗。

元件顯示如下：

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 範例1:預設網格 {#example-default-grid}

在其現成可用的版本中， **格線概述** 元件以表格格式顯示含靜態資料的視窗。 在此示例中，邏輯通過兩種方式嵌入到元件jsp中：

* 一般邏輯定義於 &lt;script>&lt;/script> 標籤
* 特定邏輯可在單獨的.js檔案中使用，並在jsp中連結到。 This setup enables to easily switch between the two logic (static/dynamic) by commenting the desired &lt;script> tags.

網格概述元件：

* 定義於：
   `/apps/extjstraining/components/gridoverview`
* 其對話框用於設定窗口的大小，以及固定/取消固定窗口。

元件jsp:

* 從儲存庫中檢索寬度、高度和停靠屬性。
* 顯示一些文本作為網格概述資料格式的簡介。
* 參考定義GridPanel對象的Javascript代碼：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`

   `defaultgrid.js` 將一些靜態資料定義為GridPanel對象的基礎。
* 在javascript標籤之間嵌入javascript代碼，該標籤定義使用GridPanel對象的窗口對象。
* 定義於：
   `apps/extjstraining/components/gridoverview/content.jsp`

元件jsp中嵌入的javascript代碼：

* 定義 `grid` 物件，方法是嘗試從頁面擷取視窗元件：
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* 若 `grid` 不存在，a [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 對象( `gridPanel`)的定義方式為呼叫 `getGridPanel()` 方法（請參閱下方）。 此方法定義於 `defaultgrid.js`.
* `grid` 是 ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)` 物件，會根據預先定義的GridPanel顯示： `grid.show();`
* 若 `grid` 已存在，則會根據從儲存庫檢索到的寬度、高度和停靠的屬性來顯示。

Javascript檔案( `defaultgrid.js`)在元件jsp中引用，定義 `getGridPanel()` 方法，由JSP中嵌入的指令碼調用，並返回 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 物件，以靜態資料為基礎。 邏輯如下：

* `myData` 是靜態資料的陣列，格式為5欄4列的表格。
* `store` 是 `CQ.Ext.data.Store` 使用的對象 `myData`.
* `store` 已載入記憶體中：
   `store.load();`
* `gridPanel` 是 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 使用的對象 `store`:
   * 欄寬隨時會重新比例：
      `forceFit: true`
   * 一次只能選取一列：
      `singleSelect:true`

#### 範例2:參考搜索網格 {#example-reference-search-grid}

安裝套件時， `content.jsp` 的 **格線概述** 元件顯示基於靜態資料的網格。 可以修改元件以顯示具有以下特徵的網格：

* 有三欄。
* 是以呼叫Servlet從存放庫擷取的資料為基礎。
* 可以編輯最後一列的儲存格。 值持續存在於 `test` 由第一列中顯示的路徑定義的節點下的屬性。

如前一節所述，視窗物件會取得其 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 物件，方法是呼叫 `getGridPanel()` 在中定義的方法 `defaultgrid.js` 檔案位置 `/apps/extjstraining/components/gridoverview/defaultgrid.js`. **網格概述**元件針對 `getGridPanel()` 方法，在中定義 `referencesearch.js` 檔案位置 `/apps/extjstraining/components/gridoverview/referencesearch.js`. 切換元件jsp中參考的.js檔案後，網格將以從儲存庫擷取的資料為基礎。

切換元件jsp中引用的.js檔案：

1. 在 **CRXDE Lite**，在 `content.jsp` 元件的檔案中，對包含 `defaultgrid.js` 檔案，因此如下所示：
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. 從包含 `referencesearch.js` 檔案，因此如下所示：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. 儲存變更。
1. 重新整理範例頁面。

元件顯示如下：

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

元件jsp中引用的javascript代碼( `referencesearch.js`)定義 `getGridPanel()` 方法從元件jsp中調用並返回 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 物件，以動態從存放庫擷取的資料為基礎。 中的邏輯 `referencesearch.js` 將某些動態資料定義為GridPanel的基礎：

* `reader` 是 ` [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`為3欄以json格式讀取servlet回應的物件。
* `cm` 是 ` [CQ.Ext.grid.ColumnModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` 3欄的物件。
「測試」欄儲存格可依使用編輯器定義的方式加以編輯：
   `editor: new [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* 欄可排序：
   `cm.defaultSortable = true;`
* `store` 是 ` [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` 物件：
   * 它會呼叫註冊於「 」的servlet以取得其資料 `/bin/querybuilder.json`&quot;，其中幾個參數用於篩選查詢
   * 其基礎為 `reader`預先定義
   * 表格會根據&#x200B;**jcr:path**&#x200B;按升序列
* `gridPanel` 是 ` [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` 可編輯的物件：
   * 其基礎為預先定義 `store` 和列模型 `cm`
   * 一次只能選取一列：
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * the `afteredit` 接聽程式會在「**測試**&#x200B;已編輯「 」列：
      * 屬性&#39; `test`「**jcr:path**「 」欄是在儲存庫中使用儲存格的值設定
      * 如果POST成功，則會將值新增至 `store` 對象，否則它被拒絕
