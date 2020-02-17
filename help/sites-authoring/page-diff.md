---
title: 頁面差異
seo-title: 頁面差異
description: 頁面比較功能可方便並排比較兩頁的差異。
seo-description: 頁面比較功能可方便並排比較兩頁的差異。
uuid: 5af8b466-5922-4fe6-9eae-7bad99be23e0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8386a16a-9d47-46d5-bc60-5f290c59e60e
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# 頁面差異{#page-diff}

## 簡介 {#introduction}

內容建立是一個反覆的過程。 製作具效率的內容需要能夠查看從一個迭代到另一個迭代的變化。 檢視一個頁面版本，然後檢視另一個頁面版本則無效率且容易出錯。 作者希望能夠輕鬆並排比較目前的頁面與其他版本。

頁面比較功能可方便並排比較兩頁的差異。

>[!CAUTION]
>
>用戶必須對節 **點具有「修改／建立／刪除** 」權 `/content/versionhistory` 限，才能使用該功能。
>
>如需 [此功能的詳細技術資訊，請參閱開發與頁面比較](/help/sites-developing/pagediff.md#operation-details) 。

## 使用 {#use}

並排比較可以比較：

* [版本](/help/sites-authoring/working-with-page-versions.md#comparing-a-version-with-current-page) -頁面的舊版，其目前狀態
* [即時副本](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page) -即時副本及其藍圖
* [啟動](/help/sites-authoring/launches-editing.md#comparing-a-launch-page-to-its-source-page) -啟動及其來源
* [語言副本](/help/sites-administering/tc-manage.md#comparing-language-copies) -翻譯前後的頁面

請參見有關如何在這些上下文中啟動差異的各個主題。

### 差異的呈現 {#presentation-of-differences}

無論比較的內容為何，比較的呈現方式都保持不變。

* 啟動比較時選擇的內容將顯示在左側（比較入口點）。
* 比較內容會顯示在右側（與所選內容比較的內容）。

例如，如果比較版本，則目前版本會顯示在左側，而舊版則會顯示在右側。

這兩個頁面的來源會清楚地顯示在瀏覽器視窗頂端的標題列中。

![chlimage_1-109](assets/chlimage_1-109.png)

比較會檢測元件和HTML級別的更改。 已變更的項目會以不同的顏色加亮顯示。

**元件變更**

* 淺綠色——已添加元件
* 粉紅色——元件已移除
* 藍色——元件已更改
* 藍色——已移動元件

請注意，「已變更」和「已移動」的顏色是相同的。

**HTML變更**

* 深綠色——已新增HTML
* 紅色——已移除HTML

>[!NOTE]
>
>在比較語言版本時，反白顯示會停用，因為在翻譯中，所有變更和反白顯示都無益。

### 全螢幕與退出 {#fullscreen-and-exiting}

為了專注於特定內容，您可以按一下並排比較的任一「側」全螢幕圖示，將其放大至全瀏覽器視窗。

![](do-not-localize/chlimage_1-18.png)

選取的一側會填滿整個視窗，但是橫條會保留在頂端，讓您在兩頁之間切換。

![chlimage_1-110](assets/chlimage_1-110.png)

您也可以按一下退出全螢幕圖示，以關閉全螢幕檢視。

![](do-not-localize/chlimage_1-19.png)

您可以隨時按一下標題中的「關閉」按鈕退出並排比較。

## 限制 {#limitations}

在某些情況下，頁面差異可能無法如預期般偵測到差異。

* 當差異版本和啟動時，差異不會考慮動態元件，例如網站導覽路徑、功能表、產品清單或標誌（依賴網站結構來呈現其內容的元件）。
* 對於版本，差異不會重新建立訪問控制策略和即時拷貝關係。
* 如果對影像進行任何變更，例如修改alt、title或src屬性，則會以藍色反白顯示變更。 但是，在某些情況下，影像具有src屬性的Base64表示，即使兩個影像看起來相同，它們也會因為src屬性的不同而被差異標籤為不同。
* 比較無法檢測到影像旋轉。
* 如果移動了頁面，則無法再對移動前進行的任何版本執行比較。

   * 如果您遇到比較問題，請查看頁 [面的時間軸](/help/sites-authoring/basic-handling.md#timeline) ，以查看頁面是否已移動。

>[!NOTE]
>
>版本之間無法比較。 只有目前版本可與頁面的其他版本比較。 目前的版本一律是會以變更反白顯示的版本。

>[!NOTE]
>
>如需頁面差異機制運作的詳細資訊以及可能影響頁面差異的限制，請參閱此功能的開 [發人員檔案](/help/sites-developing/pagediff.md) 。
