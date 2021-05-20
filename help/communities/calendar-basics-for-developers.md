---
title: 日曆要點
seo-title: 日曆要點
description: 日曆功能概觀
seo-description: 日曆功能概觀
uuid: 14ff7a83-b2a7-4f7e-8ee7-88f336329a1a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 88932a3c-ba7f-47ba-9e0b-206755c2d42e
exl-id: 069e379d-c6fd-49ca-b337-df6fd466e023
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---

# 日曆要點{#calendar-essentials}

本頁面提供使用日曆功能的基本資訊。

## 客戶端{#essentials-for-client-side}的要點

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/calendar/components/hbs/calendar</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包括</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td>
   <td> </td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱<a href="calendar.md">使用日曆</a></td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](client-customize.md)

## 伺服器端{#essentials-for-server-side}的要點

* [日曆API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [日曆端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 日曆功能 {#calendar-function}

包含[日曆函式](functions.md#calendar-function)的社區站點結構將具有配置的`calendar`元件。 日曆功能支援標識[特權成員用戶組](users.md#privileged-members-group)。

### 存取日曆貼文(UGC){#accessing-calendar-posts-ugc}

自AEM 6.1社群起，UGC使用[公用商店](working-with-srp.md)包括程式化存取UGC，而不論選擇的儲存選項（例如ASRP、MSRP或JSRP）。

**UGC在存放庫中的位置和格式可能會變更，恕不另行警告**。

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP公用程式方法與範例
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 編碼准則
* [SocialUtils重構](socialutils.md)  — 將棄用的公用程式方法對應至目前的SRP公用程式方法
