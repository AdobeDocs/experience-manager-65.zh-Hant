---
title: 標籤Essentials
description: 瞭解Communities元件設定為啟用標籤時，社群成員可標籤其在發佈環境中發佈的內容。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 2%

---

# 標籤Essentials {#tag-essentials}

設定AEM Communities元件並啟用標籤後，社群成員將可標籤他們在發佈環境中張貼的內容。

發佈環境中套用標籤的基礎基礎結構與製作環境中套用至內容（例如頁面和資產）的標籤基礎基礎結構相同：

* 如需建立和管理標籤的相關資訊，請參閱[管理標籤](../../help/sites-administering/tags.md)和[標籤使用者產生的內容](tag-ugc.md) (UGC)。

* 如需[標籤架構](../../help/sites-developing/framework.md)以及在[自訂應用程式](../../help/sites-developing/building.md)中包含和擴充標籤的詳細資訊，請參閱[開發人員標籤](../../help/sites-developing/tags.md)。

* 請參閱[使用Social Tag Cloud](tagcloud.md)，瞭解作者的相關資訊，瞭解如何將`social tag cloud`元件新增至頁面，以反白標示發佈環境中套用至UGC的標籤。

設定[社群網站](sites-console.md#tagging)或下列其中一項功能時，可以啟用UGC標籤：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [檔案庫](file-library.md)
* [論壇](forum.md)
* [QnA](working-with-qna.md)

## 使用者端的Essentials {#essentials-for-client-side}

### 社交標籤雲 {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參閱<a href="tagcloud.md">使用社交標籤雲端</a></td>
  </tr>
 </tbody>
</table>

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [社交標籤雲端API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [社交標籤管理員](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [伺服器端自訂](server-customize.md)

## 標籤搜尋 {#tag-searching}

自[Feature Pack 1](deploy-communities.md#latestfeaturepack) (FP1)起，已使用[標籤標題](../../help/sites-developing/framework.md#tag-characteristics)執行標籤搜尋。

在FP1之前，使用[標籤ID](../../help/sites-developing/framework.md#tagid)執行搜尋。
