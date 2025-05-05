---
title: 如何透過 AEM Delivery API 存取您的內容
description: 在 AEM Headless 開發人員歷程的這一部分中，了解如何使用 GraphQL 查詢來存取您的內容片段內容。
exl-id: 44f85d00-a958-470a-8a6e-e2ae1580525a
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 93%

---

# 如何透過 AEM Delivery API 存取您的內容 {#access-your-content}

在 [AEM Headless 開發人員歷程](overview.md)的這一部分中，您可以了解如何使用 GraphQL 查詢來存取您的內容片段內容並提供給您的應用程式 ( Headless 傳遞)。

## 目前進度 {#story-so-far}

在 AEM Headless 歷程的上一個文件「[如何建立內容模型](model-your-content.md)」中，您已了解在 AEM 中建立內容模型的基本知識，所以現在您應該了解如何建立內容結構模型，然後使用 AEM 內容片段模型和內容片段實現該結構。

* 認識內容模型相關的概念和術語。
* 了解為什麼 Headless 內容傳遞需要內容模型。
* 了解如何使用 AEM 內容片段模型實現此結構 (和使用內容片段製作內容)。
* 了解如何建立內容模型；基本範例的原則。

本文章以這些基本知識為基礎，以便您了解如何使用 AEM GraphQL API 在 AEM 存取您現有的 Headless 內容。

* **對象**：初學者
* **目標**：了解如何使用 GraphQL 查詢來存取內容片段的內容。
   * 介紹 GraphQL 和 AEM GraphQL API。
   * 深入了解 AEM GraphQL API 的詳細資訊。
   * 查看一些範例查詢以了解實務運作。

## 所以您想存取您的內容嗎？ {#so-youd-like-to-access-your-content}

所以...您已經取得所有這些內容，結構整齊 (在內容片段中)，正等待提供給您的新應用程式。問題是 - 如何到達那裡？

您需要的是可以找出特定內容為目標的方法，選擇您需要的內容並將其傳回到您的應用程式以進一步處理。

透過Adobe Experience Manager (AEM)，您可以使用AEM GraphQL API選擇性地存取您的內容片段，以僅傳回您需要的內容。 這表示您可以實現 Headless 傳遞結構化的內容，以便在您的應用程式中使用。

>[!NOTE]
>
>AEM GraphQL API 是根據標準 GraphQL API 規格的自訂實作。

## GraphQL - 簡介 {#graphql-introduction}

GraphQL 是一種開放原始碼的規格，它提供：

* 查詢語言，使您能夠從結構化物件中選擇特定內容。
* 執行階段，使用您的結構化內容來完成這些查詢。

GraphQL 是&#x200B;*強*&#x200B;類型 API。這表示&#x200B;*所有*&#x200B;內容必須按類型清楚結構和組織，以便 GraphQL *了解*&#x200B;要存取什麼以及如何存取。資料欄位在 GraphQL 結構描述中定義，其定義內容物件的結構。

然後，GraphQL 端點提供回應 GraphQL 查詢的路徑。

這一切表示您的應用程式可以準確、可靠和有效率地選擇它需要的內容，正是您搭配 AEM 使用時所需要的。

>[!NOTE]
>
>請參閱 *GraphQL*.org 和 *GraphQL*.com。

<!--
## AEM and GraphQL {#aem-graphql}

GraphQL is used in various locations in AEM; for example:

* Content Fragments
  * A customized API has been developed for this use-case (Headless Delivery to your app).
    * This is the AEM GraphQL API.
* Commerce
  * AEM Commerce consumes data from a Commerce platform via GraphQL.
  * There are GraphQL integrations between AEM and various third-party commerce solutions, used with the extension hooks provided by the CIF Core Components.
    * This does not use the AEM GraphQL API.

>[!NOTE]
>
>This step of the Headless Journey is only concerned with the AEM GraphQL API and Content Fragments.
-->

## AEM GraphQL API {#aem-graphql-api}

AEM GraphQL API是根據標準GraphQL API規格的自訂版本，特別設定為可讓您對內容片段執行（複雜）查詢。

使用內容片段，因為內容的結構是根據內容片段模型建立的。這滿足了 GraphQL 的基本要求。

* 內容片段模型由一個或多個欄位組成。
   * 每個欄位都是根據資料類型定義的。
* 內容片段模型用於產生對應的 AEM GraphQL 結構描述。

為了實際存取 GraphQL 以用於 AEM (和內容)，端點用於提供存取路徑。

然後，透過 AEM GraphQL API 傳回的內容可以供您的應用程式使用。

為了協助您直接輸入和測試查詢，標準 GraphiQL 介面的實作也可與 AEM GraphQL (這可與 AEM 一起安裝) 搭配使用。它提供語法醒目顯示、自動完成、自動建議等功能，以及歷史記錄和線上文件。

>[!NOTE]
>
>AEM GraphQL API 實作是以 GraphQL Java 程式庫為基礎。

<!--
### Use Cases for Author and Publish Environments {#use-cases-author-publish-environments}

