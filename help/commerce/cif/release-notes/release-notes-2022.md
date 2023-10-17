---
title: AEM Content and Commerce 2022年發行說明
description: Adobe Experience Manager Content and Commerce 2022年發行說明。
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 9%

---

# Commerce Integration Framework GitHub版本總覽

## 系統需求概觀

請檢閱下表中，您目前使用或計畫未來使用的CIF版本的最低系統需求。

| 元件 | 系統需求 |
|:-------|:-----:|
| CIF附加元件 | 最低： AEM 6.5.7、Adobe Commerce 2.3.5 GraphQL結構描述 |
| CIF核心元件 | [系統需求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 專案原型 | [系統需求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 發行日期： 2022年9月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.09.20.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.09.20.00.zip) |
| CIF核心元件 | 2.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.11.0) |
| CIF Venia參考網站 | 2022.09.02 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.09.02) |

### 新增功能 {#what-is-new-september}

* 作者可以使用體驗片段以動態方式豐富產品清單（例如：在產品清單之間放置橫幅）
* 清單元件支援相關聯的產品/類別頁面以動態顯示相關頁面
* 支援Peregrine 12.5元件
* 支援在產品Teaser和輪播中載入使用者端價格

## 發行日期： 2022年7月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.08.02.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### 新增功能 {#what-is-new-july}

* 透過AEM頁面屬性以及產品主控室中的概觀，將AEM頁面與產品和類別相關聯
  ![產品駕駛艙頁面關聯](/help/assets/CIF/product_cockpit_page_association.png)

## 發行日期： 2022年6月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.07.05.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| CIF核心元件 | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| CIF Venia參考網站 | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### 新增功能 {#what-is-new-june}

* 產品目錄擴充現在支援AEM頁面，讓作者可管理頁面 — 產品關聯。

* 各種CIF核心元件改善專案

### 錯誤修正 {#bug-fixes-june}

* 新增登入權杖至使用者端價格擷取

* 資料層中的頁面元件錯誤。

## 發行日期： 2022年5月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.05.31.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| CIF核心元件 | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| CIF Venia參考網站 | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### 新增功能 {#what-is-new-may}

* 新產品駕駛艙屬性頁面，提供更好、更簡化的概覽

![產品駕駛艙屬性概觀](/help/assets/CIF/product_cockpit_properties_overview.png)

* 改善I/O Runtime上協力廠商聯結器的相容性和健全性

* 改善對GQL使用者端設定覆寫的支援（例如，設定自訂快取行為）

### 錯誤修正 {#bug-fixes-may}

* 多值產品選取器欄位會將第二個和其他產品顯示為無效

* 產品選取器偶爾會隱藏在元件後面

## 發行日期： 2022年4月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.04.28.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| CIF核心元件 | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| CIF Venia參考網站 | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### 新增功能 {#what-is-new-april}

* 快速存取產品駕駛艙：在網站編輯器中按一下滑鼠，即可輕鬆存取完整詳細的產品資訊

  ![啟用願望清單](/help/assets/CIF/enable-wishlist.png)

* 支援其他行銷商務元件：元件可設定為顯示加入購物車和加入願望清單的號召性用語

  ![網站編輯器到產品駕駛艙的捷徑](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## 發行日期： 2022年2月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.02.24.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF核心元件 | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venia參考網站 | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### 新增功能 {#what-is-new-march}

* Beta： AEM CIF搜尋核心元件支援Commerce LiveSearch
* 改進多儲存場景的SEO：現在可以透過CIF雲端設定屬性在儲存層級上設定PDP/PLP的URL格式
* 產品選取器透過使用者介面中的新篩選器選項支援分階段產品。 讓內容從業人員為即將推出的產品準備產品內容管理
* 使用CIF Cloud Config名稱（而不是config proxy url）簡化CIF設定管理和錯誤處理
* 產品清單和轉盤元件的手動類別選擇。 允許內容從業人員在目錄體驗之外的內容頁面上使用這些元件

## 發行日期： 2022年1月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2022.01.20.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF核心元件 | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venia參考網站 | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### 新增功能 {#what-is-new-january}

* 增強的myAccount元件
* 產品推薦元件支援其他頁面型別（首頁、購物車、訂單確認）
* **希望清單**
   * 登入的訪客可將產品新增至願望清單
   * 您可以透過myAccount管理願望清單及其產品
   * 可以透過原則（例如產品Teaser、產品詳細資訊）在元件層級上啟用/停用「新增到願望清單」按鈕
   * 可作為核心元件使用，並可在AEM Venia Storefront中使用

![希望清單](/help/assets/CIF/wishlist.png)
