---
title: 基本處理
seo-title: 基本處理
description: 熟悉如何導覽AEM及其基本用途
seo-description: 熟悉如何導覽AEM及其基本用途
uuid: c78ef9da-e0bd-47be-a410-9cf2ae71749a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 21181a6f-b434-40ed-8eb1-ebdfc98964dd
docset: aem65
exl-id: ef1a3997-feb4-4cb0-9396-c8335b69bb10
source-git-commit: 440aa5a2f4a020a16104f11eaf484a2cf7291e1f
workflow-type: tm+mt
source-wordcount: '2980'
ht-degree: 5%

---

# 基本處理{#basic-handling}

>[!NOTE]
>
>* 本頁旨在概述使用AEM製作環境時的基本處理方式。 它以&#x200B;**Sites**&#x200B;控制台為基礎。
   >
   >
* 並非所有主控台都提供某些功能，某些主控台可能提供其他功能。 有關個別主控台及其相關功能的特定資訊，將在其他頁面上詳細說明。
>* AEM提供鍵盤快速鍵。 尤其是當[使用主控台](/help/sites-authoring/keyboard-shortcuts.md)和[編輯頁面](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)時。

>



## 快速入門 {#getting-started}

### 觸控式UI {#a-touch-enabled-ui}

AEM使用者介面已啟用觸控功能。 觸控式介面可讓您使用觸控功能，透過點選、觸控並按住和滑動等手勢與軟體互動。 這與傳統的案頭介面操作滑鼠操作（如按一下、按兩下、按一下右鍵和滑鼠）的方式不同。

由於AEM UI為觸控式，因此您可以在觸控裝置（例如行動裝置或平板電腦）上使用觸控手勢，以及在傳統案頭裝置上使用滑鼠動作。

### 第一步{#first-steps}

