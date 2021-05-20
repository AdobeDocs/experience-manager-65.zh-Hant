---
title: 快取與效能
description: 了解可啟用GraphQL和內容快取以最佳化商務實作效能的不同設定。
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 1%

---

# 快取與效能 {#caching}

## 元件和GraphQL回應快取 {#graphql}

AEM CIF核心元件已內建支援個別元件的快取GraphQL回應。 此功能可用來將GraphQL後端呼叫的數量減少很大。 對於重複查詢，例如檢索導航元件的類別樹或提取產品搜索和類別頁上顯示的所有可用聚合/刻面值，可以實現有效快取。

對於AEM CIF核心元件，快取是以元件為基礎進行設定，因此您可以控制是否對每個元件快取GraphQL請求/回應（以及快取的時間）。 您也可以使用GraphQL用戶端來定義OSGi服務的快取行為。

### 設定

為給定元件配置後，快取開始儲存由每個快取配置項定義的GraphQL查詢和響應。 快取的大小和每個項目的快取持續時間將根據項目來定義，具體取決於目錄資料更改的頻率、元件始終顯示最新可能資料的重要性等。 請注意，快取沒有失效，因此在設定快取持續時間時請小心。

為元件配置快取時，快取名稱必須是您在項目中定義的&#x200B;**proxy**&#x200B;元件的名稱。

在用戶端傳送GraphQL請求之前，會檢查是否已快取相同的&#x200B;**exact** GraphQL請求，並可能傳回快取回應。 為了比對，GraphQL請求必須完全符合，即查詢、操作名稱（如果有）、變數（如果有）必須全部等於快取請求，而且所有可設定的自訂HTTP標題也必須相同。 例如，Magento`Store`標題必須符合。

### 範例

建議您為搜尋服務設定一些快取，以擷取產品搜尋和類別頁面上顯示的所有可用匯總/刻面值。 這些值通常只有在例如產品新增了新屬性時才會變更，因此，如果產品屬性集不經常變更，則此快取項目的持續時間可能會是「大」。 雖然這是專案專用的，但建議在專案開發階段使用幾分鐘，在穩定的生產系統上使用數小時。

這通常會以下列快取項目來設定：

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

建議使用GraphQl快取功能的另一個範例案例是導覽元件，因為它會在所有頁面上傳送相同的GraphQL查詢。 在此情況下，快取項目通常會設為：

```
venia/components/structure/navigation:true:10:600
```

考慮使用[Venia參考儲存區](https://github.com/adobe/aem-cif-guides-venia)時。 請注意，使用元件代理名`venia/components/structure/navigation`，而&#x200B;**不**&#x200B;使用CIF導航元件的名稱(`core/cif/components/structure/navigation/v1/navigation`)。

其他元件的快取應根據專案定義，通常與Dispatcher層級設定的快取協調。 請記住，這些快取沒有任何作用中的失效，因此應謹慎設定快取持續時間。 沒有任何「一刀切」的值能符合所有可能的專案和使用案例。 請務必在專案層級定義最符合專案需求的快取策略。

## Dispatcher快取 {#dispatcher}

快取[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant)中的AEM頁面或片段，是任何AEM專案的最佳作法。 通常會仰賴無效技術，以確保AEM中變更的任何內容都能在Dispatcher中正確更新。 這是AEM Dispatcher快取策略的核心功能。

除了純AEM管理內容CIF外，頁面通常還可顯示透過GraphQL從Magento動態擷取的商務資料。 雖然頁面結構本身可能永遠不會變更，但商務內容可能會變更，例如，如果某些產品資料（例如名稱或價格）在Magento中變更。

為了確保在AEM Dispatcher中快取CIF頁面的時間有限，因此建議在AEM Dispatcher中快取CIF頁面時，使用[時間型快取無效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-time-based-cache-invalidation-enablettl)（也稱為TTL型快取）。 可在AEM中使用額外的[ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)套件來設定此功能。

使用TTL型快取功能，開發人員通常會為選取的AEM頁面定義一或多個快取持續時間。 這可確保在設定的持續時間內，AEM Dispatcher中只會快取CIF頁面，而且內容會經常更新。

>[!NOTE]
>
>雖然AEM Dispatcher可能會快取伺服器端資料，但有些CIF元件（例如`product`、`productlist`和`searchresults`元件）通常會在頁面載入時，在用戶端瀏覽器請求中重新擷取產品價格。 這可確保一律在頁面載入時擷取重要的動態內容。

## 其他資源

- [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQL快取配置](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
