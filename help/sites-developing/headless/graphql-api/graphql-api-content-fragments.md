---
title: 與內容片段搭配使用的 AEM GraphQL API
description: 瞭解如何在Adobe Experience Manager (AEM)中使用內容片段搭配AEM GraphQL API來進行Headless內容傳送。
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 47aac4b19bfbd29395fb09f3c27c981e7aa908f6
workflow-type: tm+mt
source-wordcount: '4984'
ht-degree: 54%

---

# 與內容片段搭配使用的 AEM GraphQL API {#graphql-api-for-use-with-content-fragments}

瞭解如何在Adobe Experience Manager (AEM)中使用內容片段搭配AEM GraphQL API來進行Headless內容傳送。

與內容片段搭配使用的AEM GraphQL API很大程度上取決於標準的開放原始碼GraphQL API。

在 AEM 中使用 GraphQL API 可以在 Headless CMS 實作中高效率地將內容片段傳遞給 JavaScript 用戶端：

* 避免與 REST 一樣的反覆 API 要求，
* 確保傳遞限於特定要求，
* 允許大量傳遞需要呈現的內容做為對單一 API 查詢的回應。

>[!NOTE]
>
>GraphQL用於Adobe Experience Manager (AEM)中的兩種（不同）情況：
>
>* [AEM Commerce 透過 GraphQL 取用來自 Commerce 平台的資料](/help/commerce/cif/integrating/magento.md)。
>* AEM 內容片段與 AEM GraphQL API (基於標準 GraphQL 的自訂實作) 搭配運作，以傳遞結構化內容以供您的應用程式使用。

## 先決條件 {#prerequisites}

使用GraphQL的客戶應安裝AEM內容片段搭配GraphQL索引套件1.0.5。如需詳細資訊，請參閱[發行說明](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package)。

## GraphQL API {#graphql-api}

GraphQL 是：

