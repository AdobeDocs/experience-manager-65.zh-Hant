---
title: 論壇要點
description: 瞭解在Adobe Experience Manager社群中使用論壇功能的基礎知識。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 622cf6ca-f119-4310-ad14-537576bd6f6d
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# 論壇要點 {#forum-essentials}

本頁提供使用論壇功能的基本資訊。

## 使用者端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/forum/components/hbs/forum<br /> social/forum/components/hbs/topic<br /> social/forum/components/hbs/post</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.forum</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/forum/components/hbs/forum/forum.hbs<br /> /libs/social/forum/components/hbs/post/post.hbs<br /> /libs/social/forum/components/hbs/topic/topic.hbs<br /> /libs/social/forum/components/hbs/topic/list-item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/forum/components/hbs/forum/clientlibs/forum.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>另請參閱 <a href="forum.md">論壇功能</a></td>
  </tr>
 </tbody>
</table>

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [論壇API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [論壇端點](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 論壇功能 {#forum-function}

社群網站結構包含 [論壇功能](functions.md#forum-function)，包括已設定的 `forum` 影響稽核、標籤和翻譯的元件和設定。

### 存取論壇貼文(UGC) {#accessing-forum-posts-ugc}

UGC應使用其中一種標準仲裁方法進行仲裁。
另請參閱 [稽核使用者產生的內容](moderate-ugc.md).

截至Adobe Experience Manager 6.1社群，使用 [公用存放區](working-with-srp.md) for UGC包含對UGC的程式化存取，無論選擇的儲存選項（例如ASRP、MSRP或JSRP）為何。

**UGC在存放庫中的位置和格式可能會有所變更，恕不另行警告**.

請參閱：

* [儲存資源提供者概觀](srp.md)  — 簡介和存放庫使用概述。
* [srp和UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 程式碼指南。
* [SocialUtils重構](socialutils.md)  — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。
