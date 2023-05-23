---
title: 社區元件基礎
seo-title: Communities Components Basics
description: 在編輯模式下向AEM站點添加社區功能並配置元件
seo-description: Add Communities features to AEM sites in edit mode and configure components
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---

# 社區元件基礎 {#communities-components-basics}

## 概觀 {#overview}

文檔的創作部分介紹在作者編輯模式AEM下向站點添加社區功能，以及說明元件配置。

可使用實例和交AEM互式探索元件 [社區元件指南](components-guide.md)。

## 訪問社區元件 {#accessing-communities-components}

在創作頁面內容時，如果基礎模板允許對頁面設計進行更改，則可以啟用在元件瀏覽器中尚未作為站點設計一部分的元件。

列出了可用的社區元件 [這裡](author-communities.md#available-communities-components)。

>[!NOTE]
>
>有關一般創作資訊，請查看 [創作頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md)。
>
>如果不熟悉AEM，請查看 [基本處理](../../help/sites-authoring/basic-handling.md)。

### 進入設計模式 {#entering-design-mode}

如果 **社區** 在元件瀏覽器(sidekick)中找不到元件，需要輸入 `Design Mode` 添加其他社區元件。 [所需的客戶端庫](#required-clientlibs) （客戶端）也可能需要添加。

有關詳細資訊，請參閱 [在設計模式下配置元件](../../help/sites-authoring/default-components-designmode.md)。

以下是選擇幾個社區元件並在元件瀏覽器中查看這些元件的影像：

![元件設計](assets/component-design.png)

選定的元件現在可在元件瀏覽器中使用：

![component-design1](assets/component-design1.png)

## 必需的客戶端 {#required-clientlibs}

[客戶端庫](../../help/sites-developing/clientlibs.md) 元件的正確運行(JavaScript)和樣式設定(CSS)需要(clientlibs)。

在將社區元件添加到頁面時，如果結果是錯誤或意外出現，則首先要嘗試為社區元件添加所需的客戶端。 有關詳細資訊，請參閱 [社區元件的客戶端](clientlibs.md)。

### 示例：最初放置的審閱沒有客戶端庫…… {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...使用客戶端庫 {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## 標記 {#tagging}

許多社區功能可配置為允許成員標籤在發佈環境中輸入（發佈）的內容。

如果允許添加標籤，則可以將社區站點的配置設定為限制發佈環境中成員呈現的命名空間。 查看 [社區站點控制台](sites-console.md#tagging)。

允許標籤的功能： [部落格](blog-feature.md)。 [日曆](calendar.md)。 [檔案庫](file-library.md)。 [論壇](forum.md)

使用標籤的功能： [搜索](search.md)。 [社會標籤雲](tagcloud.md)

有關創作資訊：

* [使用標記](../../help/sites-authoring/tags.md)

有關管理資訊：

* 正在建立標籤命名空間（分類）: [管理標籤](../../help/sites-administering/tags.md)
* 社區站點配置：見 [標籤](sites-console.md#tagging)
* [標籤用戶生成的內容](../../help/sites-authoring/tags.md)

有關開發人員資訊：

* [AEM 標記框架](../../help/sites-developing/framework.md)
* [標籤軟體包](tag.md)
