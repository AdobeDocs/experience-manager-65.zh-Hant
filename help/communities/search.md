---
title: 搜尋功能
seo-title: 搜尋功能
description: 向Communities站點添加和配置搜索
seo-description: 向Communities站點添加和配置搜索
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 2%

---

# 搜索功能{#search-feature}

搜尋功能可與論壇等各種其他功能搭配使用，以提供搜尋內容的功能。

新增搜尋社群成員所輸入貼文的能力時(也稱為使用者產生的內容(UGC))，有兩個元件：[搜尋](#search)和[搜尋結果](#search-results)。

包含`Search Results`元件的頁面支援搜索和顯示結果。

包含`Search`元件的頁面提供啟動搜尋的位置，結果會顯示在`Search Results`頁面上。

搜尋功能可與任何其他允許網站訪客和成員檢視內容的功能搭配使用。

## 搜尋 {#search-features}

### 將搜索添加到頁{#add-search-to-a-page}

若要以製作模式將`Search`元件新增至頁面，請使用元件瀏覽器來找出`Communities / Search`，並將其拖曳至頁面上的位置。 使用`Search`需要`Search Results.`的第二頁

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

包含所需的用戶端程式庫`cq.social.hbs.search`時，會以此顯示`Search`元件。

![新增搜尋](assets/add-search.png)

### 配置添加的搜索{#configure-the-added-search}

選取要存取的放置`Search`元件，並選取開啟編輯對話方塊的`Configure`圖示。

![配置](assets/configure-new.png)

在&#x200B;**[!UICONTROL 搜尋設定]**&#x200B;標籤下，指定當訪客輸入查詢時，要如何搜尋路徑。

![搜尋設定](assets/search-settings.png)

* **[!UICONTROL 搜]**
尋路徑使用「新增項目」按鈕新增搜尋路徑，限制了內容搜尋。例如，若要將搜尋限制在特定論壇，請選取放在頁面中的論壇元件：

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 結]**
果頁面結果將顯示在使用瀏覽器指定的單獨頁面上，以選擇包含 
`Search Results` 元件.

## 搜尋結果 {#search-results}

### 將搜尋結果新增至頁面{#add-search-results-to-a-page}

若要在製作模式中將`Search Results`元件新增至頁面，請使用元件瀏覽器來找出

* `Communities / Search Results`

並將其拖曳到頁面上。 與搜尋元件不同，不需要第二個頁面，因為結果會顯示在相同的頁面上。

如果在網站的其他地方使用「搜尋」，則此包含`Search Results`的頁面可設定為`Result Page`，適用於`Search`的任何或所有例項。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

包含所需的用戶端程式庫`cq.social.hbs.search`時，以下是`Search Result`元件的顯示方式：

![search-result](assets/search-result1.png)

### 配置添加的搜索結果{#configure-the-added-search-result}

選取要存取的放置`Search Results`元件，並選取開啟編輯對話方塊的`Configure`圖示。

![設定](assets/configure-new.png)

在&#x200B;**[!UICONTROL 搜尋結果設定]**&#x200B;標籤下，可指定當訪客輸入查詢時，搜尋中包含的路徑。

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL 每頁搜尋結果數]**

   定義每頁顯示的主題/貼文數。 預設為10。

* **[!UICONTROL 搜尋路徑]**

   使用「新增項目」按鈕新增搜尋路徑，將限制內容搜尋。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[搜尋要點](search-implementation.md)頁面。
