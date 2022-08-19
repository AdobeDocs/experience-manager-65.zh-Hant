---
title: 《 AEM 2022年內容與商業發佈說明》
description: 《 AEM 2022年內容與商業發佈說明》
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 6c5c37c1c365e1f03ea9b5c935adf63a33faba5d
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 7%

---

# Commerce Integration Framework GitHub發佈概述

## 系統要求概述

查看下表中您當前使用或計畫將來使用的CIF版本的最低系統要求。

| Component | 系統要求 |
|:-------|:-----:|
| CIF附加 | 最小：AEM 6.5.7 、Magento2.3.5 GraphQL架構 |
| CIF核心元件 | [系統要求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 專案原型 | [系統要求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 發佈日期：2022年7月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2022.08.02.00 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### 新增功能 {#what-is-new-july}

* 通過頁AEM面屬性以及產品座艙中的AEM概述將頁面與產品和類別關聯
   ![產品駕駛艙頁面關聯](/help/assets/CIF/product_cockpit_page_association.png)

## 發佈日期：2022年6月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2022.07.05.00 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| CIF核心元件 | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| CIF Venia參考站點 | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### 新增功能 {#what-is-new-june}

* 產品目錄豐富現在支援AEM頁面。 這使作者能夠管理頁面 — 產品關聯。

* 各種CIF核心元件改進

### 錯誤修正 {#bug-fixes-june}

* 將登錄令牌添加到客戶端價格提取

* 資料層中的頁元件錯誤

## 發佈日期：2022年5月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2022.05.31.00 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| CIF核心元件 | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| CIF Venia參考站點 | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### 新增功能 {#what-is-new-may}

* 新產品座艙屬性頁面，以便更好、更簡化的概述

![產品座艙屬性概述](/help/assets/CIF/product_cockpit_properties_overview.png)

* I/O運行時上第三方連接器的相容性和健壯性得到提高

* 改進對GQL客戶端配置覆蓋的支援（例如設定自定義快取行為）

### 錯誤修正 {#bug-fixes-may}

* 多值產品選取器欄位顯示第二個和其他產品無效

* 產品選取器偶爾隱藏在元件後面

## 發佈日期：2022年4月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2022.04.28.00 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| CIF核心元件 | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| CIF Venia參考站點 | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### 新增功能 {#what-is-new-april}

* 快速訪問產品駕駛艙：在站點編輯器中按一下一次即可輕鬆訪問完整的詳細產品資訊

   ![啟用願望清單](/help/assets/CIF/enable-wishlist.png)

* 支援其他營銷商務元件：可將元件配置為顯示附加購物車和附加清單的行動要求

   ![產品駕駛艙的站點編輯器快捷方式](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## 發佈日期：2022年2月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2022.02.24.00 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF核心元件 | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venia參考站點 | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### 新增功能 {#what-is-new-march}

* Beta:CIF搜AEM索核心元件支援Commerce LiveSearch
* 針對多儲存方案改進SEO:現在，可以通過CIF雲配置屬性在儲存級別上配置PDP/PLP的URL格式
* 產品選取器通過UI中的新篩選器選項支援分階段產品。  這使內容從業人員能夠為即將推出的產品準備產品內容管理
* 使用CIF雲配置名稱（而不是配置代理url）簡化CIF配置管理和錯誤處理
* 產品清單和旋轉傳送元件的手動類別選擇。 這允許內容從業人員在目錄體驗之外的內容頁面上使用這些元件

## 發佈日期：2022年1月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2022.01.20.00 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF核心元件 | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venia參考站點 | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### 新增功能 {#what-is-new-january}

* 增強的myAccount元件
* 產品建議元件支援其他頁面類型（首頁、購物車、訂單確認）
* **希望清單**
   * 已登錄的訪問者可以將產品添加到願望清單
   * 通過myAccount管理願望清單及其產品是可能的
   * 可以通過策略在元件級別上啟用/禁用「添加到願望清單」按鈕（例如，產品預告、產品詳細資訊）
   * 可作為核心元件在Venia StorefrontAEM中使用

![希望清單](/help/assets/CIF/wishlist.png)
