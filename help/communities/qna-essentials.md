---
title: QnA軟體包
seo-title: QnA Essentials
description: 問答論壇功能
seo-description: Questions and answers forum feature
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---

# QnA軟體包 {#qna-essentials}

此頁提供了使用問題和答案(QnA)論壇功能的基本資訊。

## 客戶端基本知識 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> 資源類型</td>
   <td>社交/qna/元件/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">包含</a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">客戶端</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs投票<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> 模板</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> cs</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> 屬性</td>
   <td>請參閱 <a href="working-with-qna.md">問答論壇功能</a></td>
  </tr>
 </tbody>
</table>

* [客戶端自定義](client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [QnA API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [QnA端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [伺服器端自定義](server-customize.md)

### QnA 功能 {#qna-function}

包含該社區站點結構的 [QnA函式](functions.md#qna-function) 將配置 `QnA` 元件以及影響審核和標籤的設定。 QnA函式支援標識 [特權成員用戶組](users.md#privileged-members-group)。

### 訪問QnA論壇帖子(UGC) {#accessing-qna-forum-posts-ugc}

UGC應使用一種標準的審核方法來審核。
請參閱 [調節用戶生成的內容](moderate-ugc.md)。

截至AEM6.1社區，使用 [普通商店](working-with-srp.md) UGC包括對UGC的寫程式訪問，而不考慮選擇的儲存選項（如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會發生更改，但不會發出警告**。

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [SRP和UGC軟體包](srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將不建議使用的實用程式方法映射到當前SRP實用程式方法。
