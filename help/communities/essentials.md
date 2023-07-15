---
title: 元件、函式和Feature Essentials
description: 社群網站、範本和群組的運作方式
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: e161c37544c3391607cbe495644f3353b9f77fe3
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 17%

---

# 元件、函式和Feature Essentials  {#component-function-and-feature-essentials}

Adobe Experience Manager (AEM) Communities功能需要網站訪客成為會員並登入 [社群網站](overview.md#communitiessites) 之後才能發佈內容。 因此， [社群網站範本](sites.md)，社群網站會從此建立 [已建立](sites-console.md)，包含登入功能和使用者設定檔、傳訊、搜尋、稽核和翻譯。

社群網站支援成員建立社群群組，當 [社群群組功能](functions.md#groups-function) 包含在選取的社群網站範本中。

以下是Communities元件、功能和功能之基本資訊的連結。

## 基本元件 {#base-components}

* [評論](essentials-comments.md)
* [評論](reviews-basics.md)
* [總計](tally.md)

   * [連結](essentials-liking.md)
   * [評等](rating-basics.md)
   * [投票](essentials-voting.md)
   * *輪詢（已無法使用）*

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
* [元件側載](sideloading.md)
* [傳送訊息](essentials-messaging.md)
* [RTF 編輯器](rte.md)
* [評分和預算](configure-scoring.md)
* [搜尋](search-implementation.md)
* [社交圖](essentials-socialgraph.md)
* [儲存資源提供者](srp-and-ugc.md) `(SRP)`

* [標記](tag.md)

## Javadocs {#javadocs}

此 [線上javadocs](../../help/sites-developing/reference-materials.md) 反映AEM 6.3版本中可用的API。
社群API位於 `com.adobe.cq.social.*` 封裝。

針對每個 [feature pack](deploy-communities.md#latestfeaturepack)，即可使用javadoc jar。 如需詳細資訊，請造訪 [使用適用於社群的Maven](maven.md#javadocs).

## 其他資訊 {#additional-information}

* [社交元件架構(SCF)](scf.md)

   * [使用者端自訂](client-customize.md)
   * [伺服器端自訂](server-customize.md)
   * [儲存資源提供者概觀](srp.md)

* [編碼准則](code-guide.md)
* [教學課程](tutorials.md)
* [疑難排解](troubleshooting.md)
