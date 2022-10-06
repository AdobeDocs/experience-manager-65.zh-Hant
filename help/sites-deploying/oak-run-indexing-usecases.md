---
title: Oak-run.jar索引使用案例
seo-title: Oak-run.jar Indexing Use Cases
description: 了解使用Oak-run工具執行索引的各種使用者案例。
seo-description: Learn about the various user cases for performing indexing with the Oak-run tool.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# Oak-run.jar索引使用案例{#oak-run-jar-indexing-use-cases}

Oak-run支援在命令列上建立使用案例的索引，而無須透過AEM JMX主控台協調這些使用案例的執行。

使用oak-run.jar index命令方法管理Oak索引的主要優點如下：

1. Oak-run index命令為AEM 6.4提供新的索引工具集。
1. Oak-run可縮短重新索引的時間，減少大型存放庫的重新索引時間。
1. Oak-run可減少AEM中重新索引期間的資源耗用量，整體系統效能更佳。
1. Oak-run提供帶外重新索引，支援必須提供生產環境，且無法忍受維護或停機，因此需要重新索引。

以下各節將提供示例命令。 oak-run index命令支援所有NodeStore和BlobStore設定。 以下提供的範例說明有FileDataStore和SegmentNodeStore的設定。

## 使用案例1 — 索引一致性檢查 {#usercase1indexconsistencycheck}

這是與索引損壞相關的使用案例。 在某些情況下，無法確定哪些索引已損壞。 因此，Adobe提供了以下工具：

1. 對所有索引執行索引一致性檢查，並提供索引有效且無效的報告；
1. 即使無法存取AEM，工具仍可使用；
1. 使用簡單。

檢查損壞的索引可以通過 `--index-consistency-check` 操作：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

這會在 `indexing-result/index-consistency-check-report.txt`. 如需範例報表，請參閱下方：

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

支援和系統管理員現在可以使用此工具快速確定哪些索引已損壞，然後重新索引。

## 使用案例2 — 索引統計資訊 {#usecase2indexstatistics}

為診斷查詢效能Adobe的某些情況，通常需要現有索引定義，從客戶設定中索引相關統計資訊。 到目前為止，這些資訊分散在多個資源中。 為了更方便疑難排解，Adobe已建立工具，可：

1. 將系統上存在的所有索引定義轉儲到單個JSON檔案中；

1. 從現有索引中轉儲重要統計資訊；

1. 離線分析的轉儲索引內容；

1. 即使AEM無法存取，仍可使用

現在，可透過下列操作索引命令執行上述操作：

* `--index-info`  — 收集和轉儲與索引相關的各種統計資訊

* `--index-definitions`  — 收集和轉儲索引定義

* `--index-dump`  — 轉儲索引內容

請參閱下方命令在實際中如何運作的範例：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

報表將產生於 `indexing-result/index-info.txt` 和 `indexing-result/index-definitions.json`

此外，您也可透過Web主控台提供相同的詳細資訊，且會成為設定傾印Zip的一部分。 您可在下列位置存取這些區段：

`https://serverhost:serverport/system/console/status-oak-index-defn`

### 優點 {#uc2benefits}

此工具可讓您快速收集與索引或查詢問題相關的所有必要詳細資訊，並縮短擷取此資訊所花的時間。

## 使用案例3 — 重新索引 {#usecase3reindexing}

視 [藍本](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)，在某些情況下需要執行重新索引。 目前，重新索引是透過設定 `reindex` 標幟為 `true` 通過CRXDE或Index Manager用戶介面在索引定義節點中。 標幟設定後，會以非同步方式重新建立索引。

在重新索引方面應注意以下幾點：

* 重新索引在 `DocumentNodeStore` 比較設定 `SegmentNodeStore` 設定所有內容都為本地的位置；

* 在目前的設計中，重新索引發生時，非同步索引器會遭到封鎖，而所有其他非同步索引都會過時，且在索引期間沒有取得更新。 因此，若系統正在使用中，使用者可能看不到最新的結果；
* 重新索引涉及遍歷整個儲存庫，這會給AEM設定帶來高負載，從而影響最終用戶體驗；
* 若 `DocumentNodeStore` 在安裝中重新索引可能需要相當長的時間，如果到Mongo資料庫的連接在操作中出現故障，則必須從頭開始重新索引；

* 在某些情況下，重新索引可能需要很長的時間，因為會擷取文字。 這主要是用於具有大量PDF檔案的設定，其中用於文本提取的時間會影響索引時間。

為達成這些目標，Oak-run索引工具支援不同模式，可視需要使用。 oak-run index命令提供下列優點：

