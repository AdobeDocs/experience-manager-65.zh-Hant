---
title: 稽核Essentials
description: 瞭解AEM Communities中的評論如何成為以包含一或多個評等（計分）元件的評論系統為基礎的複合元件。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---

# 稽核Essentials {#reviews-essentials}

此功能包含兩個共同運作的元件：稽核和稽核摘要。

評論是以[評論系統](essentials-comments.md)為基礎的複合元件，包含一或多個[評等](rating-basics.md) （計分）元件。

不支援評論的匿名張貼。 網站訪客必須註冊並登入才能新增評論。 登入的訪客（成員）可隨時更新其評論。

## 使用者端的Essentials {#essentials-for-client-side}

### 評論 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/reviews/components/hbs/reviews</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>是 — 屬性可在<i>設計</i>模式中編輯</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>檢視<a href="reviews.md">使用評論</a></td>
  </tr>
 </tbody>
</table>

### 審核摘要 {#review-summary}

| **resourceType** | social/reviews/components/hbs/summary |
|---|---|
| [**包含**](scf.md#add-or-include-a-communities-component) | 是 — 屬性可在*design*模式中編輯 |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **範本** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **屬性** | 檢視[使用評論](reviews.md) |

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [檢閱API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [檢閱端點](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取已張貼的評論(UGC) {#accessing-posted-reviews-ugc}

UGC應使用其中一種標準仲裁方法進行仲裁。
請參閱[仲裁使用者產生的內容](moderate-ugc.md)。

截至AEM 6.1 Communities，使用UGC的[公用存放區](working-with-srp.md)時，無論選擇的存放區選項（例如ASRP、MSRP或JSRP）為何，都可程式化存取UGC。

**存放庫中UGC的位置和格式可能會變更，而不會出現警告**。

請參閱：

* [儲存資源提供者概觀](srp.md) — 簡介和存放庫使用概觀。
* [SRP與UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md) — 編碼准則。
* [SocialUtils重構](socialutils.md) — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。
