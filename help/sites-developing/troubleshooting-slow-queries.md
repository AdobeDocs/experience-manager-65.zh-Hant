---
title: 排除慢速查詢的故障
seo-title: Troubleshooting Slow Queries
description: 排除慢速查詢的故障
seo-description: null
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2265'
ht-degree: 0%

---

# 排除慢速查詢的故障{#troubleshooting-slow-queries}

## 查詢分類速度慢 {#slow-query-classifications}

按嚴重性列出的慢速查詢有3AEM種主要分類：

1. **無索引查詢**

   * 執行此操作的查詢 **不** 解析到索引並遍歷JCR的內容以收集結果

1. **限制不足（或限定範圍）的查詢**

   * 解析為索引但必須遍歷所有索引條目以收集結果的查詢

1. **大型結果集查詢**

   * 返回大量結果的查詢

前2種查詢分類（無索引且限制性差）很慢，因為它們會強制Oak查詢引擎檢查每個查詢 **潛** 結果（內容節點或索引條目），用於標識屬於 **實際** 結果集。

檢查每個潛在結果的行為稱為「遍歷」。

由於必須檢查每個潛在結果，因此確定實際結果集的成本與潛在結果的數目呈線性增長。

添加查詢限制和調整索引允許索引資料以提供快速結果檢索的優化格式儲存，並減少或消除對潛在結果集的線性檢查的需要。

在AEM6.3中，預設情況下，當訪問100,000時，查詢失敗並引發異常。 預設情況下，在6.3AEM之前的AEM版本中不存在此限制，但可以通過Apache Jackrabbit查詢引擎設定OSGi配置和QueryEngineSettings JMX Bean（屬性LimitReads）設定。

### 檢測無索引查詢 {#detecting-index-less-queries}

#### 開發期間 {#during-development}

解釋 **全部** 查詢並確保其查詢計畫不包含 **/&amp;ast;橫** 解釋。 遍歷查詢計畫示例：

* **計畫：** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### 部署後 {#post-deployment}

* 監視 `error.log` 對於無索引遍歷查詢：

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 僅當沒有可用索引且查詢可能遍歷許多節點時，才記錄此消息。 如果索引可用，則不記錄消息，但遍歷的量很小，因此速度很快。

