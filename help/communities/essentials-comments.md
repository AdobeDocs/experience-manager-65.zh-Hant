---
title: Comments Essentials
description: 瞭解如何使用評論系統（評論元件）和管理社群成員貼文中使用者產生的內容(UGC)。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 3%

---

# Comments Essentials {#comments-essentials}

此頁面提供使用註解系統（註解元件）的基礎知識，以及管理成員張貼註解或回覆時產生的使用者產生內容(UGC)的選項。

註解元件建立註解系統，讓每個個別貼文都由註解元件（單數）表示。 它是包含在頁面上的註解系統。 呼叫註解時，註解系統會建立個別註解。

## 使用者端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>是 — 屬性可在以下位置編輯： <i>設計 </i>模式</td>
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
   <td> 另請參閱 <a href="comments.md">使用註解</a></td>
  </tr>
 </tbody>
</table>

[使用者端自訂](client-customize.md)

### 每頁一個執行處理 {#one-instance-per-page}

分頁及使用URL來快取和連結要求每個註解系統的URL必須是唯一的。 因此，每個頁面只允許一個註解系統例項。

其他功能已經包括註解系統。 說明如下：

* [部落格](blog-developer-basics.md)
* [日曆](calendar-basics-for-developers.md)
* [檔案庫](essentials-file-library.md)
* [論壇](essentials-forum.md)
* [QnA](qna-essentials.md)
* [評論](reviews-basics.md)

### 標幟原因清單 {#flag-reason-list}

您可以在應用程式中新增flagreasonlist.hbs以覆寫中的內容，進而自訂標幟原因清單

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

這適用於任何延伸註解系統的元件。

## 伺服器端的Essentials {#essentials-for-server-side}

* [註解API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [評論端點](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取發表的評論(UGC) {#accessing-posted-comments-ugc}

UGC應使用其中一種標準仲裁方法進行仲裁。
另請參閱 [稽核使用者產生的內容](moderate-ugc.md).

自AEM 6.1社群起，使用 [公用存放區](working-with-srp.md) for UGC包含對UGC的程式化存取，無論選擇的儲存選項（例如ASRP、MSRP或JSRP）為何。

**UGC在存放庫中的位置和格式可能會有所變更，恕不另行警告**.

請參閱：

* [儲存資源提供者概觀](srp.md)  — 簡介和存放庫使用概述。
* [srp和UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 程式碼指南。
* [SocialUtils重構](socialutils.md)  — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。
