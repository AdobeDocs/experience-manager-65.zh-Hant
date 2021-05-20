---
title: Communities元件基本知識
seo-title: Communities元件基本知識
description: 以編輯模式將Communities功能新增至AEM網站並設定元件
seo-description: 以編輯模式將Communities功能新增至AEM網站並設定元件
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---

# Communities元件基本知識{#communities-components-basics}

## 概覽 {#overview}

本檔案的製作區段說明如何以作者編輯模式將Communities功能新增至AEM網站，並說明元件設定。

可使用AEM例項和互動式[社群元件指南](components-guide.md)探索元件。

## 訪問Communities元件{#accessing-communities-components}

編寫頁面內容時，如果基礎範本允許對頁面設計進行變更，則可以啟用元件瀏覽器中尚未提供的元件作為網站設計的一部分。

可用的Communities元件列於[此處](author-communities.md#available-communities-components)。

>[!NOTE]
>
>如需一般製作資訊，請檢視[製作頁面快速指南](../../help/sites-authoring/qg-page-authoring.md)。
>
>若不熟悉AEM，請檢視[basic handling](../../help/sites-authoring/basic-handling.md)上的檔案。

### 進入設計模式{#entering-design-mode}

如果在元件瀏覽器(sidekick)中找不到&#x200B;**Communities**&#x200B;元件，則需要輸入`Design Mode`以新增其他Communities元件。 [也可能需要新增必要的用戶端程式庫](#required-clientlibs) (clientlibs)。

如需詳細資訊，請參閱[在設計模式下配置元件](../../help/sites-authoring/default-components-designmode.md)。

以下是選取幾個Communities元件並在元件瀏覽器中檢視的影像：

![元件設計](assets/component-design.png)

所選元件現在可在元件瀏覽器中使用：

![component-design1](assets/component-design1.png)

## 必需的Clientlibs {#required-clientlibs}

[元件的正常運作(JavaScript)和樣式(CSS)需要用戶端程式庫](../../help/sites-developing/clientlibs.md) (clientlibs)。

將Communities元件新增至頁面時，如果結果為錯誤或非預期的外觀，首先要嘗試為Communities元件新增所需的clientlibs。 如需詳細資訊，請參閱[Clientlibs for Communities Components](clientlibs.md)。

### 範例：最初置入的審核不包含客戶端庫…… {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...使用客戶端庫{#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## 標記 {#tagging}

許多Communities功能可經過設定，以允許成員標籤在發佈環境中輸入（發佈）的內容。

如果允許進行標籤，社群網站的設定可設為限制發佈環境中成員呈現的命名空間。 請參閱[社群網站主控台](sites-console.md#tagging)。

允許標籤的功能：[blog](blog-feature.md), [日曆](calendar.md), [檔案庫](file-library.md), [論壇](forum.md)

使用標籤的功能：[catalog](catalog.md), [search](search.md), [social tag cloud](tagcloud.md)

如需製作資訊：

* [使用標記](../../help/sites-authoring/tags.md)

管理資訊：

* 建立標籤命名空間（分類法）:[管理標籤](../../help/sites-administering/tags.md)
* 社區站點配置：請參閱[TAGGING](sites-console.md#tagging)
* [標籤使用者產生的內容](../../help/sites-authoring/tags.md)
* [標籤啟用資源](tag-resources.md)

如需開發人員資訊：

* [AEM標籤架構](../../help/sites-developing/framework.md)
* [標籤要點](tag.md)
