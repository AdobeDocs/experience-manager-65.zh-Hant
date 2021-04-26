---
title: 移轉至AEMCommerce Integration Framework(CIF)附加元件
description: 如何從舊版移AEM轉至Commerce Integration Framework(CIF)附加元件
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# {#cif-migration}Experience Manager附加元件的遷移指南

本指南可協助您識別Experience Manager附加移轉需要更新的區域。

## CIF附加元件

CIF附加元件可AEM通過[軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)獲得6.5版。 它相容，提供與Experience ManagerCIF附加元件相同的功能，與Cloud Service。

請參閱[內容與商AEM務快速入門](getting-started.md)。

要支援部署CIFAdobe的項目，請提供[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)。

## 產品目錄

CIF附加元件不支援匯入產品目錄資料。 使用CIF附加原則，產品與型錄要求是透過對外部商務解決方案的即時呼叫隨選。 請至「整合」一章，進一步瞭解整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則應使用含API的外部產品快取進行整合。 示例[Magentoopen-source](https://magento.com/products/magento-open-source)。

## 產品型錄體驗與轉AEM譯

如果您搭配使用Classic CIF的型錄藍圖，就需要更新產品型錄工作流程。 CIF附加元件現在使用型錄範本即時轉換產品型AEM錄體驗。 您不再需要複製產品資料或產品頁面。

## 無法快取的資料與購物互動

用戶端要求不可快取的資料和互動（例如，新增至購物車、搜尋）應透過CDN/Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除只是代理AEM的任何呼叫。
