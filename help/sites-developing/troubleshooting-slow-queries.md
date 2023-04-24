---
title: 疑難排解慢速查詢
seo-title: Troubleshooting Slow Queries
description: 疑難排解慢速查詢
seo-description: null
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
source-git-commit: a296e459461973fc2dbd0641c6fdda1d89d8d524
workflow-type: tm+mt
source-wordcount: '2262'
ht-degree: 0%

---

# 疑難排解慢速查詢{#troubleshooting-slow-queries}

## 查詢分類速度緩慢 {#slow-query-classifications}

AEM中有三個主要的慢速查詢分類，依嚴重性列出：

1. **無索引查詢**

   * 查詢 **not** 解析為索引並遍歷JCR的內容以收集結果

1. **限制不足（或限定範圍）的查詢**

   * 解析為索引的查詢，但必須遍歷所有索引條目以收集結果

1. **大型結果集查詢**

   * 返回大量結果的查詢

前兩個查詢分類（無索引和限制不足）的速度很慢。 速度緩慢，因為會強制Oak查詢引擎檢查每個 **潛在** 結果（內容節點或索引條目），以標識屬於 **實際** 結果集。

檢查每個潛在結果的行為稱為「遍歷」。

由於必須檢查每個潛在結果，因此確定實際結果集的成本與電位結果的數目呈線性增長。

添加查詢限制和調整索引允許以優化格式儲存索引資料，提供快速結果檢索，並且減少或消除對潛在結果集的線性檢查的需要。

在AEM 6.3中，依預設，當到達100,000的周遊時，查詢會失敗並擲回例外狀況。 AEM 6.3之前的AEM版本預設不存在此限制，但可透過Apache Jackrabbit查詢引擎設定OSGi設定和QueryEngineSettings JMX Bean（屬性LimitReads）設定。

### 檢測無索引查詢 {#detecting-index-less-queries}

#### 開發期間 {#during-development}

說明 **all** 查詢，並確保其查詢計畫不包含 **/&amp;ast;橫貫** 解釋。 遍歷查詢計畫的示例：

* **計畫：** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### 部署後 {#post-deployment}

* 監視 `error.log` 對於無索引遍歷查詢：

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 只有在沒有可用索引且查詢可能遍歷許多節點時，才會記錄此消息。 如果索引可用，則不會記錄消息，但遍歷的量很小，因此速度很快。

