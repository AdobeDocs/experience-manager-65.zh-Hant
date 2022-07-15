---
title: 用AEM於內容片段的GraphQL API
description: 瞭解如何將Adobe Experience Manager(AEM)中的內容碎片與AEMGraphQL API一起用於無頭內容傳送。
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: 6f3f88ea0f07c97fa8d7ff3bdd1c89114d12a8a1
workflow-type: tm+mt
source-wordcount: '3986'
ht-degree: 1%

---

# 用AEM於內容片段的GraphQL API {#graphql-api-for-use-with-content-fragments}

瞭解如何將Adobe Experience Manager(AEM)中的內容碎片與AEMGraphQL API一起用於無頭內容傳送。

與內AEM容片段一起使用的GraphQL API主要基於標準的開源GraphQL API。

在中使用GraphQL APIAEM可以在無頭CMS實現中將內容片段高效傳送到JavaScript客戶端：

* 避免像REST一樣的迭代API請求，
* 確保交付僅限於具體要求，
* 允許批量交付作為對單個API查詢的響應的呈現所需的內容。

>[!NOTE]
>
>GraphQL目前在Adobe Experience Manager(AEM)的兩種（單獨）情形中使用：
>
>* [通AEM過GraphQL從Commerce平台消耗資料](/help/commerce/cif/integrating/magento.md)。
>* 內AEM容片段與AEMGraphQL API（基於標準GraphQL的自定義實現）一起工作，以提供結構化內容供您的應用程式使用。


## GraphQL API {#graphql-api}

GraphQL為：

