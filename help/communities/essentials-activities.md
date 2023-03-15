---
title: 活動資料流要點
seo-title: Activity Stream Essentials
description: 由成員執行的最近活動的清單或單個內容線程上最近活動的清單
seo-description: List of recent activites performed by a member or a list of recent activities on a single thread of content
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---

# 活動資料流要點 {#activity-stream-essentials}

在社區成員中籤名的活動，例如張貼到論壇或部落格，被收集到流中，該流可以通過活動流元件的配置以各種方式被過濾和顯示。

當社群成員關注感興趣的帖子或其他社區成員時，跟隨能力將添加另一組活動。

全部 [社群網站](/help/communities/overview.md#communitiessites) 包括登錄成員的用戶配置檔案頁，該頁將以相同方式顯示成員活動。

## 概念 {#concepts}

安 *活動資料流* 是成員執行的最近活動的清單，或單個內容線程（如論壇主題或部落格）上最近活動的清單。

成員可以跟隨另一個個人或內容，跟隨活動流。

A *新聞摘要* 是活動流的合併，隨後成員將其合併為單個流。

A *[社交圖表](/help/communities/essentials-socialgraph.md)* 捕獲一個成員與另一個成員的以下關係。

## 用戶端的要點 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交/活動資料流/元件/hbs/活動資料流</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>包括</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱 <a href="/help/communities/activities.md">活動資料流功能</a></td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](/help/communities/client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [活動資料流API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [活動資料流接聽程式API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [伺服器端自訂](/help/communities/server-customize.md)

### 活動資料流功能 {#activity-stream-function}

包含 [活動資料流函式](/help/communities/functions.md#activity-stream-function)，包含已設定的 `activity streams` 元件。
