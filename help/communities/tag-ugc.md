---
title: 標籤用戶生成的內容
seo-title: Tagging User Generated Content
description: 標籤用戶生成的內容(UGC)是社區成員如何幫助其他成員搜索內容
seo-description: Tagging of user generated content (UGC) is how community members can help other members search for content
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 3%

---

# 標籤用戶生成的內容 {#tagging-user-generated-content}

## 概觀 {#overview}

標籤用戶生成的內容(UGC)是社區成員幫助其他成員搜索內容的方法。

通常，標籤由作者和管理員在作者環境中應用。 標籤UGC的獨特之處在於UGC標籤由發佈環境中的社區成員應用。

標籤命名空間和分類對於兩個應用程式是相同的。

## 社區功能 {#communities-features}

可配置為允許標籤的AEM Communities功能包括：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [檔案庫](file-library.md)
* [論壇](forum.md#configuretheaddedforum)
* [問題與答案](working-with-qna.md)

## 管理標籤 {#administering-tags}

請參閱 [管理標籤](../../help/sites-administering/tags.md#tagging-console) 用於建立和管理標籤命名空間和分類。

請參閱 [標籤軟體包](tag.md) 開發人員資訊。

請參閱 [使用社交標籤雲](tagcloud.md) 用於向頁面添加社交標籤雲元件，以便使用應用的標籤搜索已發佈的UGC。

### 標籤權限 {#tag-permissions}

預設權限設定為不允許發佈環境中的每個人都讀取標籤命名空間。

由於標籤在發佈環境中應用到UGC，因此需要為社區成員啟用讀取權限，以便他們能夠選擇要應用的標籤。

請參閱 [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)。

以下是當管理員將讀取權限應用於 `/etc/tag/discussions` 為組 `Community Engage Members`。

![標籤權限](assets/tag-permissions.png)
