---
title: 頁面差異
seo-title: Page Diff
description: 頁面差異功能可方便地並排比較兩個頁面，並強調顯示其差異。
seo-description: The page diff feature allows for the convenient side-by-side comparison of two pages with their differences highlighted.
uuid: 5af8b466-5922-4fe6-9eae-7bad99be23e0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8386a16a-9d47-46d5-bc60-5f290c59e60e
docset: aem65
exl-id: 3beea5cd-5ae0-485b-8dfc-8b3a23c11586
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# 頁面差異{#page-diff}

## 簡介 {#introduction}

內容建立是一個迭代過程。 以效率製作需要能夠查看從一個迭代到另一個迭代的更改。 檢視一個頁面版本，而另一個頁面版本則效率低下且容易出錯。 作者想要輕鬆並排比較目前的頁面與其他版本。

頁面差異功能可方便地並排比較兩個頁面，並強調顯示其差異。

>[!TIP]
>
>請參閱 [開發與頁面差異](/help/sites-developing/pagediff.md#operation-details) 如需此功能的詳細技術資訊。

## 使用 {#use}

並排差異可以比較：

* [版本](/help/sites-authoring/working-with-page-versions.md#comparing-a-version-with-current-page)  — 具有其當前狀態的頁面的早期版本
* [Live Copies](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page) - Live Copy及其Blueprint
* [啟動](/help/sites-authoring/launches-editing.md#comparing-a-launch-page-to-its-source-page)  — 透過其來源啟動
* [語言副本](/help/sites-administering/tc-manage.md#comparing-language-copies)  — 翻譯前後的頁面（重新）

請參閱有關如何在這些內容中啟動差異的各個主題。

### 差異的表示 {#presentation-of-differences}

無論比較的內容為何，差異的呈現方式都保持不變。

* 啟動差異時選擇的內容顯示在左側（差異入口點）。
* 比較內容會顯示在右側（比較所選內容的對象）。

例如，如果比較版本，則當前版本顯示在左側，而上一版本顯示在右側。

兩個頁面的來源會清楚顯示在瀏覽器視窗頂端的標題列中。

![chlimage_1-109](assets/chlimage_1-109.png)

差異會在元件和HTML層級偵測變更。 已變更的項目會以不同顏色強調顯示。

**元件變更**

* 淺綠色 — 新增元件
* 粉紅色 — 元件已移除

**HTML變更**

* 深綠色 — 新增HTML
* 紅色 — 已移除HTML

>[!NOTE]
>
>比較語言副本時，會停用醒目提示，因為在翻譯中，所有變更和醒目提示都沒有好處。

### 全螢幕和退出 {#fullscreen-and-exiting}

若要著重於特定內容，您可以按一下並排差異的任一「側」全螢幕圖示，將其放大至完整瀏覽器視窗。

![](do-not-localize/chlimage_1-18.png)

選取的一側會填入整個視窗，但長條會保留在頂端，讓您在兩頁之間切換。

![chlimage_1-110](assets/chlimage_1-110.png)

您也可以按一下退出全螢幕圖示，以選擇關閉全螢幕檢視。

![](do-not-localize/chlimage_1-19.png)

您可以隨時按一下標題中的「關閉」按鈕，以退出並排差異。

## 限制 {#limitations}

在某些情況下，頁面差異可能無法如預期般偵測到差異。

* 差異版本和啟動時，差異不會考慮階層連結、功能表、產品清單或標誌等動態元件（依賴網站結構呈現其內容的元件）。
* 對於版本，差異不會重新建立訪問控制策略和即時副本關係。
* 如果移動了頁面，則無法再對移動前進行的任何版本執行差異。

   * 如果您遇到差異問題，請檢查 [時間表](/help/sites-authoring/basic-handling.md#timeline) ，查看頁面是否已移動。

>[!NOTE]
>
>無法相互比較版本。 只能比較目前版本的頁面。 目前版本一律為醒目提示並變更的版本。

>[!NOTE]
>
>有關頁面差異機制操作以及可能影響頁面差異的限制的詳細資訊，請參見 [開發人員檔案](/help/sites-developing/pagediff.md) 功能。
