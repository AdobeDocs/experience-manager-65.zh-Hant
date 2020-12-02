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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 0%

---


# 疑難排解Oak索引{#troubleshooting-oak-indexes}

## 慢速重新索引{#slow-re-indexing}

AEM的內部重新索引程式會收集儲存庫資料，並將它儲存在Oak索引中，以支援內容的效能查詢。 在例外情況下，程式可能會變得緩慢甚至停滯。 本頁提供疑難排解指南，可協助您識別索引是否緩慢、找出原因並解決問題。

請務必區分需要花費不適當時間的重新建立索引，以及需要花費大量時間的重新建立索引，因為這是為大量內容建立索引。 例如，索引內容所花的時間會隨著內容量而擴展，因此大型生產儲存庫的重新索引所需時間會比小型開發儲存庫更長。

有關何時以及如何重新索引內容的詳細資訊，請參閱[查詢和索引的最佳做法](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

## 初始檢測{#initial-detection}

初始檢測慢速索引需要查看`IndexStats` JMX MBean。 在受影響的AEM例項上，執行下列動作：

1. 開啟Web控制台並按一下JMX頁籤，或轉至https://&lt;host>:&lt;port>/system/console/jmx(例如[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))。
1. 導航至`IndexStats` Mbean。
1. 開啟「 `async`」和「 `fulltext-async`」的`IndexStats` MBean。

1. 對於兩個MBean，檢查&#x200B;**Done**&#x200B;時間戳記和&#x200B;**LastIndexTime**&#x200B;時間戳記是否比當前時間少45分鐘。

1. 對於任一MBean，如果時間值（**Done**&#x200B;或&#x200B;**LastIndexedTime**）從當前時間大於45分鐘，則索引作業會失敗或過長。 這會導致非同步索引過時。

## 強制關閉{#indexing-is-paused-after-a-forced-shutdown}後索引暫停

強制關閉會導致AEM在重新啟動後最多30分鐘暫停非同步索引，而且通常需要15分鐘才能完成第一次重新索引傳遞，總共約45分鐘（與[初始偵測](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection)時間範圍45分鐘相連）。 如果您懷疑索引在強制關閉後暫停：

1. 首先，判斷AEM例項是否以強制方式關閉（AEM程式已強制中止，或發生電源故障），然後重新啟動。

   * [AEM](/help/sites-deploying/configure-logging.md) 記錄可依此目的進行審查。

1. 如果發生強制關閉，在重新啟動時，AEM會自動暫停重新建立索引最多30分鐘。
1. 等待約45分鐘，讓AEM繼續正常的非同步索引作業。

## 線程池過載{#thread-pool-overloaded}

>[!NOTE]
>
>對於AEM 6.1，請確定已安裝[AEM 6.1 CFP 11](https://helpx.adobe.com/experience-manager/release-notes-aem-6-1-cumulative-fix-pack.html)。

在特殊情況下，用於管理非同步索引的線程池可能會過載。 為了隔離索引程式，可以設定執行緒池，以防止其他AEM工作干擾Oak即時索引內容的能力。 若要這麼做，您應：

1. 為Apache Sling排程器定義新的隔離執行緒池，以用於非同步索引：

   * 在受影響的AEM例項上，導覽至AEM OSGi Web Console>OSGi>Configuration>Apache Sling Scheduler或前往https://&lt;host>:&lt;port>/system/console/configMgr(例如，[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * 在「允許的線程池」欄位中添加一個項，其值為&quot;oak&quot;。
   * 按一下右下角的「儲存」，儲存變更。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 驗證新的Apache Sling Scheduler執行緒池已註冊並顯示在Apache Sling Scheduler Satus網站主控台中。

   * 導覽至AEM OSGi Web console>Status>Sling Scheduler或前往https://&lt;host>:&lt;port>/system/console/status-slingscheduler(例如，[http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * 驗證是否存在以下池條目：

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 觀察佇列已滿{#observation-queue-is-full}

如果在短時間內對儲存庫進行了太多更改和提交，則由於完全觀察隊列，索引可能會延遲。 首先，確定觀測隊列是否滿：

1. 轉到Web控制台並按一下「JMX」頁籤，或轉到https://&lt;host>:&lt;port>/system/console/jmx(例如[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. 開啟Oak Repository統計資料MBean，並判斷是否有`ObservationQueueMaxLength`值大於10,000。

   * 在正常操作中，此值最大值最終必須降為零（尤其在`per second`部分），以驗證`ObservationQueueMaxLength`的秒量度為0。
   * 如果值為10,000或更多，並且穩步增加，則表明至少一個（可能更多）隊列無法像發生新更改（提交）那樣快速處理。
   * 每個觀察佇列都有限制（預設為10,000），如果佇列達到此限制，其處理會降低。
   * 當使用MongoMK時，當佇列長度增加時，內部Oak快取效能會降低。 在`Consolidated Cache`統計MBean中，`DocChildren`快取的`missRate`增加中可看到此關聯。

1. 為避免超過可接受的觀察隊列限制，建議您：

   * 降低提交的恆定速率。 提交中的短尖峰是可以接受的，但應該降低恆定速率。
   * 按照[效能調整提示>單次儲存調整>文檔快取大小](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html#main-pars_text_3)中所述增加`DiffCache`的大小。

## 確定並修正停滯的重新索引進程{#identifying-and-remediating-a-stuck-re-indexing-process}

在兩種情況下，重新編製索引可以被視為「完全停滯」:

* 重新編製索引非常緩慢，以至於日誌檔案中沒有報告有關所遍歷的節點數的顯著進展。

   * 例如，如果在一小時內沒有訊息，或進度太慢，以至需要一週或更久才能完成。

* 如果索引線程的日誌檔案（例如`OutOfMemoryException`）中出現重複的異常，則重新索引將被困在一個循環中。 重複記錄中的相同例外，表示Oak嘗試重複索引相同的項目，但在相同問題上失敗。

要識別並修復停滯的重新索引過程，請執行以下操作：

1. 為了找出索引卡住的原因，必須收集下列資訊：

   * 收集5分鐘的線程轉儲，每2秒一個線程轉儲。
   * [為附加程式設定DEBUG級別和日誌](/help/sites-deploying/configure-logging.md)。

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * 從非同步`IndexStats` MBean收集資料：

      * 導覽至AEM OSGi Web Console>Main>JMX>IndexStat>async

         或前往[http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * 使用[oak-run.jar的控制台模式](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)來收集* `/:async`*節點下存在內容的詳細資料。
   * 使用`CheckpointManager` MBean收集儲存庫查核點清單：

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listChreckeptions()

         或前往[http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. 收集完步驟1中概述的所有資訊後，請重新啟動AEM。

   * 重新啟動AEM可解決併發負載高（觀察佇列溢位或類似情況）的問題。
   * 如果重新啟動無法解決問題，請開啟[Adobe客戶服務](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html)的問題，並提供步驟1中收集的所有資訊。

## 安全中止非同步重新索引{#safely-aborting-asynchronous-re-indexing}

可以通過`async, async-reindex`和f `ulltext-async`索引通道(`IndexStats` Mbean)安全中止（在完成前停止）重新索引。 如需詳細資訊，請參閱[如何中止重新索引](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex)上的Apache Oak檔案。 此外，請考慮：

* Lucene和Lucene屬性索引的重新索引可以中止，因為它們是自然同步的。
* 只有透過`PropertyIndexAsyncReindexMBean`啟動重新索引時，Oak屬性索引的重新索引才能中止。

要安全中止重新編製索引，請執行以下步驟：

1. 識別控制需要停止的重新建立索引通道的IndexStats MBean。

   * 透過JMX主控台導覽至適當的IndexStats MBean，方法是前往AEM OSGi Web Console>Main>JMX或https://&lt;host>:&lt;port>/system/console/jmx(例如[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * 根據您要停止的重新索引通道（`async`、`async-reindex`或`fulltext-async`）開啟IndexStats MBean

      * 若要識別適當的通道，進而識別IndexStats MBean實例，請查看Oak Indexes &quot;async&quot;屬性。 「async」屬性將包含車道名稱：`async`、`async-reindex`或`fulltext-async`。
      * 您也可以存取「非同步」欄中的AEM的Index Manager，以取得通道。 要訪問索引管理器，請導航至操作>診斷>索引管理器。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 在相應的`IndexStats` MBean上調用`abortAndPause()`命令。
1. 正確標籤Oak索引定義，以防止在索引通道恢復時繼續重新索引。

   * 在重新索引&#x200B;**existing**&#x200B;索引時，將reindex屬性設為false

      * `/oak:index/someExistingIndex@reindex=false`
   * 或者，對於&#x200B;**new**&#x200B;索引，可以：

      * 將type屬性設為disabled

         * `/oak:index/someNewIndex@type=disabled`
      * 或完全刪除索引定義

   完成時將更改提交到儲存庫。

1. 最後，在中止的索引通道上恢復非同步索引。

   * 在步驟2中發出`abortAndPause()`命令的`IndexStats` MBean中，調用`resume()`命令。

## 防止慢速重新索引{#preventing-slow-re-indexing}

最好在安靜時段（例如，不是在大型內容收錄時）重新索引，最理想的是在維護視窗中，當AEM的負載已知並受控時。 此外，請確保在其他維護活動期間不會重新編製索引。
