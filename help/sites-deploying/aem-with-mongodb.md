---
title: Adobe Experience Manager與MongoDB
description: 瞭解成功使用MongoDB部署Adobe Experience Manager所需的工作和考量事項。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '6185'
ht-degree: 0%

---

# Adobe Experience Manager與MongoDB{#aem-with-mongodb}

本文旨在促進對於成功使用MongoDB部署AEM (Adobe Experience Manager)所需的工作和考量事項的瞭解。

如需與部署相關的詳細資訊，請參閱 [部署和維護](/help/sites-deploying/deploy.md) 一節。

## 何時搭配AEM使用MongoDB {#when-to-use-mongodb-with-aem}

MongoDB通常用於支援符合下列其中一項條件的AEM作者部署：

* 每天超過1000位不重複使用者；
* 同時有100位以上的使用者；
* 大量頁面編輯；
* 大型轉出或啟用。

上述標準僅適用於作者執行個體，不適用於所有應以TarMK為基礎之發佈執行個體。 由於作者執行個體不允許未驗證的存取，因此使用者數會參照已驗證的使用者。

如果不符合條件，則建議使用TarMK活動/待命部署來解決可用性問題。 一般而言，在縮放需求超過單一硬體專案所能達到的需求時，應考慮MongoDB。

>[!NOTE]
>
>有關作者執行個體規模及同時使用者定義的其他資訊，請參閱 [硬體大小調整准則](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### 針對AEM的最小MongoDB部署 {#minimal-mongodb-deployment-for-aem}

以下是MongoDB上AEM的最低部署。 為簡化起見，我們已將SSL終止和HTTP Proxy元件標準化。 它包含單一MongoDB復本集，包含一個主要和兩個次要復本。

![chlimage_1-4](assets/chlimage_1-4.png)

最低的部署需要三個 `mongod` 設定為復本集的執行個體。 一個執行個體被選為主要執行個體，而其他執行個體是次要執行個體，並由管理該選擇 `mongod`. 附加到每個執行個體是本機磁碟。 因此，叢集可以支援負載，建議在每秒超過3000個I/O作業(IOPS)的情況下，最低處理量為每秒12 MB。

AEM作者已連線至 `mongod` 例項，讓每個AEM作者連線到全部三個 `mongod` 執行個體。 寫入操作會傳送到主要執行個體，而讀取操作可從任何執行個體讀取。 流量會根據Dispatcher的負載分配至任何一個使用中的AEM編寫執行個體。 Oak資料存放區是 `FileDataStore`和MongoDB監控由MMS或MongoDB Ops Manager提供，視部署位置而定。 作業系統層級和記錄檔監控由第三方解決方案提供，例如Splunk或Ganglia。

在此部署中，成功實施需要所有元件。 任何缺少的元件都會讓實作無法運作。

### 作業系統 {#operating-systems}

如需AEM 6支援的作業系統清單，請參閱 [技術需求頁面](/help/sites-deploying/technical-requirements.md).

### 環境 {#environments}

如果執行專案的不同技術團隊之間有良好的溝通，即可支援虛擬化環境。 這項支援包括執行AEM的團隊、擁有作業系統的團隊，以及管理虛擬化基礎建設的團隊。

有些特定需求涵蓋MongoDB執行個體的I/O容量，這些需求必須由管理虛擬化環境的團隊來管理。 如果專案使用雲端部署(例如Amazon Web Services)，則必須布建具有足夠I/O容量和一致性的執行個體，以支援MongoDB執行個體。 否則，MongoDB流程和Oak存放庫會執行不可靠且不規則。

在虛擬化環境中，MongoDB需要特定的I/O和VM設定，以確保MongoDB的儲存引擎不會受到VMWare資源配置原則的損害。 成功的實作可確保各個團隊之間沒有障礙，而且所有團隊都已註冊可提供所需的效能。

## 硬體考量事項 {#hardware-considerations}

### 儲存空間 {#storage}

為了達到最佳效能的讀寫傳輸量，而不需要過早的水準擴充，MongoDB通常需要SSD儲存裝置或效能相當於SSD的儲存裝置。

### RAM {#ram}

使用MMAP儲存引擎的MongoDB 2.6和3.0版需要資料庫的工作集及其索引符合RAM。

RAM不足會導致效能大幅降低。 工作集和資料庫的大小與應用程式高度相關。 雖然可以做出一些估計，但最可靠的判斷所需RAM大小的方法是建置AEM應用程式並進行負載測試。

為了協助負載測試過程，可以假設工作集與資料庫總大小的比率如下：

* SSD儲存為1:10
* 硬碟儲存空間為1:3

這些比率表示SSD部署需要200 GB的RAM才能使用2 TB的資料庫。

雖然相同的限制適用於MongoDB 3.0中的WiredTiger儲存引擎，但工作集、RAM和頁面錯誤之間的關聯性並不強。 WiredTiger的記憶體對應方式與MMAP儲存引擎不同。

>[!NOTE]
>
>Adobe建議針對使用MongoDB 3.0的AEM 6.1部署，使用WiredTiger儲存引擎。

### 資料存放區 {#data-store}

由於MongoDB工作集限制，建議獨立於MongoDB維護資料存放區。 在大多數環境中， `FileDataStore` 應該使用適用於所有AEM執行個體的NAS。 若是使用Amazon Web Services的情況，也有 `S3 DataStore`. 如果由於任何原因，資料存放區是在MongoDB中維護，資料存放區的大小應新增到資料庫總大小，並且工作集計算應適當調整。 這種大小調整可能意味著提供更多RAM來維持效能，而不會造成頁面錯誤。

## 監控 {#monitoring}

監視是成功實作專案的重要條件。 只要掌握足夠的知識，便可在MongoDB上執行AEM而不進行監視。 不過，這些知識通常是由專長於部署每個區段的工程師所掌握。

這些專門知識通常包括處理Apache Oak Core的研發工程師和MongoDB專家。

若未在所有層級進行監視，則需要程式碼庫的詳細知識才能診斷問題。 監控功能就緒且針對主要統計資料提供適當指引，實作團隊即可對異常狀況做出適當反應。

雖然可以使用命令列工具來取得叢集操作的快速快照，但要在許多主機上即時執行此作業幾乎是不可能的。 命令列工具很少會在幾分鐘後提供歷史資訊，也絕不允許不同型別量度之間的交叉關聯。 一段短暫的慢速背景 `mongod` 同步作業需要大量手動操作，才能與顯然未連線的虛擬機器器的I/O等待或共用儲存資源的過度寫入層級建立關聯。

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager是MongoDB提供的免費服務，可監控和管理MongoDB執行個體。 它可即時檢視MongoDB叢集的效能和健康情況。 它同時管理雲端和私人託管的執行個體，前提是執行個體可以存取Cloud Manager監控伺服器。

它需要在MongoDB執行個體上安裝代理程式，以連線至監控伺服器。 代理程式有三個層級：

* 自動化代理程式，可完全自動化MongoDB伺服器上的所有專案，
* 可監視的監視代理程式 `mongod` 例項，
* 備份代理程式，可執行資料的排程備份。

雖然使用Cloud Manager來自動維護MongoDB叢集可讓許多例行工作變得更輕鬆，但這並非必要，而且也不會將其用於備份。 選擇Cloud Manager進行監視時，需要監視。

如需MongoDB Cloud Manager的詳細資訊，請參閱 [MongoDB檔案](https://docs.cloud.mongodb.com/).

### MongoDB作業管理員 {#mongodb-ops-manager}

MongoDB Ops Manager與MongoDB Cloud Manager是相同的軟體。 註冊後，Ops Manager即可下載並安裝在本機私人資料中心或任何其他筆記型電腦或桌上型電腦上。 它使用本機MongoDB資料庫來儲存資料，並以與Cloud Manager相同的方式與受管理的伺服器通訊。 如果您的安全性原則禁止監控代理程式，則應使用MongoDB Ops Manager。

### 作業系統監視 {#operating-system-monitoring}

執行AEM MongoDB叢集需要作業系統層級監視。

Ganglia就是這類系統的好例子，它提供了超出基本健康狀態量度（例如CPU、平均負載和可用磁碟空間）所需的範圍與詳細資訊圖片。 若要診斷問題，需要較低層級的資訊，例如平均資訊量集區層級、CPU I/O等待、FIN_WAIT2狀態的通訊端。

### 記錄彙總 {#log-aggregation}

如果叢集內有多部伺服器，生產系統需要集中記錄彙總。 Splunk等軟體支援記錄彙總，可讓團隊分析應用程式的行為模式，而不需手動收集記錄。

## 檢查清單 {#checklists}

本節說明您應採取的各種步驟，以確保在實作專案前已正確設定AEM和MongoDB部署。

### 網路 {#network}

1. 首先，請確定所有主機都有DNS專案
1. 所有主機應該可以透過來自所有其他可路由主機的DNS專案解析
1. 所有MongoDB主機都可從相同叢集中的所有其他MongoDB主機路由
1. MongoDB主機可以將封包路由到MongoDB Cloud Manager和其他監視伺服器
1. AEM伺服器可以將封包路由到所有MongoDB伺服器
1. 任何AEM伺服器與任何MongoDB伺服器之間的封包延遲均小於2毫秒，沒有封包遺失，且標準分佈為1毫秒或更少。
1. 請確定AEM和MongoDB伺服器之間的躍點不超過兩個
1. 兩個MongoDB伺服器之間的躍點不超過兩個
1. 任何核心伺服器(MongoDB或AEM或任何組合)之間都沒有高於OSI第3級的路由器。
1. 如果使用VLAN中繼或任何形式的網路通道，就必須遵守封包延遲檢查。

### AEM設定 {#aem-configuration}

#### 節點存放區設定 {#node-store-configuration}

AEM執行個體必須設定為搭配MongoMK使用AEM。 AEM中MongoMK實作的基礎是檔案節點存放區。

如需如何設定節點存放區的詳細資訊，請參閱 [在AEM中設定節點存放區和資料存放區](/help/sites-deploying/data-store-config.md).

以下是最小MongoDB部署的檔案節點存放區設定範例：

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore for example, FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

其中：

* `mongodburi`
MongoDB伺服器AEM必須連線到。 與預設復本集的所有已知成員建立連線。 如果使用MongoDB Cloud Manager，則會啟用伺服器安全性。 因此，連線字串必須包含合適的使用者名稱和密碼。 非企業版本的MongoDB僅支援使用者名稱和密碼驗證。 如需連線字串語法的詳細資訊，請參閱 [檔案](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
資料庫的名稱。 AEM的預設值為 `aem-author`.

* `customBlobStore`
如果部署將二進位檔儲存在資料庫中，則二進位檔會成為工作集的一部分。 因此，請勿在MongoDB內儲存二進位檔案，偏好使用替代資料存放區，例如 `FileSystem` nas上的資料存放區。

* `cache`
快取大小(MB)。 此空間分佈於 `DocumentNodeStore`. 預設值為256 MB。 不過，Oak的讀取效能受益於較大的快取記憶體。

* `blobCacheSize`
AEM可能會快取經常使用的Blob，以避免從資料存放區重新擷取它們。 這樣做對效能的影響更大，尤其是在MongoDB資料庫中儲存Blob時。 所有以檔案系統為基礎的資料存放區，都受益於作業系統層級的磁碟快取。

#### 資料存放區設定 {#data-store-configuration}

資料存放區是用來儲存大小大於臨界值的檔案。 低於該臨界值時，檔案會儲存為檔案節點存放區中的屬性。 如果 `MongoBlobStore` ，會在MongoDB中建立專用集合以儲存blob。 此集合對 `mongod` 執行個體，並需要 `mongod` 擁有更多RAM以避免效能問題。 因此，建議的設定是避免 `MongoBlobStore` 用於生產部署與使用 `FileDataStore` 由所有AEM執行個體共用的NAS作為後盾。 因為作業系統層級快取在管理檔案時很有效率，所以磁碟上的檔案大小下限應該設定為接近磁碟的區塊大小。 如此可確保檔案系統有效率地使用，而且許多小檔案不會對 `mongod` 執行個體。

以下是使用MongoDB進行最低AEM部署的典型資料存放區設定：

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
位元組大小。 小於或等於此大小的二進位檔會與檔案節點存放區一起儲存。 會儲存二進位檔案的內容，而非儲存blob的ID。 對於大於此大小的二進位檔，二進位檔的ID會儲存為節點集合中檔案的屬性。 而且，二進位檔案的主體會儲存在 `FileDataStore` 在磁碟上。 4096位元組是典型的檔案系統區塊大小。

* `path`
資料存放區根的路徑。 對於MongoMK部署，此路徑必須是所有AEM執行個體都可用的共用檔案系統。 通常使用網路附加儲存(NAS)伺服器。 對於類似Amazon Web Services的雲端部署， `S3DataFileStore` 也可供使用。

* `cacheSizeInMB`
二進位快取的大小總計(MB)。 它可用來快取小於下列值的二進位檔： `maxCacheBinarySize` 設定。

* `maxCachedBinarySize`
在二進位快取中快取的二進位檔案大小上限（位元組）。 若使用檔案系統型資料存放區，不建議對資料存放區快取使用高值，因為作業系統已快取二進位檔案。

#### 停用查詢提示 {#disabling-the-query-hint}

建議您新增屬性，以停用與所有查詢一併傳送的查詢提示 `-Doak.mongo.disableIndexHint=true` 當您啟動AEM時。 如此可確保MongoDB會根據內部統計資料，計算最適合使用的索引。

如果未停用查詢提示，則索引的任何效能調整都不會影響AEM的效能。

#### 啟用MongoMK的永久性快取 {#enable-persistent-cache-for-mongomk}

建議為MongoDB部署啟用持續快取設定，以針對具有高I/O讀取效能的環境最大化速度。 如需詳細資訊，請參閱 [Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## MongoDB作業系統最佳化 {#mongodb-operating-system-optimizations}

### 作業系統支援 {#operating-system-support}

MongoDB 2.6使用記憶體對應儲存引擎，對RAM和磁碟之間作業系統層級管理的某些方面很敏感。 MongoDB執行個體的查詢和讀取效能取決於避免或消除通常稱為頁面錯誤的緩慢I/O作業。 這些問題為套用至 `mongod` 特別處理。 不要與作業系統層級的頁面錯誤混淆。

為了快速作業，MongoDB資料庫應該只存取已經在RAM中的資料。 它必須存取的資料是由索引和資料所組成。 這個索引和資料的集合稱為工作集。 當工作集大於可用的RAM時，MongoDB必須從磁碟中分頁該資料，這會產生I/O成本，並逐出已在記憶體中的其他資料。 如果逐出造成資料從磁碟重新載入，頁面錯誤會占主導地位，效能會降低。 如果工作集是動態和可變的，則會產生更多頁面錯誤以支援操作。

MongoDB可在數種作業系統上執行，包括各種Linux®風格、Windows和macOS。 另請參閱 [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) 以取得其他詳細資訊。 根據您的作業系統選擇，MongoDB有不同的作業系統層級建議。 記錄在 [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) 為了方便起見，請參閱此處摘要。

#### Linux® {#linux}

* 關閉透明的hugpage和磁碟重組。 另請參閱 [透明的大型頁面設定](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) 以取得詳細資訊。
* [調整預讀設定](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 在儲存資料庫檔案的裝置上，以符合您的使用案例。

   * 對於MMAPv1儲存引擎，如果您的工作集大於可用的RAM，而且檔案存取模式是隨機的，請考慮將讀取提前數降低到32或16。 評估不同的設定，以便找出最佳值，最大化常駐記憶體並降低頁面錯誤數目。
   * 對於WiredTiger儲存引擎，無論儲存媒體型別為何（旋轉、SSD等），都請將讀取前設定為0。 一般而言，除非測試顯示可測量、可重複及可靠的好處，以獲得更高的預先讀取值，否則請使用建議的預先讀取設定。 [MongoDB Professional支援](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 可針對非零預先讀取設定提供建議和指引。

* 如果您在虛擬環境中執行RHEL 7 / CentOS 7，請停用調整工具。
* 當RHEL 7/CentOS 7在虛擬環境中執行時，調整工具會自動叫用從效能輸送量衍生的效能設定檔，這會自動將預先讀取設定設為4 MB。 此設定可能會對效能造成負面影響。
* 使用SSD磁碟機的空檔或截止日期磁碟排程器。
* 使用客體VM中虛擬化磁碟機的Noop磁碟排程器。
* 停用NUMA或設定 `vm.zone_reclaim_mode` 至0並執行 [mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 具有節點交錯的例項。 請參閱： [MongoDB與NUMA硬體](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 以取得詳細資訊。

* 調整硬體上的限制值，使其符合您的使用案例。 若為多個 [mongod](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) 或 [蒙古文](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) 例證在相同使用者下執行，請相應地縮放極限值。 請參閱： [UNIX® ulimit設定](https://docs.mongodb.com/manual/reference/ulimit/) 以取得詳細資訊。

* 使用noatime進行 [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) 掛接點。
* 針對您的部署，設定足夠的檔案控制代碼(fs.file-max)、核心pid限制(kernel.pid_max)以及每個處理序的最大執行緒數(kernel.threads-max)。 對於大型系統，下列值可提供良好的起點：

   * fs.file-max值98000，
   * 64000的kernel.pid_max值，
   * andkernel.threads-64000的最大值

* 確定系統已設定交換空間。 如需適當大小的詳細資訊，請參閱作業系統的檔案。
* 請確定系統預設的TCP keepalive已正確設定。 300的值通常可為復本集和共用叢集提供更好的效能。 請參閱： [TCP keepalive時間是否會影響MongoDB部署？](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) ，以取得詳細資訊。

#### Windows {#windows}

* 請考慮停用NTFS「上次存取時間」更新。 此設定類似於在類似Unix的系統上停用atime。

### WiredTiger {#wiredtiger}

截至MongoDB 3.2，MongoDB的預設儲存引擎為WiredTiger儲存引擎。 此引擎提供一些強大且可擴充的功能，因此更適合各種一般資料庫工作負荷。 以下各節將說明這些功能。

#### 檔案層級並行 {#document-level-concurrency}

WiredTiger使用檔案層級的並行控制來進行寫入作業。 因此，多個使用者端可同時修改集合的不同檔案。

對於大多數的讀寫作業，WiredTiger使用開放式並行控制。 WiredTiger只使用全域、資料庫和集合等層級的目的鎖定。 當儲存引擎偵測到兩個作業之間的衝突時，其中一個作業會產生寫入衝突，導致MongoDB以透明方式重試該作業。 某些全域作業（通常為涉及多個資料庫的短期作業）仍需要全域「執行個體範圍」鎖定。

某些其他作業（例如卸除集合）仍需要專屬的資料庫鎖定。

#### 快照和查核點 {#snapshots-and-checkpoints}

WiredTiger使用MultiVersion Concurrency Control (MVCC)。 作業開始時，WiredTiger會提供資料到交易的時間點快照。 快照可呈現記憶體中資料的一致檢視。

寫入磁碟時，WiredTiger會以一致的方式將快照中的所有資料寫入磁碟。 現在 —  [經久耐用](https://docs.mongodb.com/manual/reference/glossary/#term-durable) 資料在資料檔案中充當查核點。 查核點可確保資料檔案與上一個查核點一致（含上一個查核點）。 也就是說，查核點可作為復原點。

MongoDB會設定WiredTiger以60秒或2 GB日誌資料的間隔建立檢查點（即將快照資料寫入磁碟）。

在寫入新查核點期間，先前的查核點仍然有效。 因此，即使MongoDB在寫入新查核點時終止或發生錯誤，在重新啟動時，MongoDB仍可從最後一個有效的查核點復原。

當WiredTiger的中繼資料表自動更新以參考新查核點時，新查核點將變為可存取且永久性。 存取新查核點後，WiredTiger會從舊查核點釋放頁面。

使用WiredTiger，即使不使用 [日誌](https://docs.mongodb.com/manual/reference/glossary/#term-durable)，MongoDB可從最後一個查核點復原；不過，若要復原最後一個查核點之後所做的變更，請使用執行 [日誌](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 日誌 {#journal}

WiredTiger使用預先寫入交易登入組合，搭配 [查核點](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) 以確保資料耐久性。

WiredTiger日誌會在查核點之間儲存所有資料修改。 如果MongoDB在查核點之間結束，它會使用日誌來重播自上次查核點以來修改的所有資料。 有關MongoDB將日誌資料寫入磁碟的頻率的資訊，請參閱 [日誌程式](https://docs.mongodb.com/manual/core/journaling/#journal-process).

WiredTiger日誌是使用 [貼齊](https://docs.mongodb.com/manual/core/journaling/#journal-process) 壓縮程式庫。 若要指定替代壓縮演演算法或不壓縮，請使用 [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 設定。

另請參閱 [使用WiredTiger進行日誌](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>WiredTiger的最小記錄大小為128位元組。 如果記錄檔記錄為128位元組或更小，WiredTiger不會壓縮該記錄。
>
>您可以透過設定來停用日誌 [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) 設為false，這會減少維護日誌的額外負荷。
>
>的 [獨立](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) 執行個體，不使用日誌表示當MongoDB在查核點之間意外退出時，您會遺失一些資料修改。 針對成員 [復本集](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)，復寫程式可提供足夠的耐用性保證。

#### 壓縮 {#compression}

使用WiredTiger時，MongoDB支援所有集合和索引的壓縮。 壓縮可儘量減少儲存裝置的使用，但需額外的CPU。

根據預設，WiredTiger使用區塊壓縮 [貼齊](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 所有集合和的壓縮程式庫 [字首壓縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) 用於所有索引。

若為集合，則使用區塊壓縮 [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 也可供使用。 若要指定替代壓縮演演算法或不壓縮，請使用 [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 設定。

對於索引，為停用 [字首壓縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)，使用 [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) 設定。

壓縮設定也可以在集合和索引建立期間根據每個集合和每個索引進行配置。 另請參閱 [指定儲存引擎選項](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) 和 [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) 選項。

對於大部分的工作負載，預設的壓縮設定可平衡儲存效率與處理需求。

預設也會壓縮WiredTiger日誌。 如需有關日誌壓縮的資訊，請參閱 [日誌](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 記憶體使用率 {#memory-use}

使用WiredTiger時，MongoDB會同時使用WiredTiger內部快取和檔案系統快取。

從3.4版開始，WiredTiger內部快取預設會使用以下兩者中較大的一個：

* 50%的RAM減去1 GB，或
* 256毫巴

根據預設，WiredTiger會針對所有集合使用Snappy區塊壓縮，針對所有索引使用前置詞壓縮。 壓縮預設值可在全域層級設定，也可在集合和索引建立期間根據集合和索引進行設定。

WiredTiger內部快取與磁碟格式中的資料使用不同的表示方式：

* 檔案系統快取中的資料與磁碟上的格式相同，包括資料檔案的任何壓縮優點。 作業系統使用檔案系統快取來減少磁碟I/O。

載入到WiredTiger內部快取的索引與磁碟上的格式具有不同的資料表示方式，但是仍然可以利用索引首碼壓縮來減少RAM使用量。

索引首碼壓縮會從索引欄位中去除重複的通用首碼。

WiredTiger內部快取中的集合資料會解壓縮，並使用與磁碟格式不同的表示方式。 區塊壓縮可大幅節省磁碟上的儲存空間，但資料必須解壓縮才能由伺服器操作。

透過檔案系統快取，MongoDB會自動使用WiredTiger快取或其他處理程式未使用的所有可用記憶體。

若要調整WiredTiger內部快取的大小，請參閱 [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) 和 [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). 請避免增加WiredTiger內部快取大小，使其超過預設值。

### NUMA {#numa}

NUMA （非統一記憶體存取）可讓核心管理記憶體對應到處理器核心的方式。 雖然此程式會嘗試讓核心的記憶體存取速度更快，以確保他們能夠存取所需的資料，但NUMA會干擾MMAP，導致無法預測讀取的額外延遲。 因此，必須針對以下專案停用NUMA `mongod` 處理所有支援的作業系統。

實質上，在NUMA架構中，記憶體會連線至CPU，而CPU會連線至匯流排。 在SMP或UMA架構中，記憶體會連線至匯流排並由CPU共用。 當執行緒在NUMA CPU上分配記憶體時，會根據原則進行分配。 預設值是配置連線到執行緒本機CPU的記憶體，除非沒有可用的記憶體，否則會使用可用CPU的記憶體，但成本較高。 配置之後，記憶體不會在CPU之間移動。 配置是由從父系對話串繼承的原則執行，該對話串最終是啟動程式的對話串。

在許多將電腦視為多核心統一記憶體架構的資料庫中，此情況會導致先讓初始CPU滿滿，之後讓次要CPU滿滿。 如果中央執行緒負責配置記憶體緩衝區，就特別正確。 解決方案是變更用來啟動 `mongod` 執行下列命令來處理：

```shell
numactl --interleaved=all <mongod> -f config
```

此原則會以循環配置方式為所有CPU節點配置記憶體，以確保所有節點上的均分分佈。 它不會產生記憶體的最高效能存取，如同具有多個CPU硬體的系統。 大約一半的記憶體操作速度較慢，而且會透過匯流排，但是 `mongod` 並未以最佳方式寫入NUMA目標，因此這是合理的折衷方案。

### NUMA問題 {#numa-issues}

如果 `mongod` 處理序是從以外的位置啟動 `/etc/init.d` 資料夾，可能尚未以正確的NUMA原則開始。 依預設原則而定，可能會出現問題。 原因是因為適用於MongoDB的各種Linux® Package Manager安裝程式也安裝了包含組態檔的服務 `/etc/init.d` ，會執行上述步驟。 如果您直接從封存安裝並執行MongoDB ( `.tar.gz`)，您必須手動執行 `numactl` 程式。

>[!NOTE]
>
>如需有關可用NUMA原則的詳細資訊，請參閱 [numactl檔案](https://linux.die.net/man/8/numactl).

MongoDB程式在不同配置原則下的行為不同：

```

```

* `-membind=<nodes>`
僅在列出的節點上配置。 Mongod不會在列出的節點上配置記憶體，而且可能不會使用所有可用的記憶體。

* `-cpunodebind=<nodes>`
只在節點上執行。 Mongod只會在指定的節點上執行，而且只會使用這些節點上的可用記憶體。

* `-physcpubind=<nodes>`
僅於列出的CPU （核心）上執行。 Mongod只會在列出的CPU上執行，而且只使用這些CPU上可用的記憶體。

* `--localalloc`
一律在目前節點上配置記憶體，但使用執行緒執行的所有節點。 如果一個執行緒執行配置，則只會使用該CPU可用的記憶體。

* `--preferred=<node>`
偏好配置至節點，但如果偏好節點已滿，則會退回給其他節點。 可以使用定義節點的相對記號。 此外，執行緒會在所有節點上執行。

某些原則可能會造成提供給的可用記憶體不足 `mongod` 程式。 與MySQL不同，MongoDB主動避免作業系統層級分頁，因此 `mongod` 處理序可能會取得較少的可用記憶體。

#### 交換 {#swapping}

由於資料庫的記憶體密集性質，必須停用作業系統層級交換。 MongoDB程式會避免依設計進行交換。

#### 遠端檔案系統 {#remote-filesystems}

不建議將NFS等遠端檔案系統用於MongoDB的內部資料檔案（Mongod處理資料庫檔案），因為它們會導致太多延遲。 請勿混淆Oak Blob (FileDataStore)儲存（建議使用NFS）所需的共用檔案系統。

#### 預先閱讀 {#read-ahead}

提前調整讀取，以便在使用隨機讀取來分頁頁面時，不會從磁碟讀取不必要的區塊。 這樣的結果代表不必要的I/O頻寬消耗。

### Linux®需求 {#linux-requirements}

#### 最低核心版本 {#minimum-kernel-versions}

* **2.6.23** 的 `ext4` 檔案系統

* **2.6.25** 的 `xfs` 檔案系統

#### 資料庫磁碟的建議設定 {#recommended-settings-for-database-disks}

**關閉時間**

建議您 `atime` 會針對包含資料庫的磁碟關閉。

**設定NOOP磁碟排程器**

請執行下列動作：

首先，檢查透過執行以下命令設定的I/O排程器：

```shell
cat /sys/block/sdg/queue/scheduler
```

如果回應為 `noop`，您只需執行其他作業。

如果NOOP不是已設定的I/O排程器，您可以執行以變更它：

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**調整預先讀取值**

建議您在執行MongoDB資料庫的磁碟上使用值32。 此值總計為16 KB。 您可以執行下列動作加以設定：

```shell
sudo blockdev --setra <value> <device>
```

#### 啟用NTP {#enable-ntp}

請確定您已在裝載MongoDB資料庫的機器上安裝並執行NTP。 例如，您可以在CentOS電腦上使用yum Package Manager進行安裝：

```shell
sudo yum install ntp
```

在安裝NTP協助程式並成功啟動後，您可以檢查伺服器的時間偏移的漂移檔案。

#### 停用透明大型頁面 {#disable-transparent-huge-pages}

Red Hat® Linux®使用稱為Transparent Great Pages (THP)的記憶體管理演演算法。 如果您使用作業系統處理資料庫工作負載，建議您停用它。

您可以依照以下程式將其停用：

1. 開啟 `/etc/grub.conf` 檔案於您選擇的文字編輯器中。
1. 將下列行加入grub.conf檔案：

   ```xml
   transparent_hugepage=never
   ```

1. 最後，執行以檢查設定是否已生效：

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果停用THP，上述指令的輸出應該是：

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>如需透明大型頁面的詳細資訊，請參閱此 [文章](https://access.redhat.com/solutions/46111).

#### 停用NUMA {#disable-numa}

在啟用NUMA的大多數安裝中，MongoDB精靈會在透過以服務方式執行時，自動停用它。 `/etc/init.d` 資料夾。

如果不是這種情況，您可以對每個處理序層級停用NUMA。 若要停用，請執行以下命令：

```shell
numactl --interleave=all <path_to_process>
```

位置 `<path_to_process>` 是mongod流程的路徑。

接著，執行下列動作來停用區域回收：

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### 調整mongod程式的ulimit設定 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux®可讓您設定資源配置的控制權，其方式為 `ulimit` 命令。 此設定可由使用者或每個程式來完成。

建議您根據以下規則來設定mongod程式的ulimit [MongoDB建議的ulimit設定](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### 測試MongoDB I/O效能 {#test-mongodb-i-o-performance}

MongoDB提供了一個工具，稱為 `mongoperf` 這是為了測試I/O效能。 建議您使用它來測試組成您基礎建設的所有MongoDB執行個體的效能。

使用方式的詳細資訊 `mongoperf`，檢視 [MongoDB檔案](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>此 `mongoperf` 是在其執行平台上之MongoDB效能的指標。 因此，不應將結果視為生產系統效能的最終結果。
>
>如需更精確的效能結果，您可以使用 `fio` Linux®工具。

**在組成您部署的虛擬機器器上測試讀取效能**

安裝工具之後，切換至MongoDB資料庫目錄以執行測試。 接著，執行以開始第一個測試 `mongoperf`使用此設定：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

對於所有MongoDB執行個體，所需的輸出應高達每秒2 GB (2 GB/s)以及以32個執行緒執行的500.000 IOPS。

執行第二次測試，這次使用記憶體對應檔案，透過設定 `mmf:true` 引數：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

第二次測試的輸出應該會比第一次高很多，表示記憶體傳輸效能。

>[!NOTE]
>
>執行測試時，請檢查作業系統監視系統中相關虛擬機器器的I/O使用狀況統計資料。 如果I/O讀取的值低於100%，表示您的虛擬機器器可能有問題。

**測試主要MongoDB執行個體的寫入效能**

接下來，執行以檢查主要MongoDB執行個體的I/O寫入效能 `mongoperf` 從MongoDB資料庫目錄，使用相同的設定：

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

所需的輸出應為每秒12 MB，並達到約3000 IOPS，而且執行緒數目之間幾乎沒有差異。

## 虛擬化環境的步驟 {#steps-for-virtualised-environments}

### VMWare {#vmware}

如果您使用WMWare ESX來管理和部署虛擬化環境，請務必從ESX主控台執行以下設定，以適應MongoDB操作：

1. 關閉記憶體膨脹
1. 為裝載MongoDB資料庫的虛擬機器器預先配置及保留記憶體
1. 使用儲存I/O控制將足夠的I/O配置給 `mongod` 程式。
1. 透過設定來保證主控MongoDB之機器的CPU資源 [CPU保留](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)

1. 請考慮使用ParaVirtual I/O驅動程式。 另請參閱 [知識庫文章](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

如需有關如何使用Amazon Web Services設定MongoDB的檔案，請檢視 [設定AWS整合](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) MongoDB網站上的文章。

## 部署前保護MongoDB {#securing-mongodb-before-deployment}

檢視此文章於 [安全部署MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) 瞭解部署前如何保護資料庫組態安全的建議。

## Dispatcher {#dispatcher}

### 為Dispatcher選擇作業系統 {#choosing-the-operating-system-for-the-dispatcher}

為了適當地為您的MongoDB部署提供服務，託管Dispatcher的作業系統必須正在執行 **Apache httpd** **版本2.4或更新版本。**

此外，請確定組建中使用的所有程式庫都是最新的，以將安全性影響降至最低。

### Dispatcher 設定 {#dispatcher-configuration}

典型的Dispatcher設定是單一AEM執行個體請求輸送量的10到20倍。

由於Dispatcher是無狀態的，因此它可以輕鬆水平縮放。 在某些部署中，必須限製作者存取特定資源。 建議您搭配編寫執行個體使用Dispatcher。

在沒有Dispatcher的情況下執行AEM需要由其他應用程式執行SSL終止和負載平衡。 這是必要操作，因為工作階段必須和建立工作階段的AEM執行個體有相關性，這個概念稱為粘性連線。 原因是為了確保內容的更新顯示最小的延遲。

檢查 [Dispatcher檔案](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) 以取得如何設定的詳細資訊。

### 其他設定 {#additional-configuration}

#### 黏性連線 {#sticky-connections}

粘性連線可確保同一個使用者的個人化頁面和工作階段資料都是在AEM的相同執行個體上撰寫。 此資料會儲存在同一例項上，因此來自相同使用者的後續請求會傳回至相同例項。

建議對路由傳送請求至AEM執行個體的所有內部層啟用粘性連線，鼓勵後續請求到達相同的AEM執行個體。 這麼做有助於將延遲降至最低，否則在執行個體之間更新內容時，延遲現象會相當明顯。

#### 過期時間過長 {#long-expires}

依預設，從AEM Dispatcher傳送的內容具有Last-Modified和Etag標頭，沒有內容到期的指示。 此流程可確保使用者介面一律取得最新版本的資源。 這也表示瀏覽器會執行GET作業，檢視資源是否已變更。 因此，它可能會產生HTTP回應為304 （未修改）的多個請求，端視頁面載入而定。 對於未過期的資源，設定Expires標頭並移除Last-Modified和ETag標頭會導致快取內容。 而且，在符合Expires標頭中的日期之前，不會提出進一步的更新請求。

不過，使用此方法表示沒有合理的方式可讓資源在Expires標頭過期之前在瀏覽器中過期。 若要緩解此工作流程，可以將HtmlClientLibraryManager設定為使用者端程式庫使用不可變URL。

這些URL保證不會變更。 當URL中包含的資源內文變更時，這些變更會在URL中反映，以確保瀏覽器要求正確版本的資源。

預設設定會將選取器新增至HtmlClientLibraryManager。 作為選擇器，資源會在Dispatcher中快取，且選擇器保持不變。 此外，此選取器也可用來確保正確的到期行為。 預設選取器會遵循 `lc-.*?-lc` 模式。 以下Apache httpd設定指令可確保符合該模式的所有請求都以適當的到期時間提供。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### 無嗅探 {#no-sniff}

其中傳送的內容不含內容型別，許多瀏覽器會嘗試透過讀取內容的前幾個位元組來猜測內容型別。 此方法稱為「探查」。 嗅探會開啟安全性弱點，因為可以寫入存放庫的使用者可能會上傳沒有內容型別的惡意內容。

因此，建議您新增 `no-sniff` 標頭給Dispatcher提供的資源。 不過，Dispatcher不會快取標頭。 因此，這表示任何從本機檔案系統提供的內容都會由其擴充功能決定其內容型別，而非使用來自其原始AEM伺服器的原始內容型別標頭。

如果已知網頁應用程式從未提供沒有檔案型別的快取資源，則無法安全地啟用嗅探。

您可以啟用「無嗅探（含括在內）」：

```xml
Header set X-Content-Type-Options "nosniff"
```

也可以選擇啟用：

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### 內容安全性原則 {#content-security-policy}

預設的Dispatcher設定允許開啟內容安全性原則（也稱為CSP）。 這些設定可讓頁面根據瀏覽器沙箱的預設原則，從所有網域載入資源。

最好限制可從何處載入資源，以避免從不受信任或未驗證的外部伺服器將程式碼載入JavaScript引擎。

CSP可讓您微調原則。 不過，在複雜的應用程式中，開發CSP標頭時須謹慎，因為過於嚴格的原則可能會破壞部分使用者介面。

>[!NOTE]
>
>如需此運作方式的詳細資訊，請參閱 [內容安全性原則的OWASP頁面](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

### 大小調整 {#sizing}

如需有關大小調整的詳細資訊，請參閱 [硬體大小調整准則](/help/managing/hardware-sizing-guidelines.md).

### MongoDB效能最佳化 {#mongodb-performance-optimization}

如需MongoDB效能的一般資訊，請參閱 [分析MongoDB效能](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## 已知限制 {#known-limitations}

### 同時安裝 {#concurrent-installations}

雖然MongoMK支援同時使用具有單一資料庫的多個AEM執行個體，但並不支援同時安裝。

若要解決此問題，請確定先使用單一成員執行安裝，並在第一個成員完成安裝後新增其他成員。

### 頁面名稱長度 {#page-name-length}

如果AEM在MongoMK持續性管理員部署中執行， [頁面名稱長度上限為150個字元。](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>請參閱 [MongoDB檔案](https://docs.mongodb.com/manual/reference/limits/) 以便熟悉MongoDB的已知限制和臨界值。
