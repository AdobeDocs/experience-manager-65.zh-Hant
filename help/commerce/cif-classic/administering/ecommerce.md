---
title: 電子商務
description: 電AEM子商務可幫助營銷人員通過Web、移動和社交觸點提供品牌化、個性化的購物體驗。
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---

# 電子商務{#ecommerce}

* [概念](/help/commerce/cif-classic/administering/concepts.md)
* [管理（一般）](/help/commerce/cif-classic/administering/generic.md)

Adobe提供了Commerce Integration Framework的兩個版本：

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF開式</p> </th>
   <th><p>CIF雲</p> </th>
  </tr>
  <tr>
   <td><p>支援的 AEM 版本</p> </td>
   <td><p>AEMAMS 6.x</p> </td>
   <td>AEMAMS 6.4和6.5</td>
  </tr>
  <tr>
   <td><p>後端</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>整體整合、預構建映射（模板）</li>
     <li>JCR儲存庫</li>
    </ul> </td>
   <td>
    <ul>
     <li>Adobe Commerce</li>
     <li>Java和Javascript</li>
     <li>JCR儲存庫中未儲存商業資料</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>前端</p> </td>
   <td><p>AEM伺服器端呈現的頁</p> </td>
   <td>混合頁面應用程式（混合渲染）</td>
  </tr>
  <tr>
   <td><p>產品目錄</p> </td>
   <td>
    <ul>
     <li>產品導入程式、編輯器、快取AEM</li>
     <li>具有或代理頁AEM的常規目錄</li>
    </ul> </td>
   <td>
    <ul>
     <li>無產品導入</li>
     <li>通用模板</li>
     <li>通過連接器按需資料</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>可擴充性</p> </td>
   <td>
    <ul>
     <li>最多可支援幾百萬種產品（取決於使用情形）</li>
     <li>在Dispatcher上快取</li>
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
   <td>是，Adobe CommerceGraphQL架構</td>
  </tr>
  <tr>
   <td>可用性</td>
   <td><p>是. SAPCommerce Cloud(擴展已更新，AEM支援6.4和Hybris 5（預設），並保持與Hybris 4的相容性</p> <p>SalesforceCommerce Cloud(Connector開源支援AEM6.4)</p> </td>
   <td>是，通過GitHub通過開源。 Adobe Commerce(支援2.3.2（預設）並與2.3.1相容。</td>
  </tr>
  <tr>
   <td>何時使用</td>
   <td>有限的使用情形：例如，在需要導入小型靜態目錄的情況下</td>
   <td>大多數使用情形中的首選解決方案</td>
  </tr>
 </tbody>
</table>

電子商務與產品資訊管理(PIM)一起處理一個網站的活動，該網站的重點是通過線上商店銷售產品：

* 產品的建立、生命週期和過時
* 價格管理
* 交易管理
* 管理整個目錄
* 即時和集中的儲存記錄
* Web介面

電AEM子商務可幫助營銷人員通過Web、移動和社交觸點提供品牌化、個性化的購物體驗。 創作AEM環境允許您根據目標訪問者上下文和促銷策略定制頁面和元件；例如：

* 產品頁面
* 購物車元件
* 簽出元件

該實現允許即時訪問產品資訊。 這可用於強制：

* 產品資訊完整性
* 定價
* 庫存
* 購物車狀態的變化

>[!NOTE]
>
>要將整合框架與外部電子商務提供程式一起使用，您首先需要安裝所需的軟體包。 有關詳細資訊，請參見 [部署電子商務](/help/commerce/cif-classic/deploying/ecommerce.md)。
>
>有關擴展電子商務功能的資訊，請參見 [發展電子商務](/help/commerce/cif-classic/developing/ecommerce.md)。

## 主要功能 {#main-features}

AEM電子商務提供：

* 數 **現成組AEM件** 以說明您的項目可實現哪些目標：

   * 產品顯示
   * 購物車
   * 簽出
   * 最近查看的產品
   * 憑單
   * 其他

   ![](/help/sites-administering/assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >由提供的集AEM成框架還允許您構建AEM獨立於特定電子商務引擎的商務功能的其他元件。

* **搜索**  — 使用其中一項：

   * 搜AEM索
   * 電子商務系統的探索
   * 第三方搜索(如Search&amp;Promote)
   * 或其組合。

   ![](/help/sites-administering/assets/chlimage_1-131.png)

* 使AEM用 **在多個頻道上呈現您的內容**，可以是全瀏覽器窗口或移動設備。 這將以訪問者所需的格式提供內容。

   ![](/help/sites-administering/assets/chlimage_1-132.png)

* 能夠 **根據您自己的 [AEM電子商務框架](#the-framework)**。

   目前可用的兩種實現都基於相同的基礎構建 — 在通用API（框架）之上。 實施新整合只涉及實施您的整合所需的功能。 任何新實現都可以使用前端元件，因為它們使用介面（因此與實現無關）。

* 發展的可能性 **基於購物者資料和活動的經驗驅動型商務**。 這使您能夠實現許多情形：

   * 例如，當訂單總額超過特定金額時，可能會減少運輸成本。
   * 另一個選項可能允許您提供使用配置檔案資料（如位置）的季節性優惠。 然後，可以根據其他因素在必要時再次突出顯示這些內容。

   在下面的示例中，一個預告顯示為購物車的內容小於$75 :

   ![](/help/sites-administering/assets/chlimage_1-133.png)

   當購物車內容超過$75時，可以更改此項：

   ![](/help/sites-administering/assets/chlimage_1-134.png)

* 以及其他功能，包括：

   * 跨會話保留的購物車內容
   * 完整訂單歷史記錄
   * 快速目錄更新

## 框架 {#the-framework}

的 [概念](/help/commerce/cif-classic/administering/concepts.md) 部分詳細介紹了框架，但以下部分提供了框架的高級、高速視圖：

### 什麼？ {#what}

* 整合框架提供了API、一系列用於說明功能的元件和若干擴展，以提供連接方法的示例。
* 該框架提供了項目實施所需的基本結構。
* 該框架是可擴展的。
* 該框架不提供現成的、可使用的站點。 要使框架適應您的規格，總需要進行一定量的開發工作。

### 為什麼？ {#why}

* 為快速實現定制電子商務網站提供所需的基本機制。
* TP提供了開發真實電子商務網站所需的靈活性。
* 說明最佳做法。
