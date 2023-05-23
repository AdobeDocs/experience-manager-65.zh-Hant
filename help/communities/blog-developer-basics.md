---
title: 部落格要點
seo-title: Blog Essentials
description: 部落格概述
seo-description: Blog overview
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---

# 部落格要點 {#blog-essentials}

截至AEM6.1社區，部落格是社區活動。 現在，部落格是從發佈環境發佈的，以前，部落格只能在作者環境中建立並發佈。

現在，任何社區成員都可以建立部落格，除非僅限於特權成員。

此頁提供了使用部落格功能的基本資訊。

>[!NOTE]
>
>部落格功能的底層基礎是日誌功能。

## 客戶端基本知識 {#essentials-for-client-side}

部落格功能由兩個主要元件組成，通過添加 [部落格功能](/help/communities/functions.md#blog-function) 或通過在作者編輯模式下將元件添加到頁面。

### 部落格 {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td>社會/日記帳/元件/hbs/日記帳</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>客戶端</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs投票<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>見 <a href="/help/communities/blog-feature.md">部落格功能</a></td>
  </tr>
 </tbody>
</table>

### 部落格則欄 {#blog-sidebar}

| **資源類型** | 社交/日誌/元件/hbs/側欄 |
|---|---|
| [**包含**](/help/communities/scf.md#add-or-include-a-communities-component) | 否 |
| [**客戶端**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **模板** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **cs** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **屬性** | 見 [部落格功能](/help/communities/blog-feature.md) |

* [客戶端自定義](/help/communities/client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [部落格API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [部落格終結點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [伺服器端自定義](/help/communities/server-customize.md)

### 部落格功能 {#blog-function}

包含該社區站點結構的 [部落格功能](/help/communities/functions.md#blog-function) 將配置 `Blog` 和 `Blog Sidebar` 元件。 Blog功能支援標識 [特權成員用戶組](/help/communities/users.md#privileged-members-group)。

### 訪問部落格條目(UGC) {#accessing-blog-entries-ugc}

UGC應使用一種標準的審核方法來審核。
請參閱 [調節用戶生成的內容](/help/communities/moderate-ugc.md)。

截至AEM6.1社區，使用 [普通商店](/help/communities/working-with-srp.md) UGC包括對UGC的寫程式訪問，而不考慮選擇的儲存選項（如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會發生更改，但不會發出警告**。

請參閱：

* [儲存資源提供程式概述](/help/communities/srp.md)  — 簡介和儲存庫使用概述。
* [SRP和UGC軟體包](/help/communities/srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP訪問UGC](/help/communities/accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](/help/communities/socialutils.md)  — 將不建議使用的實用程式方法映射到當前SRP實用程式方法。

## 主發佈伺服器 {#primary-publisher}

當部署為發佈場時，必須標識將輪詢計畫發佈的文章的主發佈者。

請參閱 [主發佈伺服器](/help/communities/deploy-communities.md#primary-publisher) 的子菜單。

## 允許富媒體 {#allowing-rich-media}

該平AEM台阻止來自其他網站的連結，以防止XSS攻擊，如所述

* [Protect反對跨站點指令碼(XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

從6.AEM2開始，以前需要手動進行的修改包含在預設的AntiSamy配置檔案中。

通過選擇 `Embed Media from External Sites` 表徵圖：

![媒體](assets/media-icon.png)
