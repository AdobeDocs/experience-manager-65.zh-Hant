---
title: 使用離線重新索引以減少升級期間的停機時間
description: 瞭解如何使用離線重新建立索引方法來減少執行AEM升級時的系統停機時間。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---


# 使用離線重新索引以減少升級期間的停機時間 {#offline-reindexing-to-reduce-downtime-during-upgrades}

## 簡介 {#introduction}

升級Adobe Experience Manager的主要挑戰之一，是執行就地升級時與作者環境相關的停機時間。 內容作者在升級期間將無法存取環境。 因此，最好將執行升級所需的時間降到最低。 對於大型儲存庫，尤其是AEM Assets專案，這些專案通常擁有大型資料儲存空間和每小時高階的資產上傳，重新建立Oak索引的索引需要相當大比例的升級時間。

本節介紹如何在執行升級前使用Oak-run工具重新索 **引儲存庫** ，從而減少實際升級期間的停機時間。 所呈現的步驟可套用至 [AEM 6.4版及更新版本的Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) 索引。

## 概覽 {#overview}

新版AEM會隨著功能集的擴充，對Oak索引定義進行變更。 升級AEM例項時，對Oak索引所做的變更會強制重新建立索引。 重新建立索引對於資產部署而言十分昂貴，因為資產中的文字（例如，pdf檔案中的文字）會擷取並建立索引。 使用MongoMK儲存庫，資料將通過網路保存，從而進一步增加重新編製索引所需的時間。

大多數客戶在升級過程中遇到的問題是縮短停機時間。 解決方案是在升 **級期間** ，略過重新索引活動。 這可在執行升級前建立新 **的內** 容，然後在升級期間直接匯入。

## 方法 {#approach}

![離線——重新索引——升級——文字擷取](assets/offline-reindexing-upgrade-process.png)

其構想是在升級前，根據目標AEM版本的索引定義，使用 [Oak-run工具建立索引](/help/sites-deploying/indexing-via-the-oak-run-jar.md) 。 上圖說明離線重新建立索引的方法。

此外，這是方法中所述步驟的順序：

1. 從二進位檔擷取文字
2. 建立目標索引定義
3. 離線索引已建立
4. 然後在升級過程中導入索引

### 文字提取 {#text-extraction}

若要在AEM中啟用完整索引，會擷取來自二進位檔案（例如PDF）的文字並新增至索引。 這通常是索引程式中的昂貴步驟。 文本抽取是一個優化步驟，特別是在資產儲存庫儲存大量二進位檔案時，重新索引這些儲存庫。

![離線——重新索引——升級——文字擷取](assets/offline-reindexing-upgrade-text-extraction.png)

儲存在系統中的二進位檔案文字，可使用tika程式庫的thge oak-run工具來擷取。 在升級之前可以複製生產系統的克隆，並可用於此文本提取過程。 接著，此程式會透過下列步驟建立文字儲存：

**1. 遍歷儲存庫並收集二進位檔案的詳細資訊**

此步驟會產生包含二進位元組的CSV檔案，其中包含路徑和blob ID。

從要從中建立索引的目錄執行以下命令。 以下示例假定儲存庫主目錄。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

哪 `nodestore path` 里是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

使用參 `--fake-ds-path=temp` 數而非 `–fds-path` 加速處理。

**2. 重複使用現有索引中可用的二進位文字儲存區**

從現有系統轉儲索引資料並提取文本儲存。

可以使用以下命令轉儲現有索引資料：

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

哪 `nodestore path` 里是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

然後，使用上述索引轉儲填充儲存：

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

其中 `oak-index-name` 是全文索引的名稱，例如&quot;lucene&quot;。

**3. 使用tika程式庫執行文字擷取程式，以找出上述步驟中遺漏的二進位檔**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

其中 `datastore path` 是二進位資料儲存的路徑。

可以更新已建立的文字儲存空間，並在日後重新建立索引藍本。

如需文字擷取程式的詳細資訊，請參閱 [Oak-run檔案](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)。

### 離線重新建立索引 {#offline-reindexing}

![離線——重新索引——升級——離線——重新索引](assets/offline-reindexing-upgrade-offline-reindexing.png)

在升級前離線建立Lucene索引。 如果使用MongoMK，建議直接在MongoMk節點之一上執行它，因為這樣可避免網路開銷。

