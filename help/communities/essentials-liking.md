---
title: 喜歡基本功能
seo-title: Liking Essentials
description: 喜歡元件概述
seo-description: Liking component overview
uuid: 89f16859-c901-4090-8e16-363b95c508de
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f176c42b-b16b-42c9-af22-4b6421de5a90
pagetitle: Liking Essentials
exl-id: ef314385-cd5c-411c-91df-83691a81c1bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# 喜歡基本功能 {#liking-essentials}

喜歡元件， [理](tally.md) 子類是一種有用的工具，它允許成員通過簡單選擇心臟表徵圖來表達對特定內容的積極意見。

允許在同一頁面上放置多個喜歡元件實例；每個實例都必須配置為唯一 `tally name` 屬性。

不支援匿名發佈類似。 站點訪問者必須註冊並登錄以參與喜歡。 已登錄的訪問者（成員）可隨時進行類似開啟和關閉。

## 客戶端基本知識 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td>社交/統計/元件/hbs/喜歡</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>是 — 屬性可在 <i>設計 </i>模式</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>客戶端</strong></a></td>
   <td> cq.social.hbs.liking</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td><p> /libs/social/tally/components/hbs/liking/liking.hbs<br /> /libs/social/tally/components/hbs/liking/activity-icon.hbs<br /> /libs/social/tally/components/hbs/liking/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/liking/clientlibs/likingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td><p>請參閱 <a href="liking.md">使用喜歡</a></p> </td>
  </tr>
 </tbody>
</table>

* [客戶端自定義](client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [計數API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [計數端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [伺服器端自定義](server-customize.md)

### 訪問已過帳投票(UGC) {#accessing-posted-voting-ugc}

UGC應使用一種標準的審核方法來審核。
請參閱 [調節用戶生成的內容](moderate-ugc.md)。

截至AEM6.1社區，使用 [普通商店](working-with-srp.md) UGC包括對UGC的寫程式訪問，而不考慮選擇的儲存選項（如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會發生更改，但不會發出警告**。

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [SRP和UGC軟體包](srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將不建議使用的實用程式方法映射到當前SRP實用程式方法。
