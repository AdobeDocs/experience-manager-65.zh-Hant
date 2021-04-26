---
title: 利AEM用商務整合框架實現第三方商務整合
description: 企業可能需要額外的第三方商務解決方案來支撐其店面。 商務整合框架(CIF)可用於此類整合情境，以便使用I/O Runtime將第三方商務解決方案連接至Adobe Experience Manager。
thumbnail: cif-third-party-architecture.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# 和使AEM用Commerce Integration Framework {#aem-third-party}的第三方商務整合

非Adobe商務解決方案的整合是CIF的常見情況。 使用不同API和結構描述的協力廠商解決方案可透過整合層連結。

## 架構 {#architecture}

總體架構如下：

![非AEMMagento/第三方體系結構概述](../assets//AEM_nonMagento_Architecture.png)

此整合層的目的是將第三方API和結構描述映射到Adobe之外的支援的Experience ManagerCommerce GraphQL API和結構描述。 有了這種封裝，整合邏輯和系統就可以更新，而不需變更Experience Manager內的程式碼。

## 整合的解決方案需求

當Experience Manager擷取隨選資料時，需要即時的產品目錄API。

>[!TIP]
>
>如果沒有可用的即時API，則應使用含API的外部產品快取進行整合。 示例[Magentoopen-source](https://magento.com/products/magento-open-source)。

無需實施完整的GraphQL模式，只要模式的對象，即可啟用所需的使用案例。

## 後端使用案例

CIF通過即時產品目錄訪問和產品體驗管理工具擴展了Experience Manager. 此順暢整合可讓作者在需要時使用內嵌的UI來存取商務資料，而不需離開內容內容內容。

必須整合產品目錄API才能解除這些使用案例的鎖定。

## 前端使用案例

[AEMCIF核心元](https://github.com/adobe/aem-core-cif-components) 件透過CIF支援的Adobe商務API擷取和交換資料。若要重複使用元件，必須實作個別的API。

效能關鍵的客戶端元件建議直接與第三方解決方案通信，以避免延遲。

## 開發整合{#develop-integration}

我們建議使用[Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)作為整合層。 它包括在CIF第三方的附加產品中。 當它與類似微服務的方法搭配運作時，它非常適合於輕鬆整合多種解決方案。

[參考實作](https://github.com/adobe/commerce-cif-graphql-integration-reference)是建立與商務解決方案整合的絕佳起點。 雖然它支援GraphQL，但也可以與任何其他類型的API（例如REST）整合。

如果有第三方層可用（例如Mulesoft）或將整合內建在第三方解決方案之上，則不需要此整合層。
