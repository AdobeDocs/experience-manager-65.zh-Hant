---
title: 評論要點
seo-title: 評論要點
description: 審核和審核摘要元件
seo-description: 審核和審核摘要元件
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 1%

---

# 查看Essentials {#reviews-essentials}

此功能包含兩個可搭配運作的元件：審核和審核摘要。

評論是基於[注釋系統](essentials-comments.md)的複合元件，該系統包含一個或多個[rating](rating-basics.md)（計數）元件。

不支援匿名發佈審核。 網站訪客必須註冊並登入才能新增審核。 已登入的訪客（成員）可隨時更新其審核。

## 客戶端{#essentials-for-client-side}的要點

### 評論 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/reviews/components/hbs/reviews</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包括</strong></a></td>
   <td>是 — 可在<i>design </i>模式中編輯屬性</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs&lt;a2/ /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs<br /></td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參閱<a href="reviews.md">使用評論</a></td>
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
| **屬性** | 請參閱[使用評論](reviews.md) |

* [用戶端自訂](client-customize.md)

## 伺服器端{#essentials-for-server-side}的要點

* [審核API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [檢閱端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 訪問已發佈的評論(UGC){#accessing-posted-reviews-ugc}

UGC應使用其中一種標準的協調方法來協調。
請參閱[協調使用者產生的內容](moderate-ugc.md)。

自AEM 6.1社群起，UGC使用[公用商店](working-with-srp.md)包括程式化存取UGC，而不論選擇的儲存選項（例如ASRP、MSRP或JSRP）。

**UGC在存放庫中的位置和格式可能會變更，恕不另行警告**。

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將棄用的公用程式方法對應至目前的SRP公用程式方法。
