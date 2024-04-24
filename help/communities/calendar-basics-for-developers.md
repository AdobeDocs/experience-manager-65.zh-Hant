---
title: 行事曆要點
description: 瞭解如何在Experience Manager社群中使用行事曆功能。 「行事曆」支援識別有特殊許可權的成員使用者群組。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 069e379d-c6fd-49ca-b337-df6fd466e023
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 2%

---

# 行事曆要點 {#calendar-essentials}

本頁提供有關使用行事曆功能的重要資訊。

## 使用者端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/calendar/components/hbs/calendar</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
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
   <td> <strong>css</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>另請參閱 <a href="calendar.md">使用行事曆</a></td>
  </tr>
 </tbody>
</table>

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [行事曆API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [行事曆端點](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 日曆功能 {#calendar-function}

社群網站結構包含 [行事曆功能](functions.md#calendar-function) 具有 `calendar` 元件已設定。 「行事曆」功能支援識別 [有特殊許可權的成員使用者群組](users.md#privileged-members-group).

### 存取行事曆文章(UGC) {#accessing-calendar-posts-ugc}

自AEM 6.1社群起，使用 [公用存放區](working-with-srp.md) for UGC包含對UGC的程式化存取，無論選擇的儲存選項（例如ASRP、MSRP或JSRP）為何。

**UGC在存放庫中的位置和格式可能會有所變更，恕不另行警告**.

請參閱：

* [儲存資源提供者概觀](srp.md)  — 簡介和存放庫使用概述
* [srp和UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 程式碼指南
* [SocialUtils重構](socialutils.md)  — 將已棄用的公用程式方法對應到目前的SRP公用程式方法
