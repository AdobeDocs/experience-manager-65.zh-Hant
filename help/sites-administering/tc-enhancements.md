---
title: 翻譯增強
seo-title: Translation Enhancements
description: 中的翻譯增AEM強。
seo-description: Translation enhancements in AEM.
uuid: 0563603f-327b-48f1-ac14-6777c06734b9
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 42df2db3-4d3c-4954-a03e-221e2f548305
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 1be3d394283493f7c282ea4c3d794458d88e1ac3
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---

# 翻譯增強{#translation-enhancements}

本頁介紹了對翻譯管理功能的增量AEM增強和改進。

## 翻譯項目自動化 {#translation-project-automation}

已添加了一些選項來提高翻譯項目的工作效率，例如自動升級和刪除翻譯啟動，以及安排翻譯項目的定期執行。

1. 在翻譯項目中，按一下或點擊 **翻譯摘要** 平鋪。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切換到 **高級** 頁籤。 在底部，可以選擇 **自動升級翻譯啟動**。

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. （可選）在接收翻譯內容後，您可以選擇是否應自動提升和刪除翻譯啟動。

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 要選擇翻譯項目的循環執行，請選擇下拉框的頻率 **重複翻譯**。 定期項目執行將在指定的時間間隔內自動建立和執行翻譯作業。

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 多語言翻譯項目 {#multilingual-translation-projects}

可以在翻譯項目中配置多種目標語言，以減少建立的翻譯項目總數。

1. 在翻譯項目中，按一下或點擊 **翻譯摘要** 平鋪。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切換到 **高級** 頁籤。 可以在 **目標語言**。

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. 或者，如果要通過「站點」中的參照欄啟動翻譯，請添加語言並選擇 **建立多語言翻譯項目**。

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. 將在項目中為每個目標語言建立翻譯作業。 可以在項目內逐個啟動它們，也可以通過在「項目管理」中全局執行項目來同時啟動它們。

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## 翻譯記憶庫更新 {#translation-memory-updates}

翻譯內容的手動編輯可以同步回翻譯管理系統(TMS)以訓練其翻譯記憶庫。

1. 在「站點」控制台中，在已翻譯頁面中更新文本內容後，選擇 **更新翻譯記憶庫**。

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. 清單視圖顯示原始碼與已編輯的每個文本元件的翻譯的並排比較。 選擇應同步到翻譯記憶庫的翻譯更新，然後選擇 **更新記憶體**。

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

更AEM新配置TMS的翻譯儲存器中現有字串的翻譯。

* 該操作更新配置TMS的翻譯儲存器中現有字串的翻譯。
* 它不會建立新的翻譯作業。
* 它通過翻譯API(參見下AEM面)將翻譯發回TMS。

要使用此功能：

* 必須配置TMS以與一起使AEM用。
* 連接器需要實現該方法 [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html)。
   * 此方法中的代碼確定翻譯記憶庫更新請求發生的情況。
   * 轉AEM換框架通過該方法實現將字串值對（原始和更新的轉換）發回到TMS。

對於使用專有翻譯儲存器的情況，翻譯儲存器更新可以被截取併發送到定制目的地。

## 多級語言副本 {#language-copies-on-multiple-levels}

現在，語言根可以在節點下分組，例如按區域分組，同時仍被識別為語言副本的根。

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>只允許一個級別。 例如，以下內容不允許「es」頁解析為語言副本：
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>此 `es` 不會檢測到語言副本，因為它是2個級別（美洲/中美洲），遠離 `en` 的下界。

>[!NOTE]
>
>語言根可以具有任何頁名，而不只是語言的ISO代碼。 將AEM始終先檢查路徑和名稱，但如果頁面名稱未標識語言，則AEM將檢查頁面的cq:language屬性以識別語言。

## 翻譯狀態報告 {#translation-status-reporting}

現在，可以在「站點」清單視圖中選擇一個屬性，該屬性顯示頁面是已翻譯、正在翻譯還是尚未翻譯。 要顯示它，請執行以下操作：

1. 在站點中，切換到 **清單視圖。**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. 按一下或點擊 **查看設定**。

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. 檢查 **已翻譯** 複選框 **翻譯** 點擊/按一下 **更新**。

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

你現在可以看到 **已翻譯** 列，其中顯示頁面的轉換狀態。

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
