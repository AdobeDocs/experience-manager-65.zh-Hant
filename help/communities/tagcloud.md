---
title: 使用社交標籤雲
description: 瞭解如何將Social Tag Cloud元件新增至頁面，讓登入的社群成員快速識別趨勢主題並找到標籤的內容。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 4%

---

# 使用社交標籤雲 {#using-social-tag-cloud}

## 簡介 {#introduction}

此 `Social Tag Cloud` 元件會醒目顯示社群成員在發佈內容時套用的標籤。 這是識別趨勢主題並允許網站訪客快速找到標籤內容的方法。

如需其他識別目前趨勢的方法，請造訪 [活動趨勢](trends.md).

本頁會記錄 `Social Tag Cloud` 元件對話方塊設定及說明使用者體驗。

如需開發人員的詳細資訊，請參閱 [標籤Essentials](tag.md).

另請參閱 [管理標籤](../../help/sites-administering/tags.md) 以取得關於建立和管理標籤，以及已對哪些內容標籤套用的資訊。

## 新增社交標籤雲端 {#adding-a-social-tag-cloud}

若要新增 `Social Tag Cloud` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找 `Communities / Social Tag Cloud` 並將其拖曳至應顯示標籤雲的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](tag.md#essentials-for-client-side) 包含，這就是 `Social Tag Cloud` 元件出現：

![社交標籤](assets/social-tag.png)

## 設定社交標籤雲 {#configuring-social-tag-cloud}

選取已放置的 `Social Tag Cloud` 元件供您存取及選取 `Configure` 圖示可開啟編輯對話方塊。

![設定](assets/configure-new.png)

在 **[!UICONTROL 社交標籤雲]** 標籤，指定要顯示的標籤，如果標籤是作用中的連結，則指定搜尋結果的頁面位置：

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 要顯示的社交標籤]**
識別要顯示的UGC標籤。 下拉式選項包括：

   * `From page and child pages`
   * `All tags`

  預設值為 `From page and child pages`，其中「page」是指 **頁面** 設定於下方。

* **[!UICONTROL Page]**

  （若非必要，則為必要） `All tags)` 頁面的UGC路徑。 如果留白，預設為目前頁面。

* **[!UICONTROL 標記上無連結]**

  如果勾選，標籤會在標籤雲中顯示為純文字。 如果取消勾選，標籤會顯示為作用中的連結，搜尋套用該標籤的所有內容。 預設為未勾選，且需要 **[!UICONTROL 搜尋結果路徑]** 即將設定。

* **[!UICONTROL 搜尋結果路徑]**

  頁面的路徑，該頁面上 `Search Result` 元件已放置，設定為參考UGC，其中包含指定的UGC路徑 **頁面** 設定。

## 變更社交標籤雲的顯示 {#change-display-of-social-tag-cloud}

若要編輯的顯示 **社交標籤雲**，輸入 [設計模式](../../help/sites-authoring/default-components-designmode.md) 並連按兩下置入的 `Social Tag Cloud` 元件以開啟具有額外索引標籤的對話方塊。

使用 **[!UICONTROL 社交標籤雲（設計）]** 標籤，指定標籤的顯示方式。 標籤可能是簡單標籤、預設名稱空間中的單一字詞或階層式分類法：

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL 顯示完整的標題路徑]**

  如果勾選，會顯示上層標籤的標題和每個套用標籤的名稱空間。

  例如：

   * 已核取: `Geometrixx Media: Gadgets / Cars`
   * 未核取: `Cars`

  簡單標籤沒有差異。

  預設為未勾選。

* **[!UICONTROL 僅顯示葉標記]**

  如果勾選，僅顯示不包含其他標籤的已套用標籤。

  例如，假定TagID為：

  `Geometrixx Media: Gadgets / Cars`

  有三個可套用的標籤：

  `Geometrixx Media (the namespace)`, `Gadgets`, 和 `Cars`

   * 已核取：僅限 `Cars` 都會顯示（如果套用）。
   * 未勾選： `Geometrixx Media`， `Gadgets`、和 `Cars` 都會顯示（如果套用）。

  簡單標籤是葉標籤。

  預設為未勾選。

* **[!UICONTROL 連結範本]**

  預設以外的範本，用於在透過元件編輯對話方塊啟用連結時，顯示標籤雲中的連結。

* **[!UICONTROL 所有標記相同尺寸]**

  如果勾選，則標籤雲中的所有字詞的樣式都相同。 如果未勾選，則字詞的樣式會根據其使用情況而有所不同。 預設為未勾選。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [標籤Essentials](tag.md) 開發人員頁面。

另請參閱 [標籤使用者產生的內容](tag-ugc.md) (UGC)，以取得建立和管理標籤的相關資訊。
