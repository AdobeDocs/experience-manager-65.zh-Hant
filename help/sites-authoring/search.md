---
title: 完整搜尋
description: 透過全面搜尋，更快找到您的內容。
uuid: 21605b96-b467-4d01-9a64-9d0648d539f1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 4ec15013-f7ab-44d6-8053-ed28b14f95e2
docset: aem65
exl-id: dd65b308-c449-4f64-9f46-0797b922910f
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 6%

---

# 搜尋{#searching}

AEM的製作環境提供多種搜尋內容的機制，視資源型別而定。

>[!NOTE]
>
>在製作環境外，也可使用其他機制進行搜尋，例如 [查詢產生器](/help/sites-developing/querybuilder-api.md) 和 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## 搜尋基本需知 {#search-basics}

可從頂端工具列搜尋專案：

![](do-not-localize/chlimage_1-17.png)

您可以使用搜尋邊欄來：

* 搜尋特定的關鍵字、路徑或標籤。
* 根據資源特定條件進行篩選，例如修改日期、頁面狀態、檔案大小等。
* 定義並使用 [已儲存的搜尋](#saved-searches)  — 根據上述條件。

>[!NOTE]
>
>也可以使用快速鍵叫用搜尋 `/` （正斜線）。

## 搜尋和篩選 {#search-and-filter}

若要搜尋和篩選資源：

1. 開啟 **搜尋** （使用工具列中的放大鏡）並輸入搜尋字詞。 將會提出建議並可加以選取：

   ![s-01](assets/s-01.png)

   依預設，搜尋結果將限於您目前的位置（即主控台和相關資源型別）：

   ![screen_shot_2018-03-23at101445](assets/screen_shot_2018-03-23at101445.png)

1. 如有需要，您可以移除位置篩選器(選取 **X** ，以搜尋所有主控台/資源型別。
1. 將顯示結果，並根據控制檯和相關資源型別分組。

   您可以選取特定資源（供後續動作使用），或透過選取所需的資源型別向下展開；例如 **檢視所有網站**：

   ![screen-shot_2019-03-05at101900](assets/screen-shot_2019-03-05at101900.png)

1. 如果您想要進一步向下切入，請選取「邊欄」符號（左上方）以開啟側面板 **篩選和選項**.

   ![](do-not-localize/screen_shot_2018-03-23at101542.png)

   根據資源型別，搜尋將顯示預先定義的搜尋/篩選條件選擇。

   側面板可讓您選取：

   * 已儲存的搜尋
   * 搜尋目錄
   * 標記
   * 搜尋條件；例如，修改日期、發佈狀態、即時副本狀態。

   >[!NOTE]
   >
   >搜尋條件可能有所不同：
   >
   >
   >
   >    * 根據您選取的資源型別，例如Assets和Communities條件具有專業化是可以理解的。
   >    * 您的執行個體為 [搜尋Forms](/help/sites-administering/search-forms.md) 可自訂(適用於AEM內的位置)。


   ![screen-shot_2019-03-05at102509](assets/screen-shot_2019-03-05at102509.png)

1. 您也可以新增其他搜尋詞：

   ![screen-shot_2019-03-05at102613](assets/screen-shot_2019-03-05at102613.png)

1. 使用 **X** (右上方 **** )關閉搜尋。

>[!NOTE]
>
>在搜尋結果中選取專案時，搜尋條件會持續存在。
>
>當您在搜尋結果頁面上選取專案時，當使用瀏覽器返回按鈕後返回搜尋頁面時，搜尋條件會保留。

## 已儲存的搜尋 {#saved-searches}

除了依各種Facet進行搜尋外，您也可以儲存特定的搜尋設定以供擷取，並用於後續階段：

1. 定義搜尋條件並選取 **儲存**.

   ![screen-shot_2019-03-05at102613-1](assets/screen-shot_2019-03-05at102613-1.png)

1. 指派名稱，然後使用 **儲存** 確認：

   ![screen-shot_2019-03-05at102725](assets/screen-shot_2019-03-05at102725.png)

1. 下次存取搜尋面板時，您儲存的搜尋將可從選取器取得：

   ![screen-shot_2019-03-05at102927](assets/screen-shot_2019-03-05at102927.png)

1. 儲存後，您可以：

   * 使用 **x** （針對已儲存搜尋的名稱）以開始新查詢（不會刪除已儲存搜尋本身）。
   * **編輯已儲存的搜尋**，變更搜尋條件，然後 **儲存** 再來一次。

通過選擇保存的搜索並按一下搜索面板底部的「編 **輯保存的搜索** 」(Edit Saved Search)，可以修改保存的搜索。

![screen-shot_2019-03-05at103010](assets/screen-shot_2019-03-05at103010.png)
