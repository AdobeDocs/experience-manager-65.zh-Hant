---
title: 如何透過AEM Assets API更新您的內容
description: 在AEM無頭開發人員歷程的這部分，了解如何使用REST API存取及更新內容片段的內容。
source-git-commit: 7f43d9d6b631b26f7b9293aa109498d0c8040436
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 2%

---

# 如何透過AEM Assets API更新您的內容 {#update-your-content}

在 [AEM無頭開發者歷程，](overview.md) 了解如何使用REST API存取及更新內容片段的內容。

## 迄今為止的故事 {#story-so-far}

在AEM無頭歷程的上一份檔案中， [如何透過AEM傳送API存取您的內容](access-your-content.md) 您已了解如何透過AEM GraphQL API存取AEM中的無周邊內容，您現在應：

* 對GraphQL有更深入的了解。
* 了解AEM GraphQL API的運作方式。
* 了解一些實用的範例查詢。

本文以這些基本知識為基礎，讓您了解如何透過REST API更新AEM中現有的無頭內容。

## 目標 {#objective}

* **對象**:進階
* **目標**:了解如何使用REST API存取及更新內容片段的內容：
   * 介紹AEM Assets HTTP API。
   * 介紹並討論API中的內容片段支援。
   * 說明API的詳細資訊。

<!--
  * Look at sample code to see how things work in practice.
-->

## 為什麼您需要資產HTTP API才能處理內容片段 {#why-http-api}

在無周邊歷程的上一階段，您已了解如何使用AEM GraphQL API來使用查詢擷取內容。

那麼，為何還需要其他API呢？

Assets HTTP API不允許您 **閱讀** 您的內容，但也可讓您 **建立**, **更新** 和 **刪除** 內容 — GraphQL API無法執行的動作。

最新Adobe Experience Manager版本的每個現成可用安裝都提供Assets REST API。

## Assets HTTP API {#assets-http-api}

資產HTTP API包含：

* 資產REST API
* 包括支援內容片段

Assets HTTP API目前的實作是以 **REST** 架構樣式，並可讓您透過 **CRUD** 操作（建立、讀取、更新、刪除）。

透過這些操作，API可讓您將Adobe Experience Manager作為無頭CMS（內容管理系統）來運作，方法是向JavaScript前端應用程式提供內容服務。 或可執行HTTP要求和處理JSON回應的任何其他應用程式。 例如，單頁應用程式(SPA)（以架構為基礎或自訂）需要透過API提供的內容，通常為JSON格式。

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter needs to be configured correctly.

>[!NOTE]
>
>For further information see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For further information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (i.e. folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example its name, title, etc. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## 資產HTTP API和內容片段 {#assets-http-api-content-fragments}

內容片段用於無頭傳送，而內容片段是特殊類型的資產。 它們可用來存取結構化資料，例如文字、數字、日期等。

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, i.e. the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, etc. are part of the definition.

To create a new content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## 使用Assets REST API {#using-aem-assets-rest-api}

### 存取 {#access}

資產REST API使用 `/api/assets` 端點，且需要資產的路徑才能存取它(沒有前導 `/content/dam`)。

* 這表示若要存取資產，請執行下列操作：
   * `/content/dam/path/to/asset`
* 您需要請求：
   * `/api/assets/path/to/asset`

例如，若要存取 `/content/dam/wknd/en/adventures/cycling-tuscany`，要求 `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>訪問：
>
>* `/api/assets` **不** 需要使用 `.model` 選取器。
>* `/content/path/to/page` **does** 需要使用 `.model` 選取器。


### 操作 {#operation}

HTTP方法會決定要執行的操作：

* **GET**  — 擷取資產或資料夾的JSON表示法
* **POST**  — 建立新資產或資料夾
* **PUT**  — 更新資產或資料夾的屬性
* **DELETE**  — 刪除資產或資料夾

>[!NOTE]
>
>請求內文和/或URL參數可用來設定其中一些操作；例如，定義資料夾或資產應由 **POST** 請求。

API參考檔案中已定義支援請求的確切格式。

使用方式會因您使用AEM製作環境或發佈環境，以及您的特定使用案例而異。

* 強烈建議建立作業系結至製作例項（目前沒有方法使用此API復寫片段以發佈）。
* 兩者皆可傳送，因為AEM只會以JSON格式提供請求的內容。

   * 從AEM製作例項的儲存和傳送應足以在防火牆後、媒體程式庫應用程式中使用。

   * 若為即時Web傳送，建議使用AEM發佈例項。

>[!CAUTION]
>
>AEM例項上的Dispatcher設定可能會封鎖 `/api`.

>[!NOTE]
>
>如需詳細資訊，請參閱API參考。 特別是， [Adobe Experience Manager Assets API — 內容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html).

### 讀取/傳送 {#read-delivery}

使用方式為：

`GET /{cfParentPath}/{cfName}.json`

例如：

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

回應會序列化JSON，內容會以內容片段中的結構化形式顯示。 參考會以參考URL的形式傳送。

可能有兩種讀取操作：

* 依路徑讀取特定內容片段，這會傳回內容片段的JSON表示法。
* 依路徑讀取內容片段的資料夾：這會傳回資料夾中所有內容片段的JSON表示法。

### 建立 {#create}

使用方式為：

`POST /{cfParentPath}/{cfName}`

內文必須包含要建立之內容片段的JSON表示法，包括應在內容片段元素上設定的任何初始內容。 強制設定 `cq:model` 屬性，且必須指向有效的內容片段模型。 若無法這麼做，將會導致錯誤。 您也必須新增標題 `Content-Type` 設為 `application/json`.

### 更新 {#update}

使用方式為

`PUT /{cfParentPath}/{cfName}`

內文必須包含指定內容片段要更新內容的JSON表示法。

這只能是內容片段的標題或說明、單一元素或所有元素值和/或中繼資料。

### 刪除 {#delete}

使用方式為：

`DELETE /{cfParentPath}/{cfName}`

如需使用AEM Assets REST API的詳細資訊，您可以參考：

* Adobe Experience Manager Assets HTTP API（其他資源）
* AEM Assets HTTP API中的內容片段支援（其他資源）

## 下一步 {#whats-next}

現在您已完成AEM Headless Developer Journey的這一部分，您應：

* 了解AEM Assets HTTP API的基本概念。
* 了解此API如何支援內容片段。

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page isn't going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

您應繼續進行AEM無頭歷程，繼續檢閱此檔案 [如何與無頭應用程式一起運行](go-live.md) 您實際將AEM Headless專案上線的位置！

## 其他資源 {#additional-resources}

* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [內容片段REST API](/help/assets/assets-api-content-fragments.md)
   * [API參考](/help/assets/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager Assets API — 內容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)
* [使用內容片段](/help/assets/content-fragments/content-fragments.md)
* [AEM 核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)
* [CORS/AEM說明](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [影片 — 使用AEM為CORS開發](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
