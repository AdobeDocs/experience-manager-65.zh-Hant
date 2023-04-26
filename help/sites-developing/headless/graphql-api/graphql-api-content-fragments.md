---
title: 與內容片段搭配使用的 AEM GraphQL API
description: 了解如何搭配AEM GraphQL API使用Adobe Experience Manager(AEM)中的內容片段進行無頭式內容傳送。
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: cf78742614fd2d35f59905895dfacb83190140cd
workflow-type: tm+mt
source-wordcount: '3250'
ht-degree: 80%

---

# 與內容片段搭配使用的 AEM GraphQL API {#graphql-api-for-use-with-content-fragments}

了解如何搭配AEM GraphQL API使用Adobe Experience Manager(AEM)中的內容片段進行無頭式內容傳送。

與內容片段搭配使用的 AEM GraphQL API，在很大程度上是以標準、開放原始碼的 GraphQL API 為基礎。

在 AEM 中使用 GraphQL API 可以在 Headless CMS 實作中高效率地將內容片段傳遞給 JavaScript 用戶端：

* 避免與 REST 一樣的反覆 API 要求，
* 確保傳遞限於特定要求，
* 允許大量傳遞需要呈現的內容做為對單一 API 查詢的回應。

>[!NOTE]
>
>GraphQL目前用於Adobe Experience Manager(AEM)的兩種（個別）情況：
>
>* [AEM Commerce 透過 GraphQL 取用來自 Commerce 平台的資料](/help/commerce/cif/integrating/magento.md)。
>* AEM 內容片段與 AEM GraphQL API (基於標準 GraphQL 的自訂實作) 搭配運作，以傳遞結構化內容以供您的應用程式使用。


## 必備條件 {#prerequisites}

使用GraphQL的客戶應安裝包含GraphQL索引套件1.0.5的AEM內容片段。請參閱 [發行說明](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) 以取得詳細資訊。

## GraphQL API {#graphql-api}

GraphQL 是：

