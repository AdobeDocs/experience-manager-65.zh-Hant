---
title: Community Group Essentials
seo-title: Community Group Essentials
description: 動態建立社群網站
seo-description: 動態建立社群網站
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---


# 社區組基本工具{#community-group-essentials}

社群群組功能是讓來自發佈和作者環境的授權使用者在社群網站中動態建立子社群的能力。

從Communities [功能套件1](deploy-communities.md#latestfeaturepack)開始，群組可能會巢狀內嵌在其他群組中

## 客戶端{#essentials-for-client-side}的基本功能

### 社區組成員清單{#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參閱<a href="creating-groups.md">社群群組</a></td>
  </tr>
 </tbody>
</table>

### 社群群組 {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroups</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](client-customize.md)

## 伺服器端{#essentials-for-server-side}的基本工具

* [社群群組API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [社群群組端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 群組函式{#groups-function}

包含[Groups函式](functions.md#groups-function)的社群網站結構將支援從發佈和作者環境建立新`community groups`。 所建立的社區組將包含`community groups member list`元件，該元件將列出該組的成員。

當將該函式添加到[社區站點模板](sites.md)或嵌套在社區組模板中時，可為「組」功能配置一個或多個提供社區組頁設計的[社區組模板](tools-groups.md)。

加入多個社群群組範本後，在為社群網站建立新社群群組時，會向授權使用者呈現多種設計選擇，如作者[社群群組](creating-groups.md)一節所示。

### 巢狀群組{#nested-groups}

從社群[FP1](deploy-communities.md#latestfeaturepack)開始，群組功能可能會包含在群組範本中，因此允許巢狀群組（子社群）。

當社群網站或群組範本包含「群組」功能時，可以：

* 在作者環境中建立子社群。

* 在發佈環境中建立群組（設定為允許）。

在作者環境中建立群組時，必須先發佈社群網站，然後發佈群組。 發佈社群站點將發佈組的頁面，而不建立ACL所設定的子社區成員組。 因此，在明確發佈組之前，可以看到受限（秘密）組。

## 連結和相關資訊{#links-and-related-information}

* [管理使用者和使用者群組](users.md)
* [社群群組主控台](groups.md)
* [群組函式](functions.md#groups-function)
* [群組範本](tools-groups.md)

