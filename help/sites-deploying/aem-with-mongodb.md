---
title: Adobe Experience Manager與MongoDB
description: 瞭解在MongoDB中成功部署Adobe Experience Manager所需的任務和注意事項。
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '6408'
ht-degree: 0%

---

# Adobe Experience Manager與MongoDB{#aem-with-mongodb}

本文旨在提高對在MongoDB中成功部署(Adobe Experience Manager)所AEM需任務和注意事項的瞭解。

有關更多與部署相關的資訊，請參考 [部署和維護](/help/sites-deploying/deploy.md) 的雙曲餘切值。

## 何時將MongoDB與 {#when-to-use-mongodb-with-aem}

MongoDB通常用於支援符合以AEM下條件之一的作者部署：

* 每天有1000多個獨立用戶；
* 100多個併發用戶；
* 頁面編輯量大；
* 大型部署或激活。

上述條件僅適用於作者實例，而不適用於應全部基於TarMK的任何發佈實例。 用戶數是指經過身份驗證的用戶，因為作者實例不允許未經身份驗證的訪問。

如果未滿足條件，則建議使用TarMK活動/備用部署來滿足可用性。 通常，在擴展要求比單個硬體項目所能實現的要高的情況下，應考慮MongoDB。

>[!NOTE]
>
>有關作者實例大小和併發用戶定義的其他資訊，請參見 [硬體調整指南](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel)。

### 最小MongoDB部署AEM {#minimal-mongodb-deployment-for-aem}

下面是MongoDB上的最AEM小部署。 為簡單起見，SSL終端和HTTP代理元件被推廣。 它由一個MongoDB複製副本集組成，其中有一個主副本和兩個輔助副本。

![chlimage_1-4](assets/chlimage_1-4.png)

最小部署需要三個 `mongod` 將實例配置為複製副本集。 一個實例被選為主實例，而另一個實例是輔助實例，其選舉由 `mongod`。 連接到每個實例的是本地磁碟。 因此，群集可以支援負載，建議最小吞吐量為12 MB/秒，每秒的I/O操作超過3000次(IOPS)。

作AEM者與 `mongod` 實例，每個作AEM者都連接到所有三個 `mongod` 實例。 寫操作被發送到主實例，讀操作可以從任何實例讀取。 流量根據調度程式對活動作者實例中任何一個實例的負載AEM進行分配。 Oak資料庫 `FileDataStore`，並且MMS或MongoDB Ops Manager根據部署位置提供MongoDB監視。 作業系統級別和日誌監控由第三方解決方案（如Splunk或Ganglia）提供。

在此部署中，成功實施需要所有元件。 任何缺失的元件都會使實現無法正常工作。

### 作業系統 {#operating-systems}

有關6支援的作業系統AEM的清單，請參見 [「技術要求」頁](/help/sites-deploying/technical-requirements.md)。

### 環境 {#environments}

支援虛擬化環境，前提是運行項目的不同技術團隊之間有良好的溝通。 此支援包括正在運AEM行的團隊、擁有作業系統的團隊和管理虛擬化基礎架構的團隊。

MongoDB實例的I/O容量有特定要求，必須由管理虛擬化環境的團隊管理。 如果項目使用雲部署，則必須為實例配置足夠的I/O容量和一致性，以支援MongoDB實例。 否則， MongoDB進程和Oak儲存庫將不可靠且不可靠地執行。

在虛擬化環境中，MongoDB需要特定的I/O和VM配置，以確保MongoDB的儲存引擎不會因VMWare資源分配策略而受損。 成功的實施可確保各個團隊之間沒有任何障礙，並且所有團隊都已註冊以提供所需的效能。

## 硬體注意事項 {#hardware-considerations}

### 儲存空間 {#storage}

為了實現最佳效能的讀寫吞吐量，而不需要過早的橫向擴展，MongoDB通常需要SSD儲存或效能與SSD相當的儲存。

### RAM {#ram}

使用MMAP儲存引擎的MongoDB 2.6和3.0版要求資料庫及其索引的工作集適合RAM。

RAM不足導致效能顯著下降。 工作集和資料庫的大小高度依賴於應用程式。 雖然可以做出一些估計，但確定所需RAM數量的最可靠方法是構建應用AEM程式並對其進行負載測試。

為了幫助執行負載測試過程，可以假定工作集與資料庫總大小的比率如下：

* 1:10用於SSD儲存
* 1:3用於硬碟儲存

這些比率意味著，對於SSD部署，2 TB的資料庫需要200 GB的RAM。

雖然MongoDB 3.0中的WiredTiger儲存引擎也受到同樣的限制，但工作集、RAM和頁面故障之間的關聯並不強烈。 WiredTiger不像MMAP儲存引擎那樣使用記憶體映射。

>[!NOTE]
>
>Adobe建議使用WiredTiger儲存引擎AEM來進行6.1部署，這些部署使用MongoDB 3.0。

