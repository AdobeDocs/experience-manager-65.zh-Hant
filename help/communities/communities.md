---
title: 發展中社區
seo-title: Developing Communities
description: 建立和自定義社區功能，如論壇、用戶組等
seo-description: Create and customize community features such as forums, user groups, and more
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 5%

---

# 發展中社區  {#developing-communities}

## 概觀 {#overview}

AEM Communities簡化了社區功能的建立和定制，如論壇、用戶組、部落格、問答、日曆、評論、評論、投票、評級和工作分配。 這些功能導致在發佈環境中輸入用戶生成的內容(UGC)。

a的基礎 [社區站點](overview.md#communitiessites) 是 [社會構成框架](scf.md) (SCF)。 建立社區站點從選擇 [社區網站模板](sites-console.md) 由 [社區功能](functions.md)。

有關概述和入門教程，請訪問：

* [AEM Communities概述](overview.md)
* [AEM Communities入門](getting-started.md)

>[!NOTE]
> 
>強烈建議與 [最新版本](deploy-communities.md#latest-releases)。

## 建議的部署 {#recommended-deployments}

* [社區內容儲存](working-with-srp.md):討論UGC公用儲存的可用SRP選項
* [推薦的社區拓撲](topologies.md):討論基於用例的拓撲和SRP選擇

## 社會構成框架 {#social-component-framework}

* [社會構成框架](scf.md):框架和API概述。
* [SCF把手幫助器](handlebars-helpers.md):預設幫助程式以及如何編寫自定義幫助程式。
* [客戶端自定義](client-customize.md):自定義在瀏覽器中運行的代碼。
* [伺服器端定制](server-customize.md):自定義在伺服器上運行的代碼。
* [儲存資源提供程式(SRP)](srp.md):社區內容儲存概述。
* [編碼准則](code-guide.md):指南、提示和技巧。
* [社區元件指南](components-guide.md):互動式開發工具。

## 元件、功能和功能要素 {#component-function-and-feature-essentials}

AEM Communities元件、功能和功能為 [社區站點](sites-console.md)。

* [元件、功能和功能要素](essentials.md)
* [社區元件的客戶端](clientlibs.md)
* [社群功能](functions.md)
* [社群群組範本](tools-groups.md)
* [社群網站範本](sites.md)

## 社群成員 {#community-members}

* [管理用戶和用戶組](users.md)
* [與Facebook和Twitter社會登錄](social-login.md)

## 社群群組 {#community-groups}

[社區組](overview.md#communitygroups) 是允許社區成員在社區站點內形成子社區的概念。 在發佈或作者環境中可能會建立社區組。

* [社區組要件](essentials-groups.md)
* [組函式](functions.md#groups-function)
* [社群群組範本](tools-groups.md)
* [管理用戶和用戶組](users.md)
* [作者社區組](creating-groups.md)

## 管理資料 {#managing-data}

* [SRP和UGC軟體包](srp-and-ugc.md) - SRP API實用程式方法和示例
* [標籤軟體包](tag.md)  — 社區成員能夠標籤UGC和/或編錄啟用資源

## 教學課程 {#tutorials}

* [客戶端教程](tutorials.md#client-side-customization)
* [伺服器端教程](tutorials.md#server-side-customization)
* [操作說明](tutorials.md#how-to-instructions)

## 疑難排解 {#troubleshooting}

* [疑難排解](troubleshooting.md)
* [已知問題](/help/release-notes/release-notes.md)

## 相關社區文檔 {#related-communities-documentation}

* 訪問 [部署社區](deploy-communities.md) 瞭解建議的部署和調度程式配置。

* 訪問 [管理社區站點](administer-landing.md) 瞭解如何建立社區站點、配置社區站點模板、調節社區內容、管理成員和配置消息傳遞。

* 訪問 [創作社區元件](author-communities.md) 瞭解如何使用和配置社區元件。
