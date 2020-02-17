---
title: Activity Stream Essentials
seo-title: Activity Stream Essentials
description: 成員最近執行的活動清單或單個內容線程上最近執行的活動清單
seo-description: 成員最近執行的活動清單或單個內容線程上最近執行的活動清單
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# Activity Stream Essentials{#activity-stream-essentials}

在社區成員中籤名的活動，例如張貼到論壇或部落格，被收集到流中，該流可以通過活動流元件的配置以各種方式被過濾和顯示。

當社群成員關注感興趣的帖子或其他社區成員時，跟隨能力會添加另一組活動。

所有 [社群網站](/help/communities/overview.md#communitiessites) ，都包含已登入會員的使用者設定檔頁面，以相同方式顯示會員活動。

## 概念 {#concepts}

活 *動流* ，是成員最近執行的活動的清單，或是內容單一線程（如論壇主題或部落格）上最近執行的活動的清單。

會員可以跟隨其他個人或內容，跟隨活動流。

新 *聞饋送* ，是將成員跟隨的活動串流合併為單一串流。

*社 [交圖](/help/communities/essentials-socialgraph.md)*可擷取一個成員與另一個成員的下列關係。

## 用戶端基本功能 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>included</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱 <a href="/help/communities/activities.md">活動串流功能</a></td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](/help/communities/client-customize.md)

## 伺服器端的基本功能 {#essentials-for-server-side}

* [活動串流API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [活動流偵聽器API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [伺服器端自訂](/help/communities/server-customize.md)

### 活動資料流功能 {#activity-stream-function}

一種包括活動流功能的社 [區站點結構](/help/communities/functions.md#activity-stream-function)，包括配置的 `activity streams` 元件。
