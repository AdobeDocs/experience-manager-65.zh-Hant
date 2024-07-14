---
title: 快取與效能
description: 瞭解各種可用設定，以啟用GraphQL和內容快取，將您的Commerce實作效能最佳化。
exl-id: ecce64bf-5960-4ddb-b6e3-dad401038c11
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---

# 快取與效能 {#caching}

## 元件和GraphQL回應快取 {#graphql}

AEM CIF核心元件已內建對快取個別元件的GraphQL回應的支援。 此功能可用來大幅減少GraphQL後端呼叫的數量。 尤其對於重複查詢，例如擷取導覽元件的類別樹狀結構，或擷取產品搜尋和類別頁面上顯示的所有可用彙總/多面向值，可以實現有效的快取。

對於AEM CIF核心元件，快取是根據元件來設定，因此能夠控制是否對每個元件快取GraphQL請求/回應（以及快取的時長）。 您也可以使用GraphQL使用者端定義OSGi服務的快取行為。

### 設定

針對指定元件進行設定後，快取會開始儲存由每個快取設定專案定義的GraphQL查詢和回應。 快取的大小和每個專案的快取期間會根據專案來定義，例如根據目錄資料可能變更的頻率、元件一律顯示最新可能資料的重要程度等等。 請注意，沒有任何快取失效，因此在設定快取期間時請小心。

設定元件的快取時，快取名稱必須是您在專案中定義的&#x200B;**proxy**&#x200B;元件的名稱。

在使用者端傳送GraphQL要求之前，它會檢查是否已快取&#x200B;**完全**&#x200B;相同的GraphQL要求，並可能傳回快取的回應。 為了相符，GraphQL請求必須完全相符，也就是說，查詢、操作名稱（如果有的話）、變數（如果有的話）都必須等於快取請求，而且可能設定的所有自訂HTTP標頭也必須相同。 例如，Adobe Commerce `Store`標頭必須相符。

### 範例

我們建議您為搜尋服務設定一些快取，以便擷取產品搜尋和類別頁面上顯示的所有可用彙總/多面向值。 這些值通常只有在新屬性（例如，新增至產品）時才會變更，因此，如果產品屬性集合不經常變更，則此快取專案的持續時間可能會「很大」。 雖然這是專案專屬的值，但Adobe建議在專案開發階段使用幾分鐘的值，並在穩定生產系統上使用幾小時。

這通常會使用下列快取專案進行設定：

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

另一個建議使用GraphQl快取功能的範例案例是導覽元件，因為它會在所有頁面上傳送相同的GraphQL查詢。 在這種情況下，快取專案通常會設為：

```
venia/components/structure/navigation:true:10:600
```

在考慮[Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)時。 請注意，使用了元件Proxy名稱`venia/components/structure/navigation`，而&#x200B;**不是** CIF導覽元件名稱(`core/cif/components/structure/navigation/v1/navigation`)。

其他元件的快取應根據專案來定義，通常與在Dispatcher層級設定的快取協調定義。 請記住，這些快取沒有任何作用中的失效機制，因此應謹慎設定快取持續時間。 沒有任何「適合所有」的值會符合所有可能的專案和使用案例。 請務必在專案層級定義最符合專案需求的快取策略。

## Dispatcher快取 {#dispatcher}

在[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)中快取AEM頁面或片段是任何AEM專案的最佳作法。 通常，它仰賴失效技術，以確保在AEM中變更的任何內容在Dispatcher中正確更新。 這是AEM Dispatcher快取策略的核心功能。

除了純AEM受管內容CIF之外，頁面通常還可以顯示透過GraphQL從Adobe Commerce動態擷取的商務資料。 雖然頁面結構本身可能不會變更，但如果部分產品資料（例如名稱或價格）在Adobe Commerce中有所變更，商業內容可能會有所不同。

為了確保CIF頁面可以在AEM Dispatcher中快取有限的時間，因此我們建議在AEM Dispatcher中快取CIF頁面時使用[時間型快取失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) （也稱為TTL型快取）。 此功能可在AEM中使用額外的[ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)套件進行設定。

使用TTL型快取時，開發人員通常會為選取的AEM頁面定義一或多個快取持續時間。 這可確保在AEM Dispatcher中快取CIF頁面，直到設定的持續時間為止，並且內容將經常更新。

>[!NOTE]
>
>雖然AEM Dispatcher可能會快取伺服器端資料，但某些CIF元件（如`product`、`productlist`和`searchresults`元件）通常會在頁面載入時，在使用者端瀏覽器請求中重新擷取產品價格。 這可確保在頁面載入時一律會擷取重要的動態內容。

## 其他資源

- [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQL快取設定](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
