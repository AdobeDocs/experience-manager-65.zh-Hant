---
title: 製作頁面的快速指南
description: 製作頁面內容關鍵動作的快速、高階指南
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: a7e16555-9bbe-4da2-817c-4495a0193f3f
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 5%

---

# 製作頁面的快速指南{#quick-guide-to-authoring-pages}

這些程式旨在作為在AEM中編寫頁面內容之關鍵動作的快速指南（高層級）。

上述功能為：

* 不是為了提供完整的涵蓋範圍。
* 提供詳細檔案的連結。

如需使用AEM撰寫的完整詳細資訊，請參閱：

* [作者的首要步驟](/help/sites-authoring/first-steps.md)
* [製作頁面](/help/sites-authoring/page-authoring.md)

## 一些快速提示 {#a-few-quick-hints}

在概略介紹具體內容之前，請先參閱以下小冊子，其中收錄一些值得牢記的一般秘訣和提示。

### Sites 主控台 {#sites-console}

* **建立**

   * 此按鈕在許多主控台中都有提供 — 顯示的選項會區分大小寫，因此可視情況而有所不同。

* 在資料夾中重新排序頁面

   * 這可以在[清單檢視](/help/sites-authoring/basic-handling.md#list-view)中完成。 變更會套用並顯示在其他檢視中。

#### 頁面製作 {#page-authoring}

* 導覽連結

   * 當您處於&#x200B;***編輯***&#x200B;模式時，**連結無法用於導覽**。 若要使用連結導覽，您需要[使用以下其中一種方式預覽頁面](/help/sites-authoring/editing-content.md#previewing-pages)：

      * [預覽模式](/help/sites-authoring/editing-content.md#preview-mode)
      * [以已發佈狀態檢視](/help/sites-authoring/editing-content.md#view-as-published)

* 無法從頁面編輯器啟動/建立版本；現在可以從網站主控台完成（針對選取的資源透過&#x200B;**建立**&#x200B;或[時間表](/help/sites-authoring/basic-handling.md#timeline)）。

>[!NOTE]
>
>有數種鍵盤快速鍵可讓您更輕鬆進行撰寫體驗。
>
>* 編輯頁面時[鍵盤快速鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
>* 主控台的[鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md)
>

### 尋找您的頁面 {#finding-your-page}

尋找頁面有許多方面；您可以導覽及/或搜尋：

1. 開啟&#x200B;**網站**&#x200B;主控台（使用&#x200B;**全域導覽**&#x200B;中的[網站](/help/sites-authoring/basic-handling.md#global-navigation)選項） — 這會在您選取Adobe Experience Manager連結（左上方）時觸發（下拉式清單）。

1. 點選/按一下適當的頁面，在樹狀結構中向下導覽。 頁面資源的呈現方式取決於您使用的檢視 — [卡片、清單或欄](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)：

   ![screen_shot_2018-03-21at160214](assets/screen_shot_2018-03-21at160214.png)

1. 使用[標頭](/help/sites-authoring/basic-handling.md#theheaderwithbreadcrumbs)中的階層連結來向上導覽樹狀結構，可讓您返回選取的位置：

   ![qgtap-01](assets/qgtap-01.png)

1. 您也可以[搜尋](/help/sites-authoring/search.md)頁面。 您可以從顯示的結果中選取您的頁面。

   ![qgtap-03](assets/qgtap-03.png)

### 建立新頁面 {#creating-a-new-page}

若要[建立頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page)：

1. [導覽至您要建立頁面的位置](#finding-your-page)。
1. 使用&#x200B;**建立**&#x200B;圖示，然後從清單中選取&#x200B;**頁面**：

   ![qgtap-02](assets/qgtap-02.png)

1. 這會開啟精靈，引導您收集在[建立新頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page)時所需的資訊。 請依照熒幕上的指示操作。

### 選取您的頁面以採取進一步動作 {#selecting-your-page-for-further-action}

您可以選取頁面以便對其執行動作。 選取頁面會自動更新工具列，以便顯示該資源相關的動作。

如何選取頁面取決於您在主控台中使用的檢視：

1. 欄檢視：

   * 按一下所需資源的縮圖 — 縮圖上將覆蓋一個勾號，表示已選取該縮圖。

1. 清單檢視：

   * 按一下所需資源的縮圖 — 縮圖上將覆蓋一個勾號，表示已選取該縮圖。

1. 卡片檢視：

   * 透過[選取所需資源](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources)進入選擇模式，其包含：

      * 行動裝置：選取並保留
      * 案頭： [快速動作](/help/sites-authoring/basic-handling.md#quick-actions) — 勾選圖示：

   ![screen_shot_2018-03-21at160503](assets/screen_shot_2018-03-21at160503.png)

   * 卡片上將覆蓋一個勾號，表示已選取頁面。

   >[!NOTE]
   >
   >進入選取模式後，**選取**&#x200B;圖示（勾號）將變更為&#x200B;**取消選取**&#x200B;圖示（十字形）。

### 快速動作（僅限卡片檢視/案頭） {#quick-actions-card-view-desktop-only}

[快速動作](/help/sites-authoring/basic-handling.md#quick-actions)可用：

1. [瀏覽至您要採取動作的頁面](#finding-your-page)。
1. 將滑鼠指標停留在代表所需資源的卡片上；會顯示快速動作：

   ![screen_shot_2018-03-21at160503-1](assets/screen_shot_2018-03-21at160503-1.png)

### 編輯您的頁面內容 {#editing-your-page-content}

1. [瀏覽至您要編輯的頁面](#finding-your-page)。
1. [使用「編輯」（鉛筆）圖示開啟頁面以進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)：

   ![screen_shot_2018-03-21at160607](assets/screen_shot_2018-03-21at160607.png)

   您可透過下列任一方式存取此專案：

   * 適當資源的[快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only)。
   * 選取[頁面時的工具列](#selectiingyourpageforfurtheraction)。

1. 編輯器開啟時，您可以：

   * [新增元件至您的頁面](/help/sites-authoring/editing-content.md#inserting-a-component)，方法如下：

      * 開啟側面板
      * 選取[元件]索引標籤（[元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser)）
      * 將必要的元件拖曳到頁面上。

     側面板的開啟（和關閉）方式：

     ![開啟側面板](do-not-localize/screen_shot_2018-03-21at160738.png)

   * [編輯頁面上現有元件](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)的內容：

      * 按一下以開啟元件工具列。 使用&#x200B;**編輯** （鉛筆）圖示開啟對話方塊。
      * 使用select-and-hold或按兩下滑鼠鍵開啟元件的就地編輯器。 會顯示可用的動作（對於某些元件而言，為有限的選取範圍）。
      * 若要檢視所有可用動作，請使用以下方法進入全熒幕模式：

     ![全熒幕模式](do-not-localize/screen_shot_2018-03-21at160706.png)

   * [設定現有元件的屬性](/help/sites-authoring/editing-content.md#component-edit-dialog)

      * 按一下以開啟元件工具列。 使用&#x200B;**設定** （扳手）圖示開啟對話方塊。

   * [移動元件](/help/sites-authoring/editing-content.md#moving-a-component)：

      * 將所需元件拖曳至其新位置。
      * 按一下以開啟元件工具列。 必要時使用&#x200B;**剪下**&#x200B;再使用&#x200B;**貼上**&#x200B;圖示。

   * [複製（並貼上）](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)元件：

      * 按一下以開啟元件工具列。 視需要使用&#x200B;**複製**&#x200B;然後&#x200B;**貼上**&#x200B;圖示。

   >[!NOTE]
   >
   >您可以&#x200B;**貼上**&#x200B;元件至相同頁面或其他頁面。 如果貼上至剪下/復製作業前已開啟的其他頁面，則需要重新整理該頁面。

   * [刪除](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)元件：

      * 按一下以開啟元件工具列，然後使用&#x200B;**刪除**&#x200B;圖示。

   * [新增註解](/help/sites-authoring/annotations.md#annotations)至頁面：

      * 選取&#x200B;**註釋**&#x200B;模式（語音泡泡圖示）。 使用&#x200B;**新增註釋** （加號）圖示新增註釋。 使用右上方的X退出附註模式。

     ![註釋](do-not-localize/screen_shot_2018-03-21at160813.png)

   * [預覽頁面](/help/sites-authoring/editing-content.md#preview-mode) （檢視該頁面在發佈環境中的顯示方式）

      * 從工具列選取&#x200B;**預覽**。

   * 使用&#x200B;**編輯**&#x200B;下拉式選取器返回編輯模式（或選取其他模式）。

   >[!NOTE]
   >
   >若要使用內容中的連結來瀏覽，您必須使用[預覽模式](/help/sites-authoring/editing-content.md#preview-mode)。

### 編輯頁面屬性 {#editing-the-page-properties}

有兩個（主要）方法[編輯頁面屬性](/help/sites-authoring/editing-page-properties.md)：

* 從&#x200B;**網站**&#x200B;主控台：

   1. [瀏覽至您要發佈的頁面](#finding-your-page)。
   1. 選取&#x200B;**屬性**&#x200B;圖示，其來源為：

      * 適當資源的[快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only)。
      * 選取[頁面時的工具列](#selectiingyourpageforfurtheraction)。

  ![screen_shot_2018-03-21at160850](assets/screen_shot_2018-03-21at160850.png)

   1. 畫面隨即顯示頁面屬性。 您可以視需要進行更新，然後使用「儲存」來儲存這些專案

* 當[編輯您的頁面](#editing-your-page-content)時：

   1. 開啟&#x200B;**頁面資訊**&#x200B;功能表。
   1. 選取&#x200B;**開啟屬性**&#x200B;以開啟用於編輯屬性的對話方塊。

  ![screen_shot_2018-03-21at160920](assets/screen_shot_2018-03-21at160920.png)

### 發佈頁面（或取消發佈） {#publishing-your-page-or-unpublishing}

有兩種主要方法[發佈您的頁面](/help/sites-authoring/publishing-pages.md) （以及取消發佈）：

* 從&#x200B;**網站**&#x200B;主控台：

   1. [瀏覽至您要發佈的頁面](#finding-your-page)。
   1. 選取&#x200B;**快速發佈**&#x200B;圖示，其來源為：

      * 適當資源的[快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only)。
      * 選取[頁面時的工具列](#selectiingyourpageforfurtheraction) （也可存取[稍後發佈](/help/sites-authoring/publishing-pages.md#main-pars-title-12)）。

  ![screen_shot_2018-03-21at160957](assets/screen_shot_2018-03-21at160957.png)

* 當[編輯您的頁面](#editing-your-page-content)時：

   1. 開啟&#x200B;**頁面資訊**&#x200B;功能表。
   1. 選取&#x200B;**發佈頁面**。

  ![screen_shot_2018-03-21at161026](assets/screen_shot_2018-03-21at161026.png)

* 從主控台取消發佈頁面只能透過「管理出版物 **&#x200B;**&#x200B;」選項完成，此選項只能在工具列上使用 (不能透過快速動作)。

  編輯器中仍可透過&#x200B;**頁面資訊**&#x200B;功能表使用&#x200B;**取消發佈頁面**&#x200B;選項。

  ![screen_shot_2018-03-21at161059](assets/screen_shot_2018-03-21at161059.png)

  如需詳細資訊，請參閱[發佈頁面](/help/sites-authoring/publishing-pages.md#unpublishing-pages)。

### 移動、複製並貼上或刪除您的頁面 {#move-copy-and-paste-or-delete-your-page}

這些動作都可由以下動作觸發：

1. [瀏覽至您要移動、複製和貼上或刪除的頁面](#finding-your-page)。
1. 選擇複製 (然後貼上) 、移動或刪除圖示 (視需要)，使用下列任一項：

   * 所需資源的[快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only)。
   * 選取[頁面時的工具列](#selecting-your-page-for-further-action)。

   接著，視您的動作而定：

   * 複製:

      * 導覽至新位置並貼上。

   * 移動:

      * 精靈會開啟，以收集移動頁面所需的資訊。 請依照熒幕上的指示操作。

   * 刪除:

      * 系統會要求您確認動作。

   >[!NOTE]
   >
   >「刪除」不適用於「快速動作」。

### 鎖定頁面（然後解鎖） {#locking-your-page-then-unlocking}

[鎖定頁面](/help/sites-authoring/editing-content.md#locking-a-page) ，會使其他作者無法在您執行時使用頁面。您可以找到「鎖定 (和解除鎖定) 」圖示/按鈕：

* 選取[頁面時的工具列](#selecting-your-page-for-further-action)。
* 編輯頁面時，[頁面資訊下拉式功能表](#editing-the-page-properties)。
* 編輯頁面（頁面已鎖定）時的頁面工具列

例如，鎖定圖示看起來像這樣：

![screen_shot_2018-03-21at161124](assets/screen_shot_2018-03-21at161124.png)

### 存取頁面參照 {#accessing-page-references}

[在「參考」邊欄中，可以快速存取頁面或頁面的參考](/help/sites-authoring/author-environment-tools.md#references)。

1. 使用工具列圖示選取&#x200B;**參考** （在[選取您的頁面](#selecting-your-page-for-further-action)之前或之後）：

   ![screen_shot_2018-03-21at161210](assets/screen_shot_2018-03-21at161210.png)

   此時會顯示參考型別清單：

   ![screen-shot_2019-03-05at114412](assets/screen-shot_2019-03-05at114412.png)

1. 按一下所需的參照型別以顯示更多詳細資訊，並（在適當時）採取進一步動作。

### 建立頁面的版本 {#creating-a-version-of-your-page}

若要建立頁面的[版本](/help/sites-authoring/working-with-page-versions.md)：

1. 若要開啟[時間表]邊欄，請使用工具列圖示選取&#x200B;**[時間表](/help/sites-authoring/basic-handling.md#timeline)** （在[選取您的頁面](#selecting-your-page-for-further-action)之前或之後）：

   ![screen_shot_2018-03-21at161355](assets/screen_shot_2018-03-21at161355.png)

1. 按一下「時間軸」欄右下方的向上箭頭以顯示其他按鈕，包括&#x200B;**另存為版本**。

   ![screen-shot_2019-03-05at114600](assets/screen-shot_2019-03-05at114600.png)

1. 選取&#x200B;**另存為版本**，然後選取&#x200B;**建立**。

### 還原/比較頁面版本 {#restoring-comparing-a-version-of-your-page}

還原及/或比較頁面版本時，會使用相同的基本機制：

1. 使用工具列圖示選取&#x200B;**[時間表](/help/sites-authoring/basic-handling.md#timeline)** （在[選取您的頁面](#selecting-your-page-for-further-action)之前或之後）：

   ![screen_shot_2018-03-21at161355-1](assets/screen_shot_2018-03-21at161355-1.png)

   如果頁面的某個版本已儲存，則會列在時間軸中。

1. 按一下您要還原的版本 — 這會顯示其他動作按鈕：

   * **還原為此版本**

      * 版本已還原。

   * **顯示差異**

      * 頁面開啟時會反白顯示兩個版本之間的差異。
