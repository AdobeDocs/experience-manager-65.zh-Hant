---
title: 移轉至AEM Commerce Integration Framework(CIF)附加元件
description: 如何從舊版移轉至AEM Commerce Integration Framework(CIF)附加元件
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Experience Manager附加元件{#cif-migration}的遷移指南

本指南有助於識別您需要更新哪些Experience Manager附加元件移轉作業。

## CIF附加元件

AEM 6.5可透過[Software Distribution portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)使用CIF附加元件。 與CIF附加元件相容，且提供的功能與Experience ManagerCloud Service相同。

請參閱[AEM內容與商務快速入門](getting-started.md)。

若要支援部署CIF的專案，「Adobe」提供[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)。

## 產品目錄

CIF附加元件不支援匯入產品目錄資料。 使用CIF附加主體時，產品和目錄請求會透過對外部商務解決方案的即時呼叫，隨選提供。 請前往章節整合，深入了解如何整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則整合應使用具有API的外部產品快取。 範例[Magento開放原始碼](https://magento.com/products/magento-open-source)。

## 透過AEM轉譯提供產品目錄體驗

如果您搭配Classic CIF使用目錄藍圖，則需要更新產品目錄工作流程。 CIF附加元件現在會使用AEM目錄範本即時轉譯產品目錄體驗。 不再需要複製產品資料或產品頁面。

## 無法快取的資料和購物互動

用戶端對無法快取的資料和互動（例如加到購物車、搜尋）的請求，應透過CDN/Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除AEM只是Proxy的任何呼叫。
