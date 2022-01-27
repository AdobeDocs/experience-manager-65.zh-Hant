---
title: 快取和效能
description: 瞭解可用於啟用GraphQL和內容快取以優化您的商務實施效能的不同配置。
exl-id: ecce64bf-5960-4ddb-b6e3-dad401038c11
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 1%

---

# 快取和效能 {#caching}

## 元件和GraphQL響應快取 {#graphql}

CIFAEM核心元件已內置了對單個元件的GraphQL響應的快取支援。 此功能可用於將GraphQL後端調用數減少很大。 可實現有效的快取，特別是對於重複查詢，例如檢索導航元件的類別樹或讀取在產品搜索和類別頁面上顯示的所有可用聚合/小平面值。

對於AEMCIF核心元件，快取是基於元件進行配置的，因此可以控制是否（以及多長時間）為每個元件快取GraphQL請求/響應。 也可以使用GraphQL客戶端定義OSGi服務的快取行為。

### 設定

為給定元件配置後，快取開始儲存由每個快取配置項定義的GraphQL查詢和響應。 快取的大小和每個條目的快取持續時間將根據項目進行定義，例如，根據目錄資料可能更改的頻率、元件始終顯示最新可能資料的關鍵程度等而定。 請注意，沒有任何快取失效，因此在設定快取持續時間時要小心。

為元件配置快取時，快取名稱必須是 **代理** 在項目中定義的元件。

在客戶端發送GraphQL請求之前，它會檢查是否 **精確** 同一GraphQL請求已快取，並可能返回快取響應。 要匹配，GraphQL請求必須完全匹配，即查詢、操作名稱（如果有）、變數（如果有）必須等於快取請求，並且可能設定的所有自定義HTTP標頭也必須相同。 比如說Adobe Commerce `Store` 標頭必須匹配。

### 示例

我們建議為搜索服務配置一些快取，以提取產品搜索和類別頁上顯示的所有可用聚合/小平面值。 這些值通常僅在新屬性被添加到產品時才會更改，因此，如果產品屬性集不經常更改，則此快取條目的持續時間可能「很大」。 雖然這是特定於項目的，但我們建議在項目開發階段使用幾分鐘的價值，在穩定的生產系統上使用幾個小時的價值。

這通常使用以下快取項配置：

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

建議使用GraphQl快取功能的另一個示例方案是導航元件，因為它在所有頁上發送相同的GraphQL查詢。 在這種情況下，快取項通常設定為：

```
venia/components/structure/navigation:true:10:600
```

當考慮 [Venia參考儲存](https://github.com/adobe/aem-cif-guides-venia) 的子菜單。 注意元件代理名稱的使用 `venia/components/structure/navigation`, **不** CIF導航元件的名稱(`core/cif/components/structure/navigation/v1/navigation`)。

其他元件的快取應基於項目定義，通常與在Dispatcher級別配置的快取相協調。 請記住，這些快取沒有任何活動失效，因此應仔細設定快取持續時間。 沒有任何「一刀切」值可匹配所有可能的項目和使用案例。 確保在項目級別定義最適合項目要求的快取策略。

## 調度程式快取 {#dispatcher}

快取AEM中的頁或片段 [調度AEM程式](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant) 是任何項目的最佳AEM實踐。 通常，它依賴於無效技術來確保在中更改的任何內容AEM在Dispatcher中正確更新。 這是Dispatcher快取策略的AEM核心功能。

除了純受管AEM理的內容CIF外，頁面通常還可以顯示通過GraphQL從Adobe Commerce動態獲取的商業資料。 雖然頁面結構本身可能永遠不會更改，但商業內容可能會更改，例如，如果某些產品資料（如名稱或價格）在Adobe Commerce發生更改。

為確保CIF頁可以在Dispatcher中快取有限的時間AEM，我們建議使用 [基於時間的快取無效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-time-based-cache-invalidation-enablettl) 快取Dispatcher中的CIF頁時(也稱為基於TTL的緩AEM存)。 此功能可配AEM置為 [ACS公AEM域](https://adobe-consulting-services.github.io/acs-aem-commons/) 檔案。

使用基於TTL的快取，開發人員通常為選定頁定義一個或多個快取持AEM續時間。 這確保CIF頁只在Dispatcher中快取到AEM配置的持續時間，並且內容將頻繁更新。

>[!NOTE]
>
>雖然伺服器端資料可能由Dispatcher緩AEM存，但某些CIF元件(如 `product`。 `productlist`, `searchresults` 在載入頁面時，元件通常會在客戶端瀏覽器請求中重新獲取產品價格。 這可確保在頁面載入時始終讀取關鍵的動態內容。

## 其他資源

- [Venia參考儲存](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQL快取配置](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [調度AEM程式](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
