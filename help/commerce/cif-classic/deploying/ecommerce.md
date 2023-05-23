---
title: 電子商務概述
seo-title: eCommerce Overview
description: 通AEM用電子商務作為標準安裝的一部分提供，並為您提供電子商務框架的全部功能。
seo-description: AEM generic eCommerce is available as part of the standard installation and provides you with the full functionality of the eCommerce framework.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 3%

---

# 電子商務概述{#ecommerce-overview}

通AEM用電子商務作為標準安裝的一部分提供，並為您提供電子商務框架的全部功能。

Adobe提供了Commerce Integration Framework的兩個版本：

|  | CIF開式 | CIF雲 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 支援的 AEM 版本 | AEMAMS 6.x | AEMAMS 6.4和6.5 |
| 後端 | - AEM, Java <br>  — 整體整合，預構建映射（模板）<br> - JCR儲存庫 | -Adobe Commerce <br>- Java和Javascript <br>- JCR儲存庫中沒有儲存的Commerce資料 |
| 前端 | AEM伺服器端呈現的頁 | 混合頁面應用程式（混合渲染） |
| 產品目錄 |  — 產品導入程式、編輯器、快取AEM <br> — 具有或代理頁AEM的常規目錄 |  — 無產品導入 <br> — 通用模板 <br> — 通過連接器按需資料 |
| 可擴充性 |  — 最多可支援幾百萬種產品（取決於使用情形） <br> - Dispatcher上的快取 |  — 無卷限制 <br> — 在Dispatcher或CDN上快取 |
| 標準化資料模型 | 否 | 是的，Adobe CommerceGraphQL模式 |
| 可用性 | 是：<br> - SAPCommerce Cloud(擴展已更新，AEM支援6.4和Hybris 5（預設），並保持與Hybris 4的相容性 <br>- SalesforceCommerce Cloud(Connector開源支援AEM6.4) | 是，通過GitHub通過開源。 <br> Adobe Commerce(支援2.3.2（預設）並與2.3.1相容。 |
| 使用時機 | 有限的使用情形：對於可能需要導入小型靜態目錄的情形 | 大多數使用情形中的首選解決方案 |


## 部署其他實施 {#deploying-other-implementations}

對於AEM和Adobe Commerce，請 [AEMAdobe Commerce](/help/commerce/cif/integrating/magento.md) 使用 [商務整合框架](/help/commerce/cif/introduction.md)。

>[!NOTE]
>
>有關概念和管理電子商務實施的資訊，請參見 [管理電子商務](/help/commerce/cif-classic/administering/ecommerce.md)。
>
>有關擴展電子商務功能的資訊，請參見 [發展電子商務](/help/commerce/cif-classic/developing/ecommerce.md)。
