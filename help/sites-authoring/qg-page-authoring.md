---
title: 創作頁面快速指南
seo-title: Quick Guide to Authoring Pages
description: 關於創作頁面內容關鍵操作的快速、高級指南
seo-description: A quick, high-level guide to the key actions of authoring page content
uuid: ef7ab691-f80d-4eeb-9f4a-afbf1bc83669
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 2d35a2a4-0c8c-4b16-99a6-c6e6d66446dc
docset: aem65
exl-id: a7e16555-9bbe-4da2-817c-4495a0193f3f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 5%

---

# 創作頁面快速指南{#quick-guide-to-authoring-pages}

這些步驟旨在作為在中創作頁面內容的關鍵操作的快速指南（高級別）AEM。

上述功能為：

* 不是全面覆蓋。
* 提供指向詳細文檔的連結。

有關創作的完整詳細資訊，請參AEM閱：

* [作者的第一步](/help/sites-authoring/first-steps.md)
* [創作頁面](/help/sites-authoring/page-authoring.md)

## 幾個簡短提示 {#a-few-quick-hints}

在概述具體內容之前，下面是一小組的一般提示和提示，值得我們牢記。

### 站點控制台 {#sites-console}

* **建立**

   * 此按鈕在許多控制台中都可用 — 所提供的選項是上下文相關的，因此可能因場景而異。

