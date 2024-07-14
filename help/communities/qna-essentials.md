---
title: QnA要點
description: 瞭解在Adobe Experience Manager社群中使用問答(QnA)論壇功能的基礎知識。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%

---

# QnA要點 {#qna-essentials}

本頁提供使用問答(QnA)論壇功能的基本資訊。

## 使用者端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">包含</a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientllibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> 範本</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> 屬性</td>
   <td>檢視<a href="working-with-qna.md">問答論壇功能</a></td>
  </tr>
 </tbody>
</table>

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [QnA API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [QnA端點](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### QnA 功能 {#qna-function}

包含[QnA函式](functions.md#qna-function)的社群網站結構有已設定的`QnA`元件，以及影響仲裁和標籤的設定。 QnA函式支援識別[有特殊許可權的成員使用者群組](users.md#privileged-members-group)。

### 存取QnA論壇貼文(UGC) {#accessing-qna-forum-posts-ugc}

UGC應使用其中一種標準仲裁方法進行仲裁。
請參閱[仲裁使用者產生的內容](moderate-ugc.md)。

截至AEM 6.1 Communities，使用UGC的[公用存放區](working-with-srp.md)時，無論選擇的存放區選項（例如ASRP、MSRP或JSRP）為何，都可程式化存取UGC。

**存放庫中UGC的位置和格式可能會變更，而不會出現警告**。

請參閱：

* [儲存資源提供者概觀](srp.md) — 簡介和存放庫使用概觀。
* [SRP與UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md) — 編碼准則。
* [SocialUtils重構](socialutils.md) — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。
