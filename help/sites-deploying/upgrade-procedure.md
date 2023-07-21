---
title: 升級程式
description: 瞭解升級Adobe Experience Manager (AEM)的程式。
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 5242600c-2281-46f9-a347-d985b4e319b3
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# 升級程式 {#upgrade-procedure}

>[!NOTE]
>
>由於大部分的Adobe Experience Manager (AEM)升級都會就地執行，因此升級作業需要製作層級的停機時間。 透過遵循這些最佳實務，您可以最小化或消除發佈層級停機時間。

升級AEM環境時，您必須考慮升級作者環境或發佈環境之間方法上的差異，以將作者和一般使用者的停機時間降至最低。 此頁面概述升級AEM 6.x版本目前所執行AEM拓撲的高階程式。由於程式在製作和發佈層級以及基於Mongo和TarMK的部署之間有所不同，每個層級和微核心都列在單獨的區段中。 執行部署時，Adobe建議先升級作者環境、判斷是否成功，然後繼續前往發佈環境。

<!--
>[!IMPORTANT]
>
>The downtime during the upgrade can be significally reduced by indexing the repository before performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)
-->

## TarMK作者階層 {#tarmk-author-tier}

### 起始拓撲 {#starting-topology}

此區段的假設拓撲包含在TarMK上執行且具有「冷待命」的Author伺服器。 從Author伺服器復寫至TarMK發佈伺服器陣列。 雖然這裡未說明，但此方法也可用於使用解除安裝的部署。 在作者執行個體上停用復寫代理程式之後，以及重新啟用它們之前，請務必在新版本上升級或重建解除安裝執行個體。

![tarmk_starting_topology](assets/tarmk_starting_topology.jpg)

### 升級準備 {#upgrade-preparation}

![upgrade-preparation-author](assets/upgrade-preparation-author.png)

1. 停止內容製作。

1. 停止待命執行個體。

1. 停用作者上的復寫代理。

1. 執行 [升級前維護任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md).

### 升級執行 {#upgrade-execution}

![execute_upgrade](assets/execute_upgrade.jpg)

1. 執行 [就地升級](/help/sites-deploying/in-place-upgrade.md).
1. 更新Dispatcher模組 *如有需要*.

1. QA會驗證升級。

1. 關閉作者執行個體。

### 如果成功 {#if-successful}

![if_successful](assets/if_successful.jpg)

1. 複製升級的執行個體以建立「冷待命」。

1. 啟動Author例項。

1. 啟動待命執行個體。

### 如果失敗（復原） {#if-unsuccessful-rollback}

![復原](assets/rollback.jpg)

1. 啟動「冷待命」執行處理作為新的「主要」。

1. 從冷待命重新建置作者環境。

## MongoMK作者叢集 {#mongomk-author-cluster}

### 起始拓撲 {#starting-topology-1}

此區段的假設拓撲包含至少兩個AEM Author執行個體的MongoMK製作叢集，且由至少兩個MongoMK資料庫支援。 所有作者執行個體都會共用資料存放區。 這些步驟應同時套用至S3和檔案資料存放區。 從Author伺服器到TarMK Publish伺服器陣列進行復寫。

![mongo-topology](assets/mongo-topology.jpg)

### 升級準備 {#upgrade-preparation-1}

![mongo-upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. 停止內容製作。
1. 複製資料存放區以進行備份。
1. 停止所有AEM Author例項，但一個AEM Author例項除外，即您的主要作者。
1. 從復本集（您的主要Mongo執行個體）中移除除一個MongoDB節點以外的所有節點。
1. 更新 `DocumentNodeStoreService.cfg` 檔案，以反映您的單一成員復本集。
1. 重新啟動主要作者以確保其正確重新啟動。
1. 停用主要作者上的復寫代理。
1. 執行 [升級前維護任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 在主要作者執行個體上。
1. 如有需要，請使用WiredTiger將主要Mongo執行個體上的MongoDB升級至3.2版。

### 升級執行 {#Upgrade-execution-1}

![mongo-execution](assets/mongo-execution.jpg)

1. 執行 [就地升級](/help/sites-deploying/in-place-upgrade.md) 在主要作者上。
1. 更新Dispatcher或網頁模組 *如有需要*.
1. QA會驗證升級。

### 如果成功 {#if-successful-1}

![mongo-secondaries](assets/mongo-secondaries.jpg)

1. 建立新的6.5編寫執行個體，連線至升級的Mongo執行個體。

1. 重建從叢集移除的MongoDB節點。

1. 更新 `DocumentNodeStoreService.cfg` 檔案以反映完整的復本集。

1. 一次一個重新啟動Author例項。

1. 移除複製的資料存放區。

### 如果失敗（復原）  {#if-unsuccessful-rollback-2}

![mongo-rollback](assets/mongo-rollback.jpg)

1. 重新設定次要Author執行個體，以連線至複製的資料存放區。

1. 關閉升級的作者主要執行個體。

1. 關閉升級的Mongo主要執行個體。

1. 啟動次要Mongo執行個體，並將其中一個執行個體作為新的主要執行個體。

1. 設定 `DocumentNodeStoreService.cfg` 次要Author執行個體上的檔案，以指向尚未升級的Mongo執行個體的復本集。

1. 啟動次要作者執行個體。

1. 清除升級的作者執行個體、Mongo節點和資料存放區。

## TarMK發佈陣列 {#tarmk-publish-farm}

### TarMK發佈陣列 {#tarmk-publish-farm-1}

此區段的假設拓撲包含兩個TarMK發佈執行個體，由Dispatcher前導，而後者由負載平衡器前導。 從Author伺服器複製到TarMK發佈伺服器陣列時發生復寫。

![tarmk-pub-farmv5](assets/tarmk-pub-farmv5.png)

### 升級執行 {#upgrade-execution-2}

![upgrade-publish2](assets/upgrade-publish2.png)

1. 在負載平衡器處停止流向Publish 2執行個體的流量。
1. 執行 [升級前維護](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 發佈時為2。
1. 執行 [就地升級](/help/sites-deploying/in-place-upgrade.md) 發佈時為2。
1. 更新Dispatcher或網頁模組 *如有需要*.
1. 排清Dispatcher快取。
1. QA會透過防火牆後面的Dispatcher驗證Publish 2。
1. 關閉發佈2。
1. 複製Publish 2執行個體。
1. 開始發佈2.

### 如果成功 {#if-successful-2}

![upgrade-publish1](assets/upgrade-publish1.png)

1. 啟用流量以發佈2。
1. 停止流量以發佈1。
1. 停止Publish 1執行個體。
1. 將Publish 1執行個體取代為Publish 2的復本。
1. 更新Dispatcher或網頁模組 *如有需要*.
1. 排清Publish 1的Dispatcher快取。
1. 開始發佈1。
1. QA會透過防火牆後面的Dispatcher驗證Publish 1。

### 如果失敗（復原） {#if-unsuccessful-rollback-1}

![pub_rollback](assets/pub_rollback.jpg)

1. 建立Publish 1的復本。
1. 將Publish 2執行個體取代為Publish 1的復本。
1. 排清Publish 2的Dispatcher快取。
1. 開始發佈2.
1. QA會透過防火牆後面的Dispatcher驗證Publish 2。
1. 啟用流量以發佈2。

## 最終升級步驟 {#final-upgrade-steps}

1. 啟用流量以發佈1。
1. QA會從公用URL執行最終驗證。
1. 從製作環境啟用復寫代理。
1. 繼續內容製作。
1. 執行 [升級後檢查](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).

![final](assets/final.jpg)
