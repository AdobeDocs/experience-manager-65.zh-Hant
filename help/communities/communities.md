---
title: 開發社群
seo-title: 開發社群
description: 建立和自訂社群功能，例如論壇、使用者群組等
seo-description: 建立和自訂社群功能，例如論壇、使用者群組等
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 5%

---


# 開發社區{#developing-communities}

## 概覽 {#overview}

AEM Communities可簡化社群功能的建立與自訂，例如論壇、使用者群組、部落格、問答、日曆、留言、評論、投票、評分和工作。 這些功能會導致使用者產生的內容(UGC)被輸入到發佈環境中。

[社區站點](overview.md#communitiessites)的基礎是[社會元件框架](scf.md)(SCF)。 建立社區站點從選擇由[社區功能](functions.md)組成的[社區站點模板開始。](sites-console.md)

如需概觀和快速入門教學課程，請造訪：

* [AEM Communities概觀](overview.md)
* [AEM Communities快速入門](getting-started.md)
* [AEM Communities的啟用快速入門](getting-started-enablement.md)

>[!NOTE]
> 
>強烈建議您隨時更新[最新版本](deploy-communities.md#latest-releases)。

## 建議的部署{#recommended-deployments}

* [社群內容儲存](working-with-srp.md):討論UGC公用商店的可用SRP選擇
* [推薦的社群拓撲](topologies.md):討論基於使用案例和SRP選擇的拓撲

## 社交元件架構{#social-component-framework}

* [社交元件架構](scf.md):架構和API的概觀。
* [SCF Handlebers](handlebars-helpers.md):拖欠傭工，如何編寫傭工。
* [用戶端自訂](client-customize.md):自訂在瀏覽器中執行的程式碼。
* [伺服器端自訂](server-customize.md):自訂在伺服器上執行的程式碼。
* [儲存資源提供商(SRP)](srp.md):社群內容儲存的概觀。
* [編碼准則](code-guide.md):准則、秘訣與訣竅。
* [社群元件指南](components-guide.md):互動式開發工具。

## 元件、功能和功能基本工具{#component-function-and-feature-essentials}

AEM Communities元件、函式和功能提供[社群網站](sites-console.md)的建置區塊。

* [元件、功能和功能基本工具](essentials.md)
* [Clientlibs for Communities元件](clientlibs.md)
* [社群功能](functions.md)
* [社群群組範本](tools-groups.md)
* [社群網站範本](sites.md)

## 社群成員 {#community-members}

* [管理使用者和使用者群組](users.md)
* [使用Facebook和Twitter進行社交登入](social-login.md)

## 社群群組 {#community-groups}

[社](overview.md#communitygroups) 區群組的概念是允許社區成員在社區站點內形成子社區。在發佈或作者環境中可能會建立社群群組。

* [Community Group Essentials](essentials-groups.md)
* [群組函式](functions.md#groups-function)
* [社群群組範本](tools-groups.md)
* [管理使用者和使用者群組](users.md)
* [作者的社群群組](creating-groups.md)

## 管理資料{#managing-data}

* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP API實用程式方法和示例
* [Tag Essentials](tag.md)  —— 社群成員標籤UGC和／或分類啟用資源的能力

## 教學課程 {#tutorials}

* [用戶端教學課程](tutorials.md#client-side-customization)
* [伺服器端教學課程](tutorials.md#server-side-customization)
* [操作說明](tutorials.md#how-to-instructions)

## 疑難排解 {#troubleshooting}

* [疑難排解](troubleshooting.md)
* [已知問題](/help/release-notes/known-issues.md)

## 相關社群檔案{#related-communities-documentation}

* 請造訪[部署Communities](deploy-communities.md)，以瞭解建議的部署和分派程式設定。

* 請造訪[管理社群網站](administer-landing.md)，以瞭解如何建立社群網站、設定社群網站範本、協調社群內容、管理成員以及設定訊息。

* 請造訪[編寫社群元件](author-communities.md)，以瞭解如何編寫和設定社群元件。

