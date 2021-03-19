---
title: 社群網站
seo-title: 社群網站
description: AEM Communities檔案概述
seo-description: AEM Communities檔案概述
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 4%

---


# 社區站點{#communities-sites}

本節內容適用於管理AEM Communities並熟悉AEM Communities功能的人員。

## 概覽 {#overview}

如需概觀和快速入門教學課程，請造訪：

* [AEM Communities概觀](overview.md)
* [開始使用AEM Communities](getting-started.md)
* [AEM Communities啟用快速入門](getting-started-enablement.md)

## 管理和配置主題{#administration-and-configuration-topics}

### 社區站點建立和管理{#communities-site-creation-and-management}

* 社區[控制台](consoles.md)

   * [網站](sites-console.md)

      * [群組（子社群）](groups.md)
   * [審核](moderation.md)
   * [成員和組管理](members.md)
   * [啟用資源](resources.md)
   * [報表](reports.md)


* 社區&#x200B;[*工具*](tools.md):

   * [網站範本](sites.md)
   * [群組範本](tools-groups.md)
   * [社群功能](functions.md)
   * [儲存設定](srp-config.md)
   * [元件指南](components-guide.md)
   * [徽章](badges.md)


### 使用者產生的內容 {#user-generated-content}

AEM Communities的一項主要功能是，網站訪客（成員）登入產生使用者產生的內容(UGC)。 若要進一步瞭解如何使用UGC，請造訪：

* [常見UGC商店](working-with-srp.md):UGC共用儲存的SRP選擇
* [協調UGC](moderate-ugc.md):受信任的成員可以大量協調UGC或在上下文中協調UGC
* [標籤UGC](tag-ugc.md):功能可設定為允許成員標籤內容
* [翻譯UGC](translate-ugc.md):功能可設定為翻譯所有UGC，或允許成員翻譯選取的貼文
* [Analytics設定](analytics.md):使Adobe Analytics能夠報告與成員活動有關的各種度量

### 社群成員 {#community-members}

* [管理使用者和使用者群組](users.md):社區成員和成員組（包括特權成員）的詳細資訊。
* [貢獻限制](limits.md):可限制新成員張貼。
* [隧道服務](deploy-communities.md#tunnel-service-on-author):允許從作者環境訪問發佈端成員和成員組。
* [成員和組控制台](members.md):允許從作者環境建立和管理發布端成員和成員組。
* [用戶同步](sync.md):用於同步多個發佈實例的成員和成員組。
* [使用Facebook和Twitter進行社交登入](social-login.md):網站訪客使用其Facebook或Twitter憑證成為社群成員的能力。
* [計分和徽章](implementing-scoring.md):可指派徽章來識別成員的角色，以及讓成員透過參與社群而獲得徽章。
* [通知](notifications.md):可讓成員獲知其所關注的活動。
* [訂閱](subscriptions.md):讓會員使用外部電子郵件與社群互動。
* [訊息](messaging.md):讓成員使用內部訊息與社群互動。

### 啟用功能{#enablement-features}

* [設定啟用](enablement.md):正確設定啟用功能的必要資訊。
* [Analytics設定](analytics.md):為「社區」功能啟用「Adobe Analytics」的必要資訊。
* [標籤啟用資源](tag-resources.md):建立啟用目錄的必要資訊。

### 部署 {#deployment}

部署部分包含AEM Communities的特定資訊。

使用社群內容的性質會影響部署結構：

* [推薦的社區拓撲](topologies.md)

請務必在平台上安裝最新的CommunitiesAEM版本：

* [最新社群功能套件](deploy-communities.md#latestfeaturepack)

有關其他Communities特定資訊（如[Upgrading](upgrade.md)、[Dispatcher](dispatcher.md)和[Replication](deploy-communities.md#replication-agents-on-author)），請參見部署頁。

## 相關社群檔案{#related-communities-documentation}

* 請造訪[部署社群](deploy-communities.md)以瞭解建議的部署。

* 請造訪[開發社群](communities.md)以瞭解社交元件架構(SCF)和自訂社群元件和功能。

* 請造訪[編寫社群元件](author-communities.md)，以瞭解如何編寫和設定社群元件。
