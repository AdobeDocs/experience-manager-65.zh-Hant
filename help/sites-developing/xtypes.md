---
title: 使用xtypes（經典UI）
seo-title: Using xtypes (Classic UI)
description: 瞭解所有可用的xtype AEM
seo-description: Learn about all the xtypes that are available with AEM
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
exl-id: 06ca4e6d-9ab7-4c5b-905c-07c448632f2b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6400'
ht-degree: 0%

---

# 使用xtypes（經典UI）{#using-xtypes-classic-ui}

本頁介紹了Adobe Experience Manager()提供的所AEM有類型。

在ExtJS語言中， xtype是給類的符號名稱。 您可以閱讀 [ExtJS 2概述](https://www.sencha.com/learn/overview-of-extjs-2) 的子菜單。

有關所有可用小部件的完整信AEM息，請參閱 [構件API文檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)。

要查找給定xtype在中使用的元件AEM，可以在CRXDE中使用以下Xpath查詢，方法是將「checkbox」替換為您感興趣的xtype:

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>本頁介紹經典UI中ExtJS xtypes的用法。
>
>Adobe建議你利用標準，現代， [啟用觸摸的UI](/help/sites-developing/touch-ui-concepts.md) 基於 [珊瑚UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) 和 [花崗岩UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components)。

## x類型 {#xtypes}

請在下面查找Adobe Experience Manager的可用類型清單：

* 注釋

   [CQ.wcm.Annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

   「對話框」(Dialog)是一種特殊類型的窗口，其主體中包含表單，頁腳中包含按鈕組。 它通常用於編輯內容，但也只能顯示資訊。

* 陣列

   [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

   以前稱為「SimpleStore」。

   要建立的小幫助程式類 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)更輕鬆地從陣列資料中獲取。 ArrayStore將自動配置為 [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader)。

* 組合

   [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

   DAM管理中使用的資產編輯器。

* 裝配

   [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

   AssetReferenceSearchDialog是一個對話框，在頁面引用資產或標籤時會彈出該對話框。

* 藍印配置

   [CQ.wcm.msm.BlueprientConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

   BlueprientConfig提供了一個面板，用於查看藍圖的即時副本並編輯此藍圖屬性（同步觸發器和同步操作）。

* 藍印狀態

   [CQ.wcm.msm.BlueprientStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

   BlueprientStatus提供一個面板，用於查看和編輯藍圖及其即時副本關係。 瀏覽通過 [CQ.wcm.msm.BlueprientStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree)，通過 [CQ.wcm.msm.BlueprientConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) 和 [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)。

* 框

   [CQ.Ext.Box元件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

   任意基類 [元件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) 即用寬度和高度將其尺寸調整為框。

   BoxComponent提供自動的框模型調整，用於調整大小和定位，並將在「元件」渲染模型中正確工作。

* 瀏覽對話框

   [CQ.瀏覽對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

   「瀏覽」對話框允許用戶瀏覽儲存庫以選擇路徑。 通常通過 [瀏覽欄位](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)。

* 瀏覽欄位

   [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

   **已棄用：使用 [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) 改**

* 牛鞭草

   [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

   BulkEditor提供一個搜索引擎和一個網格來編輯搜索結果。

   必須將BulkEditor插入HTML表單（導入功能需要）。 這與 [CQ對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)。

* 膨脹形

   [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

   BulkEditorForm提供 [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) 被HTML形狀包圍。 這是 [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)，「導入」按鈕需要HTML窗體。

* 按鈕

   [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

   簡單按鈕類

* 按鈕組

   [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

   一組按鈕的容器。

* 圖表

   [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

   CQ.Ext.chart軟體包提供了使用基於快閃記憶體的圖表來可視化資料的功能。 每個圖表直接綁定到CQ.Ext.data.Store，以便自動更新圖表。 要更改圖表的外觀，請參閱 [圖表樣式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) 和 [額外樣式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) 配置選項。

* 核取方塊

   [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

   單個複選框欄位。 可以直接替換傳統複選框欄位。

* 檢查框組

   [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

   用於 [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox) 控制項。

* 清單組合

   [CQ.form.ClerableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

   ClerableComboBox是一個不可編輯的組合框，帶有用於清除其值的觸發器。

* 色場

   [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

   ColorField允許用戶直接或使用 [CQ.Ext.Color菜單](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu)。

* 彩色清單

   [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

   「顏色清單」(ColorList)允許用戶從可編輯清單中選擇顏色。

* 顏色菜單

   [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

   包含 [CQ.Ext.調色板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette) 元件。

* 調色板

   [CQ.Ext.調色板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

   用於選擇顏色的簡單調色板類。 調色板可呈現給任何容器。

* 組合

   [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

   一種支援自動完成、遠程載入、分頁和許多其他功能的組合框控制項。

   ComboBox的工作方式與傳統HTML類似 &lt;select> 的子菜單。 區別在於 [值欄位](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)，必須指定 [隱藏名稱](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) 的子菜單。

* 元件

   [CQ.Ext.元件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

   所有Ext元件的基類。 元件的所有子類都可以參與由元件提供的建立、渲染和銷毀的自動Ext元件生命週期 [容器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 類。 元件可通過 [項目](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 配置選項。

* 元件帶線器

   [CQ.wcm.ComponentExtractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

   ComponentExtractor允許用戶從網站/頁面中提取元件。

* 元件選擇器

   [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

   可用元件的分組、有序選擇。

* 元件樣式

   [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* 複合場

   [CQ.form.複合欄位](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

   基類，用於基於面板的複雜表單域，其中包含一個表單域或一組表單域。

* 容器

   [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

   任意基類 [CQ.Ext.Box元件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) 可能包含其他元件。 容器處理包含項的基本行為，即添加、插入和刪除項。

   最常用的容器類是 [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)。 [CQ.Ext.窗口](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 和 [CQ.Ext.Tab面板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)。

* 內容查找器

   [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

   ContentFinder是一個專用的兩列 [視區](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) 它包含左側的實際內容查找器和右側的內容框架。

* contentfindertab

   [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

   ContentFinderTab是一個專用面板，提供了在 [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)。 通常，它具有一個搜索表單（查詢框）和一個顯示搜索的資料視圖。

* cq.workflow.model.combo

   [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

   WorkflowModelCombo是自定義的 [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) 顯示可用工作流模型的清單。

* cq.workflow.model.selector

   [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

   WorkflowModelSelector將WorkflowModelCombo與工作流的縮覽圖影像以及用於建立和編輯工作流模型的按鈕組合在一起。

* 建立站點嚮導

   [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

   CreateSiteWizard是用於建立(MSM)站點的逐步嚮導。

* 建立版本對話框

   [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

   CreateVersionDialog是允許建立頁面新版本的對話框。

* 自定義內容面板

   [CQ.自定義內容面板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

   CustomContentPanel是用於 [CQ對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog):其內容將從對話框中的其他欄位檢索並提交到不同的URL。

* 循環

   [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

   包含菜單的專用SplitButton [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem) 元素。 按鈕在按一下時自動循環瀏覽每個菜單項，從而提高按鈕的 [更改](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) 事件(或調用按鈕 [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) 的子菜單。

* 資料視圖

   [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

   一種使用自定義佈局模板和格式顯示資料的機制。 DataView使用 [CQ.Ext.XT模板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) 作為內部模板機制，與 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) 這樣，當儲存中的資料發生更改時，視圖將自動更新以反映更改。

* datefield（日期欄位）

   [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

   提供帶有 [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) 下拉和自動日期驗證。

* 日期菜單

   [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

   包含 [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) 元件。

* 日期選擇器

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

   彈出式日期選取器。 此類由 [日期欄位](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) 允許瀏覽和選擇有效日期的類。

* 日期

   [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

   DateTime允許用戶通過組合輸入日期和時間 [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) 和 [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)。

* 對話方塊

   [CQ對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

   「對話框」(Dialog)是一種特殊類型的窗口，其主體中包含表單，頁腳中包含按鈕組。 它通常用於編輯內容，但也只能顯示資訊。

* 對話框欄位集

   [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

   DialogFieldSet是 [欄位集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) 用於 [對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)。

* 直銷

   [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

   用於建立 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) 配置為 [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) 和 [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) 與 [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) 伺服器端 [提供程式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) 更簡單。

* 顯示欄位

   [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

   未驗證且未提交的僅顯示文本欄位。

* 編輯欄

   [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

   編輯欄允許用戶使用欄上的按鈕編輯內容。

   雖然未在此列出，但EditBar具有 [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase)。

* 編輯器

   [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

   處理按需顯示/隱藏的基本編輯器欄位，具有一些內置的調整大小和事件處理邏輯。

* 編輯

   [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

   此類擴展 [GridPanel類](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 提供所選單元格編輯 [列](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column)。 通過提供 [編輯器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) 的 [列配置](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column)。

* 編輯

   [CQ.wcm.EditRoulder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

   「編輯」(Edit)「滾動」(Roupler)允許用戶通過按兩下來編輯內容，並通過上下文菜單提供更多編輯操作。 當滑鼠滾動到內容上時，可編輯區域以框架表示。

* feediporter

   [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

   FeedImporter允許用戶導入RSS或Atom源並為每個源項建立頁面。

* 欄位

   [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

   提供預設事件處理、調整大小、值處理和其他功能的表單域的基類。

* 欄位集

   [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

   用於在 [表格](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel)。...

* 檔案加密按鈕

   [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

   FileUploadDialogButton會建立一個按鈕，該按鈕會開啟一個新對話框，用於通過FileUploadField上載檔案。 可以在編輯對話框內使用，其中上載必須以單獨的形式進行。

* 檔案上載欄位

   [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

   FileUploadField允許用戶選擇要上載的單個檔案。

* 定義對話框

   [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

   FindReplaceDialog是一個對話框，用於查找和替換頁面及其子頁面中的標籤。

* 閃

   [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* 網格

   [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

   此類表示基於元件的網格控制項的主要介面，以行和列的表格格式表示資料。

* 組儲存

   [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

   提供按可用欄位之一分組記錄的專用儲存實現。 通常與 [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) 以證明分組GridPanel的資料模型。

* 重彈

   [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

   HeavyMoveDialog是一個用於移動頁面及其子頁面的對話框，還考慮重新激活以前激活的頁面（「heavy」移動）。

* 隱藏

   [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

   一個基本隱藏欄位，用於儲存表單中需要傳遞的隱藏值。

* 歷史記錄按鈕

   [CQ.歷史記錄按鈕](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

   HistoryButton是一個小幫助類，可輕鬆提供後向和前向按鈕。 通常需要兩個相關實例：正向按鈕實例是連結到處理歷史記錄的後向按鈕實例的簡單按鈕。

* 海德

   [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

   提供輕量級HTML編輯器元件。 Safari不支援某些工具欄功能，並將在需要時自動隱藏。 在配置選項中（如適用）註明了這些內容。

   編輯器的工具欄按鈕在 [按鈕提示](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor) 屬性。

* 伊斯蘭國

   [CQ.Iframe對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

   一個純對話框，顯示iframe的內容並允許在iframe中使用表單。

* 菲拉美

   [CQ.Iframe面板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

   包含iframe的面板。 提供iframe的輕鬆建立、iframe載入事件和對iframe內容的輕鬆訪問。

* inlinetextfield

   [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

   InlineField是一個文本欄位，在不處於焦點時顯示為標籤。

* 松斯托

   [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

   要建立的小幫助程式類 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)Json資料中的s更簡單。 JsonStore將自動配置為 [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)。

* 標籤

   [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

   基本標籤欄位。

* 語言

   [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

   LanguageCopyDialog是用於複製語言樹的對話框。

* 連結檢查器

   [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

   LinkChecker是檢查站點中外部連結的工具。

* 清單視圖

   [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

   CQ.Ext.list.ListView是快速且輕量化的 [網格](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 就像風景。

* 逆性

   [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

   LiveCopyProperties提供了一個面板，用於查看和編輯Live Copy屬性（關係繼承、同步觸發器和同步操作）。

* 縱列

   [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

   呈現布爾資料欄位的列定義類。 查看 [x類型](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) config選項 [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 的子菜單。

* lvc列

   [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

   此類封裝要用於初始化的列配置資料 [清單視圖](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)。

* lvdate列

   [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

   根據預設區域設定呈現傳遞日期的列定義類，或配置 [格式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)。 查看 [x類型](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) config選項 [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 的子菜單。

* lvnumber列

   [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

   Column定義類，它根據 [格式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn) 的下界。 查看 [x類型](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) config選項 [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 的子菜單。

* 媒體對話

   [CQ.媒體瀏覽對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

   **已棄用：使用 [內容查找器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) 瀏覽媒體。**

   MediaBrowseDialog是用於瀏覽媒體庫的對話框。

* 菜單

   [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

   菜單對象。 這是可以向其中添加菜單項的容器。 當您想要基於另一個元件的專用菜單時，菜單也可以用作基類(如 [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) 例如)。

   菜單可包含 [菜單項](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)或常規 [元件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)s

* 門巴塞特姆

   [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

   呈現到菜單中的所有項的基類。 BaseItem提供預設呈現、激活的狀態管理和所有菜單元件共用的基本配置選項。

* 門切基特

   [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

   預設情況下，添加包含複選框但也可以是無線電組的一部分的菜單項。

* 門項

   [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

   需要與菜單相關功能（如子菜單）且不是靜態顯示項的所有菜單項的基類。 項擴展了 [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) 添加菜單特定激活，然後按一下處理。

* 使用者

   [CQ.Ext.menu.分隔符](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

   將分隔符條添加到菜單，用於劃分菜單項的邏輯組。 通常，在調用add()或項目配置中使用「 — 」來添加其中一個，而不是直接建立。

* 門特斯提特姆

   [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

   將靜態文本字串添加到菜單，通常用作標題或組分隔符。

* 中繼資料

   [CQ.dam.form.元資料](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

   元資料提供一組欄位以確定元資料欄位所需的資訊（例如在資產編輯器頁上）。

   它提供以下欄位：

* 多場

   [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

   「多欄位」是可編輯的表單域清單，用於編輯多值屬性。

* mvt

   [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

   多變數測試元件可用於定義和編輯一組影像，這些影像以交替橫幅顯示。 按一下按標題收集速率統計資訊。

* 通知收件箱

   [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

   NotificationInbox允許用戶訂閱WCM操作和管理通知。

* 數字欄位

   [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

   提供自動擊鍵過濾和數字驗證的數字文本欄位。

* 離線進口商

   [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

   OfflineImporter是一種工具，可將MicrosoftWord文檔導入和轉換AEM為頁面。 此功能允許使用文字處理器離線編輯內容。

* 所有權

   [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

   OwnerDraw可包含自定義HTML代碼（直接輸入或從URL檢索）。

* 尋呼

   [CQ.Ext.Paging工具欄](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

   隨著記錄數量的增加，瀏覽器呈現這些記錄所需的時間也會增加。 使用尋呼來減少與客戶端交換的資料量。

* 面板

   [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

   面板是具有特定功能和結構元件的容器，使其成為面向應用程式的用戶介面的完美構建基塊。

   由於小組繼承了 [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)。

* 段落引用

   [CQ.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

   段落引用欄位允許瀏覽頁面並選擇其中一個段落。 它由觸發器欄位和關聯的段落瀏覽對話框組成。

* 密碼

   [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

   密碼類似於 [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) 但保持其值為私有，允許用戶輸入敏感資料。

* 路徑完成

   [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

   **已棄用：使用 [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) 改**

* 路徑

   [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

   PathField是為路徑完成路徑設計的輸入欄位和用於開啟 [CQ.瀏覽對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) 瀏覽伺服器儲存庫。 它還可以瀏覽頁面段落以生成高級連結。

* 進度

   [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

   可更新的進度條元件。 進度條支援兩種不同模式：手動和自動。

   在手動模式下，您負責顯示、更新(通過 [更新進度](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar))並根據需要從您自己的代碼中清除進度條。 當要顯示進度時，此方法最合適。

* 屬性網格

   [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

   專門的網格實現旨在模仿開發IDE中通常看到的傳統屬性網格。 網格中的每一行表示某個對象的屬性，資料以一組名稱/值對的形式儲存在 [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)s

* 丙格網

   [CQ.屬性網格](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

   PropertyGrid是用於顯示和編輯對象屬性的通用網格。

* 快速提示

   [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

   @xtype quicktip（快速提示）工具提示的專用工具提示類，可在標籤中指定並由全局自動管理 [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips) 實例。 有關其他使用情況詳細資訊和示例，請參閱快速提示類標題。

* 無線電

   [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

   單個無線電場。 與複選框相同，但為自動設定輸入類型提供了方便。 如果給組中的每個無線電指定相同的名稱，則瀏覽器會自動處理無線電分組。

* 放射組

   [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

   用於 [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio) 控制項。

* 參照對話框

   [CQ.wcm.References對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

   「參照」(References)「對話框」(Dialog)是用於在頁面上顯示參照的對話框。

* 重排樹

   [CQ.wcm.RestoreTree對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

   RestoreTreeDialog是用於恢復樹的早期版本的對話框。

* 重排版本對話框

   [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

   RestoreVersionDialog是用於恢復頁面早期版本的對話框。

* RichText

   [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

   RichText提供了一個表單域，用於編輯樣式文本資訊(RTF)。

   RichText元件當前提供了以下功能：

* 推出計畫

   [CQ.wcm.msm.SolvultPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

   OllovatePlan提供一個對話框來監視頁面的展開進度。 OlvoltPlan由 [CQ.wcm.msm.OllovateWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)。

* 滾向

   [CQ.wcm.msm.OllovateWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

   OllovateWizard提供了用於滾出頁面的嚮導。 OutloctWizard啟動 [CQ.wcm.msm.SolvultPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)。

* 搜索欄位

   [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

   SearchField提供搜索欄位，該欄位在下拉清單中提供結果，該下拉清單可用於搜索儲存庫。

* 選擇

   [CQ.form.選擇](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

   「選擇」(Selection)允許用戶在多個選項之間進行選擇。 這些選項可以是配置的一部分，也可以從JSON響應中載入。 「選擇」可以呈現為下拉清單（選擇）或組合框（選擇加自由文本條目）。

* 側衛

   [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

   Sidekick是一個浮動幫助程式，為用戶提供用於頁面編輯的通用工具。

* 站點管理

   [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

   SiteAdmin是提供WCM管理功能的控制台。

* 站點導入程式

   [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

   SiteImporter允許用戶導入完整網站並建立初始項目。

* sizefile（大小欄位）

   [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

   SizeField允許用戶輸入寬度和高度（例如，影像）。

* 滑桿

   [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

   支援垂直或水準方向、鍵盤調整、可配置貼緊、軸按一下和動畫的滑塊。 可以將項目添加到任何容器。 示例用法：...

* 幻燈片

   [CQ.form.幻燈片](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

   幻燈片放映提供了一個元件，可用於定義和編輯一組影像和影像標題，這些影像和影像標題可以作為幻燈片放映來查看。

   「幻燈片放映」元件基於 [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage) 元件。

* smartfile

   [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

   SmartFile是智慧檔案上載程式。

   如果安裝了Flash插件（版本>= 9），則使用SWFupload庫執行上載，該庫提供了一種處理上載的便捷方法。

* 智慧

   [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

   SmartImage是一種智慧映像上載器。 它提供了處理上載影像的工具，例如定義影像映射和影像剪切器的工具。

   請注意，該元件主要設計用於單獨的對話框頁籤上。

* 間隔

   [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

   用於在佈局中提供較大的空間。

* 旋轉器

   [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

   Spinner是數值、日期或時間值的觸發器欄位。 通過使用所提供的上下觸發器、滾輪或鍵，可以增加和減小該值。

* 拆分按鈕

   [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

   一個拆分按鈕，它提供一個內置的下拉箭頭，該箭頭可以與按鈕的預設按一下事件分開觸發事件。 通常，這用於顯示一個下拉菜單，該下拉菜單為主按鈕操作提供了其他選項，但任何自定義處理程式都可提供arrowclick實現。

* 靜態

   [CQ.靜態](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

   「靜態」(Static)可用於顯示任意文本或HTML。

* statistics

   [CQ.wcm.統計](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

   統計資訊將頁印象顯示為圖表。 該小部件允許選擇期間，應顯示其統計資訊。

* 商店

   [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

   Store類封裝客戶端快取 [記錄](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) 為元件(如 [網格面板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)，也請參見Wiki頁。 [組合框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)，或 [資料視圖](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)。

* 暗示場

   [CQ.form.SuggestField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

   SeggestField根據用戶的條目向用戶提供建議。

* 切換

   [CQ.切換器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

   Switcher為控制台中的標題欄提供一個按鈕組，以在網站、數字資產、工具、工作流和安全性之間切換。

* 表格編輯

   [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

   **已棄用：使用 [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) 的雙曲餘切值。**

* tableedit2

   [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

   TableEdit2提供了用於建立表的構件。

* table面板

   [CQ.Ext.Tab面板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

   基本頁籤容器。 TabPanels可以完全像標準 [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) 用於佈局目的，但還支援包含子元件([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container))。

* 標記

   [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

   ```
   CQ.tagging.TagInputField
   ```

   是用於輸入標籤的表單小部件。 它有一個彈出菜單，用於從現有標籤中進行選擇，包括自動完成和許多其他功能。

* 毛蕊

   [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

   多行文本欄位。 可以直接替代傳統的文本區域欄位，並增加對自動調整大小的支援。

* 文本按鈕

   [CQ.文本按鈕](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

   TextButton提供具有 [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)。

* 文本欄位

   [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

   基本文本欄位。 可用作傳統文本輸入的直接替換，或用作更複雜輸入控制項的基類(如 [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) 和 [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox))。

* 縮略圖

   [CQ.form.縮略圖](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* 時域

   [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

   提供帶時間下拉清單和自動時間驗證的時間輸入欄位。 示例用法：...

* 尖端

   [CQ.Ext.提示](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

   @xtype提示這是 [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) 和 [CQ.Ext.工具提示](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) 提供所有基於提示的類所需的基本佈局和定位。 此類可直接用於簡單靜態定位的提示。

* 角色角

   [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

   將分隔符條添加到菜單，用於劃分菜單項的邏輯組。 分隔器可附加地承載標題。

* 工具欄

   [CQ.Ext.工具欄](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

   基本工具欄類。 儘管 [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 工具欄 [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)，工具欄元素（工具欄容器的子項）實際上可以是任何類型的元件。 可以通過其建構子顯式建立工具欄元素。

* 提示

   [CQ.Ext.工具提示](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

   一種標準工具提示實現，用於在懸停於目標元素上時提供附加資訊。 @xtype工具提示。

* 樹狀網格

   [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

   @xtype樹網格

* 樹面

   [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

   TreePanel提供樹結構化資料的樹結構化UI表示。

   [樹節點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)添加到TreePanel的每個元件都可能包含應用程式在其中使用的元資料 [屬性](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) 屬性。

* 觸發

   [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

   為添加可按一下的觸發按鈕的TextField提供方便的包裝（預設情況下，該按鈕看起來像組合框）。 觸發器沒有預設操作，因此您必須通過覆蓋來指定函式來實現觸發器按一下處理程式 [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)。 可以直接建立TriggerField，因為它呈現得與組合框完全一樣。

* 升級

   [CQ.上載對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

   UploadDialog允許用戶將檔案上載到儲存庫建立新的UploadDialog。

* 用戶資訊

   [CQ.用戶資訊](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

   工具欄項，用於顯示當前用戶名並允許用戶執行編輯用戶屬性和模擬等操作。

* 視區

   [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

   表示可視應用程式區域（瀏覽器視區）的專用容器。

   「視區」(Viewport)將自身呈現到文檔主體中，並自動將自身大小調整到瀏覽器視區的大小，並管理窗口大小調整。 只能建立一個視區。

* 視窗

   [CQ.Ext.窗口](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

   專用面板，用作應用程式窗口。 窗子浮了， [可調整](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window), [拖放](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 預設值。 Windows可以是 [最大化](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 填充視區，恢復到其原有大小，並且 [最小化](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

   [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

   要建立的小幫助程式類 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)從XML資料中更輕鬆。 XmlStore將自動配置為 [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader)。

   **cqincu** 偽xtype，包括儲存庫中不同路徑中的小部件定義。 它最常用於頁面對話框。 此類型沒有實際的JavaScript小部件類。 它由CQ.Util類的formatData()函式處理。 有關詳細資訊，請參閱此知識庫文章。
