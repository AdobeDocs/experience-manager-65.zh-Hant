---
title: 升級程式
seo-title: Upgrade Procedure
description: 了解升級AEM所需遵循的程式。
seo-description: Learn about the procedure you need to follow in order to upgrade AEM.
uuid: 81126a70-c082-4f01-a1ad-7152182da88b
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 5c035d4c-6e03-48b6-8404-800b52d659b8
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 5242600c-2281-46f9-a347-d985b4e319b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# 升級程式 {#upgrade-procedure}

>[!NOTE]
>
>由於大部分AEM升級都是就地執行，因此升級需要製作層級的停機時間。 遵循這些最佳實務，可將發佈層級停機時間最小化或消除。

升級AEM環境時，您需要考慮升級製作環境或發佈環境之間的方法差異，以將作者和使用者的停機時間減至最少。 本頁概述升級當前在AEM 6.x版上運行的AEM拓撲的高級過程。由於製作和發佈層級，以及Mongo和TarMK部署之間的程式不同，因此每個層級和微內核已列在個別區段中。 執行部署時，建議您先升級製作環境、判斷是否成功，然後繼續前往發佈環境。

<!--
>[!IMPORTANT]
>
>The downtime during the upgrade can be significally reduced by indexing the repository before performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)
-->

## TarMK作者階層 {#tarmk-author-tier}

### 啟動拓撲 {#starting-topology}

此部分假定的拓撲由運行在TarMK上且具有冷備用的製作伺服器組成。 從製作伺服器復寫至TarMK發佈伺服器場。 雖然此處未說明，但此方法也可用於使用卸載的部署。 在Author例項上停用復寫代理後，以及重新啟用復寫代理之前，請務必升級或重建新版本上的卸載例項。

![tarmk_starting_topology](assets/tarmk_starting_topology.jpg)

### 升級準備 {#upgrade-preparation}

![upgrade-preparation-author](assets/upgrade-preparation-author.png)

1. 停止內容編寫

1. 停止備用實例

1. 停用作者上的復寫代理

1. 執行 [預升級維護任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md).

### 升級執行 {#upgrade-execution}

![execute_upgrade](assets/execute_upgrade.jpg)

1. 執行 [就地升級](/help/sites-deploying/in-place-upgrade.md)
1. 更新Dispatcher模組 *若有需要*

1. QA驗證升級

1. 關閉製作例項。

### 如果成功 {#if-successful}

![if_successful](assets/if_successful.jpg)

1. 複製升級實例以建立新的冷備用

1. 啟動Author例項

1. 啟動備用實例。

### 如果失敗（回滾） {#if-unsuccessful-rollback}

![回滾](assets/rollback.jpg)

1. 將冷備用實例啟動為新主實例

1. 從冷待機重建製作環境。

## MongoMK製作叢集 {#mongomk-author-cluster}

### 啟動拓撲 {#starting-topology-1}

此區段的假設拓撲包含MongoMK製作叢集，其中至少包含兩個AEM製作執行個體，且至少有兩個MongoMK資料庫作為後備。 所有製作執行個體都共用資料存放區。 這些步驟應同時套用至S3和檔案資料存放區。 從製作伺服器復寫至TarMK發佈伺服器陣列。

![mongo拓撲](assets/mongo-topology.jpg)

### 升級準備 {#upgrade-preparation-1}

![mongo-upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. 停止內容編寫
1. 克隆資料儲存以進行備份
1. 除了一個AEM Author例項（您的主要作者）以外，請停止所有
1. 從副本集（即主Mongo實例）中刪除除一個MongoDB節點之外的所有節點
1. 更新 `DocumentNodeStoreService.cfg` 主作者上的檔案，以反映您的單一成員副本集
1. 重新啟動主作者，確保其重新正常啟動
1. 停用主要作者上的復寫代理
1. 執行 [預升級維護任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 在主要製作例項上
1. 如有必要，請使用WiredTiger將主Mongo實例上的MongoDB升級到3.2版

### 升級執行 {#Upgrade-execution-1}

![mongo-execution](assets/mongo-execution.jpg)

1. 執行 [就地升級](/help/sites-deploying/in-place-upgrade.md) 在主要作者上
1. 更新Dispatcher或Web模組 *若有需要*
1. QA驗證升級

### 如果成功 {#if-successful-1}

![mongo-secondaries](assets/mongo-secondaries.jpg)

1. 建立新的6.5製作執行個體，並連線至升級的Mongo執行個體

1. 重建已從群集中刪除的MongoDB節點

1. 更新 `DocumentNodeStoreService.cfg` 要反映完整副本集的檔案

1. 重新啟動Author例項，一次一個

1. 移除複製的資料存放區。

### 如果失敗（回滾）  {#if-unsuccessful-rollback-2}

![mongo-rollback](assets/mongo-rollback.jpg)

1. 重新設定次要製作執行個體以連線至複製的資料存放區

1. 關閉升級的Author主執行個體

1. 關閉升級的Mongo主實例。

1. 啟動次Mongo實例，其中一個實例作為新主實例

1. 設定 `DocumentNodeStoreService.cfg` 次Author實例上的檔案，以指向尚未升級的Mongo實例的複製副本集

1. 啟動次要製作例項

1. 清除升級的製作例項、Mongo節點和資料存放區。

## TarMK發佈伺服器陣列 {#tarmk-publish-farm}

### TarMK發佈伺服器陣列 {#tarmk-publish-farm-1}

此區段的假設拓撲包含兩個TarMK發佈執行個體，前端為Dispatcher，後端為負載平衡器。 從製作伺服器復寫至TarMK發佈伺服器陣列。

![tarmk-pub-farmv5](assets/tarmk-pub-farmv5.png)

### 升級執行 {#upgrade-execution-2}

![upgrade-publish2](assets/upgrade-publish2.png)

1. 在負載平衡器上停止發佈2例項的流量
1. 執行 [升級前維護](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 在第2版
1. 執行 [就地升級](/help/sites-deploying/in-place-upgrade.md) 在第2版
1. 更新Dispatcher或Web模組 *若有需要*
1. 排清Dispatcher快取
1. QA會透過防火牆後的Dispatcher驗證Publish 2
1. 關閉發佈2
1. 複製Publish 2例項
1. 開始發佈2

### 如果成功 {#if-successful-2}

![upgrade-publish1](assets/upgrade-publish1.png)

1. 啟用流量以發佈2
1. 停止流量以發佈1
1. 停止Publish 1例項
1. 將Publish 1例項取代為Publish 2
1. 更新Dispatcher或Web模組 *若有需要*
1. 排清發佈1的Dispatcher快取
1. 開始發佈1
1. QA會透過防火牆後的Dispatcher驗證Publish 1

### 如果失敗（回滾） {#if-unsuccessful-rollback-1}

![pub_rollback](assets/pub_rollback.jpg)

1. 建立發佈1的副本
1. 將Publish 2例項取代為Publish 1復本
1. 排清發佈2的Dispatcher快取
1. 開始發佈2
1. QA會透過防火牆後的Dispatcher驗證Publish 2
1. 啟用流量以發佈2

## 最終升級步驟 {#final-upgrade-steps}

1. 啟用流量以發佈1
1. QA會從公用URL執行最終驗證
1. 從製作環境啟用復寫代理
1. 繼續內容製作
1. 執行 [升級後檢查](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).

![fal](assets/final.jpg)
