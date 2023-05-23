---
title: 使用社交標籤雲
seo-title: Using Social Tag Cloud
description: 將社交標籤雲元件添加到頁面
seo-description: Adding a Social Tag Cloud component to a page
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 5%

---

# 使用社交標籤雲 {#using-social-tag-cloud}

## 簡介 {#introduction}

的 `Social Tag Cloud` 元件突出顯示發佈內容時由社區成員應用的標籤。 它是一種識別趨勢主題並允許站點訪問者快速查找標籤內容的方法。

要確定當前趨勢的另一種方法，請訪問 [活動趨勢](trends.md)。

此頁面記錄 `Social Tag Cloud` 元件對話框設定並描述用戶體驗。

有關開發人員的詳細資訊，請參閱 [標籤軟體包](tag.md)。

請參閱 [管理標籤](../../help/sites-administering/tags.md) 有關建立和管理標籤的資訊，以及已應用了哪些內容標籤。

## 添加社交標籤雲 {#adding-a-social-tag-cloud}

添加 `Social Tag Cloud` 在作者模式下對頁面的元件，使用元件瀏覽器查找 `Communities / Social Tag Cloud` 並將其拖到應顯示標籤雲的頁面上。

如需必要資訊，請訪問 [社區元件基礎](basics.md)。

當 [所需的客戶端庫](tag.md#essentials-for-client-side) 包括，這是 `Social Tag Cloud` 元件將出現：

![社交標籤](assets/social-tag.png)

## 配置社交標籤雲 {#configuring-social-tag-cloud}

選取已放置的 `Social Tag Cloud` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置](assets/configure-new.png)

在 **[!UICONTROL 社交標籤雲]** 頁籤，指定要顯示的標籤，如果標籤是活動連結，則指定搜索結果頁面的位置：

![社會標籤雲](assets/social-tag-cloud.png)

* **[!UICONTROL 要顯示的社交標籤]**
確定要顯示的UGC標籤。 下拉選項包括：

   * `From page and child pages`
   * `All tags`

   預設值為 `From page and child pages`，其中「page」是指 **頁面** 的下界。

* **[!UICONTROL Page]**

   (如果不需要，則為必需 `All tags)` 頁面的UGC路徑。 如果留空，則預設為當前頁。

* **[!UICONTROL 標記上無連結]**

   如果選中，則標籤將以純文字檔案形式顯示在標籤雲中。 如果未選中，則標籤將顯示為活動連結，這些連結將搜索應用該標籤的所有內容。 預設值未選中，並要求 **[!UICONTROL 搜索結果路徑]** 來設定。

* **[!UICONTROL 搜索結果路徑]**

   頁面的路徑 `Search Result` 元件已放置，配置為引用UGC，該UGC包括由 **頁面** 的子菜單。

## 更改社交標籤雲的顯示 {#change-display-of-social-tag-cloud}

編輯 **社交標籤雲**&#x200B;輸入 [設計模式](../../help/sites-authoring/default-components-designmode.md) 並按兩下放置的 `Social Tag Cloud` 的子菜單。

使用 **[!UICONTROL 社交標籤雲（設計）]** 頁籤，指定標籤的顯示方式。 標籤可以是簡單標籤、預設命名空間中的單個單詞或分層分類：

![社會標籤雲設計](assets/social-tag-cloud-design.png)

* **[!UICONTROL 顯示完整的標題路徑]**

   如果選中，則顯示每個應用標籤的父標籤和命名空間的標題。

   例如：

   * 已核取: `Geometrixx Media: Gadgets / Cars`
   * 未核取: `Cars`

   簡單的標籤沒有區別。

   未選中預設值。

* **[!UICONTROL 僅顯示葉標記]**

   如果選中，則僅顯示不包含其他標籤的已應用標籤。

   例如，給定的TagID為：

   `Geometrixx Media: Gadgets / Cars`

   可以應用3個標籤：

   `Geometrixx Media (the namespace)`, `Gadgets`, 和 `Cars`

   * 已選中：僅 `Cars` 將顯示。
   * 未選中： `Geometrixx Media` 和 `Gadgets`以及 `Cars` 將顯示。

   簡單的標籤是葉標籤。

   未選中預設值。

* **[!UICONTROL 連結範本]**

   當通過元件編輯對話框啟用連結時，用於在標籤雲中顯示連結的模板（預設模板除外）。

* **[!UICONTROL 所有標記相同尺寸]**

   如果選中，則標籤雲中的所有字樣都相同。 如果未選中，則根據詞的用法將不同樣式。 未選中預設值。

## 其他資訊 {#additional-information}

有關 [標籤軟體包](tag.md) 頁面。

請參閱 [標籤用戶生成的內容](tag-ugc.md) (UGC)，以獲取有關建立和管理標籤的資訊。
