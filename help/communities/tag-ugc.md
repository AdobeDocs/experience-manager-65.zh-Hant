---
title: 標籤使用者產生的內容
seo-title: 標籤使用者產生的內容
description: 標籤使用者產生的內容(UGC)是社群成員如何協助其他成員搜尋內容
seo-description: 標籤使用者產生的內容(UGC)是社群成員如何協助其他成員搜尋內容
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 標籤使用者產生的內容 {#tagging-user-generated-content}

## 概覽 {#overview}

標籤使用者產生的內容(UGC)是社群成員可協助其他成員搜尋內容的方式。

通常，標籤由作者和管理員在作者環境中套用。 標籤UGC是唯一的，因為UGC標籤是由發佈環境中的社群成員套用的。

這兩個應用程式的標籤名稱空間和分類都相同。

## 社群功能 {#communities-features}

可設定為允許標籤的AEM Communities功能為

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [檔案庫](file-library.md)
* [論壇](forum.md#configuretheaddedforum)
* [問題與答案](working-with-qna.md)

## 管理標籤 {#administering-tags}

請參 [閱管理標籤](../../help/sites-administering/tags.md#tagging-console) ，以建立和管理標籤名稱空間和分類。

如需開 [發人員資訊](tag.md) ，請參閱Tag Essentials。

請參 [閱使用Social Tag Cloud](tagcloud.md) ，將Social Tag cloud元件新增至頁面，以利使用套用的標籤搜尋已張貼的UGC。

### 標籤權限 {#tag-permissions}

預設權限設定為不允許發佈環境中的每個人讀取標籤名稱空間。

由於標籤會套用至發佈環境中的UGC，因此必須為社群成員啟用讀取權限，才能讓他們選取要套用的標籤。

請參閱 [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)。

以下是當管理員將讀取權限套用至群組時，在CRXDE中 `/etc/tag/discussions` 的顯示方式 `*Community Engage Members*`。

![chlimage_1-74](assets/chlimage_1-74.png)

