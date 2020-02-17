---
title: 社群元件基礎知識
seo-title: 社群元件基礎知識
description: 以編輯模式新增社群功能至AEM網站並設定元件
seo-description: 以編輯模式新增社群功能至AEM網站並設定元件
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 社群元件基礎知識 {#communities-components-basics}

## 概覽 {#overview}

說明檔案的編寫章節說明以作者編輯模式將社群功能新增至AEM網站，以及說明元件組態。

您可使用AEM例項和互動式社群元件指南來探 [索元件](components-guide.md)。

## 訪問社群元件 {#accessing-communities-components}

製作頁面內容時，如果基礎範本允許變更頁面設計，則可啟用在網站設計中元件瀏覽器中尚未提供的元件。

此處列出了可用的Communities [元件](author-communities.md#available-communities-components)。

>[!NOTE]
>
>如需一般製作資訊，請檢視 [製作頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md)。
>
>如果不熟悉AEM，請檢視基本處理的 [檔案](../../help/sites-authoring/basic-handling.md)。

### 進入設計模式 {#entering-design-mode}

如果在 **元件瀏覽器** (sidekick)中找不到Communities元件，則必須輸入才能 `Design Mode` 新增其他Communities元件。 [也可能需要新增必要的用戶端程式庫](#required-clientlibs) (clientlibs)。

如需詳細資訊，請 [參閱「在設計模式中設定元件」](../../help/sites-authoring/default-components-designmode.md)。

以下是選取一些Communities元件並在元件瀏覽器中檢視這些元件的影像：

![chlimage_1-424](assets/chlimage_1-424.png)

現在，元件瀏覽器中可使用選取的元件：

![chlimage_1-425](assets/chlimage_1-425.png)

## 必要的Clientlibs {#required-clientlibs}

[需要用戶端程式庫](../../help/sites-developing/clientlibs.md) (clientlibs)，才能正確運作元件(JavaScript)和樣式(CSS)。

在將Communities元件新增至頁面時，如果結果是錯誤或非預期的外觀，首先要嘗試新增Communities元件所需的clientlibs。 如需詳細資訊，請參 [閱Clientlibs for Communities元件](clientlibs.md)。

### 範例：最初放置的審核沒有客戶端庫…… {#example-initially-placed-reviews-without-client-libraries}

![chlimage_1-426](assets/chlimage_1-426.png)

### ...使用用戶端程式庫 {#and-with-client-libraries}

![chlimage_1-427](assets/chlimage_1-427.png)

## 標記 {#tagging}

許多社群功能可設定為允許成員標籤在發佈環境中輸入（發佈）的內容。

如果允許標籤，則可以設定社區站點的配置，以限制發佈環境中成員顯示的名稱空間。 請參閱社 [群網站主控台](sites-console.md#tagging)。

允許標籤的功能：部 [落格](blog-feature.md)、 [日曆](calendar.md)、 [檔案庫](file-library.md)、論 [壇](forum.md)

使用標籤的功能：目 [錄](catalog.md)、搜 [尋](search.md)、社 [交標籤雲](tagcloud.md)

製作資訊：

* [使用標籤](../../help/sites-authoring/tags.md)

若需管理資訊：

* 建立標籤名稱空間（分類）:管 [理標籤](../../help/sites-administering/tags.md)
* 社群網站設定：請參閱 [標籤](sites-console.md#tagging)
* [標籤使用者產生的內容](../../help/sites-authoring/tags.md)
* [標籤啟用資源](tag-resources.md)

如需開發人員資訊：

* [AEM標籤架構](../../help/sites-developing/framework.md)
* [標籤基本功能](tag.md)