登入後，您會立即進入[導覽面板](#navigation-panel)。 選取其中一個選項會開啟個別主控台。

![bh-01](assets/bh-01.png)

>[!NOTE]
>
>為了充分了解AEM的基本使用，本檔案以&#x200B;**Sites**&#x200B;主控台為基礎。
>
>按一下或點選&#x200B;**Sites**&#x200B;以開始使用。

### 產品導覽 {#product-navigation}

每當使用者首次存取主控台時，就會啟動產品導覽教學課程。 點選或點進需要一分鐘的時間，即可取得AEM基本處理方式的完整概觀。

![bh-02](assets/bh-02.png)

按一下或點選「**Next** 」以前往概觀的下一頁。 按一下或點選「**關閉**」，或按一下或點選「概觀」對話方塊外部以關閉。

除非您查看所有幻燈片，或選中「**不再顯示**」選項，否則概覽將在下次訪問控制台時重新啟動。

## 全局導航{#global-navigation}

您可以使用全域導覽面板，在主控台之間導覽。 當您按一下或點選畫面左上角的Adobe Experience Manager連結，就會以全螢幕下拉式清單觸發。

您可以按一下或點選&#x200B;**Close**&#x200B;以關閉全域導覽面板，以返回您的上一個位置。

![bh-05](assets/bh-03.png)

>[!NOTE]
>
>首次登入時，您會顯示「**導覽**」面板。

全域導覽有兩個面板，由螢幕左邊界的圖示表示：

* **[導航](/help/sites-authoring/basic-handling.md#navigation-panel)**  — 用羅盤表示
* **[工具](/help/sites-authoring/basic-handling.md#tools-panel)**  — 用錘子表示

以下說明這些面板上可用的選項。

### 導航面板{#navigation-panel}

「導覽」面板可讓您存取AEM主控台：

![bh-01](assets/bh-01.png)

瀏覽器標籤的標題將會更新，以反映您在主控台和內容中導覽時的位置。

在導覽中，可用的主控台包括：

<table>
 <tbody>
  <tr>
   <td><strong>主控台</strong></td>
   <td><strong>用途</strong></td>
  </tr>
  <tr>
   <td>資產<br /> </td>
   <td>這些主控台可讓您匯入和<a href="/help/assets/home.md">管理數位資產</a>，例如影像、視訊、檔案和音訊檔案。 然後，在相同AEM例項上執行的任何網站都可以使用這些資產。 </td>
  </tr>
  <tr>
   <td>社群</td>
   <td>此主控台可讓您為<a href="/help/communities/overview.md#engagement-community">參與</a>和<a href="/help/communities/overview.md#enablement-community">啟用</a>建立和管理<a href="/help/communities/sites-console.md">社群網站</a>。</td>
  </tr>
  <tr>
   <td>商務</td>
   <td>這可讓您管理與<a href="/help/commerce/cif-classic/administering/ecommerce.md">Commerce</a>網站相關的產品、產品目錄和訂單。</td>
  </tr>
  <tr>
   <td>體驗片段</td>
   <td><a href="/help/sites-authoring/experience-fragments.md">體驗片段</a>是獨立的體驗，可跨管道重複使用，且有變數，因此可避免重複複製和貼上體驗或體驗的某些部分。</td>
  </tr>
  <tr>
   <td>表單</td>
   <td>此控制台允許您建立、管理和處理<a href="/help/forms/home.md">表單和文檔</a>。</td>
  </tr>
  <tr>
   <td>個性化</td>
   <td>此主控台提供<a href="/help/sites-authoring/personalization.md">工具架構，用於編寫目標內容及呈現個人化體驗</a>。</td>
  </tr>
  <tr>
   <td>專案</td>
   <td><a href="/help/sites-authoring/touch-ui-managing-projects.md">專案主控台可讓您直接存取您的專案</a>。 專案是虛擬控制面板。 它們可用來建立團隊，然後讓該團隊存取資源、工作流程和任務，讓人們能夠按照共同的目標工作。<br /> </td>
  </tr>
  <tr>
   <td>畫面</td>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/authoring/setting-up-projects/creating-a-screens-project.html"></a> 螢幕可讓您管理所有面向客戶的螢幕、任何大小和位置。</td>
  </tr>
  <tr>
   <td>網站</td>
   <td>「網站」主控台可讓您<a href="/help/sites-authoring/page-authoring.md">建立、檢視及管理AEM執行個體上執行的網站</a>。 通過這些控制台，您可以建立、編輯、複製、移動和刪除網站頁面、啟動工作流程和發佈頁面。<br /> </td>
  </tr>
 </tbody>
</table>

### 工具面板{#tools-panel}

在「工具」面板中，側面板中的每個選項都包含一系列子菜單。 此處提供的[工具控制台](/help/sites-administering/tools-consoles.md)可讓您存取許多專門的工具和控制台，以協助您管理網站、數位資產和內容存放庫的其他方面。

![bh-04](assets/bh-04.png)

## 標題{#the-header}

標題一律顯示在畫面頂端。 雖然無論您位於系統中的哪個位置，標題中的大多數選項都保持不變，但有些選項是內容專屬的。

![bh-05](assets/bh-03.png)

* [全域導覽](#navigatingconsolesandtools)

   選取&#x200B;**Adobe Experience Manager**&#x200B;連結，以在主控台之間導覽。

   ![screen_shot_2018-03-23at103615](assets/screen_shot_2018-03-23at103615.png)

* [搜尋](/help/sites-authoring/search.md)

   ![](do-not-localize/screen_shot_2018-03-23at103542.png)

   您也可以使用[快捷鍵](/help/sites-authoring/keyboard-shortcuts.md) `/`（正斜線）從任何控制台調用搜索。

* [解決方案](https://www.adobe.com/experience-cloud.html)

   ![](do-not-localize/screen_shot_2018-03-23at103552.png)

* [說明](#accessinghelptouchoptimizedui)

   ![](do-not-localize/screen_shot_2018-03-23at103547.png)

* [通知](/help/sites-authoring/inbox.md)

   ![](do-not-localize/screen_shot_2018-03-23at103558.png)

   此圖示將與目前指派的未完成通知數目加上標籤。

   >[!NOTE]
   >
   >現成可用的AEM會預先載入指派給管理員使用者群組的管理工作。 有關詳細資訊，請參閱[收件箱 — 現成管理任務](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks)。

* [使用者屬性](/help/sites-authoring/user-properties.md)

   ![](do-not-localize/screen_shot_2018-03-23at103603.png)

* [邊欄選取器](/help/sites-authoring/basic-handling.md#rail-selector)

   ![](do-not-localize/screen_shot_2018-03-23at103943.png)

   顯示的選項取決於您目前的主控台。 例如，在&#x200B;**Sites**&#x200B;中，您只能選取內容（預設值）、時間軸、參照或篩選端面板。

   ![screen_shot_2018-03-23at104029](assets/screen_shot_2018-03-23at104029.png)

* 階層連結

   ![bh-05](assets/bh-05.png)

   瀏覽路徑標示位於邊欄的中間，一律會顯示目前所選項目的說明，可讓您在特定主控台中導覽。 在Sites Console中，您可以瀏覽網站的各個層級。

   只需按一下階層連結文字，即可顯示下拉式清單，列出目前所選項目的階層等級。 按一下某個條目以跳轉到該位置。

   ![bh-06](assets/bh-06.png)

* 選擇Analytics時段

   ![screen_shot_2018-03-23at104126](assets/screen_shot_2018-03-23at104126.png)

   這僅適用於清單檢視。 如需詳細資訊，請參閱[清單檢視](#list-view) 。

* **** Createbutton

   ![screen_shot_2018-03-23at104301](assets/screen_shot_2018-03-23at104301.png)

   按一下後，所顯示的選項就適合主控台/內容。

* [檢視](/help/sites-authoring/basic-handling.md#viewingandselectingyourresourcescardlistcolumn)

   檢視圖示位於AEM工具列的最右側。 由於它也表示目前的檢視，因此會變更。 例如，在預設視圖中， **列視圖**&#x200B;顯示：

   ![bh-07](assets/bh-07.png)

   您可以在欄檢視、卡片檢視和清單檢視之間切換；在清單檢視中，它也會顯示檢視設定。

   ![bh-09](assets/bh-09.png)

* 鍵盤導覽

   您只能使用鍵盤來導覽網站。 這會使用&#x200B;**TAB**&#x200B;鍵（或&#x200B;**OPT+TAB**）的標準瀏覽器功能，在&#x200B;*可聚焦*&#x200B;頁面上的元素之間移動您。

   在&#x200B;**Sites**&#x200B;主控台中，新增了&#x200B;**跳至主要內容**&#x200B;的選項。 當您&#x200B;*標籤*&#x200B;透過標題選項時，就會顯示此內容，並可讓您略過（產品）工具列中的標準元素，直接導覽至主要內容，以加快導覽速度。

   ![bh-30](assets/bh-30.png)

## 訪問幫助{#accessing-help}

提供多種說明資源：

* **控制台工具欄**

   視您的位置而定，**Help**&#x200B;圖示將會開啟適當的資源：

   ![bh-10](assets/bh-10.png)

* **導覽**

   第一次導航系統時， [一系列幻燈片將介紹AEM導航](/help/sites-authoring/basic-handling.md#product-navigation)。

* **頁面編輯器**

   第一次編輯頁面時，會有一系列投影片導入頁面編輯器。

   ![bh-11](assets/bh-11.png)

   如同首次存取任何主控台時[產品導覽概述](/help/sites-authoring/basic-handling.md#product-navigation)，請導覽此概述。

   從&#x200B;[**頁面資訊**&#x200B;功能表中，您可以隨時選擇&#x200B;**Help**](/help/sites-authoring/author-environment-tools.md#accessing-help)&#x200B;以再次顯示此資訊。

* **工具主控台**

   從&#x200B;**Tools**&#x200B;控制台，您還可以訪問外部&#x200B;**Resources**:

   * ****
檔案檢視Web體驗管理檔案

   * **開發人**
員資源開發人員資源及下載
   >[!NOTE]
   >
   >在控制台中時，您可以隨時使用快捷鍵`?`（問號）來訪問可用快捷鍵的概述。
   >
   >如需所有鍵盤快速鍵的概觀，請參閱下列檔案：
   >
   >    * [編輯頁面的鍵盤快速鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [控制台的鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md)


## 操作工具欄{#actions-toolbar}

每當選取資源（例如頁面或資產）時，工具列中就會有說明文字的圖示來指出各種動作。 這些動作取決於：

* 當前控制台。
* 目前的內容。
* 無論您處於[選擇模式](#navigatingandselectionmode)。

工具列中可用的動作會變更，以反映您可以對選取的特定項目採取的動作。

如何選擇資源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)取決於該視圖。[

由於某些視窗的空間限制，工具列可能會很快變得比可用的空間長。發生此情況時，會出現其他選項。按一下或點選省略號(三個點或…… ****)會開啟一個下拉式選取器，其中包含所有剩餘的動作。例如，在Sites主控台中選取頁面 **後** :

![動作工具列](assets/bh-12.png)

>[!NOTE]
可用的個別圖示會記錄在適當的主控台/功能/情境中。

## 快速動作 {#quick-actions}

在[卡片檢視](#cardviewquickactions)中，某些動作既可作為快速動作圖示，也可作為工具列使用。 一次只有一個項目可使用快速操作表徵圖，無需預選。

當您移動資源卡（案頭設備）時，將顯示快速操作。 可用的快速動作取決於主控台和內容。 例如，以下是&#x200B;**Sites**&#x200B;控制台中某頁面的快速操作：

![bh-13](assets/bh-13.png)

## 查看和選擇資源{#viewing-and-selecting-resources}

檢視、導覽和選取在所有檢視中的概念上都相同，但處理方式的變異很小，取決於您使用的檢視。

您可以使用任何可用檢視來檢視、導覽及選取（以利進一步動作）您的資源，每個檢視都可由右上角的圖示選取：

* [欄檢視](#column-view)
* [卡片檢視](#card-view)

* [清單檢視](#list-view)

>[!NOTE]
依預設，AEM Assets不會在UI中以縮圖的形式顯示資產的原始轉譯。 如果您是管理員，可以使用覆蓋來設定AEM Assets，將原始轉譯顯示為縮圖。

### 選擇資源{#selecting-resources}

選取特定資源取決於檢視與裝置的組合：

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
     <li>案頭：<br />按一下縮圖</li>
     <li>行動裝置：<br />點選縮圖</li>
    </ul> </td>
   <td>
    <ul>
     <li>案頭：<br />按一下縮圖</li>
     <li>行動裝置：<br />點選縮圖</li>
    </ul> </td>
  </tr>
  <tr>
   <td>卡片檢視<br /> </td>
   <td>
    <ul>
     <li>案頭：<br />滑鼠，然後使用勾號快速動作</li>
     <li>行動裝置：<br />點選並按住卡片</li>
    </ul> </td>
   <td>
    <ul>
     <li>案頭：<br />按一下卡</li>
     <li>行動裝置：<br />點選卡片</li>
    </ul> </td>
  </tr>
  <tr>
   <td>清單檢視</td>
   <td>
    <ul>
     <li>案頭：<br />按一下縮圖</li>
     <li>行動裝置：<br />點選縮圖</li>
    </ul> </td>
   <td>
    <ul>
     <li>案頭：<br />按一下縮圖</li>
     <li>行動裝置：<br />點選縮圖</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### 全選 {#select-all}

您可以按一下控制台右上角的&#x200B;**全選**&#x200B;選項，以選取任何檢視中的所有項目。

* 在&#x200B;**卡片檢視**&#x200B;中，已選取所有卡片。
* 在&#x200B;**清單檢視**&#x200B;中，選取清單中的所有項目。
* 在&#x200B;**欄檢視**&#x200B;中，選取最左側欄中的所有項目。

![screen-shot_2019-03-05at094659](assets/screen-shot_2019-03-05at094659.png)

#### 取消選擇全部{#deselecting-all}

在所有情況下，當您選取項目時，所選項目的計數會顯示在工具列的右上角。

您可以透過下列任一方式，取消選取所有項目並退出選取模式：

* 按一下或點選計數旁的&#x200B;**X**,

* 或使用&#x200B;**escape**。

![bh-14](assets/bh-14.png)

在所有檢視中，如果您使用桌上型電腦裝置，點選鍵盤上的逸出即可偵測所有項目。

#### 選擇示例{#selecting-example}

1. 例如，在卡片檢視中：

   ![bh-15](assets/bh-15.png)

1. 在您選擇了資源後，[actions工具欄](#actionstoolbar)將覆蓋頂部標題，該工具欄提供對當前適用於所選資源的操作的訪問。

   要退出選擇模式，請選擇右上角的&#x200B;**X**，或使用&#x200B;**escape**。

### 欄檢視 {#column-view}

![bh-16](assets/bh-16.png)

列視圖允許通過一系列級聯列對內容樹進行可視導航。 此檢視可讓您視覺化並周遊網站的樹狀結構。

在最左邊的列中選擇一個資源將在右側的列中顯示子資源。 接著，在右側欄中選取資源後，會將子資源顯示在另一欄的右側，依此類推。

* 您可以點選或按一下資源名稱或資源名稱右側的>形，以在樹狀結構中上下導覽。

   * 點選或按一下時，資源名稱和>形箭號會醒目提示。

   ![bh-15](assets/bh-17.png)

   * 已點按/已點按資源的子項會顯示在已點按/已點按資源右側的欄中。
   * 如果您點選或按一下沒有子項的資源名稱，其詳細資訊將顯示在最終欄中。


* 點選或按一下縮圖會選取資源。

   * 選取後，勾選記號將覆蓋在縮圖上，且資源名稱也會反白顯示。
   * 所選資源的詳細資訊將顯示在最終列中。
   * 動作工具列將可供使用。

   ![bh-18](assets/bh-18.png)

   在欄檢視中選取頁面時，選取的頁面會連同下列詳細資料一起顯示在最終欄中：

   * 頁面標題
   * 頁面名稱（頁面URL的一部分）
   * 頁面所依據的範本
   * 修改詳細資訊
   * 頁面語言
   * 發佈詳細資訊


### 卡片檢視 {#card-view}

![bh-15-1](assets/bh-15-1.png)

* 卡片視圖顯示當前級別上每個項目的資訊卡。 這些功能提供下列資訊：

   * 頁面內容的視覺表示法。
   * 頁面標題。
   * 重要日期（例如上次編輯、上次發佈）。
   * 如果頁面已鎖定、隱藏或是Live Copy的一部分。
   * 如果適用，則需要您在工作流程中採取動作。

      * 指示所需操作的標籤可能與[收件箱](/help/sites-authoring/inbox.md)中的條目相關。

* [此檢](#quick-actions) 視中也提供快速動作，例如選取和編輯等常見動作。

   ![bh-13-1](assets/bh-13-1.png)

* 您可以點選/按一下資訊卡（注意以避免快速動作），或使用標題](/help/sites-authoring/basic-handling.md#the-header)中的[導覽路徑標示，以向下導覽樹狀結構。

### 清單檢視 {#list-view}

![bh-19](assets/bh-19.png)

* 清單視圖列出當前級別上每個資源的資訊。
* 您可以點選/按一下資源名稱，然後使用標題](/help/sites-authoring/basic-handling.md#the-header)中的[階層連結來向下導覽樹狀結構。

* 若要輕鬆選取清單中的所有項目，請使用清單左上角的核取方塊。

   ![bh-20](assets/bh-20.png)

   * 選取清單中的所有項目時，此核取方塊隨即顯示為已勾選。

      * 按一下或點選核取方塊，取消選取全部。
   * 只選取某些項目時，會以減號顯示。

      * 按一下或點選核取方塊以選取全部。
      * 再按一下或點選核取方塊，取消選取全部。


* 使用位於「視圖」按鈕下的「查看設定」**選項選擇要顯示的列。**&#x200B;下列欄可供顯示：

   * **名稱**  — 頁面名稱，這在多語言編寫環境中很實用，因為它是頁面URL的一部分，不會變更（不論語言為何）
   * **已修改**  — 上次修改日期和上次由使用者修改日期
   * **已發佈**  — 發佈狀態
   * **範本**  — 頁面所依據的範本
   * **工作流程**  — 目前套用至頁面的工作流程。當您滑鼠或開啟時間軸時，會提供更多資訊。

   * **頁面分析**
   * **不重複訪客**
   * **頁面逗留時間**

   ![bh-21](assets/bh-21.png)

   依預設，會顯示&#x200B;**Name**&#x200B;欄，這是頁面URL的一部分。 在某些情況下，作者可能需要存取使用不同語言的頁面，如果作者不知道頁面的語言，則檢視頁面名稱（通常不會改變）可能有很大幫助。

* 使用清單中每個項目最右邊的點狀垂直條來變更項目順序。

   >[!NOTE]
   更改順序只在具有`jcr:primaryType`值作為`sling:OrderedFolder`的有序資料夾中有效。

   ![bh-22](assets/bh-22.png)

   按一下或點選垂直選取列，然後將項目拖曳至清單中的新位置。

   ![bh-23](assets/bh-23.png)

* 您可以使用&#x200B;**檢視設定**&#x200B;對話方塊顯示適當的欄，以顯示Analytics資料。

   您可以使用標題右側的篩選選項來篩選過去30、90或365天的Analytics資料。

   ![bh-24](assets/bh-24.png)

## 邊欄選取器{#rail-selector}

**邊欄選取器**&#x200B;位於視窗左上角，並根據您目前的主控台顯示選項。

![bh-25](assets/bh-25.png)

例如，在Sites中，您只能選取內容（預設值）、內容樹、時間軸、參照或篩選端面板。

如果僅選取內容，則只會顯示邊欄圖示。 選取任何其他選項時，選項名稱會出現在邊欄圖示旁。

>[!NOTE]
[鍵盤](/help/sites-authoring/keyboard-shortcuts.md) 快速鍵可快速切換邊欄顯示選項。

### 內容樹 {#content-tree}

內容樹可用來快速導覽側面板內的網站階層，並檢視目前資料夾中頁面的詳細資訊。

使用內容樹側面板結合清單視圖或卡片視圖，用戶可以輕鬆查看項目的分層結構，使用內容樹側面板輕鬆瀏覽內容結構，並在清單視圖中查看詳細的頁面資訊。

![bh-26](assets/bh-26.png)

>[!NOTE]
選取階層檢視中的項目後，即可使用方向鍵來快速導覽階層。
如需詳細資訊，請參閱[鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md)。

### 時間軸 {#timeline}

時間軸可用於查看和/或啟動在所選資源上發生的事件。 若要開啟時間軸欄，請使用邊欄選取器：

時間軸欄可讓您：

* [檢視與](#timelineviewevents) 選取項目相關的各種事件。

   * 可從下拉式清單中選取事件類型：

      * [評論](#timelineaddingandviewingcomments)
      * 註解
      * 活動
      * [啟動](/help/sites-authoring/launches.md)
      * [版本](/help/sites-authoring/working-with-page-versions.md)
      * [工作流程](/help/sites-authoring/workflows-applying.md)

         * 但[暫時工作流](/help/sites-developing/workflows.md#transient-workflows)除外，因為沒有為這些工作流保存歷史資訊
      * 和全部顯示


* [新增/檢視有關所選項目的註解。](#timelineaddingandviewingcomments)「注 **釋** 」方塊會顯示在事件清單的底部。鍵入注釋後跟Return將註冊注釋。當選取「注 **釋** 」或「 **全部顯示** 」時顯示。

* 特定主控台有其他功能。 例如，在Sites Console中，您可以：

   * [儲存版本](/help/sites-authoring/working-with-page-versions.md#creatinganewversiontouchoptimizedui)。
   * [啟動工作流程](/help/sites-authoring/workflows-applying.md#startingaworkflowfromtherail).

可通過&#x200B;**Comment**&#x200B;欄位旁的>形找到這些選項。

![bh-27](assets/bh-27.png)

### 引用 {#references}

**** 參考會顯示與所選資源的任何連線。例如，在&#x200B;**Sites**&#x200B;控制台[參考](/help/sites-authoring/author-environment-tools.md#showingpagereferences)的頁面中，會顯示：

* [啟動](/help/sites-authoring/launches.md#launches-in-references-sites-console)
* [即時副本](/help/sites-administering/msm-livecopy-overview.md#openingthelivecopyoverviewfromreferences)
* [語言副本](/help/sites-administering/tc-prep.md#seeing-the-status-of-language-roots)
* 內容參考：

   * 從其他頁面連結至所選頁面
   * 由參考元件從選定頁面借入和/或借出的內容

![bh-28](assets/bh-28.png)

### 篩選 {#filter}

這會開啟類似[search](/help/sites-authoring/search.md)的面板，其中已設定適當的位置篩選器，讓您能夠進一步篩選您要檢視的內容。

![bh-29](assets/bh-29.png)
