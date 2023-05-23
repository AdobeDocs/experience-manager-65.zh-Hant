---
title: 使用內容頁面版本
description: 建立、比較和還原頁面的版本
uuid: 29e049f0-532c-4e3b-b64f-5be88ee6b08c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1368347a-9b65-4cfc-87e1-62993dc627fd
docset: aem65
exl-id: cb7a9da2-7112-4ef0-b1cf-211a7df93625
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 5%

---

# 使用頁面版本{#working-with-page-versions}

版本控制在特定時間點建立頁面的「快照」。 使用版本控制，您可以執行以下操作：

* 建立頁面版本。
* 將頁面還原到以前的版本，以撤消對頁面所做的更改。
* 將當前版本的頁面與先前版本進行比較，其中突出顯示的文本和影像有所不同。

## 建立新版本 {#creating-a-new-version}

您可以從以下位置建立資源版本：

* 這樣 [時間軸](#creating-a-new-version-timeline)
* 這樣 [建立](#creating-a-new-version-create-with-a-selected-resource) 選項（當選擇資源時）

### 建立新版本 — 時間軸 {#creating-a-new-version-timeline}

1. 導航到要為其建立版本的頁面。
1. 在中選擇頁面 [選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟 **時間軸** 的雙曲餘切值。
1. 按一下/點擊注釋欄位的箭頭以顯示選項：

   ![screen-shot_2019-03-05at112335](assets/screen-shot_2019-03-05at112335.png)

1. 選擇 **另存為版本**。
1. 輸入 **標籤** 和 **注釋** 的子菜單。

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. 確認新版本 **建立**。

   時間軸中的資訊將更新以指示新版本。

### 建立新版本 — 使用選定資源建立 {#creating-a-new-version-create-with-a-selected-resource}

1. 導航到要為其建立版本的頁面。
1. 在中選擇頁面 [選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 選擇 **建立** 的子菜單。
1. 對話框將開啟。 您可以輸入 **標籤** 和 **注釋** 如果需要，

   ![screen_shot_2012-02-15at105050am](assets/screen_shot_2012-02-15at105050am.png)

1. 確認新版本 **建立**。

   時間線將開啟，並更新資訊以指示新版本。

## 恢復版本 {#reinstating-versions}

建立頁面版本後，可以使用多種方法來恢復以前的版本：

* 這樣 **還原到此版本** 的 [時間軸](/help/sites-authoring/basic-handling.md#timeline) 軌

   恢復所選頁面的先前版本。

* 這樣 **還原** 選項 [動作工具欄](/help/sites-authoring/basic-handling.md#actions-toolbar)

   * **還原版本**

      恢復當前選定資料夾中指定頁面的版本；這還可包括恢復以前已刪除的頁面。

   * **還原樹狀結構**

      在指定日期和時間恢復整個樹的版本；這可以包括以前已刪除的頁面。

>[!NOTE]
>
>恢復頁面時，建立的版本將是新分支的一部分。
>
>為說明：
>
>1. 建立任何頁面的版本。
>1. 初始標籤和版本節點名稱將為1.0、1.1、1.2等。
>1. 恢復第一個版本；即1.0
>1. 再次建立新版本。
>1. 生成的標籤和節點名稱現1.0.0為1.0.1、1.0.2等。


### 還原為版本 {#revert-to-a-version}

至 **還原** 選定頁面到上一版本：

1. 導航以顯示要還原為以前版本的頁面。
1. 在中選擇頁面 [選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。將列出所選頁面的頁面版本。
1. 選擇要還原到的版本。 可能的選項將顯示：

   ![還原為此版本](assets/screen-shot_2019-03-05at112505.png)

1. 選擇 **還原到此版本**。 將還原所選版本，並更新時間線中的資訊。

### 還原版本 {#restore-version}

此方法可用於還原當前資料夾中指定頁面的版本；這還可以包括恢復以前已刪除的頁面：

1. 導航到和 [選擇](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)的子菜單。

1. 選擇 **還原**，則 **還原版本** 從頂部 [動作工具欄](/help/sites-authoring/basic-handling.md#actions-toolbar)。

   >[!NOTE]
   >
   >如果，則：
   >
   >* 您選擇了單個頁面，該頁面從未包含子頁面，
   >* 或者資料夾中的頁面沒有版本，

   >
   >然後，由於沒有適用的版本，顯示將為空。

1. 將列出可用版本：

   ![還原版本 — 資料夾中所有頁的清單](/help/sites-authoring/assets/versions-restore-version-01.png)

1. 對於特定頁，請使用下面的下拉選擇器 **還原到版本** 選擇該頁的必需版本。

   ![還原版本 — 選擇版本](/help/sites-authoring/assets/versions-restore-version-02.png)

1. 在主顯示中，選擇要還原的所需頁：

   ![「還原版本 — 選擇」頁](/help/sites-authoring/assets/versions-restore-version-03.png)

1. 選擇 **還原** 將選定頁面的選定版本還原為當前版本。

>[!NOTE]
>
>選擇所需頁面和相關版本的順序是可互換的。

### 還原樹狀結構 {#restore-tree}

此方法可用於在指定日期和時間還原樹的版本；這可能包括以前刪除的頁面：

1. 導航到和 [選擇](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)的子菜單。

1. 選擇 **還原**，則 **還原樹** 從頂部 [動作工具欄](/help/sites-authoring/basic-handling.md#actions-toolbar)。 將顯示樹的最新版本：

   ![還原樹狀結構](/help/sites-authoring/assets/versions-restore-tree-02.png)

1. 使用日期和時間選擇器 **最新版本** 選擇樹的其他版本 — 要恢復的版本。

1. 設定標誌 **保留的未版本化頁面** 根據需要：

   * 如果處於活動狀態（已選定），則任何未版本化的頁面都將得到維護，並且不會受恢復的影響。

   * 如果不活動（未選定），則任何未版本化的頁面都將被刪除，因為這些頁面在版本化樹中不存在。

1. 選擇 **還原** 將樹的選定版本還原為 *當前* 。

## 預覽版本 {#previewing-a-version}

可以預覽特定版本：

1. 導航以顯示要比較的頁面。
1. 在中選擇頁面 [選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。
1. 將列出頁面版本。 選擇要預覽的版本：

   ![screen-shot_2019-03-05at112505-1](assets/screen-shot_2019-03-05at112505-1.png)

1. 選擇 **預覽**。 該頁面將顯示在新頁籤中。

   >[!CAUTION]
   >
   >如果已移動頁面，則無法再對移動之前建立的任何版本執行預覽。
   >
   >* 如果預覽遇到問題，請檢查 [時間軸](/help/sites-authoring/basic-handling.md#timeline) ，查看是否已移動頁面。


## 將版本與當前頁進行比較 {#comparing-a-version-with-current-page}

要將上一版本與當前頁進行比較，請執行以下操作：

1. 導航以顯示要比較的頁面。
1. 在中選擇頁面 [選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。
1. 將列出頁面版本。 選擇要比較的版本：

   ![screen-shot_2019-03-05at112505-2](assets/screen-shot_2019-03-05at112505-2.png)

1. 選擇 **與當前比較**。 的 [頁面差異](/help/sites-authoring/page-diff.md) 將開啟並顯示差異。

## Timewarp {#timewarp}

時間曲線是用於模擬 *出版* 過去特定時間的頁面狀態。

>[!TIP]
>
>[Timewarp還可與「啟動」一起使用，以預覽將來](/help/sites-authoring/launches.md) 運行AEM6.5.10.0或更高版本。

由於內容建立是一個持續和協作的過程，因此Timewarp的目的是允許作者跟蹤已發佈的網站，以便瞭解內容是如何更改的。 此功能使用頁面版本來確定發佈環境的狀態。

要執行此操作：

* 系統查找在選定時間處於活動狀態的頁面版本。
* 這表示所顯示的版本已建立/激活 *先* 在Timewarp中選擇的時間點。
* 導航到已刪除的頁面時，也會呈現該頁面 — 只要該頁面的舊版本仍然在儲存庫中可用。
* 如果找不到已發佈的版本，則Timewarp將恢復到作者環境中頁面的當前狀態（這將防止出現錯誤/404頁面，從而阻止瀏覽）。

### 使用Timewarp {#using-timewarp}

時間曲線是 [模式](/help/sites-authoring/author-environment-tools.md#page-modes) 的子菜單。 要啟動它，只需像切換其它模式一樣切換它。

1. 啟動要啟動Timewarp的頁面的編輯器，然後選擇 **時間曲線** 的子菜單。

   ![wwpv-01](assets/wwpv-01.png)

1. 在對話方塊中設定目標日期和時間，然後按一下或點選「設 **定日期」**。如果您未選取時間，則預設為目前時間。

   ![wwpv-02](assets/wwpv-02.png)

1. 根據日期集顯示頁面。 通過窗口頂部的藍色狀態欄來指示時間曲線模式。 使用狀態欄中的連結選擇新的目標日期或退出「時間曲線」模式。

   ![wwpv-03](assets/wwpv-03.png)

### 時間曲線限制 {#timewarp-limitations}

Timewarp會盡最大努力在選定的時間點再現頁面。 但是，由於中內容的連續創作非常複雜，AEM這並不總能實現。 使用Timewarp時應牢記這些限制。

* **基於已發佈頁面的Timewarp作品** - Timewarp只有在您以前已發佈該頁面時才能完全工作。 否則，timewarp將顯示作者環境中的當前頁面。
* **Timewarp使用頁面版本**  — 如果導航到已從儲存庫中刪除/刪除的頁面，則如果該頁面的舊版本仍在儲存庫中可用，則會正確呈現該頁面。
* **刪除的版本影響Timewarp**  — 如果從儲存庫中刪除了版本，則Timewarp無法顯示正確的視圖。

* **時間曲線為只讀**  — 無法編輯頁面的舊版本。 它僅可供查看。 如果要恢復舊版本，必須使用 [恢復](#reverting-to-a-page-version)。

* **時間曲線僅基於頁面內容**  — 如果用於呈現網站的元素（如代碼、css、資產/影像等）已更改，則視圖將不同於原來的視圖，因為這些項目未在儲存庫中進行版本控制。

>[!CAUTION]
>
>Timewarp是一種工具，可幫助作者理解和建立其內容。 它不打算作為審計日誌或用於法律目的。
