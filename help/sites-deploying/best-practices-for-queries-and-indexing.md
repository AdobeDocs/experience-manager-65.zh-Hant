---
title: 查詢和索引的最佳做法
seo-title: Best Practices for Queries and Indexing
description: 本文提供了有關如何優化索引和查詢的指導。
seo-description: This article provides guidelines on how to optimize your indexes and queries.
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
source-git-commit: c9df4b43083376f0110368afe642ec74290a52f8
workflow-type: tm+mt
source-wordcount: '4679'
ht-degree: 0%

---

# 查詢和索引的最佳做法{#best-practices-for-queries-and-indexing}

隨著6版向Oak的轉AEM換，查詢和索引的管理方式也發生了一些重大變化。 在Jackrabbit 2下，預設情況下所有內容都已編製索引，可以自由查詢。 在Oak中，必須在 `oak:index` 的下界。 可以在沒有索引的情況下執行查詢，但對於大型資料集，它的執行速度會非常慢，甚至會中止。

本文將概述何時建立索引以及何時不需要索引、在不需要時避免使用查詢的技巧以及優化索引和查詢以盡可能最佳地執行的提示。

此外，確保 [關於編寫查詢和索引的Oak文檔](/help/sites-deploying/queries-and-indexing.md)。 除了索引是6中的一個新概念AEM之外，Oak查詢中還存在語法差異，在從以前的安裝遷移代碼時需要考慮這AEM些差異。

## 何時使用查詢 {#when-to-use-queries}

### 儲存庫和分類設計 {#repository-and-taxonomy-design}

在設計儲存庫的分類時，需要考慮幾個因素。 這些包括訪問控制、本地化、元件和頁面屬性繼承等。

在設計可解決這些問題的分類時，考慮索引設計的「可遍歷性」也很重要。 在此上下文中，可遍歷性是分類的功能，它允許根據內容的路徑可預知地訪問內容。 這將使系統更易於維護，而不是需要執行大量查詢的系統。

此外，在設計分類時，必須考慮排序是否重要。 在不需要顯式排序且需要大量同級節點的情況下，最好使用未排序的節點類型，如 `sling:Folder` 或 `oak:Unstructured`。 如果需要訂購， `nt:unstructured` 和 `sling:OrderedFolder` 更合適。

### 元件中的查詢 {#queries-in-components}

由於查詢可能是在系統上執行的較繁重的操作AEM之一，因此最好在元件中避免查詢。 每次呈現頁面時執行多個查詢通常會降低系統效能。 有兩種策略可用於避免在渲染元件時執行查詢： **遍歷節點** 和 **預取結果**。

#### 遍歷節點 {#traversing-nodes}

如果儲存庫的設計方式允許預先知道所需資料的位置，則可以部署從必要路徑檢索此資料的代碼，而無需運行查詢以查找它。

其中一個示例是呈現符合特定類別的內容。 一種方法是使用可查詢的類別屬性來組織內容，以填充顯示類別中項目的元件。

更好的方法是將此內容按類別結構化，以便可以手動檢索。

例如，如果內容儲存在類別中，類似於：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

這樣 `/content/myUnstructuredContent/parentCategory/childCategory` 節點可以簡單地檢索，其子項可以被解析並用於呈現元件。

此外，當您處理小型或同構結果集時，遍歷儲存庫和收集所需節點的速度可以更快，而不是編寫查詢以返回相同的結果集。 作為一般考慮，在可能的情況下應避免查詢。

#### 預取結果 {#prefetching-results}

有時，元件周圍的內容或要求不允許使用節點遍歷作為檢索所需資料的方法。 在這些情況下，需要在呈現元件之前執行所需的查詢，以便確保最終用戶的最佳效能。

如果可以在建立元件時計算元件所需的結果，並且沒有預期內容會更改，則當作者在對話框中應用設定時，可以執行查詢。

