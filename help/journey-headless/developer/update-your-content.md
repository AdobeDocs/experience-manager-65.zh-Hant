---
title: 如何透過 AEM Assets API 更新您的內容
description: 在 AEM Headless 開發人員歷程的這一部分中，了解如何使用 REST API 存取和更新內容片段的內容。
exl-id: af29cb77-0210-4fc4-8d86-2a833d19b49f
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 87%

---

# 如何透過 AEM Assets API 更新您的內容 {#update-your-content}

在 [AEM Headless 開發人員歷程](overview.md)的這一部分中，了解如何使用 REST API 存取和更新內容片段的內容。

## 目前進度 {#story-so-far}

在 AEM Headless 歷程的上一個文件「[如何透過 AEM Delivery API 存取您的內容](access-your-content.md)」中，您已了解如何透過 AEM GraphQL API 存取 AEM 中的 Headless 內容，現在您應該：

* 對 GraphQL 有概略的了解。
* 了解 AEM GraphQL API 運作方式。
* 了解一些實際的範例查詢。

本文章以這些基本知識為基礎，以便您了解如何透過 REST API 在 AEM 更新您的現有 Headless 內容。

## 目標 {#objective}

* **對象**：進階
* **目標**：了解如何使用 REST API 存取和更新內容片段的內容：
   * 介紹 AEM Assets HTTP API。
   * 介紹和討論 API 支援內容片段。
   * 說明 API 的詳細資訊。

<!--
  * Look at sample code to see how things work in practice.
-->

## 為什麼您需要 Assets HTTP API 用於內容片段？ {#why-http-api}

在 Headless 歷程的上一個文件中，您已了解如何使用 AEM GraphQL API 透過查詢擷取您的內容。

那麼為什麼需要另一個 API？

Assets HTTP API可讓您&#x200B;**讀取**&#x200B;您的內容，但也可讓您&#x200B;**建立**、**更新**&#x200B;及&#x200B;**刪除**&#x200B;內容 — GraphQL API無法執行的動作。

Assets REST API適用於最新版Adobe Experience Manager的每一次現成安裝。

## Assets HTTP API {#assets-http-api}

Assets HTTP API 包含：

* Assets REST API
* 包含支援內容片段

Assets HTTP API 的目前實作是以 **REST** 架構型式為基礎，可讓您透過 **CRUD** 操作 (建立、讀取、更新、刪除) 存取內容。

透過這些作業，API可讓您藉由向Adobe Experience Manager前端應用程式提供內容服務，將JavaScript當作Headless CMS （內容管理系統）來作業。 或者任何其他可以執行 HTTP 要求並處理 JSON 回應的應用程式。例如，框架型或自訂的單頁應用程式 (SPA) 需要透過 API 提供的內容，通常採 JSON 格式。

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
>Paging is typically applied on container entities (that is, folders or assets with renditions), as it relates to the children of the requested entity.

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

The Assets REST API exposes access to the properties of a folder; for example, its name, title, and so on. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## Assets HTTP API 和內容片段 {#assets-http-api-content-fragments}

內容片段用於 Headless 傳遞，內容片段是一種特殊類型的資產。它們用於存取結構化資料，例如文字、數字、日期等。

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, that is, the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, and so on. are part of the definition.

To create a content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## 使用 Assets REST API {#using-aem-assets-rest-api}

### 存取 {#access}

Assets REST API 使用 `/api/assets` 端點並需要資產的路徑來存取它 (開頭無 `/content/dam`)。

* 這表示要存取以下位置的資產：
   * `/content/dam/path/to/asset`
* 您需要要求：
   * `/api/assets/path/to/asset`