* **帶外重新索引** - oak執行重新索引可與執行中的AEM設定分開執行，因此可將對使用中AEM例項的影響降至最低；

* **出入重新索引**  — 重新編製索引不影響編製索引的操作。 這表示非同步索引器可以繼續為其他索引建立索引；

* **簡化DocumentNodeStore安裝的重新索引**  — 適用於 `DocumentNodeStore` 安裝時，只需使用一個命令即可完成重新索引，這可確保以最佳的方式完成重新索引；

* **支援更新索引定義和引入新索引定義**

### 重新索引 — DocumentNodeStore {#reindexdocumentnodestore}

針對 `DocumentNodeStore` 安裝可透過單一oak-run命令完成重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

這提供下列優點

* 對執行AEM例項的影響最小。 大部分的讀取可從次要伺服器完成，且執行中的AEM快取不會因為重新索引所需的所有周遊而受到即時影響；
* 使用者也可以透過 `--index-definitions-file` 選項。

### 重新索引 — SegmentNodeStore {#reindexsegmentnodestore}

針對 `SegmentNodeStore` 安裝可通過以下方法之一完成重新索引：

#### 聯機重新索引 — SegmentNodeStore {#onlinereindexsegmentnodestore}

遵循透過設定來重新索引的既定方式 `reindex` 標籤。

#### 線上重新索引 — SegmentNodeStore -AEM執行個體正在執行 {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

針對 `SegmentNodeStore` 只有安裝一個進程才能以讀寫模式訪問段檔案。 因此，在oak-run索引中執行某些作業時，需要執行額外的手動步驟。

這將涉及下列事項：

1. 步驟文字
1. 連接 `oak-run` 至AEM以唯讀模式使用的相同存放庫，並執行索引。 如何達成此目標的範例：

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 最後，透過 `IndexerMBean#importIndex` 從oak-run執行上述命令後儲存索引檔案的路徑執行操作。

在此案例中，您不需要停止AEM伺服器或布建任何新執行個體。 但是，由於索引涉及遍歷整個儲存庫，因此會增加安裝的I/O負載，從而對運行時效能產生負面影響。

#### 線上重新索引 — SegmentNodeStore — 關閉AEM例項 {#onlinereindexsegmentnodestoreaeminstanceisdown}

針對 `SegmentNodeStore` 安裝可透過單一oak-run命令完成重新索引。 不過，AEM例項需要關閉。

您可以使用以下命令觸發重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

此方法與上述方法的差異在於，檢查點建立和索引匯入會自動完成。 缺點在於，AEM需要在此過程中停止運作。

#### 帶外重新索引 — SegmentNodeStore {#outofbandreindexsegmentnodestore}

在此使用案例中，您可以對複製的設定執行重新索引，以將對執行中的AEM例項的影響降至最低：

1. 通過JMX操作建立檢查點。 您可以前往 [JMX控制台](/help/sites-administering/jmx-console.md) 和搜索 `CheckpointManager`. 然後，按一下 **createCheckpoint(long p1)** 以秒為單位的高值運算(例如 **2592000**)。
1. 複製 `crx-quickstart` 資料夾到新電腦
1. 透過oak-run index命令執行重新索引

1. 將生成的索引檔案複製到AEM伺服器

1. 通過JMX導入索引檔案。

在此使用案例中，會假設資料存放區可在其他執行個體上存取，如果 `FileDataStore` 放置在EBS等雲儲存解決方案上。 這會排除以下情境： `FileDataStore` 也會複製。 如果索引定義不執行全文索引，則訪問 `DataStore` 非必要。

## 使用案例4 — 更新索引定義 {#usecase4updatingindexdefinitions}

目前，您可以透過 [ACS確保索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 包。 這可讓您透過內容套件傳送索引定義，之後需要透過設定 `reindex` 標幟為 `true`.

這對於重新索引不需要很長時間的較小安裝非常有用。 但是，對於非常大的儲存庫，重新索引將在相當長的時間內完成。 針對這類情況，我們現在可使用Oak-run索引工具。

Oak-run現在支援以JSON格式提供索引定義，並以頻外模式建立索引，在即時執行個體上不會執行任何變更。

針對此使用案例，您需要考慮的程式為：

1. 開發人員會更新本機執行個體上的索引定義，然後透過 `--index-definitions` 選項

1. 接著，更新的JSON會提供給系統管理員
1. 系統管理員遵循帶外方法，並在不同安裝上準備索引
1. 完成後，在執行中的AEM安裝中會匯入產生的索引檔案。
