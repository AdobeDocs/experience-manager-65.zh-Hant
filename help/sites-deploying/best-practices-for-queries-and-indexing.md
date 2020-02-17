---
title: 查詢和索引的最佳做法
seo-title: 查詢和索引的最佳做法
description: 本文提供如何最佳化索引和查詢的指引。
seo-description: 本文提供如何最佳化索引和查詢的指引。
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 查詢和索引的最佳做法{#best-practices-for-queries-and-indexing}

在AEM 6中轉換至Oak後，對查詢和索引的管理方式做了一些重大變更。 在Jackrabbit 2下，預設會建立所有內容的索引，並可自由查詢。 在Oak中，索引必須在節點下手動 `oak:index` 建立。 查詢可以在沒有索引的情況下執行，但對於大型資料集，執行速度會非常慢，甚至中止。

本文將概述何時建立索引以及何時不需要索引、避免在不需要查詢時使用查詢的技巧，以及最佳化索引和查詢以盡可能最佳化執行的提示。

此外，請務必閱讀有關編寫查 [詢和索引的Oak檔案](/help/sites-deploying/queries-and-indexing.md)。 除了索引是AEM 6的新概念外，從舊版AEM安裝移轉程式碼時，Oak查詢中也有語法差異需要考慮。

## 何時使用查詢 {#when-to-use-queries}

### 儲存庫和分類法設計 {#repository-and-taxonomy-design}

在設計儲存庫的分類時，需要考慮幾個因素。 其中包括存取控制、本地化、元件和頁面屬性繼承等。

在設計可解決這些問題的分類法時，還必須考慮索引設計的「可通過性」。 在此上下文中，可遍歷性是分類法的能力，它允許根據內容的路徑可預測地訪問內容。 這樣，與需要執行大量查詢的系統相比，更易於維護的系統效能更高。

此外，在設計分類時，務必考慮排序是否重要。 在不需要顯式排序且需要大量同級節點的情況下，最好使用無序節點類型，如 `sling:Folder` 或 `oak:Unstructured`。 如果需要訂購， `nt:unstructured` 則 `sling:OrderedFolder` 更合適。

### 元件中的查詢 {#queries-in-components}

由於查詢是AEM系統上較耗時的作業之一，因此建議您在元件中避免查詢。 每次呈現頁面時執行多個查詢通常會降低系統的效能。 在呈現元件時，有兩種策略可用來避免執行查詢：遍 **歷節點** , **預取結果**。

#### 遍歷節點 {#traversing-nodes}

如果儲存庫的設計允許事先知道所需資料的位置，則可從所需路徑中檢索此資料的代碼可以部署，而無需運行查詢以查找該資料。

例如，可轉換符合特定類別的內容。 一種方法是使用類別屬性來組織內容，該類別屬性可以查詢，以填入顯示類別項目的元件。

更好的方法是將此內容按類別結構化，以便手動檢索。

例如，如果內容儲存在類似以下內容的分類中：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

節 `/content/myUnstructuredContent/parentCategory/childCategory` 點可以簡單地檢索，其子項可以被解析並用於渲染元件。

此外，在處理小型或同構結果集時，更快地遍歷儲存庫並收集所需節點，而不是建立一個查詢以返回相同的結果集。 作為一般考慮，應盡可能避免查詢。

#### 預取結果 {#prefetching-results}

有時，元件的內容或要求不允許使用節點遍歷作為檢索所需資料的方法。 在這些情況下，需要在轉換元件之前執行所需的查詢，以確保最終用戶的最佳效能。

如果在編寫元件時可以計算所需的結果，而且內容不會更改，則當作者在對話框中應用設定時可以執行查詢。

如果資料或內容會定期變更，則可依排程或透過監聽程式執行查詢，以更新基礎資料。 然後，結果可以寫入儲存庫中的共用位置。 任何需要此資料的元件，都可從此單一節點提取值，而不需在執行時期執行查詢。

## 查詢優化 {#query-optimization}

運行未使用索引的查詢時，將記錄有關節點遍歷的警告。 如果此查詢將經常運行，則應建立索引。 要確定給定查詢使用的索引，建議使 [用「解釋查詢](/help/sites-administering/operations-dashboard.md#explain-query) 」工具。 如需詳細資訊，可針對相關搜尋API啟用DEBUG記錄。

>[!NOTE]
>
>修改索引定義後，需要重建索引（重新建立索引）。 根據索引的大小，可能需要一些時間才能完成。

在運行複雜查詢時，可能會將查詢分解為多個較小的查詢，並在事實性更高後通過代碼連接資料。 這些案例的建議是比較兩種方法的績效，以確定哪個選項更適合有關的使用案例。

AEM允許以下列三種方式之一來編寫查詢：

* 透過 [QueryBuilder API](/help/sites-developing/querybuilder-api.md) （建議）
* 使用XPath（建議）
* 使用SQL2

雖然所有查詢在運行前都轉換為SQL2，但查詢轉換的開銷非常小，因此，選擇查詢語言時最關心的是開發團隊的可讀性和舒適性。

>[!NOTE]
>
>使用QueryBuilder時，會依預設判斷結果計數，與舊版Jackrabbit相比，Oak中的結果計數較慢。 若要彌補這一點，您可以使用 [guessTotal參數](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)。

### Explain Query Tool {#the-explain-query-tool}

和任何查詢語言一樣，最佳化查詢的第一步是瞭解查詢的執行方式。 要啟用此活動，可以使用「操 [作儀表板」中的](/help/sites-administering/operations-dashboard.md#explain-query) 「解釋查詢」工具。 使用此工具，可插入並解釋查詢。 如果查詢將導致大型儲存庫以及執行時間和將使用的索引出現問題，則會顯示警告。 此工具也可以載入慢速和常用查詢清單，然後加以說明並最佳化。

### 查詢的DEBUG日誌 {#debug-logging-for-queries}

若要取得有關Oak如何選擇要使用的索引以及查詢引擎如何實際執行查詢的其他資訊，可針對下列套件新增 **DEBUG** logging configuration:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

請務必在查詢除錯完成後移除此記錄器，因為查詢會輸出許多活動，並最終會用記錄檔填滿您的磁碟。

如需如何執行此動作的詳細資訊，請參閱記 [錄檔案](/help/sites-deploying/configure-logging.md)。

### 索引統計資訊 {#index-statistics}

Lucene註冊一個JMX Bean，該Bean將提供有關索引內容的詳細資訊，包括每個索引中存在的文檔的大小和數量。

您可以存取JMX主控台， `https://server:port/system/console/jmx`

登入JMX主控台後，請搜尋 **Lucene Index Statistics** ，以便找到它。 其他索引統計資料可在 **IndexStats** MBean中找到。

若為查詢統計資料，請查看名為 **Oak Query Statistics的MBean**。

如果想使用像 [Luke](https://code.google.com/p/luke/)這樣的工具挖掘索引，則需要使用Oak控制台將索引從檔案系統目錄 `NodeStore` 轉儲到檔案系統目錄。 有關如何執行此操作的說明，請閱讀 [Lucene文檔](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

您也可以擷取系統中的JSON格式索引。 若要這麼做，您必須存取 `https://server:port/oak:index.tidy.-1.json`

### 查詢限制 {#query-limits}

**開發期間**

設定低臨界值 `oak.queryLimitInMemory` (例如 10000)和橡樹。 `queryLimitReads` (例如 5000)，並最佳化當點擊「查詢讀取的節點數超過x個……」的UnsupportedOperationException時，昂貴的查詢。

這有助於避免資源密集型查詢(即 不受任何索引的支援，或受較少覆蓋指數的支援)。 例如，讀取100萬個節點的查詢會導致I/O增加，並對整體應用程式效能產生負面影響。 任何因上述限制而失敗的查詢都應加以分析和最佳化。

#### **部署後**{#post-deployment}

* 監視日誌中觸發大節點遍歷或大堆記憶體消耗的查詢：&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 優化查詢以減少遍歷的節點數

* 監視日誌中觸發大量堆記憶體消耗的查詢：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 優化查詢以減少堆記憶體消耗

對於AEM 6.0 - 6.2版本，您可以在AEM啟動指令碼中調整透過JVM參數的節點周遊臨界值，以防止大型查詢超出環境負載。

建議的值為：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述2個參數是預先設定的OOTB，並可透過OSGi queryEngineSettings持續存在。

以下網址提供更多資訊： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 建立高效索引的提示 {#tips-for-creating-efficient-indexes}

### 我應該建立索引嗎？ {#should-i-create-an-index}

建立或最佳化索引時，首先要問的問題是，是否確實需要索引來設定特定情況。 如果您只要運行問題查詢一次，或僅偶爾運行查詢，並且在通過批處理的非高峰時間運行，則最好不要建立索引。

建立索引後，每次更新索引資料時，索引也必須更新。 由於這對系統具有效能影響，因此僅應在實際需要索引時建立索引。

此外，索引只有在索引中包含的資料足夠唯一以保證其安全時才有用。 考慮一本書中的索引及其涵蓋的主題。 在為文字中的一組主題建立索引時，通常會有數百或數千個項目，這可讓您快速跳至頁面的子集，以快速找到您要尋找的資訊。 如果該索引只有兩三個條目，每個條目指向幾百個頁面，則該索引將不太有用。 這一概念同樣適用於資料庫索引。 如果只有幾個唯一值，則索引將非常有用。 話雖如此，一個指數也可能變得過大，無法發揮作用。 要查看索引統計資訊，請參 [閱上述索引統計](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) 。

### Lucene或屬性索引？ {#lucene-or-property-indexes}

Lucene索引已在Oak 1.0.9中引入，並針對AEM 6初次啟動時引入的屬性索引提供一些強大的最佳化功能。 在決定是使用Lucene索引還是屬性索引時，請考慮以下因素：

* Lucene索引提供的功能比屬性索引更多。 例如，屬性索引只能為單一屬性建立索引，而Lucene索引可以包含許多屬性。 有關Lucene索引中所有可用功能的詳細資訊，請參閱文 [檔](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。
* Lucene索引是非同步的。 雖然這可大幅提升效能，但也會在將資料寫入儲存庫和更新索引之間造成延遲。 如果讓查詢傳回100%精確的結果至關重要，則需要屬性索引。
* 由於Lucene索引是非同步的，因此無法強制執行唯一性約束。 如果需要，則需要建立屬性索引。

通常，建議您使用Lucene索引，除非您迫切需要使用屬性索引，以便獲得更高的效能和靈活性。

### 索爾索引 {#solr-indexing}

AEM也依預設提供Solr索引支援。 這主要用於支援全文搜尋，但也可用於支援任何類型的JCR查詢。 當AEM例項沒有CPU容量來處理搜尋密集型部署（例如同時擁有大量使用者的搜尋導向網站）所需查詢數時，應考慮Solr。 此外，Solr可以採用基於爬蟲的方法來實現，以利用平台的一些更高級的功能。

Solr索引可設定為在AEM伺服器上執行以用於開發環境，或可卸載至遠端例項，以改善生產與測試環境的搜尋延展性。 雖然卸載搜索將改善可擴充性，但會引入延遲，因此，除非需要，否則不建議這樣做。 有關如何配置Solr整合以及如何建立Solr索引的詳細資訊，請參閱 [Oak查詢和索引文檔](/help/sites-deploying/queries-and-indexing.md#the-solr-index)。

>[!NOTE]
>
>採用整合的Solr搜索方法時，可將索引卸載到Solr伺服器。 如果通過基於爬蟲的方法使用Solr伺服器的更高級功能，則需要額外的配置工作。 Headwire已建立開放 [原始碼連接器](https://www.aemsolrsearch.com/#/) ，以加速這些類型的實施。

採用此方法的缺點是，雖然依預設，AEM查詢會尊重ACL，因此會隱藏使用者無權存取的結果，將搜尋外部化至Solr伺服器將不支援此功能。 如果要以這種方式將搜尋外部化，則必須格外小心，以確保使用者不會看到他們不應看到的結果。

如果此方法可能適合的潛在使用案例，則可能需要匯整來自多個來源的搜尋資料。 例如，您可能有一個網站是在AEM上代管，而另一個網站是在第三方平台上代管。 Solr可設定為編目兩個網站的內容，並將它們儲存在匯總索引中。 這可允許跨網站搜尋。

### 設計考量 {#design-considerations}

Oak documentation for Lucene indexes列出設計索引時要考慮的幾項事項：

* 如果查詢使用不同的路徑限制，請使用 `evaluatePathRestrictions`。 這將允許查詢返回指定路徑下的結果子集，然後根據查詢篩選結果。 否則，查詢將搜索與儲存庫中的查詢參數匹配的所有結果，然後根據路徑進行篩選。
* 如果查詢使用排序，請為sorted屬性定義明確的屬性，並為其 `ordered` 設定 `true` 為。 這樣，結果就可以在索引中按此順序排列，並節省查詢執行時的昂貴排序操作。

* 只將所需內容放入索引中。 新增不需要的功能或屬性會導致索引增長並降低效能。
* 在屬性索引中，具有唯一的屬性名稱有助於減小索引的大小，但對於Lucene索引，應使用 `nodeTypes``mixins` 和以實現連貫索引。 查詢特定 `nodeType` 或的 `mixin` 效能將高於查詢 `nt:base`。 使用此方法時，請 `indexRules` 為有關 `nodeTypes` 的定義。

* 如果您的查詢僅在某些路徑下運行，請在這些路徑下建立這些索引。 索引在儲存庫的根目錄中不是必需的。
* 建議在所有要索引的屬性都相關時使用單一索引，讓Lucene能夠以原生方式評估盡可能多的屬性限制。 此外，查詢將只使用一個索引，即使在執行連接時也是如此。

### CopyOnRead {#copyonread}

在遠程儲存 `NodeStore` 時，可以啟用名為 `CopyOnRead` 的選項。 該選項將使遠程索引在讀取時寫入本地檔案系統。 這有助於改進經常針對這些遠程索引運行的查詢的效能。

這可在OSGi控制台的 **LuceneIndexProvider** service下進行設定，並自Oak 1.0.13起預設啟用。

### 刪除索引 {#removing-indexes}

刪除索引時，建議您先將屬性設為並執行測試，以確 `type` 保應用程 `disabled` 式在實際刪除前正常運作，以暫時停用索引。 請注意，索引在停用時不會更新，因此，如果重新啟用索引，並且可能需要重新建立索引，則可能沒有正確的內容。

在刪除TarMK實例上的屬性索引後，將需要運行壓縮以回收任何正在使用的磁碟空間。 對於Lucene索引，實際索引內容存在於BlobStore中，因此需要資料存放區廢棄項目收集。

刪除MongoDB實例上的索引時，刪除成本與索引中的節點數成比例。 由於刪除大型索引可能會造成問題，建議的方法是停用索引，並僅在維護視窗期間使用 **oak-mongo.js等工具加以刪除**。 請注意，此方法不適用於一般節點內容，因為它可能會造成資料不一致。

>[!NOTE]
>
>如需oak-mongo.js的詳細資訊，請參閱Oak文 [件的「命令列工具](https://jackrabbit.apache.org/oak/docs/command_line.html) 」區段。

## 重新建立索引 {#re-indexing}

本節概述重新 **索引** Oak索引的唯一可接受理由。

在下列原因外，啟動Oak索引的重新索引不會變 **更行為** 或解決問題，而且無須增加AEM的負載。

除非下表中的原因涵蓋，否則應避免重新索引Oak索引。

>[!NOTE]
>
>在查閱下表以判斷是否重新建立索引之前，請務必**確認：
>
>* 查詢正確
>* 查詢解析為預期索引(使用「解 [釋查詢」](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* 索引程式已完成
>



### Oak索引組態變更 {#oak-index-configuration-changes}

唯一可接受的Oak索引重新索引的非重新索引條件，是Oak索引的組態已變更。

*應始終對重新索引進行處理，並適當考慮它對AEM整體效能的影響，並在活動量較低或維護期間執行。*

以下是可能的細節問題和決議：

* [屬性索引定義更改](#property-index-definition-change)
* [Lucene指數定義更改](#lucene-index-definition-change)

#### 屬性索引定義更改 {#property-index-definition-change}

* 適用／如果：

   * 所有Oak版本
   * 僅屬 [性索引](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* 症狀：

   * 屬性索引定義之前存在的節點更新結果中缺少

* 如何驗證：

   * 確定是否在部署更新的索引定義之前建立／修改了丟失的節點。
   * 根據索 `jcr:created` 引的修 `jcr:lastModified` 改時間驗證任何缺失節點的或屬性

* 如何解決：

   * [對lucene指數重新編製索引](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index)
   * 或者，對缺少的節點進行觸摸（執行良性寫操作）

      * 需要手動觸碰或自訂程式碼
      * 需要已知缺少的節點集
      * 需要更改節點上的任何屬性

#### Lucene指數定義更改 {#lucene-index-definition-change}

* 適用／如果：

   * 所有Oak版本
   * 僅 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症狀：

   * Lucene指數不包含預期結果
   * 查詢結果不反映索引定義的預期行為
   * 查詢計畫不根據索引定義報告預期輸出

* 如何驗證：

   * 使用Lucene Index統計資訊JMX Mbean(LuceneIndex)方法驗證索引定義是否已更改 `diffStoredIndexDefinition`。

* 如何解決：

   * Oak 1.6之前版本：

      * [對lucene指數重新編製索引](#how-to-re-index)
   * Oak 1.6+版

      * 如果現有內容不受變更影響，則只需重新整理

         * [透過設定](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) oak:queryIndexDefinition []@refresh=true，重新整理lucene索引
      * 否則， [重新為lucene指數](#how-to-re-index) (R)

         * 注意：將使用上次正確重新索引（或初始索引）的索引狀態，直到觸發新的重新索引



### 錯誤和異常情況 {#erring-and-exceptional-situations}

下表說明重新建立Oak索引索引將解決此問題的唯一可接受的錯誤和例外情況。

如果AEM發生不符合下列標準的問題，請 **不要重新索引** ，因為它不會解決問題。

以下是可能的細節問題和決議：

* [缺少Lucene索引二進位檔案](#lucene-index-binary-is-missing)
* [Lucene索引二進位檔案已損壞](#lucene-index-binary-is-corrupt)

#### 缺少Lucene索引二進位檔案 {#lucene-index-binary-is-missing}

* 適用／如果：

   * 所有Oak版本
   * 僅 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症狀：

   * Lucene指數不包含預期結果

* 如何驗證：

   * 錯誤日誌檔案包含異常，表示缺少Lucene索引的二進位檔案

* 如何解決：

   * 執行遍歷儲存庫檢查；例如：

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      遍歷儲存庫可確定是否缺少其他二進位檔案（除lucene檔案外）

   * 如果缺少lucene索引以外的二進位檔案，則從備份中恢復
   * 否則，重 [新索引所有](#how-to-re-index)*lucene索引*
   * 注意:

      此條件表示可能導致ANY二進位的配置錯誤的資料儲存(如 資產二進位檔)遺失。

      在這種情況下，恢復到儲存庫的最後一個已知正常版本，以恢復所有丟失的二進位檔案。

#### Lucene索引二進位檔案已損壞 {#lucene-index-binary-is-corrupt}

* 適用／如果：

   * 所有Oak版本
   * 僅 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症狀：

   * Lucene指數不包含預期結果

* 如何驗證：

   * ( `AsyncIndexUpdate` 每5秒)將失敗，錯誤。log中出現例外：

      `...a Lucene index file is corrupt...`

* 如何解決：

   * 刪除lucene索引的本地副本

      1. 停止AEM
      1. 刪除lucene索引的本地副本(位於 `crx-quickstart/repository/index`
      1. 重新啟動AEM
   * 如果這無法解決問題，且例外情 `AsyncIndexUpdate` 況持續存在：

      1. [重新索引](#how-to-re-index) erring索引
      1. 另外，也可以 [歸檔Adobe支援](https://helpx.adobe.com/support.html) 票證


### 如何重新索引 {#how-to-re-index}

>[!NOTE]
>
>在AEM 6.5中， [oak-run.jar是MongoMK或RDBMK儲存庫上重新建立索引的唯一支援方法](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) 。

#### 重新索引屬性索引 {#re-indexing-property-indexes}

* 使 [用oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) 重新索引屬性索引
* 在屬性索引上將async-reindex屬性設為true

   * `[oak:queryIndexDefinition]@reindex-async=true`

* 使用Web控制台，透過 **PropertyIndexAsyncReindex** MBean，以非同步方式重新索引屬性索引；

   例如，

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### 重新索引Lucene屬性索引 {#re-indexing-lucene-property-indexes}

* 使 [用oak-run.jar重新索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) Lucene屬性索引。
* 在lucene屬性索引上將async-reindex屬性設為true

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>上節摘要並框定AEM內容中 [Apache Oak檔案中的Oak重新索引指引](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) 。

### 二進位文本預提取 {#text-pre-extraction-of-binaries}

文字預擷取是從二進位檔擷取和處理文字的程式，直接透過隔離的程式從資料存放區擷取並處理文字，並直接將擷取的文字呈現在Oak索引的後續重新／索引中。

* 建議使用Oak文本預抽取功能，在包含可抽取文本(如 PDF、Word檔案、PPT、TXT等)可透過部署的Oak索引取得全文搜尋；例如 `/oak:index/damAssetLucene`。
* 文本預抽取只對Lucene索引和NOT Oak屬性索引的重新／索引有利，因為屬性索引不會從二進位檔擷取文字。
* 當對大量文字的二進位檔（PDF、Doc、TXT等）進行全文重新索引時，文字預擷取會產生很大的正面影響，因為影像儲存庫不包含可擷取的文字，所以效率不相同。
* 文字預擷取會以特別有效率的方式執行全文搜尋相關文字的擷取，並以特別有效率的方式讓它進入Oak重新／索引程式以便使用。

#### 何時使用CAN文字預先擷取？ {#when-can-text-pre-extraction-be-used}

啟用二進位提取 **的現** 有lucene索引重新索引

* 重新索引處理儲存 **庫中** 所有候選內容；當要從中擷取全文的二進位檔數眾多或複雜時，AEM會增加執行全文擷取的運算負擔。 文字預先擷取將文字擷取的「運算量大、成本高」移入可直接存取AEM資料存放區的隔離程式，以避免AEM中的開銷和資源爭用。

支援在啟用二進位擷 **取的** AEM中部署新的lucene索引

* 當新索引（啟用二進位擷取）部署至AEM時，Oak會在下次執行非同步全文索引時自動為所有候選內容建立索引。 基於上述重新建立索引中所述的相同原因，這可能會導致AEM負載過重。

#### 何時不能使用文字預先擷取？ {#when-can-text-pre-extraction-not-be-used}

文本預抽取不能用於添加到儲存庫的新內容，也不必。

將新內容添加到儲存庫中，將通過非同步全文索引過程自然地逐步編製索引（預設情況下，每5秒）。

在AEM的正常運作下，例如透過網頁UI上傳資產或程式化收錄資產，AEM將自動以增量式全文索引新的二進位內容。 由於資料量是遞增的，而且相對較小（大約5秒內可保存至儲存庫的資料量）,AEM可在建立索引期間從二進位檔案執行全文擷取，而不會影響整體系統效能。

#### 使用文字預先擷取的先決條件 {#prerequisites-to-using-text-pre-extraction}

* 您將重新索引執行全文二進位擷取的lucene索引，或部署新索引，將現有內容的全文索引二進位檔案
* 要預先提取文本的內容（二進位檔案）必須位於儲存庫中
* 用於生成CSV檔案並執行最終重新索引的維護窗口
* Oak版本：1.0.18+、1.2.3+
* [oak-run.](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)jarversion 1.7.4+
* 檔案系統資料夾／共用，以儲存可從索引AEM例項存取的擷取文字

   * 「文字預先擷取OSGi」設定需要擷取文字檔案的檔案系統路徑，因此必須直接從AEM例項（本機磁碟機或檔案共用載入）存取這些檔案

#### 如何執行文字預擷取 {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***以下概述的oak-run.jar命令可在https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html上完整列舉[。](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>上圖和以下步驟可說明並補充Apache Oak檔案中概述的技術文字預先擷取步驟。

![文本預提取流程](assets/chlimage_1-139.png)

**產生要預先擷取的內容清單**

*在維護窗口／低使用期間執行步驟1(a-b)，因為在此操作期間會遍歷節點儲存，這可能會對系統產生大量負載。*

1a。 執 `oak-run.jar --generate` 行以建立預提取其文本的節點清單。

1b. 節點清單(1a)以CSV檔案形式儲存到檔案系統

請注意，每次執行時都會遍歷整個節點儲存區（如oak-run命令中的路徑所指定），並 `--generate` 且會建立 **新** CSV檔案。 CSV檔案不 **會在** 文字預擷取程式的離散執行之間重複使用（步驟1 - 2）。

**預先擷取文字至檔案系統**

*步驟2(a-c)只能與資料存放區互動，才可在AEM的正常運作期間執行。*

2a。 執 `oak-run.jar --tika` 行以預先擷取(1b)中產生之CSV檔案中列舉之二進位節點的文字

2b. 在(2a)中啟動的程式會直接存取在資料存放區的CSV中定義的二進位節點，並擷取文字。

2c.  提取的文本以Oak重新索引過程(3a)可接收的格式儲存在檔案系統上

預先提取的文本在CSV中由二進位指紋標識。 如果二進位檔案相同，則可在AEM執行個體中使用相同的預先擷取文字。 由於AEM Publish通常是AEM Author的子集，因此從AEM Author預先擷取的文字通常也可以用來重新為AEM Publish建立索引（假設AEM Publish擁有擷取文字檔案的檔案系統存取權）。

預先擷取的文字可逐漸新增至一段時間。 文字預擷取將略過先前擷取的二進位檔的擷取，因此最好保留預先擷取的文字，以免日後必須重新索引（假設擷取的內容不會過大）。 如果是，請評估在中間壓縮內容，因為文字會很好壓縮)。

**重新為Oak索引建立索引，從擷取的文字檔案擷取全文**

*在維護／低使用期間執行重新索引（步驟3a-b），因為在此操作期間會遍歷節點儲存，這可能會對系統造成大量負載。*

3a。 [在AEM中調用](#how-to-re-index) Lucene索引的重新索引

3b. Apache Jackrabbit Oak dataStore PreExtractedTextProvider OSGi組態（設定為透過檔案系統路徑指向Extracted文字）會指示Oak從Extracted Files取得全文，並避免直接點擊和處理儲存在儲存庫中的資料。

