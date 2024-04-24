---
title: Adobe Experience Manager內容與Commerce 2021年發行說明
description: Adobe Experience Manager內容和Commerce發行說明2021年。
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 9%

---

# Commerce integration framework GitHub版本總覽

## 系統需求概觀

請檢閱下表中，您目前使用或計畫未來使用的CIF版本的最低系統需求。

| 元件 | 系統需求 |
|:-------|:-----:|
| CIF附加元件 | 最低： Adobe Experience Manager (AEM) 6.5.7、Adobe Commerce 2.3.5 GraphQL結構描述 |
| CIF Core Components | [系統需求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 專案原型 | [系統需求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 發行日期： 2021年11月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.11.18.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.11.18.00.zip) |
| CIF Core Components | 2.4.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.2) |
| CIF Venia參考網站 | 2021.12.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.12.01) |

### 新增功能 {#what-is-new-november}

* 以Commerce的可擴充Peregrine元件為基礎的擴充myAccount元件

![延伸的myAccount元件](/help/assets/CIF/extended-myAccount-components.png)

* 作者可使用其他建議型別來建立臨機Commerce產品Recommendations

* 支援AEM Storefront中的禮品卡

## 發行日期： 2021年10月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.10.20.02 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| CIF Core Components | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| CIF Venia參考網站 | 2021.11.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### 新增功能 {#what-is-new-october}

* CIF附加元件支援具有新Commerce API和結構描述的最新GraphQL v2.4.3

* 作者可使用RTF編輯器(RTE)，在文字欄位中新增產品與目錄頁面的連結。 RTE工具列中新增了CIF圖示，可開啟選擇器，以便快速搜尋並選取產品或類別，而不需離開內容。

* 現有的彈出式購物車和結帳頁面已替換為專用的AEM購物車和結帳頁面。 這些頁面上的元件是使用Adobe Commerce的可擴充Peregrine元件所建置

* 商家可使用Commerce後端，在導覽中隱藏特定產品目錄類別。 CIF導覽核心元件依照商務後端設定「包含在功能表中」以在導覽中顯示/隱藏類別

* 如果找不到類別或產品頁面，AEM Storefront Venia會傳回HTTP 404錯誤

## 發行日期： 2021年9月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.09.27 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| CIF Core Components | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| CIF Venia參考網站 | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### 新增功能 {#what-is-new-september}

* Sites編輯器中新的「相關商務內容」索引標籤可快速存取目前內容的相關AEM產品內容，提升作者效率

  ![關聯的商務內容](/help/assets/CIF/associated-commerce-content.png)

* 改良產品選擇器UI，提供更佳的使用者體驗、更高的效率，並支援複雜的產品目錄

  ![新的產品挑選器](/help/assets/CIF/product-picker.png)

* 在導覽元件中遵循「include_in_menu」屬性

### 錯誤修正 {#bug-fixes-september}

* 功能表快取排清未按預期運作

* AEM CS部署步驟期間及未使用使用者端元件時的JS錯誤

* 無法在具有sling：configs節點的資料夾中建立CIF雲端設定

## 發行日期： 2021年8月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.09.02 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| CIF Core Components | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| CIF Venia參考網站 | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### 新增功能 {#what-is-new-august}

* 新的類別選擇器UI可改善使用者體驗、提高效率，以及更好地支援複雜的產品目錄

  ![新增類別選取器](/help/assets/CIF/category-picker.png)

* CIF核心元件更好的A11Y支援

### 錯誤修正 {#bug-fixes-august}

* 類別篩選器摺疊式功能表開啟後即無法關閉

* 產品Teaser中的「呼叫動作文字」屬性已中斷

* AEM CS部署步驟期間的CIF JS錯誤

* 修正對應產品清單專案的原始產品存取權

## 發行日期： 2021年7月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.07.21 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIF Core Components | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| CIF Venia參考網站 | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### 新增功能 {#what-is-new-july}

* CIF核心元件v2
   * 簡化並改善PDP/PLP URL和SEO的設定
   * 在製作模式下分階段產品資料的視覺指示器，可更清楚顯示即將發生的變更
   * 內容和商務頁面的新Sitemap元件

* 支援 [Adobe Commerce Sensei產品推薦，由Adobe Sensei提供技術支援](https://business.adobe.com/products/magento/product-recommendations.html) 在AEM Storefront中使用預先定義或即時建立的建議

## 發行日期： 2021年6月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.06.18 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIF Core Components | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Venia參考網站 | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### 新增功能 {#what-is-new-june}

* 內容片段的新增CIF產品和類別參考資料型別(包括 產品/類別選擇器UI支援)
* 全新Commerce內容片段核心元件
* AEM後端支援全文檢索商務搜尋
* Commerce核心元件支援Adobe Commerce Sensei Recs資料收集
* 改善類別頁面的SEO易記URL
* 支援每個網站/設定的自訂HTTP標頭

## 發行日期： 2021年5月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.05.26 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIF Core Components | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Venia參考網站 | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### 新增功能 {#what-is-new-may}

* 產品主控台屬性中的相關內容支援分頁

### 錯誤修正 {#bug-fixes-may}

* 資產縮圖未顯示在產品屬性的「資產」標籤中

* 階層連結在產品主控台中重設預覽資料

## 發行日期： 2021年4月

| 元件 | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加元件 | 2021.04.22 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF Core Components | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考網站 | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-april}

* 類別UID的支援 — 針對使用字串當做類別ID的系統，此功能可開啟協力廠商商業整合功能

* PWA Studio的AEM擴充功能，包括 整合範例

* 可擴充WCM導覽核心元件的新CIF導覽核心元件

### 錯誤修正 {#bug-fixes-april}

* 根類別欄位未顯示在類別頁面的頁面屬性中的商務索引標籤下

## 發行日期： 2021年3月 {#what-is-new-march}

| GitHub | 版本 | 詳細的發行說明 |
|:-------|:-----:|---------------------:|
| CIF聯結器 | 1.9.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF Core Components | 1.9.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考網站 | 2021.03.25 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能

* 支援Adobe Commerce 2.4.2

### 功能改善

* 改善內容導向頁面之產品詳細資料元件的可重複使用性

* PDP的快取功能更佳，後端呼叫也更少

* 多項錯誤修正。

## 發行日期： 2021年2月

| GitHub | 版本 | 詳細的發行說明 |
|:-------|:-----:|---------------------:|
| CIF聯結器 | 1.8.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF Core Components | 1.8.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考網站 | 2021.02.24 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-february}

* 產品體驗管理：使用體驗片段個別豐富產品目錄頁面。

* 擴充產品主控台屬性，以顯示連結的資產和體驗片段，包括快速導覽至關聯內容的動作。

### 功能改善  {#what-is-improved-february}

* 使用產品影像url和類別資訊增強使用者端資料層。

* 多項錯誤修正。

## 發行日期： 2021年1月

| GitHub | 版本 | 詳細的發行說明 |
|:-------|:-----:|---------------------:|
| CIF聯結器 | 1.7.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF Core Components | 1.7.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考網站 | 2021.02.02 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-january}

* 產品體驗管理：資產和體驗片段的新「Commerce」屬性標籤。 此索引標籤可讓您將資產和體驗片段連結到產品和類別。 此索引標籤也會顯示連結的商務物件的即時資料，以及在產品主控台中顯示詳細資訊的連結。

### 功能改善  {#what-is-improved-january}

* 在驗證後將使用者資料傳送至Adobe使用者端資料層。

* 多項錯誤修正。
