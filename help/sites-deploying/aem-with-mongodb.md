---
title: AEM與MongoDB
seo-title: AEM with MongoDB
description: 了解成功部署MongoDB的AEM所需的工作和考量。
seo-description: Learn about the tasks and considerations needed for a successful AEM with MongoDB deployment.
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6496'
ht-degree: 0%

---

# AEM與MongoDB{#aem-with-mongodb}

本文旨在改善有關使用MongoDB成功部署Adobe Experience Manager所需工作和考量事項的知識。

如需與部署相關的詳細資訊，請參閱 [部署和維護](/help/sites-deploying/deploy.md) 一節。

## 何時將MongoDB與AEM搭配使用 {#when-to-use-mongodb-with-aem}

MongoDB通常用於支援AEM製作部署，其中符合下列其中一個條件：

* 每天不重複使用者超過1000人；
* 100多名用戶同時使用；
* 頁面編輯量大；
* 大型轉出或啟用。

上述條件僅適用於製作例項，不適用於應全部以TarMK為基礎的任何發佈例項。 使用者人數會參照已驗證的使用者，因為製作例項不允許未驗證的存取。

如果不符合標準，則建議使用TarMK活動/備用部署來解決可用性問題。 通常，在擴展要求比單個硬體項所能達到的要高的情況下，應考慮MongoDB。

