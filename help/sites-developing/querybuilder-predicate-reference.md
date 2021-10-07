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
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2310'
ht-degree: 2%

---

# 查詢產生器述詞參考{#query-builder-predicate-reference}

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

在JCR布林屬性上符合。 僅接受值「 `true`」和「 `false`」。 若是「 `false`」，則如果屬性的值為「 `false`」，或完全不存在，則符合。 這對於檢查僅在啟用時設定的布林值標幟非常有用。

繼承的&quot; `operation`&quot;參數沒有意義。

支援小面擷取。 將為每個`true`或`false`值提供貯體，但僅為現有屬性提供。

#### 屬性 {#properties}

* ****
boolproperty相對屬性路徑，例如 
`myFeatureEnabled` 或 `jcr:content/myFeatureEnabled`

* ****
要檢查屬性的值，為&quot; 
`true`&quot; 或 &quot; `false`&quot;

### contentfragment {#contentfragment}

將結果限制為內容片段。

不支援篩選。

不支援Facet擷取。

#### 屬性 {#properties-1}

* ****
contentfragmentIt可與任何值搭配使用，以檢查內容片段。

### dateComparison {#datecomparison}

比較兩個JCR DATE屬性。 可以測試它們是否相等、不等、是否大於或等於。

這是僅限篩選的謂語，無法使用搜尋索引。

#### 屬性 {#properties-2}

* **property1**

   第一個日期屬性的路徑

* **屬性2**

   日期屬性的路徑

* **操作**

   「 `equals`」表示完全匹配，「 `!=`」表示不相等比較，「 `greater`」表示屬性1大於屬性2，「 `>=`」表示屬性1大於或等於屬性2。 預設值為 &quot; `equals`&quot;.

### 達特朗日 {#daterange}

比對日期/時間間隔的JCR DATE屬性。 這使用ISO8601
日期和時間的格式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)，並允許部分表示，例如`YYYY-MM-DD`。 或者，時間戳記可以以自1970年以來的毫秒數，以UTC時區（Unix時間格式）表示。

您可以尋找兩個時間戳記之間的任何項目，任何較新或較指定日期舊的項目，也可以在包含和開啟的間隔之間進行選擇。

支援小面擷取。 將提供貯體「今天」、「本週」、「本月」、「最近3個月」、「今年」、「去年」和「比去年早」。

不支援篩選。

#### 屬性 {#properties-3}

* **屬性**

   `DATE`屬性的相對路徑，例如`jcr:lastModified`

* **lowerBound**

   要檢查屬性的下限日期範圍，例如`2014-10-01`

* **lowerOperation**

   &quot; `>`&quot;（較新）或&quot; `>=`&quot;（at或更新）適用於`lowerBound`。 預設值為&quot; `>`&quot;。

