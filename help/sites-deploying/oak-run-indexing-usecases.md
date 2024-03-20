---
title: Oak-run.jar索引使用案例
description: 瞭解使用Oak-run工具執行索引的各種使用者案例。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---

# Oak-run.jar索引使用案例{#oak-run-jar-indexing-use-cases}

Oak-run支援在命令列上索引使用案例，不必透過AEM JMX主控台協調這些使用案例的執行。

使用oak-run.jar index命令方法來管理Oak索引的總體優點包括：

1. Oak-run index命令提供適用於AEM 6.4的新索引工具集。
1. Oak-run可減少重新索引的時間，從而減少大型存放庫上的重新索引時間。
1. Oak-run減少在AEM中重新索引時的資源消耗，導致整體更好的系統效能。
1. Oak-run提供頻外重新索引，支援生產必須可用的情況，並且無法忍受維護或停機時間，否則需要重新索引。

以下各節將提供範例指令。 Oak-run index命令支援所有NodeStore和BlobStore設定。 以下提供的範例關於具有FileDataStore和SegmentNodeStore的設定。

## 使用案例1 — 索引一致性檢查 {#usercase1indexconsistencycheck}

這是與索引損毀相關的使用案例。 有時無法判斷哪些索引已損毀。 因此，Adobe提供的工具如下：

1. 對所有索引執行索引一致性檢查，並提供關於哪些索引有效哪些索引無效的報告；
1. 即使AEM無法存取，該工具仍可使用；
1. 使用方便。

檢查損壞的索引的方式如下 `--index-consistency-check` 操作：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

這會在中產生報表 `indexing-result/index-consistency-check-report.txt`. 如需範例報表，請參閱下文：

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### 優點 {#uc1benefits}

支援團隊和系統管理員現在可以使用此工具來快速判斷哪些索引已損毀，然後重新編制索引。

## 使用案例2 — 索引統計資料 {#usecase2indexstatistics}

為了診斷查詢效能Adobe的某些案例，通常需要現有的索引定義、來自客戶設定的索引相關統計資料。 目前為止，這項資訊分散在多個資源中。 為了更輕鬆進行疑難排解，Adobe已建立具有以下功能的工具：

1. 將系統上存在的所有索引定義傾印到單一JSON檔案中；

1. 從現有索引傾印重要統計資料；

1. 傾印索引內容以供離線分析；

1. 即使AEM無法存取，仍可使用

上述作業現在可透過下列作業索引命令來完成：

* `--index-info`  — 收集並傾印與索引相關的各種統計資料

* `--index-definitions`  — 收集並傾印索引定義

* `--index-dump`  — 傾印索引內容

請參閱下面的指令實際運作方式範例：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

報告產生於 `indexing-result/index-info.txt` 和 `indexing-result/index-definitions.json`

此外，透過Web控制檯提供相同的詳細資訊，並將成為設定傾印zip的一部分。 您可在下列位置存取這些區段：

`https://serverhost:serverport/system/console/status-oak-index-defn`

### 優點 {#uc2benefits}

此工具可讓您快速收集與索引或查詢問題相關的所有必要詳細資訊，並減少擷取此資訊所花費的時間。

## 使用案例3 — 重新索引 {#usecase3reindexing}

依據 [情境](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)有時候，必須執行重新索引。 目前，重新索引是透過設定 `reindex` 標幟到 `true` 在索引定義節點中，透過CRXDE或透過Index Manager使用者介面。 設定標幟後，會以非同步方式完成重新索引。

關於重新索引要注意以下幾點：

* 重新索引在下列日期要慢很多： `DocumentNodeStore` 設定比較 `SegmentNodeStore` 設定所有內容為本機；

* 使用目前的設計，當重新索引發生時，非同步索引器會遭到封鎖，而所有其他非同步索引會過時，且在索引期間不會更新。 因此，如果系統正在使用，使用者可能不會看到最新結果；
* 重新索引涉及周遊整個存放庫，這可能對AEM設定造成高負載，從而影響一般使用者體驗；
* 針對 `DocumentNodeStore` 在其中重新索引可能需要相當長的時間的安裝，如果與Mongo資料庫的連線在作業期間失敗，則必須從頭開始重新索引；

* 有時候，由於文字擷取，重新索引可能需要很長的時間。 這是特定於具有許多PDF檔案的設定，其中花費在文字擷取上的時間可能會影響索引時間。

為了滿足這些目標，Oak-run索引工具支援可視需要使用之重新索引的不同模式。 oak-run index指令提供下列優點：

