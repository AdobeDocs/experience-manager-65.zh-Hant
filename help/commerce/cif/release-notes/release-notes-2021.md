---
title: 《 AEM 2021年內容與商業發佈說明》
description: 《 AEM 2021年內容與商業發佈說明》
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 9%

---

# Commerce Integration Framework GitHub發佈概述

## 系統要求概述

查看下表中您當前使用或計畫將來使用的CIF版本的最低系統要求。

| Component | 系統要求 |
|:-------|:-----:|
| CIF附加 | 最小：AEM6.5.7Adobe Commerce2.3.5GraphQL架構 |
| CIF核心元件 | [系統要求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 專案原型 | [系統要求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 發佈日期：2021年11月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2021.11.18.00 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.11.18.00.zip) |
| CIF核心元件 | 2.4.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.2) |
| CIF Venia參考站點 | 2021.12.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.12.01) |

### 新增功能 {#what-is-new-november}

* 基於Commerce可擴展的Peregrine元件的擴展myAccount元件

![擴展的myAccount元件](/help/assets/CIF/extended-myAccount-components.png)

* 作者可以使用其他建議類型建立臨時商務產品Recommendations

* 在店面中支援禮品AEM卡

## 發佈日期：2021年10月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2021.10.20.02 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| CIF核心元件 | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| CIF Venia參考站點 | 2021.11.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### 新增功能 {#what-is-new-october}

* CIF附加模組支援最新的Commerce v2.4.3和新的GraphQLAPI和架構

* 作者可以使用富格文本編輯器(RTE)在文本欄位中添加到產品和目錄頁面的連結。 CIF表徵圖已添加到RTE工具欄，該工具欄將開啟選擇者以快速搜索和選擇產品或類別而不離開上下文。

* 現有的彈出式購物車和結帳已替換為專用的購AEM物車和結帳頁。 這些頁面上的元件是使用Adobe Commerce的可擴展Peregrine元件構建的

* 商家可以使用Commerce後端在導航中隱藏某些產品目錄類別。 CIF導航核心元件尊重商業後端配置「包括在菜單中」以顯示/隱藏導航中的類別

* 如AEM果找不到類別或產品頁，Storefront Venia將返回HTTP 404錯誤

## 發佈日期：2021年9月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2021.09.27 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| CIF核心元件 | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| CIF Venia參考站點 | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### 新增功能 {#what-is-new-september}

* 「站點」編輯器中新的「關聯商業內容」頁籤通過快速訪問當前上下文的AEM相關產品內容而提高了作者效率

   ![關聯的商務內容](/help/assets/CIF/associated-commerce-content.png)

* 改進了產品選取器UI，以獲得更好的用戶體驗、提高效率和支援複雜產品目錄

   ![新產品選取器](/help/assets/CIF/product-picker.png)

* 在導航元件中尊重&quot;include_in_menu&quot;屬性

### 錯誤修正 {#bug-fixes-september}

* 菜單快取刷新未按預期工作

* CS部署步驟AEM和不使用客戶端元件時的JS錯誤

* 無法在具有sling:configs節點的資料夾中建立CIF雲配置

## 發佈日期：2021年8月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2021.09.02 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| CIF核心元件 | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| CIF Venia參考站點 | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### 新增功能 {#what-is-new-august}

* 新的類別選取器UI可改善用戶體驗、提高效率並更好地支援複雜的產品目錄

   ![新建類別選取器](/help/assets/CIF/category-picker.png)

* 更好地支援CIF核心元件

### 錯誤修正 {#bug-fixes-august}

* 開啟類別篩選器折疊面板後無法關閉

* 產品預告中斷開的「操作調用文本」屬性

* CIF JS在CS部署步AEM驟期間出錯

* 修復映射產品清單項的原始產品訪問

## 發佈日期：2021年7月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2021.07.21 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIF核心元件 | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| CIF Venia參考站點 | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### 新增功能 {#what-is-new-july}

* CIF核心元件v2
   * PDP/PLP URL和SEO的簡化和改進配置
   * 在創作模式下用於分段產品資料的可視指示器，以更好地查看即將進行的更改
   * 用於內容和商業頁面的新站點地圖元件

* 支援 [Adobe CommerceSensei產品推薦，由Adobe Sensei提供支援](https://business.adobe.com/products/magento/product-recommendations.html) 在AEM店面中使用預定義或即時建立的建議

## 發佈日期：2021年6月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2021.06.18 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIF核心元件 | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Venia參考站點 | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### 新增功能 {#what-is-new-june}

* 內容片段的新CIF產品和類別引用資料類型(包括 產品/類別選取器UI支援)
* 新商務內容片段核心元件
* 後端支援全文商務搜AEM索
* Commerce核心元件支援Adobe CommerceSenseiRecs資料收集
* 類別頁的SEO友好型URL的改進
* 支援每個站點/配置的自定義HTTP標頭

## 發佈日期：2021年5月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2021.05.26 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIF核心元件 | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Venia參考站點 | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### 新增功能 {#what-is-new-may}

* 產品控制台屬性中關聯內容的分頁支援

### 錯誤修正 {#bug-fixes-may}

* 未在產品屬性的「資產」頁籤中顯示資產縮略圖

* Breadcrumb重置產品控制台中的預覽資料

## 發佈日期：2021年4月

| Component | 版本 | 詳細資料 |
|:-------|:-----:|---------------------:|
| CIF附加 | 2021.04.22 | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF核心元件 | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考站點 | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-april}

* 支援類別UID — 這將解除對使用Strings進行類別ID的系統的第三方商務整合的鎖定

* 擴展AEMPWA Studio，包括 示例整合

* 擴展WCM導航核心元件的新CIF導航核心元件

### 錯誤修正 {#bug-fixes-april}

* 根類別欄位未顯示在類別頁的頁面屬性中的commerce頁籤下

## 發佈日期：2021年3月 {#what-is-new-march}

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 1.9.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 1.9.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考站點 | 2021.03.25 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能

* 支援Adobe Commerce2.4.2

### 改進內容

* 用於內容驅動頁面的產品細節元件的改進的可重用性

* 更好的快取，減少對PDP的後端呼叫

* 多個錯誤修復。

## 發佈日期：2021年2月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 1.8.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 1.8.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考站點 | 2021.02.24 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-february}

* 產品體驗管理：使用經驗片段單獨豐富產品目錄頁。

* 擴展的產品控制台屬性，用於顯示連結的資產和體驗片段，包括快速導航到相關內容的操作。

### 改進內容  {#what-is-improved-february}

* 增強的客戶端資料層，具有產品影像url和類別資訊。

* 多個錯誤修復。

## 發佈日期：2021年1月

| GitHub | 版本 | 詳細發行說明 |
|:-------|:-----:|---------------------:|
| CIF連接器 | 1.7.0 | [發行說明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心元件 | 1.7.0 | [發行說明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia參考站點 | 2021.02.02 | [發行說明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-january}

* 產品體驗管理：「資產」和「體驗片段」的新「商業」屬性頁籤。 此頁籤使您能夠將資產和體驗片段連結到產品和類別。 該頁籤還顯示連結商業對象的即時資料以及在產品控制台中顯示詳細資訊的連結。

### 改進內容  {#what-is-improved-january}

* 在驗證後將用戶資料發送到Adobe客戶端資料層。

* 多個錯誤修復。
