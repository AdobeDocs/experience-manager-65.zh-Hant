---
title: 持續性 GraphQL 查詢
description: 了解如何在Adobe Experience Manager中保留GraphQL查詢以最佳化效能。 用戶端應用程式可以使用 HTTP GET 方法要求持續性查詢，回應可以在 Dispatcher 和 CDN 層快取，最終提高用戶端應用程式的效能。
source-git-commit: 9369f7cb9c507bbd7d7761440ceef907552aeb7d
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 98%

---

# 持續性 GraphQL 查詢 {#persisted-queries-caching}

持續性查詢是在 Adobe Experience Manager (AEM) as a Cloud Service 伺服器上建立和儲存的 GraphQL 查詢。用戶端應用程式可以透過 GET 要求來要求它們。GET 要求的回應可以在 Dispatcher 和 CDN 層快取，最終提高發出要求之用戶端應用程式的效能。這與標準的 GraphQL 查詢不同，後者使用 POST 要求執行，其回應無法輕鬆快取。

<!--
>[!NOTE]
>
>Persisted Queries are recommended. See [GraphQL Query Best Practices (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) for details, and the related Dispatcher configuration.
-->

AEM 有提供 [GraphiQL IDE](/help/assets/content-fragments/graphiql-ide.md)，可讓您在[傳送到生產環境](#transfer-persisted-query-production)之前，開發、測試和保留您的 GraphQL 查詢。如果需要自訂 (例如[自訂快取](/help/assets/content-fragments/graphiql-ide.md#caching-persisted-queries)時)，您可以使用 API，請參閱[如何保留 GraphQL 查詢](#how-to-persist-query)中提供的 curl 範例。

## 持續性查詢和端點 {#persisted-queries-and-endpoints}

持續性查詢必須一律使用與[適當的 Sites 設定](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-aem-endpoint)相關的端點；所以可以使用以下其中之一，或兩者都使用：

* 全域設定和端點
查詢可以存取所有內容片段模型。
* 特定 Sites 設定和端點
為特定 Sites 設定建立持續性查詢時，需要相應的 Sites 設定專屬端點 (以提供相關內容片段模型的存取權)。
例如，若要專門為 WKND Sites 設定建立持續性查詢，必須提前建立相應的 WKND 專屬 Sites 設定和 WKND 專屬端點。

>[!NOTE]
>
>如需詳細資料，請參閱[在設定瀏覽器中啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)。
>
>必須為適當的 Sites 設定啟用 **GraphQL 持續性查詢**。

例如，如果有一個名為 `my-query` 的特定查詢，它使用 Sites 設定 `my-conf` 中的模型 `my-model`：

* 您可以使用 `my-conf` 專屬端點建立查詢，然後查詢將儲存為：
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 您可以使用 `global` 端點建立相同查詢，然後查詢將儲存為：
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>這是兩個不同的查詢 - 儲存在不同的路徑下。
>
>他們只是碰巧使用相同的模型，但透過不同的端點。

## 如何保留 GraphQL 查詢 {#how-to-persist-query}

建議最初在 AEM 作者環境中保留查詢，然後[將查詢傳輸到](#transfer-persisted-query-production)生產 AEM 發佈環境，以供應用程式使用。

有多種保留查詢的方法，包括：

* GraphiQL IDE - 請參閱[儲存持續性查詢](/help/assets/content-fragments/graphiql-ide.md#saving-persisted-queries) (首選方法)
* curl - 請參閱以下範例。
* 其他工具，包括 [Postman](https://www.postman.com/)

GraphiQL IDE 是保留查詢的&#x200B;**首選**&#x200B;方法。若要使用 **curl** 命令列工具保留給定查詢：

1. 透過將查詢放入新端點 URL `/graphql/persist.json/<config>/<persisted-label>` 來準備查詢。

   例如，建立持續性查詢：

   ```shell
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

1. 此時，檢查回應。

   例如，檢查是否成功：

   ```json
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 然後，您可以透過取得 URL `/graphql/execute.json/<shortPath>` 來要求持續性查詢。

   例如，使用持續性查詢：

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 透過發佈到一個已經存在的查詢路徑來更新持續性查詢。

   例如，使用持續性查詢：

   ```shell
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

1. 建立已包裝的普通查詢。

   例如：

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 建立含快取控制的已包裝普通查詢。

   例如：

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 建立含參數的持續性查詢：

   例如：

   ```shell
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


## 如何執行持續性查詢 {#execute-persisted-query}

若要執行持續性查詢，用戶端應用程式使用以下語法發出 GET 要求：

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

其中 `PERSISTENT_PATH` 是持續性查詢儲存所在的縮短路徑。

1. 例如 `wknd` 是設定名稱，`plain-article-query` 是持續性查詢的名稱。若要執行查詢：

   ```shell
   $ curl -X GET \
       https://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 執行含參數的查詢。

   >[!NOTE]
   >
   > 執行持續性查詢時，查詢變數和值必須正確[編碼](#encoding-query-url)。

   例如：

   ```xml
   $ curl -X GET \
       "https://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   如需詳細資料，請參閱使用[查詢變數](#query-variables)。

## 使用查詢變數 {#query-variables}

查詢變數可以與持續性查詢一起使用。查詢變數使用變數名稱和值附加到開頭為分號 (`;`) 的要求。多個變數會用分號分隔。

模式如下所示：

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

例如，以下查詢包含一個變數 `activity` 以根據活動值篩選清單：

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

此查詢可以保留在路徑 `wknd/adventures-by-activity` 下。若要在 `activity=Camping` 呼叫持續性查詢，要求將如下所示：

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

請注意，`%3B` 是 `;` 的 UTF-8 編碼，`%3D` 是 `=` 的編碼。查詢變數和任何特殊字元必須[正確編碼](#encoding-query-url)才能執行持續性查詢。

<!--
## Caching your persisted queries {#caching-persisted-queries}

Persisted queries are recommended as they can be cached at the dispatcher and CDN layers, ultimately improving the performance of the requesting client application.

By default AEM will invalidate the Content Delivery Network (CDN) cache based on a default Time To Live (TTL). 

This value is set to:

* 7200 seconds is the default TTL for the Dispatcher and CDN; also known as *shared caches*
  * default: s-maxage=7200
* 60 is the default TTL for the client (for example, a browser)
  * default: maxage=60

If you want to change the TTL for your GraphLQ query, then the query must be either:

* persisted after managing the [HTTP Cache headers - from the GraphQL IDE](#http-cache-headers)
* persisted using the [API method](#cache-api). 

### Managing HTTP Cache Headers in GraphQL  {#http-cache-headers-graphql}

The GraphiQL IDE - see [Saving Persisted Queries](/help/assets/content-fragments/graphiql-ide.md#managing-cache)

### Managing Cache from the API {#cache-api}

This involves posting the query to AEM using CURL in your command line interface. 

For an example:

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "https://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

The `cache-control` can be set at the creation time (PUT) or later on (for example, via a POST request for instance). The cache-control is optional when creating the persisted query, as AEM can provide the default value. See [How to persist a GraphQL query](#how-to-persist-query), for an example of persisting a query using curl.
-->

## 編碼查詢 URL 以供應用程式使用 {#encoding-query-url}

為供應用程式使用，建構查詢變數時使用的任何特殊字元 (即分號 (`;`)、等號 (`=`)、斜線 `/`) 必須是轉換為使用相應的 UTF-8 編碼。

例如：

```xml
curl -X GET \ "https://localhost:4502/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

URL 可以分解成以下幾個部分：

| URL 部分 | 說明 |
|----------| -------------|
| `/graphql/execute.json` | 持續性查詢端點 |
| `/wknd/adventure-by-path` | 持續性查詢路徑 |
| `%3B` | `;` 編碼 |
| `adventurePath` | 查詢變數 |
| `%3D` | `=` 編碼 |
| `%2F` | `/` 編碼 |
| `%2Fcontent%2Fdam...` | 內容片段的已編碼路徑 |

在純文字中，要求 URI 如下所示：

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

若要在用戶端應用程式中使用持續性查詢，AEM 無周邊用戶端 SDK 應該用於 [JavaScript](https://github.com/adobe/aem-headless-client-js)、[Java](https://github.com/adobe/aem-headless-client-java) 或 [NodeJS](https://github.com/adobe/aem-headless-client-nodejs)。Headless 用戶端 SDK 會自動將要求中的任何查詢變數適當地編碼。

## 將持續性查詢轉移到您的生產環境  {#transfer-persisted-query-production}

持續性查詢應一律建立在 AEM Author 服務上，然後發佈 (複製) 到 AEM Publish 服務。通常，持續性查詢是在低層環境 (例如本機或開發環境) 中建立和測試的。然後，必須將持續性查詢提升到高層環境，最終使它們能在生產 AEM Publish 環境中供用戶端應用程式使用。

### 封裝持續性查詢

持續性查詢可以內建在 [AEM 套件](/help/sites-administering/package-manager.md) 中。然後，AEM 套件可以下載和安裝在不同的環境中。AEM 套件也可以從 AEM 作者環境複製到 AEM 發佈環境。

若要建立套件：

1. 導覽至&#x200B;**工具** > **部署** > **套件**。
1. 點選&#x200B;**建立套件**&#x200B;來建立新套件。這將開啟一個對話框來定義套件。
1. 在套件定義對話框中，在 **一般**&#x200B;下輸入&#x200B;**名稱**，例如「wknd-persistent-queries」。
1. 輸入版本號碼，例如「1.0」。
1. 在&#x200B;**篩選器**&#x200B;下加入新&#x200B;**篩選器**。使用路徑尋找工具選取設定下方的 `persistentQueries` 資料夾。例如，對於 `wknd` 設定，完整路徑將為 `/conf/wknd/settings/graphql/persistentQueries`。
1. 點選&#x200B;**儲存**&#x200B;以儲存新的套件定義並關閉對話框。
1. 點選新建立之套件定義中的&#x200B;**建置**&#x200B;按鈕。

建置套件後，您可以：

* **下載**&#x200B;套件並在不同環境中重新上傳。
* 點選&#x200B;**更多** > **複製**&#x200B;來&#x200B;**複製**&#x200B;套件。這會將套件複製到連接的 AEM 發佈環境。

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
