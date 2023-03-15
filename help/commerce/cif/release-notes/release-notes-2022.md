---
title: AEM內容與商務發行說明2022年
description: AEM內容與商務發行說明2022年
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 0fdff88695646603cec120d25f156f8c918686df
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 7%

---

# 商務整合架構GitHub發行概述

## 系統需求概述

請參閱下表中您目前使用或計畫未來使用的CIF版本的最低系統需求。

| Component | 系統需求 |
|:-------|:-----:|
| CIF附加元件 | 最低：AEM 6.5.7、Magento2.3.5 GraphQL結構 |
| CIF核心元件 | [系統需求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 專案原型 | [系統需求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 發行日期：2022年9月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.09.20.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.09.20.00.zip) |
| CIF核心元件 | 2.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.11.0) |
| CIF Venia參考站 | 2022.09.02 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.09.02) |

### 新增功能 {#what-is-new-september}

* 作者可以使用體驗片段來動態豐富產品清單(範例：在產品清單之間放置橫幅)
* 清單元件支援相關產品/類別頁面，以動態顯示相關頁面
* 支援Peregrine 12.5元件
* 支援產品預告和輪播中的用戶端價格載入

## 發行日期：2022年7月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.08.02.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### 新增功能 {#what-is-new-july}

* 透過AEM頁面屬性將AEM頁面與產品和類別關聯，並在產品座艙中提供概覽
   ![產品座艙頁面關聯](/help/assets/CIF/product_cockpit_page_association.png)

## 發行日期：2022年6月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.07.05.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| CIF核心元件 | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| CIF Venia參考站 | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### 新增功能 {#what-is-new-june}

* 產品目錄擴充現在支援AEM頁面。 這可讓作者管理頁面 — 產品關聯。

* 各種CIF核心元件改良

### 錯誤修正 {#bug-fixes-june}

* 將登入代號新增至用戶端取價

* 資料層中的頁面元件錯誤

## 發行日期：2022年5月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.05.31.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| CIF核心元件 | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| CIF Venia參考站 | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### 新增功能 {#what-is-new-may}

* 新產品座艙屬性頁面，提供更佳和簡化的概觀

![產品座艙屬性概述](/help/assets/CIF/product_cockpit_properties_overview.png)

* 改善I/O Runtime上第三方連接器的相容性和健全性

* 改善對GQL客戶端配置覆蓋的支援（例如設定自定義快取行為）

### 錯誤修正 {#bug-fixes-may}

* 多值產品選擇器欄位將第2個和其他產品顯示為無效

* 產品選擇器偶爾會隱藏在元件後面

## 發行日期：2022年4月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.04.28.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| CIF核心元件 | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| CIF Venia參考站 | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### 新增功能 {#what-is-new-april}

* 快速訪問產品座艙：在Sites Editor中按一下即可輕鬆存取完整的詳細產品資訊

   ![啟用願望清單](/help/assets/CIF/enable-wishlist.png)

* 支援其他行銷商務元件：元件可設定為顯示附加至購物車和附加至願望清單呼叫動作

   ![Sites編輯器快速鍵至產品座艙](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## 發行日期：2022年2月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.02.24.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF核心元件 | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venia參考站 | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### 新增功能 {#what-is-new-march}

* 測試版：AEM CIF搜尋核心元件支援Commerce LiveSearch
* 改善多商店案例的SEO:現在可透過CIF雲端設定屬性，在商店層級設定PDP/PLP的URL格式
* 產品選擇器透過UI中的新篩選器選項支援分段產品。  這可讓內容從業人員為即將推出的產品做準備產品內容管理
* 使用CIF雲端設定名稱（而非設定代理url）簡化CIF設定管理和錯誤處理
* 手動選擇產品清單和輪播元件的類別。 這可讓內容從業人員在目錄體驗之外的內容頁面上使用這些元件

## 發行日期：2022年1月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.01.20.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF核心元件 | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venia參考站 | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### 新增功能 {#what-is-new-january}

* 增強的myAccount元件
* 產品建議元件支援其他頁面類型（首頁、購物車、訂單確認）
* **希望清單**
   * 登入的訪客可將產品新增至願望清單
   * 可通過myAccount管理願望清單及其產品
   * 可以通過策略（例如產品預告、產品詳細資訊）在元件級別上啟用/禁用「添加到願望清單」按鈕
   * 以核心元件形式提供，並可在AEM Venia Storefront中使用

![希望清單](/help/assets/CIF/wishlist.png)