若要離線建立索引，請遵循下列步驟：

**1. 產生目標AEM版本的Oak Lucene索引定義**

轉儲現有索引定義。 已進行變更的索引定義是使用目標AEM版本和oak-run的Adobe Granite儲存庫套裝產生。

要從源 **AEM實例轉儲索引定** 義，請運行以下命令：

>[!NOTE]
>
>有關轉儲索引定義的詳細資訊，請參閱 [Oak檔案](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)。

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

來 `datastore path` 源 `nodestore path` AEM **例項的** 位置和位置。

然後，使用目標版本的 **Granite儲存庫套裝，從Target** AEM版本產生索引定義。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> 上述索引定義建立過程僅從版本開始 `oak-run-1.12.0` 受支援。 定位是使用Granite儲存庫套裝完成 `com.adobe.granite.repository-x.x.xx.jar`。

上述步驟會建立名為索引定 `merge-index-definitions_target.json` 義的JSON檔案。

**2. 在儲存庫中建立檢查點**

在生產來源 **AEM例項中** ，建立具有長存留期的查核點。 應在克隆儲存庫之前完成此操作。

透過位於的JMX主 `http://serveraddress:serverport/system/console/jmx`控台，前 `CheckpointMBean` 往並建立具有足夠長存留期（例如200天）的查核點。 為此，請以 `CheckpointMBean#createCheckpoint` 毫 `17280000000` 秒為存留期間的參數調用。

完成此作業後，請複製新建立的查核點ID，並使用JMX驗證期限 `CheckpointMBean#listCheckpoints`。

>[!NOTE]
>
> 稍後導入索引時，將刪除此查核點。

如需詳細資訊，請參 [閱Oak檔案中](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) ，建立查核點。

**對生成的索引定義執行離線索引**

Lucene可使用oak-run離線完成重新索引。 此過程將在下的磁碟中建立索引資料 `indexing-result/indexes`。 它不 **會寫入** 儲存庫，因此不需要停止執行中的AEM例項。 已建立的文字儲存區會饋送至此程式：

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

MongoMK安裝可 `--doc-traversal-mode` 以方便使用參數，因為它可通過將儲存庫內容假離線到本地平面檔案中，從而大大縮短重新索引時間。 但是，它需要儲存庫大小兩倍的額外磁碟空間。

在MongoMK中，如果在離MongoDB實例更近的實例中執行此步驟，則可加速此過程。 如果在同一台機器上運行，可以避免網路開銷。

如需其他技術詳細資訊，請參 [閱oak-run檔案以索引](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)。

### 導入索引 {#importing-indexes}

在AEM 6.4和更新版本中，AEM具備內建功能，可在啟動順序時從磁碟匯入索引。 在啟動 `<repository>/indexing-result/indexes` 期間，會監視資料夾是否存在索引資料。 您可以在升級程式期間，先將預先建立的索引複製到上述 [位置](in-place-upgrade.md#performing-the-upgrade) ，再從新版本的 **target** AEM jar開始。 AEM會將它匯入儲存庫，並從系統移除對應的查核點。 因此完全避免了重新索引。

## 其他提示與疑難排解 {#troubleshooting}

在下方，您將會找到一些有用的提示和疑難排解指示。

### 降低對即時生產系統的影響 {#reduce-the-impact-on-the-live-production-system}

建議您複製生產系統，並使用克隆建立離線索引。 如此可避免對生產系統造成任何潛在影響。 但是，導入索引所需的檢查點必須存在於生產系統中。 因此，在獲取克隆之前建立檢查點至關重要。

### 準備操作手冊和試用版執行 {#prepare-a-runbook-and-trial-run}

建議您先準備操作 [手冊](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) ，然後執行一些試用版，再在生產中執行升級。

### 具有離線索引的文檔遍歷模式 {#doc-traversal-mode-with-offline-indexing}

離線索引需要對整個儲存庫進行多次遍歷。 在安裝MongoMK後，可通過網路訪問儲存庫，從而影響索引過程的效能。 一個選項是在MongoDB複製副本本身運行離線索引過程，這將消除網路開銷。 另一個選項是使用doc遍歷模式。

Doc遍歷模式可借由將命令列參數新增至oak-run `—doc-traversal` 命令以進行離線索引來套用。 此模式將本地磁碟中整個儲存庫的副本視為平面檔案，並使用它運行索引。
