---
title: 搜尋功能
description: 將搜尋新增及設定至Communities網站
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# 搜尋功能 {#search-feature}

搜尋功能可與各種其他功能（例如論壇）搭配使用，以提供搜尋內容的功能。

新增搜尋由社群成員輸入的帖子(稱為使用者產生的內容(UGC))的功能時，有兩個元件： [搜尋](#search) 和 [搜尋結果](#search-results).

包含下列專案的頁面 `Search Results` 元件支援搜尋和顯示結果。

包含下列專案的頁面 `Search` 元件會提供位置來啟動搜尋，且搜尋結果會顯示在 `Search Results` 頁面。

搜尋功能可與任何其他可讓網站訪客和成員檢視內容的功能搭配使用。

## 搜尋 {#search-features}

### 將搜尋新增至頁面 {#add-search-to-a-page}

若要新增 `Search` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找 `Communities / Search` 並將其拖曳至頁面上的適當位置。 使用 `Search` 需要第二個頁面 `Search Results.`

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當需要使用者端程式庫時， `cq.social.hbs.search`，包含，這就是 `Search` 元件隨即出現。

![add-search](assets/add-search.png)

### 設定新增的搜尋 {#configure-the-added-search}

選取已放置的 `Search` 元件以存取和選取 `Configure` 圖示可開啟編輯對話方塊。

![設定](assets/configure-new.png)

在 **[!UICONTROL 搜尋設定]** 索引標籤，指定當訪客輸入查詢時如何搜尋路徑。

![搜尋設定](assets/search-settings.png)

* **[!UICONTROL 搜尋路徑]**
透過使用新增專案按鈕新增搜尋路徑，內容搜尋受到限制。 例如，若要將搜尋限制在特定論壇，請選取放置在頁面中的論壇元件：

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 結果頁面]**
結果會顯示在指定的個別頁面上，此頁面是使用瀏覽器來選取包含 `Search Results` 元件。

## 搜尋結果 {#search-results}

### 將搜尋結果新增至頁面 {#add-search-results-to-a-page}

若要新增 `Search Results` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Search Results`

並將其拖曳至頁面上的適當位置。 與搜尋元件不同，不需要第二個頁面，因為結果將顯示在同一頁面上。

如果在網站內的其他位置使用「搜尋」，此頁面會顯示 `Search Results` 可設定為 `Result Page` 針對的任何或所有執行個體 `Search`.

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當需要使用者端程式庫時， `cq.social.hbs.search`，包含，這就是 `Search Result` 元件隨即出現：

![search-result](assets/search-result1.png)

### 設定新增的搜尋結果 {#configure-the-added-search-result}

選取已放置的 `Search Results` 元件以存取和選取 `Configure` 圖示可開啟編輯對話方塊。

![設定](assets/configure-new.png)

在 **[!UICONTROL 搜尋結果設定]** 索引標籤中，可指定訪客輸入查詢時，搜尋中包含哪些路徑。

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL 每頁搜尋結果數]**

  定義每個頁面顯示的主題/帖子數。 預設值為10。

* **[!UICONTROL 搜尋路徑]**

  透過使用新增專案按鈕新增搜尋路徑，內容搜尋受到限制。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [搜尋Essentials](search-implementation.md) 開發人員頁面。