例如，若要存取 `/content/dam/wknd/en/adventures/cycling-tuscany`，要求 `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>存取：
>
>* `/api/assets`**不需要**&#x200B;使用 `.model` 選擇器。
>* `/content/path/to/page` **需要**&#x200B;使用 `.model` 選擇器。

### 操作 {#operation}

HTTP 方法決定要執行的操作：

* **GET** - 檢索資產或資料夾的 JSON 表示
* **POST** - 建立新資產或資料夾
* **PUT** - 更新資產或資料夾的屬性
* **DELETE** - 刪除資產或資料夾

>[!NOTE]
>
>要求內文和/或 URL 參數可用於設定其中一些操作；例如，定義資料夾或資產應由 **POST** 要求建立。

API 參考文件中定義了受支援要求的確切格式。

根據您使用的是 AEM 作者環境還是發佈環境，以及您的特定使用案例，使用情況可能會有所不同。

* 強烈建議建立操作與作者執行個體綁定 (目前沒有辦法複製片段以使用此 API 發佈)。
* 都可以從兩者傳遞，因為 AEM 僅以 JSON 格式提供要求的內容。

   * 來自 AEM 作者執行個體的儲存和傳遞操作應該足以滿足防火牆後的媒體庫應用程式的需求。

   * 如果是即時 Web 傳遞，則建議使用 AEM 發佈執行個體。

>[!CAUTION]
>
>AEM執行個體上的Dispatcher設定可能會封鎖對`/api`的存取權。

>[!NOTE]
>
>如需更多詳細資訊，請參閱 API 參考。特別是 [Adobe Experience Manager Assets API - 內容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)。

### 讀取/傳遞 {#read-delivery}

使用方式：

`GET /{cfParentPath}/{cfName}.json`

例如：

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

回應是序列化的 JSON，其內容結構與內容片段中的一樣。參考是以參考 URL 的形式傳遞。

可能有兩種類型的讀取操作：

* 按路徑讀取特定內容片段，這將傳回內容片段的 JSON 表示。
* 按路徑讀取內容片段資料夾：這將傳回資料夾內所有內容片段的 JSON 表示。

### 建立 {#create}

使用方式：

`POST /{cfParentPath}/{cfName}`

內文必須包含要建立的內容片段的 JSON 表示，包括應在內容片段元素上設定的任何初始內容。必須設定 `cq:model` 屬性，並且它必須指向有效的內容片段模型。未這麼做會導致錯誤。也必須加上標頭 `Content-Type`，其設定為 `application/json`。

### 更新 {#update}

使用方式：

`PUT /{cfParentPath}/{cfName}`

內文必須包含給定內容片段要更新之內容的 JSON 表示。

這可以只是內容片段的標題或描述，或單一元素，或所有元素值和/或中繼資料。

### 刪除 {#delete}

使用方式：

`DELETE /{cfParentPath}/{cfName}`

如需使用 AEM Assets REST API 的更多詳細資訊，您可以參考：

* Adobe Experience Manager Assets HTTP API (其他資源)
* AEM Assets HTTP API 支援內容片段 (其他資源)

## 下一步 {#whats-next}

您已完成此部分的 AEM Headless 開發人員歷程，您應該：

* 了解 AEM Assets HTTP API 的基本知識。
* 了解此 API 如何支援內容片段。

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page is not going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

您應該透過下一次檢視檔案[如何與您的Headless應用程式上線](go-live.md)，繼續您的AEM Headless歷程，您將在其中實際將AEM Headless專案上線！

## 其他資源 {#additional-resources}

* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [內容片段 REST API](/help/assets/assets-api-content-fragments.md)
   * [API 參考](/help/assets/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager Assets API - 內容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)
* [使用內容片段](/help/assets/content-fragments/content-fragments.md)
* [AEM 核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)
* [CORS/AEM 說明](https://helpx.adobe.com/tw/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [影片 - 使用 AEM 開發 CORS](https://helpx.adobe.com/tw/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
* [AEM as a Headless CMS 簡介](/help/sites-developing/headless/introduction.md)
* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hant)
* [AEM 中的 Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hant)
