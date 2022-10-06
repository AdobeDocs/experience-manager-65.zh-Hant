---
title: 注釋要點
seo-title: Comments Essentials
description: 註解元件概觀
seo-description: Comments component overview
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 3%

---

# 注釋要點 {#comments-essentials}

本頁提供了使用注釋系統（注釋元件）的要點，以及管理成員發佈注釋或答復時生成的用戶生成內容(UGC)的選項。

評論部件建立評論系統，使得每個單獨的帖子由評論部件（單數）表示。 頁面上包含的註解系統。 注釋系統將在調用時建立各個注釋。

## 用戶端的要點 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包括</strong></a></td>
   <td>是 — 可在中編輯屬性 <i>設計 </i>模式</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
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

分頁和使用URL來快取和連結時，每個註解系統的URL必須是唯一的。 因此，每頁僅允許一個注釋系統例項。

其他功能已包括注釋系統。 說明如下：

* [部落格](blog-developer-basics.md)
* [日曆](calendar-basics-for-developers.md)
* [檔案庫](essentials-file-library.md)
* [論壇](essentials-forum.md)
* [QnA](qna-essentials.md)
* [評論](reviews-basics.md)

### 標誌原因清單 {#flag-reason-list}

您可將flagreasonlist.hbs新增至應用程式以覆寫中的內容，以自訂標幟原因清單

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

這適用於擴充註解系統的任何元件。

## 伺服器端的Essentials {#essentials-for-server-side}

* [注釋API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [注釋端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取已張貼的留言(UGC) {#accessing-posted-comments-ugc}

UGC應使用其中一種標準的協調方法來協調。
請參閱 [協調使用者產生的內容](moderate-ugc.md).

自AEM 6.1社群起，請使用 [公用商店](working-with-srp.md) 針對UGC包括可程式化地存取UGC，而無論選擇的儲存選項（例如ASRP、MSRP或JSRP）。

**UGC在存放庫中的位置和格式可能會變更，恕不另行警告**.

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和存放庫使用概觀。
* [SRP和UGC要點](srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將棄用的公用程式方法對應至目前的SRP公用程式方法。
