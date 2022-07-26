---
title: 查詢產生器 API
seo-title: Query Builder API
description: 資產共用查詢生成器的功能通過Java API和REST API公開。
seo-description: The functionality of the Asset Share Query Builder is exposed through a Java API and a REST API.
uuid: 6928c3e9-96a1-44ad-9785-350d95f1869a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7965b7ef-dec4-441a-a012-daf1d60df0fb
pagetitle: Query Builder API
tagskeywords: querybuilder
exl-id: b2288442-d055-4966-8057-8b7b7b6bff28
source-git-commit: bfb02e79d6895be498e6e40888c6d8d4e3a8fcd4
workflow-type: tm+mt
source-wordcount: '2313'
ht-degree: 0%

---

# 查詢產生器 API{#query-builder-api}

功能 [資產共用查詢生成器](/help/assets/assets-finder-editor.md) 通過Java API和REST API公開。 本節介紹這些API。

伺服器端查詢生成器( [`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html))將接受查詢說明，建立並運行XPath查詢，可選地過濾結果集，並提取facet（如果需要）。

查詢說明只是一組謂語([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html))。 示例包括與 `jcr:contains()` 函式。

對於每個謂詞類型，都有一個計算器元件([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html))，它知道如何處理XPath、篩選和刻面提取的特定謂詞。 建立自定義計算器非常容易，這些計算器通過OSGi元件運行時插入。

REST API通過HTTP提供對完全相同功能的訪問，響應以JSON形式發送。

>[!NOTE]
>
>QueryBuilder API是使用JCR API構建的。 您也可以使用JCR API從OSGi捆綁包中查詢Adobe Experience ManagerJCR。 有關資訊，請參見 [使用JCR API查詢Adobe Experience Manager資料](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)。

## Gem會話 {#gem-session}

[寶石AEM](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) 是Adobe專家對Adobe Experience Manager進行的一系列深度技術潛水。 此專用於查詢生成器的會話對於工具的概述和使用非常有用。

>[!NOTE]
>
>查看AEMGem會話 [使用查詢生成器輕鬆搜索表AEM單](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2017/aem-search-forms-using-querybuilder.html) 的子菜單。

## 示例查詢 {#sample-queries}

這些示例以Java屬性樣式表示法提供。 要將它們與Java API一起使用，請使用Java `HashMap` 如下API示例中所示。

對於 `QueryBuilder` JSON Servlet的每個示例都包含指向本地CQ安裝的連結(在預設位置， `http://localhost:4502`)。 請注意，在使用這些連結之前，必須登錄到CQ實例。

>[!CAUTION]
>
>預設情況下，查詢生成器json servlet最多顯示10次命中。
>
>添加以下參數可使servlet顯示所有查詢結果：
>
>**`p.limit=-1`**

>[!NOTE]
>
>要在瀏覽器中查看返回的JSON資料，您可能希望使用插件，如JSONView for Firefox。

### 返回所有結果 {#returning-all-results}

以下查詢將 **返回十個結果** （或者確切地說，最多十個），但通知你 **點擊次數：** 實際可用：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

同一查詢（帶參數） `p.limit=-1`) **返回所有結果** （根據您的實例，此數字可能較高）:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### 使用p.guessTotal返回結果 {#using-p-guesstotal-to-return-the-results}

目的 `p.guessTotal` 參數是返回通過組合最小可行p.offset和p.limit值可以顯示的適當數目的結果。 在大結果集的情況下，使用該參數的優點是提高了效能。 這避免了計算全部總數(如調用result.getSize())和讀取整個結果集，並一直優化到OAK引擎和索引。 當結果達到100,000個時，這可能是一個顯著差異，無論是執行時間還是記憶體使用情況。

參數的缺點是用戶看不到確切的總數。 但您可以設定一個最小數字，如p.guessTotal=1000，這樣它總能讀到1000，因此您可以得到較小結果集的準確合計，但如果結果超過此值，則只能顯示「和更多」。

添加 `p.guessTotal=true` 查詢，查看其工作原理：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

查詢將返回 `p.limit` 預設值 `10` 結果 `0` 偏移：

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

從AEM6.0 SP2開始，您還可以使用一個數值來計算自定義的最大結果數。 使用與上面相同的查詢，但更改 `p.guessTotal` 至 `50`:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

它將返回一個與預設限制相同的數字：10個結果，0個偏移，但最多只顯示50個結果：

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### 實現分頁 {#implementing-pagination}

預設情況下，查詢生成器還會提供命中次數。 根據結果大小，這可能需要很長時間，因為確定準確計數涉及檢查每個結果以獲取訪問控制。 大多數情況下，總數用於實現最終用戶UI的分頁。 由於確定確切計數可能會很慢，建議使用guessTotal功能來實現分頁。

例如，UI可以調整以下方法：

* 獲取並顯示總命中數的準確計數([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) 或querybuilder.json響應中的總數)小於或等於100;
* 設定 `guessTotal` 調用查詢生成器時調用到100。

* 響應可能具有以下結果：

   * `total=43`。 `more=false`  — 表示命中總數為43。 UI最多可以顯示10個結果作為第一頁的一部分，並為接下來的3頁提供分頁。 您也可以使用此實現來顯示描述性文本，如 **&quot;發現43個結果&quot;**。
   * `total=100`。 `more=true`  — 表示命中總數大於100且未知準確計數。 UI最多可顯示10個作為第一頁的一部分，並為接下來的10個頁面提供分頁。 您也可以使用它顯示類似 **&quot;發現100多個結果&quot;**。 當用戶轉到對查詢生成器進行的調用的下一頁時， `guessTotal` 還有 `offset` 和 `limit` 參數。

`guessTotal` 在UI需要使用無限滾動時，也應使用，以避免查詢生成器確定準確的命中計數。

### 查找jar檔案並訂購它們，最新先訂購 {#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### 查找所有頁面並按上次修改的順序排序 {#find-all-pages-and-order-them-by-last-modified}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### 查找所有頁面並按上次修改後的降序排序 {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc]`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### 全文搜索，按分數排序 {#fulltext-search-ordered-by-score}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### 搜索標籤有特定標籤的頁面 {#search-for-pages-tagged-with-a-certain-tag}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&tagid=marketing:interest/product&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

使用 `tagid` 謂詞（如果知道顯式標籤ID）。

使用 `tag` 標籤標題路徑的謂詞（不帶空格）。

因為，在上例中，您正在搜索頁( `cq:Page` 節點)，需要使用該節點的相對路徑 `tagid.property` 謂語，即 `jcr:content/cq:tags`。 預設情況下， `tagid.property` 就是 `cq:tags`。

### 在多個路徑下搜索（使用組） {#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

此查詢使用 *組* （命名&quot;） `group`&quot;)，它用於在查詢中劃分子表達式，就像括弧在更多標準符號中所做的那樣。 例如，上一個查詢可能以更熟悉的樣式表示為：

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

