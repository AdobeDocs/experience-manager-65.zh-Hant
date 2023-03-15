---
title: 與BrightEdge Content Optimizer整合
seo-title: Integrating with BrightEdge Content Optimizer
description: 了解如何整合AEM與BrightEdge Content Optimizer。
seo-description: Learn about integrating AEM with BrightEdge Content Optimizer.
uuid: 7075dd3c-2fd6-4050-af1c-9b16ad4366ec
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: cf25c9a8-0555-4c67-8aa5-55984fd8d301
exl-id: f14cc5fd-aeab-4619-b926-b6f1df7e50e5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 1%

---

# 與BrightEdge Content Optimizer整合{#integrating-with-brightedge-content-optimizer}

建立BrightEdge雲端設定，以便AEM可使用BrightEdge帳戶的認證進行連線。 如果您使用多個帳戶，則可建立多個設定。

建立設定時，需指定標題。 標題應具有描述性，以便讓使用者將設定與BrightEdge帳戶建立關聯。 當頁面作者或管理員將網頁與BrightEdge帳戶關聯時，此標題會顯示在下拉式清單中。

1. 在邊欄中，按一下「工具>作業>雲端>Cloud Services」。
1. 按一下顯示在「BrightEdge Content Optimizer」區段中的連結。 是否已建立BrightEdge設定，會決定連結文字：

   * 立即配置：未建立任何設定時，就會顯示此連結。
   * 顯示配置：建立一或多個設定時，就會顯示此連結。

   ![chlimage_1-4](assets/chlimage_1-4a.png)

1. 如果按一下「顯示配置」，請按一下「可用配置」旁的+連結。
1. 輸入設定的標題。 （可選）鍵入用於將配置儲存在儲存庫中的節點的名稱。 按一下建立。
1. 在「BrightEdge Content Optimizer配置」對話框中，鍵入BrightEdge帳戶的用戶名和密碼，然後按一下「確定」。

## 編輯BrightEdge組態 {#editing-a-brightedge-configuration}

視需要修改BrightEdge設定的使用者名稱和密碼。 修改會影響使用設定的所有頁面。

1. 在邊欄中，按一下「工具>作業>雲端>Cloud Services」。
1. 在「BrightEdge Content Optimizer」區段中，按一下「顯示配置」。

   ![chlimage_1-5](assets/chlimage_1-5a.png)

1. 按一下您要編輯的組態名稱。
1. 按一下「編輯」，修改屬性值，然後按一下「確定」。

## 將頁面與BrightEdge組態關聯 {#associating-pages-with-a-brightedge-configuration}

將頁面與BrightEdge設定關聯，以將頁面資料傳送至BrightEdge服務進行分析。 將頁面與配置關聯時，子頁面將繼承關聯。 通常，您會將網站的首頁建立關聯，以便從所有頁面傳送資料至BrightEdge。

1. 開啟傳統網站主控台。 ([http://localhost:4502/siteadmin#/content](http://localhost:4502/siteadmin#/content))
1. 在「網站」樹中，選擇包含要與BrightEdge配置關聯的頁的資料夾或頁。
1. 在頁面清單中，以滑鼠右鍵按一下要設定的頁面，然後按一下「屬性」。
1. 在「Cloud Services」頁簽上，按一下「添加服務」按鈕，然後在「Cloud Services」對話框中，選擇「BrightEdge Content Optimizer」，然後按一下「確定」。
1. 在BrightEdge Content Optimizer清單中，選擇要與頁面關聯的BrightEdge配置，然後按一下「確定」。

   ![chlimage_1-6](assets/chlimage_1-6a.png)

## 啟用BrightEdge組態 {#activating-a-brightedge-configuration}

啟動BrightEdge設定，以在發佈執行個體上複製該設定，並讓已發佈頁面與BrightEdge服務互動。

1. 在邊欄上，按一下「網站」，然後瀏覽並選取您與BrightEdge設定相關聯的頁面。
1. 按一下或點選「發佈」圖示，然後按一下或點選「發佈」。

   ![chlimage_1-7](assets/chlimage_1-7a.png)

1. 在顯示的設定清單中，確定已選取您的BrightEdge設定，然後按一下「發佈」。

   ![chlimage_1-8](assets/chlimage_1-8a.png)
