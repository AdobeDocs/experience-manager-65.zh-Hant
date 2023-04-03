---
title: 疑難排解Oak索引
seo-title: Troubleshooting Oak Indexes
description: 如何偵測並修正緩慢的重新索引。
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 2%

---

# 疑難排解Oak索引{#troubleshooting-oak-indexes}

## 慢速重新索引  {#slow-re-indexing}

AEM內部重新索引程式會收集存放庫資料，並將其儲存在Oak索引中，以支援內容的效能查詢。 在特殊情況下，該過程可能會變得緩慢甚至停滯。 本頁作為故障排除指南，幫助確定索引是否緩慢、查找原因並解決問題。

必須區分重新索引需要的時間長得不恰當，而重新索引需要的時間長，因為它正在索引大量的內容。 例如，索引內容所花的時間會隨著內容量而調整，因此大型生產存放庫重新索引所需的時間會比小型開發存放庫長。

請參閱 [查詢和索引的最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md) 以取得內容重新索引的時間和方式的詳細資訊。

## 初始偵測 {#initial-detection}

初始檢測慢速索引需要檢查 `IndexStats` JMX MBean。 在受影響的AEM例項上，執行下列動作：

1. 開啟Web控制台，然後按一下JMX頁簽或轉到https://&lt;host>:&lt;port>/system/console/jmx(例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))。
1. 導覽至 `IndexStats` 姆班斯。
1. 開啟 `IndexStats` 「 `async`&quot;和&quot; `fulltext-async`」。

1. 對於兩個MBean，檢查 **完成** 時間戳記和 **LastIndexTime** 時間戳記自目前時間起不到45分鐘。

1. 對於任一MBean，如果時間值(**完成** 或 **LastIndexedTime**)大於當前時間的45分鐘，則索引作業失敗或花費太長時間。 此問題會導致非同步索引過時。

## 強制關閉後索引暫停 {#indexing-is-paused-after-a-forced-shutdown}

強制關閉會導致AEM在重新啟動後最多暫停30分鐘的非同步索引。 此外，通常需要15分鐘才能完成第一個重新索引通過，總共約45分鐘(連結回 [初始偵測](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) 45分鐘的時間範圍)。 如果強制關閉後索引暫停：

1. 首先，判斷AEM執行個體是否以強制方式關閉(AEM程式已強制終止，或發生電源故障)並稍後重新啟動。

   * [AEM記錄](/help/sites-deploying/configure-logging.md) 可就此審查。

1. 如果發生強制關閉，重新啟動時，AEM會自動暫停重新索引最多30分鐘。
1. 等待約45分鐘，讓AEM繼續正常的非同步索引操作。

## 線程池超載 {#thread-pool-overloaded}

>[!NOTE]
>
>針對AEM 6.1，請確定 [AEM 6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant) 已安裝。

在特殊情況下，用於管理非同步索引的線程池可能會變為過載。 若要隔離索引程式，可設定執行緒池，以防止其他AEM工作干擾Oak及時索引內容的能力。 在這種情況下，請執行下列操作：

