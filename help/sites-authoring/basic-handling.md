---
title: 使用AEM作者環境時的基本處理
description: 熟悉如何導覽AEM及其基本用法
uuid: c78ef9da-e0bd-47be-a410-9cf2ae71749a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 21181a6f-b434-40ed-8eb1-ebdfc98964dd
docset: aem65
exl-id: ef1a3997-feb4-4cb0-9396-c8335b69bb10
source-git-commit: d045fc1ac408f992d594a4cb68d1c4eeae2b0de1
workflow-type: tm+mt
source-wordcount: '3024'
ht-degree: 7%

---

# 基本處理{#basic-handling}

>[!NOTE]
>
>* 此頁面旨在概述使用AEM製作環境時的基本處理方式。 它會使用 **網站** 以主控台為基礎。
>
>* 部分功能並未在所有主控台中提供，而其他功能可能也在某些主控台中提供。 有關個別主控台及其相關功能的特定資訊，將在其他頁面上詳細說明。
>* 在整個AEM環境中都可以使用鍵盤快速鍵。 尤其是當 [使用主控台](/help/sites-authoring/keyboard-shortcuts.md) 和 [編輯頁面](/help/sites-authoring/page-authoring-keyboard-shortcuts.md).
>

## 快速入門 {#getting-started}

### 觸控式UI {#a-touch-enabled-ui}

AEM使用者介面已啟用觸控功能。 觸控式介面可讓您使用觸控功能，透過點選、觸控並按住及撥動等手勢與軟體互動。 這與傳統案頭介面使用滑鼠動作（例如按一下、連按兩下、按一下滑鼠右鍵和滑鼠懸停滑鼠）的操作方式相反。

由於AEM UI支援觸控功能，因此您可以在觸控裝置（例如行動裝置或平板電腦）上使用觸控手勢，並在傳統桌上型裝置上使用滑鼠動作。

### 首要步驟 {#first-steps}

