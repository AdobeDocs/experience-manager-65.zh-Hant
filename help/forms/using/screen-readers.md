---
title: HTML5表單的螢幕閱讀程式
seo-title: HTML5表單的螢幕閱讀程式
description: 列出HTML5表單支援的螢幕閱讀程式。
seo-description: 列出HTML5表單支援的螢幕閱讀程式。
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 1%

---


# HTML5表單的螢幕閱讀程式{#screen-readers-for-html-forms}

HTML5表單元件會將XFA表單範本轉換為HTML5格式。 所有支援HTML5的標準瀏覽器都可轉換這些表格。 為支援跨PDF和HTML5表單的類似資料擷取體驗，HTML5表單會保留PDF forms的版面配置。

HTML5表格使用標準的HTML結構，可讓HTML的一般協助工具搭配這些表格使用。 如果表單是根據可存取表單的最佳實務設計，則可搭配任何支援的螢幕閱讀程式使用。 此外，這類表單可用於鍵盤導覽。

## 協助工具標準{#accessibility-standards}

HTML5表格符合第508節中已知例外的協助工具規定。 如需詳細資訊，請參閱[VPAT for HTML5 forms](https://www.adobe.com/mena_en/accessibility/compliance/livecycle-mobile-forms-es4-section-508-vpat.html)。

## HTML5表單{#certified-screen-readers-for-html-forms}的認證螢幕閱讀程式

* Microsoft Windows上的JAWS 14.0
* Mac OS X和iPad上的VoiceOver

### JAWS {#jaws}

所有預設的按鍵輸入和快速鍵都適用於HTML5表格。 有關使用JAWS的更多資訊，請訪問[https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp)。

### VoiceOver {#voiceover}

HTML5表格支援Voice over的所有預設按鍵和手勢。 有關設定和使用VoiceOver的詳細資訊，請參閱[https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/)。

## 已知問題 {#known-issues}

* **（僅限內部檔案總管9）** 在HTML5表單中，頁面會隨選載入（動態）。隨選頁面載入會造成螢幕閱讀程式的運作問題。 當螢幕閱讀器的焦點位於頁面的最後一個欄位，而使用者按下標籤時，螢幕閱讀器不會將焦點設定在下一頁的第一個欄位上，而會將焦點返回表單第一頁的第一個欄位。
* **（僅限內部瀏覽器9）** HTML5表單中的「日期選擇器」控制項無法透過鍵盤完全存取。在「日期選擇器」控制項中，如果您多次按向上／向下鍵，「日期選擇器」控制項會關閉，焦點會移至下一個／最後一個欄位。

* iPad safari上的日期介面工具集上的VoiceOver無法偵測到方向鍵。
