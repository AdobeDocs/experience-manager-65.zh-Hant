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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 搜尋功能 {#search-feature}

搜尋功能可與各種其他功能搭配使用，例如論壇，以提供搜尋內容的功能。

新增搜尋社群成員輸入之貼文(稱為使用者產生的內容(UGC))的能力時，有兩個元件： [`Search`](#search) 和 [`Search Results`](#search-results)。

包含該元件的頁 `Search Results` 面支援搜索和結果顯示。

包含元件的頁面 `Search`提供啟動搜尋的位置，搜尋結果會顯示在頁 `Search Results` 面上。

搜尋功能可與任何其他允許網站訪客和成員檢視內容的功能一起使用。

## 搜尋 {#search-features}

### 新增搜尋至頁面 {#add-search-to-a-page}

若要在作 `Search` 者模式下將元件新增至頁面，請使用元件瀏覽器來 `Communities / Search` 尋找並拖曳元件至頁面上。 使用 `Search` 需要第二頁 `Search Results.`

如需必要資訊，請造 [訪Communities Components Basics](basics.md)。

當需要的用戶端程式庫( `cq.social.hbs.search`)包含時，這就是元件的 `Search` 顯示方式。

![chlimage_1-373](assets/chlimage_1-373.png)

### 設定新增的搜尋 {#configure-the-added-search}

選擇要訪問 `Search` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-374](assets/chlimage_1-374.png)

在「搜 **[!UICONTROL 尋設定]** 」標籤下，指定訪客輸入查詢時要搜尋的路徑。

![chlimage_1-375](assets/chlimage_1-375.png)

* **[!UICONTROL 搜尋路徑]**&#x200B;使用「新增項目」按鈕新增搜尋路徑，內容搜尋就受到限制。 例如，若要將搜尋限制在特定論壇，請選取位於頁面內的論壇元件：

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 結果頁]**：結果將顯示在使用瀏覽器選擇包含元件的頁所指定的單獨頁 `Search Results` 上。

## 搜尋結果 {#search-results}

### 新增搜尋結果至頁面 {#add-search-results-to-a-page}

若要在作 `Search Results` 者模式中將元件新增至頁面，請使用元件瀏覽器來尋找

* `Communities / Search Results`

並將它拖曳至頁面上的位置。 與「搜尋」元件不同，不需要第二頁，因為結果會顯示在同一頁。

如果在網站的其他位置使用「搜尋」，則此頁 `Search Results` 面可設定為任何或 `Result Page` 所有例項的頁面 `Search`。

如需必要資訊，請造 [訪Communities Components Basics](basics.md)。

當需要的用戶端程式庫( `cq.social.hbs.search`)包含時，元件的顯示 `Search Result` 方式如下：

![chlimage_1-376](assets/chlimage_1-376.png)

### 設定新增的搜尋結果 {#configure-the-added-search-result}

選擇要訪問 `Search Results` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-377](assets/chlimage_1-377.png)

在「搜 **[!UICONTROL 尋結果設定]** 」標籤下，可指定訪客輸入查詢時，搜尋中包含哪些路徑。

![chlimage_1-378](assets/chlimage_1-378.png)

* **[!UICONTROL 每頁搜尋結]**&#x200B;果定義每頁顯示的主題／貼文數。 預設值為10。

* **[!UICONTROL 搜尋路徑]**&#x200B;使用「新增項目」按鈕新增搜尋路徑，內容搜尋就受到限制。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人 [員的Search Essentials](search-implementation.md) （搜尋基本工具）頁面。
