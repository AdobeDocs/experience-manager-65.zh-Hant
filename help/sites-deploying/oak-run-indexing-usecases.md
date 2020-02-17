---
title: Oak-run.jar索引使用案例
seo-title: Oak-run.jar索引使用案例
description: 瞭解使用Oak-run工具執行索引的各種使用者案例。
seo-description: 瞭解使用Oak-run工具執行索引的各種使用者案例。
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Oak-run.jar索引使用案例{#oak-run-jar-indexing-use-cases}

Oak-run支援在命令列上建立使用案例索引，而不需透過AEM的JMX主控台協調這些使用案例的執行。

使用oak-run.jar index命令方法管理Oak索引的主要優點包括：

1. Oak-run index命令為AEM 6.4提供新的索引工具集。
1. Oak-run可縮短重新索引的時間，減少大型儲存庫的重新索引時間。
1. Oak-run可降低AEM中重新索引期間的資源消耗，進而提升整體系統效能。
1. Oak-run提供帶外重新索引功能，支援必須有生產可供使用的情況，而且無法容忍需要維護或停機才能重新索引。

以下各節將提供示例命令。 oak-run index命令支援所有NodeStore和BlobStore設定。 以下提供的範例是有關具有FileDataStore和SegmentNodeStore的設定。

## 使用案例1 —— 索引一致性檢查 {#usercase1indexconsistencycheck}

這是與索引損壞相關的使用案例。 在某些情況下，無法確定哪些索引已損壞。 因此，Adobe提供了以下工具：

1. 對所有索引執行索引一致性檢查，並提供索引有效和無效的報告；
1. 即使AEM無法存取，工具仍可使用；
1. 使用起來簡單。

可以通過以下操作來檢查損壞的索 `--index-consistency-check` 引：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

這將在中生成報告 `indexing-result/index-consistency-check-report.txt`。 請參閱以下範例報表：

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

## 使用案例2 —— 索引統計資料 {#usecase2indexstatistics}

若要診斷查詢效能的某些情況，Adobe通常需要現有的索引定義、來自客戶設定的索引相關統計資料。 到目前為止，這些資訊分散在多種資源中。 為方便疑難排解，Adobe已建立工具，可：

1. 將系統上所有索引定義轉儲為單一JSON檔案；

1. 從現有索引中轉儲重要統計資訊；

1. 轉儲索引內容以進行離線分析；

1. 即使AEM無法存取，仍可使用

現在，可通過以下操作索引命令執行上述操作：

* `--index-info` -收集和轉儲與索引相關的各種統計資訊

* `--index-definitions` -收集和轉儲索引定義

* `--index-dump` -轉儲索引內容

請參閱下列指令如何實際運作的範例：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

報表將產生於 `indexing-result/index-info.txt` 和 `indexing-result/index-definitions.json`

此外，Web Console也提供相同的詳細資訊，這些資訊將會包含在設定轉儲zip中。 您可從下列位置存取這些檔案：

`https://serverhost:serverport/system/console/status-oak-index-defn`

### 優點 {#uc2benefits}

此工具可快速收集與索引或查詢問題相關的所有必要詳細資訊，並縮短擷取此資訊的時間。

## 使用案例3 —— 重新建立索引 {#usecase3reindexing}

視情況 [而定](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)，在某些情況下需要重新建立索引。 當前，通過通過CRXDE或「索引管理器」用 `reindex` 戶介面將標 `true` 志設定為索引定義節點中的，可以重新編製索引。 設定旗標後，會以非同步方式重新建立索引。

關於重新編製索引，有些地方需要注意：

* 與所有內容都是本機的設 `DocumentNodeStore` 定相比，在設定 `SegmentNodeStore` 中重新建立索引的速度要慢得多；

* 在目前的設計中，重新建立索引時，非同步索引器會遭到封鎖，而所有其他非同步索引都會失效，因此在建立索引期間不會取得更新。 因此，如果系統在使用中，用戶可能看不到最新的結果；
* 重新建立索引需要遍歷整個儲存庫，這會給AEM設定帶來高負載，進而影響使用者體驗；
* 對於重 `DocumentNodeStore` 新編製索引可能需要相當長時間的安裝，如果在操作過程中與Mongo資料庫的連接失敗，則必須從頭開始編製索引；

* 在某些情況下，由於文字擷取，重新建立索引可能需要很長時間。 這主要是針對具有大量PDF檔案的設定，在這些設定中，擷取文字所花的時間可能會影響索引時間。

為了達到這些目標，Oak-run索引工具支援可視需要使用的不同模式來重新建立索引。 oak-run index命令提供下列優點：

* **帶外重新索引** - oak-run重新索引可與執行中的AEM設定分開進行，因此，可將對使用中的AEM例項的影響降至最低；

* **非通路重新索引** -重新索引可進行，而不會影響索引建立作業。 這表示非同步索引器可以繼續為其他索引建立索引；

* **簡化DocumentNodeStore安裝的重新索引** -對於安裝 `DocumentNodeStore` ，只需使用單一命令即可重新建立索引，以確保以最佳的方式重新建立索引；

* **支援更新索引定義並引入新的索引定義**

### 重新索引- DocumentNodeStore {#reindexdocumentnodestore}

對於 `DocumentNodeStore` 安裝，可透過單一oak-run命令進行重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

這提供下列優點

* 對執行AEM例項的影響最小。 大部分的讀取作業都可從次要伺服器完成，而執行AEM快取並不會因為重新建立索引所需的所有遍歷而受到影響；
* 使用者也可以透過選項提供新索引或更新索引的JSON `--index-definitions-file` 。

### 重新索引- SegmentNodeStore {#reindexsegmentnodestore}

對於 `SegmentNodeStore` 安裝，可以通過以下方法之一重新編製索引：

#### 聯機重新索引- SegmentNodeStore {#onlinereindexsegmentnodestore}

依循已建立的方式，透過設定標幟來重新建立 `reindex` 索引。

#### Online Reindex - SegmentNodeStore - AEM例項正在執行 {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

對於 `SegmentNodeStore` 安裝，只有一個進程可以以讀寫模式訪問段檔案。 由於此，在oak-run索引中的某些操作需要執行額外的手動步驟。

這將涉及以下內容：

1. 步驟文字
1. 將連線 `oak-run` 至AEM以唯讀模式使用的相同儲存庫，並執行索引。 如何達成此目的的範例：

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 最後，從oak-run在執行上述命 `IndexerMBean#importIndex` 令後儲存索引檔案的路徑，透過作業匯入已建立的索引檔案。

在此案例中，您不必停止AEM伺服器或布建任何新例項。 但是，由於索引涉及遍歷整個儲存庫，因此會增加安裝的I/O負載，從而對運行時效能產生負面影響。

#### Online Reindex - SegmentNodeStore - AEM Instance is Shut Down {#onlinereindexsegmentnodestoreaeminstanceisdown}

對於 `SegmentNodeStore` 安裝，可透過單一oak-run命令重新建立索引。 不過，AEM例項必須關閉。

您可以使用下列命令觸發重新建立索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

此方法與上述方法的不同之處在於，檢查點建立和索引導入是自動完成的。 缺點是AEM必須在流程中關閉。

#### 帶外重新索引- SegmentNodeStore {#outofbandreindexsegmentnodestore}

在此使用案例中，您可以對已複製的設定執行重新建立索引，以將對執行中AEM例項的影響降到最低：

1. 透過JMX作業建立查核點。 您可以前往 [JMX Console](/help/sites-administering/jmx-console.md) ，搜尋 `CheckpointManager`。 然後，按一下 **createCheckpoint(long p1)** (operation in seconds)(expiration in seconds, **例如2592000**)。
1. 將檔案 `crx-quickstart` 夾複製到新電腦
1. 透過oak-run index命令執行重新索引

1. 將產生的索引檔案複製至AEM伺服器

1. 透過JMX匯入索引檔案。

在此使用案例中，假定資料儲存可以在其他實例上訪問，如果將其放在基於雲的儲存解決方案（如EBS）上， `FileDataStore` 則可能無法訪問該實例。 這會排除同時複製 `FileDataStore` 的藍本。 如果索引定義不執行全文索引，則不需 `DataStore` 要訪問。

## 使用案例4 —— 更新索引定義 {#usecase4updatingindexdefinitions}

目前，您可以通過 [ACS Ensure Index包發送索引定義更改](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 。 這允許通過內容包發送索引定義，以後需要通過將標誌設定為來執行重新 `reindex` 索引 `true`。

這對於重新建立索引不需要很長時間的較小安裝非常適用。 但是，對於非常大的儲存庫，重新編製索引將在相當長的時間內完成。 針對這些情況，我們現在可以使用Oak-run索引工具。

Oak-run現在支援提供JSON格式的索引定義，並支援在帶外模式中建立索引，在帶外模式中不會對即時執行個體執行任何變更。

您需要考慮的此使用案例流程為：

1. 開發人員會更新本機例項上的索引定義，然後透過選項產生索引定義JSON檔 `--index-definitions` 案

1. 更新的JSON接著會提供給系統管理員
1. 系統管理員採用帶外方法並準備不同安裝上的索引
1. 完成此作業後，產生的索引檔案將會匯入執行中的AEM安裝。

