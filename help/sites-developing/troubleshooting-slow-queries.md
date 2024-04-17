---
title: 疑難排解緩慢查詢
description: 瞭解如何疑難排解Adobe Experience Manager中的緩慢查詢。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 0%

---

# 疑難排解緩慢查詢{#troubleshooting-slow-queries}

## 查詢分類緩慢 {#slow-query-classifications}

AEM中有三個主要分類為緩慢查詢，依嚴重程度列出：

1. **無索引查詢**

   * 有此功能的查詢 **非** 解析為索引並遍歷JCR的內容以收集結果

1. **限制不良（或設定範圍）的查詢**

   * 解析成索引，但必須周遊所有索引專案以收集結果的查詢

1. **大型結果集查詢**

   * 傳回大量結果的查詢

查詢的前兩個分類（無索引和限制不佳）很慢。 速度較慢，因為它們強制Oak查詢引擎檢查每個 **潛在** 識別屬於下列專案之結果（內容節點或索引專案）： **實際** 結果集。

檢查每個潛在結果的行為稱為「周遊」。

由於必須檢查每個潛在結果，因此確定實際結果集的成本會與潛在結果的數量成線性增長。

新增查詢限制和調整索引可讓索引資料以最佳化格式儲存，以快速擷取結果，並減少或免除線性檢查潛在結果集的需求。

在AEM 6.3中，依預設，當達到100,000的周遊時，查詢會失敗並擲回例外狀況。 此限制在AEM 6.3之前的AEM版本中預設不存在，但可透過Apache Jackrabbit查詢引擎設定OSGi設定和QueryEngineSettings JMX bean （屬性LimitReads）設定。

### 偵測無索引查詢 {#detecting-index-less-queries}

#### 開發期間 {#during-development}

說明 **全部** 查詢並確保其查詢計畫不包含 **/&amp;ast；周遊** 說明書。 周遊查詢計畫的範例：

* **計畫：** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### 部署後 {#post-deployment}

* 監視 `error.log` 對於無索引周遊查詢：

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 只有在沒有索引可用，且查詢可能周遊許多節點時，才會記錄此訊息。 如果索引可用，則不會記錄訊息，但周遊的量很小，因此很快速。

