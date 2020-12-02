---
title: AEM與MongoDB
seo-title: AEM與MongoDB
description: 瞭解成功部署MongoDB的AEM所需的工作和考量事項。
seo-description: 瞭解成功部署MongoDB的AEM所需的工作和考量事項。
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
translation-type: tm+mt
source-git-commit: 56006a1f49e4d357cd7ee44a4a1dd1af7189e70a
workflow-type: tm+mt
source-wordcount: '6513'
ht-degree: 0%

---


# AEM with MongoDB{#aem-with-mongodb}

本文旨在改善有關成功部署Adobe Experience Manager with MongoDB所需工作和考量事項的知識。

有關部署的詳細資訊，請參閱文檔的[部署和維護](/help/sites-deploying/deploy.md)部分。

## 何時將MongoDB與AEM {#when-to-use-mongodb-with-aem}搭配使用

MongoDB通常用於支援符合下列條件之一的AEM作者部署：

* 每天有超過1000位不重複使用者；
* 100多名併發用戶；
* 大量的頁面編輯；
* 大量推展或啟動。

上述條件僅適用於作者例項，而不適用於所有應以TarMK為基礎的發佈例項。 使用者數量是指已驗證的使用者，因為作者例項不允許未驗證的存取。

如果未滿足標準，則建議使用TarMK活動／備用部署來解決可用性問題。 通常，在擴展要求比單個硬體項目所能達到的要大的情況下，應考慮MongoDB。

>[!NOTE]
>
>有關作者實例大小和併發用戶定義的其他資訊，請參閱[硬體大小指南](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel)。

### AEM {#minimal-mongodb-deployment-for-aem}的最小MongoDB部署

以下是AEM在MongoDB上的最低部署。 為簡單起見，SSL終止和HTTP Proxy元件已推廣。 它由一個MongoDB複製副本集組成，具有一個主映像和兩個輔助映像。

![chlimage_1-4](assets/chlimage_1-4.png)

最小部署需要配置為複製副本集的3個`mongod`實例。 一個實例將被選為主實例，而另一個實例將被選為輔助實例，其選舉由`mongod`管理。 連接到每個實例的是本地磁碟。 為了使群集支援負載，建議最低吞吐量為12MB/s，每秒I/O操作數超過3000次(IOPS)。

AEM作者會連線至`mongod`例項，而每個AEM作者會連線至所有三個`mongod`例項。 寫入被發送到主實例，讀取可從任意實例讀取。 流量是根據分派器將流量載入至任一個作用中AEM作者例項來分發。 OAK資料存放區是`FileDataStore`，而MongoDB監控則由MMS或MongoDB Ops Manager提供，視部署位置而定。 作業系統級別和日誌監控由Splunk或Ganglia等第三方解決方案提供。

在此部署中，所有元件都是成功實作的必要條件。 任何遺失的元件都會使實施無法運作。

### 作業系統{#operating-systems}

如需AEM 6支援的作業系統清單，請參閱[技術需求頁面](/help/sites-deploying/technical-requirements.md)。

### 環境 {#environments}

支援虛擬化環境，前提是運行項目的不同技術團隊之間有良好的溝通。 這包括運行AEM的團隊、擁有作業系統的團隊以及管理虛擬化基礎架構的團隊。

MongoDB實例的I/O容量有特定要求，需要由管理虛擬化環境的團隊管理。 如果項目使用雲部署（如Amazon Web Services），則需要為實例提供足夠的I/O容量和一致性以支援MongoDB實例。 否則，MongoDB進程和Oak儲存庫將不可靠且不可靠地執行。

在虛擬化環境中， MongoDB將需要特定的I/O和VM配置，以確保MongoDB的儲存引擎不受VMWare資源分配策略的限制。 成功的實施將確保各個團隊之間沒有障礙，而且所有團隊都已註冊，以提供所需的效能。

## 硬體注意事項{#hardware-considerations}

### 儲存 {#storage}

為了實現最佳效能的讀寫吞吐量，而不需要過早的水準擴展，MongoDB通常需要SSD儲存或與SSD相當的效能儲存。

### RAM {#ram}

使用MMAP儲存引擎的MongoDB 2.6和3.0版要求資料庫及其索引的工作集與RAM相配合。

RAM不足將導致效能顯著降低。 工作集和資料庫的大小高度依賴於應用程式。 雖然您可進行一些估計，但決定所需RAM量的最可靠方式是建立AEM應用程式並進行負載測試。

為了幫助進行負載測試，可以假定工作集與總資料庫大小的比率如下：

* 1:10用於SSD儲存
* 硬碟儲存的1:3

這表示在部署SSD時，2TB的資料庫需要200GB的記憶體。

雖然MongoDB 3.0中的WiredTiger儲存引擎也受到同樣的限制，但工作集、RAM和頁故障之間的關聯性不如WiredTiger不像MMAP儲存引擎那樣使用記憶體映射。

