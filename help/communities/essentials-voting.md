---
title: Potting Essentials
seo-title: Potting Essentials
description: 投票元件概觀
seo-description: 投票元件概觀
uuid: ed0a771d-1c14-4fbf-ab6a-a028e5ee2e2a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 1a947a06-6a5c-4be9-b2fa-e5fa809ff3b8
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# 投票基本工具{#voting-essentials}

投票元件[tally](tally.md)子類是一種有用的工具，它允許成員通過選擇向上或向下箭頭來表示其意見來對特定內容評分。

允許在同一頁放置多個投票元件實例；每個實例都必須配置有唯一的`tally name`屬性。

不支援匿名張貼投票。 網站訪客必須註冊並登入才能參與投票一次，登入的訪客（會員）可隨時變更投票。

## 客戶端{#essentials-for-client-side}的基本功能

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/potting</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>included</strong></a></td>
   <td>是——在<i>design </i>模式中可編輯屬性</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
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
   <td><p>請參閱<a href="voting.md">使用投票</a></p> </td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](client-customize.md)

## 伺服器端{#essentials-for-server-side}的基本工具

* [計數API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [計數端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取已張貼的投票(UGC){#accessing-posted-voting-ugc}

UGC應使用其中一種標準的協調方法來協調。
請參閱[協調使用者產生的內容](moderate-ugc.md)。

自AEM 6.1 Communities起，使用[通用商店](working-with-srp.md)做為UGC，不論選擇的儲存選項（例如ASRP、MSRP或JSRP），都可程式化存取UGC。

**UGC在儲存庫中的位置和格式可能會變更，但不會發出警告**。

請參閱：

* [儲存資源提供方概述](srp.md) -簡介和儲存庫使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP實用程式方法和示例。
* [使用SRP](accessing-ugc-with-srp.md) -編碼准則存取UGC。
* [SocialUtils重構](socialutils.md) -將淘汰的公用程式方法對應至目前的SRP公用程式方法。

