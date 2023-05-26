---
title: 製作 — AEM中的環境和工具
description: AEM的製作環境提供各種機制來組織和編輯您的內容。
uuid: 23a8aa93-b3d2-423b-b402-9e5f3f273d9a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f488ba79-5bda-46e9-9c15-9a8c3dbfa2ce
docset: aem65
exl-id: 3b3c118b-ca35-484b-a62e-7bec98953123
source-git-commit: bc1f0bd20804bbae78c7ea9a5209e183d6bbaaf3
workflow-type: tm+mt
source-wordcount: '2230'
ht-degree: 9%

---

# 製作 — 環境與工具{#authoring-the-environment-and-tools}

AEM的製作環境提供各種機制來組織和編輯您的內容。 提供的工具可從各種主控台和頁面編輯器存取。

## 管理您的網站 {#managing-your-site}

此 **網站** console可讓您使用標題列、工具列、動作圖示（適用於選取的資源）、階層連結，以及選取時的輔助導軌（例如時間軸和參考），來導覽和管理您的網站。

例如，欄檢視：

![ateat-01](assets/ateat-01.png)

## 編輯頁面內容 {#editing-page-content}

您可以使用頁面編輯器編輯頁面。 例如：

`https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

![ateat-02](assets/ateat-02.png)

>[!NOTE]
>
>第一次開啟頁面進行編輯時，系統會提供一系列投影片來導覽功能。
>
>您可以視需要略過導覽，並隨時透過選擇 **頁面資訊** 功能表。

## 存取說明 {#accessing-help}

編輯頁面時， **說明** 可從下列位置存取：

* 此 [**頁面資訊**](/help/sites-authoring/editing-page-properties.md#page-properties) 選擇器；這將顯示簡介幻燈片（在您第一次存取編輯器時顯示）。
* 此 [設定](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) 特定元件的對話方塊(使用？ 圖示)；這將顯示上下文相關說明。

進一步的 [說明相關資源可從主控台取得](/help/sites-authoring/basic-handling.md#accessing-help).

## 元件瀏覽器 {#components-browser}

元件瀏覽器會顯示可在目前頁面上使用的所有元件。 這些檔案可以拖曳至適當位置，然後編輯以新增您的內容。

元件瀏覽器是側面板中的標籤(連同資產 [瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser)[和內容樹](/help/sites-authoring/author-environment-tools.md#content-tree))。要開啟 (或關閉) 側面板，請使用工具欄左上角的表徵圖：

![ateat-03](assets/ateat-03.png)

當您開啟側面板時，它將從左側滑開(選取 **元件** 索引標籤（如有需要）。 開啟時，您可以瀏覽頁面可用的所有元件。

實際的外觀和處理方式取決於您使用的裝置型別：

>[!NOTE]
>
>當寬度小於1024畫素時會偵測到行動裝置。 小型案頭視窗亦可如此。

* **行動裝置(例如iPad)**

   元件瀏覽器會完整涵蓋正在編輯的頁面。

   若要新增元件至頁面，請按住所需元件並向右移動，元件瀏覽器將關閉並重新顯示頁面 — 您可以在此處放置元件。

   ![ateat-04](assets/ateat-04.png)

* **案頭裝置**

   元件瀏覽器會在視窗左側開啟。

   若要新增元件至頁面，請按一下所需元件，然後將其拖曳至所需位置。

   ![ateat-05](assets/ateat-05.png)

   元件表示方式：

   * 元件名稱
   * 元件群組（灰色）
   * 圖示或縮寫

      * 標準元件的圖示為單色。
      * 縮寫一律為元件名稱的前兩個字元。

   從頂部工具列中的 **元件** 瀏覽器您可以：

   * 依名稱篩選元件。
   * 使用下拉式選取範圍將顯示限製為特定群組。

   如需元件的詳細說明，您可以在「元件」瀏覽器中按一下或點選元件旁的資訊圖示(如果 **有** )。例如，對於「版面 **容器」**:

   ![ateat-06](assets/ateat-06.png)

   如需有關可用元件的詳細資訊，請參閱 [元件主控台](/help/sites-authoring/default-components-console.md).

## 資產瀏覽器 {#assets-browser}

資產瀏覽器會顯示全部 [資產](/help/assets/home.md) 直接在您目前頁面上使用。

資產瀏覽器是側面板中的標籤，以及 [元件瀏覽](/help/sites-authoring/author-environment-tools.md#components-browser)r和 [內容樹狀結構](/help/sites-authoring/author-environment-tools.md#content-tree). 要開啟或關閉側面板，請使用工具欄左上角的表徵圖：

![ateat-03-1](assets/ateat-03-1.png)

當您開啟側面板時，它將從左側滑開。 選取 **資產** 索引標籤進行標籤（如有必要）。

![ateat-07](assets/ateat-07.png)

當資產瀏覽器開啟時，您可以瀏覽頁面可用的所有資產。 如有需要，可使用無限捲動來展開清單。

![ateat-08](assets/ateat-08.png)

若要將資產新增至頁面，請選取並拖曳至所需位置。 這可以是：

* 適當型別的現有元件。

   * 例如，您可以將影像型別的資產拖曳至影像元件上。

* A [預留位置](/help/sites-authoring/editing-content.md#component-placeholder) 在段落系統中建立適當型別的新元件。

   * 例如，您可以將影像型別的資產拖曳至段落系統，以建立「影像」元件。

>[!NOTE]
>
>這適用於特定資產和元件型別。 另請參閱 [使用「資產瀏覽器」插入元件](/help/sites-authoring/editing-content.md#inserting-a-component-using-the-assets-browser) 以取得更多詳細資料。

從資產瀏覽器的頂端工具列，您可以依下列方式篩選資產：

* 名稱
* 路徑
* 資產型別，例如，影像、手稿、檔案、影片、頁面、段落和產品
* 資產特性，例如方向（縱向、橫向、正方形）和樣式（顏色、單色、灰階）

   * 僅適用於特定資產型別

實際的外觀和處理方式取決於您使用的裝置型別：

>[!NOTE]
>
>當寬度小於1024畫素時（亦即在小案頭視窗上）會偵測到行動裝置。

* **行動裝置，例如iPad**

   資產瀏覽器會完整涵蓋正在編輯的頁面。

   若要將資產新增至頁面，請觸控並按住所需資產，然後將其向右移動 — 資產瀏覽器將關閉並重新顯示頁面，您可以在其中將資產新增至所需元件。

   ![ateat-09](assets/ateat-09.png)

* **案頭裝置**

   資產瀏覽器會在視窗左側開啟。

   若要將資產新增至頁面，請按一下所需的資產，並將其拖曳至所需的元件或位置。

   ![ateat-10](assets/ateat-10.png)

如果您需要快速變更資產，可以開始 [資產編輯器](/help/assets/manage-assets.md) 直接從資產瀏覽器按一下資產名稱旁邊顯示的編輯圖示。

![](do-not-localize/screen_shot_2018-03-22at142448.png)

## 內容樹 {#content-tree}

此 **內容樹狀結構** 提供階層中頁面所有元件的概觀，讓您一眼就能看到頁面的構成方式。

內容樹狀結構是側面板中的標籤（連同元件和資產瀏覽器）。 要開啟 (或關閉) 側面板，請使用工具欄左上角的表徵圖：

![](do-not-localize/screen_shot_2018-03-22at142042.png)

當您開啟側面板時，它會滑開（從左側）。 選取 **內容樹狀結構** 索引標籤進行標籤（如有必要）。 開啟時，您可以看到頁面或範本的樹狀檢視表示法，因此更容易瞭解其內容如何以階層方式建構。 此外，在複雜頁面上，它可讓您更輕鬆地在頁面的元件之間跳轉。

![ateat-11](assets/ateat-11.png)

頁面可以輕鬆地由許多相同型別的元件組成，因此內容（元件）樹狀結構會在元件型別名稱（黑色）之後顯示描述性文字（灰色）。 描述性文字來自元件的常見屬性，例如標題或文字。

元件型別將以使用者語言顯示，而元件說明文字則來自頁面語言。

按一下元件旁的>形箭號將會收合或展開該層級。

![screen_shot_2018-03-22at142559](assets/screen_shot_2018-03-22at142559.png)

>[!NOTE]
>
>如果您在行動裝置上編輯頁面（如果瀏覽器寬度小於1024畫素），則無法使用內容樹狀結構。

按一下元件即可在頁面編輯器中反白顯示該元件。 可用的動作取決於頁面狀態：

* 例如，基本頁面：

   `https://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html`

   ![ateat-12](assets/ateat-12.png)

   如果您在樹狀結構中點選的元件可編輯，則名稱右側會出現扳手圖示。 按一下此圖示將直接啟動元件的編輯對話方塊。

   ![](do-not-localize/screen_shot_2018-03-22at142725.png)