### 資料儲存 {#data-store}

由於MongoDB工作集的限制，建議獨立於MongoDB維護資料儲存。 在大多數環境中， `FileDataStore` 應使用所有實例AEM都可用的NAS。 對於使用Amazon Web Services的情況， `S3 DataStore`。 如果出於任何原因，資料儲存在MongoDB內維護，應將資料儲存的大小添加到總資料庫大小中，並相應調整工作集計算。 此調整可能意味著配置更多RAM以保持效能而不出現頁故障。

## 監控 {#monitoring}

監測對於成功實施該項目至關重要。 如果掌握足夠的知識，則可以在AEMMongoDB上運行而不進行監控。 但是，這些知識通常在專門用於部署每個部分的工程師中找到。

這些專業知識通常包括一名在Apache Oak Core公司工作的研發工程師和一名MongoDB公司的專家。

如果不在所有級別進行監控，則需要詳細瞭解代碼庫才能診斷問題。 在對主要統計情況進行監測並提供適當指導的情況下，執行小組可對異常情況作出適當反應。

雖然使用命令行工具可以快速獲取群集操作的快照，但在許多主機上即時執行此操作幾乎是不可能的。 命令行工具很少提供超過幾分鐘的歷史資訊，並且從不允許不同類型的度量之間的交叉關聯。 短暫的慢背景 `mongod` 同步需要大量手動工作，以與I/O Wait或從明顯未連接的虛擬機到共用儲存資源的過多寫入級別相關聯。

### MongoDB雲管理器 {#mongodb-cloud-manager}

MongoDB Cloud Manager是MongoDB提供的免費服務，允許監視和管理MongoDB實例。 它即時地對MongoDB集群的效能和運行狀況進行了分析。 它管理雲實例和私有托管實例，前提是實例可以訪問Cloud Manager監控伺服器。

它要求在MongoDB實例上安裝一個連接到監控伺服器的代理。 代理有三個級別：

* 一個自動化代理，可以完全自動化MongoDB伺服器上的所有內容，
* 可監視 `mongod` 實例，
* 可執行資料定時備份的備份代理。

雖然使用Cloud Manager實現MongoDB群集的維護自動化使許多例行任務更加輕鬆，但它不是必需的，而且也不使用它進行備份。 選擇雲管理器進行監視時，需要進行監視。

