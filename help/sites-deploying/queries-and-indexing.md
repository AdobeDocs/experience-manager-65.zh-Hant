---
title: Oak查詢和索引
seo-title: Oak Queries and Indexing
description: 瞭解如何在中配置索AEM引。
seo-description: Learn how to configure indexes in AEM.
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
source-git-commit: b27a7a1cc2295b1640520dcb56be4f3eb4851499
workflow-type: tm+mt
source-wordcount: '2674'
ht-degree: 1%

---

# Oak查詢和索引{#oak-queries-and-indexing}

>[!NOTE]
>
>本文介紹在6中配置索AEM引。 有關優化查詢和索引效能的最佳做法，請參見 [查詢和索引的最佳做法](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

## 簡介 {#introduction}

與Jackrabbit 2不同，Oak預設不為內容編製索引。 需要時需要建立自定義索引，與傳統關係資料庫非常相似。 如果沒有特定查詢的索引，可能會遍歷許多節點。 查詢可能仍然有效，但可能非常慢。

如果Oak遇到沒有索引的查詢，則會打印WARN級別日誌消息：

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## 支援的查詢語言 {#supported-query-languages}

Oak查詢引擎支援以下語言：

* XPath（推薦）
* SQL-2
* SQL（不建議使用）
* JQOM

## 索引器類型和成本計算 {#indexer-types-and-cost-calculation}

基於Apache Oak的後端允許將不同的索引器插入儲存庫。

一個索引器是 **屬性索引**，其中索引定義儲存在儲存庫本身中。

用於 **阿帕奇盧塞內** 和 **索爾** 預設情況下也可用，這兩個都支援全文索引。

的 **遍歷索引** 的下界。 這意味著未對內容進行索引，並遍歷內容節點以查找與查詢的匹配項。

如果多個索引器可用於查詢，則每個可用索引器估計執行查詢的成本。 然後Oak以最低的估計成本選擇索引器。

![chlimage_1-148](assets/chlimage_1-148.png)

上圖是Apache Oak查詢執行機制的高級表示。

首先，將查詢解析為抽象語法樹。 然後，檢查查詢並將其轉換為SQL-2,SQL-2是Oak查詢的本機語言。

接下來，參考每個索引來估計查詢的成本。 一旦完成，將檢索最便宜索引的結果。 最後，對結果進行篩選，以確保當前用戶對結果具有讀訪問權，並且結果與完整查詢匹配。

## 配置索引 {#configuring-the-indexes}

>[!NOTE]
>
>對於大型儲存庫，構建索引是一項耗時的操作。 對於初始建立索引和重新編製索引（在更改定義後重建索引），都是如此。 另請參閱 [Oak索引故障排除](/help/sites-deploying/troubleshooting-oak-indexes.md) 和 [防止慢速重新索引](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing)。

如果在非常大的儲存庫中需要重新編製索引，特別是在使用MongoDB和用於全文索引時，請考慮文本預提取，並使用oak-run構建初始索引和重新編製索引。

索引配置為儲存庫中位於 **橡樹：索引** 的下界。

索引節點的類型必須為 **oak:QueryIndexDefinition。** 對於每個索引器，可以使用多個配置選項作為節點屬性。 有關詳細資訊，請參閱下面每個索引器類型的配置詳細資訊。

### 屬性索引 {#the-property-index}

屬性索引通常適用於具有屬性約束但不是全文的查詢。 可以通過以下過程進行配置：

1. 通過轉到 `http://localhost:4502/crx/de/index.jsp`
1. 在 **橡樹：索引**
1. 命名節點 **屬性索引**，並將節點類型設定為 **oak:QueryIndexDefinition**
1. 為新節點設定以下屬性：

   * **類型：**  `property` （類型為字串）
   * **屬性名稱：**  `jcr:uuid` （類型為名稱）

   此特定示例將為 `jcr:uuid` 屬性，其作業是公開它所附加到的節點的通用唯一標識符(UUID)。

1. 儲存變更。

屬性索引具有以下配置選項：

* 的 **類型** 屬性將指定索引的類型，在這種情況下，必須將其設定為 **屬性**

* 的 **屬性名稱** 屬性指明將儲存在索引中的屬性的清單。 如果缺少，節點名稱將用作屬性名稱引用值。 在此示例中， **jcr:uuid** 其作業要公開其節點的唯一標識符(UUID)的屬性將添加到索引中。

* 的 **獨特** 標誌，如果設定為 **真** 為屬性索引添加唯一性約束。

* 的 **聲明NodeTypes** 屬性允許您指定索引將僅應用於的特定節點類型。
* 的 **重新索引** 標籤如果設定為 **真**，將觸發完整內容重新索引。

### 有序索引 {#the-ordered-index}

Ordered索引是屬性索引的擴展。 但是，它已被棄用。 此類型的索引需要替換為 [Lucene屬性索引](#the-lucene-property-index)。

### Lucene全文索引 {#the-lucene-full-text-index}

基於Apache Lucene的全文索引器在6中提AEM供。

如果配置了全文索引，則具有全文條件的所有查詢都使用全文索引，無論是否有其他條件被編入索引，也無論是否有路徑限制。

如果未配置全文索引，則具有全文條件的查詢將無法按預期工作。

由於索引是通過非同步後台線程更新的，因此在後台進程完成之前，某些全文搜索將在一小段時間內不可用。

您可以按照以下步驟配置Lucene全文索引：

1. 開啟CRXDE並在 **橡樹：索引**。
1. 命名節點 **盧塞內指數** 並將節點類型設定為 **oak:QueryIndexDefinition**
1. 將以下屬性添加到節點：

   * **類型：**  `lucene` （類型為字串）
   * **非同步：**  `async` （類型為字串）

1. 儲存變更。

Lucene索引具有以下配置選項：

* 的 **類型** 必須指定索引類型的屬性必須設定為 **苜蓿**
* 的 **非同步** 必須設定為的屬性 **非同步**。 這將將索引更新進程發送到後台線程。
* 的 **includePropertyTypes** 屬性，該屬性將定義索引中將包含哪些屬性類型子集。
* 的 **排除屬性名** 屬性，該屬性將定義屬性名稱清單 — 應從索引中排除的屬性。
* 的 **重新索引** 標籤設定為 **真**，觸發完整內容重新索引。

### Lucene屬性索引 {#the-lucene-property-index}

自 **橡1.0.8**,Lucene可用於建立包含非全文的屬性約束的索引。

為了實現Lucene屬性索引 **全文已啟用** 必須始終將屬性設定為false。

以下示例查詢為例：

```xml
select * from [nt:base] where [alias] = '/admin'
```

為了為上述查詢定義Lucene屬性索引，可以通過在下面建立新節點來添加以下定義 **橡木:index:**

* **名稱:** `LucenePropertyIndex`
* **類型：** `oak:QueryIndexDefinition`

建立節點後，添加以下屬性：

* **類型:**

   ```xml
   lucene (of type String)
   ```

* **非同步處理:**

   ```xml
   async (of type String)
   ```

* **全文已啟用：**

   ```xml
   false (of type Boolean)
   ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>與常規屬性索引相比，Lucene屬性索引始終以非同步模式配置。 因此，索引返回的結果可能並不總是反映儲存庫的最新狀態。

>[!NOTE]
>
>有關Lucene屬性索引的更詳細資訊，請參見 [Apache Jackrabbit Oak Lucene文檔頁](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### Lucene分析器 {#lucene-analyzers}

自1.2.0版以來，Oak支援Lucene分析器。

分析器在對文檔進行索引時和在查詢時都使用。 分析器檢查欄位的文本並生成令牌流。 Lucene分析器由一系列標籤器和過濾器類組成。

分析器可通過 `analyzers` 節點（類型） `nt:unstructured`) `oak:index` 定義。

索引的預設分析器在 `default` 分析器節點的子級。

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>有關可用分析器的清單，請參考您使用的Lucene版本的API文檔。

#### 直接指定Analyzer類 {#specifying-the-analyzer-class-directly}

如果希望使用任何出廠分析器，可按以下步驟配置：

1. 找到要使用分析器的索引 `oak:index` 的下界。

1. 在索引下，建立名為 `default` 類型 `nt:unstructured`。

1. 將屬性添加到具有以下屬性的預設節點：

   * **名稱:** `class`
   * **類型：** `String`
   * **值:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   值是要使用的分析器類的名稱。

   還可以使用可選 `luceneMatchVersion` 字串屬性。 與Lucene 4.7配合使用的有效合成為：

   * **名稱:** `luceneMatchVersion`
   * **類型：** `String`
   * **值:** `LUCENE_47`

   如果 `luceneMatchVersion` Oak將使用隨附的Lucene版本。

1. 如果要向分析器配置中添加停止詞檔案，可以在 `default` 具有以下屬性的：

   * **名稱:** `stopwords`
   * **類型：** `nt:file`

#### 通過合成建立分析器 {#creating-analyzers-via-composition}

分析器也可基於 `Tokenizers`。 `TokenFilters` 和 `CharFilters`。 可以通過指定分析器並建立其可選標籤器和篩選器的子節點來執行此操作，這些子節點將按列出的順序應用。 另請參閱 [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

以此節點結構為例：

* **名稱:** `analyzers`

   * **名稱:** `default`

      * **名稱:** `charFilters`
      * **類型：** `nt:unstructured`

         * **名稱:** `HTMLStrip`
         * **名稱:** `Mapping`
      * **名稱:** `tokenizer`

         * **屬性名稱:** `name`

            * **類型：** `String`
            * **值:** `Standard`
      * **名稱:** `filters`
      * **類型：** `nt:unstructured`

         * **名稱:** `LowerCase`
         * **名稱:** `Stop`

            * **屬性名稱:** `words`

               * **類型：** `String`
               * **值:** `stop1.txt, stop2.txt`
            * **名稱:** `stop1.txt`

               * **類型：** `nt:file`
            * **名稱:** `stop2.txt`

               * **類型：** `nt:file`





過濾器、charFilters和標籤器的名稱通過刪除工廠尾碼形成。 因此：

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` 變成 `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` 變成 `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` 變成 `Stop`

工廠所需的任何配置參數都指定為相關代碼的屬性。

對於例如需要載入來自外部檔案的內容的停止詞的載入情況，可以通過建立的 `nt:file` 鍵入有關檔案。

### 索爾指數 {#the-solr-index}

Solr索引的目的主要是全文搜索，但也可以用於按路徑、屬性限制和主要類型限制對搜索進行索引。 這意味著Oak中的Solr索引可用於任何類型的JCR查詢。

中的集AEM成在儲存庫級別進行，因此Solr是Oak中可能使用的索引之一，Oak是隨附的新儲存庫實施AEM。

它可配置為與實例一起作為遠程服AEM務器。

### 使用AEM單個遠程Solr伺服器配置 {#configuring-aem-with-a-single-remote-solr-server}

還可AEM以配置為與遠程Solr伺服器實例一起使用：

1. 下載並解壓最新版本的Solr。 有關如何執行此操作的詳細資訊，請參考 [Apache Solr安裝文檔](https://cwiki.apache.org/confluence/display/solr/Installing+Solr)。
1. 現在，建立兩個索爾碎片。 可以通過在已解壓Solr的資料夾中為每個分片建立資料夾來執行此操作：

   * 對於第一個分片，請建立資料夾：

   `<solrunpackdirectory>\aemsolr1\node1`

   * 對於第二個分片，請建立資料夾：

   `<solrunpackdirectory>\aemsolr2\node2`

1. 在Solr包中找到示例實例。 它通常位於名為「」的資料夾中 `example`」。
1. 將以下資料夾從示例實例複製到兩個分片資料夾( `aemsolr1\node1` 和 `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 新建名為「」的資料夾 `cfg`」。
1. 將Solr和Zookeeper配置檔案放在新建立的 `cfg` 資料夾。

   >[!NOTE]
   >
   >有關Solr和ZooKeeper配置的詳細資訊，請參閱 [Solr配置文檔](https://wiki.apache.org/solr/ConfiguringSolr) 和 [《 ZooKeeper入門指南》](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html)。

1. 在ZooKeeper支援下啟動第一個碎片 `aemsolr1\node1` 並運行以下命令：

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 開始第二個分片， `aemsolr2\node2` 並運行以下命令：

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 啟動兩個分片後，通過連接到位於的Solr介面，test所有分片都已啟動並運行 `http://localhost:8983/solr/#/`
1. 啟AEM動並轉至Web控制台 `http://localhost:4502/system/console/configMgr`
1. 在下面設定以下配置 **Oak Solr遠程伺服器配置**:

   * 解析HTTP URL: `http://localhost:8983/solr/`

1. 選擇 **遠程解決方** 在 **奧克索爾** 伺服器提供程式。

1. 轉到CRXDE並以Admin身份登錄。
1. 建立名為 **索爾索引** 在 **橡樹：索引**，並設定以下屬性：

   * **類型：** solr（字串類型）
   * **非同步：** async（屬於字串類型）
   * **重新索引：** true（布爾型）

1. 儲存變更。

#### 建議的Solr配置 {#recommended-configuration-for-solr}

下面是一個基本配置示例，可用於本文中描述的所有三個Solr部署。 它可容納中已存在且不應與其AEM他應用程式一起使用的專用屬性索引。

為了正確使用它，您需要將存檔的內容直接放在Solr Home Directory中。 在部署多節點時，它應直接位於每個節點的根資料夾下。

推薦的Solr配置檔案

[取得檔案](assets/recommended-conf.zip)

### 索AEM引工具 {#aem-indexing-tools}

AEM6.1還整合了6.0中提供的兩AEM種索引工具，作為Adobe咨詢服務公域工具集的一部分：

1. **解釋查詢**&#x200B;工具旨在幫助管理員瞭解如何執行查詢；
1. **Oak索引管理器**，用於維護現有索引的Web用戶介面。

你現在可以通過 **工具 — 操作 — 儀表板 — 診斷** 的上AEM界。

有關如何使用它們的詳細資訊，請參閱 [操作儀表板文檔](/help/sites-administering/operations-dashboard.md)。

#### 通過OSGi建立屬性索引 {#creating-property-indexes-via-osgi}

ACS Commons軟體包還公開了可用於建立屬性索引的OSGi配置。

您可以通過搜索「 」從Web控制台訪問&#x200B;**確保Oak屬性索引**。

![chlimage_1-150](assets/chlimage_1-150.png)

### 索引問題疑難解答 {#troubleshooting-indexing-issues}

出現查詢執行時間長且一般系統響應時間慢的情況。

本節提供了一組建議，說明需要採取哪些措施來查明這些問題的原因，並就如何解決這些問題提出了建議。

#### 準備分析的調試資訊 {#preparing-debugging-info-for-analysis}

獲取正在執行的查詢所需資訊的最簡單方法是 [解釋查詢工具](/help/sites-administering/operations-dashboard.md#explain-query)。 這樣，您就可以收集調試慢速查詢所需的準確資訊，而無需查閱日誌級別資訊。 如果您知道正在調試的查詢，則這是可取的。

如果由於任何原因不可能這樣做，則可以在單個檔案中收集索引日誌，並使用它來解決您的特定問題。

#### 啟用日誌記錄 {#enable-logging}

要啟用日誌記錄，您需要啟用 **調試** 與Oak索引和查詢相關的類別的級別日誌。 這些類別包括：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

的 **com.day.cq.search** 類別僅在您使用提供的QueryBuilder實AEM用程式時適用。

>[!NOTE]
>
>在執行要排除故障的查詢的過程中，日誌僅設定為DEBUG，這一點非常重要，否則，日誌中將隨著時間的推移生成大量事件。 因此，一旦收集到所需日誌，就會切換回上述類別的INFO級日誌記錄。

您可以通過以下過程啟用日誌記錄：

1. 將瀏覽器指向 `https://serveraddress:port/system/console/slinglog`
1. 按一下 **添加新記錄器** 按鈕
1. 在新建立的行中，添加上述類別。 您可以使用 **+** 登錄以向單個記錄器添加多個類別。
1. 選擇 **調試** 從 **日誌級別** 的下界。
1. 將輸出檔案設定為 `logs/queryDebug.log`。 這將將所有DEBUG事件關聯到單個日誌檔案中。
1. 運行查詢或呈現使用要調試的查詢的頁面。
1. 執行查詢後，返回日誌控制台，並將新建立的記錄器的日誌級別更改為 **資訊**。

#### 索引配置 {#index-configuration}

查詢的評估方式在很大程度上受索引配置的影響。 獲取索引配置對於分析或發送支援非常重要。 您可以將配置作為內容包獲取，也可以獲取JSON格式副本。

因為在大多數情況下，索引配置儲存在 `/oak:index` 節點，可以在以下位置獲取JSON版本：

`https://serveraddress:port/oak:index.tidy.-1.json`

如果索引配置在不同的位置，請相應更改路徑。

#### MBean輸出 {#mbean-output}

在某些情況下，提供與索引相關的MBean的輸出以供調試。 您可以透過以下方式進行：

1. 轉到JMX控制台：
   `https://serveraddress:port/system/console/jmx`

1. 搜索以下MBean:

   * Lucene索引統計資訊
   * CopyOnRead支援統計資訊
   * Oak查詢統計資訊
   * 索引統計

1. 按一下每個MBean獲取效能統計資訊。 建立螢幕截圖或記下螢幕截圖，以備需要提交支援。

您還可以在以下URL上獲取這些統計資訊的JSON變型：

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

您還可以通過 `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`。 這將包括所有與Oak相關的MBean詳細資訊（JSON格式）。

#### 其他詳細資訊 {#other-details}

您可以收集其他詳細資訊以幫助解決問題，例如：

1. 您的實例正在運行的Oak版本。 您可以通過開啟CRXDE並查看歡迎頁面右下角的版本，或檢查 `org.apache.jackrabbit.oak-core` 捆綁。
1. 繁雜查詢的QueryBuilder調試器輸出。 可以在以下位置訪問調試器： `https://serveraddress:port/libs/cq/search/content/querydebug.html`