* 或屬於的頁面 [即時副本](/help/sites-administering/msm.md)，其中元件繼承自其他頁面；例如：

   `https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

   ![ateat-13](assets/ateat-13.png)

## 片段 — 關聯的內容瀏覽器 {#fragments-associated-content-browser}

如果您的頁面包含內容片段，那麼您也可以存取 [相關內容的瀏覽器](/help/sites-authoring/content-fragments.md#using-associated-content).

## 引用 {#references}

**引用** 顯示所選頁面的連線：

* BluePrint
* 啟動
* 即時副本
* 語言副本
* 導入連結
* 參考元件的使用：借入和借出的內容
* 產品頁面的參考（從「商務 — 產品」主控台）

開啟所需的主控台，然後導覽至所需的資源並開啟 **引用** 使用：

![screen_shot_2018-03-22at153653](assets/screen_shot_2018-03-22at153653.png)

[選取您需要的資源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) 若要顯示與該資源相關的參照型別清單：

![ateat-22](assets/ateat-22.png)

選取適當的參照型別以取得詳細資訊。 在某些情況下，當您選取特定參照時，可以使用進一步的動作，包括：

* **傳入連結**，提供參照頁面的頁面清單，並可直接存取 **編輯** 選擇特定連結時顯示的其中一個頁面

* 借入和借出內容的例項，使用 **參考資料** 元件，您可以在此處導覽至參照/參照的頁面

* [產品頁面的參考](/help/commerce/cif-classic/administering/generic.md#showing-product-references) （可從Commerce-Products控制檯取得）
* [啟動](/help/sites-authoring/launches.md)，提供相關啟動項的存取權
* [即時副本](/help/sites-administering/msm.md) 顯示基於所選資源的所有即時副本的路徑。
* [Blueprint](/help/sites-administering/msm-best-practices.md)，提供詳細資訊和各種動作
* [語言副本](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel)，提供詳細資訊和各種動作

例如，您可以修正「參照」元件中的破斷參照：

![ateat-14](assets/ateat-14.png)

## 事件 — 時間表 {#events-timeline}

以取得適當的資源(例如 **網站** 控制檯或資產 **資產** console) [時間軸可用來顯示任何選取專案的最近活動](/help/sites-authoring/basic-handling.md#timeline).

開啟所需的主控台，然後導覽至所需的資源並開啟 **時間表**，使用：

![ateat-15](assets/ateat-15.png)

[選取您需要的資源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)，然後執行以下任一項作業 **全部顯示** 或 **活動** 若要列出所選資源上任何最近的動作：

![ateat-16](assets/ateat-16.png)

## 頁面資訊 {#page-information}

「頁面資訊」按鈕（均衡器圖示）會開啟一個功能表，其中也提供上次編輯和上次發佈的詳細資訊。 視頁面、其網站和您的例項的特性而定，可能有更多或更少的選項可用：

![ateat-17](assets/ateat-17.png)

* [開啟屬性](/help/sites-authoring/editing-page-properties.md)
* [轉出頁面](/help/sites-administering/msm.md#msm-from-the-ui)
* [啟動工作流程](/help/sites-authoring/workflows-applying.md#starting-a-workflow-from-the-page-editor)
* [鎖定頁面](/help/sites-authoring/editing-content.md#locking-a-page)
* [發佈頁面](/help/sites-authoring/publishing-pages.md#main-pars-title-10)
* [取消發佈頁面](/help/sites-authoring/publishing-pages.md#main-pars-title-5)
* [編輯範本](/help/sites-authoring/templates.md)；當頁面根據 [可編輯的範本](/help/sites-authoring/templates.md#editable-and-static-templates)

* [以已發佈狀態檢視](/help/sites-authoring/editing-content.md#view-as-published)
* 在Admin中檢視；在 [網站主控台](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)
* [說明](/help/sites-authoring/basic-handling.md#accessing-help)

例如，適當時， **頁面資訊** 也有選項：

* [提升啟動](/help/sites-authoring/launches-promoting.md) 如果頁面為啟動項。
* [在傳統UI中開啟](/help/sites-authoring/select-ui.md#switching-to-classic-ui-when-editing-a-page) 如果此選項已 [由管理員啟用](/help/sites-administering/enable-classic-ui-editor.md)

此外， **頁面資訊** 可讓您在適當時存取analytics和建議。

## 頁面模式 {#page-modes}

編輯頁面時，有多種模式可允許不同的動作：

* [編輯](/help/sites-authoring/editing-content.md)  — 編輯頁面內容時使用的模式。
* [版面](/help/sites-authoring/responsive-layout.md)  — 可讓您根據裝置建立及編輯回應式配置（如果頁面根據配置容器）

* [支架](/help/sites-authoring/scaffolding.md)  — 協助您建立共用相同結構但內容不同的大型頁面集。
* [開發人員](/help/sites-developing/developer-mode.md)  — 可讓您執行各種動作（需要許可權）。 其中包括檢查頁面及其元件的技術細節。

* [設計](/help/sites-authoring/default-components-designmode.md)  — 可讓您啟用/停用頁面上使用的元件，並設定元件的設計(如果頁面根據 [靜態範本](/help/sites-authoring/templates.md#editable-and-static-templates))。

* [目標定位](/help/sites-authoring/content-targeting-touch.md)  — 透過所有管道的目標定位和測量，提高內容關聯性。
* [Activity Map](/help/sites-authoring/page-analytics-using.md#analyticsvisiblefromthepageeditor)  — 顯示頁面的Analytics資料。

* [時間扭曲](/help/sites-authoring/working-with-page-versions.md#timewarp)  — 可讓您檢視特定時間點的頁面狀態。
* [即時副本狀態](/help/sites-authoring/editing-content.md#live-copy-status)  — 可讓您快速概覽即時副本狀態以及不會繼承哪些元件。
* [預覽](/help/sites-authoring/editing-content.md#previewing-pages)  — 用於檢視將在發佈環境中顯示的頁面；或使用內容中的連結導覽。

* [註釋](/help/sites-authoring/annotations.md)  — 用於在頁面上新增或檢視註解。

您可以使用右上角的圖示來存取這些專案。 實際圖示會變更，以反映您目前使用的模式：

![ateat-18](assets/ateat-18.png)

>[!NOTE]
>
>* 視頁面特性而定，某些模式可能無法使用。
>* 存取某些模式需要適當的許可權。
>* 由於空間限制，開發人員模式不適用於行動裝置。
>* 有一個鍵 [盤](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) ( `Ctrl-Shift-M`可切換 **)，在「預覽」和目前選取的模式之間切換(例如，「編輯」、「排版**********」等)。
>


## 路徑選擇 {#path-selection}

通常在製作時，需要選取其他資源，例如定義指向其他頁面或資源的連結，或選取影像時。 若要輕鬆選取路徑， [路徑欄位](/help/sites-authoring/author-environment-tools.md#path-fields) 優惠自動完成和 [路徑瀏覽器](/help/sites-authoring/author-environment-tools.md#path-browser) 允許更強大的選擇。

### 路徑欄位 {#path-fields}

此處用來說明的範例是影像元件。 如需使用和編輯元件的詳細資訊，請參閱 [用於頁面編寫的元件](/help/sites-authoring/default-components.md).

路徑欄位現在具有自動完成和先行等功能，可更輕鬆找到資源。

按一下 **開啟選取範圍對話方塊** 路徑欄位中的按鈕會開啟 [路徑瀏覽器](/help/sites-authoring/author-environment-tools.md#path-browser) 對話方塊，以取得更詳細的選取選項。

![](do-not-localize/screen_shot_2018-03-22at154427.png)

或者，您可以開始在路徑欄位中輸入，AEM會在您輸入時提供相符的路徑。

![ateat-19](assets/ateat-19.png)

### 路徑瀏覽器 {#path-browser}

路徑瀏覽器的組織方式如下 [欄檢視](/help/sites-authoring/basic-handling.md#column-view) ，以取得更詳細的資源選擇。

![screen_shot_2018-03-22at154521](assets/screen_shot_2018-03-22at154521.png)

* 選取資源後， **選取** 對話方塊右上角的按鈕會變成使用中。 按一下或點選以確認選取範圍或 **取消** 以中止。
* 如果上下文允許選擇多個資源，則選擇資源也會激活「選擇 **** 」按鈕，但也會向窗口的右上角添加選定資源的計數。按一下 **數字旁** 的X，取消選取全部。
* 當您瀏覽樹狀結構時，您的位置會反映在對話方塊頂端的階層連結中。 這些階層連結也可用來在資源階層內快速跳轉。
* 您可以隨時使用對話方塊頂端的搜尋欄位。 按一下 **X** 以清除搜尋。
* 若要縮小搜尋範圍，您可以顯示篩選選項並根據特定路徑篩選結果。

   ![ateat-21](assets/ateat-21.png)

## 鍵盤快速鍵 {#keyboard-shortcuts}

各種 [鍵盤快速鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) 可用。