* 「*...API 的查詢語言和使用現有資料完成這些查詢的執行階段。GraphQL 可完整清楚地描述 API 中的資料，使用戶端能夠準確地要求所需內容，別無其他，如此可輕鬆地隨著時間發展 API，造就強大的開發人員工具。*」。

   請參閱 [GraphQL.org](https://graphql.org)

* 「*...靈活 API 層的開放規格。將 GraphQL 置於現有後端之上，可比以往更快速地建置產品....*」。

   請參閱[探索 GraphQL](https://www.graphql.com)。

* *「...一種資料查詢語言和規格，由 Facebook 於 2012 年在內部開發，然後於 2015 年公開原始碼。它提供了 REST 式架構的替代方案，目的是提高開發人員的生產力並盡量減少傳輸的資料量。GraphQL 用於生產環境，數百個各種規模的組織都在使用...」*

   請參閱 [GraphQL 基礎](https://foundation.graphql.org/)。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

有關 GraphQL API 的更多資訊，請參閱以下章節 (以及許多其他資源)：

* 位於 [graphql.org](https://graphql.org)：

   * [GraphQL 簡介](https://graphql.org/learn)

   * [GraphQL 規格](https://spec.graphql.org/)

* 位於 [graphql.com](https://graphql.com)：

   * [指南](https://www.graphql.com/guides/)

   * [教學課程](https://www.graphql.com/tutorials/)

   * [案例研究](https://www.graphql.com/case-studies/)

GraphQL for AEM 實作是以標準 GraphQL Java 庫為基礎。請參閱：

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub 上的 GraphQL Java](https://github.com/graphql-java)

### GraphQL 術語 {#graphql-terminology}

GraphQL 使用以下項目：

* **[查詢](https://graphql.org/learn/queries/)**

* **[結構描述和類型](https://graphql.org/learn/schema/)**：

   * 結構描述是由 AEM 根據內容片段模型所產生。
   * 使用您的結構描述，GraphQL 呈現 GraphQL for AEM 實作可用的類型和操作。

* **[欄位](https://graphql.org/learn/queries/#fields)**

* **[GraphQL 端點](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#graphql-aem-endpoint)**
   * AEM 中回應 GraphQL 查詢並提供 GraphQL 結構描述存取權的路徑。

   * 如需詳細資訊，請參閱[啟用 GraphQL 端點](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)。

請參閱 [(GraphQL.org) GraphQL 簡介](https://graphql.org/learn/) 了解完整的詳細資訊，包括[最佳做法](https://graphql.org/learn/best-practices/)。

### GraphQL 查詢類型 {#graphql-query-types}

使用 GraphQL，您可以執行查詢以傳回以下兩者之一：

* **單一項目**

* **[項目清單](https://graphql.org/learn/schema/#lists-and-non-null)**

AEM 提供將查詢 (兩種類型) 轉換為[](/help/sites-developing/headless/graphql-api/persisted-queries.md)持續性查詢的功能，可由 Dispatcher 和 CDN 快取。

### GraphQL 查詢最佳做法 (Dispatcher 和 CDN) {#graphql-query-best-practices}

[持續性查詢](/help/sites-developing/headless/graphql-api/persisted-queries.md)是建議用於發佈執行個體的方法，如下：

* 它們被快取
* 由AEM集中管理

<!-- is this fully accurate? -->
>[!NOTE]
>
>作者上通常沒有dispatcher/CDN，因此使用持續的查詢不會提高效能；除了測試它們。

不建議使用 POST 要求的 GraphQL 查詢，因為它們不會被快取，因此在預設執行個體上，Dispatcher 設定為阻擋此類查詢。

雖然 GraphQL 也支援 GET 要求，但這些要求可能會達到限制 (例如 URL 的長度)，而使用持續性查詢可以避免此狀況。

>[!NOTE]
>
>執行直接查詢的功能可能會在未來的某個時間被淘汰。

## GraphiQL介面 {#graphiql-interface}

標準的實施 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) 介面可與AEM GraphQL搭配使用。

>[!NOTE]
>
>GraphiQL 包含在 AEM 的所有環境中 (但只有在您配定端點時才可存取/可見)。
>
>在先前版本，需要套件來安裝 GraphiQL IDE。如果您已安裝，現在可以將其移除。

此介面允許您直接輸入和測試查詢。

例如：

* `http://localhost:4502/content/graphiql.html`

這提供語法醒目提示、自動完成、自動建議等功能，以及歷史記錄和線上檔案：

![GraphiQL 介面](assets/cfm-graphiql-interface.png "GraphiQL 介面")

>[!NOTE]
>
>如需詳細資訊，請參閱 [使用GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md).

## 作者和發佈環境的使用案例 {#use-cases-author-publish-environments}

使用案例取決於AEM環境的類型：

* 發佈環境：用於：
   * 為 JS 應用程式查詢資料 (標準使用案例)

* 作者環境：用於：
   * 為「內容管理目的」查詢資料：
      * AEM中的GraphQL目前是唯讀API。
      * REST API 可用於 CR(u)D 操作。

## 權限 {#permission}

權限是存取資產所需的權限。

GraphQL 查詢是在基礎要求之 AEM 使用者的許可下執行的。如果使用者沒有某些片段 (儲存為資產) 的讀取權限，它們將不會包含在結果集中。

此外，使用者必須可以存取 GraphQL 端點才能執行 GraphQL 查詢。

## 結構描述產生 {#schema-generation}

GraphQL 是強式類型 API，這表示資料必須結構明確並按類型組織。

GraphQL 規格提供了一系列指南，說明如何建立健全的 API 來查詢特定執行個體上的資料。為此，用戶端需要擷取[結構描述](#schema-generation)，其中包含查詢所需的所有類型。

對於內容片段，GraphQL 結構描述 (結構和類型) 是以&#x200B;**啟用的**[內容片段模型](/help/assets/content-fragments/content-fragments-models.md)及其資料類型為基礎。

>[!CAUTION]
>
>所有 GraphQL 結構描述 (衍生自已&#x200B;**啟用**&#x200B;的內容片段模型) 都可透過 GraphQL 端點讀取。
>
>這表示您必須確保沒有敏感資料，因為它可能會以這種方式洩露；例如，這包括可以在模型定義中做為欄位名稱出現的資訊。

例如，如果使用者建立的內容片段模型稱為 `Article`，則AEM會產生物件 `article` 屬於 `ArticleModel`. 此類型中的欄位對應於模型中定義的欄位和資料類型。

1. 內容片段模型：

   ![與 GraphQL 搭配使用的內容片段模型](assets/cfm-graphqlapi-01.png "與 GraphQL 搭配使用的內容片段模型")

1. 對應的 GraphQL 結構描述 (來自 GraphiQL 自動文件的輸出)：
   ![根據內容片段模型的 GraphQL 結構描述](assets/cfm-graphqlapi-02.png "根據內容片段模型的 GraphQL 結構描述")

   此顯示產生的類型 `ArticleModel` 包含多個[欄位](#fields)。

   * 其中三個已由使用者控制：`author`、`main` 和 `referencearticle`。

   * 其他欄位是由AEM自動新增的，是提供特定內容片段相關資訊的實用方法；在本例中， `_path`, `_metadata`, `_variations`. 這些 [Helper 欄位](#helper-fields)前面加上 `_` 以區分是使用者定義的還是自動產生的。

1. 使用者根據文章模型建立內容片段後，就可以透過 GraphQL 對其進行查詢。例如，請參閱[範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#graphql-sample-queries) (根據[與 GraphQL 搭配使用的範例內容片段結構](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql))。

在 GraphQL for AEM 中，結構描述是靈活的。這表示著每次建立、更新或刪除內容片段模型時都會自動產生它。當您更新內容片段模型時，資料結構描述快取也會重新整理。

Sites GraphQL 服務偵聽 (在背景) 對內容片段模型所做的任何修改。當偵測到更新時，只有該部分的結構描述會重新產生。這種最佳化作業可以節省時間並提供穩定性。

例如，您可以：

1. 安裝包含 `Content-Fragment-Model-1` 和 `Content-Fragment-Model-2` 的套件：

   1. 將產生 `Model-1` 和 `Model-2` 的 GraphQL 類型。

1. 然後修改 `Content-Fragment-Model-2`：

   1. 只有 `Model-2` GraphQL 類型會更新。

   1. 而 `Model-1` 將保持不變。

>[!NOTE]
>
>如果您想透過 REST API 或其他方式對內容片段模型進行大量更新，請務必注意這一點。

結構描述透過與 GraphQL 查詢相同的端點提供服務，用戶端處理以 `GQLschema` 副檔名呼叫結構描述這一事實。例如，對 `/content/cq:graphql/global/endpoint.GQLschema` 執行簡單的 `GET` 要求，將導致內容類型為 `text/x-graphql-schema;charset=iso-8859-1` 的結構描述輸出。

### 結構描述產生 - 未發佈的模型 {#schema-generation-unpublished-models}

巢狀內嵌內容片段時，可能會發佈父內容片段模型，但不會發佈被參考的模型。

>[!NOTE]
>
>AEM UI 可防止這種情況發生，但如果以程式設計方式或使用內容套件進行發佈，則可能會發生這種情況。

發生這種情況時，AEM 會為父內容片段模型產生&#x200B;*不完整*&#x200B;結構描述。這表示相依於未發佈模型的片段參考已從結構描述中刪除。

## 欄位 {#fields}

在結構描述中有個別欄位，分成兩個基本類別：

* 產生的欄位。

   一系列[資料類型](#data-types)用於根據內容片段模型的設定方式建立欄位。欄位名稱取自 **屬性名稱** 欄位 **資料類型**.

   * 還有 **呈現為** 屬性，因為使用者可以設定某些資料類型；例如，作為單行文字或多欄位。

* GraphQL for AEM 也會產生許多 [Helper 欄位](#helper-fields)。

   這些用於識別內容片段，或用於取得有關內容片段的詳細資訊。

### 資料類型 {#data-types}

GraphQL for AEM 支援類型清單。表示所有支援的內容片段模型資料類型和對應的 GraphQL 類型：

| 內容片段模型 - 資料類型 | GraphQL 類型 | 說明 |
|--- |--- |--- |
| 單行文字 | `String`, `[String]` |  用於簡單字串，例如作者名稱、位置名稱等。 |
| 多行文字 | `String` |  用於輸出文字，例如文章正文 |
| 數字 |  `Float`, `[Float]` | 用於顯示浮點數和正規數 |
| 布林值 |  `Boolean` |  用於顯示核取方塊 → 簡單的 true/false 陳述式 |
| 日期和時間 | `Calendar` |  用於以ISO 8086格式顯示日期和時間。 視所選類型而定，AEM GraphQL 中可使用三種風格：`onlyDate`、`onlyTime`、`dateTime` |
| 列舉 |  `String` |  用於顯示模型建立時定義之選項清單中的選項 |
|  標記 |  `[String]` |  用於顯示字串清單，字串代表 AEM 中使用的標記 |
| 內容參考 |  `String` |  用於顯示 AEM 中另一個資產的路徑 |
| 片段參考 |  *模型類型* <br><br>單一欄位： `Model`  — 模型類型，直接引用 <br><br>多欄位，其中一個參考型別： `[Model]`  — 類型陣列 `Model`，直接從陣列參照 <br><br>多欄位，包含多個參考類型： `[AllFragmentModels]`  — 所有模型類型的陣列，從具有聯合類型的陣列引用 |  用於參照建立模型時定義的特定模型類型的一或多個內容片段 |

{style="table-layout:auto"}

### Helper 欄位 {#helper-fields}

除了使用者產生之欄位的資料類型外，GraphQL for AEM 也會產生許多 *Helper* 欄位，以協助識別內容片段，或提供有關內容片段的其他資訊。

#### 路徑 {#path}

路徑欄位作為 GraphQL 中的標識符。它代表 AEM 存放庫中內容片段資產的路徑。我們選擇此作為內容片段的識別碼，因為它：

* 在 AEM 中是唯一的，
* 容易撷取。

下列程式碼會顯示根據內容片段模型建立的所有內容片段路徑 `Person`.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

若要撷取特定類型的單一內容片段，您還需要先確定其路徑。例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
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

透過 GraphQL，AEM 還公開內容片段的中繼資料。中繼資料是描述內容片段的資訊，例如內容片段的標題、縮圖路徑、內容片段的說明、建立日期等。

由於中繼資料是透過結構描述編輯器產生的，因此沒有特定的結構，所以實作 `TypedMetaData` GraphQL 類型來公開內容片段的中繼資料。`TypedMetaData` 公開依以下純量類型群組的資訊：

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

例如，如果你想擷取內容片段的標題，我們知道這個屬性是字串屬性，所以我們會查詢所有的字串中繼資料：

若要查詢中繼資料：

```xml
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

如果檢視產生的 GraphQL 結構描述，則可以檢視所有中繼資料 GraphQL 類型。所有模型類型都具有相同的 `TypedMetaData`。

>[!NOTE]
>
>**一般和陣列中繼資料的區別**
>請記住，`StringMetadata` 和 `StringArrayMetadata` 都是指儲存在存放庫的中繼資料，而不是擷取它們的方式。
>
>例如，呼叫 `stringMetadata` 欄位，您將收到以 `String` 儲存在存放庫之所有中繼資料的陣列，如果呼叫 `stringArrayMetadata`，則會收到以 `String[]` 儲存在存放庫之所有中繼資料的陣列。

請參閱[中繼資料的範例查詢 - 列出 GB 獎項的中繼資料](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-metadata-awards-gb)。

#### 變化 {#variations}

`_variations` 欄位已實作以簡化查詢內容片段具有的變化。例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

請參閱[範例查詢 - 所有具有名稱變化的城市](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation)。

>[!NOTE]
>
>如果內容片段不存在給定的變化，則主變化將作為 (備援) 預設值傳回。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL 變數 {#graphql-variables}

GraphQL 允許在查詢中放置變數。有關詳細資訊，您可以參閱[用於變數的 GraphQL 文件](https://graphql.org/learn/queries/#variables)。

例如，若要取得類型的所有內容片段 `Article` 具有特定變數時，您可以指定變數 `variation` 在GraphiQL中。

![GraphQL 變數](assets/cfm-graphqlapi-03.png "GraphQL 變數")

```xml
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

在 GraphQL 中，可以根據變數變更查詢，稱為 GraphQL 指示詞。

例如，您可以根據變數 `includePrice`，在對所有 `AdventureModels` 的查詢中加入 `adventurePrice` 欄位。

![GraphQL 指示詞](assets/cfm-graphqlapi-04.png "GraphQL 指示詞")

```xml
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

例如，下列（基本）查詢會篩選名稱為 `Jobs` 或 `Smith`:

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

如需進一步範例，請參閱：

* [GraphQL for AEM 擴充功能](#graphql-extensions) 的詳細資訊

* [使用此範例內容和結構的範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 以及準備用於範例查詢的[範例內容和結構](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql) 

* [以 WKND 專案為基礎的範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL for AEM - 擴充功能摘要 {#graphql-extensions}

使用 GraphQL for AEM 進行查詢的基本操作符合標準 GraphQL 規格。使用 GraphQL for AEM 進行查詢，有一些擴充功能：

* 如果您需要單一結果：
   * 使用模型名稱，例如城市

* 如果您期望結果清單：
   * 新增 `List` 到模型名稱，例如 `cityList`
   * 請參閱[範例查詢 - 所有城市的所有資訊](#sample-all-information-all-cities)

* 篩選 `includeVariations` 包含在 `List` 查詢類型。  若要擷取查詢結果中的內容片段變化，請 `includeVariations` 篩選器必須設為 `true`.

   >[!CAUTION]
   >篩選 `includeVariations` 不能與系統生成的欄位一起使用 `_variation`.

* 如果要使用邏輯 OR：
   * 使用 ` _logOp: OR`
   * 請參閱[範例查詢 - 姓名為「Jobs」或「Smith」的所有人員](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-persons-jobs-smith)

* 邏輯 AND 也存在，但 (通常) 是隱含的

* 您可以查詢與內容片段模型內欄位相對應的欄位名稱
   * 請參閱[範例查詢 - 公司 CEO 和員工的完整詳細資料](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-full-details-company-ceos-employees)

* 除了模型內的欄位外，還有一些系統產生的欄位 (前面有底線)：

   * 對於內容：

      * `_locale`：顯示語言，根據語言管理員
         * 請參閱[範例查詢：給定地區設定的多個內容片段](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-given-locale)
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
         >如果內容片段不存在給定的變化，則主變化將作為 (備援) 預設值傳回。

         >[!CAUTION]
         >系統產生的欄位 `_variation` 無法與篩選器搭配使用 `includeVariations`.

         * 請參閱[範例查詢 - 所有具有名稱變化的城市](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation)
      * `_tags` :顯示包含標籤之內容片段或變體的ID;這是 `cq:tags` 識別碼。

         * 請參閱 [查詢示例 — 標籤為城市分行的所有城市的名稱](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-names-all-cities-tagged-city-breaks)
         * 請參閱 [附加特定標籤之指定模型的內容片段變異查詢範例](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-fragment-variations-given-model-specific-tag)

         >[!NOTE]
         >
         >您也可以列出內容片段的中繼資料來查詢標籤。
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

   * 如果請求的變異不存在於巢狀片段中，則 **主版** 將會傳回變數。

### CORS 篩選器 {#cors-filter}

>[!NOTE]
>
>如需 AEM 中 CORS 資源共用原則的詳細概述，請參閱[了解跨原始資源共用 (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors))。

若要存取GraphQL端點，必須在客戶Git存放庫中設定CORS原則。 做法是為所需端點新增適當的 OSGi CORS 設定。

此配置必須指定受信任的網站源 `alloworigin` 或 `alloworiginregexp` 必須授予其存取權。

例如，若要授予 GraphQL 端點  和 `https://my.domain` 之持續性查詢端點的存取權，您可以使用：

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

除了CORS設定，反向連結篩選器還必須設定為允許從第三方主機存取。

若要這麼做，請新增適當的OSGi反向連結篩選設定檔案，該設定檔案可：

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
>* 確保敏感資訊沒有公開
>* 不要使用萬用字元 [*] 語法；這將停用對 GraphQL 端點的已驗證存取，並將其公開給整個世界。


>[!CAUTION]
>
>所有 GraphQL [結構描述](#schema-generation) (衍生自&#x200B;**已啟用**&#x200B;的內容片段模型) 都可透過 GraphQL 端點讀取。
>
>這表示您必須確保沒有敏感資料，因為它可能會以這種方式洩露；例如，這包括可以在模型定義中做為欄位名稱出現的資訊。

## 驗證 {#authentication}

請參閱[針對內容片段之遠端 AEM GraphQL 查詢的驗證](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md)。

## 常見問題 {#faqs}

出現的問題：

1. **問題**：「*GraphQL API for AEM 與查詢產生器 API 有何不同？*」

   * **答案**：
「*AEM GraphQL API 可讓您完全控制 JSON 輸出，是業界的查詢內容標準。
在未來，AEM 計劃投資 AEM GraphQL API。*」

## 教學課程 - AEM Headless 和 GraphQL 快速入門 {#tutorial}

正在尋找實作教學課程？查看[AEM Headless 和 GraphQL 快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端對端教學課程，說明如何在 Headless CMS 情境下使用 AEM GraphQL API 建立和公開內容並供外部應用程式取用。
