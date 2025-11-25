---
title: 最佳化 GraphQL 查詢
description: 瞭解如何在Adobe Experience Manager as a Cloud Service中篩選、分頁和排序內容片段時最佳化GraphQL查詢，以進行Headless內容傳送。
exl-id: 47d0570b-224e-4109-b94e-ccc369d7ac5f
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 88%

---

# 最佳化 GraphQL 查詢 {#optimizing-graphql-queries}

>[!NOTE]
>
>在套用這些最佳化建議之前，請考慮[在GraphQL篩選中更新您的內容片段以進行分頁和排序](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md)以獲得最佳效能。

提供這些指南是為了幫助防止 GraphQL 查詢出現效能問題。

## GraphQL 檢查清單 {#graphql-checklist}

以下檢查清單旨在協助您在 Adobe Experience Manager (AEM) as a Cloud Service 中最佳化 GraphQL 的設定和使用。

### 第一原則 {#first-principles}

#### 使用持續性 GraphQL 查詢 {#use-persisted-graphql-queries}

**推薦**

強烈建議使用持續性 GraphQL 查詢。

持續性 GraphQL 查詢利用內容傳遞網路 (CDN) 來幫助降低查詢執行效能。用戶端應用程式透過 GET 要求要求持續性查詢，以達到邊緣支援的快速執行。

**進一步參考**

請參閱：

* [持續性 GraphQL 查詢](/help/sites-developing/headless/graphql-api/persisted-queries.md).
* [了解搭配使用 GraphQL 與 AEM - 範例內容和查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md)

#### 安裝GraphQL索引套件 {#install-graphql-index-package}

**推薦**

使用GraphQL *的客戶必須*&#x200B;安裝Experience Manager內容片段與GraphQL索引套件。 如此一來，您就可以根據使用者實際使用的功能，新增必要的索引定義。 無法安裝此套件可能會導致GraphQL查詢變慢或失敗。

如需瞭解適合您Service Pack的版本，請參閱發行說明。 例如，如需最新的Service Pack，請參閱[安裝GraphQL內容片段的Experience Manager索引套件](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) 。

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝。

**其他參考**
請參閱：

* [安裝適用於Experience Manager內容片段的GraphQL索引套件](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package)

### 快取策略 {#cache-strategy}

還可以使用各種快取方法進行最佳化。

#### 啟用 AEM Dispatcher 快取 {#enable-aem-dispatcher-caching}

**推薦**

[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) 是 AEM 服務中的第一層快取，位於 CDN 快取之前。

**進一步參考**

請參閱：

* [GraphQL 持續性查詢 - 在 Dispatcher 中啟用快取](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphql-persisted-queries-enabling-caching-dispatcher)

#### 使用內容傳遞網路 (CDN) {#use-cdn}

**推薦**

使用 CDN 時，如果作為目標 `GET` 要求，則可以快取 GraphQL 查詢及其 JSON 回應。相反地，未快取的要求可能非常昂貴 (資源) 且處理速度緩慢，並且可能對來源資源產生進一步的有害影響。

**進一步參考**

請參閱：

* [在AEM中使用CDN](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn)

#### 設定 HTTP 快取控制標頭 {#set-http-cache-control-headers}

**推薦**

當將持續性 GraphQL 查詢與 CDN 結合使用時，建議設定適當的 HTTP 快取控制標頭。

每個持續性查詢都可以有自己特定的一組快取控制標頭。標頭可透過[GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)設定。

也可以使用&#x200B;**cURL**&#x200B;命令列工具來設定它們。 例如，使用`PUT`要求建立含快取控制項的包裝簡單查詢。