* 造訪AEM [查詢效能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制檯和 [說明](/help/sites-administering/operations-dashboard.md#explain-query) 尋找周遊或無索引查詢說明的緩慢查詢。

### 偵測限制不佳的查詢 {#detecting-poorly-restricted-queries}

#### 開發期間 {#during-development-1}

說明所有查詢並確保它們解析為調整為符合查詢屬性限制的索引。

* 理想的查詢計畫涵蓋範圍有 `indexRules` 用於所有屬性限制，以及查詢中最嚴格的屬性限制。
* 排序結果的查詢應解析為Lucene屬性索引，其中包含用於按設定的屬性排序的索引規則 `orderable=true.`

#### 例如，預設值 `cqPageLucene` 沒有索引規則 `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

新增cq：tags索引規則之前

* **cq：tags索引規則**

   * 不存在立即可用的

* **查詢產生器查詢**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=my:tag
  ```

* **查詢計畫**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

此查詢解析為 `cqPageLucene` 索引，但因為沒有屬性索引規則存在 `jcr:content` 或 `cq:tags`，當評估此限制時， `cqPageLucene` 會檢查索引以判斷相符專案。 因此，如果索引包含100萬 `cq:Page` 節點，則會檢查100萬筆記錄以確定結果集。

新增cq：tags索引規則後

* **cq：tags索引規則**

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

新增indexRule for `jcr:content/cq:tags` 在 `cqPageLucene` 索引允許 `cq:tags` 以最佳化方式儲存的資料。

當查詢使用 `jcr:content/cq:tags` 執行限制，索引可以按值查詢結果。 這表示如果100 `cq:Page` 節點具有 `myTagNamespace:myTag` 作為值，僅傳回這100個結果，而其他999,000個結果會排除在限制檢查之外，以10,000的係數提升效能。

更多的查詢限制會減少符合資格的結果集，並進一步最佳化查詢最佳化。

同樣地，不需為建立額外的索引規則 `cq:tags` 屬性，甚至是限製為的全文查詢 `cq:tags` 會表現不佳，因為來自索引的結果會傳回所有全文相符專案。 cq：tags上的限制會在之後被篩選。

索引後篩選的另一個原因是存取控制清單，在開發期間經常會遺漏。 請嘗試確保查詢未傳回使用者可能無法存取的路徑。 若要這麼做，可改善內容結構，並在查詢上提供相關路徑限制。

若要識別Lucene索引是否傳回許多結果以傳回小型子集作為查詢結果，一個有效方法是啟用DEBUG記錄 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. 這麼做可讓您檢視從索引載入的檔案數。 最終結果數量與載入檔案數量不應不成比例。 如需詳細資訊，請參閱 [記錄](/help/sites-deploying/configure-logging.md).

#### 部署後 {#post-deployment-1}

* 監視 `error.log` 若為周遊查詢：

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* 造訪AEM [查詢效能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制檯和 [說明](/help/sites-administering/operations-dashboard.md#explain-query) 查詢速度緩慢，查詢計畫無法解決查詢屬性限制以索引屬性規則。

### 偵測大型結果集查詢 {#detecting-large-result-set-queries}

#### 開發期間 {#during-development-2}

為oak.queryLimitInMemory (例如10000)和oak.queryLimitReads （例如5000）設定低臨界值，並在遇到顯示「查詢讀取超過x個節點……」的UnsupportedOperationException時最佳化昂貴查詢

設定低臨界值有助於避免資源密集的查詢（亦即，不受任何索引支援或較少涵蓋範圍索引所支援）。 例如，讀取一百萬個節點的查詢會導致大量IO，並對整體應用程式效能產生負面影響。 因此，應該分析和最佳化任何由於上述限制而失敗的查詢。

#### 部署後 {#post-deployment-2}

* 監視查詢記錄以觸發大型節點周遊或大型棧積記憶體消耗： &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 最佳化查詢，以減少周遊的節點數。

* 監視觸發大型棧積記憶體消耗之查詢的記錄檔：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 最佳化查詢，以減少棧積記憶體耗用量。

對於AEM 6.0 - 6.2版本，您可以透過AEM啟動指令碼中的JVM引數調整節點周遊的臨界值，以防止大型查詢使環境過載。 建議的值為：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述兩個引數預設為預先設定，並可透過OSGi QueryEngineSettings修改。

下的詳細資訊： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 查詢效能調整 {#query-performance-tuning}

AEM中查詢效能最佳化的座右銘為：

**「限制越多越好。」**

以下概述為確保查詢效能而建議的調整。 首先，調整查詢（較不容易引起干擾的活動），然後視需要調整索引定義。

### 調整查詢陳述式 {#adjusting-the-query-statement}

AEM支援下列查詢語言：

* 查詢產生器
* JCR-SQL2
* XPath

以下範例使用查詢產生器，因為這是AEM開發人員最常使用的查詢語言，不過，相同的原則適用於JCR-SQL2和XPath。

1. 新增節點型別限制，讓查詢解析為現有的Lucene屬性索引。

* **未最佳化的查詢**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **最佳化的查詢**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  缺少節點型別限制的查詢強制AEM假設 `nt:base` nodetype，AEM中的每個節點都是其子型別，因此不會產生任何節點型別限制。

  設定 `type=cq:Page` 將此查詢限製為僅限 `cq:Page` 節點，並將查詢解析為AEM cqPageLucene，將結果限製為節點子集(僅限 `cq:Page` AEM節點)。

1. 調整查詢的節點型別限制，讓查詢解析為現有的Lucene屬性索引。

* **未最佳化的查詢**

  ```js
  type=nt:hierarchyNode
  property=jcr:content/contentType
  property.value=article-page
  ```

* **最佳化的查詢**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  `nt:hierarchyNode` 為的父節點型別 `cq:Page`. 假設 `jcr:content/contentType=article-page` 僅套用至 `cq:Page` 節點透過Adobe的自訂應用程式，此查詢只會傳回 `cq:Page` 節點，其中 `jcr:content/contentType=article-page`. 不過，此流量是次優限制，因為：

   * 其他節點繼承自 `nt:hierarchyNode` (例如， `dam:Asset`)將不必要地新增至潛在結果集。
   * 「 」沒有AEM提供的索引 `nt:hierarchyNode`，但由於有為 `cq:Page`.

  設定 `type=cq:Page` 將此查詢限製為僅限 `cq:Page` 節點，並將查詢解析為AEM cqPageLucene，將結果限製為AEM中的節點子集（僅限cq：Page節點）。

1. 或者，調整屬性限制，讓查詢解析為現有的屬性索引。

* **未最佳化的查詢**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **最佳化的查詢**

  ```js
  property=jcr:content/sling:resourceType
  property.value=my-site/components/structure/article-page
  ```

  變更屬性限制 `jcr:content/contentType` （自訂值）至已知屬性 `sling:resourceType` 讓查詢解析為屬性索引 `slingResourceType` 會依據以下條件索引所有內容： `sling:resourceType`.

  當查詢未依節點型別識別，且單一屬性限制主導結果集時，最好使用屬性索引（與Lucene屬性索引相反）。

1. 將最嚴格的路徑限制加入查詢。 例如，偏好設定 `/content/my-site/us/en` 超過 `/content/my-site`，或 `/content/dam` 超過 `/`.

* **未最佳化的查詢**

  ```js
  type=cq:Page
  path=/content
  property=jcr:content/contentType
  property.value=article-page
  ```

* **最佳化的查詢**

  ```js
  type=cq:Page
  path=/content/my-site/us/en
  property=jcr:content/contentType
  property.value=article-page
  ```

  設定路徑限制的範圍 `path=/content`至 `path=/content/my-site/us/en` 允許索引減少必須檢查的索引專案數。 當查詢可以限制路徑時，不僅僅是 `/content` 或 `/content/dam`，確認索引具有 `evaluatePathRestrictions=true`.

  注意使用 `evaluatePathRestrictions` 增加索引大小。

1. 可能的話，請避免查詢函式和查詢操作，例如： `LIKE` 和 `fn:XXXX` 因為成本會隨著限制型結果的數量而調整。

* **未最佳化的查詢**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.operation=like
  property.value=%article%
  ```

* **最佳化的查詢**

  ```js
  type=cq:Page
  fulltext=article
  fulltext.relPath=jcr:content/contentType
  ```

  LIKE條件的評估速度很慢，因為如果文字以萬用字元(&quot;%。..&#39;)開頭，則無法使用索引。 jcr：contains條件允許使用全文檢索，因此是偏好使用。 需要解析的Lucene屬性索引才能有indexRule `jcr:content/contentType` 替換為 `analayzed=true`.

  使用類似以下的查詢函式 `fn:lowercase(..)` 如果沒有速度更快的對等專案（在更複雜且干擾更重的索引分析器設定之外），可能更難最佳化。 最好找出其他範圍限制以改善整體查詢效能，要求函式儘可能在最小的潛在結果集合上操作。

1. ***此調整是Query Builder專用，不適用於JCR-SQL2或XPath。***

   使用 [查詢產生器的guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) 當完整的結果集為 **非** 立即需要。

   * **未最佳化的查詢**

     ```js
     type=cq:Page
     path=/content
     ```

   * **最佳化的查詢**

     ```js
     type=cq:Page
     path=/content
     p.guessTotal=100
     ```

   若查詢執行快速但結果數量很大的情況，p。 `guessTotal` 是Query Builder查詢的重要最佳化。

   `p.guessTotal=100` 告知Query Builder只收集前100個結果。 若要設定布林值標幟，指出是否至少還有一個結果（但不表示還有多少個結果，因為計算此數字會導致速度變慢）。 此最佳化不適用於分頁或無限載入的使用案例，這些案例只會以累加方式顯示結果子集。

## 現有的索引調整 {#existing-index-tuning}

1. 如果最佳查詢解析為屬性索引，則沒有剩餘要做的事，因為屬性索引最低限度可以調整。
1. 否則，查詢應該解析為Lucene屬性索引。 如果無法解析索引，請跳至建立索引。
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

   * **從Query Builder查詢產生的XPath**

     ```js
     /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
     ```

1. 將XPath （或JCR-SQL2）提供給Oak索引定義產生器，位於 `https://oakutils.appspot.com/generate/index` 以便產生最佳化的Lucene屬性索引定義。 <!-- The above URL is 404 as of April 24, 2023 -->

   **產生的Lucene屬性索引定義**

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

1. 以累加方式手動將產生的定義合併到現有Lucene屬性索引中。 請注意不要移除現有的設定，因為這些設定可用於滿足其他查詢。

   1. 找到涵蓋cq：Page的現有Lucene屬性索引（使用索引管理員）。 在這種情況下， `/oak:index/cqPageLucene`.
   1. 識別最佳化索引定義(步驟#4)和現有索引(/oak：index/cqPageLucene)之間的設定差異，並將最佳化索引中缺少的設定新增到現有索引定義。
   1. 根據AEM重新索引最佳實務，重新整理或重新索引會依序進行，視此索引設定變更是否會影響現有內容而定。

## 建立新索引 {#create-a-new-index}

1. 確認查詢未解析為現有的Lucene屬性索引。 如果是，請參閱上面關於微調和現有索引的章節。
1. 視需要將查詢轉換為XPath或JCR-SQL2。

   * **查詢產生器查詢**

     ```js
     type=myApp:Author
     property=firstName
     property.value=ira
     ```

   * **從Query Builder查詢產生的XPath**

     ```js
     //element(*, myApp:Page)[@firstName = 'ira']
     ```

1. 將XPath （或JCR-SQL2）提供給Oak索引定義產生器，位於 `https://oakutils.appspot.com/generate/index` 以便產生最佳化的Lucene屬性索引定義。 <!-- The above URL is 404 as of April 24, 2023 -->

   **產生的Lucene屬性索引定義**

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

1. 部署產生的Lucene屬性索引定義。

   將Oak索引定義產生器為新索引提供的XML定義新增到管理Oak索引定義的AEM專案（記住，將Oak索引定義視為程式碼，因為程式碼取決於它們）。

   依照一般的AEM軟體開發生命週期，部署及測試新索引，並確認查詢解析至索引且查詢執行正常。

   在此索引的初始部署中，AEM會使用必要資料填入索引。

## 無索引查詢和周遊查詢何時正常？ {#when-index-less-and-traversal-queries-are-ok}

由於AEM靈活的內容架構，很難預測內容結構的周遊情況並確保其不會隨時間演化而變得無法接受的龐大。

因此，除非路徑限制和節點型別限制的組合保證 **周遊的節點數少於20個。**

## 查詢開發工具 {#query-development-tools}

### 支援的Adobe {#adobe-supported}

* **Query Builder Debugger**

   * 用於執行Query Builder查詢並產生支援XPath的WebUI （用於Explain Query或Oak Index Definition Generator）。
   * 在AEM上 [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite — 查詢工具**

   * 用於執行XPath和JCR-SQL2查詢的WebUI。
   * 在AEM上 [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) >工具>查詢……

* **[說明查詢](/help/sites-administering/operations-dashboard.md#explain-query)**

   * 「AEM作業」儀表板，針對任何指定的XPATH或JCR-SQL2查詢，提供詳細的說明（查詢計畫、查詢時間和結果數）。

* **[緩慢/熱門查詢](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM Operations儀表板會列出最近在AEM上執行的緩慢且熱門的查詢。

* **[索引管理員](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * 顯示AEM執行個體上索引的AEM Operations WebUI；有助於瞭解存在哪些索引；可以定位或增加。

* **[記錄](/help/sites-administering/operations-dashboard.md#log-messages)**

   * 查詢產生器記錄

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`

   * Oak查詢執行記錄

      * `DEBUG @ org.apache.jackrabbit.oak.query`

* **Apache Jackrabbit查詢引擎設定OSGi設定**

   * 用於設定周遊查詢的失敗行為的OSGi設定。
   * 在AEM上 [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * JMX MBean用於估算AEM中內容樹狀結構的節點數量。
   * 在AEM上 [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### 社群支援 {#community-supported}

* **Oak索引定義產生器位於`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * 從XPath或JCR-SQL2查詢陳述式產生最佳的Lucence屬性索引。

* **_AEM Chrome外掛程式_** <!-- For whatever reason, the URL to this extension was causing too many redirects when doing the request so it was removed entirely to get rid of the error; users can easily look up the extension in Google instead. DO NOT ADD THE URL AGAIN!-->

   * 此 _AEM Chrome外掛程式_ 是Google Chrome網頁瀏覽器擴充功能，可在瀏覽器的開發工具主控台中公開每個要求的記錄資料，包括執行查詢及其查詢計畫。
   * 需要您安裝和啟用 [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) 在AEM上。
