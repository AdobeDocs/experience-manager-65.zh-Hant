---
title: Oak-run.jar索引使用案例
seo-title: Oak-run.jar Indexing Use Cases
description: 瞭解使用Oak-run工具執行索引的各種用戶案例。
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

Oak-run支援在命令行上對使用案例進行索引，而無需通過AEMJMX控制台協調這些使用案例的執行。

使用oak-run.jar index命令方法管理Oak索引的主要好處是：

1. Oak-run index命令為6.4提供了新的索AEM引工具集。
1. Oak-run減少了重新索引的時間，減少了大型資料庫的重新索引時間。
1. Oak-run減少了重新索引過程中的資源消耗AEM，從而整體上提高了系統效能。
1. Oak-run提供帶外重新索引，支援生產必須可用的情況，並且不能容忍維護或停機，否則需要重新索引。

以下各節將提供示例命令。 oak-run index命令支援所有NodeStore和BlobStore設定。 下面提供的示例圍繞具有FileDataStore和SegmentNodeStore的設定。

## 用例1 — 索引一致性檢查 {#usercase1indexconsistencycheck}

這是與索引損壞相關的使用案例。 在某些情況下，無法確定哪些索引已損壞。 因此，Adobe提供了以下工具：

1. 對所有索引執行索引一致性檢查並提供索引有效且無效的報告；
1. 即使無法訪問，該工具AEM也可用；
1. 使用起來很方便。

檢查損壞的索引可通過 `--index-consistency-check` 操作：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

這將在 `indexing-result/index-consistency-check-report.txt`。 有關示例報告，請參閱下面：

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

現在，支援和系統管理員可以使用此工具快速確定哪些索引已損壞，然後重新編製索引。

## 用例2 — 索引統計 {#usecase2indexstatistics}

為診斷查詢效能Adobe中的某些案例，通常需要現有索引定義和客戶設定中與索引相關的統計資訊。 到目前為止，這些資訊分散在多個資源中。 為了簡化故障排除，Adobe建立了以下工具：

1. 轉儲單個JSON檔案中系統上存在的所有索引定義；

1. 從現有索引中轉儲重要統計資訊；

1. 轉儲索引內容以進行離線分析；

1. 即使無法訪問，AEM也將可用

現在，可以通過以下操作索引命令執行上述操作：

* `--index-info`  — 收集和轉儲與索引相關的各種統計資訊

* `--index-definitions`  — 收集和轉儲索引定義

* `--index-dump`  — 轉儲索引內容

請參見下面的命令如何在實際中工作的示例：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

將在 `indexing-result/index-info.txt` 和 `indexing-result/index-definitions.json`

此外，還通過Web控制台提供了相同的詳細資訊，這些資訊將是配置dump zip的一部分。 可在以下位置訪問它們：

`https://serverhost:serverport/system/console/status-oak-index-defn`

### 優點 {#uc2benefits}

此工具可快速收集與索引或查詢問題相關的所有所需詳細資訊，並減少提取此資訊所花的時間。

## 用例3 — 重新索引 {#usecase3reindexing}

取決於 [場景](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)，在某些情況下需要執行重新索引。 當前，通過設定 `reindex` 標籤 `true` 通過CRXDE或「索引管理器」用戶介面在索引定義節點中。 設定標誌後，非同步執行重新索引。

在重新編製索引時需要注意的一點是：

* 重新索引在 `DocumentNodeStore` 設定與 `SegmentNodeStore` 所有內容都是本地內容的設定；

* 在當前設計下，當重新索引發生時，非同步索引器被阻止，而所有其他非同步索引都變得陳舊，在索引期間不獲得更新。 因此，如果系統在使用中，用戶可能看不到最新結果；
* 重新索引涉及遍歷整個儲存庫，這會給設定帶來高負AEM載，從而影響最終用戶體驗；
* 對於 `DocumentNodeStore` 安裝時，重新編製索引可能需要相當長的時間，如果到Mongo資料庫的連接在操作中失敗，則必須從頭開始重新編製索引；

* 在某些情況下，由於文本提取，重新索引可能需要很長時間。 這主要針對具有大量PDF檔案的設定，其中文本提取所花費的時間可能會影響索引時間。

為了實現這些目標，可運行的索引工具支援不同的重新索引模式，這些模式可根據需要使用。 oak-run index命令具有以下優點：

* **帶外重新索引** -oak run reindexing可與運行的設定分AEM開執行，因此，它將對正在使用的實AEM例的影響降至最低；

