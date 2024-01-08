---
title: 最佳化 GraphQL 查詢
description: 瞭解如何在Adobe Experience Manager as a Cloud Service中篩選、分頁和排序內容片段時最佳化GraphQL查詢，以進行Headless內容傳送。
exl-id: 47d0570b-224e-4109-b94e-ccc369d7ac5f
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 58%

---

# 最佳化 GraphQL 查詢 {#optimizing-graphql-queries}

>[!NOTE]
>
>套用這些最佳化建議之前，請考慮 [在GraphQL篩選中更新要分頁和排序的內容片段](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) 獲得最佳效能。

提供這些准則是為了協助防止您的GraphQL查詢出現效能問題。

## GraphQL檢查清單 {#graphql-checklist}

下列檢查清單旨在協助您在Adobe Experience Manager (AEM)as a Cloud Service中最佳化GraphQL的設定和使用。

### 首要原則 {#first-principles}

#### 使用持續的GraphQL查詢 {#use-persisted-graphql-queries}

**建議**

強烈建議使用持續的GraphQL查詢。

持續的GraphQL查詢利用內容傳遞網路(CDN)來協助降低查詢執行效能。 使用者端應用程式要求持續查詢，而GET要求快速啟用邊緣的執行。

**進一步參考資料**

請參閱：

* [持續的GraphQL查詢](/help/sites-developing/headless/graphql-api/persisted-queries.md).
* [了解搭配使用 GraphQL 與 AEM - 範例內容和查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md)

#### 安裝GraphQL索引套件 {#install-graphql-index-package}

**建議**

使用GraphQL的客戶 *必須* 使用GraphQL索引封裝安裝Experience Manager內容片段。 如此一來，您就可以根據使用者實際使用的功能，新增必要的索引定義。 無法安裝此套件可能會導致GraphQL查詢變慢或失敗。

如需瞭解適合您Service Pack的版本，請參閱發行說明。 例如，如需最新的Service Pack，請參閱 [安裝Experience Manager內容片段的GraphQL索引套件](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) .

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝。

**進一步參考資料**
請參閱：

* [安裝Experience Manager內容片段的GraphQL索引套件](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package)

### 快取策略 {#cache-strategy}

您也可以使用各種快取方法來最佳化。

#### 啟用AEM Dispatcher快 {#enable-aem-dispatcher-caching}

**建議**

[AEM傳送器](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) 是AEM服務中的第一層快取，在CDN快取之前。

**進一步參考資料**

請參閱：

* [GraphQL 持續性查詢 - 在 Dispatcher 中啟用快取](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphql-persisted-queries-enabling-caching-dispatcher)

#### 使用內容傳遞網路(CDN) {#use-cdn}

**建議**

如果定位為，則可快取GraphQL查詢及其JSON回應 `GET` 使用CDN時的請求。 相反地，未快取的請求可能非常（資源）昂貴且處理緩慢，可能對來源的資源造成進一步的負面影響。

**進一步參考資料**

請參閱：

* [在AEM中使用CDN](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn)

#### 設定HTTP快取控制標題 {#set-http-cache-control-headers}

**建議**

搭配CDN使用持續的GraphQL查詢時，建議設定適當的HTTP快取控制標頭。

每個持續性查詢可以有自己一組特定的快取控制標頭。 標題可設定在 [GRAPHQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md).

您也可以使用設定 **cURL** 命令列工具。 例如，使用 `PUT` 要求使用快取控制項建立包裝的簡單查詢。

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

**進一步參考資料**

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

### GraphQL查詢最佳化 {#graphql-query-optimization}

在具備大量共有相同模式內容片段的 AEM 執行個體上，GraphQL 列表查詢費用可能會變得很昂貴 (以資源來說)。

這是因為在 GraphQL 查詢中使用共用一個模式的&#x200B;*所有*&#x200B;片段必須載入記憶體中。這會消耗時間和記憶體。篩選 (可能會減少 (最終) 結果集中的項目數量) 只能在&#x200B;****&#x200B;將整個結果集載入記憶體後應用。

這可能會給人留下這樣的印象，即使是很小的結果集 (也可能) 會導致效能不佳。然而，實際上緩慢是由初始結果集的大小引起的，因為它必須在套用篩選之前在內部進行處理。

為了減少效能和記憶體問題，這個初始結果集必須盡可能維持最小。

AEM 提供兩種方式進行 GraphQL 查詢最佳化：