* **頻外重新索引** - Oak-run重新索引可以與正在執行的AEM設定分開完成，因此可將對正在使用的AEM執行個體的影響降至最低；

* **非同道重新索引**  — 重新索引不影響索引操作。 這表示非同步索引器可以繼續索引其他索引；

* **DocumentNodeStore安裝的簡化重新索引**  — 用於 `DocumentNodeStore` 安裝，重新索引可以使用單一命令完成，以確保以最佳方式完成重新索引；

* **支援更新索引定義及引入新索引定義**

### 重新索引 — 檔案節點存放區 {#reindexdocumentnodestore}

的 `DocumentNodeStore` 安裝可透過單一oak-run命令完成重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

這樣將提供下列優點

* 對執行AEM執行個體影響極小。 大部分的讀取可以從次要伺服器完成，而且由於重新索引所需的所有周遊，執行AEM快取不會受到不利的影響；
* 使用者也可透過 `--index-definitions-file` 選項。

### 重新索引 — SegmentNodeStore {#reindexsegmentnodestore}

的 `SegmentNodeStore` 安裝可透過下列其中一種方式完成重新索引：

#### 線上重新索引 — 區段節點存放區 {#onlinereindexsegmentnodestore}

遵循透過設定完成重新索引的既定方式 `reindex` 標幟。

#### 線上重新索引 — SegmentNodeStore - AEM執行個體正在執行 {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

的 `SegmentNodeStore` 安裝時，只有一個處理程式能夠以讀寫模式存取區段檔案。 因此，Oak-run索引中的一些操作需要執行額外的手動步驟。

這將涉及以下專案：

1. 步驟文字
1. 連線 `oak-run` 以唯讀模式移至AEM使用的相同存放庫，並執行索引。 如何達成此目標的範例：

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 最後，匯入建立的索引檔案，方式為 `IndexerMBean#importIndex` oak-run在執行上述命令後儲存索引檔案的路徑中的操作。

在此案例中，您不需要停止AEM伺服器或布建任何新執行個體。 但是，由於索引涉及遍歷整個存放庫，這會增加安裝上的I/O負載，對執行階段效能產生負面影響。

#### 線上重新索引 — SegmentNodeStore - AEM執行個體已關閉 {#onlinereindexsegmentnodestoreaeminstanceisdown}

的 `SegmentNodeStore` 安裝，重新索引可透過單一oak-run命令完成。 不過，必須關閉AEM執行個體。

您可以使用以下命令觸發重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

此方法與上述方法的不同之處在於，查核點建立和索引匯入會自動完成。 缺點是AEM在此過程中必須關閉。

#### 頻外重新索引 — SegmentNodeStore {#outofbandreindexsegmentnodestore}

在此使用案例中，您可以在複製的設定上執行重新索引，以將對正在執行的AEM執行個體造成的影響降至最低：

1. 透過JMX作業建立查核點。 您可以前往 [JMX主控台](/help/sites-administering/jmx-console.md) 並搜尋 `CheckpointManager`. 然後，按一下 **createCheckpoint(long p1)** 以秒為單位使用過期值上限的作業(例如， **2592000**)。
1. 複製 `crx-quickstart` 資料夾至新電腦
1. 透過oak-run index命令執行重新索引

1. 將產生的索引檔案複製到AEM伺服器

1. 透過JMX匯入索引檔案。

在此使用案例中，我們假設資料存放區可在其他執行個體上存取，但若有下列情況，則可能無法存取： `FileDataStore` 會放置在雲端型儲存解決方案（例如EBS）上。 這排除了以下情況 `FileDataStore` 亦已複製。 如果索引定義未執行全文檢索索引，則存取 `DataStore` 非必要。

## 使用案例4 — 更新索引定義 {#usecase4updatingindexdefinitions}

目前，您可以透過以下方式傳送索引定義變更： [ACS確認索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 封裝。 這允許透過內容包來傳送索引定義，之後需要透過設定來執行重新索引。 `reindex` 標幟到 `true`.

這項操作適用於重新索引時間不長的小型安裝。 然而，對於大型存放庫，重新索引會在相當長的時間內完成。 對於這種情況，我們現在可以使用Oak-run索引工具。

Oak-run現在支援提供JSON格式的索引定義，以及在未對即時執行個體執行變更的頻外模式下建立索引。

針對此使用案例要考慮的流程為：

1. 開發人員將更新本機執行個體上的索引定義，然後透過 `--index-definitions` 選項

1. 更新的JSON隨後會提供給系統管理員
1. 系統管理員遵循頻外方法，在不同的安裝上準備索引
1. 完成此操作後，產生的索引檔案會匯入到正在執行的AEM安裝中。
