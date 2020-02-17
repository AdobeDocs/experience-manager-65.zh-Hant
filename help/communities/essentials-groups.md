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
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Community Group Essentials {#community-group-essentials}

社群群組功能是讓來自發佈和作者環境的授權使用者在社群網站中動態建立子社群的能力。

自Communities功 [能套件1起](deploy-communities.md#latestfeaturepack)，群組可能會巢狀內嵌在其他群組中

## 用戶端基本功能 {#essentials-for-client-side}

### 社區組成員清單 {#community-groups-member-list}

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
   <td>請參閱 <a href="creating-groups.md">社群群組</a></td>
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

## 伺服器端的基本功能 {#essentials-for-server-side}

* [社群群組API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [社群群組端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 群組函式 {#groups-function}

包含「群組」功能的社群網 [站結構](functions.md#groups-function) ，將支援從發佈和作者 `community groups` 環境建立新的網站。 所建立的社群群組將包含 `community groups member list` 一個元件，列出群組成員。

當功能被 [添加到社區站點模板或嵌套在社區組模板中時，可為「組」功能配置一個或多](tools-groups.md)個社區組模板 [](sites.md) ，該模板提供社區組頁的設計。

加入多個社群群組範本後，在為社群網站建立新社群群組時，會選擇向授權使用者呈現設計，如作者的社群群 [組](creating-groups.md) 。

### 巢狀群組 {#nested-groups}

自Communities [FP1起](deploy-communities.md#latestfeaturepack)，群組功能可能會包含在群組範本中，因此允許巢狀群組（子社群）。

當社群網站或群組範本包含「群組」功能時，

* 在作者環境中建立子社群
* 在發佈環境中建立群組（若設定為允許）

在作者環境中建立群組時，必須先發佈社群網站，然後發佈群組。 發佈社群站點將發佈組的頁面，而不建立ACL所設定的子社區成員組。 因此，在明確發佈組之前，可以看到受限（秘密）組。

## 連結與相關資訊 {#links-and-related-information}

* [管理使用者和使用者群組](users.md)
* [社群群組主控台](groups.md)
* [群組函式](functions.md#groups-function)
* [群組範本](tools-groups.md)

