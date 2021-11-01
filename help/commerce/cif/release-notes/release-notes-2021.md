---
title: AEM內容與商務發行說明2021年
description: AEM內容與商務發行說明2021年
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: 7261a71769dfb968c768e0cb4835d7d4cca97b1a
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 8%

---

# 商務整合架構GitHub發行概述

## 系統需求概述

請參閱下表中您目前使用或計畫未來使用的CIF版本的最低系統需求。

**在4月的版本中，我們已將GitHub的CIF連接器更換為CIF附加元件** 可在 [Adobe軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 切換至附加元件可為專案帶來絕佳優勢：

* AEM 6.5將立即提供大部分新功能（不再等待功能端埠）
* 易於升級到新的附加版本
* 準備Cloud Service

舊版AEM CIF連接器將進入維護模式，不應再使用。 請將CIF連接器更換為新的CIF附加元件。 大多數項目都應該可以簡單地更換套件。

| 元件 | 系統需求 |
|:-------|:-----:|
| CIF附加元件 | 最低：AEM 6.5.7、Magento2.3.5 GraphQL結構 |
| CIF核心元件 | [系統需求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 專案原型 | [系統需求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 發行日期：2021年10月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.10.20.02 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| CIF核心元件 | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| CIF Venia參考站 | 2021.11.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### 新增功能 {#what-is-new-october}

* CIF附加元件支援最新的Commerce v2.4.3，並提供新的GraphQL API和結構

* 作者可使用RTF編輯器(RTE)，在文字欄位中新增產品和目錄頁面的連結。 RTE工具列中已新增CIF圖示，可開啟選擇器以快速搜尋並選取產品或類別，而不需離開內容。

* 現有的快顯購物車和結帳已取代為專用的AEM購物車和結帳頁面。 這些頁面上的元件是使用Magento的可擴充Peregrine元件所建置

* 商家可使用商務後端，在導覽中隱藏特定產品目錄類別。 CIF導覽核心元件會依照商務後端設定「包含在功能表中」，顯示/隱藏導覽中的類別

* AEM Storefront Venia在找不到類別或產品頁面時傳回HTTP 404錯誤

## 發行日期：2021年9月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.09.27 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| CIF核心元件 | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| CIF Venia參考站 | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### 新增功能 {#what-is-new-september}

* Sites編輯器中新的「關聯商務內容」索引標籤可快速存取目前內容的相關AEM產品內容，進而提高作者效率

   ![關聯商務內容](/help/assets/CIF/associated-commerce-content.png)

* 改善產品選擇器UI，提供更佳的使用者體驗、更高的效率，以及對複雜產品目錄的支援

   ![新產品選擇器](/help/assets/CIF/product-picker.png)

* 在導航元件中遵循「include_in_menu」屬性

### 錯誤修正 {#bug-fixes-september}

* 菜單快取刷新未如預期工作

* AEM CS部署步驟期間和不使用clientside元件時的JS錯誤

* 無法在具有sling:configs節點的資料夾中建立CIF雲端設定

## 發行日期：2021年8月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.09.02 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| CIF核心元件 | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| CIF Venia參考站 | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### 新增功能 {#what-is-new-august}

* 新的類別選擇器UI可改善使用者體驗、提高效率，以及更完善地支援複雜的產品目錄

   ![新類別選擇器](/help/assets/CIF/category-picker.png)

* 更A11Y支援CIF核心元件

### 錯誤修正 {#bug-fixes-august}

* 開啟類別篩選折疊式功能表後，就無法關閉它

* 產品預告中「呼叫動作文字」屬性損毀

* AEM CS部署步驟期間出現CIF JS錯誤

* 修正對應產品清單項目的原始產品存取權

## 發行日期：2021年7月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.07.21 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIF核心元件 | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| CIF Venia參考站 | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### 新增功能 {#what-is-new-july}

* CIF核心元件v2
   * 簡化並改善PDP/PLP URL和SEO的設定
   * 以製作模式呈現階段產品資料的視覺指標，可更清楚掌握即將進行的變更
   * 適用於內容與商務頁面的新Sitemap元件

* 支援 [Adobe Commerce Sensei產品建議，由Adobe Sensei提供技術支援](https://business.adobe.com/products/magento/product-recommendations.html) 在AEM Storefront中使用預先定義或即時建立的建議

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
* 商務核心元件支援Adobe Commerce Sensei Recs資料收集
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