* **upperBound**

   要檢查屬性的上界，例如`2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot;（舊）或&quot; `<=`&quot;（舊）適用於`upperBound`。 預設值為&quot; `<`&quot;。

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

允許建立巢狀條件。 群組可包含巢狀群組。 查詢建立器查詢中的所有內容都隱含在根組中，根組中也可以包含`p.or`和`p.not`參數。

比對兩個屬性其中之一與值的範例：

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

這在概念上`(1_property`或`2_property)`。

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

這在概念上`fulltext AND ( (path AND type) OR (path AND type) )`。 請注意，此類OR連接需要良好的效能索引。

#### 屬性 {#properties-6}

* **p.or**

   如果設為「 `true`」，則組中只能有一個謂詞匹配。 此預設值為「 `false`」，表示所有值必須符合

* **p.not**

   如果設為「 `true`」，則會否定群組（預設為「 `false`」）

* **&lt;predicate>**

   添加嵌套謂詞

* **N_&lt;predicate>**

   新增多個同時的巢狀述詞，例如`1_property, 2_property, ...`

### hasPermission {#haspermission}

將結果限制為當前會話具有指定[JCR權限的項目。](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

這是僅限篩選的謂語，無法使用搜尋索引。 不支援小面擷取。

#### 屬性 {#properties-7}

* **hasPermission**

   目前使用者工作階段必須具有的逗號分隔JCR權限，「全部」才能針對相關節點；例如`jcr:write`、`jcr:modifyAccessControl`

### 語言 {#language}

以特定語言尋找CQ頁面。 這會同時查看頁面語言屬性和頁面路徑，這些路徑通常包括頂層網站結構中的語言或地區設定。

這是僅限篩選的謂語，無法使用搜尋索引。

支援小面擷取。 會為每個唯一語言代碼提供貯體。

#### 屬性 {#properties-8}

* **語言**

   ISO語言代碼，例如&quot; `de`&quot;

### mainasset {#mainasset}

檢查節點是否為DAM主要資產，而非子資產。 基本上，這是不在「子資產」節點內的每個節點。 請注意，這不會檢查`dam:Asset`節點類型。 若要使用此謂語，只要設定&quot; `mainasset=true`&quot;或&quot; `mainasset=false`&quot;，就沒有其他屬性。

這是僅限篩選的謂語，無法使用搜尋索引。

支援小面擷取。 將提供2個貯體給主要和子資產。

#### 屬性 {#properties-9}

* **mainasset**

   布林值，主資產為「 `true`」，子資產為「 `false`」

### memberOf {#memberof}

查找屬於特定[sling資源集合](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)的項。

這是僅限篩選的謂語，無法使用搜尋索引。 不支援Facet擷取。

#### 屬性 {#properties-10}

* **memberOf**

   Sling資源收集路徑

### nodename {#nodename}

在JCR節點名稱上符合。

支援小面擷取。 會為每個唯一節點名稱提供貯體（檔案名稱）。

#### 屬性 {#properties-11}

* **nodename**

   允許通配符的節點名稱模式：`*` =任何字元或無字元，`?` =任何字元，`[abc]` =只有方括弧中的字元

### notexpired {#notexpired}

檢查JCR DATE屬性是否大於或等於目前伺服器時間以比對項目。 這可用來檢查「`expiresAt`」之類的日期屬性，並僅限於尚未過期(`notexpired=true`)或已過期(`notexpired=false`)的日期屬性。

不支援篩選。

支援Facet擷取，方式與Daterange述詞相同。

#### 屬性 {#properties-12}

* **notexpired**

   布林值， &quot; `true`&quot;表示尚未過期（未來日期或等於）, &quot; `false`&quot;表示過期（過去日期）（必要）

* **屬性**

   要檢查的`DATE`屬性的相對路徑（必要）

### orderby {#orderby}

允許對結果進行排序。 如果需要依多個屬性排序，則需要使用數字首碼（例如`1_orderby=first`、`2_oderby=second`）多次新增此述詞。

#### 屬性 {#properties-13}

* **orderby**

   以前導@（例如`@jcr:lastModified`或`@jcr:content/jcr:title`）指示的JCR屬性名稱，或查詢中要排序的其他謂語（例如`2_property`）

* **排序**

   排序方向，降序為&quot; `desc`&quot;，升序為&quot; `asc`&quot;（預設）

* **案例**

   若設為「 `ignore`」，則會讓排序不區分大小寫，表示「a」會在「B」之前；如果空白或遺漏，則排序會區分大小寫，表示「B」在「a」之前

### 路徑 {#path}

在指定路徑內搜尋。

不支援Facet擷取。

#### 屬性 {#properties-14}

* **路徑**

   路徑模式；根據完全不同，整個子樹會相符（例如在xpath中附加`//*`，但請注意這不包括基本路徑）（exact=false，預設值），或僅有完全相符的路徑，其中可包含萬用字元(`*`);如果設定了self，則搜索包含基節點的整個子樹

* **精準**

   如果`exact`為true/on，則確切路徑必須相符，但可包含簡單的萬用字元(`*`)，該萬用字元符合名稱，但不能是&quot; `/`&quot;;如果為false（預設），則包括所有子代（可選）

* **扁平**

   僅搜索直接子項（如在xpath中附加&quot; `/*`&quot;）（僅在「 `exact`」不是true時使用，可選）

* **self**

   搜索子樹，但包括作為路徑指定的基節點（無通配符）

### 屬性 {#property}

在JCR屬性及其值上相符。

支援小面擷取。 會為結果中的每個唯一屬性值提供貯體。

#### 屬性 {#properties-15}

* **屬性**

   屬性的相對路徑，例如`jcr:title`

* **值**

   要檢查屬性的值；會遵循JCR屬性類型來轉換字串

* **N_value**

   使用`1_value`、`2_value`、...檢查多個值（預設為與`OR`結合，若且=true）（自5.3起）`AND`

