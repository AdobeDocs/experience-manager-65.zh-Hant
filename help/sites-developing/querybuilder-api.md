---
title: 查詢產生器 API
seo-title: 查詢產生器 API
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
exl-id: b2288442-d055-4966-8057-8b7b7b6bff28
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 0%

---

# 查詢產生器 API{#query-builder-api}

[資產共用查詢產生器](/help/assets/assets-finder-editor.md)的功能透過Java API和REST API公開。 本節將說明這些API。

伺服器端查詢產生器([`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html))將接受查詢說明、建立並執行XPath查詢、選擇性篩選結果集，並視需要擷取Facet。

查詢說明只是一組謂語([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html))。 例如，全文謂語，與XPath中的`jcr:contains()`函式對應。

對於每個謂語類型，都有一個求值器元件([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html))，它知道如何處理XPath、篩選和面向提取的特定謂語。 很容易建立自訂評估程式，這些評估程式會透過OSGi元件執行階段插入。

REST API可透過HTTP存取完全相同的功能，並在JSON中傳送回應。

>[!NOTE]
>
>QueryBuilder API是使用JCR API建置而成。 您也可以從OSGi套件組合內使用JCR API來查詢Adobe Experience Manager JCR。 如需詳細資訊，請參閱[使用JCR API](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)查詢Adobe Experience Manager資料。

## Gem會話{#gem-session}

[AEM ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) GemsisAdobe專家對Adobe Experience Manager進行了一系列技術深入探討。此查詢產生器專用的工作階段對於概述和使用工具非常有用。

>[!NOTE]
>
>如需查詢產生器的詳細概覽，請參閱AEM Gem工作階段[使用AEM查詢產生器輕鬆搜尋表單。](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html)

## 範例查詢{#sample-queries}

這些範例會以Java屬性樣式標籤法提供。 若要與Java API搭配使用，請使用Java `HashMap`，如以下API範例所示。

對於`QueryBuilder` JSON Servlet，每個範例都包含本機CQ安裝的連結（位於預設位置`http://localhost:4502`）。 請注意，您必須先登入CQ例項，才能使用這些連結。

>[!CAUTION]
>
>依預設，查詢產生器json servlet最多可顯示10個點擊。
>
>新增下列參數可讓servlet顯示所有查詢結果：
>
>**`p.limit=-1`**

>[!NOTE]
>
>若要在瀏覽器中檢視傳回的JSON資料，您可能想使用外掛程式，例如Firefox的JSONView。

### 返回所有結果{#returning-all-results}

下列查詢會&#x200B;**傳回10個結果**（或精確為最多10個），但會通知您實際可用的&#x200B;**點擊數：**:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

相同的查詢（參數為`p.limit=-1`）將&#x200B;**傳回所有結果**（根據您的例項，這可能是高數字）:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### 使用p.guessTotal返回結果{#using-p-guesstotal-to-return-the-results}

`p.guessTotal`參數的目的是返回通過組合最小可行p.offset值和p.limit值可以顯示的適當數目的結果。 在大結果集下，使用該參數的優點是提高了效能。 如此可避免計算完整總計(例如呼叫result.getSize())並讀取整個結果集，最佳化至OAK引擎和索引。 當結果達10萬個時，這可能會有顯著差異，包括執行時間和記憶體使用量。

參數的缺點是使用者看不到確切的總計。 但您可以設定一個最小數字，例如p.guessTotal=1000，這樣一來，它就一律可讀取到1000，這樣您就能得到較小結果集的確切總數，但如果數字大於此值，您只能顯示「且更多」。

將`p.guessTotal=true`新增至下列查詢，以了解其運作方式：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

查詢會傳回`p.limit`預設值`10`結果，並帶有`0`偏移：

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

自AEM 6.0 SP2起，您也可以使用數值來計算最多自訂的最大結果數。 使用與上面相同的查詢，但將`p.guessTotal`的值變更為`50`:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

它會傳回與10個結果相同的預設限制數，但偏移為0，但最多只顯示50個結果：

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### 實作分頁{#implementing-pagination}

依預設，查詢產生器也會提供點擊數。 根據結果大小，確定準確計數可能需要花很長時間，因為需要檢查每個結果以進行訪問控制。 大多數情況下，會使用總計來為使用者UI實作分頁。 由於判斷確切計數可能會很慢，因此建議使用guessTotal功能來實作分頁。

例如，UI可調整下列方法：

* 取得並顯示點擊總數([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches)或querybuilder.json回應中的總計)的精確計數小於或等於100;
* 呼叫查詢產生器時，將`guessTotal`設為100。

* 回應可能會有下列結果：

   * `total=43`,  `more=false`  — 指出點擊總數為43次。UI最多可在第一個頁面中顯示10個結果，並提供後續3個頁面的分頁。 您也可以使用此實施來顯示描述性文字，例如&#x200B;**&quot;43 results found&quot;**。
   * `total=100`,  `more=true`  — 指出點擊總數大於100，且未知確切計數。UI最多可在第一頁中顯示10個頁面，並提供後續10個頁面的分頁。 您也可以使用它來顯示文字，例如&#x200B;**&quot;超過100個結果找到&quot;**。 當使用者前往對查詢產生器進行的後續頁面呼叫時，會增加`guessTotal`以及`offset`和`limit`參數的限制。

`guessTotal` 當UI需要使用無限捲動時，也應使用，以避免查詢產生器決定確切的點擊計數。

### 查找jar檔案並訂購它們，最新的前{#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### 查找所有頁，並按上次修改的{#find-all-pages-and-order-them-by-last-modified}排序

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### 查找所有頁面，並按上次修改的順序排序，但降序{#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc]`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### 全文搜索，按分數{#fulltext-search-ordered-by-score}排序

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### 搜尋標籤有特定{#search-for-pages-tagged-with-a-certain-tag}標籤的頁面

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&tagid=marketing:interest/product&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

如果您知道明確標籤ID，請使用`tagid`述詞，如範例所示。

使用`tag`述詞作為標籤標題路徑（不含空格）。

因為在上例中，您正在搜索頁（`cq:Page`節點），因此需要使用該節點的相對路徑作為`tagid.property`謂語，該謂語為`jcr:content/cq:tags`。 預設情況下，`tagid.property`將僅為`cq:tags`。

### 在多個路徑下搜尋（使用群組）{#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

此查詢使用&#x200B;*group*（名為&quot; `group`&quot;），其作用是在查詢內分隔子運算式，正如括弧在更標準的句號中所做的那樣。 例如，上一個查詢可能以更熟悉的樣式表示，如下：

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

在範例的群組內，使用了多次`path`述詞。 要區分並排序謂語的兩個實例（某些謂語需要排序），您必須將謂語的前置詞為&#x200B;*N* `_ where`*N*&#x200B;作為排序索引。 在上例中，產生的謂語是`1_path`和`2_path`。

`p.or`中的`p`是表示以下內容（在本例中為`or`）是組的&#x200B;*參數*&#x200B;的特殊分隔符，而不是組的子謂詞，如`1_path`。

如果未給定`p.or` ，則所有謂語都是ANDed，即每個結果必須滿足所有謂語。

>[!NOTE]
>
>您無法在單一查詢中使用相同的數值首碼，即使對不同謂語亦然。

### 搜索屬性{#search-for-properties}

在此處，您使用`cq:template`屬性來搜尋指定範本的所有頁面：

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

這有一個缺點，即會傳回頁面的`jcr:content`節點，而非頁面本身。 要解決此問題，可以按相對路徑進行搜索：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### 搜索多個屬性{#search-for-multiple-properties}

當多次使用屬性述詞時，您必須再次新增數字前置詞：

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### 搜索多個屬性值{#search-for-multiple-property-values}

若要避免在您要搜尋屬性的多個值(`"A" or "B" or "C"`)時出現大型群組，您可以為`property`述詞提供多個值：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

對於多值屬性，您也可以要求多個值相符(`"A" and "B" and "C"`):

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## 精簡傳回的{#refining-what-is-returned}

依預設，QueryBuilder JSON Servlet會針對搜尋結果中的每個節點（例如路徑、名稱、標題等）傳回一組預設屬性。 若要控制要傳回的屬性，您可以執行下列其中一項操作：

指定

```
p.hits=full
```

在這種情況下，每個節點都會包含所有屬性：

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

[ `http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle) [p.hits=selective&amp;](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.nodedepth=5&amp;p.properties=sling%3aresourceType%20jcr%3apath&amp;property=jcr%3atitle&amp;property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=三角形

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

另外，您可以在QueryBuilder回應中加入子節點。 為此，您需要指定

```
p.nodedepth=n
```

其中`n`是您要查詢傳回的層級數。 請注意，若要傳回子節點，必須由屬性選取器指定

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

## 更多謂語 {#morepredicates}

如需更多述詞，請參閱[查詢產生器述詞參考頁面](/help/sites-developing/querybuilder-predicate-reference.md)。

還可以檢查`PredicateEvaluator`類](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)的[ Javadoc。 這些類的Javadoc包含可使用的屬性清單。

類名的前置詞（例如[`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)中的&quot; `similar`&quot;）是類的&#x200B;*主屬性*。 此屬性也是查詢中使用的謂語名稱（小寫為）。

對於這些主體屬性，您可以縮短查詢並使用&quot; `similar=/content/en`&quot;，而不是完全限定的變體&quot; `similar.similar=/content/en`&quot;。 必須將完全限定的表單用於類的所有非主屬性。

## 查詢產生器API使用範例{#example-query-builder-api-usage}

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
>若要了解如何建立使用QueryBuilder API的OSGi套件組合，以及在Adobe Experience Manager應用程式內使用該OSGi套件組合，請參閱[建立使用Query Builder AP](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)I的Adobe CQ OSGi套件組合。

使用查詢產生器(JSON)Servlet透過HTTP執行的相同查詢：

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## 儲存和載入查詢{#storing-and-loading-queries}

查詢可以儲存到儲存庫，以便以後使用。 `QueryBuilder`提供具有以下簽名的「 `storeQuery`方法：

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

使用[ `QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession)方法時，根據`createFile`引數值，給定的`Query`作為檔案或屬性儲存到儲存庫中。 以下示例說明如何將`Query`保存到路徑`/mypath/getfiles`中，作為檔案：

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

可使用[`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession)方法從儲存庫載入任何先前儲存的查詢：

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

例如，儲存至路徑`/mypath/getfiles`的`Query`可透過下列程式碼片段載入：

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## 測試和調試{#testing-and-debugging}

若要播放查詢並偵錯查詢產生器查詢，您可以在

`http://localhost:4502/libs/cq/search/content/querydebug.html`

或是在

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

（`path=/tmp`只是範例）。

### 一般偵錯Recommendations {#general-debugging-recommendations}

### 通過記錄{#obtain-explain-able-xpath-via-logging}獲取可解釋的XPath

對目標索引集在開發週期中說明&#x200B;**all**&#x200B;查詢。

* 啟用QueryBuilder的DEBUG日誌以獲取基礎、可解釋的XPath查詢

   * 導覽至https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog。 在&#x200B;**DEBUG**&#x200B;為`com.day.cq.search.impl.builder.QueryImpl`建立新記錄器。

* 為上述類別啟用DEBUG後，記錄檔會顯示查詢產生器產生的XPath。
* 從關聯QueryBuilder查詢的日誌條目複製XPath查詢，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 將XPath查詢貼入[Explain Query](/help/sites-administering/operations-dashboard.md#explain-query)作為XPath以獲取查詢計畫

### 透過查詢產生器除錯程式{#obtain-explain-able-xpath-via-the-query-builder-debugger}取得可解釋的XPath

* 使用AEM QueryBuilder偵錯工具產生可說明的XPath查詢：

對目標索引集在開發週期中說明&#x200B;**all**&#x200B;查詢。

**通過日誌獲取可解釋的XPath**

* 啟用QueryBuilder的DEBUG日誌以獲取基礎、可解釋的XPath查詢

   * 導覽至https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog。 在&#x200B;**DEBUG**&#x200B;為`com.day.cq.search.impl.builder.QueryImpl`建立新記錄器。

* 為上述類別啟用DEBUG後，記錄檔會顯示查詢產生器產生的XPath。
* 從關聯QueryBuilder查詢的日誌條目複製XPath查詢，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 將XPath查詢貼入[Explain Query](/help/sites-administering/operations-dashboard.md#explain-query)作為XPath，以獲得查詢計畫

**透過Query Builder除錯程式取得可說明的XPath**

* 使用AEM QueryBuilder偵錯工具產生可說明的XPath查詢：

![chlimage_1-66](assets/chlimage_1-66a.png)

1. 在查詢產生器偵錯工具中提供查詢產生器查詢
1. 執行搜索
1. 獲取生成的XPath
1. 將XPath查詢貼入Explain Query as XPath中，以獲得查詢計畫

>[!NOTE]
>
>可以直接提供非查詢生成器查詢(XPath、JCR-SQL2)以解釋查詢。

如需如何使用QueryBuilder除錯查詢的執行個體，請參閱下方的影片。

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## 使用記錄{#debugging-queries-with-logging}調試查詢

>[!NOTE]
>
>記錄器的配置在[建立您自己的記錄器和寫入器](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers)一節中描述。

執行測試和除錯中所述的查詢時，查詢產生器實作的記錄輸出（INFO層級）:

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

如果您有使用謂詞求值器來篩選的查詢，或使用按比較器的自定義順序的查詢，查詢中也會注意到：

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
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | 基本QueryBuilder和查詢API |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | 結果API |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.buckets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | 貯體（包含在Facet內） |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | 謂語求值器 |
| [com.day.cq.search.facets.extractors](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Facet提取器（用於求值器） |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | 查詢建立器servlet的JSON結果點擊寫入器(/bin/querybuilder.json) |
