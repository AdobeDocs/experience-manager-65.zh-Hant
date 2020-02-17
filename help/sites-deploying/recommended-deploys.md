---
title: 建議的部署
seo-title: 建議的部署
description: 本文說明AEM的建議拓撲。
seo-description: 本文說明AEM的建議拓撲。
uuid: bc638121-c531-43eb-9ec6-3283a33519f8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 66d351e1-87f1-4006-bf8a-3cbbd33db9ed
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 建議的部署{#recommended-deployments}

>[!NOTE]
>
>本頁參考AEM的建議拓撲。 如需叢集功能及如何設定的詳細資訊，請參閱 [Apache Sling Discovery API檔案](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html)。

從AEM 6.2開始，MicroKernels就是永續性管理程式。選擇符合您需求的項目取決於您實例的用途以及您考慮的部署類型。

下列範例旨在指出他們在最常見AEM設定中的建議用途。

## 部署方案 {#deployment-scenarios}

### 單一TarMK實例 {#single-tarmk-instance}

在此案例中，單一TarMK執行個體會在單一伺服器上執行。

**這是作者例項的預設部署。**

![chlimage_1-15](assets/chlimage_1-15.png)

優點：

* 簡單
* 輕鬆維護
* 良好的效能

缺點是：

* 不能超出伺服器容量的限制
* 無故障切換容量

### TarMK冷備用 {#tarmk-cold-standby}

一個TarMK實例用作主實例。 主系統中的儲存庫被複製到備用故障切換系統。

冷備用機制也可用作備份，因為完整的儲存庫會不斷複製到故障切換伺服器。 故障轉移伺服器以冷備用模式運行，這意味著只運行實例的HttpReceiver。

![chlimage_1-16](assets/chlimage_1-16.png)

優點：

* 簡單
* 可維護性
* 效能
* 故障切換

缺點是：

* 不能超出伺服器容量的限制
* 大部分時間內，一個伺服器處於空閒狀態
* 故障切換不是自動的。 必須在外部檢測到它，故障切換系統才能開始服務請求。

>[!NOTE]
>
>如需如何使用TarMK Cold Standby設定AEM的詳細資訊，請參 [閱](/help/sites-deploying/tarmk-cold-standby.md) 本文。

>[!NOTE]
>
>此TarMK示例中的Cold Standby部署要求主實例和備用實例都分別獲得許可，因為故障切換伺服器會不斷複製。 如需授權的詳細資訊，請參閱 [Adobe一般授權條款](https://www.adobe.com/legal/terms/enterprise-licensing.html)。

### TarMK Farm {#tarmk-farm}

每個Oak例項會以一個TarMK例項執行。 TarMK儲存庫是獨立的，需要保持同步。

使儲存庫保持同步的前提是作者伺服器正在向每個群成員發佈相同的內容。 有關詳細資訊，請參 [閱複製](/help/sites-deploying/replication.md)。

對於AEM Communities，使用者產生的內容(UGC)不會複製。 如需支援TarMK農場的UGC，請參閱 [AEM Communities的考量事項](#considerations-for-aem-communities)。

**這是發佈環境的預設部署。**

![chlimage_1-17](assets/chlimage_1-17.png)

優點：

* 效能
* 讀取存取的可擴充性
* 故障切換

### 具有MongoMK故障切換功能的Oak Cluster在單個資料中心實現高可用性 {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

此方法表示在單一資料中心記憶體取MongoDB複製集的多個Oak例項，實際上為AEM作者環境建立作用中叢集。 MongoDB中的複製副本集用於在發生硬體或網路故障時提供高可用性和冗餘。

![chlimage_1-18](assets/chlimage_1-18.png)

優點：

* 可使用新的AEM作者例項水準縮放
* 資料層的高可用性、冗餘和自動故障切換

缺點是：

* 在某些情況下，效能可能低於TarMK

### Oak Cluster，具有跨多個資料中心的MongoMK故障切換 {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

此方法意味著多個Oak實例訪問跨多個資料中心的MongoDB複製副本集，實際上是為AEM作者環境建立活動——活動群集。 MongoDB複製具有多個資料中心，可提供相同的高可用性和冗餘，但現在還包括了處理資料中心停機的能力。

![oakclustermongofailover2datacenters](assets/oakclustermongofailover2datacenters.png)

優點：

* 可使用新的AEM作者例項水準縮放
* 資料層的高可用性、冗餘和自動故障切換（包括資料中心停機）

>[!NOTE]
>
>在上圖中，AEM Server 3和AEM Server 4會呈現非作用中狀態，假設資料中心2的AEM伺服器與資料中心1的MongoDB主節點之間有網路延遲，高於此處說明的 [要求](/help/sites-deploying/aem-with-mongodb.md#checklists)。 如果最大延遲與需求相容（例如透過使用可用區），則資料中心2中的AEM伺服器也可以是作用中的，以建立跨多個資料中心的作用中AEM叢集。

>[!NOTE]
>
>有關本節中介紹的MongoDB體系結構概念的其他資訊，請參見 [MongoDB複製](https://docs.mongodb.org/manual/replication/)。

## 微內核：其中一個 {#microkernels-which-one-to-use}

在兩個可用的微內核之間選擇時需要考慮的基本規則是TarMK是為效能而設計，而MongoMK是為可擴充性而設計。

您可以使用這些決策表來建立最適合您需求的部署類型。

Adobe強烈建議TarMK為所有部署案例（AEM Author和Publish執行個體）中客戶使用的預設永續性技術，但下列使用案例除外。

### 在作者例項上選擇AEM MongoMK而非TarMK的例外 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

選擇MongoMK持久性後端而非TarMK的主要原因是水準縮放實例。 這表示有兩個或兩個以上的活動作者實例始終運行，並使用MongoDB作為持久性儲存系統。 執行多個作者執行個體的需求，通常是因為單一伺服器的CPU和記憶體容量支援所有並行編寫活動，已不再持續。

在新網站上線後，幾乎無法預測確切的並行模式。 因此，Adobe建議您在評估是否使用MongoMK和兩個或兩個以上「作者」活動節點時，考慮下列准則：

1. 一天中連接的指名用戶數：數以千計。
1. 並行用戶數：數以百計。
1. 每日資產收錄量：數十萬甚至更多。
1. 每天編輯的頁數量：數以十萬計（例如透過多網站管理員或新聞摘要擷取的自動更新）。
1. 每日搜尋量：數以萬計甚至更多。

>[!NOTE]
>
>Tough Day can be used to evaluate the performance of the customer application in the context of the hardware configuration deployed. 有關此工具的詳細資訊，請 [參閱](/help/sites-developing/tough-day.md)。

使用MongoDB的最低部署通常涉及以下拓撲：

* 一個MongoDB複製副本集由一個主節點、兩個輔助節點組成，每個MongoDB實例在可用區中運行，每個節點的延遲低於15毫秒；
* 一個作者實例群集，其中一個領導節點、一個非領導節點，並且兩者始終處於活動狀態，每個作者實例在每個資料中心中運行，其中MongoDB主實例和輔助實例正在運行。

此外，強烈建議在共用檔案系統或Amazon S3上配置資料儲存，這樣資產或二進位檔案就不會儲存在MongoDB中。 這將確保部署中的最佳效能。

部署具有兩個或多個作者實例的群集的MongoDB複製副本集的額外好處之一是，在作者實例、MongoDB複製副本或完全資料中心故障的情況下，具有自動恢復情形，停機時間最短。 不過，選擇MongoMK而不是TarMK不應僅由恢復要求驅動，因為TarMK還可以提供具有受控故障切換機制的最短停機時間解決方案。

如果上述標準預期在部署的前18個月內未達成，建議您先使用TarMK部署AEM，然後在日後適用上述標準時重新評估您的設定，最後決定是要保留在TarMK上或移轉至MongoMK。

### 在發佈例項上選擇AEM MongoMK而非TarMK的例外 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

不建議為發佈例項部署MongoMK。 部署的發佈層幾乎總是部署為運行TarMK的完全獨立的發佈實例群，這些實例通過從作者實例複製內容保持同步。 此「無共用」架構適用於發佈例項，可讓發佈層的部署以線性方式水準縮放。 農場拓撲還提供了以滾動方式應用任何更新或升級來發佈實例的好處，這樣對發佈層的任何更改都不需要停機。

當發佈層有多個發佈者時，這不適用於使用MongoMK叢集的AEM Communities。 如果選擇JSRP(請參 [閱社群內容儲存](/help/communities/working-with-srp.md))，則MongoMK叢集將適合，與任何發佈端叢集一樣，不論選擇的MK如MongoDB或RDB。

### 使用MongoMK部署AEM時的必要條件與建議 {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

如果您正在考慮針對AEM部署MongoMK，則可使用一組先決條件和建議：

**MongoDB部署的必要先決條件：**

1. 在熟悉AEM的Adobe Consulting或MongoDB Architects的協助下，MongoDB部署架構和規模調整必須是專案實作的一部分；
1. MongoDB的專業知識必須存在於合作夥伴或客戶團隊中，以便有信心能夠維持和維護現有或新的MongoDB環境；
1. 您可以選擇部署MongoDB（AEM支援兩者）的商業版或開放原始碼版本，但必須直接向MongoDB Inc;
1. 整體AEM和MongoDB架構與基礎架構應由Adobe AEM Architect妥善定義與驗證；
1. 您必須檢閱包含MongoDB的AEM部署支援模型。

**MongoDB部署的強烈建議：**

* 請參閱MongoDB for Adobe Experience Manager文 [章](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager);
* 審查MongoDB生產核 [對表](https://docs.mongodb.org/manual/administration/production-checklist/);
* 參加MongoDB的認證課程，您可在此 [處](https://university.mongodb.com/)。

>[!NOTE]
>
>如需有關這些准則、必要條件和建議的其他問題，請聯絡 [Adobe客戶服務](https://helpx.adobe.com/marketing-cloud/contact-support.html)。

### AEM Communities的考量事項 {#considerations-for-aem-communities}

對於計畫部署 [AEM Communities的網站](/help/communities/overview.md)，建議您選擇最佳化的部 [署](/help/communities/working-with-srp.md#characteristicsofstorageoptions) ，以處理社群成員從發佈環境張貼的UGC。

使用通 [用商店](/help/communities/working-with-srp.md)，就不需要在作者和其他發佈例項之間複製UGC，即可獲得一致的UGC檢視。

以下是一組決策矩陣，可協助您選擇部署的最佳永續性類型：

#### 選擇作者例項的部署類型 {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### 選擇發佈實例的部署類型 {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB是協力廠商軟體，不包含在AEM授權套件中。 如需詳細資訊，請參 [閱MongoDB授權政策頁](https://www.mongodb.org/about/licensing/) 。
>
>為了充份運用您的AEM部署，Adobe建議您授權MongoDB企業版，以便從專業支援中獲益。
>
>該許可證包括一個標準副本集，該副本集由一個主實例和兩個輔助實例組成，可用於作者或發佈部署。
>
>如果您想要在MongoDB上執行作者和發佈，則需要購買兩個不同的授權。
>
>如需詳細資訊，請參 [閱Adobe Experience Manager專用的MongoDB頁面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。

