---
title: 與BrightEdge Content Optimizer整合
description: 瞭解如何整合AEM與BrightEdge Content Optimizer。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f14cc5fd-aeab-4619-b926-b6f1df7e50e5
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 2%

---

# 與BrightEdge Content Optimizer整合{#integrating-with-brightedge-content-optimizer}

建立BrightEdge雲端設定，讓AEM可以使用您BrightEdge帳戶的憑證連線。 如果您使用多個帳戶，則可建立多個設定。

建立設定時，請指定標題。 標題應為描述性，以便人們能夠將設定與BrightEdge帳戶建立關聯。 當頁面作者或管理員將網頁與BrightEdge帳戶建立關聯時，此標題會顯示在下拉式清單中。

1. 在邊欄上，按一下「工具>作業>雲端>Cloud Service」 。
1. 按一下BrightEdge Content Optimizer區段中顯示的連結。 是否已建立BrightEdge設定會決定連結文字：

   * 立即設定：尚未建立設定時，此連結就會顯示。
   * 顯示組態：建立一或多個組態後，就會出現此連結。

   ![chlimage_1-4](assets/chlimage_1-4a.png)

1. 如果您按一下「顯示組態」 ，請按一下「可用組態」旁邊的+連結。
1. 輸入設定的標題。 選擇性地輸入節點名稱，該節點用來將設定儲存在存放庫中。 按一下「建立」。
1. 在「BrightEdge Content Optimizer設定」對話方塊中，輸入BrightEdge帳戶的使用者名稱和密碼，然後按一下「確定」。

## 編輯BrightEdge設定 {#editing-a-brightedge-configuration}

必要時修改BrightEdge組態的使用者名稱和密碼。 修改會影響使用設定的所有頁面。

1. 在邊欄上，按一下「工具>作業>雲端>Cloud Service」 。
1. 在BrightEdge Content Optimizer區段中，按一下「顯示組態」 。

   ![chlimage_1-5](assets/chlimage_1-5a.png)

1. 按一下要編輯的組態名稱。
1. 按一下「編輯」，修改屬性值，然後按一下「確定」。

## 將頁面與BrightEdge組態建立關聯 {#associating-pages-with-a-brightedge-configuration}

將頁面與BrightEdge設定建立關聯，以將頁面資料傳送至BrightEdge服務進行分析。 將頁面與組態建立關聯時，子頁面會繼承關聯。 通常您會將網站的首頁建立關聯，以便將所有頁面的資料傳送到BrightEdge。

1. 開啟「傳統網站」主控台。 ([http://localhost:4502/siteadmin#/content](http://localhost:4502/siteadmin#/content))
1. 在「網站」樹狀結構中，選取包含您要與BrightEdge設定產生關聯之頁面的資料夾或頁面。
1. 在頁面清單中，以滑鼠右鍵按一下要設定的頁面，然後按一下「內容」。
1. 在「Cloud Service」標籤上，按一下「新增服務」按鈕，然後在「Cloud Service」對話方塊中選取「BrightEdge Content Optimizer」，然後按一下「確定」。
1. 在BrightEdge Content Optimizer清單中，選取要與頁面建立關聯的BrightEdge設定，然後按一下「確定」。

   ![chlimage_1-6](assets/chlimage_1-6a.png)

## 啟用BrightEdge設定 {#activating-a-brightedge-configuration}

啟動BrightEdge設定以在發佈執行個體上復寫它，並啟用已發佈頁面與BrightEdge服務互動。

1. 在邊欄上，按一下「網站」，然後瀏覽並選取您與BrightEdge設定相關聯的頁面。
1. 按一下「發佈」圖示，然後按一下「發佈」。

   ![chlimage_1-7](assets/chlimage_1-7a.png)

1. 在出現的設定清單中，確定已選取您的BrightEdge設定，然後按一下「發佈」。

   ![chlimage_1-8](assets/chlimage_1-8a.png)