>[!NOTE]
>
>Adobe建議使用WiredTiger儲存引擎，以用於使用MongoDB 3.0的AEM 6.1部署。

### 資料儲存{#data-store}

由於MongoDB工作集限制，強烈建議維護資料儲存獨立於MongoDB。 在大多數環境中，應使用`FileDataStore`來使用所有AEM實例都可用的NAS。 對於使用Amazon Web Services的情況，也有`S3 DataStore`。 如果由於任何原因，資料儲存在MongoDB中，則應將資料儲存的大小添加到資料庫總大小中，並適當調整工作集計算。 這可能意味著要配置更多的RAM以保持效能而不發生頁面故障。

## 監控 {#monitoring}

監測對項目的成功實施至關重要。 雖然具備充份的知識，您仍可在MongoDB上執行AEM，而不需進行監控，但這些知識通常可在專門負責部署每個部分的工程師中找到。

這通常包括Apache Oak Core的研發工程師和MongoDB專員。

若未在所有層級進行監控，則需要詳細瞭解程式碼庫才能診斷問題。 隨著對主要統計資料的監測和適當的指導，執行小組將能夠對異常情況作出適當反應。

雖然可以使用命令行工具快速獲取群集操作的快照，但在許多主機上即時執行該操作幾乎是不可能的。 命令列工具很少會提供幾分鐘以上的歷史資訊，也絕不允許不同類型的量度產生交叉關聯。 在短暫的慢背景`mongod`同步期間，需要大量的手動操作來關聯I/O等待或對來自看似未連接的虛擬機的共用儲存資源的過多寫入級別。

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager是MongoDB提供的免費服務，允許監控和管理MongoDB實例。 它可即時查看MongoDB集群的效能和運行狀況。 它可管理雲和私人托管實例，前提是實例可以訪問Cloud Manager監控伺服器。

它要求在MongoDB實例上安裝一個連接到監控伺服器的代理。 代理程式有3個級別：

* 一種自動化代理，可完全自動化MongoDB伺服器上的所有功能，
* 可監視`mongod`實例的監視代理，
* 可執行資料定時備份的備份代理。

雖然使用Cloud Manager實現MongoDB群集的維護自動化使許多例行任務變得更輕鬆，但它不是必需的，也不是將它用於備份。 當選擇Cloud Manager進行監控時，需要進行監控。

