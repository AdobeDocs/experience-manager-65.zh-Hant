---
title: 建議的部署
seo-title: Recommended Deployments
description: 本文介紹推薦的拓撲AEM。
seo-description: This article describes the recommended topologies for AEM.
uuid: bc638121-c531-43eb-9ec6-3283a33519f8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 66d351e1-87f1-4006-bf8a-3cbbd33db9ed
docset: aem65
exl-id: baec7fc8-d48c-4bc6-b12b-4bf4eff695ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 0%

---

# 建議的部署{#recommended-deployments}

>[!NOTE]
>
>本頁指推薦的拓撲AEM。 有關群集功能以及如何配置這些功能的詳細資訊，請參見 [Apache Sling Discovery API文檔](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html)。

從6.2開始，MicroKernels充當持AEM久性管理器。根據實例的用途和您考慮的部署類型來選擇適合您需要的部署類型。

以下示例旨在說明它們在最常見的設定中推薦使用的AEM用途。

## 部署方案 {#deployment-scenarios}

### 單個TarMK實例 {#single-tarmk-instance}

在此情況下，單個TarMK實例在單個伺服器上運行。

**這是作者實例的預設部署。**

![chlimage_1-15](assets/chlimage_1-15.png)

優點：

* 簡單
* 易於維護
* 效能良好

缺點：

* 無法擴展到超過伺服器容量限制
* 無故障轉移容量

### TarMK冷備用 {#tarmk-cold-standby}

一個TarMK實例用作主實例。 將主系統的儲存庫複製到備用故障切換系統。

冷備用機制也可以用作備份，因為整個儲存庫會不斷複製到故障切換伺服器。 故障轉移伺服器在冷備用模式下運行，這意味著只運行實例的HttpReceiver。

![chlimage_1-16](assets/chlimage_1-16.png)

優點：

* 簡潔
* 可維護性
* 效能
* 故障轉移

缺點：

* 無法擴展到超過伺服器容量限制
* 大多數情況下，一台伺服器處於空閒狀態
* 故障轉移不是自動的。 必須先從外部檢測它，然後故障切換系統才能開始提供請求服務。

>[!NOTE]
>
>有關如何配置TarMK冷備AEM用的詳細資訊，請參見 [這個](/help/sites-deploying/tarmk-cold-standby.md) 文章。

