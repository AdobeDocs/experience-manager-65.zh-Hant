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
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# 社群群組要點  {#community-group-essentials}

社群群組功能可讓發佈和作者環境中的授權使用者在社群網站中動態建立子社群。

社群起始 [feature pack 1](deploy-communities.md#latestfeaturepack)，群組可巢狀內嵌於其他群組中。

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
   <td>另請參閱 <a href="creating-groups.md">社群群組</a></td>
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

* [社群群組API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [社群群組端點](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 群組功能 {#groups-function}

社群網站結構包含 [群組功能](functions.md#groups-function) 支援建立新的 `community groups` 來自發佈和作者環境。 建立的社群群組包括 `community groups member list` 列出群組成員的元件。

一或多個 [社群群組範本](tools-groups.md)（提供社群群組頁面設計）可針對「群組」功能進行設定。 若要將函式新增至 [社群網站範本](sites.md) 或巢狀內嵌在社群群組範本中。

納入多個社群群組範本後即可供選擇。 亦即，在為社群網站建立社群群組時，向授權使用者呈現的設計選擇。 請參閱以下小節： [社群群組](creating-groups.md) 適用於作者。

### 巢狀群組 {#nested-groups}

社群起始 [FP1](deploy-communities.md#latestfeaturepack)，群組功能可包含在群組範本中，以便巢狀群組（子社群）。

當社群網站或群組範本包含「群組」功能時，可以：

* 在製作環境中建立子社群。

* 設定為允許時，在發佈環境中建立群組。

在作者環境中建立群組時，必須先發佈社群網站，然後再發佈群組。 發佈社群網站會發佈群組的頁面，而不需建立ACL所設定的子社群成員群組。 因此，在群組明確發佈之前，受限制的（秘密）群組可能一直可見。

## 連結和相關資訊 {#links-and-related-information}

* [管理使用者和使用者群組](users.md)
* [社群群組主控台](groups.md)
* [群組功能](functions.md#groups-function)
* [群組範本](tools-groups.md)
