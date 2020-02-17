---
title: 電子商務概觀
seo-title: 電子商務概觀
description: AEM一般電子商務可做為標準安裝的一部分，並提供您電子商務架構的完整功能。
seo-description: AEM一般電子商務可做為標準安裝的一部分，並提供您電子商務架構的完整功能。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 5d46836a8b7b66daa8f27bc6fad14319ab1f58a7

---


# 電子商務概觀{#ecommerce-overview}

AEM一般電子商務可做為標準安裝的一部分，並提供您電子商務架構的完整功能。

Adobe提供兩個版本的商務整合架構：

|  | CIF On-prem | CIF雲 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 支援的 AEM 版本 | AEM on-prem或AMS 6.x | AEM AMS 6.4和6.5 |
| 後端 | - AEM,Java <br> -整合，預建對應（範本）<br> - JCR儲存庫 | - Magento <br>- java和Javascript <br>-無商務資料儲存在JCR儲存庫中 |
| 前端 | AEM伺服器端轉譯的頁面 | 混合頁面應用程式（混合演算） |
| 產品目錄 | -產品匯入工具、編輯器、AEM中的快取 <br>-含AEM或Proxy頁面的一般型錄 | -無產品匯入 <br>-通用範本 <br>-透過連接器的隨選資料 |
| 可擴充性 | -最多可支援幾百萬種產品（取決於使用案例） <br> - Caching on Dispatcher | -無卷限制 <br>- Dispatcher或CDN的快取 |
| 標準化資料模型 | 否 | 是，Magento GraphQL模式 |
| 可用性 | <br> 是：- SAP Commerce Cloud(Extension已更新，以支援AEM 6.4和Hybris 5（預設值），並維持與Hybris 4 <br>- Salesforce Commerce Cloud(Connector open-sourced to support AEM 6.4)的相容性 | 是，透過GitHub透過開放原始碼。 <br> Magento Commerce(支援Magento 2.3.2（預設值），並與Magento 2.3.1相容)。 |
| 使用時機 | 有限的使用案例：對於需要匯入小型靜態型錄的情況 | 大多數使用案例中的首選解決方案 |


## 部署其他實施 {#deploying-other-implementations}

如需AEM和Magento，請使用 [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md) ，查看 [AEM和Magento整合](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html)。

>[!NOTE]
>
>如需有關概念和管理電子商務實作的資訊，請參 [閱管理電子商務](/help/sites-administering/ecommerce.md)。
>
>如需擴充電子商務功能的詳細資訊，請參 [閱開發電子商務](/help/sites-developing/ecommerce.md)。