* **非通道重新索引**  — 重新編製索引時不影響編製索引的操作。 這意味著非同步索引器可以繼續為其他索引編製索引；

* **簡化的DocumentNodeStore安裝索引**  — 用於 `DocumentNodeStore` 安裝時，只需使用一個命令即可完成重新索引，這可確保以最佳化的方式完成重新索引；

* **支援更新索引定義和引入新的索引定義**

### 重新索引 — DocumentNodeStore {#reindexdocumentnodestore}

對於 `DocumentNodeStore` 安裝可通過單條oak-run命令進行重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

這提供了以下好處

* 對運行實例的影AEM響最小。 大多數讀取操作都可從次伺服器完成，而AEM由於重新索引所需的所有遍歷操作，運行的快取不會受到影響；
* 用戶還可以通過 `--index-definitions-file` 的雙曲餘切值。

### 重新索引 — SegmentNodeStore {#reindexsegmentnodestore}

對於 `SegmentNodeStore` 可以通過以下方法之一進行安裝重新索引：

#### 聯機重新索引 — SegmentNodeStore {#onlinereindexsegmentnodestore}

按照通過設定重新索引的既定方式 `reindex` 。

#### 聯機重新索引 — SegmentNodeStore — 實AEM例正在運行 {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

對於 `SegmentNodeStore` 只有一個進程可以在讀寫模式下訪問段檔案。 由於這一點，在運行索引中的一些操作需要採取額外的手動步驟。

這將涉及以下內容：

1. 步驟文本
1. 連接 `oak-run` 到只讀模式下使用AEM的同一儲存庫並執行索引。 如何實現此目標的示例：

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 最後，通過 `IndexerMBean#importIndex` 運行上述命令後，從oak-run保存索引檔案的路徑執行操作。

在此方案中，您不必停止服AEM務器或設定任何新實例。 但是，由於索引涉及遍歷整個儲存庫，因此會增加安裝的I/O負載，從而對運行時效能產生負面影響。

#### 聯機重新索引 — SegmentNodeStore — 實AEM例已關閉 {#onlinereindexsegmentnodestoreaeminstanceisdown}

對於 `SegmentNodeStore` 安裝可通過單條oak-run命令進行重新索引。 但是，AEM需要關閉實例。

可以使用以下命令觸發重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

這種方法與上述方法的不同之處在於，檢查點建立和索引導入是自動完成的。 不利的AEM是，在這個過程中需要降低。

#### 帶外重新索引 — SegmentNodeStore {#outofbandreindexsegmentnodestore}

在此使用情形中，可以對克隆的設定執行重新索引，以最小化對運行實例的AEM影響：

1. 通過JMX操作建立檢查點。 您可以通過 [JMX控制台](/help/sites-administering/jmx-console.md) 並搜索 `CheckpointManager`。 然後，按一下 **createCheckpoint(long p1)** 使用高值的操作（以秒為單位）(例如， **2592000**)。
1. 複製 `crx-quickstart` 資料夾到新電腦
1. 通過oak-run index命令執行重新索引

1. 將生成的索引檔案複製到服AEM務器

1. 通過JMX導入索引檔案。

在此使用情形下，假定資料儲存可以在另一個實例上訪問，如果 `FileDataStore` 放置在基於雲的儲存解決方案（如EBS）上。 這不包括在 `FileDataStore` 也克隆了。 如果索引定義不執行全文索引，則訪問 `DataStore` 不需要。

## 用例4 — 更新索引定義 {#usecase4updatingindexdefinitions}

目前，您可以通過 [ACS確保索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 檔案。 這允許通過內容包傳送索引定義，該內容包稍後需要通過設定 `reindex` 標籤 `true`。

這對於重新編製索引不需要很長時間的較小安裝非常有效。 但是，對於非常大的儲存庫，重新編製索引將在相當長的時間內完成。 對於這類情況，我們現在可以使用橡木制索引工具。

Oak-run現在支援以JSON格式提供索引定義，並支援以帶外模式建立索引，在帶外模式下，即時實例上不執行任何更改。

您需要考慮的此使用案例的流程是：

1. 開發人員將更新本地實例上的索引定義，然後通過 `--index-definitions` 選項

1. 更新後的JSON隨後將提供給系統管理員
1. 系統管理員採用帶外方法，並在其他安裝上準備索引
1. 完成此操作後，將在正在運行的安裝中導入生成的索AEM引檔案。