>[!NOTE]
>
>此TarMK示例中的冷備用部署要求主實例和備用實例都分別獲得許可，因為故障切換伺服器的複製是恆定的。 有關許可的詳細資訊，請參考 [Adobe一般許可條款](https://www.adobe.com/legal/terms/enterprise-licensing.html)。

### TarMK場 {#tarmk-farm}

每個Oak實例都使用一個TarMK實例運行。 TarMK儲存庫是獨立的，需要保持同步。

使儲存庫保持同步的前提是作者伺服器正在向每個場成員發佈相同的內容。 有關詳細資訊，請參見 [複製](/help/sites-deploying/replication.md)。

對於AEM Communities，用戶生成的內容(UGC)從不被複製。 有關在TarMK場上支援UGC的資訊，請參見 [對AEM Communities的考慮](#considerations-for-aem-communities)。

**這是發佈環境的預設部署。**

![chlimage_1-17](assets/chlimage_1-17.png)

優點：

* 效能
* 可擴展的讀訪問
* 故障轉移

### 具有MongoMK故障轉移的Oak群集，在單個資料中心實現高可用性 {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

此方法意味著多個Oak實例訪問單個資料中心內的一個MongoDB複製副本集，這實際上為作者環境建立了一個活動AEM群集。 MongoDB中的複製副本集用於在出現硬體或網路故障時提供高可用性和冗餘。

![chlimage_1-18](assets/chlimage_1-18.png)

優點：

* 能夠使用新作者實例水準AEM縮放
* 資料層的高可用性、冗餘和自動故障切換

缺點：

* 某些情況下，效能可能低於TarMK

### Oak群集，具有跨多個資料中心的MongoMK故障切換 {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

此方法意味著多個Oak實例跨多個資料中心訪問一個MongoDB複製副本集，實際上為作者環境建立了一個活動 — 活AEM動群集。 MongoDB複製具有多個資料中心，可提供相同的高可用性和冗餘，但現在包括處理資料中心停機的能力。

![oakclustermongofailover2datacenters](assets/oakclustermongofailover2datacenters.png)

優點：

* 能夠使用新作者實例水準AEM縮放
* 資料層的高可用性、冗餘和自動故障切換（包括資料中心停機）

>[!NOTE]
>
>在上圖中，AEM Server 3和AEMServer 4處於非活動狀態，假定資料中心2中的伺服器與資料中心1中的AEMMongoDB主節點之間的網路延遲高於記錄的要求 [這裡](/help/sites-deploying/aem-with-mongodb.md#checklists)。 如果最大延遲與要求相容，則資料中心2中的伺服器也可以處於活動狀態AEM，從而跨多個資料中心建立活動 — AEM活動群集。

>[!NOTE]
>
>有關本節中介紹的MongoDB體系結構概念的其他資訊，請參見 [MongoDB複製](https://docs.mongodb.org/manual/replication/)。

## 微內核：一個 {#microkernels-which-one-to-use}

在兩個可用的微內核之間進行選擇時需要考慮的基本規則是TarMK是為效能而設計的，而MongoMK是為可擴充性而設計的。

您可以使用這些決策清單來確定適合您要求的最佳部署類型。

Adobe強烈建議將TarMK作為所有部署方案（AEM Author和Publish實例）中客戶使用的預設持久性技術，但下面概述的使用案例除外。

### 在作者實AEM例上選擇MongoMK而不是TarMK的例外 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

選擇MongoMK持久性後端(TarMK)的主要原因是橫向縮放實例。 這意味著有兩個或兩個以上活動的作者實例始終運行，並將MongoDB用作持久性儲存系統。 需要運行多個作者實例通常是因為單個伺服器的CPU和記憶體容量（支援所有併發創作活動）不再可持續。

幾乎無法預測新網站投入使用後的準確併發模型。 因此，Adobe建議在評估是否使用MongoMK和兩個或多個「作者」活動節點時考慮以下標準：

1. 一天中連接的指定用戶數：數以千計。
1. 併發用戶數：數以百計甚至更多。
1. 每天資產接收量：數十萬甚至更多。
1. 每天編輯的頁數：數以十萬計甚至更多（包括通過多站點管理器或新聞源接收的自動更新）。
1. 每天的搜索量：數以萬計甚至更多。

>[!NOTE]
>
>在部署硬體配置的上下文中，可以使用「艱難的一天」來評估客戶應用程式的效能。 有關此工具的詳細資訊 [這裡](/help/sites-developing/tough-day.md)。

使用MongoDB的最小部署通常涉及以下拓撲：

* 由一個主節點、兩個輔助節點組成的MongoDB複製副本集，每個MongoDB實例在可用區域中運行，每個節點的延遲低於15毫秒；
* 一個作者實例群集，其中一個領導節點、一個非領導節點並且兩者始終處於活動狀態，每個作者實例在每個資料中心中運行，其中MongoDB主實例和次實例正在運行。

此外，強烈建議在共用檔案系統或AmazonS3上配置資料儲存，以便資產或二進位檔案不儲存在MongoDB中。 這將確保部署內的最佳效能。

使用包含兩個或多個作者實例的群集部署MongoDB複製副本集的額外好處之一是，在作者實例、MongoDB複製副本或整個資料中心出現故障時，具有自動恢複方案，停機時間最小。 儘管如此，選擇MongoMK而不是TarMK不應僅由恢復要求驅動，因為TarMK還可以通過受控故障轉移機制提供最小停機時間解決方案。

如果預計在部署的頭18個月中不能滿足上述標準，則建議您首先使用AEMTarMK進行部署，然後在以後應用上述標準時重新評估您的配置，最後確定是保留在TarMK上還是遷移到MongoMK。

### 在發佈實例AEM上選擇MongoMK而不是TarMK的例外 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

建議不要為發佈實例部署MongoMK。 部署的發佈層幾乎總是部署為運行TarMK的完全獨立的發佈實例的場，這些實例通過從作者實例複製內容而保持同步。 此「無共用」體系結構適用於發佈實例，允許發佈層的部署以線性方式水準擴展。 伺服器場拓撲還提供了以滾動方式應用任何更新或升級來發佈實例的好處，這樣對發佈層的任何更改都不需要任何停機。

這不適用於在發佈層上使用MongoMK群集的AEM Communities，只要有多個發佈者。 如果選擇JSRP(請參見 [社區內容儲存](/help/communities/working-with-srp.md))，則MongoMK群集將是合適的，任何發佈側群集也是如此，而不管選擇的MK如MongoDB或RDB。

### 必備元件和RecommendationsAEM在部署MongoMK時 {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

如果您正在考慮MongoMK部署，則可以提供一組先決條件和建AEM議：

**MongoDB部署的必備元件：**

1. MongoDB部署體系結構和規模調整必須在Adobe咨詢或熟悉MongoDB架構師的幫助下成為項目實施的一AEM部分；
1. MongoDB的專業知識必須在合作夥伴或客戶團隊中存在，以便有信心能夠維持和維護現有的或新的MongoDB環境；
1. 您可以選擇部署商業版或開放源版本的MongoDB(AEM同時支援兩者)，但必須直接從MongoDB公司購買MongoDB維護和支援合同；
1. 總體AEM和MongoDB體系結構和基礎架構應由Adobe架構師進行詳細定義和AEM驗證；
1. 必須查看包含MongoDB的AEM部署的支援模型。

**針對MongoDB部署的強項建議：**

* 請咨詢MongoDB以瞭解Adobe Experience Manager [文章](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager);
* 查看MongoDB生產 [清單](https://docs.mongodb.org/manual/administration/production-checklist/);
* 參加MongoDB上的認證課，可聯機使用 [這裡](https://university.mongodb.com/)。

>[!NOTE]
>
>有關這些准則、先決條件和建議的所有其他問題，請聯繫 [Adobe客戶關懷](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html)。

### 關於AEM Communities的考慮 {#considerations-for-aem-communities}

針對計畫部署的站點 [AEM Communities](/help/communities/overview.md)，建議 [選擇部署](/help/communities/working-with-srp.md#characteristicsofstorageoptions) 已優化，用於處理由社區成員從發佈環境中發佈的UGC。

使用 [普通商店](/help/communities/working-with-srp.md),UGC不需要在作者和其他發佈實例之間複製，以便獲得UGC的一致視圖。

下面是一組可幫助您為部署選擇最佳持久性類型的決策矩陣：

#### 為作者實例選擇部署類型 {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### 選擇發佈實例的部署類型 {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB是第三方軟體，不包括在許AEM可包中。 有關詳細資訊，請參閱 [MongoDB許可策略](https://www.mongodb.org/about/licensing/) 的子菜單。
>
>為了充分利用您的部署AEM,Adobe建議授予MongoDB Enterprise版本許可，以便從專業支援中獲益。
>
>許可證包括標準副本集，該副本集由一個主實例和兩個輔助實例組成，這些實例可用於作者或發佈部署。
>
>如果您希望同時運行作者並在MongoDB上發佈，則需要購買兩個單獨的許可證。
>
>有關詳細資訊，請參見 [用於Adobe Experience Manager的MongoDB頁](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。
