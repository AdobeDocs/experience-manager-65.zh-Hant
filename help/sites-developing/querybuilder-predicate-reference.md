---
title: Query Builder Predicate Reference
seo-title: Query Builder Predicate Reference
description: Query Builder API的完整謂詞參考。
seo-description: Query Builder API的完整謂詞參考。
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
translation-type: tm+mt
source-git-commit: 7a96ff5cdd187291efe108d1171782bcbecfaeb0
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 2%

---


# Query Builder Predicate Reference{#query-builder-predicate-reference}

## 一般 {#general}

* [根](#root)
* [群組](#group)
* [orderby](#orderby)

## 謂語{#predicates}

* [布爾屬性](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [達朗日](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
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
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [相對變更](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [相似](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [標籤](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [類型](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

在JCR布爾屬性上匹配。 僅接受值&quot; `true`&quot;和&quot; `false`&quot;。 對於&quot; `false`&quot;，如果屬性的值為&quot; `false`&quot;，或完全不存在，則匹配。 這對於檢查僅在啟用時設定的布爾標誌非常有用。

繼承的&quot; `operation`&quot;參數沒有意義。

支援Facet擷取。 將為每個`true`或`false`值提供儲存區，但僅為現有屬性提供儲存區。

#### 屬性 {#properties}

* **Boolpropertyproperty**
屬性相對路徑，例如 
`myFeatureEnabled` 或 `jcr:content/myFeatureEnabled`

* ****
值值，用於檢查屬性， &quot; 
`true`&quot; 或 &quot; `false`&quot;

### contentfragment {#contentfragment}

將結果限制為內容片段。

不支援篩選。

不支援Facet擷取。

#### 屬性 {#properties-1}

* **content**
fragmentIt可與任何值搭配使用，以檢查內容片段。

### dateComparison {#datecomparison}

將兩個JCR DATE屬性相互比較。 可以測試它們是等於、不等於、大於或等於。

這是僅限篩選的謂語，無法運用搜尋索引。

#### 屬性 {#properties-2}

* **property1**

   第一個日期屬性的路徑

* **property2**

   路徑至第二個日期屬性

* **操作**

   「`equals`」代表完全相符，「`!=`」代表不等比，「`greater`」代表屬性1大於屬性2,「`>=`」代表屬性1大於或等於屬性2。 預設值為 &quot;`equals`&quot;.

### daterange {#daterange}

與日期／時間間隔的JCR DATE屬性相符。 這使用ISO8601
格式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)，並允許部分表示，例如`YYYY-MM-DD`。 或者，時間戳可以以1970年以來的毫秒數提供，以UTC時區（UNIX時間格式）表示。

您可以尋找兩個時間戳記之間的任何項目（任何比指定日期更新或更舊的項目），也可以選擇包含和開啟的間隔。

支援Facet擷取。 將提供「今天」、「本週」、「本月」、「最近3個月」、「今年」、「去年」和「比去年早」的時段。

不支援篩選。

#### 屬性 {#properties-3}

* **屬性**

   `DATE`屬性的相對路徑，例如`jcr:lastModified`

* **下界**

   lower date bound to check property for, for example `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot;（較新）或&quot; `>=`&quot;（at或更新），適用於`lowerBound`。 預設值為&quot; `>`&quot;。

* **上界**

   上界檢查屬性，例如`2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot;（舊版）或&quot; `<=`&quot;（舊版）適用於`upperBound`。 預設值為&quot; `<`&quot;。

* **時區**

   未指定為ISO-8601日期字串時使用的時區ID。 預設為系統的預設時區。

### 排除路徑{#excludepaths}

從其路徑與規則運算式匹配的結果中排除節點。

這是僅限篩選的謂語，無法運用搜尋索引。

不支援Facet擷取。

#### 屬性 {#properties-4}

* **排除路徑**

   規則運算式與結果路徑相符，從結果中排除相符的運算式。

### 全文{#fulltext}

在全文索引中搜尋詞語。

不支援篩選。

不支援Facet擷取。

#### 屬性 {#properties-5}

* **全文**

   全文搜尋詞

* **relPath**

   屬性或子節點中要搜索的相對路徑。 此屬性為可選屬性。

### 群組 {#group}

允許建立巢狀條件。 群組可以包含巢狀群組。 查詢建立工具查詢中的所有項目都會隱含在根群組中，根群組中也可以有`p.or`和`p.not`參數。

比對兩個屬性中任一屬性與值的範例：

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

這在概念上是`(1_property`或`2_property)`。

巢狀群組的範例：

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

這會在`/content/geometrixx/en`的頁面或`/content/dam/geometrixx`的資產中搜尋「**Management**」一詞。

這在概念上是`fulltext AND ( (path AND type) OR (path AND type) )`。 請注意，此類OR連接需要良好的效能索引。

#### 屬性 {#properties-6}

* **p.or**

   如果設定為&quot; `true`&quot;，則組中只有一個謂詞必須匹配。 此預設為&quot; `false`&quot;，表示所有項目都必須符合

* **p.not**

   如果設定為&quot; `true`&quot;，則會否定組（預設為&quot; `false`&quot;）

* **&lt;predicate>**

   添加嵌套謂語

* **N_&lt;predicate>**

   添加多個同時的嵌套謂語，如`1_property, 2_property, ...`

### hasPermission {#haspermission}

將結果限制為當前會話具有指定[JCR權限的項目。](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

這是僅限篩選的謂語，無法運用搜尋索引。 它不支援Facet擷取。

#### 屬性 {#properties-7}

* **hasPermission**

   當前用戶會話必須ALL對有問題的節點具有的逗號分隔JCR權限；例如`jcr:write`、`jcr:modifyAccessControl`

### 語言 {#language}

尋找特定語言的CQ頁面。 這會查看頁面語言屬性和頁面路徑，這些路徑通常包含頂層網站結構中的語言或地區設定。

這是僅限篩選的謂語，無法運用搜尋索引。

支援Facet擷取。 將為每個唯一的語言代碼提供時段。

#### 屬性 {#properties-8}

* **語言**

   ISO語言代碼，例如&quot; `de`&quot;

### mainasset {#mainasset}

檢查節點是否是DAM主資產而非子資產。 基本上，這是不在「子資產」節點內的每個節點。 請注意，這不會檢查`dam:Asset`節點類型。 若要使用此謂語，只要設定&quot; `mainasset=true`&quot;或&quot; `mainasset=false`&quot;，就沒有其他屬性。

這是僅限篩選的謂語，無法運用搜尋索引。

支援Facet擷取。 將為主資產和子資產提供2個桶。

#### 屬性 {#properties-9}

* **mainasset**

   布林值，主資產為&quot; `true`&quot;，子資產為&quot; `false`&quot;

### {#memberof}的成員

查找屬於特定[sling資源集合](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)成員的項目。

這是僅限篩選的謂語，無法運用搜尋索引。 不支援Facet擷取。

#### 屬性 {#properties-10}

* **memberOf**

   Sling資源集合的路徑

### nodename {#nodename}

與JCR節點名稱匹配。

支援Facet擷取。 將為每個唯一節點名稱（檔案名）提供儲存段。

#### 屬性 {#properties-11}

* **nodename**

   允許通配符的節點名模式：`*` = any or no char, `?` = any char, `[abc]` = only chars,  = only chars

### notexpired {#notexpired}

檢查JCR DATE屬性是否大於或等於目前伺服器時間，以比對項目。 這可用於檢查「 `expiresAt`」類似日期屬性，並僅限於尚未過期的(`notexpired=true`)或已過期的(`notexpired=false`)。

不支援篩選。

支援Facet擷取，其方式與daterange謂詞相同。

#### 屬性 {#properties-12}

* **notexpired**

   布林值、「 `true`」（未到期日或等於未來日期）、「 `false`」（過去日期）（必要）

* **屬性**

   要檢查的`DATE`屬性的相對路徑（必需）

### orderby {#orderby}

允許對結果進行排序。 如果需要按多個屬性排序，則需要使用數字前置詞多次添加此謂語，如`1_orderby=first`、`2_oderby=second`。

#### 屬性 {#properties-13}

* **orderby**

   由前導@（例如`@jcr:lastModified`或`@jcr:content/jcr:title`）指示的JCR屬性名稱，或查詢中的另一個謂語，例如`2_property`，要對其排序

* **排序**

   排序方向，「 `desc`」代表遞減，「 `asc`」代表遞增（預設）

* **案例**

   如果設為&quot; `ignore`&quot;，則排序不區分大小寫，表示&quot;a&quot;在&quot;B&quot;之前；如果空或缺，則排序區分大小寫，表示&quot;B&quot;在&quot;a&quot;之前

### 路徑 {#path}

在指定路徑內搜尋。

不支援Facet擷取。

#### 屬性 {#properties-14}

* **路徑**

   路徑模式；根據具體情況，整個子樹將匹配（如在xpath中附加`//*`，但請注意，這不包括基本路徑）(exact=false, default)或僅匹配完全路徑(可包括通配符(`*`));如果設定了self，則搜索包含基節點的整個子樹

* **精確**

   如果`exact`為true/on，則精確路徑必須相符，但可包含簡單萬用字元(`*`)、符合名稱，但不能包含&quot; `/`&quot;;如果為false（預設），則會包含所有子系（選用）

* **扁平**

   僅搜索直接子項（如在xpath中附加&quot; `/*`&quot;）（僅在&#39; `exact`&#39;不是true時使用，可選）

* **self**

   搜索子樹，但包括作為路徑給定的基節點（無通配符）

### 屬性 {#property}

與JCR屬性及其值相符。

支援Facet擷取。 將為結果中的每個唯一屬性值提供時段。

#### 屬性 {#properties-15}

* **屬性**

   屬性的相對路徑，例如`jcr:title`

* **值**

   值以檢查屬性；跟隨JCR屬性類型到字串轉換

* **N值**

   使用`1_value`、`2_value`、...若要檢查多個值（依預設與`OR`結合，若與=true則與`AND`結合）（自5.3起）

* **與**

   設為true時，結合多個值(`N_value`)與AND（自5.3起）

* **操作**

   「`equals`」代表完全相符（預設值）,「`unequals`」代表不等比較，「`like`」代表使用`jcr:like` xpath函式（選用）,「`not`」代表不相符(例如 xpath中的&quot;`not(@prop)`&quot;，值param將被忽略)或&quot;`exists`&quot;用於存在檢查（值可以是true —— 屬性必須存在，預設——或false —— 與&quot;`not`&quot;相同）

* **深度**

   屬性／相對路徑可存在的通配符級別數（例如，`property=size depth=2`將檢查節點／大小、node/&amp;ast;/size和node/&amp;ast;/&amp;ast;/size）

### rangeproperty {#rangeproperty}

與JCR屬性對應的時間間隔。 這適用於具有線性類型的屬性，例如`LONG`、`DOUBLE`和`DECIMAL`。 如需`DATE`，請參閱已最佳化日期格式輸入的變更述詞。

您可以定義下界和上界，或僅定義其中一個。 操作(如 也可以針對下界限和上界限分別指定「小於」或「小於或等於」)。

不支援Facet擷取。

#### 屬性 {#properties-16}

* **屬性**

   相對路徑至屬性

* **下界**

   下界檢查屬性

* **lowerOperation**

   &quot; `>`&quot;（預設值）或&quot; `>=`&quot;，適用於`lowerValue`

* **上界**

   上界檢查屬性

* **upperOperation**

   &quot; `<`&quot;（預設值）或&quot; `<=`&quot;，適用於`lowerValue`

* **小數點**

   &quot; `true`&quot;（如果選中的屬性類型為Decimal）

### 相對變更範圍{#relativedaterange}

使用相對於目前伺服器時間的時間偏移，比對日期／時間間隔的`JCR DATE`屬性。 您可以使用毫秒值或bugzilla語法`1s 2m 3h 4d 5w 6M 7y`（一秒、二分鐘、三小時、四天、五週、六個月、七年）來指定`lowerBound`和`upperBound`。 首碼為&quot; `-`&quot;，表示目前時間前有負偏移。 如果您只指定`lowerBound`或`upperBound`，則另一個預設為0，表示目前時間。

例如：

* `upperBound=1h` (且無 `lowerBound`)會在下一小時內選取任何項目
* `lowerBound=-1d` (且無 `upperBound`)會在過去24小時內選取任何項目
* `lowerBound=-6M` 選 `upperBound=-3M` 擇6個月到3個月的
* `lowerBound=-1500` 並 `upperBound=5500` 且會選取過去1500毫秒到未來5500毫秒之間的任何項目
* `lowerBound=1d` 然 `upperBound=2d` 後在後天選擇任何

請注意，這並不需要花上多年時間，而且所有月份都是30天。

不支援篩選。

支援Facet擷取，其方式與daterange謂詞相同。

#### 屬性 {#properties-17}

* **上界**

   相對於目前伺服器時間的上限日期界限(毫秒，或`1s 2m 3h 4d 5w 6M 7y`（一秒、二分鐘、三小時、四天、五週、六個月、七年）)，對於負偏移使用&quot;-&quot;

* **下界**

   相對於目前伺服器時間的較低日期界限（毫秒、兩分鐘、三小時、四天、五週、六個月、七年），對於負偏移使用&quot;-&quot;`1s 2m 3h 4d 5w 6M 7y`

### root {#root}

根謂片語。 支援群組的所有功能，並允許設定全域查詢參數。

「root」名稱從未用於查詢，它是隱式的。

#### 屬性 {#properties-18}

* **p.offset**

   表示結果頁面開始的編號，即要略過的項目數

* **p.limit**

   表示頁面大小的數字

* **p.guessTotal**

   建議：避免計算全部結果總和，代價高昂；指出總計上限的數字（例如1000，一個數字可讓使用者對粗略大小有足夠意見回應，而結果較小的數字）或&quot; `true`&quot;，只計算最低所需的`p.offset` + `p.limit`

* **p.expert**

   如果設定為&quot; `true`&quot;，則在結果中包含全文摘錄

* **p.hits**

   （僅適用於JSON servlet）選取點擊以JSON格式寫入的方式，並使用這些標準點擊（可透過ResultHitWriter服務擴充）:

   * **簡單**:

      如`path`、`title`、`lastmodified`、`excerpt`等最小項目（如果已設定）

   * **完整**:

      sling JSON演算節點，其中`jcr:path`表示點擊的路徑：預設情況下，只列出節點的直接屬性，包含一個具有`p.nodedepth=N`的更深樹，其中0表示整個無限子樹；添加`p.acls=true`以包含當前會話對給定結果項的JCR權限(映射：`create` = `add_node`, `modify` = `set_property`, `delete` = `remove`

   * **選擇性**:

      僅在`p.properties`中指定的屬性，此屬性是分隔的空格（在URL中使用&quot;+&quot;）相對路徑清單；如果相對路徑的深度大於1，則表示為子對象；特殊jcr:path屬性包含點擊的路徑

### savedquery {#savedquery}

將持續查詢建立器查詢的所有謂語納入目前查詢中，作為子群組謂語。

請注意，這不會執行額外查詢，但會延伸目前的查詢。

查詢可使用`QueryBuilder#storeQuery()`以程式設計方式保存。 格式可以是多行String屬性或`nt:file`節點，該節點將查詢作為Java屬性格式的文本檔案。

不支援儲存查詢的謂語的Facet擷取。

#### 屬性 {#properties-19}

* **savedquery**

   已保存查詢的路徑（String屬性或`nt:file`節點）

### 類似{#similar}

使用JCR XPath的`rep:similar()`進行相似性搜索。

不支援篩選。 不支援Facet擷取。

#### 屬性 {#properties-20}

* **要**
查找相似節點的節點的相似絕對路徑

* **到**
子節點或 
`.` 對於當前節點(可選，預設為&quot; `.`&quot;)

### 標籤{#tag}

透過指定標籤標題路徑，搜尋以一或多個標籤標籤的內容。

支援Facet擷取。 將使用每個唯一標籤的目前標籤標題路徑，為每個標籤提供區段。

#### 屬性 {#properties-21}

* **標籤**

   要尋找的標籤標題路徑，例如「資產屬性：方向／橫向」

* **N值**

   使用`1_value`、`2_value`、...若要檢查多個標籤（依預設與`OR`結合，若與=true則與`AND`結合）（自5.6起）

* **屬性**

   屬性（或屬性的相對路徑）以查看（預設值&quot; `cq:tags`&quot;）

### tagid {#tagid}

透過指定標籤ID，搜尋以一或多個標籤標籤的內容。

支援Facet擷取。 將使用每個唯一標籤的目前標籤ID來提供區段。

#### 屬性 {#properties-22}

* **tagid**

   要尋找的標籤ID，例如&quot; `properties:orientation/landscape`&quot;

* **N值**

   使用`1_value`、`2_value`、...若要檢查多個標語（依預設與`OR`結合，並搭配`AND`if和=true）（自5.6起）

* **屬性**

   屬性（或屬性的相對路徑）以查看（預設值&quot; `cq:tags`&quot;）

### tagsearch {#tagsearch}

透過指定關鍵字，搜尋以一或多個標籤標籤的內容。 這會先搜尋標題中包含這些關鍵字的標籤，然後將結果限制為僅包含這些標籤的項目。

不支援Facet擷取。

#### 屬性 {#Properties-1}

* **tagsearch**

   在標籤標題中搜尋的關鍵字

* **屬性**

   屬性（或屬性的相對路徑）以查看（預設值&quot; `cq:tags`&quot;）

* **lang**

   僅在特定本地化標籤標題中搜尋(例如&quot; `de`&quot;

* **全部**

   (bool)搜尋整個標籤全文，即所有標題、說明等。 （優先於&quot;l `ang`&quot;）

### 類型 {#type}

將結果限制為特定的JCR節點類型，包括主節點類型或混合類型。 這也會找出該節點類型的子類型。 請注意，儲存庫搜索索引需要涵蓋節點類型，以便高效執行。

支援Facet擷取。 將為結果中的每個唯一類型提供時段。

#### 屬性 {#Properties-2}

* **類型**

   要搜索的節點類型或混合名稱，例如`cq:Page`