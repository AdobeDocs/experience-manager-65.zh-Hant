---
title: 產品座艙
description: 使用產品座艙
source-git-commit: f3e286c7b5404812655f3b257de17be7bfde7487
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# 產品座艙 {#product-cockpit}

## 概覽 {#overview}

「產品座艙」提供連結產品目錄和相關內容的統一概述。 所有相關內容都具有連結，可快速從駕駛艙訪問。

分階段產品資料包括未來的任何變異，如新類別、產品或更新的屬性。

>[!NOTE]
>
>術語產品目錄可與商店、商店視圖和類似表達式互換。

## 設定 {#configuration}

產品目錄需要在中配AEM置。 請參閱 [配置儲存和目錄](/help/commerce/cif/getting-started.md#catalog) 的子菜單。

啟用分段目錄功能需要身份驗證。 請參閱 [入門](/help/commerce/cif/getting-started.md) 的子菜單。

>[!NOTE]
>
>分段目錄功能僅適用於支援基於令牌的身份驗證的Adobe Commerce和第三方連接器。

## 開啟產品座艙 {#opening-product-cockpit}

訪問「產品座艙」的最簡單方法是通過主菜單中的「商AEM業」菜單。 也可以使用Omnisearch（搜索Commerce）或開啟 `https://<yourAEMInstance>/commerce.html`。

![AEM菜單](/help/commerce/cif/assets/aem-menu.png)

## 瀏覽產品目錄 {#browsing-product-catalogs}

「產品座艙」按照產品目錄結構以分層方式組織。 第一級顯示所有已配置產品目錄的目錄根級別，包括商業後端的元資訊。

![配置的目錄](/help/commerce/cif/assets/catalog-overview.png)

按一下某個類別將載入已按一下類別的子項。

![類別子項](/help/commerce/cif/assets/catalog-category-children.png)

按一下產品將載入產品變體（如果可用）。

![產品變體](/help/commerce/cif/assets/catalog-product-variation.png)

>[!NOTE]
>
>中的產品目AEM錄資料是通過配置的商業端點即時檢索的資料。 沒有儲存產品目錄數AEM據。

## 搜索產品目錄 {#searching-product-catalog}

在左側的過濾器頁籤中提供對產品目錄的全文搜索，以快速查找產品。

![搜尋](/help/commerce/cif/assets/search-cockpit.png)

## 瀏覽分階段產品目錄 {#staged-product-catalogs}

預設情況下，產品座艙顯示即時產品目錄資料。 使用左側篩選器頁籤中的「STACED CATALOG」將載入任何選定日期的產品目錄。

![暫存目錄](/help/commerce/cif/assets/staged-cockpit.png)

## 產品目錄屬性 {#catalog-properties}

按一下產品或類別的屬性表徵圖將開啟所選對象的屬性視圖。 產品變型的開啟屬性等於開啟主要產品屬性。

### 商業頁籤 {#tabs}

常規和變型頁籤顯示來自商業後端的預定義商業屬性。 此資料(包括 變型)是只讀資料，AEM因為記錄系統是商務後端。 變型頁籤僅出現在具有變型的產品中，並顯示所有變型的清單。

![目錄屬性](/help/commerce/cif/assets/catalog-properties.png)

### 內AEM容頁籤 {#content-tabs}

這些頁籤按AEM內容類型（「體驗片段」、「內容片段」、「關聯資產」）分組，AEM顯示與商業對象關聯的內容。 操作「查看詳細資訊」會開啟一個新瀏覽器頁籤，其中包含選定的內容。

![內容屬性](/help/commerce/cif/assets/content-properties.png)