* 訪AEM問 [查詢效能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制台和 [解釋](/help/sites-administering/operations-dashboard.md#explain-query) 查找遍歷或無索引查詢解釋的查詢速度較慢。

### 檢測受限性差的查詢 {#detecting-poorly-restricted-queries}

#### 開發期間 {#during-development-1}

解釋所有查詢並確保它們解析為已調整以匹配查詢的屬性限制的索引。

* 理想的查詢計畫覆蓋範圍 `indexRules` 對於所有屬性限制，對於查詢中最緊的屬性限制，則至少要執行。
* 對結果排序的查詢應解析為Lucene屬性索引，該索引具有按設定的屬性排序的索引規則 `orderable=true.`

#### 例如， `cqPageLucene` 沒有的索引規則 `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

添加cq:tags索引規則之前

* **cq：標籤索引規則**

   * 不在機箱外

* **查詢生成器查詢**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **查詢計畫**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

此查詢解析為 `cqPageLucene` 索引，但是因為沒有屬性索引規則 `jcr:content` 或 `cq:tags`，在評估此限制時，每個記錄 `cqPageLucene` 檢查索引以確定匹配項。 這意味著如果指數包含100萬 `cq:Page` 然後檢查100萬條記錄以確定結果集。

添加cq:tags索引規則後

* **cq：標籤索引規則**

   ```js
   /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
   @name=jcr:content/cq:tags
   @propertyIndex=true
   ```

* **查詢生成器查詢**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=myTagNamespace:myTag
   ```

* **查詢計畫**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

為添加索引規則 `jcr:content/cq:tags` 的 `cqPageLucene` 索引允許 `cq:tags` 以優化方式儲存的資料。

當查詢 `jcr:content/cq:tags` 執行限制，索引可以按值查找結果。 這意味著如果100 `cq:Page` 節點 `myTagNamespace:myTag` 作為值，僅返回這100個結果，而其他999,000個則不在限制檢查中，使效能提高了10,000倍。

當然，進一步的查詢限制會減少符合條件的結果集並進一步優化查詢優化。

同樣，沒有附加的索引規則 `cq:tags` 屬性，甚至具有限制的全文查詢 `cq:tags` 效果會很差，因為索引的結果將返回所有全文匹配項。 在cq:tags後將過濾該限制。

索引後篩選的另一個原因是訪問控制清單，在開發過程中經常會錯過該清單。 嘗試確保查詢不返回用戶可能無法訪問的路徑。 這通常可以通過更好的內容結構以及對查詢提供相關的路徑限制來實現。

確定Lucene索引是否返回大量結果以返回很小的子集的一種有效方法是為 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` 並查看從索引中載入的文檔數。 最終結果的數量與載入檔案的數量之間不應不成比例。 有關詳細資訊，請參見 [記錄](/help/sites-deploying/configure-logging.md)。

#### 部署後 {#post-deployment-1}

* 監視 `error.log` 用於遍歷查詢：

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* 訪AEM問 [查詢效能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制台和 [解釋](/help/sites-administering/operations-dashboard.md#explain-query) 查詢速度慢，查找不將查詢屬性限制解析為索引屬性規則的查詢計畫。

### 檢測大型結果集查詢 {#detecting-large-result-set-queries}

#### 開發期間 {#during-development-2}

為oak.queryLimitInMemory設定低閾值(例如 10000)和oak.queryLimitReads(例如 5000)，並在命中UnsupportedOperationException（說「查詢讀取的節點數超過x個……」）時優化昂貴的查詢。

這有助於避免資源密集型查詢(即。 不支援任何索引或支援較少覆蓋索引)。 例如，讀取1M節點的查詢會導致大量IO，並對整體應用程式效能產生負面影響。 因此，任何由於超出限制而失敗的查詢都應進行分析和優化。

#### 部署後 {#post-deployment-2}

* 監視日誌，查看觸發大節點遍歷或大堆記憶體消耗的查詢：&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 優化查詢以減少遍歷節點數

* 監視日誌以查找觸發大堆記憶體消耗的查詢：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 優化查詢以減少堆記憶體消耗

對AEM於6.0 - 6.2版本，可以通過啟動指令碼中的JVM參數調整節點遍歷的閾值AEM，以防止大型查詢使環境過載。 建議的值為：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM6.3中，上述2個參數預設預配置，可通過OSGi QueryEngineSettings進行修改。

更多資訊可在以下位置獲得： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 查詢效能優化 {#query-performance-tuning}

查詢效能優化的格AEM言是：

**「限制越多越好。」**

以下概述了為確保查詢效能而建議的調整。 首先調整查詢，這是一個不太引人注目的活動，然後根據需要調整索引定義。

### 調整查詢語句 {#adjusting-the-query-statement}

支AEM持以下查詢語言：

* 查詢產生器
* JCR-SQL2
* XPath

下面的示例使用Query Builder作為開發人員使用的最常見的查詢語言AEM，但同樣的原則適用於JCR-SQL2和XPath。

1. 添加nodetype限制，以便查詢解析為現有Lucene屬性索引。

* **未優化查詢**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **優化查詢**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   缺少nodetype限制力AEM的查詢 `nt:base` nodetype，其中每個節點都AEM是的子類型，有效地導致nodetype不受約束。

   設定 `type=cq:Page` 僅限制此查詢 `cq:Page` ，並將查詢解析為AEMcqPageLucene，將結果限制為節點的子集(僅 `cq:Page` 節點)AEM。

1. 調整查詢的nodetype限制，使查詢解析為現有的Lucene屬性索引。

* **未優化查詢**

   ```js
   type=nt:hierarchyNode
   property=jcr:content/contentType
   property.value=article-page
   ```

* **優化查詢**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   `nt:hierarchyNode` 是的父節點類型 `cq:Page`，假設 `jcr:content/contentType=article-page` 僅應用於 `cq:Page` 節點，此查詢僅返回 `cq:Page` 節點 `jcr:content/contentType=article-page`。 但這是次優限制，因為：

   * 其他節點繼承自 `nt:hierarchyNode` (例如 `dam:Asset`)不必要地添加到一組潛在結果中。
   * 不AEM存在 `nt:hierarchyNode`，但是，由於為 `cq:Page`。
   設定 `type=cq:Page` 僅限制此查詢 `cq:Page` 將查詢解析為AEMcqPageLucene，將結果限制為中的節點子集（僅cq:Page節點）AEM。

1. 或者，調整屬性限制，使查詢解析為現有屬性索引。

* **未優化查詢**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **優化查詢**

   ```js
   property=jcr:content/sling:resourceType
   property.value=my-site/components/structure/article-page
   ```

   將屬性限制更改為 `jcr:content/contentType` （自定義值）到已知屬性 `sling:resourceType` 允許查詢解析為屬性索引 `slingResourceType` 將所有內容索引為 `sling:resourceType`。

   當查詢不按nodetype進行識別且結果集由單個屬性限制主導時，最好使用屬性索引（與Lucene屬性索引相對）。

1. 向查詢添加可能的最緊路徑限制。 例如，首選 `/content/my-site/us/en` 超 `/content/my-site`或 `/content/dam` 超 `/`。

* **未優化查詢**

   ```js
   type=cq:Page
   path=/content
   property=jcr:content/contentType
   property.value=article-page
   ```

* **優化查詢**

   ```js
   type=cq:Page
   path=/content/my-site/us/en
   property=jcr:content/contentType
   property.value=article-page
   ```

   將路徑限制範圍從 `path=/content`至 `path=/content/my-site/us/en` 允許索引減少需要檢查的索引條目數。 當查詢可以很好地限制路徑時， `/content` 或 `/content/dam`，確保索引 `evaluatePathRestrictions=true`。

   注釋使用 `evaluatePathRestrictions` 增加索引大小。

1. 盡可能避免查詢函式/操作查詢為： `LIKE` 和 `fn:XXXX` 隨著基於限制的結果的數量增加，成本會隨之增加。

* **未優化查詢**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.operation=like
   property.value=%article%
   ```

* **優化查詢**

   ```js
   type=cq:Page
   fulltext=article
   fulltext.relPath=jcr:content/contentType
   ```

   LIKE條件計算速度慢，因為如果文本以通配符(「%。..」)開頭，則不能使用索引。 jcr:contains條件允許使用全文索引，因此是首選。 這要求解析的Lucene屬性索引具有的indexRule `jcr:content/contentType` 與 `analayzed=true`。

   使用查詢函式(如 `fn:lowercase(..)` 由於沒有更快的等效項（超出更複雜和更引人注目的索引分析器配置），因此可能更難進行優化。 最好確定其他範圍界定限制以改進整體查詢效能，要求函式對盡可能小的潛在結果集進行操作。

1. ***此調整特定於查詢生成器，不適用於JCR-SQL2或XPath。***

   使用 [查詢生成器的guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) 當整個結果集 **不** 立即需要。

   * **未優化查詢**

      ```js
      type=cq:Page
      path=/content
      ```

   * **優化查詢**

      ```js
      type=cq:Page
      path=/content
      p.guessTotal=100
      ```
   對於查詢執行速度快但結果數量大的情況，p。 `guessTotal` 是查詢生成器查詢的關鍵優化。

   `p.guessTotal=100` 指示Query Builder僅收集前100個結果，並設定一個布爾標誌，指示是否至少存在一個結果（但不存在多少個結果，因為計算此數字將導致速度減慢）。 此優化在分頁或無限載入使用情形中表現出色，在這些情形中只增量顯示結果的子集。

## 現有索引優化 {#existing-index-tuning}

1. 如果最佳查詢解析為屬性索引，則沒有其他可執行的操作，因為屬性索引是可調性最小的。
1. 否則，查詢應解析為Lucene屬性索引。 如果無法解析索引，請跳轉到「建立新索引」。
1. 根據需要，將查詢轉換為XPath或JCR-SQL2。

   * **查詢生成器查詢**

      ```js
      query type=cq:Page
      path=/content/my-site/us/en
      property=jcr:content/contentType
      property.value=article-page
      orderby=@jcr:content/publishDate
      orderby.sort=desc
      ```

   * **從Query Builder查詢生成的XPath**

      ```js
      /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
      ```

1. 將XPath（或JCR-SQL2）提供給 [Oak索引定義生成器](https://oakutils.appspot.com/generate/index) 生成優化的Lucene屬性索引定義。

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

1. 以添加方式將生成的定義手動合併到現有Lucene屬性索引中。 請注意，不要刪除現有配置，因為它們可能用於滿足其他查詢。

   1. 找到覆蓋cq:Page的現有Lucene屬性索引（使用索引管理器）。 在這個例子中， `/oak:index/cqPageLucene`。
   1. 確定優化索引定義(步驟#4)和現有索引(/oak:index/cqPageLucene)之間的配置增量，並將優化索引中缺少的配置添加到現有索引定義中。
   1. 根AEM據重新編製最佳做法索引，根據現有內容是否會受到此索引配置更改的影響而進行刷新或重新編製索引。

## 建立新索引 {#create-a-new-index}

1. 驗證查詢是否未解析為現有Lucene屬性索引。 如果確實如此，請參見上面關於優化和現有索引的部分。
1. 根據需要，將查詢轉換為XPath或JCR-SQL2。

   * **查詢生成器查詢**

      ```js
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **從Query Builder查詢生成的XPath**

      ```js
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. 將XPath（或JCR-SQL2）提供給 [Oak索引定義生成器](https://oakutils.appspot.com/generate/index) 生成優化的Lucene屬性索引定義。

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

   將Oak索引定義生成器為新索引提供的XML定義添加到管理Oak索引定義的項目AEM（請記住，將Oak索引定義視為代碼，因為代碼取決於它們）。

   在通常的軟體開發生命週期後部署和testAEM新索引，並驗證查詢是否解析為索引且查詢是效能。

   初始部署此索引時，AEM將使用必需資料填充索引。

## 無索引和遍歷查詢何時可以？ {#when-index-less-and-traversal-queries-are-ok}

由於AEM內容體系結構靈活，很難預測和確保內容結構的遍歷不會隨著時間而演化為不可接受的大。

因此，確保索引滿足查詢，除非路徑限制和nodetype限制的組合保證 **遍歷的節點數不到20個。**

## 查詢開發工具 {#query-development-tools}

### Adobe支援 {#adobe-supported}

* **查詢生成器調試器**

   * 用於執行查詢生成器查詢並生成支援的XPath的WebUI（用於解釋查詢或Oak索引定義生成器）。
   * 位於AEM [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite — 查詢工具**

   * 用於執行XPath和JCR-SQL2查詢的WebUI。
   * 位於AEM [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) >工具>查詢……

* **[說明查詢](/help/sites-administering/operations-dashboard.md#explain-query)**

   * 一個操AEM作面板，它為任何給定的XPATH或JCR-SQL2查詢提供詳細說明（查詢計畫、查詢時間和結果數）。

* **[慢速/常用查詢](/help/sites-administering/operations-dashboard.md#query-performance)**

   * 列出AEM最近執行的慢速和常用查詢的「操作」控AEM制板。

* **[索引管理員](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * 一AEM個操作WebUI，顯示實例上的AEM索引；有助於瞭解哪些索引已經存在，可以定向或增強。

* **[記錄](/help/sites-administering/operations-dashboard.md#log-messages)**

   * 查詢生成器日誌記錄

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak查詢執行日誌記錄

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit查詢引擎設定OSGi配置**

   * 配置用於遍歷查詢的失敗行為的OSGi配置。
   * 位於AEM [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * JMX MBean用於估計中內容樹中的節點數AEM。
   * 位於AEM [/system/console/jmx/org.apache.jackrabbit.oak%3名稱%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### 支援的社區 {#community-supported}

* **[Oak索引定義生成器](https://oakutils.appspot.com/generate/index)**

   * 從XPath或JCR-SQL2查詢語句生成最佳Lucence屬性索引。

* **[AEMChrome插件](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * GoogleChrome Web瀏覽器擴展，在瀏覽器的開發工具控制台中顯示每個請求的日誌資料，包括已執行的查詢及其查詢計畫。
   * 需要 [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) 上安裝並啟AEM用。
