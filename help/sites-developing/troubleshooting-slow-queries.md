---
title: 疑難排解慢速查詢
seo-title: 疑難排解慢速查詢
description: 'null'
seo-description: 'null'
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 疑難排解慢速查詢{#troubleshooting-slow-queries}

## 慢速查詢分類 {#slow-query-classifications}

AEM中有3種主要的慢速查詢分類，依嚴重性列出：

1. **無索引查詢**

   * 不解析 **為索引** ，並遍歷JCR內容以收集結果的查詢

1. **限制不嚴（或範圍不廣）的查詢**

   * 解析為索引，但必須遍歷所有索引條目才能收集結果的查詢

1. **大型結果集查詢**

   * 傳回大量結果的查詢

前2個查詢分類（無索引且限制不佳）的速度較慢，因為它們會強制Oak查詢引擎檢查每個潛在結果 **（內容節點或索引項目），以識別屬於實際結果集的** 結果 **** 。

每個潛在結果的檢查操作稱為遍歷。

由於每個勢結果都必須被檢查，因此確定實際結果集的成本隨勢結果的數目線性增加。

添加查詢限制和調整索引允許以優化格式儲存索引資料，從而提供快速的結果檢索，並且減少或消除了對潛在結果集的線性檢查的需要。

在AEM 6.3中，預設情況下，當到達100,000的遍歷時，查詢會失敗並引發例外。 AEM 6.3之前的AEM版本中預設不存在此限制，但可透過Apache Jackrabbit查詢引擎設定OSGi組態和QueryEngineSettings JMX Bean（屬性LimitReads）來設定。

### 檢測無索引查詢 {#detecting-index-less-queries}

#### 開發期間 {#during-development}

解 **釋所有** ，並確保其查詢計畫不包含 **/&amp;ast;在它們中** ，遍歷解釋。 遍歷查詢計畫示例：

* **** 計畫： `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### 部署後 {#post-deployment}

* 監控無 `error.log` 索引遍歷查詢：

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 僅當沒有可用索引且查詢可能遍歷許多節點時，才會記錄此消息。 如果索引可用，則不記錄消息，但遍歷的量很小，因此速度很快。

* 請造訪AEM [Query Performance](/help/sites-administering/operations-dashboard.md#query-performance) operations主控台和 [Explain](/help/sites-administering/operations-dashboard.md#explain-query) slow queries，尋找遍歷或無索引查詢解釋。

### 檢測受限查詢 {#detecting-poorly-restricted-queries}

#### 開發期間 {#during-development-1}

解釋所有查詢，並確保它們解析為已調整為與查詢的屬性限制匹配的索引。

* 理想的查詢計畫涵蓋 `indexRules` 範圍適用於所有屬性限制，至少適用於查詢中緊密的屬性限制。
* 對結果排序的查詢應解析為Lucene屬性索引，該索引具有按設定的屬性排序的索引規則 `orderable=true.`

#### 例如，預設 `cqPageLucene``jcr:content/cq:tags` 的索引規則不適用於 {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

新增cq:tags索引規則之前

* **cq：標籤索引規則**

   * 不存在現成可用的

* **查詢建立工具查詢**

   * 
      ```
      type=cq:Page
       property=jcr:content/cq:tags
       property.value=my:tag
      ```

* **查詢計畫**

   * `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

此查詢解析為索 `cqPageLucene` 引，但由於沒有屬性索引規則 `jcr:content` 或 `cq:tags``cqPageLucene` ，因此在評估此限制時，會檢查索引中的每個記錄以確定匹配。 這表示如果索引包含100萬個節 `cq:Page` 點，則檢查100萬條記錄以確定結果集。

新增cq:tags索引規則後

* **cq：標籤索引規則**

   * 
      ```
      /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
       @name=jcr:content/cq:tags
       @propertyIndex=true
      ```

* **查詢建立工具查詢**

   * 
      ```
      type=cq:Page
       property=jcr:content/cq:tags
       property.value=myTagNamespace:myTag
      ```

* **查詢計畫**

   * `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

在索引中加入indexRule `jcr:content/cq:tags` 可讓 `cqPageLucene` 以最 `cq:tags` 佳化的方式儲存資料。

當執行具有限制 `jcr:content/cq:tags` 的查詢時，索引可以按值查找結果。 這表示如果100個 `cq:Page` 節點有 `myTagNamespace:myTag` 值，則只會傳回100個結果，而其他999,000則會從限制檢查中排除，將效能提升10,000倍。

當然，進一步的查詢限制會減少符合條件的結果集，並進一步優化查詢優化。

同樣地，如果沒有屬性的其他索引規則， `cq:tags` 即使是具有限制的全文查詢，其執行效 `cq:tags` 果也會不佳，因為來自索引的結果會傳回所有全文相符項目。 cq:tags的限制會在之後加以篩選。

索引後篩選的另一個原因是在開發期間經常遺漏的存取控制清單。 請嘗試確定查詢未傳回使用者可能無法存取的路徑。 這通常可以通過更好的內容結構以及對查詢提供相關路徑限制來實現。

要識別Lucene索引是否返回大量結果以作為查詢結果返回很小的子集，一個有用的方法是啟用DEBUG日誌 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` ，並查看從索引中載入的文檔數。 結果與載入檔案的數量之間不應不成比例。 如需詳細資訊，請參 [閱記錄](/help/sites-deploying/configure-logging.md)。

#### 部署後 {#post-deployment-1}

* 監視遍歷 `error.log` 查詢的情況：

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* 請造訪AEM [Query Performance](/help/sites-administering/operations-dashboard.md#query-performance) operations主控台和 [Explain](/help/sites-administering/operations-dashboard.md#explain-query) slow queries，尋找查詢計畫，以尋找不會將查詢屬性限制解析為索引屬性規則的查詢計畫。

### 檢測大結果集查詢 {#detecting-large-result-set-queries}

#### 開發期間 {#during-development-2}

為oak.queryLimitInMemory設定低臨界值(例如 10000)和oak.queryLimitReads(例如 5000)，並最佳化當點擊「查詢讀取的節點數超過x個……」的UnsupportedOperationException時，昂貴的查詢。

這有助於避免資源密集型查詢(即 不受任何索引的支援，或受較少覆蓋指數的支援)。 例如，讀取1M個節點的查詢會導致大量的IO，並對整體應用程式效能產生負面影響。 因此，任何因上述限制而失敗的查詢都應加以分析和優化。

#### 部署後 {#post-deployment-2}

* 監視日誌中觸發大節點遍歷或大堆記憶體消耗的查詢：&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 優化查詢以減少遍歷的節點數

* 監視日誌中觸發大量堆記憶體消耗的查詢：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 優化查詢以減少堆記憶體消耗

對於AEM 6.0 - 6.2版本，您可以在AEM啟動指令碼中調整透過JVM參數的節點周遊臨界值，以防止大型查詢超出環境負載。 建議的值為：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述2個參數預設已預先設定，並可透過OSGi queryEngineSettings加以修改。

以下網址提供更多資訊： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 查詢效能優化 {#query-performance-tuning}

AEM中查詢效能優化的格言是：

**「限制越多越好。」**

以下概述建議的調整以確保查詢效能。 首先調整查詢（較不顯眼的活動），然後視需要調整索引定義。

### 調整查詢語句 {#adjusting-the-query-statement}

AEM支援下列查詢語言：

* 查詢產生器
* JCR-SQL2
* XPath

下列範例使用Query Builder，因為它是AEM開發人員最常用的查詢語言，但JCR-SQL2和XPath也適用相同的原則。

1. 新增nodetype限制，讓查詢解析至現有的Lucene屬性索引。

   * **未最佳化查詢**

      * 
         ```
          property=jcr:content/contentType
          property.value=article-page
         ```
   * **最佳化查詢**

      * 
         ```
          type=cq:Page
          property=jcr:content/contentType
          property.value=article-page
         ```
   缺乏nodetype限制的查詢會強制AEM假設nodetype，而 `nt:base` AEM中的每個節點都是nodetype的子類型，有效地產生nodetype限制。

   設定 `type=cq:Page` 會限制此查詢僅限 `cq:Page` 節點，並將查詢解析為AEM的cqPageLucene，並將結果限制為AEM中的節點子集(僅 `cq:Page` 節點)。

1. 調整查詢的nodetype限制，使查詢解析為現有的Lucene屬性索引。

   * **未最佳化查詢**

      * 
         ```
         type=nt:hierarchyNode
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **最佳化查詢**

      * 
         ```
         type=cq:Page
         property=jcr:content/contentType
         property.value=article-page
         ```
   `nt:hierarchyNode` 是的父節點類 `cq:Page`型，且假設 `jcr:content/contentType=article-page` 僅透過我們的自訂應 `cq:Page` 用程式套用至節點，此查詢只會傳回節點 `cq:Page` 的位置 `jcr:content/contentType=article-page`。 不過，這是次優的限制，因為：

   * 其他節點繼承 `nt:hierarchyNode` 自(如 `dam:Asset`)不必要地新增至一組潛在結果。
   * AEM提供的索引不存在 `nt:hierarchyNode`，但提供的索引 `cq:Page`。
   設定 `type=cq:Page` 會限制此查詢僅限 `cq:Page` 節點，並將查詢解析為AEM的cqPageLucene，並將結果限制為AEM中的節點子集（僅cq:Page節點）。

1. 或者，調整屬性限制，使查詢解析為現有的屬性索引。

   * **未最佳化查詢**

      * 
         ```
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **最佳化查詢**

      * 
         ```
         property=jcr:content/sling:resourceType
         property.value=my-site/components/structure/article-page
         ```
   將屬性限制從 `jcr:content/contentType` （自訂值）變更為已知屬性 `sling:resourceType` ，可讓查詢解析為屬性索引，以 `slingResourceType` 依此索引所有內容 `sling:resourceType`。

   當查詢不由nodetype識別，而結果集中以單一屬性限制時，最好使用屬性索引（與Lucene屬性索引相反）。

1. 將最緊密的路徑限制添加到查詢。 例如，偏好 `/content/my-site/us/en` 勝 `/content/my-site`過或 `/content/dam` 過去 `/`。

   * **未最佳化查詢**

      * 
         ```
         type=cq:Page
         path=/content
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **最佳化查詢**

      * 
         ```
         type=cq:Page
         path=/content/my-site/us/en
         property=jcr:content/contentType
         property.value=article-page
         ```
   將路徑限制範圍 `path=/content`從 `path=/content/my-site/us/en` 到允許索引減少需要檢查的索引條目數。 當查詢可以很好地限制路徑時，除了或 `/content` 以外 `/content/dam`，請確保索引已包含 `evaluatePathRestrictions=true`。

   請注意，使 `evaluatePathRestrictions` 用會增加索引大小。

1. 盡可能避免查詢函式／操作查詢：隨 `LIKE` 著成 `fn:XXXX` 本的增加，成本會隨著限制結果的增加而增加。

   * **未最佳化查詢**

      * 
         ```
         type=cq:Page
         property=jcr:content/contentType
         property.operation=like
         property.value=%article%
         ```
   * **最佳化查詢**

      * 
         ```
         type=cq:Page
         fulltext=article
         fulltext.relPath=jcr:content/contentType
         ```
   LIKE條件評估速度緩慢，因為如果文本以通配符(&quot;%。..&quot;)開頭，則不能使用索引。 jcr:contains條件允許使用全文索引，因此是首選條件。 這要求已解析的Lucene屬性索引具有的indexRule `jcr:content/contentType` 與 `analayzed=true`。

   使用查詢函式( `fn:lowercase(..)` 例如)可能較難進行最佳化，因為沒有更快的等效功能（在更複雜且更顯眼的索引分析器組態外）。 最好找出其他範圍界定限制，以改善整體查詢效能，要求函式在盡可能小的潛在結果集上運作。

1. ***此調整是Query builder專用，不適用於JCR-SQL2或XPath。***

   當完 [](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) 整結果集為**不是立即需要**時，請使用Query Builder的guessTotal。

   * **未最佳化查詢**

      * 
         ```
         type=cq:Page
         path=/content
         ```
   * **最佳化查詢**

      * 
         ```
         type=cq:Page
         path=/content
         p.guessTotal=100
         ```
   對於查詢執行速度快但結果數量大的情況，p. `guessTotal` 是Query Builder查詢的關鍵優化。

   `p.guessTotal=100` 告訴Query builder僅收集前100個結果，並設定布林值標幟，指出是否至少存在一個結果（但不包含多少個結果），因為計算此數字會導致速度變慢。 此最佳化優於分頁或無限載入使用案例，其中只會逐步顯示結果子集。

## 現有索引調整 {#existing-index-tuning}

1. 如果最佳查詢解析為屬性索引，則沒有其他可做的，因為屬性索引可進行最小調整。
1. 否則，查詢應解析為Lucene屬性索引。 如果無法解析索引，請跳至「建立新索引」。
1. 視需要將查詢轉換為XPath或JCR-SQL2。

   * **查詢建立工具查詢**

      * 
         ```
         query type=cq:Page
         path=/content/my-site/us/en
         property=jcr:content/contentType
         property.value=article-page
         orderby=@jcr:content/publishDate
         orderby.sort=desc
         ```
   * **XPath從Query Builder查詢產生**

      * 
         ```
         /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
         ```


1. 將XPath（或JCR-SQL2）提供給 [Oak Index Definition Generator](https://oakutils.appspot.com/generate/index) ，以產生最佳化的Lucene屬性索引定義。

   **生成的Lucene屬性索引定義**

   ```xml
   - evaluatePathRestrictions = true
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + cq:Page
           + properties
           + contentType
               - name = "jcr:content/contentType"
               - propertyIndex = true
           + publishDate
               - ordered = true
               - name = "jcr:content/publishDate"
   ```

1. 以加法方式手動將生成的定義合併到現有的Lucene屬性索引中。 請小心不要刪除現有配置，因為它們可能用於滿足其他查詢。

   1. 找到涵蓋cq:Page（使用索引管理器）的現有Lucene屬性索引。 在這個例子中， `/oak:index/cqPageLucene`.
   1. 識別最佳化索引定義（步驟4）和現有索引(/oak:index/cqPageLucene)之間的組態增量，並將最佳化索引中遺失的組態新增至現有的索引定義。
   1. 根據AEM的「重新索引最佳實務」，重新整理或重新索引的順序是正確的，這取決於現有內容是否會受到此索引設定變更的影響。

## 建立新索引 {#create-a-new-index}

1. 驗證查詢未解析為現有的Lucene屬性索引。 如果有，請參閱上節中有關優化和現有索引的說明。
1. 視需要將查詢轉換為XPath或JCR-SQL2。

   * **查詢建立工具查詢**

      * 
         ```
         type=myApp:Author
         property=firstName
         property.value=ira
         ```
   * **XPath從Query Builder查詢產生**

      * 
         ```
         //element(*, myApp:Page)[@firstName = 'ira']
         ```


1. 將XPath（或JCR-SQL2）提供給 [Oak Index Definition Generator](https://oakutils.appspot.com/generate/index) ，以產生最佳化的Lucene屬性索引定義。

   **生成的Lucene屬性索引定義**

   ```xml
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + myApp:AuthorModel
           + properties
           + firstName
               - name = "firstName"
               - propertyIndex = true
   ```

1. 部署生成的Lucene屬性索引定義。

   將Oak Index Definition Generator針對新索引提供的XML定義新增至管理Oak索引定義的AEM專案（請記住，請將Oak索引定義視為程式碼，因為程式碼會視其而定）。

   在AEM軟體開發常規生命週期後，部署並測試新索引，並驗證查詢解析為索引且查詢是效能。

   在初次部署此索引時，AEM會將必要資料填入索引。

## 無索引查詢和遍歷查詢何時可以？ {#when-index-less-and-traversal-queries-are-ok}

由於AEM有彈性的內容架構，因此很難預測並確保內容結構的遍歷性不會隨著時間而演化為無法接受的大小。

因此，確保索引滿足查詢，除非路徑限制和節點類型限制的組合保證 **少於20個節點被遍歷。**

## 查詢開發工具 {#query-development-tools}

### Adobe支援 {#adobe-supported}

* **Query Builder除錯程式**

   * WebUI，用於執行查詢產生器查詢並產生支援的XPath（用於Explain Query或Oak Index Definition Generator）。
   * 位於AEM，網址為 [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite —— 查詢工具**

   * 用於執行XPath和JCR-SQL2查詢的WebUI。
   * 位於AEM的 [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) >工具>查詢……

* **[說明查詢](/help/sites-administering/operations-dashboard.md#explain-query)**

   * AEM Operations控制面板，提供任何指定XPATH或JCR-SQL2查詢的詳細說明（查詢計畫、查詢時間和結果數）。

* **[慢速／熱門查詢](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM Operations控制面板會列出在AEM上執行的最近緩慢和常用查詢。

* **[索引管理員](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * 顯示AEM例項索引的AEM Operations webUI;有助於瞭解哪些索引已存在，可以定位或擴展。

* **[記錄](/help/sites-administering/operations-dashboard.md#log-messages)**

   * 查詢產生器記錄

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak查詢執行記錄

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit查詢引擎設定OSGi Config**

   * OSGi配置，用於配置遍歷查詢的故障行為。
   * 位於AEM的 [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * JMX MBean用於估計AEM中內容樹中的節點數。
   * 位於AEM的 [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### 社群支援 {#community-supported}

* **[Oak Index Definition Generator](https://oakutils.appspot.com/generate/index)**

   * 從XPath或JCR-SQL2查詢語句生成最佳Lucence屬性索引。

* **[AEM Chrome增效模組](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Google Chrome網頁瀏覽器擴充功能，可在瀏覽器的開發工具主控台中公開每個請求記錄檔資料，包括已執行的查詢及其查詢計畫。
   * 需要 [在AEM上安裝並啟用Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) 。

