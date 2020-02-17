---
title: 使用頁面版本
seo-title: 使用頁面版本
description: 建立、比較和還原頁面版本
seo-description: 建立、比較和還原頁面版本
uuid: 29e049f0-532c-4e3b-b64f-5be88ee6b08c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1368347a-9b65-4cfc-87e1-62993dc627fd
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50

---


# 使用頁面版本{#working-with-page-versions}

版本修訂會在特定時間點建立頁面的「快照」。 使用版本控制，您可以執行下列動作：

* 建立頁面版本。
* 將頁面還原為舊版，以還原您對頁面所做的變更，例如。
* 比較目前版本的頁面與先前版本，其中反白顯示文字和影像的差異。

## 建立新版本 {#creating-a-new-version}

您可以從以下網址建立資源版本：

* 時間 [軸邊欄](#creating-a-new-version-timeline)
* 「創 [建](#creating-a-new-version-create-with-a-selected-resource) 」選項（選擇資源時）

### 建立新版本——時間軸 {#creating-a-new-version-timeline}

1. 導覽以顯示您要建立版本的頁面。
1. 在選擇模式 [下選擇頁](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟「時 **間軸** 」欄。
1. 按一下／點選注釋欄位旁的箭頭，以顯示選項：

   ![screen-shot_2019-03-05at112335](assets/screen-shot_2019-03-05at112335.png)

1. 選擇「 **另存為版本**」。
1. 如果需要， **請輸入** 「標 **簽」和「注釋** 」。

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. 使用「建立」確認新 **版本**。

   時間軸中的資訊將會更新，以指出新版本。

### 建立新版本——使用選定資源建立 {#creating-a-new-version-create-with-a-selected-resource}

1. 導覽以顯示您要建立版本的頁面。
1. 在選擇模式 [下選擇頁](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 從工具 **列中選** 取「建立」選項。
1. 對話方塊將會開啟。 如果需要，可 **以輸入** 「標籤」 **和「注釋** 」:

   ![screen_shot_2012-02-15at105050am](assets/screen_shot_2012-02-15at105050am.png)

1. 使用「建立」確認新 **版本**。

   時間軸將會開啟，並更新資訊以指出新版本。

## 回復為頁面版本 {#reverting-to-a-page-version}

建立版本後，您可視需要回復至該版本。

>[!NOTE]
>
>在恢復頁面時，所建立的版本將是新分支的一部分。
>
>要說明：

>1. 建立任何頁面的版本。
>1. 初始標籤和版本節點名稱為1.0、1.1、1.2等。
1. 恢復第一個版本；即1.0。
1. 再次建立新版本。
1. 產生的標籤和節點名稱現在會是1.0.0、1.0.1、1.0.2等。



要回復到以前的版本：

1. 導覽以顯示您要回復為舊版的頁面。
1. 在選擇模式 [下選擇頁](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。 將列出所選頁面的頁面版本。
1. 選擇要回復的版本。 可能的選項將顯示：

   ![screen-shot_2019-03-05at112505](assets/screen-shot_2019-03-05at112505.png)

1. Select **Revert to this Version**. 將還原所選版本，並更新時間軸中的資訊。

## 預覽版本 {#previewing-a-version}

您可以預覽特定版本：

1. 導覽以顯示您要比較的頁面。
1. 在選擇模式 [下選擇頁](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。
1. 將列出頁面版本。 選擇您要預覽的版本：

   ![screen-shot_2019-03-05at112505-1](assets/screen-shot_2019-03-05at112505-1.png)

1. 選擇「 **預覽**」。 頁面將顯示在新標籤中。

   >[!CAUTION]
   如果頁面已移動，您無法再對移動前進行的任何版本執行預覽。
   * 如果您在預覽時遇到問題，請檢查頁 [面的時間軸](/help/sites-authoring/basic-handling.md#timeline) ，以查看頁面是否已移動。


## 比較版本與目前頁面 {#comparing-a-version-with-current-page}

若要比較舊版與目前頁面：

1. 導覽以顯示您要比較的頁面。
1. 在選擇模式 [下選擇頁](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟「時 **間軸** 」欄，然後選 **取「全部顯示** 」 **或「版本**」。
1. 將列出頁面版本。 選擇要比較的版本：

   ![screen-shot_2019-03-05at112505-2](assets/screen-shot_2019-03-05at112505-2.png)

1. 選擇 **與目前比較**。 頁 [面差異](/help/sites-authoring/page-diff.md) ，會開啟並顯示差異。

## Timewarp {#timewarp}

時間彎曲是一種功能，可模 *擬過去* 特定時間頁面的發佈狀態。

由於內容建立是持續的協作程式，因此「時間彎曲」的目的是讓作者能夠隨時追蹤發佈的網站，以便瞭解內容的變更。 此功能使用頁面版本來判斷發佈環境的狀態。

要執行此操作：

* 系統會尋找在選取時間作用中的頁面版本。
* 這表示在「時間彎曲」中選取的時 *間點之前* ，已建立／啟動顯示的版本。
* 導航到已刪除的頁面時，也會呈現該頁面——只要該頁面的舊版本仍然在儲存庫中可用。
* 如果找不到發佈版本，則「時間彎曲」會回復為作者環境上頁面的目前狀態（這是為了防止發生錯誤/404頁面，這會防止瀏覽）。

### 使用時間彎曲 {#using-timewarp}

時間彎曲是頁 [面編輯](/help/sites-authoring/author-environment-tools.md#page-modes) 器的一種模式。 若要啟動它，只需像切換任何其他模式一樣來切換它。

1. 啟動您要啟動「時間彎曲」頁面的編輯器，然後在模式選 **擇中選擇** 「時間彎曲」。

   ![wwpv-01](assets/wwpv-01.png)

1. 在對話方塊中設定目標日期和時間，然後按一下或點選「設 **定日期」**。 如果您未選取時間，則預設為目前時間。

   ![wwpv-02](assets/wwpv-02.png)

1. 頁面會根據日期集顯示。 時間彎曲模式會透過視窗頂端的藍色狀態列來指示。 使用狀態列中的連結來選取新的目標日期或退出時間彎曲模式。

   ![wwpv-03](assets/wwpv-03.png)

### 時間彎曲限制 {#timewarp-limitations}

時間彎曲會盡力在選取的時間點重制頁面。 不過，由於AEM中持續製作內容十分複雜，因此並非總能做到。 當您使用Timewarp時，應牢記這些限制。

* **時間彎曲會根據已發佈的頁面運作** -只有在您先前已發佈頁面時，時間彎曲才會完全運作。 如果不是，時間彎曲會顯示作者環境中的目前頁面。
* **時間彎曲使用頁面版本** -如果您導覽至已從儲存庫中移除／刪除的頁面，如果舊版頁面仍在儲存庫中，則會正確呈現該頁面。
* **刪除的版本會影響「時間彎曲** 」 —— 如果從儲存庫中刪除版本，則「時間彎曲」無法顯示正確的視圖。

* **時間彎曲為唯讀** -您無法編輯舊版頁面。 僅供檢視。 如果要恢復舊版，則必須使用恢復手動執行 [操作](#reverting-to-a-page-version)。

* **時間彎曲僅基於頁面內容** -如果轉換網站的元素（例如程式碼、css、資產／影像等）已變更，檢視會與原本的檢視不同，因為這些項目未在儲存庫中版本化。

>[!CAUTION]
時間彎曲功能是設計為工具，可協助作者瞭解並建立其內容。 它不是作為審計日誌或用於法律目的。