在示例中的組內， `path` 謂詞被多次使用。 要區分並排序謂詞的兩個實例（某些謂詞需要排序），必須在謂詞前面加上 *N* `_ where`*N* 是排序索引。 在上一個示例中，生成的謂語是 `1_path` 和 `2_path`。

的 `p` 在 `p.or` 是一個特殊分隔符，它指示後面的內容(在本例中， `or`) *參數* 與組的子謂語相反，如 `1_path`。

否 `p.or` 表示所有謂語，即每個結果必須滿足所有謂語。

>[!NOTE]
>
>不能在單個查詢中使用相同的數字前置詞，即使對於不同的謂語也是如此。

### 搜索屬性 {#search-for-properties}

在此，您使用 `cq:template` 屬性：

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

這有一個缺點 `jcr:content` 將返回頁面的節點，而不是頁面本身。 要解決此問題，可以按相對路徑進行搜索：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### 搜索多個屬性 {#search-for-multiple-properties}

多次使用屬性謂詞時，必須再次添加數字前置詞：

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### 搜索多個屬性值 {#search-for-multiple-property-values}

要在搜索屬性的多個值時避免大型組( `"A" or "B" or "C"`)，可以為 `property` 謂語：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

對於多值屬性，您還可以要求多個值匹配( `"A" and "B" and "C"`):

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## 改進返回的內容 {#refining-what-is-returned}

預設情況下，QueryBuilder JSON Servlet將為搜索結果中的每個節點（如路徑、名稱、標題等）返回一組預設屬性。 為了獲得對返回屬性的控制，可以執行以下操作之一：

指定

```
p.hits=full
```

在這種情況下，每個節點都將包含所有屬性：

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

並指定要進入的屬性

```
p.properties
```

