---
title: AEM內容與商務發行說明2021年
description: AEM內容與商務發行說明2021年
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: 71782a3caae3f74a4886c52cf9b29f9e998913fa
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 8%

---

# 商務整合架構GitHub發行概述

## 系統需求概述

請參閱下表中您目前使用或計畫未來使用的CIF版本的最低系統需求。

**在4月的版本中，我們以[Adobe軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上提供的CIF附加元件取代了GitHub的CIF連接器。 切換至附加元件可為專案帶來絕佳優勢：

* AEM 6.5將立即提供大部分新功能（不再等待功能端埠）
* 易於升級到新的附加版本
* 準備Cloud Service

舊版AEM CIF連接器將進入維護模式，不應再使用。 請將CIF連接器更換為新的CIF附加元件。 大多數項目都應該可以簡單地更換套件。 **

| 元件 | 系統需求 |
|:-------|:-----:|
| CIF附加元件 | 最低：AEM 6.5.7、Magento2.3.5 GraphQL結構 |
| CIF核心元件 | [系統需求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 專案原型 | [系統需求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 發行日期：2021年6月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.06.18 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIF核心元件 | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Venia參考站 | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### 新增功能 {#what-is-new-june}

* 內容片段的新CIF產品和類別參考資料類型(包括 產品/類別選擇器UI支援)
* 新商務內容片段核心元件
* AEM後端支援的全文商務搜尋
* 商務核心元件支援Adobe商務Sensei Recs資料收集
* 改善類別頁面的SEO易記URL
* 支援每個網站/設定的自訂HTTP標題

## 發行日期：2021年5月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.05.26 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIF核心元件 | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Venia參考站 | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### 新增功能 {#what-is-new-may}

* 產品控制台屬性中關聯內容的分頁支援

### 錯誤修正 {#bug-fixes-may}

* 產品屬性的「資產」索引標籤中未顯示資產縮圖

* 階層連結會重設產品主控台中的預覽資料

## 發行日期：2021年4月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.04.22 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF核心元件 | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考站 | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-april}

* 支援類別UID — 如此可為使用類別ID字串的系統解除鎖定第三方商務整合

* AEM的PWA Studio擴充功能，包括 範例整合

* 擴展WCM導覽核心元件的全新CIF導覽核心元件

* AEM店面中分段目錄資料的視覺指示器

### 錯誤修正 {#bug-fixes-april}

* 根類別欄位沒有顯示在類別頁面的頁面屬性中的商務標籤下

## 發行日期：2021年3月 {#what-is-new-march}

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 1.9.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 1.9.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考站 | 2021.03.25 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新功能

* 支援Magento2.4.2

### 改進項目

* 改進內容驅動頁面的產品詳細資訊元件的可重複使用性

* PDP的快取效能更好，後端呼叫也更少

* 多項錯誤修正。

## 發行日期：2021年2月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 1.8.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 1.8.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考站 | 2021.02.24 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-february}

* 產品體驗管理：使用體驗片段，讓產品目錄頁面個別豐富。

* 延伸產品控制台屬性，可顯示連結的資產和體驗片段，包括快速導覽至相關內容的動作。

### 改進項目  {#what-is-improved-february}

* 增強的用戶端資料層，提供產品影像url和類別資訊。

* 多項錯誤修正。

## 發行日期：2021年1月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 1.7.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 1.7.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考站 | 2021.02.02 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-january}

* 產品體驗管理：針對資產和體驗片段新增「商務」屬性標籤。 此索引標籤可讓您將資產和體驗片段連結至產品和類別。 索引標籤也會顯示連結商務物件的即時資料，以及可在產品主控台中顯示詳細資料的連結。

### 改進項目  {#what-is-improved-january}

* 在驗證後傳送使用者資料至Adobe用戶端資料層。

* 多項錯誤修正。