* **與**

   若結合多個值(`N_value`)與AND（自5.3起），則設為true

* **操作**

   「`equals`」表示完全匹配（預設值），「 `unequals`」表示不相等比較，「 `like`」表示使用`jcr:like` xpath函式（可選），「 `not`」表示不匹配(例如 &quot;`not(@prop)`&quot;在xpath中，值參數將被忽略)或&quot; `exists`&quot;以檢查存在（值可以是true — 屬性必須存在，預設值 — 或false — 與&quot; `not`&quot;相同）

* **深度**

   屬性/相對路徑可存在的萬用字元層級數（例如`property=size depth=2`將檢查節點/大小、節點/&amp;ast;/size和node/&amp;ast;/&amp;ast;/&amp;ast;/ast;/size;/size）

### 範圍屬性 {#rangeproperty}

比對間隔的JCR屬性。 這會套用至具有線性類型的屬性，例如`LONG`、`DOUBLE`和`DECIMAL`。 對於`DATE`，請參閱已優化日期格式輸入的日期範圍謂詞。

您可以定義下界限和上界限，或僅定義其中一個界限。 操作(例如 也可以為上下界限分別指定&quot;小於&quot;或&quot;小於等於&quot;)。

不支援Facet擷取。

#### 屬性 {#properties-16}

* **屬性**

   相對屬性路徑

* **lowerBound**

   下限，檢查屬性

* **lowerOperation**

   &quot; `>`&quot;（預設值）或&quot; `>=`&quot;，適用於`lowerValue`

* **upperBound**

   上限將檢查屬性

* **upperOperation**

   &quot; `<`&quot;（預設值）或&quot; `<=`&quot;，適用於`lowerValue`

* **小數**

   &quot; `true`&quot;，如果選定的屬性類型為「小數」

### relativedaterange {#relativedaterange}

使用相對於當前伺服器時間的時間偏移，將`JCR DATE`屬性與日期/時間間隔匹配。 您可以使用毫秒值或bugzilla語法`1s 2m 3h 4d 5w 6M 7y`（一秒、二分鐘、三小時、四天、五週、六個月、七年）來指定`lowerBound`和`upperBound`。 前置詞為&quot; `-`&quot;，表示目前時間之前的負偏移。 如果僅指定`lowerBound`或`upperBound`，則另一個預設為0，表示當前時間。

例如：

* `upperBound=1h` （且否） `lowerBound`會在接下來的小時內選取任何項目
* `lowerBound=-1d` （且否） `upperBound`會在過去24小時內選取任何項目
* `lowerBound=-6M` 選 `upperBound=-3M` 擇6個月至3個月
* `lowerBound=-1500` 和 `upperBound=5500` 會選取過去1500毫秒到未來5500毫秒之間的任何值
* `lowerBound=1d` 然 `upperBound=2d` 後在後天選擇

請注意，不需要考慮閏年，且所有月份均為30天。

不支援篩選。

支援Facet擷取，方式與Daterange述詞相同。

#### 屬性 {#properties-17}

* **upperBound**

   以毫秒為單位的上限日期(或`1s 2m 3h 4d 5w 6M 7y`（一秒、二分鐘、三小時、四天、五週、六個月、七年）)，與目前伺服器時間相比，使用「 — 」作為負偏移

* **lowerBound**

   以毫秒為單位的下限日期，或以毫秒為單位，或以`1s 2m 3h 4d 5w 6M 7y`（一秒、二分鐘、三小時、四天、五週、六個月、七年）為單位，相對於目前伺服器時間，請使用&quot;-&quot;作為負偏移

### 根 {#root}

根謂片語。 支援組的所有功能，並允許設定全局查詢參數。

查詢中從未使用「root」名稱，此名稱為隱式。

#### 屬性 {#properties-18}

* **p.offset**

   表示結果頁面開始的數字，即要略過的項目數

* **p.limit**

   表示頁面大小的數字

* **p.guessTotal**

   建議：避免計算全部結果總計，而這可能會造成很大成本；指示最大總計的數字（例如1000，該數字為用戶提供了對粗大和精確數字的足夠反饋，以便小結果）或&quot; `true`&quot;以僅計算最小所需的`p.offset` + `p.limit`

