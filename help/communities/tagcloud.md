---
title: 使用Social Tag Cloud
seo-title: 使用Social Tag Cloud
description: 將Social Tag Cloud元件新增至頁面
seo-description: 將Social Tag Cloud元件新增至頁面
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 4%

---

# 使用社交標籤雲{#using-social-tag-cloud}

## 簡介 {#introduction}

`Social Tag Cloud`元件會在發佈內容時醒目提示社群成員套用的標籤。 這是一種識別趨勢主題，並允許網站訪客快速找到已標籤內容的方法。

如需識別目前趨勢的其他方法，請造訪[活動趨勢](trends.md)。

此頁面記錄`Social Tag Cloud`元件對話方塊設定，並說明使用者體驗。

如需開發人員的詳細資訊，請參閱[Tag Essentials](tag.md)。

請參閱[管理標籤](../../help/sites-administering/tags.md) ，了解如何建立和管理標籤以及套用了哪些內容標籤的資訊。

## 新增社交標籤雲{#adding-a-social-tag-cloud}

若要在製作模式中將`Social Tag Cloud`元件新增至頁面，請使用元件瀏覽器來找出`Communities / Social Tag Cloud`，並將其拖曳至應該出現標籤雲端的頁面上。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

包含[必要的用戶端程式庫](tag.md#essentials-for-client-side)時，以下是`Social Tag Cloud`元件的顯示方式：

![社交標籤](assets/social-tag.png)

## 設定社交標籤雲{#configuring-social-tag-cloud}

選取要存取的放置`Social Tag Cloud`元件，並選取開啟編輯對話方塊的`Configure`圖示。

![設定](assets/configure-new.png)

在&#x200B;**[!UICONTROL Social Tag Cloud]**&#x200B;標籤下，指定要顯示的標籤，以及如果標籤為作用中連結，則指定搜尋結果頁面的位置：

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 要顯示的社]**
交標籤識別要顯示的UGC標籤。下拉式選項為：

   * `From page and child pages`
   * `All tags`

   預設值為`From page and child pages`，其中&quot;page&quot;表示下方的&#x200B;**Page**&#x200B;設定。

* **[!UICONTROL 頁面]**

   （若非`All tags)`，則為必要）頁面的UGC路徑。 若保留為空白，則預設為目前頁面。

* **[!UICONTROL 標記上無連結]**

   若勾選此選項，標籤會以純文字顯示於標籤雲中。 如果取消勾選，標籤會顯示為作用中連結，可搜尋套用該標籤的所有內容。 預設值為未勾選，需要設定&#x200B;**[!UICONTROL 搜尋結果路徑]**。

* **[!UICONTROL 搜索結果路徑]**

   放置`Search Result`元件的頁面的路徑，配置為引用UGC，該UGC包括由&#x200B;**Page**&#x200B;設定指定的UGC路徑。

## 變更社交標籤雲的顯示{#change-display-of-social-tag-cloud}

若要編輯&#x200B;**Social Tag Cloud**&#x200B;的顯示，請輸入[設計模式](../../help/sites-authoring/default-components-designmode.md)並連按兩下已放置的`Social Tag Cloud`元件，以開啟含有其他索引標籤的對話方塊。

使用&#x200B;**[!UICONTROL Social Tag Cloud(Design)]**&#x200B;標籤，指定標籤的顯示方式。 標籤可以是簡單標籤、預設命名空間中的單一字或分層分類法：

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL 顯示完整的標題路徑]**

   若勾選此選項，會顯示父標籤的標題和每個套用標籤的命名空間。

   例如：

   * 已核取: `Geometrixx Media: Gadgets / Cars`
   * 未核取: `Cars`

   簡單標籤沒有差異。

   預設為未勾選。

* **[!UICONTROL 僅顯示葉標記]**

   若勾選此選項，則只會顯示不含其他標籤的已套用標籤。

   例如，假設TagID為：

   `Geometrixx Media: Gadgets / Cars`

   可套用3個標籤：

   `Geometrixx Media (the namespace)`、  `Gadgets`和  `Cars`

   * 已勾選：若套用，則只會顯示`Cars`。
   * 未勾選：若已套用，則會顯示`Geometrixx Media`和`Gadgets`以及`Cars`。

   簡單的標籤是葉標籤。

   預設為未勾選。

* **[!UICONTROL 連結範本]**

   透過元件編輯對話方塊啟用連結時，用來在Tag Cloud中顯示連結的範本（預設值除外）。

* **[!UICONTROL 所有標記相同尺寸]**

   若勾選此選項，標籤雲端中的所有字詞都會設定相同的樣式。 如果未勾選，字詞的樣式會根據其使用方式而有所不同。 預設為未勾選。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[ Tag Essentials](tag.md)頁面。

如需建立和管理標籤的相關資訊，請參閱[標籤使用者產生的內容](tag-ugc.md)(UGC)。
