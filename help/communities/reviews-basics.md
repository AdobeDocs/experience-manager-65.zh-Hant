---
title: 評論要點
seo-title: Reviews Essentials
description: 審核和審核摘要元件
seo-description: Reviews and Review Summary components
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 1%

---

# 評論要點 {#reviews-essentials}

此功能包含兩個可搭配運作的元件：審核和審核摘要。

審核是以 [註解系統](essentials-comments.md) 包含一或多個 [評分](rating-basics.md) （計數）元件。

不支援匿名發佈審核。 網站訪客必須註冊並登入才能新增審核。 已登入的訪客（成員）可隨時更新其審核。

## 用戶端的要點 {#essentials-for-client-side}

### 評論 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/reviews/components/hbs/reviews</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包括</strong></a></td>
   <td>是 — 可在中編輯屬性 <i>設計 </i>模式</td>
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
   <td> <strong>cs</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參閱 <a href="reviews.md">使用審核</a></td>
  </tr>
 </tbody>
</table>

### 審核摘要 {#review-summary}

| **resourceType** | social/reviews/components/hbs/summary |
|---|---|
| [**包括**](scf.md#add-or-include-a-communities-component) | 是 — 可在*design *模式中編輯屬性 |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **範本** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **cs** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **屬性** | 請參閱 [使用審核](reviews.md) |

* [用戶端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [審核API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [檢閱端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 訪問發佈的評論(UGC) {#accessing-posted-reviews-ugc}

UGC應使用其中一種標準的協調方法來協調。
請參閱 [協調使用者產生的內容](moderate-ugc.md).

自AEM 6.1社群起，請使用 [公用商店](working-with-srp.md) 針對UGC包括可程式化地存取UGC，而無論選擇的儲存選項（例如ASRP、MSRP或JSRP）。

**UGC在存放庫中的位置和格式可能會變更，恕不另行警告**.

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和存放庫使用概觀。
* [SRP和UGC要點](srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將棄用的公用程式方法對應至目前的SRP公用程式方法。
