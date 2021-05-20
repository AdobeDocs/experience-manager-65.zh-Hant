---
title: 社群群組要點
seo-title: 社群群組要點
description: 動態建立社群網站
seo-description: 動態建立社群網站
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---

# 社區組要點{#community-group-essentials}

社群群組功能是讓來自發佈和製作環境的授權使用者在社群網站內動態建立子社群的功能。

自Communities [Feature Pack 1](deploy-communities.md#latestfeaturepack)起，群組可以巢狀內嵌在其他群組中

## 客戶端{#essentials-for-client-side}的要點

### 社區組成員清單{#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交/群組/元件/hbs/社群組成員清單</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
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
   <td>社交/群組/元件/hbs/社群群組</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](client-customize.md)

## 伺服器端{#essentials-for-server-side}的要點

* [社群群組API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [社群群組端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 組函式{#groups-function}

包含[群組函式](functions.md#groups-function)的社群網站結構將支援從發佈和製作環境建立新的`community groups`。 建立的社區組將包含一個`community groups member list`元件，該元件將列出該組的成員。

當將函式添加到[社區站點模板](sites.md)中或嵌套在社區組模板中時，可為組函式配置一個或多個[社區組模板](tools-groups.md)，該模板提供社區組頁的設計。

納入多個社區組模板導致在為社區站點建立新社區組時向授權用戶呈現設計選項，如[社區組](creating-groups.md)上針對作者的部分所示。

### 嵌套組{#nested-groups}

從Communities [FP1](deploy-communities.md#latestfeaturepack)開始，組函式可以包含在組模板中，從而允許嵌套組（子社區）。

當社群網站或群組範本包含「群組」功能時，您可以：

* 在製作環境中建立子社群。

* 在發佈環境中建立群組（若設定為允許）。

在製作環境中建立群組時，必須先發佈社群網站，然後再發佈群組。 發佈社區網站將發佈組的頁面，而不建立設定ACL的子社區成員組。 因此，在顯式發佈組之前，可以顯示受限（秘密）組。

## 連結和相關資訊{#links-and-related-information}

* [管理使用者和使用者群組](users.md)
* [Communities群組主控台](groups.md)
* [組函式](functions.md#groups-function)
* [群組範本](tools-groups.md)
