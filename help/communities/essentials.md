---
title: 元件、功能和功能要素
seo-title: Component, Function and Feature Essentials
description: 社區站點、模板和組的功能
seo-description: How community sites, templates, and groups function
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 17%

---

# 元件、功能和功能要素  {#component-function-and-feature-essentials}

AEM Communities功能要求站點訪問者成為成員並登錄到 [社區站點](overview.md#communitiessites) 才能發佈內容。 因此， [社區網站模板](sites.md)，社區站點從中 [建立](sites-console.md)，旨在包括登錄功能以及用戶配置檔案、消息、搜索、審核和翻譯。

社區站點將支援成員在 [社區組功能](functions.md#groups-function) 包含在所選社區網站模板中。

以下是社區元件、功能和功能的基本資訊連結。

## 基本元件 {#base-components}

* [評論](essentials-comments.md)
* [評論](reviews-basics.md)
* [計數](tally.md)

   * [連結](essentials-liking.md)
   * [評等](rating-basics.md)
   * [投票](essentials-voting.md)
   * *輪詢（不再可用）*

## 具有函式的元件 {#components-with-functions}

* [活動資料流](essentials-activities.md)
* [部落格](blog-developer-basics.md) ( `Journal`)

* [日曆](calendar-basics-for-developers.md)
* [主要內容](essentials-featured.md)
* [檔案庫](essentials-file-library.md)
* [論壇](essentials-forum.md)
* [群組](essentials-groups.md)
* [創意力](ideation.md)
* [排行榜](leaderboard.md)
* [問題與答案](qna-essentials.md) `(QnA)`

## 功能 {#features}

* [用戶端資料庫](clientlibs.md)
* [社群網站](sites-for-developers.md)
* [元件OSGi事件](events.md)
* [元件旁載入](sideloading.md)
* [傳送訊息](essentials-messaging.md)
* [RTF 編輯器](rte.md)
* [評分和徽章](configure-scoring.md)
* [搜尋](search-implementation.md)
* [社交圖](essentials-socialgraph.md)
* [儲存資源提供程式](srp-and-ugc.md) `(SRP)`

* [標記](tag.md)

## 賈瓦多克 {#javadocs}

的 [線上javadoc](../../help/sites-developing/reference-materials.md) 反映6.3版中AEM的API。
社區API位於 `com.adobe.cq.social.*` 包。

每個 [特徵包](deploy-communities.md#latestfeaturepack)，將提供javadoc jar。 有關詳細資訊，請訪問 [將Maven用於社區](maven.md#javadocs)。

## 其他資訊 {#additional-information}

* [社會構成框架](scf.md)

   * [客戶端自定義](client-customize.md)
   * [伺服器端自定義](server-customize.md)
   * [儲存資源提供程式概述](srp.md)

* [編碼准則](code-guide.md)
* [教學課程](tutorials.md)
* [疑難排解](troubleshooting.md)
