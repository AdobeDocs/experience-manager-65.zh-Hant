---
title: 電子商務
description: AEM eCommerce可協助行銷人員透過網路、行動裝置及社交接觸點，提供品牌化的個人化購物體驗。
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 2%

---

# 電子商務{#ecommerce}

* [概念](/help/commerce/cif-classic/administering/concepts.md)
* [管理（一般）](/help/commerce/cif-classic/administering/generic.md)

Adobe提供兩個版本的Commerce Integration Framework:

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF內部部署</p> </th>
   <th><p>CIF雲</p> </th>
  </tr>
  <tr>
   <td><p>支援的 AEM 版本</p> </td>
   <td><p>AEM內部部署或AMS 6.x</p> </td>
   <td>AEM AMS 6.4和6.5</td>
  </tr>
  <tr>
   <td><p>後端</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>整體整合、預建映射（範本）</li>
     <li>JCR存放庫</li>
    </ul> </td>
   <td>
    <ul>
     <li>Adobe Commerce</li>
     <li>Java與Javascript</li>
     <li>JCR儲存庫中未儲存任何商務資料</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>前端</p> </td>
   <td><p>AEM伺服器端轉譯的頁面</p> </td>
   <td>混合頁面應用程式（混合演算）</td>
  </tr>
  <tr>
   <td><p>產品目錄</p> </td>
   <td>
    <ul>
     <li>產品匯入工具、編輯器、AEM中的快取</li>
     <li>包含AEM或Proxy頁面的一般目錄</li>
    </ul> </td>
   <td>
    <ul>
     <li>無產品導入</li>
     <li>一般範本</li>
     <li>透過連接器提供隨選資料</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>可擴充性</p> </td>
   <td>
    <ul>
     <li>最多可支援數百萬種產品（取決於使用案例）</li>
     <li>Dispatcher上的快取</li>
    </ul> </td>
   <td>
    <ul>
     <li>無卷限制</li>
     <li>在Dispatcher或CDN上快取</li>
    </ul> </td>
  </tr>
  <tr>
   <td>標準化資料模型</td>
   <td>否</td>
   <td>是，Adobe Commerce GraphQL結構</td>
  </tr>
  <tr>
   <td>可用性</td>
   <td><p>可以。SAPCommerce Cloud(更新擴充功能以支援AEM 6.4和Hybris 5（預設），並維持與Hybris 4的相容性</p> <p>SalesforceCommerce Cloud(支援AEM 6.4的Connector開源)</p> </td>
   <td>是，透過GitHub透過開放原始碼。 Adobe Commerce(支援2.3.2（預設），並與2.3.1相容)。</td>
  </tr>
  <tr>
   <td>使用時機</td>
   <td>有限的使用案例：例如，可能需要匯入小型靜態目錄的案例</td>
   <td>大多數使用案例中的首選解決方案</td>
  </tr>
 </tbody>
</table>

電子商務與產品資訊管理(PIM)一起處理網站的活動，重點是通過線上商店銷售產品：

* 產品的建立、存留期和淘汰
* 價格管理
* 交易管理
* 管理整個目錄
* 即時和集中儲存記錄
* Web介面

AEM eCommerce可協助行銷人員透過網路、行動裝置及社交接觸點，提供品牌化的個人化購物體驗。 AEM製作環境可讓您根據目標訪客內容和銷售策略來自訂頁面和元件；例如：

* 產品頁面
* 購物車元件
* 結帳元件

實施可讓您即時存取產品資訊。 這可用於強制：

* 產品資訊完整性
* 定價
* 庫存庫存
* 購物車狀態的變化

>[!NOTE]
>
>若要與外部電子商務提供者使用整合架構，您必須先安裝所需的套件。 如需詳細資訊，請參閱 [部署eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>如需擴充電子商務功能的詳細資訊，請參閱 [開發電子商務](/help/commerce/cif-classic/developing/ecommerce.md).

## 主要功能 {#main-features}

AEM eCommerce提供：

* 數 **現成可用的AEM元件** 以說明可為您的專案達成哪些目標：

   * 產品顯示
   * 購物車
   * 結帳
   * 最近查看的產品
   * 憑單
   * 其他

   ![](/help/sites-administering/assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >AEM提供的整合架構也可讓您針對商務功能建立其他AEM元件，而不受特定電子商務引擎影響。

* **搜尋**  — 使用下列其中一項：

   * AEM搜尋
   * 電子商務系統的搜索
   * 第三方搜尋
   * 或其組合。

   ![](/help/sites-administering/assets/chlimage_1-131.png)

* 使用AEM功能 **在多個頻道上呈現內容**，可以是完整瀏覽器視窗或行動裝置。 這會以訪客所需的格式提供內容。

   ![](/help/sites-administering/assets/chlimage_1-132.png)

* 能夠 **根據開發您自己的整合實作 [AEM eCommerce架構](#the-framework)**.

   目前可用的兩個實施都是以相同為基礎而建置，而非一般API（架構）。 實作新整合只涉及實作您的整合需求的功能。 任何新實作都可以使用前端元件，因為前端元件使用介面（因此與實作無關）。

* 發展 **基於購物者資料和活動的體驗導向商務**. 這可讓您了解許多情況：

   * 例如，當訂單總額超過特定金額時，可能會降低運費。
   * 另一個選件可讓您提供使用設定檔資料的季節性選件（例如位置）。 接著，視需要再視其他因素，再強調顯示這些項目。

   在以下範例中，一個宣傳預告顯示為購物車內容小於$75:

   ![](/help/sites-administering/assets/chlimage_1-133.png)

   當購物車內容超過$75時，可以變更此項：

   ![](/help/sites-administering/assets/chlimage_1-134.png)

* 以及其他功能，包括：

   * 跨工作階段保留的購物車內容
   * 完整訂單歷史記錄
   * 快速目錄更新

## 框架 {#the-framework}

此 [概念](/help/commerce/cif-classic/administering/concepts.md) 一節更詳細地介紹了該框架，但下面提供了該框架的高級、高速視圖：

### 什麼？ {#what}

* 整合架構提供API、說明功能的一系列元件，以及提供連線方法範例的數個擴充功能。
* 該框架提供了項目實施所需的基本結構。
* 該框架是可擴展的。
* 框架不提供現成可用的網站。 要使框架適應您的規範，始終需要進行一定數量的開發工作。

### 原因為何？ {#why}

* 提供快速實現定制電子商務站點所需的基本機制。
* Tp提供開發真實電子商務站點所需的靈活性。
* 說明最佳實務。
