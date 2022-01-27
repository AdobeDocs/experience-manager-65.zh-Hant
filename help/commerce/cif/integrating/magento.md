---
title: 商AEM務整合框架與Adobe Commerce
description: 而AEMAdobe Commerce則利用商業整合框架(CIF)進行無縫整合。 CIF使AEM用GraphQL訪問Adobe Commerce實例並與Adobe Commerce通信。 它還允許AEM作者使用產品和類別選擇器以及產品控制台瀏覽從Adobe Commerce按需獲取的產品和類別資料。 此外，CIF還提供了一個現成的店面，可以加快商業項目。
thumbnail: aem-magento-architecture.jpg
exl-id: f843784c-5ff7-41d1-97c5-13facb8459b2
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---

# 利用AEMCommerce Integration Framework與Adobe Commerce(Magento)整合 {#aem-commerce-framework}

該Experience Manager和Adobe Commerce利用商業整合框架(CIF)進行無縫整合。 CIF使AEM用Adobe Commerce的 [GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/)。

>[!NOTE]
>
> 支援的GraphQL API最低版本為2.3.5。某些功能僅在較新版本或僅在Adobe Commerce版中受支援。

## 體系結構概述 {#overview}

總體體系結構如下：

![CIF體系結構概述](../assets/AEM_Magento_Architecture.png)

在CIF中，支援伺服器端和客戶端通信模式。
伺服器端API調用使用內置通用 [GraphQL客戶端](https://github.com/adobe/commerce-cif-graphql-client) 與 [生成的資料模型集](https://github.com/adobe/commerce-cif-magento-graphql) GraphQL架構。 此外，可以使用任何GQL格式的GraphQL查詢或變異。

對於使用 [反應](https://reactjs.org/)，也請參見Wiki頁。 [阿波羅客戶](https://www.apollographql.com/docs/react/) 的子菜單。

## CIF核AEM心元件體系結構 {#cif-core-components}

![CIF核AEM心元件體系結構](../assets/cif-component-architecture.jpg)

[AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components) 遵循非常相似的設計模式和最佳做法 [AEMWCM核心元件](https://github.com/adobe/aem-core-wcm-components)。

CIF核心元件的業務邏輯和與Adobe CommerceAEM的後端通信在Sling模型中實現。 如果需要自定義此邏輯以滿足項目特定要求，則可以使用Sling模型的委託模式。

>[!TIP]
>
>的 [自定義AEMCIF核心元件](../customizing/customize-cif-components.md) 頁面提供了有關如何自定義CIF核心元件的詳細示例和最佳實踐。

在項目中，AEM CIF核心元件和定制項目元件可以通過Sling Context-Aware配置輕鬆檢索與頁面關聯的Adobe Commerce儲存的AEM配置客戶端。
