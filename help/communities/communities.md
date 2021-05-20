---
title: 開發社區
seo-title: 開發社區
description: 建立和自訂社群功能，例如論壇、使用者群組等
seo-description: 建立和自訂社群功能，例如論壇、使用者群組等
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 5%

---

# 開發社區{#developing-communities}

## 概覽 {#overview}

AEM Communities可簡化社群功能的建立和自訂作業，例如論壇、使用者群組、部落格、問答、日曆、留言、評論、投票、評分和指派。 這些功能會導致在發佈環境中輸入使用者產生的內容(UGC)。

[社區站點](overview.md#communitiessites)的基礎是[社會元件框架](scf.md)(SCF)。 建立社區站點從選擇[社區站點模板](sites-console.md)開始，該模板由[社區函式](functions.md)組成。

如需概述和快速入門教學課程，請造訪：

* [AEM Communities概述](overview.md)
* [開始使用AEM Communities](getting-started.md)
* [AEM Communities啟用快速入門](getting-started-enablement.md)

>[!NOTE]
> 
>強烈建議您與[最新版本](deploy-communities.md#latest-releases)保持最新。

## 建議的部署{#recommended-deployments}

* [社群內容儲存](working-with-srp.md):討論UGC通用商店的可用SRP選擇
* [適用於社群的建議拓撲](topologies.md):基於用例和SRP選擇討論拓撲

## 社交元件架構{#social-component-framework}

* [社交元件架構](scf.md):架構和API概觀。
* [SCF Handlebars Helpers](handlebars-helpers.md):預設幫助器，如何編寫定制幫助器。
* [用戶端自訂](client-customize.md):自訂在瀏覽器中執行的程式碼。
* [伺服器端自訂](server-customize.md):自訂在伺服器上執行的程式碼。
* [儲存資源提供商(SRP)](srp.md):社群內容儲存概觀。
* [編碼准則](code-guide.md):准則、提示與秘訣。
* [社群元件指南](components-guide.md):互動式開發工具。

## 元件、函式和功能要點{#component-function-and-feature-essentials}

AEM Communities元件、功能和功能提供[社群網站](sites-console.md)的建置區塊。

* [元件、功能和功能要點](essentials.md)
* [Communities元件的Clientlibs](clientlibs.md)
* [社群功能](functions.md)
* [社群群組範本](tools-groups.md)
* [社群網站範本](sites.md)

## 社群成員 {#community-members}

* [管理使用者和使用者群組](users.md)
* [使用Facebook和Twitter進行社交登入](social-login.md)

## 社群群組 {#community-groups}

[社](overview.md#communitygroups) 群群組的概念是允許社群成員在社群網站內形成子社群。發佈或製作環境中可能會建立社群群組。

* [社群群組要點](essentials-groups.md)
* [組函式](functions.md#groups-function)
* [社群群組範本](tools-groups.md)
* [管理使用者和使用者群組](users.md)
* [作者社群群組](creating-groups.md)

## 管理資料{#managing-data}

* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP API公用程式方法與範例
* [Tag Essentials](tag.md)  — 社群成員標籤UGC和/或已編目的啟用資源的功能

## 教學課程 {#tutorials}

* [用戶端教學課程](tutorials.md#client-side-customization)
* [伺服器端教學課程](tutorials.md#server-side-customization)
* [作法指示](tutorials.md#how-to-instructions)

## 疑難排解 {#troubleshooting}

* [疑難排解](troubleshooting.md)
* [已知問題](/help/release-notes/known-issues.md)

## 相關社群檔案{#related-communities-documentation}

* 請造訪[部署Communities](deploy-communities.md)以了解建議的部署和Dispatcher設定。

* 請訪問[管理社區站點](administer-landing.md)了解如何建立社區站點、配置社區站點模板、協調社區內容、管理成員以及配置消息。

* 請造訪[編寫社群元件](author-communities.md)，了解如何使用和設定社群元件。
