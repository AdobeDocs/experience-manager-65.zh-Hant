---
title: Oak索引故障排除
seo-title: Troubleshooting Oak Indexes
description: 如何檢測並修復慢速重新索引。
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 1%

---

# Oak索引故障排除{#troubleshooting-oak-indexes}

## 慢速重新索引  {#slow-re-indexing}

內部AEM重新索引過程收集儲存庫資料並將其儲存在Oak索引中，以支援對內容的效能查詢。 在特殊情況下，這一過程可能會變得緩慢，甚至停滯。 此頁用作故障排除指南，幫助確定索引是否慢、查找原因並解決問題。

區分需要不適當長時間的重新索引和需要長時間的重新索引非常重要，因為它正在為大量內容編製索引。 例如，索引內容所花的時間隨內容量而擴展，因此大型生產儲存庫重新索引所需的時間比小型開發儲存庫要長。

查看 [查詢和索引方面的最佳做法](/help/sites-deploying/best-practices-for-queries-and-indexing.md) 的子菜單。

## 初始檢測 {#initial-detection}

初始檢測慢索引需要查看 `IndexStats` JMX MBean。 在受影響的AEM實例上，執行以下操作：

1. 開啟Web控制台，然後按一下JMX頁籤或轉到https://&lt;host>:&lt;port>/system/console/jmx(例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))。
1. 導航到 `IndexStats` 姆本。
1. 開啟 `IndexStats` 「」的MBean `async`&quot;和&quot; `fulltext-async`。

1. 對於兩個MBean，檢查 **完成** 時間戳和 **上次索引時間** 時間戳從當前時間起小於45分鐘。

1. 對於任一MBean，如果時間值(**完成** 或 **上次索引時間**)從當前時間開始大於45分鐘，則索引作業失敗或花費太長。 此問題導致非同步索引失效。

## 強制關閉後索引暫停 {#indexing-is-paused-after-a-forced-shutdown}

強制關閉導致在AEM重新啟動後掛起非同步索引長達30分鐘。 而且，通常需要再花15分鐘才能完成第一次重新索引通過，總共需要約45分鐘(與 [初始檢測](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) 45分鐘)。 如果索引在強制關閉後暫停：

1. 首先，確定實AEM例是否以強制方式關閉(進AEM程被強制終止，或電源故障)，然後重新啟動。

   * [AEM日誌](/help/sites-deploying/configure-logging.md) 可就此進行審閱。

1. 如果發生強制關閉，則在重新啟AEM動時，自動暫停重新索引長達30分鐘。
1. 大約等待45分鐘，AEM以恢復正常的非同步索引操作。

## 線程池重載 {#thread-pool-overloaded}

>[!NOTE]
>
>對AEM於6.1，確保 [AEM6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant) 已安裝。

在特殊情況下，用於管理非同步索引的線程池可能會過載。 為了隔離索引過程，可以配置線程池來防止其AEM他工作干擾Oak及時索引內容的能力。 在這種情況下，請執行以下操作：

