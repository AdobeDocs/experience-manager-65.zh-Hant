---
title: 使用Commerce integration framework整合AEM和Adobe Commerce
description: 使用Commerce integration framework (CIF)將AEM與Adobe Commerce緊密整合。 CIF可讓AEM存取Adobe Commerce執行個體，並透過GraphQL與Adobe Commerce通訊。 它也可讓AEM作者使用產品和類別選擇器以及產品主控台，來瀏覽隨選從Adobe Commerce擷取的產品和類別資料。 此外，CIF提供立即可用的店面，可加速商業專案。
thumbnail: aem-magento-architecture.jpg
exl-id: f843784c-5ff7-41d1-97c5-13facb8459b2
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%

---

# 使用Commerce integration framework整合AEM和Adobe Commerce (Magento) {#aem-commerce-framework}

使用Commerce integration framework(CIF)將Experience Manager與Adobe Commerce緊密整合。 CIF可讓AEM使用Adobe Commerce直接存取及與商務執行個體通訊 [GRAPHQL API](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
>最低支援的GraphQL API版本為2.3.5。只有較新版本或Adobe Commerce版本才支援某些功能。

## 架構概述 {#overview}

整體架構如下：

![CIF架構概述](../assets/AEM_Magento_Architecture.png)

CIF支援伺服器端和使用者端通訊模式。
伺服器端API呼叫是使用一般組建來實作 [GraphQL使用者端](https://github.com/adobe/commerce-cif-graphql-client) 與 [已產生資料模型集](https://github.com/adobe/commerce-cif-magento-graphql) 用於商務GraphQL結構描述。 此外，您也可以使用GQL格式的任何GraphQL查詢或變異。

對於使用者端元件，使用建置 [React](https://reactjs.org/)，則 [Apollo使用者端](https://www.apollographql.com/docs/react/) 已使用。

## AEM CIF核心元件架構 {#cif-core-components}

![AEM CIF核心元件架構](../assets/cif-component-architecture.jpg)

[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components) 遵循非常類似的設計模式和最佳實務作為 [AEM WCM核心元件](https://github.com/adobe/aem-core-wcm-components).

在Sling模型中實作用於AEM CIF核心元件的商業邏輯和與Adobe Commerce的後端通訊。 萬一需要自訂此邏輯以滿足專案特定的要求，可以使用Sling模型的委派模式。

>[!TIP]
>
>此 [自訂AEM CIF核心元件](../customizing/customize-cif-components.md) 頁面提供詳細範例和最佳實務，說明如何自訂CIF核心元件。

在專案中，AEM CIF核心元件和自訂專案元件可透過Sling內容感知設定，輕鬆擷取與AEM頁面相關聯之Adobe Commerce商店的已設定使用者端。