1. 為Apache Sling排程器定義新的隔離執行緒池，以用於非同步索引：

   * 在受影響的AEM例項上，導覽至AEM OSGi Web Console>OSGi > Configuration > Apache Sling Scheduler或前往https://&lt;host>:&lt;port>/system/console/configMgr(例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * 將項目新增至「允許的執行緒池」欄位，並將其值設為「oak」。
   * 若要儲存變更，請按一下 **儲存** 在右下角。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 確認已註冊新的Apache Sling排程器執行緒池，並顯示在Apache Sling排程器狀態Web主控台中。

   * 導覽至AEM OSGi Web主控台>狀態> Sling排程器，或前往https://&lt;host>:&lt;port>/system/console/status-slingscheduler(例如， [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * 驗證是否存在以下池項：

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 觀察隊已滿 {#observation-queue-is-full}

如果在短時間內對儲存庫進行了太多更改和提交，則索引可能會因為完整觀察隊列而延遲。 首先，確定觀察隊列是否已滿：

1. 轉到Web控制台，然後按一下JMX頁簽或轉到https://&lt;host>:&lt;port>/system/console/jmx(例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. 開啟Oak Repository Statistics MBean，並判斷是否有 `ObservationQueueMaxLength` 值大於10,000。

   * 在正常操作中，此最大值必須最終降為零(尤其是 `per second` 部分)，確認 `ObservationQueueMaxLength`的秒量度為0。
   * 如果值為10,000或更多，並且穩步增加，則表示至少一個（可能更多）隊列無法像發生新更改（提交項）一樣快速處理。
   * 每個觀察佇列都有一個限制（預設為10,000），如果佇列達到該限制，其處理會降低。
   * 使用MongoMK時，當佇列長度長度增加時，內部Oak快取效能會降低。 此關聯可以在 `missRate` 針對 `DocChildren` 快取 `Consolidated Cache` 統計MBean。

1. 為避免超過可接受的觀察隊列限制，建議執行以下操作：

   * 降低提交的恆定速率。 提交量中短的尖峰是可接受的，但應該降低恆定速率。
   * 增加 `DiffCache` 如 [效能調整提示> Mongo儲存調整>文檔快取大小](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/configuring/configuring-performance.html?lang=zh-Hant).

## 識別和修正停滯的重新索引過程 {#identifying-and-remediating-a-stuck-re-indexing-process}

在兩種情況下，重新索引可以被視為「完全卡住」：

* 重新索引的速度很慢，以致於記錄檔中沒有關於已遍歷的節點數的顯著進度報告。

   * 例如，如果一小時內沒有訊息，或進度太慢，需要一週或更久才能完成。

* 如果記錄檔中出現重複的例外狀況，則重新索引會卡在無盡的回圈中(例如， `OutOfMemoryException`)。 記錄中重複出現一或多個相同例外，表示Oak會嘗試重複為相同項目建立索引，但在相同問題上失敗。

要識別並修復停滯的重新索引過程，請執行以下操作：

1. 要確定索引停滯的原因，必須收集以下資訊：

   * 收集5分鐘的線程轉儲，每2秒收集一個線程轉儲。
   * [設定附加程式的DEBUG層級和記錄](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * 從非同步收集資料 `IndexStats` MBean:

      * 導覽至「AEM OSGi Web Console>Main>JMX>IndexStat>async」

         或前往 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * 使用 [oak-run.jar的主控台模式](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) 收集* `/:async`*節點。
   * 使用 `CheckpointManager` MBean:

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listChapperits()

         或前往 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. 收集步驟1中概述的所有資訊後，請重新啟動AEM。

   * 如果併發負載較高（觀察隊列溢出或類似），重新啟動AEM可能會解決問題。
   * 如果重新啟動無法解決問題，請開啟 [Adobe客戶服務](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support) 並提供在步驟1中收集的所有資訊。

## 安全中止非同步重新索引 {#safely-aborting-asynchronous-re-indexing}

可透過 `async, async-reindex`和f `ulltext-async` 索引通道( `IndexStats` Mbean)。 如需詳細資訊，請參閱Apache Oak檔案，位於 [如何中止重新索引](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). 此外，請考量下列事項：

* Lucene和Lucene屬性索引的重新索引可以被中止，因為它們自然是非同步的。
* 只有透過 `PropertyIndexAsyncReindexMBean`.

要安全地中止重新索引，請執行以下步驟：

1. 標識控制必須停止的重新索引通道的IndexStats MBean。

   * 通過轉到AEM OSGi Web Console>Main>JMX或https://，導航到JMX控制台的相應IndexStats MBean&lt;host>:&lt;port>/system/console/jmx(例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * 根據要停止的重新索引通道開啟IndexStats MBean( `async`, `async-reindex`，或 `fulltext-async`)

      * 若要識別適當的通道，進而識別IndexStats MBean例項，請查看Oak Indexes &quot;async&quot;屬性。 「async」屬性包含通道名稱： `async`, `async-reindex`，或 `fulltext-async`.
      * 存取「非同步」欄中的AEM Index Manager也可使用通道。 要訪問索引管理器，請導航至操作>診斷>索引管理器。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 叫用 `abortAndPause()` 命令 `IndexStats` MBean。
1. 正確標示Oak索引定義，以防止在索引通道恢復時繼續重新索引。

   * 重新索引 **現有** 索引，將reindex屬性設定為false

      * `/oak:index/someExistingIndex@reindex=false`
   * 或者，對於 **new** 索引，或者：

      * 將type屬性設定為已禁用

         * `/oak:index/someNewIndex@type=disabled`
      * 或完全刪除索引定義

   完成後將更改提交到儲存庫。

1. 最後，在中止的索引通道上繼續非同步索引。

   * 在 `IndexStats` 發出 `abortAndPause()` 命令，調用 `resume()`命令。

## 防止慢速重新索引 {#preventing-slow-re-indexing}

最好在安靜時段（例如，不是在大型內容擷取期間）重新索引，最好在已知並控制AEM負載的維護時段重新索引。 另外，確保在其他維護活動期間不進行重新索引。
