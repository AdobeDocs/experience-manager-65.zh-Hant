---
title: 翻譯增強功能
description: AEM翻譯管理功能的漸進式增強和細化。
topic-tags: site-features
content-type: reference
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# 翻譯增強功能{#translation-enhancements}

此頁面顯示AEM翻譯管理功能的遞增增強功能和細化。

## 翻譯專案自動化 {#translation-project-automation}

已新增選項，以提升使用翻譯專案的生產力，例如自動提升和刪除翻譯啟動，以及排程翻譯專案的週期性執行。

1. 在您的翻譯專案中，按一下 **翻譯摘要** 圖磚。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切換至 **進階** 標籤。 在底部，您可以選取 **自動提升翻譯啟動**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. 或者，您可以選擇在收到翻譯內容後，是否應該自動提升和刪除翻譯啟動。

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 若要選取翻譯專案的循環執行，請選取頻率（在下方下拉式清單中） **重複翻譯**. 週期性專案執行將在指定的時間間隔內自動建立和執行翻譯工作。

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 多語言翻譯專案 {#multilingual-translation-projects}

您可以在翻譯專案中設定多種目標語言，以減少建立的翻譯專案總數。

1. 在您的翻譯專案中，按一下 **翻譯摘要** 圖磚。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切換至 **進階** 標籤。 您可以在下列位置新增多種語言 **目標語言**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. 或者，如果您要透過Sites中的參照邊欄啟動翻譯，請新增您的語言並選取 **建立多語言翻譯專案**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. 翻譯工作將在專案中針對每種目標語言建立。 您可以在專案中逐一啟動，或透過在專案管理員中全域執行專案來一次啟動。

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## 翻譯記憶更新 {#translation-memory-updates}

翻譯內容的手動編輯可以同步回翻譯管理系統(TMS)，以訓練其翻譯記憶庫。

1. 在網站主控台中，更新翻譯頁面中的文字內容後，選取 **更新翻譯記憶庫**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. 清單檢視會顯示每個已編輯文字元件的來源與翻譯的並排比較。 選取應將哪些翻譯更新同步至翻譯記憶庫，然後選取 **更新記憶體**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

AEM會更新已設定TMS的翻譯記憶庫中現有字串的翻譯。

* 動作會更新已設定TMS的翻譯記憶庫中現有字串的翻譯。
* 它不會建立新的翻譯工作。
* 它會透過AEM翻譯API （請參閱下文）將翻譯傳回TMS。

若要使用此功能：

* TMS必須設定為可與AEM搭配使用。
* 聯結器需要實作方法 [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html).
   * 此方法中的程式碼會決定翻譯記憶體更新請求的情況。
   * AEM翻譯架構會透過此方法實作，將字串值配對（原始和更新的翻譯）傳送回TMS。

在使用專有翻譯記憶庫的情況下，可以攔截翻譯記憶庫更新並傳送到自訂目的地。

## 多個層級的語言副本 {#language-copies-on-multiple-levels}

語言根現在可以在節點下分組（例如，按區域），同時仍被識別為語言副本的根。

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>只允許一個層級。 例如，下列專案不會允許&quot;es&quot;頁面解析為語言副本：
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>這個 `es` 系統不會偵測到語言副本，因為它位於2個層級（美洲/中美洲） `en` 節點。

>[!NOTE]
>
>語言根可以有任何頁面名稱，而不僅僅是語言的ISO程式碼。 AEM一律會先檢查路徑和名稱，但如果頁面名稱未識別語言，AEM會檢查頁面的cq：language屬性以取得語言識別。

## 翻譯狀態報表 {#translation-status-reporting}

現在，您可以在網站清單檢視中選取屬性，以顯示頁面是否已翻譯、正在翻譯或尚未翻譯。 若要顯示它：

1. 在Sites中，切換至 **清單檢視。**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. 按一下 **檢視設定**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. 檢查 **已翻譯** 核取方塊於 **翻譯** 並按一下 **更新**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

您現在可以看到 **已翻譯** 欄，其中顯示頁面的翻譯狀態。

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