有關MongoDB Cloud Manager的詳細資訊，請參閱[MongoDB文檔](https://docs.cloud.mongodb.com/)。

### MongoDB操作管理器{#mongodb-ops-manager}

MongoDB Ops Manager與MongoDB Cloud Manager是相同的軟體。 在註冊後，Ops Manager可以在本地下載並安裝到專用資料中心，或者安裝到任何其他筆記型電腦或台式機上。 它使用本地MongoDB資料庫來儲存資料，並以與Cloud Manager完全相同的方式與受控伺服器通信。 如果您有禁止監視代理的安全策略，則應使用MongoDB Ops Manager。

### 作業系統監視{#operating-system-monitoring}

需要執行作業系統層級監控才能執行AEM MongoDB叢集。

Ganglia是這樣一個系統的一個很好的例子，它提供了所需資訊的範圍和細節，這些資訊超出了CPU、平均負載和可用磁碟空間等基本健康指標。 要診斷問題，需要較低級別的資訊，如熵池級別、CPU I/O等待、FIN_WAIT2狀態的套接字。

### 日誌聚合{#log-aggregation}

對於多台伺服器的群集，集中日誌聚合是生產系統的需要。 像Splunk這樣的軟體支援日誌聚合，並允許團隊分析應用程式的行為模式，而無需手動收集日誌。

## 檢查清單{#checklists}

本節說明您應採取的各種步驟，以確保在實作專案之前，已正確設定您的AEM和MongoDB部署。

### 網路{#network}

1. 首先，請確定所有主機都有DNS項目
1. 所有主機都應通過其DNS條目從所有其它可路由主機中解析
1. 所有MongoDB主機都可通過同一群集中所有其他MongoDB主機進行路由
1. MongoDB主機可以將資料包路由到MongoDB Cloud Manager和其他監視伺服器
1. AEM Servers可將封包路由至所有MongoDB伺服器
1. 任何AEM伺服器與任何MongoDB伺服器之間的封包延遲都小於兩毫秒，不會造成封包遺失，標準散發時間也不超過一毫秒。
1. 確保AEM和MongoDB伺服器之間不超過兩跳
1. 兩個MongoDB伺服器之間不超過兩跳
1. 任何核心伺服器（MongoDB或AEM或任何組合）之間沒有高於OSI Level 3的路由器。
1. 如果使用VLAN中繼或任何形式的網路隧道，則必須符合資料包延遲檢查。

### AEM Configuration {#aem-configuration}

#### 節點儲存配置{#node-store-configuration}

AEM例項必須設定為搭配MongoMK使用AEM。 AEM中MongoMK實作的基礎是Document Node Store。

如需如何設定節點儲存區的詳細資訊，請參閱[在AEM中設定節點儲存區和資料儲存區。](/help/sites-deploying/data-store-config.md)

以下是Document Node Store配置的示例，用於最小的MongoDB部署：

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore e.g. FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

其中：

* `mongodburi`
這是MongoDB伺服器AEM需要連線到的。將連接到預設複製副本集的所有已知成員。 如果使用MongoDB Cloud Manager，則會啟用伺服器安全性。 因此，連接字串必須包含合適的用戶名和密碼。 非企業版MongoDB僅支援用戶名和密碼驗證。 有關連接字串語法的詳細資訊，請參閱[documentation](https://docs.mongodb.org/manual/reference/connection-string/)。

* `db`
資料庫的名稱。AEM的預設值為 
`aem-author`。

* `customBlobStore`
如果部署將二進位檔案儲存在資料庫中，則它們將構成工作集的一部分。因此，建議您不要在MongoDB中儲存二進位檔，並提供類似 
`FileSystem` NAS上的資料儲存。

* `cache`
快取大小(MB)。這會分佈於 
`DocumentNodeStore`.預設為256MB。 不過，Oak讀取效能將受益於更大的快取。

* `blobCacheSize`
AEM可能會快取常用的blob，以避免從資料存放區重新擷取。這將對效能產生更大的影響，尤其是在MongoDB資料庫中儲存blob時。 所有基於檔案系統的資料儲存都將受益於作業系統級別的磁碟快取。

#### 資料儲存配置{#data-store-configuration}

「資料儲存區」用來儲存大於臨界值的檔案。 在該閾值以下，檔案將作為屬性儲存在Document Node Store中。 如果使用`MongoBlobStore`，則在MongoDB中會建立專用的系列來儲存blob。 此集合有助於`mongod`實例的工作集，並且要求`mongod`擁有更多RAM以避免效能問題。 因此，建議的設定是避免生產部署使用`MongoBlobStore`，並使用由所有AEM執行個體共用的NAS所支援的`FileDataStore`。 由於作業系統級快取在管理檔案方面非常有效，因此應將磁碟上檔案的最小大小設定為接近磁碟的塊大小，以便高效地使用檔案系統，並且許多小文檔不會過多地貢獻於`mongod`實例的工作集。

以下是使用MongoDB進行最少AEM部署的典型Data Store配置：

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
# The minimum size of an object that should be stored in this data store.
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```

其中：

* `minRecordLength`
大小（以位元組為單位）。小於或等於此大小的二進位檔案將儲存在Document Node Store中。 儲存二進位檔案的內容，而不是儲存二進位檔案的ID。 對於大於此大小的二進位檔案，二進位檔案的ID將作為Document屬性儲存在節點集合中，而二進位檔案的主體將儲存在 
`FileDataStore` 在磁碟上。4096位元組是典型的檔案系統塊大小。

* `path`
資料儲存的根路徑。若是MongoMK部署，這必須是可供所有AEM例項使用的共用檔案系統。 通常使用網路連接儲存(NAS)伺服器。 對於雲端部署，例如Amazon Web Services, 
`S3DataFileStore` 的下界。

* `cacheSizeInMB`
二進位快取的總大小（兆位元組）。它用於快取小於 
`maxCacheBinarySize` 的雙曲餘切值。

* `maxCachedBinarySize`
二進位快取中快取的二進位檔案的最大大小（以位元組為單位）。如果使用以檔案系統為基礎的資料存放區，則不建議對資料存放區快取使用高值，因為作業系統已快取二進位檔。

#### 禁用查詢提示{#disabling-the-query-hint}

建議您通過添加屬性來禁用隨所有查詢一起發送的查詢提示

`-Doak.mongo.disableIndexHint=true`

啟動AEM時。 這樣，MongoDB將根據內部統計資料計算最合適的索引。

如果查詢提示未停用，索引的任何效能調整都不會影響AEM的效能。

#### 為MongoMK {#enable-persistent-cache-for-mongomk}啟用永久快取

建議為MongoDB部署啟用永久快取配置，以便為具有高I/O讀取效能的環境提供最大速度。 如需詳細資訊，請參閱[Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html)。

## MongoDB作業系統優化{#mongodb-operating-system-optimizations}

### 作業系統支援{#operating-system-support}

MongoDB 2.6使用對RAM和磁碟之間作業系統級別管理的某些方面敏感的記憶體映射儲存引擎。 查詢和讀取MongoDB實例的效能依賴於避免或消除通常稱為頁面故障的慢速I/O操作。 這些頁面錯誤尤其適用於`mongod`進程。 不應將它們與作業系統級別的頁面錯誤混淆。

為了快速操作，MongoDB資料庫只應訪問已在RAM中的資料。 它需要訪問的資料由索引和資料組成。 此索引和資料集合稱為工作集。 當工作集大於可用RAM時，MongoDB必須從磁碟將該資料頁入，從而導致I/O成本，從而驅逐已在記憶體中的其他資料。 如果遷出導致從磁碟頁故障中重新載入資料，將佔主導地位，效能將降低。 當工作集為動態和變數時，支援操作將產生更多的頁面故障。

MongoDB可在多種作業系統上執行，包括多種Linux風格、Windows和Mac OS。 如需詳細資訊，請參閱[https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms)。 MongoDB有不同的作業系統層級建議，視您的作業系統選擇而定。 有關[https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration)的說明，請在此摘述，以方便您使用。

#### Linux {#linux}

* 關閉透明頁面和碎片整理。 如需詳細資訊，請參閱[透明巨型頁面設定](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/)。
* [調整儲存數](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 據庫檔案的設備的預讀設定，以適應您的使用案例。

   * 對於MMAPv1儲存引擎，如果您的工作集大於可用的RAM，且檔案存取模式是隨機的，請考慮將預先讀取數降低至32或16。 評估不同的設定，以找出最佳值，最大化駐留記憶體並降低頁面錯誤數。
   * 對於WiredTiger儲存引擎，無論儲存介質類型（旋轉、SSD等）如何，都可將讀前置設定為0。 一般而言，請使用建議的預先讀取設定，除非測試顯示較高的預讀取取取值可衡量、可重複且可靠的優點。 [MongoDB專業版支](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 持可以就非零預讀配置提供建議和指導。

* 如果您在虛擬環境中運行RHEL 7 / CentOS 7，請禁用調整的工具。
* 當RHEL 7 / CentOS 7在虛擬環境中運行時，調整的工具會自動調用從效能吞吐量派生的效能配置檔案，該效能配置檔案會自動將預讀設定設定為4MB。 這會對效能造成負面影響。
* 使用SSD驅動器的節點或期限磁碟調度程式。
* 在來賓VM中使用用於虛擬化驅動器的noop磁碟調度程式。
* 禁用NUMA或將vm.zone_recalim_mode設定為0，並運行具有節點交織功能的[mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead)實例。 請參閱：[MongoDB和NUMA硬體](https://docs.mongodb.com/manual/administration/production-notes/#readahead)以瞭解詳細資訊。

* 調整硬體上的上限值，以符合您的使用案例。 如果多個[mongod](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod)或[mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos)例項在同一個用戶下運行，請相應地縮放ulimit值。 請參閱：[UNIX上限設定](https://docs.mongodb.com/manual/reference/ulimit/)以瞭解詳細資訊。

* 對[dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath)掛載點使用noatime。
* 為部署配置足夠的檔案句柄(fs.file-max)、內核pid限制(kernel.pid_max)和每個進程的最大線程(kernel.threads-max)。 對於大型系統，以下值提供了良好的起點：

   * fs.file-max值98000,
   * kernel.pid_max值64000,
   * andkernel.threads-max值64000

* 確保系統已配置交換空間。 請參閱作業系統檔案，以取得適當調整大小的詳細資訊。
* 確保系統預設的TCP keepalive設定正確。 值300通常為複製副本集和共用的群集提供更好的效能。 請參閱：[TCP keepalive時間是否會影響MongoDB部署？](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) 中，以取得詳細資訊。

#### Windows {#windows}

* 考慮禁用NTFS的「上次訪問時間」更新。 這類似於在類似Unix的系統上禁用atime。

### WiredTiger {#wiredtiger}

自MongoDB 3.2起，MongoDB的預設儲存引擎是WiredTiger儲存引擎。 此引擎提供許多強穩和可擴充的功能，使其更適合於所有一般資料庫工作負載。 以下各節將說明這些功能。

#### 文檔級併發{#document-level-concurrency}

WiredTiger使用檔案層級的並行控制來執行寫入作業。 因此，多個用戶端可同時修改系列的不同檔案。

對於大多數的讀寫操作，WiredTiger使用樂觀的並行控制。 WiredTiger在全球、資料庫和系列層級僅使用意圖鎖。 當儲存引擎檢測到兩個操作之間的衝突時，一個操作將發生寫衝突，導致MongoDB透明地重試該操作。一些全局操作（通常是涉及多個資料庫的短期操作）仍然需要全局「全實例」鎖。

某些其他操作（如刪除集合）仍需要獨佔的資料庫鎖。

#### 快照和查核點{#snapshots-and-checkpoints}

WiredTiger使用MultiVersion Concurrency Control(MVCC)。 在操作開始時，WiredTiger為事務提供資料的時間點快照。 快照呈現一致的記憶體資料視圖。

在寫入磁碟時，WiredTiger會以一致的方式將快照中的所有資料寫入磁碟，跨所有資料檔案。 現在[持久](https://docs.mongodb.com/manual/reference/glossary/#term-durable)的資料充當資料檔案中的檢查點。 查核點可確保資料檔案始終一致，包括最後一個查核點；即查核點可以作為恢復點。

MongoDB將WiredTiger配置為以60秒或2 GB的日誌資料間隔建立檢查點（即將快照資料寫入磁碟）。

在寫入新查核點期間，上一個查核點仍然有效。 因此，即使MongoDB在寫入新檢查點時終止或遇到錯誤，在重新啟動時，MongoDB仍可從最後一個有效檢查點恢復。

當WiredTiger的中繼資料表格自動更新以參考新的查核點時，新的查核點便可存取且永久。 一旦新查核點可供存取，WiredTiger就會從舊查核點中釋放頁面。

使用WiredTiger，即使沒有[日誌](https://docs.mongodb.com/manual/reference/glossary/#term-durable) , MongoDB也能從最後一個檢查點恢復；但是，要恢復在上一個檢查點之後所做的更改，請使用[ journaling](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)運行。

#### 日誌 {#journal}

WiredTiger結合[查核點](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints)使用預寫事務日誌以確保資料的持久性。

WiredTiger日誌會保留查核點之間的所有資料修改。 如果MongoDB在查核點之間退出，則會使用日誌來重放自上次查核點以來修改的所有資料。 有關MongoDB將日誌資料寫入磁碟的頻率的資訊，請參見[日誌記錄進程](https://docs.mongodb.com/manual/core/journaling/#journal-process)。

使用[snappy](https://docs.mongodb.com/manual/core/journaling/#journal-process)壓縮庫壓縮WiredTiger日誌。 若要指定替代壓縮演算法或無壓縮，請使用[storage.wiredTiger.engineConfig.journalPlaxor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor)設定。

如需詳細資訊，請參閱：[使用WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger)進行日誌記錄。

>[!NOTE]
>
>WiredTiger的最小日誌記錄大小為128位元組。 如果記錄為128個位元組或更小，WiredTiger將不會壓縮該記錄。
>
>通過將[storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled)設定為false，可以禁用日誌記錄，這樣可以減少維護日誌的開銷。
>
>對於[standalone](https://docs.mongodb.com/manual/reference/glossary/#term-standalone)實例，不使用日誌表示當MongoDB意外退出查核點時，將丟失某些資料修改。 對於[複製集](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)的成員，複製過程可提供足夠的耐用性保證。

#### 壓縮 {#compression}

使用WiredTiger,MongoDB支援所有系列和索引的壓縮。 壓縮可以最大限度地減少儲存的使用，而不會增加CPU。

預設情況下，WiredTiger對所有系列使用帶有[snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy)壓縮庫的塊壓縮，而對所有索引使用[前置詞壓縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)。

對於系列，也提供具有[zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib)的區塊壓縮。 若要指定替代壓縮演算法或無壓縮，請使用[storage.wiredTiger.collectionConfig.blockPlaxor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib)設定。

對於索引，要禁用[前置詞壓縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)，請使用[storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression)設定。

在建立系列和索引時，也可依每個系列和每個索引來設定壓縮設定。 請參閱[指定儲存引擎選項](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options)和[db.collection.createIndex()storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options)選項。

對於大多數工作負載，預設的壓縮設定平衡了儲存效率和處理要求。

WiredTiger日誌也預設壓縮。 有關日記賬壓縮的資訊，請參閱[日記賬](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)。

#### 記憶體使用{#memory-use}

MongoDB使用WiredTiger，同時使用WiredTiger內部快取和檔案系統快取。

從3.4版開始，WiredTiger內部快取預設會使用下列其中一項較大的：

* 50%的記憶體減去1 GB，或
* 256 MB

預設情況下，WiredTiger對所有集合使用Snappy塊壓縮，所有索引使用前置詞壓縮。 壓縮預設值可在全域層級進行設定，也可在建立系列和索引時，依每個系列和每個索引來設定。

WiredTiger內部快取中的資料與磁碟格式的資料使用不同的表示法：

* 檔案系統快取中的資料與磁碟上的格式相同，包括資料檔案的任何壓縮的好處。 作業系統使用檔案系統快取來減少磁碟I/O。

載入WiredTiger內部快取中的索引與磁碟格式的資料呈現方式不同，但仍可運用索引首碼壓縮來降低記憶體使用量。

索引前置詞壓縮會消除索引欄位中的公共前置詞重複。

WiredTiger內部快取中的收集資料會解壓縮，並使用與磁碟格式不同的表示法。 塊壓縮可以顯著節省磁碟內儲存，但資料必須解壓才能由伺服器處理。

通過檔案系統快取，MongoDB自動使用WiredTiger快取或其他進程未使用的所有空閒記憶體。

要調整WiredTiger內部快取的大小，請參見[ storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB)和[—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb)。 請避免將WiredTiger內部快取大小增加至其預設值以上。

### NUMA {#numa}

非均勻記憶體訪問(NUMA)允許內核管理記憶體映射到處理器內核的方式。 雖然這種方式會嘗試加快內核的記憶體訪問速度，確保內核能夠訪問所需資料，但NUMA會干擾MMAP，因為讀取無法預測，而引入了額外的延遲。 因此，在所有具有該功能的作業系統上，`mongod`進程需要禁用NUMA。

實質上，在NUMA架構中，儲存器連接到CPU,CPU連接到匯流排。 在SMP或UMA架構中，儲存器連接到匯流排並由CPU共用。 當線程在NUMA CPU上分配記憶體時，它根據策略分配記憶體。 預設情況是分配連接到線程本地CPU的記憶體，除非沒有空閒，此時它以較高的成本使用來自空閒CPU的記憶體。 分配後，記憶體不會在CPU之間移動。 分配由繼承自父線程的策略執行，該策略最終是啟動進程的線程。

在許多將電腦視為多核統一記憶體體系結構的資料庫中，這會導致初始CPU首先滿足，而次要CPU隨後填充，特別是如果中央線程負責分配記憶體緩衝區。 解決方案是更改用於啟動`mongod`進程的主線程的NUMA策略。

這可以通過運行以下命令來完成：

```shell
numactl --interleaved=all <mongod> -f config
```

此策略會以循環方式在所有CPU節點上分配記憶體，以確保在所有節點上均勻分配記憶體。 它不會像在具有多CPU硬體的系統中那樣對記憶體產生最高效能的訪問。 大約一半的記憶體操作會比匯流排慢，但`mongod`沒有以最佳方式寫入到目標NUMA，因此這是合理的折中。

### NUMA問題{#numa-issues}

如果`mongod`進程從`/etc/init.d`資料夾以外的位置啟動，則很可能不會使用正確的NUMA策略啟動。 根據預設策略的不同，可能會出現問題。 這是因為MongoDB的各種Linux軟體包管理器安裝程式也安裝了配置檔案位於`/etc/init.d`中的服務，該配置檔案將執行上述步驟。 如果直接從歸檔檔案(`.tar.gz`)安裝並運行MongoDB，則需要在`numactl`進程下手動運行mongod。

>[!NOTE]
>
>有關NUMA政策的更多資訊，請查閱[numactl文檔](https://linux.die.net/man/8/numactl)。

MongoDB進程在不同分配策略下的行為將不同：

```

```

* `-membind=<nodes>`
僅在列出的節點上分配。Mongod不會在列出的節點上分配記憶體，並且可能不會使用所有可用記憶體。

* `-cpunodebind=<nodes>`
僅在節點上執行。Mongod將僅在指定的節點上運行，並且僅使用這些節點上可用的記憶體。

* `-physcpubind=<nodes>`
僅對列出的CPU（內核）執行。Mongod將僅在列出的CPU上運行，並僅使用這些CPU上可用的記憶體。

* `--localalloc`
始終在當前節點上分配記憶體，但使用線程運行的所有節點。如果一個線程執行分配，則只使用該CPU可用的記憶體。

* `--preferred=<node>`
偏好對節點進行配置，但如果偏好的節點已滿，則會回落至其他節點。可以使用用於定義節點的相對記號。 此外，線程在所有節點上運行。

某些策略可能導致分配給`mongod`進程的可用RAM少於所有。 與MySQL不同，MongoDB主動避免作業系統級別的分頁，因此`mongod`進程可獲得的可用記憶體可能更少。

#### 調換{#swapping}

由於資料庫的記憶體密集型特性，必須禁用作業系統級別的交換。 MongoDB程式將通過設計避免交換。

#### 遠程檔案系統{#remote-filesystems}

不建議將遠程檔案系統（如NFS）用於MongoDB的內部資料檔案（mongod進程資料庫檔案），因為它們會帶來太多延遲。 這不要與建議使用NFS的Oak Blob(FileDataStore)儲存所需的共用檔案系統混淆。

#### Read Aead {#read-ahead}

需要調整預先讀取，以便當頁面使用隨機讀取進行分頁時，不會從磁碟讀取不必要的塊，從而導致不必要的I/O頻寬消耗。

### Linux要求{#linux-requirements}

#### 最小內核版本{#minimum-kernel-versions}

* **2.6.23檔案** 系 `ext4` 統

* **檔案系統的2.6.25** 版 `xfs` 本

#### 資料庫磁碟{#recommended-settings-for-database-disks}的建議設定

**關閉時間**

建議對包含資料庫的磁碟關閉`atime`。

**設定NOOP磁碟調度程式**

您可以透過下列方式執行此動作：

首先，檢查當前設定的I/O調度程式。 這可以通過運行以下命令來完成：

```shell
cat /sys/block/sdg/queue/scheduler
```

如果回應為`noop`，您就不需要做進一步的工作。

如果NOOP不是已設定的I/O調度程式，則可以通過運行來更改它：

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**調整預讀值**

建議對MongoDB資料庫從中運行的磁碟使用32值。 這相當於16 KB。 您可以透過執行：

```shell
sudo blockdev --setra <value> <device>
```

#### 啟用NTP {#enable-ntp}

請確保在托管MongoDB資料庫的電腦上已安裝並運行NTP。 例如，您可在CentOS機器上使用yum套件管理器來安裝它：

```shell
sudo yum install ntp
```

安裝NTP守護程式並成功啟動後，可以檢查漂移檔案中伺服器的時間偏移。

#### 禁用透明大頁{#disable-transparent-huge-pages}

Red Hat Linux使用稱為透明巨頁(THP)的記憶體管理演算法。 如果您使用資料庫工作負載的作業系統，建議您禁用它。

您可依照下列程式加以停用：

1. 在您選擇的文字編輯器中開啟`/etc/grub.conf`檔案。
1. 將以下行添加到grub.conf檔案：

   ```xml
   transparent_hugepage=never
   ```

1. 最後，請執行下列動作，檢查設定是否已生效：

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用了THP，則上述命令的輸出應為：

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>如需透明巨型頁面的詳細資訊，請參閱此[文章](https://access.redhat.com/solutions/46111)。

#### 禁用NUMA {#disable-numa}

在大多數啟用NUMA的安裝中，如果MongoDB守護程式以服務形式從`/etc/init.d`資料夾運行，它將自動禁用。

如果不是這樣，您可以在每個流程級別禁用NUMA。 要禁用它，請運行以下命令：

```shell
numactl --interleave=all <path_to_process>
```

其中`<path_to_process>`是指向mongod進程的路徑。

然後，通過運行以下命令禁用區域回收：

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### 調整mongod進程的ulimit設定{#tweak-the-ulimit-settings-for-the-mongod-process}

Linux允許通過`ulimit`命令對資源分配進行可配置的控制。 這可以依使用者或依每個程式執行。

建議您根據[MongoDB建議的ulimit Settings](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings)來設定mongod進程的ulimit。

#### 測試MongoDB I/O效能{#test-mongodb-i-o-performance}

MongoDB提供了一個名為`mongoperf`的工具，用於測試I/O效能。 建議您使用它來測試構成基礎結構的所有MongoDB實例的效能。

有關如何使用`mongoperf`的資訊，請查看[MongoDB文檔](https://docs.mongodb.org/manual/reference/program/mongoperf/)。

>[!NOTE]
>
>請注意，`mongoperf`設計為在其上運行的平台上MongoDB效能的指標。 因此，不應將結果視為生產系統效能的決定性結果。
>
>為獲得更準確的效能結果，可以使用`fio` Linux工具運行補充測試。

**在組成部署的虛擬機上測試讀取效能**

安裝該工具後，請切換到MongoDB資料庫目錄以運行測試。 然後，使用此配置運行`mongoperf`以啟動第一個測試：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

所有MongoDB實例的所需輸出應高達每秒2GB(2GB/s)和每32個線程運行500.000 IOPS。

此次使用記憶體映射檔案運行第二次測試，方法是設定`mmf:true`參數：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

第二測試的輸出應比第一測試高得多，表示儲存器傳輸效能。

>[!NOTE]
>
>執行測試時，檢查作業系統監視系統中相關虛擬機的I/O使用情況統計資訊。 如果它們表示I/O讀取的值低於100%，則虛擬機可能會發生問題。

**測試主MongoDB實例的寫效能**

接著，從具有相同設定的MongoDB資料庫目錄運行`mongoperf` ，以檢查主MongoDB實例的I/O寫效能：

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

所需的輸出應為每秒12 MB ，達到約3000 IOPS ，線程數之間的變化很小。

## 虛擬化環境{#steps-for-virtualised-environments}的步驟

### VMWare {#vmware}

如果您使用WMWare ESX管理和部署虛擬化環境，請確保從ESX控制台執行以下設定以適應MongoDB操作：

1. 關閉記憶體膨脹
1. 為將托管MongoDB資料庫的虛擬機預分配和保留記憶體
1. 使用儲存I/O控制為`mongod`進程分配足夠的I/O。
1. 通過設定[CPU保留](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)來保證MongoDB所在電腦的CPU資源

1. 考慮使用ParaVirtual I/O驅動程式。 有關如何執行此操作的詳細資訊，請查看此[知識庫文章](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398)。

### Amazon Web Services {#amazon-web-services}

有關如何使用Amazon Web Services設定MongoDB的文檔，請查看MongoDB網站上的[配置AWS Integration](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/)文章。

## 部署前保護MongoDB {#securing-mongodb-before-deployment}

請參閱[上的這篇文章，安全地部署MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html)，以瞭解如何在部署前保護資料庫的配置。

## Dispatcher {#dispatcher}

### 選擇Dispatcher {#choosing-the-operating-system-for-the-dispatcher}的作業系統

為了正確提供MongoDB部署服務，裝載調度程式的作業系統必須運行&#x200B;**Apache httpd** **版本2.4或更高版本。**

此外，請確定您建立中使用的所有程式庫都是最新的，以便將安全性影響降至最低。

### Dispatcher Configuration {#dispatcher-configuration}

典型的Dispatcher設定的服務量是單一AEM例項的十到二十倍。

由於Dispatcher主要是無狀態的，因此它可以輕鬆水準擴展。 在某些部署中，作者必須受到限制，無法存取特定資源。 因此，強烈建議您搭配作者例項使用分派程式。

在沒有分派程式的情況下執行AEM，將需要SSL終止和負載平衡由其他應用程式執行。 這是必要的，因為工作階段必須與其所建立的AEM例項（稱為黏著連線）有相關性。 其目的在於確保內容更新顯示的延遲性最低。

有關如何配置[Dispatcher文檔](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)的詳細資訊，請查看&lt;a0/> Dispatcher文檔&lt;a1/>。

### 其他配置{#additional-configuration}

#### 自黏連線{#sticky-connections}

嚴格連線可確保個人化頁面和作業資料，都是在相同的AEM例項上合成。 此資料會儲存在例項上，因此來自相同使用者的後續要求會傳回至相同的例項。

建議所有內層將請求路由至AEM例項時，都啟用嚴格連線，以鼓勵後續請求到達相同的AEM例項。 這有助於將例項間更新內容時，會引起注意的延遲降至最低。

#### 長期過期{#long-expires}

依預設，從AEM分派器傳出的內容具有「上次修改日期」和「Etag」標題，而不會顯示內容到期。 這可確保使用者介面永遠取得資源的最新版本，也表示瀏覽器將執行GET作業，以檢查資源是否已變更。 這可能會導致HTTP回應為304（未修改）的多個請求，視頁面載入而定。 對於已知未過期的資源，設定「過期」標題並移除「上次修改」和「ETag」標題將導致內容被快取，在「過期」標題中的日期滿足之前，不會再提出更新請求。

但是，使用此方法表示沒有合理的方法可讓資源在過期標題過期之前在瀏覽器中過期。 為了減輕此問題，HtmlClientLibraryManager可設定為對用戶端程式庫使用不可變的URL。

這些URL保證不會變更。 當URL中包含的資源正文變更時，這些變更會自動反映在URL中，以確保瀏覽器會要求正確的資源版本。

預設設定會將選擇器新增至HtmlClientLibraryManager。 作為選擇器，資源將快取在調度器中，並且選擇器保持不變。 此外，此選擇器也可用來確保正確的過期行為。 預設選擇器遵循`lc-.*?-lc`模式。 下列Apache httpd組態指令可確保所有符合該模式的請求都會在適當的過期時間內送達。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### 無聞{#no-sniff}

若內容是在沒有內容類型的情況下傳出，許多瀏覽器會嘗試透過讀取內容的前幾個位元組來猜測內容類型。 這叫做&quot;嗅探&quot;。 嗅探操作會開啟一個安全漏洞，因為可以寫入儲存庫的用戶可能上傳沒有內容類型的惡意內容。

因此，建議將`no-sniff`標頭添加到調度程式所服務的資源中。 但是，調度程式不快取標頭。 這表示從本機檔案系統提供的任何內容，其內容類型都將由其擴充功能決定，而不是使用其AEM伺服器原始內容類型標題。

如果已知Web應用程式從不提供沒有檔案類型的快取資源，則無法安全地啟用嗅探。

您可以包含啟用「無嗅探」:

```xml
Header set X-Content-Type-Options "nosniff"
```

您也可以選擇性啟用它：

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### 內容安全性策略{#content-security-policy}

預設的調度器設定允許開啟的內容安全策略，也稱為CSP。 這可讓頁面從受瀏覽器沙盒預設原則約束的所有網域載入資源。

最好限制可載入資源的位置，以避免從不受信任的或未驗證的外部伺服器將程式碼載入Javascript引擎。

CSP允許對策略進行微調。 但是，在複雜的應用程式中，CSP標題需要謹慎開發，因為限制過大的原則可能會破壞使用者介面的部分。

>[!NOTE]
>
>有關如何運作的詳細資訊，請參見[Content Security Policy](https://www.owasp.org/index.php/Content_Security_Policy)上的&lt;a0/>OWASP頁。

### 調整{#sizing}大小

有關調整大小的詳細資訊，請參閱[硬體調整指南](/help/managing/hardware-sizing-guidelines.md)。

### MongoDB效能優化{#mongodb-performance-optimization}

有關MongoDB效能的一般資訊，請參見[分析MongoDB效能](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/)。

## 已知限制{#known-limitations}

### 併發安裝{#concurrent-installations}

雖然MongoMK支援將多個AEM執行個體與單一資料庫同時使用，但並行安裝則不受支援。

為瞭解決這個問題，請務必先使用單一成員運行安裝，然後在完成安裝後添加其他成員。

### 頁面名稱長度{#page-name-length}

如果AEM是在MongoMK永續性管理器部署上執行，則[頁面名稱的限制為150個字元。](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[請參閱MongoDB文](https://docs.mongodb.com/manual/reference/limits/) 件，以熟悉MongoDB本身的已知限制和臨界值。

