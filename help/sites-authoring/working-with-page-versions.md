---
title: 使用頁面版本
seo-title: Working with Page Versions
description: 建立、比較和還原頁面的版本
seo-description: Create, compare, and restore versions of a page
uuid: 29e049f0-532c-4e3b-b64f-5be88ee6b08c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1368347a-9b65-4cfc-87e1-62993dc627fd
docset: aem65
exl-id: cb7a9da2-7112-4ef0-b1cf-211a7df93625
source-git-commit: b11a97b9b00e6f80fb0243e234ed1dc2c004ed3a
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 5%

---

# 使用頁面版本{#working-with-page-versions}

版本設定會在特定時間點建立頁面的「快照」。 使用版本設定，您可以執行下列動作：

* 建立頁面版本。
* 將頁面還原為舊版，以還原您對頁面所做的變更（例如）。
* 比較目前版本的頁面與先前版本，其文字和影像會反白顯示差異。

## 建立新版本 {#creating-a-new-version}

您可以從以下來源建立資源版本：

* the [時間軸邊欄](#creating-a-new-version-timeline)
* the [建立](#creating-a-new-version-create-with-a-selected-resource) 選項（選取資源時）

### 建立新版本 — 時間軸 {#creating-a-new-version-timeline}

1. 導覽以顯示您要建立版本的頁面。
1. 選取 [選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. 開啟 **時間表** 欄。
1. 按一下/點選註解欄位旁的箭頭，以顯示選項：

   ![screen-shot_2019-03-05at112335](assets/screen-shot_2019-03-05at112335.png)

1. 選擇 **另存為版本**.
1. 輸入 **標籤** 和 **註解** （如果需要）。

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. 使用確認新版本 **建立**.

   時間軸中的資訊將會更新，以指出新版本。

### 建立新版本 — 使用所選資源建立 {#creating-a-new-version-create-with-a-selected-resource}

1. 導覽以顯示您要建立版本的頁面。
1. 選取 [選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. 選取 **建立** 選項。
1. 對話方塊將會開啟。 您可以輸入 **標籤** 和 **註解** 如果需要：

   ![screen_shot_2012-02-15at105050am](assets/screen_shot_2012-02-15at105050am.png)

1. 使用確認新版本 **建立**.

   將開啟時間軸，其中會更新指示新版本的資訊。

## 恢復版本 {#reinstating-versions}

建立頁面版本後，有多種方法可重新安裝舊版：

* the **回復到此版本** 選項 [時間表](/help/sites-authoring/basic-handling.md#timeline) 邊欄

   恢復所選頁面的先前版本。

* the **還原** 選項 [動作工具列](/help/sites-authoring/basic-handling.md#actions-toolbar)

   * **還原版本**

      恢復當前所選資料夾中指定頁面的版本；這也可以包括還原先前已刪除的頁面。

   * **還原樹狀結構**

      在指定的日期和時間恢復整個樹的版本；這可能包括先前已刪除的頁面。

>[!NOTE]
>
>恢復頁面時，建立的版本將是新分支的一部分。
>
>以說明：
>
>1. 建立任何頁面的版本。
>1. 初始標籤和版本節點名稱將為1.0、1.1、1.2等。
>1. 恢復第一個版本；即1.0。
>1. 再次建立新版本。
>1. 產生的標籤和節點名稱現在會是1.0.0、1.0.1、1.0.2等。


### 回復到版本 {#revert-to-a-version}

結束日期 **還原** 選定頁面至上一版：

1. 導覽以顯示您要回復為舊版的頁面。
1. 選取 [選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。將列出所選頁面的頁面版本。
1. 選擇要恢復的版本。 可能的選項將顯示：

   ![還原為此版本](assets/screen-shot_2019-03-05at112505.png)

1. 選擇 **回復到此版本**. 將還原所選版本，並更新時間軸中的資訊。

### 還原版本 {#restore-version}

此方法可用來還原目前資料夾中指定頁面的版本；這也可以包括還原先前已刪除的頁面：

1. 導覽至和 [選取](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)，為必要資料夾。

1. 選擇 **還原**，然後 **還原版本** 從上方 [動作工具列](/help/sites-authoring/basic-handling.md#actions-toolbar).

   >[!NOTE]
   >
   >若：
   >
   >* 您選擇了單個頁面，該頁面從未有子頁面，
   >* 或資料夾中沒有任何頁面有版本，

   >
   >然後顯示會是空的，因為沒有適用的版本。

1. 將列出可用版本：

   ![還原版本 — 資料夾中所有頁的清單](/help/sites-authoring/assets/versions-restore-version-01.png)

1. 對於特定頁面，請使用下方的下拉式選取器 **還原到版本** 來選擇該頁面所需的版本。

   ![還原版本 — 選擇版本](/help/sites-authoring/assets/versions-restore-version-02.png)

1. 在主顯示畫面中，選取要還原的必要頁面：

   ![還原版本 — 選擇頁](/help/sites-authoring/assets/versions-restore-version-03.png)

1. 選擇 **還原** 針對所選版本，將選定頁面的還原為當前版本。

>[!NOTE]
>
>選擇所需頁面和相關版本的順序是可互換的。

### 還原樹狀結構 {#restore-tree}

此方法可用於在指定日期和時間還原樹的版本；其中可能包括先前已刪除的頁面：

1. 導覽至和 [選取](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)，為必要資料夾。

1. 選擇 **還原**，然後 **還原樹** 從上方 [動作工具列](/help/sites-authoring/basic-handling.md#actions-toolbar). 將顯示樹的最新版本：

   ![還原樹狀結構](/help/sites-authoring/assets/versions-restore-tree-02.png)

1. 在使用日期和時間選取器 **最新版本** 選擇樹的其他版本 — 要還原的版本。

1. 設定標幟 **保留的非版本頁面** 視需要：

   * 如果處於活動狀態（已選取），則任何非版本控制頁面都將受到維護，且不會受到還原的影響。

   * 如果非活動（未選中），則任何非版本化頁面都將被移除，因為這些頁面在版本化樹中不存在。

1. 選擇 **還原** 將要還原為 *電流* 版本。

## 預覽版本 {#previewing-a-version}

您可以預覽特定版本：

1. 導覽以顯示您要比較的頁面。
1. 選取 [選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。
1. 將列出頁面版本。 選擇要預覽的版本：

   ![screen-shot_2019-03-05at112505-1](assets/screen-shot_2019-03-05at112505-1.png)

1. 選擇 **預覽**. 頁面會顯示在新索引標籤中。

   >[!CAUTION]
   >
   >如果頁面已移動，則您無法再對移動前進行的任何版本執行預覽。
   >
   >* 如果預覽遇到問題，請核取 [時間表](/help/sites-authoring/basic-handling.md#timeline) ，查看頁面是否已移動。


## 比較版本與目前頁面 {#comparing-a-version-with-current-page}

若要比較舊版與目前頁面：

1. 導覽以顯示您要比較的頁面。
1. 選取 [選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。
1. 將列出頁面版本。 選取您要比較的版本：

   ![screen-shot_2019-03-05at112505-2](assets/screen-shot_2019-03-05at112505-2.png)

1. 選擇 **與目前比較**. 此 [頁面差異](/help/sites-authoring/page-diff.md) 會開啟並顯示差異。

## Timewarp {#timewarp}

時間扭曲功能是專為模擬 *已發佈* 過去特定時間的頁面狀態。

>[!TIP]
>
>[時間扭曲也可與啟動搭配使用，以預覽未來](/help/sites-authoring/launches.md) 執行AEM 6.5.10.0或更新版本時。

由於內容建立是持續進行的協作程式，因此「時間扭曲」的目的是讓作者追蹤一段時間內發佈的網站，以了解內容的變更情形。 此功能使用頁面版本來判斷發佈環境的狀態。

要執行此操作：

* 系統會尋找在選取時間處於作用中狀態的頁面版本。
* 這表示顯示的版本已建立/啟用 *befor* 時間扭曲中選取的時間點。
* 導覽至已刪除的頁面時，只要舊版頁面仍可在存放庫中使用，則也會呈現該頁面。
* 如果找不到已發佈的版本，則Timewarp會回復到製作環境上頁面的目前狀態（這是為了防止錯誤/404頁面，這會防止瀏覽）。

### 使用時間扭曲 {#using-timewarp}

時間扭曲是 [模式](/help/sites-authoring/author-environment-tools.md#page-modes) 頁面編輯器中。 要啟動它，只需像切換任何其他模式一樣切換它。

1. 啟動您要啟動Timewarp的頁面的編輯器，然後選取 **時間扭曲** 在模式選擇中。

   ![wwpv-01](assets/wwpv-01.png)

1. 在對話方塊中設定目標日期和時間，然後按一下或點選「設 **定日期」**。如果您未選取時間，則預設為目前時間。

   ![wwpv-02](assets/wwpv-02.png)

1. 頁面會根據日期集顯示。 時間扭曲模式會透過視窗頂端的藍色狀態列來指示。 使用狀態列中的連結來選取新的目標日期或退出時間扭曲模式。

   ![wwpv-03](assets/wwpv-03.png)

### 時間扭曲限制 {#timewarp-limitations}

時間扭曲會盡力在選取的時間點重制頁面。 不過，由於AEM中持續製作內容的複雜度，這並非總是可能的。 使用「時間扭曲」時，請謹記這些限制。

* **時間扭曲會根據已發佈的頁面運作**  — 只有在您先前已發佈頁面時，時間扭曲才會完全運作。 否則，時間扭曲會顯示製作環境上的目前頁面。
* **時間扭曲使用頁面版本**  — 如果您導覽至已從存放庫移除/刪除的頁面，如果存放庫中仍有舊版頁面，則會正確呈現該頁面。
* **移除的版本會影響時間扭曲**  — 如果從存放庫中移除版本，時間扭曲無法顯示正確的檢視。

* **時間扭曲為唯讀**  — 您無法編輯舊版頁面。 它僅供檢視。 如果您想要還原較舊的版本，則必須使用 [還原](#reverting-to-a-page-version).

* **時間扭曲僅根據頁面內容**  — 如果轉譯網站的元素（例如程式碼、CSS、資產/影像等）已變更，檢視會與原本不同，因為這些項目未在存放庫中版本化。

>[!CAUTION]
>
>Timewarp是專為協助作者了解及建立其內容而設計的工具。 此檔案並非作為稽核記錄檔，或用於法律用途。
