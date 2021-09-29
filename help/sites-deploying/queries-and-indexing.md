---
title: Oak查詢和索引
seo-title: Oak Queries and Indexing
description: 了解如何在AEM中設定索引。
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
source-git-commit: 7cd4b6918a8b0de68f9f5c6a79ab3b49e8ef6fc1
workflow-type: tm+mt
source-wordcount: '2868'
ht-degree: 0%

---

# Oak查詢和索引{#oak-queries-and-indexing}

>[!NOTE]
>
>本文主要探討如何在AEM 6中設定索引。 有關優化查詢和索引效能的最佳實踐，請參閱[查詢和索引的最佳實踐](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

## 簡介 {#introduction}

與Jackrabbit 2不同，Oak預設不會為內容建立索引。 必要時需要建立自定義索引，與傳統關係資料庫類似。 如果沒有特定查詢的索引，則可能會遍歷許多節點。 查詢可能仍然有效，但可能非常慢。

如果Oak遇到沒有索引的查詢，則會列印WARN層級記錄訊息：

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## 支援的查詢語言 {#supported-query-languages}

Oak查詢引擎支援下列語言：

* XPath（推薦）
* SQL-2
* SQL（已廢止）
* JQOM

## 索引器類型和成本計算 {#indexer-types-and-cost-calculation}

Apache Oak後端可讓不同的索引器插入存放庫。

一個索引器是&#x200B;**屬性索引**，其索引定義儲存在儲存庫本身中。

預設也提供&#x200B;**Apache Lucene**&#x200B;和&#x200B;**Solr**&#x200B;的實施，兩者均支援全文索引。

如果沒有其他索引器可用，則使用&#x200B;**遍歷索引**。 這表示內容沒有編列索引，內容節點會經過各處以尋找與查詢的相符項目。

如果一個查詢有多個索引器，則每個可用索引器估計執行該查詢的成本。 然後Oak以最低的估計成本選擇索引器。

![chlimage_1-148](assets/chlimage_1-148.png)

上圖為Apache Oak查詢執行機制的高階表示法。

首先，將查詢剖析為抽象語法樹。 接著，會檢查查詢並轉換為SQL-2（Oak查詢的原生語言）。

接下來，咨詢每個索引以估計查詢的成本。 完成後，將檢索最便宜的索引的結果。 最後，篩選結果，以確保當前用戶對結果具有讀取訪問權，並且結果與完整查詢匹配。

## 配置索引 {#configuring-the-indexes}

>[!NOTE]
>
>對於大型儲存庫，建立索引是一項耗時的操作。 對於初始建立索引和重新索引（在更改定義後重建索引），都是如此。 另請參閱[疑難排解Oak Indexes](/help/sites-deploying/troubleshooting-oak-indexes.md)和[防止重新索引緩慢](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing)。

如果在非常大型的存放庫中需要重新索引，尤其是使用MongoDB和進行全文索引時，請考慮文字預先擷取，並使用oak-run來建立初始索引和重新索引。

索引在&#x200B;**oak:index**&#x200B;節點下設定為存放庫中的節點。

索引節點的類型必須為&#x200B;**oak:QueryIndexDefinition。** 每個索引器有幾個配置選項可用作節點屬性。有關詳細資訊，請參見下面每個索引器類型的配置詳細資訊。

### 屬性索引 {#the-property-index}

對於具有屬性約束但不是全文的查詢，屬性索引通常很有用。 您可以依照下列程式進行設定：

1. 前往`http://localhost:4502/crx/de/index.jsp`開啟CRXDE
1. 在&#x200B;**oak:index**&#x200B;下建立新節點
1. 將節點命名為&#x200B;**PropertyIndex**，並將節點類型設定為&#x200B;**oak:QueryIndexDefinition**
1. 為新節點設定以下屬性：

   * **類型：**  `property` （類型為字串）
   * **propertyNames:**  `jcr:uuid` （類型為Name）

   此特定示例將為`jcr:uuid`屬性編製索引，其作業是公開其所連接節點的通用唯一標識符(UUID)。

1. 儲存變更。

「屬性索引」具有以下配置選項：

* **type**&#x200B;屬性將指定索引的類型，在此情況下，必須將其設定為&#x200B;**property**

* **propertyNames**&#x200B;屬性指示將儲存在索引中的屬性清單。 如果缺少，則節點名稱將用作屬性名稱引用值。 在此範例中，將作業為公開其節點的唯一識別碼(UUID)的&#x200B;**jcr:uuid**&#x200B;屬性新增至索引。

* **unique**&#x200B;標幟，若設為&#x200B;**true**，則會在屬性索引上新增唯一性限制。

* **declibingNodeTypes**&#x200B;屬性允許您指定索引將僅應用到的特定節點類型。
* **reindex**&#x200B;標幟若設為&#x200B;**true**，將觸發完整內容重新索引。

### 有序索引 {#the-ordered-index}

Ordered索引是屬性索引的擴展。 不過，已遭取代。 此類型的索引需要替換為[Lucene屬性索引](#the-lucene-property-index)。

### 盧塞內全文索引 {#the-lucene-full-text-index}

AEM 6提供以Apache Lucene為基礎的全文索引器。

如果配置了全文索引，則具有全文條件的所有查詢都使用全文索引，無論是否有其他條件已編列索引，也無論是否有路徑限制。

如果未配置全文索引，則具有全文條件的查詢將無法如預期運作。

由於索引是透過非同步背景執行緒更新，因此在完成背景程式之前，某些全文搜尋功能將無法在短時間內完成。

您可以依照下列程式來設定Lucene全文索引：

1. 開啟CRXDE並在&#x200B;**oak:index**&#x200B;下建立新節點。
1. 將節點命名為&#x200B;**LuceneIndex**，並將節點類型設定為&#x200B;**oak:QueryIndexDefinition**
1. 將下列屬性新增至節點：

   * **類型：**  `lucene` （類型為字串）
   * **async:**  `async` （類型為字串）

1. 儲存變更。

Lucene索引具有以下配置選項：

* 將指定索引類型的&#x200B;**type**&#x200B;屬性必須設定為&#x200B;**lucene**
* 必須設為&#x200B;**async**&#x200B;的&#x200B;**async**&#x200B;屬性。 這會將索引更新程式傳送至背景執行緒。
* **includePropertyTypes**&#x200B;屬性，將定義將包含在索引中的屬性類型子集。
* **excludePropertyNames**&#x200B;屬性，將定義屬性名稱清單 — 應從索引中排除的屬性。
* 將&#x200B;**重新索引**&#x200B;標幟設為&#x200B;**true**&#x200B;時，會觸發完整內容重新索引。

### Lucene屬性索引 {#the-lucene-property-index}

由於&#x200B;**Oak 1.0.8**，因此Lucene可用來建立索引，其中涉及非全文的屬性限制。

為了實現Lucene屬性索引，**fulltextEnabled**&#x200B;屬性必須始終設定為false。

以下列範例查詢為例：

```xml
select * from [nt:base] where [alias] = '/admin'
```

若要定義上述查詢的Lucene屬性索引，您可以在&#x200B;**oak:index:**&#x200B;下建立新節點，以新增下列定義

* **名稱：** `LucenePropertyIndex`
* **類型：** `oak:QueryIndexDefinition`

建立節點後，新增下列屬性：

* **類型:**

   ```xml
   lucene (of type String)
   ```

* **非同步處理:**

   ```xml
   async (of type String)
   ```

* **fulltextEnabled:**

   ```xml
   false (of type Boolean)
   ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>與常規屬性索引相比， Lucene屬性索引始終以非同步模式配置。 因此，索引返回的結果可能並不總是反映儲存庫的最新狀態。

>[!NOTE]
>
>如需Lucene屬性索引的詳細資訊，請參閱[Apache Jackrabbit Oak Lucene檔案頁面](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### 盧塞內分析器 {#lucene-analyzers}

自1.2.0版起，Oak支援Lucene分析器。

在對文檔編製索引時和在查詢時都使用分析器。 分析器檢查欄位文本並生成令牌流。 Lucene分析器由一系列標籤器和過濾器類組成。

可以通過`oak:index`定義內的`analyzers`節點（類型`nt:unstructured`）配置分析器。

索引的預設分析器配置在分析器節點的`default`子項中。

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>如需可用分析器的清單，請參閱您所使用Lucene版本的API檔案。

#### 直接指定分析器類 {#specifying-the-analyzer-class-directly}

如果要使用任何現成分析器，可以按照以下過程進行配置：

1. 在`oak:index`節點下找到要使用具有的分析器的索引。

1. 在索引下，建立`nt:unstructured`類型的`default`子節點。

1. 將屬性新增至預設節點，並具有下列屬性：

   * **名稱：** `class`
   * **類型：** `String`
   * **值：** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   值是要使用的分析器類的名稱。

   您也可以使用可選的`luceneMatchVersion`字串屬性，將分析器設定為與特定lucene版本一起使用。 與Lucene 4.7一起使用的有效合成酶是：

   * **名稱：** `luceneMatchVersion`
   * **類型：** `String`
   * **值：** `LUCENE_47`

   若未提供`luceneMatchVersion`,Oak將會使用隨附的Lucene版本。

1. 如果要向分析器配置中添加秒數檔案，可以在`default`下建立一個具有以下屬性的新節點：

   * **名稱：** `stopwords`
   * **類型：** `nt:file`

#### 透過合成建立分析器 {#creating-analyzers-via-composition}

分析器也可以基於`Tokenizers`、`TokenFilters`和`CharFilters`來組成。 您可以通過指定分析器並建立其可選標籤和篩選器的子節點來執行此操作，這些節點將按列出順序應用。 另請參閱[https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

以此節點結構為例：

* **名稱：** `analyzers`

   * **名稱：** `default`

      * **名稱：** `charFilters`
      * **類型：** `nt:unstructured`

         * **名稱：** `HTMLStrip`
         * **名稱：** `Mapping`
      * **名稱：** `tokenizer`

         * **屬性名稱:** `name`

            * **類型：** `String`
            * **值：** `Standard`
      * **名稱：** `filters`
      * **類型：** `nt:unstructured`

         * **名稱：** `LowerCase`
         * **名稱：** `Stop`

            * **屬性名稱：** `words`

               * **類型：** `String`
               * **值：** `stop1.txt, stop2.txt`
            * **名稱：** `stop1.txt`

               * **類型：** `nt:file`
            * **名稱：** `stop2.txt`

               * **類型：** `nt:file`





篩選器、charFilters和標籤器的名稱是通過刪除工廠尾碼而形成的。 因此：

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` com  `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` com  `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` com  `Stop`

工廠所需的任何配置參數都指定為相關代碼的屬性。

對於載入需要載入外部檔案內容的停止字等情況，可通過為相關檔案建立`nt:file`類型的子節點來提供內容。

### 索爾指數 {#the-solr-index}

Solr索引的目的主要是全文搜索，但它也可以用於按路徑、屬性限制和主類型限制進行索引搜索。 這表示Oak中的Solr索引可用於任何類型的JCR查詢。

AEM中的整合會在存放庫層級進行，因此Solr是可用於Oak(AEM隨附的新存放庫實作)的其中一個可能索引。

可將其設定為以具有AEM例項的內嵌伺服器或遠端伺服器運作。

### 使用內嵌Solr伺服器設定AEM {#configuring-aem-with-an-embedded-solr-server}

>[!CAUTION]
>
>請勿在生產環境中使用內嵌的Solr伺服器。 此變數僅應用於開發環境。

AEM可與可透過Web主控台設定的內嵌Solr伺服器搭配使用。 在這種情況下，Solr伺服器將在與其嵌入的AEM實例相同的JVM中運行。

可以通過以下方式配置嵌入式Solr伺服器：

1. 前往`https://serveraddress:4502/system/console/configMgr`的Web主控台
1. 搜尋「**Oak Solr伺服器提供者**」。
1. 按下編輯按鈕，然後在下拉清單中的以下窗口中將伺服器類型設定為&#x200B;**嵌入式Solr**。

1. 接下來，編輯「**Oak Solr內嵌伺服器設定**」並建立設定。 有關配置選項的詳細資訊，請訪問[Apache Solr網站](https://lucene.apache.org/solr/documentation.html)。

   >[!NOTE]
   >
   >Solr主目錄(solr.home.path)配置將在AEM安裝資料夾中查找同名的資料夾。

1. 開啟CRXDE並以管理員身分登入。
1. 在&#x200B;**oak:index**&#x200B;下新增&#x200B;**** oak:QueryIndexDefinition **類型的**&#x200B;節點，其屬性如下：

   * **類型：** `solr`（類型為字串）
   * **async:** `async`（類型為字串）
   * **reindex:** `true`（類型為布林值）

1. 儲存變更。

### 使用單一遠端Solr伺服器設定AEM {#configuring-aem-with-a-single-remote-solr-server}

AEM也可以設定為與遠端Solr伺服器執行個體搭配使用：

1. 下載並解壓最新版本的Solr。 有關如何執行此操作的詳細資訊，請參閱[Apache Solr安裝文檔](https://cwiki.apache.org/confluence/display/solr/Installing+Solr)。
1. 現在，建立兩個索爾碎片。 您可以為已解壓縮Solr的資料夾中的每個共用建立資料夾，來執行此操作：

   * 對於第一個共用，建立資料夾：

   `<solrunpackdirectory>\aemsolr1\node1`

   * 對於第二個共用，建立資料夾：

   `<solrunpackdirectory>\aemsolr2\node2`

1. 在Solr包中找到示例實例。 它通常位於包根目錄中名為「`example`」的資料夾中。
1. 將以下資料夾從示例實例複製到兩個共用資料夾（`aemsolr1\node1`和`aemsolr2\node2`）:

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 在兩個共用資料夾中的每個資料夾中建立名為「 `cfg`」的新資料夾。
1. 將Solr和Zookeeper配置檔案放置在新建的`cfg`資料夾中。

   >[!NOTE]
   >
   >有關Solr和ZooKeeper配置的詳細資訊，請參閱[Solr配置文檔](https://wiki.apache.org/solr/ConfiguringSolr)和[ZooKeeper入門指南](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html)。

1. 前往`aemsolr1\node1`並執行下列命令，啟動支援ZooKeeper的第一個共用：

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 前往`aemsolr2\node2`並執行下列命令，以啟動第二個共用：

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 啟動兩個分片後，通過連接`http://localhost:8983/solr/#/`的Solr介面來測試所有元件是否都已啟動並運行
1. 啟動AEM並前往`http://localhost:4502/system/console/configMgr`的Web主控台
1. 在&#x200B;**Oak Solr遠端伺服器設定**&#x200B;下設定下列設定：

   * Sol HTTP URL:`http://localhost:8983/solr/`

1. 在&#x200B;**Oak Solr**&#x200B;伺服器提供者下拉式清單中，選擇&#x200B;**遠端Solr**。

1. 前往CRXDE並以管理員身分登入。
1. 在&#x200B;**oak:index**&#x200B;下建立名為&#x200B;**solrIndex**&#x200B;的新節點，並設定下列屬性：

   * **類型：** solr（類型為字串）
   * **async:** async（類型為字串）
   * **reindex:** true（類型為布林值）

1. 儲存變更。

#### Solr的建議配置 {#recommended-configuration-for-solr}

下面是基本配置的示例，可用於本文中描述的所有三個Solr部署。 它可容納AEM中已存在且不應與其他應用程式搭配使用的專用屬性索引。

為了正確使用它，您需要將存檔的內容直接放在Solr Home Directory中。 若是多節點部署，則應直接前往每個節點的根資料夾底下。

建議的Solr配置檔案

[取得檔案](assets/recommended-conf.zip)

### AEM索引工具 {#aem-indexing-tools}

AEM 6.1也整合了AEM 6.0中提供的兩種索引工具，作為Adobe諮詢服務公域工具集的一部分：

1. **說明查詢**，此工具旨在協助管理員了解查詢的執行方式；
1. **Oak Index Manager**，此Web使用者介面可維護現有索引。

您現在可以從AEM歡迎畫面前往&#x200B;**工具 — 作業 — 控制面板 — 診斷**，以存取這些變數。

有關如何使用它們的詳細資訊，請參閱[操作儀表板文檔](/help/sites-administering/operations-dashboard.md)。

#### 通過OSGi建立屬性索引 {#creating-property-indexes-via-osgi}

ACS Commons包還公開可用於建立屬性索引的OSGi配置。

您可以搜尋「**Ensure Oak Property Index**」，從Web主控台存取屬性。

![chlimage_1-150](assets/chlimage_1-150.png)

### 疑難排解索引問題 {#troubleshooting-indexing-issues}

查詢執行時間較長，且一般系統回應時間較慢的情況可能會出現。

本節提供一套建議，說明需要採取哪些措施來追蹤這些問題的原因，並就如何解決這些問題提供建議。

#### 準備分析的除錯資訊 {#preparing-debugging-info-for-analysis}

要獲取正在執行的查詢所需資訊，最簡單的方法是通過[Explain Query tool](/help/sites-administering/operations-dashboard.md#explain-query)。 這可讓您收集對慢速查詢進行偵錯所需的精確資訊，而無須查詢記錄層級資訊。 如果您知道要除錯的查詢，則這是理想的作法。

如果由於任何原因不可能，您可以在單一檔案中收集索引記錄，並使用它來疑難排解您的特定問題。

#### 啟用記錄 {#enable-logging}

若要啟用記錄，您必須針對與Oak索引和查詢相關的類別啟用&#x200B;**DEBUG**&#x200B;層級記錄。 這些類別包括：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

**com.day.cq.search**&#x200B;類別僅適用於使用AEM提供的QueryBuilder公用程式時。

>[!NOTE]
>
>請務必在您要疑難排解的查詢執行期間，將記錄檔設為DEBUG，否則隨著時間推移，記錄檔中將會產生大量事件。 因此，收集到所需記錄後，系統會針對上述類別切換回資訊層級記錄。

您可以依照以下程式啟用記錄：

1. 將瀏覽器指向`https://serveraddress:port/system/console/slinglog`
1. 按一下控制台下部的&#x200B;**添加新記錄器**&#x200B;按鈕。
1. 在新建立的列中，新增上述類別。 您可以使用&#x200B;**+**&#x200B;符號將多個類別新增至單一記錄器。
1. 從&#x200B;**日誌級別**&#x200B;下拉清單中選擇&#x200B;**DEBUG**。
1. 將輸出檔案設定為`logs/queryDebug.log`。 這會將所有除錯事件關聯至單一記錄檔。
1. 執行查詢或呈現使用您要除錯的查詢的頁面。
1. 執行查詢後，返回日誌控制台，並將新建記錄器的日誌級別更改為&#x200B;**INFO**。

#### 索引配置 {#index-configuration}

查詢的評估方式在很大程度上受索引配置的影響。 必須獲取索引配置，以便分析或發送給支援。 您可以以內容套件形式取得設定，或取得JSON轉譯。

由於在大多數情況下，索引設定會儲存在CRXDE的`/oak:index`節點下，因此您可以在取得JSON版本：

`https://serveraddress:port/oak:index.tidy.-1.json`

如果索引配置在不同的位置，請相應地更改路徑。

#### MBean輸出 {#mbean-output}

在某些情況下，提供索引相關MBean的輸出以進行偵錯會很有幫助。 您可以透過下列方式執行此作業：

1. 前往JMX控制台：
   `https://serveraddress:port/system/console/jmx`

1. 搜索以下MBean:

   * 盧塞內索引統計資訊
   * CopyOnRead支援統計資訊
   * Oak查詢統計資料
   * IndexStats

1. 按一下每個MBean以獲取效能統計資訊。 建立螢幕截圖或記下來，以備需要提交支援時使用。

您也可以在下列URL取得這些統計資料的JSON變體：

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

您也可以通過`https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`提供整合的JMX輸出。 這會包含JSON格式的所有Oak相關MBean詳細資訊。

#### 其他詳細資訊 {#other-details}

您可以收集其他詳細資訊，以協助疑難排解問題，例如：

1. 您執行個體執行的Oak版本。 您可以開啟CRXDE並查看歡迎頁面右下角的版本，或檢查`org.apache.jackrabbit.oak-core`套件組合的版本，即可看到此內容。
1. 麻煩查詢的QueryBuilder Debugger輸出。 除錯工具的存取位置：`https://serveraddress:port/libs/cq/search/content/querydebug.html`
