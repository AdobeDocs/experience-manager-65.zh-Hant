---
title: 編寫——環境和工具
seo-title: 編寫——環境和工具
description: 的製作環境提AEM供多種機制來組織和編輯您的內容
seo-description: 的製作環境提AEM供多種機制來組織和編輯您的內容
uuid: 23a8aa93-b3d2-423b-b402-9e5f3f273d9a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f488ba79-5bda-46e9-9c15-9a8c3dbfa2ce
docset: aem65
exl-id: 3b3c118b-ca35-484b-a62e-7bec98953123
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '2239'
ht-degree: 10%

---

# 編寫——環境和工具{#authoring-the-environment-and-tools}

的製作環境提AEM供多種機制來組織和編輯您的內容。 提供的工具可從各種控制台和頁面編輯器中存取。

## 管理您的網站{#managing-your-site}

**Sites**&#x200B;主控台可讓您使用標題列、工具列、動作圖示（適用於選取的資源）、導覽路徑標示，以及選取時的次要導軌（例如時間軸和參考），來導覽和管理您的網站。

例如，列視圖：

![ateat-01](assets/ateat-01.png)

## 編輯頁面內容 {#editing-page-content}

您可以使用頁面編輯器編輯頁面。 例如：

`https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

![ateat-02](assets/ateat-02.png)

>[!NOTE]
>
>當您第一次開啟頁面進行編輯時，一連串的投影片會提供您功能指南。
>
>您可以視需要略過導覽，並隨時從&#x200B;**頁面資訊**&#x200B;選單中選取以重複。

## 訪問幫助{#accessing-help}

編輯頁面時，可從以下位置訪問&#x200B;**Help**:

* [**頁面資訊**](/help/sites-authoring/editing-page-properties.md#page-properties)&#x200B;選擇器；這將顯示介紹性投影片（如您第一次存取編輯器時所顯示）。
* [configuration](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)對話方塊，以取得特定元件(使用？ 表徵圖);這會顯示內容相關的說明。

控制台](/help/sites-authoring/basic-handling.md#accessing-help)還提供與幫助相關的其他資源。[

## 元件瀏覽器{#components-browser}

元件瀏覽器會顯示目前頁面上可用的所有元件。 這些內容可拖曳至適當位置，然後進行編輯以新增內容。

元件瀏覽器是側面板中的標籤(連同資產 [瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser)[和內容樹](/help/sites-authoring/author-environment-tools.md#content-tree))。要開啟 (或關閉) 側面板，請使用工具欄左上角的表徵圖：

![ateat-03](assets/ateat-03.png)

當您開啟側面板時，它會從左側滑動開啟（如有必要，請選取「**元件**」標籤）。 開啟時，您可以瀏覽頁面的所有可用元件。

實際外觀和處理方式取決於您使用的設備類型：

>[!NOTE]
>
>當寬度小於1024px時檢測到移動設備。 此外，小型案頭視窗也可能適用。

* **行動裝置（例如iPad）**

   元件瀏覽器完全涵蓋正在編輯的頁面。

   若要將元件新增至頁面，並按住所需的元件並向右移動——元件瀏覽器會關閉，再次顯示頁面——您可在此處放置元件。

   ![ateat-04](assets/ateat-04.png)

* **案頭裝置**

   元件瀏覽器在窗口的左側開啟。

   若要將元件新增至您的頁面，請按一下所需元件，並將其拖曳至所需位置。

   ![ateat-05](assets/ateat-05.png)

   元件由

   * 元件名稱
   * 元件群組（以灰色顯示）
   * 圖示或縮寫

      * 標準元件的圖示為單色。
      * 縮寫始終是元件名稱的前兩個字元。

   從&#x200B;**Components**&#x200B;瀏覽器的頂部工具欄，您可以：

   * 依名稱篩選元件。
   * 使用下拉式選取範圍，將顯示限制在特定群組。

   如需元件的詳細說明，您可以在「元件」瀏覽器中按一下或點選元件旁的資訊圖示(如果 **有** )。例如，對於「版面 **容器」**:

   ![ateat-06](assets/ateat-06.png)

   有關可用元件的更多資訊，請參閱[元件控制台](/help/sites-authoring/default-components-console.md)。

## 資產瀏覽器{#assets-browser}

資產瀏覽器會顯示目前頁面上所有可直接使用的[資產](/help/assets/home.md)。

資產瀏覽器是側面板內的標籤，以及[元件browse](/help/sites-authoring/author-environment-tools.md#components-browser)r和[內容樹狀結構](/help/sites-authoring/author-environment-tools.md#content-tree)。 要開啟或關閉側面板，請使用工具欄左上角的表徵圖：

![ateat-03-1](assets/ateat-03-1.png)

當您開啟側面板時，它會從左側滑動開啟。 如有必要，請選擇&#x200B;**Assets**&#x200B;標籤。

![ateat-07](assets/ateat-07.png)

當資產瀏覽器開啟時，您可以瀏覽頁面的所有可用資產。 視需要使用無限捲動來展開清單。

![ateat-08](assets/ateat-08.png)

若要將資產新增至頁面，請選取並拖曳至所需位置。 這可以是：

* 適當類型的現有元件。

   * 例如，您可以將文字影像的資產拖曳至影像元件上。

* 段落系統中的[佔位符](/help/sites-authoring/editing-content.md#component-placeholder)可建立適當類型的新元件。

   * 例如，您可以將文字影像的資產拖曳至段落系統，以建立影像元件。

>[!NOTE]
>
>這適用於特定資產和元件類型。 如需詳細資訊，請參閱[使用資產瀏覽器插入元件](/help/sites-authoring/editing-content.md#inserting-a-component-using-the-assets-browser)。

從資產瀏覽器的頂端工具列，您可以依下列方式篩選資產：

* 名稱
* 路徑
* 資產類型，例如影像、手稿、檔案、影片、頁面、段落和產品
* 資產特性，例如方向（縱向、橫向、正方形）和樣式（彩色、單色、灰階）

   * 僅適用於特定資產類型

實際外觀和處理方式取決於您使用的設備類型：

>[!NOTE]
>
>當移動設備寬度小於1024px時，檢測到移動設備；例如，也可在小型案頭視窗上。

* **行動裝置，例如iPad**

   資產瀏覽器會完全涵蓋正在編輯的頁面。

   若要將資產新增至頁面並按住必要的資產，然後將其向右移動——資產瀏覽器會關閉以再次顯示頁面，您可在其中將資產新增至所需元件。

   ![ateat-09](assets/ateat-09.png)

* **案頭裝置**

   資產瀏覽器會在視窗左側開啟。

   若要將資產新增至頁面，請按一下所需資產，然後拖曳至所需元件或位置。

   ![ateat-10](assets/ateat-10.png)

如果您需要快速變更資產，可以按一下資產名稱旁的編輯圖示，直接從資產瀏覽器啟動[資產編輯器](/help/assets/manage-assets.md)。

![](do-not-localize/screen_shot_2018-03-22at142448.png)

## 內容樹 {#content-tree}

**內容樹**&#x200B;概述了分層結構中頁面上的所有元件，讓您一目瞭然地瞭解頁面的構成方式。

「內容樹」是側面板（連同元件和資產瀏覽器）中的標籤。 要開啟 (或關閉) 側面板，請使用工具欄左上角的表徵圖：

![](do-not-localize/screen_shot_2018-03-22at142042.png)

當您開啟側面板時，它會滑開（從左側）。 如有必要，請選擇&#x200B;**內容樹**&#x200B;頁籤。 當開啟時，您可以看到頁面或範本的樹狀檢視表示，以便更輕鬆地瞭解其內容的階層式結構。 此外，在複雜的頁面上，可更輕鬆地在頁面的元件之間跳轉。

![ateat-11](assets/ateat-11.png)

頁面可輕鬆由許多相同類型的元件組成，因此內容（元件）樹狀結構會在元件類型名稱（黑色）後顯示描述性文字（以灰色顯示）。 描述性文字來自元件的常用屬性，例如標題或文字。

元件類型將以用戶語言顯示，而元件說明文本則來自頁面語言。

按一下元件旁邊的雪佛龍將折疊或展開該級別。

![screen_shot_2018-03-22at142559](assets/screen_shot_2018-03-22at142559.png)

>[!NOTE]
>
>如果您在行動裝置上編輯頁面（如果瀏覽器寬度小於1024像素），則無法使用「內容樹」。

按一下元件會在頁面編輯器中反白顯示元件。 可用的動作將視頁面狀態而定：

* 例如，基本頁面：

   `https://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html`

   ![ateat-12](assets/ateat-12.png)

   如果您在樹狀結構中按一下的元件是可編輯的，則名稱右側會出現扳手圖示。 按一下此表徵圖將直接啟動元件的編輯對話框。

   ![](do-not-localize/screen_shot_2018-03-22at142725.png)

