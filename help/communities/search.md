---
title: 搜尋功能
seo-title: 搜尋功能
description: 向社群站點添加和配置搜索
seo-description: 向社群站點添加和配置搜索
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
translation-type: tm+mt
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 2%

---


# 搜尋功能{#search-feature}

搜尋功能可與各種其他功能搭配使用，例如論壇，以提供搜尋內容的功能。

新增搜尋社群成員輸入之貼文(稱為使用者產生的內容(UGC))的能力時，有兩個元件：[搜尋](#search)和[搜尋結果](#search-results)。

包含`Search Results`元件的頁面同時支援搜尋和結果顯示。

包含`Search`元件的頁面提供啟動搜尋的位置，搜尋結果會顯示在`Search Results`頁面上。

搜尋功能可與任何其他允許網站訪客和成員檢視內容的功能一起使用。

## 搜尋 {#search-features}

### 將搜尋新增至頁面{#add-search-to-a-page}

若要在作者模式下將`Search`元件新增至頁面，請使用元件瀏覽器來找出`Communities / Search`並將它拖曳至頁面上。 使用`Search`時，`Search Results.`需要第二頁

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

當需要的用戶端程式庫`cq.social.hbs.search`包含時，`Search`元件會以此顯示。

![新增搜尋](assets/add-search.png)

### 配置添加的搜索{#configure-the-added-search}

選擇要訪問的已放置的`Search`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![configur](assets/configure-new.png)

在&#x200B;**[!UICONTROL 搜尋設定]**&#x200B;標籤下，指定訪客輸入查詢時搜尋路徑的方式。

![搜尋設定](assets/search-settings.png)

* **[!UICONTROL 搜尋]**
路徑使用「新增項目」按鈕新增搜尋路徑，內容搜尋就受到限制。例如，若要將搜尋限制在特定論壇，請選取位於頁面內的論壇元件：

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 結果]**
頁面結果將顯示在使用瀏覽器選取包含 
`Search Results` 元件.

## 搜尋結果 {#search-results}

### 將搜尋結果新增至頁面{#add-search-results-to-a-page}

若要在作者模式下將`Search Results`元件新增至頁面，請使用元件瀏覽器來尋找

* `Communities / Search Results`

並將它拖曳至頁面上的位置。 與「搜尋」元件不同，不需要第二頁，因為結果會顯示在同一頁。

如果在網站的其他位置使用「搜尋」，則此`Search Results`頁面可設定為`Result Page`的任何或所有例項。`Search`

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

當包含所需的客戶端庫`cq.social.hbs.search`時，`Search Result`元件的顯示方式如下：

![搜索結果](assets/search-result1.png)

### 配置添加的搜索結果{#configure-the-added-search-result}

選擇要訪問的已放置的`Search Results`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![配置](assets/configure-new.png)

在&#x200B;**[!UICONTROL 搜尋結果設定]**&#x200B;標籤下，可指定訪客輸入查詢時，搜尋中包含哪些路徑。

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL 每頁搜尋結果數]**

   定義每頁顯示的主題／貼文數。 預設值為10。

* **[!UICONTROL 搜尋路徑]**

   使用「新增項目」按鈕新增搜尋路徑，內容搜尋就會受到限制。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[ Search Essentials](search-implementation.md)頁面。
