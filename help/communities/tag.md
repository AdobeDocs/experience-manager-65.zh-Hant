---
title: 標籤軟體包
seo-title: Tag Essentials
description: 標籤概述
seo-description: Tag overview
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 2%

---

# 標籤軟體包 {#tag-essentials}

當AEM Communities元件配置為啟用標籤時，社區成員可以標籤他們在發佈環境中發佈的內容。

在發佈環境中應用的標籤的基礎結構與在作者環境中應用於內容的標籤（如頁面和資產）的基礎結構相同：

* 請參閱 [管理標籤](../../help/sites-administering/tags.md) 和 [標籤用戶生成的內容](tag-ugc.md) (UGC)，以獲取有關建立和管理標籤的資訊。

* 請參閱 [為開發人員添加標籤](../../help/sites-developing/tags.md) 的 [標籤框架](../../help/sites-developing/framework.md) 以及在 [自定義應用程式](../../help/sites-developing/building.md)。

* 請參閱 [使用社交標籤雲](tagcloud.md) 有關如何添加 `social tag cloud` 元件到頁面，以突出顯示在發佈環境中應用於UGC的標籤。

配置UGC時，可啟用UGC標籤 [社區站點](sites-console.md#tagging) 或以下功能之一：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [檔案庫](file-library.md)
* [論壇](forum.md)
* [QnA](working-with-qna.md)

## 客戶端基本知識 {#essentials-for-client-side}

### 社交標籤雲 {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td>社會/公共/元件/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>客戶端</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參閱 <a href="tagcloud.md">使用社交標籤雲</a></td>
  </tr>
 </tbody>
</table>

* [客戶端自定義](client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [社交標籤雲API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [社交標籤管理器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [伺服器端自定義](server-customize.md)

## 標籤搜索 {#tag-searching}

截至 [功能包1](deploy-communities.md#latestfeaturepack) (FP1)，使用 [標題](../../help/sites-developing/framework.md#tag-characteristics)。

在FP1之前，使用 [標籤ID](../../help/sites-developing/framework.md#tagid)。