* &quot;*...API的查詢語言和用現有資料完成這些查詢的運行時。 GraphQL提供了對API中資料的完整且易於理解的描述，使客戶能夠準確詢問他們需要什麼，而不需要更多，使API更易於隨時間推移而發展，並支援功能強大的開發人員工具。*。

   請參閱 [GraphQL.org](https://graphql.org)

* &quot;*...靈活API層的開放規範。 將GraphQL置於您現有的後端上，以比以往更快地構建產品……。*。

   請參閱 [瀏覽GraphQL](https://www.graphql.com)。

* *&quot;。..2012年，Facebook在內部開發了資料查詢語言和規範，2015年公開開源。 它提供了基於REST的體系結構的替代方案，目的是提高開發人員的工作效率並最大限度地減少資料傳輸量。 GraphQL由數百個不同規模的組織在生產中使用……」*

   請參閱 [GraphQL基礎](https://foundation.graphql.org/)。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

有關GraphQL API的詳細資訊，請參閱以下各節（包括許多其他資源）:

* 在 [graphql.org](https://graphql.org):

   * [GraphQL簡介](https://graphql.org/learn)

   * [GraphQL規範](https://spec.graphql.org/)

* 在 [graphql.com](https://graphql.com):

   * [參考線](https://www.graphql.com/guides/)

   * [教學課程](https://www.graphql.com/tutorials/)

   * [案例研究](https://www.graphql.com/case-studies/)

用於實現的AEMGraphQL基於標準的GraphQL Java庫。 請參閱：

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub上的GraphQL Java](https://github.com/graphql-java)

### GraphQL術語 {#graphql-terminology}

GraphQL使用以下功能：

* **[查詢](https://graphql.org/learn/queries/)**

* **[方案和類型](https://graphql.org/learn/schema/)**:

   * 架構由基於AEM內容片段模型生成。
   * 使用您的架構，GraphQL將顯示GraphQL允許用於實現的類型和AEM操作。

* **[欄位](https://graphql.org/learn/queries/#fields)**

* **[GraphQL終結點](#graphql-aem-endpoint)**
   * 響應GraphQL查AEM詢並提供對GraphQL架構的訪問的路徑。

   * 請參閱 [啟用GraphQL終結點](#enabling-graphql-endpoint) 的上界。

查看 [(GraphQL.org)GraphQL簡介](https://graphql.org/learn/) 全面詳情，包括 [最佳做法](https://graphql.org/learn/best-practices/)。

### GraphQL查詢類型 {#graphql-query-types}

使用GraphQL，您可以執行查詢以返回以下任一值：

* A **單項**

* A **[條目清單](https://graphql.org/learn/schema/#lists-and-non-null)**

您還可以執行以下操作：

* [已快取的永續查詢](#persisted-queries-caching)

>[!NOTE]
>可以使用test和調試GraphQL查詢 [GraphiQL IDE](#graphiql-interface)。

## GraphQL用於端點AEM {#graphql-aem-endpoint}

端點是用於訪問GraphQL的路AEM徑。 使用此路徑，您（或您的應用）可以：

* 訪問GraphQL架構，
* 發送GraphQL查詢，
* 接收響應（對GraphQL查詢）。

中有兩種端點類型AEM:

* 全域
   * 可供所有站點使用。
   * 此終結點可以使用所有站點配置(在 [配置瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser))。
   * 如果站點配置之間應共用任何內容片段模型，則應在全局站點配置下建立這些模型。
* 站點配置：
   * 對應於在 [配置瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)。
   * 特定於指定的站點/項目。
   * 特定站點配置的終結點將使用來自該特定站點配置的內容片段模型以及來自全局站點配置的內容片段模型。

>[!CAUTION]
>
>內容片段編輯器允許一個站點配置的內容片段引用另一個站點配置的內容片段（通過策略）。
>
>在這種情況下，並非所有內容都可以使用特定於站點配置的終結點進行檢索。
>
>內容作者應控制此情景；例如，考慮將共用內容片段模型置於「全局站點」配置下可能很有用。

全局終結點的GraphQL的AEM儲存庫路徑是：

`/content/cq:graphql/global/endpoint`

您的應用可以在請求URL中使用以下路徑：

`/content/_cq_graphql/global/endpoint.json`

要為GraphQL啟用終結點，AEM您需要：

* [啟用GraphQL終結點](#enabling-graphql-endpoint)
* [發佈GraphQL終結點](#publishing-graphql-endpoint)

### 啟用GraphQL終結點 {#enabling-graphql-endpoint}

要啟用GraphQL終結點，您首先需要具有適當的配置。 請參閱 [內容片段 — 配置瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md)。

>[!CAUTION]
>
>如果 [未啟用內容片段模型的使用](/help/assets/content-fragments/content-fragments-configuration-browser.md)，也請參見Wiki頁。 **建立** 選項。

要啟用相應端點，請執行以下操作：

1. 導航到 **工具**。 **資產**，然後選擇 **圖形QL**。
1. 選擇 **建立**。
1. 的 **建立新GraphQL終結點** 對話框。 您可以在此處指定：
   * **名稱**:端點名稱；可以輸入任何文本。
   * **使用由提供的GraphQL架構**:使用下拉清單選擇所需的站點/項目。

   >[!NOTE]
   >
   >對話框中顯示以下警告：
   >
   >* *如果未妥善管理，GraphQL 端點可能會導致資料安全性和效能問題。在建立端點後，請務必設定適當的權限。*


1. 確認 **建立**。
1. 的 **後續步驟** 對話框將提供到安全控制台的直接連結，以便您能夠確保新建立的終結點具有適當的權限。

   >[!CAUTION]
   >
   >每個人都可以訪問該終結點。 這可能會引起安全問題，因為GraphQL查詢會給伺服器帶來沈重負載。
   >
   >您可以在端點上設定與您的使用案例相適應的ACL。

### 發佈GraphQL終結點 {#publishing-graphql-endpoint}

選擇新端點並 **發佈** 使其在所有環境中都完全可用。

>[!CAUTION]
>
>每個人都可以訪問該終結點。
>
>在發佈實例時，這可能會引起安全問題，因為GraphQL查詢會給伺服器帶來沈重負載。
>
>必須在端點上設定與用例相適應的ACL。

## GraphiQL介面 {#graphiql-interface}

標準的實施 [圖形QL](https://graphql.org/learn/serving-over-http/#graphiql) 介面可用於AEMGraphQL。 這可以是 [已安AEM裝](#installing-graphiql-interface)。

>[!NOTE]
>
>GraphiQL已綁定全局終結點（不與特定站點配置的其他終結點一起使用）。

此介面允許您直接輸入和test查詢。

例如：

* `http://localhost:4502/content/graphiql.html`

這提供了語法突出顯示、自動完成、自動建議等功能，以及歷史記錄和線上文檔：

![GraphiQL介面](assets/cfm-graphiql-interface.png "GraphiQL介面")

### 安裝AEMGraphiQL介面 {#installing-graphiql-interface}

GraphiQL用戶介面可隨專用AEM軟體包一起安裝：這樣 [GraphiQL內容包0.0.6版(2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip) 檔案。

>[!NOTE]
>
>可用的包與AEM6.5.10.0和AEMas a Cloud Service完全相容。

## 作者和發佈環境的使用案例 {#use-cases-author-publish-environments}

使用案例可以取決於環境的類AEM型：

* 發佈環境；用於：
   * 查詢JS應用程式的資料（標準用例）

* 作者環境；用於：
   * 為「內容管理目的」查詢資料：
      * 中的AEMGraphQL當前是只讀API。
      * REST API可用於CR(u)D操作。

## 權限 {#permission}

這些權限是訪問Assets所需的權限。

## 架構生成 {#schema-generation}

GraphQL是強類型API，這意味著資料必須按類型清晰地結構化和組織。

GraphQL規範提供了一系列指導原則，說明如何建立用於查詢特定實例上的資料的強健API。 要執行此操作，客戶端需要獲取 [架構](#schema-generation)，其中包含查詢所需的所有類型。

對於內容片段，GraphQL架構（結構和類型）基於 **已啟用** [內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 以及資料類型。

>[!CAUTION]
>
>所有GraphQL架構（從已導出的內容片段模型派生） **已啟用**)可通過GraphQL終結點讀取。
>
>這意味著您需要確保沒有敏感資料可用，因為敏感資料可能會以這種方式洩露；例如，這包括在模型定義中可以作為欄位名稱顯示的資訊。

例如，如果用戶建立了名為 `Article`，然AEM後生成對象 `article` 是 `ArticleModel`。 此類型中的欄位與模型中定義的欄位和資料類型相對應。

1. 內容片段模型：

   ![用於GraphQL的內容片段模型](assets/cfm-graphqlapi-01.png "用於GraphQL的內容片段模型")

1. 相應的GraphQL架構（從GraphiQL自動文檔輸出）:
   ![基於內容片段模型的GraphQL模式](assets/cfm-graphqlapi-02.png "基於內容片段模型的GraphQL模式")

   這顯示生成的類型 `ArticleModel` 包含 [欄位](#fields)。

   * 其中三個由用戶控制： `author`。 `main` 和 `referencearticle`。

   * 其他欄位則由自動添加AEM，並代表提供某一內容片段資訊的有用方法；在本例中， `_path`。 `_metadata`。 `_variations`。 這些 [幫助器欄位](#helper-fields) 標有前面 `_` 區分用戶定義的內容和自動生成的內容。

1. 用戶根據文章模型建立內容片段後，可通過GraphQL查詢。 有關示例，請參見 [示例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (基於 [用於GraphQL的內容片段結構示例](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql))。

在GraphQL中AEM，架構是靈活的。 這意味著每次建立、更新或刪除內容片段模型時，都會自動生成它。 更新內容片段模型時，還會刷新資料架構快取。

站點GraphQL服務監聽（在後台）對內容片段模型進行的任何修改。 檢測到更新後，只會重新生成該模式的那一部分。 這種優化節省了時間並提供了穩定性。

例如，如果：

1. 安裝包含 `Content-Fragment-Model-1` 和 `Content-Fragment-Model-2`:

   1. GraphQL類型 `Model-1` 和 `Model-2` 生成。

1. 然後修改 `Content-Fragment-Model-2`:

   1. 僅 `Model-2` 將更新GraphQL類型。

   1. 然而 `Model-1` 將保持不變。

>[!NOTE]
>
>請注意，如果要通過REST api或其他方式對內容片段模型進行批量更新，則必須注意這一點。

通過與GraphQL查詢相同的終結點來提供架構，而客戶端則處理使用擴展調用架構的事實 `GQLschema`。 例如，執行簡單 `GET` 請求 `/content/cq:graphql/global/endpoint.GQLschema` 將導致輸出具有Content-type的架構： `text/x-graphql-schema;charset=iso-8859-1`。

### 架構生成 — 未發佈的模型 {#schema-generation-unpublished-models}

嵌套內容片段時，可能會發佈父內容片段模型，但引用的模型未發佈。

>[!NOTE]
>
>UI可AEM以阻止此情況發生，但如果以寫程式方式或使用內容包進行發佈，則可能發生此情況。

當發生這種情況時，AEM將生成 *不完整* 父內容片段模型的架構。 這意味著從架構中刪除依賴於未發佈模型的片段引用。

## 欄位 {#fields}

在架構中，有兩個基本類別的單個欄位：

* 生成的欄位。

   選擇 [欄位類型](#field-types) 用於根據配置內容片段模型的方式建立欄位。 欄位名稱取自 **屬性名稱** 的 **資料類型**。

   * 還有 **呈現為** 屬性需要考慮，因為用戶可以配置某些資料類型；例如，作為單行文本或多欄位。

* GraphQLAEM還生成 [幫助器欄位](#helper-fields)。

   這些內容用於標識內容片段或獲取有關內容片段的詳細資訊。

### 欄位類型 {#field-types}

用於AEM的GraphQL支援類型清單。 所有支援的內容片段模型資料類型和相應的GraphQL類型都表示：

| 內容片段模型 — 資料類型 | GraphQL類型 | 說明 |
|--- |--- |--- |
| 單行文本 | 字串， [字串] |  用於簡單字串，如作者名、位置名等。 |
| 多行文本 | 字串 |  用於輸出文本，例如文章的正文 |
| 數量 |  浮起， [浮動] | 用於顯示浮點數和常規數 |
| 布林值 |  布林值 |  用於顯示複選框→簡單的true/false語句 |
| 日期和時間 | 日曆 |  用於以ISO 8086格式顯示日期和時間。 根據所選類型，GraphQL中有三種可用的AEM類型： `onlyDate`。 `onlyTime`。 `dateTime` |
| 列舉 |  String |  用於從建立模型時定義的選項清單中顯示選項 |
|  標記 |  [String] |  用於顯示表示中使用的標籤的字串列AEM表 |
| 內容參考資料 |  字串 |  用於在中顯示指向另一個資產的路AEM徑 |
| 片段引用 |  *模型類型* |  用於引用建立模型時定義的特定模型類型的另一個內容片段 |

### 幫助程式欄位 {#helper-fields}

除了用戶生成欄位的資料類型外，GraphQL還AEM生成許多 *幫助* 欄位，以幫助標識內容片段，或提供有關內容片段的其他資訊。

#### 路徑 {#path}

路徑欄位用作GraphQL中的標識符。 它表示儲存庫內的內容片段資AEM產路徑。 我們選擇此作為內容片段的標識符，因為它：

* 在AEM,
* 很容易摘取。

以下代碼將顯示基於內容片段模型建立的所有內容片段的路徑 `Person`。

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

要檢索特定類型的單個內容片段，還需要先確定其路徑。 例如：

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

請參閱 [示例查詢 — 單個特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)。

#### 中繼資料 {#metadata}

通過GraphQL還AEM會顯示內容片段的元資料。 元資料是描述內容片段的資訊，如內容片段的標題、縮略圖路徑、內容片段的說明、建立日期等。

由於元資料是通過架構編輯器生成的，因此沒有特定的結構，因此 `TypedMetaData` 實現了GraphQL類型以公開內容片段的元資料。 `TypedMetaData` 顯示按以下標量類型分組的資訊：

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

每個標量類型都表示單個名稱值對或名稱值對的陣列，其中該對的值屬於其分組的類型。

例如，如果要檢索內容片段的標題，我們知道此屬性是String屬性，因此我們將查詢所有String元資料：

要查詢元資料，請執行以下操作：

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

如果查看生成的GraphQL架構，則可以查看所有元資料GraphQL類型。 所有模型類型都具有相同 `TypedMetaData`。

>[!NOTE]
>
>**正常元資料和陣列元資料的差異**
>記住 `StringMetadata` 和 `StringArrayMetadata` 這兩個選項都引用儲存在儲存庫中的內容，而不是如何檢索它們。
>
>例如，通過調用 `stringMetadata` 欄位中，您將接收儲存在儲存庫中的所有元資料的陣列 `String` ，如果您 `stringArrayMetadata` 您將接收儲存在儲存庫中的所有元資料的陣列 `String[]`。

請參閱 [元資料查詢示例 — 列出標題為GB的獎項的元資料](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)。

#### 變數 {#variations}

的 `_variations` 已實現欄位，以簡化對內容片段的變體的查詢。 例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

請參閱 [示例查詢 — 具有命名變體的所有城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)。

>[!NOTE]
>
>如果內容片段不存在給定的變體，則主變體將作為（回退）預設值返回。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL變數 {#graphql-variables}

GraphQL允許將變數放在查詢中。 有關詳細資訊，請參閱 [變數的GraphQL文檔](https://graphql.org/learn/queries/#variables)。

例如，要獲取類型的所有內容片段 `Article` 具有特定變數的變數，可以 `variation` 在GraphiQL中。

![GraphQL變數](assets/cfm-graphqlapi-03.png "GraphQL變數")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## GraphQL指令 {#graphql-directives}

在GraphQL中，有可能基於變數更改查詢，稱為GraphQL指令。

例如，您可以在 `adventurePrice` 查詢中的 `AdventureModels`，基於變數 `includePrice`。

![GraphQL指令](assets/cfm-graphqlapi-04.png "GraphQL指令")

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

您還可以在GraphQL查詢中使用篩選來返回特定資料。

篩選使用基於邏輯運算子和表達式的語法。

例如，以下（基本）查詢將篩選名稱為 `Jobs` 或 `Smith`:

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

有關更多示例，請參見：

* 詳細資訊 [GraphQL擴展AEM版](#graphql-extensions)

* [使用此示例內容和結構的示例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 還有 [示例內容和結構](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) 準備用於示例查詢

* [基於WKND項目的示例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL for AEM — 擴展摘要 {#graphql-extensions}

使用GraphQL查詢的基本操作，AEM以符合標準GraphQL規範。 對於具有以下幾AEM個副檔名的GraphQL查詢：

* 如果需要一個結果：
   * 使用模型名稱；eg城

* 如果您希望列出結果：
   * 添加 `List` 模型名稱；比如說，  `cityList`
   * 請參閱 [示例查詢 — 有關所有城市的所有資訊](#sample-all-information-all-cities)

* 如果要使用邏輯OR:
   * use ` _logOp: OR`
   * 請參閱 [示例查詢 — 名稱為「Jobs」或「Smith」的所有人員](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-jobs-smith)

* 邏輯AND也存在，但是（通常）是隱式的

* 可以查詢與內容片段模型中的欄位對應的欄位名稱
   * 請參閱 [示例查詢 — 公司CEO和員工的完整詳細資訊](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-full-details-company-ceos-employees)

* 除了模型中的欄位外，還有一些系統生成的欄位（前面帶下划線）:

   * 對於內容：

      * `_locale` :揭示語言；基於語言管理器
         * 請參閱 [給定區域設定的多個內容片段的示例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` :顯示片段的元資料
         * 請參閱 [元資料查詢示例 — 列出標題為GB的獎項的元資料](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
      * `_model` :允許查詢內容片段模型（路徑和標題）
         * 請參閱 [從模型中查詢內容片段模型的示例](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-content-fragment-model-from-model)
      * `_path` :儲存庫中內容片段的路徑
         * 請參閱 [示例查詢 — 單個特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
      * `_reference` :顯示參考；包括RTF編輯器中的內聯引用
         * 請參閱 [具有預取引用的多個內容片段的示例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` :顯示內容片段中的特定變體

         >[!NOTE]
         >
         >如果內容片段不存在給定的變體，則主變體將作為（回退）預設值返回。

         * 請參閱 [示例查詢 — 具有命名變體的所有城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
   * 及營運：

      * `_operator` :應用特定運算子； `EQUALS`。 `EQUALS_NOT`。 `GREATER_EQUAL`。 `LOWER`。 `CONTAINS`。 `STARTS_WITH`
         * 請參閱 [示例查詢 — 沒有「職務」名稱的所有人員](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-not-jobs)
         * 請參閱 [示例查詢 — 所有冒險，其中 `_path` 以特定前置詞開頭](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` :具體條件；比如說，  `AT_LEAST_ONCE`
         * 請參閱 [示例查詢 — 對包含項的陣列進行篩選，該項必須至少發生一次](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-array-item-occur-at-least-once)
      * `_ignoreCase` :在查詢時忽略案例
         * 請參閱 [示例查詢 — 名稱中包含SAN的所有城市，不考慮大小寫](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-cities-san-ignore-case)









* 支援GraphQL聯合類型：

   * 使用 `... on`
      * 請參閱 [具有內容引用的特定模型的內容片段的示例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-fragment-specific-model-content-reference)

* 查詢嵌套片段時回退：

   * 如果請求的變體在嵌套片段中不存在，則 **母版** 將返回變體。

## 永續查詢（快取） {#persisted-queries-caching}

在準備具有POST請求的查詢後，可以使用可由HTTP快取或CDN快取的GET請求執行該查詢。

這是必需的，因為POST查詢通常不進行快取，並且如果將GET與查詢一起用作參數，則參數對於HTTP服務和中間產品而言變得過大有很大風險。

永續查詢必須始終使用與 [適當的站點配置](#graphql-aem-endpoint);這樣它們就可以使用其中一種或兩種：

* 全局配置和終結點查詢有權訪問所有內容片段模型。
* 特定站點配置和終結點為特定站點配置建立永續查詢需要特定於特定站點配置的相應終結點（以提供對相關內容片段模型的訪問）。
例如，要為WKND站點配置專門建立永續查詢，必須提前建立相應的WKND特定站點配置和WKND特定終結點。

>[!NOTE]
>
>請參閱 [在配置瀏覽器中啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) 的子菜單。
>
>的 **GraphQL持久性查詢** 需要啟用相應的站點配置。

例如，如果有一個特定查詢 `my-query`，它使用模型 `my-model` 從站點配置 `my-conf`:

* 您可以使用 `my-conf` 特定端點，然後查詢將保存如下：
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 可以使用 `global` 終結點，但查詢將保存如下：
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>這是兩個不同的查詢 — 保存在不同的路徑下。
>
>他們只是碰巧使用了同一種模式 — 但是通過不同的端點。


以下是保留給定查詢所需的步驟：

1. 通過將查詢PUTing到新終結點URL來準備查詢 `/graphql/persist.json/<config>/<persisted-label>`。

   例如，建立永續查詢：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. 此時，檢查響應。

   例如，檢查是否成功：

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 然後，可以通過GETing URL重播保留的查詢 `/graphql/execute.json/<shortPath>`。

   例如，使用永續查詢：

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 通過POSTing將永續查詢更新到已存在的查詢路徑。

   例如，使用永續查詢：

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. 建立換行的純查詢。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 使用快取控制項建立包裝的純查詢。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 使用參數建立永續查詢：

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. 使用參數執行查詢。

   例如：

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. 要在發佈時執行查詢，需要複製相關持久樹

   * 使用POST進行複製：

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * 使用包：
      1. 建立新包定義。
      1. 包括配置(例如， `/conf/wknd/settings/graphql/persistentQueries`)。
      1. 生成包。
      1. 複製包。
   * 使用複製/分發工具。
      1. 轉到分發工具。
      1. 為配置選擇樹激活(例如， `/conf/wknd/settings/graphql/persistentQueries`)。
   * 使用工作流（通過工作流啟動程式配置）:
      1. 定義工作流啟動程式規則，用於執行將在不同事件上複製配置的工作流模型（例如，建立、修改等）。



1. 在發佈上查詢配置後，同樣的原則也適用，只使用發佈端點。

   >[!NOTE]
   >
   >對於匿名訪問，系統假定ACL允許「每個人」訪問查詢配置。
   >
   >如果情況不是這樣，它將無法執行。

   >[!NOTE]
   >
   >需要對URL中的任何分號(&quot;;&quot;)進行編碼。
   >
   >例如，與執行永續查詢的請求一樣：
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## 從外部網站查詢GraphQL終結點 {#query-graphql-endpoint-from-external-website}

要從外部網站訪問GraphQL終結點，您需要配置：

* [CORS篩選器](#cors-filter)
* [引用篩選器](#referrer-filter)

### CORS篩選器 {#cors-filter}

>[!NOTE]
>
>有關CORS資源共用策略的詳細概述，請參AEM見 [瞭解跨源資源共用(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors))。

要訪問GraphQL終結點，必須在客戶Git儲存庫中配置CORS策略。 這是通過為所需端點添加適當的OSGi CORS配置檔案來完成的。

此配置必須指定受信任的網站源 `alloworigin` 或 `alloworiginregexp` 必須授予其訪問權限。

例如，授予對GraphQL終結點和永續查詢終結點的訪問權限 `https://my.domain` 您可以使用：

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

如果已為端點配置虛榮路徑，也可以在 `allowedpaths`。

### 引用篩選器 {#referrer-filter}

除了CORS配置外，還必須配置引用過濾器以允許從第三方主機訪問。

通過添加適當的OSGi引用者篩選器配置檔案來完成此操作，該配置檔案：

* 指定受信任的網站主機名；或 `allow.hosts` 或 `allow.hosts.regexp`。
* 授予對此主機名的訪問權限。

例如，向引用者授予對請求的訪問權限 `my.domain` 您可以：

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
>客戶仍有責任：
>
>* 僅授予受信任域的訪問權限
>* 確保沒有洩露任何敏感資訊
>* 不使用通配符 [*] 語法；這既會禁用對GraphQL端點的經過身份驗證的訪問，又會將其向全世界公開。


>[!CAUTION]
>
>所有GraphQL [模式](#schema-generation) (源於已 **已啟用**)可通過GraphQL終結點讀取。
>
>這意味著您需要確保沒有敏感資料可用，因為敏感資料可能會以這種方式洩露；例如，這包括在模型定義中可以作為欄位名稱顯示的資訊。

## 驗證 {#authentication}

請參閱 [內容片段AEM上遠程GraphQL查詢的驗證](/help/assets/content-fragments/graphql-authentication-content-fragments.md)。

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## 常見問題 {#faqs}

出現的問題：

1. **問**:&quot;*GraphQL API與Query Builder APIAEM有何不同？*&quot;

   * **A**:&quot;*GraphQL APIAEM提供對JSON輸出的完全控制，是查詢內容的行業標準。
今後，AEM計畫投資GraphQLAEM API。*&quot;

## 教程 — 無頭和AEMGraphQL入門 {#tutorial}

想要實習教程嗎？ 簽出 [無頭和AEMGraphQL入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) 端到端教程，演示如何使用AEMGraphQL API構建和公開內容，並讓外部應用在無頭CMS方案中使用。
