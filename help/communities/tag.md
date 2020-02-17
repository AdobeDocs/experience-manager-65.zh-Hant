---
title: Tag Essentials
seo-title: Tag Essentials
description: 標籤概述
seo-description: 標籤概述
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Tag Essentials {#tag-essentials}

當AEM Communities元件設定為啟用標籤時，社群成員可以標籤他們在發佈環境中張貼的內容。

在發佈環境中套用之標籤的基礎架構與在作者環境中套用至內容（例如頁面和資產）的標籤相同：

* 如需 [建立和管理](../../help/sites-administering/tags.md) 標籤 [](tag-ugc.md) 的相關資訊，請參閱管理標籤和標籤使用者產生的內容(UGC)。

* 如需 [自訂應用程式中標籤框](../../help/sites-developing/tags.md) 架 [，以及包含和擴充標籤的相關資訊，請參閱「為開發人員](../../help/sites-developing/framework.md) 標籤」 [](../../help/sites-developing/building.md)。

* 如需 [作者如何新增元件至頁面以反白標示發佈環境中套用至](tagcloud.md)`social tag cloud` UGC之標籤的詳細資訊，請參閱使用Social Tag Cloud。

* 如需標 [記目錄資源的詳細資訊](tag-resources.md) ，請參閱標籤啟用資源。

在設定社群網站或下列功能之一 [時](sites-console.md#tagging) ，可啟用UGC標籤：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [檔案庫](file-library.md)
* [論壇](forum.md)
* [QnA](working-with-qna.md)

## 用戶端基本功能 {#essentials-for-client-side}

### Social Tag Cloud {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>included</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參 <a href="tagcloud.md">閱使用Social Tag Cloud</a></td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](client-customize.md)

## 伺服器端的基本功能 {#essentials-for-server-side}

* [Social Tag Cloud API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [社交標籤管理員](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [伺服器端自訂](server-customize.md)

## 標籤搜尋 {#tag-searching}

從功 [能包1](deploy-communities.md#latestfeaturepack) (FP1)開始，使用標籤標題執行標 [簽搜尋](../../help/sites-developing/framework.md#tag-characteristics)。

在FP1之前，使用標籤ID進 [行搜尋](../../help/sites-developing/framework.md#tagid)。