有關MongoDB雲管理器的詳細資訊，請參閱 [MongoDB文檔](https://docs.cloud.mongodb.com/)。

### MongoDB Ops管理器 {#mongodb-ops-manager}

MongoDB Ops Manager與MongoDB雲管理器是相同的軟體。 註冊後，Ops Manager可以本地下載並安裝在專用資料中心或任何其他筆記型電腦或台式機上。 它使用本地MongoDB資料庫儲存資料，並以與Cloud Manager相同的方式與受控伺服器通信。 如果您有禁止監視代理的安全策略，則應使用MongoDB Ops Manager。

### 作業系統監視 {#operating-system-monitoring}

運行MongoDB群集需要作業系統級AEM別監視。

Ganglia是此類系統的一個很好的示例，它提供了所需資訊的範圍和詳細資訊，這些資訊超出了基本的運行狀況指標（如CPU、負載平均值和可用磁碟空間）。 要診斷問題，需要低級資訊，如FIN_WAIT2狀態的CPU I/O Wait、套接字。

### 日誌聚合 {#log-aggregation}

對於多個伺服器的群集，生產系統需要集中日誌聚合。 Splunk等軟體支援日誌聚合，並允許團隊分析應用程式的行為模式而無需手動收集日誌。

## 檢查清單 {#checklists}

本節介紹在實施項目之前應採取的各AEM種步驟，以確保正確設定您的部署和MongoDB部署。

### 網路 {#network}

1. 首先，確保所有主機都有DNS條目
1. 所有主機都應通過其DNS條目從所有其他可路由主機解析
1. 所有MongoDB主機都可從同一群集中的所有其他MongoDB主機路由
1. MongoDB主機可以將資料包路由到MongoDB雲管理器和其他監控伺服器
1. 服AEM務器可將資料包路由到所有MongoDB伺服器
1. 任何伺服器和任AEM何MongoDB伺服器之間的資料包延遲都小於兩毫秒，不會丟失資料包，標準分佈則小於一毫秒。
1. 確保MongoDB伺服器與MongoDB伺服器之間不AEM超過兩個跳數
1. 兩個MongoDB伺服器之間不超過兩跳
1. 任何核心伺服器（MongoDB或任何組合）之間沒有高於OSI第3級AEM的路由器。
1. 如果使用VLAN中繼或任何形式的網路隧道，則必須符合資料包延遲檢查。

### 配AEM置 {#aem-configuration}

#### 節點儲存配置 {#node-store-configuration}

實AEM例必須配置為與AEMMongoMK一起使用。 MongoMK實現的基礎是AEM文檔節點儲存。

有關如何配置節點儲存的詳細資訊，請參見 [在中配置節點儲存和資料存AEM儲](/help/sites-deploying/data-store-config.md)。

下面是用於最小MongoDB部署的文檔節點儲存配置示例：

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
MongoDB伺服器AEM必須連接到。 連接到預設複製副本集的所有已知成員。 如果使用MongoDB雲管理器，則會啟用伺服器安全。 因此，連接字串必須包含合適的用戶名和密碼。 非企業版本的MongoDB僅支援用戶名和密碼驗證。 有關連接字串語法的詳細資訊，請參閱 [文檔](https://docs.mongodb.org/manual/reference/connection-string/)。

* `db`
資料庫的名稱。 預設AEM為 
`aem-author`。

* `customBlobStore`
如果部署將二進位檔案儲存在資料庫中，則它們將構成工作集的一部分。 因此，建議不要在MongoDB中儲存二進位檔案，而是選擇像 
`FileSystem` NAS上的資料儲存。

* `cache`
快取大小(MB)。 此空間分佈在中使用的各種快取中 
`DocumentNodeStore`。預設為256 MB。 但是，Oak讀取效能得益於更大的快取。

* `blobCacheSize`
常用的Blob可通過快取來AEM避免從資料儲存中重取它們。 這樣做對效能的影響更大，特別是在MongoDB資料庫中儲存Blob時。 所有基於檔案系統的資料儲存都受益於作業系統級磁碟快取。

#### 資料儲存配置 {#data-store-configuration}

資料儲存用於儲存大於閾值的檔案。 在該閾值以下，檔案作為屬性儲存在文檔節點儲存中。 如果 `MongoBlobStore` ，在MongoDB中建立專用集合以儲存blob。 此收集有助於 `mongod` 實例，並要求 `mongod` 擁有更多記憶體以避免效能問題。 因此，建議的配置是避免 `MongoBlobStore` 用於生產部署和使用 `FileDataStore` 由所有實例之間共用的NASAEM備份。 由於作業系統級快取在管理檔案方面非常高效，因此應將磁碟上檔案的最小大小設定為接近磁碟的塊大小。 這樣可確保檔案系統得到有效的使用，並且許多小文檔不會過多地對檔案的工作集作出貢獻 `mongod` 實例。

以下是典型的Data Store配置，用於使用MongoDBAEM進行最小部署：

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
大小（以位元組為單位）。 小於或等於此大小的二進位檔案與文檔節點儲存一起儲存。 儲存二進位檔案的內容而不是儲存blob的ID。 對於大於此大小的二進位檔案，二進位檔案的ID將作為Document的屬性儲存在節點集合中。 而二進位的主體儲存在 
`FileDataStore` 在磁碟上。 4096位元組是典型的檔案系統塊大小。

* `path`
資料儲存根的路徑。 對於MongoMK部署，此路徑必須是所有實例都可用的共用文AEM件系統。 通常使用網路連接儲存(NAS)伺服器。 對於像Amazon Web Services這樣的雲部署， 
`S3DataFileStore` 的上界。

* `cacheSizeInMB`
二進位快取的總大小(MB)。 它用於快取小於 
`maxCacheBinarySize` 的子菜單。

* `maxCachedBinarySize`
快取在二進位快取中的二進位檔案的最大大小（位元組）。 如果使用基於檔案系統的資料儲存，則不建議為資料儲存快取使用高值，因為作業系統已快取二進位檔案。

#### 禁用查詢提示 {#disabling-the-query-hint}

建議通過添加屬性來禁用與所有查詢一起發送的查詢提示 `-Doak.mongo.disableIndexHint=true` 開始AEM。 這樣可確保MongoDB根據內部統計資料計算使用的最合適的索引。

如果未禁用查詢提示，則索引的任何效能調整都不會影響的性AEM能。

#### 為MongoMK啟用永久快取 {#enable-persistent-cache-for-mongomk}

建議為MongoDB部署啟用持久快取配置，以最大化具有高I/O讀取效能的環境的速度。 有關詳細資訊，請參閱 [Jackrabbit Oak文檔](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html)。

## MongoDB作業系統優化 {#mongodb-operating-system-optimizations}

### 作業系統支援 {#operating-system-support}

MongoDB 2.6使用記憶體映射的儲存引擎，該引擎對RAM和磁碟之間的作業系統級別管理的某些方面非常敏感。 查詢和讀取MongoDB實例的效能依賴於避免或消除通常稱為頁故障的慢速I/O操作。 這些問題是適用於 `mongod` 特別是流程。 不要與作業系統級頁面錯誤混淆。

為了快速操作，MongoDB資料庫應僅訪問RAM中已有的資料。 它必須訪問的資料由索引和資料組成。 此索引和資料集合稱為工作集。 當工作集大於可用RAM時， MongoDB必須從磁碟中將該資料頁入，這會導致I/O成本，從而驅逐記憶體中已有的其他資料。 如果逐出導致從磁碟重新載入資料，則頁面故障將佔主導地位，效能將降低。 如果工作集是動態的和可變的，則會產生更多的頁錯誤以支援操作。

MongoDB在多個作業系統上運行，包括各種Linux®版本、Windows和macOS。 請參閱 [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) 的雙曲餘切值。 根據您的作業系統選擇，MongoDB有不同的作業系統級別建議。 有文檔記錄在 [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) 為了方便而總結。

#### Linux® {#linux}

* 關閉透明頁面和碎片整理。 請參閱 [透明大頁設定](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) 的子菜單。
* [調整預讀設定](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 儲存資料庫檔案的設備上，以便適合您的使用情形。

   * 對於MMAPv1儲存引擎，如果工作集大於可用RAM，且文檔訪問模式是隨機的，請考慮將預讀數降低到32或16。 評估不同的設定，以便您能夠找到一個最佳值，使駐留記憶體最大化並減少頁面故障數。
   * 對於WiredTiger儲存引擎，無論儲存介質類型（旋轉、固態硬碟等）如何，都應將讀前置設定為0。 一般而言，除非測試以更高的預讀值顯示可衡量、可重複且可靠的好處，否則請使用建議的預讀設定。 [MongoDB專業支援](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 可以就非零預讀配置提供建議和指導。

* 如果在虛擬環境中運行RHEL 7 / CentOS 7，請禁用調諧工具。
* 當RHEL 7/CentOS 7在虛擬環境中運行時，調諧的工具將自動調用從效能吞吐量派生的效能配置檔案，該效能配置檔案會自動將預讀設定設定為4 MB。 此設定可能對效能產生負面影響。
* 使用SSD驅動器的noop或截止時間磁碟計畫程式。
* 對來賓VM中的虛擬化驅動器使用noop磁碟計畫程式。
* 禁用NUMA或設定 `vm.zone_reclaim_mode` 到0並運行 [蒙上](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 具有節點交錯的實例。 請參閱： [MongoDB和NUMA硬體](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 的子菜單。

* 調整硬體上的上限值，使其適合您的使用情形。 如果為多 [蒙上](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) 或 [蒙古](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) 實例在同一用戶下運行，相應地縮放ulimit值。 請參閱： [UNIX®限制設定](https://docs.mongodb.com/manual/reference/ulimit/) 的子菜單。

* 將noatime用於 [db路徑](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) 安裝點。
* 為部署配置足夠的檔案句柄(fs.file-max)、內核pid限制(kernel.pid_max)和每個進程的最大線程(kernel.threads-max)。 對於大型系統，以下值提供了良好的起點：

   * fs.file-max值98000,
   * kernel.pid_max值64000,
   * andkernel.threads-max值64000

* 確保系統已配置交換空間。 有關適當規模的詳細資訊，請參閱作業系統文檔。
* 確保系統預設的TCP keepalive設定正確。 值300通常為副本集和共用群集提供更好的效能。 請參閱： [TCP keepalive時間是否影響MongoDB部署？](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) 的上界。

#### Windows {#windows}

* 考慮禁用NTFS「上次訪問時間」更新。 此設定類似於在類似Unix的系統上禁用時間。

### 連線虎 {#wiredtiger}

從MongoDB 3.2開始，MongoDB的預設儲存引擎是WiredTiger儲存引擎。 此引擎提供一些強健和可擴展的功能，使其更適合於全面的一般資料庫工作負載。 以下各節介紹這些功能。

#### 文檔級併發 {#document-level-concurrency}

WiredTiger使用文檔級併發控制進行寫操作。 因此，多個客戶端可以同時修改集合的不同文檔。

對於大多數讀寫操作，WiredTiger使用樂觀的併發控制。 WiredTiger在全局、資料庫和收集級別僅使用意圖鎖。 當儲存引擎檢測到兩個操作之間的衝突時，一個操作會產生寫衝突，導致MongoDB透明地重試該操作。 一些全局操作（通常涉及多個資料庫的短時間操作）仍需要全局「實例範圍」鎖。

某些其他操作（如刪除集合）仍需要獨佔資料庫鎖。

#### 快照和檢查點 {#snapshots-and-checkpoints}

WiredTiger使用MultiVersion併發控制(MVCC)。 在操作開始時，WiredTiger會向事務提供資料的時間點快照。 快照提供記憶體中資料的一致視圖。

在寫入磁碟時， WiredTiger會以一致的方式將快照中的所有資料寫入磁碟，並覆蓋所有資料檔案。 現在。 [耐用](https://docs.mongodb.com/manual/reference/glossary/#term-durable) 資料充當資料檔案中的檢查點。 檢查點確保資料檔案在最後一個檢查點之前（包括最後一個檢查點）保持一致。 即，檢查點可以充當恢復點。

MongoDB將WiredTiger配置為以60秒或2 GB的日誌資料間隔建立檢查點（即將快照資料寫入磁碟）。

在寫入新檢查點期間，上一個檢查點仍然有效。 因此，即使MongoDB在寫入新檢查點時終止或遇到錯誤，在重新啟動時，MongoDB也可以從最後一個有效檢查點恢復。

當WiredTiger的元資料表自動更新以引用新檢查點時，新檢查點將變得可訪問且永久。 一旦可以訪問新檢查點，WiredTiger將從舊檢查點中釋放頁面。

使用WiredTiger，即使沒有 [日誌](https://docs.mongodb.com/manual/reference/glossary/#term-durable),MongoDB可以從最後一個檢查點恢復；但是，要恢復上一個檢查點之後所做的更改，請使用 [日誌](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)。

#### 日誌 {#journal}

WiredTiger使用預寫事務登錄組合 [檢查點](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) 確保資料的持久性。

WiredTiger日誌保留檢查點之間的所有資料修改。 如果MongoDB在檢查點之間存在，則它使用日誌來重放自上次檢查點以來修改的所有資料。 有關MongoDB將日誌資料寫入磁碟的頻率的資訊，請參見 [日誌處理](https://docs.mongodb.com/manual/core/journaling/#journal-process)。

WiredTiger日誌使用 [輕快](https://docs.mongodb.com/manual/core/journaling/#journal-process) 壓縮庫。 要指定替代壓縮算法或無壓縮，請使用 [storage.wiredTiger.engineConfig.journalCompxator](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 的子菜單。

請參閱 [使用WiredTiger日誌](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger)。

>[!NOTE]
>
>WiredTiger的最小日誌記錄大小為128位元組。 如果日誌記錄為128位元組或更小，則WiredTiger不會壓縮該記錄。
>
>可以通過設定 [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) 為false，這樣可減少維護日誌的開銷。
>
>對於 [獨立](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) 實例，不使用日誌意味著當MongoDB意外退出檢查點時，會丟失一些資料修改。 對於 [複製副本集](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)，複製過程可以提供足夠的持久性保證。

#### 壓縮 {#compression}

使用WiredTiger,MongoDB支援對所有集合和索引進行壓縮。 壓縮可以最大限度地減少儲存使用，而另外的CPU則會因此而減少。

預設情況下，WiredTiger使用塊壓縮 [輕快](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 所有集合和壓縮庫 [前置詞壓縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) 的雙曲餘切值。

對於集合，塊壓縮 [茲利布](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 的上界。 要指定替代壓縮算法或無壓縮，請使用 [storage.wiredTiger.collectionConfig.blockExpdor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 的子菜單。

對於索引，禁用 [前置詞壓縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)，使用 [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) 的子菜單。

在收集和索引建立期間，還可以按每個集合和每個索引配置壓縮設定。 請參閱 [指定儲存引擎選項](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) 和 [db.collection.createIndex()storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) 的雙曲餘切值。

對於大多數工作負載，預設壓縮設定平衡了儲存效率和處理要求。

預設情況下，WiredTiger日誌也會被壓縮。 有關日記帳壓縮的資訊，請參見 [日記](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)。

#### 記憶體使用 {#memory-use}

使用WiredTiger時，MongoDB同時使用WiredTiger內部快取和檔案系統快取。

預設情況下，從3.4開始，WiredTiger內部快取使用以下任一大寫：

* 50%的RAM減去1 GB ，或
* 256 MB

預設情況下，WiredTiger對所有集合使用Snappy塊壓縮，對所有索引使用前置詞壓縮。 可在全局級別配置壓縮預設值，也可以在建立收集和索引期間按每個集合和每個索引設定壓縮預設值。

WiredTiger內部快取中的資料與磁碟格式的資料使用不同的表示法：

* 檔案系統快取中的資料與磁碟上的格式相同，包括資料檔案的任何壓縮的好處。 作業系統使用檔案系統快取來減少磁碟I/O。

載入到WiredTiger內部快取中的索引與磁碟格式的資料表示形式不同，但仍然可以利用索引前置詞壓縮來減少RAM的使用。

索引前置詞壓縮會消除索引欄位中的常用前置詞重複。

WiredTiger內部快取中的收集資料未壓縮，並使用與磁碟格式不同的表示形式。 塊壓縮可以顯著節省磁碟儲存，但資料必須解壓縮才能由伺服器處理。

通過檔案系統快取，MongoDB自動使用WiredTiger快取或其他進程未使用的所有可用記憶體。

要調整WiredTiger內部快取的大小，請參見 [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) 和 [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb)。 避免將WiredTiger內部快取大小增加到其預設值以上。

### 努馬 {#numa}

NUMA（非統一記憶體訪問）允許內核管理記憶體映射到處理器內核的方式。 儘管此過程試圖加快內核的記憶體訪問速度以確保它們能夠訪問所需的資料，但NUMA會干擾MMAP引入額外的延遲，因為讀取無法預測。 因此，必須為 `mongod` 處理所有可用的作業系統。

本質上，NUMA架構儲存器連接到CPU,CPU連接到匯流排。 在SMP或UMA架構中，儲存器連接到匯流排並由CPU共用。 當線程在NUMA CPU上分配記憶體時，它根據策略進行分配。 預設情況是分配連接到線程本地CPU的記憶體，除非沒有空閒記憶體，此時它會以較高的成本使用來自空閒CPU的記憶體。 分配後，記憶體不會在CPU之間移動。 分配由從父線程繼承的策略執行，該策略最終是啟動進程的線程。

在許多將電腦視為多核統一記憶體體系結構的資料庫中，這種情況會導致初始CPU首先滿，而次CPU隨後滿。 如果中央線程負責分配記憶體緩衝區，則情況尤其如此。 解決方案是更改用於啟動的主線程的NUMA策略 `mongod` 進程：

```shell
numactl --interleaved=all <mongod> -f config
```

此策略在所有CPU節點上以循環方式分配記憶體，確保在所有節點上均勻分配記憶體。 它不會像在具有多個CPU硬體的系統中那樣生成對記憶體的最高效能訪問。 大約一半的記憶體操作速度較慢，而且在匯流排上，但 `mongod` 並未以最佳方式寫入目標NUMA，因此這是一種合理的折衷。

### NUMA問題 {#numa-issues}

如果 `mongod` 進程從除 `/etc/init.d` 資料夾，可能尚未使用正確的NUMA策略啟動。 根據預設策略的不同，可能會出現問題。 原因是，用於MongoDB的各種Linux®軟體包管理器安裝程式還安裝了包含以下配置檔案的服務 `/etc/init.d` 執行上述步驟。 如果直接從存檔安裝和運行MongoDB( `.tar.gz`)，必須在 `numactl` 處理。

>[!NOTE]
>
>有關NUMA策略的詳細資訊，請參閱 [numactl文檔](https://linux.die.net/man/8/numactl)。

在不同的分配策略下，MongoDB進程的行為不同：

```

```

* `-membind=<nodes>`
僅在列出的節點上分配。 Mongod未在列出的節點上分配記憶體，因此可能不會使用所有可用記憶體。

* `-cpunodebind=<nodes>`
僅在節點上運行。 Mongod僅在指定的節點上運行，並且僅使用這些節點上可用的記憶體。

* `-physcpubind=<nodes>`
僅在列出的CPU（核心）上運行。 Mongod僅在列出的CPU上運行，並且僅使用這些CPU上可用的記憶體。

* `--localalloc`
始終在當前節點上分配記憶體，但使用線程運行的所有節點。 如果一個線程執行分配，則只使用該CPU可用的記憶體。

* `--preferred=<node>`
首選節點分配，但如果首選節點已滿，則回退到其他節點。 可使用用於定義節點的相對符號。 此外，線程在所有節點上運行。

某些策略可能導致提供的可用RAM少於 `mongod` 處理。 與MySQL不同，MongoDB主動避免作業系統級別分頁，因此 `mongod` 進程可能獲得的可用記憶體較少。

#### 交換 {#swapping}

由於資料庫的記憶體密集型特性，必須禁用作業系統級別的交換。 MongoDB進程通過設計避免了交換。

#### 遠程檔案系統 {#remote-filesystems}

不建議將遠程檔案系統（如NFS）用於MongoDB的內部資料檔案（即mongod進程資料庫檔案），因為它們會帶來太多的延遲。 不要與建議使用NFS的Oak Blob儲存(FileDataStore)所需的共用檔案系統混淆。

#### 預讀 {#read-ahead}

調整前讀，以便當使用隨機讀取的頁面調入頁面時，不會從磁碟讀取不必要的塊。 這種結果意味著I/O頻寬的不必要消耗。

### Linux®要求 {#linux-requirements}

#### 最小內核版本 {#minimum-kernel-versions}

* **2.6.23** 為 `ext4` 檔案系統

* **2.6.25** 為 `xfs` 檔案系統

#### 建議的資料庫磁碟設定 {#recommended-settings-for-database-disks}

**關閉時間**

建議 `atime` 已關閉包含資料庫的磁碟。

**設定NOOP磁碟調度程式**

請執行下列動作：

首先，檢查通過運行以下命令設定的I/O調度程式：

```shell
cat /sys/block/sdg/queue/scheduler
```

如果響應為 `noop`你不能再做什麼了。

如果NOOP不是已設定的I/O計畫程式，則可以通過運行以下命令來更改它：

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**調整預讀值**

建議對運行MongoDB資料庫的磁碟使用32值。 此值為16 KB。 可以通過運行以下命令來設定它：

```shell
sudo blockdev --setra <value> <device>
```

#### 啟用NTP {#enable-ntp}

確保在承載MongoDB資料庫的電腦上已安裝並運行NTP。 例如，可以在CentOS電腦上使用yum包管理器來安裝它：

```shell
sudo yum install ntp
```

安裝NTP守護程式並成功啟動後，可以檢查漂移檔案中伺服器的時間偏移。

#### 禁用透明大頁 {#disable-transparent-huge-pages}

Red Hat® Linux®使用稱為「透明大頁」(THP)的記憶體管理算法。 如果正在將作業系統用於資料庫工作負載，建議禁用它。

您可以按照以下步驟禁用它：

1. 開啟 `/etc/grub.conf` 的子菜單。
1. 將以下行添加到grub.conf檔案：

   ```xml
   transparent_hugepage=never
   ```

1. 最後，通過運行以下命令檢查設定是否生效：

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用了THP，則上述命令的輸出應為：

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>有關透明大頁的詳細資訊，請參閱此 [文章](https://access.redhat.com/solutions/46111)。

#### 禁用NUMA {#disable-numa}

在啟用NUMA的大多數安裝中，如果MongoDB守護程式作為服務從 `/etc/init.d` 的子菜單。

如果不是這樣，則可以在每個進程級別上禁用NUMA。 要禁用它，請運行以下命令：

```shell
numactl --interleave=all <path_to_process>
```

位置 `<path_to_process>` 是通往蒙古進程的路。

然後，通過運行以下操作禁用區域回收：

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### 調整mongod進程的上限設定 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux®允許通過以下方式對資源分配進行可配置的控制： `ulimit` 的子菜單。 此配置可以基於用戶或每個進程執行。

建議根據 [MongoDB建議的上限設定](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings)。

#### TestMongoDB I/O效能 {#test-mongodb-i-o-performance}

MongoDB提供了一個名為 `mongoperf` 設計用於testI/O效能。 建議您使用它來test構成基礎架構的所有MongoDB實例的效能。

有關如何使用的資訊 `mongoperf`，查看 [MongoDB文檔](https://docs.mongodb.org/manual/reference/program/mongoperf/)。

>[!NOTE]
>
>的 `mongoperf` 是運行MongoDB的平台上的MongoDB效能的指標。 因此，不應將結果視為生產系統效能的確定結果。
>
>為獲得更準確的效能結果，您可以使用 `fio` Linux®工具。

**Test讀取構成部署的虛擬機上的效能**

安裝該工具後，切換到MongoDB資料庫目錄以運行test。 然後，通過運行來啟動第一個test `mongoperf`使用此配置：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

所有MongoDB實例的所需輸出應高達每秒2 GB(2 GB/s)和以32個線程運行的500.000 IOPS。

通過設定以下項來運行第二個test（此次使用記憶體映射檔案） `mmf:true` 參數：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

第二test的輸出應比第一儲存器的輸出高得多，這表示儲存器傳輸效能。

>[!NOTE]
執行test時，檢查作業系統監視系統中有關虛擬機的I/O使用情況統計資訊。 如果它們表示I/O讀取的值低於100%，則虛擬機可能會出現問題。

**Test主MongoDB實例的寫入效能**

接下來，通過運行檢查主MongoDB實例的I/O寫入效能 `mongoperf` 從MongoDB資料庫目錄中，設定相同：

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

期望的輸出應為每秒12 MB，達到約3000 IOPS，而線程數之間的變化很小。

## 虛擬化環境的步驟 {#steps-for-virtualised-environments}

### VMWare {#vmware}

如果使用WMWare ESX管理和部署虛擬化環境，請確保在ESX控制台中執行以下設定以適應MongoDB操作：

1. 關閉記憶體膨脹
1. 為承載MongoDB資料庫的虛擬機預分配和保留記憶體
1. 使用儲存I/O控制為 `mongod` 處理。
1. 通過設定來保證承載MongoDB的電腦的CPU資源 [CPU保留](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)

1. 請考慮使用ParaVirtual I/O驅動程式。 請參閱 [知識庫文章](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398)。

### Amazon Web Services {#amazon-web-services}

有關如何設定MongoDB與Amazon Web Services的文檔，請查看 [配置AWS整合](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) MongoDB網站上的文章。

## 部署前保護MongoDB {#securing-mongodb-before-deployment}

查看此帖子 [安全部署MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) 有關如何在部署前保護資料庫配置的建議。

## Dispatcher {#dispatcher}

### 為調度程式選擇作業系統 {#choosing-the-operating-system-for-the-dispatcher}

要正確為MongoDB部署服務，必須運行承載Dispatcher的作業系統 **Apache httpd** **版本2.4或更高版本。**

另外，確保構建中使用的所有庫都是最新的，以最大限度地減少對安全的影響。

### 調度程式配置 {#dispatcher-configuration}

典型的Dispatcher配置服務於單個實例的請求吞吐量的10到20AEM倍。

由於Dispatcher是無狀態的，因此它可以輕鬆地水準擴展。 在某些部署中，必須限製作者訪問某些資源。 建議將Dispatcher與作者實例一起使用。

在沒有AEMDispatcher的情況下運行需要由其他應用程式執行SSL終止和負載平衡。 需要此選項，因為會話必須與創AEM建它們的實例具有關聯性，這一概念稱為粘滯連接。 原因是為了確保內容更新顯示最小的延遲。

檢查 [調度程式文檔](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant) 的子菜單。

### 其他配置 {#additional-configuration}

#### 黏性連線 {#sticky-connections}

粘滯連接可確保一個用戶的個性化頁面和會話資料都在同一實例AEM上。 此資料儲存在實例上，因此來自同一用戶的後續請求會返回到同一實例。

建議為所有內部層將請求路由到實例時啟用粘AEM滯連接，鼓勵後續請求到達同AEM一實例。 這樣做有助於最大限度地減少在實例之間更新內容時可注意的延遲。

#### 長期過期 {#long-expires}

預設情況下，從AEMDispatcher發送的內容具有Last-Modified和Etag標頭，但沒有顯示內容的到期。 此流確保用戶介面始終獲取資源的最新版本。 它還意味著瀏覽器執行GET操作以查看資源是否已更改。 結果，它可能導致HTTP響應為304（未修改）的多個請求，這取決於頁負載。 對於未過期的資源，設定「過期」標頭並刪除「上次修改」和「ETag」標頭會導致內容被快取。 而且，在滿足「過期」標頭中的日期之前，不會再發出更新請求。

但是，使用此方法意味著在過期標頭過期之前，沒有合理的方法導致瀏覽器中的資源過期。 要緩解此工作流，可將HtmlClientLibraryManager配置為對客戶端庫使用不可變的URL。

這些URL保證不會更改。 當URL中包含的資源正文更改時，這些更改將反映在URL中，以確保瀏覽器請求資源的正確版本。

預設配置將選擇器添加到HtmlClientLibraryManager。 作為選擇器，資源將快取在Dispatcher中，而選擇器將保持不變。 此選擇器還可用於確保正確的過期行為。 預設選擇器位於 `lc-.*?-lc` 的上界。 以下Apache httpd配置指令確保所有與該模式匹配的請求都在適當的到期時間內得到服務。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### 無嗅 {#no-sniff}

在沒有內容類型的內容發送出去的地方，許多瀏覽器會嘗試通過讀取內容的前幾個位元組來猜測內容類型。 此方法稱為「嗅探」。 嗅探操作會開啟一個安全漏洞，因為可以寫入儲存庫的用戶可能上載沒有內容類型的惡意內容。

因此，建議添加 `no-sniff` 指向由Dispatcher提供的資源。 但是， Dispatcher不快取標頭。 因此，這意味著從本地檔案系統服務的任何內容都具有由其擴展確定的內容類型，而不是使用其源伺服器中的原始內容AEM類型頭。

如果已知Web應用程式從不提供沒有檔案類型的快取資源，則無法安全啟用嗅探。

可以包括啟用「無嗅」：

```xml
Header set X-Content-Type-Options "nosniff"
```

還可以有選擇地啟用它：

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### 內容安全策略 {#content-security-policy}

預設的Dispatcher設定允許開啟的內容安全策略，也稱為CSP。 這些設定允許頁面從受瀏覽器沙箱預設策略約束的所有域載入資源。

最好限制資源可從何處載入，以避免從不受信任的或未經驗證的外來伺服器將代碼載入到JavaScript引擎中。

CSP允許策略的微調。 但是，在複雜的應用程式中，CSP報頭必須謹慎開發，因為過於嚴格的策略可能會破壞用戶介面的部分部分。

>[!NOTE]
有關此操作方式的詳細資訊，請參閱 [內容安全策略上的OWASP頁](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)。

### 調整大小 {#sizing}

有關調整大小的詳細資訊，請參閱 [硬體調整指南](/help/managing/hardware-sizing-guidelines.md)。

### MongoDB效能優化 {#mongodb-performance-optimization}

有關MongoDB效能的一般資訊，請參見 [分析MongoDB效能](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/)。

## 已知限制 {#known-limitations}

### 併發安裝 {#concurrent-installations}

雖然MongoMK支AEM持將多個實例與單個資料庫併發使用，但併發安裝不支援。

要解決此問題，請確保先使用單個成員運行安裝，並在第一個成員完成安裝後添加其他成員。

### 頁名長度 {#page-name-length}

如果AEM在MongoMK持久性管理器部署上運行， [頁名限制為150個字元。](/help/sites-authoring/managing-pages.md)

>[!NOTE]
查看 [MongoDB文檔](https://docs.mongodb.com/manual/reference/limits/) 以便您熟悉MongoDB的已知限制和閾值。
