---
title: HTML5表單的螢幕助讀程式
seo-title: HTML5表單的螢幕助讀程式
description: 列出HTML5表單支援的螢幕助讀程式。
seo-description: 列出HTML5表單支援的螢幕助讀程式。
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: 行動表單
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 1%

---

# HTML5表單的螢幕助讀程式{#screen-readers-for-html-forms}

HTML5表單元件會將XFA表單範本轉譯為HTML5格式。 所有支援HTML5的標準瀏覽器都可轉譯這些表單。 為支援PDF和HTML5表單的類似資料擷取體驗，PDF forms的版面會保留在HTML5表單中。

HTML5表單使用標準HTML結構，可讓HTML的一般協助工具與這些表單搭配使用。 如果表單是根據無障礙表單的最佳實務設計，則可搭配任何支援的螢幕助讀程式使用。 此外，還啟用了鍵盤導航。

## 無障礙標準{#accessibility-standards}

HTML5表單符合第508節中已知例外的協助工具規定。 如需詳細資訊，請參閱HTML5表單的[VPAT](https://www.adobe.com/mena_en/accessibility/compliance/livecycle-mobile-forms-es4-section-508-vpat.html) 。

## HTML5表單的認證螢幕閱讀器{#certified-screen-readers-for-html-forms}

* Microsoft Windows上的JAWS 14.0
* Mac OS X和iPad上的VoiceOver

### 下頜 {#jaws}

所有預設鍵擊和快捷方式都適用於HTML5表單。 有關使用JAWS的詳細資訊，請訪問[https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp)。

### VoiceOver {#voiceover}

HTML5表單支援語音傳遞的所有預設鍵擊和手勢。 有關設定和使用VoiceOver的詳細資訊，請參閱[https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/)。

## 已知問題 {#known-issues}

* **（僅限內部Explorer 9）** 在HTML5表單中，頁面會依需求（動態）載入。隨需頁面載入會造成螢幕助讀程式運作問題。 當螢幕助讀程式的焦點位於頁面的最後一個欄位，且使用者按下索引標籤時，螢幕助讀程式不會將焦點設定在下一頁的第一個欄位上，而會將焦點返回表單第一頁的第一個欄位。
* **（僅限內部Explorer 9）** HTML5表單中的「日期選取器」控制項無法透過鍵盤完全存取。在「日期選擇器」控制項中，如果多次按上/下鍵，「日期選擇器」控制項將關閉，焦點將移到下一個/最後一個欄位。

* 在iPad Safari上，VoiceOver無法偵測日期介面工具集上的方向鍵。