登入後立即到達 [導覽面板](#navigation-panel). 選取其中一個選項會開啟相應的主控台。

![導覽](assets/bh-01.png)

>[!NOTE]
>
>為了更清楚瞭解AEM的基本用法，本檔案以 **網站** 主控台。
>
>按一下或點選 **網站** 以開始使用。

### 產品導覽 {#product-navigation}

每當使用者首次存取主控台時，就會啟動產品導覽教學課程。 請花一分鐘時間按一下或點選，以取得AEM基本處理的良好概觀。

![產品導覽](assets/bh-02.png)

按一下或點選 **下一個** 以進入概覽的下一頁。 按一下或點選 **關閉** 或按一下或點選「概述」對話方塊外部以關閉。

除非您檢視所有投影片或核取選項，否則概觀會在您下次存取主控台時重新啟動 **不要再顯示**.

## 全域導覽 {#global-navigation}

您可以使用全域導覽面板在主控台之間導覽。 當您按一下或點選畫面左上方的Adobe Experience Manager連結時，就會以全熒幕下拉式清單的形式觸發此動作。

您可以按一下或點選以關閉全域導覽面板 **關閉** 以返回您先前所在的位置。

![全域導覽](assets/bh-03.png)

>[!NOTE]
>
>第一次登入時，您會看到 **導覽** 面板。

全域導覽有兩個面板，由畫面左邊緣的圖示表示：

* **[導覽](/help/sites-authoring/basic-handling.md#navigation-panel)**  — 以指南針表示
* **[工具](/help/sites-authoring/basic-handling.md#tools-panel)**  — 以槌子表示

這些面板上可用的選項說明如下。

### 導覽面板 {#navigation-panel}

「導覽」面板可讓您存取AEM主控台：

![導覽](assets/bh-01.png)

當您瀏覽控制檯和內容時，瀏覽器索引標籤的標題將會更新以反映您的位置。

在「導覽」中，可用的主控台有：

<table>
 <tbody>
  <tr>
   <td><strong>主控台</strong></td>
   <td><strong>用途</strong></td>
  </tr>
  <tr>
   <td>資產<br /> </td>
   <td>這些主控台可讓您匯入和 <a href="/help/assets/home.md">管理數位資產</a> 例如影像、影片、檔案和音訊檔案。 然後這些資產便可由同一AEM執行個體上執行的任何網站使用。 </td>
  </tr>
  <tr>
   <td>社群</td>
   <td>此主控台可讓您建立和管理 <a href="/help/communities/sites-console.md">社群網站</a> 的 <a href="/help/communities/overview.md#engagement-community">參與</a> 和 <a href="/help/communities/overview.md#enablement-community">啟用</a>.</td>
  </tr>
  <tr>
   <td>商務</td>
   <td>這可讓您管理與您的相關產品、產品目錄和訂單 <a href="/help/commerce/cif-classic/administering/ecommerce.md">商務</a> 網站。</td>
  </tr>
  <tr>
   <td>體驗片段</td>
   <td>一個 <a href="/help/sites-authoring/experience-fragments.md">體驗片段</a> 是獨立的體驗，可以跨管道重複使用，也可以有變數，省去重複複製和貼上體驗或體驗片段的麻煩。</td>
  </tr>
  <tr>
   <td>Forms</td>
   <td>此主控台可讓您建立、管理及處理 <a href="/help/forms/home.md">表單和檔案</a>.</td>
  </tr>
  <tr>
   <td>個人化</td>
   <td>此主控台提供 <a href="/help/sites-authoring/personalization.md">用於編寫目標內容和呈現個人化體驗的工具架構</a>.</td>
  </tr>
  <tr>
   <td>專案</td>
   <td>此 <a href="/help/sites-authoring/touch-ui-managing-projects.md">專案主控台可讓您直接存取專案</a>. 專案是虛擬儀表板。 它們可用於建立團隊，然後授予該團隊存取資源、工作流程和任務的許可權，允許人員致力於共同目標。 <br /> </td>
  </tr>
  <tr>
   <td>Screens</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/authoring/setting-up-projects/creating-a-screens-project.html">Screens</a> 可讓您管理所有對外畫面，不管是任何大小、在任何位置。</td>
  </tr>
  <tr>
   <td>Sites</td>
   <td>Sites主控台可讓您 <a href="/help/sites-authoring/page-authoring.md">建立、檢視及管理網站</a> 在您的AEM執行個體上執行。 透過這些主控台，您可以建立、編輯、複製、移動和刪除網站頁面、開始工作流程以及發佈頁面。<br /> </td>
  </tr>
 </tbody>
</table>

### 工具面板 {#tools-panel}

在「工具」面板中，側面板中的每個選項都包含一系列子選單。 此 [工具主控台](/help/sites-administering/tools-consoles.md) 您可以在此處存取許多專用工具和控制檯，協助您管理網站、數位資產和內容存放庫的其他方面。

![「工具」面板](assets/bh-04.png)

## 標頭 {#the-header}

 標頭會始終顯示在畫面頂端。雖然無論您在系統中的何處，標頭中的大部分選項都保持不變，但有些選項是上下文特定的。

![頁首](assets/bh-03.png)

* [全域導覽](#navigatingconsolesandtools)

  選取 **Adobe Experience Manager** 連結可在主控台之間導覽。

  ![Adobe Experience Manager連結](assets/screen_shot_2018-03-23at103615.png)

* [搜尋](/help/sites-authoring/search.md)

  ![搜尋](do-not-localize/screen_shot_2018-03-23at103542.png)

  您也可以使用 [快速鍵](/help/sites-authoring/keyboard-shortcuts.md) `/` （正斜線）以從任何主控台叫用搜尋。

* [解決方案](https://www.adobe.com/experience-cloud.html)

  ![解決方案](do-not-localize/screen_shot_2018-03-23at103552.png)

* [說明](#accessinghelptouchoptimizedui)

  ![說明](do-not-localize/screen_shot_2018-03-23at103547.png)

* [通知](/help/sites-authoring/inbox.md)

  ![通知](do-not-localize/screen_shot_2018-03-23at103558.png)

  此圖示將標有目前已分配的未完成通知數目。

  >[!NOTE]
  >
  >現成可用的AEM會預先載入指派給管理員使用者群組的管理任務。 另請參閱 [您的收件匣 — 立即可用的管理工作](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks) 以取得詳細資訊。

* [使用者屬性](/help/sites-authoring/user-properties.md)

  ![使用者屬性](do-not-localize/screen_shot_2018-03-23at103603.png)

* [邊欄選擇器](/help/sites-authoring/basic-handling.md#rail-selector)

  ![Adobe Experience Manager畫面左側顯示的邊欄選擇器清單。](do-not-localize/screen_shot_2018-03-23at103943.png)

  顯示的選項取決於您目前的主控台。 例如，在 **網站** 您可以選取「僅限內容」（預設值）、「時間軸」、「參照」或「篩選器」側面板。

  ![邊欄選擇器](assets/screen_shot_2018-03-23at104029.png)

* 階層連結

  ![階層連結](assets/bh-05.png)

  階層連結位於邊欄中間，且一律顯示目前所選專案的說明，可讓您在特定主控台內導覽。 在Sites主控台中，您可以瀏覽網站的各個層級。

  只要按一下階層連結文字，即可顯示下拉式清單，列出目前所選專案的階層層次。 按一下專案以跳至該位置。

  ![階層層級](assets/bh-06.png)

* Analytics時段選擇

  ![Analytics時段](assets/screen_shot_2018-03-23at104126.png)

  這僅在清單檢視中可用。 另請參閱 [清單檢視](#list-view) 以取得詳細資訊。

* **建立** 按鈕

  ![建立](assets/screen_shot_2018-03-23at104301.png)

  按一下後，顯示的選項即適用於主控台/前後關聯。

* [檢視](/help/sites-authoring/basic-handling.md#viewingandselectingyourresourcescardlistcolumn)

  檢檢視示位於AEM工具列的最右側。 由於它也會指出目前檢視，因此會變更。 例如，在預設檢視中， **欄檢視** 它顯示：

  ![欄檢視](assets/bh-07.png)

  您可以在欄檢視、卡片檢視和清單檢視之間切換；在清單檢視中，它也會顯示檢視設定。

  ![切換檢視](assets/bh-09.png)

* 鍵盤導覽

  您僅能使用鍵盤導覽網站。 這會使用的標準瀏覽器功能 **標籤** 金鑰(或 **OPT+TAB**)，將您移動至頁面上 *可聚焦*.

  在 **網站** 主控台新增選項至  **跳至主要內容**. 當您看到時，它就會變得可見 *標籤* 透過「 」標頭選項，可讓您略過（產品）工具列中的標準元素，並直接前往主要內容，以加速導覽。

  ![跳至主要內容](assets/bh-30.png)

## 存取說明 {#accessing-help}

有多種可用的說明資源：

* **主控台工具列**

  根據您的位置 **說明** 圖示會開啟適當的資源：

  ![主控台工具列](assets/bh-10.png)

* **導覽**

  第一次瀏覽系統時， [一系列投影片介紹AEM導覽](/help/sites-authoring/basic-handling.md#product-navigation).

* **頁面編輯器**

  第一次編輯頁面時，系統會以一系列投影片來介紹頁面編輯器。

  ![頁面編輯器](assets/bh-11.png)

  依照您的指示瀏覽此概觀 [產品導覽概觀](/help/sites-authoring/basic-handling.md#product-navigation) 第一次存取任何主控台時。

  從 [**頁面資訊** 您可選取的功能表 **說明**](/help/sites-authoring/author-environment-tools.md#accessing-help) 以隨時再次顯示。

* **工具主控台**

  從 **工具** 主控台您也可以存取外部 **資源**：

   * **檔案**
檢視網站體驗管理檔案

   * **開發人員資源**
開發人員資源和下載

  >[!NOTE]
  >
  >您可以隨時使用快速鍵來存取可用快速鍵的概觀 `?` （問號）在主控台中。
  >
  >如需所有鍵盤快速鍵的概觀，請參閱下列檔案：
  >
  >* [用於編輯頁面的鍵盤快速鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
  >* [主控台的鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md)

## 動作工具列 {#actions-toolbar}

每當選取資源（例如頁面或資產）時，工具列中都會有附有說明文字的圖示來指示各種動作。 這些動作相依於：

* 目前的主控台。
* 目前內容。
* 無論您是否在 [選擇模式](#navigatingandselectionmode).

工具列中的可用動作會變更，以反映您可對所選特定專案執行的動作。

您如何進行 [選取資源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) 視檢視而定。

由於某些視窗的空間限制，工具列可能會很快變得比可用的空間長。發生此情況時，會出現其他選項。按一下或點選省略號(三個點或…… ****)會開啟一個下拉式選取器，其中包含所有剩餘的動作。例如，在Sites主控台中選取頁面 **後** :

![動作工具列](assets/bh-12.png)

>[!NOTE]
>
>可用的個別圖示會記錄為與適當的主控台/功能/情境相關。

## 快速動作 {#quick-actions}

在 [卡片檢視](#cardviewquickactions) 某些動作會以快速動作圖示的形式呈現，同時也會出現在工具列上。 快速動作圖示一次只適用於一個專案，您不需要預先選取。

當您將滑鼠懸停在資源卡上（案頭裝置）時，可以看到快速動作。 可用的快速動作取決於主控台和內容。 例如，以下為中頁面的快速動作 **網站** 主控台：

![快速動作](assets/bh-13.png)

## 檢視和選擇資源 {#viewing-and-selecting-resources}

檢視、導覽和選取在概念上所有檢視都相同，但根據您使用的檢視，處理方式略有不同。

您可以使用任何可用檢視來檢視、導覽及選取（以採取進一步動作）您的資源，您可以透過右上角的圖示來選取每個檢視：

* [欄檢視](#column-view)
* [卡片檢視](#card-view)

* [清單檢視](#list-view)

>[!NOTE]
>
>依預設，AEM Assets不會在任何檢視中將資產的原始轉譯顯示為縮圖。 如果您是管理員，則可以使用覆蓋圖來設定AEM Assets，以將原始轉譯顯示為縮圖。

### 選取資源 {#selecting-resources}

選取特定資源取決於檢視和裝置的組合：

<table>
 <tbody>
  <tr>
   <td> </td>
   <td>選擇</td>
   <td>取消選取</td>
  </tr>
  <tr>
   <td>欄檢視<br /> </td>
   <td>
    <ul>
     <li>案頭：<br /> 按一下縮圖</li>
     <li>行動裝置：<br /> 點選縮圖</li>
    </ul> </td>
   <td>
    <ul>
     <li>案頭：<br /> 按一下縮圖</li>
     <li>行動裝置：<br /> 點選縮圖</li>
    </ul> </td>
  </tr>
  <tr>
   <td>卡片檢視<br /> </td>
   <td>
    <ul>
     <li>案頭：<br /> 滑鼠懸停，然後使用核取記號快速動作</li>
     <li>行動裝置：<br /> 點選並按住卡片</li>
    </ul> </td>
   <td>
    <ul>
     <li>案頭：<br /> 按一下卡片</li>
     <li>行動裝置：<br /> 點選卡片</li>
    </ul> </td>
  </tr>
  <tr>
   <td>清單檢視</td>
   <td>
    <ul>
     <li>案頭：<br /> 按一下縮圖</li>
     <li>行動裝置：<br /> 點選縮圖</li>
    </ul> </td>
   <td>
    <ul>
     <li>案頭：<br /> 按一下縮圖</li>
     <li>行動裝置：<br /> 點選縮圖</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### 全選 {#select-all}

您可以按一下「 」，選取任何檢視中的所有專案 **全選** 選項。

* 在 **卡片檢視** 已選取所有卡片。
* 在 **清單檢視** 選取清單中的所有專案。
* 在 **欄檢視** 會選取最左側欄中的所有專案。

![全選](assets/screen-shot_2019-03-05at094659.png)

#### 取消全選 {#deselecting-all}

在任何情況下，當您選取專案時，選取專案的計數都會顯示在工具列的右上方。

您可以透過以下任一方式取消選取所有專案並退出選取模式：

* 按一下或點選 **X** 在計數旁邊，

* 或使用 **逸出**.

![取消選取](assets/bh-14.png)

在所有檢視中，如果您使用案頭裝置，只要點選鍵盤上的Esc鍵，即可選取所有專案。

#### 選取範例 {#selecting-example}

1. 例如在卡片檢視中：

   ![選取 — 卡片檢視](assets/bh-15.png)

1. 選取資源後，頂端標題會由 [動作工具列](#actionstoolbar) 提供目前適用於所選資源的動作的存取權。

   若要結束選取模式，請選取 **X** 右上方，或使用 **逸出**.

### 欄檢視 {#column-view}

![欄檢視](assets/bh-16.png)

欄檢視允許透過一系列階層式欄對內容樹進行視覺導覽。 此檢視可讓您視覺化並周遊網站的樹狀結構。

在最左邊的欄中選取資源，會在右邊的欄中顯示子資源。 在右側欄中選取資源後，會在右側的其他欄中顯示子資源，依此類推。

* 您可以點選或按一下資源名稱或資源名稱右側的>形箭號，在樹狀結構中向上和向下導覽。

   * 點選或按一下時，資源名稱和V形符號會反白顯示。

     ![欄檢視](assets/bh-17.png)

   * 已點按/已點按資源的子項會顯示在已點按/已點按資源右側的欄中。
   * 如果您點選或按一下沒有子系的資源名稱，其詳細資訊將顯示在最後一欄。

* 點選或按一下縮圖可選取資源。

   * 選取時，縮圖上將會覆蓋核取記號，並且資源名稱也會反白顯示。
   * 所選資源的詳細資訊將顯示在最後一欄。
   * 動作工具列將變為可用。

     ![欄檢視](assets/bh-18.png)

  在欄檢視中選取頁面時，選取的頁面會連同下列詳細資訊顯示在最終欄中：

   * 頁面標題
   * 頁面名稱（頁面URL的一部分）
   * 頁面所依據的範本
   * 修改詳細資料
   * 頁面語言
   * 出版物詳細資料

### 卡片檢視 {#card-view}

![bh-15-1](assets/bh-15-1.png)

* 卡片檢視會顯示目前層級中每個專案的資訊卡片。 這些會提供下列資訊：

   * 頁面內容的視覺化表示法。
   * 頁面標題。
   * 重要日期（例如上次編輯、上次發佈）。
   * 如果頁面已鎖定、隱藏或是LiveCopy的一部分。
   * 適當時，您何時需要在工作流程中採取動作。

      * 指出所需動作的標籤，可能與 [收件匣](/help/sites-authoring/inbox.md).

* [快速動作](#quick-actions) 也可以在此檢視中使用，例如選取和常見動作，例如編輯。

  ![卡片檢視 — 快速動作](assets/bh-13-1.png)

* 您可以點選/按一下卡片來向下瀏覽樹狀結構（注意避免快速動作），或使用 [標題中的階層連結](/help/sites-authoring/basic-handling.md#the-header).

### 清單檢視 {#list-view}

![清單檢視](assets/bh-19.png)

* 清單檢視會列出目前層級中每個資源的資訊。
* 您可以點選/按一下資源名稱，在樹狀結構中向下導覽，然後使用 [標題中的階層連結](/help/sites-authoring/basic-handling.md#the-header).

* 若要輕鬆選取清單中的所有專案，請使用清單左上方的核取方塊。

  ![清單檢視 — 全選](assets/bh-20.png)

   * 選取清單中的所有專案時，此核取方塊會顯示為已核取。

      * 按一下或點選核取方塊以取消選取全部。

   * 僅選取部分專案時，會出現減號。

      * 按一下或點選核取方塊以選取全部。
      * 再次按一下或點選核取方塊以取消全選。

* 使用以下專案選取要顯示的欄 **檢視設定** 選項位於「檢視」按鈕下。 下列欄可供顯示：

   * **名稱**  — 頁面名稱，在多語言撰寫環境中相當實用，因為它是頁面URL的一部分，無論使用何種語言，都不會變更
   * **修改時間**  — 上次修改日期和上次修改者
   * **已發佈**  — 發佈狀態
   * **範本**  — 頁面所依據的範本
   * **工作流程**  — 目前套用至頁面的工作流程。 當您滑鼠懸停或開啟時間軸時，會提供詳細資訊。

   * **頁面分析**
   * **不重複訪客**
   * **頁面逗留時間**

  ![檢視設定 — 設定欄](assets/bh-21.png)

  根據預設 **名稱** 欄隨即顯示，它構成了頁面URL的一部分。 在某些情況下，作者可能需要存取不同語言的頁面，如果作者不知道頁面的語言，檢視頁面名稱（通常不會變更）會很有幫助。

* 使用清單中每個專案最右側的點狀垂直列，變更專案的順序。

  >[!NOTE]
  >
  >變更順序僅適用於具有下列條件的已排序資料夾： `jcr:primaryType` value as `sling:OrderedFolder`.

  ![變更順序](assets/bh-22.png)

  在垂直選取列上按一下或點選，然後將專案拖曳至清單中的新位置。

  ![變更順序 — 拖曳](assets/bh-23.png)

* 您可以使用「 」顯示適當的欄，以顯示Analytics資料。 **檢視設定** 對話方塊。

  您可以使用標頭右側的篩選選項來篩選過去30、90或365天的Analytics資料。

  ![分析](assets/bh-24.png)

## 邊欄選擇器 {#rail-selector}

此 **邊欄選擇器** 可在視窗左上角取得，並根據您目前的主控台顯示選項。

![邊欄選擇器](assets/bh-25.png)

例如，在Sites中，您可以選取「僅限內容」（預設）、「內容樹」、「時間軸」、「參照」或「篩選器」側面板。

如果選取「僅限內容」，則只會出現邊欄圖示。 選取任何其他選項時，選項名稱會出現在邊欄圖示旁邊。

>[!NOTE]
>
>[鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md) 可用來快速切換邊欄顯示選項。

### 內容樹 {#content-tree}

內容樹狀結構可用來快速導覽側面板中的網站階層，以及檢視目前資料夾中頁面的許多相關資訊。

使用內容樹側面板搭配清單檢視或卡片檢視，使用者可以輕鬆檢視專案的階層結構，並使用內容樹側面板輕鬆瀏覽內容結構，以及在清單檢視中檢視詳細的頁面資訊。

![內容樹](assets/bh-26.png)

>[!NOTE]
>
>選取階層檢視中的專案後，可使用方向鍵來快速瀏覽階層。
>
>請參閱 [鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md) 以取得詳細資訊。

### 時間軸 {#timeline}

時間軸可用於檢視和/或啟動所選資源上已發生的事件。 若要開啟時間軸欄，請使用邊欄選取器：

時間軸欄可讓您：

* [檢視各種事件](#timelineviewevents) 與選取專案相關。

   * 您可以從下拉式清單中選取事件型別：

      * [評論](#timelineaddingandviewingcomments)
      * 註解
      * 活動
      * [Launch](/help/sites-authoring/launches.md)
      * [版本](/help/sites-authoring/working-with-page-versions.md)
      * [工作流程](/help/sites-authoring/workflows-applying.md)

         * 但以下各項除外 [暫時性工作流程](/help/sites-developing/workflows.md#transient-workflows) 因為沒有儲存這些專案的歷史記錄資訊

      * 和全部顯示

* [新增/檢視有關所選項目的註解。](#timelineaddingandviewingcomments)「注 **釋** 」方塊會顯示在事件清單的底部。鍵入注釋後跟Return將註冊注釋。當選取「注 **釋** 」或「 **全部顯示** 」時顯示。

* 特定的主控台具有其他功能。 例如，在Sites主控台中，您可以：

   * [儲存版本](/help/sites-authoring/working-with-page-versions.md#creatinganewversiontouchoptimizedui).
   * [啟動工作流程](/help/sites-authoring/workflows-applying.md#startingaworkflowfromtherail).

這些選項可透過 **註解** 欄位。

![時間軸](assets/bh-27.png)

### 引用 {#references}

**引用** 顯示所選資源的任何連線。 例如，在 **網站** 主控台 [引用](/help/sites-authoring/author-environment-tools.md#showingpagereferences) 若為頁面，則顯示：

* [Launch](/help/sites-authoring/launches.md#launches-in-references-sites-console)
* [即時副本](/help/sites-administering/msm-livecopy-overview.md#openingthelivecopyoverviewfromreferences)
* [語言副本](/help/sites-administering/tc-prep.md#seeing-the-status-of-language-roots)
* 內容參考：

   * 從其他頁面連結至所選頁面的連結
   * 參考元件在所選頁面中借用的內容和/或借出的內容

![bh-28](assets/bh-28.png)

### 篩選 {#filter}

這將會開啟一個面板，類似於 [搜尋](/help/sites-authoring/search.md) 已設定適當的位置篩選器，可讓您進一步篩選您要檢視的內容。

![篩選](assets/bh-29.png)
