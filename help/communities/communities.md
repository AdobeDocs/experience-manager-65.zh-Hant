---
title: 開發社群
description: 建立和自訂社群功能，例如論壇、使用者群組等。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# 開發社群  {#developing-communities}

## 概觀 {#overview}

Adobe Experience Manager (AEM)社群可簡化社群功能（例如論壇、使用者群組、部落格、Q&amp;A、行事曆、評論、評論、投票、評分和指派）的建立和自訂。 這些功能會導致使用者產生的內容(UGC)進入發佈環境。

[社群網站](overview.md#communitiessites)的基礎是[社交元件架構](scf.md) (SCF)。 社群網站的建立從選取由[社群功能](functions.md)所組成的[社群網站範本](sites-console.md)開始。

如需概覽和快速入門教學課程，請造訪：

* [AEM Communities概觀](overview.md)
* [AEM Communities快速入門](getting-started.md)

>[!NOTE]
> 
>強烈建議您隨時更新[最新版本](deploy-communities.md#latest-releases)。

## 建議的部署 {#recommended-deployments}

* [社群內容存放區](working-with-srp.md)：討論UGC一般存放區可用的社交資源提供者(SRP)選擇
* [社群建議拓撲](topologies.md)：根據使用案例和SRP選擇討論拓撲

## 社交元件架構 {#social-component-framework}

* [社交元件架構](scf.md)：架構和API的概觀。
* [SCF Handlebars協助程式](handlebars-helpers.md)：預設協助程式以及如何撰寫自訂協助程式。
* [使用者端自訂](client-customize.md)：自訂瀏覽器中執行的程式碼。
* [伺服器端自訂](server-customize.md)：自訂伺服器上執行的程式碼。
* [儲存資源提供者(SRP)](srp.md)：社群內容儲存的總覽。
* [程式碼指南](code-guide.md)：指南、提示與秘訣。
* [社群元件指南](components-guide.md)：互動式開發工具。

## 元件、函式和Feature Essentials {#component-function-and-feature-essentials}

AEM Communities元件、功能和功能提供[社群網站](sites-console.md)的建置組塊。

* [元件、功能和功能要點](essentials.md)
* [適用於社群元件的Clientlibs](clientlibs.md)
* [社群功能](functions.md)
* [社群群組範本](tools-groups.md)
* [社群網站範本](sites.md)

## 社群成員 {#community-members}

* [管理使用者和使用者群組](users.md)
* [使用Facebook和Twitter進行社交登入](social-login.md)

## 社群群組 {#community-groups}

[社群群組](overview.md#communitygroups)的概念是允許社群成員在社群網站內建立子社群。 您可以在發佈或製作環境中建立社群群組。

* [社群群組要點](essentials-groups.md)
* [群組功能](functions.md#groups-function)
* [社群群組範本](tools-groups.md)
* [管理使用者和使用者群組](users.md)
* [作者的社群群組](creating-groups.md)

## 管理資料 {#managing-data}

* [SRP與UGC Essentials](srp-and-ugc.md) - SRP API公用程式方法與範例
* [標籤Essentials](tag.md) — 社群成員標籤UGC和/或目錄啟用資源的能力

## 教學課程 {#tutorials}

* [使用者端教學課程](tutorials.md#client-side-customization)
* [伺服器端教學課程](tutorials.md#server-side-customization)
* [操作說明](tutorials.md#how-to-instructions)

## 疑難排解 {#troubleshooting}

* [疑難排解](troubleshooting.md)
* [已知問題](/help/release-notes/release-notes.md)

## 相關社群檔案 {#related-communities-documentation}

* 請造訪[部署社群](deploy-communities.md)，瞭解建議的部署和Dispatcher設定。

* 請造訪[管理社群網站](administer-landing.md)，瞭解如何建立社群網站、設定社群網站範本、管理社群內容、管理成員，以及設定訊息。

* 請造訪[Authoring Communities Components](author-communities.md)，瞭解如何使用及設定Communities元件進行創作。
