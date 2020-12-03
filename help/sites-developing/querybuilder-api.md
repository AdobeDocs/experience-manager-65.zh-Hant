---
title: Query Builder API
seo-title: Query Builder API
description: 「資產共用查詢產生器」的功能是透過Java API和REST API公開。
seo-description: 「資產共用查詢產生器」的功能是透過Java API和REST API公開。
uuid: 6928c3e9-96a1-44ad-9785-350d95f1869a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7965b7ef-dec4-441a-a012-daf1d60df0fb
pagetitle: Query Builder API
tagskeywords: querybuilder
translation-type: tm+mt
source-git-commit: a491d4e9bd9ffc68c4ba7cac3149f48cf7576ee8
workflow-type: tm+mt
source-wordcount: '2350'
ht-degree: 0%

---


# Query Builder API{#query-builder-api}

[資產共用查詢產生器](/help/assets/assets-finder-editor.md)的功能是透過Java API和REST API公開。 本節將說明這些API。

伺服器端查詢產生器([`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html))將接受查詢說明、建立並執行XPath查詢、選擇性篩選結果集，並視需要擷取刻面。

查詢說明只是一組謂語([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html))。 示例包括與XPath中的`jcr:contains()`函式相對應的全文謂語。

對於每個謂詞類型，都有一個求值器元件([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html))，它知道如何處理XPath、filtering和facet抽取的特定謂詞。 建立自訂評估程式非常簡單，這些評估程式會透過OSGi元件執行時期插入。

REST API可透過HTTP存取與JSON中傳送的回應完全相同的功能。

>[!NOTE]
>
>QueryBuilder API是使用JCR API建立。 您也可以在OSGi套件中使用JCR API來查詢Adobe Experience Manager JCR。 如需詳細資訊，請參閱「使用JCR API[查詢Adobe Experience Manager資料」。](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)

## Gem會話{#gem-session}

[AEM ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) Gemsis是Adobe專家針對Adobe Experience Manager提供的一系列技術深入探討。此專用於查詢產生器的作業對於概述和使用工具非常有用。

>[!NOTE]
>
>請參閱「AEM Gem工作階段[使用AEM查詢建立工具](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html)輕鬆搜尋表單」，以取得查詢建立工具的詳細概觀。

## 範例查詢{#sample-queries}

這些示例以Java屬性樣式表示法提供。 若要搭配Java API使用，請使用Java `HashMap`，如下面的API範例中所示。

對於`QueryBuilder` JSON Servlet，每個範例都包含本機CQ安裝的連結（位於預設位置`http://localhost:4502`）。 請注意，您必須先登入CQ例項，才能使用這些連結。

>[!CAUTION]
>
>依預設，查詢建立工具json servlet最多可顯示10次點擊。
>
>添加以下參數可讓servlet顯示所有查詢結果：
>
>**`p.limit=-1`**

>[!NOTE]
>
>若要在瀏覽器中檢視傳回的JSON資料，您可能想要使用外掛程式，例如JSONView for Firefox。

### 傳回所有結果{#returning-all-results}

下列查詢會&#x200B;**傳回10個結果**（或確切地說，最多10個），但會通知您實際可用的&#x200B;**點擊數：**:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

相同查詢（使用參數`p.limit=-1`）將&#x200B;**傳回所有結果**（這可能是高數字，視您的例項而定）:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### 使用p.guessTotal傳回結果{#using-p-guesstotal-to-return-the-results}

`p.guessTotal`參數的目的是傳回適當數目的結果，這些結果可透過結合最小可行的p.offset和p.limit值來顯示。 使用此參數的優點在於，對於大的結果集，其效能得到了改善。 如此可避免計算完整總計(例如呼叫result.getSize())並讀取整個結果集，一直最佳化至OAK引擎與索引。 當有100,000個結果時，這可能會有顯著差異，包括執行時間和記憶體使用。

此參數的缺點是使用者看不到確切總數。 但您可以設定最小數目，例如p.guessTotal=1000，如此一來，它永遠會讀取1000，因此您可以取得較小結果集的精確總計，但若超過此數目，您只能顯示「且更多」。

將`p.guessTotal=true`新增至以下查詢，以瞭解其運作方式：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

查詢將返回`p.limit`預設的`10`結果，並返回`0`偏移：

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

自AEM 6.0 SP2起，您也可以使用數值計算自訂的最大結果數。 使用與上述相同的查詢，但將`p.guessTotal`的值變更為`50`:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

它會傳回與預設值相同的10個結果上限，且0個偏移，但最多只會顯示50個結果：

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### 實作編頁{#implementing-pagination}

依預設，「查詢產生器」也會提供點擊數。 根據結果大小，由於確定準確計數需要檢查每個結果以瞭解訪問控制，因此可能需要很長的時間。 大部份的分頁總數都用來為使用者UI建置分頁。 當決定確切計數可能會變慢時，建議使用guessTotal功能來實作分頁。

例如，UI可以調整下列方法：

* 取得並顯示總點擊數的準確計數(SearchResult.getTotalMatches()[或querybuilder.json回應中的總計)小於或等於100;](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches)
* 在呼叫查詢產生器時，將`guessTotal`設為100。

* 回應可能會有下列結果：

   * `total=43`,  `more=false` -指出點擊總數為43。UI最多可顯示10個結果作為第一頁的一部分，並為接下來的3個頁面提供分頁。 您也可以使用此實作來顯示描述性文字，例如&#x200B;**&quot;43 results found&quot;**。
   * `total=100`,  `more=true` -指出點擊總數大於100，且未確認確切計數。UI最多可顯示10個頁面作為第一頁的一部分，並提供接下來10個頁面的編頁。 您也可以使用它來顯示文字，例如&#x200B;**「找到100個以上結果」**。 當使用者前往下一頁呼叫查詢產生器時，會增加`guessTotal`和`offset`參數的限制。`limit`

`guessTotal` 在UI需要使用無限捲動時，也應使用此功能，以避免「查詢產生器」決定確切的點擊計數。

### 尋找jar檔案並加以訂購，最新的前{#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### 尋找所有頁面並依上次修改的{#find-all-pages-and-order-them-by-last-modified}排序

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### 尋找所有頁面並依上次修改的順序排列，但遞減{#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc]`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### 全文搜尋，依分數{#fulltext-search-ordered-by-score}排序

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### 搜尋標籤有特定標籤{#search-for-pages-tagged-with-a-certain-tag}的頁面

「http://localhost:4502/bin/querybuilder.json?type=cq:Page&amp;tagid=marketing:interest/product&amp;tagid.property=jcr:content/cq:tags」

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

如果您知道顯式標籤ID，請使用`tagid`謂語，如範例中所述。

對標籤標題路徑使用`tag`謂語（不含空格）。

因為，在上例中，您正在搜索頁（`cq:Page`節點），因此，您需要為`tagid.property`謂語使用該節點的相對路徑，該謂語為`jcr:content/cq:tags`。 依預設，`tagid.property`將會是`cq:tags`。

### 在多個路徑下進行搜索（使用組）{#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

此查詢使用&#x200B;*group*（名為&quot; `group`&quot;），它的作用是在查詢中分隔子表達式，就像括弧在更標準的標注中所做的那樣。 例如，上一個查詢可能以更熟悉的樣式表示為：

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

在範例中的群組內，`path`謂語被多次使用。 要區分並排序謂語的兩個實例（某些謂語需要排序），您必須在謂語前置詞&#x200B;*N*`_ where`*N*&#x200B;為排序索引。 在上例中，產生的謂語是`1_path`和`2_path`。

`p.or`中的`p`是一個特殊分隔字元，指示如下內容（在本例中為`or`）是群組的&#x200B;*參數*，而不是群組的子謂詞，如`1_path`。

如果未給定`p.or`，則所有謂語都是ANDed，即每個結果必須滿足所有謂語。

>[!NOTE]
>
>您不能在單一查詢中使用相同的數值前置詞，即使對於不同的謂語也是如此。

### 搜索屬性{#search-for-properties}

在此，您使用`cq:template`屬性搜索給定模板的所有頁：

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

這有一個缺點：返回頁面的`jcr:content`節點，而不是頁面本身。 要解決此問題，可以按相對路徑搜索：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### 搜索多個屬性{#search-for-multiple-properties}

多次使用屬性謂語時，必須再次添加數字前置詞：

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### 搜索多個屬性值{#search-for-multiple-property-values}

要避免在搜索屬性(`"A" or "B" or "C"`)的多個值時出現大組，可以為`property`謂語提供多個值：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

對於多值屬性，您也可以要求多個值符合(`"A" and "B" and "C"`):

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## 調整返回內容{#refining-what-is-returned}

依預設，QueryBuilder JSON Servlet會傳回搜尋結果中每個節點的預設屬性集（例如路徑、名稱、標題等）。 若要控制要傳回的屬性，您可以執行下列其中一項作業：

指定

```
p.hits=full
```

在這種情況下，每個節點將包含所有屬性：

`http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
```

使用

```
p.hits=selective
```

並指定您要加入的屬性

```
p.properties
```

以空格分隔：

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[ `http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle) [p.hits=selective&amp;](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.nodedepth=5&amp;p.properties=sling%3aresourceType%20jcr%3apath&amp;property=jcr%3atitle&amp;property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

您可以做的另一件事，是在QueryBuilder回應中包含子節點。 若要這麼做，您必須指定

```
p.nodedepth=n
```

其中`n`是您希望查詢返回的層數。 請注意，要返回子節點，必須由屬性選擇器指定

```
p.hits=full
```

範例:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
p.nodedepth=5
```

## 更多謂語{#morepredicates}

如需更多謂語，請參閱[Query Builder Predicate Reference頁面](/help/sites-developing/querybuilder-predicate-reference.md)。

您也可以檢查`PredicateEvaluator`類](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)的[Javadoc。 這些類的Javadoc包含可使用的屬性清單。

類名的前置詞（例如[`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)中的&quot; `similar`&quot;）是類的&#x200B;*主屬性*。 此屬性也是要在查詢中使用的謂詞的名稱（在小寫中）。

對於這些主體屬性，您可以縮短查詢並使用&quot; `similar=/content/en`&quot;，而不是完全限定的變型&quot; `similar.similar=/content/en`&quot;。 完全限定的表單必須用於類的所有非主屬性。

## 查詢建立工具API使用範例{#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "Geometrixx";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory =     DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

>[!NOTE]
>
>如要瞭解如何建立使用QueryBuilder API的OSGi套件，並在Adobe Experience Manager應用程式內使用該OSGi套件，請參閱「建立使用Query Builder AP[I的Adobe CQ OSGi套件」。](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)

使用查詢產生器(JSON)Servlet在HTTP上執行的相同查詢：

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## 儲存和載入查詢{#storing-and-loading-queries}

查詢可以儲存到儲存庫，以便您以後可以使用它們。 `QueryBuilder`提供&quot;`storeQuery`方法及下列簽名：

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

使用[ `QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession)方法時，給定的`Query`將作為檔案或屬性儲存到儲存庫中，並根據`createFile`參數值。 以下示例說明如何將`Query`保存到路徑`/mypath/getfiles`作為檔案：

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

使用[`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession)方法，可以從儲存庫載入任何以前儲存的查詢：

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

例如，儲存至路徑`/mypath/getfiles`的`Query`可由下列程式碼片段載入：

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## 測試與除錯{#testing-and-debugging}

若要播放和除錯查詢建立工具查詢，您可以使用QueryBuilder除錯控制台，位於

`http://localhost:4502/libs/cq/search/content/querydebug.html`

或查詢建立工具json servlet或

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

（`path=/tmp`僅為範例）。

### 一般除錯建議{#general-debugging-recommendations}

### 通過記錄{#obtain-explain-able-xpath-via-logging}獲取可解釋的XPath

針對目標索引集說明開發週期中的&#x200B;**all**&#x200B;查詢。

* 啟用QueryBuilder的DEBUG記錄檔，以取得基礎、可解釋的XPath查詢

   * 導覽至https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog。 在&#x200B;**DEBUG**&#x200B;建立`com.day.cq.search.impl.builder.QueryImpl`的新記錄器。

* 對上述類啟用DEBUG後，記錄檔將顯示Query Builder產生的XPath。
* 從相關QueryBuilder查詢的記錄項目複製XPath查詢，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 將XPath查詢貼上到[Explain Query](/help/sites-administering/operations-dashboard.md#explain-query)中，作為XPath獲得查詢計畫

### 透過Query Builder除錯程式{#obtain-explain-able-xpath-via-the-query-builder-debugger}取得可解釋的XPath

* 使用AEM QueryBuilder除錯程式產生可解釋的XPath查詢：

針對目標索引集說明開發週期中的&#x200B;**all**&#x200B;查詢。

**通過日誌獲取可解釋的XPath**

* 啟用QueryBuilder的DEBUG記錄檔，以取得基礎、可解釋的XPath查詢

   * 導覽至https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog。 在&#x200B;**DEBUG**&#x200B;建立`com.day.cq.search.impl.builder.QueryImpl`的新記錄器。

* 對上述類啟用DEBUG後，記錄檔將顯示Query Builder產生的XPath。
* 從相關QueryBuilder查詢的記錄項目複製XPath查詢，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 將XPath查詢貼上到[Explain Query](/help/sites-administering/operations-dashboard.md#explain-query)中作為XPath以獲取查詢計畫

**透過Query Builder除錯程式取得可解釋的XPath**

* 使用AEM QueryBuilder除錯程式產生可解釋的XPath查詢：

![chlimage_1-66](assets/chlimage_1-66a.png)

1. 在Query Builder除錯程式中提供查詢建立工具查詢
1. 執行搜尋
1. 獲取生成的XPath
1. 將XPath查詢貼上到Explain Query as XPath以獲取查詢計畫

>[!NOTE]
>
>可以直接提供非querybuilder查詢(XPath、JCR-SQL2)給「說明查詢」。

如需如何使用QueryBuilder除錯查詢的執行階段，請參閱以下影片。

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## 使用記錄{#debugging-queries-with-logging}調試查詢

>[!NOTE]
>
>[建立您自己的記錄程式和寫入程式](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers)部分介紹了記錄程式的配置。

執行「測試與除錯」中所述之查詢時，查詢產生器實作的記錄檔輸出（INFO層級）:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

如果您有使用謂詞求值器進行篩選的查詢，或使用由比較器進行的自定義順序，查詢中也會注意到：

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Javadoc連結{#javadoc-links}

| **Javadoc** | **說明** |
|---|---|
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | 基本QueryBuilder和Query API |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | 結果API |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | 刻面 |
| [com.day.cq.search.facets.burkets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | 桶（包含在小平面中） |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | Predicate Evaluators |
| [com.day.cq.search.facets.extrovers](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Facet擷取器（用於評估器） |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | Querybuilder servlet的JSON結果點擊寫入器(/bin/querybuilder.json) |

