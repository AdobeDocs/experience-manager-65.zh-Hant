---
title: SRP —— 社群內容儲存
seo-title: SRP —— 社群內容儲存
description: 從AEM Communities6.1開始，用戶生成的內容(UGC)被儲存在由儲存資源提供商(SRP)提供的單個公共儲存中
seo-description: 從AEM Communities6.1開始，用戶生成的內容(UGC)被儲存在由儲存資源提供商(SRP)提供的單個公共儲存中
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---


# SRP —— 社區內容儲存{#srp-community-content-storage}

## 簡介 {#introduction}

從AEM Communities6.1開始，用戶生成的內容(UGC)被儲存在由儲存資源提供商(SRP)提供的單個公共儲存中。 有幾種SRP選項可供選擇，例如ASRP、MSRP和JSRP。

與舊版不同，UGC在實例間沒有反向／正向復AEM制。 SRP可讓UGC直接存取，以便從所有作者和發佈例項建立、讀取、更新和刪除(CRUD)作業，但JSRP除外。

以下是每個SRP選項的[特性，這是選擇適當的SRP和[基礎部署時決策過程的關鍵資訊。](#characteristics-of-srp-options)](/help/communities/topologies.md)

有關UGC使用SRP的詳細資訊，請參見[儲存資源提供方概述](/help/communities/srp.md)。

>[!NOTE]
>
>SRP僅適用於社群內容。 它不會影響網站內容的儲存位置([node store](/help/sites-deploying/data-store-config.md))，也不會影響在例項之間對使用者註冊、使用者個人檔案和使用者群組的安全處理AEM（另請參閱[管理使用者資料](#managing-user-data)）。

>[!CAUTION]
>
>從AEM6.1開始，[UGC不會複製](#ugc-never-replicated)。
>
>當部署不包含公用商店（例如預設的[JSRP](/help/communities/topologies.md#jsrp)拓撲）時，UGC只會顯示在其上輸入的AEM發佈或作者實例上。 只有當拓撲包含發佈群集時，UGC才會顯示在任何發佈實例上。

## SRP選項{#characteristics-of-srp-options}的特點

[ASRP -Adobe儲存資源提供方](/help/communities/asrp.md)

使用此選項，UGC會在由Adobe托管和管理的雲端服務中遠程保存。 它需要額外的授權，並與帳戶代表合作為該特定授權提供帳戶。 ASRP要求：

* 由Adobe提供並支援的相關雲端服務，以儲存社群內容。
* 在特定地理位置（美國、歐洲、中東和非洲、亞太地區）選擇資料中心。

* UGC的所有程式化存取皆可透過SRP API。

ASRP適合：

* 適用於TarMK發佈農場。
* 當沒有投資本地儲存的意圖時。

>[!NOTE]
>
>ASRP中的貼文（或留言）上傳附件的限制為50 MB。

[MSRP - MongoDB儲存資源提供程式](/help/communities/msrp.md)

使用此選項，UGC會直接保存在本地MongoDB實例中。

MSRP需要：

* 本機授權安裝的MongoDB可儲存社群內容。
* 本機安裝Apache Solr。
* UGC的所有程式化存取皆可透過SRP API。

ASRP適合：

* 適用於現有的TarMK發佈農場。
* 用於MongoMK或RdbMK群集。
* 當需要大量社群內容時。

[DSRP —— 關係資料庫儲存資源提供程式](/help/communities/dsrp.md)

使用此選項，UGC將直接保存在本地MySQL資料庫實例中。

DSRP要求：

* 本地安裝MySQL以儲存社區內容。
* 本機安裝Apache Solr。
* UGC的所有程式化存取皆可透過SRP API。

DSRP適合：

* 適用於現有的TarMK發佈農場。
* 用於MongoMK或RdbMK群集。
* 當需要大量社群內容時。

[JSRP - JCR儲存資源提供商](/help/communities/jsrp.md)

使用預設選項時，沒有共用商店。 UGC僅與輸入UGC的實例保存在AEM相同的JCR儲存庫中。

JSRP:

* 將社群內容儲存在作者的JCR儲存AEM庫或發佈執行個體中。
* 需要透過SRP API以程式化方式存取UGC。
* 如果部署了多個發佈實例，則需要發佈群集（TarMK場中的發佈實例之間沒有複製機制）。
* 協調僅在發佈環境中執行（作者和發佈之間沒有反向／正向複製機制）。
* 最適合開發、展示和培訓。

## 配置SRP {#configuring-srp}

根據基礎部署指定預設儲存選項是通過[儲存配置控制台](/help/communities/srp-config.md)進行的。

如需每個選項的設定詳細資訊，請參閱：

* [ASRP -Adobe儲存資源提供方](/help/communities/asrp.md)
* [MSRP - MongoDB儲存資源提供程式](/help/communities/msrp.md)
* [DSRP —— 關係資料庫儲存資源提供程式](/help/communities/dsrp.md)
* [JSRP - JCR儲存資源提供商](/help/communities/jsrp.md)

如果未主動選擇儲存選項，則預設啟用JSRP。

## 其他資訊 {#additional-information}

### UGC從不複製{#ugc-never-replicated}

在作者環境中，作者會建立頁面內容並將它複製至發佈環境。 當頁面包含互動式AEM Communities功能（例如註解、評論、論壇、部落格或QnA）時，成員（在網站訪客中登入）對發佈例項的互動會導致使用者產生的內容(UGC)進入發佈環境。

以前，此社群內容會反向複製至作者例項，以及從作者複製至發佈例項。 在具有反向和正向複製的實例之間AEM保持一致性存在問題。

從AEM Communities6.1開始，通過使用UGC的共用儲存，已消除了複製UGC的需要，如上所述。

在複製網站內容時，不會複製UGC。

### 管理用戶資料{#managing-user-data}

CommunitIes也感興趣的是&#x200B;[*用戶*、*用戶組*&#x200B;和&#x200B;*用戶配置檔案*](/help/communities/users.md)。 當拓撲為[publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm)時，在發佈環境中建立和更新此用戶相關資料時，需要將其提供給其他發佈實例。

自AEM Communities6.1起，使用者相關資料會使用Sling散發來同步化，而非複製。 有關詳細資訊，請訪問[用戶同步](/help/communities/sync.md)。

### 升級至AEM Communities6.5 {#upgrading-to-aem-communities}

在升級至AEM6.5社群時，如果需要保留現有的UGC，則應根據AEM5.6.1或AEM6.0社群是否使用Adobe隨選儲存或UGC的內部部署儲存來採取步驟。

如需詳細資訊，請造訪[升級至AEM Communities6.5](/help/communities/upgrade.md)。
