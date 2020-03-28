---
title: Comments Essentials
seo-title: Comments Essentials
description: Comments元件概觀
seo-description: Comments元件概觀
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Comments Essentials {#comments-essentials}

本頁提供了使用注釋系統（注釋元件）的基本要點，以及管理成員張貼注釋或回覆時產生的用戶生成內容(UGC)的選項。

該注釋元件建立注釋系統，使得每個單獨的帖子由注釋元件（單數）表示。 它是包含在頁面上的注釋系統。 注釋系統會在呼叫時建立個別注釋。

## 用戶端基本功能 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>included</strong></a></td>
   <td>是——可在設計模式中編輯 <i>屬 </i>性</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.porting</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td> 請參閱 <a href="comments.md">使用注釋</a></td>
  </tr>
 </tbody>
</table>

[用戶端自訂](client-customize.md)

### 每頁一個例項 {#one-instance-per-page}

分頁和使用URL進行快取和連結需要URL在每個留言系統中都是唯一的。 因此，每頁僅允許一個注釋系統實例。

其他功能已包括註解系統。 以下是：

* [部落格](blog-developer-basics.md)
* [日曆](calendar-basics-for-developers.md)
* [檔案庫](essentials-file-library.md)
* [論壇](essentials-forum.md)
* [QnA](qna-essentials.md)
* [評論](reviews-basics.md)

### 標籤原因清單 {#flag-reason-list}

您可自訂標籤原因清單，方法是將flagreasonlist.hbs新增至應用程式以覆寫

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

這適用於擴充注釋系統的任何元件。

## 伺服器端的基本功能 {#essentials-for-server-side}

* [注釋API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [注釋端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取已張貼的留言(UGC) {#accessing-posted-comments-ugc}

UGC應使用其中一種標準的協調方法來協調。
請參 [閱協調使用者產生的內容](moderate-ugc.md)。

自AEM 6.1 Communities起，使用UGC的 [公用商店](working-with-srp.md) ，包括程式化存取UGC，不論選擇的儲存選項（例如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會變更，但不會發出警告**。

請參閱：

* [儲存資源提供方概述](srp.md) -簡介和儲存庫使用概述
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP實用程式方法和示例
* [使用SRP存取UGC](accessing-ugc-with-srp.md) —— 編碼准則
* [SocialUtils重構](socialutils.md) -將不建議使用的公用程式方法對應至目前的SRP公用程式方法

