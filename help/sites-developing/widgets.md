---
title: 使用和擴充Widget(Classic UI)
seo-title: 使用和擴充Widget(Classic UI)
description: AEM的網路介面使用AJAX和其他現代瀏覽器技術，讓作者直接在網頁上編輯和格式化內容，
seo-description: AEM的網路介面使用AJAX和其他現代瀏覽器技術，讓作者直接在網頁上編輯和格式化內容，
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '4965'
ht-degree: 0%

---


# 使用和擴充Widget(Classic UI){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>本頁說明傳統UI中Widget的使用情形，AEM 6.4已過時。
>
>Adobe建議您運用以[Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)和[Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components)為基礎的現代化觸控式UI[。](/help/sites-developing/touch-ui-concepts.md)

Adobe Experience Manager的網頁介面使用AJAX和其他現代瀏覽器技術，讓作者直接在網頁上編輯和格式化內容。

Adobe Experience Manager(AEM)使用[ExtJS](https://www.sencha.com/) Widget程式庫，提供高度精美的使用者介面元素，可跨所有最重要的瀏覽器運作，並允許建立案頭等級的UI體驗。

這些Widget包含在AEM中，而且除了AEM本身使用外，還可供任何使用AEM建立的網站使用。

如需AEM中所有可用介面工具集的完整參考，請參閱[介面工具集API檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)或現有xtypes](/help/sites-developing/xtypes.md)清單。 [此外，在[Sencha](https://www.sencha.com/products/extjs/examples/)網站（架構的擁有者）上，也提供許多說明如何使用ExtJS架構的範例。

本頁提供如何使用和擴充Widget的深入資訊。 它首先說明如何[在頁面](#including-the-client-sided-code-in-a-page)中包含用戶端程式碼。 然後，它說明已建立的一些範例元件，以說明其基本用途和擴充功能。 這些元件可在&#x200B;**Package Share**&#x200B;上的&#x200B;**Using ExtJS Widgets**&#x200B;套件中使用。

此套件包含下列範例：

* [使](#basic-dialogs) 用現成可用的Widget建立基本對話方塊。
* [使用](#dynamic-dialogs) 現成可用的Widget和自訂的Javascript邏輯建立動態對話方塊。
* 以[自訂Widget](#custom-widgets)為基礎的對話方塊。
* [樹面板](#tree-overview)在給定路徑下顯示JCR樹。
* [格線面板](#grid-overview)以表格格式顯示資料。

>[!NOTE]
>
>Adobe Experience Manager的傳統UI建立在[ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/)上。

## 在頁面{#including-the-client-sided-code-in-a-page}中包含用戶端代碼

客戶端的javascript和樣式表代碼應放置在客戶端庫中。

要建立客戶端庫：

1. 使用以下屬性在`/apps/<project>`下建立節點：

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * 類別=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. 在`clientlib`下面建立`css`和`js`資料夾(nt:folder)。

1. 在`clientlib`下建立`css.txt`和`js.txt`檔案(nt:files)。 這些。txt檔案會列出程式庫所包含的檔案。

1. 編輯`js.txt`:它需要從&#39; `#base=js`&#39;開始，後面接著CQ客戶端庫服務要聚合的檔案清單，例如：

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. 編輯`css.txt`:它需要從&#39; `#base=css`&#39;開始，後面接著CQ客戶端庫服務要聚合的檔案清單，例如：

   ```
   #base=css
    components.css
   ```

1. 在`js`資料夾下方，放置屬於程式庫的javascript檔案。

1. 在`css`資料夾下方，放置`.css`檔案和css檔案所使用的資源(例如`my_icon.png`)。

>[!NOTE]
>
>以前所述的樣式表處理是可選的。

要在頁面元件jsp中包含客戶端庫，請：

* 要同時包括javascript代碼和樣式表，請執行以下操作：
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
where 
`<category-nameX>` 是客戶端庫的名稱。

* 若要僅包含javascript程式碼：
   `<ui:includeClientLib js="<category-name>"/>`

如需詳細資訊，請參閱[&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib)標籤的說明。

在某些情況下，用戶端程式庫只能在作者模式下使用，而且應在發佈模式中排除。 具體實現如下：

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### 開始使用範例{#getting-started-with-the-samples}

若要遵循本頁的教學課程，請在本機AEM例項中安裝名為&#x200B;**使用ExtJS Widgets**&#x200B;的套件，並建立包含元件的範例頁面。 若要這麼做：

1. 在您的AEM例項中，從「套件共用」下載名為「使用ExtJS Widgets(v01)**的套件並安裝此套件。**&#x200B;它會在儲存庫中建立`/apps`下的`extjstraining`項目。
1. 將包含指令碼(js)和樣式表(css)的用戶端程式庫包含在geometrixx頁面jsp的head標籤中，因為您會將範例元件包含在&#x200B;**Geometrixx**分支的新頁面中：
在**CRXDE Lite**&#x200B;中，開啟檔案`/apps/geometrixx/components/page/headlibs.jsp`並將`cq.extjstraining`類別新增至現有的`<ui:includeClientLib>`標籤，如下所示：
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. 在`/content/geometrixx/en/products`下方的&#x200B;**Geometrixx**&#x200B;分支中建立新頁面，並呼叫&#x200B;**使用ExtJS Widgets**。
1. 進入設計模式，並將名為&#x200B;**「使用ExtJS Widgets**&#x200B;的群組所有元件新增至Geometrixx的設計
1. 返回編輯模式：「使用ExtJS介面工具集」群組&#x200B;**的元件可在Sidekick中使用。**

>[!NOTE]
>
>本頁的範例是以Geometrixx範例內容為基礎，此內容已不再隨AEM一起出貨，而已由We.Retail取代。 如需如何下載和安裝Geometrixx的資訊，請參閱檔案[We.Retail Reference Implementation](/help/sites-developing/we-retail.md#we-retail-geometrixx)。

### 基本對話框{#basic-dialogs}

對話框通常用於編輯內容，但也只能顯示資訊。 檢視完整對話方塊的簡單方式，是存取其json格式的表示法。 若要這麼做，請將您的瀏覽器指向：

`https://localhost:4502/<path-to-dialog>.-1.json`

Sidekick中&#x200B;**使用ExtJS Widgets**&#x200B;群組的第一個元件稱為&#x200B;**1。 Dialog Basics**&#x200B;並包含4個基本對話方塊，這些對話方塊是使用現成可用的Widget建立，而不需自訂的Javascript邏輯。 對話方塊儲存在`/apps/extjstraining/components/dialogbasics`下方。 基本對話框包括：

* 完整對話框（`full`節點）:它顯示一個包含3個頁籤的窗口，每個頁籤具有2個文本欄位。
* 「單面板」對話框（`singlepanel`節點）:它顯示一個包含1個頁籤的窗口，其中包含2個文本欄位。
* 多面板對話框（`multipanel`節點）:其顯示與「完整」對話框相同，但其構建方式不同。
* 設計對話框（`design`節點）:它顯示一個包含2個頁籤的窗口。 第一個標籤具有文字欄位、下拉式選單和可收合的文字區域。 第二個標籤有一個欄位集，其中包含4個文本欄位，另一個可折疊的欄位集，其中包含2個文本欄位。

包含&#x200B;**1。 範例頁中的Dialog Basics**&#x200B;元件：

1. 添加&#x200B;**1。 從** Sidekick **的「使用ExtJS Widgets**」標籤中，將Dialog Basics **元件傳送至範例頁面。**
1. 元件顯示標題、部分文本和&#x200B;**PROPERTIES**&#x200B;連結：按一下連結可顯示儲存在儲存庫中的段落的屬性。 再按一下連結以隱藏屬性。

元件顯示如下：

![chlimage_1-60](assets/chlimage_1-60.png)

#### 範例1:完整對話框{#example-full-dialog}

**Full**&#x200B;對話方塊會顯示一個視窗，其中包含三個標籤，每個標籤包含兩個文字欄位。 它是&#x200B;**Dialog Basics**&#x200B;元件的預設對話框。 其特點是：

* 由節點定義：節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`。
* 顯示3個頁籤（節點類型= `cq:Panel`）。
* 每個頁籤有2個文本欄位（節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/full`
* 以JSON格式呈現，請求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

對話方塊顯示如下：

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 範例2:單面板對話框{#example-single-panel-dialog}

**「單一面板」**&#x200B;對話方塊會顯示一個視窗，其中有一個標籤包含兩個文字欄位。 其特點是：

* 顯示1個頁籤（節點類型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）
* 該頁籤有2個文本欄位（節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* 請求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* 與&#x200B;**Full Dialog**&#x200B;相比，其優勢之一是所需的配置更少。
* 建議使用：，以取得顯示資訊或只有幾個欄位的簡單對話方塊。

要使用「單一面板」對話框：

1. 將&#x200B;**Dialog Basics**&#x200B;元件的對話框替換為&#x200B;**Single Panel**&#x200B;對話框：
   1. 在&#x200B;**CRXDE Lite**&#x200B;中，刪除節點：`/apps/extjstraining/components/dialogbasics/dialog`
   1. 按一下&#x200B;**保存所有**&#x200B;保存更改。
   1. 複製節點：`/apps/extjstraining/components/dialogbasics/singlepanel`
   1. 將複製的節點貼上到下面：`/apps/extjstraining/components/dialogbasics`
   1. 選擇節點：`/apps/extjstraining/components/dialogbasics/Copy of singlepanel`並將其重新命名為`dialog`。
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 範例3:多面板對話框{#example-multi-panel-dialog}

**多面板**&#x200B;對話框的顯示與&#x200B;**完整**&#x200B;對話框的顯示相同，但其構建方式不同。 其特點是：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）。
* 顯示3個頁籤（節點類型= `cq:Panel`）。
* 每個頁籤有2個文本欄位（節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/multipanel`
* 請求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* 與&#x200B;**Full Dialog**&#x200B;相比，其優點之一是其結構簡化。
* 建議使用：對話框。

要使用「多面板」對話框：

1. 將&#x200B;**Dialog Basics**&#x200B;元件的對話框替換為&#x200B;**Multi Panel**對話框：
請遵循[範例2說明的步驟：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 範例4:豐富對話框{#example-rich-dialog}

**Rich**&#x200B;對話方塊會顯示一個包含兩個標籤的視窗。 第一個標籤具有文字欄位、下拉式選單和可收合的文字區域。 第二個頁籤具有一個欄位集，其中包含四個文本欄位和一個可折疊的欄位集，其中包含兩個文本欄位。 其特點是：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示2個頁籤（節點類型= `cq:Panel`）。
* 第一個頁籤具有` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`介面工具集（帶有` [textfield](/help/sites-developing/xtypes.md#textfield)`）和` [selection](/help/sites-developing/xtypes.md#selection)`介面工具集（帶有3個選項），以及帶有` [textarea](/help/sites-developing/xtypes.md#textarea)`介面工具集的可折疊` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`。
* 第二個標籤具有` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`介面工具集（4個` [textfield](/help/sites-developing/xtypes.md#textfield)`介面工具集）和可折疊`dialogfieldset`介面工具集（2個` [textfield](/help/sites-developing/xtypes.md#textfield)`介面工具集）。
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/rich`
* 請求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

要使用&#x200B;**Rich**&#x200B;對話框：

1. 將&#x200B;**Dialog Basics**&#x200B;元件的對話框替換為&#x200B;**Rich**對話框：
請遵循[範例2說明的步驟：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at50429](assets/screen_shot_2012-01-31at50429pm.png) ![pmscreen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### 動態對話框{#dynamic-dialogs}

Sidekick中&#x200B;**使用ExtJS Widgets**&#x200B;群組的第二個元件稱為&#x200B;**2。 動態對話方塊**&#x200B;並包含三個動態對話方塊，這些對話方塊是使用現成可用的Widget建立，而&#x200B;**則使用自訂的javascript邏輯**。 對話方塊儲存在`/apps/extjstraining/components/dynamicdialogs`下方。 動態對話框包括：

* 交換機頁籤對話框（`switchtabs`節點）:它顯示一個包含兩個頁籤的窗口。 第一個標籤有一個頁籤選項，其中包含三個選項：當選取選項時，會顯示與選項相關的標籤。 第二個標籤有兩個文字欄位。
* 任意對話框（`arbitrary`節點）:它會顯示一個含有一個標籤的視窗。 此標籤有一個可拖放或上傳資產的欄位，以及一個欄位，其中顯示有關包含頁面的資訊，以及參考資產的資訊。
* 切換欄位對話框（`togglefield`節點）:它會顯示一個含有一個標籤的視窗。 該頁籤具有複選框：勾選時，會顯示包含兩個文字欄位的欄位集。

包含&#x200B;**2。 範例頁面上的動態對話框**&#x200B;元件：

1. 添加&#x200B;**2。 從** Sidekick **的「使用ExtJS Widgets**」標籤中，動態對話方塊&#x200B;**元件至範例頁面。**
1. 元件顯示標題、部分文本和&#x200B;**PROPERTIES**&#x200B;連結：按一下以顯示儲存在儲存庫中的段落的屬性。 再按一下以隱藏屬性。

元件顯示如下：

![chlimage_1-61](assets/chlimage_1-61.png)

#### 範例1:交換機頁籤對話框{#example-switch-tabs-dialog}

**交換機頁籤**&#x200B;對話框顯示一個帶有兩個頁籤的窗口。 第一個標籤有一個頁籤選項，其中包含三個選項：當選取選項時，會顯示與選項相關的標籤。 第二個標籤有兩個文字欄位。

其主要特點是：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示2個頁籤（節點類型= `cq:Panel`）:1頁籤，第2個頁籤取決於第1個頁籤（3個選項）中的選擇。
* 有3個可選頁籤（節點類型= `cq:Panel`），每個頁籤有2個文本欄位（節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。 一次只顯示一個可選頁籤。
* 由`switchtabs`節點定義，位於：
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* 請求：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

邏輯是透過事件接聽程式和javascript程式碼實作，如下所示：

* 對話框節點具有&quot; `beforeshow`&quot;偵聽器，在顯示對話框之前隱藏所有可選頁籤：
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`

   `dialog.items.get(0)` 取得包含選取面板和3個選用面板的表格面板。
* `Ejst.x2`物件定義於`exercises.js`檔案中，網址為：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在`Ejst.x2.manageTabs()`方法中，由於`index`的值為-1，所有可選頁籤都隱藏（i從1到3）。
* 選擇頁籤有2個偵聽程式：一個在載入對話框時顯示選定頁籤（&quot; `loadcontent`&quot;事件），另一個在更改選擇時顯示選定頁籤（&quot; `selectionchanged`&quot;事件）:
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* 在`Ejst.x2.showTab()`方法中：
   `field.findParentByType('tabpanel')` 取得包含所有標籤的表格面板( `field` 代表選取介面工具集)
   `field.getValue()` 獲取選擇的值，例如：tab2
   `Ejst.x2.manageTabs()` 顯示選定頁籤。
* 每個可選頁籤都有一個偵聽器，它隱藏&quot; `render`&quot;事件上的頁籤：
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* 在`Ejst.x2.hideTab()`方法中：
   `tabPanel` 是包含所有標籤的表格面板
   `index` 是可選頁籤的索引
   `tabPanel.hideTabStripItem(index)` 隱藏標籤

其顯示如下：

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 範例2:任意對話框{#example-arbitrary-dialog}

對話方塊通常會顯示基礎元件的內容。 此處介紹的對話方塊稱為&#x200B;**Arbitary**&#x200B;對話方塊，會從不同的元件提取內容。

**任意**&#x200B;對話框顯示一個帶有一個頁籤的窗口。 此標籤包含兩個欄位：一個要拖放或上傳資產，另一個要顯示包含頁面的相關資訊，而另一個要顯示包含頁面的相關資訊（如果已參考）。

其主要特點是：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示1個面板構件（節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）和1個面板（節點類型= `cq:Panel`）
* 此面板具有smartfile Widget（節點類型= `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`）和ownerdraw Widget（節點類型= `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`）
* 由`arbitrary`節點定義，位於：
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* 請求：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

邏輯是透過事件接聽程式和javascript程式碼實作，如下所示：

* ownerdraw Widget有一個&quot; `loadcontent`&quot;偵聽器，它顯示包含元件的頁面和smartfile Widget在載入內容時引用的資產的相關資訊：
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`

   `field` 與ownerdraw對象一起設定
   `path` 是與元件的內容路徑一起設定(例如：/content/geometrixx/tw/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs)
* `Ejst.x2`物件定義於`exercises.js`檔案中，網址為：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在`Ejst.x2.showInfo()`方法中：
   `pagePath` 是包含該元件的頁面的路徑
   `pageInfo` 代表json格式的頁面屬性
   `reference` 是參考資產的路徑
   `metadata` 代表json格式的資產中繼資料
   `ownerdraw.getEl().update(html);` 在對話方塊中顯示已建立的html

要使用&#x200B;**任意**&#x200B;對話框：

1. 將&#x200B;**動態對話框**&#x200B;元件的對話框替換為&#x200B;**任意**對話框：
請遵循[範例2說明的步驟：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 範例3:切換欄位對話方塊{#example-toggle-fields-dialog}

**切換欄位**&#x200B;對話方塊會顯示一個含有一個標籤的視窗。 該頁籤具有複選框：勾選時，會顯示包含兩個文字欄位的欄位集。

其主要特點是：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示1個面板構件（節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`）和1個面板（節點類型= `cq:Panel`）。
* 面板具有選擇／複選框構件（節點類型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`，類型= ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`）和可折疊的對話框欄位集構件（節點類型= `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`），預設情況下隱藏，並有2個文本欄位構件（節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由`togglefields`節點定義，位於：
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* 請求：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

邏輯是透過事件接聽程式和javascript程式碼實作，如下所示：

* 選擇頁籤有2個偵聽程式：一個顯示載入內容時的對話框欄位集（&quot; `loadcontent`&quot;事件），另一個顯示更改選擇時的對話框欄位集（&quot; `selectionchanged`&quot;事件）:
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* `Ejst.x2`物件定義於`exercises.js`檔案中，網址為：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在`Ejst.x2.toggleFieldSet()`方法中：
   `box` 是選擇對象
   `panel` 是包含選取範圍和對話欄位集Widget的面板
   `fieldSet` 是對話框欄位集對象
   `show` 是根據對話框欄位集的&#39; `show`&#39;選擇的值（true或false）

要使用&#x200B;**切換欄位**&#x200B;對話框：

1. 將&#x200B;**動態對話框**&#x200B;元件的對話框替換為&#x200B;**切換欄位**對話框：
請遵循[範例2說明的步驟：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### 自訂介面工具集{#custom-widgets}

AEM隨附的現成可用Widget應涵蓋大部分的使用案例。 不過，有時可能需要建立自訂介面工具集，以涵蓋專案特定需求。 您可以延伸現有的Widget來建立自訂Widget。 為協助您開始進行此類自訂，**使用ExtJS Widgets**&#x200B;套件包含三個使用三個不同自訂Widget的對話方塊：

* 「多欄位」對話框（`multifield`節點）顯示一個帶有一個頁籤的窗口。 此標籤有一個自訂的多欄位介面工具集，其中包含兩個欄位：下拉式選單（含兩個選項）和文字欄位。 由於它以現成可用的`multifield`介面工具集（僅包含文字欄位）為基礎，因此具有`multifield`介面工具集的所有功能。
* 「樹瀏覽」對話框（`treebrowse`節點）顯示一個窗口，其中一個頁籤包含路徑瀏覽構件：按一下箭頭時，將開啟一個窗口，您可以在其中瀏覽層次並選擇一個項目。 然後項目的路徑會新增至路徑欄位，並在對話方塊關閉時持續存在。
* 「富格文本編輯器插件」對話框（`rteplugin`節點），它向富格文本編輯器添加一個自定義按鈕，以將一些自定義文本插入主文本。 它由`richtext` Widget(RTE)和通過RTE插件機制添加的自定義功能組成。

自訂Widget和外掛程式都包含在名為&#x200B;**3的元件中。**&#x200B;使用ExtJS Widgets **套件的自訂Widget**。 要將此元件包含到示例頁中：

1. 添加&#x200B;**3。 自訂Widgets**&#x200B;元件至&#x200B;**Sidekick**&#x200B;中「使用ExtJS Widgets **」標籤的範例頁面。**
1. 元件顯示標題和部分文本，並在按一下&#x200B;**PROPERTIES**連結時，顯示儲存在儲存庫中的段落的屬性。 再按一下會隱藏屬性。
元件顯示如下：

![chlimage_1-62](assets/chlimage_1-62.png)

#### 範例1:自訂多欄位介面工具集{#example-custom-multifield-widget}

**自訂多欄位**&#x200B;介面工具集對話方塊會顯示一個含有一個標籤的視窗。 此標籤有自訂的多欄位介面工具集，與標準的多欄位介面工具集不同，它有兩個欄位：下拉式選單（含兩個選項）和文字欄位。

**自訂多欄位**&#x200B;介面工具集對話方塊：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示1個包含面板（節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）的面板構件（節點類型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* 此面板具有`multifield`介面工具集（節點類型= `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`）。
* `multifield`介面工具集具有基於自定義xtype &#39; `ejstcustom`&#39;的欄位配置（節點類型= `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`）:
   * 「 `fieldconfig`」是` [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)`對象的配置選項。
   * &#39; `optionsProvider`&#39;是`ejstcustom`介面工具集的配置。 它以`Ejst.x3.provideOptions`方法設定，定義於`exercises.js`，網址為：
      `/apps/extjstraining/clientlib/js/exercises.js`
並傳回2個選項。
* 由`multifield`節點定義，位於：
   `/apps/extjstraining/components/customwidgets/multifield`
* 請求：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

自訂多欄位介面工具集(xtype = `ejstcustom`):

* 是名為`Ejst.CustomWidget`的javascript物件。
* 定義於`CustomWidget.js` javascript檔案中：
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* 延伸` [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)`介面工具集。
* 有3個欄位：`hiddenField`（文字欄位）、`allowField`(ComboBox)和`otherField`（文字欄位）
* 覆寫`CQ.Ext.Component#initComponent`以新增3個欄位：
   * `allowField` 是CQ. [form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) Selectionobject，類型為&#39;select&#39;。optionsProvider是Selection物件的設定，會以對話方塊中定義之自訂介面工具集的optionsProvider設定實例化
   * `otherField` 是 [CQ.Ext.form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) TextFieldobject
* 覆寫[的`setValue`、`getValue`和`getRawValue`方法CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)，以設定並擷取格式為：
   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`。
* 將自身註冊為&#39; `ejstcustom`&#39; xtype:
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

**自訂多欄位**&#x200B;介面工具集對話方塊顯示如下：

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 範例2:自訂樹狀瀏覽介面工具集{#example-custom-treebrowse-widget}

基於自定義&#x200B;**樹狀瀏覽**&#x200B;構件的對話框顯示一個窗口，其中一個頁籤包含自定義路徑瀏覽構件：按一下箭頭時，將開啟一個窗口，您可以在其中瀏覽層次並選擇一個項目。 然後項目的路徑會新增至路徑欄位，並在對話方塊關閉時持續存在。

自訂樹狀瀏覽對話框：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示1個包含面板（節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）的面板構件（節點類型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* 面板具有自訂介面工具集（節點類型= `cq:Widget`, xtype = `ejstbrowse`）
* 由`treebrowse`節點定義，位於：
   `/apps/extjstraining/components/customwidgets/treebrowse`
* 請求：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

自訂樹狀瀏覽介面工具集(xtype = `ejstbrowse`):

* 是名為`Ejst.CustomWidget`的javascript物件。
* 定義於`CustomBrowseField.js` javascript檔案中：
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* 延伸` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`。
* 定義名為`browseWindow`的瀏覽窗口。
* 覆寫` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick`以在按下箭頭時顯示瀏覽視窗。
* 定義[CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)物件：
   * 它通過調用在`/bin/wcm/siteadmin/tree.json`註冊的servlet來獲取其資料。
   * 其根為&quot; `apps/extjstraining`&quot;。
* 定義`window`對象(` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`):
   * 根據預先定義的面板。
   * 具有&#x200B;**OK**&#x200B;按鈕，可設定選定路徑的值並隱藏面板。
* 窗口錨定在&#x200B;**Path**&#x200B;欄位下。
* 所選路徑將從瀏覽欄位傳遞到`show`事件上的窗口。
* 將自身註冊為&#39; `ejstbrowse`&#39; xtype:
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

要使用基於&#x200B;**自定義樹狀瀏覽**&#x200B;構件的對話框：

1. 將&#x200B;**自訂介面工具集**&#x200B;元件的對話方塊取代為&#x200B;**自訂樹狀瀏覽**對話方塊：
請遵循[範例2說明的步驟：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 範例3:富格文本編輯器(RTE)插件{#example-rich-text-editor-rte-plug-in}

基於&#x200B;**Rich Text Editor(RTE)Plug-in**&#x200B;的對話框是基於Rich Text Editor的對話框，它具有一個自定義按鈕，可在方括弧內插入一些自定義文本。 自訂文字可由某些伺服器端邏輯來解析（在此範例中未實作），例如新增某些在指定路徑上定義的文字：

基於&#x200B;**RTE plugin**&#x200B;的對話框：

* 由retplugin節點定義，位於：
   `/apps/extjstraining/components/customwidgets/rteplugin`
* 請求：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* `rtePlugins`節點具有以插件命名的子節點`inserttext`（節點類型= `nt:unstructured`）。 它有一個名為`features`的屬性，用於定義RTE可用的插件功能。

RTE外掛程式：

* 是名為`Ejst.InsertTextPlugin`的javascript物件。
* 定義於`InsertTextPlugin.js` javascript檔案中：
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* 擴展` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`對象。
* 下列方法定義` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`物件，並在實作外掛程式中覆寫：
   * `getFeatures()` 傳回外掛程式可用之所有功能的陣列。
   * `initializeUI()` 將新按鈕添加到RTE工具欄。
   * `notifyPluginConfig()` 在按鈕暫留時顯示標題和文字。
   * `execute()` 在按下按鈕並執行外掛程式動作時呼叫：它顯示一個窗口，用於定義要包含的文本。
* `insertText()` 使用對應的對話框對象插入 `Ejst.InsertTextPlugin.Dialog` 文本（請參見後面）。
* `executeInsertText()` 由對話框的 `apply()` 方法調用，該方法在按一下「確定」按鈕時 **** 觸發。
* 將自身註冊為&#39; `inserttext`&#39; plugin:
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* `Ejst.InsertTextPlugin.Dialog`物件定義在按下外掛程式按鈕時開啟的對話方塊。 該對話框由面板、表單、文本欄位和2個按鈕（**OK**&#x200B;和&#x200B;**Cancel**）組成。

要使用基於&#x200B;**Rich Text Editor(RTE)Plug-in**&#x200B;的對話框：

1. 將&#x200B;**自訂介面工具集**&#x200B;元件的對話方塊取代為以&#x200B;**RTE外掛程式**為基礎的對話方塊：
請遵循[範例2說明的步驟：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件。
1. 按一下右邊的最後一個圖示（四個箭頭的圖示）。 輸入路徑，然後按一下&#x200B;**OK**:
路徑顯示在方括弧內([ ])。
1. 按一下&#x200B;**確定**&#x200B;以關閉Rich Text Editor。

基於&#x200B;**Rich Text Editor(RTE)Plug-in**&#x200B;的對話框顯示如下：

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>此範例僅說明如何實作邏輯的用戶端部分：然後必須在伺服器端顯式解析佔位符（例如，在元件JSP中）。]**[

### 樹概述{#tree-overview}

現成可用的` [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)`物件提供樹狀結構資料的樹狀結構UI表示。 **使用ExtJS Widgets**&#x200B;套件中包含的樹概述元件顯示了如何使用`TreePanel`對象在給定路徑下顯示JCR樹。 窗口本身可以與塢站連接／斷開塢站連接。 在此示例中，窗口邏輯嵌入到&lt;script>&lt;/script>標籤之間的元件jsp中。

要將&#x200B;**樹概述**&#x200B;元件包含到示例頁中：

1. 添加&#x200B;**4。 樹概述**&#x200B;元件到&#x200B;**Sidekick**&#x200B;中「使用ExtJS Widgets **」標籤中的示例頁。**
1. 元件將顯示：
   * 標題，含有文字
   * a **屬性**&#x200B;連結：按一下以顯示儲存在儲存庫中的段落的屬性。 再按一下以隱藏屬性。
   * 一個浮動窗口，其中包含儲存庫的樹形表示，可以展開。

元件顯示如下：

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

樹概述元件：

* 定義於：
   `/apps/extjstraining/components/treeoverview`

* 其對話框用於設定窗口的大小和將窗口固定／取消固定（請參閱下面的詳細資訊）。

元件jsp:

* 從儲存庫檢索寬度、高度和停靠屬性。
* 顯示樹概述資料格式的一些文本。
* 在javascript標籤之間，將視窗邏輯內嵌在元件jsp中。
* 定義於：
   `apps/extjstraining/components/treeoverview/content.jsp`

元件jsp中嵌入的javascript代碼：

* 通過嘗試從頁面檢索樹窗口來定義`tree`對象。
* 如果顯示樹的窗口不存在，則建立`treePanel`([CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)):
   * `treePanel` 包含用於建立窗口的資料。
   * 通過調用在以下位置註冊的servlet來檢索資料：
      `/bin/wcm/siteadmin/tree.json`
* `beforeload`偵聽器確保已載入已按一下的節點。
* `root`對象將路徑`apps/extjstraining`設定為樹根。
* `tree` ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`)是根據預先定義而設定 `treePanel`，並以下列方式顯示：
   `tree.show();`
* 如果窗口已存在，則根據從儲存庫檢索到的寬度、高度和停靠屬性來顯示窗口。

元件對話框：

* 顯示1個標籤和2個欄位，以設定樹概述窗口的大小（寬度和高度），並顯示1個欄位以固定／取消固定窗口
* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* 此面板具有大小欄位構件（節點類型= `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`）和選擇構件（節點類型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = `radio`），其中包含2個選項(true/false)
* 由對話框節點定義，位於：
   `/apps/extjstraining/components/treeoverview/dialog`
* 請求：
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* 顯示如下：

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### 格線概述{#grid-overview}

「格線面板」以表格式表示行和列的資料。 它由以下幾部分組成：

* 商店：保存資料記錄（行）的模型。
* 欄模型：專欄的構成。
* 檢視：封裝了用戶介面。
* 選擇模型：選擇行為。

**使用ExtJS Widgets**&#x200B;套件中包含的格線概述元件顯示如何以表格格式顯示資料：

* 範例1使用靜態資料。
* 示例2使用從儲存庫檢索到的資料。

要將網格概述元件包括到示例頁中，請執行以下操作：

1. 添加&#x200B;**5。 格線概述**&#x200B;元件至範例頁面，範例頁面位於&#x200B;**Sidekick**&#x200B;的「使用ExtJS Widgets **」標籤中。**
1. 元件將顯示：
   * 帶有文字的標題
   * a **屬性**&#x200B;連結：按一下以顯示儲存在儲存庫中的段落的屬性。 再按一下以隱藏屬性。
   * 包含表格格式的資料的浮動窗口。

元件顯示如下：

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 範例1:預設網格{#example-default-grid}

在其現成版本中，**格線概述**&#x200B;元件以表格格式顯示一個包含靜態資料的窗口。 在此示例中，邏輯以兩種方式嵌入到元件jsp中：

* 一般邏輯定義於&lt;script>&lt;/script>標籤之間
* 特定邏輯可在個別的。js檔案中使用，並在jsp中連結至。 此設定可讓您在兩個邏輯（靜態／動態）之間輕鬆切換，方法是加上所需&lt;script>標籤的註解。

網格概述元件：

* 定義於：
   `/apps/extjstraining/components/gridoverview`
* 其對話框用於設定窗口的大小，並將窗口固定／取消固定。

元件jsp:

* 從儲存庫檢索寬度、高度和停靠屬性。
* 顯示部分文字作為網格概述資料格式的簡介。
* 參考定義GridPanel物件的Javascript程式碼：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`

   `defaultgrid.js` 將某些靜態資料定義為GridPanel對象的基礎。
* 在javascript標籤之間內嵌javascript程式碼，此標籤定義使用GridPanel物件的Window物件。
* 定義於：
   `apps/extjstraining/components/gridoverview/content.jsp`

元件jsp中嵌入的javascript代碼：

* 通過嘗試從頁面檢索窗口元件來定義`grid`對象：
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* 如果`grid`不存在，則[CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)物件(`gridPanel`)是透過呼叫`getGridPanel()`方法來定義的（請參閱下文）。 此方法在`defaultgrid.js`中定義。
* `grid` 是基於 ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)` 預定義的GridPanel的對象，並顯示：  `grid.show();`
* 如果`grid`已存在，則根據從儲存庫檢索到的寬度、高度和塢站連接屬性來顯示該屬性。

元件jsp中引用的javascript檔案(`defaultgrid.js`)定義了`getGridPanel()`方法，該方法由嵌入在JSP中的指令碼調用，並基於靜態資料返回` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`對象。 邏輯如下：

* `myData` 是一組靜態資料，格式為5列和4行的表。
* `store` 是一 `CQ.Ext.data.Store` 個使用的對象 `myData`。
* `store` 已載入到記憶體中：
   `store.load();`
* `gridPanel` 是一 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 個對象，它使用 `store`:
   * 欄寬會隨時重新比例：
      `forceFit: true`
   * 一次只能選取一行：
      `singleSelect:true`

#### 範例2:參考搜索網格{#example-reference-search-grid}

安裝軟體包時，**Grid Overview**&#x200B;元件的`content.jsp`將顯示基於靜態資料的網格。 可以修改元件以顯示具有以下特徵的網格：

* 有三欄。
* 基於通過調用servlet從儲存庫檢索到的資料。
* 可編輯最後一列的儲存格。 值保存在由第一列中顯示的路徑所定義的節點下的`test`屬性中。

如前一節所述，窗口對象通過調用`defaultgrid.js`檔案`/apps/extjstraining/components/gridoverview/defaultgrid.js`中定義的`getGridPanel()`方法來獲取其` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`對象。 **格線概述**元件為`getGridPanel()`方法提供了不同的實現，該方法在`referencesearch.js`檔案中定義於`/apps/extjstraining/components/gridoverview/referencesearch.js`。 切換元件jsp中引用的。js檔案後，網格將基於從儲存庫中檢索的資料。

切換元件jsp中引用的。js檔案：

1. 在&#x200B;**CRXDE Lite**&#x200B;中，在元件的`content.jsp`檔案中，對包含`defaultgrid.js`檔案的行加上註解，使其如下所示：
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. 從包含`referencesearch.js`檔案的行中刪除注釋，使其如下所示：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. 儲存變更。
1. 重新整理範例頁面。

元件顯示如下：

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

元件jsp(`referencesearch.js`)中引用的javascript代碼定義了從元件jsp調用的`getGridPanel()`方法，並基於從儲存庫動態檢索的資料返回` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`對象。 `referencesearch.js`中的邏輯將一些動態資料定義為GridPanel的基礎：

* `reader` 是讀取 ` [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`3欄json格式之servlet回應的物件。
* `cm` 是3 ` [CQ.Ext.grid.ColumnModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` 欄的物件。「測試」欄儲存格可依使用編輯器定義的方式加以編輯：
   `editor: new [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* 這些列是可排序的：
   `cm.defaultSortable = true;`
* `store` 是對 ` [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` 像：
   * 它通過調用註冊於&quot; `/bin/querybuilder.json`&quot;的servlet來獲取其資料，其中有一些參數用於過濾查詢
   * 它以`reader`為基礎，預先定義
   * 表按照「**jcr:path**」列的升序排序
* `gridPanel` 是可 ` [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` 以編輯的對象：
   * 它基於預定義的`store`和列模型`cm`
   * 一次只能選取一行：
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * `afteredit`偵聽器確保在&quot;**Test**&quot;列中的單元格被編輯後：
      * 在儲存庫中設定由「**jcr:path**」列定義的路徑上節點的屬性「 `test`」，其值為單元格
      * 如果POST成功，則該值將添加到`store`對象中，否則將被拒絕
