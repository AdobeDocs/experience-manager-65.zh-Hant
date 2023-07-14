---
title: 開發社群
description: 建立和自訂社群功能，例如論壇、使用者群組等。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 5%

---

# 開發社群  {#developing-communities}

## 概觀 {#overview}

Adobe Experience Manager (AEM) Communities可簡化社群功能的建立和自訂作業，例如論壇、使用者群組、部落格、Q&amp;A、行事曆、評論、評論、投票、評分和指派。 這些功能導致使用者產生的內容(UGC)被輸入發佈環境中。

的基礎 [社群網站](overview.md#communitiessites) 是 [社交元件框架](scf.md) (SCF)。 社群網站的建立從選擇開始 [社群網站範本](sites-console.md) 由下列專案組成 [社群功能](functions.md).

如需概覽和快速入門教學課程，請造訪：

* [AEM Communities概觀](overview.md)
* [AEM Communities快速入門](getting-started.md)

>[!NOTE]
> 
>強烈建議隨時掌握最新資訊 [最新版本](deploy-communities.md#latest-releases).

## 建議的部署 {#recommended-deployments}

* [社群內容儲存](working-with-srp.md)：討論UGC一般存放區可用的社交資源提供者(SRP)選擇
* [社群適用的建議拓撲](topologies.md)：根據使用案例和SRP選擇討論拓撲

## 社交元件架構 {#social-component-framework}

* [社交元件架構](scf.md)：框架和API概觀。
* [SCF Handlebars協助程式](handlebars-helpers.md)：預設協助程式以及如何撰寫自訂協助程式。
* [使用者端自訂](client-customize.md)：自訂在瀏覽器中執行的程式碼。
* [伺服器端自訂](server-customize.md)：自訂在伺服器上執行的程式碼。
* [儲存資源提供者(SRP)](srp.md)：社群內容儲存概述。
* [編碼准則](code-guide.md)：指南、提示與秘訣。
* [社群元件指南](components-guide.md)：互動式開發工具。

## 元件、函式和Feature Essentials {#component-function-and-feature-essentials}

AEM Communities元件、函式和功能提供建置區塊， [社群網站](sites-console.md).

* [元件、函式和Feature Essentials](essentials.md)
* [Communities元件的Clientlibs](clientlibs.md)
* [社群功能](functions.md)
* [社群群組範本](tools-groups.md)
* [社群網站範本](sites.md)

## 社群成員 {#community-members}

* [管理使用者和使用者群組](users.md)
* [使用Facebook和Twitter進行社交登入](social-login.md)

## 社群群組 {#community-groups}

[社群群組](overview.md#communitygroups) 是允許社群成員在社群網站內建立子社群的構想。 您可以在發佈或作者環境中建立社群群組。

* [社群群組Essentials](essentials-groups.md)
* [群組功能](functions.md#groups-function)
* [社群群組範本](tools-groups.md)
* [管理使用者和使用者群組](users.md)
* [作者適用的社群群組](creating-groups.md)

## 管理資料 {#managing-data}

* [SRP和UGC Essentials](srp-and-ugc.md) - SRP API公用程式方法與範例
* [標籤Essentials](tag.md)  — 社群成員可標籤UGC和/或編目啟用資源

## 教學課程 {#tutorials}

* [使用者端教學課程](tutorials.md#client-side-customization)
* [伺服器端教學課程](tutorials.md#server-side-customization)
* [操作說明](tutorials.md#how-to-instructions)

## 疑難排解 {#troubleshooting}

* [疑難排解](troubleshooting.md)
* [已知問題](/help/release-notes/release-notes.md)

## 相關Communities檔案 {#related-communities-documentation}

* 造訪 [部署社群](deploy-communities.md) 以瞭解建議的部署和Dispatcher設定。

* 造訪 [管理社群網站](administer-landing.md) 瞭解有關建立社群網站、設定社群網站範本、仲裁社群內容、管理成員和設定傳訊功能的資訊。

* 造訪 [Authoring Communities元件](author-communities.md) 瞭解如何使用及設定Communities元件進行創作。
