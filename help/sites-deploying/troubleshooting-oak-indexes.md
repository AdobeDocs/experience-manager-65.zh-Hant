---
title: 疑難排解Oak索引
description: 瞭解如何識別索引是否緩慢、尋找原因並解決問題。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---

# 疑難排解Oak索引{#troubleshooting-oak-indexes}

## 重新索引緩慢  {#slow-re-indexing}

AEM內部重新索引程式會收集存放庫資料並將其儲存在Oak索引中，以支援內容的效能查詢。 在特殊情況下，流程可能會變得緩慢甚至停滯。 本頁作為疑難排解指南，有助於識別索引是否緩慢、找出原因並解決問題。

區分需要花費不適當的長時間重新索引與需要很長時間重新索引很重要，因為這會索引大量內容。 例如，為內容建立索引所需的時間會隨著內容量而調整，因此大型生產存放庫重新建立索引的時間會比小型開發存放庫長。

請參閱 [查詢和建立索引的最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md) 以取得何時及如何重新索引內容的其他資訊。

## 初始偵測 {#initial-detection}

初始偵測緩慢索引需要檢閱 `IndexStats` JMX MBean。 在受影響的AEM執行個體上，執行下列動作：

1. 開啟Web主控台，然後按一下JMX標籤或前往https://&lt;host>：&lt;port>/system/console/jmx (例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))。
1. 導覽至 `IndexStats` Mbeans。
1. 開啟 `IndexStats` 「 」的MBean `async`「和」 `fulltext-async`「。

1. 對於兩個MBean，檢查 **完成** 時間戳記和 **LastIndexTime** 時間戳記距離目前時間不到45分鐘。

1. 對於任一MBean，如果時間值(**完成** 或 **LastIndexedTime**)超過目前時間的45分鐘，則索引作業會失敗或花費太長時間。 此問題會導致非同步索引過時。

## 在強制關機後暫停索引 {#indexing-is-paused-after-a-forced-shutdown}

強制關閉導致AEM在重新啟動後暫停非同步索引長達30分鐘。 此外，這通常需要再花15分鐘來完成第一個重新索引階段，總共約為45分鐘(繫結至 [初始偵測](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) 45分鐘的時間範圍)。 如果索引在強制關機後暫停：

1. 首先，判斷AEM執行個體是否以強制方式關閉(AEM處理序已強制終止，或發生電源故障)，然後重新啟動。

   * [AEM記錄](/help/sites-deploying/configure-logging.md) 可針對此目的檢閱。

1. 如果發生強制關閉，在重新啟動時，AEM會自動暫停重新索引最多30分鐘。
1. 請等候約45分鐘，讓AEM繼續正常的非同步索引作業。

## 執行緒集區超載 {#thread-pool-overloaded}

>[!NOTE]
>
>對於AEM 6.1，請確保 [AEM 6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html) 已安裝。

在特殊情況下，用於管理非同步索引的對話串池可能會變得超載。 為了隔離索引過程，可以配置對話串池以防止其他AEM工作干擾Oak及時索引內容的能力。 在這種情況下，請執行以下操作：