如果資料或內容將定期更改，則查詢可以按計畫或通過監聽程式執行，以更新基礎資料。 然後，結果可以寫入儲存庫中的共用位置。 需要此資料的任何元件隨後都可以從此單個節點中提取值，而無需在運行時執行查詢。

## 查詢優化 {#query-optimization}

運行未使用索引的查詢時，將記錄有關節點遍歷的警告。 如果這是將經常運行的查詢，則應建立索引。 要確定給定查詢正在使用哪個索引， [解釋查詢工具](/help/sites-administering/operations-dashboard.md#explain-query) 。 有關其他資訊，可以為相關搜索API啟用DEBUG日誌記錄。

>[!NOTE]
>
>修改索引定義後，需要重新生成（重新編入索引）索引。 根據索引的大小，完成此操作可能需要一些時間。

在運行複雜查詢時，可能會出現這樣的情況：將查詢分解為多個較小的查詢，並在事實性更強後通過代碼將資料聯接起來。 這些案例的建議是比較兩種方法的績效，以確定哪一種方法更適合有關的使用案例。

AEM允許以三種方式之一寫入查詢：

* 通過 [QueryBuilder API](/help/sites-developing/querybuilder-api.md) （推薦）
* 使用XPath（推薦）
* 使用SQL2

雖然所有查詢在運行前都轉換為SQL2，但查詢轉換的開銷是最小的，因此，選擇查詢語言時最關心的是開發團隊的可讀性和舒適性。

>[!NOTE]
>
>使用QueryBuilder時，它將預設確定結果計數，與Jackrabbit的早期版本相比，Oak中的結果計數較慢。 為了彌補這一缺點，您可以 [guessTotal參數](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)。

### 解釋查詢工具 {#the-explain-query-tool}

與任何查詢語言一樣，優化查詢的第一步是瞭解如何執行查詢。 要啟用此活動，可以使用 [解釋查詢工具](/help/sites-administering/operations-dashboard.md#explain-query) 屬於「操作」操控板的一部分。 使用此工具，可插入並解釋查詢。 如果查詢將導致大型儲存庫以及將使用的索引出現問題，則會顯示警告。 該工具還可以載入慢速和常用查詢清單，然後可以解釋和優化這些查詢。

### 查詢的DEBUG日誌記錄 {#debug-logging-for-queries}

要獲取有關Oak如何選擇要使用的索引以及查詢引擎如何實際執行查詢的其他資訊， **調試** 可以為以下包添加日誌記錄配置：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

確保在完成查詢的調試後刪除此記錄器，因為查詢將輸出大量活動，並且最終會用日誌檔案填充磁碟。

有關如何執行此操作的詳細資訊，請參閱 [記錄文檔](/help/sites-deploying/configure-logging.md)。

### 索引統計資訊 {#index-statistics}

Lucene註冊JMX Bean，該JMX Bean將提供有關索引內容的詳細資訊，包括每個索引中所存在的文檔的大小和數量。

通過訪問JMX控制台，您可以訪問 `https://server:port/system/console/jmx`

登錄到JMX控制台後，執行搜索 **Lucene索引統計資訊** 才能找到。 可在 **索引統計** MBean。

有關查詢統計資訊，請查看名為 **Oak查詢統計資訊**。

如果您想使用類似 [盧克](https://code.google.com/p/luke/)，您需要使用Oak控制台從 `NodeStore` 檔案系統目錄。 有關如何執行此操作的說明，請閱讀 [Lucene文檔](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

您還可以以JSON格式提取系統中的索引。 為了做到這一點，你需要 `https://server:port/oak:index.tidy.-1.json`

### 查詢限制 {#query-limits}

**開發期間**

設定低閾值 `oak.queryLimitInMemory` (例如 10000)和橡木。 `queryLimitReads` (例如 5000)，並在命中UnsupportedOperationException（說「查詢讀取的節點數超過x個……」）時優化昂貴的查詢。

這有助於避免資源密集型查詢(即。 不支援任何索引或支援較少覆蓋索引)。 例如，讀取100萬個節點的查詢將導致I/O增加，並對整個應用程式效能產生負面影響。 應分析並優化任何由於上述限制而失敗的查詢。

#### **部署後** {#post-deployment}

* 監視日誌，查看觸發大節點遍歷或大堆記憶體消耗的查詢：&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 優化查詢以減少遍歷節點數

* 監視日誌以查找觸發大堆記憶體消耗的查詢：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 優化查詢以減少堆記憶體消耗

對AEM於6.0 - 6.2版本，可以通過啟動指令碼中的JVM參數調整節點遍歷的閾值AEM，以防止大型查詢使環境過載。

建議的值為：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM6.3中，上述2個參數是預配置的OOTB，可通過OSGi QueryEngineSettings永續。

更多資訊可在以下位置獲得： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 建立有效索引的提示 {#tips-for-creating-efficient-indexes}

### 是否應建立索引？ {#should-i-create-an-index}

在建立或優化索引時要問的第一個問題是，在給定情況下是否確實需要索引。 如果您只要通過批處理在系統的非高峰時間運行查詢一次或僅偶爾運行查詢，則最好不要建立索引。

建立索引後，每次更新索引資料時，也必須更新索引。 由於這會對系統產生效能影響，因此只應在實際需要索引時才建立索引。

此外，只有當索引中包含的資料足夠唯一，足以保證其可用時，索引才有用。 考慮一本書中的索引及其所涵蓋的主題。 在對文本中的一組主題進行索引時，通常會有成百上千個條目，這允許您快速跳轉到頁面的子集以快速查找您正在查找的資訊。 如果該索引只有兩、三個條目，每個條目指向數百頁，則該索引將不太有用。 這一概念同樣適用於資料庫索引。 如果只有幾個唯一值，則索引將不會非常有用。 話雖如此，一個指數也可能變得過大，無法發揮作用。 要查看索引統計資訊，請參見 [索引統計資訊](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) 上。

### Lucene還是屬性索引？ {#lucene-or-property-indexes}

在Oak 1.0.9中引入了Lucene指數，對6號初始發射時引入的效能指標進行了強AEM大優化。 在決定是使用Lucene索引還是屬性索引時，請考慮以下因素：

* Lucene索引提供的功能比屬性索引多得多。 例如，屬性索引只能為單個屬性編製索引，而Lucene索引可以包含多個屬性。 有關Lucene索引中所有可用功能的詳細資訊，請參閱 [文檔](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。
* Lucene索引是非同步的。 雖然這可以顯著提高效能，但也會導致在將資料寫入儲存庫和更新索引之間出現延遲。 如果查詢返回100%準確結果至關重要，則需要屬性索引。
* 由於非同步，Lucene索引無法強制執行唯一性約束。 如果需要，則需要設定屬性索引。

通常，建議您使用Lucene索引，除非迫切需要使用屬性索引，以便您能夠獲得更高效能和靈活性的好處。

### 索爾索引 {#solr-indexing}

AEM預設情況下還支援Solr索引。 這主要用於支援全文搜索，但也可用於支援任何類型的JCR查詢。 當實例沒有CPUAEM容量來處理搜索密集型部署（如具有大量併發用戶的搜索驅動網站）所需的查詢數時，應考慮Solr。 或者，Solr可以採用基於爬蟲的方法來實現，以利用平台的一些更高級的功能。

可以將Solr索引配置為在伺服器上AEM為開發環境運行嵌入式索引，或將其卸載到遠程實例，以提高生產和轉移環境上的搜索可擴充性。 雖然卸載搜索會提高可擴充性，但會引入延遲，因此，除非需要，不建議這樣做。 有關如何配置Solr整合以及如何建立Solr索引的詳細資訊，請參閱 [Oak查詢和索引文檔](/help/sites-deploying/queries-and-indexing.md#the-solr-index)。

>[!NOTE]
>
>而採用整合的Solr搜索方法則允許將索引卸載到Solr伺服器。 如果通過基於爬網程式的方法使用Solr伺服器的更高級功能，則需要進行其他配置工作。 頭線已經 [開源連接器](https://www.aemsolrsearch.com/#/) 以加速這些類型的實施。

採用這種方法的缺點是，在預設AEM情況下，查詢會尊重ACL，從而隱藏用戶無法訪問的結果，將搜索外部化到Solr伺服器將不支援此功能。 如果要以這種方式將搜索外部化，則必須格外小心，以確保用戶不會看到他們不應看到的結果。

此方法可能適合的潛在使用案例，是指可能需要聚合來自多個來源的搜索資料的案例。 例如，您可能有一個站點在AEM第三方平台上承載，另一個站點在第三方平台上承載。 可以配置Solr來爬網兩個站點的內容並將它們儲存在聚合索引中。 這將允許跨站點搜索。

### 設計注意事項 {#design-considerations}

Oak文檔中的Lucene索引列出了設計索引時需要考慮的幾個問題：

* 如果查詢使用不同的路徑限制，則利用 `evaluatePathRestrictions`。 這將允許查詢返回指定路徑下的結果子集，然後根據查詢篩選結果。 否則，查詢將搜索儲存庫中與查詢參數匹配的所有結果，然後根據路徑篩選這些結果。
* 如果查詢使用排序，請為sorted屬性定義顯式屬性並設定 `ordered` 至 `true` 為了它。 這樣，結果就可以在索引中按此順序排序，並在查詢執行時節省昂貴的排序操作。

* 只將所需內容放入索引中。 添加不需要的功能或屬性將導致索引增長並降低效能。
* 在屬性索引中，具有唯一屬性名稱有助於減小索引的大小，但對於Lucene索引，使用 `nodeTypes` 和 `mixins` 以達到凝聚性指標。 查詢特定 `nodeType` 或 `mixin` 比查詢效能更高 `nt:base`。 使用此方法時，定義 `indexRules` 為 `nodeTypes` 的。

* 如果查詢僅在某些路徑下運行，則在這些路徑下建立這些索引。 索引不必駐留在儲存庫的根中。
* 建議當所有要索引的屬性都與允許Lucene以本機方式計算盡可能多的屬性限制相關時使用單個索引。 此外，即使執行連接，查詢也只使用一個索引。

### CopyOnRead {#copyonread}

在 `NodeStore` 遠程儲存，名為 `CopyOnRead` 的子菜單。 此選項將導致讀取遠程索引時將其寫入本地檔案系統。 這有助於提高通常針對這些遠程索引運行的查詢的效能。

可以在OSGi控制台中的 **LuceneIndexProvider** 預設啟用，Oak 1.0.13。

### 刪除索引 {#removing-indexes}

刪除索引時，總是建議通過設定 `type` 屬性 `disabled` 並執行測試以確保應用程式在實際刪除之前正確運行。 請注意，索引在禁用時未更新，因此如果重新啟用，則可能沒有正確的內容，並且可能需要重新編製索引。

在刪除TarMK實例上的屬性索引後，需要運行壓縮以回收正在使用的任何磁碟空間。 對於Lucene索引，實際索引內容位於BlobStore中，因此需要資料儲存垃圾收集。

在MongoDB實例上刪除索引時，刪除成本與索引中的節點數成比例。 由於刪除大索引可能會導致問題，建議的方法是禁用索引並僅在維護窗口期間使用工具(如 **奧克蒙戈**。 請注意，常規節點內容不應採用這種方法，因為它可能會導致資料不一致。

>[!NOTE]
>
>有關oak-mongo.js的詳細資訊，請參閱 [「命令行工具」部分](https://jackrabbit.apache.org/oak/docs/command_line.html) Oak的文檔。

### JCR查詢作弊表 {#jcrquerycheatsheet}

為支援建立高效的JCR查詢和索引定義， [JCR查詢作弊表](assets/JCR_query_cheatsheet-v1.1.pdf) 可供下載，並在開發過程中用作參考。 它包含QueryBuilder、XPath和SQL-2的示例查詢，涵蓋多個在查詢效能方面表現不同的情形。 它還提供了如何構建或自定義Oak索引的建議。 本「作弊表」的內容適AEM用於6.5和AEMas a Cloud Service。

## 重新索引 {#re-indexing}

本節概述 **僅** 重新編製Oak索引的合理理由。

在下面介紹的原因之外，啟動Oak索引的重新索引 **不** 更改行為或解決問題，並不必要地增加負AEM載。

除非下表中的原因包含，否則應避免重新編製Oak索引。

>[!NOTE]
>
>在查閱下表以確定是否重新編製索引之前， **總是** 驗證：
>
>* 查詢正確
>* 查詢解析為預期索引(使用 [解釋查詢](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* 索引過程已完成
>


### Oak索引配置更改 {#oak-index-configuration-changes}

重新索引Oak索引的唯一可接受的非索引條件是Oak索引的配置已更改。

*應始終對重新編製索引進行處理，並適當考慮其對AEM整體效能的影響，並在活動量較低或維護時間較短的期間執行。*

下列可能的具體問題和決議：

* [屬性索引定義更改](#property-index-definition-change)
* [Lucene索引定義更改](#lucene-index-definition-change)

#### 屬性索引定義更改 {#property-index-definition-change}

* 申請/如果：

   * 所有Oak版本
   * 僅 [屬性索引](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* 症狀:

   * 屬性索引定義更新之前存在的節點在結果中缺失

* 如何驗證：

   * 確定是否在部署更新的索引定義之前建立/修改了缺少的節點。
   * 驗證 `jcr:created` 或 `jcr:lastModified` 根據索引的修改時間顯示的任何缺失節點的屬性

* 如何解決：

   * [重新索引](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) lucene指數
   * 或者，對缺少的節點進行觸摸（執行良性寫入操作）

      * 需要手動觸摸或自定義代碼
      * 需要已知缺少的節點集
      * 需要更改節點上的任何屬性

#### Lucene索引定義更改 {#lucene-index-definition-change}

* 申請/如果：

   * 所有Oak版本
   * 僅 [苜蓿指數](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症狀:

   * Lucene指數不包含預期結果
   * 查詢結果不反映索引定義的預期行為
   * 查詢計畫不根據索引定義報告預期輸出

* 如何驗證：

   * 使用Lucene索引統計資訊JMX Mbean(LuceneIndex)、方法驗證索引定義是否已更改 `diffStoredIndexDefinition`。

* 如何解決：

   * 1.6之前的橡木版：

      * [重新索引](#how-to-re-index) lucene指數
   * 橡木版本1.6+

      * 如果現有內容不受更改的影響，則只需刷新

         * [刷新](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) lucene指數 [oak:queryIndexDefinition]@refresh=true
      * 否則， [重新索引](#how-to-re-index) lucene指數

         * 注：將使用上次正確重新索引（或初始索引）的索引狀態，直到觸發新的重新索引



### 錯誤和異常情況 {#erring-and-exceptional-situations}

下表介紹了重新索引Oak索引將解決該問題的唯一可接受的錯誤和異常情況。

如果遇到與下AEM面列出的標準不匹配的問題，請執行 **不** 重新索引所有索引，因為它不會解決問題。

下列可能的具體問題和決議：

* [缺少Lucene索引二進位檔案](#lucene-index-binary-is-missing)
* [Lucene索引二進位檔案已損壞](#lucene-index-binary-is-corrupt)

#### 缺少Lucene索引二進位檔案 {#lucene-index-binary-is-missing}

* 申請/如果：

   * 所有Oak版本
   * 僅 [苜蓿指數](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症狀:

   * Lucene指數不包含預期結果

* 如何驗證：

   * 錯誤日誌檔案包含異常，表示缺少Lucene索引的二進位檔案

* 如何解決：

   * 執行遍歷儲存庫檢查；例如：

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      遍歷儲存庫確定是否缺少其他二進位檔案（除lucene檔案外）

   * 如果缺少除lucene索引以外的二進位檔案，則從備份中恢復
   * 否則， [重新索引](#how-to-re-index) *全部* 苜蓿指數
   * 注意:

      此條件表示可能導致ANY二進位的配置錯誤的資料儲存(例如 assets二進位檔案)。

      在這種情況下，還原到儲存庫的最後一個已知良好版本以恢復所有丟失的二進位檔案。

#### Lucene索引二進位檔案已損壞 {#lucene-index-binary-is-corrupt}

* 申請/如果：

   * 所有Oak版本
   * 僅 [苜蓿指數](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症狀:

   * Lucene指數不包含預期結果

* 如何驗證：

   * 的 `AsyncIndexUpdate` （每5秒）將失敗，錯誤日誌中出現異常：

      `...a Lucene index file is corrupt...`

* 如何解決：

   * 刪除lucene索引的本地副本

      1. 停AEM止
      1. 刪除位於的lucene索引的本地副本 `crx-quickstart/repository/index`
      1. 重新啟AEM動
   * 如果這無法解決問題， `AsyncIndexUpdate` 例外會繼續存在。

      1. [重新索引](#how-to-re-index) 檢索
      1. 另請提交 [Adobe支援](https://helpx.adobe.com/support.html) 票


### 如何重新索引 {#how-to-re-index}

>[!NOTE]
>
>在AEM6.5 [oak-run.jar是ONL支援的方法](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) 用於在MongoMK或RDBMK儲存庫上重新索引。

#### 重新索引屬性索引 {#re-indexing-property-indexes}

* 使用 [oak run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) 重新索引屬性索引
* 在屬性索引上將async-reindex屬性設定為true

   * `[oak:queryIndexDefinition]@reindex-async=true`

* 使用Web控制台通過 **PropertyIndexAsyncReindex** MBean;

   比如說，

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### 重新索引Lucene屬性索引 {#re-indexing-lucene-property-indexes}

* 使用 [oak-run.jar到重新索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) Lucene屬性索引。
* 在lucene屬性索引上將async-reindex屬性設定為true

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>前一部分總結並框定了Oak重新索引指南 [Apache Oak文檔](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) 的下AEM界。

### 二進位文本預提取 {#text-pre-extraction-of-binaries}

文本預提取是從二進位檔案中提取和處理文本的過程，通過隔離的過程直接從資料儲存中提取，並直接將提取的文本暴露在Oak索引的後續重新/索引中。

* 建議對包含可提取文本(如 PDF、Word文檔、PPT、TXT等) 通過已部署的Oak索引進行全文搜索；例如 `/oak:index/damAssetLucene`。
* 文本預提取將只有利於Lucene索引和NOT Oak屬性索引的重新/索引，因為屬性索引不會從二進位檔案中提取文本。
* 文本預提取在重文本二進位檔案(PDF、文檔、TXT等)的全文重新索引時具有很高的積極影響，因為影像不包含可提取文本，所以作為影像儲存庫的文本預提取不會獲得同樣的效率。
* 文本預提取以一種超高效的方式執行全文搜索相關文本的提取，並以超高效的方式將其呈現給Oak重建/索引過程以便消耗。

#### 何時使用CAN文本預提取？ {#when-can-text-pre-extraction-be-used}

重新索引 **現有** 啟用二進位提取的lucene索引

* 重新索引處理 **全部** 儲存庫中的候選內容；當二進位檔案從中提取全文時，會增加執行全文提取的計算負擔AEM。 文本預提取將文本提取的「計算成本高的工作」移入直接訪問資料儲存的隔離進程AEM，從而避免了在中的開銷和資源爭AEM用。

支援部署 **新** 啟用二進位AEM提取的lucene索引

* 在將新索引（啟用二進位提取）部署到中時AEM,Oak會在下次非同步全文索引運行時自動為所有候選內容編製索引。 出於上述重新索引中所述的相同原因，這可能導致過度載入AEM。

#### 何時不能使用文本預提取？ {#when-can-text-pre-extraction-not-be-used}

文本預提取不能用於添加到儲存庫的新內容，也不必。

將新內容添加到儲存庫後，將通過非同步全文索引過程自然地以增量方式進行索引（預設情況下，每5秒）。

在的正常操AEM作下，例如，通過Web UI或寫程式的Assets接收上傳Assets ，將自AEM動以增量方式將新二進位內容全文索引。 由於資料量是增量的，並且相對較小（大約5秒內可保存到儲存庫的資料量）,AEM因此可以在索引期間從二進位檔案執行全文提取，而不影響總體系統效能。

#### 使用文本預提取的先決條件 {#prerequisites-to-using-text-pre-extraction}

* 您將重新為執行全文二進位提取的lucene索引編製索引，或部署將現有內容的全文索引二進位檔案的新索引
* 要預提取文本的內容（二進位檔案）必須位於儲存庫中
* 生成CSV檔案並執行最終重新索引的維護窗口
* 橡木版：1.0.18+,1.2.3+
* [oak run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)版本1.7.4+
* 儲存可從索引實例訪問的提取文本的檔案AEM系統資料夾/共用

   * 文本預提取OSGi配置需要提取的文本檔案的檔案系統路徑，因此必須直接從實例(本地驅動器或檔案共用裝載AEM)訪問這些檔案

#### 如何執行文本預提取 {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***下面概述的oak-run.jar命令在以下位置完全枚舉 [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>上圖和下面的步驟用於解釋和補充Apache Oak文檔中概述的技術文本預提取步驟。

![文本預提取流程](assets/chlimage_1-139.png)

**生成要預提取的內容清單**

*在維護窗口/低使用期間執行步驟1(a-b)，因為節點儲存在此操作期間會遍歷，這可能會給系統帶來大量負載。*

1a 執行 `oak-run.jar --generate` 建立要預提取其文本的節點清單。

1b 節點清單(1a)作為CSV檔案儲存到檔案系統

請注意，每次都會遍歷整個節點儲存（如oak-run命令中的路徑所指定） `--generate` 執行，並且 **新** 建立CSV檔案。 CSV檔案為 **不** 在文本預提取過程的離散執行之間重新使用（步驟1-2）。

**預提取文本到檔案系統**

*步驟2(a-c)只與資料儲存AEM器交互，在正常操作期間執行。*

2a 執行 `oak-run.jar --tika` 為在(1b)中生成的CSV檔案中枚舉的二進位節點預提取文本

2b 在(2a)中啟動的進程直接訪問資料儲存中CSV中定義的二進位節點，並提取文本。

2c  提取的文本以Oak重新索引處理(3a)可接收的格式儲存在檔案系統上

預提取的文本在CSV中由二進位指紋標識。 如果二進位檔案相同，則可以跨實例使用相同的預提取文AEM本。 由於AEM發佈通常是AEM作者的子集，因此從AEM Author中預提取的文本也經常用於重新索引AEM發佈（假定AEM發佈具有檔案系統對提取的文本檔案的訪問權限）。

預提取的文本可以逐漸添加到時間中。 文本預提取將跳過對先前提取的二進位檔案的提取，因此最好保留預提取的文本，以防將來必須再次重新索引（假定提取的內容不會過大）。 如果是，則評估在中間對內容進行壓縮，因為文本壓縮良好)。

**重新索引Oak索引，從提取的文本檔案中獲取全文**

*在維護/低使用期間執行重新索引（步驟3a-b），因為節點儲存在此操作期間會被遍歷，這可能會給系統帶來重大負載。*

3a [重新索引](#how-to-re-index) 調用Lucene索引AEM

3b Apache Jackrabbit Oak DataStore PreExtractTextProvider OSGi配置（配置為通過檔案系統路徑指向提取的文本）指示Oak從提取的檔案中提取全文文本，並避免直接訪問和處理儲存在儲存庫中的資料。
