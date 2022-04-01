---
title: 《 AEM 2022年內容與商業發佈說明》
description: 《 AEM 2022年內容與商業發佈說明》
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 1a82930d9f0aa84cea590782aba2e70ec23b41c3
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 6%

---

# Commerce Integration Framework GitHub發佈概述

## 系統要求概述

查看下表中您當前使用或計畫將來使用的CIF版本的最低系統要求。

| 元件 | 系統要求 |
|:-------|:-----:|
| CIF附加 | 最小：AEM 6.5.7 、Magento2.3.5 GraphQL架構 |
| CIF核心元件 | [系統要求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 專案原型 | [系統要求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 發佈日期：2022年3月

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
   * 通過myAccount修改願望清單及其產品
   * 可以通過策略在元件級別上啟用/禁用「添加到願望清單」按鈕（例如，產品預告、產品詳細資訊）
   * 可作為核心元件在Venia StorefrontAEM中使用

![希望清單](/help/assets/CIF/wishlist.png)
