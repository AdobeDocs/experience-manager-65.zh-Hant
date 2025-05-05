---
title: 使用離線重新索引以減少升級期間的停機時間
description: 瞭解如何使用離線重新索引方法，以減少執行AEM升級時的系統停機時間。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 0%

---

# 使用離線重新索引以減少升級期間的停機時間 {#offline-reindexing-to-reduce-downtime-during-upgrades}

## 簡介 {#introduction}

升級Adobe Experience Manager的主要挑戰之一，是執行就地升級時與製作環境相關的停機時間。 內容作者在升級期間將無法存取環境。 因此，最好將執行升級所需的時間減至最少。 對於大型存放庫，尤其是AEM Assets專案，通常具有大型資料存放庫和每小時大量的資產上傳，重新索引Oak索引需要佔升級時間的很大百分比。

本節說明如何使用Oak執行工具在執行升級之前&#x200B;**重新索引存放庫**，以減少實際升級期間的停機時間。 顯示的步驟可套用至AEM 6.4及更高版本的[Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)索引。

## 概觀 {#overview}

隨著功能集的展開，新版本的AEM會引入Oak索引定義的變更。 在升級AEM執行個體時，對Oak索引的變更會強制重新索引。 由於資產中的文字（例如PDF檔案中的文字）會被擷取及編制索引，因此重新索引對於資產部署而言成本較高。 使用MongoMK存放庫時，資料會透過網路持續存在，進一步增加重新索引所花費的時間。

在升級期間，大多數客戶面臨的問題是縮短停機時間。 解決方案是在升級期間&#x200B;**略過**&#x200B;重新索引活動。 若要達成此目的，請先建立新指令&#x200B;**prior**&#x200B;以執行升級，然後在升級期間直接匯入這些指令。

## 方針 {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

其想法是在升級之前使用[Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md)工具針對目標AEM版本的索引定義建立索引。 上圖顯示離線重新索引方法。

此外，這是方法中所述的步驟順序：

1. 系統會先擷取二進位檔中的文字
2. 目標索引定義已建立
3. 已建立離線索引
4. 然後在升級過程中匯入索引

### 文字提取 {#text-extraction}

若要在AEM中啟用完整索引，會擷取二進位檔(例如PDF)的文字並將其新增至索引。 在索引過程中，這通常是昂貴的步驟。 文字擷取是特別建議用於重新索引資產存放庫（因為它們儲存大量二進位檔案）的最佳化步驟。

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

使用包含Tika程式庫的Oak-run工具，可擷取儲存在系統中的二進位檔文字。 您可以在升級前複製生產系統，並可用於此文字擷取程式。 此程式接著會透過下列步驟建立文字存放區：

**1. 周遊存放庫並收集二進位檔的詳細資料**

此步驟會產生一個包含二進位檔案元組的CSV檔案，其中包含路徑和blob ID。

從您想要建立索引的目錄執行下列命令。 以下範例假設是存放庫主目錄。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

其中`nodestore path`是`mongo_ur`或`crx-quickstart/repository/segmentstore/`

使用`--fake-ds-path=temp`引數而非`–fds-path`來加速處理序。

**2. 重複使用現有索引**&#x200B;中可用的二進位文字存放區

從現有系統傾印索引資料並擷取文字存放區。

您可以使用以下命令傾印現有的索引資料：

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

其中`nodestore path`是`mongo_ur`或`crx-quickstart/repository/segmentstore/`

然後，使用上述索引傾印來填入存放區：

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

其中`oak-index-name`是全文檢索索引的名稱，例如「lucene」。

**3。 針對上述步驟**&#x200B;中遺漏的二進位檔案，使用Tika程式庫執行文字擷取程式

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

其中`datastore path`是二進位資料存放區的路徑。

建立的文字存放區可以更新，並可在未來重新索引情境時使用。

如需文字擷取程式的詳細資訊，請參閱[Oak執行檔案](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)。

### 離線重新索引 {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

在升級前離線建立Lucene索引。 若使用MongoMK，建議直接在其中一個MongoMk節點上執行，因為這可避免網路額外負荷。

若要離線建立索引，請遵循下列步驟：

**1. 產生目標AEM版本**&#x200B;的Oak Lucene索引定義