以空格分隔：

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[ `http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle) [點擊率=選擇性，](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.nodedepth=5&amp;p.properties=sling%3aresourceType%20jcr%3apath&amp;property=jcr%3atitle&amp;property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=三角形

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

您可以做的另一件事是，在QueryBuilder響應中包括子節點。 要執行此操作，需要指定

```
p.nodedepth=n
```

何處 `n` 是希望查詢返回的級別數。 請注意，要返回子節點，必須由屬性選擇器指定

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

有關更多謂語，請參見 [「查詢生成器謂詞參考」頁](/help/sites-developing/querybuilder-predicate-reference.md)。

您還可以 [的Javadoc `PredicateEvaluator` 類](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)。 這些類的Javadoc包含可使用的屬性清單。

類名的前置詞（例如， &quot;） `similar`&quot; [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) *主要屬性* 全班同學。 此屬性也是查詢中使用的謂詞的名稱（小寫）。

對於此類主體屬性，可以縮短查詢並使用「」 `similar=/content/en`&quot;而不是完全限定的變型&quot; `similar.similar=/content/en`。 類的所有非主屬性都必須使用完全限定窗體。

## 查詢生成器API用法示例 {#example-query-builder-api-usage}

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
>要瞭解如何構建使用QueryBuilder API的OSGi捆綁包，並在Adobe Experience Manager應用程式內使用該OSGi捆綁包，請參見 [建立使用查詢生成器AP的Adobe CQOSGi捆綁包](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)我。

使用查詢生成器(JSON)Servlet通過HTTP執行的同一查詢：

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## 儲存和載入查詢 {#storing-and-loading-queries}

查詢可以儲存到儲存庫，以便您以後可以使用這些查詢。 的 `QueryBuilder` 提供了「 `storeQuery` 具有以下簽名的方法：

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

使用 [ `QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession) 方法，給出 `Query` 作為檔案或屬性儲存到儲存庫中 `createFile` 參數值。 以下示例說明如何保存 `Query` 到路徑 `/mypath/getfiles` 檔案：

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

可以使用 [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession) 方法：

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

例如， `Query` 儲存到路徑 `/mypath/getfiles` 可以由以下代碼段載入：

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## 測試和調試 {#testing-and-debugging}

要播放和調試querybuilder查詢，可以在

`http://localhost:4502/libs/cq/search/content/querydebug.html`

或查詢生成器json servlet位於

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

( `path=/tmp` 只是個例子)。

### 常規調試Recommendations {#general-debugging-recommendations}

### 通過日誌獲取可解釋的XPath {#obtain-explain-able-xpath-via-logging}

解釋 **全部** 在開發週期中對目標索引集進行查詢。

* 啟用QueryBuilder的DEBUG日誌以獲取基礎、可解釋的XPath查詢

   * 導航到https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog。 為建立新記錄器 `com.day.cq.search.impl.builder.QueryImpl` 在 **調試**。

* 為上述類啟用DEBUG後，日誌將顯示Query Builder生成的XPath。
* 從關聯的QueryBuilder查詢的日誌條目中複製XPath查詢，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 將XPath查詢貼上到 [解釋查詢](/help/sites-administering/operations-dashboard.md#explain-query) 作為XPath來獲取查詢計畫

### 通過查詢生成器調試器獲取可解釋的XPath {#obtain-explain-able-xpath-via-the-query-builder-debugger}

* 使用AEMQueryBuilder調試器生成可解釋的XPath查詢：

解釋 **全部** 在開發週期中對目標索引集進行查詢。

**通過日誌獲取可解釋的XPath**

* 啟用QueryBuilder的DEBUG日誌以獲取基礎、可解釋的XPath查詢

   * 導航到https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog。 為建立新記錄器 `com.day.cq.search.impl.builder.QueryImpl` 在 **調試**。

* 為上述類啟用DEBUG後，日誌將顯示Query Builder生成的XPath。
* 從關聯的QueryBuilder查詢的日誌條目中複製XPath查詢，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 將XPath查詢貼上到 [解釋查詢](/help/sites-administering/operations-dashboard.md#explain-query) 作為XPath獲取查詢計畫

**通過查詢生成器調試器獲取可解釋的XPath**

* 使用AEMQueryBuilder調試器生成可解釋的XPath查詢：

![chlimage_1-66](assets/chlimage_1-66a.png)

1. 在Query Builder調試器中提供Query Builder查詢
1. 執行搜索
1. 獲取生成的XPath
1. 將XPath查詢貼上到解釋查詢中作為XPath以獲取查詢計畫

>[!NOTE]
>
>非querybuilder查詢(XPath、JCR-SQL2)可直接提供給「解釋查詢」。

有關如何使用QueryBuilder調試查詢的詳細說明，請參閱下面的視頻。

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## 調試具有日誌記錄的查詢 {#debugging-queries-with-logging}

>[!NOTE]
>
>本節介紹了伐木器的配置 [建立您自己的伐木工和作者](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers)。

執行測試和調試中描述的查詢時查詢生成器實現的日誌輸出（INFO級別）:

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

如果您有一個使用謂詞計算器進行篩選的查詢，或者使用按比較器進行的自定義順序的查詢，則查詢中也會注意到這一點：

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

## Javadoc連結 {#javadoc-links}

| **Javadoc** | **說明** |
|---|---|
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | 基本QueryBuilder和查詢API |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | 結果API |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | 小平面 |
| [com.day.cq.search.facets.buckets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | 桶（包含在小平面內） |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | 謂詞計算器 |
| [com.day.cq.search.facets.extractors](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | 小平面提取器（用於計算器） |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | Querybuilder Servlet的JSON結果命中寫入程式(/bin/querybuilder.json) |
