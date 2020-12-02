---
title: 使用Social Tag Cloud
seo-title: 使用Social Tag Cloud
description: 新增Social Tag Cloud元件至頁面
seo-description: 新增Social Tag Cloud元件至頁面
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 4%

---


# 使用社交標籤雲端{#using-social-tag-cloud}

## 簡介 {#introduction}

`Social Tag Cloud`元件會在張貼內容時反白顯示社群成員套用的標籤。 它可識別趨勢主題，並讓網站訪客快速找到標籤內容。

若需另一種識別目前趨勢的方法，請造訪[活動趨勢](trends.md)。

本頁記錄`Social Tag Cloud`元件對話框設定並說明用戶體驗。

如需開發人員的詳細資訊，請參閱[Tag Essentials](tag.md)。

如需建立和管理標籤以及已套用內容標籤的相關資訊，請參閱[管理標籤](../../help/sites-administering/tags.md)。

## 新增社交標籤雲端{#adding-a-social-tag-cloud}

若要在作者模式下將`Social Tag Cloud`元件新增至頁面，請使用元件瀏覽器來找出`Communities / Social Tag Cloud`，並將它拖曳至應出現標籤雲的頁面上。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

當包含[必要的用戶端程式庫](tag.md#essentials-for-client-side)時，`Social Tag Cloud`元件的顯示方式如下：

![social-tag](assets/social-tag.png)

## 設定社交標籤雲端{#configuring-social-tag-cloud}

選擇要訪問的已放置的`Social Tag Cloud`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![配置](assets/configure-new.png)

在&#x200B;**[!UICONTROL Social Tag Cloud]**&#x200B;標籤下，指定要顯示的標籤，以及如果標籤是作用中連結，則指定搜尋結果頁面的位置：

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 顯示的社交標]**
記識別要顯示的UGC標籤。下拉式選項包括：

   * `From page and child pages`
   * `All tags`

   預設值為`From page and child pages`，其中&quot;page&quot;是指下方的&#x200B;**Page**&#x200B;設定。

* **[!UICONTROL 頁面]**

   (如果`All tags)`不是頁面的UGC路徑，則為必填項目。 如果保留空白，預設為目前頁面。

* **[!UICONTROL 標記上無連結]**

   如果勾選，標籤會以純文字顯示在標籤雲端。 如果取消勾選，標籤會顯示為活動連結，可搜尋套用該標籤的所有內容。 預設為未勾選，且需要設定&#x200B;**[!UICONTROL 搜尋結果路徑]**。

* **[!UICONTROL 搜尋結果路徑]**

   放置`Search Result`元件的頁面的路徑，配置為引用UGC，該UGC包括由&#x200B;**Page**&#x200B;設定指定的UGC路徑。

## 變更社交標籤雲端的顯示{#change-display-of-social-tag-cloud}

若要編輯&#x200B;**Social Tag Cloud**&#x200B;的顯示，請輸入[設計模式](../../help/sites-authoring/default-components-designmode.md)並連按兩下置入的`Social Tag Cloud`元件，以開啟具有其他標籤的對話方塊。

使用&#x200B;**[!UICONTROL Social Tag Cloud(Design)]**&#x200B;標籤，指定標籤的顯示方式。 標籤可以是簡單標籤、預設名稱空間中的單個單詞或分層分類：

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL 顯示完整的標題路徑]**

   如果勾選，則顯示父標籤的標題和每個套用標籤的名稱空間。

   例如：

   * 已核取: `Geometrixx Media: Gadgets / Cars`
   * 未核取: `Cars`

   簡單標籤沒有區別。

   預設為未勾選。

* **[!UICONTROL 僅顯示葉標記]**

   如果勾選，則只會顯示不含其他標籤的已套用標籤。

   例如，假設TagID為：

   `Geometrixx Media: Gadgets / Cars`

   可套用3個標籤：

   `Geometrixx Media (the namespace)`、 `Gadgets`和  `Cars`

   * 已勾選：如果套用，則只會顯示`Cars`。
   * 未勾選：如果應用，將顯示`Geometrixx Media`和`Gadgets`以及`Cars`。

   簡單的標籤是葉標籤。

   預設為未勾選。

* **[!UICONTROL 連結範本]**

   透過元件編輯對話方塊啟用連結時，用來在標籤雲端中顯示連結的範本（預設值除外）。

* **[!UICONTROL 所有標記相同尺寸]**

   如果勾選，標籤雲端中的所有字詞樣式都相同。 如果未勾選，字詞的樣式會根據其使用而不同。 預設為未勾選。

## 其他資訊 {#additional-information}

開發人員可在[Tag Essentials](tag.md)頁面上找到更多資訊。

如需建立和管理標籤的相關資訊，請參閱[標籤使用者產生的內容](tag-ugc.md)(UGC)。
