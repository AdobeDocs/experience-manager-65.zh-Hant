---
title: 2021AEM年內容與商務發行說明
description: 2021AEM年內容與商務發行說明
translation-type: tm+mt
source-git-commit: 2d0b52dbf85e1fbe91c09a8366744aa77f25cd73
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 10%

---

# 商務整合架構GitHub發行概觀

## 系統需求概述

請檢閱下表中您目前使用或計畫日後使用之CIF版本的最低系統需求。

**CIF附加元件現在可透過 [Adobe軟體散發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。舊AEMCIF連接器將進入維護模式，不應再使用。 請移轉至新的CIF附加元件。**

| 元件 | 系統需求 |
|:-------|:-----:|
| CIF附加元件 | 最低：AEM 6.5.7,Magento2.3.5 GraphQL結構 |
| CIF核心元件 | [系統需求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 專案原型 | [系統需求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 發行日期：2021年4月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | v2021.04.22 | [軟體散發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF核心元件 | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韋尼亞參考站 | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新功能 {#what-is-new-april}

* **CIF附加元件現在可透過 [Adobe軟體散發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。舊AEMCIF連接器將進入維護模式，不應再使用。 請移轉至新的CIF附加元件。**

* 支援類別UID —— 這可為使用類別ID字串的系統解除協力廠商商務整合鎖定

* AEM擴充PWA Studio 範例整合

* 擴充WCM導覽核心元件的全新CIF導覽核心元件

* 店面中分段型錄資料的可視指AEM示器

### 錯誤修正 {#bug-fixes-april}

* 類別頁面的頁面屬性中，根類別欄位未顯示在商務標籤下方

## 發行日期：2021年3月{#what-is-new-march}

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 1.9.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 1.9.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韋尼亞參考站 | 2021.03.25 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新功能

* 支援Magento2.4.2

### 功能改善

* 針對內容導向頁面改善產品細節元件的可重複性

* 更佳的快取功能和更少的PDP後端呼叫

* 多個錯誤修正。

## 發行日期：2021年2月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 1.8.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 1.8.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韋尼亞參考站 | 2021.02.24 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新功能 {#what-is-new-february}

* 產品體驗管理：使用體驗片段讓產品目錄頁面更加豐富。

* 延伸產品主控台屬性以顯示連結的資產和體驗片段，包括快速導覽至相關內容的動作。

### 功能改善  {#what-is-improved-february}

* 增強的用戶端資料層，包含產品影像URL和類別資訊

* 多個錯誤修正。

## 發行日期：2021年1月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 1.7.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 1.7.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韋尼亞參考站 | 2021.02.02 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新功能 {#what-is-new-january}

* 產品體驗管理：資產和體驗片段的新「商務」屬性標籤。 此標籤可讓您將資產和體驗片段連結至產品和類別。 此標籤也會顯示連結商務物件的即時資料，以及在產品主控台中顯示詳細資料的連結。

### 功能改善  {#what-is-improved-january}

* 在驗證後傳送使用者資料至Adobe用戶端資料層。

* 多個錯誤修正。
