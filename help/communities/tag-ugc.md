---
title: 標籤使用者產生的內容
description: 標籤使用者產生的內容(UGC)是社群成員如何協助其他成員搜尋內容
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 4%

---

# 標籤使用者產生的內容 {#tagging-user-generated-content}

## 概觀 {#overview}

標籤使用者產生的內容(UGC)是社群成員協助其他成員搜尋內容的方法。

標籤通常由作者和管理員在作者環境中套用。 標籤UGC的獨特之處在於，UGC標籤已由發佈環境中的社群成員套用。

兩個應用程式的標籤名稱空間和分類相同。

## Communities功能 {#communities-features}

可設定為允許標籤的AEM Communities功能包括：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [檔案庫](file-library.md)
* [論壇](forum.md#configuretheaddedforum)
* [問題與答案](working-with-qna.md)

## 管理標記 {#administering-tags}

請參閱[管理標籤](../../help/sites-administering/tags.md#tagging-console)，以建立和管理標籤名稱空間和分類。

如需開發人員資訊，請參閱[Tag Essentials](tag.md)。

請參閱[使用Social Tag Cloud](tagcloud.md)，將Social Tag Cloud元件新增至頁面，以方便使用套用的標籤搜尋已張貼的UGC。

### 標籤許可權 {#tag-permissions}

預設許可權已設定為不允許發佈環境中的每個人都讀取標籤名稱空間。

由於標籤已套用至發佈環境中的UGC，因此社群成員需要啟用讀取許可權，才能選取標籤以套用。

請參閱[設定標籤許可權](../../help/sites-administering/tags.md#setting-tag-permissions)。

下列是管理員對群組`Community Engage Members`的`/etc/tag/discussions`套用讀取許可權時，它在CRXDE中的顯示方式。

![標籤許可權](assets/tag-permissions.png)
