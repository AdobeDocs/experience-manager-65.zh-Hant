---
title: 標籤使用者產生的內容
seo-title: 標籤使用者產生的內容
description: 標籤使用者產生的內容(UGC)是社群成員如何協助其他成員搜尋內容的方法
seo-description: 標籤使用者產生的內容(UGC)是社群成員如何協助其他成員搜尋內容的方法
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
role: Administrator
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 3%

---

# 標籤使用者產生的內容{#tagging-user-generated-content}

## 概覽 {#overview}

標籤使用者產生的內容(UGC)是社群成員可協助其他成員搜尋內容的方式。

標籤通常是由作者和管理員在製作環境中套用。 標籤UGC是唯一的，因為UGC標籤是由發佈環境中的社群成員套用。

這兩個應用程式的標籤命名空間和分類相同。

## 社區功能{#communities-features}

可設定為允許標籤的AEM Communities功能包括：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [檔案庫](file-library.md)
* [論壇](forum.md#configuretheaddedforum)
* [問題與答案](working-with-qna.md)

## 管理標籤{#administering-tags}

請參閱[管理標籤](../../help/sites-administering/tags.md#tagging-console)，以了解如何建立和管理標籤命名空間和分類。

如需開發人員資訊，請參閱[Tag Essentials](tag.md) 。

請參閱[使用Social Tag Cloud](tagcloud.md) ，將Social Tag Cloud元件新增至頁面，以利使用套用的標籤來搜尋已張貼的UGC。

### 標籤權限{#tag-permissions}

預設權限設為不允許發佈環境中的每個人讀取標籤命名空間。

由於標籤會在發佈環境中套用至UGC，因此必須為社群成員啟用讀取權限，才能夠選取要套用的標籤。

請參閱[設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)。

以下是當管理員將讀取權限應用於組`Community Engage Members`的`/etc/tag/discussions`時，CRXDE中顯示的方式。

![標籤權限](assets/tag-permissions.png)