* 或是屬於[livecopy](/help/sites-administering/msm.md)的一部分的頁面，其中元件繼承自另一頁；例如：

   `https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

   ![ateat-13](assets/ateat-13.png)

## 片段——關聯的內容瀏覽器{#fragments-associated-content-browser}

如果您的頁面包含內容片段，則您也可以存取[瀏覽器以取得關聯的內容](/help/sites-authoring/content-fragments.md#using-associated-content)。

## 引用 {#references}

**參** 考顯示到選定頁的連接：

* BluePrint
* 啟動
* 即時副本
* 語言副本
* 導入連結
* 使用參考元件：借閱和借閱內容
* 產品頁面的參考（來自「商務——產品」主控台）

開啟所需的控制台，然後導航到所需資源，並使用以下方式開啟&#x200B;**引用**:

![screen_shot_2018-03-22at153653](assets/screen_shot_2018-03-22at153653.png)

[選擇所需](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) 資源以顯示與該資源相關的參考型別清單：

![ateat-22](assets/ateat-22.png)

選擇適當的參考類型以瞭解詳細資訊。 在某些情況下，當您選擇特定參照時，可以執行其他操作，包括：

* **傳入連結**，提供參考頁面的頁面清單，以及當您選取特定連結時，可直接存取這些頁 **** 面的「編輯」功能

* 使用&#x200B;**Reference**&#x200B;元件借閱和借閱內容的例項，您可從這裡導覽至參考／參考頁面

* [產品頁面的參考](/help/commerce/cif-classic/administering/generic.md#showing-product-references) （可從Commerce-Products主控台取得）
* [啟動](/help/sites-authoring/launches.md)，提供相關啟動的存取權
* [即時](/help/sites-administering/msm.md) 副本顯示所有基於所選資源的即時副本的路徑。
* [Blueprint](/help/sites-administering/msm-best-practices.md)，提供詳細資訊和各種動作
* [語言復本](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel)，提供詳細資訊和各種動作

例如，可以在「參照」(Reference)元件中修正損壞的參照：

![ateat-14](assets/ateat-14.png)

## 事件——時間軸{#events-timeline}

對於適當的資源（例如&#x200B;**Sites**&#x200B;控制台中的頁面，或&#x200B;**Assets**&#x200B;控制台中的資產）,[時間軸可用於顯示任何選定項目上的最近活動](/help/sites-authoring/basic-handling.md#timeline)。

開啟必要的主控台，然後導覽至所需的資源，並開啟&#x200B;**時間軸**，使用：

![ateat-15](assets/ateat-15.png)

[選擇所需資源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)，然後選擇 **顯示** 所有活 **** 動以列出所選資源上的任何最近操作：

![ateat-16](assets/ateat-16.png)

## 頁面資訊 {#page-information}

「頁面資訊 (均衡器圖示) 」會開啟一個功能表，其中也提供上次編輯和上次發佈的詳細資訊。視頁面、其網站和您的例項的特性而定，可能有更多或更少的選項可用：

![ateat-17](assets/ateat-17.png)

* [開啟屬性](/help/sites-authoring/editing-page-properties.md)
* [轉出頁面](/help/sites-administering/msm.md#msm-from-the-ui)
* [啟動工作流程](/help/sites-authoring/workflows-applying.md#starting-a-workflow-from-the-page-editor)
* [鎖定頁面](/help/sites-authoring/editing-content.md#locking-a-page)
* [發佈頁面](/help/sites-authoring/publishing-pages.md#main-pars-title-10)
* [取消發佈頁面](/help/sites-authoring/publishing-pages.md#main-pars-title-5)
* [編輯範本](/help/sites-authoring/templates.md);頁面以可編輯的範本為 [基礎](/help/sites-authoring/templates.md#editable-and-static-templates)

* [以已發佈狀態檢視](/help/sites-authoring/editing-content.md#view-as-published)
* [在 Admin 中檢視](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)
* [說明](/help/sites-authoring/basic-handling.md#accessing-help)

例如，在適當時，**頁面資訊**&#x200B;也有下列選項：

* [升級](/help/sites-authoring/launches-promoting.md) 啟動（如果頁面是啟動）。
* [在Classic ](/help/sites-authoring/select-ui.md#switching-to-classic-ui-when-editing-a-page) UI中開啟如果管理員已 [啟用此選項](/help/sites-administering/enable-classic-ui-editor.md)

此外，**頁面資訊**&#x200B;可在適當時提供分析和建議的存取權。

## 頁面模式{#page-modes}

編輯頁面時有多種模式，允許執行不同的動作：

* [編輯](/help/sites-authoring/editing-content.md) -編輯頁面內容時使用的模式。
* [版面](/help/sites-authoring/responsive-layout.md) -可讓您根據裝置建立和編輯互動式版面（如果頁面是以版面容器為基礎）

* [Shapblare](/help/sites-authoring/scaffolding.md)  —— 協助您建立大量共用相同結構但內容不同的頁面。
* [開發人員](/help/sites-developing/developer-mode.md) -可讓您執行各種動作（需要權限）。這些檢查包括檢查頁面及其元件的技術詳細資訊。

* [Design](/help/sites-authoring/default-components-designmode.md)  —— 可讓您啟用／停用要用於頁面的元件，以及設定元件的設計(如果頁面是以靜態範本 [為基礎](/help/sites-authoring/templates.md#editable-and-static-templates))。

* [定位](/help/sites-authoring/content-targeting-touch.md) -透過跨所有通道的定位和測量來提高內容相關性。
* [Activity Map](/help/sites-authoring/page-analytics-using.md#analyticsvisiblefromthepageeditor) -顯示頁面的Analytics資料。

* [時間彎曲](/help/sites-authoring/working-with-page-versions.md#timewarp) -可讓您在特定時間點檢視頁面狀態。
* [即時副本狀態](/help/sites-authoring/editing-content.md#live-copy-status) -可快速概述即時副本狀態，以及哪些元件是／未繼承的。
* [預覽](/help/sites-authoring/editing-content.md#previewing-pages) -用於檢視頁面在發佈環境中的顯示效果；或在內容中使用連結進行導覽。

* [Annotate](/help/sites-authoring/annotations.md)  —— 用於在頁面上添加或查看批注。

您可以使用右上角的圖示來存取這些圖示。 實際圖示會變更，以反映您目前使用的模式：

![ateat-18](assets/ateat-18.png)

>[!NOTE]
>
>* 根據頁面的特性，某些模式可能無法使用。
>* 存取某些模式需要適當的權限／權限。
>* 由於空間限制，行動裝置無法使用開發人員模式。
>* 有一個鍵 [盤](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) ( `Ctrl-Shift-M`可切換 **)，在「預覽」和目前選取的模式之間切換(例如，「編輯」、「排版**********」等)。

>



## 路徑選擇{#path-selection}

通常在編寫時，需要選擇其他資源，例如定義到其他頁面或資源的連結或選擇映像。 為了輕鬆選擇路徑，[路徑欄位](/help/sites-authoring/author-environment-tools.md#path-fields)提供自動完成功能，而[路徑瀏覽器](/help/sites-authoring/author-environment-tools.md#path-browser)則提供更強穩的選擇。

### 路徑欄位{#path-fields}

這裡用來說明的範例是影像元件。 有關使用和編輯元件的詳細資訊，請參閱[ Components for Page Authoring](/help/sites-authoring/default-components.md)。

路徑欄位現在具有自動完成和前瞻功能，讓尋找資源變得更輕鬆。

按一下路徑欄位中的&#x200B;**開啟選擇對話框**&#x200B;按鈕可開啟路徑瀏覽器](/help/sites-authoring/author-environment-tools.md#path-browser)對話框，以提供更詳細的選擇選項。[

![](do-not-localize/screen_shot_2018-03-22at154427.png)

或者，您可以開始在路徑欄位中輸入，AEM並在輸入時提供相符的路徑。

![ateat-19](assets/ateat-19.png)

### 路徑瀏覽器 {#path-browser}

路徑瀏覽器的組織方式與站點控制台的[列視圖](/help/sites-authoring/basic-handling.md#column-view)類似，允許更詳細地選擇資源。

![screen_shot_2018-03-22at154521](assets/screen_shot_2018-03-22at154521.png)

* 在選擇資源後，對話框右上方的&#x200B;**選擇**&#x200B;按鈕將變為活動狀態。 按一下或點選以確認選擇，或&#x200B;**取消**&#x200B;中止。
* 如果上下文允許選擇多個資源，則選擇資源也會激活「選擇 **** 」按鈕，但也會向窗口的右上角添加選定資源的計數。按一下 **數字旁** 的X，取消選取全部。
* 在樹狀結構中導覽時，您的位置會反映在對話方塊頂端的階層連結中。 這些網站導覽路徑標示也可用來快速跳入資源階層。
* 您隨時都可以使用對話方塊頂端的搜尋欄位。 按一下搜尋欄位中的&#x200B;**X**&#x200B;以清除搜尋。
* 若要縮小搜尋範圍，您可以顯示篩選選項並根據特定路徑篩選結果。

   ![ateat-21](assets/ateat-21.png)

## 鍵盤快速鍵 {#keyboard-shortcuts}

有各種[鍵盤快速鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)可供使用。