The use cases for the AEM GraphQL API can depend on the type of AEMenvironment:

* Publish environment; used to: 
  * Query content for JS application (standard use-case)

* Author environment; used to: 
  * Query content for "content management purposes":
    * GraphQL in AEM is currently a read-only API.
    * The REST API can be used for CR(u)D operations.
-->

## 與 AEM GraphQL API 搭配使用的內容片段 {#content-fragments-use-with-aem-graphql-api}

內容片段可作為 AEM 結構描述和查詢之 GraphQL 的基礎，如下所示：

* 它們使您能夠設計、建立、策劃和發佈可以 Headless 方式傳遞之獨立於頁面的內容。
* 它們根據內容片段模型，該模型使用選擇的資料類型為產生的片段預先定義結構。
* 可以使用片段參考資料類型完成額外的結構層，在定義模型時可用。

### 內容片段模型 {#content-fragments-models}

這些內容片段模型：

* **啟用**&#x200B;後，用於產生結構描述。
* 提供 GraphQL 所需的資料類型和欄位。它們確保您的應用程式只要求可能的內容並接收預期的內容。
* **片段參考**&#x200B;資料類型可在您的模型中用來參考另一個內容片段，從而引入額外的結構層。

### 片段參考 {#fragment-references}

**片段參考**：

* 是在定義內容片段模型時可用的特定資料類型。
* 可參考另一個片段，取決於特定的內容片段模型。
* 可讓您建立並接著擷取結構化資料。

   * 當定義為 **multifeed** 時，主片段可以參考 (擷取) 多個子片段。

### JSON 預覽 {#json-preview}

為了協助設計和開發內容片段模型，您可以在內容片段編輯器中預覽 JSON 輸出。

![JSON 預覽](assets/cfm-model-json-preview.png "JSON 預覽")

<!--
## GraphQL Schema Generation from Content Fragments {#graphql-schema-generation-content-fragments}

GraphQL is a strongly typed API, which means that content must be clearly structured and organized by type. The GraphQL specification provides a series of guidelines on how to create a robust API for interrogating content on a certain instance. To do this, a client needs to fetch the Schema, which contains all the types necessary for a query. 

For Content Fragments, the GraphQL schemas (structure and types) are based on **Enabled** Content Fragment Models and their data types.

>[!CAUTION]
>
>All the GraphQL schemas (derived from Content Fragment Models that have been **Enabled**) are readable through the GraphQL endpoint.
>
>This means that you need to ensure that no sensitive content is available, to ensure that no sensitive data is exposed via GraphQL endpoints; for example, this includes information that could be present as field names in the model definition.

For example, if a user created a Content Fragment Model called `Article`, then AEM generates the object `article` that is of a type `ArticleModel`. The fields within this type correspond to the fields and data types defined in the model.

1. A Content Fragment Model:

   ![Content Fragment Model for use with GraphQL](assets/graphqlapi-cfmodel.png "Content Fragment Model for use with GraphQL")