>[!NOTE]
>
>有關製作例項大小和同時使用者定義的其他資訊，請參閱 [硬體調整指南](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### AEM的最小MongoDB部署 {#minimal-mongodb-deployment-for-aem}

以下是MongoDB上AEM的最低部署。 為了簡單起見，SSL終止和HTTP代理元件已推廣。 它包含單個MongoDB複製副本集，其中一個主副本和兩個副本。

![chlimage_1-4](assets/chlimage_1-4.png)

最少部署需要3 `mongod` 配置為複製副本集的實例。 一個實例將被選為主實例，而另一個實例是輔助實例，選舉由管理 `mongod`. 連接到每個實例的是本地磁碟。 為了使群集支援負載，建議最低吞吐量為12 MB/s，每秒超過3000個I/O操作(IOPS)。

AEM作者會連結至 `mongod` 例項，讓每個AEM作者都連線至這三個 `mongod` 例項。 寫入被發送到主實例，並且可從任何實例讀取讀取。 流量會根據Dispatcher的負載分配至任何一個作用中的AEM製作例項。 OAK資料存放區是 `FileDataStore`，而MongoDB監控則由MMS或MongoDB Ops Manager提供，視部署位置而定。 作業系統層級和記錄監控由第三方解決方案提供，例如Splunk或Ganglia。

在此部署中，成功實施需要所有元件。 任何遺失的元件都會讓實施無法正常運作。

### 作業系統 {#operating-systems}

如需AEM 6支援的作業系統清單，請參閱 [技術需求頁面](/help/sites-deploying/technical-requirements.md).

### 環境 {#environments}

如果運行項目的不同技術團隊之間有良好的溝通，則支援虛擬化環境。 這包括運行AEM的團隊、擁有作業系統的團隊和管理虛擬化基礎架構的團隊。

MongoDB實例的I/O容量需由管理虛擬化環境的團隊管理。 如果項目使用雲部署(如Amazon Web Services)，則需要為實例布建足夠的I/O容量和一致性，以支援MongoDB實例。 否則，MongoDB程式和Oak存放庫的執行將會不可靠且不穩定。

在虛擬化環境中， MongoDB將需要特定的I/O和VM配置，以確保MongoDB的儲存引擎不會因VMWare資源分配策略而受損。 成功的實作將確保各團隊之間沒有障礙，而且所有團隊都已註冊，以提供所需的效能。

## 硬體考量事項 {#hardware-considerations}

### 儲存空間 {#storage}

為了實現讀寫吞吐量以獲得最佳效能而無需過早進行水準擴展，MongoDB通常需要SSD儲存或與SSD效能相當的儲存。

### RAM {#ram}

使用MMAP儲存引擎的MongoDB 2.6和3.0版要求資料庫及其索引的工作集與RAM相符。

RAM不足將導致效能的顯著降低。 工作集和資料庫的大小與應用程式高度相關。 雖然可以做出一些估計，但確定所需RAM量的最可靠方法是構建AEM應用程式並對其進行負載測試。

為了幫助進行負載測試，可以假定工作集與總資料庫大小的比率如下：

* 1:10用於SSD儲存
* 1:3（硬碟儲存）

這意味著，在SSD部署的情況下，2TB的資料庫需要200GB的RAM。

雖然MongoDB 3.0中的WiredTiger儲存引擎也受到同樣的限制，但工作集、RAM和頁故障之間的關聯性不如WiredTiger不使用與MMAP儲存引擎相同的記憶體映射。

>[!NOTE]
>
>Adobe建議針對使用MongoDB 3.0的AEM 6.1部署，使用WiredTiger儲存引擎。

### 資料儲存 {#data-store}

由於MongoDB工作集限制，強烈建議維護資料儲存獨立於MongoDB。 在大部分環境中a `FileDataStore` 應使用所有AEM執行個體都可用的NAS。 若是使用Amazon Web Services, `S3 DataStore`. 如果由於任何原因，資料儲存區在MongoDB內被維護，則資料儲存區的大小應添加到資料庫總大小中，並適當調整工作集計算。 這可能意味著要配置更多的RAM，以保持效能而不發生頁面故障。

## 監控 {#monitoring}

監測對於成功實施該項目至關重要。 儘管具備足夠的知識，但在MongoDB上運行AEM時無需監控，但通常在專門用於部署的每個部分的工程師中都能找到這些知識。

這通常涉及一名研發工程師在Apache Oak Core工作，以及一名MongoDB專員。

若不在所有層級進行監控，診斷問題時將需要詳細了解程式碼庫。 實施小組將能對異常情況作出適當反應，並對主要統計資料進行監測和適當指導。

雖然可以使用命令行工具獲得群集操作的快速快照是可能的，但在許多主機上即時執行此操作幾乎是不可能的。 命令列工具很少會提供超過幾分鐘的歷史資訊，也絕不允許不同類型的量度之間產生交叉關聯。 一段短暫的緩慢背景 `mongod` 同步需要大量的手動工作，以便與來自明顯未連接的虛擬機的共用儲存資源的I/O等待或過多的寫入級別相關聯。

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager是MongoDB提供的免費服務，允許監控和管理MongoDB實例。 它即時提供MongoDB群集的效能和運行狀況的視圖。 只要執行個體可以連線至Cloud Manager監控伺服器，它便可同時管理雲端和私人托管執行個體。

它需要安裝在MongoDB實例上的代理，該代理連接到監視伺服器。 代理程式有3個層級：

* 一種自動化代理，可以完全自動化MongoDB伺服器上的所有內容，
* 可監視 `mongod` 例項，
* 執行資料定時備份的備份代理。

雖然使用Cloud Manager實現MongoDB群集的維護自動化使許多常式任務更加輕鬆，但它不是必需的，而且也不是將它用於備份。 選擇Cloud Manager進行監視時，需要進行監視。

有關MongoDB Cloud Manager的詳細資訊，請參閱 [MongoDB檔案](https://docs.cloud.mongodb.com/).

### MongoDB Ops Manager {#mongodb-ops-manager}

MongoDB Ops Manager與MongoDB Cloud Manager軟體相同。 註冊後，Ops Manager就可以下載並安裝到本地的專用資料中心，或任何其他筆記型電腦或台式電腦上。 它使用本地MongoDB資料庫來儲存資料，並以與Cloud Manager完全相同的方式與受控伺服器通信。 如果您的安全策略禁止監視代理，則應使用MongoDB Ops Manager。

### 作業系統監控 {#operating-system-monitoring}

運行AEM MongoDB群集需要作業系統級別監視。

Ganglia是此類系統的一個很好的示例，它提供了所需資訊的範圍和詳細資訊，這些資訊超出了CPU、負載平均值和可用磁碟空間等基本健康指標。 要診斷問題，需要較低級別的資訊，如熵池級別、CPU I/O等待、FIN_WAIT2狀態的套接字。

### 日誌聚合 {#log-aggregation}

使用多個伺服器的群集時，生產系統需要集中日誌聚合。 Splunk等軟體支援日誌聚合，並允許團隊分析應用程式的行為模式，而無需手動收集日誌。

## 核取清單 {#checklists}

本節說明您應採取的各種步驟，以確保在實作專案前已正確設定AEM和MongoDB部署。

### 網路 {#network}

1. 首先，請確定所有主機都有DNS項目
1. 所有主機應可通過其DNS項從所有其他可路由主機中解析
1. 所有MongoDB主機都可從同一群集中的所有其他MongoDB主機路由
1. MongoDB主機可以將資料包路由到MongoDB Cloud Manager和其他監視伺服器
1. AEM伺服器可將資料包路由到所有MongoDB伺服器
1. 任何AEM伺服器與任何MongoDB伺服器之間的資料包延遲均小於兩毫秒，不會丟失資料包，且標準分佈為1毫秒或更短。
1. 確保AEM和MongoDB伺服器之間不超過兩跳
1. 兩台MongoDB伺服器之間的跳數不超過兩個
1. 在任何核心伺服器(MongoDB、AEM或任何組合)之間，沒有高於OSI Level 3的路由器。
1. 如果使用VLAN中繼或任何形式的網路隧道，則必須符合資料包延遲檢查。

### AEM設定 {#aem-configuration}

#### 節點儲存配置 {#node-store-configuration}

AEM例項必須設定為搭配MongoMK使用AEM。 AEM中MongoMK實作的基礎為檔案節點存放區。

如需如何設定節點存放區的詳細資訊，請參閱 [在AEM中設定節點儲存和資料儲存](/help/sites-deploying/data-store-config.md).

以下是用於最小MongoDB部署的Document Node Store配置的示例：

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
這是MongoDB伺服器AEM需要連接的。 將連接到預設副本集的所有已知成員。 如果使用了MongoDB Cloud Manager，則會啟用伺服器安全性。 因此，連接字串必須包含適當的用戶名和密碼。 非企業版的MongoDB僅支援用戶名和密碼驗證。 如需連線字串語法的詳細資訊，請參閱 [檔案](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
資料庫的名稱。 AEM的預設值為 
`aem-author`。

* `customBlobStore`
如果部署將二進位檔儲存在資料庫中，則它們將成為工作集的一部分。 因此，建議不要在MongoDB中儲存二進位檔，並提供類似 
`FileSystem` NAS上的資料儲存。

* `cache`
快取大小(MB)。 這會分佈於 
`DocumentNodeStore`. 預設為256MB。 不過，更大的快取可讓Oak讀取效能受益。

* `blobCacheSize`
AEM可快取常用的Blob，以避免從資料存放區重新擷取。 這對效能的影響更大，尤其是在MongoDB資料庫中儲存Blob時。 所有基於檔案系統的資料儲存都將受益於作業系統級磁碟快取。

#### 資料儲存配置 {#data-store-configuration}

資料儲存區用於儲存大於臨界值的檔案。 低於該閾值時，檔案將作為屬性儲存在文檔節點儲存區中。 若 `MongoBlobStore` ，則會在MongoDB中建立專用集合以儲存blob。 此集合有助於 `mongod` 例項，以及需要 `mongod` 有更多RAM以避免效能問題。 因此，建議的設定是避免 `MongoBlobStore` 供生產部署及使用 `FileDataStore` 由所有AEM實例共用的NAS作為備份。 由於作業系統級快取在管理檔案方面是有效的，因此應將磁碟上檔案的最小大小設定為接近磁碟的塊大小，以便檔案系統得到有效使用，並且許多小文檔不會對磁碟的工作集產生過大的貢獻 `mongod` 例項。

以下是使用MongoDB進行最少AEM部署的典型資料儲存配置：

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
大小（位元組）。 小於或等於此大小的二進位檔會與Document Node Store一起儲存。 儲存二進位檔的內容，而非儲存blob的ID。 對於大於此大小的二進位檔，二進位檔的ID會儲存為節點集合中Document的屬性，而二進位檔的內文會儲存在 
`FileDataStore` 在磁碟上。 4096位元組是典型的檔案系統塊大小。

* `path`
資料儲存根的路徑。 若為MongoMK部署，這必須是可供所有AEM執行個體使用的共用檔案系統。 通常使用網路連接儲存(NAS)伺服器。 若是雲端部署(例如Amazon Web Services), 
`S3DataFileStore` 也可用。

* `cacheSizeInMB`
二進位快取的總大小(MB)。 用於快取小於的二進位檔 
`maxCacheBinarySize` 設定。

* `maxCachedBinarySize`
二進位快取中二進位快取的最大位元組大小。 如果使用基於檔案系統的資料儲存，則不建議對資料儲存快取使用高值，因為作業系統已快取二進位檔。

#### 停用查詢提示 {#disabling-the-query-hint}

建議您借由新增屬性來停用隨所有查詢傳送的查詢提示

`-Doak.mongo.disableIndexHint=true`

啟動AEM時。 這樣，MongoDB將根據內部統計資料計算要使用的最合適索引。

如果未停用查詢提示，任何索引的效能調整將不會影響AEM的效能。

#### 為MongoMK啟用永久快取 {#enable-persistent-cache-for-mongomk}

建議為MongoDB部署啟用永久性快取配置，以最大化具有高I/O讀取效能的環境的速度。 如需詳細資訊，請參閱 [Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## MongoDB作業系統優化 {#mongodb-operating-system-optimizations}

### 作業系統支援 {#operating-system-support}

MongoDB 2.6使用記憶體映射儲存引擎，該引擎對RAM和磁碟之間作業系統級別管理的某些方面很敏感。 MongoDB實例的查詢和讀取效能依賴於避免或消除慢速的I/O操作（通常稱為頁面故障）。 這些是適用於的頁面錯誤 `mongod` 過程。 不應將它們與作業系統級頁錯誤混淆。

為了快速操作，MongoDB資料庫應該只訪問已在RAM中的資料。 它需要存取的資料由索引和資料組成。 此索引和資料集合稱為工作集。 當工作集大於可用RAM時，MongoDB必須從磁碟中將該資料頁面化，從而產生I/O成本，從而將記憶體中已有的其他資料逐出。 如果遷出導致從磁碟頁故障中重新載入資料，將佔據主導地位，效能將降低。 如果工作集為動態和變數，則會發生更多頁面錯誤以支援操作。

MongoDB在多種作業系統上運行，包括各種Linux版本、Windows和Mac OS。 請參閱 [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) 以取得其他詳細資訊。 MongoDB根據您的作業系統選擇提供不同的作業系統級別建議。 有檔案記錄於 [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) 為方便起見。

#### Linux {#linux}

* 關閉透明護頁和碎片整理。 請參閱 [透明大頁設定](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) 以取得更多資訊。
* [調整預讀設定](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 儲存資料庫檔案以適合您的使用案例的裝置上。

   * 對於MMAPv1儲存引擎，如果工作集大於可用RAM，且文檔訪問模式是隨機的，請考慮將預讀數降低到32或16。 評估不同的設定，以找到最佳值，最大化駐留記憶體並減少頁面故障數。
   * 對於WiredTiger儲存引擎，無論儲存介質類型（旋轉、固態硬碟等）如何，請將預讀設定為0。 一般而言，除非測試顯示更高的預讀值可以帶來可衡量、可重複且可靠的好處，否則請使用建議的預讀設定。 [MongoDB專業支援](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 可以就非零預讀配置提供建議和指導。

* 如果您在虛擬環境中執行RHEL 7 / CentOS 7，請停用調整工具。
* 當RHEL 7 / CentOS 7在虛擬環境中運行時，調諧的工具會自動調用從效能吞吐量派生的效能配置檔案，該效能配置檔案會自動將預讀設定設定為4MB。 這可能會對效能造成負面影響。
* 使用SSD驅動器的noop或截止日期磁碟計畫程式。
* 在來賓VM中使用用於虛擬化驅動器的noop磁碟調度程式。
* 禁用NUMA或將vm.zone_recliam_mode設定為0並運行 [蒙古](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 具有節點交錯的實例。 請參閱： [MongoDB和NUMA硬體](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 以取得更多資訊。

* 調整硬體上的上限值以符合您的使用案例。 若為多個 [蒙古](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) 或 [蒙古](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) 例項在相同使用者下執行，請據以縮放上限值。 請參閱： [UNIX上限設定](https://docs.mongodb.com/manual/reference/ulimit/) 以取得更多資訊。

* 將noatime用於 [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) 掛點。
* 為部署配置足夠的檔案句柄(fs.file-max)、內核pid限制(kernel.pid_max)和每個進程的最大線程數(kernel.threads-max)。 對於大型系統，以下值提供了良好的起點：

   * fs.file-max值98000,
   * kernel.pid_max值為64000,
   * andkernel.threads-max值64000

* 確保系統配置了交換空間。 如需適當大小的詳細資訊，請參閱作業系統的檔案。
* 確保系統預設TCP keepalive設定正確。 值300通常為副本集和共用群集提供更好的效能。 請參閱： [TCP保持活動時間是否會影響MongoDB部署？](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) ，以取得詳細資訊。

#### Windows {#windows}

* 請考慮禁用NTFS「上次訪問時間」更新。 這類似於在類似Unix的系統上禁用atime。

### WiredTiger {#wiredtiger}

自MongoDB 3.2起，MongoDB的預設儲存引擎是WiredTiger儲存引擎。 此引擎提供許多強大且可擴展的功能，使其更適合於所有一般資料庫工作負載。 以下幾節將介紹這些功能。

#### 文檔級併發 {#document-level-concurrency}

WiredTiger對寫操作使用文檔級併發控制。 因此，多個用戶端可以同時修改集合的不同檔案。

對於大多數讀寫操作，WiredTiger使用樂觀的併發控制。 WiredTiger僅在全局、資料庫和收集級別使用意圖鎖。 當儲存引擎檢測到兩個操作之間的衝突時，將產生一個寫入衝突，導致MongoDB透明地重試該操作。某些全局操作（通常涉及多個資料庫的短期操作）仍需要全局「實例範圍」鎖。

某些其他操作（如刪除集合）仍需要專用的資料庫鎖。

#### 快照和查核點 {#snapshots-and-checkpoints}

WiredTiger使用MultiVersion Concurrency Control(MVCC)。 在操作開始時，WiredTiger為事務提供資料的時間點快照。 快照呈現記憶體內資料的一致視圖。

寫入磁碟時，WiredTiger會以一致的方式在所有資料檔案中將快照中的所有資料寫入磁碟。 現在 —  [耐用](https://docs.mongodb.com/manual/reference/glossary/#term-durable) 資料會作為資料檔案中的查核點。 檢查點可確保資料檔案一致，直到並包括最後一個檢查點；即查核點可作為恢復點。

MongoDB配置WiredTiger以60秒或2GB的日誌資料間隔建立檢查點（即將快照資料寫入磁碟）。

在寫入新查核點期間，上一個查核點仍然有效。 因此，即使MongoDB在寫入新檢查點時終止或遇到錯誤，在重新啟動時，MongoDB仍可從最後一個有效檢查點恢復。

當WiredTiger的中繼資料表原子性更新以參考新查核點時，新查核點便可存取且永久存取。 一旦新查核點可供存取，WiredTiger就會從舊查核點中釋放頁面。

使用WiredTiger，即使沒有 [日誌](https://docs.mongodb.com/manual/reference/glossary/#term-durable), MongoDB可從最後一個查核點恢復；但是，要恢復在上一個檢查點之後所做的更改，請使用 [日誌](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 日誌 {#journal}

WiredTiger使用預寫事務日誌與 [查核點](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) 確保資料的持久性。

WiredTiger日誌會保存查核點之間的所有資料修改。 如果MongoDB在查核點之間退出，則會使用日誌來重播自上次檢查點以來修改的所有資料。 有關MongoDB將日誌資料寫入磁碟的頻率的資訊，請參見 [日誌處理](https://docs.mongodb.com/manual/core/journaling/#journal-process).

WiredTiger日誌使用 [快照](https://docs.mongodb.com/manual/core/journaling/#journal-process) 壓縮程式庫。 若要指定替代的壓縮演算法或不壓縮，請使用 [storage.wiredTiger.engineConfig.journalCompxator](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 設定。

如需詳細資訊，請參閱： [與WiredTiger聯繫](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>WiredTiger的最小日誌記錄大小為128位元組。 如果日誌記錄為128個位元組或更小，則WiredTiger不會壓縮該記錄。
>
>您可以通過設定 [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) 設為false，可降低維護日記帳的開銷。
>
>針對 [獨立](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) 例項，不使用日記帳表示當MongoDB意外退出查核點之間時，您將丟失某些資料修改。 若 [副本集](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)，複製過程可提供足夠的持久性保證。

#### 壓縮 {#compression}

使用WiredTiger,MongoDB支援對所有集合和索引進行壓縮。 壓縮使儲存的使用最小化，而不會犧牲額外的CPU。

依預設，WiredTiger會使用區塊壓縮功能，搭配 [快照](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 所有集合和 [前置詞壓縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) （適用於所有索引）。

對於集合，使用 [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 也可用。 若要指定替代的壓縮演算法或不壓縮，請使用 [storage.wiredTiger.collectionConfig.blockComplassor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 設定。

對於索引，要禁用 [前置詞壓縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)，請使用 [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) 設定。

在建立集合和索引期間，也可以根據每個集合和每個索引配置壓縮設定。 請參閱 [指定儲存引擎選項](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) 和 [db.collection.createIndex()storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) 選項。

對於大多數工作負載，預設壓縮設定平衡了儲存效率和處理要求。

預設也會壓縮WiredTiger日誌。 有關日誌壓縮的資訊，請參閱 [日誌](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 記憶體使用 {#memory-use}

使用WiredTiger時，MongoDB既利用WiredTiger內部快取，又利用檔案系統快取。

從3.4版開始，預設情況下，WiredTiger內部快取將使用下列其中一項的較大：

* 50%的RAM減去1 GB，或
* 256 MB

預設情況下，WiredTiger對所有集合使用Snappy塊壓縮，對所有索引使用前置詞壓縮。 壓縮預設值可在全局級別配置，也可以在建立集合和索引期間按每個集合和每個索引設定。

WiredTiger內部快取中的資料與磁碟上的資料使用不同的表示法：

* 檔案系統快取中的資料與磁碟上的格式相同，包括資料檔案的任何壓縮的好處。 作業系統使用檔案系統快取來減少磁碟I/O。

在WiredTiger內部快取中載入的索引與磁碟格式的資料表示方式不同，但仍可利用索引前置詞壓縮來減少RAM的使用。

索引前置詞壓縮會去除索引欄位中的常見前置詞重複。

WiredTiger內部快取中的收集資料未壓縮，且使用與磁碟格式不同的表示法。 塊壓縮可以顯著節省磁碟上的儲存，但必須解壓縮資料才能由伺服器操作。

通過檔案系統快取，MongoDB自動使用WiredTiger快取或其他進程未使用的所有空閒記憶體。

要調整WiredTiger內部快取的大小，請參閱 [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) 和 [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). 避免將WiredTiger內部快取大小增加到其預設值以上。

### 努馬 {#numa}

非統一記憶體訪問(NUMA)允許內核管理記憶體映射到處理器內核的方式。 儘管這種方法試圖使內核的記憶體訪問速度加快，以確保內核能夠訪問所需資料，但NUMA會干擾MMAP引入額外的延遲，因為無法預測讀取。 因此，NUMA必須在 `mongod` 處理所有具有此功能的作業系統。

本質上，在NUMA體系結構中，儲存器連接到CPU,CPU連接到匯流排。 在SMP或UMA體系結構中，記憶體連接到匯流排並由CPU共用。 當線程在NUMA CPU上分配記憶體時，它會根據策略分配記憶體。 預設值是分配連接到線程的本地CPU的記憶體，除非沒有空閒記憶體，此時它會以較高的成本使用空閒CPU的記憶體。 分配後，記憶體不會在CPU之間移動。 分配由從父線程繼承的策略執行，該策略最終是啟動進程的線程。

在許多將電腦視為多核統一記憶體體系結構的資料庫中，這會導致初始CPU首先滿足，而次要CPU稍後填滿，尤其是如果中央線程負責分配記憶體緩衝區時。 解決方案是更改用於啟動的主線程的NUMA策略 `mongod` 程式。

執行下列命令即可完成此作業：

```shell
numactl --interleaved=all <mongod> -f config
```

此策略會以循環方式在所有CPU節點上分配記憶體，以確保在所有節點上均勻分配。 它不會像使用多CPU硬體的系統那樣，對記憶體產生最高效能的訪問。 大約一半的記憶體操作會比匯流排慢，但 `mongod` 並未以最佳方式向NUMA目標寫入，因此它是合理的妥協。

### NUMA問題 {#numa-issues}

若 `mongod` 進程從以下位置啟動： `/etc/init.d` 資料夾中，可能不會使用正確的NUMA策略啟動。 根據預設策略的不同，可能會出現問題。 這是因為MongoDB的各種Linux套件管理器安裝程式也安裝了配置檔案位於 `/etc/init.d` 執行上述步驟。 如果直接從歸檔檔案安裝並運行MongoDB( `.tar.gz`)，則您需要在 `numactl` 程式。

>[!NOTE]
>
>有關NUMA政策的更多資訊，請查閱 [numactl檔案](https://linux.die.net/man/8/numactl).

MongoDB進程在不同分配策略下的行為將不同：

```

```

* `-membind=<nodes>`
僅在列出的節點上分配。 Mongod不會在列出的節點上分配記憶體，並且可能不會使用所有可用記憶體。

* `-cpunodebind=<nodes>`
僅在節點上執行。 Mongod只會在指定的節點上運行，並且只使用這些節點上可用的記憶體。

* `-physcpubind=<nodes>`
僅對列出的CPU（核心）執行。 Mongod只會在列出的CPU上運行，並且只使用這些CPU上可用的記憶體。

* `--localalloc`
始終在當前節點上分配記憶體，但使用線程運行的所有節點。 如果一個線程執行分配，則只使用該CPU可用的記憶體。

* `--preferred=<node>`
偏好對節點進行配置，但如果偏好的節點已滿，則會回復給其他節點。 可使用用於定義節點的相對注釋。 此外，線程在所有節點上運行。

某些策略可能導致提供給的可用RAM少於 `mongod` 程式。 與MySQL不同， MongoDB主動避免作業系統級別分頁，因此 `mongod` 進程可能獲得的記憶體可能較少。

#### 交換 {#swapping}

由於資料庫的記憶體密集性質，必須禁用作業系統級別交換。 MongoDB程式將避免設計交換。

#### 遠程檔案系統 {#remote-filesystems}

不建議將NFS等遠程檔案系統用於MongoDB的內部資料檔案（mongod進程資料庫檔案），因為它們會導致太多延遲。 這與儲存建議使用NFS的Oak Blob(FileDataStore)所需的共用檔案系統不容混淆。

#### 預讀 {#read-ahead}

需要調整預讀，以便當使用隨機讀取來調入頁面時，不會從磁碟中讀取不必要的塊，從而不必要地消耗I/O頻寬。

### Linux需求 {#linux-requirements}

#### 最小內核版本 {#minimum-kernel-versions}

* **2.6.23** for `ext4` 檔案

* **2.6.25** for `xfs` 檔案

#### 資料庫磁碟的建議設定 {#recommended-settings-for-database-disks}

**關閉時間**

建議 `atime` 將對包含資料庫的磁碟關閉。

**設定NOOP磁碟調度程式**

您可以透過以下方式達成此目的：

首先，檢查當前設定的I/O調度程式。 執行下列命令即可完成此作業：

```shell
cat /sys/block/sdg/queue/scheduler
```

如果回應為 `noop` 你沒什麼可做的。

如果NOOP不是已設定的I/O排程器，則可以通過運行來更改它：

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**調整預讀值**

建議將值32用於運行MongoDB資料庫的磁碟。 這等於16 KB。 您可以執行以進行設定：

```shell
sudo blockdev --setra <value> <device>
```

#### 啟用NTP {#enable-ntp}

請確保在承載MongoDB資料庫的電腦上安裝並運行NTP。 例如，您可以在CentOS電腦上使用yum套件管理器來安裝：

```shell
sudo yum install ntp
```

安裝NTP守護程式並成功啟動後，可以檢查漂移檔案中伺服器的時間偏移。

#### 禁用透明大頁 {#disable-transparent-huge-pages}

Red Hat Linux使用名為Transparent Heage Pages(THP)的記憶體管理算法。 如果您正在將作業系統用於資料庫工作負載，建議禁用它。

您可以依照下列程式加以停用：

1. 開啟 `/etc/grub.conf` 檔案。
1. 將以下行添加到grub.conf檔案中：

   ```xml
   transparent_hugepage=never
   ```

1. 最後，檢查設定是否已通過運行生效：

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用了THP，則上述命令的輸出應為：

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>有關透明大頁的詳細資訊，請參閱此 [文章](https://access.redhat.com/solutions/46111).

#### 禁用NUMA {#disable-numa}

在啟用NUMA的大多數安裝中，如果MongoDB守護程式以服務的形式運行，則會自動禁用它 `/etc/init.d` 檔案夾。

如果情況並非如此，您可以在每個進程級別禁用NUMA。 要禁用它，請運行以下命令：

```shell
numactl --interleave=all <path_to_process>
```

其中 `<path_to_process>` 是通往蒙古進程的路。

然後，通過運行禁用區域回收：

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### 調整mongod程式的上限設定 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux允許可配置控制通過 `ulimit` 命令。 您可以透過使用者或依每個程式來執行。

建議您根據 [MongoDB建議的限制設定](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### 測試MongoDB I/O效能 {#test-mongodb-i-o-performance}

MongoDB提供一種名為 `mongoperf` 用於測試I/O效能。 建議您使用它來測試構成您基礎架構的所有MongoDB實例的效能。

如需如何使用的資訊 `mongoperf`，檢視 [MongoDB檔案](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>請注意 `mongoperf` 設計為其所運行平台上MongoDB效能的指標。 因此，不應將結果視為生產系統效能的最終結果。
>
>為獲得更準確的效能結果，您可以使用 `fio` Linux工具。

**在組成部署的虛擬機上測試讀取效能**

安裝此工具後，請切換到MongoDB資料庫目錄以運行測試。 然後，執行以開始第一個測試 `mongoperf`使用此設定：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

對於所有MongoDB實例，所需輸出應高達每秒2GB(2GB/s)和每秒500.000 IOPS（以32個線程運行）。

通過設定 `mmf:true` 參數：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

第二測試的輸出應比第一測試的輸出大得多，表明儲存器傳輸效能。

>[!NOTE]
>
>執行測試時，檢查作業系統監視系統中有關虛擬機的I/O使用情況統計資訊。 如果它們表示I/O讀取的值低於100%，則您的虛擬機可能會有問題。

**測試主MongoDB實例的寫入效能**

接下來，通過運行檢查主MongoDB實例的I/O寫效能 `mongoperf` 從具有相同設定的MongoDB資料庫目錄：

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

所需的輸出應為每秒12 MB，達到約3000 IOPS，線程數之間的變化很小。

## 虛擬化環境的步驟 {#steps-for-virtualised-environments}

### VMWare {#vmware}

如果您使用WMWare ESX來管理和部署您的虛擬化環境，請確保從ESX控制台執行以下設定以適應MongoDB操作：

1. 關閉記憶體膨脹
1. 為將承載MongoDB資料庫的虛擬機預分配和保留記憶體
1. 使用儲存I/O控制項為 `mongod` 程式。
1. 通過設定，保證承載MongoDB的電腦的CPU資源 [CPU預留](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)

1. 請考慮使用ParaVirtual I/O驅動程式。 如需如何執行此動作的詳細資訊，請查看此 [知識庫文章](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

如需如何使用Amazon Web Services設定MongoDB的檔案，請查看 [設定AWS整合](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) MongoDB網站上的文章。

## 在部署前保護MongoDB {#securing-mongodb-before-deployment}

請查看此貼文 [安全部署MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) 以了解部署前如何保護資料庫配置的相關建議。

## Dispatcher {#dispatcher}

### 選擇Dispatcher的作業系統 {#choosing-the-operating-system-for-the-dispatcher}

為了正確提供MongoDB部署，將托管Dispatcher的作業系統必須執行 **Apache httpd** **2.4版或更新版本。**

此外，請確定您組建中使用的所有程式庫都為最新狀態，以將安全性影響降至最低。

### Dispatcher設定 {#dispatcher-configuration}

一般的Dispatcher設定，其作用是單一AEM例項之請求總處理量的十到二十倍。

由於Dispatcher主要是無狀態的，因此可輕鬆水準縮放。 在某些部署中，作者必須受限於無法存取特定資源。 因此，強烈建議您將Dispatcher與Author例項搭配使用。

在沒有Dispatcher的情況下執行AEM將需要SSL終止和負載平衡，才能由其他應用程式執行。 這是必要操作，因為工作階段必須與其建立所在的AEM例項有相關性，這個概念稱為黏著連線。 其目的在於確保內容更新顯示的延遲極低。

檢查 [Dispatcher檔案](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 以取得如何設定的詳細資訊。

### 其他配置 {#additional-configuration}

#### 黏性連線 {#sticky-connections}

黏著連線可確保一個使用者的個人化頁面和工作階段資料都在AEM的相同例項上撰寫。 此資料會儲存在例項上，因此來自相同使用者的後續請求會傳回至相同例項。

建議針對將請求路由至AEM例項的所有內層啟用黏著連線，鼓勵後續請求連至相同的AEM例項。 這有助於將執行個體之間更新內容時可注意到的延遲降至最低。

#### 長期過期 {#long-expires}

依預設，從AEM Dispatcher傳送的內容具有「上次修改時間」和「Etag」標題，且沒有內容過期的指示。 這可確保使用者介面一律會取得資源的最新版本，也表示瀏覽器將執行GET操作以檢查資源是否已變更。 視頁面載入而定，這可能會導致HTTP回應為304（未修改）的多個請求。 對於已知不會過期的資源，設定「過期」標題並移除「上次修改時間」和「ETag」標題，會導致快取內容，直到「過期」標題中的日期符合為止，才會提出進一步的更新請求。

不過，使用此方法表示在過期標題過期之前，沒有合理的方式可讓資源在瀏覽器中過期。 為了緩解此問題，可將HtmlClientLibraryManager設定為對用戶端程式庫使用不可變的URL。

這些URL必定不會變更。 當URL中包含之資源的內文變更時，變更會自動反映在URL中，確保瀏覽器會要求正確版本的資源。

預設配置將一個選擇器添加到HtmlClientLibraryManager中。 資源是選取器，會在Dispatcher中快取，且選取器保持不變。 此外，此選取器也可用來確保正確的過期行為。 預設選取器會遵循 `lc-.*?-lc` 模式。 以下Apache httpd配置指令將確保所有與該模式匹配的請求都以適當的到期時間提供。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### 無嗅 {#no-sniff}

若內容以無內容類型傳出，許多瀏覽器會透過讀取內容的前幾個位元組來嘗試猜測內容類型。 這叫「嗅探」。 嗅探會開啟安全漏洞，因為可寫入儲存庫的用戶可能上傳沒有內容類型的惡意內容。

因此，建議您新增 `no-sniff` 標題至dispatcher提供的資源。 不過，Dispatcher不會快取標題。 這意味著從本地檔案系統提供的任何內容都將由其擴展確定其內容類型，而不是使用其源AEM伺服器的原始內容類型標頭。

如果已知Web應用程式從不提供快取資源（沒有檔案類型），則無法安全地啟用嗅探。

您可以包含啟用「無嗅探」：

```xml
Header set X-Content-Type-Options "nosniff"
```

也可選擇性地啟用：

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### 內容安全性原則 {#content-security-policy}

預設的Dispatcher設定允許開啟的內容安全性原則，也稱為CSP。 這可讓頁面從所有網域載入資源，但須受瀏覽器沙箱的預設原則限制。

最好限制資源可從哪個位置載入，以避免從不受信任的或未驗證的外部伺服器將代碼載入到javascript引擎中。

CSP可微調策略。 不過，在複雜的應用程式中，CSP標頭必須謹慎開發，因為限制太嚴格的原則可能會破壞使用者介面的部分。

>[!NOTE]
>
>如需此功能的詳細資訊，請參閱 [內容安全策略上的OWASP頁](https://www.owasp.org/index.php/Content_Security_Policy).

### 大小調整 {#sizing}

如需大小調整的詳細資訊，請參閱 [硬體調整指南](/help/managing/hardware-sizing-guidelines.md).

### MongoDB效能優化 {#mongodb-performance-optimization}

有關MongoDB效能的一般資訊，請參見 [分析MongoDB效能](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## 已知限制 {#known-limitations}

### 同時安裝 {#concurrent-installations}

雖然MongoMK支援同時使用多個AEM例項搭配單一資料庫，但不支援同時安裝。

要解決此問題，請確保先使用單個成員運行安裝，然後在完成安裝後添加其他成員。

### 頁面名稱長度 {#page-name-length}

如果AEM在MongoMK永續性管理器部署上執行， [頁面名稱上限為150個字元。](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[請參閱MongoDB檔案](https://docs.mongodb.com/manual/reference/limits/) 讓自己也熟悉MongoDB本身的已知限制和臨界值。
