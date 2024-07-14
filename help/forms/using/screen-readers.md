---
title: HTML5表單的熒幕助讀程式
description: 列出HTML5表單支援的熒幕助讀程式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: HTML5 Forms,Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# HTML5表單的熒幕助讀程式 {#screen-readers-for-html-forms}

HTML5表單元件會將XFA表單範本轉譯為HTML5格式。 支援HTML5的所有標準瀏覽器都可以轉譯這些表單。 為了支援跨PDF和HTML5表單的類似資料擷取體驗，PDF forms版面配置會保留在HTML5表單中。

HTML5表單會使用標準的HTML建構，以便讓一般的HTML協助工具可搭配這些表單使用。 如果表單是根據無障礙表單的最佳實務而設計，則可與任何支援的熒幕助讀程式搭配使用。 此外，這類表單已啟用鍵盤導覽。

## 協助工具標準 {#accessibility-standards}

HTML5表單符合協助工具的第508條，但有已知例外。 如需詳細資訊，請參閱HTML5表單的[VPAT](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf)。

## HTML5表單的認證熒幕閱讀程式 {#certified-screen-readers-for-html-forms}

* Microsoft® Windows上的JAWS 14.0
* macOS X和iPad上的VoiceOver

### JAWS {#jaws}

所有預設按鍵和捷徑都適用於HTML5表單。 如需使用JAWS的詳細資訊，請造訪[https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp)。

### 配音 {#voiceover}

HTML5表單支援所有預設的按鍵動作和配音手勢。 如需設定和使用VoiceOver的詳細資訊，請參閱[https://www.apple.com/accessibility/vision/](https://www.apple.com/accessibility/vision/)。

## 已知問題 {#known-issues}

* **（僅限Internal Explorer 9）**&#x200B;在HTML5表單中，頁面會隨選載入（動態）。 隨選頁面載入導致熒幕朗讀程式的功能發生問題。 當熒幕助讀程式的焦點在頁面的最後一個欄位上，且使用者按下Tab鍵時，熒幕助讀程式會將焦點返回到表單上第一頁的第一個欄位。
* **（僅限Internal Explorer 9）** HTML5表單中的日期選擇器控制項無法完全使用鍵盤存取。 在「日期選擇器」控制項中，如果多次按「向上/向下」鍵，「日期選擇器」控制項會關閉，且焦點會移至下一個/最後一個欄位。

* VoiceOver無法在iPad safari上的日期Widget上偵測到方向鍵。
