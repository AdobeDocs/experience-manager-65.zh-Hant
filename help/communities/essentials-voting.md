---
title: Voting Essentials
description: 瞭解如何使用投票元件，透過選取向上或向下箭頭來指示成員意見，讓成員可對特定內容片段進行評分。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e8ff751f-404a-498d-8e90-62a13ab593ff
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# Voting Essentials {#voting-essentials}

投票元件（一個[總計](tally.md)子類別）是一種有用的工具，可讓成員只要選取向上或向下箭頭來表示其意見，即可對特定內容進行評等。

允許將投票元件的多個執行個體放在相同頁面上；每個執行個體都必須設定唯一的`tally name`屬性。

不支援匿名張貼投票。 網站訪客必須註冊並登入才能參與投票一次。 登入的訪客（會員）可隨時變更投票。

## 使用者端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/voting</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>是 — 屬性可在<i>設計</i>模式中編輯</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td><p>檢視<a href="voting.md">使用投票</a></p> </td>
  </tr>
 </tbody>
</table>

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [總計API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [計數的端點](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取已張貼的投票(UGC) {#accessing-posted-voting-ugc}

UGC應使用其中一種標準仲裁方法進行仲裁。
請參閱[仲裁使用者產生的內容](moderate-ugc.md)。

截至AEM 6.1 Communities，使用UGC的[公用存放區](working-with-srp.md)時，無論選擇的存放區選項（例如ASRP、MSRP或JSRP）為何，都可程式化存取UGC。

**存放庫中UGC的位置和格式可能會變更，而不會出現警告**。

請參閱：

* [儲存資源提供者概觀](srp.md) — 簡介和存放庫使用概觀。
* [SRP與UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md) — 編碼准則。
* [SocialUtils重構](socialutils.md) — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。
