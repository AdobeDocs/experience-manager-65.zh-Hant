---
title: 構想要點
seo-title: 構想要點
description: 構思功能概觀
seo-description: 構思功能概觀
uuid: abaf03ee-8bf4-4241-96c3-474c95a30a88
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9e4f2f0-d1ff-40c0-abcf-645e40586a84
exl-id: 7ad3592b-f8b5-45c0-97bc-15f781d7b811
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 3%

---

# 構想要點{#ideation-essentials}

本頁面提供使用構思功能的基本資訊，這類功能類似於論壇，但能儲存為草稿，且提供更協作的風格。

## 客戶端{#essentials-for-client-side}的要點

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交/構思/元件/hbs/構思</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包括</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.voting<br /> cq.social.hbs.like<br /> cq.social.hbs.ideation</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/ideation.hbs<br /> /libs/social/ideation/components/hbs/ideation/ideationlists.hbs<br /> /libs/social/ideation/components/hbs/ideation/composer.hbs</td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/clientlibs/ideation.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱<a href="ideation-feature.md">構想功能</a></td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](client-customize.md)

### 創意力功能 {#ideation-function}

包括[標識函式](functions.md#ideation-function)的社區站點結構包括配置的`ideation`元件。
