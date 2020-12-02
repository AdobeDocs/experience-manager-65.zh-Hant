---
title: Calendar Essentials
seo-title: Calendar Essentials
description: 日曆功能概觀
seo-description: 日曆功能概觀
uuid: 14ff7a83-b2a7-4f7e-8ee7-88f336329a1a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 88932a3c-ba7f-47ba-9e0b-206755c2d42e
translation-type: tm+mt
source-git-commit: 82affd528f2526384b319fe89082e0f574ab5855
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---


# 日曆基本功能{#calendar-essentials}

本頁提供使用日曆功能的基本資訊。

## 客戶端{#essentials-for-client-side}的基本功能

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/calendar/components/hbs/calendar</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>included</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td>
   <td> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱<a href="calendar.md">使用日曆</a></td>
  </tr>
 </tbody>
</table>

* [用戶端自訂](client-customize.md)

## 伺服器端{#essentials-for-server-side}的基本工具

* [日曆API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [日曆端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 日曆功能 {#calendar-function}

包含[Calendar函式](functions.md#calendar-function)的社群網站結構將具有已配置的`calendar`元件。 Calendar函式支援標識[特權成員用戶組](users.md#privileged-members-group)。

### 存取日曆貼文(UGC){#accessing-calendar-posts-ugc}

自AEM 6.1 Communities起，使用[通用商店](working-with-srp.md)做為UGC，不論選擇的儲存選項（例如ASRP、MSRP或JSRP），都可程式化存取UGC。

**UGC在儲存庫中的位置和格式可能會變更，但不會發出警告**。

請參閱：

* [儲存資源提供方概述](srp.md) -簡介和儲存庫使用概述
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP實用程式方法和示例
* [使用SRP](accessing-ugc-with-srp.md) -編碼准則存取UGC
* [SocialUtils重構](socialutils.md) -將淘汰的公用程式方法對應至目前的SRP公用程式方法

