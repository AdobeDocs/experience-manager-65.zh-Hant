---
title: 部落格要點
description: 瞭解如何將部落格功能新增到頁面，以便登入的社群成員可以發表部落格。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# 部落格要點 {#blog-essentials}

截至AEM 6.1 Communities，部落格是社群活動。 部落格現在從發佈環境發佈，而以前只能在作者環境中建立並發佈部落格。

部落格現在可由任何社群成員建立，除非僅限於有特殊許可權的成員。

本頁提供使用部落格功能的基本資訊。

>[!NOTE]
>
>部落格功能的基礎架構是日誌功能。

## 使用者端的Essentials {#essentials-for-client-side}

部落格功能由兩個主要元件組成，這些元件可透過新增 [部落格功能](/help/communities/functions.md#blog-function) 或透過在作者編輯模式下將元件新增至頁面。

### 部落格 {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>另請參閱 <a href="/help/communities/blog-feature.md">部落格功能</a></td>
  </tr>
 </tbody>
</table>

### 部落格則欄 {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**包含**](/help/communities/scf.md#add-or-include-a-communities-component) | 否 |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **範本** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **屬性** | 另請參閱 [部落格功能](/help/communities/blog-feature.md) |

* [使用者端自訂](/help/communities/client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [部落格API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [部落格端點](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [伺服器端自訂](/help/communities/server-customize.md)

### 部落格功能 {#blog-function}

社群網站結構包含 [部落格功能](/help/communities/functions.md#blog-function) 有 `Blog` 和 `Blog Sidebar` 元件已設定。 Blog功能支援識別 [有特殊許可權的成員使用者群組](/help/communities/users.md#privileged-members-group).

### 存取部落格專案(UGC) {#accessing-blog-entries-ugc}

UGC應使用其中一種標準仲裁方法進行仲裁。
另請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

自AEM 6.1社群起，使用 [公用存放區](/help/communities/working-with-srp.md) for UGC包含對UGC的程式化存取，無論選擇的儲存選項（例如ASRP、MSRP或JSRP）為何。

**UGC在存放庫中的位置和格式可能會有所變更，恕不另行警告**.

請參閱：

* [儲存資源提供者概觀](/help/communities/srp.md)  — 簡介和存放庫使用概述。
* [srp和UGC Essentials](/help/communities/srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](/help/communities/accessing-ugc-with-srp.md)  — 程式碼指南。
* [SocialUtils重構](/help/communities/socialutils.md)  — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。

## 主要發行者 {#primary-publisher}

當部署為發佈伺服器陣列時，必須識別輪詢排定發佈之文章的主要發佈者。

另請參閱 [主要發行者](/help/communities/deploy-communities.md#primary-publisher) 以取得更多詳細資料。

## 允許多媒體 {#allowing-rich-media}

AEM平台會封鎖其他網站的連結，以防止XSS攻擊，如所述

* [Protect避免跨網站指令碼(XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

自AEM 6.2起，先前需要手動進行的修改會包含在預設的AntiSamy設定檔案中。

透過選取 `Embed Media from External Sites` 圖示：

![媒體](assets/media-icon.png)