* **p.expert**

   如果設為「 `true`」，請在結果中包含全文摘要

* **p.hits**

   （僅限JSON servlet）選取將點擊寫入為JSON的方式，並搭配這些標準點擊（可透過ResultHitWriter服務擴充）:

   * **簡單**:

      `path`、`title`、`lastmodified`、`excerpt`等最小項目（如果已設定）

   * **完整**:

      sling JSON轉譯節點，並搭配`jcr:path`指出點擊的路徑：預設情況下，僅列出節點的直接屬性，包括包含`p.nodedepth=N`的更深的樹，0表示整個無限子樹；新增`p.acls=true`以包含目前工作階段對指定結果項目的JCR權限(對應：`create` = `add_node`, `modify` = `set_property`, `delete` = `remove`

   * **選擇性**:

      `p.properties`中指定的屬性，該屬性是分隔的空格（在URL中使用「+」）相對路徑清單；如果相對路徑的深度大於1，則這些將表示為子對象；特殊的jcr:path屬性包含點擊的路徑

### savedquery {#savedquery}

將持續查詢建立器查詢的所有謂語作為子組謂語包含到當前查詢中。

請注意，這不會執行額外的查詢，而會延伸目前的查詢。

可使用`QueryBuilder#storeQuery()`以寫程式方式保存查詢。 格式可以是多行字串屬性，也可以是`nt:file`節點，該節點以Java屬性格式的文本檔案形式包含查詢。

不支援儲存查詢的述詞的Facet擷取。

#### 屬性 {#properties-19}

* **savedquery**

   儲存查詢的路徑（字串屬性或`nt:file`節點）

### 相似 {#similar}

使用JCR XPath的`rep:similar()`進行相似性搜索。

不支援篩選。 不支援Facet擷取。

#### 屬性 {#properties-20}

* ****
相似絕對路徑到要查找相似節點的節點

* ****
指向子代節點或 
`.` 針對目前節點(選用，預設為「 `.`」)

### 標籤 {#tag}

通過指定標籤標題路徑搜索標籤為一個或多個標籤的內容。

支援小面擷取。 會使用每個唯一標籤的目前標籤標題路徑，為每個標籤提供貯體。

#### 屬性 {#properties-21}

* **標籤**

   要尋找的標籤標題路徑，例如「資產屬性」：方向/橫向」

* **N_value**

   使用`1_value`、`2_value`、...檢查多個標籤（依預設會與`OR`結合，若與=true）（自5.6起）`AND`

* **屬性**

   要查看的屬性（或相對屬性路徑）（預設值&quot; `cq:tags`&quot;）

### tagid {#tagid}

通過指定標籤ID搜索標籤為一個或多個標籤的內容。

支援小面擷取。 會使用每個唯一標籤的目前標籤ID，為每個標籤提供貯體。

#### 屬性 {#properties-22}

* **tagid**

   要尋找的標籤id，例如&quot; `properties:orientation/landscape`&quot;

* **N_value**

   使用`1_value`、`2_value`、...檢查多個tagid（依預設會與`OR`結合，若且=true）（自5.6起）`AND`

* **屬性**

   要查看的屬性（或相對屬性路徑）（預設值&quot; `cq:tags`&quot;）

### tagsearch {#tagsearch}

通過指定關鍵字搜索標籤為一個或多個標籤的內容。 這會先搜尋標題中包含這些關鍵字的標籤，然後將結果限制為僅限標籤這些關鍵字的項目。

不支援Facet擷取。

#### 屬性 {#Properties-1}

* **tagsearch**

   要在標籤標題中搜索的關鍵字

* **屬性**

   要查看的屬性（或相對屬性路徑）（預設值&quot; `cq:tags`&quot;）

* **朗**

   僅搜尋特定本地化標籤標題(例如&quot; `de`&quot;

* **全部**

   (bool)搜尋整個標籤全文，即所有標題、說明等。 （優先於&quot;l `ang`&quot;）

### 類型 {#type}

將結果限制為特定的JCR節點類型，主節點類型或混合類型。 這也會找到該節點類型的子類型。 請注意，儲存庫搜索索引需要涵蓋節點類型，才能有效執行。

支援小面擷取。 將為結果中的每個唯一類型提供貯體。

#### 屬性 {#Properties-2}

* **類型**

   要搜索的節點類型或混合名稱，例如`cq:Page`
