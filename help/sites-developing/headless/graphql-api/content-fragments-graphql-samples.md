---
title: 瞭解如何搭配AEM使用GraphQL — 範例內容和查詢
description: 瞭解如何搭配AEM使用GraphQL，透過探索範例內容和查詢來無頭提供內容。
feature: Content Fragments,GraphQL API
exl-id: 91c5f61c-9c15-4d72-9b9b-0c23f31e7cdc
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 79%

---

# 了解搭配使用 GraphQL 與 AEM - 範例內容和查詢 {#learn-graphql-with-aem-sample-content-queries}

瞭解如何搭配AEM使用GraphQL，透過探索範例內容和查詢來無頭提供內容。

>[!NOTE]
>
>本頁應與以下主題一起閱讀：
>
>* [內容片段](/help/assets/content-fragments/content-fragments.md)
>* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
>* [與內容片段搭配使用的 AEM GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)

若要開始使用GraphQL查詢以及它們如何與AEM內容片段搭配運作，檢視一些實用的範例會有所幫助。

如需相關幫助，請參閱：

* [範例內容片段結構](#content-fragment-structure-graphql)

* 以及部分 [範例GraphQL查詢](#graphql-sample-queries)，根據範例內容片段結構（內容片段模型及相關內容片段）。


## GraphQL - 使用範例內容片段結構的範例查詢 {#graphql-sample-queries-sample-content-fragment-structure}

請參閱這些範例查詢，以了解如何建立查詢以及範例結果。

>[!NOTE]
>
>視您的執行個體而定，您可以直接存取 [AEM GraphQL API 包含的 GraphiQL 介面](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface)以提交和測試查詢。
>
>例如：`http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>範例查詢是根據[與 GraphQL 搭配使用的範例內容片段結構](#content-fragment-structure-graphql)

### 範例查詢 - 所有可用的綱要和資料類型 {#sample-all-schemes-datatypes}

此範例查詢傳回所有 `types` 用於所有可用的結構描述。

**範例查詢**

```graphql
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### 範例查詢 - 關於所有城市的所有資訊 {#sample-all-information-all-cities}

若要擷取有關所有城市的所有資訊，您可以使用基本查詢：
**範例查詢**

```graphql
{
  cityList {
    items
  }
}
```

執行時，系統會自動擴展查詢以包括所有欄位：

```graphql
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### 範例查詢 - 所有城市的名稱 {#sample-names-all-cities}

此範例查詢是直接查詢，可傳回 `name`中所有專案的 `city`綱要。

**範例查詢**

```xmgraphqll
query {
  cityList {
    items {
      name
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### 範例查詢 - 單一特定城市片段 {#sample-single-specific-city-fragment}

此範例查詢是傳回存放庫中特定位置單一片段專案詳細資料的查詢。

**範例查詢**

```graphql
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### 範例查詢 - 所有具有名稱變化的城市 {#sample-cities-named-variation}

如果您建立名為「柏林中心」的變數(`berlin_centre`)，針對 `city` 柏林，您可以使用查詢傳回變數的詳細資訊。

**範例查詢**

```graphql
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### 範例查詢 — 所有標籤為城市分隔符號的城市名稱 {#sample-names-all-cities-tagged-city-breaks}

如果您：

* 建立各種標記，名稱為 `Tourism`：`Business`、`City Break`、`Holiday`
* 並將這些標籤指派給各種變數的主變數 `City` 執行個體

接著您可以使用查詢傳回在 `city` 綱要中標記為「City Breaks」之所有項目的 `name` 和 `tags` 的詳細資料。

**範例查詢**

```graphql
query {
  cityList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "tourism:city-break", _operator: CONTAINS}]}}
  ){
    items {
      name,
      _tags
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Berlin",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        },
        {
          "name": "Zurich",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        }
      ]
    }
  }
}
```

### 範例查詢 - 公司 CEO 和員工的完整詳細資訊 {#sample-full-details-company-ceos-employees}

使用巢狀片段的結構，此查詢傳回公司 CEO 及其所有員工的完整詳細資訊。

**範例查詢**

```graphql
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### 範例查詢 - 所有名稱為「Jobs」或「Smith」的所有人員 {#sample-all-persons-jobs-smith}

此範例查詢會篩選所有 `persons` ，適用於任何擁有名稱的 `Jobs`或 `Smith`.

**範例查詢**

```graphql
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

**範例結果**

```json
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### 範例查詢 - 所有名稱不為「Jobs」的人員 {#sample-all-persons-not-jobs}

此範例查詢會篩選所有 `persons` ，適用於任何擁有名稱的 `Jobs`或 `Smith`.

**範例查詢**

```graphql
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
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

**範例結果**

```json
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### 範例查詢 - 其 `_path` 以特定前置詞開頭的所有冒險 {#sample-wknd-all-adventures-cycling-path-filter}

其 `_path` 以特定前置詞 (`/content/dam/wknd/en/adventures/cycling`) 開頭的所有 `adventures`。

**範例查詢**

```graphql
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### 範例查詢 — 德國或瑞士人口為400000到999999的所有城市 {#sample-all-cities-d-ch-population}

這裡篩選了欄位組合。`AND` (隱含) 用於選擇 `population` 範圍，而 `OR` (明確) 用於選擇所需城市。

**範例查詢**

```graphql
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### 範例查詢 - 名稱中包含 SAN 的所有城市，不區分大小寫 {#sample-all-cities-san-ignore-case}

此查詢會質詢名稱中包含 `SAN`的所有城市，不區分大小寫。

**範例查詢**

```graphql
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### 範例查詢 - 篩選至少出現一次項目的陣列 {#sample-array-item-occur-at-least-once}

此查詢篩選至少出現一次項目 (`city:na`) 的陣列。

**範例查詢**

```graphql
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### 範例查詢 - 篩選確切的陣列值 {#sample-array-exact-value}

此查詢會篩選確切的陣列值。

**範例查詢**

```graphql
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### 巢狀內容片段的範例查詢 - 至少有一名員工名稱為「Smith」的所有公司 {#sample-companies-employee-smith}

此查詢說明篩選出任何 `name` 為「Smith」的 `person`，從兩個巢狀片段 - `company` 和 `employee` 傳回資訊。

**範例查詢**

```graphql
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### 巢狀內容片段的範例查詢 - 所有員工都獲得「Gamestar」獎項的所有公司 {#sample-all-companies-employee-gamestar-award}

此查詢說明了跨三個巢狀片段 - `company`、`employee` 和 `award` 的篩選作業。

**範例查詢**

```graphql
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
        awards {
          id
          title
        }
      }
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### 中繼資料的範例查詢 - 列出 GB 獎項的中繼資料 {#sample-metadata-awards-gb}

此查詢說明了跨三個巢狀片段 - `company`、`employee` 和 `award` 的篩選作業。

**範例查詢**

```graphql
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**範例結果**

```json
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## 使用 WKND 專案的範例查詢 {#sample-queries-using-wknd-project}

這些是根據 WKND 專案的範例查詢。其具有以下：

* 內容片段模型可在以下位置取用：
  `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 內容片段 (和其他內容) 可在以下位置取用：
  `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>由於結果可能會很龐大，此處不再重現。

### 具有指定的屬性之特定模型的所有內容片段的範例查詢 {#sample-wknd-all-model-properties}

此範例查詢會質詢：

* 類型為 `article` 的所有內容片段
* 使用 `path`和 `author` 屬性。

**範例查詢**

```graphql
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### 中繼資料的範例查詢 {#sample-wknd-metadata}

此查詢會質詢：

* 類型為 `adventure` 的所有內容片段
* 中繼資料

**範例查詢**

```graphql
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### 特定模型之單一內容片段的範例查詢 {#sample-wknd-single-content-fragment-of-given-model}

此範例查詢會質詢：

* 在特定路徑中類型為 `article` 的單一內容片段
   * 在該路徑內，所有格式的內容：
      * HTML
      * Markdown
      * 純文字
      * JSON

**範例查詢**

```graphql
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### 來自模型的內容片段模型的範例查詢 {#sample-wknd-content-fragment-model-from-model}

此範例查詢會質詢：

* 單一內容片段
   * 基礎內容片段模型的詳細資訊

**範例查詢**

```graphql
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### 巢狀內容片段的範例查詢 - 單一模型類型{#sample-wknd-nested-fragment-single-model}

此查詢會質詢：

* 在特定路徑中類型為 `article` 的單一內容片段
   * 在該路徑內，參照（巢狀）片段的路徑和作者

>[!NOTE]
>
>`referencearticle` 欄位的資料類型為 `fragment-reference`。

**範例查詢**

```graphql
{
  adventureByPath(_path: "/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van") {
    item {
      _path
      title
      _model {
        _path
        title
      }
    }
  }
}
```

### 巢狀內容片段的範例查詢 - 多個模型類型{#sample-wknd-nested-fragment-multiple-model}

#### 單一參考的模型類型

此查詢會質詢：

* 多個類型為 `bookmark` 的內容片段
   * 具有片段參考，其會參考特定模型類型 `Article` 的其他片段。

>[!NOTE]
>
>`fragments` 欄位的資料類型為 `fragment-reference`，且已選取 `Article` 模型。查詢傳遞次數 `fragments` 作為陣列 `[Article]`.

```graphql
{
  bookmarkList {
    items {
        fragments {
          _path
          author
        }
     }
  }
}
```

#### 多個參考的模型類型

此查詢會質詢：

* 多個類型為 `bookmark` 的內容片段
   * 具有片段參考，其會參考特定模型類型 `Article` 和 `Adventure` 的其他片段。

>[!NOTE]
>
>`fragments` 欄位的資料類型為 `fragment-reference`，且已選取 `Article`、`Adventure` 模型。查詢將 `fragments` 以 `[AllFragmentModels]` 陣列形式傳遞，其使用聯合類型取消參考。

```graphql
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### 具有內容參考之特定模型的內容片段的範例查詢{#sample-wknd-fragment-specific-model-content-reference}

此查詢有兩種形式：

1. 傳回所有內容參考。
1. 傳回類型為 `attachments` 的特定內容參考。

此查詢會質詢：

* 多個類型為 `bookmark` 的內容片段
   * 具有對其他片段的內容參考

#### 具有預先擷取之參考的多個內容片段的範例查詢 {#sample-wknd-multiple-fragments-prefetched-references}

以下查詢使用 `_references` 傳回所有內容參考：

```graphql
{
  bookmarkList {
     _references {
         ... on ImageRef {
          _path
          type
          height
        }
        ... on MultimediaRef {
          _path
          type
          size
        }
        ... on DocumentRef {
          _path
          type
          author
        }
        ... on ArchiveRef {
          _path
          type
          format
        }
    }
    items {
        _path
    }
  }
}
```

#### 具有附件之多個內容片段的範例查詢 {#sample-wknd-multiple-fragments-attachments}

以下查詢傳回所有 `attachments` - 類型為 `content-reference` 的特定欄位 (子群組)：

>[!NOTE]
>
>`attachments` 欄位的資料類型為 `content-reference`，並選擇了各種表單。

```graphql
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### 具有 RTE 內聯參考的單一內容片段的範例查詢 {#sample-wknd-single-fragment-rte-inline-reference}

此查詢會質詢：

* 在特定路徑中類型為 `bookmark` 的單一內容片段
   * 其中有 RTE 內聯參考

>[!NOTE]
>
>RTE 內聯參考在 `_references` 中被序列化。

**範例查詢**

```graphql
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### 特定模型的單一內容片段變化的範例查詢 {#sample-wknd-single-fragment-given-model}

此查詢會質詢：

* 在特定路徑中類型為 `article` 的單一內容片段
   * 在該路徑中，與變數相關的資料： `variation1`

**範例查詢**

```graphql
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### 特定模型之多個內容片段的名稱變化的範例查詢 {#sample-wknd-variation-multiple-fragment-given-model}

此查詢會質詢：

* 類型為 `article` 的內容片段，具有特定變化：`variation1`

**範例查詢**

```graphql
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### 對指定模式的多個內容片段及其變化的範例查詢 {#sample-wknd-multiple-fragment-variations-given-model}

此查詢會質詢：

* 類型為 `article` 的內容片段和所有變化

**範例查詢**

```graphql
query {
  articleList(
    includeVariations: true  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### 對附加了特定標記的指定模式的內容片段變化的範例查詢{#sample-wknd-fragment-variations-given-model-specific-tag}

此查詢會質詢：

* 類型為 `article` 的內容片段以及具有 `WKND : Activity / Hiking` 標記的一或多種變化

**範例查詢**

```graphql
{
  articleList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "wknd:activity/hiking", _operator: CONTAINS}]}}
  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### 特定地區設定的多個內容片段的範例查詢 {#sample-wknd-multiple-fragments-given-locale}

此查詢會質詢：

* 在 `fr` 地區設定中類型為 `article` 的內容片段

**範例查詢**

```graphql
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

## 範例內容片段結構 (與 GraphQL 搭配使用) {#content-fragment-structure-graphql}

這些範例查詢是根據以下結構，該結構使用：

* 一個或多個[範例內容片段模型](#sample-content-fragment-models-schemas) - 構成 GraphQL 綱要的基礎

* 根據上述模型的[範例內容片段](#sample-content-fragments)

### 範例內容片段結構 (綱要) {#sample-content-fragment-models-schemas}

對於範例查詢，請使用以下內容模型及其相互關係（參照 — >）：

* [公司](#model-company)
-> [人員](#model-person)
 -> [獎項](#model-award)

* [城市](#model-city)

#### 公司 {#model-company}

定義公司的基本欄位是：

| 欄位名稱 | 資料類型 | 參考 |
|--- |--- |--- |
| 公司名稱 | 單行文字 | |
| CEO | 片段參考 (單一) | [人員](#model-person) |
| 員工 | 片段參考 (多個欄位) | [人員](#model-person) |

#### 人員 {#model-person}

定義人員的欄位，人員也可以是員工：

| 欄位名稱 | 資料類型 | 參考 |
|--- |--- |--- |
| 名稱 | 單行文字 | |
| 名字 | 單行文字 | |
| 獎項 | 片段參考 (多個欄位) | [獎項](#model-award) |

#### 獎項 {#model-award}

定義獎項的欄位是：

| 欄位名稱 | 資料類型 | 參考 |
|--- |--- |--- |
| 快速鍵/ID | 單行文字 | |
| 標題 | 單行文字 | |

#### 城市 {#model-city}

定義城市的名稱是：

| 欄位名稱 | 資料類型 | 參考 |
|--- |--- |--- |
| 名稱 | 單行文字 | |
| 國家/地區 | 單行文字 | |
| 人口 | 數字 | |
| 類別 | 標記 | |

### 範例內容片段 {#sample-content-fragments}

以下片段用於適當的模型。

#### 公司 {#fragment-company}

| 公司名稱 | CEO | 員工 |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max Caulfield |
|  小馬公司 | Adam Smith | Lara Croft<br>Cutter Slade |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### 人員 {#fragment-person}

| 名稱 | 名字 | 獎項 |
|--- |--- |--- |
| Lincoln |  Abe | |
| Smith | Adam |   |
| Slade |  刀具 |  Gameblitz<br>Gamestar |
| Marsh |  Duke |   |   |
|  Smith |  Joe |   |
| Croft |  Lara | Gamestar |
| Caulfield |  最大 |  Gameblitz |
|  工作 |  Steve |   |

#### 獎項 {#fragment-award}

| 快速鍵/ID | 標題 |
|--- |--- |
| GB | Gameblitz |
|  GS | Gamestar |
|  OSC | Oscar |

#### 城市 {#fragment-city}

| 名稱 | 國家/地區 | 人口 | 類別 |
|--- |--- |--- |--- |
| 巴塞爾 | 瑞士 | 172258 | city:emea |
| 柏林 | 德國 | 3669491 | city:capital<br>city:emea |
| 布加勒斯特 | 羅馬尼亞 | 1821000 |  city：capital<br>city：emea |
| 舊金山 |  美國 |  883306 |  city：beach<br>city：na |
| 聖荷西 |  美國 |  102635 |  city：na |
| 斯圖加特 |  德國 |  634830 |  city：emea |
|  蘇黎世 |  瑞士 |  415367 |  city：capital<br>city：emea |
