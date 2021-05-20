---
title: AEM與Adobe商務(Magento)整合（使用Commerce Integration Framework）
description: AEM和Adobe商務(Magento)可透過Commerce Integration Framework(CIF)順暢地整合。 CIF可讓AEM存取Magento執行個體，並透過GraphQL與Magento通訊。 此外，AEM作者也可使用產品和類別選擇器，以及產品主控台來瀏覽從Magento依需求擷取的產品和類別資料。 此外，CIF提供現成可加速商業項目的店面。
thumbnail: aem-magento-architecture.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 1%

---

# AEM與Adobe商務(Magento)整合使用Commerce Integration Framework {#aem-magento-framework}

Experience Manager與Adobe商務(Magento)可透過商務整合架構(CIF)順暢整合。 CIF可讓AEM使用Commerce的[GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/)直接存取及與商務執行個體通訊。

## 架構概述 {#overview}

整體架構如下：

![CIF架構概觀](../assets/AEM_Magento_Architecture.png)

CIF內支援伺服器端和用戶端通訊模式。
伺服器端API呼叫是使用內建的通用[GraphQL用戶端](https://github.com/adobe/commerce-cif-graphql-client)，並結合商務GraphQL架構的[一組產生的資料模型](https://github.com/adobe/commerce-cif-magento-graphql)來實作。 此外，還可以使用GQL格式的任何GraphQL查詢或變異。

對於使用[React](https://reactjs.org/)建立的用戶端元件，會使用[Apollo Client](https://www.apollographql.com/docs/react/)。

## AEM CIF核心元件架構{#cif-core-components}

![AEM CIF核心元件架構](../assets/cif-component-architecture.jpg)

[AEM CIF核心元](https://github.com/adobe/aem-core-cif-components) 件遵循與AEM WCM核心元件非常類似的設計 [模式和最佳實務](https://github.com/adobe/aem-core-wcm-components)。

AEM CIF核心元件的商業邏輯和與Adobe商務的後端通訊會在Sling模型中實作。 如果您需要自訂此邏輯以符合專案特定需求，則可使用Sling模型的委派模式。

>[!TIP]
>
>[自訂AEM CIF核心元件](../customizing/customize-cif-components.md)頁面提供如何自訂CIF核心元件的詳細範例和最佳實務。

在專案中，AEM CIF核心元件和自訂專案元件可透過Sling內容感知設定，輕鬆擷取與AEM頁面相關聯的Adobe商務存放區所設定的用戶端。
