---
title: 標籤要點
seo-title: 標籤要點
description: 標籤概觀
seo-description: 標籤概觀
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---

# 標籤要點{#tag-essentials}

在設定AEM Communities元件時啟用標籤時，社群成員就能標籤他們在發佈環境中張貼的內容。

發佈環境中套用之標籤的基礎架構，與在製作環境中套用至內容（例如頁面和資產）的標籤相同：

* 如需建立和管理標籤的相關資訊，請參閱[管理標籤](../../help/sites-administering/tags.md)和[標籤使用者產生的內容](tag-ugc.md)(UGC)。

* 如需[標籤架構](../../help/sites-developing/framework.md)以及在[自訂應用程式](../../help/sites-developing/building.md)中包含和延伸標籤的相關資訊，請參閱[開發人員的標籤](../../help/sites-developing/tags.md)。

* 請參閱[使用Social Tag Cloud](tagcloud.md) ，了解作者如何將`social tag cloud`元件新增至頁面，以反白標示在發佈環境中套用至UGC的標籤。

* 有關為目錄標籤資源的資訊，請參閱[標籤啟用資源](tag-resources.md)。

配置[社區站點](sites-console.md#tagging)或以下功能之一時，可以啟用UGC的標籤：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [檔案庫](file-library.md)
* [論壇](forum.md)
* [QnA](working-with-qna.md)

## 客戶端{#essentials-for-client-side}的要點

### 社交標籤雲{#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包括</strong></a></td>
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
   <td> <strong>cs</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參閱<a href="tagcloud.md">使用社交標籤雲</a></td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](client-customize.md)

## 伺服器端{#essentials-for-server-side}的要點

* [Social Tag Cloud API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [社交標籤管理員](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [伺服器端自訂](server-customize.md)

## 標籤搜索{#tag-searching}

自[feature pack 1](deploy-communities.md#latestfeaturepack)(FP1)起，使用[標籤標題](../../help/sites-developing/framework.md#tag-characteristics)執行標籤搜索。

在FP1之前，搜尋是使用[標籤id](../../help/sites-developing/framework.md#tagid)執行。