* [混合篩選](#use-aem-graphql-hybrid-filtering)
* [分頁](#use-aem-graphql-pagination) (或進行分頁)

   * [排序](#use-graphql-sorting)與最佳化沒有直接關係，而是與分頁有關

每種方法都有自己的使用案例和局限性。本節提供混合式篩選和分頁的相關資訊，以及部分 [最佳實務](#best-practices) 以便用於最佳化GraphQL查詢。

#### 使用AEM GraphQL混合篩選 {#use-aem-graphql-hybrid-filtering}

**建議**

混合篩選結合了 JCR 篩選和 AEM 篩選。

在將結果集載入記憶體以進行 AEM 篩選之前，這類篩選會套用 JCR 篩選器 (以查詢限制的形式)。這是為了減少載入記憶體內的結果集，因為 JCR 篩選器會在此之前刪除多餘的結果。

>[!NOTE]
>
>出於技術原因 (例如靈活性、片段嵌套)，AEM 無法將整個篩選作業委派給 JCR。

這種技術保留了 GraphQL 篩選器提供的靈活性，同時將盡可能多將篩選作業委派給 JCR。

>[!NOTE]
>
>AEM混合篩選需要更新現有的內容片段

**進一步參考資料**

請參閱：

* [在GraphQL篩選中更新要分頁和排序的內容片段](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md)
* [依 _tags ID 進行篩選並排除變化的範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

#### 使用GraphQL分頁 {#use-aem-graphql-pagination}

**建議**

透過使用GraphQL標準pagination將回應分割為區塊，可改善具有大型結果集的複雜查詢的回應時間。

AEM中的GraphQL支援兩種分頁型別：

* [限制/以偏移量為基礎的分頁](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
這用於清單查詢；這些結尾為 `List`；例如， `articleList`.
若要使用，您必須提供第一個要返回項目的位置 (`offset`) 和要返回的項目數 (`limit`，或頁面大小)。

* [游標式分頁](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after) (以 `first` 和 `after` 表示)
這為每個項目提供了唯一 ID；也稱為游標。
在查詢中，您要指定上一頁最後一項的游標，加上頁面大小 (要返回的最大項目數)。

  由於游標式分頁不適合列表式查詢的資料結構，AEM 引入了 `Paginated` 查詢類型；例如，`articlePaginated`。使用的資料結構和參數需依 [GraphQL 游標連接規格](https://relay.dev/graphql/connections.htm)訂定。

  >[!NOTE]
  >
  >AEM 目前支援前向分頁 (使用 `after`/`first` 參數)。
  >
  >不支援向後分頁 (使用 `before`/`last` 參數)。

**進一步參考資料**

請參閱：

* [使用 first 和 after 的範例分頁查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-pagination-first-after)

#### 使用GraphQL排序 {#use-graphql-sorting}

**建議**

這也是GraphQL標準，排序可讓使用者端以排序的順序接收JSON內容。 這可以降低在使用者端上進一步處理的需求。

只有所有排序標準都與頂層片段相關時，排序才有效。

如果排序的順序包括位於嵌套片段上的一個或多個欄位，則必須將共用頂層模式的所有片段載入記憶體中。這會對效能產生負面影響。

>[!NOTE]
>
>對頂層欄位進行排序也會對效能產生 (儘管很小) 影響。

**進一步參考資料**

請參閱：

* [具有依_tags ID篩選並排除變數，以及依名稱排序的範例查詢](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

## 最佳做法 {#best-practices}

所有最佳化建議的主要目標是減少初始結果集。 此處所列最佳實務提供許多方式來達到這個目標。這些方式可以 (且應該) 合起來使用。

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

### 將內容片段巢狀最小化 {#minimize-content-fragment-nesting}

巢狀內容片段是建立自訂內容結構模型的好方法。 您甚至可以有含巢狀片段的片段，其中包含巢狀片段、具有……等等。

但是，如果建立的結構包含太多層級，可能會增加GraphQL查詢的處理時間，因為GraphQL必須周遊所有巢狀內容片段的整個階層。

深層巢狀結構也會對內容控管造成不良影響。 一般而言，建議將內容片段巢狀限制在五或六個層級以下。

### 不要輸出所有格式（多行文字元素） {#do-not-output-all-formats}

AEM GraphQL可傳回文字，其製作方式為 **[多行文字](/help/assets/content-fragments/content-fragments-models.md#data-types)** 資料型別，有多種格式： RTF、簡單文字和Markdown。

輸出全部三種格式會將JSON中文字輸出的大小增加3倍。 再加上來自非常廣泛查詢的通常大型結果集，可能會產生非常大的JSON回應，因此需要很長時間才能計算。 最好將輸出限製為呈現內容所需的文字格式。

### 修改內容片段 {#modifying-content-fragments}

僅使用AEM UI或API修改內容片段及其資源。 請勿直接在JCR中進行修改。

### 測試您的查詢 {#test-your-queries}

處理GraphQL查詢與處理搜尋查詢類似，而且比簡單的包含所有內容的GETAPI請求要複雜得多。

在生產環境中使用查詢時，在受控的非生產環境中仔細規劃、測試和最佳化您的查詢，是日後取得成功的關鍵。
