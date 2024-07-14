---
title: 使用和擴充Widget （傳統UI）
description: Adobe Experience Manager的網頁型介面使用AJAX和其他現代瀏覽器技術，讓作者能夠透過所見即所得的方式編輯內容並將內容格式化
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '4896'
ht-degree: 0%

---

# 使用和擴充Widget （傳統UI）{#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>本頁說明傳統UI中Widget的使用方式，AEM 6.4已棄用該功能。
>
>Adobe建議您使用以[Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)和[Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components)為基礎的現代[觸控式UI](/help/sites-developing/touch-ui-concepts.md)。

Adobe Experience Manager (AEM)的網頁型介面使用AJAX和其他現代瀏覽器技術，讓作者能在網頁上以WYSIWYG方式編輯和格式化內容。

AEM使用[ExtJS](https://www.sencha.com/) Widget程式庫，此程式庫提供高度完善的使用者介面元素，可在所有最重要的瀏覽器上運作，並可建立案頭級的UI體驗。

這些Widget包含在AEM中，除了供AEM本身使用外，也可供任何使用AEM建立的網站使用。

如需AEM中所有可用Widget的完整參考，請參閱[Widget API檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)或現有xtype](/help/sites-developing/xtypes.md)的[清單。 此外，許多說明如何使用ExtJS架構的範例可在架構擁有者[Sencha](https://examples.sencha.com/extjs/7.6.0/)網站上取得。

本頁提供如何使用及擴充Widget的一些深入分析。 它首先說明如何[在頁面](#including-the-client-sided-code-in-a-page)中包含使用者端程式碼。 然後它會說明一些已建立的範例元件，以說明一些基本用途和擴充功能。 這些元件可在&#x200B;**封裝共用**&#x200B;上的&#x200B;**使用ExtJS Widget**&#x200B;封裝中使用。

此套件包含下列範例：

* [基本對話方塊](#basic-dialogs)使用現成可用的Widget建置。
* [動態對話方塊](#dynamic-dialogs)使用現成的Widget和自訂JavaScript邏輯建置。
* 以[自訂Widget](#custom-widgets)為基礎的對話方塊。
* 在指定路徑下方顯示JCR樹狀結構的[樹狀結構面板](#tree-overview)。
* 以表格格式顯示資料的[格線面板](#grid-overview)。

>[!NOTE]
>
>Adobe Experience Manager的傳統UI是以[ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/)建置。

## 在頁面中包含使用者端程式碼 {#including-the-client-sided-code-in-a-page}

使用者端的JavaScript和樣式表程式碼應放置在使用者端程式庫中。

若要建立使用者端資源庫：

1. 在`/apps/<project>`底下建立具有以下屬性的節點：

   * name=&quot;clientlib&quot;
   * jcr：mixinTypes=&quot;[mix：lockable]&quot;
   * jcr：primaryType=&quot;cq：ClientLibraryFolder&quot;
   * sling：resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;category-name>]&quot;
   * 相依性=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (for example, "cq.extjstraining") and is used to include the library on the page.`

1. 在`clientlib`底下建立`css`和`js`資料夾(nt：folder)。

1. 在`clientlib`底下建立`css.txt`和`js.txt`檔案(nt：files)。 這些.txt檔案會列出資料庫中包含的檔案。

1. 編輯`js.txt`：它必須以&#39; `#base=js`&#39;開頭，後面接著由CQ使用者端程式庫服務彙總的檔案清單，例如：

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. 編輯`css.txt`：它必須以&#39; `#base=css`&#39;開頭，後面接著由CQ使用者端程式庫服務彙總的檔案清單，例如：

   ```
   #base=css
    components.css
   ```

1. 在`js`資料夾下方，放置屬於資料庫的JavaScript檔案。

1. 在`css`資料夾下方，置入`.css`個檔案及css檔案所使用的資源（例如`my_icon.png`）。

>[!NOTE]
>
>之前說明的樣式表處理方式是選擇性的。

若要在頁面元件jsp中包含使用者端程式庫：

* 若要同時包含JavaScript程式碼和樣式表：
  `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
其中`<category-nameX>`是使用者端程式庫的名稱。

* 若只要包含JavaScript程式碼：
  `<ui:includeClientLib js="<category-name>"/>`

有關更多詳細信息，請參閱標記的說明 [&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 。&lt;/ui:includeClientLib>

有時，用戶端資料庫應該只在作者模式下可用，而在發佈模式下應該排除。 它可以按如下方式實現：

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### 使用示例快速入門 {#getting-started-with-the-samples}

若要遵循此頁面的教學課程，在本機AEM執行個體中安裝套件&#x200B;**使用ExtJS Widget**，並建立包含元件的範例頁面。 若要這麼做，請執行下列動作：

1. 在您的AEM執行個體中，從封裝共用下載名為&#x200B;**使用ExtJS Widget (v01)**&#x200B;的封裝並安裝封裝。 它在存放庫中的`/apps`下建立專案`extjstraining`。
1. 將包含指令碼(js)和樣式表(css)的使用者端資料庫包含在Geometrixx頁面jsp的head標籤中。 您即將在&#x200B;**Geometrixx**分支的新頁面中包含範例元件：
在**CRXDE Lite**&#x200B;中，開啟檔案`/apps/geometrixx/components/page/headlibs.jsp`並將`cq.extjstraining`類別新增至現有的`<ui:includeClientLib>`標籤，如下所示：
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. 在`/content/geometrixx/en/products`下方的&#x200B;**Geometrixx**&#x200B;分支中建立頁面，並使用ExtJS Widget **呼叫它**。
1. 進入設計模式，並將名為&#x200B;**使用ExtJS Widget**&#x200B;之群組的所有元件新增到Geometrixx的設計中
1. 返回編輯模式：Sidekick中提供&#x200B;**使用ExtJS Widget**&#x200B;群組的元件。

>[!NOTE]
>
>本頁範例是根據AEM不再隨附的Geometrixx範例內容，已被We.Retail取代。 請參閱[We.Retail參考實作](/help/sites-developing/we-retail.md#we-retail-geometrixx)，瞭解如何下載及安裝Geometrixx。

### 基本對話方塊 {#basic-dialogs}

對話方塊通常用於編輯內容，但也可以顯示資訊。 檢視完整對話方塊的一個簡單方法是存取其json格式的表示法。 若要這麼做，請將瀏覽器指向：

`https://localhost:4502/<path-to-dialog>.-1.json`

在Sidekick中使用ExtJS Widget **群組的**&#x200B;的第一個元件稱為&#x200B;**1。 對話方塊基本概念**&#x200B;並包含四個使用現成Widget建置且沒有自訂JavaScript邏輯的基本對話方塊。 對話方塊儲存在`/apps/extjstraining/components/dialogbasics`下方。 基本對話方塊包括：

* 完整對話方塊（ `full`節點）：它會顯示一個視窗，其中包含三個索引標籤，每個索引標籤都有兩個文字欄位。
* 單一面板對話方塊（ `singlepanel`節點）：它會顯示一個視窗，其中有一個索引標籤，其中包含兩個文字欄位。
* 多面板對話方塊（ `multipanel`節點）：其顯示與「完整」對話方塊相同，但建置方式不同。
* 設計對話方塊（ `design`節點）：它會顯示一個視窗，其中包含兩個索引標籤。 第一個標籤具有文字欄位、下拉式功能表和可摺疊的文字區域。 第二個索引標籤有一個包含四個文字欄位的欄位集，以及一個包含兩個文字欄位的可摺疊欄位集。

包含&#x200B;**1。 範例頁面中的Dialog Basics**&#x200B;元件：

1. 新增&#x200B;**1。 從** Sidekick **中的**&#x200B;使用ExtJS Widget **索引標籤，將對話方塊基本概念**&#x200B;元件新增至範例頁面。
1. 元件會顯示標題、某些文字和&#x200B;**屬性**&#x200B;連結。 選取連結會顯示儲存在存放庫中的段落屬性。 再次選取連結以隱藏屬性。

元件顯示如下：

![chlimage_1-60](assets/chlimage_1-60.png)

#### 範例1：完整對話方塊 {#example-full-dialog}

**完整**&#x200B;對話方塊會顯示一個包含三個索引標籤的視窗，每個索引標籤都有兩個文字欄位。 這是&#x200B;**對話方塊基本概念**&#x200B;元件的預設對話方塊。 其特性包括：

* 由節點定義：節點型別= `cq:Dialog`，xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`。
* 顯示三個索引標籤（節點型別= `cq:Panel`）。
* 每個索引標籤都有兩個文字欄位（節點型別= `cq:Widget`，xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由節點定義：
  `/apps/extjstraining/components/dialogbasics/full`
* 會要求以JSON格式轉譯：
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

對話方塊顯示如下：

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 範例2：單一面板對話方塊 {#example-single-panel-dialog}

**單一面板**&#x200B;對話方塊會顯示一個視窗，其中有一個索引標籤有兩個文字欄位。 其特性包括：

* 顯示一個索引標籤（節點型別= `cq:Dialog`，xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）
* 索引標籤有兩個文字欄位（節點型別= `cq:Widget`，xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）
* 由節點定義：
  `/apps/extjstraining/components/dialogbasics/singlepanel`
* 透過請求以json格式轉譯：
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* 與&#x200B;**完整對話方塊**&#x200B;相比，有一個優點就是所需的設定較少。
* 建議使用：用於顯示資訊或只有幾個欄位的簡單對話方塊。

若要使用「單一面板」對話方塊：

1. 將&#x200B;**對話方塊基本概念**&#x200B;元件的對話方塊取代為&#x200B;**單一面板**&#x200B;對話方塊：
   1. 在&#x200B;**CRXDE Lite**&#x200B;中刪除節點： `/apps/extjstraining/components/dialogbasics/dialog`
   1. 按一下[全部儲存]**儲存變更。**
   1. 複製節點： `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. 在下方貼上複製的節點： `/apps/extjstraining/components/dialogbasics`
   1. 選取節點： `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`並將其重新命名`dialog`。
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 範例3：多面板對話方塊 {#example-multi-panel-dialog}

**多重面板**&#x200B;對話方塊與&#x200B;**完整**&#x200B;對話方塊的顯示相同，但建置方式不同。 其特性包括：

* 由節點定義（節點型別= `cq:Dialog`，xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）。
* 顯示三個索引標籤（節點型別= `cq:Panel`）。
* 每個標籤都有兩個文本字段（節點類型 = `cq:Widget`， xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由以下節點定義：
  `/apps/extjstraining/components/dialogbasics/multipanel`
* 透過請求以json格式轉譯：
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* 相較於&#x200B;**完整對話方塊**，其優點之一是結構簡化。
* 建議使用：用於多索引標籤對話方塊。

若要使用「多面板」對話方塊：

1. 將&#x200B;**對話方塊基本概念**&#x200B;元件的對話方塊取代為&#x200B;**多重面板**對話方塊：
請依照[範例2：單一面板對話方塊](#example-single-panel-dialog)中說明的步驟操作
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 範例4： Rich對話方塊 {#example-rich-dialog}

**Rich**&#x200B;對話方塊會顯示包含兩個索引標籤的視窗。 第一個標籤具有文字欄位、下拉式功能表和可摺疊的文字區域。 第二個索引標籤有一個包含四個文字欄位的欄位集，以及一個包含兩個文字欄位的可摺疊欄位集。 其特性包括：

* 由節點定義（節點型別= `cq:Dialog`，xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示兩個標籤（節點型別= `cq:Panel`）。
* 第一個索引標籤具有具有` [textfield](/help/sites-developing/xtypes.md#textfield)`的` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` Widget和具有三個選項的` [selection](/help/sites-developing/xtypes.md#selection)` Widget，以及具有` [textarea](/help/sites-developing/xtypes.md#textarea)` Widget的可摺疊` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`。
* 第二個索引標籤具有包含四個` [textfield](/help/sites-developing/xtypes.md#textfield)`介面工具的` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`介面工具集，以及包含兩個` [textfield](/help/sites-developing/xtypes.md#textfield)`介面工具的可收合`dialogfieldset`。
* 由節點定義：
  `/apps/extjstraining/components/dialogbasics/rich`
* 透過請求以json格式轉譯：
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

若要使用&#x200B;**Rich**&#x200B;對話方塊：

1. 將&#x200B;**對話方塊基本資訊**&#x200B;元件的對話方塊取代為&#x200B;**Rich**對話方塊：
請依照[範例2：單一面板對話方塊](#example-single-panel-dialog)中說明的步驟操作
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### 動態對話方塊 {#dynamic-dialogs}

Sidekick中&#x200B;**使用ExtJS Widget**&#x200B;群組的第二個元件稱為&#x200B;**2。 動態對話方塊**&#x200B;並包含三個動態對話方塊，這些對話方塊是使用現成可用的Widget以及&#x200B;**使用自訂的JavaScript邏輯**&#x200B;建置。 對話方塊儲存在`/apps/extjstraining/components/dynamicdialogs`下方。 動態對話方塊包括：

* 切換標籤對話方塊（ `switchtabs`節點）：它會顯示一個包含兩個標籤的視窗。 第一個標籤具有包含三個選項的選項選擇：選取選項時，會顯示與選項相關的標籤。 第二個索引標籤有兩個文字欄位。
* 任意對話方塊（ `arbitrary`節點）：它會顯示一個含有一個索引標籤的視窗。 索引標籤含有要放置或上傳資產的欄位，以及顯示容納頁面和資產相關資訊（若有參考頁面）的欄位。
* [切換欄位]對話方塊（ `togglefield`節點）：它會顯示一個含有一個索引標籤的視窗。 索引標籤具有核取方塊：核取時，會顯示包含兩個文字欄位的欄位集。

加入&#x200B;**2。 範例頁面上的動態對話方塊**&#x200B;元件：

1. 新增&#x200B;**2。 從**&#x200B;使用&#x200B;**Sidekick**&#x200B;中的ExtJS Widget **索引標籤，將動態對話方塊**&#x200B;元件移至範例頁面。
1. 元件會顯示標題、某些文字和&#x200B;**屬性**&#x200B;連結。 選取連結會顯示儲存在存放庫中的段落屬性。 再次選取連結以隱藏屬性。

元件顯示如下：

![chlimage_1-61](assets/chlimage_1-61.png)

#### 範例1：切換索引標籤對話方塊 {#example-switch-tabs-dialog}

**切換標籤**&#x200B;對話方塊會顯示包含兩個標籤的視窗。 第一個標籤具有包含三個選項的選項選擇：選取選項時，會顯示與選項相關的標籤。 第二個索引標籤有兩個文字欄位。

其主要特性包括：

* 由節點定義（節點型別= `cq:Dialog`，xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示兩個標籤（節點型別= `cq:Panel`）：一個選項標籤，第二個標籤取決於第一個標籤中的選項（三個選項）。
* 有三個選用的索引標籤（節點型別= `cq:Panel`），每一個都有兩個文字欄位（節點型別= `cq:Widget`，xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。 一次只顯示一個可選標籤。
* 由下列位置的`switchtabs`節點定義：
  `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* 透過請求以json格式轉譯：
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

此邏輯會透過事件接聽程式和JavaScript程式碼實作，如下所示：

* 對話方塊節點有一個&quot; `beforeshow`&quot;接聽程式，會在顯示對話方塊之前隱藏所有選用的索引標籤：
  `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`
  `dialog.items.get(0)`取得包含選取範圍面板和三個選用面板的`tabpanel`。
* `Ejst.x2`物件定義於`exercises.js`檔案中，位於：
  `/apps/extjstraining/clientlib/js/exercises.js`
* 在`Ejst.x2.manageTabs()`方法中，因為`index`的值為–1，所以所有選用的索引標籤都會隱藏（i會從1變成3）。
* 選取索引標籤有兩個接聽程式：一個會在載入對話方塊時顯示選取的索引標籤（&quot; `loadcontent`&quot;事件），另一個會在選取範圍變更時顯示選取的索引標籤（&quot; `selectionchanged`&quot;事件）：
  `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* 針對`Ejst.x2.showTab()`方法，
  `field.findParentByType('tabpanel')`取得包含所有索引標籤的`tabpanel` （ `field`代表選取專案Widget）
  `field.getValue()`取得選取專案的值，例如tab2
  `Ejst.x2.manageTabs()`顯示選取的索引標籤。
* 每個選擇性標籤都有一個接聽程式，會隱藏「`render`」事件上的標籤：
  `render="function(tab){Ejst.x2.hideTab(tab);}"`
* 針對`Ejst.x2.hideTab()`方法，
  `tabPanel``tabpanel`是包含所有標籤的
  `index` 是可選標籤的索引
  `tabPanel.hideTabStripItem(index)` 隱藏標籤

它顯示如下：

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 範例2：任意對話方塊 {#example-arbitrary-dialog}

通常會有一個對話方塊顯示基礎元件的內容。 此處說明的對話方塊（稱為&#x200B;**任意**&#x200B;對話方塊）從不同的元件提取內容。

**任意**&#x200B;對話方塊會顯示有一個索引標籤的視窗。 索引標籤有兩個欄位：一個可放置或上傳資產，另一個可顯示容納頁面的一些相關資訊，另一個則會顯示資產的相關資訊（如果已參考）。

其主要特性包括：

* 由節點定義（節點型別= `cq:Dialog`，xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示具有單一面板（節點型別= `cq:Panel`）的`tabpanel` Widget （節點型別= `cq:Widget`， xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）
* 面板具有smartfile Widget （節點型別= `cq:Widget`，xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`）和ownerdraw Widget （節點型別= `cq:Widget`，xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`）
* 由下列位置的`arbitrary`節點定義：
  `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* 透過請求以json格式轉譯：
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

此邏輯會透過事件接聽程式和JavaScript程式碼實作，如下所示：

* `ownerdraw` Widget有一個&quot; `loadcontent`&quot;接聽程式，可顯示包含元件之頁面的相關資訊。 也就是說，載入內容時smartfile Widget所參考的資產：
  `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`
  `field`已設定為`ownerdraw`物件
  `path`設定為元件的內容路徑（例如，`/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs`）
* `Ejst.x2`物件定義於`exercises.js`檔案中，位於：
  `/apps/extjstraining/clientlib/js/exercises.js`
* 針對`Ejst.x2.showInfo()`方法，
  `pagePath`是包含元件的頁面的路徑；
  `pageInfo`代表json格式的頁面屬性；
  `reference`是參考資產的路徑；
  `metadata`代表json格式的資產中繼資料；
  `ownerdraw.getEl().update(html);`在對話方塊中顯示已建立的html

若要使用&#x200B;**任意**&#x200B;對話方塊：

1. 使用任何&#x200B;**對話框取代**&#x200B;動態對話框&#x200B;**元件的**對話盒：
追隨示例 2：單面板對話框中所述的步驟[](#example-single-panel-dialog)
1. 編輯元件：對話框顯示如下：

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 範例3：切換欄位對話方塊 {#example-toggle-fields-dialog}

**切換欄位**&#x200B;對話方塊會顯示有一個索引標籤的視窗。 標籤有一個複選框：選中時，將顯示包含兩個文本字段的欄位集。

其主要特點是：

* 由節點定義 （節點 type = `cq:Dialog`， xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示一個`tabpanel`帶有一個面板（節點類型 = ）的小組件（節點類型 `cq:Widget`= `cq:Panel`， xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`）。
* 該面板有一個選擇/複選框小部件（節點類型 = `cq:Widget`， xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`， type = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`） 和一個可摺疊的 dialogfieldset 小部件（節點 type = `cq:Widget`， xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`），默認情況下隱藏，有兩個文本字段小部件（節點 type = `cq:Widget`， xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由下列位置的`togglefields`節點定義：
  `/apps/extjstraining/components/dynamicdialogs/togglefields`
* 透過請求以json格式轉譯：
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

此邏輯會透過事件接聽程式和JavaScript程式碼實作，如下所示：

* 選取專案索引標籤有兩個接聽程式：一個會在內容載入時顯示dialogfieldset （&quot; `loadcontent`&quot;事件），另一個會在選取專案變更時顯示dialogfieldset （&quot; `selectionchanged`&quot;事件）：
  `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* `Ejst.x2`物件定義於`exercises.js`檔案中，位於：
  `/apps/extjstraining/clientlib/js/exercises.js`
* 針對`Ejst.x2.toggleFieldSet()`方法，
  `box`是選取範圍物件；
  `panel`是包含選取範圍和dialogfieldset Widget的面板；
  `fieldSet`是dialogfieldset物件；
  `show`是選取範圍的值（true或false）；
是否顯示dialogfieldset （根據&#39; `show`&#39;）

若要使用&#x200B;**切換欄位**&#x200B;對話方塊，請執行下列動作：

1. 將&#x200B;**動態對話方塊**&#x200B;元件的對話方塊取代為&#x200B;**切換欄位**對話方塊：
請依照[範例2：單一面板對話方塊](#example-single-panel-dialog)中說明的步驟操作
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### 自訂Widget {#custom-widgets}

AEM隨附的現成可用Widget應該涵蓋大部分的使用案例。 不過，有時可能需要建立自訂Widget來涵蓋專案的特定需求。 自訂Widget可藉由擴充現有元件來建立。 為協助您開始進行這類自訂，**`Using ExtJS Widgets`**&#x200B;套件包含三個使用三個不同自訂Widget的對話方塊：

* 多欄位對話方塊（ `multifield`節點）會顯示一個視窗，其中包含一個索引標籤。 索引標籤具有自訂的多欄位Widget，其中包含兩個欄位：包含兩個選項的下拉式功能表以及一個文字欄位。 由於是以現成可用的`multifield` Widget （只有文字欄位）為基礎，因此具有`multifield` Widget的所有功能。
* 「樹狀結構瀏覽」對話方塊（`treebrowse`節點）會顯示一個視窗，其中有一個索引標籤包含路徑瀏覽Widget：當您按一下箭頭時，會開啟一個視窗，您可以在其中瀏覽階層並選取專案。 專案的路徑接著會新增至路徑欄位，並在對話方塊關閉時持續存在。
* 以RTF編輯器外掛程式為基礎的對話方塊（ `rteplugin`節點），將自訂按鈕新增到RTF編輯器中，以插入一些自訂文字到主要文字。 它包含`richtext` Widget (RTE)以及透過RTE外掛程式機制新增的自訂功能。

自訂Widget和外掛程式包含在名為&#x200B;**3的元件中。 使用 ExtJS 介面工具集**&#x200B;軟體包的&#x200B;**自訂介面工具集**。要將此元件包含在示例頁面中，請執行以下操作：

1. 新增 **3. 自定義介面工具集**&#x200B;元件為範例頁面，來自 Sidekick **中的**「**使用 ExtJS 介面工具集**」標籤。
1. 該元件顯示標題、一些文本，並按下 **「屬性** 」連結時，將顯示存儲在存放庫中的段落的屬性。 再按一下會隱藏屬性。
元件顯示如下：

![chlimage_1-62](assets/chlimage_1-62.png)

#### 範例1：自訂多欄位Widget {#example-custom-multifield-widget}

**自訂多欄位** Widget型對話方塊會顯示一個視窗，其中包含一個索引標籤。 索引標籤具有自訂的多欄位Widget，不像標準小工具只有一個欄位，它有兩個欄位：包含兩個選項的下拉式功能表以及一個文字欄位。

**自訂多欄位** Widget型對話方塊：

* 由節點定義（節點型別= `cq:Dialog`，xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示包含面板（節點型別= `cq:Widget`，xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）的`tabpanel` Widget （節點型別= `cq:Widget`，xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）。
* 面板有`multifield` Widget （節點型別= `cq:Widget`，xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`）。
* `multifield` Widget具有以自訂xtype &#39; `ejstcustom`&#39;為基礎的fieldconfig （節點型別= `nt:unstructured`，xtype = `ejstcustom`，optionsProvider = `Ejst.x3.provideOptions`）：
   * &#39;`fieldconfig`&#39;是` [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MultiField)`物件的組態選項。
   * &#39;`optionsProvider`&#39;是`ejstcustom` Widget的設定。 它是使用定義於`exercises.js`中的`Ejst.x3.provideOptions`方法設定的：
     `/apps/extjstraining/clientlib/js/exercises.js`
和會傳回兩個選項。
* 由下列位置的`multifield`節點定義：
  `/apps/extjstraining/components/customwidgets/multifield`
* 透過請求以json格式轉譯：
  `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

自訂`multifield` Widget (xtype = `ejstcustom`)：

* 是名為`Ejst.CustomWidget`的JavaScript物件
* 已在`CustomWidget.js` JavaScript檔案中定義於：
  `/apps/extjstraining/clientlib/js/CustomWidget.js`
* 擴充` [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)` Widget。
* 有三個欄位： `hiddenField` (Textfield)、`allowField` (ComboBox)和`otherField` (Textfield)
* 覆寫`CQ.Ext.Component#initComponent`以新增三個欄位：
   * `allowField`是型別為&#39;select&#39;的[CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Selection)物件。 optionsProvider是Selection物件的組態，它是使用對話方塊中定義的CustomWidget的optionsProvider組態具現化
   * `otherField`是[CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)物件
* 覆蓋 `setValue`方法 、 `getValue`和 `getRawValue` [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField) 以設定和檢索 CustomWidget 的值，內容如下格式：
  `<allowField value>/<otherField value>, for example: 'Bla1/hello'`。
* 將自身註冊為&#39; `ejstcustom`&#39; xtype：
  `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

**自訂多欄位** Widget型對話方塊顯示如下：

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 範例 2： 自定義 `Treebrowse` Widget {#example-custom-treebrowse-widget}

基於自定義 **`Treebrowse`** 微件的對話框顯示一個視窗，其中一個標籤包含一個自定義路徑流覽微件。 選擇箭號時，將打開一個視窗，您可以在其中流覽階層並選擇專案。 然後，項目的路徑將添加到路徑欄位中，並在對話框關閉時保留。

自訂 `treebrowse` 對話框：

* 由節點定義 （節點 type = `cq:Dialog`， xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 顯示包含面板（節點型別= `cq:Widget`，xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）的`tabpanel` Widget （節點型別= `cq:Widget`，xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）。
* 面板有自訂Widget （節點型別= `cq:Widget`，xtype = `ejstbrowse`）
* 由下列位置的`treebrowse`節點定義：
  `/apps/extjstraining/components/customwidgets/treebrowse`
* 透過請求以json格式轉譯：
  `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

自訂樹狀瀏覽Widget (xtype = `ejstbrowse`)：

* 是名為`Ejst.CustomWidget`的JavaScript物件
* 已在`CustomBrowseField.js` JavaScript檔案中定義於：
  `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* 延伸` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`。
* 定義名為`browseWindow`的瀏覽視窗。
* 覆寫` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick`以在按一下箭頭時顯示瀏覽視窗。
* 定義[CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)物件：
   * 它透過呼叫在`/bin/wcm/siteadmin/tree.json`註冊的servlet來取得其資料。
   * 其根目錄為&quot; `apps/extjstraining`&quot;。
* 定義`window`物件( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`)：
   * 根據預先定義的面板。
   * 具有&#x200B;**確定**&#x200B;按鈕，可設定所選路徑的值並隱藏面板。
* 視窗錨定在&#x200B;**路徑**&#x200B;欄位下方。
* 選取的路徑會從`show`事件的瀏覽欄位傳至視窗。
* 將自身註冊為&#39; `ejstbrowse`&#39; xtype：
  `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

若要使用&#x200B;**自訂樹狀瀏覽** Widget式對話方塊：

1. 將&#x200B;**自訂Widget**&#x200B;元件的對話方塊取代為&#x200B;**自訂樹狀瀏覽**對話方塊：
請依照[範例2：單一面板對話方塊](#example-single-panel-dialog)中說明的步驟操作
1. 編輯元件：對話方塊顯示如下：

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 範例 3： RTF 編輯器 （RTE） 外掛程式 {#example-rich-text-editor-rte-plug-in}

**基於富文本編輯器 （RTE）** 外掛程式的對話框是基於富文本編輯器的對話框，具有在方括弧內插入一些自定義文本的自定義按鈕。自定義文字可以通過一些伺服器端邏輯（此示例中未實現）進行分析，例如，添加在給定路徑定義的一些文本：

**基於 RTE 外掛程式**&#x200B;對話盒：

* 由下列位置的Reteplugin節點定義：
  `/apps/extjstraining/components/customwidgets/rteplugin`
* 透過請求以json格式轉譯：
  `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* `rtePlugins`節點具有以外掛程式命名的子節點`inserttext` （節點型別= `nt:unstructured`）。 它有一個名為`features`的屬性，定義了RTE可用的外掛程式功能。

RTE外掛程式：

* 是名為`Ejst.InsertTextPlugin`的JavaScript物件
* 已在`InsertTextPlugin.js` JavaScript檔案中定義於：
  `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* 擴充` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`物件。
* 下列方法定義` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`物件，且會在實作外掛程式中覆寫：
   * `getFeatures()`會傳回外掛程式使其可用的所有功能陣列。
   * `initializeUI()`將新按鈕新增至RTE工具列。
   * 當按鈕懸停時，`notifyPluginConfig()`顯示標題和文字。
   * 按一下按鈕並執行plugin動作時會呼叫`execute()`：它會顯示一個視窗，用來定義要包含的文字。
* `insertText()`使用對應的對話方塊物件`Ejst.InsertTextPlugin.Dialog`插入文字（請參閱後續內容）。
* 對話方塊的`apply()`方法呼叫`executeInsertText()`，此動作會在按一下&#x200B;**確定**&#x200B;按鈕時觸發。
* 將自身註冊為&#39; `inserttext`&#39;外掛程式：
  `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* `Ejst.InsertTextPlugin.Dialog`物件會定義按一下外掛程式按鈕時所開啟的對話方塊。 此對話方塊包含面板、表單、文字欄位和兩個按鈕（**確定**&#x200B;和&#x200B;**取消**）。

若要使用以&#x200B;**RTF編輯器(RTE) Plug-in**&#x200B;為基礎的對話方塊：

1. 以&#x200B;**RTF編輯器(RTE)外掛程式**&#x200B;對話方塊取代&#x200B;**自訂Widget**元件的對話方塊：
請依照[範例2：單一面板對話方塊](#example-single-panel-dialog)中說明的步驟操作
1. 編輯元件。
1. 按一下右側的最後一個圖示（四個箭頭的圖示）。 輸入路徑並按一下&#x200B;**確定**：
路徑會顯示在方括弧([)中 ])。
1. 按一下&#x200B;**確定**，關閉RTF編輯器。

**基於 RTF 編輯器** （RTE） 外掛程式的對話框顯示如下：

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>此示例僅顯示如何實施邏輯的用戶端部分：然後必須在伺服器端上顯式解析佔位元（*[文本]*）（例如，在元件 JSP 中）。

### 樹狀結構概述 {#tree-overview}

現成可用的` [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)`物件提供樹狀結構資料的UI表示法。 使用 ExtJS Widgets **包中包含的**&#x200B;樹概述元件顯示了如何使用該`TreePanel`物件在給定路徑下顯示 JCR 樹。視窗本身可以停靠/取消停靠。 在此範例中，視窗邏輯嵌入在元件 jsp 中的標記之間 &lt;script> 。

要將樹 **概述** 元件包含在示例頁面中，請執行以下操作：

1. **新增 4.從 Sidekick 中的**&#x200B;使用 **ExtJS 接口工具**&#x200B;集標籤到示例頁面的樹概述&#x200B;**元件。**
1. 元件將顯示：
   * 標題，包含一些文字
   * **屬性**&#x200B;連結：按一下以顯示儲存在存放庫中的段落屬性。 再按一下可隱藏屬性。
   * 具有可展開之存放庫樹狀結構的浮動視窗。

元件顯示如下：

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

樹狀結構概觀元件：

* 定義於：
  `/apps/extjstraining/components/treeoverview`

* 對話方塊可讓您設定視窗的大小，並固定或取消固定視窗（請參閱下列詳細資訊）。

元件jsp：

* 從存放庫中擷取寬度、高度和停駐屬性。
* 顯示樹狀結構概觀資料格式的部分文字。
* 在JavaScript標籤之間，將視窗邏輯內嵌在元件jsp中。
* 定義於：
  `apps/extjstraining/components/treeoverview/content.jsp`

內嵌在元件jsp中的JavaScript程式碼：

* 嘗試從頁面擷取樹狀結構視窗，以定義`tree`物件。
* 如果顯示樹狀結構的視窗不存在，則會建立`treePanel` ([CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel))：
   * `treePanel`包含用來建立視窗的資料。
   * 系統會呼叫在下列位置註冊的servlet來擷取資料：
     `/bin/wcm/siteadmin/tree.json`
* `beforeload`接聽程式會確定已載入選取的節點。
* `root`物件將路徑`apps/extjstraining`設定為樹狀根目錄。
* `tree` ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`)是根據預先定義的`treePanel`設定的，且顯示為：
  `tree.show();`
* 如果視窗存在，視窗會根據從存放庫擷取的寬度、高度和停駐屬性顯示。

元件對話方塊：

* 顯示一個頁簽，其中有兩個欄位可設定樹狀概觀視窗的大小（寬度和高度），以及一個欄位可固定/取消固定視窗
* 由節點定義（節點型別= `cq:Dialog`，xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* 面板具有sizefield Widget （節點型別= `cq:Widget`，xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`）和選取專案Widget （節點型別= `cq:Widget`，xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`，型別= `radio`），其中包含兩個選項(true/false)
* 由下列位置的對話方塊節點定義：
  `/apps/extjstraining/components/treeoverview/dialog`
* 透過請求以json格式轉譯：
  `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* 顯示如下：

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### 格線概觀 {#grid-overview}

格線面板以表格格式的列和欄表示資料。 它由下列專案組成：

* 儲存：儲存資料記錄（列）的模型。
* 欄模型：欄組成。
* 檢視：封裝使用者介面。
* 選取範圍模型：選取範圍行為。

**使用ExtJS Widget**&#x200B;封裝中包含的Grid Overview元件會顯示如何以表格格式顯示資料：

* 範例1使用靜態資料。
* 範例2使用從存放庫擷取的資料。

將「網格概述」元件加入範例頁面：

1. 新增&#x200B;**5。 從**&#x200B;使用&#x200B;**Sidekick**&#x200B;中的ExtJS Widget **索引標籤，將格線概觀**&#x200B;元件移至範例頁面。
1. 元件隨即顯示：
   * 包含一些文字的標題
   * **屬性**&#x200B;連結：按一下以顯示儲存在存放庫中的段落屬性。 再按一下可隱藏屬性。
   * 包含表格格式資料的浮動視窗。

元件顯示如下：

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 範例1：預設格線 {#example-default-grid}

在其現成版本中， **「網格概述」** 元件在表格格式中顯示一個包含靜態數據的視窗。 在此範例中，邏輯以兩種方式嵌入到元件 JSP 中：

* 一般邏輯是在標記之間 &lt;script> 定義
* 特定邏輯可在個別的.js檔案中使用，並在jsp中連結至。 此設定可讓您藉由註解所需的&lt;script>標籤，在兩個邏輯（靜態/動態）之間切換。

「網格概述」元件：

* 定義於..
  `/apps/extjstraining/components/gridoverview`
* 該對話框允許您設定視窗的大小以及停靠或取消停靠視窗。

元件 jsp：

* 從存放庫檢索寬度、高度和停靠屬性。
* 顯示部分文字作為網格概覽數據格式的簡介。
* 參考定義GridPanel物件的JavaScript程式碼：
  `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`
  `defaultgrid.js`定義一些靜態資料做為GridPanel物件的基底。
* 在JavaScript標籤之間嵌入JavaScript程式碼，該標籤定義使用GridPanel物件的Window物件。
* 定義於：
  `apps/extjstraining/components/gridoverview/content.jsp`

內嵌在元件jsp中的JavaScript程式碼：

* 嘗試從頁面擷取視窗元件，以定義`grid`物件：
  `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* 如果`grid`不存在，則會呼叫`getGridPanel()`方法以定義[CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)物件(`gridPanel`) （請參閱下文）。 此方法已在`defaultgrid.js`中定義。
* `grid`是根據預先定義的GridPanel的` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`物件，顯示為： `grid.show();`
* 如果`grid`存在，則會根據從存放庫擷取的寬度、高度及停駐屬性來顯示。

元件jsp中參考的JavaScript檔案(`defaultgrid.js`)定義了`getGridPanel()`方法，該方法由內嵌於JSP中的指令碼呼叫，並根據靜態資料傳回` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`物件。 邏輯如下：

* `myData`是靜態資料的陣列，格式化為包含五欄和四列的表格。
* `store`是使用`myData`的`CQ.Ext.data.Store`物件。
* `store`已載入記憶體：
  `store.load();`
* `gridPanel`是使用`store`的` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`物件：
   * 欄寬一律會按比例分配：
     `forceFit: true`
   * 一次只能選取一列：
     `singleSelect:true`

#### 範例2：參照搜尋格線 {#example-reference-search-grid}

當您安裝套件時，**網格概述**&#x200B;元件的`content.jsp`會顯示以靜態資料為基礎的網格。 您可以修改元件，以顯示具有以下特性的格點：

* 有三個欄。
* 是以呼叫servlet從存放庫擷取的資料為基礎。
* 可以編輯最後一欄的儲存格。 值會保留在第一欄中顯示的路徑所定義的節點下方的`test`屬性中。

如前節所述，視窗物件透過呼叫`/apps/extjstraining/components/gridoverview/defaultgrid.js`的`defaultgrid.js`檔案中定義的`getGridPanel()`方法，取得其` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`物件。 **Grid概述**元件為`getGridPanel()`方法提供不同的實作，方法定義於`/apps/extjstraining/components/gridoverview/referencesearch.js`的`referencesearch.js`檔案。 透過切換元件jsp中參照的.js檔案，格線會以從儲存庫中擷取的資料為基礎。

切換在元件jsp中參照的.js檔案：

1. 在&#x200B;**CRXDE Lite**&#x200B;中，在元件的`content.jsp`檔案中，註解包含`defaultgrid.js`檔案的行，使其如下所示：
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. 從包含`referencesearch.js`檔案的行中移除註解，使其如下所示：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. 儲存變更。
1. 重新整理範例頁面。

元件顯示如下：

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

元件jsp ( `referencesearch.js`)中參考的JavaScript程式碼會定義從元件jsp呼叫的`getGridPanel()`方法，並根據從存放庫動態擷取的資料傳回` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`物件。 `referencesearch.js`中的邏輯將某些動態資料定義為GridPanel的基礎：

* `reader`是` [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`物件，讀取三欄的json格式的servlet回應。
* `cm`是三欄的` [CQ.Ext.grid.ColumnModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)`物件。
「測試」欄儲存格可以編輯，因為它們是使用編輯器定義的：
  `editor: new [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* 欄可排序：
  `cm.defaultSortable = true;`
* `store`是` [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)`物件：
   * 它會透過呼叫「`/bin/querybuilder.json`」上註冊的servlet來取得其資料，並使用一些用於篩選查詢的引數
   * 它是以`reader`為基礎，預先定義
   * 資料表是根據&#39;**jcr：path**&#39;資料行以遞增順序排序
* `gridPanel`是可編輯的` [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)`物件：
   * 是以預先定義的`store`和資料行模型`cm`為基礎
   * 一次只能選取一列：
     `sm: new [CQ.Ext.grid.RowSelectionModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * `afteredit`接聽程式會確定已編輯&#39;&#39;**Test**&#39;&#39;資料行中的儲存格之後：
      * &#39;**jcr：path**&#39;資料行所定義路徑之節點的屬性&#39;`test`&#39;是在儲存庫中以儲存格的值設定的
      * 如果POST成功，則會將值新增至`store`物件，否則會遭到拒絕
