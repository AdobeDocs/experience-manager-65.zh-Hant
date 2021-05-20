---
title: 電子商務概述
seo-title: 電子商務概述
description: AEM通用電子商務是標準安裝的一部分，可提供您電子商務架構的完整功能。
seo-description: AEM通用電子商務是標準安裝的一部分，可提供您電子商務架構的完整功能。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: 商務整合架構
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 3%

---

# 電子商務概述{#ecommerce-overview}

AEM通用電子商務是標準安裝的一部分，可提供您電子商務架構的完整功能。

Adobe提供兩個版本的Commerce Integration Framework:

|  | CIF內部部署 | CIF雲 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 支援的 AEM 版本 | AEM內部部署或AMS 6.x | AEM AMS 6.4和6.5 |
| 後端 | - AEM, Java <br> — 整體整合，預建映射（範本）<br> - JCR存放庫 | -Magento<br>- Java和Javascript <br> — 無商務資料儲存在JCR儲存庫中 |
| 前端 | AEM伺服器端轉譯的頁面 | 混合頁面應用程式（混合演算） |
| 產品目錄 |  — 產品匯入工具、編輯器、AEM <br>中的快取 — 包含AEM或Proxy頁面的一般目錄 |  — 無產品導入<br> — 通用模板<br> — 通過連接器的按需資料 |
| 可擴充性 |  — 最多可支援數百萬項產品（視使用案例而定）<br> — 快取Dispatcher |  — 無卷限制<br> — 在Dispatcher或CDN上快取 |
| 標準化資料模型 | 否 | 是，MagentoGraphQL架構 |
| 可用性 | 是：<br> - SAPCommerce Cloud(更新擴充功能以支援AEM 6.4和Hybris 5（預設），並維護與Hybris 4 <br> - SalesforceCommerce Cloud的相容性(支援AEM 6.4的連接器開源) | 是，透過GitHub透過開放原始碼。 <br> Magento Commerce(支援Magento2.3.2（預設），並與Magento2.3.1相容)。 |
| 使用時機 | 有限的使用案例：對於可能需要匯入小型靜態目錄的情況 | 大多數使用案例中的首選解決方案 |


## 部署其他實施{#deploying-other-implementations}

若為AEM和Magento，請參閱[AEM和Magento整合](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)，使用[商務整合架構](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html)。

>[!NOTE]
>
>有關概念和管理電子商務實施的資訊，請參閱[管理電子商務](/help/commerce/cif-classic/administering/ecommerce.md)。
>
>有關擴展電子商務功能的資訊，請參閱[開發電子商務](/help/commerce/cif-classic/developing/ecommerce.md)。

