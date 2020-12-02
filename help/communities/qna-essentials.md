---
title: QnA Essentials
seo-title: QnA Essentials
description: 問答論壇功能
seo-description: 問答論壇功能
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
translation-type: tm+mt
source-git-commit: ca15258a5dc7ca99b6c9d6ae85e42c77a3802c87
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---


# QnA Essentials {#qna-essentials}

本頁提供使用問題和答案(QnA)論壇功能的基本資訊。

## 客戶端{#essentials-for-client-side}的基本功能

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">included</a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientlibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.porting<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> 模板</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> 屬性</td>
   <td>請參閱<a href="working-with-qna.md">問答論壇功能</a></td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](client-customize.md)

## 伺服器端{#essentials-for-server-side}的基本工具

* [QnA API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [QnA端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### QnA 功能 {#qna-function}

包含[QnA函式](functions.md#qna-function)的社群網站結構將具有已配置的`QnA`元件以及影響協調和標籤的設定。 QnA函式支援標識[特權成員用戶組](users.md#privileged-members-group)。

### 訪問QnA論壇帖子(UGC){#accessing-qna-forum-posts-ugc}

UGC應使用其中一種標準的協調方法來協調。
請參閱[協調使用者產生的內容](moderate-ugc.md)。

自AEM 6.1 Communities起，使用[通用商店](working-with-srp.md)做為UGC，不論選擇的儲存選項（例如ASRP、MSRP或JSRP），都可程式化存取UGC。

**UGC在儲存庫中的位置和格式可能會變更，但不會發出警告**。

請參閱：

* [儲存資源提供方概述](srp.md) -簡介和儲存庫使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP實用程式方法和示例。
* [使用SRP](accessing-ugc-with-srp.md) -編碼准則存取UGC。
* [SocialUtils重構](socialutils.md) -將淘汰的公用程式方法對應至目前的SRP公用程式方法。

