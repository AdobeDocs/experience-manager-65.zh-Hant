---
title: 疑難排解Oak索引
seo-title: 疑難排解Oak索引
description: 如何偵測並修正緩慢的重新索引。
seo-description: 如何偵測並修正緩慢的重新索引。
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 0%

---

# 疑難排解Oak索引{#troubleshooting-oak-indexes}

## 慢速重新索引{#slow-re-indexing}

AEM內部重新索引程式會收集存放庫資料，並將其儲存在Oak索引中，以支援內容的效能查詢。 在特殊情況下，該過程可能會變得緩慢甚至停滯。 本頁作為故障排除指南，幫助確定索引是否緩慢、查找原因並解決問題。

必須區分需要不恰當的長時間的重新索引和需要很長時間的重新索引，因為它正在索引大量的內容。 例如，索引內容所花的時間會隨著內容量而調整，因此大型生產存放庫重新索引所需的時間會比小型開發存放庫長。

有關重新索引內容的時間和方式的詳細資訊，請參閱[查詢和索引的最佳做法](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

## 初始檢測{#initial-detection}

初始檢測慢索引需要檢查`IndexStats` JMX MBean。 在受影響的AEM例項上，執行下列動作：

1. 開啟Web控制台，然後按一下JMX頁簽，或轉到https://&lt;host>:&lt;port>/system/console/jmx(例如[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))。
1. 導覽至`IndexStats` Mbean。
1. 開啟「 `async`」和「 `fulltext-async`」的`IndexStats` MBean。

1. 對於這兩個MBean，檢查&#x200B;**Done**&#x200B;時間戳記和&#x200B;**LastIndexTime**&#x200B;時間戳記是否少於當前時間的45分鐘。

1. 對於MBean，如果時間值（**Done**&#x200B;或&#x200B;**LastIndexedTime**）從當前時間開始大於45分鐘，則索引作業失敗或花費太長時間。 這會導致非同步索引過時。

## 強制關閉{#indexing-is-paused-after-a-forced-shutdown}後索引暫停

強制關閉會導致AEM在重新啟動後最多暫停非同步索引30分鐘，且通常需要另外15分鐘才能完成第一次重新索引通過，總共約45分鐘（與45分鐘的[初始偵測](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection)時間範圍相連）。 如果您懷疑在強制關閉後索引暫停：

1. 首先，判斷AEM執行個體是否以強制方式關閉(AEM程式已強制終止，或發生電源故障)，然後重新啟動。

   * [AEM](/help/sites-deploying/configure-logging.md) 記錄可依此目的進行審核。

1. 如果發生強制關閉，重新啟動時，AEM會自動暫停重新索引最多30分鐘。
1. 等待約45分鐘，讓AEM繼續正常的非同步索引操作。

## 線程池超載{#thread-pool-overloaded}

>[!NOTE]
>
>針對AEM 6.1，請確定已安裝[AEM 6.1 CFP 11](https://helpx.adobe.com/experience-manager/release-notes-aem-6-1-cumulative-fix-pack.html)。

在特殊情況下，用於管理非同步索引的線程池可能會變得過載。 為了隔離索引程式，可設定執行緒池，以防止其他AEM工作干擾Oak及時索引內容的能力。 若要這麼做，您應：

1. 為Apache Sling排程器定義新的隔離執行緒池，以用於非同步索引：

   * 在受影響的AEM例項上，導覽至AEM OSGi Web Console>OSGi>Configuration>Apache Sling排程器，或前往https://&lt;host>:&lt;port>/system/console/configMgr(例如[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * 將項目新增至「允許的執行緒池」欄位，並將其值設為「oak」。
   * 按一下右下角的「儲存」 ，儲存變更。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 確認已註冊新的Apache Sling排程器執行緒池，並在Apache Sling排程器狀態Web主控台中顯示。

   * 導覽至AEM OSGi Web主控台> Status>Sling排程器，或前往https://&lt;host>:&lt;port>/system/console/status-sling排程器(例如[http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * 驗證是否存在以下池項：

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 觀察隊列已滿{#observation-queue-is-full}

如果在短時間內對儲存庫進行了太多更改和提交，則索引可能會因為完整觀察隊列而延遲。 首先，確定觀測隊列是否滿：

1. 轉到Web控制台，然後按一下JMX頁簽，或轉到https://&lt;host>:&lt;port>/system/console/jmx(例如[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. 開啟Oak Repository Statistics MBean ，並判斷是否有任何`ObservationQueueMaxLength`值大於10,000。

   * 在正常操作中，此最大值最終必須減少為零（特別是在`per second`部分中），以驗證`ObservationQueueMaxLength`的秒量度為0。
   * 如果值為10,000或更多，並且穩步增加，則表示至少一個（可能更多）隊列無法像發生新更改（提交項）一樣快速處理。
   * 每個觀察佇列都有一個限制（預設為10,000），如果佇列達到該限制，其處理會降低。
   * 使用MongoMK時，當佇列長度長度增加時，內部Oak快取效能會降低。 在`Consolidated Cache`統計MBean中`DocChildren`快取的增加`missRate`中可看到此關聯。

1. 為避免超過可接受的觀察隊列限制，建議執行以下操作：

   * 降低提交的恆定速率。 提交量中短的尖峰是可接受的，但應該降低恆定速率。
   * 按照[效能調整提示> Mongo儲存調整>文檔快取大小](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html#main-pars_text_3)中所述，增加`DiffCache`的大小。

## 識別和修正停滯的重新索引進程{#identifying-and-remediating-a-stuck-re-indexing-process}

在兩種情況下，重新索引可以被視為「完全卡住」：

* 重新索引的速度非常慢，以至於在日誌檔案中，對於所遍歷的節點數沒有報告顯著進展。

   * 例如，如果一小時內沒有訊息，或進度太慢，以致需要一週或更長時間才能完成。

* 如果索引線程的日誌檔案（例如`OutOfMemoryException`）中出現重複的異常，則重新索引卡在無窮循環中。 記錄中重複相同例外狀況，表示Oak嘗試重複索引相同項目，但在相同問題上失敗。

要識別並修復停滯的重新索引過程，請執行以下操作：

1. 為了確定索引停滯的原因，必須收集以下資訊：

   * 收集5分鐘的線程轉儲，每2秒收集一個線程轉儲。
   * [設定附加程式的DEBUG層級和記錄](/help/sites-deploying/configure-logging.md)。

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * 從非同步`IndexStats` MBean收集資料：

      * 導覽至「AEM OSGi Web Console>Main>JMX>IndexStat>async」

         或轉至[http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * 使用[oak-run.jar的主控台模式](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)來收集* `/:async`*節點下存在內容的詳細資訊。
   * 使用`CheckpointManager` MBean收集儲存庫查核點清單：

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listChapperits()

         或轉至[http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. 收集步驟1中概述的所有資訊後，請重新啟動AEM。

   * 重新啟動AEM可解決併發負載高（觀察隊列溢出或類似情況）的問題。
   * 如果重新啟動無法解決問題，請開啟[Adobe客戶服務](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html)的問題，並提供在步驟1中收集的所有資訊。

## 安全中止非同步重新索引{#safely-aborting-asynchronous-re-indexing}

可通過`async, async-reindex`和f `ulltext-async`索引通道(`IndexStats` Mbean)安全地中止（在完成前停止）重新索引。 如需詳細資訊，請參閱[How to Abort Reindexing](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex)上的Apache Oak檔案。 此外，請考量：

* Lucene和Lucene屬性索引的重新索引可以被中止，因為它們是自然非同步的。
* 只有透過`PropertyIndexAsyncReindexMBean`啟動重新索引時，才能中止Oak屬性索引的重新索引。

要安全地中止重新索引，請執行以下步驟：

1. 識別控制需要停止的重新索引通道的IndexStats MBean。

   * 通過轉到AEM OSGi Web Console>Main>JMX或https://&lt;host>:&lt;port>/system/console/jmx(例如[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))，導航到相應的IndexStats MBean
   * 根據要停止的重新索引通道（`async`、`async-reindex`或`fulltext-async`）開啟IndexStats MBean

      * 若要識別適當的通道，進而識別IndexStats MBean例項，請查看Oak Indexes &quot;async&quot;屬性。 「async」屬性將包含通道名稱：`async`、`async-reindex`或`fulltext-async`。
      * 存取「非同步」欄中的AEM Index Manager也可使用通道。 要訪問索引管理器，請導航到操作>診斷>索引管理器。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 在相應的`IndexStats` MBean上調用`abortAndPause()`命令。
1. 正確標示Oak索引定義，以防止在索引通道恢復時繼續重新索引。

   * 重新索引&#x200B;**existing**&#x200B;索引時，請將reindex屬性設為false

      * `/oak:index/someExistingIndex@reindex=false`
   * 或者，對於&#x200B;**new**&#x200B;索引，可以：

      * 將type屬性設定為已禁用

         * `/oak:index/someNewIndex@type=disabled`
      * 或完全刪除索引定義

   完成後將更改提交到儲存庫。

1. 最後，在中止的索引通道上繼續非同步索引。

   * 在步驟2中發出`abortAndPause()`命令的`IndexStats` MBean中，調用`resume()`命令。

## 防止慢速重新索引{#preventing-slow-re-indexing}

最好在安靜時段（例如，不是在大型內容擷取期間）重新索引，最好在已知並控制AEM負載的維護時段重新索引。 另外，確保在其他維護活動期間不進行重新索引。
