---
title: 注釋要點
seo-title: Comments Essentials
description: 注釋元件概述
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

此頁提供使用注釋系統（注釋元件）的基本內容以及管理成員發佈注釋或答復時生成的用戶生成內容(UGC)的選項。

注釋元件建立注釋系統，使得每個單獨的帖子由注釋元件（單數）表示。 它是包含在頁面上的注釋系統。 注釋系統將在調用時建立單個注釋。

## 客戶端基本知識 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td> 社交/公共/元件/hbs/評論</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>是 — 屬性可在 <i>設計 </i>模式</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>客戶端</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs投票</td>
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

[客戶端自定義](client-customize.md)

### 每頁一個實例 {#one-instance-per-page}

分頁和使用URL進行快取和連結要求每個注釋系統的URL是唯一的。 因此，每頁只允許一個注釋系統實例。

其他功能已包括注釋系統。 說明如下：

* [部落格](blog-developer-basics.md)
* [日曆](calendar-basics-for-developers.md)
* [檔案庫](essentials-file-library.md)
* [論壇](essentials-forum.md)
* [QnA](qna-essentials.md)
* [評論](reviews-basics.md)

### 標誌原因清單 {#flag-reason-list}

可以通過將flagreasonlist.hbs添加到應用來自定義標籤的原因清單，以覆蓋中的內容

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

這適用於擴展注釋系統的任何元件。

## 伺服器端軟體包 {#essentials-for-server-side}

* [注釋API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [注釋終結點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [伺服器端自定義](server-customize.md)

### 訪問已發佈的注釋(UGC) {#accessing-posted-comments-ugc}

UGC應使用一種標準的審核方法來審核。
請參閱 [調節用戶生成的內容](moderate-ugc.md)。

截至AEM6.1社區，使用 [普通商店](working-with-srp.md) UGC包括對UGC的寫程式訪問，而不考慮選擇的儲存選項（如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會發生更改，但不會發出警告**。

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [SRP和UGC軟體包](srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將過時的實用程式方法映射到當前SRP實用程式方法。
