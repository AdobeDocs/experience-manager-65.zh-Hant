---
title: 最佳化 GraphQL 查詢
description: 瞭解如何在Adobe Experience Manager as a Cloud Service中篩選、分頁和排序內容片段時最佳化GraphQL查詢，以進行Headless內容傳送。
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 58%

---


# 最佳化 GraphQL 查詢 {#optimizing-graphql-queries}

>[!NOTE]
>
>在套用這些最佳化建議之前，請考慮 [更新GraphQL篩選中用於分頁和排序的內容片段](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) 獲得最佳效能。

在具有相同模型的大量內容片段的AEM執行個體上，GraphQL清單查詢可能會變得昂貴（就資源而言）。

原因在於 *全部* 共用GraphQL查詢中所使用模型的片段必須載入記憶體。 這樣做會同時消耗時間和記憶體。 篩選 (可能會減少 (最終) 結果集中的項目數量) 只能在&#x200B;****&#x200B;將整個結果集載入記憶體後應用。

此程式可能會造成即使很小的結果集（可能）也會導致效能不佳的印象。 但實際上，速度變慢是由初始結果集的大小所造成，因為必須先由內部處理才能套用篩選。

為了減少效能和記憶體問題，這個初始結果集必須盡可能維持最小。

AEM 提供兩種方式進行 GraphQL 查詢最佳化：

* [混合篩選](#hybrid-filtering)
* [分頁](#paging) (或進行分頁)

   * [排序](#sorting)與最佳化沒有直接關係，而是與分頁有關

每種方法都有自己的使用案例和局限性。 本文件提供有關混合篩選和分頁的資訊，以及一些最佳化 GraphQL 查詢的[最佳實務](#best-practices)。

## 混合篩選 {#hybrid-filtering}

混合篩選結合了 JCR 篩選和 AEM 篩選。

在將結果集載入記憶體以進行 AEM 篩選之前，這類篩選會套用 JCR 篩選器 (以查詢限制的形式)。 此程式是為了減少載入記憶體的結果集，因為JCR篩選器會預先移除多餘的結果。

>[!NOTE]
>
>由於技術原因（例如，靈活性、片段的巢狀），AEM無法將整個篩選委派給JCR。

這種技術保留了 GraphQL 篩選器提供的靈活性，同時將盡可能多將篩選作業委託給 JCR。

## 分頁 {#paging}

AEM中的GraphQL支援兩種分頁型別：

* [限制/以偏移量為基礎的分頁](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
此型別的分頁用於清單查詢；這些查詢的結尾是 
`List`；例如， `articleList`。
若要使用，您必須提供第一個要返回項目的位置 (`offset`) 和要返回的項目數 (`limit`，或頁面大小)。

* [游標型分頁](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after) (代表為 `first`和 `after`)此分頁型別為每個專案提供唯一的ID；也稱為游標。
在查詢中，您要指定上一頁最後一項的游標，加上頁面大小 (要返回的最大項目數)。

   由於游標式分頁不適合列表式查詢的資料結構，AEM 引入了 `Paginated` 查詢類型；例如，`articlePaginated`。使用的資料結構和參數需依 [GraphQL 游標連接規格](https://relay.dev/graphql/connections.htm)訂定。

   >[!NOTE]
   >
   >AEM 目前支援前向分頁 (使用 `after`/`first` 參數)。
   >
   >不支援向後分頁 (使用 `before`/`last` 參數)。

## 排序 {#sorting}

只有所有排序標準都與頂層片段相關時，排序才有效。

如果排序順序包括巢狀片段上的一或多個欄位，則必須將共用頂層模型的所有片段載入記憶體。 此流量會對效能造成負面影響。

>[!NOTE]
>
>對頂層欄位進行排序也會對效能產生 (儘管很小) 影響。

## 最佳做法 {#best-practices}

所有最佳化的主要目標是要減少初始結果集。 此處所列最佳實務提供許多方式來達到這個目標。這些方式可以 (且應該) 合起來使用。

### 限針對頂層屬性的篩選器 {#filter-top-level-properties-only}

目前，JCR 級別的篩選僅適用於頂層片段。

如果篩選器要處理嵌套片段的欄位，AEM 必須退回以載入所有共用基本模式的片段 (至記憶體中)。

您仍然可以透過結合頂層片段欄位和巢狀片段欄位上的篩選運算式來最佳化此類GraphQL查詢。 [AND運運算元](#logical-operations-in-filter-expressions).

### 使用內容結構 {#use-content-structure}

在AEM中，使用存放庫結構來縮小要處理的內容範圍被認為是良好的做法。

將此方法套用至GraphQL查詢，方法是在 `_path` 頂層片段的欄位：

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

如果您篩選或排序巢狀片段，分頁查詢可能仍然會很慢，因為AEM仍必須將更多片段載入記憶體中。 因此，如果結合篩選和分頁，請考慮遵守篩選規則 (如上所述)。

對於分頁，排序同樣重要，因為分頁結果一定會排序 (無論是顯式還是隱式)。

如果您主要只有興趣擷取前幾頁內容，則使用 `...List` 或 `...Paginated` 查詢之間沒有顯著差異。 但是，如果您的應用程式不僅有興趣閱讀一兩頁，您應該考慮 `...Paginated` 查詢，因為這在後面頁面的查詢效能更好。

### 篩選器運算式中的邏輯運算 {#logical-operations-in-filter-expressions}

如果您正在篩選巢狀片段，您仍然可以套用JCR篩選，方法是在使用 `AND` 運運算元。

典型的使用案例是使用 `_path` 頂層片段的欄位。 然後，篩選可能在頂層或巢狀片段上的其他欄位。

在這種情況下，不同的篩選器運算式將與 `AND` 結合。因此，`_path` 上的篩選器可以有效限制初始結果集。 頂層欄位上的所有其他篩選器也可以幫助減少初始結果集 - 只要篩選器與 `AND` 結合使用。

如果涉及嵌套片段，篩選運算式結合 `OR` 則無法進行最佳化。 此類 `OR` 運算式只能最佳化於 *否* 涉及巢狀片段。

### 避免篩選多行文字欄位 {#avoid-filtering-multiline-textfields}

無法透過JCR查詢篩選多行文字欄位（html、markdown、純文字、json）的欄位，因為這些欄位的內容必須即時計算。

如果您仍然必須篩選多行文字欄位，請考慮新增其他篩選運算式並將它們與合併，以限制初始結果集的大小 `AND`. 透過對 `_path` 欄位進行篩選來限制範圍也是一種很好的方法。

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

* 篩選上的運算式 `Calendar`， `Date`，或 `Time` 使用 `NOT_AT` 運運算元。
