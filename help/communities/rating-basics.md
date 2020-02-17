---
title: Rating Essentials
seo-title: Rating Essentials
description: 分級元件概觀
seo-description: 分級元件概觀
uuid: 48ef61ad-be7a-4a6b-a284-23e5bb4f1671
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7dc3ef57-05c3-45d4-ace3-bb3ba6ea768b
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Rating Essentials {#rating-essentials}

評等元件是計 [分子類](tally.md) ，可讓登入社群成員對網站上的功能評分。

允許在同一頁放置多個投票元件實例；每個實例都必須配置一個唯一 `tally name` 屬性。

不支援匿名張貼評分。 網站訪客必須註冊並登入，才能只參與一次評分。 已登入的訪客（會員）隨時可能變更其評分。

## 用戶端基本功能 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/tally/components/hbs/rating</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>included</strong></a></td>
   <td>是——可在設計模式中編輯 <i>屬 </i>性</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.rating</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td><p> /libs/social/tally/components/hbs/rating/rating.hbs<br /> /libs/social/tally/components/hbs/rating/display.hbs<br /> /libs/social/tally/components/hbs/rating/histogram.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/rating/clientlibs/ratingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td><p>請參 <a href="rating.md">閱使用分級</a></p> </td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](client-customize.md)

## 伺服器端的基本功能 {#essentials-for-server-side}

* [計數API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [計數端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取已張貼的評分(UGC) {#accessing-posted-ratings-ugc}

UGC應使用其中一種標準的協調方法來協調。
請參 [閱協調使用者產生的內容](moderate-ugc.md)。

自AEM 6.1 Communities起，使用UGC的 [公用商店](working-with-srp.md) ，包括程式化存取UGC，不論選擇的儲存選項（例如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會變更，但不會發出警告**。

請參閱：

* [儲存資源提供方概述](srp.md) -簡介和儲存庫使用概述
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP實用程式方法和示例
* [使用SRP存取UGC](accessing-ugc-with-srp.md) —— 編碼准則
* [SocialUtils重構](socialutils.md) -將不建議使用的公用程式方法對應至目前的SRP公用程式方法

