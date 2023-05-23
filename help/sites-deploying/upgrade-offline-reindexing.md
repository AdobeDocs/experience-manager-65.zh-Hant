---
title: 使用離線重新索引減少升級期間的停機時間
description: 瞭解如何使用離線重新索引方法來減少執行升級時的系AEM統停機時間。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 1%

---

# 使用離線重新索引減少升級期間的停機時間 {#offline-reindexing-to-reduce-downtime-during-upgrades}

## 簡介 {#introduction}

升級Adobe Experience Manager的關鍵挑戰之一是執行就地升級時與作者環境相關的停機時間。 內容作者將無法在升級期間訪問該環境。 因此，最好盡量減少執行升級所花費的時間。 對於大型儲存庫，特別是AEM Assets項目，這些項目通常擁有大型資料儲存並且每小時資產上載量較高，對Oak索引重新編製索引需要相當大比例的升級時間。

本節介紹如何使用Oak-run工具重新索引儲存庫 **先** 執行升級，從而減少實際升級期間的停機時間。 所介紹的步驟可應用於 [盧塞內](https://jackrabbit.apache.org/oak/docs/query/lucene.html) 6.AEM4及更高版本的索引。

## 概觀 {#overview}

新版本的功能AEM集在擴展時對Oak索引定義進行更改。 升級實例時，對Oak索引的更改會強制重新AEM索引。 重新索引對於資產部署而言非常昂貴，因為資產中的文本（例如，pdf檔案中的文本）會被提取並索引。 使用MongoMK儲存庫，資料通過網路永續，從而進一步增加重新索引所花費的時間。

大多數客戶在升級過程中面臨的問題是縮短停機時間。 解決方案是 **跳** 升級期間的重新索引活動。 這可以通過建立新的索引來實現 **先** 執行升級，然後在升級期間直接導入。

## 方法 {#approach}

![離線重索引 — 升級 — 文本提取](assets/offline-reindexing-upgrade-process.png)

其思想是在升級前根據目標版本的索引定義使用AEM以下 [橡樹](/help/sites-deploying/indexing-via-the-oak-run-jar.md) 工具欄。 上圖顯示了離線重新索引的方法。

此外，這是方法中描述的步驟順序：

1. 首先從二進位檔案中提取文本
2. 建立目標索引定義
3. 已建立離線索引
4. 然後在升級過程中導入索引

### 文字提取 {#text-extraction}

要在中啟用完AEM全索引，將從二進位檔案(如PDF)中提取文本並添加到索引中。 這通常是索引過程中一個昂貴的步驟。 文本提取是一種優化步驟，尤其是在資產儲存庫儲存大量二進位檔案時，對其重新索引。

![離線重索引 — 升級 — 文本提取](assets/offline-reindexing-upgrade-text-extraction.png)

系統中儲存的二進位檔案的文本可以使用tika庫的thge oak-run工具提取。 可以在升級之前獲取生產系統的克隆，並可用於此文本提取過程。 然後，此過程通過以下步驟建立文本儲存：

**1. 遍歷儲存庫並收集二進位檔案的詳細資訊**

此步驟將生成包含二進位檔案元組的CSV檔案，該檔案包含路徑和blob ID。

從要從中建立索引的目錄執行以下命令。 以下示例假定儲存庫主目錄。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

位置 `nodestore path` 是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

使用 `--fake-ds-path=temp` 參數 `–fds-path` 加快進程。

**2. 重新使用現有索引中可用的二進位文本儲存**

從現有系統中轉儲索引資料並提取文本儲存。

可以使用以下命令轉儲現有索引資料：

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

位置 `nodestore path` 是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

然後，使用上述索引轉儲填充儲存：

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

位置 `oak-index-name` 是全文索引的名稱，例如&quot;lucene&quot;。

**3. 使用tika庫為上述步驟中遺漏的二進位檔案運行文本提取過程**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

位置 `datastore path` 是二進位資料儲存的路徑。

所建立的文本儲存可以更新，並可以在將來重新索引方案。

有關文本提取過程的詳細資訊，請參閱 [Oak運行文檔](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)。

### 離線重新索引 {#offline-reindexing}

![離線重新索引 — 升級 — 離線重新索引](assets/offline-reindexing-upgrade-offline-reindexing.png)

在升級前離線建立Lucene索引。 如果使用MongoMK，建議直接在一個MongoMk節點上運行它，因為這樣可以避免網路開銷。

要離線建立索引，請執行以下步驟：

**1. 生成目標版本的Oak Lucene索引定AEM義**

轉儲現有索引定義。 使用目標版本和Oak-run的Adobe花崗岩資料庫捆綁包生成AEM了發生更改的索引定義。

從 **源** AEM實例：

>[!NOTE]
>
>有關傾銷指數定義的詳細資訊，請參考 [橡木文檔](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)。

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

位置 `datastore path` 和 `nodestore path` 是 **源** 實AEM例。

然後，從 **目標** 使AEM用目標版本的Granite儲存庫包的版本。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>上述索引定義建立過程僅支援 `oak-run-1.12.0` 版本。 目標是使用花崗岩資料庫捆綁包完成的 `com.adobe.granite.repository-x.x.xx.jar`。

以上步驟建立名為 `merge-index-definitions_target.json` 即索引定義。

**2. 在儲存庫中建立檢查點**

在生產中建立檢查點 **源** 例AEM如，有很長的一生。 在克隆儲存庫之前，應先執行此操作。

通過位於以下位置的JMX控制台 `http://serveraddress:serverport/system/console/jmx`，轉到 `CheckpointMBean` 並建立一個具有足夠長生命週期（例如200天）的檢查點。 為此，請調用 `CheckpointMBean#createCheckpoint` 與 `17280000000` 作為生命期的參數（毫秒）。

完成此操作後，複製新建立的檢查點ID並使用JMX驗證生存期 `CheckpointMBean#listCheckpoints`。

>[!NOTE]
>
>稍後導入索引時，將刪除此檢查點。

有關詳細資訊，請參考 [檢查點建立](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) 從Oak文檔中。

**對生成的索引定義執行離線索引**

Lucene重新索引可以使用oak-run離線完成。 此過程在磁碟中建立索引資料 `indexing-result/indexes`。 是的 **不** 寫入儲存庫，因此不需要停止運行的實AEM例。 建立的文本儲存庫將輸入到此流程中：

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

使用 `--doc-traversal-mode` 參數在MongoMK安裝中非常方便，因為它通過將儲存庫內容假離線到本地平面檔案而大大縮短了重新索引時間。 但是，它需要額外的磁碟空間，其大小是儲存庫的兩倍。

在MongoMK的情況下，如果此步驟是在更接近MongoDB實例的實例中執行，則可以加速此過程。 如果在同一台電腦上運行，則可避免網路開銷。

其他技術詳細資訊可在 [用於索引的Oak運行文檔](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)。

### 導入索引 {#importing-indexes}

在6AEM.4和更新版本AEM中，內置了在啟動順序上從磁碟導入索引的功能。 資料夾 `<repository>/indexing-result/indexes` 在啟動期間監視索引資料是否存在。 在 [升級過程](in-place-upgrade.md#performing-the-upgrade) 開始使用 **目標** 小AEM罐子。 將AEM其導入儲存庫，並從系統中刪除相應的檢查點。 因此完全避免了重新索引。

## 其他提示和故障排除 {#troubleshooting}

在下面，您將找到一些有用的提示和故障排除說明。

### 減少對即時生產系統的影響 {#reduce-the-impact-on-the-live-production-system}

建議克隆生產系統並使用克隆建立離線索引。 這消除了對生產系統的任何潛在影響。 但是，導入索引所需的檢查點需要存在於生產系統中。 因此，在獲取克隆之前建立檢查點至關重要。

### 準備Runbook和試運行 {#prepare-a-runbook-and-trial-run}

建議準備 [Runbook](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) 並在生產中運行升級之前執行一些測試。

### 帶有離線索引的Doc遍歷模式 {#doc-traversal-mode-with-offline-indexing}

離線索引需要對整個儲存庫進行多次遍歷。 使用MongoMK安裝，可以通過網路訪問儲存庫，從而影響索引過程的效能。 一個選項是在MongoDB副本本身上運行離線索引過程，這將消除網路開銷。 另一個選項是使用doc遍歷模式。

可以通過添加命令行參數來應用文檔遍歷模式 `—doc-traversal` 到oak-run命令進行離線索引。 此模式將本地磁碟中整個儲存庫的副本作為平面檔案後線處理，並使用它運行索引。
