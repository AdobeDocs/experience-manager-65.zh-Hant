---
title: 查詢和建立索引的最佳實務
seo-title: 查詢和建立索引的最佳實務
description: 本文提供如何最佳化索引和查詢的准則。
seo-description: 本文提供如何最佳化索引和查詢的准則。
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4618'
ht-degree: 0%

---

# 查詢和索引的最佳實務{#best-practices-for-queries-and-indexing}

在AEM 6中，隨著轉換為Oak，查詢和索引的管理方式也有所重大變更。 在Jackrabbit 2下，所有內容預設為索引，並可自由查詢。 在Oak中，必須在`oak:index`節點下手動建立索引。 查詢可在不使用索引的情況下執行，但對於大型資料集，執行速度會非常緩慢，甚至會中止。

本文將概述何時建立索引以及何時不需要索引、在不需要查詢時避免使用查詢的技巧，以及最佳化索引和查詢以盡可能完美執行的秘訣。

此外，請務必閱讀[有關寫入查詢和索引](/help/sites-deploying/queries-and-indexing.md)的Oak檔案。 除了AEM 6的新概念之索引外，從先前的AEM安裝移轉程式碼時，Oak查詢中也有語法差異需要納入考量。

## 查詢的使用時機{#when-to-use-queries}

### 儲存庫和分類設計{#repository-and-taxonomy-design}

在設計儲存庫的分類法時，需要考慮幾個因素。 這些功能包括存取控制、本地化、元件和頁面屬性繼承等。

在設計可解決這些問題的分類法時，也必須考慮索引設計的「可遍歷性」。 在此情境中，可周遊性是分類法的功能，分類法可根據內容的路徑進行可預測的存取。 這將使系統更易於維護，而不是需要執行大量查詢的系統。

此外，在設計分類法時，請務必考慮排序是否重要。 在不需要顯式排序且需要大量同級節點的情況下，最好使用無序節點類型，如`sling:Folder`或`oak:Unstructured`。 在需要排序的情況下，`nt:unstructured`和`sling:OrderedFolder`更合適。

### 元件{#queries-in-components}中的查詢

由於查詢可能是在AEM系統上執行的較繁重作業之一，最好在元件中避免查詢。 每次呈現頁面時執行多個查詢通常會降低系統的效能。 可使用兩種策略來避免在呈現元件時執行查詢：**遍歷節點**&#x200B;和&#x200B;**預取結果**。

#### 遍歷節點{#traversing-nodes}

如果儲存庫的設計方式允許事先了解所需資料的位置，則可從必要路徑檢索此資料的代碼可以部署，而無需運行查詢才能查找。

例如，會轉譯符合特定類別的內容。 一種方法是使用類別屬性來組織內容，可查詢該屬性以填入顯示類別中項目的元件。

更好的方法是依類別將此內容結構化，以便手動擷取。

例如，如果內容儲存在類似以下的分類法中：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

`/content/myUnstructuredContent/parentCategory/childCategory`節點可以簡單地檢索，其子節點可以被分析並用於呈現元件。

此外，處理小型或同構的結果集時，遍歷儲存庫和收集所需節點的速度可能會更快，而不是將查詢精心構建以返回相同的結果集。 作為一般考慮，在可能的情況下應避免查詢。

#### 預取結果{#prefetching-results}

有時，元件周圍的內容或需求不允許使用節點遍歷作為檢索所需資料的方法。 在這些情況下，需要在呈現元件之前執行所需的查詢，以確保最終用戶的最佳效能。

如果元件所需的結果可在製作時計算，而且內容不會變更的預期時間，則當作者在對話方塊中套用設定時，可執行查詢。

如果資料或內容會定期變更，則可依排程或透過監聽程式執行查詢，以更新基礎資料。 然後，可將結果寫入儲存庫中的共用位置。 然後，需要此資料的任何元件都可以從此單一節點提取值，而無需在執行階段執行查詢。

## 查詢優化{#query-optimization}

