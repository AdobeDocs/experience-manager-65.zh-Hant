---
title: AEM Content and Commerce 2019年發行說明
description: Adobe Experience Manager Content and Commerce發行說明2019年。
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 7%

---

# Commerce Integration Framework GitHub版本總覽

## 發行日期： 2019年11月

| GitHub | 版本 | 詳細的發行說明 |
|:-------|:-----:|---------------------:|
| CIF聯結器 | 0.7.1 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.6.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.6.2 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-november}

* 作者可以在Sites編輯器中使用新的「檢視產品/類別」選項，預覽產品/類別的產品詳細資料和產品清單頁面。

* 作者可以依產品SKU標籤資產，並依SKU搜尋產品專屬資產。

* 新增/移除購物車中新增的優惠券支援。

* AEM Venia商店前方新增Braintree付款支援。

### 功能改善 {#what-is-improved-november}

* 類別/產品選擇器已增強，可在多商店設定中遵循指定的Adobe Commerce商店檢視。

* React型元件可作為npm套件使用。 如此一來，開發人員就能將React元件套件當做新React專案的相依性使用，以便自訂現有元件或開發新的React型元件。

* 簡化GraphQL查詢自訂。 如此一來，開發人員就能使用較少的程式碼自訂CIF核心元件。

## 發行日期： 2019年10月

| GitHub | 版本 | 詳細的發行說明 |
|:-------|:-----:|---------------------:|
| CIF聯結器 | 0.6.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.5.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.5.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-october}

* 產品詳細資料頁面和產品清單頁面的完全可編寫範本。 作者現在可以建立範本，並將產品清單和產品詳細資料元件拖放至這些範本上。 除了新增其他元件外，作者現在也可以變更這些範本的版面，為他們提供無限制的自由，以建立結合行銷和商務內容的令人驚豔體驗。

* 所有對作者友善的CIF核心元件均已增強以支援 [AEM樣式系統](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html?lang=en). 已為產品清單元件提供範例樣式。

* 用於帳戶管理的React型使用者端元件。 此版本支援下列功能：登入、忘記密碼和建立帳戶。

### 功能改善 {#what-is-improved-october}

* 產品詳細資料和產品清單元件已增強，以顯示虛擬資料，以便讓作者在將這些元件放置到範本/頁面時預覽版面。

* Minicart和Checkout元件現在使用React鉤點來改善擴充性。

## 發行日期： 2019年9月

| GitHub | 版本 | 詳細的發行說明 |
|:-------|:-----:|---------------------:|
| CIF聯結器 | 0.5.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.4.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.4.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-september}

* 多範本功能可讓作者擴充特定產品詳細資料頁面或產品清單頁面。 作者可輕鬆建立自訂產品詳細資料頁面或產品清單頁面，並使用產品或類別選擇器將自訂頁面指派給特定產品或類別。

* 多目錄繫結，可讓作者在AEM產品主控台中繫結多個目錄。 作者也可以在建立繫結後，編輯及檢視目錄繫結屬性。

* 使用GraphQL的React型使用者端結帳和迷你購物車可支援完整的基本購物歷程。

* 「結帳」元件包含地址表單、付款選擇和運送方式選擇。

### 功能改善 {#what-is-improved-september}

* 產品Teaser和產品輪播元件支援產品變體。

## 發行日期： 2019年8月

| GitHub | 版本 | 詳細的發行說明 |
|:-------|:-----:|---------------------:|
| CIF聯結器 | 0.4.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.3.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.3.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-august}

* 在CIF原型中內嵌CIF Connector是選用專案，可讓開發人員獲得更多彈性。

* CIF元件與「Venia」特定的CSS樣式脫鉤，讓開發人員可套用他們選擇的CSS樣式。

* 多商店/網站功能，可讓您在多個AEM網站結構上使用CIF核心元件，並讓底層GraphQL使用者端實作連線至不同的Adobe Commerce商店/商店檢視。

* 透過HTTPGET為某些GraphQL查詢啟用GraphQL快取，以減少回應時間。

* 產品說明檢視會在AEM產品主控台中啟用。

* Commerce Teaser擴充WCM Teaser元件，讓作者也能將CTA欄位新增至產品詳細資料頁面或產品清單頁面。

* 按鈕可讓作者放置在AEM頁面上並連結至AEM頁面、產品詳細資料頁面、產品清單頁面或外部連結。

### 功能改善 {#what-is-improved-august}

* Adobe Commerce商店設定已從OSGi移至AEM產品主控台，讓整合設定更方便編寫人員使用。

## 發行日期： 2019年7月

| GitHub | 版本 | 詳細的發行說明 |
|:-------|:-----:|---------------------:|
| CIF聯結器 | 0.3.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.2.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.2.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-july}

* 第一個CIF原型，為開發人員提供數個部署選項： 1.部署AEM Venia店面2. 為新專案部署支架3。 在現有專案中使用CIF元素

* 多階層目錄導覽，可支援類別和子類別的導覽。

* 類別頁面上的分頁以提供更好的UX。

* 使用者端轉譯產品詳細資料和產品清單元件中的價格屬性，以支援轉譯動態屬性。

* 伺服器端產品輪播，以輪播形式顯示精選產品清單。

* 伺服器端精選類別清單，可在AEM頁面上顯示類別清單。

### 功能改善 {#what-is-improved-july}

* 支援Adobe Commerce 2.3.2，以及與產品主控台中顯示的產品屬性相關的錯誤修正。

## 發行日期： 2019年6月

| GitHub | 版本 | 詳細的發行說明 |
|:-------|:-----:|---------------------:|
| CIF聯結器 | 0.2.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.1.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |

### 新增功能 {#what-is-new-june}

* AEM B2C店面具有行動優先的Venia CSS樣式、登陸頁面、透過產品和類別頁面的動態目錄導覽、產品搜尋頁面和購物車功能，以快速啟動和加速商業專案。

* CIF聯結器和撰寫工具（產品主控台、產品選擇器和類別選擇器）可讓作者在AEM中建立具有商務內容的體驗。

* 與Adobe Commerce 2.3.1相容的CIF Core Components第一版：
   * 產品詳細資料
   * 產品清單
   * 產品Teaser
   * 導覽
   * 產品搜尋
   * 購物車(REST)