* 「*...API 的查詢語言和使用現有資料完成這些查詢的執行階段。GraphQL提供API中資料的完整且可理解的說明。 它讓使用者端能夠精確地要求他們需要的內容，而不需要更多內容，讓API更容易隨時間演化，並啟用強大的開發人員工具。*」

  請參閱 [GraphQL.org](https://graphql.org)

* 「*...靈活 API 層的開放規格。將GraphQL放在現有後端之上，讓您可以以前所未有的速度建置產品....*&quot;。

  請參閱[探索 GraphQL](https://graphql.com/)。

* *&quot;。..一種資料查詢語言和規格，由Facebook在2012年內部開發，然後在2015年公開開放原始碼。 它提供了 REST 式架構的替代方案，目的是提高開發人員的生產力並盡量減少傳輸的資料量。GraphQL 用於生產環境，數百個各種規模的組織都在使用...」*

  請參閱 [GraphQL 基礎](https://graphql.org/foundation)。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all the tools they need to understand and adopt GraphQL.*". 
-->

如需GraphQL API的詳細資訊，請參閱下列章節（以及其他許多資源）：

* 位於 [graphql.org](https://graphql.org)：

   * [GraphQL 簡介](https://graphql.org/learn)

   * [GraphQL 規格](https://spec.graphql.org/)

* 位於 [graphql.com](https://graphql.com)：

   * [教學課程](https://graphql.com/tutorials/)


適用於AEM的GraphQL實作是根據標準GraphQL Java™資料庫。 請參閱：

* [graphQL.org - Java](https://graphql.org/code/#java)

* 在GitHub™[&#128279;](https://github.com/graphql-java)使用GraphQL Java&rbrace;

### GraphQL 術語 {#graphql-terminology}

GraphQL 使用以下項目：

* **[查詢](https://graphql.org/learn/queries/)**

* **[綱要和類型](https://graphql.org/learn/schema/)**：

   * 綱要是由 AEM 根據內容片段模型所產生。
   * 使用您的綱要，GraphQL 呈現 GraphQL for AEM 實作可用的類型和操作。

* **[欄位](https://graphql.org/learn/queries/#fields)**

* **[GraphQL 端點](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#graphql-aem-endpoint)**
   * AEM 中回應 GraphQL 查詢並提供 GraphQL 綱要存取權的路徑。

   * 如需詳細資訊，請參閱[啟用 GraphQL 端點](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)。

請參閱 [(GraphQL.org) GraphQL 簡介](https://graphql.org/learn/) 了解完整的詳細資訊，包括[最佳做法](https://graphql.org/learn/best-practices/)。

### GraphQL 查詢類型 {#graphql-query-types}

使用 GraphQL，您可以執行查詢以傳回以下兩者之一：

* **單一項目**

* **[項目清單](https://graphql.org/learn/schema/#lists-and-non-null)**

AEM提供將查詢（兩種型別）轉換為Dispatcher和CDN快取的[持續查詢](/help/sites-developing/headless/graphql-api/persisted-queries.md)的功能。

### GraphQL 查詢最佳做法 (Dispatcher 和 CDN) {#graphql-query-best-practices}

[持續查詢](/help/sites-developing/headless/graphql-api/persisted-queries.md)是建議用於發佈執行個體的方法：

* 它們被快取
* 由AEM集中管理

<!-- is this fully accurate? -->
>[!NOTE]
>
>通常創作例項上沒有Dispatcher/CDN，因此在那裡使用持續性查詢不會提高效能；除了測試它們。

不建議使用 POST 要求的 GraphQL 查詢，因為它們不會被快取，因此在預設執行個體上，Dispatcher 設定為阻擋此類查詢。

雖然GraphQL也支援GET要求，但這些要求可能會達到限制（例如URL的長度），而使用持續性查詢可以避免這些限制。

如需更多的詳細資訊，請參閱[啟用持續性查詢的快取](#enable-caching-persisted-queries)。

>[!NOTE]
>
>執行直接查詢的功能可能會在未來的某個時間被淘汰。

## GraphiQL介面 {#graphiql-interface}

標準[GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)介面的實作可用於AEM GraphQL。

>[!NOTE]
>
>GraphiQL包含在AEM的所有環境中（但只有在您設定端點時才能存取/顯示）。
>
>在舊版中，您需要有套件才能安裝GraphiQL IDE。 如果您已安裝此套件，現在可以將其移除。

此介面可讓您直接輸入及測試查詢。

例如：

* `http://localhost:4502/content/graphiql.html`

它提供語法醒目提示、自動完成、自動建議等功能，以及歷史記錄和線上檔案：

![GraphiQL 介面](assets/cfm-graphiql-interface.png "GraphiQL 介面")

>[!NOTE]
>
>請參閱[使用GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md)。

## 作者和發佈環境的使用案例 {#use-cases-author-publish-environments}

使用案例可能取決於AEM環境的型別：

* 發佈環境：用於：
   * 為 JS 應用程式查詢資料 (標準使用案例)

* 編寫環境：用於：
   * 為「內容管理目的」查詢資料：
      * AEM中的GraphQL是唯讀API。
      * REST API 可用於 CR(u)D 操作。

## 權限 {#permission}

存取Assets需要許可權。

GraphQL查詢是在基礎請求的AEM使用者許可權下執行。 如果使用者沒有某些片段的讀取存取權(儲存為Assets)，這些片段就不會成為結果集的一部分。

此外，使用者必須擁有GraphQL端點的存取權，才能執行GraphQL查詢。

## 綱要產生 {#schema-generation}

GraphQL是型別API，這表示資料必須清楚建構並依型別組織。

GraphQL 規格提供了一系列指南，說明如何建立健全的 API 來查詢特定執行個體上的資料。若要完成這些准則，使用者端必須擷取[結構描述](#schema-generation)，其中包含查詢所需的所有型別。

對於內容片段，GraphQL 綱要 (結構和類型) 是以&#x200B;**啟用的**&#x200B;[內容片段模型](/help/assets/content-fragments/content-fragments-models.md)及其資料類型為基礎。

>[!CAUTION]
>
>所有 GraphQL 綱要 (衍生自已&#x200B;**啟用**&#x200B;的內容片段模型) 都可透過 GraphQL 端點讀取。
>
>此功能表示您必須確保沒有可用的敏感資料，因為資料可能會以這種方式外洩。 例如，其中包含可作為模型定義中的欄位名稱顯示的資訊。

例如，如果使用者建立了一個名為 `Article` 的內容片段模型，則 AEM 會產成一個 GraphQL 類型 `ArticleModel`。此類型中的欄位對應於模型中定義的欄位和資料類型。此外，它還為操作此類型的查詢建立一些登入點，例如 `articleByPath` 或 `articleList`。

1. 內容片段模型：

   ![與 GraphQL 搭配使用的內容片段模型](assets/cfm-graphqlapi-01.png "與 GraphQL 搭配使用的內容片段模型")

1. 對應的 GraphQL 綱要 (來自 GraphiQL 自動文件的輸出)：
   ![根據內容片段模型的 GraphQL 綱要](assets/cfm-graphqlapi-02.png "根據內容片段模型的 GraphQL 綱要")

   此影像顯示產生的型別`ArticleModel`包含多個[欄位](#fields)。

   * 其中三個已由使用者控制： `author`、`main`和`referencearticle`。

   * 其他欄位則由AEM自動新增，並代表提供特定內容片段相關資訊的實用方法。 在此範例中，
（[協助程式欄位](#helper-fields)） `_path`、`_metadata`、`_variations`。

1. 使用者根據文章模型建立內容片段後，就可以透過 GraphQL 對其進行查詢。例如，請參閱[範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#graphql-sample-queries) (根據[與 GraphQL 搭配使用的範例內容片段結構](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql))。

在 GraphQL for AEM 中，綱要是靈活的。這種靈活性表示每次建立、更新或刪除內容片段模型時都會自動產生。 當您更新內容片段模型時，資料綱要快取也會重新整理。

Sites GraphQL 服務偵聽 (在背景) 對內容片段模型所做的任何修改。當偵測到更新時，只有該部分的綱要會重新產生。這種最佳化作業可以節省時間並提供穩定性。

例如，您可以：

1. 安裝包含 `Content-Fragment-Model-1` 和 `Content-Fragment-Model-2` 的套件：

   1. 會產生 `Model-1` 和 `Model-2` 的 GraphQL 類型。

1. 然後修改 `Content-Fragment-Model-2`：

   1. 只更新`Model-2` GraphQL型別。

   1. 而`Model-1`會維持不變。

>[!NOTE]
>
>此詳細資料務必注意，以備您透過REST API或以其他方式大量更新內容片段模型。

綱要透過與 GraphQL 查詢相同的端點提供服務，用戶端處理以 `GQLschema` 副檔名呼叫綱要這一事實。例如，在`/content/cq:graphql/global/endpoint.GQLschema`上執行簡單的`GET`要求會導致輸出具有內容型別的結構描述： `text/x-graphql-schema;charset=iso-8859-1`。

### 綱要產生 - 未發佈的模型 {#schema-generation-unpublished-models}

巢狀內嵌內容片段時，可能會發佈父內容片段模型，但不會發佈被參考的模型。

>[!NOTE]
>
>AEM使用者介面可防止這種情況的發生，但如果以程式設計方式發佈，或透過內容套件發佈，則可能會發生。

發生這種情況時，AEM會為上層內容片段模型產生&#x200B;*不完整的*&#x200B;結構描述。 這表示從結構描述中移除依賴未發佈模型的片段參考。

## 欄位 {#fields}

在結構描述中，有兩個基本類別的個別欄位：

* 產生的欄位。

  一系列[資料類型](#data-types)用於根據內容片段模型的設定方式建立欄位。欄位名稱取自&#x200B;**資料型別**&#x200B;的&#x200B;**屬性名稱**&#x200B;欄位。

   * 還需要考慮&#x200B;**轉譯為**&#x200B;設定，因為使用者可以設定某些資料型別。 例如，您可以從下拉式清單中選擇`multifield`，將單行文字欄位設定為包含多個單行文字。

* 適用於AEM的GraphQL也會產生數個[協助程式欄位](#helper-fields)。

  這些欄位用於識別內容片段，或取得有關內容片段的詳細資訊。

### 資料類型 {#data-types}

GraphQL for AEM 支援類型清單。表示所有支援的內容片段模型資料類型和對應的 GraphQL 類型：

| 內容片段模型 - 資料類型 | GraphQL 類型 | 說明 |
|--- |--- |--- |
| 單行文字 | `String`、`[String]` |  用於簡單字串，例如作者名稱和位置名稱。 |
| 多行文字 | `String` |  用於輸出文字，例如文章內文 |
| 數字 |  `Float`，`[Float]` | 用於顯示浮點數和正規數 |
| 布林值 |  `Boolean` |  用於顯示核取方塊→簡單的true/false陳述式 |
| 日期和時間 | `Calendar` |  用於以ISO 8086格式顯示日期和時間。 視所選類型而定，AEM GraphQL 中可使用三種風格：`onlyDate`、`onlyTime`、`dateTime` |
| 列舉 |  `String` |  用於顯示模型建立時定義的選項清單中的選項 |
|  標籤 |  `[String]` |  用來顯示代表AEM中所使用標籤的字串清單 |
| 內容參考 |  `String` |  用來顯示指向AEM中另一個資產的路徑 |
| 片段參考 |  *模型類型* <br><br>單一欄位：`Model` - 模型類型，直接參考<br><br>多個欄位，具單一參考類型：`[Model]` - `Model` 類型陣列，從陣列直接參考<br><br>多個欄位，具多個參考類型：`[AllFragmentModels]` - 所有模型類型陣列，從聯合類型的陣列參考 | 用於參考特定模型類型的一個或多個內容片段，在建立模型時定義 |

{style="table-layout:auto"}

### Helper 欄位 {#helper-fields}

除了使用者產生的欄位資料型別之外，適用於AEM的GraphQL也會產生數個&#x200B;*協助程式*&#x200B;欄位，以協助識別內容片段，或提供有關內容片段的額外資訊。

這些 [Helper 欄位](#helper-fields)前面加上 `_` 以區分是使用者定義的還是自動產生的。

#### 路徑 {#path}

路徑欄位作為 AEM GraphQL 中的標識符。它代表 AEM 存放庫中內容片段資產的路徑。選擇此路徑作為內容片段的識別碼，因為它：

* 在 AEM 中是唯一的，
* 容易撷取。

下列程式碼會顯示根據內容片段模式`Person`建立的所有內容片段的路徑。

```graphql
{
  personList {
    items {
      _path
    }
  }
}
```

若要擷取特定型別的單一內容片段，您也必須先決定其路徑。 例如：

```graphql
{
  authorByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

請參閱[範例查詢 - 單一特定城市片段](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)。

#### 中繼資料 {#metadata}

透過 GraphQL，AEM 還公開內容片段的中繼資料。中繼資料是說明內容片段的資訊，如下所示：

* 內容片段的標題
* 縮圖路徑
* 內容片段的說明
* 以及建立日期等。

由於中繼資料是透過綱要編輯器產生的，因此沒有特定的結構，所以實作 `TypedMetaData` GraphQL 類型來公開內容片段的中繼資料。`TypedMetaData`會公開依下列純量型別分組的資訊：

| 欄位 |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

每個純量類型代表單一名稱-值配對或名稱-值配對組，配對中的值屬於該群組的類型。

例如，如果您想擷取內容片段的標題，此屬性為字串屬性，因此您要查詢所有字串中繼資料：

若要查詢中繼資料：

```graphql
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

如果檢視產生的 GraphQL 綱要，則可以檢視所有中繼資料 GraphQL 類型。所有模型類型都具有相同的 `TypedMetaData`。

>[!NOTE]
>
>**一般和陣列中繼資料的區別**
>請記住，`StringMetadata` 和 `StringArrayMetadata` 都是指儲存在存放庫的中繼資料，而不是擷取它們的方式。
>
>例如，呼叫`stringMetadata`欄位，您會收到儲存於儲存庫中所有中繼資料的陣列作為`String`。 如果您呼叫`stringArrayMetadata`，則會收到儲存於存放庫中所有中繼資料的陣列作為`String[]`。

請參閱[中繼資料的範例查詢 - 列出 GB 獎項的中繼資料](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-metadata-awards-gb)。

#### 變化 {#variations}

`_variations` 欄位已實作以簡化查詢內容片段具有的變化。例如：

```graphql
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>`_variations`欄位不包含`master`變數，因為技術上來說，原始資料（在UI中參考為&#x200B;*Master*）不被視為明確變數。

請參閱[範例查詢 - 所有具有名稱變化的城市](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation)。

>[!NOTE]
>
>如果內容片段不存在特定的變化，則原始資料 (也稱為主版變化) 會作為 (備援) 預設值傳回。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL 變數 {#graphql-variables}

GraphQL 允許在查詢中放置變數。如需詳細資訊，請參閱 [GraphQL 變數文件](https://graphql.org/learn/queries/#variables)。

例如，若要取得具有特定變數之型別`Article`的所有內容片段，您可以在GraphiQL中指定變數`variation`。

![GraphQL 變數](assets/cfm-graphqlapi-03.png "GraphQL 變數")

```graphql
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
            _variations
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## GraphQL 指示詞 {#graphql-directives}

在GraphQL中，可以根據變數變更查詢，這稱為GraphQL指示。

例如，您可以根據變數 `includePrice`，在對所有 `AdventureModels` 的查詢中加入 `adventurePrice` 欄位。

![GraphQL 指示詞](assets/cfm-graphqlapi-04.png "GraphQL 指示詞")

```graphql
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## 篩選 {#filtering}

您還可以在 GraphQL 查詢中使用篩選來傳回特定資料。

篩選使用以邏輯運算子和運算式的語法。

最不可部分完成的部分是可套用到特定欄位內容的單一運算式。它將欄位內容與特定的常數值進行比較。

例如，下列運算式會比較欄位內容與值`some text`，如果內容等於值，則成功。 否則，運算式會失敗。：

```graphql
{
  value: "some text"
  _op: EQUALS
}
```

以下運算子可用於將欄位與特定值相比較：

| 運算子 | 類型 | 運算式成功，如果... |
|--- |--- |--- |
| `EQUALS` | `String`, `ID`, `Boolean` | ...值與欄位內容相同 |
| `EQUALS_NOT` | `String`, `ID` | ...值與欄位內容&#x200B;*不*&#x200B;相同 |
| `CONTAINS` | `String` | ...欄位內容包含值（`{ value: "mas", _op: CONTAINS }`符合`Christmas`、`Xmas`、`master`、...） |
| `CONTAINS_NOT` | `String` | ...欄位內容 *不*&#x200B;包含值 |
| `STARTS_WITH` | `ID` | ...識別碼以特定值開頭(`{ value: "/content/dam/", _op: STARTS_WITH`符合`/content/dam/path/to/fragment`，但不符合`/namespace/content/dam/something` |
| `EQUAL` | `Int`、`Float` | ...值與欄位內容相同 |
| `UNEQUAL` | `Int`, `Float` | ...值與欄位內容&#x200B;*不*&#x200B;相同 |
| `GREATER` | `Int`, `Float` | ...欄位內容大於值 |
| `GREATER_EQUAL` | `Int`, `Float` | ...欄位內容大於或等於值 |
| `LOWER` | `Int`, `Float` | ...欄位內容小於值 |
| `LOWER_EQUAL` | `Int`, `Float` | ...欄位內容小於或等於值 |
| `AT` | `Calendar`, `Date`, `Time` | ...欄位內容與值相同（包括時區設定） |
| `NOT_AT` | `Calendar`, `Date`, `Time` | ...欄位內容與值&#x200B;*不*&#x200B;相同 |
| `BEFORE` | `Calendar`, `Date`, `Time` | ...值表示的時間點在欄位內容表示的時間點之前 |
| `AT_OR_BEFORE` | `Calendar`, `Date`, `Time` | ... 值表示的時間點在欄位內容表示的時間點之前或相同 |
| `AFTER` | `Calendar`, `Date`, `Time` | ...值表示的時間點在欄位內容表示的時間點之後 |
| `AT_OR_AFTER` | `Calendar`, `Date`, `Time` | ...值表示的時間點在欄位內容表示的時間點之後或相同 |

有些型別也可讓您指定其他選項，以修改運算式的評估方式：

| 選項 | 類型 | 說明 |
|--- |--- |--- |
| `_ignoreCase` | `String` | 忽略字串的大小寫，例如`time`的值符合`TIME`、`time`、`tImE`... |
| `_sensitiveness` | `Float` | 允許 `float` 值的某些差數視為相同 (以解決由於 `float` 值的內部表示造成的技術限制；應避免，因為此選項可能對效能有負面影響 |

運算式可以使用邏輯運算子 (`_logOp`) 合併成一個集合：

* `OR` — 如果至少有一個運算式成功，則運算式整合功
* `AND` — 如果所有運算式都成功，運算式集就會成功（預設）

每個欄位都可以由自己的運算式集進行篩選。篩選器引數中提及的所有欄位的運算式集最終將由其自己的邏輯運運算元組合。

篩選器定義 (作為 `filter` 引數傳遞給查詢) 包含：

* 每個欄位的子定義(可透過其名稱存取欄位，例如，資料（欄位）型別中`lastName`欄位的篩選器中有`lastName`欄位)
* 每個子定義包含`_expressions`陣列，提供運算式集，以及`_logOp`欄位，定義運算式應結合使用的邏輯運運算元
* 每個運算式由值 (`value` 欄位) 和運算子 (`_operator` 欄位) 定義，應比較欄位內容與

如果您想要將專案與`AND`和`_operator`合併，但想要檢查是否相等，則可以省略`_logOp`，因為這些值是預設值。

以下範例示範一個完整的查詢，該查詢會篩選所有 `lastName`為 `Provo` 或包含 `sjö` 的人，不受大小寫影響：

```graphql
{
  authorList(filter: {
    lastname: {
      _logOp: OR
      _expressions: [
        {
          value: "sjö",
          _operator: CONTAINS,
          _ignoreCase: true
        },
        {
          value: "Provo"
        }
      ]
    }
  }) {
    items {
      lastName
      firstName
    }
  }
}
```

使用選用變數執行GraphQL查詢時，如果特定值是為該選用變數&#x200B;**未提供**，則篩選評估中會忽略該變數。 這表示，查詢結果將包含篩選變數相關屬性的所有值，包括`null`而非`null`。

>[!NOTE]
>
>如果`null`值是為這類變數明確指定的&#x200B;**，則篩選只會比對對應屬性的`null`值。

例如，在下列查詢中，沒有指定屬性`lastName`的值：

```graphql
query getAuthorsFilteredByLastName($authorLastName: String) {
  authorList(filter:
    {
      lastName: {_expressions: {value: $authorLastName}
      }}) {
    items {
      lastName
    }
  }
}
```

將會傳回所有作者：

```graphql
{
  "data": {
    "authorList": {
      "items": [
        {
          "lastName": "Hammer"
        },
        {
          "lastName": "Provo"
        },
        {
          "lastName": "Wester"
        },
        {
          "lastName": null
        },
         ...
      ]
    }
  }
}
```

雖然您也可以對巢狀欄位進行篩選，但不建議這樣做，因為這可能會導致效能問題。

如需進一步範例，請參閱：

* [GraphQL for AEM 擴充功能](#graphql-extensions) 的詳細資訊

* [使用此範例內容和結構的範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 以及準備用於範例查詢的[範例內容和結構](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql) 

* [以 WKND 專案為基礎的範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## 排序 {#sorting}

>[!NOTE]
>
>為獲得最佳效能，請考慮在GraphQL篩選中[更新您的內容片段以進行分頁和排序](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md)。

此功能可讓您根據指定的欄位將查詢結果進行排序。

排序標準：

* 是以逗號分隔的值清單，代表欄位路徑
   * 清單中的第一個欄位會定義主要排序順序
      * 如果主要排序標準的兩個值相等，則使用第二個欄位
      * 如果前兩個條件相等，則會使用第三個欄位，依此類推。
   * 點狀標籤法，也就是`field1.subfield.subfield`等等。
* 具有順序方向 (選擇性)
   * ASC (遞增) 或 DESC (遞減)；預設是套用 ASC
   * 方向可依欄位指定；此功能表示您可以依遞增順序排序一個欄位，依遞減順序排序另一個欄位（名稱、名字DESC）

例如：

```graphql
query {
  authorList(sort: "lastName, firstName") {
    items {
      firstName
      lastName
    }
  }
}
```

同時：

```graphql
{
  authorList(sort: "lastName DESC, firstName DESC") {
    items {
        lastName
        firstName
    }
  }
}
```

您也可以使用 `nestedFragmentname.fieldname`格式，對巢狀片段內的欄位進行排序。

>[!NOTE]
>
>此格式可能會對效能產生負面影響。

例如：

```graphql
query {
  articleList(sort: "authorFragment.lastName")  {
    items {
      title
      authorFragment {
        firstName
        lastName
        birthDay
      }
      slug
    }
  }
}
```

## 分頁 {#paging}

>[!NOTE]
>
>為獲得最佳效能，請考慮在GraphQL篩選中[更新您的內容片段以進行分頁和排序](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md)。

此功能可讓您針對傳回清單的查詢類型執行分頁。提供兩種方法：

* 在 `List` 查詢中，`offset` 和 `limit`
* 在 `Paginated` 查詢中，`first` 和 `after`

### 清單查詢 - offset 和 limit {#list-offset-limit}

在 `...List` 查詢中，您可以使用 `offset` 和 `limit` 傳回特定的結果子集：

* `offset`：指定第一個要傳回的資料集
* `limit`：指定傳回的資料集數量上限

例如，要輸出最多包含五篇文章的結果頁面，從&#x200B;*完整*&#x200B;結果清單中的第五篇文章開始：

```graphql
query {
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        lastName
        firstName
      }
    }
  }
}
```

<!-- When available link to BP and replace "JCR query level" with a more neutral term. -->

<!-- When available link to BP and replace "JCR query result set" with a more neutral term. -->

>[!NOTE]
>
>* 分頁需要穩定的排序順序，才能在多個查詢要求同一結果集的不同頁面時，跨多個查詢正常運作。預設情況下，它使用結果集中每個專案的存放庫路徑來確保順序始終相同。 如果使用不同的排序順序，且無法在JCR查詢層級完成排序，則會對效能產生負面影響。 原因是因為在決定分頁之前，必須將整個結果集載入記憶體。
>
>* 位移越大，從完整JCR查詢結果集中略過專案所需的時間就越多。 針對大型結果集的替代解決方案是使用已分頁查詢搭配 `first` 和 `after` 方法。

### 已分頁查詢 - first 和 after {#paginated-first-after}

`...Paginated` 查詢類型重複使用大部分的 `...List` 查詢類型功能 (篩選、排序)，但沒有使用 `offset`/`limit` 引數，而是使用 `first`/`after`，如 [GraphQL 游標連接規格](https://relay.dev/graphql/connections.htm)所定義。您可以在 [GraphQL 簡介](https://graphql.org/learn/pagination/#pagination-and-edges)中找到不太正式的簡介。

* `first`：要傳回的前 `n` 個項目。
預設為 `50`。
最大值為 `100`。
* `after`：決定請求頁面開頭的游標。 游標所代表的專案不包含在結果集中。 專案的游標由`edges`結構的`cursor`欄位決定。

例如，要輸出最多包含五篇文章的結果頁面，從&#x200B;*完整*&#x200B;結果清單中的特定游標項目開始：

```graphql
query {
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            title
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

<!-- When available link to BP -->
<!-- Due to internal technical constraints, performance will degrade if sorting and filtering is applied on nested fields. Therefore it is recommended to use filter/sort fields stored at root level. For more information, see the [Best Practices document](link). -->

>[!NOTE]
>
>* 依預設，分頁使用代表片段排序的存放庫節點的UUID，以確保結果的順序始終相同。 使用 `sort` 時，會以隱含的方式使用 UUID 以確保唯一排序；即使是排序鍵相同的兩個項目也一樣。
>
>* 由於內部技術限制，如果對巢狀欄位套用排序和篩選，效能會降低。 因此，請使用儲存在根層級的篩選/排序欄位。 如果要查詢大型分頁結果集，也建議使用此技巧。

## GraphQL 持續性查詢 - 在 Dispatcher 中啟用快取 {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>如果啟用了 Dispatcher 的快取，就不需要 [CORS 篩選器](#cors-filter)，因此可以忽略該部分。

根據預設，不啟用 Dispatcher 的持續性查詢快取。因為使用具有多個來源的 CORS (跨來源資源共用) 的客戶必須檢閱，且可能更新其 Dispatcher 設定，因此無法預設啟用。

>[!NOTE]
>
>Dispatcher 不會快取 `Vary` 標頭。
>
>在 Dispatcher 中可以啟用其他 CORS 相關標頭的快取，但在有多個 CORS 來源時可能不足。

### 啟用持續性查詢的快取 {#enable-caching-persisted-queries}

若要啟用持續性查詢的快取，需要對Dispatcher設定檔案進行下列更新：

* `<conf.d/rewrites/base_rewrite.rules>`

  ```xml
  # Allow the dispatcher to be able to cache persisted queries - they need an extension for the cache file
  RewriteCond %{REQUEST_URI} ^/graphql/execute.json
  RewriteRule ^/(.*)$ /$1;.json [PT] 
  ```

  >[!NOTE]
  >
  >Dispatcher會將字尾`.json`新增至所有持續存在的查詢URL，以便可以快取結果。
  >
  >這是為了確保查詢符合Dispatcher對可快取檔案的要求。 如需詳細資訊，請參閱[Dispatcher如何傳回檔案？](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html#how-does-the-dispatcher-return-documents%3F)

* `<conf.dispatcher.d/filters/ams_publish_filters.any>`

  ```xml
  # Allow GraphQL Persisted Queries & preflight requests
  /0110 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
  ```

### Dispatcher 的 CORS 設定 {#cors-configuration-in-dispatcher}

使用 CORS 要求的客戶可能必須在 Dispatcher 中檢閱和更新其 CORS 設定。

* `Origin` 標頭不得透過 Dispatcher 傳遞到 AEM 發佈：
   * 檢查 `clientheaders.any` 檔案。
* 而是必須在 Dispatcher 級別評估 CORS 要求是否為許可的來源。此方法也能確保在所有情況下，CORS 相關標頭正確設定於一個位置。
   * 如此的設定應該新增至 `vhost` 檔案。以下提供一個範例設定；為了簡單起見，僅提供了 CORS 相關部分。您可以根據特定使用案例進行調整。

  ```xml
  <VirtualHost *:80>
     ServerName "publish"
  
     # ...
  
     <IfModule mod_headers.c>
         Header add X-Vhost "publish"
  
          ################## Start of the CORS specific configuration ##################
  
          SetEnvIfExpr "req_novary('Origin') == ''"  CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''"  CORSType=cors CORSProcessing=true CORSTrusted=false
  
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch 'https://%{HTTP_HOST}*'"  CORSType=samedomain CORSProcessing=false
  
          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1
  
          ################## Adapt the regex to match CORS origin for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
  
          # Extract the Origin header 
          SetEnvIfNoCase ^Origin$ ^https://(.*)$ CORSTrustedOrigin=https://$1
  
          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials
  
          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"
  
          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
  
          # Always vary on origin, even if its not there.
          Header merge Vary Origin
  
          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]
  
          ################## End of the CORS specific configuration ##################
  
     </IfModule>
  
     <Directory />
  
         # ...
  
     </Directory>
  
     # ...
  
  </VirtualHost>
  ```

## GraphQL for AEM - 擴充功能摘要 {#graphql-extensions}

使用 GraphQL for AEM 進行查詢的基本操作符合標準 GraphQL 規格。對於使用AEM的GraphQL查詢，有幾個擴充功能：

* 如果您需要單一結果：
   * 使用模型名稱；例如city

* 如果您期望結果清單：
   * 新增 `List` 到模型名稱，例如 `cityList`
   * 請參閱[範例查詢 - 所有城市的所有資訊](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-information-all-cities)

  然後，您可以：

   * [排序結果](#sorting)

      * `ASC`：遞增
      * `DESC`：遞減

   * 使用以下任一方法傳回一頁結果：

      * [清單查詢，使用 offset 和 limit](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#list-offset-limit)
      * [已分頁查詢，使用 first 和 after](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#paginated-first-after)
   * 請參閱[範例查詢 - 所有城市的所有資訊](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-information-all-cities)

* 篩選器`includeVariations`包含在`List`查詢型別中。 若要擷取查詢結果中的內容片段變數，`includeVariations`篩選器必須設定為`true`。

  >[!CAUTION]
  >篩選器`includeVariations`無法與系統產生的欄位`_variation`搭配使用。

* 如果要使用邏輯 OR：
   * 使用 ` _logOp: OR`
   * 請參閱[範例查詢 - 姓名為「Jobs」或「Smith」的所有人員](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-persons-jobs-smith)

* 邏輯 AND 也存在，但 (通常) 是隱含的

* 您可以查詢與內容片段模型內欄位相對應的欄位名稱
   * 請參閱[範例查詢 - 公司 CEO 和員工的完整詳細資料](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-full-details-company-ceos-employees)

* 除了模型內的欄位外，還有一些系統產生的欄位 (前面有底線)：

   * 對於內容：

      * `_locale`：顯示語言，根據語言管理員
         * 請參閱[範例查詢：特定地區設定的多個內容片段](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-given-locale)

      * `_metadata`：顯示片段的中繼資料
         * 請參閱[中繼資料的範例查詢 - 列出 GB 獎項的中繼資料](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-metadata-awards-gb)

      * `_model`：允許查詢內容片段模型 (路徑和標題)
         * 請參閱[從模型進行的內容片段模型範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-content-fragment-model-from-model)

      * `_path`：存放庫中內容片段的路徑
         * 請參閱[範例查詢 - 單一特定城市片段](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)

      * `_reference`：顯示參考；包含 RTF 編輯器中的內聯參考
         * 請參閱[預先擷取參考之多個內容片段的範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-prefetched-references)

      * `_variation`：顯示內容片段中的特定變化

        >[!NOTE]
        >
        >如果內容片段不存在特定的變化，則主變化會作為 (備援) 預設值傳回。

        >[!CAUTION]
        >系統產生的欄位 `_variation` 不能和篩選器 `includeVariations` 同時使用。

         * 請參閱[範例查詢 - 所有具有名稱變化的城市](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation)

      * `_tags` ：用於顯示包含標籤的內容片段或變數的ID；此清單是`cq:tags`個識別碼的陣列。

         * 請參閱[範例查詢 - 所有標記為 City Breaks 的城市名稱](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-names-all-cities-tagged-city-breaks)
         * 請參閱[對附加了特定標記的特定模式之內容片段變化的範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-fragment-variations-given-model-specific-tag)

        >[!NOTE]
        >
        >對標記的查詢還能透過列出內容片段的中繼資料進行。

   * And 操作：

      * `_operator`：套用特定的運算子；`EQUALS`、`EQUALS_NOT`、`GREATER_EQUAL`、`LOWER`、`CONTAINS`、`STARTS_WITH`
         * 請參閱[範例查詢 - 所有姓名沒有「Jobs」的人員](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-persons-not-jobs)
         * 請參閱[範例查詢 - 所有 `_path` 以特定前置詞開頭的冒險](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-all-adventures-cycling-path-filter)

      * `_apply`：套用特定條件；例如，`AT_LEAST_ONCE`
         * 請參閱[範例查詢 - 篩選內含必須至少出現一次之項目的陣列](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-array-item-occur-at-least-once)

      * `_ignoreCase`：查詢時忽略大小寫
         * 請參閱[範例查詢 - 所有名稱包含 SAN 的城市，不區分大小寫](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-cities-san-ignore-case)

* 支援 GraphQL 聯合類型：

   * 使用 `... on`
      * 請參閱[含內容參考之特定模型的內容片段的範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-fragment-specific-model-content-reference)

* 查詢巢狀片段時的備援：

   * 如果要求的變數不存在於巢狀片段中，則會傳回&#x200B;**Master**&#x200B;變數。

### CORS 篩選器 {#cors-filter}

>[!CAUTION]
>
>如果已經啟用 Dispatcher 的[快取，](#graphql-persisted-queries-enabling-caching-dispatcher)就不需要 CORS 篩選器，因此可以忽略該部分。

>[!NOTE]
>
>如需AEM中CORS資源共用原則的詳細概觀，請參閱[瞭解跨原始資源共用(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors))。

若要存取GraphQL端點，請在客戶Git存放庫中設定CORS原則。 此設定可透過為一個或多個所需端點新增適當的OSGi CORS設定檔案來完成。

此設定必須指定必須授與存取權的受信任網站來源`alloworigin`或`alloworiginregexp`。

例如，若要授予`https://my.domain`的GraphQL端點和持續查詢端點的存取權，您可以使用：

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

如果您為端點設定了虛名路徑，您也可以在 `allowedpaths` 中使用它。

### 查閱者篩選器 {#referrer-filter}

除了CORS設定，反向連結篩選條件必須設定為允許從協力廠商主機存取。

若要完成此篩選，請新增適當的OSGi反向連結篩選設定檔，其可：

* 指定受信任網站的主機名稱；`allow.hosts` 或 `allow.hosts.regexp`，
* 授予此主機名稱的存取權。

例如，要授予使用查閱者 `my.domain` 之要求的存取權，您可以：

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>客戶有責任：
>
>* 僅將存取權授予受信任網域
>* 請確定未公開任何敏感資訊
>* 不使用萬用字元[*]語法；此功能會停用對GraphQL端點的已驗證存取權，也會將它公開給整個世界。

>[!CAUTION]
>
>所有 GraphQL [結構描述](#schema-generation) (衍生自&#x200B;**已啟用**&#x200B;的內容片段模型) 都可透過 GraphQL 端點讀取。
>
>此功能表示您必須確保沒有可用的敏感資料，因為這樣可能會洩漏資料。 例如，其中包含可作為模型定義中的欄位名稱顯示的資訊。

## 限制 {#limitations}

為了防止潛在問題，您的查詢有預設限制：

* 查詢不能包含超過1M (1024 * 1024)個字元
* 查詢不能包含超過15000個權杖
* 查詢不能包含超過200000個空白代號

您也需要注意：

* 當您的GraphQL查詢包含兩個（或更多）模型中具有相同名稱的欄位，並且符合以下條件時，將傳回欄位衝突錯誤：

   * 因此，其中：

      * 兩個（或更多模型）可能用作參考；當它們在內容片段參考中定義為允許的&#x200B;**模型型別**&#x200B;時。

     和：

      * 這兩個模型都有相同名稱的欄位；這表示兩個模型中有相同名稱。

     和

      * 這些欄位屬於不同的資料型別。

   * 例如：

      * 當兩個或更多具有不同模型的片段時（例如`M1`、`M2`），可能作為來自另一個片段的參考（內容參考或片段參考）；例如`Fragment1` `MultiField/List`
      * 而且這兩個具有不同模型(`M1`、`M2`)的片段具有名稱相同，但型別不同的欄位。
舉例說明：
         * `M1.Title`為`Text`
         * `M2.Title`為`Text/MultiField`
      * 如果GraphQL查詢包含`Title`欄位，則會發生欄位衝突錯誤。

## 驗證 {#authentication}

請參閱[針對內容片段之遠端 AEM GraphQL 查詢的驗證](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md)。

## 常見問題 {#faqs}

出現的問題：

1. **問題**：「*GraphQL API for AEM 與查詢產生器 API 有何不同？*」

   * **答案**：
「*AEM GraphQL API 可讓您完全控制 JSON 輸出，是業界的查詢內容標準。
AEM計畫在未來投資AEM GraphQL API。*」

## 教學課程 - AEM Headless 和 GraphQL 快速入門 {#tutorial}

正在尋找實作教學課程？查看 [AEM Headless 和 GraphQL 快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端對端教學課程，說明如何在 Headless CMS 情境下使用 AEM GraphQL API 建立和公開內容並供外部應用程式取用。