運行未使用索引的查詢時，將記錄有關節點遍歷的警告。 如果這是將經常運行的查詢，則應建立索引。 要確定給定查詢正在使用的索引，建議使用[解釋查詢工具](/help/sites-administering/operations-dashboard.md#explain-query)。 如需詳細資訊，可為相關搜尋API啟用DEBUG記錄。

>[!NOTE]
>
>修改索引定義後，需要重建索引（重新索引）。 根據索引的大小，完成此操作可能需要一些時間。

在運行複雜的查詢時，可能會在事實效能更好後，將查詢分解為多個較小的查詢並通過代碼加入資料。 這些案例的建議是比較兩種方法的效能，以確定哪一種方法對有關使用案例更合適。

AEM允許以三種方式之一寫入查詢：

* 透過[QueryBuilder API](/help/sites-developing/querybuilder-api.md)（建議）
* 使用XPath（建議）
* 使用SQL2

雖然在運行前所有查詢都轉換為SQL2，但查詢轉換的開銷是最小的，因此，在選擇查詢語言時最需要注意的是開發團隊的可讀性和舒適性。

>[!NOTE]
>
>使用QueryBuilder時，會依預設判斷結果計數，與舊版Jackrabbit相比，Oak中的計數較慢。 若要彌補這一點，您可以使用[guessTotal參數](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)。

### 說明查詢工具{#the-explain-query-tool}

和任何查詢語言一樣，最佳化查詢的第一步是了解查詢的執行方式。 若要啟用此活動，您可以使用作為操作控制面板一部分的[解釋查詢工具](/help/sites-administering/operations-dashboard.md#explain-query)。 使用此工具，可插入查詢並進行說明。 如果查詢會造成大型存放庫問題，以及執行時間和使用的索引，則會顯示警告。 此工具也可載入慢速和熱門查詢清單，然後可加以說明和最佳化。

### 查詢{#debug-logging-for-queries}的DEBUG記錄

若要取得其他資訊，了解Oak如何選擇要使用的索引，以及查詢引擎實際執行查詢的方式，可針對下列套件新增&#x200B;**DEBUG**&#x200B;記錄設定：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

在完成對查詢的調試後，請確保刪除此記錄器，因為它將輸出許多活動，並最終可以用日誌檔案填充磁碟。

有關如何執行此操作的詳細資訊，請參閱[記錄檔案](/help/sites-deploying/configure-logging.md)。

### 索引統計資料{#index-statistics}

Lucene註冊JMX Bean，該JMX Bean將提供有關索引內容的詳細資訊，包括每個索引中存在的文檔的大小和數量。

您可以通過訪問`https://server:port/system/console/jmx`上的JMX控制台來訪問它

登錄到JMX控制台後，請執行&#x200B;**Lucene索引統計資訊**&#x200B;的搜索以找到它。 在&#x200B;**IndexStats** MBean中可找到其他索引統計資訊。

若是查詢統計資料，請查看名為&#x200B;**Oak Query Statistics**&#x200B;的MBean。

如果您想使用[Luke](https://code.google.com/p/luke/)等工具挖掘索引，則需使用Oak主控台將索引從`NodeStore`傾印至檔案系統目錄。 有關如何執行此操作的說明，請閱讀[Lucene文檔](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

您也可以以JSON格式擷取系統中的索引。 要執行此操作，您需要存取`https://server:port/oak:index.tidy.-1.json`

### 查詢限制 {#query-limits}

**開發期間**

為`oak.queryLimitInMemory`設定低閾值(例如 10000)和橡木。 `queryLimitReads` (例如5000)，並在點擊「查詢讀取的節點數超過x個……」的UnsupportedOperationException時，優化昂貴的查詢

這有助於避免資源密集型查詢(即。 不受任何索引的支援或受覆蓋索引較少的支援)。 例如，讀取100萬個節點的查詢將導致I/O增加，並對整體應用程式效能產生負面影響。 任何因上述限制而失敗的查詢，都應加以分析和最佳化。

#### **部署後** {#post-deployment}

* 監視日誌中是否有觸發大節點遍歷或大堆記憶體消耗的查詢：&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 優化查詢以減少已遍歷的節點數

* 監視日誌中觸發大堆記憶體消耗的查詢：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 優化查詢以減少堆記憶體消耗

對於AEM 6.0 - 6.2版，您可以透過AEM啟動指令碼中的JVM參數來調整節點周遊臨界值，以防止大型查詢超出環境負載。

建議的值為：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述2個參數已預先設定OOTB，且可透過OSGi QueryEngineSettings持續保存。

如需詳細資訊，請參閱：[https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 建立有效索引的提示{#tips-for-creating-efficient-indexes}

### 應建立索引嗎？{#should-i-create-an-index}

建立或最佳化索引時要詢問的第一個問題是，在特定情況下，這些索引是否確實是必要項目。 如果您只打算通過批處理在系統的非高峰時間運行有關查詢一次或僅運行一次，則最好不要建立索引。

建立索引後，每次更新索引資料時，也必須更新索引。 由於這會對系統產生效能影響，因此只有在實際需要索引時才應建立索引。

此外，只有索引中包含的資料足夠唯一，足以保證其安全時，索引才有用。 以一本書中的索引及其所涵蓋的主題為例。 在文本中為一組主題建立索引時，通常會有數百個或數千個條目，這允許您快速跳轉到一個頁的子集，以快速查找您要查找的資訊。 如果該索引只有兩三個條目，每個條目指向數百個頁，則該索引將不會非常有用。 這個概念同樣適用於資料庫索引。 如果只有幾個唯一值，則索引將不會非常有用。 話雖如此，一個指數也可能變得過大，無法發揮作用。 要查看索引統計資訊，請參閱上面的[索引統計資訊](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics)。

### Lucene或屬性索引？{#lucene-or-property-indexes}

Lucene索引已導入Oak 1.0.9，並針對AEM 6初次啟動時引入的屬性索引提供一些強大的最佳化。 在決定是使用Lucene索引還是屬性索引時，請考慮以下因素：

* Lucene索引提供的功能比屬性索引更多。 例如，屬性索引只能索引單一屬性，而Lucene索引可以包含許多屬性。 有關Lucene索引中所有可用功能的詳細資訊，請參閱[文檔](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。
* Lucene索引為非同步。 雖然這可大幅提升效能，但也可能在將資料寫入存放庫與更新索引之間造成延遲。 如果讓查詢傳回100%準確結果至關重要，則需要屬性索引。
* 由於為非同步，Lucene索引無法強制執行唯一性約束。 如果需要，則需要設定屬性索引。

通常，建議您使用Lucene索引，除非迫切需要使用屬性索引，這樣您就可以獲得更高效能和靈活性的好處。

### 索引{#solr-indexing}

AEM預設也支援Solr索引。 這主要用於支援全文搜尋，但也可用於支援任何類型的JCR查詢。 當AEM例項沒有CPU容量來處理搜尋密集型部署（例如同時擁有大量使用者的搜尋驅動網站）所需的查詢數時，才應考慮使用Solr。 或者，Solr可以採用基於爬蟲的方法來實現，以利用平台的一些更高級的功能。

Solr索引可配置為在AEM伺服器上嵌入用於開發環境，或可卸載到遠程實例以改進生產和測試環境上的搜索可擴充性。 雖然卸載搜索將提高可擴充性，但會導致延遲，因此除非需要，否則不建議使用。 如需如何設定Solr整合以及如何建立Solr索引的詳細資訊，請參閱[Oak Querys and Indexing說明檔案](/help/sites-deploying/queries-and-indexing.md#the-solr-index)。

>[!NOTE]
>
>採用整合的Solr搜索方法將允許將索引卸載到Solr伺服器。 如果通過基於爬蟲的方法使用Solr伺服器的更高級功能，則需要進行額外的配置工作。 Headwire已建立[開放原始碼連接器](https://www.aemsolrsearch.com/#/)以加速這些類型的實施。

採用此方法的缺點是，雖然預設情況下AEM查詢會遵守ACL，因此會隱藏使用者無法存取的結果，將搜尋外部化至Solr伺服器將不支援此功能。 如果要以此方式將搜尋外部化，則必須格外小心，以確保使用者不會看到他們不應看到的結果。

此方法可能適當的潛在使用案例是指可能需要匯總來自多個來源的搜尋資料的情況。 例如，您可能有一個網站是在AEM上托管，而第二個網站是在協力廠商平台上托管。 Solr可配置為對兩個站點的內容進行編目，並將它們儲存在聚合索引中。 這可允許跨網站搜尋。

### 設計考量事項{#design-considerations}

Lucene索引的Oak檔案列出設計索引時要考量的幾項事項：

* 如果查詢使用不同的路徑限制，請利用`evaluatePathRestrictions`。 這可讓查詢在指定的路徑下傳回結果子集，然後根據查詢篩選結果。 否則，查詢將搜索與儲存庫中的查詢參數匹配的所有結果，然後根據路徑進行篩選。
* 如果查詢使用排序，請為sorted屬性定義顯式屬性，並為其設定`ordered`到`true`。 這將允許在索引中按此順序排序結果，並在查詢執行時節省成本高昂的排序操作。

* 只把需要的東西放入索引中。 添加不需要的功能或屬性將導致索引增長並降低效能。
* 在屬性索引中，具有唯一屬性名稱有助於減小索引的大小，但對於Lucene索引，應使用`nodeTypes`和`mixins`來實現連結索引。 查詢特定`nodeType`或`mixin`將比查詢`nt:base`更具效能。 使用此方法時，請為相關的`nodeTypes`定義`indexRules`。

* 如果您的查詢僅在特定路徑下運行，則在這些路徑下建立這些索引。 索引不是存放在存放庫根目錄的必要項目。
* 建議在所有被索引的屬性都與允許Lucene以本機方式評估盡可能多的屬性限制相關時使用單個索引。 此外，即使執行聯接，查詢也只會使用一個索引。

### CopyOnRead {#copyonread}

在遠程儲存`NodeStore`時，可以啟用名為`CopyOnRead`的選項。 該選項將使遠程索引在讀取時寫入本地檔案系統。 這有助於改進經常針對這些遠程索引運行的查詢的效能。

這可在OSGi主控台的&#x200B;**LuceneIndexProvider**&#x200B;服務下進行設定，並於Oak 1.0.13時預設啟用。

### 刪除索引{#removing-indexes}

刪除索引時，始終建議將`type`屬性設定為`disabled`以臨時禁用該索引，並進行測試以確保應用程式在實際刪除該索引之前能夠正常運行。 請注意，索引在禁用時不會更新，因此如果重新啟用，則可能沒有正確的內容，並且可能需要重新編製索引。

移除TarMK例項上的屬性索引後，必須執行壓縮以回收任何使用中的磁碟空間。 對於Lucene索引，實際索引內容仍存在於BlobStore中，因此需要資料儲存垃圾收集。

刪除MongoDB實例上的索引時，刪除成本與索引中的節點數成比例。 由於刪除大型索引可能會造成問題，建議的方法是使用工具（例如&#x200B;**oak-mongo.js**），停用索引並僅在維護期間刪除該索引。 請注意，一般節點內容不應採用此方法，因為這會導致資料不一致。

>[!NOTE]
>
>如需oak-mongo.js的詳細資訊，請參閱Oak檔案的[命令列工具區段](https://jackrabbit.apache.org/oak/docs/command_line.html)。

## 重新索引{#re-indexing}

本節概述&#x200B;**only**&#x200B;重新索引Oak索引的可接受原因。

在下列說明的原因之外，起始Oak索引的重新索引將會&#x200B;**不**&#x200B;變更行為或解決問題，並無法增加AEM的負載。

請避免重新索引Oak索引，除非下表有說明。

>[!NOTE]
>
>在查看下表以確定重新索引是否有用之前，**始終**證：
>
>* 查詢正確
>* 查詢解析到預期索引（使用[Explain Query](/help/sites-administering/operations-dashboard.md#diagnosis-tools)）
>* 索引過程已完成

>



### Oak索引組態變更{#oak-index-configuration-changes}

重新索引Oak索引的唯一可接受的非回溯條件，是Oak索引的設定已變更。

*應始終對重新索引進行處理，並適當考慮其對AEM整體效能的影響，並在活動量低或維護期間執行。*

以下是可能的問題和決議：

* [屬性索引定義更改](#property-index-definition-change)
* [Lucene索引定義更改](#lucene-index-definition-change)

#### 屬性索引定義更改{#property-index-definition-change}

* 適用於/如果：

   * 所有Oak版本
   * 僅[屬性索引](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* 症狀：

   * 屬性索引定義更新之前存在的節點在結果中缺失

* 如何驗證：

   * 確定是否在部署更新的索引定義之前建立/修改了丟失的節點。
   * 根據索引的修改時間驗證任何缺失節點的`jcr:created`或`jcr:lastModified`屬性

* 如何解決：

   * [重新索](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) 引lucene指數
   * 或者，對缺少的節點進行觸摸（執行良性寫入操作）

      * 需要手動接觸或自訂程式碼
      * 需要知道缺少的節點集
      * 需要更改節點上的任何屬性

#### Lucene索引定義更改{#lucene-index-definition-change}

* 適用於/如果：

   * 所有Oak版本
   * 僅[lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症狀：

   * Lucene索引不包含預期結果
   * 查詢結果未反映索引定義的預期行為
   * 查詢計畫不根據索引定義報告預期輸出

* 如何驗證：

   * 使用Lucene索引統計資訊JMX Mbean(LuceneIndex)，方法`diffStoredIndexDefinition`驗證索引定義是否已更改。

* 如何解決：

   * Oak 1.6之前的版本：

      * [重新索](#how-to-re-index) 引lucene指數
   * Oak 1.6+版

      * 如果現有內容不受變更影響，則只需要重新整理

         * [](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) 設定oak:queryIndexDefinition []@refresh=true，以重新整理lucene索引
      * 否則，[重新索引](#how-to-re-index)lucene索引

         * 注意：將使用上次正確重新索引（或初始索引）的索引狀態，直到觸發新的重新索引



### 錯誤和異常情況{#erring-and-exceptional-situations}

下表說明唯一可接受的錯誤，以及重新索引Oak索引以解決問題的例外情況。

如果AEM上發生不符合下列標準的問題，請執行&#x200B;**not**&#x200B;重新索引任何索引，因為這無法解決問題。

以下是可能的問題和決議：

* [缺少Lucene索引二進位](#lucene-index-binary-is-missing)
* [Lucene索引二進位檔損壞](#lucene-index-binary-is-corrupt)

#### 缺少Lucene索引二進位{#lucene-index-binary-is-missing}

* 適用於/如果：

   * 所有Oak版本
   * 僅[lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症狀：

   * Lucene索引不包含預期結果

* 如何驗證：

   * 錯誤日誌檔案包含異常，表示缺少Lucene索引的二進位

* 如何解決：

   * 執行遍歷儲存庫檢查；例如：

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      遍歷儲存庫可確定是否缺少其他二進位檔案（lucene檔案除外）

   * 如果缺少lucene索引以外的二進位檔，請從備份中還原
   * 否則，[re-index](#how-to-re-index) *all* lucene索引
   * 注意:

      此條件表示未配置的資料存放區可能導致任何二進位(例如 資產二進位檔)遺失。

      在此情況下，請還原到上一個已知良好的儲存庫版本，以恢復所有遺失的二進位檔。

#### Lucene索引二進位檔損壞{#lucene-index-binary-is-corrupt}

* 適用於/如果：

   * 所有Oak版本
   * 僅[lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症狀：

   * Lucene索引不包含預期結果

* 如何驗證：

   * `AsyncIndexUpdate`（每5秒）會失敗，error.log中出現例外：

      `...a Lucene index file is corrupt...`

* 如何解決：

   * 刪除lucene索引的本地副本

      1. 停止AEM
      1. 在`crx-quickstart/repository/index`刪除lucene索引的本地副本
      1. 重新啟動AEM
   * 如果這無法解決問題，且`AsyncIndexUpdate`例外仍會持續存在：

      1. [重新索](#how-to-re-index) 引錯誤索引
      1. 還要提交[Adobe支援](https://helpx.adobe.com/support.html)票證


### 如何重新索引{#how-to-re-index}

>[!NOTE]
>
>在AEM 6.5中，[oak-run.jar是唯一支援在MongoMK或RDBMK存放庫上重新索引的方法](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree)。

#### 重新索引屬性索引{#re-indexing-property-indexes}

* 使用[oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing)重新索引屬性索引
* 在屬性索引上將async-reindex屬性設為true

   * `[oak:queryIndexDefinition]@reindex-async=true`

* 使用Web控制台通過&#x200B;**PropertyIndexAsyncReindex** MBean，以非同步方式重新索引屬性索引；

   例如，

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### 重新索引Lucene屬性索引{#re-indexing-lucene-property-indexes}

* 使用[oak-run.jar重新索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) Lucene屬性索引。
* 在lucene屬性索引上將async-reindex屬性設為true

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>前一節會在AEM內容中，從[Apache Oak檔案](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)摘要並建構Oak重新索引指引。

### 二進位檔的文字預先擷取{#text-pre-extraction-of-binaries}

文字預先擷取是指從二進位檔擷取及處理文字的程式，透過隔離的程式直接從資料存放區擷取，並直接將擷取的文字顯示於後續的Oak索引重新/索引中。

* 建議使用Oak文字預先擷取，在具有大量包含可擷取文字之檔案（二進位檔）的存放庫上重新/索引Lucene索引(例如 PDF、Word檔案、PPT、TXT等) 可透過部署的Oak索引進行全文搜尋；例如`/oak:index/damAssetLucene`。
* 文字預先擷取功能只能讓Lucene索引的重新/索引，以及NOT Oak屬性索引更有利，因為屬性索引不會從二進位檔擷取文字。
* 文字預先擷取對重複索引大量文字的二進位檔（PDF、Doc、TXT等）會產生很大正面影響，因為影像不包含可擷取的文字，因此作為影像存放庫的影像效率不會相同。
* 文字預先擷取會以非常有效率的方式執行全文搜尋相關文字的擷取，並以非常有效率的方式將其公開至Oak重新索引程式，供使用者使用。

#### 何時可以使用文字預先擷取？{#when-can-text-pre-extraction-be-used}

重新索引&#x200B;**existing** lucene索引，並啟用二進位擷取

* 重新索引儲存庫中的&#x200B;**all**&#x200B;候選內容；從中擷取全文的二進位檔數量眾多或複雜時，AEM會增加執行全文擷取的運算負擔。 文本預提取將文本提取的「計算成本高的工作」移動到直接訪問AEM資料儲存的隔離進程中，避免了AEM中的開銷和資源爭用。

支援將&#x200B;**new** lucene索引部署至已啟用二進位擷取的AEM

* 將新索引（已啟用二進位擷取）部署至AEM時，Oak會在下次執行非同步全文索引時，自動為所有候選內容建立索引。 基於上述重新索引中所述的相同原因，這可能會導致AEM負載過重。

#### 何時可以不使用文字預先擷取？{#when-can-text-pre-extraction-not-be-used}

文字預先擷取無法用於新增至存放庫的新內容，也不是必要功能。

新內容會自然地新增至存放庫，並依非同步全文索引程式（預設為每5秒）逐步建立索引。

在AEM的一般操作下（例如透過網頁UI上傳資產或以程式化方式擷取資產）,AEM會自動以逐步方式將新二進位內容的全文索引編入新索引。 由於資料量是增量的，而且相對較小（大約可以在5秒內保存到儲存庫的資料量）,AEM可以在索引期間從二進位檔執行全文提取，而不會影響整體系統效能。

#### 使用文字預先擷取{#prerequisites-to-using-text-pre-extraction}的必要條件

* 您將重新索引執行全文二進位擷取的lucene索引，或部署新索引，將現有內容的全文索引二進位檔
* 要預先擷取文字的內容（二進位檔）必須位於存放庫中
* 一個維護窗口，用於生成CSV檔案AND以執行最終的重新索引
* Oak版本：1.0.18+、1.2.3+
* [oak-run.](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)jarversion 1.7.4+
* 檔案系統資料夾/共用，用於儲存可從索引AEM實例訪問的提取文本

   * 文本預提取OSGi配置需要到提取的文本檔案的檔案系統路徑，因此必須直接從AEM實例（本地驅動器或檔案共用裝載）訪問這些檔案

#### 如何執行文字預先擷取{#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***以下概述的oak-run.jar命令可在https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html上完整列 [舉](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>上圖和下列步驟可說明並補充Apache Oak檔案中概述的技術文字預先擷取步驟。

![文本預提取流程](assets/chlimage_1-139.png)

**產生要預先擷取的內容清單**

*在維護窗口/低使用期間執行步驟1(a-b)，因為在此操作期間遍歷節點儲存，這可能會對系統造成大量負載。*

1a。 執行`oak-run.jar --generate`以建立預先擷取其文字的節點清單。

1b. 節點清單(1a)以CSV檔案形式儲存到檔案系統

請注意，每次執行`--generate`時，都會遍歷整個Node Store（如oak-run命令中的路徑所指定），並建立&#x200B;**new** CSV檔案。 CSV檔案為&#x200B;**not**，會在文字預先擷取程式的離散執行之間重複使用（步驟1 - 2）。

**預先將文本解壓到檔案系統**

*步驟2(a-c)只會與資料存放區互動，才能在AEM正常運作期間執行。*

2a。 執行`oak-run.jar --tika`以預先擷取(1b)中產生之CSV檔案中列舉之二進位節點的文字

2b。 在(2a)中啟動的程式可直接存取在資料存放區的CSV中定義的二進位節點，並擷取文字。

2c。  擷取的文字會以Oak重新索引程式(3a)可擷取的格式儲存在檔案系統上

預先擷取的文字會以二進位指紋在CSV中識別。 如果二進位檔案相同，則可在AEM例項間使用相同的預先擷取文字。 由於AEM Publish通常是AEM Author的子集，因此從AEM Author預先擷取的文字通常也可用來重新索引AEM Publish（假設AEM Publish有檔案系統存取已擷取的文字檔）。

預先擷取的文字可逐步新增至一段時間。 文字預先擷取將略過先前擷取之二進位檔的擷取，因此最好保留預先擷取的文字，以備日後必須重新索引時使用（假設擷取的內容不會過大）。 如果是，請評估在中間壓縮內容，因為文本壓縮效果很好)。

**重新索引Oak索引，從擷取的文字檔案取得全文**

*在維護/低使用期間執行重新索引（步驟3a-b），因為在此操作期間遍歷節點儲存，這可能會對系統造成重大負載。*

3a。 [在AEM中](#how-to-re-index) 調用Lucene索引的重新索引

3b. Apache Jackrabbit Oak DataStore PreExtractedTextProvider OSGi設定（設定為透過檔案系統路徑指向擷取的文字）指示Oak從擷取的檔案中取得全文，並避免直接點擊和處理儲存在存放庫中的資料。