```shell
$ curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

<!-- or the [AEM GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache). 
-->

**進一步參考**

請參閱：

* [快取持續性查詢](/help/sites-developing/headless/graphql-api/persisted-queries.md#caching-persisted-queries)
* [如何保留 GraphQL 查詢](/help/sites-developing/headless/graphql-api/persisted-queries.md#how-to-persist-query)
<!--
* [Managing cache for your persisted queries](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache)
-->

<!--
#### Use AEM GraphQL pre-caching {#use-aem-graphql-pre-caching}

**Recommendation**

This capability allows AEM to further cache content within the scope of GraphQL queries that can then be assembled as blocks in JSON output rather than line by line. 

**Further Reference**

Contact Adobe to enable this capability for your AEM Cloud Service program and environments. 
-->

### GraphQL 查詢最佳化 {#graphql-query-optimization}

在具備大量共有相同模式內容片段的 AEM 執行個體上，GraphQL 列表查詢費用可能會變得很昂貴 (以資源來說)。

這是因為在 GraphQL 查詢中使用共用一個模式的&#x200B;*所有*&#x200B;片段必須載入記憶體中。這會消耗時間和記憶體。篩選 (可能會減少 (最終) 結果集中的項目數量) 只能在&#x200B;**&#x200B;**&#x200B;將整個結果集載入記憶體後應用。

這可能會給人留下這樣的印象，即使是很小的結果集 (也可能) 會導致效能不佳。然而，實際上緩慢是由初始結果集的大小引起的，因為它必須在套用篩選之前在內部進行處理。

為了減少效能和記憶體問題，這個初始結果集必須盡可能維持最小。

AEM 提供兩種方式進行 GraphQL 查詢最佳化：

* [混合篩選](#use-aem-graphql-hybrid-filtering)
* [分頁](#use-aem-graphql-pagination) (或進行分頁)

   * [排序](#use-graphql-sorting)與最佳化沒有直接關係，而是與分頁有關

每種方法都有自己的使用案例和局限性。本節提供有關混合篩選和分頁的資訊，以及一些用於最佳化 GraphQL 查詢的[最佳實務](#best-practices)。

#### 使用 AEM GraphQL 混合篩選 {#use-aem-graphql-hybrid-filtering}

**推薦**

混合篩選結合了 JCR 篩選和 AEM 篩選。

在將結果集載入記憶體以進行 AEM 篩選之前，這類篩選會套用 JCR 篩選器 (以查詢限制的形式)。這是為了減少載入記憶體內的結果集，因為 JCR 篩選器會在此之前刪除多餘的結果。

>[!NOTE]
>
>出於技術原因 (例如靈活性、片段嵌套)，AEM 無法將整個篩選作業委派給 JCR。

這種技術保留了 GraphQL 篩選器提供的靈活性，同時將盡可能多將篩選作業委派給 JCR。

>[!NOTE]
>
>AEM 混合篩選需要更新現有內容片段

**進一步參考**

請參閱：

* [更新內容片段以在 GraphQL 篩選中進行分頁和排序](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md)
* [依 _tags ID 進行篩選並排除變化的範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

#### 使用 GraphQL 分頁 {#use-aem-graphql-pagination}

**推薦**

透過使用分頁 (一種 GraphQL 標準) 將回應分段為區塊，可以縮短具有大型結果集的複雜查詢的回應時間。

AEM中的GraphQL支援兩種分頁型別：

* [限制式/位移式分頁](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
這是用於列表查詢；這些結尾是 `List`；例如 `articleList`。若要使用，您必須提供第一個要返回項目的位置 (`offset`) 和要返回的項目數 (`limit`，或頁面大小)。

* [游標式分頁](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after) (以 `first` 和 `after` 表示)
這為每個項目提供了唯一 ID；也稱為游標。
在查詢中，您要指定上一頁最後一項的游標，加上頁面大小 (要返回的最大項目數)。

  由於游標式分頁不適合列表式查詢的資料結構，AEM 引入了 `Paginated` 查詢類型；例如，`articlePaginated`。使用的資料結構和參數需依 [GraphQL 游標連接規格](https://relay.dev/graphql/connections.htm)訂定。

  >[!NOTE]
  >
  >AEM 目前支援前向分頁 (使用 `after`/`first` 參數)。
  >
  >不支援向後分頁 (使用 `before`/`last` 參數)。

**進一步參考**

請參閱：

* [使用 first 和 after 的範例分頁查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-pagination-first-after)

#### 使用 GraphQL 排序 {#use-graphql-sorting}

**推薦**

排序也是一種 GraphQL 標準，使用戶端能夠按排序順序接收 JSON 內容。這可以減少用戶端進一步處理的需要。

只有所有排序標準都與頂層片段相關時，排序才有效。

如果排序的順序包括位於嵌套片段上的一個或多個欄位，則必須將共用頂層模式的所有片段載入記憶體中。這會對效能產生負面影響。

>[!NOTE]
>
>對頂層欄位進行排序也會對效能產生 (儘管很小) 影響。

**進一步參考**

請參閱：

* [依 _tags ID 進行篩選並排除變化的範例查詢，按名稱排序](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

## 最佳做法 {#best-practices}

所有最佳化推薦的主要目標是要減少初始結果集。此處所列最佳實務提供許多方式來達到這個目標。這些方式可以 (且應該) 合起來使用。

### 限針對頂層屬性的篩選器 {#filter-top-level-properties-only}

目前，JCR 級別的篩選僅適用於頂層片段。

如果篩選器要處理嵌套片段的欄位，AEM 必須退回以載入所有共用基本模式的片段 (至記憶體中)。

您仍然可以透過使用 [AND 運算元](#logical-operations-in-filter-expressions)來組合頂層片段欄位上的篩選器運算式和嵌套片段欄位上的篩選器運算式來最佳化此類 GraphQL 查詢。

### 使用內容結構 {#use-content-structure}

在 AEM 中，使用存放庫結構來縮小要處理的內容範圍通常被視為是很好的做法。

這種方法也應該應用於 GraphQL 查詢。

這可以通過在頂層片段的 `_path` 欄位上應用篩選器來完成：

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>`value` 必須要有 `/` 行尾才能達到最佳效能。

### 使用分頁 {#use-paging}

您還可以使用分頁來減少初始結果集；特別是如果您的請求不使用任何篩選和排序。

如果您對嵌套片段進行篩選或排序，分頁查詢可能仍然很慢，因為 AEM 可能仍需要將大量片段載入記憶體中。因此，如果結合篩選和分頁，請考慮遵守篩選規則 (如上所述)。

對於分頁，排序同樣重要，因為分頁結果一定會排序 (無論是顯式還是隱式)。

如果您主要只有興趣擷取前幾頁內容，則使用 `...List` 或 `...Paginated` 查詢之間沒有顯著差異。但是，如果您的應用程式不僅有興趣閱讀一兩頁，您應該考慮 `...Paginated` 查詢，因為這在後面頁面的查詢效能更好。

### 篩選器運算式中的邏輯運算 {#logical-operations-in-filter-expressions}

如果您在嵌套片段上進行篩選，您仍然可以透過在使用 `AND` 運算元來組合的頂層欄位上提供隨附的篩選器來套用 JCR 篩選。

一個典型使用案例是在頂層片段的 `_path` 欄位上使用篩選器來限制查詢的範圍，然後篩選可能位於頂層的其他欄位，或者篩選可能在嵌套片段上的欄位。

在這種情況下，不同的篩選器運算式將與 `AND` 結合。因此，`_path` 上的篩選器可以有效限制初始結果集。頂層欄位上的所有其他篩選器也可以幫助減少初始結果集 - 只要篩選器與 `AND` 結合使用。

如果涉及嵌套片段，篩選運算式結合 `OR` 則無法進行最佳化。只有&#x200B;*不涉及*&#x200B;嵌套片段時，`OR` 運算式才可進行最佳化。

### 避免篩選多行文字欄位 {#avoid-filtering-multiline-textfields}

多行文字欄位 (html、markdown、純文本字、json) 的欄位無法通過 JCR 查詢進行篩選，因為這些欄位的內容必須進行動態計算。

如果您仍然需要在多行文字欄位上進行篩選，請考慮透過新增額外的篩選運算式並將其與 `AND` 結合來限制初始結果集的大小。透過對 `_path` 欄位進行篩選來限制範圍也是一種很好的方法。

### 避免篩選虛擬欄位 {#avoid-filtering-virtual-fields}

虛擬欄位 (大多數以 `_` 開頭的欄位) 是在執行 GraphQL 查詢時進行計算，因此不在以 JCR 為主的篩選範圍內。

有個重要的例外是 `_path` 欄位；這個欄位可以有效地用於減小初始結果集的大小 - 如果是根據內容結構來進行 (請參閱[使用內容結構](#use-content-structure))。

### 篩選：排除 {#filtering-exclusions}

還有其他幾種情況無法在 JCR 級別評估篩選器運算式 (因此應該避免這些情況以達到最佳效能)：

* 使用 `_sensitiveness` 篩選選項的 `Float` 值篩選運算式，且其中的 `_sensitiveness` 設定為 `0.0` 以外的任何值。

* 使用 `_ignoreCase` 篩選器選項來篩選 `String` 值的運算式。

* 篩選 `null` 值。

* 使用 `_apply: ALL_OR_EMPTY` 陣列的篩選器。

* 使用 `_apply: INSTANCES`、`_instances: 0` 陣列的篩選器。

* 使用 `CONTAINS_NOT` 運算元來篩選運算式。

* 使用 `NOT_AT` 運算元來篩選 `Calendar`、`Date` 或 `Time` 值的運算式。

### 最小化內容片段巢狀內嵌 {#minimize-content-fragment-nesting}

巢狀內容片段是為自訂內容結構建立模型的絕佳方法。您甚至可以有含巢狀片段的片段，其中包含巢狀片段、具有……等等。

然而，建立具有過多層級的結構可能會增加 GraphQL 查詢的處理時間，因為 GraphQL 需要遍歷所有巢狀內容片段的整個層級結構。

深層巢狀結構還可能對內容治理產生不利影響。通常建議將內容片段的巢狀層級限制在五層或六層以下。

### 不要輸出所有格式 (多行文字元素) {#do-not-output-all-formats}

AEM GraphQL 可以以多種格式傳回在&#x200B;**[多行文字](/help/assets/content-fragments/content-fragments-models.md#data-types)**&#x200B;資料類型中編寫的文字：RTF 文字、簡單文字和 Markdown。

輸出所有三種格式會使 JSON 中的文字輸出大小增加三倍。再加上來自廣泛查詢，通常較大的結果集，可能會產生非常大的 JSON 回應，從而導致計算所需的時間很長。最好將輸出限制為僅轉譯內容所需的文字格式。

### 修改內容片段 {#modifying-content-fragments}

僅使用 AEM UI 或 API 修改內容片段及其資源。不要直接在 JCR 中進行修改。

### 測試您的查詢 {#test-your-queries}

處理 GraphQL 查詢類似於處理搜尋查詢，並且比簡單的 GET-all-content API 要求複雜得多。

在受控的非生產環境中仔細規劃、測試和最佳化查詢是在生產環境中成功使用的關鍵。
