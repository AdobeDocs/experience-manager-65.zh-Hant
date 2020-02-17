---
title: 社群網站
seo-title: 社群網站
description: AEM Communities檔案概觀
seo-description: AEM Communities檔案概觀
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Communities Sites {#communities-sites}

本節適用於管理AEM Communities並假設熟悉AEM Communities功能的人員。

## 概覽 {#overview}

如需概觀和快速入門教學課程，請造訪：

* [AEM Communities概觀](overview.md)
* [AEM Communities快速入門](getting-started.md)
* [AEM Communities的啟用快速入門](getting-started-enablement.md)

## 管理和配置主題 {#administration-and-configuration-topics}

### 社群網站的建立與管理 {#communities-site-creation-and-management}

* 社群主 [控台](consoles.md)

   * [網站](sites-console.md)

      * [群組（子社群）](groups.md)
   * [審核](moderation.md)
   * [成員和組管理](members.md)
   * [啟用資源](resources.md)
   * [報表](reports.md)


* 社群 [*工具&#x200B;*](tools.md):

   * [網站範本](sites.md)
   * [群組範本](tools-groups.md)
   * [社群功能](functions.md)
   * [儲存設定](srp-config.md)
   * [元件指南](components-guide.md)
   * [徽章](badges.md)


### 使用者產生的內容 {#user-generated-content}

AEM Communities的主要功能是，由網站訪客（成員）登入產生使用者產生的內容(UGC)。 若要進一步瞭解如何使用UGC，請造訪：

* [常見UGC商店](working-with-srp.md):UGC共用儲存的SRP選擇
* [協調UGC](moderate-ugc.md):受信任的成員可以大量協調UGC或在上下文中協調UGC
* [標籤UGC](tag-ugc.md):功能可設定為允許成員標籤內容
* [翻譯UGC](translate-ugc.md):功能可設定為翻譯所有UGC，或允許成員翻譯選取的貼文
* [Analytics設定](analytics.md):讓Adobe Analytics能夠報告與成員活動相關的各種度量

### 社群成員 {#community-members}

* [管理使用者和使用者群組](users.md):社區成員和成員組（包括特權成員）的詳細資訊
* [貢獻限制](limits.md):能夠限制新成員張貼
* [隧道服務](deploy-communities.md#tunnel-service-on-author):允許從作者環境訪問發佈端成員和成員組
* [成員和組控制台](members.md):允許從作者環境建立和管理發布端成員和成員組
* [用戶同步](sync.md):在多個發佈實例中同步成員和成員組
* [使用Facebook和Twitter進行社交登入](social-login.md):網站訪客使用其Facebook或Twitter憑證成為社群成員的能力
* [計分和徽章](implementing-scoring.md):可指派徽章來識別成員角色，以及讓成員透過參與社群而獲得徽章
* [通知](notifications.md):能夠通知成員所關注的活動
* [訂閱](subscriptions.md):讓會員使用外部電子郵件與社群互動的能力
* [訊息](messaging.md):讓成員使用內部訊息與社群互動的能力

### 啟用功能 {#enablement-features}

* [設定啟用](enablement.md):正確設定啟用功能的必要資訊
* [Analytics設定](analytics.md):啟用Adobe Analytics for Communities功能的必要資訊
* [標籤啟用資源](tag-resources.md):建立啟用型錄的必要性

### 部署 {#deployment}

部署區段包含AEM Communities專屬的資訊。

使用社群內容的性質會影響部署結構：

* [推薦的社區拓撲](topologies.md)

請務必在AEM平台上安裝最新的Communities版本：

* [最新社群功能套件](deploy-communities.md#latestfeaturepack)

有關其他Communities特定資訊(如升級、 [Dispatcher](upgrade.md)和複製)的資訊，請 [參見部署頁](dispatcher.md)[](deploy-communities.md#replication-agents-on-author)。

## 相關社群檔案 {#related-communities-documentation}

* 請造 [訪部署社群](deploy-communities.md) ，以瞭解建議的部署。

* 請造 [訪開發社群](communities.md) ，以瞭解社交元件架構(SCF)及自訂社群元件與功能。

* 請造 [訪編寫社群元件](author-communities.md) ，以瞭解如何使用和設定社群元件。
