---
title: 使用Commerce integration framework整合AEM和Adobe Commerce
description: 使用Commerce integration framework (CIF)將AEM與Adobe Commerce緊密整合。 CIF可讓AEM存取Adobe Commerce執行個體，並透過GraphQL與Adobe Commerce通訊。 它也可讓AEM作者使用產品和類別選擇器以及產品主控台，來瀏覽隨選從Adobe Commerce擷取的產品和類別資料。 此外，CIF提供立即可用的店面，可加速商業專案。
thumbnail: aem-magento-architecture.jpg
exl-id: f843784c-5ff7-41d1-97c5-13facb8459b2
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%

---

# 使用Commerce integration framework整合AEM和Adobe Commerce (Magento) {#aem-commerce-framework}

使用Commerce integration framework(CIF)將Experience Manager與Adobe Commerce緊密整合。 CIF可讓AEM使用Adobe Commerce的[GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/)直接存取及與商務執行個體通訊。

>[!NOTE]
>
>最低支援的GraphQL API版本為2.3.5。只有較新版本或Adobe Commerce版本才支援某些功能。

## 架構概述 {#overview}

整體架構如下：

![CIF架構概述](../assets/AEM_Magento_Architecture.png)

CIF支援伺服器端和使用者端通訊模式。
伺服器端API呼叫是使用內建一般[GraphQL使用者端](https://github.com/adobe/commerce-cif-graphql-client)，結合[商業用GraphQL結構描述的一組產生資料模型](https://github.com/adobe/commerce-cif-magento-graphql)實作。 此外，您也可以使用GQL格式的任何GraphQL查詢或變異。

對於使用[React](https://reactjs.org/)建置的使用者端元件，則使用[Apollo Client](https://www.apollographql.com/docs/react/)。

## AEM CIF核心元件架構 {#cif-core-components}

![AEM CIF核心元件架構](../assets/cif-component-architecture.jpg)

[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)遵循與[AEM WCM核心元件](https://github.com/adobe/aem-core-wcm-components)非常類似的設計模式和最佳實務。

在Sling模型中實作用於AEM CIF核心元件的商業邏輯和與Adobe Commerce的後端通訊。 萬一需要自訂此邏輯以滿足專案特定的要求，可以使用Sling模型的委派模式。

>[!TIP]
>
>[自訂AEM CIF核心元件](../customizing/customize-cif-components.md)頁面包含有關如何自訂CIF核心元件的詳細範例和最佳實務。

在專案中，AEM CIF核心元件和自訂專案元件可透過Sling內容感知設定，輕鬆擷取與AEM頁面相關聯之Adobe Commerce商店的已設定使用者端。
