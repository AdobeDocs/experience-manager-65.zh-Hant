---
title: 使用Social Tag Cloud
seo-title: 使用Social Tag Cloud
description: 新增Social Tag cloud元件至頁面
seo-description: 新增Social Tag cloud元件至頁面
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用Social Tag Cloud {#using-social-tag-cloud}

## 簡介 {#introduction}

此元 `Social Tag Cloud` 件會在張貼內容時反白標示社群成員套用的標籤。 它可識別趨勢主題，並讓網站訪客快速找到標籤內容。

若需另一種識別目前趨勢的方法，請造訪活 [動趨勢](trends.md)。

本頁記錄了組 `Social Tag Cloud` 件對話框設定並描述了用戶體驗。

如需開發人員的詳細資訊，請參 [閱Tag Essentials](tag.md)。

如需 [有關建立和管理標籤](../../help/sites-administering/tags.md) ，以及已套用內容標籤的資訊，請參閱管理標籤。

## 新增社交標籤雲端 {#adding-a-social-tag-cloud}

若要在作 `Social Tag Cloud` 者模式下將元件新增至頁面，請使用元件瀏覽器來 `Communities / Social Tag Cloud` 尋找並拖曳元件至應出現標籤雲端的頁面上。

如需必要資訊，請造 [訪Communities Components Basics](basics.md)。

當包含 [所需的用戶端程式庫](tag.md#essentials-for-client-side) ，元件的顯示方式 `Social Tag Cloud` 如下：

![chlimage_1-303](assets/chlimage_1-303.png)

## 設定Social標籤雲端 {#configuring-social-tag-cloud}

選擇要訪問 `Social Tag Cloud` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-304](assets/chlimage_1-304.png)

在「 **[!UICONTROL Social標籤雲端]** 」標籤下，指定要顯示的標籤，以及（如果標籤是作用中連結）搜尋結果頁面的位置：

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL 顯示的社交標籤]**&#x200B;識別要顯示的UGC標籤。 下拉式選項包括

   * `From page and child pages`
   * `All tags`
   預設值 `From page and child pages`為，其中「頁面」是指下 **方的** 「頁面」設定。

* **[!UICONTROL 頁面]**(若非頁面 `All tags)` 的UGC路徑，則為必要項目)。 如果保留空白，預設為目前頁面。

* **[!UICONTROL 標籤上沒有連結]**&#x200B;如果勾選，標籤會以純文字顯示在標籤雲端。 如果取消勾選，標籤會顯示為活動連結，可搜尋套用該標籤的所有內容。 預設為未勾選，且 **[!UICONTROL 需要設定搜尋結果路徑]** 。

* **[!UICONTROL 搜尋結果路]**&#x200B;徑：放置元件之頁面的路徑， `Search Result` 設定為參照UGC，其中包含 **** Page設定所指定的UGC路徑。

## 變更Social Tag cloud的顯示 {#change-display-of-social-tag-cloud}

若要編輯 **Social Tag Cloud**，請進入「 [Design Mode](../../help/sites-authoring/default-components-designmode.md) 」（設計模式）並連按兩下置入的元件，以開啟具有其他標籤 `Social Tag Cloud` 的對話方塊。

使用「 **[!UICONTROL Social Tag Cloud(Design)」標籤]** ，指定標籤的顯示方式。 標籤可以是簡單標籤、預設名稱空間中的單個單詞或分層分類：

![chlimage_1-306](assets/chlimage_1-306.png)

* **[!UICONTROL 顯示完整標題路徑]**&#x200B;如果勾選，則顯示父標籤的標題和每個套用標籤的名稱空間。

   例如：

   * 已核取: `Geometrixx Media: Gadgets / Cars`
   * 未核取: `Cars`
   簡單標籤沒有區別。

   預設為未勾選。

* **[!UICONTROL 僅顯示葉標籤]**&#x200B;如果勾選，則僅顯示不含其他標籤的已套用標籤。

   例如，若TagID為

   `Geometrixx Media: Gadgets / Cars`

   可套用3個標籤： `Geometrixx Media (the namespace)`、 `Gadgets`和 `Cars`

   * 已勾選：只 `Cars` 會顯示，如果套用
   * 未勾選：並 `Geometrixx Media` 且 `Gadgets``Cars` 會顯示（如果套用）
   簡單的標籤是葉標籤。

   預設為未勾選。

* **[!UICONTROL 連結範本]**：當透過元件編輯對話方塊啟用連結時，用來在標籤雲端中顯示連結的範本（預設值除外）。

* **[!UICONTROL 所有標籤的大小相]**&#x200B;同如果勾選，則標籤雲中的所有字詞樣式都相同。 如果未勾選，字詞的樣式會根據其使用而不同。 預設為未勾選。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員 [的Tag Essentials](tag.md) （標籤基本工具）頁面。

如需 [建立和管理標籤的相關資訊，請參閱標籤使用者產生的內容](tag-ugc.md) (UGC)。