1. The corresponding GraphQL schema (output from GraphiQL automatic documentation):
   ![GraphQL Schema based on Content Fragment Model](assets/graphqlapi-cfm-schema.png "GraphQL Schema based on Content Fragment Model")

   This shows that the generated type `ArticleModel` contains several [fields](#fields). 
   
   * Three of them have been controlled by the user: `author`, `main` and `referencearticle`.

   * The other fields were added automatically by AEM, and represent helpful methods to provide information about a certain Content Fragment; in this example, `_path`, `_metadata`, `_variations`. These [helper fields](#helper-fields) are marked with a preceding `_` to distinguish between what has been defined by the user and what has been auto-generated.

1. After a user creates a Content Fragment based on the Article model, it can then be interrogated through GraphQL. For examples, see the Sample Queries.md#graphql-sample-queries) (based on a sample Content Fragment structure for use with GraphQL.

In GraphQL for AEM, the schema is flexible. This means that it is auto-generated each and every time a Content Fragment Model is created, updated or deleted. The data schema caches are also refreshed when you update a Content Fragment Model.

The Sites GraphQL service listens (in the background) for any modifications made to a Content Fragment Model. When updates are detected, only that part of the schema is regenerated. This optimization saves time and provides stability.

So for example, if you:

1. Install a package containing `Content-Fragment-Model-1` and `Content-Fragment-Model-2`:
 
   1. GraphQL types for `Model-1` and `Model-2` will be generated.

1. Then modify `Content-Fragment-Model-2`:

   1. Only the `Model-2` GraphQL type will get updated.

   1. Whereas `Model-1` will remain the same. 

>[!NOTE]
>
>This is important to note in case you want to do bulk updates on Content Fragment Models through the REST api, or otherwise.

The schema is served through the same endpoint as the GraphQL queries, with the client handling the fact that the schema is called with the extension `GQLschema`. For example, performing a simple `GET` request on `/content/cq:graphql/global/endpoint.GQLschema` will result in the output of the schema with the Content-type: `text/x-graphql-schema;charset=iso-8859-1`.

### Schema Generation - Unpublished Models {#schema-generation-unpublished-models}

When Content Fragments are nested it can happen that a parent Content Fragment Model is published, but a referenced model is not.

>[!NOTE]
>
>The AEM UI prevents this happening, but if publishing is made programmatically, or with content packages, it can occur.

When this happens, AEM generates an *incomplete* Schema for the parent Content Fragment Model. This means that the Fragment Reference, which is dependent on the unpublished model, is removed from the schema.

## AEM GraphQL Endpoints {#aem-graphql-endpoints}

An endpoint is the path used to access GraphQL for AEM. Using this path you (or your app) can:

* access the GraphQL schemas,
* send your GraphQL queries,
* receive the responses (to your GraphQL queries).

AEM allows for:

* A global endpoint - available for use by all sites.
* Endpoints for specific Sites configurations - that you can configure (in the Configuration Browser), specific to a specified site/project.

## Permissions {#permissions}

The permissions are those required for accessing Assets.

## The AEM GraphiQL Interface {#aem-graphiql-interface}

To help you directly input, and test queries, an implementation of the standard GraphiQL interface is available for use with AEM GraphQL. This can be installed with AEM.

>[!NOTE]
>
>GraphiQL is bound the global endpoint (and does not work with other endpoints for specific Sites configurations).

It provides features such as syntax-highlighting, auto-complete, auto-suggest, together with a history and online documentation.

![GraphiQL Interface](assets/graphiql-interface.png "GraphiQL Interface")
-->

## 實際使用 AEM GraphQL API {#actually-using-aem-graphiql}

### 初始設定 {#initial-setup}

在開始對您的內容進行查詢之前，您需要：

* 啟用您的端點
   * 使用「工具> Assets > GraphQL」
   * [啟用 GraphQL 端點](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)

* 存取GraphiQL （如有必要）
   * [AEM GraphiQL介面](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface)

### 範例結構 {#sample-structure}

若要實際在查詢中使用 AEM GraphQL API，我們可以使用兩個非常基本的內容片段模型結構：

* 公司
   * 名稱 - 文字
   * CEO (人員) - 片段參考
   * 員工 (人員) - 片段參考
* 人員
   * 名稱 - 文字
   * 名字 - 文字

如您所見，CEO 和員工欄位參考了人員片段。

使用的片段模型：

* 在內容片段編輯器建立內容時
* 產生您將查詢的 GraphQL 結構描述

### 在哪裡測試您的查詢 {#where-to-test-your-queries}

可在[GraphiQL介面](/help/sites-developing/headless/graphql-api/graphiql-ide.md)中輸入查詢，例如：

* `http://localhost:4502/aem/graphiql.html`

![GraphiQL 介面](assets/graphiql-interface.png "GraphiQL 介面")

### 查詢快速入門 {#getting-Started-with-queries}

一個簡單的查詢是傳回「公司」結構描述中所有項目的名稱。您在這裡要求所有公司名稱的清單：

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

一個稍微複雜的查詢是選擇所有名稱不是「Jobs」的人員。這將篩選出所有名稱沒有 Jobs 的人員。這是使用 EQUALS_NOT 運算子完成 (還有更多)：

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

您還可以建構更複雜的查詢。例如，查詢至少有一名員工名稱為「Smith」的所有公司。此查詢說明了對任何名稱為「Smith」的人員的篩選，從跨巢狀片段傳回資訊：

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

<!-- need code / curl / cli examples-->

如需使用 AEM GraphQL API 的完整詳細資訊，以及設定必要的元素，您可以參考：

* 了解如何將 GraphQL 與 AEM 搭配使用
* 範例內容片段結構
* 了解搭配使用 GraphQL 與 AEM - 範例內容和查詢

## 下一步 {#whats-next}

現在您已經了解如何使用 AEM GraphQL API 存取和查詢 Headless 內容，您現在可以[了解如何使用 REST API 存取和更新內容片段的內容](update-your-content.md)。

## 其他資源 {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [結構描述](https://graphql.org/learn/schema/)
   * [變數](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java 程式庫](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [了解如何將 GraphQL 與 AEM 搭配使用](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)
   * [啟用 GraphQL 端點](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)
   * [安裝 AEM GraphiQL 介面](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface)
* [範例內容片段結構](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [了解搭配使用 GraphQL 與 AEM - 範例內容和查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md)
   * [範例查詢 - 單一特定城市片段](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [中繼資料的範例查詢 - 列出 GB 獎項的中繼資料](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [範例查詢 - 所有具有名稱變化的城市](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [在設定瀏覽器中啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [使用內容片段](/help/assets/content-fragments/content-fragments.md)
   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON 輸出](/help/assets/content-fragments/content-fragments-json-preview.md)
* [了解跨原始資源共用 (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=zh-Hant#understand-cross-origin-resource-sharing-(cors))
* [AEM Headless 快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=zh-Hant) - 此為簡短的教學影片系列，概述如何使用 AEM 的 Headless 功能，包括內容模型和 GraphQL。

<!--
* [Generating Access Tokens for Server Side APIs](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
-->
