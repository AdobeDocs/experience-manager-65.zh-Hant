---
title: 社區組要件
seo-title: Community Group Essentials
description: 動態建立社區站點
seo-description: Creating community sites dynamically
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# 社區組要件  {#community-group-essentials}

社區組功能是子社區在社區站點內由來自發佈和作者環境的授權用戶動態建立的能力。

截至社區 [功能包1](deploy-communities.md#latestfeaturepack)，組可能嵌套在其他組中

## 客戶端基本知識 {#essentials-for-client-side}

### 社區組成員清單 {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td>社會/組/元件/hbs/社區組成員清單</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>客戶端</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參閱 <a href="creating-groups.md">社區組</a></td>
  </tr>
 </tbody>
</table>

### 社群群組 {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td>社會/群體/構成部分/hbs/社區群體</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>客戶端</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [客戶端自定義](client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [社區組API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [社區組終結點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [伺服器端自定義](server-customize.md)

### 組函式 {#groups-function}

包括一個 [組函式](functions.md#groups-function) 將支援建立 `community groups` 出版和作者環境。 建立的社區組將包括 `community groups member list` 列出組成員的元件。

一個或多個 [社區組模板](tools-groups.md)當將該函式添加到 [社區網站模板](sites.md) 或嵌套在社區組模板中。

包含多個社區組模板導致在為社區站點建立新社區組時向授權用戶呈現一種設計選擇，如上一節所示 [社區組](creating-groups.md) 作者。

### 嵌套組 {#nested-groups}

截至社區 [FP1](deploy-communities.md#latestfeaturepack)，組函式可能包含在組模板中，從而允許嵌套組（子社區）。

當社區站點或組模板包含「組」功能時，可以執行以下操作：

* 在作者環境中建立子社區。

* 在配置為允許時，在發佈環境中建立組。

在作者環境中建立組時，需要先發佈社區網站，然後發佈組。 發佈社區網站將發佈組的頁面，而不會建立ACL設定到的子社區成員組。 因此，在明確發佈組之前，可以看到受限（秘密）組。

## 連結和相關資訊 {#links-and-related-information}

* [管理用戶和用戶組](users.md)
* [社區組控制台](groups.md)
* [組函式](functions.md#groups-function)
* [群組範本](tools-groups.md)
