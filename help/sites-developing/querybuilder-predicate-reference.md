---
title: 查詢產生器述詞參考
seo-title: Query Builder Predicate Reference
description: 查詢產生器API的完整述詞參考。
seo-description: Complete predicate reference for the Query Builder API.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: f97eb2e028263016131b0c86be5a0508ae4def9b
workflow-type: tm+mt
source-wordcount: '2371'
ht-degree: 3%

---

# 查詢產生器述詞參考{#query-builder-predicate-reference}

>[!CAUTION]
>
>本頁面上的資訊並非詳盡無遺。
>
>如需完整資訊，請參閱 **可用謂語** 在Query Builder Debugger主控台上；例如：
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>例如，請參閱：
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)


## 一般 {#general}

* [根](#root)
* [群組](#group)
* [orderby](#orderby)

## 謂語 {#predicates}

* [布爾屬性](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [達特朗日](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [排除路徑](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [全文](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [語言](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [mainasset](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [notexpired](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [路徑](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [屬性](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [範圍屬性](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativedaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [相似](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [標籤](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [類型](/help/sites-developing/querybuilder-predicate-reference.md#type)

### 布爾屬性 {#boolproperty}

在JCR布林屬性上符合。 僅接受值「 `true`&quot;和&quot; `false`」。 若為「 `false`&quot;，如果屬性具有值&quot; `false`「或者，如果它根本不存在。 這對於檢查僅在啟用時設定的布林值標幟非常有用。

繼承的「 `operation`&quot;參數沒有意義。

支援小面擷取。 會為每個 `true` 或 `false` 值，但僅限現有屬性。

#### 屬性 {#properties}

* **布爾屬性**
屬性的相對路徑，例如 
`myFeatureEnabled` 或 `jcr:content/myFeatureEnabled`

* **value**
要檢查屬性的值，&#39; 
`true`&quot; 或 &quot; `false`&quot;

### contentfragment {#contentfragment}

將結果限制為內容片段。

不支援篩選。

不支援Facet擷取。

#### 屬性 {#properties-1}

* **contentfragment**
可與任何值搭配使用，以檢查內容片段。

### dateComparison {#datecomparison}

比較兩個JCR DATE屬性。 可以測試它們是否相等、不等、是否大於或等於。

這是僅限篩選的謂語，無法使用搜尋索引。

#### 屬性 {#properties-2}

* **property1**

   第一個日期屬性的路徑

* **property2**

   日期屬性的路徑

* **操作**

   &quot; `equals`&quot;完全匹配， &quot; `!=`&quot;用於不相等的比較， &quot; `greater`&quot;表示屬性1大於屬性2, &quot; `>=`&quot;表示屬性1大於或等於屬性2。 預設值為 &quot; `equals`&quot;.

### 達特朗日 {#daterange}

比對日期/時間間隔的JCR DATE屬性。 日期和時間( `YYYY-MM-DDTHH:mm:ss.SSSZ`)，也允許部分表示，例如 `YYYY-MM-DD`. 或者，時間戳記可以以自1970年以來的毫秒數，以UTC時區（Unix時間格式）表示。

您可以尋找兩個時間戳記之間的任何項目，任何較新或較指定日期舊的項目，也可以在包含和開啟的間隔之間進行選擇。

支援小面擷取。 將提供貯體「今天」、「本週」、「本月」、「最近3個月」、「今年」、「去年」和「比去年早」。

不支援篩選。

#### 屬性 {#properties-3}

* **屬性**

   相對路徑 `DATE` 屬性，例如 `jcr:lastModified`

* **lowerBound**

   例如，下限界限以檢查屬性 `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot;（較新）或&quot; `>=`「（at或更新版本）」適用於 `lowerBound`. 預設值為「 `>`」。

* **upperBound**

   例如，要檢查屬性的上界 `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot;（舊）或&quot; `<=`「（在或更舊）」適用於 `upperBound`. 預設值為「 `<`」。

* **timeZone**

   未將其指定為ISO-8601日期字串時使用的時區ID。 預設為系統的預設時區。

### 排除路徑 {#excludepaths}

從其路徑符合規則運算式的結果中排除節點。

這是僅限篩選的謂語，無法使用搜尋索引。

不支援Facet擷取。

#### 屬性 {#properties-4}

* **排除路徑**

   規則運算式與結果路徑相符，從結果中排除相符的路徑。

### 全文 {#fulltext}

在全文索引中搜尋詞語。

不支援篩選。

不支援Facet擷取。

#### 屬性 {#properties-5}

* **全文**

   全文搜尋詞

* **relPath**

   要在屬性或子節點中搜索的相對路徑。 此屬性為選用。

### 群組 {#group}

允許建立巢狀條件。 群組可包含巢狀群組。 查詢建立器查詢中的所有內容都會隱含在根群組中，根群組可具有 `p.or` 和 `p.not` 參數。

比對兩個屬性其中之一與值的範例：

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

從概念上講 `(1_property` 或 `2_property)`.

巢狀群組的範例：

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

這會搜尋「**管理**「」 `/content/geometrixx/en` 或在 `/content/dam/geometrixx`.

從概念上講 `fulltext AND ( (path AND type) OR (path AND type) )`. 請注意，此類OR連接需要良好的效能索引。

#### 屬性 {#properties-6}

* **p.or**

   如果設為&quot; `true`&quot;，組中只有一個謂詞必須匹配。 這預設為「 `false`&quot;表示所有必須符合

* **p.not**

   如果設為&quot; `true`&quot;，則會否定群組(預設為「 `false`&quot;)

* **&lt;predicate>**

   添加嵌套謂詞

* **N_&lt;predicate>**

   新增多個同時的巢狀述詞，例如 `1_property, 2_property, ...`

### hasPermission {#haspermission}

將結果限制為目前工作階段已指定的項目 [JCR權限。](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

這是僅限篩選的謂語，無法使用搜尋索引。 不支援小面擷取。

#### 屬性 {#properties-7}

* **hasPermission**

   目前使用者工作階段必須具有的逗號分隔JCR權限，「全部」才能針對相關節點；例如 `jcr:write`, `jcr:modifyAccessControl`

### 語言 {#language}

以特定語言尋找CQ頁面。 這會同時查看頁面語言屬性和頁面路徑，這些路徑通常包括頂層網站結構中的語言或地區設定。

這是僅限篩選的謂語，無法使用搜尋索引。

支援小面擷取。 會為每個唯一語言代碼提供貯體。

#### 屬性 {#properties-8}

* **語言**

   ISO語言代碼，例如「 `de`&quot;

### mainasset {#mainasset}

檢查節點是否為DAM主要資產，而非子資產。 基本上，這是不在「子資產」節點內的每個節點。 請注意，這不會檢查 `dam:Asset` 節點類型。 要使用此謂語，只需設定&quot; `mainasset=true`&quot;或&quot; `mainasset=false`「，沒有其他屬性。

這是僅限篩選的謂語，無法使用搜尋索引。

支援小面擷取。 將提供2個貯體給主要和子資產。

#### 屬性 {#properties-9}

* **mainasset**

   布林值， &quot; `true`&quot;對於主要資產， &quot; `false`&quot;子資產

### memberOf {#memberof}

查找屬於特定 [sling資源集合](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

這是僅限篩選的謂語，無法使用搜尋索引。 不支援Facet擷取。

#### 屬性 {#properties-10}

* **memberOf**

   Sling資源收集路徑

### nodename {#nodename}

在JCR節點名稱上符合。

支援小面擷取。 會為每個唯一節點名稱提供貯體（檔案名稱）。

#### 屬性 {#properties-11}

* **nodename**

   允許通配符的節點名稱模式： `*` =任何字元或無字元， `?` =任何字元， `[abc]` =僅括弧中的字元

### notexpired {#notexpired}

檢查JCR DATE屬性是否大於或等於目前伺服器時間以比對項目。 這可用來檢查「 `expiresAt`&quot;贊日期屬性，並僅限於尚未過期的屬性( `notexpired=true`)或已過期( `notexpired=false`)。

不支援篩選。

支援Facet擷取，方式與Daterange述詞相同。

#### 屬性 {#properties-12}

* **notexpired**

   布林值， &quot; `true`「尚未過期（未來日期或等於）, 」 `false`&quot;過期（過去的日期）（必要）

* **屬性**

   相對路徑 `DATE` 要檢查的屬性（必要）

### orderby {#orderby}

允許對結果進行排序。 如果需要依多個屬性排序，則需要使用數字首碼多次新增此述詞，例如 `1_orderby=first`, `2_oderby=second`.

#### 屬性 {#properties-13}

* **orderby**

   以前導@表示的JCR屬性名稱，例如 `@jcr:lastModified` 或 `@jcr:content/jcr:title`，或查詢中的其他謂語，例如 `2_property`，排序

* **排序**

   排序方向，或&quot; `desc`&quot;代表降序或&quot; `asc`&quot;代表遞增（預設）

* **案例**

   如果設為&quot; `ignore`&quot;會使排序不區分大小寫，表示&quot;a&quot;在&quot;B&quot;之前；如果空白或遺漏，則排序會區分大小寫，表示「B」在「a」之前

### 路徑 {#path}

在指定路徑內搜尋。

不支援Facet擷取。

#### 屬性 {#properties-14}

* **路徑**

   路徑模式；視確切情況而定，整個子樹狀結構會相符(例如附加 `//*` 在xpath中，但請注意，這不包括基本路徑)（exact=false，預設）或只有完全的路徑符合，其中可包含萬用字元( `*`);如果設定了self，則搜索包含基節點的整個子樹

* **精準**

   if `exact` 為true/on，則確切路徑必須相符，但可包含簡單的萬用字元( `*`)，該匹配名稱，但不是&quot; `/`&quot;如果為false（預設），則包括所有子代（可選）

* **扁平**

   僅搜索直接子項(如附加&quot; `/*`&quot;在xpath中(僅在「 `exact`&#39;不是true，可選)

* **self**

   搜索子樹，但包括作為路徑指定的基節點（無通配符）

### 屬性 {#property}

在JCR屬性及其值上相符。

支援小面擷取。 會為結果中的每個唯一屬性值提供貯體。

#### 屬性 {#properties-15}

* **屬性**

   屬性的相對路徑，例如 `jcr:title`

* **值**

   要檢查屬性的值；會遵循JCR屬性類型來轉換字串

* **N_value**

   use `1_value`, `2_value`,...檢查多個值(結合 `OR` 預設情況下，使用 `AND` if and=true)（自5.3起）

* **和**

   設為true以結合多個值( `N_value`)和（自5.3起）

* **操作**

   &quot;`equals`&quot;完全匹配（預設）, &quot; `unequals`&quot;用於不相等的比較， &quot; `like`」 `jcr:like` xpath函式（可選）, &quot; `not`&quot;表示不匹配(例如 &quot;`not(@prop)`&quot;在xpath中，值參數將被忽略)或&quot; `exists`&quot; for exist check(value可以是true — 屬性必須存在，預設值 — 或false — 與&quot;相同 `not`&quot;)

* **深度**

   屬性/相對路徑可存在的通配符級別數(例如 `property=size depth=2` 將檢查節點/大小、節點/&amp;ast;/size和node/&amp;ast;/&amp;ast;/size

### 範圍屬性 {#rangeproperty}

比對間隔的JCR屬性。 這會套用至具有線性類型的屬性，例如 `LONG`, `DOUBLE` 和 `DECIMAL`. 針對 `DATE` 請參閱已最佳化日期格式輸入的daterange述詞。

您可以定義下界限和上界限，或僅定義其中一個界限。 操作(例如 也可以為上下界限分別指定&quot;小於&quot;或&quot;小於等於&quot;)。

不支援Facet擷取。

#### 屬性 {#properties-16}

* **屬性**

   相對屬性路徑

* **lowerBound**

   下限，檢查屬性

* **lowerOperation**

   &quot; `>`&quot;（預設值）或&quot; `>=`」，適用於 `lowerValue`

* **upperBound**

   上限將檢查屬性

* **upperOperation**

   &quot; `<`&quot;（預設值）或&quot; `<=`」，適用於 `lowerValue`

* **小數**

   &quot; `true`&quot;如果選定的屬性類型為「小數」

### relativedaterange {#relativedaterange}

符合 `JCR DATE` 使用相對於目前伺服器時間的時間偏移來比較日期/時間間隔的屬性。 您可以指定 `lowerBound` 和 `upperBound` 使用毫秒值或bugzilla語法 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分鐘、三小時、四天、五週、六個月、七年）。 前置詞為&quot; `-`&quot;表示當前時間之前的負偏移。 如果您僅指定 `lowerBound` 或 `upperBound`，另一個會預設為0，表示目前時間。

例如：

* `upperBound=1h` （否） `lowerBound`)會在下一小時內選取任何項目
* `lowerBound=-1d` （否） `upperBound`)會在過去24小時內選取任何項目
* `lowerBound=-6M` 和 `upperBound=-3M` 選擇6個月或3個月
* `lowerBound=-1500` 和 `upperBound=5500` 會選取過去1500毫秒到未來5500毫秒之間的任何值
* `lowerBound=1d` 和 `upperBound=2d` 會在後天選出任何東西

請注意，不需要考慮閏年，且所有月份均為30天。

不支援篩選。

支援Facet擷取，方式與Daterange述詞相同。

#### 屬性 {#properties-17}

* **upperBound**

   以毫秒或毫秒為單位的上日期界限 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分鐘、三小時、四天、五週、六個月、七年），相對於當前伺服器時間，使用「 — 」作為負偏移

* **lowerBound**

   以毫秒或毫秒為單位的下限日期 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分鐘、三小時、四天、五週、六個月、七年），相對於當前伺服器時間，使用「 — 」作為負偏移

### 根 {#root}

根謂片語。 支援組的所有功能，並允許設定全局查詢參數。

查詢中從未使用「root」名稱，此名稱為隱式。

#### 屬性 {#properties-18}

* **p.offset**

   表示結果頁面開始的數字，即要略過的項目數

* **p.limit**

   表示頁面大小的數字

* **p.guessTotal**

   建議：避免計算全部結果總計，而這可能會造成很大成本；指出總計上限的數字（例如1000，該數字讓使用者對粗細大小和精確數字有足夠的意見，以取得較小的結果）或「 `true`&quot;只計算最少必要值 `p.offset` + `p.limit`

* **p.expert**

   如果設為&quot; `true`&quot;，將全文摘錄在結果中

* **p.hits**

   （僅限JSON servlet）選取將點擊寫入為JSON的方式，並搭配這些標準點擊（可透過ResultHitWriter服務擴充）:

   * **簡單**:

      最小的項目 `path`, `title`, `lastmodified`, `excerpt` （若已設定）

   * **完整**:

      sling JSON轉譯節點，搭配 `jcr:path` 指出點擊的路徑：預設情況下，僅列出節點的直接屬性，包括更深的樹，其中 `p.nodedepth=N`,0表示整個無限子樹；新增 `p.acls=true` 要包含當前會話對給定結果項的JCR權限(映射： `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **選擇性**:

      僅指定屬性 `p.properties`，這是以空格分隔的（在URL中使用「+」）相對路徑清單；如果相對路徑的深度大於1，則這些將表示為子對象；特殊的jcr:path屬性包含點擊的路徑

### savedquery {#savedquery}

將持續查詢建立器查詢的所有謂語作為子組謂語包含到當前查詢中。

請注意，這不會執行額外的查詢，而會延伸目前的查詢。

查詢可以用程式保存，使用 `QueryBuilder#storeQuery()`. 格式可以是多行字串屬性或 `nt:file` 包含查詢的節點，該查詢以Java屬性格式為文本檔案。

不支援儲存查詢的述詞的Facet擷取。

#### 屬性 {#properties-19}

* **savedquery**

   儲存查詢的路徑(字串屬性或 `nt:file` node)

### 相似 {#similar}

用JCR XPath搜索相似度 `rep:similar()`.

不支援篩選。 不支援Facet擷取。

#### 屬性 {#properties-20}

* **相似**
查找相似節點的節點的絕對路徑

* **本地**
到子節點或 
`.` 對於當前節點(可選，預設為「 `.`&quot;)

### 標籤 {#tag}

通過指定標籤標題路徑搜索標籤為一個或多個標籤的內容。

支援小面擷取。 會使用每個唯一標籤的目前標籤標題路徑，為每個標籤提供貯體。

#### 屬性 {#properties-21}

* **標籤**

   要尋找的標籤標題路徑，例如「資產屬性」：方向/橫向」

* **N_value**

   use `1_value`, `2_value`,...檢查多個標籤(結合 `OR` 預設情況下，使用 `AND` if and=true)（自5.6起）

* **屬性**

   要查看的屬性（或屬性的相對路徑）(預設值為「 `cq:tags`&quot;)

### tagid {#tagid}

通過指定標籤ID搜索標籤為一個或多個標籤的內容。

支援小面擷取。 會使用每個唯一標籤的目前標籤ID，為每個標籤提供貯體。

#### 屬性 {#properties-22}

* **tagid**

   要尋找的標籤id，例如「 `properties:orientation/landscape`&quot;

* **N_value**

   use `1_value`, `2_value`,...檢查多個tagid(結合 `OR` 預設情況下，使用 `AND` if and=true)（自5.6起）

* **屬性**

   要查看的屬性（或屬性的相對路徑）(預設值為「 `cq:tags`&quot;)

### tagsearch {#tagsearch}

通過指定關鍵字搜索標籤為一個或多個標籤的內容。 這會先搜尋標題中包含這些關鍵字的標籤，然後將結果限制為僅限標籤這些關鍵字的項目。

不支援Facet擷取。

#### 屬性 {#Properties-1}

* **tagsearch**

   要在標籤標題中搜索的關鍵字

* **屬性**

   要查看的屬性（或屬性的相對路徑）(預設值為「 `cq:tags`&quot;)

* **朗**

   僅搜尋特定本地化標籤標題(例如&quot; `de`&quot;)

* **全部**

   (bool)搜尋整個標籤全文，即所有標題、說明等。 (優先於l `ang`&quot;)

### 類型 {#type}

將結果限制為特定的JCR節點類型，主節點類型或混合類型。 這也會找到該節點類型的子類型。 請注意，儲存庫搜索索引需要涵蓋節點類型，才能有效執行。

支援小面擷取。 將為結果中的每個唯一類型提供貯體。

#### 屬性 {#Properties-2}

* **類型**

   要搜索的節點類型或混合名稱，例如 `cq:Page`
