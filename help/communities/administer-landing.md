---
title: 社區站點
seo-title: Communities Sites
description: AEM Communities檔案概述
seo-description: Overview of the AEM Communities documentation
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 4%

---

# 社區站點 {#communities-sites}

本節面向管理AEM Communities並假定熟悉AEM Communities功能的人員。

## 概觀 {#overview}

有關概述和入門教程，請訪問：

* [AEM Communities概述](overview.md)
* [AEM Communities入門](getting-started.md)

## 管理和配置主題 {#administration-and-configuration-topics}

### 社區站點建立和管理 {#communities-site-creation-and-management}

* 社區 [控制台](consoles.md)

   * [Sites](sites-console.md)

      * [組（子社區）](groups.md)
   * [審核](moderation.md)
   * [成員和組管理](members.md)
   * [報告](reports.md)


* 社區 [*工具*](tools.md):

   * [網站範本](sites.md)
   * [群組範本](tools-groups.md)
   * [社群功能](functions.md)
   * [儲存設定](srp-config.md)
   * [元件指南](components-guide.md)
   * [徽章](badges.md)


### 使用者產生的內容 {#user-generated-content}

AEM Communities的一個主要特點是通過登錄站點訪問者（成員）生成用戶生成的內容(UGC)。 要瞭解有關使用UGC的詳細資訊，請訪問：

* [公用UGC儲存](working-with-srp.md):UGC共用儲存的SRP選擇
* [調節UGC](moderate-ugc.md):受信任成員可以批量或在上下文中調節UGC
* [標籤UGC](tag-ugc.md):功能可配置為允許成員標籤內容
* [翻譯UGC](translate-ugc.md):功能可配置為轉換所有UGC或允許成員轉換所選帖子
* [分析配置](analytics.md):使Adobe Analytics能夠報告關於成員活動的各種指標

### 社群成員 {#community-members}

* [管理用戶和用戶組](users.md):社區成員和成員組（包括特權成員）的詳細資訊。
* [繳費限額](limits.md):能夠限制新成員的過帳。
* [隧道服務](deploy-communities.md#tunnel-service-on-author):允許從作者環境訪問發佈端成員和成員組。
* [成員和組控制台](members.md):允許從作者環境建立和管理發布端成員和成員組。
* [用戶同步](sync.md):用於在多個發佈實例之間同步成員和成員組。
* [與Facebook和Twitter社會登錄](social-login.md):站點訪問者使用其Facebook或Twitter證書成為社區成員的能力。
* [評分和徽章](implementing-scoring.md):獲得徽章以識別成員角色的能力，以及通過成員參與社區獲得徽章的能力。
* [通知](notifications.md):允許成員獲知其所遵循的活動。
* [訂閱](subscriptions.md):使成員能夠使用外部電子郵件與社區交互。
* [消息](messaging.md):允許成員使用內部消息與社區交互。

### 部署 {#deployment}

部署部分包含特定於AEM Communities的資訊。

使用社區內容的性質會影響部署的結構：

* [推薦的社區拓撲](topologies.md)

在平台上安裝最新的社區版本非常AEM重要：

* [最新社區功能包](deploy-communities.md#latestfeaturepack)

請參見部署頁以瞭解其他特定於社區的資訊，如 [升級](upgrade.md)。 [調度程式](dispatcher.md) 和 [複製](deploy-communities.md#replication-agents-on-author)。

## 相關社區文檔 {#related-communities-documentation}

* 訪問 [部署社區](deploy-communities.md) 瞭解建議的部署。

* 訪問 [發展中社區](communities.md) 瞭解社會元件框架(SCF)和自定義社區元件和功能。

* 訪問 [創作社區元件](author-communities.md) 瞭解如何使用和配置社區元件。
