---
title: 查詢產生器述詞參考
seo-title: Query Builder Predicate Reference
description: 完成查詢生成器API的謂詞引用。
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
>本頁上的資訊並非詳盡無遺。
>
>有關完整資訊，請參閱下面的清單 **可用謂語** 在查詢生成器調試器控制台上；例如，在：
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>例如，請參見：
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)


## 一般 {#general}

* [根](#root)
* [群組](#group)
* [排序](#orderby)

## 謂語 {#predicates}

* [布爾屬性](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [內容片段](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [日期比較](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [達朗格](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [排除路徑](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [全文](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [具有權限](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [語言](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [維護](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [成員](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [諾登姆](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [諾德皮](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [路徑](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [屬性](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [牧場](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [相對變化](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [保存查詢](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [相似](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [標籤](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [標籤](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [標籤](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [類型](/help/sites-developing/querybuilder-predicate-reference.md#type)

### 布爾屬性 {#boolproperty}

在JCR布爾屬性上匹配。 僅接受值&quot; `true`&quot;和&quot; `false`。 對於「」 `false`&quot;，如果屬性具有值&quot; `false`或者根本不存在。 這對於檢查只有在啟用時才設定的布爾標誌非常有用。

繼承的「」 `operation`&quot;參數沒有意義。

支援小平面提取。 將為每個 `true` 或 `false` 值，但僅用於現有屬性。

#### 屬性 {#properties}

* **布爾屬性**
相對於屬性的路徑，例如 
`myFeatureEnabled` 或 `jcr:content/myFeatureEnabled`

* **值**
值，用於檢查屬性&quot; 
`true`&quot; 或 &quot; `false`&quot;

### 內容片段 {#contentfragment}

將結果限制為內容片段。

不支援篩選。

不支援刻面提取。

#### 屬性 {#properties-1}

* **內容片段**
它可與任何值一起用於檢查內容片段。

### 日期比較 {#datecomparison}

將兩個JCR DATE屬性相互比較。 test是否等於、不等於、大於或大於等。

這是僅篩選謂詞，無法利用搜索索引。

#### 屬性 {#properties-2}

* **property1**

   第一個日期屬性的路徑

* **property2**

   第二個日期屬性的路徑

* **操作**

   &quot; `equals`&quot;以獲得完全匹配， &quot; `!=`&quot;用於不等式比較， &quot; `greater`&quot;表示屬性1大於屬性2, &quot; `>=`&quot;表示屬性1大於或等於屬性2。 預設值為 &quot; `equals`&quot;.

### 達朗格 {#daterange}

將JCR DATE屬性與日期/時間間隔匹配。 這使用ISO8601格式記錄日期和時間( `YYYY-MM-DDTHH:mm:ss.SSSZ`)並允許部分表示，例如 `YYYY-MM-DD`。 或者，時間戳可以以UTC時區（UNIX時間格式）自1970年以來的毫秒數提供。

您可以查找兩個時間戳之間的任何內容，任何比給定日期更新或更舊的內容，也可以在包含時間戳和開啟時間間隔之間進行選擇。

支援小平面提取。 將提供時段「今天」、「本週」、「本月」、「過去3個月」、「今年」、「去年」和「比去年早」。

不支援篩選。

#### 屬性 {#properties-3}

* **屬性**

   到 `DATE` 屬性，例如 `jcr:lastModified`

* **下界**

   綁定到的日期較低，例如 `2014-10-01`

* **lowerOperation（低操作）**

   &quot; `>`&quot;（較新）或&quot; `>=`「（在或更新）」 `lowerBound`。 預設值為&quot; `>`。

* **上界**

   上界檢查屬性，例如 `2014-10-01T12:15:00`

* **上操作**

   &quot; `<`&quot;（較舊）或&quot; `<=`「（在或更舊）」 `upperBound`。 預設值為&quot; `<`。

* **時區**

   未將其指定為ISO-8601日期字串時要使用的時區ID。 預設值是系統的預設時區。

### 排除路徑 {#excludepaths}

從其路徑與規則運算式匹配的結果中排除節點。

這是僅篩選謂詞，無法利用搜索索引。

不支援刻面提取。

#### 屬性 {#properties-4}

* **排除路徑**

   與結果路徑匹配的規則運算式，將匹配的表達式從結果中排除。

### 全文 {#fulltext}

在全文索引中搜索詞。

不支援篩選。

不支援刻面提取。

#### 屬性 {#properties-5}

* **全文**

   全文搜索詞

* **rel路徑**

   屬性或子節點中要搜索的相對路徑。 此屬性是可選的。

### 群組 {#group}

允許生成嵌套條件。 組可以包含嵌套組。 查詢生成器查詢中的所有內容都隱式地位於根組中，根組可以 `p.or` 和 `p.not` 參數。

將兩個屬性中的任一屬性與值匹配的示例：

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

這在概念上 `(1_property` 或 `2_property)`。

嵌套組示例：

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

此搜索術語「」**管理**&quot;在頁面中 `/content/geometrixx/en` 或在資產中 `/content/dam/geometrixx`。

這在概念上 `fulltext AND ( (path AND type) OR (path AND type) )`。 請注意，此類OR連接需要良好的效能索引。

#### 屬性 {#properties-6}

* **p或**

   如果設定為「 `true`&quot; ，組中只能有一個謂詞匹配。 預設為「」 `false`&quot;表示所有項必須匹配

* **不**

   如果設定為「 `true`&quot;，它將組取消(預設為&quot; `false`「)

* **&lt;predicate>**

   添加嵌套謂詞

* **N_&lt;predicate>**

   添加多個同時的嵌套謂詞，如 `1_property, 2_property, ...`

### 具有權限 {#haspermission}

將結果限制為當前會話具有指定的項 [JCR權限。](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

這是僅篩選謂詞，無法利用搜索索引。 它不支援刻面提取。

#### 屬性 {#properties-7}

* **具有權限**

   當前用戶會話必須具有的逗號分隔的JCR權限對於所討論的節點必須具有；例如 `jcr:write`。 `jcr:modifyAccessControl`

### 語言 {#language}

查找特定語言的CQ頁。 這會查看頁面語言屬性和頁面路徑，這些路徑通常包括頂級站點結構中的語言或區域設定。

這是僅篩選謂詞，無法利用搜索索引。

支援小平面提取。 將為每個唯一語言代碼提供儲存桶。

#### 屬性 {#properties-8}

* **語言**

   ISO語言代碼，例如&quot; `de`&quot;

### 維護 {#mainasset}

檢查節點是否是DAM主資產而不是子資產。 這基本上是不在「子元件」節點內的每個節點。 請注意，這不檢查 `dam:Asset` 節點類型。 要使用此謂語，只需設定「 `mainasset=true`&quot;或&quot; `mainasset=false`&quot;沒有其他屬性。

這是僅篩選謂詞，無法利用搜索索引。

支援小平面提取。 將為主集和子集提供2個桶。

#### 屬性 {#properties-9}

* **維護**

   布爾型， &quot; `true`&quot;用於主資產， &quot; `false`&quot;子資產

### 成員 {#memberof}

查找屬於特定成員的項目 [sling資源收集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)。

這是僅篩選謂詞，無法利用搜索索引。 不支援刻面提取。

#### 屬性 {#properties-10}

* **成員**

   Sling資源集合路徑

### 諾登姆 {#nodename}

與JCR節點名稱匹配。

支援小平面提取。 將為每個唯一節點名稱（檔案名）提供儲存桶。

#### 屬性 {#properties-11}

* **諾登姆**

   節點名稱模式允許通配符： `*` =任何字元或無字元， `?` =任何字元， `[abc]` =只有括弧中的字元

### 諾德皮 {#notexpired}

通過檢查JCR DATE屬性是否大於或等於當前伺服器時間來匹配項。 這可用於檢查「」 `expiresAt`&quot;類似date屬性，並僅限於尚未過期的( `notexpired=true`)或已過期( `notexpired=false`)。

不支援篩選。

支援與變更謂詞相同的方式的小平面提取。

#### 屬性 {#properties-12}

* **諾德皮**

   布爾型， &quot; `true`&quot;表示尚未過期（將來日期或等於日期）, &quot; `false`&quot;表示已過期（過去的日期）（必需）

* **屬性**

   相對路徑 `DATE` 要檢查的屬性（必需）

### 排序 {#orderby}

允許對結果進行排序。 如果需要按多個屬性排序，則需要使用數字前置詞多次添加此謂語，如 `1_orderby=first`。 `2_oderby=second`。

#### 屬性 {#properties-13}

* **排序**

   JCR屬性名稱，例如，由前導@表示 `@jcr:lastModified` 或 `@jcr:content/jcr:title`，或查詢中的其他謂語，例如 `2_property`，排序

* **排序**

   排序方向，或&quot; `desc`&quot;表示降序或&quot; `asc`&quot;表示升序（預設）

* **案**

   如果設定為「 `ignore`&quot;將使分類不區分大小寫，即&quot;a&quot;在&quot;B&quot;之前；如果為空或遺漏，則排序區分大小寫，即&quot;B&quot;在&quot;a&quot;之前

### 路徑 {#path}

在給定路徑內搜索。

不支援刻面提取。

#### 屬性 {#properties-14}

* **路徑**

   路徑模式；完全取決於，整個子樹會匹配(如附加 `//*` 在xpath中，但請注意，這不包括基本路徑)(exact=false,default)，或者只有精確的路徑匹配項，其中可以包括通配符( `*`);如果設定了self，則搜索包括基節點的整個子樹

* **精確**

   如果 `exact` 為true/on，精確路徑必須匹配，但它可以包含簡單通配符( `*`)，匹配名稱，但不匹配&quot; `/`「；如果為false（預設），則包括所有後代（可選）

* **平**

   僅搜索直接子項（如附加&quot;） `/*`&quot;在xpath中(僅在&#39; `exact`&#39;不是true，可選

* **self**

   搜索子樹，但包括作為路徑指定的基節點（無通配符）

### 屬性 {#property}

與JCR屬性及其值匹配。

支援小平面提取。 將為結果中的每個唯一屬性值提供儲存段。

#### 屬性 {#properties-15}

* **屬性**

   相對於屬性的路徑，例如 `jcr:title`

* **值**

   值以檢查其屬性；跟隨JCR屬性類型到字串轉換

* **值(_V)**

   使用 `1_value`。 `2_value`,...要檢查多個值(與 `OR` 預設情況下，使用 `AND` 如果和=true)（自5.3）

* **和**

   設定為true以組合多個值( `N_value`)和（自5.3）

* **操作**

   &quot;`equals`&quot;以獲得完全匹配（預設）, &quot; `unequals`&quot;用於不等式比較， &quot; `like`」 `jcr:like` xpath函式（可選）, &quot; `not`&quot;不匹配(例如 &quot;`not(@prop)`&quot;在xpath中，值參數將被忽略)或&quot; `exists`&quot;用於存在檢查(值可以為true — 屬性必須存在，預設 — 或false與&quot;相同 `not`「)

* **深度**

   屬性/相對路徑可以存在的通配符級別數(例如， `property=size depth=2` 將檢查節點/大小、節點/&amp;ast;/size和節點/&amp;ast;/&amp;ast;/size

### 牧場 {#rangeproperty}

將JCR屬性與間隔匹配。 這適用於具有線性類型的屬性，如 `LONG`。 `DOUBLE` 和 `DECIMAL`。 對於 `DATE` 請參閱具有優化日期格式輸入的daterange謂詞。

可定義下界和上界，或只定義其中一個。 操作(例如 也可以分別為下界和上界指定「小於」或「小於或等於」)。

不支援刻面提取。

#### 屬性 {#properties-16}

* **屬性**

   屬性的相對路徑

* **下界**

   下界檢查屬性

* **lowerOperation（低操作）**

   &quot; `>`&quot;（預設）或&quot; `>=`」 `lowerValue`

* **上界**

   上界檢查屬性

* **上操作**

   &quot; `<`&quot;（預設）或&quot; `<=`」 `lowerValue`

* **小數**

   &quot; `true`&quot;如果選中的屬性類型為Decimal

### 相對變化 {#relativedaterange}

匹配項 `JCR DATE` 使用相對於當前伺服器時間的時間偏移對日期/時間間隔的屬性。 可以指定 `lowerBound` 和 `upperBound` 使用毫秒值或bugzilla語法 `1s 2m 3h 4d 5w 6M 7y` （1秒、2分鐘、3小時、4天、5週、6個月、7年）。 前置詞為&quot; `-`&quot;表示當前時間之前的負偏移。 如果僅指定 `lowerBound` 或 `upperBound`，另一個將預設為0，表示當前時間。

例如：

* `upperBound=1h` （否） `lowerBound`)將在下一小時內選擇任何
* `lowerBound=-1d` （否） `upperBound`)會在過去24小時內選擇任何
* `lowerBound=-6M` 和 `upperBound=-3M` 選擇任何6個月到3個月的
* `lowerBound=-1500` 和 `upperBound=5500` 將選擇過去1500毫秒到將來5500毫秒之間的任何內容
* `lowerBound=1d` 和 `upperBound=2d` 會在後天選擇任何

請注意，不考慮閏年，所有月份均為30天。

不支援篩選。

支援與變更謂詞相同的方式的小平面提取。

#### 屬性 {#properties-17}

* **上界**

   限定的上日期（毫秒）或 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分鐘、三小時、四天、五週、六個月、七個月、七年）相對於當前伺服器時間，使用「 — 」作為負偏移量

* **下界**

   以毫秒或以毫秒為單位綁定的較低日期 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分鐘、三小時、四天、五週、六個月、七個月、七年）相對於當前伺服器時間，使用「 — 」作為負偏移量

### 根 {#root}

根謂片語。 支援組的所有功能並允許設定全局查詢參數。

「root」名稱從未在查詢中使用，它是隱式的。

#### 屬性 {#properties-18}

* **p偏移**

   指示結果頁開始的編號，即要跳過的項數

* **p限制**

   指示頁面大小的編號

* **p.guessTotal**

   建議：避免計算全部結果總和，這樣做成本高；一個數字，表示要計數的最大總數（例如1000，該數字為用戶提供了對粗略大小和精確數字的足夠反饋，以便獲得較小結果）或&quot; `true`&quot;只計算最低值 `p.offset` + `p.limit`

* **節選**

   如果設定為「 `true`「 」，在結果中包含全文摘要

* **點擊**

   （僅適用於JSON servlet）選擇將命中寫為JSON的方式，並使用這些標準命中（可通過ResultHitWriter服務擴展）:

   * **簡單**:

      最小項 `path`。 `title`。 `lastmodified`。 `excerpt` （如果設定）

   * **完整**:

      sling節點的JSON呈現，帶 `jcr:path` 指示命中路徑：預設情況下，僅列出節點的直接屬性，包括更深的樹 `p.nodedepth=N`,0表示整個、無限子樹；添加 `p.acls=true` 包括當前會話對給定結果項的JCR權限(映射： `create` = `add_node`。 `modify` = `set_property`。 `delete` = `remove`)

   * **選擇性**:

      僅指定屬性 `p.properties`，是空格分隔（在URL中使用&quot;+&quot;）相對路徑清單；如果相對路徑的深度大於1，則這些深度將表示為子對象；特殊jcr:path屬性包括命中路徑

### 保存查詢 {#savedquery}

將永續查詢生成器查詢的所有謂語作為子組謂語包含到當前查詢中。

請注意，這不會執行額外查詢，而會擴展當前查詢。

可以通過寫程式方式保留查詢 `QueryBuilder#storeQuery()`。 格式可以是多行String屬性或 `nt:file` 節點，該節點將查詢作為Java屬性格式的文本檔案。

不支援對已保存查詢的謂詞進行刻面提取。

#### 屬性 {#properties-19}

* **保存查詢**

   已保存查詢的路徑(String屬性或 `nt:file` 節點)

### 相似 {#similar}

使用JCR XPath的相似性搜索 `rep:similar()`。

不支援篩選。 不支援刻面提取。

#### 屬性 {#properties-20}

* **相似**
要為其查找類似節點的節點的絕對路徑

* **本地**
子節點或 
`.` 對於當前節點(可選，預設值為「 `.`「)

### 標籤 {#tag}

通過指定標籤標題路徑搜索用一個或多個標籤標籤的內容。

支援小平面提取。 將使用每個唯一標籤的當前標籤標題路徑為其提供儲存段。

#### 屬性 {#properties-21}

* **標籤**

   要查找的標籤標題路徑，例如「資產屬性：方向/橫向」

* **值(_V)**

   使用 `1_value`。 `2_value`,...要檢查多個標籤(與 `OR` 預設情況下，使用 `AND` 如果和=true)（自5.6）

* **屬性**

   要查看的屬性（或屬性的相對路徑）(預設值&quot; `cq:tags`「)

### 標籤 {#tagid}

通過指定標籤ID搜索用一個或多個標籤標籤的內容。

支援小平面提取。 將使用每個唯一標籤的當前標籤ID為它們提供儲存桶。

#### 屬性 {#properties-22}

* **標籤**

   要查找的標籤id，例如&quot; `properties:orientation/landscape`&quot;

* **值(_V)**

   使用 `1_value`。 `2_value`,...檢查多個標籤(與 `OR` 預設情況下，使用 `AND` 如果和=true)（自5.6）

* **屬性**

   要查看的屬性（或屬性的相對路徑）(預設值&quot; `cq:tags`「)

### 標籤 {#tagsearch}

通過指定關鍵字搜索標籤有一個或多個標籤的內容。 這將首先搜索標題中包含這些關鍵字的標籤，然後將結果限制為僅包含這些關鍵字的項。

不支援刻面提取。

#### 屬性 {#Properties-1}

* **標籤**

   在標籤標題中搜索的關鍵字

* **屬性**

   要查看的屬性（或屬性的相對路徑）(預設值&quot; `cq:tags`「)

* **朗**

   僅搜索某個本地化標籤標題(例如&quot; `de`「)

* **全部**

   (bool)搜索整個標籤全文，即所有標題、說明等。 (優先於&quot;l&quot; `ang`「)

### 類型 {#type}

將結果限制為特定的JCR節點類型（主節點類型或混合類型）。 這還將查找該節點類型的子類型。 請注意，儲存庫搜索索引需要覆蓋節點類型，以便高效執行。

支援小平面提取。 將為結果中的每種唯一類型提供儲存桶。

#### 屬性 {#Properties-2}

* **類型**

   要搜索的節點類型或混合名稱，例如 `cq:Page`
