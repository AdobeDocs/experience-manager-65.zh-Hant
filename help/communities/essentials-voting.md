---
title: 投票要點
seo-title: Voting Essentials
description: 投票元件概述
seo-description: Voting component overview
uuid: ed0a771d-1c14-4fbf-ab6a-a028e5ee2e2a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 1a947a06-6a5c-4be9-b2fa-e5fa809ff3b8
exl-id: e8ff751f-404a-498d-8e90-62a13ab593ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# 投票要點 {#voting-essentials}

投票部分， [理](tally.md) 子類是一種有用的工具，它允許成員通過僅選擇向上或向下箭頭來指示其意見來對特定內容進行評級。

允許將投票元件的多個實例放置在同一頁上；每個實例都必須配置為唯一 `tally name` 屬性。

不支援匿名投票。 網站訪問者必須註冊登記一次才能參加投票，已簽名的訪客（會員）可以隨時更改投票。

## 客戶端基本知識 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td>社會/統計/構成部分/hbs/投票</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>是 — 屬性可在 <i>設計 </i>模式</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>客戶端</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td><p>請參閱 <a href="voting.md">使用投票</a></p> </td>
  </tr>
 </tbody>
</table>

* [客戶端自定義](client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [計數API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [計數端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [伺服器端自定義](server-customize.md)

### 訪問已過帳投票(UGC) {#accessing-posted-voting-ugc}

UGC應使用一種標準的審核方法來審核。
請參閱 [調節用戶生成的內容](moderate-ugc.md)。

截至AEM6.1社區，使用 [普通商店](working-with-srp.md) UGC包括對UGC的寫程式訪問，而不考慮選擇的儲存選項（如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會發生更改，但不會發出警告**。

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [SRP和UGC軟體包](srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將不建議使用的實用程式方法映射到當前SRP實用程式方法。
