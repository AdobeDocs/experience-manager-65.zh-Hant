---
title: 頁面差異
seo-title: Page Diff
description: 頁面差異功能允許在突出顯示兩頁差異的情況下方便地進行並排比較。
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

內容建立是一個迭代過程。 創作時需要能夠看到從一個迭代到另一個迭代的更改。 查看一個頁面版本，然後查看另一個頁面版本效率低下且容易出錯。 作者希望能夠輕鬆地將當前頁面與另一個版本並排進行比較。

頁面差異功能允許在突出顯示兩頁差異的情況下方便地進行並排比較。

>[!TIP]
>
>請參閱 [開發和頁面差異](/help/sites-developing/pagediff.md#operation-details) 有關此功能的更多技術詳細資訊。

## 使用 {#use}

並排比較可以比較：

* [版本](/help/sites-authoring/working-with-page-versions.md#comparing-a-version-with-current-page)  — 當前狀態的頁面的早期版本
* [即時拷貝](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page)  — 即時複製及其藍圖
* [啟動](/help/sites-authoring/launches-editing.md#comparing-a-launch-page-to-its-source-page)  — 使用其源啟動
* [語言副本](/help/sites-administering/tc-manage.md#comparing-language-copies)  — 翻譯前後的頁面

請參閱有關如何在這些上下文中啟動差異的各主題。

### 差異的表示 {#presentation-of-differences}

無論比較的內容如何，差異的呈現方式都保持不變。

* 啟動差異時選擇的內容顯示在左側（差異入口點）。
* 比較內容顯示在右側（與所選內容進行比較）。

例如，如果比較版本，則當前版本顯示在左側，先前版本顯示在右側。

兩個頁面的源都清楚地顯示在瀏覽器窗口頂部的標題欄中。

![chlimage_1-109](assets/chlimage_1-109.png)

差異在元件和HTML級別檢測更改。 已更改的項會用不同顏色加亮。

**元件更改**

* 淺綠色 — 已添加元件
* 粉紅色 — 元件已移除

**HTML更改**

* 深綠色 — 已添加HTML
* 紅色 — HTML已刪除

>[!NOTE]
>
>在比較語言副本時，會取消突出顯示，因為在翻譯中，所有更改和突出顯示都無益。

### 全屏和退出 {#fullscreen-and-exiting}

為了關注特定內容，您可以按一下「並排」差異的任一「並排」全屏表徵圖，將其放大到全面瀏覽器窗口。

![](do-not-localize/chlimage_1-18.png)

選定的側面將填充整個窗口，但欄將保持在頂部，允許您在兩個頁面之間切換。

![chlimage_1-110](assets/chlimage_1-110.png)

也可以通過按一下退出全屏表徵圖來選擇關閉全屏視圖。

![](do-not-localize/chlimage_1-19.png)

通過按一下標題中的「關閉」按鈕，可以隨時退出並排差異。

## 限制 {#limitations}

在某些情況下，頁面差異可能無法檢測到預期的差異。

* 當差異版本和啟動時，差異不會考慮動態元件，如麵包屑、菜單、產品清單或徽標（依賴站點結構呈現其內容的元件）。
* 對於版本，差異不會重新建立訪問控制策略和即時複製關係。
* 如果移動了頁面，則無法再對移動前建立的任何版本執行差異。

   * 如果遇到差異問題，請檢查 [時間軸](/help/sites-authoring/basic-handling.md#timeline) ，查看是否已移動頁面。

>[!NOTE]
>
>版本無法相互比較。 只能將當前版本與頁面的其他版本進行比較。 當前版本始終是用更改突出顯示的版本。

>[!NOTE]
>
>有關頁面差異機制操作以及可能影響頁面差異的限制的詳細資訊，請參閱 [開發者文檔](/help/sites-developing/pagediff.md) 功能。
