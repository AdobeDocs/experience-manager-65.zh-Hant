---
title: AEM內容與商務發行說明2021年
description: AEM內容與商務發行說明2021年
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 7%

---

# 商務整合架構GitHub發行概述

## 發行日期：2019年11月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.7.1 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.6.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.6.2 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-november}

* 作者可以在Sites編輯器中使用新的「檢視產品/類別」選項，預覽產品詳細資訊和產品清單頁面及產品/類別。

* 作者可依產品SKU標籤資產，並依SKU搜尋產品專屬資產。

* 新增/移除購物車中新增的抵用券支援。

* Braintree支援已新增至AEM Venia商店前端。

### 改進項目 {#what-is-improved-november}

* 在多商店設定中，類別/產品選擇器已針對指定的Adobe Commerce商店檢視而增強。

* 以npm套件形式提供的React型元件。 這可讓開發人員使用React元件套件作為新React專案的相依性，以自訂現有元件或開發新的React型元件。

* GraphQL查詢自訂已簡化。 這可讓開發人員以更少的程式碼來自訂CIF核心元件。

## 發行日期：2019年10月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.6.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.5.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.5.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-october}

* 產品詳細資料頁面和產品清單頁面的完全可授權範本。 作者現在可以建立新範本，並將產品清單和產品詳細資料元件拖放到這些範本上。 除了新增其他元件外，作者現在也可以變更這些範本的版面，讓他們無限自由建立結合行銷和商務內容的絕佳體驗。

* 所有方便撰寫的CIF核心元件均已增強，可支援 [AEM樣式系統](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html). 已提供產品清單元件的範例樣式。

* 用於帳戶管理的React式用戶端元件。 此版本支援下列功能：登入、忘記密碼和建立帳戶。

### 改進項目 {#what-is-improved-october}

* 產品詳細資料和產品清單元件已經過增強，可顯示虛擬資料，以便在這些元件放置於範本/頁面時，為作者提供版面的預覽。

* 迷你圖和結帳元件現在使用React鈎點來提升擴充性。

## 發行日期：2019年9月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.5.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.4.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.4.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-september}

* 多範本功能，可讓作者擴充特定產品詳細資料頁面或產品清單頁面。 作者可輕鬆建立自訂產品詳細資料頁面或產品清單頁面，並使用產品或類別選擇器，將自訂頁面指派給特定產品或類別。

* 多目錄系結，可讓作者在AEM產品主控台中系結多個目錄。 建立綁定後，作者還可以編輯和查看目錄綁定屬性。

* 使用GraphQL的React式用戶端結帳和Mini Cart支援完整的基本購物歷程。

* 結帳元件包括地址表單、付款選擇和運送方法選擇。

### 改進項目 {#what-is-improved-september}

* 產品預告和產品轉盤元件支援產品變體。

## 發行日期：2019年8月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.4.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.3.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.3.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-august}

* 將CIF連接器內嵌於CIF原型中，為開發人員提供更大的彈性。

* CIF元件與「Venia」特定CSS樣式脫鈎，讓開發人員可套用其所選擇的CSS樣式。

* 多存放區/網站功能，可在多個AEM網站結構上使用CIF核心元件，並讓基礎的GraphQL用戶端實作可連線至不同的Adobe Commerce存放區/存放區檢視。

* GraphQL快取已透過HTTPGET啟用某些GraphQL查詢，以縮短回應時間。

* 在AEM產品控制台中啟用產品說明檢視。

* Commerce Teaser延伸了WCM Teaser元件，讓作者也可將CTA欄位新增至產品詳細資料頁面或產品清單頁面。

* 可讓作者放置在AEM頁面上，並連結至AEM頁面、產品詳細資料頁面、產品清單頁面或外部連結的按鈕。

### 改進項目 {#what-is-improved-august}

* Adobe Commerce存放區設定從OSGi移至AEM產品主控台，讓整合設定更適合作者使用。

## 發行日期：2019年7月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.3.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.2.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.2.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-july}

* 第一個CIF原型，可為開發人員提供數種部署選項：1.部署AEM Venia storefront 2. 為新專案3部署支架。 在現有專案中使用CIF元素

* 多層級目錄導覽，以支援在類別和子類別中導覽。

* 類別頁面上的分頁，以獲得更好的UX。

* 在產品詳細資料和產品清單元件中的用戶端價格屬性轉譯，以支援動態屬性轉譯。

* 伺服器端產品轉盤，以轉盤樣式顯示精選產品清單。

* 伺服器端精選類別清單，以顯示AEM頁面上的類別清單。

### 改進項目 {#what-is-improved-july}

* 產品主控台中會顯示支援Adobe Commerce 2.3.2及產品屬性相關錯誤修正。

## 發行日期：2019年6月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.2.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.1.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |

### 新增功能 {#what-is-new-june}

* AEM B2C店面，具有行動優先的Venia CSS樣式、登陸頁面、透過產品和類別頁面導覽的動態目錄、產品搜尋頁面，以及購物車功能，以啟動和加速商務專案。

* CIF Connector和製作工具（產品控制台、產品選擇器和類別選擇器）可讓作者在AEM中建立具有商務內容的體驗。

* 與Adobe Commerce 2.3.1相容的CIF核心元件第一版：
   * 產品詳細資料
   * 產品清單
   * Product Teaser
   * 導覽
   * 產品搜尋
   * 購物車(REST)
