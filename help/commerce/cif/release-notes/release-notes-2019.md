---
title: 2021AEM年內容與商務發行說明
description: 2021AEM年內容與商務發行說明
translation-type: tm+mt
source-git-commit: c2fb9af056fa4be13cfd7e60e8a44485e8712c0b
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 8%

---

# 商務整合架構GitHub發行概觀

## 發行日期：2019年11月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.7.1 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.6.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.6.2 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新功能 {#what-is-new-november}

* 作者可以在「網站」編輯器中使用新的「檢視產品／類別」選項，預覽包含產品／類別的產品詳細資訊和產品清單頁面。

* 作者可依產品SKU來標籤資產，並依SKU來搜尋產品特定資產。

* 新增／移除購物車中新增的抵用券支援。

* Braintree支付支AEM援在Venia商店前面。

### 功能改善 {#what-is-improved-november}

* 類別／產品挑選器已增強，可在多商店設定中依照指定的Magento商店檢視。

* 以NPM套件形式提供的反應型元件。 這可讓開發人員將React Components套件當成對新React專案的依賴，以允許自訂現有元件或開發新的React架構元件。

* GraphQL查詢自訂已簡化。 這可讓開發人員以較少的程式碼來自訂CIF核心元件。

## 發行日期：2019年10月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.6.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.5.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.5.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新功能 {#what-is-new-october}

* 產品詳細資訊頁面和產品清單頁面的完全可授權範本。 作者現在可以建立新範本，並在這些範本上拖放產品清單和產品詳細資訊元件。 除了新增其他元件外，作者現在也可以變更這些範本的版面配置，讓他們無限自由地建立結合行銷和商務內容的絕佳體驗。

* 所有對作者友好的CIF核心元件都已增強，支援[AEM Style System](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html)。 產品清單元件已提供範例樣式。

* 以客戶端元件為主的反應式客戶端元件，以進行帳戶管理。 本版本支援下列功能：登入、忘記密碼及建立帳戶。

### 功能改善 {#what-is-improved-october}

* 產品詳細資訊和產品清單元件已增強，可顯示虛擬資料，讓作者在將這些元件置於範本／頁面時，預覽版面配置。

* Minicart和Checkout元件現在使用React勾點來改善擴充性。

## 發行日期：2019年9月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.5.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.4.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.4.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新功能 {#what-is-new-september}

* 多範本功能，可讓作者豐富特定產品詳細資訊頁面或產品清單頁面。 作者可以輕鬆建立自訂產品詳細資訊頁面或產品清單頁面，並使用產品或類別選擇器將自訂頁面指派給特定產品或類別。

* 多目錄系結可讓作者在產品主控台中系結AEM多個目錄。 作者也可以在建立系結後編輯和檢視目錄系結屬性。

* 使用GraphQL以回應式用戶端結帳和Mini Cart，以支援完整的基本購物歷程。

* 結帳元件包括地址表單、付款選擇和送貨方法選擇。

### 功能改善 {#what-is-improved-september}

* 產品摘要和產品轉盤元件支援產品變體。

## 發行日期：2019年8月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.4.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.3.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.3.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新功能 {#what-is-new-august}

* 將CIF連接器嵌入CIF Archetype中是可選的，為開發人員提供更大的靈活性。

* CIF元件與「Venia」特定CSS樣式解耦，讓開發人員可套用自選的CSS樣式。

* 多儲存／站點功能允許在多個站點結構上使用CIF核心組AEM件，並使底層GraphQL客戶端實現能夠連接到不同的Magento儲存／儲存視圖。

* 通過HTTPGET為某些GraphQL查詢啟用GraphQL快取，以縮短響應時間。

* 產品說明檢視在產品主控台AEM中啟用。

* Commerce Teaser擴充了WCM Teaser元件，讓作者也能將CTA欄位新增至產品詳細資訊頁面或產品清單頁面。

* 「按鈕」，可讓作者放AEM置在頁面上，並連結至AEM頁面、產品詳細資訊頁面、產品清單頁面或外部連結。

### 功能改善 {#what-is-improved-august}

* Magento商店設定從OSGi移AEM至產品主控台，讓整合設定更方便使用者。

## 發行日期：2019年7月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.3.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.2.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.2.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新功能 {#what-is-new-july}

* First CIF Archetype，為開發人員提供多種部署選項：1.部署AEMVenia店面2。 為新專案3部署腳手架。 在現有專案中使用CIF元素

* 多層級型錄導覽，以支援在類別和子類別中導覽。

* 類別頁面上的分頁功能，以獲得更佳的UX。

* 在「產品詳細資訊」和「產品清單」元件中，用戶端呈現價格屬性，以支援動態屬性的呈現。

* 伺服器端產品轉盤，以轉盤樣式顯示精選產品的清單。

* 伺服器端功能類別清單，以顯示頁面上的類別AEM清單。

### 功能改善 {#what-is-improved-july}

* 產品主控台中會顯示與產品屬性相關的Magento2.3.2和錯誤修正支援。

## 發行日期：2019年6月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.2.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.1.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |

### 新功能 {#what-is-new-june}

* AEM B2C店面，提供行動優先的Venia CSS樣式、登陸頁面、透過產品和類別頁面的動態型錄導覽、產品搜尋頁面和購物車功能，以啟動並加速商務專案。

* CIF連接器和製作工具（產品主控台、產品選擇器和類別選擇器），讓作者建立商務內容AEM的體驗。

* CIF核心元件第一版與2.3.1Magento相容：
   * 產品詳細資訊
   * 產品清單
   * 產品摘要
   * 導覽
   * 產品搜尋
   * 購物車(REST)

