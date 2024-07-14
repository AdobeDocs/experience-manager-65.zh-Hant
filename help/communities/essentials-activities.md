---
title: Activity Stream Essentials
description: 成員最近執行的活動清單，或內容單一執行緒上的最近活動清單
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---

# Activity Stream Essentials {#activity-stream-essentials}

已登入社群成員的活動（例如張貼至論壇或部落格）會收集到資料流中，可透過活動資料流元件的設定以各種方式篩選及顯示。

當社群成員追蹤感興趣的張貼或其他社群成員時，追蹤功能會新增另一組活動。

所有[社群網站](/help/communities/overview.md#communitiessites)皆包含已登入成員的使用者設定檔頁面，此頁面會以相同方式顯示成員活動。

## 概念 {#concepts}

*活動資料流*&#x200B;是成員最近執行的活動清單，或是內容單一執行緒（例如論壇主題或部落格）上最近的活動清單。

成員可以追隨活動資料流，方法是追隨其他個人或內容。

*新聞摘要*&#x200B;是將成員所追蹤的活動資料流合併成單一資料流。

*[社交圖](/help/communities/essentials-socialgraph.md)*&#x200B;會擷取一個成員與另一個成員的下列關係。

## 使用者端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
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
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱<a href="/help/communities/activities.md">活動資料流功能</a></td>
  </tr>
 </tbody>
</table>

* [使用者端自訂](/help/communities/client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [活動資料流API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [活動串流接聽程式API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [伺服器端自訂](/help/communities/server-customize.md)

### 活動資料流功能 {#activity-stream-function}

包含[活動資料流函式](/help/communities/functions.md#activity-stream-function)的社群網站結構包含已設定的`activity streams`元件。
