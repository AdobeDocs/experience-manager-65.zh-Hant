---
title: 頁面差異
seo-title: Page Diff
description: 頁面差異功能可方便的對兩個頁面進行並排比較，並反白顯示其差異。
seo-description: The page diff feature allows for the convenient side-by-side comparison of two pages with their differences highlighted.
uuid: 5af8b466-5922-4fe6-9eae-7bad99be23e0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8386a16a-9d47-46d5-bc60-5f290c59e60e
docset: aem65
exl-id: 3beea5cd-5ae0-485b-8dfc-8b3a23c11586
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---

# 頁面差異{#page-diff}

## 簡介 {#introduction}

內容建立是一個反複的過程。 以高效率撰寫需要能夠檢視反複專案之間的變更。 檢視一個頁面版本然後檢視另一個頁面版本會效率低下，並容易發生錯誤。 作者希望能夠輕鬆地將目前頁面與其他版本並排比較。

頁面差異功能可方便的對兩個頁面進行並排比較，並反白顯示其差異。

>[!TIP]
>
>另請參閱 [開發和頁面差異](/help/sites-developing/pagediff.md#operation-details) 以取得此功能的詳細技術資訊。

## 使用 {#use}

可以並排比較：

* [版本](/help/sites-authoring/working-with-page-versions.md#comparing-a-version-with-current-page)  — 具有目前狀態的舊版頁面
* [即時副本](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page)  — 即時副本與其Blueprint
* [啟動](/help/sites-authoring/launches-editing.md#comparing-a-launch-page-to-its-source-page)  — 以其來源啟動
* [語言副本](/help/sites-administering/tc-manage.md#comparing-language-copies)  — 將翻譯之前和翻譯之後（重新翻譯）的頁面進行比較

請參閱相關主題，瞭解如何在這些內容中開始差異。

### 差異的呈現 {#presentation-of-differences}

無論比較的內容為何，差異的呈現方式均相同。

* 開始差異時選取的內容會顯示在左側（差異進入點）。
* 比較對象內容會顯示在右側（與所選內容進行比較的內容）。

例如，如果比較版本，目前版本會顯示在左側，而先前版本會顯示在右側。

兩個頁面的來源會清楚顯示在瀏覽器視窗頂端的標題列中。

![標題中顯示的來源](assets/chlimage_1-109.png)

差異會偵測元件和HTML層級的變更。 已變更的專案會以不同的顏色反白。

**元件變更**

* 淺綠色 — 已新增元件
* 粉紅色 — 已移除元件

**HTML變更**

* 深綠色 — 新增HTML
* 紅色 — 已移除HTML

>[!NOTE]
>
>比較語言副本時，反白顯示會停用，因為在翻譯中，所有變更和反白顯示都沒有好處。

### 全熒幕和正在退出 {#fullscreen-and-exiting}

若要聚焦於特定內容，您可以按一下並排差異比較任一邊的全熒幕圖示，將其放大至整個瀏覽器視窗。

![全熒幕模式圖示](do-not-localize/chlimage_1-18.png)

選取的一側會填滿整個視窗，但長條會保留在頂端，讓您在兩個頁面之間切換。

![頂端列可讓您切換頁面](assets/chlimage_1-110.png)

您也可以選擇按一下退出全熒幕圖示來關閉全熒幕檢視。

![關閉全熒幕](do-not-localize/chlimage_1-19.png)

您可以按一下標頭中的關閉按鈕，隨時結束並排的差異。

## 限制 {#limitations}

在某些情況下，頁面差異可能不會如預期偵測到差異。

* 不同版本和啟動時，差異不會考慮階層連結、功能表、產品清單或標誌（依賴網站結構呈現其內容的元件）等動態元件。
* 對於版本，差異不會重新建立存取控制原則與即時副本關係。
* 如果頁面已移動，您將無法再執行與移動前所做的任何版本之間的差異。

   * 如果您遇到差異問題，請檢查 [時間表](/help/sites-authoring/basic-handling.md#timeline) ，以檢視頁面是否已移動。

>[!NOTE]
>
>版本無法相互比較。 只有目前版本可以和頁面的其他版本比較。 目前的版本永遠是醒目提示變更的版本。

>[!NOTE]
>
>如需有關頁面差異機制的操作，以及可能影響頁面差異的限制的詳細資訊，請參閱 [開發人員檔案](/help/sites-developing/pagediff.md) 此功能的設定檔。
