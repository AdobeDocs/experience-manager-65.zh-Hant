---
title: HTML5 表單的螢幕閱讀器
description: 列出HTML5表單支援的熒幕助讀程式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: HTML5 Forms,Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 3%
---
# HTML5 表單的螢幕閱讀器 {#screen-readers-for-html-forms}

HTML5 forms元件會將XFA表單範本轉譯為HTML5格式。 支援HTML5的所有標準瀏覽器都可以轉譯這些表單。 為了在PDF和HTML5表單中支援類似的資料擷取體驗，PDF forms的版面配置保留在HTML5表單中。

HTML5 forms使用標準的HTML建構，可讓HTML的常規協助工具用於這些表單。 如果表單是根據無障礙表單的最佳實務而設計，則可與任何支援的熒幕助讀程式搭配使用。 此外，這類表單已啟用鍵盤導覽。

## 協助工具標準 {#accessibility-standards}

HTML5 forms符合第508條，具有已知例外狀況的協助工具。 如需詳細資訊，請參閱HTML5表單的[VPAT](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf)。

## HTML5表單的認證熒幕助讀程式 {#certified-screen-readers-for-html-forms}

* ® Windows上的JAWS 14.0
* macOS X和iPad上的VoiceOver

### JAWS {#jaws}

所有預設按鍵和捷徑都適用於HTML5表單。 如需使用JAWS的詳細資訊，請造訪[https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp)。

### 配音 {#voiceover}

HTML5 forms支援所有預設的按鍵動作和配音手勢。 如需設定和使用VoiceOver的詳細資訊，請參閱[https://www.apple.com/accessibility/vision/](https://www.apple.com/accessibility/vision/)。

## 已知問題 {#known-issues}

* **（僅限Internal Explorer 9）**&#x200B;在HTML5表單中，頁面會隨選載入（動態）。 隨選頁面載入導致熒幕朗讀程式的功能發生問題。 當熒幕助讀程式的焦點在頁面的最後一個欄位上，且使用者按下Tab鍵時，熒幕助讀程式會將焦點返回到表單上第一頁的第一個欄位。
* **（僅限Internal Explorer 9）** HTML5表單中的日期選擇器控制項無法完全使用鍵盤存取。 在「日期選擇器」控制項中，如果多次按「向上/向下」鍵，「日期選擇器」控制項會關閉，且焦點會移至下一個/最後一個欄位。

* VoiceOver無法在iPad safari上的日期Widget上偵測到方向鍵。
