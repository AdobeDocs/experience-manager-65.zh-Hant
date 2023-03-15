---
title: 社群網站
seo-title: Communities Sites
description: AEM Communities檔案概觀
seo-description: Overview of the AEM Communities documentation
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 4%

---

# 社群網站 {#communities-sites}

本節內容適用於管理AEM Communities且熟悉AEM Communities功能的使用者。

## 概觀 {#overview}

如需概述和快速入門教學課程，請造訪：

* [AEM Communities概述](overview.md)
* [開始使用AEM Communities](getting-started.md)
* [AEM Communities啟用快速入門](getting-started-enablement.md)

## 管理和設定主題 {#administration-and-configuration-topics}

### Communities站點建立和管理 {#communities-site-creation-and-management}

* 社群 [主控台](consoles.md)

   * [Sites](sites-console.md)

      * [組（子社區）](groups.md)
   * [審核](moderation.md)
   * [成員和組管理](members.md)
   * [啟用資源](resources.md)
   * [報表](reports.md)


* 社群 [*工具*](tools.md):

   * [網站範本](sites.md)
   * [群組範本](tools-groups.md)
   * [社群功能](functions.md)
   * [儲存設定](srp-config.md)
   * [元件指南](components-guide.md)
   * [徽章](badges.md)


### 使用者產生的內容 {#user-generated-content}

AEM Communities的主要功能是透過登入的網站訪客（成員）產生使用者產生的內容(UGC)。 若要進一步了解如何使用UGC，請造訪：

* [通用UGC儲存](working-with-srp.md):UGC共用儲存的SRP選擇
* [調節UGC](moderate-ugc.md):受信任的成員可以批量或在上下文中協調UGC
* [標籤UGC](tag-ugc.md):功能可配置為允許成員標籤內容
* [翻譯UGC](translate-ugc.md):功能可配置為翻譯所有UGC或允許成員翻譯所選貼文
* [Analytics設定](analytics.md):啟用Adobe Analytics，報告關於成員活動的各種量度

### 社群成員 {#community-members}

* [管理使用者和使用者群組](users.md):社區成員和成員組（包括特權成員）的詳細資訊。
* [貢獻限制](limits.md):能夠限制由新成員張貼。
* [通道服務](deploy-communities.md#tunnel-service-on-author):允許從製作環境存取發佈端成員和成員群組。
* [成員和組控制台](members.md):允許從製作環境建立和管理發布端成員和成員群組。
* [使用者同步](sync.md):用於跨多個發佈實例同步成員和成員組。
* [使用Facebook和Twitter進行社交登入](social-login.md):網站訪客可使用其Facebook或Twitter憑證成為社群成員。
* [計分和徽章](implementing-scoring.md):指派徽章以識別成員角色的能力，以及透過成員參與社群而獲得徽章的能力。
* [通知](notifications.md):可通知成員其所遵循的活動。
* [訂閱](subscriptions.md):讓成員使用外部電子郵件與社群互動。
* [傳訊](messaging.md):讓成員使用內部訊息與社群互動。

### 啟用功能 {#enablement-features}

* [配置啟用](enablement.md):正確設定啟用功能的必要資訊。
* [Analytics設定](analytics.md):啟用Adobe Analytics for Communities功能的必要資訊。
* [標籤啟用資源](tag-resources.md):建立啟用目錄的必要條件。

### 部署 {#deployment}

部署區段包含AEM Communities的特定資訊。

使用社區內容的性質會影響部署的結構：

* [適用於社群的建議拓撲](topologies.md)

請務必在AEM平台上安裝最新的Communities版本：

* [最新Communities Feature Pack](deploy-communities.md#latestfeaturepack)

有關其他Communities特定資訊(如 [升級](upgrade.md), [Dispatcher](dispatcher.md) 和 [復寫](deploy-communities.md#replication-agents-on-author).

## 相關社群檔案 {#related-communities-documentation}

* 瀏覽 [部署社群](deploy-communities.md) 了解建議的部署。

* 瀏覽 [開發社區](communities.md) 了解社交元件架構(SCF)和自訂社群元件和功能。

* 瀏覽 [編寫Communities元件](author-communities.md) 了解如何使用和設定Communities元件。
