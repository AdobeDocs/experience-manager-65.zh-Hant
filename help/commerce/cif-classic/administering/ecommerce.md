---
title: 電子商務
description: 電AEM子商務可協助行銷人員透過網路、行動裝置和社交觸點提供品牌化的個人化購物體驗。
topic-tags: e-commerce
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---

# 電子商務{#ecommerce}

* [概念](/help/commerce/cif-classic/administering/concepts.md)
* [管理（一般）](/help/commerce/cif-classic/administering/generic.md)

Adobe提供兩個版本的商務整合架構：

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF On-prem</p> </th>
   <th><p>CIF雲</p> </th>
  </tr>
  <tr>
   <td><p>支援的 AEM 版本</p> </td>
   <td><p>AEMon-prem或AMS 6.x</p> </td>
   <td>AEMAMS 6.4和6.5</td>
  </tr>
  <tr>
   <td><p>後端</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>整體整合、預建對應（範本）</li>
     <li>JCR資料庫</li>
    </ul> </td>
   <td>
    <ul>
     <li>Magento</li>
     <li>Java與Javascript</li>
     <li>JCR儲存庫中未儲存任何商務資料</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>前端</p> </td>
   <td><p>AEM伺服器端轉譯頁面</p> </td>
   <td>混合頁面應用程式（混合演算）</td>
  </tr>
  <tr>
   <td><p>產品目錄</p> </td>
   <td>
    <ul>
     <li>產品匯入工具、編輯器、快取AEM</li>
     <li>具有或代理頁AEM面的常規目錄</li>
    </ul> </td>
   <td>
    <ul>
     <li>無產品匯入</li>
     <li>一般範本</li>
     <li>透過連接器的隨選資料</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>可擴充性</p> </td>
   <td>
    <ul>
     <li>最多可支援幾百萬種產品（視使用案例而定）</li>
     <li>Dispatcher上的快取</li>
    </ul> </td>
   <td>
    <ul>
     <li>無卷限制</li>
     <li>Dispatcher或CDN上的快取</li>
    </ul> </td>
  </tr>
  <tr>
   <td>標準化資料模型</td>
   <td>否</td>
   <td>是，Magento圖QL模式</td>
  </tr>
  <tr>
   <td>可用性</td>
   <td><p>是. SAPCommerce Cloud(擴充功能已更新，支援AEM6.4和Hybris 5（預設），並維持與Hybris 4的相容性</p> <p>SalesforceCommerce Cloud(支援6.4的開源AEM連接器)</p> </td>
   <td>是，透過GitHub透過開放原始碼。 Magento Commerce(支援Magento2.3.2（預設）並與Magento2.3.1相容)。</td>
  </tr>
  <tr>
   <td>使用時機</td>
   <td>有限的使用案例：例如，在需要匯入小型靜態型錄的情況下</td>
   <td>大多數使用案例中的首選解決方案</td>
  </tr>
 </tbody>
</table>

電子商務與產品資訊管理(PIM)一起處理網站的活動，主要透過線上商店銷售產品：

* 建立、存留期間和淘汰產品
* 價格管理
* 交易管理
* 管理整個型錄
* 即時和集中化的儲存記錄
* 網頁介面

電AEM子商務可協助行銷人員透過網路、行動裝置和社交觸點提供品牌化的個人化購物體驗。 製作環AEM境可讓您根據目標訪客的上下文和銷售策略來自訂頁面和元件；例如：

* 產品頁面
* 購物車元件
* 結帳元件

實施可讓您即時存取產品資訊。 這可用於強制：

* 產品資訊完整性
* 定價
* 庫存
* 購物車狀態的變化

>[!NOTE]
>
>若要與外部電子商務提供者使用整合架構，您必須先安裝所需的套件。 如需詳細資訊，請參閱[部署電子商務](/help/commerce/cif-classic/deploying/ecommerce.md)。
>
>如需擴充電子商務功能的詳細資訊，請參閱[開發電子商務](/help/commerce/cif-classic/developing/ecommerce.md)。

## 主要功能{#main-features}

AEM電子商務提供：

* 一些&#x200B;**現成可用的元件AEM**，以說明可為項目實現的目標：

   * 產品展示
   * 購物車
   * 結帳
   * 最近檢視的產品
   * 憑單
   * 及其他

   ![](/help/sites-administering/assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >由提供的整合架構AEM也可讓您建立其他元AEM件，以建立獨立於特定電子商務引擎的商務功能。

* **搜尋** -使用下列其中一項：

   * 搜尋AEM
   * 電子商務系統的研究
   * 第三方搜尋(例如Search&amp;Promote)
   * 或其組合。

   ![](/help/sites-administering/assets/chlimage_1-131.png)

* 使用&lt;AEMa0/>在多個頻道（無論是完整瀏覽器視窗或行動裝置）上呈現您的內容的能力。 ****&#x200B;這會以訪客所需的格式提供您的內容。

   ![](/help/sites-administering/assets/chlimage_1-132.png)

* **根據[電子商務架構](#the-framework)**&#x200B;開發您自己AEM的整合實作的能力。

   目前可用的兩個實作都是以相同的基礎建立——以一般API（架構）為基礎。 實作新整合只涉及實作您整合所需的功能。 任何新的實作都可以使用前端元件，因為它們使用介面（因此與實作無關）。

* 基於購物者資料和活動&#x200B;**開發體驗驅動型商務的可能性。**&#x200B;這可讓您瞭解許多情形：

   * 例如，當訂單總量超過特定金額時，可能會降低運費。
   * 另一種可能可讓您提供使用描述檔資料的季節性選件（例如位置）。 然後，視需要依其他因素，再加亮這些項目。

   在下列範例中，一個摘要顯示為購物車內容小於$75:

   ![](/help/sites-administering/assets/chlimage_1-133.png)

   當購物車內容超過$75時，可以變更此項：

   ![](/help/sites-administering/assets/chlimage_1-134.png)

* 其他功能包括：

   * 跨作業保留的購物車內容
   * 完整訂單記錄
   * 快速目錄更新

## 框架{#the-framework}

[Concepts](/help/commerce/cif-classic/administering/concepts.md)一節更詳細地介紹了框架，但以下內容提供了框架的高級、高速視圖：

### 什麼？{#what}

* 整合架構提供API、一系列元件來說明功能，以及數種擴充功能來提供連線方法的範例。
* 該框架提供了項目實施所需的基本結構。
* 該框架具有可擴充性。
* 此架構不提供現成可用的網站。 為了配合您的規格調整架構，一律需要進行一定量的開發工作。

### 為什麼？{#why}

* 提供快速實現自訂電子商務網站所需的基本機制。
* 提供開發實際電子商務網站所需的彈性。
* 說明最佳實務。
