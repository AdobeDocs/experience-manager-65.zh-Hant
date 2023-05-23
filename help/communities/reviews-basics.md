---
title: 審閱基本內容
seo-title: Reviews Essentials
description: 審閱和審閱摘要元件
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

# 審閱基本內容 {#reviews-essentials}

此功能由兩個可協同工作的元件組成：審閱和審閱摘要。

審閱是基於 [注釋系統](essentials-comments.md) 包含一個或多個 [評級](rating-basics.md) （計數）元件。

不支援匿名發佈審閱。 站點訪問者必須註冊並登錄以添加審閱。 已簽署的訪問者（成員）可隨時更新其審查。

## 客戶端基本知識 {#essentials-for-client-side}

### 評論 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td>社交/評論/元件/hbs/評論</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>是 — 屬性可在 <i>設計 </i>模式</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>客戶端</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參閱 <a href="reviews.md">使用審閱</a></td>
  </tr>
 </tbody>
</table>

### 審核摘要 {#review-summary}

| **資源類型** | 社交/評論/元件/hbs/摘要 |
|---|---|
| [**包含**](scf.md#add-or-include-a-communities-component) | 是 — 屬性在*design *模式下可編輯 |
| [**客戶端**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **模板** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **cs** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **屬性** | 請參閱 [使用審閱](reviews.md) |

* [客戶端自定義](client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [查看API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [查看終結點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [伺服器端自定義](server-customize.md)

### 訪問已過帳的審閱(UGC) {#accessing-posted-reviews-ugc}

UGC應使用一種標準的審核方法來審核。
請參閱 [調節用戶生成的內容](moderate-ugc.md)。

截至AEM6.1社區，使用 [普通商店](working-with-srp.md) UGC包括對UGC的寫程式訪問，而不考慮選擇的儲存選項（如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會發生更改，但不會發出警告**。

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [SRP和UGC軟體包](srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將過時的實用程式方法映射到當前SRP實用程式方法。
