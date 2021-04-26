---
title: 電子商務概觀
seo-title: 電子商務概觀
description: 通AEM用電子商務是標準安裝的一部分，提供您電子商務架構的完整功能。
seo-description: 通AEM用電子商務是標準安裝的一部分，提供您電子商務架構的完整功能。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: 商務整合框架
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 3%

---

# 電子商務概觀{#ecommerce-overview}

通AEM用電子商務是標準安裝的一部分，提供您電子商務架構的完整功能。

Adobe提供兩個版本的商務整合架構：

|  | CIF On-prem | CIF雲 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 支援的 AEM 版本 | AEMon-prem或AMS 6.x | AEMAMS 6.4和6.5 |
| 後端 | - AEM, Java <br> —— 整合，預構建映射（模板）<br> - JCR儲存庫 | -Magento<br>- Java和Javascript <br>-無儲存在JCR儲存庫中的商務資料 |
| 前端 | AEM伺服器端轉譯頁面 | 混合頁面應用程式（混合演算） |
| 產品目錄 | -產品匯入工具、編輯器、AEM<br>中的快取——含有或Proxy頁面的一般AEM型錄 | -無產品導入<br> —— 通用模板<br> —— 通過連接器按需資料 |
| 可擴充性 | -最多可支援幾百萬種產品（取決於使用案例）<br> - Caching on Dispatcher | -無卷限制<br> - Dispatcher或CDN上的快取 |
| 標準化資料模型 | 否 | 是，Magento圖QL模式 |
| 可用性 | 是：<br> - SAPCommerce Cloud(擴充功能已更新，支援AEM6.4和Hybris 5（預設值），並維持與Hybris 4 <br> - SalesforceCommerce Cloud(開放來源以支援AEM6.4的連接器) | 是，透過GitHub透過開放原始碼。 <br> Magento Commerce(支援Magento2.3.2（預設）並與Magento2.3.1相容)。 |
| 使用時機 | 有限的使用案例：對於需要匯入小型靜態型錄的情況 | 大多數使用案例中的首選解決方案 |


## 部署其他實施{#deploying-other-implementations}

有關AEM和Magento，請參閱&lt;a0/AEM>和Magento整合](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)使用[商務整合框架](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html)。[

>[!NOTE]
>
>有關概念和管理電子商務實施的資訊，請參閱[管理電子商務](/help/commerce/cif-classic/administering/ecommerce.md)。
>
>如需擴充電子商務功能的詳細資訊，請參閱[開發電子商務](/help/commerce/cif-classic/developing/ecommerce.md)。

