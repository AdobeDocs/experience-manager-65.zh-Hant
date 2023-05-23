---
title: 日曆要件
seo-title: Calendar Essentials
description: 日曆功能概述
seo-description: Calendar feature overview
uuid: 14ff7a83-b2a7-4f7e-8ee7-88f336329a1a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 88932a3c-ba7f-47ba-9e0b-206755c2d42e
exl-id: 069e379d-c6fd-49ca-b337-df6fd466e023
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 2%

---

# 日曆要件 {#calendar-essentials}

此頁提供有關使用日曆功能的基本資訊。

## 客戶端基本知識 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td>社交/日曆/元件/hbs/日曆</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>客戶端</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td>
   <td> </td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>見 <a href="calendar.md">使用日曆</a></td>
  </tr>
 </tbody>
</table>

* [客戶端自定義](client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [日曆API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [日曆終結點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [伺服器端自定義](server-customize.md)

### 日曆功能 {#calendar-function}

包含該社區站點結構的 [日曆函式](functions.md#calendar-function) 將配置 `calendar` 元件。 Calendar函式支援標識 [特權成員用戶組](users.md#privileged-members-group)。

### 訪問日曆帖子(UGC) {#accessing-calendar-posts-ugc}

截至AEM6.1社區，使用 [普通商店](working-with-srp.md) UGC包括對UGC的寫程式訪問，而不考慮選擇的儲存選項（如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會發生更改，但不會發出警告**。

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述
* [SRP和UGC軟體包](srp-and-ugc.md) - SRP實用程式方法和示例
* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 編碼准則
* [SocialUtils重構](socialutils.md)  — 將過時的實用程式方法映射到當前SRP實用程式方法
