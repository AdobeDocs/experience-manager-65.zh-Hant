---
title: Communities元件基本知識
description: 在編輯模式下將社群功能新增至AEM網站並設定元件
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 1%

---

# Communities元件基本知識 {#communities-components-basics}

## 概觀 {#overview}

檔案的製作區段說明如何在作者編輯模式中將Communities功能新增至AEM網站，以及說明元件設定。

可以使用AEM執行個體和互動式[社群元件指南](components-guide.md)來探索元件。

## 存取Communities元件 {#accessing-communities-components}

編寫頁面內容時，如果基礎範本允許變更頁面設計，則有可能啟用元件瀏覽器中尚未提供的元件，做為網站設計的一部分。

檢視[可用社群元件](author-communities.md#available-communities-components)下的清單。

>[!NOTE]
>
>如需一般編寫資訊，請檢視[編寫頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md)。
>
>如果不熟悉AEM，請檢視有關[基本處理](../../help/sites-authoring/basic-handling.md)的檔案。

### 進入設計模式 {#entering-design-mode}

如果在元件瀏覽器(sidekick)中找不到&#x200B;**Communities**&#x200B;元件，則必須輸入`Design Mode`以新增其他Communities元件。 [可能也需要新增必要的使用者端資料庫](#required-clientlibs) (clientlibs)。

如需詳細資訊，請參閱[在設計模式中設定元件](../../help/sites-authoring/default-components-designmode.md)。

以下是選取一些Communities元件並在元件瀏覽器中檢視這些元件的影像：

![元件設計](assets/component-design.png)

元件瀏覽器現在提供選取的元件：

![元件設計1](assets/component-design1.png)

## 必要的Clientlibs {#required-clientlibs}

[必須有](../../help/sites-developing/clientlibs.md)使用者端資料庫(clientlibs)，元件才能正常運作(JavaScript)和樣式設定(CSS)。

將Communities元件新增至頁面時，如果結果為錯誤或意外外觀，首先要嘗試為Communities元件新增必要的clientlibs。 如需詳細資訊，請參閱[社群元件的Clientlibs](clientlibs.md)。

### 範例：最初放置的檢閱沒有使用者端資料庫…… {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...以及使用使用者端資料庫 {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## 標記 {#tagging}

許多Communities功能皆可設定為允許成員標籤在發佈環境中輸入（張貼）的內容。

如果允許標籤，則可設定社群網站的設定，以限制向發佈環境中的成員顯示的名稱空間。 檢視[社群網站主控台](sites-console.md#tagging)。

允許標籤的功能： [部落格](blog-feature.md)、[行事曆](calendar.md)、[檔案庫](file-library.md)、[論壇](forum.md)

使用標籤的功能： [搜尋](search.md)，[社交標籤雲端](tagcloud.md)

如需製作資訊：

* [使用標記](../../help/sites-authoring/tags.md)

如需管理資訊：

* 正在建立標籤名稱空間（分類法）： [管理標籤](../../help/sites-administering/tags.md)
* 社群網站組態：請參閱[標籤](sites-console.md#tagging)
* [標籤使用者產生的內容](../../help/sites-authoring/tags.md)

如需開發人員資訊：

* [AEM 標記框架](../../help/sites-developing/framework.md)
* [標籤Essentials](tag.md)
