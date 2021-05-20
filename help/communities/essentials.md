---
title: 元件、功能和功能要點
seo-title: 元件、功能和功能要點
description: 社群網站、範本和群組如何運作
seo-description: 社群網站、範本和群組如何運作
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 17%

---

# 元件、函式和功能要點{#component-function-and-feature-essentials}

AEM Communities功能要求網站訪客必須成為成員，並先登入[社群網站](overview.md#communitiessites)，才能張貼內容。 因此，[社區站點模板](sites.md)被設計為包括登錄功能以及用戶配置檔案、消息、搜索、協調和翻譯。[](sites-console.md)

當所選社區站點模板中包含[社區組函式](functions.md#groups-function)時，社區站點將支援成員建立社區組。

以下是Communities元件、功能和功能的基本資訊連結。

## 基本元件{#base-components}

* [評論](essentials-comments.md)
* [評論](reviews-basics.md)
* [計數](tally.md)

   * [連結](essentials-liking.md)
   * [評等](rating-basics.md)
   * [投票](essentials-voting.md)
   * *民調問答（不再提供）*

## 具有函式{#components-with-functions}的元件

* [活動資料流](essentials-activities.md)
* [指定任務](essentials-assignments.md)
* [部落格](blog-developer-basics.md) ( `Journal`)

* [日曆](calendar-basics-for-developers.md)
* [目錄](catalog-developer-essentials.md)
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
* [元件側載](sideloading.md)
* [傳送訊息](essentials-messaging.md)
* [RTF 編輯器](rte.md)
* [計分和徽章](configure-scoring.md)
* [搜尋](search-implementation.md)
* [社交圖](essentials-socialgraph.md)
* [儲存資源提供程式](srp-and-ugc.md) `(SRP)`

* [標記](tag.md)

## Javadocs {#javadocs}

[線上javadocs](../../help/sites-developing/reference-materials.md)反映AEM 6.3版本中可用的API。
Communities API位於`com.adobe.cq.social.*`套件中。

對於每個[功能包](deploy-communities.md#latestfeaturepack)，將提供javadoc jar。 如需詳細資訊，請造訪[使用Maven for Communities](maven.md#javadocs)。

## 其他資訊 {#additional-information}

* [社會構成框架](scf.md)

   * [用戶端自訂](client-customize.md)
   * [伺服器端自訂](server-customize.md)
   * [儲存資源提供程式概述](srp.md)

* [編碼准則](code-guide.md)
* [教學課程](tutorials.md)
* [疑難排解](troubleshooting.md)
