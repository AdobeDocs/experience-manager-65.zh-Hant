---
title: 使用和擴充Widget（傳統UI）
seo-title: 使用和擴充Widget（傳統UI）
description: AEM網頁型介面使用AJAX和其他現代瀏覽器技術，讓作者直接在網頁上編輯和格式化內容
seo-description: AEM網頁型介面使用AJAX和其他現代瀏覽器技術，讓作者直接在網頁上編輯和格式化內容
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
source-wordcount: '4965'
ht-degree: 0%

---

# 使用和擴展Widget（傳統UI）{#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>本頁面說明傳統UI中Widget的使用方式，該UI已於AEM 6.4中淘汰。
>
>Adobe建議您根據[Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)和[Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components)運用現代化的[觸控式UI](/help/sites-developing/touch-ui-concepts.md)。

Adobe Experience Manager的網頁型介面使用AJAX和其他現代瀏覽器技術，讓作者直接在網頁上編輯和格式化內容。

Adobe Experience Manager(AEM)使用[ExtJS](https://www.sencha.com/) Widget程式庫，提供精良的使用者介面元素，可在所有最重要的瀏覽器上運作，並可建立案頭級UI體驗。

這些Widget包含在AEM中，除了供AEM本身使用外，也可供使用AEM建立的任何網站使用。

如需AEM中所有可用小工具的完整參考，請參閱[小工具集API檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)或現有xtypes](/help/sites-developing/xtypes.md)清單。 [此外，在[Sencha](https://www.sencha.com/products/extjs/examples/)網站（該架構的擁有者）上也提供許多顯示如何使用ExtJS架構的範例。

本頁面提供如何使用和擴充Widget的相關分析。 它首先說明如何在頁面](#including-the-client-sided-code-in-a-page)中包含用戶端代碼。 [接著，它會說明已建立的一些範例元件，以說明一些基本用途和擴充功能。 這些元件可在&#x200B;**封裝共用**&#x200B;的&#x200B;**使用ExtJS Widget**&#x200B;封裝中使用。

套件包含下列範例：

* [使](#basic-dialogs) 用現成可用的小工具建立基本對話方塊。
* [使](#dynamic-dialogs) 用現成可用的Widget和自訂的JavaScript邏輯建立動態對話方塊。
* 以[自訂Widget](#custom-widgets)為基礎的對話方塊。
* [樹面板](#tree-overview)在給定路徑下顯示JCR樹。
* [網格面板](#grid-overview)以表格格式顯示資料。

>[!NOTE]
>
>Adobe Experience Manager的傳統UI是以[ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/)為基礎而建置。

## 在{#including-the-client-sided-code-in-a-page}頁面中包含用戶端代碼

客戶端javascript和樣式表代碼應放置在客戶端庫中。

要建立客戶端庫：

1. 使用以下屬性在`/apps/<project>`下建立節點：

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. 在`clientlib`下建立`css`和`js`資料夾(nt:folder)。

1. 在`clientlib`下建立`css.txt`和`js.txt`檔案(nt:files)。 這些.txt檔案會列出程式庫中包含的檔案。

1. 編輯`js.txt`:它需要從「`#base=js`」開始，後面接著CQ用戶端程式庫服務要匯總的檔案清單，例如：

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. 編輯`css.txt`:它需要從「`#base=css`」開始，後面接著CQ用戶端程式庫服務要匯總的檔案清單，例如：

   ```
   #base=css
    components.css
   ```

1. 在`js`資料夾下方，放置屬於程式庫的javascript檔案。

1. 在`css`資料夾下方，放置`.css`檔案和CSS檔案使用的資源(例如`my_icon.png`)。

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

如需詳細資訊，請參閱[&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib)標籤的說明。

在某些情況下，用戶端程式庫應僅能以製作模式使用，且應以發佈模式排除。 具體實現如下：

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### 範例{#getting-started-with-the-samples}快速入門

若要遵循本頁的教學課程，請在本機AEM例項中安裝名為&#x200B;**使用ExtJS Widget**&#x200B;的套件，並建立將包含元件的範例頁面。 若要這麼做：

1. 在您的AEM例項中，從Package Share下載名為&#x200B;**Using ExtJS Widget(v01)**&#x200B;的套件並安裝該套件。 它會在存放庫的`/apps`下建立專案`extjstraining`。
1. 將包含指令碼(js)和樣式表(css)的客戶端庫包括在geometrixx頁jsp的head標籤中，因為將示例元件包含在&#x200B;**Geometrixx**分支的新頁中：
在**CRXDE Lite**&#x200B;中，開啟檔案`/apps/geometrixx/components/page/headlibs.jsp`並將`cq.extjstraining`類別新增至現有的`<ui:includeClientLib>`標籤，如下所示：
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. 在`/content/geometrixx/en/products`下方的&#x200B;**Geometrixx**&#x200B;分支中建立新頁面，並呼叫它&#x200B;**使用ExtJS介面工具集**。
1. 進入設計模式，將名為&#x200B;**Using ExtJS Widgets**&#x200B;的組的所有元件添加到Geometrixx設計中
1. 在編輯模式中返回：組&#x200B;**使用ExtJS Widget**&#x200B;的元件可在Sidekick中使用。

>[!NOTE]
>
>本頁的範例以Geometrixx範例內容為基礎，這些內容已由We.Retail取代，不再隨AEM提供。 有關如何下載和安裝Geometrixx，請參閱文檔[We.Retail Reference Implementation](/help/sites-developing/we-retail.md#we-retail-geometrixx)。

### 基本對話框{#basic-dialogs}

對話方塊通常用於編輯內容，但也只能顯示資訊。 檢視完整對話方塊的簡單方式，是存取其json格式的表示法。 若要這麼做，請將瀏覽器指向：

`https://localhost:4502/<path-to-dialog>.-1.json`

Sidekick中&#x200B;**使用ExtJS Widget**&#x200B;組的第一個元件稱為&#x200B;**1。 Dialog Basics**，包含四個基本對話方塊，這些對話方塊是使用現成可用的Widget建置，而不使用自訂的Javascript邏輯。 對話框儲存在`/apps/extjstraining/components/dialogbasics`下。 基本對話方塊為：

* 完整對話框（`full`節點）:它顯示一個包含3個頁簽的窗口，每個頁簽都包含2個文本欄位。
* 「單面板」對話框（`singlepanel`節點）:它會顯示一個包含1個標籤的視窗，其中包含2個文字欄位。
* 多面板對話框（`multipanel`節點）:其顯示與「完整」對話方塊相同，但建置方式不同。
* 設計對話框（`design`節點）:它顯示一個包含2個頁簽的窗口。 第一個頁簽具有文本欄位、下拉菜單和可折疊的文本區域。 第二個頁簽具有一個欄位集，其中包含4個文本欄位，另一個可折疊欄位集，其中包含2個文本欄位。

納入&#x200B;**1。 範例頁面中的Dialog Basics**&#x200B;元件：

1. 新增&#x200B;**1。 從** Sidekick **的「使用ExtJS Widget**」標籤，將Dialog Basics **元件導向至範例頁面。**
1. 元件顯示標題、部分文本和&#x200B;**PROPERTIES**&#x200B;連結：按一下連結以顯示儲存庫中儲存的段落的屬性。 再按一下連結以隱藏屬性。

元件顯示如下：

![chlimage_1-60](assets/chlimage_1-60.png)

#### 範例1:完整對話框{#example-full-dialog}

**Full**&#x200B;對話框顯示一個窗口，其中包含三個頁簽，每個頁簽都包含兩個文本欄位。 這是&#x200B;**Dialog Basics**&#x200B;元件的預設對話框。 其特點是：

* 由節點定義：節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`。
* 顯示3個頁簽（節點類型= `cq:Panel`）。
* 每個索引標籤都有2個文字欄位（節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/full`
* 會以JSON格式呈現，方法是要求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

對話方塊顯示如下：

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 範例2:單面板對話框{#example-single-panel-dialog}

**單面板**&#x200B;對話框顯示一個窗口，其中一個頁簽包含兩個文本欄位。 其特點是：

* 顯示1個頁簽（節點類型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）
* 索引標籤有2個文字欄位（節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* 與&#x200B;**完整對話**&#x200B;相比，優勢之一在於需要的配置較少。
* 建議使用：顯示資訊或只有幾個欄位的簡單對話框。

若要使用「單一面板」對話方塊：

1. 將&#x200B;**Dialog Basics**&#x200B;元件的對話框替換為&#x200B;**Single Panel**&#x200B;對話框：
   1. 在&#x200B;**CRXDE Lite**&#x200B;中，刪除節點：`/apps/extjstraining/components/dialogbasics/dialog`
   1. 按一下「**全部保存」以保存更改。**
   1. 複製節點：`/apps/extjstraining/components/dialogbasics/singlepanel`
   1. 將複製的節點貼到下方：`/apps/extjstraining/components/dialogbasics`
   1. 選取節點：`/apps/extjstraining/components/dialogbasics/Copy of singlepanel`並將其重新命名為`dialog`。
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 範例3:多面板對話框{#example-multi-panel-dialog}

**多面板**&#x200B;對話方塊的顯示與&#x200B;**完整**&#x200B;對話方塊的顯示相同，但建置方式不同。 其特點是：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）。
* 顯示3個頁簽（節點類型= `cq:Panel`）。
* 每個索引標籤都有2個文字欄位（節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/multipanel`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* 與&#x200B;**完整對話**&#x200B;相比，優勢之一在於它具有簡化的結構。
* 建議使用：對話框。

要使用「多面板」對話框，請執行以下操作：

1. 將&#x200B;**Dialog Basics**&#x200B;元件的對話框替換為&#x200B;**Multi Panel**對話框：
請依照[範例2所述的步驟操作：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 範例4:富對話框{#example-rich-dialog}

**Rich**&#x200B;對話框顯示一個帶有兩個頁簽的窗口。 第一個頁簽具有文本欄位、下拉菜單和可折疊的文本區域。 第二個頁簽有一個欄位集，包含四個文本欄位，一個可折疊欄位集包含兩個文本欄位。 其特點是：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示2個頁簽（節點類型= `cq:Panel`）。
* 第一個頁簽具有` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`介面工具集（具有` [textfield](/help/sites-developing/xtypes.md#textfield)`）和` [selection](/help/sites-developing/xtypes.md#selection)`介面工具集（具有3個選項），以及具有` [textarea](/help/sites-developing/xtypes.md#textarea)`介面工具集的可折疊` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`。
* 第二個頁簽具有帶4個` [textfield](/help/sites-developing/xtypes.md#textfield)`小工具的` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`小工具，以及帶2個` [textfield](/help/sites-developing/xtypes.md#textfield)`小工具的可折疊`dialogfieldset`。
* 由節點定義：
   `/apps/extjstraining/components/dialogbasics/rich`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

要使用&#x200B;**Rich**&#x200B;對話框，請執行以下操作：

1. 將&#x200B;**Dialog Basics**&#x200B;元件的對話框替換為&#x200B;**Rich**對話框：
請依照[範例2所述的步驟操作：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at50429](assets/screen_shot_2012-01-31at50429pm.png) ![pmscreen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### 動態對話框{#dynamic-dialogs}

Sidekick中&#x200B;**使用ExtJS Widget**&#x200B;組的第二個元件稱為&#x200B;**2。 動態對話框**，包括三個使用現成小工具構建的動態對話框，以及使用自定義javascript邏輯&#x200B;**構建的**。 對話框儲存在`/apps/extjstraining/components/dynamicdialogs`下。 動態對話方塊為：

* 「交換機頁簽」對話框（`switchtabs`節點）:它會顯示一個包含兩個索引標籤的視窗。 第一個索引標籤有一個選項選項，包含三個選項：選取選項時，會顯示與選項相關的索引標籤。 第二個索引標籤有兩個文字欄位。
* 任意對話框（`arbitrary`節點）:它會顯示一個包含一個索引標籤的視窗。 索引標籤有一個欄位，可拖放或上傳資產，以及一個欄位，可顯示容納頁面和資產的相關資訊（如果參考了該頁面）。
* 切換欄位對話框（`togglefield`節點）:它會顯示一個包含一個索引標籤的視窗。 索引標籤中有核取方塊：勾選此欄位時，會顯示包含兩個文字欄位的欄位集。

納入&#x200B;**2。 範例頁面上的動態對話方塊**&#x200B;元件：

1. 新增&#x200B;**2。 從** Sidekick **的「使用ExtJS Widget**」標籤中&#x200B;**使用ExtJS Widget範例頁面的動態對話**&#x200B;元件。
1. 元件顯示標題、部分文本和&#x200B;**PROPERTIES**&#x200B;連結：按一下以顯示儲存庫中儲存的段落的屬性。 再按一下以隱藏屬性。

元件顯示如下：

![chlimage_1-61](assets/chlimage_1-61.png)

#### 範例1:切換頁簽對話框{#example-switch-tabs-dialog}

**交換機頁簽**&#x200B;對話框顯示一個帶有兩個頁簽的窗口。 第一個索引標籤有一個選項選項，包含三個選項：選取選項時，會顯示與選項相關的索引標籤。 第二個索引標籤有兩個文字欄位。

其主要特點是：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示2個頁簽（節點類型= `cq:Panel`）:1選擇頁簽，第2個頁簽取決於第1個頁簽（3個選項）中的選擇。
* 有3個可選頁簽（節點類型= `cq:Panel`），每個頁簽都有2個文本欄位（節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。 一次只會顯示一個選用索引標籤。
* 由`switchtabs`節點在下列位置定義：
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

此邏輯是透過事件接聽程式和Javascript程式碼來實作，如下所示：

* 對話框節點具有「 `beforeshow`」監聽器，該監聽器在顯示對話框之前隱藏所有可選頁簽：
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`

   `dialog.items.get(0)` 獲取包含「選擇」面板和3個可選面板的表。
* `Ejst.x2`物件定義於`exercises.js`檔案中：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在`Ejst.x2.manageTabs()`方法中，由於`index`的值為–1，所有可選頁簽都隱藏（從1到3）。
* 選擇頁簽有2個偵聽器：一個在載入對話框時顯示選定頁簽(&quot; `loadcontent`&quot; event)，另一個在更改選擇時顯示選定頁簽(&quot; `selectionchanged`&quot; event):
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* 在`Ejst.x2.showTab()`方法中：
   `field.findParentByType('tabpanel')` 獲取包含所有頁簽的表格面板( `field` 表示選取介面工具集)
   `field.getValue()` 獲取選取項的值，例如：tab2
   `Ejst.x2.manageTabs()` 顯示所選頁簽。
* 每個可選頁簽都有一個監聽器，它隱藏「 `render`」事件上的頁簽：
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* 在`Ejst.x2.hideTab()`方法中：
   `tabPanel` 是包含所有標籤的表格面板
   `index` 是可選頁簽的索引
   `tabPanel.hideTabStripItem(index)` 隱藏索引標籤

其顯示如下：

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 範例2:任意對話框{#example-arbitrary-dialog}

對話方塊通常會顯示基礎元件的內容。 此處描述的對話方塊（稱為&#x200B;**Anvertial**&#x200B;對話框）從不同元件提取內容。

**任意**&#x200B;對話框顯示一個帶有一個頁簽的窗口。 索引標籤有兩個欄位：一個用於拖放或上傳資產，一個用於顯示容納頁面和資產的相關資訊（若已參考）。

其主要特點是：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示1個面板構件（節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`），其中1個面板（節點類型= `cq:Panel`）
* 該面板具有智慧檔案介面工具集（節點類型= `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`）和所有權繪圖介面工具集（節點類型= `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`）
* 由`arbitrary`節點在下列位置定義：
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

此邏輯是透過事件接聽程式和Javascript程式碼來實作，如下所示：

* ownerdraw widget具有「 `loadcontent`」監聽器，該監聽器顯示包含元件的頁面資訊以及載入內容時智慧檔案widget引用的資產：
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`

   `field` 是使用ownerdraw對象設定的
   `path` 是以元件的內容路徑設定(例如：/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs)
* `Ejst.x2`物件定義於`exercises.js`檔案中：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在`Ejst.x2.showInfo()`方法中：
   `pagePath` 是包含元件的頁面路徑
   `pageInfo` 以json格式代表頁面屬性
   `reference` 是參考資產的路徑
   `metadata` 以json格式表示資產的中繼資料
   `ownerdraw.getEl().update(html);` 在對話方塊中顯示已建立的html

要使用&#x200B;**任意**&#x200B;對話框，請執行以下操作：

1. 將&#x200B;**動態對話框**&#x200B;元件的對話框替換為&#x200B;**任意**對話框：
請依照[範例2所述的步驟操作：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 範例3:切換欄位對話框{#example-toggle-fields-dialog}

**切換欄位**&#x200B;對話框顯示一個帶有一個頁簽的窗口。 索引標籤中有核取方塊：勾選此欄位時，會顯示包含兩個文字欄位的欄位集。

其主要特點是：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示1個面板構件（節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`），其中1個面板（節點類型= `cq:Panel`）。
* 該面板具有一個選擇/複選框構件（節點類型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`，類型= ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`）和一個可折疊的對話框欄位集構件（節點類型= `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`），預設情況下隱藏，其中包含2個文本欄位構件（節點類型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由`togglefields`節點在下列位置定義：
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

此邏輯是透過事件接聽程式和Javascript程式碼來實作，如下所示：

* 「選擇」頁簽有2個監聽器：一個顯示載入內容時的dialogfieldset(&quot; `loadcontent`&quot; event)，另一個顯示更改選擇時的dialogfieldset(&quot; `selectionchanged`&quot; event):
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* `Ejst.x2`物件定義於`exercises.js`檔案中：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在`Ejst.x2.toggleFieldSet()`方法中：
   `box` 是選取物件
   `panel` 是包含選取項目和dialogfieldset小工具的面板
   `fieldSet` 是dialogfieldset對象
   `show` 是根據「 」選取的值（true或false）, `show`則顯示或不顯示對話欄位集

要使用&#x200B;**切換欄位**&#x200B;對話框，請執行以下操作：

1. 使用&#x200B;**切換欄位**&#x200B;對話框替換&#x200B;**動態對話框**元件的對話框：
請依照[範例2所述的步驟操作：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### 自定義小部件{#custom-widgets}

AEM隨附的現成可用Widget應涵蓋大部分使用案例。 不過，有時可能需要建立自訂Widget，以滿足專案特定需求。 可通過擴展現有小部件來建立自定義小部件。 為協助您開始進行此類自訂，**使用ExtJS介面工具集**&#x200B;套件包含三個對話方塊，分別使用三個不同的自訂介面工具集：

* 「多欄位」對話框（`multifield`節點）顯示一個帶有一個頁簽的窗口。 索引標籤具有自訂的多欄位介面工具集，其中包含兩個欄位：一個下拉式功能表，其中包含兩個選項和一個文字欄位。 由於它以現成可用的`multifield`介面工具集（僅包含文字欄位）為基礎，因此它具有`multifield`介面工具集的所有功能。
* 「樹瀏覽」對話框（`treebrowse`節點）顯示一個窗口，其中一個頁簽包含路徑瀏覽介面工具集：按一下箭頭時，會向上開啟一個窗口，您可以在其中瀏覽層次並選擇項目。 然後，項目的路徑會新增至路徑欄位，並在對話方塊關閉時持續保存。
* RTF編輯器外掛程式對話方塊（`rteplugin`節點）會新增自訂按鈕至RTF編輯器，以將一些自訂文字插入主要文字。 它包含`richtext`介面工具集(RTE)和透過RTE外掛程式機制新增的自訂功能。

自訂Widget和外掛程式包含在名為&#x200B;**3的元件中。**&#x200B;使用ExtJS Widget **套件的自訂Widget**。 若要將此元件包含至範例頁面：

1. 新增&#x200B;**3。 從** Sidekick **的「使用ExtJS Widget**」標籤的&#x200B;**使用ExtJS Widget**&#x200B;元件到範例頁面。
1. 元件顯示標題和一些文本，並在按一下&#x200B;**PROPERTIES**連結時，顯示儲存在儲存庫中的段落的屬性。 再按一下會隱藏屬性。
元件顯示如下：

![chlimage_1-62](assets/chlimage_1-62.png)

#### 範例1:自訂多欄位介面工具集{#example-custom-multifield-widget}

**自訂多欄位**&#x200B;介面工具集對話方塊會顯示一個含有一個索引標籤的視窗。 索引標籤具有自訂的多欄位介面工具集，與具有一個欄位的標準介面工具集不同，它有兩個欄位：一個下拉式功能表，其中包含兩個選項和一個文字欄位。

**自訂多欄位**&#x200B;介面工具集對話方塊：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示1個包含面板（節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）的表板Widget（節點類型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* 此面板具有`multifield`介面工具集（節點類型= `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`）。
* `multifield`介面工具集的欄位配置（節點類型= `nt:unstructured`, xtype = `ejstcustom`,optionsProvider = `Ejst.x3.provideOptions`）是以自訂xtype &#39; `ejstcustom`&#39;為基礎：
   * 「 `fieldconfig`」是` [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)`對象的配置選項。
   * 「 `optionsProvider`」是`ejstcustom`介面工具集的配置。 它以`Ejst.x3.provideOptions`方法設定，該方法在`exercises.js`中定義：
      `/apps/extjstraining/clientlib/js/exercises.js`
和會傳回2個選項。
* 由`multifield`節點在下列位置定義：
   `/apps/extjstraining/components/customwidgets/multifield`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

自訂多欄位介面工具集(xtype = `ejstcustom`):

* 是名為`Ejst.CustomWidget`的Javascript物件。
* 在`CustomWidget.js` javascript檔案中定義：
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* 延伸` [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)`介面工具集。
* 有3個欄位：`hiddenField`（文本欄位）、`allowField`(ComboBox)和`otherField`（文本欄位）
* 覆蓋`CQ.Ext.Component#initComponent`以添加3個欄位：
   * `allowField` 是CQ. [form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) 「selectionobject」類型的。optionsProvider是Selection對象的配置，在對話框中定義的CustomWidget的optionsProvider配置已實例化
   * `otherField` 是 [CQ.Ext.form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) TextFieldobject
* 覆寫[CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)的方法`setValue`、`getValue`和`getRawValue`，以便以下格式設定和檢索CustomWidget的值：
   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`。
* 註冊為「 `ejstcustom`」xtype:
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

**自訂多欄位**&#x200B;介面工具集對話方塊顯示如下：

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 範例2:自訂樹狀瀏覽介面工具集{#example-custom-treebrowse-widget}

基於自定義&#x200B;**樹狀瀏覽**&#x200B;介面工具集的對話框顯示一個窗口，其中一個頁簽包含自定義路徑瀏覽介面工具集：按一下箭頭時，會向上開啟一個窗口，您可以在其中瀏覽層次並選擇項目。 然後，項目的路徑會新增至路徑欄位，並在對話方塊關閉時持續保存。

自定義樹瀏覽對話框：

* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示1個包含面板（節點類型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）的表板Widget（節點類型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* 面板具有自訂Widget（節點類型= `cq:Widget`, xtype = `ejstbrowse`）
* 由`treebrowse`節點在下列位置定義：
   `/apps/extjstraining/components/customwidgets/treebrowse`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

自訂樹狀瀏覽介面工具集(xtype = `ejstbrowse`):

* 是名為`Ejst.CustomWidget`的Javascript物件。
* 在`CustomBrowseField.js` javascript檔案中定義：
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* 擴展` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`。
* 定義名為`browseWindow`的瀏覽窗口。
* 覆蓋` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick`以在按一下箭頭時顯示瀏覽窗口。
* 定義[CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)物件：
   * 它通過調用在`/bin/wcm/siteadmin/tree.json`註冊的servlet來獲取其資料。
   * 其根為&quot; `apps/extjstraining`&quot;。
* 定義`window`對象(` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`):
   * 根據預先定義的面板。
   * 具有&#x200B;**OK**&#x200B;按鈕，該按鈕設定選定路徑的值並隱藏面板。
* 窗口錨定在&#x200B;**Path**&#x200B;欄位下。
* 所選路徑將從瀏覽欄位傳遞到`show`事件上的窗口。
* 註冊為「 `ejstbrowse`」xtype:
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

要使用基於&#x200B;**自定義樹瀏覽**&#x200B;介面工具集的對話框，請執行以下操作：

1. 將&#x200B;**自訂介面工具集**&#x200B;元件的對話框替換為&#x200B;**自訂樹瀏覽**對話框：
請依照[範例2所述的步驟操作：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 範例3:RTF編輯器(RTE)外掛程式{#example-rich-text-editor-rte-plug-in}

以&#x200B;**RTF編輯器(RTE)外掛程式**&#x200B;為基礎的對話方塊是以RTF編輯器為基礎的對話方塊，其中具有自訂按鈕，可在方括弧內插入某些自訂文字。 自訂文字可由某些伺服器端邏輯剖析（此範例中未實作），例如新增在指定路徑上定義的一些文字：

基於&#x200B;**RTE插件**&#x200B;的對話框：

* 由rtplugin節點定義：
   `/apps/extjstraining/components/customwidgets/rteplugin`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* `rtePlugins`節點具有以插件命名的子節點`inserttext`（節點類型= `nt:unstructured`）。 它有一個名為`features`的屬性，該屬性定義哪些外掛程式功能可用於RTE。

RTE外掛程式：

* 是名為`Ejst.InsertTextPlugin`的Javascript物件。
* 在`InsertTextPlugin.js` javascript檔案中定義：
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* 擴展` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`對象。
* 下列方法定義` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`物件，並在實作外掛程式中覆寫：
   * `getFeatures()` 會傳回外掛程式可用之所有功能的陣列。
   * `initializeUI()` 將新按鈕添加到RTE工具欄。
   * `notifyPluginConfig()` 當按鈕暫留時顯示標題和文字。
   * `execute()` 按一下按鈕並執行外掛程式動作時，會呼叫：它顯示一個窗口，用於定義要包括的文本。
* `insertText()` 使用對應的對話框對象插入文 `Ejst.InsertTextPlugin.Dialog` 本（請參閱之後）。
* `executeInsertText()` 會由對話方 `apply()` 塊的方法呼叫，按一下「確定」按鈕時 **** 就會觸發。
* 將自身註冊為「 `inserttext`」插件：
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* `Ejst.InsertTextPlugin.Dialog`物件定義按一下外掛程式按鈕時開啟的對話方塊。 對話框由面板、表單、文本欄位和2個按鈕（**OK**&#x200B;和&#x200B;**Cancel**）組成。

要使用基於&#x200B;**RTF編輯器(RTE)插件**&#x200B;的對話框，請執行以下操作：

1. 使用&#x200B;**RTF編輯器(RTE)插件**&#x200B;基於對話框的&#x200B;**自定義Widget**元件的對話框替換：
請依照[範例2所述的步驟操作：單一面板對話方塊](#example-single-panel-dialog)
1. 編輯元件。
1. 按一下右側的最後一個圖示（四個箭頭的圖示）。 輸入路徑，然後按一下&#x200B;**OK**:
路徑會顯示在方括弧內([ ])。
1. 按一下&#x200B;**OK**&#x200B;以關閉RTF編輯器。

**RTF編輯器(RTE)外掛程式**&#x200B;對話方塊顯示如下：

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>此範例僅顯示如何實作邏輯的用戶端部分：然後，必須在伺服器端明確剖析預留位置(*[text]*)（例如在元件JSP中）。

### 樹概覽{#tree-overview}

現成可用的` [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)`物件提供樹狀結構資料的樹狀結構UI表示法。 **使用ExtJS Widget**&#x200B;套件中包含的樹概覽元件顯示如何使用`TreePanel`物件在指定路徑下顯示JCR樹。 窗口本身可以停靠/取消停靠。 在此示例中，窗口邏輯嵌入到&lt;script>&lt;/script>標籤之間的元件jsp中。

要將&#x200B;**樹概述**&#x200B;元件包含到示例頁：

1. 新增&#x200B;**4。 從** Sidekick **中的**&#x200B;使用ExtJS Widget **標籤到範例頁面的樹狀結構概述**&#x200B;元件。
1. 元件隨即顯示：
   * 標題，帶有文字
   * a **PROPERTIES**&#x200B;連結：按一下以顯示儲存庫中儲存的段落的屬性。 再按一下以隱藏屬性。
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

* 通過嘗試從頁中檢索樹窗口來定義`tree`對象。
* 如果顯示樹的窗口不存在，則會建立`treePanel`([CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)):
   * `treePanel` 包含用於建立視窗的資料。
   * 通過調用在註冊的servlet來檢索資料：
      `/bin/wcm/siteadmin/tree.json`
* `beforeload`監聽程式確保已載入點擊的節點。
* `root`對象將路徑`apps/extjstraining`設定為樹根。
* `tree` ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`)是根據預先定義而設 `treePanel`定，並顯示為：
   `tree.show();`
* 如果窗口已存在，則根據從儲存庫檢索到的寬度、高度和停靠屬性顯示該窗口。

元件對話方塊：

* 顯示1個頁簽，其中包含2個欄位，用於設定樹概覽窗口的大小（寬度和高度），以及1個欄位用於固定/取消固定窗口
* 由節點定義（節點類型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* 此面板具有大小欄位構件（節點類型= `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`）和選擇構件（節點類型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = `radio`），其中包含2個選項(true/false)
* 由對話方塊節點在下列位置定義：
   `/apps/extjstraining/components/treeoverview/dialog`
* 會透過要求：
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* 顯示如下：

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### 網格概述{#grid-overview}

「網格面板」以行和列的表格格式表示資料。 由下列部分組成：

* 商店：保存資料記錄（列）的模型。
* 欄模型：柱子的組成。
* 檢視：封裝用戶介面。
* 選取模型：選取行為。

**使用ExtJS Widget**&#x200B;套件中包含的格線概述元件顯示如何以表格格式顯示資料：

* 範例1使用靜態資料。
* 範例2使用從存放庫擷取的資料。

要將「網格概述」元件包含到示例頁，請執行以下操作：

1. 新增&#x200B;**5。 從** Sidekick **中的**&#x200B;使用ExtJS Widget **標籤到範例頁面的格線概述**&#x200B;元件。
1. 元件隨即顯示：
   * 帶有文本的標題
   * a **PROPERTIES**&#x200B;連結：按一下以顯示儲存庫中儲存的段落的屬性。 再按一下以隱藏屬性。
   * 包含表格格式的資料的浮動視窗。

元件顯示如下：

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 範例1:預設網格{#example-default-grid}

在其現成版本中，**格線概述**&#x200B;元件以表格格式顯示一個包含靜態資料的窗口。 在此示例中，邏輯通過兩種方式嵌入到元件jsp中：

* 在&lt;script>&lt;/script>標籤之間定義一般邏輯
* 特定邏輯可在單獨的.js檔案中使用，並在jsp中連結到。 此設定可借由註解所需的&lt;script>標籤，輕鬆在兩個邏輯（靜態/動態）之間切換。

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

* 通過嘗試從頁中檢索窗口元件來定義`grid`對象：
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* 如果`grid`不存在，則通過調用`getGridPanel()`方法來定義[CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)對象(`gridPanel`)（請參見下面）。 此方法在`defaultgrid.js`中定義。
* `grid` 是以 ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)` 預先定義的GridPanel為基礎的物件，且會顯示：  `grid.show();`
* 如果`grid`已存在，則根據從儲存庫檢索到的寬度、高度和停靠屬性來顯示它。

元件jsp中引用的javascript檔案(`defaultgrid.js`)定義了由嵌入JSP中的指令碼調用的`getGridPanel()`方法，並基於靜態資料返回` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`對象。 邏輯如下：

* `myData` 是靜態資料的陣列，格式為5欄4列的表格。
* `store` 是耗 `CQ.Ext.data.Store` 用的物 `myData`件。
* `store` 已載入記憶體中：
   `store.load();`
* `gridPanel` 是會 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 使用的物件 `store`:
   * 欄寬隨時會重新比例：
      `forceFit: true`
   * 一次只能選取一列：
      `singleSelect:true`

#### 範例2:參考搜索網格{#example-reference-search-grid}

安裝軟體包時，**網格概述**&#x200B;元件的`content.jsp`將顯示基於靜態資料的網格。 可以修改元件以顯示具有以下特徵的網格：

* 有三欄。
* 是以呼叫Servlet從存放庫擷取的資料為基礎。
* 可以編輯最後一列的儲存格。 值會保存在`test`屬性中，位於由第一欄中顯示的路徑所定義的節點下方。

如前一節所述，窗口對象通過調用`defaultgrid.js`檔案中`/apps/extjstraining/components/gridoverview/defaultgrid.js`中定義的`getGridPanel()`方法來獲取其` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`對象。 **Grid Overview **元件為`getGridPanel()`方法提供了不同的實現，該方法在`referencesearch.js`檔案中定義，位於`/apps/extjstraining/components/gridoverview/referencesearch.js`。 切換元件jsp中參考的.js檔案後，網格將以從儲存庫擷取的資料為基礎。

切換元件jsp中引用的.js檔案：

1. 在元件的&#x200B;**CRXDE Lite**&#x200B;檔案的`content.jsp`檔案中，注釋包含`defaultgrid.js`檔案的行，使其如下所示：
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. 從包含`referencesearch.js`檔案的行中移除註解，使其如下所示：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. 儲存變更。
1. 重新整理範例頁面。

元件顯示如下：

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

元件jsp(`referencesearch.js`)中引用的javascript代碼定義了從元件jsp調用的`getGridPanel()`方法，並根據從儲存庫動態檢索的資料返回` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`對象。 `referencesearch.js`中的邏輯將某些動態資料定義為GridPanel的基礎：

* `reader` 是物 ` [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`件，可讀取3欄json格式的servlet回應。
* `cm` 是3 ` [CQ.Ext.grid.ColumnModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` 欄的物件。「測試」欄儲存格可依使用編輯器定義的方式加以編輯：
   `editor: new [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* 欄可排序：
   `cm.defaultSortable = true;`
* `store` 是物 ` [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` 件：
   * 它會呼叫註冊於&quot; `/bin/querybuilder.json`&quot;的servlet，並使用一些用於篩選查詢的參數來取得其資料
   * 它以`reader`為基礎，預先定義
   * 表按「**jcr:path**」列的升序排序
* `gridPanel` 是可 ` [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` 編輯的物件：
   * 它以預定義的`store`和列模型`cm`為基礎
   * 一次只能選取一列：
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * `afteredit`接聽程式確保在「**Test**」欄中的儲存格已編輯後：
      * 儲存庫中設定了由「**jcr:path**」列定義的路徑上節點的屬性「 `test`」，其值為單元格
      * 如果POST成功，則值將添加到`store`對象，否則它將被拒絕
