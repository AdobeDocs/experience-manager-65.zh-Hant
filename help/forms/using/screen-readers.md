---
title: HTML5窗體的螢幕閱讀器
seo-title: Screen readers for HTML5 forms
description: 列出HTML5窗體支援的螢幕閱讀器。
seo-description: Lists the screen readers supported with HTML5 forms.
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# HTML5窗體的螢幕閱讀器 {#screen-readers-for-html-forms}

HTML5表單元件將XFA表單模板呈現為HTML5格式。 所有支援HTML5的標準瀏覽器都可以呈現這些表單。 為支援跨PDF和HTML5表單的類似資料捕獲體驗，PDF forms的佈局將保留在HTML5表單中。

HTML5表單使用標準HTML結構，允許與這些表單一起使用常規的HTML輔助工具。 如果表單是按照可訪問表單的最佳做法設計的，則它可與任何受支援的螢幕閱讀器配合使用。 此外，還為鍵盤導航啟用了這種表單。

## 無障礙標準 {#accessibility-standards}

HTML5表單符合第508節中已知例外的輔助功能。 請參閱 [用於HTML5表單的VPAT](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf) 的雙曲餘切值。

## 經認證的HTML5窗體螢幕閱讀器 {#certified-screen-readers-for-html-forms}

* Microsoft® Windows上的JAWS 14.0
* macOSX和iPad

### 大白鯊 {#jaws}

所有預設擊鍵和快捷方式都適用於HTML5表單。 有關使用JAWS的詳細資訊，請訪問 [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp)。

### 語音轉換 {#voiceover}

HTML5表單支援Voice over的所有預設擊鍵和手勢。 有關設定和使用VoiceOver的詳細資訊，請參見 [https://www.apple.com/accessibility/vision/](https://www.apple.com/accessibility/vision/)。

## 已知問題 {#known-issues}

* **（僅限內部資源管理器9）** 在HTML5窗體中，頁面按需（動態）載入。 按需頁面載入導致螢幕閱讀器功能出現問題。 當螢幕閱讀器的焦點位於頁面的最後一個欄位上並且用戶按下頁籤時，螢幕閱讀器將焦點返回到表單上第一頁的第一個欄位。
* **（僅限內部資源管理器9）** HTML5窗體中的「日期選取器」控制項無法通過鍵盤完全訪問。 在「日期選取器」(Date Picker)控制項中，如果多次按上/下鍵，則「日期選取器」(Date Picker)控制項將關閉，焦點將移至下一個/最後一個欄位。

* VoiceOver在iPad野生動物園旅行中無法檢測日期小部件上的箭頭鍵。
