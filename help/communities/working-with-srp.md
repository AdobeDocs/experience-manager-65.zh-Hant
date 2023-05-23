---
title: SRP — 社區內容儲存
seo-title: SRP - Community Content Storage
description: 從AEM Communities6.1開始，用戶生成的內容(UGC)被儲存在由儲存資源提供商(SRP)提供的單個公共儲存中
seo-description: As of AEM Communities 6.1, user generated content (UGC) is stored in a single, common store provided by a storage resource provider (SRP)
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# SRP — 社區內容儲存 {#srp-community-content-storage}

## 簡介 {#introduction}

從AEM Communities6.1開始，用戶生成的內容(UGC)被儲存在由儲存資源提供商(SRP)提供的單個公共儲存中。 SRP、MSRP和JSRP等SRP選項可供選擇。

與以前的版本不同，UGC在實例之間沒有反向/正向復AEM制。 相反，SRP使UGC可以直接訪問，以便從所有作者和發佈實例建立、讀取、更新和刪除(CRUD)操作，JSRP除外。

以下是 [每個SRP選項的特性](#characteristics-of-srp-options)SRP和SRP的選擇是決策過程的關鍵資訊 [基礎部署](/help/communities/topologies.md)。

有關UGC使用SRP的詳細資訊，請參見 [儲存資源提供程式概述](/help/communities/srp.md)。

>[!NOTE]
>
>SRP僅適用於社區內容。 它不影響站點內容的儲存位置([節點儲存](/help/sites-deploying/data-store-config.md))，並且不會影響用戶註冊、用戶配置檔案和實例之間的用戶組的安全AEM處理(另請參閱 [管理用戶資料](#managing-user-data))。

>[!CAUTION]
>
>截至AEM6.1 [UGC從未複製](#ugc-never-replicated)。
>
>當部署不包括公用儲存時，如預設 [JSRP](/help/communities/topologies.md#jsrp) 拓撲，UGC僅在其上輸AEM入的發佈或作者實例上可見。 僅當拓撲包含發佈群集時，UGC才在任何發佈實例上可見。

## SRP選項的特點 {#characteristics-of-srp-options}

[ASRP -Adobe儲存資源提供程式](/help/communities/asrp.md)

通過此選項，UGC將遠程保留在托管並由Adobe管理的雲服務中。 它需要額外的許可證，並與客戶代表合作為該特定許可證設定帳戶。 ASRP要求：

* 由Adobe提供並支援的關聯雲服務，用於儲存社區內容。
* 在特定地理位置（美國、 EMEA、APAC）選擇資料中心。

* 所有對UGC的寫程式訪問都通過SRP API。

ASRP適合：

* 用於TarMK發佈場。
* 當沒有投資本地儲存的意圖時。

>[!NOTE]
>
>將附件上載到ASRP中的帖子（或注釋）的限制為50 MB。

[MSRP - MongoDB儲存資源提供程式](/help/communities/msrp.md)

通過此選項，UGC直接保留在本地MongoDB實例中。

MSRP要求：

* 本地許可的MongoDB安裝，用於儲存社區內容。
* 本地安裝Apache Solr。
* 所有對UGC的寫程式訪問都通過SRP API。

ASRP適合：

* 用於現有TarMK發佈場。
* 用於MongoMK或RdbMK群集。
* 當需要大量社區內容時。

[DSRP — 關係資料庫儲存資源提供程式](/help/communities/dsrp.md)

使用此選項，UGC將直接保留在本地MySQL資料庫實例中。

DSRP要求：

* 本地安裝MySQL以儲存社區內容。
* 本地安裝Apache Solr。
* 所有對UGC的寫程式訪問都通過SRP API。

DSRP適合：

* 用於現有TarMK發佈場。
* 用於MongoMK或RdbMK群集。
* 當需要大量社區內容時。

[JSRP - JCR儲存資源提供程式](/help/communities/jsrp.md)

使用預設選項時，沒有公用儲存。 UGC僅保留在與輸入JCR的實AEM例相同的JCR儲存庫中。

JSRP:

* 將社區內容儲存在作者的JCRAEM儲存庫中，或將其發佈到的發佈實例中。
* 需要通過SRP API對UGC進行所有寫程式訪問。
* 如果部署了多個發佈實例，則需要發佈群集（TarMK場中的發佈實例之間沒有複製機制）。
* 審核僅在發佈環境中執行（作者和發佈之間沒有反向/正向複製機制）。
* 最適合於開發、演示和培訓。

## 配置SRP {#configuring-srp}

通過 [儲存配置控制台](/help/communities/srp-config.md)。

有關每個選項的配置詳細資訊，請參閱：

* [ASRP -Adobe儲存資源提供程式](/help/communities/asrp.md)
* [MSRP - MongoDB儲存資源提供程式](/help/communities/msrp.md)
* [DSRP — 關係資料庫儲存資源提供程式](/help/communities/dsrp.md)
* [JSRP - JCR儲存資源提供程式](/help/communities/jsrp.md)

如果未主動選擇儲存選項，則預設情況下會啟用JSRP。

## 其他資訊 {#additional-information}

### UGC從不複製 {#ugc-never-replicated}

在作者環境中，作者建立頁面內容並將其複製到發佈環境。 當頁面包括互動式AEM Communities功能（如注釋、評論、論壇、部落格或QnA）時，成員（在站點訪問者中籤名）對發佈實例的交互將導致用戶生成內容(UGC)在發佈環境中輸入。

以前，此社區內容被反向複製到作者實例，從作者複製到發佈實例。 在具有反向和正向複製的實AEM例之間保持一致性是有問題的。

從AEM Communities6.1開始，使用UGC的共用儲存消除了複製UGC的需要，如上所述。

在複製站點內容時， UGC從不複製。

### 管理用戶資料 {#managing-user-data}

共同體也感興趣 [*用戶*。 *用戶組*, *用戶配置檔案*](/help/communities/users.md)。 在發佈環境中建立和更新此用戶相關資料時，拓撲為 [發佈場](/help/sites-deploying/recommended-deploys.md#tarmk-farm)。

從AEM Communities6.1開始，使用Sling分發而不是複製來同步與用戶相關的資料。 有關詳細資訊，請訪問 [用戶同步](/help/communities/sync.md)。

### 升級到AEM Communities6.5 {#upgrading-to-aem-communities}

升級到AEM6.5社區時，如果需要保留現有的UGC，則應根據AEM5.6.1或AEM6.0社區是否使用了UGC的Adobe按需儲存或內部儲存採取步驟。

有關詳細資訊，請訪問 [升級到AEM Communities6.5](/help/communities/upgrade.md)。
