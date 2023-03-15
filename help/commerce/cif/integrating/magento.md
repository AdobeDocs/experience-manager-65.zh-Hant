---
title: AEM與Adobe Commerce使用Commerce Integration Framework整合
description: AEM和Adobe Commerce可透過Commerce Integration Framework(CIF)順暢整合。 CIF可讓AEM存取Adobe Commerce執行個體，並透過GraphQL與Adobe Commerce通訊。 此外，AEM作者也可以使用產品和類別選擇器，以及產品主控台，瀏覽從Adobe Commerce依需求擷取的產品和類別資料。 此外，CIF提供現成可加速商業項目的店面。
thumbnail: aem-magento-architecture.jpg
exl-id: f843784c-5ff7-41d1-97c5-13facb8459b2
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---

# AEM與Adobe Commerce(Magento)使用Commerce Integration Framework整合 {#aem-commerce-framework}

Experience Manager與Adobe Commerce可透過Commerce Integration Framework(CIF)順暢整合。 CIF可讓AEM使用Adobe Commerce直接存取商務執行個體並與其通訊 [GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
>最低支援的GraphQL API版本為2.3.5。某些功能僅支援較新版本，或僅支援Adobe Commerce版本。

## 架構概述 {#overview}

整體架構如下：

![CIF架構概觀](../assets/AEM_Magento_Architecture.png)

CIF內支援伺服器端和用戶端通訊模式。
伺服器端API呼叫是使用內建的一般實作 [GraphQL用戶端](https://github.com/adobe/commerce-cif-graphql-client) 與 [生成的資料模型集](https://github.com/adobe/commerce-cif-magento-graphql) (商務GraphQL結構)。 此外，還可以使用GQL格式的任何GraphQL查詢或變異。

針對使用 [React](https://reactjs.org/), [阿波羅客戶](https://www.apollographql.com/docs/react/) 中所有規則的URL區段。

## AEM CIF核心元件架構 {#cif-core-components}

![AEM CIF核心元件架構](../assets/cif-component-architecture.jpg)

[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components) 遵循與 [AEM WCM核心元件](https://github.com/adobe/aem-core-wcm-components).

AEM CIF核心元件與Adobe Commerce的商業邏輯和後端通訊是在Sling模型中實作。 如果您需要自訂此邏輯以符合專案特定需求，則可使用Sling模型的委派模式。

>[!TIP]
>
>此 [自訂AEM CIF核心元件](../customizing/customize-cif-components.md) 頁面提供自訂CIF核心元件的詳細範例和最佳實務。

在專案中，AEM CIF核心元件和自訂專案元件可透過Sling內容感知設定，輕鬆擷取與AEM頁面相關聯的Adobe Commerce存放區所設定的用戶端。