傾印現有的索引定義。 發生變更的索引定義是使用目標AEM版本和Oak-run的AdobeGranite存放庫套件組合所產生。

若要從&#x200B;**來源** AEM執行個體傾印索引定義，請執行此命令：

>[!NOTE]
>
>如需有關轉儲索引定義的詳細資訊，請參閱[Oak檔案](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)。

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

其中`datastore path`和`nodestore path`來自&#x200B;**來源** AEM執行個體。

然後，使用目標版本的Granite存放庫套件從&#x200B;**目標** AEM版本產生索引定義。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>只有從`oak-run-1.12.0`版本開始才支援上述索引定義建立程式。 目標定位已使用Granite存放庫套件`com.adobe.granite.repository-x.x.xx.jar`完成。

上述步驟會建立名為`merge-index-definitions_target.json`的JSON檔案，此檔案為索引定義。

**2. 在存放庫中建立查核點**

在長存留期的生產&#x200B;**來源** AEM執行個體中建立查核點。 這應在複製存放庫之前完成。

透過位於`http://serveraddress:serverport/system/console/jmx`的JMX主控台，前往`CheckpointMBean`並建立存留期夠長的查核點（例如200天）。 對此，請叫用`CheckpointMBean#createCheckpoint`並將`17280000000`作為存留期持續時間的引數（以毫秒為單位）。

完成此操作後，複製新建立的查核點ID，並使用JMX `CheckpointMBean#listCheckpoints`驗證存留期。

>[!NOTE]
>
>稍後匯入索引時，會刪除此查核點。

如需詳細資訊，請參閱Oak檔案中的[檢查點建立](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint)。

**為產生的索引定義執行離線索引**

Lucene重新索引可以使用Oak-run離線完成。 此程式會在`indexing-result/indexes`下的磁碟中建立索引資料。 它&#x200B;**不會**&#x200B;寫入存放庫，因此不需要停止執行中的AEM執行個體。 建立的文字存放區會傳入此程式：

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

在MongoMK安裝中使用`--doc-traversal-mode`引數很方便，因為透過將存放庫內容多工緩衝到本機一般檔案，它可大幅改善重新索引時間。 但是，它需要儲存庫大小兩倍的額外磁碟空間。

如果存在MongoMK，則在更接近MongoDB執行個體的執行個體中執行此步驟時，可加速此程式。 如果在同一台電腦上執行，可以避免網路額外負荷。

在[Oak-run檔案中可找到索引編制](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)的其他技術細節。

### 匯入索引 {#importing-indexes}

使用AEM 6.4及更新版本時，AEM具有在啟動順序從磁碟匯入索引的內建功能。 啟動期間會觀察資料夾`<repository>/indexing-result/indexes`是否有索引資料。 在開始新版本的&#x200B;**target** AEM jar之前，您可以在[升級程式](in-place-upgrade.md#performing-the-upgrade)期間將預先建立的索引複製到上述位置。 AEM會將其匯入存放庫，並從系統中移除對應的查核點。 因此，完全避免重新索引。

## 其他秘訣和疑難排解 {#troubleshooting}

在下方，您會找到一些實用的提示和疑難排解指示。

### 減少對即時生產系統的影響 {#reduce-the-impact-on-the-live-production-system}

建議複製生產系統，並使用複製建立離線索引。 如此可消除對生產系統的任何潛在影響。 不過，生產系統中需要呈現匯入索引所需的查核點。 因此，在複製前先建立查核點非常重要。

### 準備Runbook並試用執行 {#prepare-a-runbook-and-trial-run}

建議先準備[Runbook](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade-planning.html?lang=zh-Hant#building-the-upgrade-and-rollback-runbook)並執行一些試驗，然後再在生產環境中執行升級。

### 具有離線索引的檔案周遊模式 {#doc-traversal-mode-with-offline-indexing}

離線索引需要遍訪整個存放庫。 使用MongoMK安裝時，會透過網路存取存放庫，影響索引程式的效能。 其中一個選項是對MongoDB復本本身執行離線索引程式，這將消除網路負荷。 另一個選項是使用檔案周遊模式。

可將命令列引數`—doc-traversal`新增至Oak-run命令以套用檔案周遊模式，以進行離線索引。 此模式會將本機磁碟中整個存放庫的復本卷製成平面檔案，並使用它來執行索引。