* 造訪AEM [查詢效能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制台和 [說明](/help/sites-administering/operations-dashboard.md#explain-query) 查詢查找遍歷或沒有索引查詢解釋的速度較慢。

### 檢測限制不良的查詢 {#detecting-poorly-restricted-queries}

#### 開發期間 {#during-development-1}

說明所有查詢，並確保它們解析為符合查詢屬性限制的調整索引。

* 理想的查詢計畫覆蓋範圍 `indexRules` ，並且至少對於查詢中最緊的屬性限制。
* 對排序結果進行查詢時，應解析為具有按設定的屬性排序的索引規則的Lucene屬性索引 `orderable=true.`

#### 例如，預設 `cqPageLucene` 沒有的索引規則 `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

新增cq:tags索引規則之前

* **cq:tags索引規則**

   * 不存在

* **查詢產生器查詢**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **查詢計畫**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

此查詢解析到 `cqPageLucene` 索引，但因為沒有屬性索引規則 `jcr:content` 或 `cq:tags`，在評估此限制時， `cqPageLucene` 檢查索引以確定匹配項。 因此，如果指數包含100萬 `cq:Page` 然後檢查100萬條記錄以確定結果集。

新增cq:tags索引規則後

* **cq:tags索引規則**

   ```js
   /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
   @name=jcr:content/cq:tags
   @propertyIndex=true
   ```

* **查詢產生器查詢**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=myTagNamespace:myTag
   ```

* **查詢計畫**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

為 `jcr:content/cq:tags` 在 `cqPageLucene` 索引允許 `cq:tags` 以最佳方式儲存的資料。

若查詢包含 `jcr:content/cq:tags` 執行限制時，索引可依值查詢結果。 這意味著如果100 `cq:Page` 節點 `myTagNamespace:myTag` 作為值，僅返回這100個結果，而其他999,000則從限制檢查中排除，使效能提高10,000倍。

更多查詢限制會減少符合條件的結果集，並進一步最佳化查詢最佳化。

同樣地，沒有 `cq:tags` 屬性，甚至具有 `cq:tags` 執行效果不佳，因為索引的結果會傳回所有全文相符項目。 cq:tags上的限制會在之後篩選。

索引後篩選的另一個原因是存取控制清單，在開發期間經常會遺漏。 嘗試確定查詢未返回用戶可能無法訪問的路徑。 這樣可以通過更好的內容結構以及對查詢提供相關的路徑限制來完成。

要識別Lucene索引是否傳回許多結果以傳回小子集作為查詢結果，有一種很實用的方法是為 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. 這樣可讓您查看從索引中載入的文檔數。 最終結果的數量與載入的文檔的數量之間不應不成比例。 如需詳細資訊，請參閱 [記錄](/help/sites-deploying/configure-logging.md).

#### 部署後 {#post-deployment-1}

* 監視 `error.log` 對於遍歷查詢：

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* 造訪AEM [查詢效能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制台和 [說明](/help/sites-administering/operations-dashboard.md#explain-query) 查詢查找查詢計畫時速度緩慢，無法將查詢屬性限制解析為索引屬性規則。

### 檢測大型結果集查詢 {#detecting-large-result-set-queries}

#### 開發期間 {#during-development-2}

為oak.queryLimitInMemory(如10000)和oak.queryLimitReads（如5000）設定低臨界值，並在點擊「查詢讀取的節點數超過x個」的UnsupportedOperationException時，最佳化昂貴的查詢。

設定低閾值有助於避免資源密集型查詢（即不由任何索引支援，或由覆蓋範圍較小的索引支援）。 例如，讀取100萬個節點的查詢將導致大量IO，並對整體應用程式效能產生負面影響。 因此，任何因上述限制而失敗的查詢都應加以分析和最佳化。

#### 部署後 {#post-deployment-2}

* 監視日誌中是否有觸發大節點遍歷或大堆記憶體消耗的查詢：&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 優化查詢，以減少已遍歷的節點數。

* 監視日誌中觸發大堆記憶體消耗的查詢：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 優化查詢，以減少堆記憶體消耗。

對於AEM 6.0 - 6.2版，您可以透過AEM啟動指令碼中的JVM參數來調整節點周遊臨界值，以防止大型查詢超出環境負載。 建議的值為：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述兩個參數預設已預先設定，並可透過OSGi QueryEngineSettings修改。

如需詳細資訊，請參閱： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 查詢效能調整 {#query-performance-tuning}

AEM中查詢效能最佳化的格言為：

**「限制越多越好。」**

以下概述了為確保查詢效能而建議的調整。 首先調整查詢（不那麼引人注目的活動），然後根據需要調整索引定義。

### 調整查詢語句 {#adjusting-the-query-statement}

AEM支援下列查詢語言：

* 查詢產生器
* JCR-SQL2
* XPath

下列範例使用查詢產生器，因為這是AEM開發人員最常使用的查詢語言，但JCR-SQL2和XPath也適用相同的原則。

1. 添加nodetype限制，使查詢解析到現有Lucene屬性索引。

* **未優化的查詢**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **最佳化查詢**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   缺少nodetype限制的查詢會強制AEM採用 `nt:base` nodetype,AEM中的每個節點都是的子類型，因此有效地沒有nodetype限制。

   設定 `type=cq:Page` 僅限此查詢 `cq:Page` 節點，並將查詢解析為AEM cqPageLucene，將結果限制為節點子集(僅限於 `cq:Page` 節點)。

1. 調整查詢的nodetype限制，使查詢解析為現有Lucene屬性索引。

* **未優化的查詢**

   ```js
   type=nt:hierarchyNode
   property=jcr:content/contentType
   property.value=article-page
   ```

* **最佳化查詢**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   `nt:hierarchyNode` 是的父節點類型 `cq:Page`. 假設 `jcr:content/contentType=article-page` 僅套用至 `cq:Page` 節點(通過Adobe的自定義應用程式)，此查詢只返回 `cq:Page` 節點 `jcr:content/contentType=article-page`. 此流量是次優限制，因為：

   * 其他節點繼承自 `nt:hierarchyNode` (例如， `dam:Asset`)會不必要地新增至可能的結果集。
   * 沒有AEM提供的索引 `nt:hierarchyNode`，但由於 `cq:Page`.
   設定 `type=cq:Page` 僅限此查詢 `cq:Page` 節點，並將查詢解析為AEM cqPageLucene，將結果限制為AEM中的節點子集（僅cq:Page節點）。

1. 或者，調整屬性限制，使查詢解析為現有屬性索引。

* **未優化的查詢**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **最佳化查詢**

   ```js
   property=jcr:content/sling:resourceType
   property.value=my-site/components/structure/article-page
   ```

   將屬性限制從 `jcr:content/contentType` （自訂值）至已知屬性 `sling:resourceType` 可讓查詢解析為屬性索引 `slingResourceType` 對所有內容進行索引 `sling:resourceType`.

   當查詢不能通過nodetype進行辨識，並且單個屬性限制主導結果集時，最好使用屬性索引（與Lucene屬性索引相對）。

1. 將最緊的路徑限制添加到查詢。 例如，偏好 `/content/my-site/us/en` over `/content/my-site`，或 `/content/dam` over `/`.

* **未優化的查詢**

   ```js
   type=cq:Page
   path=/content
   property=jcr:content/contentType
   property.value=article-page
   ```

* **最佳化查詢**

   ```js
   type=cq:Page
   path=/content/my-site/us/en
   property=jcr:content/contentType
   property.value=article-page
   ```

   將路徑限制範圍從 `path=/content`to `path=/content/my-site/us/en` 允許索引減少必須檢查的索引條目數。 當查詢可以很好地限制路徑時，除了 `/content` 或 `/content/dam`，確保索引具有 `evaluatePathRestrictions=true`.

   附註使用 `evaluatePathRestrictions` 增加索引大小。

1. 盡可能避免查詢函式和查詢操作，例如： `LIKE` 和 `fn:XXXX` 因為其成本隨著限制結果的數量而增加。

* **未優化的查詢**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.operation=like
   property.value=%article%
   ```

* **最佳化查詢**

   ```js
   type=cq:Page
   fulltext=article
   fulltext.relPath=jcr:content/contentType
   ```

   LIKE條件評估速度緩慢，因為如果文字以萬用字元(&quot;%。..&#39;)開頭，則無法使用索引。 jcr:contains條件允許使用全文索引，因此是推薦條件。 它要求解析的Lucene屬性索引具有的indexRule `jcr:content/contentType` with `analayzed=true`.

   使用查詢函式，如 `fn:lowercase(..)` 可能更難進行優化，因為沒有更快的等效值（除了更複雜且更突出的索引分析器配置外）。 最好找出其他範圍界定限制，以改善整體查詢效能，要求函式對盡可能小的潛在結果集進行操作。

1. ***此調整專用於查詢生成器，不適用於JCR-SQL2或XPath。***

   使用 [查詢產生器的guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) 完整結果集為 **not** 立即需要。

   * **未優化的查詢**

      ```js
      type=cq:Page
      path=/content
      ```

   * **最佳化查詢**

      ```js
      type=cq:Page
      path=/content
      p.guessTotal=100
      ```
   若是查詢執行速度快但結果數量大的情況，請參閱。 `guessTotal` 是查詢產生器查詢的重要最佳化。

   `p.guessTotal=100` 告訴查詢產生器只收集前100個結果。 此外，要設定一個布林值標幟，指出是否至少存在一個結果（但不存在多少個結果，因為計算此數字會導致速度變慢）。 此最佳化優於分頁或無限載入使用案例，其中只會逐步顯示結果子集。

## 現有索引調整 {#existing-index-tuning}

1. 如果最佳查詢解析為屬性索引，則沒有其他任何可做的，因為屬性索引可調性最低。
1. 否則，查詢應解析為Lucene屬性索引。 如果無法解析索引，請跳到「建立新索引」。
1. 視需要將查詢轉換為XPath或JCR-SQL2。

   * **查詢產生器查詢**

      ```js
      query type=cq:Page
      path=/content/my-site/us/en
      property=jcr:content/contentType
      property.value=article-page
      orderby=@jcr:content/publishDate
      orderby.sort=desc
      ```

   * **從查詢生成器查詢生成的XPath**

      ```js
      /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
      ```

1. 將XPath（或JCR-SQL2）提供給Oak Index Definition Generator() `https://oakutils.appspot.com/generate/index` 以便生成優化的Lucene屬性索引定義。 <!-- The above URL is 404 as of April 24, 2023 -->

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

1. 以添加方式手動將生成的定義合併到現有Lucene屬性索引中。 請小心不要刪除現有配置，因為它們可能用於滿足其他查詢。

   1. 找出涵蓋cq:Page的現有Lucene屬性索引（使用索引管理器）。 在這種情況下， `/oak:index/cqPageLucene`.
   1. 識別最佳化索引定義(步驟#4)與現有索引(/oak:index/cqPageLucene)之間的設定差值，並將最佳化索引中遺漏的設定新增至現有索引定義。
   1. 根據AEM重新索引最佳實務，會根據現有內容是否可能受此索引配置變更影響，依序重新整理或重新索引。

## 建立新索引 {#create-a-new-index}

1. 驗證查詢未解析為現有Lucene屬性索引。 如果有，請參閱上節中關於優化和現有索引的部分。
1. 視需要將查詢轉換為XPath或JCR-SQL2。

   * **查詢產生器查詢**

      ```js
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **從查詢生成器查詢生成的XPath**

      ```js
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. 將XPath（或JCR-SQL2）提供給Oak Index Definition Generator() `https://oakutils.appspot.com/generate/index` 以便生成優化的Lucene屬性索引定義。 <!-- The above URL is 404 as of April 24, 2023 -->

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

   將Oak Index Definition Generator提供之新索引的XML定義新增至AEM專案，以管理Oak索引定義（請記住，將Oak索引定義視為程式碼，因為程式碼取決於這些定義）。

   在通常的AEM軟體開發生命週期後部署並測試新索引，並驗證查詢解析為索引且查詢效能良好。

   在初始部署此索引時，AEM會使用必要資料填入索引。

## 無索引和遍歷查詢何時可以？ {#when-index-less-and-traversal-queries-are-ok}

由於AEM有彈性的內容架構，很難預測並確保內容結構的周遊不會隨著時間而演化為無法接受的大。

因此，確保索引滿足查詢，除非路徑限制和nodetype限制的組合保證 **每次瀏覽的節點不到20個。**

## 查詢開發工具 {#query-development-tools}

### Adobe支援 {#adobe-supported}

* **查詢產生器除錯程式**

   * 執行查詢產生器查詢並產生支援XPath的WebUI（用於說明查詢或Oak索引定義產生器）。
   * 在AEM上 [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite — 查詢工具**

   * 用於執行XPath和JCR-SQL2查詢的WebUI。
   * 在AEM上 [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) >工具>查詢……

* **[說明查詢](/help/sites-administering/operations-dashboard.md#explain-query)**

   * AEM Operations控制面板，提供任何給定XPATH或JCR-SQL2查詢的詳細說明（查詢計畫、查詢時間和結果數）。

* **[慢速/熱門查詢](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM Operations控制面板列出最近在AEM上執行的緩慢和熱門查詢。

* **[索引管理員](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * AEM Operations WebUI顯示AEM例項上的索引；有助於了解哪些索引存在；可定位或增強。

* **[記錄](/help/sites-administering/operations-dashboard.md#log-messages)**

   * 查詢產生器記錄

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak查詢執行記錄

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit查詢引擎設定OSGi設定**

   * 用於配置遍歷查詢的故障行為的OSGi配置。
   * 在AEM上 [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * JMX MBean用於估計AEM中內容樹中的節點數。
   * 在AEM上 [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### 支援的社群 {#community-supported}

* **Oak Index Definition Generator(位於`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * 從XPath或JCR-SQL2查詢語句生成最佳Lucence屬性索引。

* **[AEM Chrome外掛程式](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Google Chrome網頁瀏覽器擴充功能會在瀏覽器的開發工具主控台中公開每個請求記錄資料，包括已執行的查詢及其查詢計畫。
   * 需要 [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) 以在AEM上安裝並啟用。
