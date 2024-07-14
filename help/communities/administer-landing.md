---
title: 社群網站
description: 瞭解適用於已熟悉其基本功能之管理員的Adobe Experience Manager (AEM)社群基礎知識。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 4%

---

# 社群網站 {#communities-sites}

本節適用於管理AEM Communities並假設熟悉AEM Communities功能的人。

## 概觀 {#overview}

如需概覽和快速入門教學課程，請造訪：

* [AEM Communities概觀](overview.md)
* [AEM Communities快速入門](getting-started.md)

## 管理和設定主題 {#administration-and-configuration-topics}

### 社群網站建立與管理 {#communities-site-creation-and-management}

* 社群[主控台](consoles.md)

   * [Sites](sites-console.md)

      * [群組（子社群）](groups.md)

   * [審核](moderation.md)
   * [成員和群組管理](members.md)
   * [報告](reports.md)

* 社群&#x200B;[*工具*](tools.md)：

   * [網站範本](sites.md)
   * [群組範本](tools-groups.md)
   * [社群功能](functions.md)
   * [儲存體設定](srp-config.md)
   * [元件指南](components-guide.md)
   * [徽章](badges.md)


### 使用者產生的內容 {#user-generated-content}

AEM Communities的主要功能是透過登入網站訪客（成員）產生使用者產生的內容(UGC)。 若要進一步瞭解如何使用UGC，請造訪：

* [通用UGC存放區](working-with-srp.md)：選擇UGC共用存放區的SRP
* [正在稽核UGC](moderate-ugc.md)：受信任的成員可能會大量或內嵌稽核UGC
* [標籤UGC](tag-ugc.md)：功能可設定為允許成員標籤內容
* [翻譯UGC](translate-ugc.md)：功能可設定為翻譯所有UGC或允許成員翻譯選取的貼文
* [Analytics設定](analytics.md)：啟用Adobe Analytics以報告有關成員活動的各種量度

### 社群成員 {#community-members}

* [管理使用者和使用者群組](users.md)：社群成員和成員群組（包括特殊許可權成員）的詳細資料。
* [貢獻限制](limits.md)：限制新成員張貼的能力。
* [通道服務](deploy-communities.md#tunnel-service-on-author)：允許從作者環境存取發佈端成員和成員群組。
* [成員和群組主控台](members.md)：允許從作者環境建立和管理發布端成員和成員群組。
* [使用者同步處理](sync.md)：同步處理多個發佈執行個體的成員與成員群組。
* [使用Facebook和Twitter的社交登入](social-login.md)：網站訪客能夠使用其Facebook或Twitter認證成為社群成員。
* [評分與徽章](implementing-scoring.md)：指派徽章以識別成員角色的能力，以及讓成員透過參與社群來獲得徽章的能力。
* [通知](notifications.md)：成員能夠收到他們所關注活動的通知。
* [訂閱](subscriptions.md)：成員可使用外部電子郵件與社群互動。
* [傳訊](messaging.md)：成員使用內部訊息與社群互動的能力。

### 部署 {#deployment}

部署區段包含AEM Communities的特定資訊。

使用社群內容的性質會影響部署結構：

* [社群適用的建議拓撲](topologies.md)

在AEM平台上安裝最新的Communities版本很重要：

* [最新Communities Feature Pack](deploy-communities.md#latestfeaturepack)

請參閱部署頁面以取得其他社群特定的資訊，例如[升級](upgrade.md)、[Dispatcher](dispatcher.md)以及[復寫](deploy-communities.md#replication-agents-on-author)。

## 相關社群檔案 {#related-communities-documentation}

* 請造訪[部署社群](deploy-communities.md)，瞭解建議的部署。

* 造訪[開發Communities](communities.md)，瞭解社交元件架構(SCF)和自訂Communities元件和功能。

* 造訪[Authoring Communities Components](author-communities.md)，瞭解如何使用及設定Communities元件進行創作。