1. 定義新的獨立執行緒集區，以供Apache Sling排程器用於非同步索引：

   * 在受影響的AEM執行個體上，導覽至AEM OSGi Web Console>OSGi>設定>Apache Sling排程器，或前往https://&lt;host>：&lt;port>/system/console/configMgr (例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * 將專案新增到「允許的執行緒集區」欄位，其值為「oak」。
   * 若要儲存變更，請按一下 **儲存** 在右下角。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 確認新的Apache Sling排程器執行緒集區已註冊，並顯示在Apache Sling排程器狀態Web主控台中。

   * 導覽至「AEM OSGi Web主控台>狀態>Sling排程器」，或前往https://&lt;host>：&lt;port>/system/console/status-slingscheduler (例如， [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * 確認下列集區專案存在：

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 觀察佇列已滿 {#observation-queue-is-full}

如果在短時間內對存放庫進行了太多變更和認可，則索引可能會由於觀察佇列已滿而延遲。 首先，判斷觀察佇列是否已滿：

1. 前往Web主控台，然後按一下JMX標籤或前往https://&lt;host>：&lt;port>/system/console/jmx (例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. 開啟Oak存放庫統計MBean並判斷是否有 `ObservationQueueMaxLength` 值大於10,000。

   * 在正常作業中，這個最大值最終必須減少到零(尤其是在 `per second` 部分)，因此請確認 `ObservationQueueMaxLength`的秒數量度為0。
   * 如果值為10,000或更多，並且穩定增加，則表示至少一個（可能更多）佇列無法以新變更（認可）發生時的速度處理。
   * 每個觀察佇列都有限制（預設為10,000），如果佇列點選該限制，其處理會降級。
   * 使用MongoMK時，隨著佇列長度增加，內部Oak快取效能會降低。 此關聯性可從增加中看出 `missRate` 針對 `DocChildren` 中的快取 `Consolidated Cache` 統計MBean。

1. 為避免超過可接受的觀察佇列限制，建議：

   * 降低認可固定速率。 認可中的短尖峰是可接受的，但固定速率應降低。
   * 增加的大小 `DiffCache` 如所述 [效能調整秘訣> Mongo儲存體調整>檔案快取大小](/help/sites-deploying/configuring-performance.md).

## 識別及修正停滯的重新索引程式 {#identifying-and-remediating-a-stuck-re-indexing-process}

在兩種情況下，重新索引可被視為「完全停滯」：

* 重新索引的速度很慢，以至於記錄檔案中並未報告有關已周遊節點數的顯著進度。

   * 例如，如果一小時內沒有訊息，或進度太慢，需要一週或更長時間才能完成。

* 如果記錄檔案中出現重複的例外狀況(例如， `OutOfMemoryException`)進行索引。 記錄中重複一或多個相同的例外狀況，表示Oak嘗試重複將相同專案編列索引，但因相同問題而失敗。

若要識別並修正停滯的重新索引程式，請執行下列動作：

1. 若要找出索引卡住的原因，必須收集下列資訊：

   * 收集5分鐘的執行緒傾印，每2秒收集一次執行緒傾印。
   * [為附加器設定DEBUG層級和記錄](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*

   * 從非同步處理收集資料 `IndexStats` MBean：

      * 導覽至AEM OSGi Web Console>Main>JMX>IndexStat>async

        或前往 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)

   * 使用 [oak-run.jar的主控台模式](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) 以收集底下存在的詳細資訊* `/:async`*節點。
   * 使用收集存放庫查核點清單 `CheckpointManager` MBean：

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listCheckpoints()

        或前往 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)

1. 收集步驟1中概述的所有資訊後，請重新啟動AEM。

   * 重新啟動AEM可解決高並行負載（觀察佇列溢位或類似情況）時的問題。
   * 如果重新啟動無法解決問題，請開啟 [Adobe客戶服務](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support) 並提供在步驟1中收集的所有資訊。

## 安全地中止非同步重新索引 {#safely-aborting-asynchronous-re-indexing}

重新索引可以安全地中止（在完成之前停止），方法是透過 `async, async-reindex`和f `ulltext-async` 索引通道( `IndexStats` Mbean)。 如需詳細資訊，另請參閱上的Apache Oak檔案 [如何中止重新索引](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). 此外，請考量下列事項：

* Lucene和Lucene屬性索引的重新索引可以中止，因為它們自然非同步。
* 只有在透過啟動重新索引時，才能中止Oak屬性索引的重新索引。 `PropertyIndexAsyncReindexMBean`.

若要安全地中止重新索引，請執行下列步驟：

1. 識別控制必須停止的重新索引通道的IndexStats MBean。

   * 請前往AEM OSGi Web Console>Main>JMX或https:// ，透過JMX主控台導覽至適當的IndexStats MBean&lt;host>：&lt;port>/system/console/jmx (例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * 根據您想要停止的重新索引路線開啟IndexStats MBean ( `async`， `async-reindex`，或 `fulltext-async`)

      * 若要識別適當的通道，並藉此識別IndexStats MBean執行個體，請檢視Oak索引「非同步」屬性。 「非同步」屬性包含通道名稱： `async`， `async-reindex`，或 `fulltext-async`.
      * 您也可以存取「非同步」欄中的AEM Index Manager來存取通道。 若要存取「索引管理員」，請瀏覽至「作業」>「診斷」>「索引管理員」。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 叫用 `abortAndPause()` 命令於適當的 `IndexStats` MBean。
1. 適當地標籤Oak索引定義，以防止在索引通道恢復時恢復重新索引。

   * 重新索引時 **現有** 索引，將reindex屬性設定為false

      * `/oak:index/someExistingIndex@reindex=false`

   * 否則，針對 **新** 索引：

      * 將type屬性設定為disabled

         * `/oak:index/someNewIndex@type=disabled`

      * 或完全移除索引定義

   完成時將變更提交到存放庫。

1. 最後，在中止的索引通道上恢復非同步索引。

   * 在 `IndexStats` 發出 `abortAndPause()` 命令在步驟2中，叫用 `resume()`命令。

## 防止緩慢重新索引 {#preventing-slow-re-indexing}

最好在靜默期（例如，在大型內容擷取期間）重新索引，最好在已知並控制AEM載入的維護期間重新索引。 此外，請確定重新索引不會在其他維護活動期間發生。
