---
title: 學習如何搭配AEM使用GraphQL — 範例內容與查詢
description: 了解如何透過探索範例內容和查詢，將GraphQL與AEM搭配使用，以無故提供內容。
feature: Content Fragments,GraphQL API
source-git-commit: 94145c6428f61e31f6784a3d6ea67aa8d81cedd6
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 6%

---

# 學習如何搭配AEM使用GraphQL — 範例內容與查詢 {#learn-graphql-with-aem-sample-content-queries}

了解如何透過探索範例內容和查詢，將GraphQL與AEM搭配使用，以無故提供內容。

>[!NOTE]
>
>本頁面應與：
>
>* [內容片段](/help/assets/content-fragments/content-fragments.md)
>* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
>* [AEM GraphQL API以搭配內容片段使用](/help/assets/content-fragments/graphql-api-content-fragments.md)


若要開始使用GraphQL查詢，以及這些查詢如何搭配AEM內容片段使用，請參閱一些實用範例。

如需此項目的協助，請參閱：

* A [範例內容片段結構](#content-fragment-structure-graphql)

* 以及根據範例內容片段結構（內容片段模型與相關內容片段）的某些[範例GraphQL查詢](#graphql-sample-queries)。


## GraphQL — 使用範例內容片段結構的範例查詢 {#graphql-sample-queries-sample-content-fragment-structure}

請參閱這些範例查詢以取得建立查詢的圖解以及範例結果。

>[!NOTE]
>
>根據您的實例，您可以直接訪問AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)中包含的[Graph *i* QL介面，以提交和測試查詢。
>
>例如：`http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>範例查詢以[要與GraphQL](#content-fragment-structure-graphql)搭配使用的範例內容片段結構為基礎

### 範例查詢 — 所有可用的結構和資料類型 {#sample-all-schemes-datatypes}

這會傳回所有可用結構的所有`types`。

**範例查詢**

```xml
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

```xml
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

### 範例查詢 — 所有城市的所有資訊 {#sample-all-information-all-cities}

若要擷取關於所有城市的所有資訊，您可以使用非常基本的查詢：
**範例查詢**

```xml
{
  cityList {
    items
  }
}
```

執行時，系統會自動展開查詢以包含所有欄位：

```xml
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

```xml
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

### 範例查詢 — 所有城市的名稱 {#sample-names-all-cities}

這是直接查詢，可傳回`city`架構中所有項目的`name`。

**範例查詢**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**範例結果**

```xml
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

### 範例查詢 — 單一特定城市片段 {#sample-single-specific-city-fragment}

這是一個查詢，用於返回儲存庫中特定位置的單個片段條目的詳細資訊。

**範例查詢**

```xml
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

```xml
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

### 範例查詢 — 具有已命名變數的所有城市 {#sample-cities-named-variation}

如果您為`city`柏林建立名為&quot;Berlin Center&quot;(`berlin_centre`)的新變數，則可使用查詢傳回變數的詳細資料。

**範例查詢**

```xml
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

```xml
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

### 示例查詢 — 公司CEO和員工的完整詳細資訊 {#sample-full-details-company-ceos-employees}

使用巢狀片段的結構，此查詢會傳回公司CEO及其所有員工的完整詳細資訊。

**範例查詢**

```xml
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

```xml
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

### Sample Query — 名為「Jobs」或「Smith」的所有人員 {#sample-all-persons-jobs-smith}

這將篩選所有名稱為`Jobs`或`Smith`的`persons`。

**範例查詢**

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

**範例結果**

```xml
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

### 示例查詢 — 沒有「Jobs」名稱的所有人員 {#sample-all-persons-not-jobs}

這將篩選所有名稱為`Jobs`或`Smith`的`persons`。

**範例查詢**

```xml
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

```xml
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

### 範例查詢 — 其`_path`開頭為特定首碼的所有歷險 {#sample-wknd-all-adventures-cycling-path-filter}

`_path`中的`adventures`以特定前置詞(`/content/dam/wknd/en/adventures/cycling`)開頭。

**範例查詢**

```xml
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

```xml
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

### 範例查詢 — 位於德國或瑞士，人口介於400000和999999之間的所有城市 {#sample-all-cities-d-ch-population}

此處會篩選欄位組合。 `AND`（隱式）用於選擇`population`範圍，而`OR`（顯式）用於選擇所需城市。

**範例查詢**

```xml
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

```xml
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

### 示例查詢 — 名稱中包含SAN的所有城市（不考慮大小寫） {#sample-all-cities-san-ignore-case}

此查詢會詢問名稱中包含`SAN`的所有城市，而不考慮大小寫。

**範例查詢**

```xml
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

```xml
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

### 範例查詢 — 對項目必須至少發生一次的陣列進行篩選 {#sample-array-item-occur-at-least-once}

此查詢會篩選陣列上必須至少發生一次的項目(`city:na`)。

**範例查詢**

```xml
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

```xml
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

### 範例查詢 — 篩選精確的陣列值 {#sample-array-exact-value}

此查詢會篩選確切的陣列值。

**範例查詢**

```xml
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

```xml
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

### 巢狀內容片段的查詢範例 — 所有至少有一名員工且名稱為「Smith」的公司 {#sample-companies-employee-smith}

此查詢說明了對`name` &quot;Smith&quot;的任何`person`進行篩選，從兩個巢狀片段 — `company`和`employee`返回資訊。

**範例查詢**

```xml
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

```xml
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

### 巢狀內容片段的範例查詢 — 所有員工皆獲得「遊戲之星」獎的公司 {#sample-all-companies-employee-gamestar-award}

此查詢說明如何跨三個巢狀片段（`company`、`employee`和`award`）進行篩選。

**範例查詢**

```xml
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

```xml
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

### 中繼資料的範例查詢 — 列出題為GB的獎項中繼資料 {#sample-metadata-awards-gb}

此查詢說明如何跨三個巢狀片段（`company`、`employee`和`award`）進行篩選。

**範例查詢**

```xml
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

```xml
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

## 使用WKND專案的查詢範例 {#sample-queries-using-wknd-project}

這些範例查詢是以WKND專案為基礎。 這包括：

* 內容片段模型可用於：
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 下列位置提供內容片段（和其他內容）:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>由於結果可能很廣泛，因此這些結果不會在此處重現。

### 具有指定屬性之特定模型的所有內容片段的範例查詢 {#sample-wknd-all-model-properties}

此示例查詢將詢問：

* `article`類型的所有內容片段
* 和`author`屬性。`path`

**範例查詢**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### 中繼資料的查詢範例 {#sample-wknd-metadata}

此查詢將詢問：

* `adventure`類型的所有內容片段
* 中繼資料

**範例查詢**

```xml
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

### 指定模型的單一內容片段的查詢範例 {#sample-wknd-single-content-fragment-of-given-model}

此示例查詢將詢問：

* 針對特定路徑上`article`類型的單一內容片段
   * 其中，所有格式的內容：
      * HTML
      * Markdown
      * 純文字
      * JSON

**範例查詢**

```xml
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

### 從模型中查詢內容片段模型的範例 {#sample-wknd-content-fragment-model-from-model}

此示例查詢將詢問：

* （適用於單一內容片段）
   * 基礎內容片段模型的詳細資訊

**範例查詢**

```xml
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

### 巢狀內容片段的查詢範例 — 單一模型類型{#sample-wknd-nested-fragment-single-model}

此查詢將詢問：

* 針對特定路徑上`article`類型的單一內容片段
   * 其中，參照（巢狀）片段的路徑和作者

>[!NOTE]
>
>欄位`referencearticle`具有資料類型`fragment-reference`。

**範例查詢**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### 巢狀內容片段的範例查詢 — 多模型類型{#sample-wknd-nested-fragment-multiple-model}

此查詢將詢問：

* 適用於`bookmark`類型的多個內容片段
   * 具有特定模型類型`article`和`adventure`的其他片段參考

>[!NOTE]
>
>欄位`fragments`具有資料類型`fragment-reference`，且已選取模型`Article`、`Adventure`。

```xml
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

### 具有內容參考之特定模型的內容片段查詢範例{#sample-wknd-fragment-specific-model-content-reference}

此查詢有兩種類型：

1. 傳回所有內容參考。
1. 返回類型`attachments`的特定內容引用。

這些查詢會詢問：

* 適用於`bookmark`類型的多個內容片段
   * 搭配其他片段的內容參考

#### 具有預先擷取的參考之多個內容片段的查詢範例 {#sample-wknd-multiple-fragments-prefetched-references}

下列查詢會使用`_references`傳回所有內容參考：

```xml
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

#### 含附件的多個內容片段的查詢範例 {#sample-wknd-multiple-fragments-attachments}

以下查詢返回所有`attachments` — 類型`content-reference`的特定欄位（子組）:

>[!NOTE]
>
>欄位`attachments`具有資料類型`content-reference`，且已選取各種表單。

```xml
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

### 具有RTE內嵌參考的單一內容片段的查詢範例 {#sample-wknd-single-fragment-rte-inline-reference}

此查詢將詢問：

* 針對特定路徑上`bookmark`類型的單一內容片段
   * 其中，RTE內嵌參照

>[!NOTE]
>
>在`_references`中對RTE內嵌引用進行水合。

**範例查詢**

```xml
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

### 指定模型的單一內容片段變異的範例查詢 {#sample-wknd-single-fragment-given-model}

此查詢將詢問：

* 針對特定路徑上`article`類型的單一內容片段
   * 其中，與變異相關的資料：`variation1`

**範例查詢**

```xml
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

### 指定模型的多個內容片段之命名變異的查詢範例 {#sample-wknd-variation-multiple-fragment-given-model}

此查詢將詢問：

* 針對具有特定變異之`article`類型的內容片段：`variation1`

**範例查詢**

```xml
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

### 指定地區的多個內容片段的查詢範例 {#sample-wknd-multiple-fragments-given-locale}

此查詢將詢問：

* `fr`地區設定內`article`類型的內容片段

**範例查詢**

```xml
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

## 範例內容片段結構（與GraphQL搭配使用） {#content-fragment-structure-graphql}

範例查詢以下列結構為基礎，其使用：

* 一個或多個[示例內容片段模型](#sample-content-fragment-models-schemas) — 構成GraphQL架構的基礎

* [根據上](#sample-content-fragments) 述模型的內容片段範例

### 內容片段模型範例（結構） {#sample-content-fragment-models-schemas}

對於範例查詢，我們將使用下列內容模型及其相互關係（參考 — >）:

* [公司](#model-company)
->人 [員](#model-person)
    ->獎 [項](#model-award)

* [城市](#model-city)

#### 公司 {#model-company}

定義公司的基本欄位包括：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 公司名稱 | 單行文字 |  |
| 首席執行官 | 片段參考（單一） | [人員](#model-person) |
| 員工 | 片段參考（多欄位） | [人員](#model-person) |

#### 人員 {#model-person}

定義人員的欄位，也可以是員工：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 名稱 | 單行文字 |  |
| 名字 | 單行文字 |  |
| 獎勵 | 片段參考（多欄位） | [獎勵](#model-award) |

#### 獎勵 {#model-award}

定義獎勵的欄位包括：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 快捷方式/ID | 單行文字 |  |
| 標題 | 單行文字 |  |

#### 城市 {#model-city}

定義城市的欄位有：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 名稱 | 單行文字 |  |
| 國家/地區 | 單行文字 |  |
| 人口 | 數量 |  |
| 類別 | 標記 |  |

### 範例內容片段 {#sample-content-fragments}

下列片段用於適當的模型。

#### 公司 {#fragment-company}

| 公司名稱 | 首席執行官 | 員工 |
|--- |--- |--- |
| Apple | 史蒂夫·喬布斯 | 杜克·馬什<br>馬克斯·考爾菲爾德 |
|  小馬公司 | 亞當·斯密 | 拉拉·克羅夫特<br>刀刀刀刀 |
| NextStep Inc. | 史蒂夫·喬布斯 | 喬·史密斯<br>阿部·林肯 |

#### 人員 {#fragment-person}

| 名稱 | 名字 | 獎勵 |
|--- |--- |--- |
| 林肯 |  阿部 |  |
| 史密斯 | Adam |   |
| 斯萊德 |  刀具 |  Gameblitz<br>Gamestar |
| 馬什 |  杜克 |   |   |
|  史密斯 |  喬 |   |
| 克羅夫特 |  拉拉 | 遊戲之星 |
| 考爾菲爾德 |  最大值 |  加梅布利茨 |
|  工作 |  史蒂夫 |   |

#### 獎勵 {#fragment-award}

| 快捷方式/ID | 標題 |
|--- |--- |
| GB | 加梅布利茨 |
|  GS | 遊戲之星 |
|  OSC | 奧斯卡 |

#### 城市 {#fragment-city}

| 名稱 | 國家/地區 | 人口 | 類別 |
|--- |--- |--- |--- |
| 巴塞爾 | 瑞士 | 172258 | 城市：emea |
| 柏林 | 德國 | 3669491 | city:capital<br>city:emea |
| 布加勒斯特 | 羅馬尼亞 | 1821000 |  city:capital<br>city:emea |
| 舊金山 |  美國 |  883306 |  city:beach<br>city:na |
| 聖荷西 |  美國 |  102635 |  城市：納 |
| 斯圖加特 |  德國 |  634830 |  城市：emea |
|  蘇黎世 |  瑞士 |  415367 |  city:capital<br>city:emea |