1. 為Apache Sling Scheduler定義一個用於非同步索引的新孤立線程池：

   * 在受影響的AEM實例上，導航AEM到OSGi Web Console>OSGi>Configuration>Apache Sling Scheduler或轉到https://&lt;host>:&lt;port>/system/console/configMgr(例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * 在值為&quot;oak&quot;的「允許的線程池」欄位中添加一個項。
   * 要保存更改，請按一下 **保存** 在右下角。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 驗證新的Apache Sling Scheduler線程池是否已註冊並顯示在Apache Sling Scheduler Status web控制台中。

   * 導航到AEMOSGi Web控制台>狀態>Sling Scheduler或轉到https://&lt;host>:&lt;port>/system/console/status-slingscheduler(例如， [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * 驗證是否存在以下池項：

      * 阿帕奇斯林戈克
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 觀察隊列已滿 {#observation-queue-is-full}

如果在短時間內對儲存庫進行了太多的更改和提交，則索引可能會因為完全觀察隊列而延遲。 首先，確定觀察隊列是否已滿：

1. 轉到Web控制台，然後按一下JMX頁籤或轉到https://&lt;host>:&lt;port>/system/console/jmx(例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. 開啟Oak儲存庫統計資訊MBean並確定是否有 `ObservationQueueMaxLength` 值大於10,000。

   * 在正常操作中，此最大值必須最終降到零(特別是在 `per second` 部分)以驗證 `ObservationQueueMaxLength`秒度量為0。
   * 如果值為10,000或更多，並且穩步增加，則表示至少一個（可能更多）隊列無法像發生新更改（提交）那樣快速處理。
   * 每個觀察隊列都有一個限制（預設為10,000），如果隊列達到該限制，其處理會降級。
   * 當使用MongoMK時，隨著隊列長度的增長，內部Oak快取效能降低。 這種關聯性可以從 `missRate` 為 `DocChildren` 快取 `Consolidated Cache` 統計資訊MBean。

1. 為避免超出可接受的觀察隊列限制，建議：

   * 降低提交的恆定速率。 提交中短的尖峰值是可接受的，但應減少恆定的速率。
   * 增加 `DiffCache` 如所述 [效能調整提示> Mongo儲存調整>文檔快取大小](/help/sites-deploying/configuring-performance.md)。

## 識別並修正停滯的重新索引過程 {#identifying-and-remediating-a-stuck-re-indexing-process}

在兩種情況下，重新編製索引可以被視為「完全停滯」：

* 重新索引速度很慢，以至於日誌檔案中沒有報告有關已遍歷的節點數的顯著進展。

   * 例如，如果在一小時內沒有消息，或者進度太慢，需要一週或更長時間才能完成。

* 如果日誌檔案中出現重複的異常，則重新索引將陷入循環(例如， `OutOfMemoryException`)。 日誌中重複出現一個或多個相同的異常表明，Oak嘗試重複對同一事項進行索引，但在同一問題上失敗。

要識別和修復停滯的重新索引過程，請執行以下操作：

1. 要確定索引卡滯的原因，必須收集以下資訊：

   * 收集5分鐘的線程轉儲，每2秒收集一次線程轉儲。
   * [為附加程式設定DEBUG級別和日誌](/help/sites-deploying/configure-logging.md)。

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * 從非同步收集資料 `IndexStats` MBean:

      * 導航至AEMOSGi Web Console>Main>JMX>IndexStat>非同步

         或轉到 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * 使用 [oak-run.jar的控制台模式](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) 以收集*項下的詳細資訊 `/:async`*節點。
   * 使用 `CheckpointManager` MBean:

      * AEMOSGi Web Console>Main>JMX>CheckpointManager>listCheckpoints()

         或轉到 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. 收集完步驟1中概述的所有資訊後，重新啟AEM動。

   * 如果AEM併發負載較高（觀察隊列溢出或類似情況），重新啟動可能會解決此問題。
   * 如果重新啟動無法解決問題，請開啟 [Adobe客戶關懷](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support) 提供步驟1中收集的所有資訊。

## 安全中止非同步重新索引 {#safely-aborting-asynchronous-re-indexing}

通過 `async, async-reindex`和 `ulltext-async` 索引通道( `IndexStats` Mbean)。 有關詳細資訊，另請參見上的Apache Oak文檔 [如何中止重新索引](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex)。 另外，請考慮以下事項：

* Lucene和Lucene屬性索引的重新索引可以中止，因為它們是自然非同步的。
* 只有在通過 `PropertyIndexAsyncReindexMBean`。

要安全中止重新索引，請執行以下步驟：

1. 標識控制必須停止的重新索引通道的IndexStats MBean。

   * 通過JMX控制台導航到相應的IndexStats MBean，方法是轉AEM到OSGi Web Console>Main>JMX或https://&lt;host>:&lt;port>/system/console/jmx(例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * 根據要停止的重新索引通道開啟IndexStats MBean( `async`。 `async-reindex`或 `fulltext-async`)

      * 要標識相應的通道，從而標識IndexStats MBean實例，請查看Oak Indexes &quot;async&quot;屬性。 「async」屬性包含通道名稱： `async`。 `async-reindex`或 `fulltext-async`。
      * 通過訪問「Async」列AEM中的Index Manager，通道也可用。 要訪問索引管理器，請導航到「操作」>「診斷」>「索引管理器」。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 調用 `abortAndPause()` 命令 `IndexStats` MBean。
1. 正確標籤Oak索引定義，以防止在索引通道恢復時恢復重新索引。

   * 重新索引 **現有** index，將reindex屬性設定為false

      * `/oak:index/someExistingIndex@reindex=false`
   * 否則，對於 **新** 索引：

      * 將type屬性設定為禁用

         * `/oak:index/someNewIndex@type=disabled`
      * 或完全刪除索引定義

   完成後將更改提交到儲存庫。

1. 最後，在中止的索引通道上恢復非同步索引。

   * 在 `IndexStats` 發出 `abortAndPause()` 命令，調用 `resume()`的子菜單。

## 防止慢速重新索引 {#preventing-slow-re-indexing}

最好在安靜期間（例如，不是在大內容攝取期間）重新索引，最好在已知和控制負載的維護窗口AEM期間重新索引。 另外，確保在其他維護活動期間不進行重新索引。
