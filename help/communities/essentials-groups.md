---
title: 社群群組要點
description: 瞭解獲授權的使用者如何使用社群群組功能，在社群網站中動態建立子社群。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%
---
# 社群群組要點  {#community-group-essentials}

社群群組功能可讓發佈和作者環境中的授權使用者在社群網站中動態建立子社群。

自Communities [功能套件1](deploy-communities.md#latestfeaturepack)起，群組可巢狀內嵌於其他群組中。

## 使用者端的Essentials {#essentials-for-client-side}

### 社群群組成員清單 {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroupmemberlist</td>
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
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>檢視<a href="creating-groups.md">社群群組</a></td>
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
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [社群群組API](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [社群群組端點](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 群組功能 {#groups-function}

包含[群組函式](functions.md#groups-function)的社群網站結構支援從發佈和作者環境建立新的`community groups`。 建立的社群群組包含列出群組成員的`community groups member list`元件。

一或多個[社群群組範本](tools-groups.md)提供社群群組頁面的設計，可設定為「群組」功能。 將函式新增至[社群網站範本](sites.md)或巢狀加入社群群組範本時，即屬如此。

納入多個社群群組範本後即可供選擇。 亦即，在為社群網站建立社群群組時，向授權使用者呈現的設計選擇。 請參閱作者的[社群群組](creating-groups.md)相關章節。

### 巢狀群組 {#nested-groups}

從Communities [FP1](deploy-communities.md#latestfeaturepack)開始，群組功能可以包含在群組範本中，因此允許巢狀群組（子社群）。

當社群網站或群組範本包含「群組」功能時，可以：

* 在製作環境中建立子社群。

* 設定為允許時，在發佈環境中建立群組。

在作者環境中建立群組時，必須先發佈社群網站，然後再發佈群組。 發佈社群網站會發佈群組的頁面，而不需建立ACL所設定的子社群成員群組。 因此，在群組明確發佈之前，受限制的（秘密）群組可能一直可見。

## 連結和相關資訊 {#links-and-related-information}

* [管理使用者和使用者群組](users.md)
* [社群群組主控台](groups.md)
* [群組功能](functions.md#groups-function)
* [群組範本](tools-groups.md)
