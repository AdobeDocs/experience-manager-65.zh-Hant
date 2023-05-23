---
title: 搜索功能
seo-title: Search Feature
description: 向社區站點添加和配置搜索
seo-description: Adding and configuring Search to a Communities site
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 2%

---

# 搜索功能 {#search-feature}

該搜索功能可與各種其它功能（如論壇）配合使用，以提供搜索內容的能力。

添加搜索社區成員輸入的帖子(稱為用戶生成內容(UGC))的功能時，有兩個元件： [搜索](#search) 和 [搜索結果](#search-results)。

包含 `Search Results` 元件支援搜索和結果顯示。

包含 `Search` 元件提供了啟動搜索的位置，結果將出現在 `Search Results` 的子菜單。

該搜索特徵可以與允許站點訪問者和成員查看內容的任何其他特徵一起使用。

## 搜尋 {#search-features}

### 將搜索添加到頁面 {#add-search-to-a-page}

添加 `Search` 在作者模式下對頁面的元件，使用元件瀏覽器查找 `Communities / Search` 然後拖到頁面上。 使用 `Search` 需要第二頁 `Search Results.`

如需必要資訊，請訪問 [社區元件基礎](basics.md)。

當所需的客戶端庫時， `cq.social.hbs.search`，包括，這是 `Search` 元件。

![添加搜索](assets/add-search.png)

### 配置添加的搜索 {#configure-the-added-search}

選取已放置的 `Search` 要訪問和選擇的元件 `Configure` 表徵圖。

![供給](assets/configure-new.png)

在 **[!UICONTROL 搜索設定]** 頁籤，指定訪問者輸入查詢時搜索的路徑。

![搜索設定](assets/search-settings.png)

* **[!UICONTROL 搜索路徑]**
通過使用「添加項」按鈕添加搜索路徑，內容搜索受到限制。 例如，要將搜索限制到特定論壇，請選擇位於頁面中的論壇元件：

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 結果頁]**
結果將顯示在使用瀏覽器選擇包含 
`Search Results` 元件.

## 搜尋結果 {#search-results}

### 將搜索結果添加到頁面 {#add-search-results-to-a-page}

添加 `Search Results` 在作者模式下對頁面的元件，使用元件瀏覽器查找

* `Communities / Search Results`

然後拖到頁面上。 與搜索元件不同，不需要第二頁，因為結果將顯示在同一頁上。

如果在網站的其他位置使用「搜索」，則此頁面 `Search Results` 可以配置為 `Result Page` 對於任何或所有實例 `Search`。

如需必要資訊，請訪問 [社區元件基礎](basics.md)。

當所需的客戶端庫時， `cq.social.hbs.search`，包括，這是 `Search Result` 元件將出現：

![搜索結果](assets/search-result1.png)

### 配置添加的搜索結果 {#configure-the-added-search-result}

選取已放置的 `Search Results` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置](assets/configure-new.png)

在 **[!UICONTROL 搜索結果設定]** 頁籤中，可以指定訪問者輸入查詢時搜索中包含的路徑。

![搜索結果設定](assets/search-result-settings.png)

* **[!UICONTROL 每頁搜尋結果數]**

   定義每頁顯示的主題/帖子數。 預設值為10。

* **[!UICONTROL 搜索路徑]**

   通過使用「添加項」按鈕添加搜索路徑，內容搜索受到限制。

## 其他資訊 {#additional-information}

有關 [搜索要件](search-implementation.md) 頁面。
