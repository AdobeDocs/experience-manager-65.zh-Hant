---
title: 活動流軟體包
seo-title: Activity Stream Essentials
description: 成員執行的最新活動清單或單個內容線程上最近活動的清單
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

# 活動流軟體包 {#activity-stream-essentials}

已登錄社區成員的活動，例如發佈到論壇或部落格，被收集到流中，該流可以通過活動流元件的配置以各種方式被過濾和顯示。

當社區成員跟蹤關注的帖子或其他社區成員時，跟蹤功能會添加另一組活動。

全部 [社區站點](/help/communities/overview.md#communitiessites) 包括登錄成員的用戶配置檔案頁，該頁面將以相同方式顯示成員活動。

## 概念 {#concepts}

安 *活動流* 是成員執行的最近活動的清單或單個內容線程（如論壇主題或部落格）上最近活動的清單。

成員可以通過跟蹤其他個人或內容來跟蹤活動流。

A *新聞* 是將成員跟蹤的活動流合併到單個流中。

A *[社會圖](/help/communities/essentials-socialgraph.md)* 捕獲一個成員與另一個成員的以下關係。

## 客戶端基本知識 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td>社交/活動流/元件/hbs/活動流</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>客戶端</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱 <a href="/help/communities/activities.md">活動流功能</a></td>
  </tr>
 </tbody>
</table>

* [客戶端自定義](/help/communities/client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [活動流API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [活動流偵聽器API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [伺服器端自定義](/help/communities/server-customize.md)

### 活動資料流功能 {#activity-stream-function}

包含該社區站點結構的 [活動流函式](/help/communities/functions.md#activity-stream-function)，包括已配置 `activity streams` 元件。