* 對資料夾中的頁面重新排序

   * 可以在 [清單視圖](/help/sites-authoring/basic-handling.md#list-view)。 將應用這些更改，並在其他視圖中可見。

#### 頁面創作 {#page-authoring}

* 導航連結

   * ***連結不可用於導航*** 當您進入 **編輯** 的子菜單。 要使用需要的連結導航 [預覽頁面](/help/sites-authoring/editing-content.md#previewing-pages) 使用其中之一：

      * [預覽模式](/help/sites-authoring/editing-content.md#preview-mode)
      * [以已發佈狀態檢視](/help/sites-authoring/editing-content.md#view-as-published)

* 版本不是從頁面編輯器啟動/建立的；現在可通過站點控制台(通過 **建立** 或 [時間軸](/help/sites-authoring/basic-handling.md#timeline) )。

>[!NOTE]
>
>有許多鍵盤快捷方式可讓創作體驗更輕鬆。
>
>* [編輯頁面時的鍵盤快捷鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
>* [控制台的鍵盤快捷鍵](/help/sites-authoring/keyboard-shortcuts.md)
>


### 查找頁面 {#finding-your-page}

查找頁面有多方面；您可以導航和/或搜索：

1. 開啟 **站點** 控制台(使用 **站點** 的上界 [全局導航](/help/sites-authoring/basic-handling.md#global-navigation)  — 當您選擇Adobe Experience Manager連結（左上）時，將觸發（下拉）該連結。

1. 按一下/按一下相應頁面，在樹下導航。 頁面資源的表示方式取決於您使用的視圖 —  [卡、清單或列](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources):

   ![screen_shot_2018-03-21at160214](assets/screen_shot_2018-03-21at160214.png)

1. 使用 [標題中的breadcrumb](/help/sites-authoring/basic-handling.md#theheaderwithbreadcrumbs)，允許您返回到選定位置：

   ![qgtap-01](assets/qgtap-01.png)

1. 您也可以 [搜索](/help/sites-authoring/search.md) 的雙曲餘切值。 您可以從顯示的結果中選擇頁面。

   ![qgtap-03](assets/qgtap-03.png)

### 建立新頁面 {#creating-a-new-page}

至 [建立新頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page):

1. [導航到位置](#finding-your-page) 建立新頁面的位置。
1. 使用 **建立** 表徵圖，然後選擇 **頁面** 清單中：

   ![qgtap-02](assets/qgtap-02.png)

1. 這將開啟嚮導，該嚮導將指導您收集在 [建立新頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page)。 按照螢幕上的說明進行操作。

### 選擇頁面以執行進一步操作 {#selecting-your-page-for-further-action}

您可以選擇頁面，以便對其執行操作。 選擇頁面將自動更新工具欄，以便顯示與該資源相關的操作。

如何選擇頁面取決於您在控制台中使用的視圖：

1. 欄檢視:

   * 點擊/按一下所需資源的縮略圖 — 縮略圖將覆蓋一個勾選項，以顯示其已被選中。

1. 清單檢視:

   * 點擊/按一下所需資源的縮略圖 — 縮略圖將覆蓋一個勾選項，以顯示其已被選中。

1. 卡片檢視:

   * 進入選擇模式 [選擇所需資源](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) 與：

      * 移動設備：點擊和保持
      * 案頭：這樣 [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)  — 刻度表徵圖：

   ![screen_shot_2018-03-21at160503](assets/screen_shot_2018-03-21at160503.png)

   * 卡片將覆蓋一個勾號，以顯示已選擇頁面。
   >[!NOTE]
   >
   >一旦處於選擇模式， **選擇** 表徵圖（勾選）將更改為 **取消選擇** 表徵圖（十字）。

### 快速操作（僅限卡視圖/案頭） {#quick-actions-card-view-desktop-only}

[快速操作](/help/sites-authoring/basic-handling.md#quick-actions) 可用：

1. [導航到該頁](#finding-your-page) 你想對它採取行動。
1. 將滑鼠指針懸停在表示所需資源的卡上；將顯示快速操作：

   ![screen_shot_2018-03-21at160503-1](assets/screen_shot_2018-03-21at160503-1.png)

### 編輯頁面內容 {#editing-your-page-content}

要編輯頁面：

1. [導航到該頁](#finding-your-page) 編輯。
1. [開啟頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing) 使用「編輯（鉛筆）」表徵圖：

   ![screen_shot_2018-03-21at160607](assets/screen_shot_2018-03-21at160607.png)

   可以從以下任一位置訪問此選項：

   * [快速操作（僅限卡視圖/案頭）](#quick-actions-card-view-desktop-only) 。
   * 工具欄 [已選擇頁面](#selectiingyourpageforfurtheraction)。

1. 開啟編輯器時，您可以：

   * [向頁面添加新補償](/help/sites-authoring/editing-content.md#inserting-a-component) 按：

      * 開啟側面板
      * 選擇「元件」(components)頁籤( [元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser))
      * 將所需元件拖到頁面上。

      側面板可開啟（和關閉），具有：
   ![](do-not-localize/screen_shot_2018-03-21at160738.png)

   * [編輯現有元件的內容](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) 頁上：

      * 按一下或按一下開啟元件工具欄。 使用 **編輯** （鉛筆）表徵圖以開啟對話框。
      * 開啟元件的就地編輯器，按一下並按住或按兩下。 將顯示可用操作（對於某些元件，這將是有限的選擇）。
      * 要查看所有可用操作，請使用：

   ![](do-not-localize/screen_shot_2018-03-21at160706.png)

   * [配置現有元件的屬性](/help/sites-authoring/editing-content.md#component-edit-dialog)

      * 按一下或按一下開啟元件工具欄。 使用 **配置** （扳手）表徵圖以開啟對話框。
   * [移動元件](/help/sites-authoring/editing-content.md#moving-a-component) 其中之一：

      * 將所需元件拖到其新位置。
      * 按一下或按一下開啟元件工具欄。 使用 **剪切** 然後 **貼上** 表徵圖。
   * [複製（並貼上）](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) 元件：

      * 按一下或按一下開啟元件工具欄。 使用 **複製** 然後 **貼上** 表徵圖。
   >[!NOTE]
   >
   >你可以 **貼上** 元件到同一頁或不同頁。 如果貼上到剪切/複製操作之前已開啟的其他頁面，則該頁面需要刷新頁面。

   * [刪除](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) 元件：

      * 使用點擊或按一下開啟元件工具欄，然後使用 **刪除** 表徵圖
   * [添加註釋](/help/sites-authoring/annotations.md#annotations) 到頁面：

      * 選擇 **注釋** 模式（語音氣泡表徵圖）。 使用 **添加註釋** 表徵圖。 使用右上角的X退出注釋模式。

   ![](do-not-localize/screen_shot_2018-03-21at160813.png)

   * [預覽頁面](/help/sites-authoring/editing-content.md#preview-mode) （查看它在發佈環境中的顯示方式）

      * 選擇 **預覽** 的子菜單。
   * 使用 **編輯** 下拉選擇器。

   >[!NOTE]
   >
   >要使用必須使用的內容中的連結導航 [預覽模式](/help/sites-authoring/editing-content.md#preview-mode)。

### 編輯頁面屬性 {#editing-the-page-properties}

有兩種（主要）方法 [編輯頁面屬性](/help/sites-authoring/editing-page-properties.md):

* 從 **站點** 控制台：

   1. [導航到該頁](#finding-your-page) 要發佈。
   1. 選擇 **屬性** 表徵圖：

      * [快速操作（僅限卡視圖/案頭）](#quick-actions-card-view-desktop-only) 。
      * 工具欄 [已選擇頁面](#selectiingyourpageforfurtheraction)。

   ![screen_shot_2018-03-21at160850](assets/screen_shot_2018-03-21at160850.png)

   1. 將顯示頁面屬性。 您可以根據需要進行更新，然後使用「保存」保留這些


* 當 [編輯頁面](#editing-your-page-content):

   1. 開啟 **頁面資訊** 的子菜單。
   1. 選擇 **開啟屬性** 開啟對話框以編輯屬性。

   ![screen_shot_2018-03-21at160920](assets/screen_shot_2018-03-21at160920.png)

### 發佈頁面（或取消發佈） {#publishing-your-page-or-unpublishing}

有兩種主要方法 [發佈頁面](/help/sites-authoring/publishing-pages.md) （以及取消發佈）:

* 從 **站點** 控制台：

   1. [導航到該頁](#finding-your-page) 要發佈。
   1. 選擇 **快速發佈** 表徵圖：

      * [快速操作（僅限卡視圖/案頭）](#quick-actions-card-view-desktop-only) 。
      * 工具欄 [已選擇頁面](#selectiingyourpageforfurtheraction) (還允許訪問 [稍後發佈](/help/sites-authoring/publishing-pages.md#main-pars-title-12))。

   ![screen_shot_2018-03-21at160957](assets/screen_shot_2018-03-21at160957.png)

* 當 [編輯頁面](#editing-your-page-content):

   1. 開啟 **頁面資訊** 的子菜單。
   1. 選擇 **發佈頁面**。

   ![screen_shot_2018-03-21at161026](assets/screen_shot_2018-03-21at161026.png)

* 從主控台取消發佈頁面只能透過「管理出版物 **** 」選項完成，此選項只能在工具列上使用 (不能透過快速動作)。

   的 **取消發佈頁面** 選項 **頁面資訊** 的子菜單。

   ![screen_shot_2018-03-21at161059](assets/screen_shot_2018-03-21at161059.png)

   請參閱 [發佈頁面](/help/sites-authoring/publishing-pages.md#unpublishing-pages) 的子菜單。

### 移動、複製和貼上或刪除頁面 {#move-copy-and-paste-or-delete-your-page}

這些操作都可通過以下方式觸發：

1. [導航到該頁](#finding-your-page) 要移動、複製和貼上或刪除。
1. 選擇複製 (然後貼上) 、移動或刪除圖示 (視需要)，使用下列任一項：

   * [快速操作（僅限卡視圖/案頭）](#quick-actions-card-view-desktop-only) 的下界。
   * 工具欄 [已選擇頁面](#selecting-your-page-for-further-action)。

   然後，取決於您的操作：

   * 複製:

      * 然後，您需要導航到新位置並貼上。
   * 移動:

      * 將開啟嚮導以收集移動頁面所需的資訊。 按照螢幕上的說明進行操作。
   * 刪除:

      * 系統將要求您確認操作。
   >[!NOTE]
   >
   >「刪除」不能作為「快速操作」使用。

### 鎖定頁面（然後解鎖） {#locking-your-page-then-unlocking}

[鎖定頁面](/help/sites-authoring/editing-content.md#locking-a-page) ，會使其他作者無法在您執行時使用頁面。您可以找到「鎖定 (和解除鎖定) 」圖示/按鈕：

* 工具欄 [已選擇頁面](#selecting-your-page-for-further-action)。
* 的 [「頁面資訊」下拉菜單](#editing-the-page-properties) 編輯頁面時。
* 編輯頁面時（當頁面被鎖定時），頁面工具欄

例如，鎖表徵圖如下所示：

![screen_shot_2018-03-21at161124](assets/screen_shot_2018-03-21at161124.png)

### 訪問頁面引用 {#accessing-page-references}

[快速訪問引用](/help/sites-authoring/author-environment-tools.md#references) 「參考」(References)導軌中提供「至」(to)/「自」(from)頁面。

1. 選擇 **引用** 使用工具欄表徵圖（之前或之後） [選擇頁面](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-21at161210](assets/screen_shot_2018-03-21at161210.png)

   將顯示參考型別清單：

   ![screen-shot_2019-03-05at114412](assets/screen-shot_2019-03-05at114412.png)

1. 點擊/按一下所需的參考型別以顯示更多詳細資訊，並（在適當時）採取進一步的操作。

### 建立頁面版本 {#creating-a-version-of-your-page}

建立 [版本](/help/sites-authoring/working-with-page-versions.md) 頁面中：

1. 要開啟時間軸滑軌，請選擇 **[時間軸](/help/sites-authoring/basic-handling.md#timeline)** 使用工具欄表徵圖（之前或之後） [選擇頁面](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-21at161355](assets/screen_shot_2018-03-21at161355.png)

1. 點擊/按一下「時間軸」列右下角的上箭頭可顯示額外的按鈕，包括 **另存為版本**。

   ![螢幕抓拍_2019-03-05at114600](assets/screen-shot_2019-03-05at114600.png)

1. 選擇 **另存為版本**，則 **建立**。

### 恢復/比較頁面版本 {#restoring-comparing-a-version-of-your-page}

恢復和/或比較頁面版本時使用的基本機制相同：

1. 選擇 **[時間軸](/help/sites-authoring/basic-handling.md#timeline)** 使用工具欄表徵圖（之前或之後） [選擇頁面](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-21at161355-1](assets/screen_shot_2018-03-21at161355-1.png)

   如果已保存頁面的版本，則會在時間軸中列出。

1. 點擊/按一下要恢復的版本 — 這將顯示其他操作按鈕：

   * **還原為此版本**

      * 版本將還原。
   * **顯示差異**

      * 將開啟頁面，並突出顯示兩個版本之間的差異。
