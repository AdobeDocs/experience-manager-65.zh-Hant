---
title: 《 AEM 2021年內容與商業發佈說明》
description: 《 AEM 2021年內容與商業發佈說明》
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 7%

---

# Commerce Integration Framework GitHub發佈概述

## 發佈日期：2019年11月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.7.1 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.6.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.6.2 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-november}

* 作者可以在「站點」編輯器中使用新的「查看產品/類別」選項預覽產品詳細資訊和產品清單頁。

* 作者可以按產品SKU標籤資產，並按SKU搜索特定於產品的資產。

* 添加/刪除購物車中添加的優惠券支援。

* Braintree支付支AEM持在Venia商店前面。

### 改進內容 {#what-is-improved-november}

* 類別/產品選擇器在多商店設定中增強，以符合指定的Adobe Commerce商店視圖。

* 基於反應的元件可作為npm包提供。 這允許開發人員將React Components包用作新React項目的依賴項，以允許定制現有元件或開發新的基於React的元件。

* 簡化了GraphQL查詢自定義。 這使開發人員能夠用較少的代碼定制CIF核心元件。

## 發佈日期：2019年10月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.6.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.5.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.5.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-october}

* 產品詳細資訊頁面和產品清單頁面的完全授權模板。 作者現在可以建立新模板，並將產品清單和產品詳細資訊元件拖放到這些模板上。 除了添加其他元件外，作者現在還可以更改這些模板的佈局，使它們可以無限自由地創造結合營銷和商業內容的驚人體驗。

* 所有對作者友好的CIF核心元件都得到加強，以支援 [樣AEM式系統](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html)。 為產品清單元件提供了示例樣式。

* 基於反應的客戶端元件，用於客戶管理。 此版本支援以下功能：登錄、忘記密碼和建立帳戶。

### 改進內容 {#what-is-improved-october}

* 產品詳細資訊和產品清單元件已得到增強，以顯示虛擬資料，以便在將這些元件放在模板/頁面上時為作者提供佈局的預覽。

* Minicart和Checkout元件現在使用React掛接來改進擴展性。

## 發佈日期：2019年9月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.5.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.4.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.4.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-september}

* 多模板功能，允許作者豐富特定產品詳細資訊頁面或產品清單頁面。 作者可以輕鬆建立定制產品詳細資訊頁面或產品清單頁面，並使用產品或類別選擇器將定制頁面分配給特定產品或類別。

* 多目錄綁定，允許作者在產品控制台中綁AEM定多個目錄。 建立綁定後，作者還可以編輯和查看目錄綁定屬性。

* 使用GraphQL的基於React的客戶端結帳和Mini Cart支援完整的基本購物之旅。

* 結帳元件包括地址表單、付款選擇和發運方法選擇。

### 改進內容 {#what-is-improved-september}

* 產品預告和產品旋轉傳送器元件支援產品變型。

## 發佈日期：2019年8月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.4.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.3.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.3.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-august}

* 將CIF連接器嵌入CIF原型中使開發人員具有更大的靈活性。

* CIF元件與「Venia」特定的CSS樣式相分離，使開發人員能夠應用他們選擇的CSS樣式。

* 多儲存/站點功能，允許在多個站點結構上使用CIF核心元件AEM，並使基礎GraphQL客戶端實現能夠連接到Adobe Commerce不同的儲存/儲存視圖。

* 通過HTTPGET為某些GraphQL查詢啟用GraphQL快取，以縮短響應時間。

* 在「產品」控制台中啟AEM用產品說明視圖。

* Commerce Teaser擴展了WCM Teaser元件，允許作者還將CTA欄位添加到產品詳細資訊頁面或產品清單頁面。

* 用於允許作者將其放置在AEM頁面上並連結到AEM頁面、產品詳細資訊頁面、產品清單頁面或外部連結的按鈕。

### 改進內容 {#what-is-improved-august}

* Adobe Commerce商店配置從OSGi移AEM到Product控制台，以使整合設定更便於作者使用。

## 發佈日期：2019年7月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.3.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.2.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.2.0 | [發行說明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-july}

* 第一個CIF原型，為開發人員提供多種部署選項：1.部署AEMVenia店面2。 為新項目3部署腳手架。 在現有項目中使用CIF元素

* 多級目錄導航，支援通過類別和子類別進行導航。

* 類別頁上的分頁，以獲得更好的UX。

* 在「產品詳細資訊」和「產品清單」元件中對價格屬性進行客戶端呈現，以支援動態屬性的呈現。

* 伺服器端產品傳送帶以傳送帶樣式顯示特色產品清單。

* 伺服器端特色類別清單顯示頁面上的類別AEM清單。

### 改進內容 {#what-is-improved-july}

* 產品控制台中顯示對Adobe Commerce2.3.2和與產品屬性相關的錯誤修復的支援。

## 發佈日期：2019年6月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 0.2.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 0.1.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |

### 新增功能 {#what-is-new-june}

* AEM B2C店面具有移動首發Venia CSS樣式、登錄頁、通過產品和類別頁進行動態目錄導航、產品搜索頁和購物車功能，以啟動和加速商業項目。

* CIF連接器和創作工具（產品控制台、產品選取器和類別選取器），使作者能夠建立商業內AEM容的體驗。

* 與Adobe Commerce2.3.1相容的CIF核心元件第一版：
   * 產品詳細資訊
   * 產品清單
   * 產品預告
   * 導覽
   * 產品搜索
   * 購物車(REST)
