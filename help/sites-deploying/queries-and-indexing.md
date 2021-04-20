---
title: Oak查詢和索引
seo-title: Oak查詢和索引
description: 瞭解如何在中配置索引AEM。
seo-description: 瞭解如何在中配置索引AEM。
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2881'
ht-degree: 0%

---


# Oak Queries and Indexing{#oak-queries-and-indexing}

>[!NOTE]
>
>本文的內容是在AEM6中配置索引。 有關優化查詢和索引效能的最佳實踐，請參見[查詢和索引的最佳實踐](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

## 簡介 {#introduction}

與Jackrabbit 2不同，Oak預設不會為內容建立索引。 自訂索引需要在需要時建立，就像使用傳統的關聯式資料庫。 如果沒有特定查詢的索引，則可能會遍歷許多節點。 查詢可能仍然有效，但可能非常慢。

如果Oak遇到沒有索引的查詢，則會列印WARN級別的記錄訊息：

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## 支援的查詢語言{#supported-query-languages}

Oak查詢引擎支援下列語言：

* XPath（建議）
* SQL-2
* SQL（不建議使用）
* JQOM

## 索引器類型和成本計算{#indexer-types-and-cost-calculation}

基於Apache Oak的後端允許將不同的索引器插入儲存庫。

一個索引器是&#x200B;**屬性索引**，其索引定義儲存在儲存庫本身中。

預設情況下，**Apache Lucene**&#x200B;和&#x200B;**Solr**&#x200B;的實現也可用，這兩種實現都支援全文索引。

如果沒有其他索引器可用，則使用&#x200B;**遍歷索引**。 這表示未對內容建立索引，並且會遍歷內容節點以查找與查詢的匹配項。

如果一個查詢有多個索引器，則每個可用索引器估計執行查詢的成本。 然後，Oak以最低的估計成本選擇索引器。

![chlimage_1-148](assets/chlimage_1-148.png)

上圖是Apache Oak查詢執行機制的高級表示。

首先，將查詢解析為抽象語法樹。 然後，將查詢檢查並轉換為SQL-2,SQL-2是Oak查詢的原生語言。

接著，參考每個索引來估計查詢的成本。 一旦完成，就會擷取最便宜的指數結果。 最後，篩選結果，以確保當前用戶具有對結果的讀取訪問權，並確保結果與完整查詢匹配。

## 配置索引{#configuring-the-indexes}

>[!NOTE]
>
>對於大型儲存庫，建立索引是一項耗時的操作。 對於索引的初始建立和重新編製索引（在更改定義後重建索引）都是如此。 另請參閱[疑難排解Oak索引](/help/sites-deploying/troubleshooting-oak-indexes.md)和[防止慢速重新索引](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing)。

如果在非常大的儲存庫中需要重新編製索引，特別是在使用MongoDB和對全文索引時，請考慮文本預抽取，並使用oak-run構建初始索引和重新編製索引。

索引在&#x200B;**oak:index**&#x200B;節點下配置為儲存庫中的節點。

索引節點的類型必須為&#x200B;**oak:QueryIndexDefinition。** 對於每個索引器，有幾個配置選項作為節點屬性。如需詳細資訊，請參閱下方每個索引器類型的設定詳細資訊。

### 屬性索引{#the-property-index}

屬性索引通常適用於具有屬性約束但非全文的查詢。 它可依下列程式進行設定：

1. 轉至`http://localhost:4502/crx/de/index.jsp`以開啟CRXDE
1. 在&#x200B;**oak:index**&#x200B;下建立新節點
1. 將節點命名為&#x200B;**PropertyIndex**，並將節點類型設定為&#x200B;**oak:QueryIndexDefinition**
1. 為新節點設定以下屬性：

   * **type:**  `property` （類型為字串）
   * **propertyNames:**  `jcr:uuid` (of type Name)

   此特定示例將為`jcr:uuid`屬性編製索引，其作業是公開其所連接節點的通用唯一標識符(UUID)。

1. 儲存變更。

屬性索引具有以下配置選項：

* **type**&#x200B;屬性將指定索引類型，在此例中，必須將其設為&#x200B;**property**

* **propertyNames**&#x200B;屬性指示將儲存在索引中的屬性清單。 如果缺少，則節點名稱將用作屬性名稱引用值。 在此示例中，**jcr:uuid**&#x200B;屬性將添加到索引中，其作業是公開其節點的唯一標識符(UUID)。

* 如果設定為&#x200B;**true**，則&#x200B;**unique**&#x200B;標籤會在屬性索引上添加唯一性約束。

* **arclibingNodeTypes**&#x200B;屬性允許您指定索引將僅應用於的特定節點類型。
* 如果設為&#x200B;**true**，則&#x200B;**reindex**&#x200B;標幟將觸發完整內容重新索引。

### 有序索引{#the-ordered-index}

Ordered索引是屬性索引的擴展。 不過，它已過時。 此類型的索引需要替換為[Lucene屬性索引](#the-lucene-property-index)。

### Lucene全文索引{#the-lucene-full-text-index}

6.提供了基於Apache Lucene的全文索引器AEM。

如果配置了全文索引，則所有具有全文條件的查詢都使用全文索引，無論是否有其他條件已編製索引，也無論是否存在路徑限制。

如果未配置全文索引，則具有全文條件的查詢將無法如預期般運作。

由於索引是透過不同步的背景執行緒來更新，因此在一小段時間內，部分全文搜尋將無法使用，直到背景處理完成為止。

您可以按照以下過程配置Lucene全文索引：

1. 開啟CRXDE並在&#x200B;**oak:index**&#x200B;下建立新節點。
1. 將節點命名為&#x200B;**LuceneIndex**，並將節點類型設定為&#x200B;**oak:QueryIndexDefinition**
1. 將以下屬性添加到節點：

   * **type:**  `lucene` （類型為字串）
   * **async:**  `async` （字串類型）

1. 儲存變更。

Lucene Index具有以下配置選項：

* 將指定索引類型的&#x200B;**type**&#x200B;屬性必須設為&#x200B;**lucene**
* **async**&#x200B;屬性，必須設為&#x200B;**async**。 這會將索引更新程式發送到後台線程。
* **includePropertyTypes**&#x200B;屬性，可定義索引中將包含哪些屬性類型子集。
* **excludePropertyNames**&#x200B;屬性，它將定義屬性名稱的清單——應從索引中排除的屬性。
* 當設為&#x200B;**true**&#x200B;時，**reindex**&#x200B;標幟會觸發完整內容重新索引。

### Lucene屬性索引{#the-lucene-property-index}

由於&#x200B;**Oak 1.0.8**，因此Lucene可用來建立包含非全文的屬性約束的索引。

為了實現Lucene屬性索引，**fulltextEnabled**&#x200B;屬性必須始終設定為false。

以下列查詢為例：

```xml
select * from [nt:base] where [alias] = '/admin'
```

為了為上述查詢定義Lucene屬性索引，可通過在&#x200B;**oak:index:**&#x200B;下建立新節點來添加以下定義

* **名稱：** `LucenePropertyIndex`
* **類型：** `oak:QueryIndexDefinition`

建立節點後，添加以下屬性：

* **類型:**

   ```
   lucene (of type String)
   ```

* **非同步處理:**

   ```
   async (of type String)
   ```

* **fulltextEnabled:**

   ```
   false (of type Boolean)
   ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>與常規屬性索引相比，Lucene屬性索引始終以非同步模式配置。 因此，索引返回的結果不一定總是反映儲存庫的最新狀態。

>[!NOTE]
>
>有關Lucene屬性索引的更多特定資訊，請參閱[Apache Jackrabbit Oak Lucene檔案頁面](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### Lucene Analyzers {#lucene-analyzers}

自1.2.0版起，Oak支援Lucene分析器。

分析器在建立檔案索引時和在查詢時都使用。 分析器會檢查欄位文字並產生代號串流。 Lucene分析器由一系列的Tokenizer和過濾器類組成。

分析器可通過`oak:index`定義內的`analyzers`節點（類型`nt:unstructured`）進行配置。

索引的預設分析器配置在分析器節點的`default`子項中。

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>如需可用分析器的清單，請參閱您所使用之Lucene版本的API檔案。

#### 直接指定Analyzer類{#specifying-the-analyzer-class-directly}

如果希望使用任何現成可用的分析器，可以按照以下過程進行配置：

1. 在`oak:index`節點下找到要使用Analyzer的索引。

1. 在索引下，建立名為`default`的子節點，該子節點類型為`nt:unstructured`。

1. 使用以下屬性將屬性添加到預設節點：

   * **名稱：** `class`
   * **類型：** `String`
   * **值：** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   該值是您要使用的分析器類的名稱。

   您也可以使用可選的`luceneMatchVersion`字串屬性，將分析器與特定lucene版本一起使用。 與Lucene 4.7搭配使用的有效合成產品為：

   * **名稱：** `luceneMatchVersion`
   * **類型：** `String`
   * **值：** `LUCENE_47`

   如果未提供`luceneMatchVersion`,Oak將使用隨附的Lucene版本。

1. 如果要向Analyzer配置中添加stopwords檔案，可以在`default`配置下建立一個具有以下屬性的新節點：

   * **名稱：** `stopwords`
   * **類型：** `nt:file`

#### 透過構圖建立分析器{#creating-analyzers-via-composition}

分析器也可以基於`Tokenizers`、`TokenFilters`和`CharFilters`來構成。 通過指定分析器並建立其可選令牌和篩選器的子節點（按清單順序應用），可以執行此操作。 另請參閱[https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

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





篩選器、charFilters和Tokenizers的名稱是透過移除工廠字尾來形成的。 因此：

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` becomes  `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` becomes  `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` becomes  `Stop`

工廠所需的任何配置參數都指定為相關代碼的屬性。

例如，如果需要載入來自外部檔案的內容的停止字詞，則可為相關檔案建立`nt:file`類型的子節點來提供內容。

### 索爾指數{#the-solr-index}

Solr索引的目的主要是全文搜索，但也可以用於按路徑、屬性限制和主要類型限制進行索引搜索。 這表示Oak中的Solr索引可用於任何類型的JCR查詢。

中的集AEM成在儲存庫級別進行，因此Solr是可用於Oak（隨附的新儲存庫實施）的可能索引之一AEM。

它可配置為與實例一起使用的嵌入式伺服器AEM，或作為遠程伺服器。

### 使用AEM嵌入式Solr伺服器{#configuring-aem-with-an-embedded-solr-server}進行配置

>[!CAUTION]
>
>請勿在生產環境中使用內嵌的Solr伺服器。 它只應用於開發環境。

可AEM以與可通過Web控制台配置的嵌入式Solr伺服器一起使用。 在這種情況下，Solr伺服器將在與其嵌入的實例相同的AEMJVM中運行。

通過以下方式，可以配置嵌入式Solr伺服器：

1. 前往`https://serveraddress:4502/system/console/configMgr`的Web控制台
1. 搜索「**Oak Solr伺服器提供商**」。
1. 按下編輯按鈕，然後在下列視窗中，將下拉式清單中的伺服器類型設定為&#x200B;**內嵌Solr**。

1. 接著，編輯「**Oak Solr嵌入式伺服器配置**」並建立配置。 有關配置選項的詳細資訊，請訪問[Apache Solr網站](https://lucene.apache.org/solr/documentation.html)。

   >[!NOTE]
   >
   >Solr主目錄(solr.home.path)配置將在安裝資料夾中查找同名的AEM資料夾。

1. 開啟CRXDE並以管理員身分登入。
1. 在&#x200B;**oak:index**&#x200B;下新增&#x200B;**sollndex**&#x200B;類型&#x200B;**oak:QueryIndexDefinition**&#x200B;的節點，其屬性如下：

   * **type:** `solr`（類型為字串）
   * **async:** `async`（字串類型）
   * **reindex:** `true`(of type boolean)

1. 儲存變更。

### 使用AEM單個遠程Solr伺服器{#configuring-aem-with-a-single-remote-solr-server}進行配置

還可AEM以配置為與遠程Solr伺服器實例一起使用：

1. 下載並摘取最新版Solr。 有關如何執行此操作的詳細資訊，請參閱[Apache Solr安裝文檔](https://cwiki.apache.org/confluence/display/solr/Installing+Solr)。
1. 現在，建立兩個索爾碎片。 通過為Solr已備份的資料夾中的每個分片建立資料夾，可以執行此操作：

   * 對於第一個分片，請建立資料夾：

   `<solrunpackdirectory>\aemsolr1\node1`

   * 對於第二個分片，請建立資料夾：

   `<solrunpackdirectory>\aemsolr2\node2`

1. 在Solr包中找到示例實例。 它通常位於軟體包根目錄中名為&quot; `example`&quot;的資料夾中。
1. 將以下資料夾從示例實例複製到兩個共用資料夾（`aemsolr1\node1`和`aemsolr2\node2`）:

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 在兩個分片資料夾中，分別建立一個名為&quot; `cfg`&quot;的新資料夾。
1. 將Solr和Zookeeper配置檔案放在新建立的`cfg`資料夾中。

   >[!NOTE]
   >
   >有關Solr和ZooKeeper配置的詳細資訊，請參閱[Solr配置文檔](https://wiki.apache.org/solr/ConfiguringSolr)和[ZooKeeper入門指南](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html)。

1. 前往`aemsolr1\node1`並執行下列命令，即可啟動第一個具有ZooKeeper支援的分區：

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 前往`aemsolr2\node2`並執行下列命令，以啟動第二個分片：

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 啟動兩個分片後，通過連接到`http://localhost:8983/solr/#/`的Solr介面來測試所有分片都已啟動並運行
1. 啟AEM動並轉至`http://localhost:4502/system/console/configMgr`的Web控制台
1. 在&#x200B;**Oak Solr遠程伺服器配置**&#x200B;下設定以下配置：

   * Solr HTTP URL:`http://localhost:8983/solr/`

1. 在&#x200B;**Oak Solr**&#x200B;伺服器供應商下方的下拉式清單中，選擇&#x200B;**遠端Solr**。

1. 前往CRXDE，以管理員身分登入。
1. 在&#x200B;**oak:index**&#x200B;下建立名為&#x200B;**solrIndex**&#x200B;的新節點，並設定以下屬性：

   * **type:** solr（類型為字串）
   * **async:** async（字串類型）
   * **reindex:** true（類型為布林）

1. 儲存變更。

#### Solr {#recommended-configuration-for-solr}的建議配置

下面是基本配置的示例，可用於本文中描述的所有三種Solr部署。 它包含已存在且不應用於其AEM他應用程式的專用屬性索引。

為了正確使用它，您需要將存檔的內容直接放在Solr Home Directory中。 如果是多節點部署，則應直接位於每個節點的根資料夾下。

建議的Solr配置檔案

[取得檔案](assets/recommended-conf.zip)

### 索AEM引工具{#aem-indexing-tools}

AEM6.1還整合了6.0中提供的AEM兩種索引工具，作為Adobe咨詢服務公域工具集的一部分：

1. **Explain Query**，這項工具旨在幫助管理員瞭解如何執行查詢；
1. **Oak Index Manager**，用於維護現有索引的Web用戶介面。

您現在可以從「歡迎」畫面前往&#x200B;**工具——作業——儀表板——診斷**，以取AEM得。

有關如何使用它們的詳細資訊，請參閱[操作儀表板文檔](/help/sites-administering/operations-dashboard.md)。

#### 通過OSGi {#creating-property-indexes-via-osgi}建立屬性索引

ACS Commons軟體包還公開了可用於建立屬性索引的OSGi配置。

您可以從Web主控台中搜尋「**Ensure Oak Property Index**」來存取它。

![chlimage_1-150](assets/chlimage_1-150.png)

### 索引問題疑難排解{#troubleshooting-indexing-issues}

出現查詢執行時間較長，且一般系統響應時間較慢的情況。

本節就需要採取哪些行動來追蹤這些問題的原因提出一組建議，並就如何解決這些問題提出建議。

#### 準備分析的調試資訊{#preparing-debugging-info-for-analysis}

要獲取正在執行的查詢所需資訊，最簡單的方法是通過[解釋查詢工具](/help/sites-administering/operations-dashboard.md#explain-query)。 這可讓您收集需要的精確資訊，以除錯慢速查詢，而不需查詢記錄檔層級資訊。 如果您知道要除錯的查詢，這是可取的。

如果由於任何原因無法做到這一點，您可以在單一檔案中收集索引記錄檔，並使用它來疑難排解您的特定問題。

#### 啟用記錄{#enable-logging}

若要啟用記錄功能，您必須針對與Oak索引和查詢相關的類別啟用&#x200B;**DEBUG**&#x200B;層級記錄檔。 這些類別包括：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

**com.day.cq.search**&#x200B;類別僅適用於您使用提供的QueryBuilder公用程AEM式時。

>[!NOTE]
>
>請務必在執行您要疑難排解的查詢期間，將記錄檔設為DEBUG，否則日誌中會隨著時間產生大量事件。 因此，在收集到所需記錄檔後，請切換回上述類別的INFO層級記錄檔。

您可以按照以下過程啟用記錄：

1. 將瀏覽器指向`https://serveraddress:port/system/console/slinglog`
1. 按一下控制台下部的&#x200B;**Add new Logger**&#x200B;按鈕。
1. 在新建立的行中，添加上述類別。 您可以使用&#x200B;**+**&#x200B;符號，將多個類別新增至單一記錄器。
1. 從&#x200B;**日誌級別**&#x200B;下拉清單中選擇&#x200B;**DEBUG**。
1. 將輸出檔案設定為`logs/queryDebug.log`。 這會將所有DEBUG事件關聯至單一記錄檔。
1. 執行查詢或演算使用您要除錯之查詢的頁面。
1. 執行查詢後，返回日誌控制台，並將新建立的日誌程式的日誌級別更改為&#x200B;**INFO**。

#### 索引配置{#index-configuration}

查詢的評估方式在很大程度上受索引配置的影響。 為了分析或發送給支援，必須獲取索引配置。 您可以以內容套件的形式取得設定，或取得JSON轉譯。

由於在大多數情況下，索引設定會儲存在CRXDE的`/oak:index`節點下，因此您可以在以下網址取得JSON版本：

`https://serveraddress:port/oak:index.tidy.-1.json`

如果索引配置在不同的位置，請相應地更改路徑。

#### MBean輸出{#mbean-output}

在某些情況下，提供索引相關MBean的輸出有助於調試。 您可以透過下列方式執行此動作：

1. 前往JMX主控台，網址為：
   `https://serveraddress:port/system/console/jmx`

1. 搜尋下列MBean:

   * Lucene指數統計
   * CopyOnRead支援統計資料
   * Oak查詢統計
   * IndexStats

1. 按一下每個MBean以獲取效能統計資訊。 建立螢幕擷取或記下畫面，以備需要提交支援時使用。

您也可以在下列URL取得這些統計資料的JSON變體：

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

您也可以透過`https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`提供整合的JMX輸出。 這將包含所有JSON格式的Oak相關MBean詳細資訊。

#### 其他詳細資訊{#other-details}

您可以收集其他詳細資訊以協助疑難排解問題，例如：

1. 您的例項正在執行的Oak版本。 您可以開啟CRXDE並檢視歡迎頁面右下角的版本，或檢查`org.apache.jackrabbit.oak-core`套件的版本，以瞭解此點。
1. 麻煩查詢的QueryBuilder除錯器輸出。 除錯程式可從以下網址存取：`https://serveraddress:port/libs/cq/search/content/querydebug.html`

