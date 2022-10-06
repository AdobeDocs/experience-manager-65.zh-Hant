---
title: 移轉至AEM Commerce Integration Framework(CIF)附加元件
description: 如何從舊版移轉至AEM Commerce Integration Framework(CIF)附加元件
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 4%

---

# Experience Manager附加元件的移轉指南 {#cif-migration}

本指南有助於識別您需要更新哪些Experience Manager附加元件移轉作業。

## CIF附加元件

AEM 6.5可透過 [Software Distribution入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 它相容，且提供與CIF附加元件相同的功能，以提供Experience Manageras a Cloud Service。

請參閱 [AEM內容與商務快速入門](getting-started.md).

若要支援部署CIF的專案，Adobe提供 [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components).

## 產品目錄

CIF附加元件不支援匯入產品目錄資料。 使用CIF附加主體時，產品和目錄請求會透過對外部商務解決方案的即時呼叫，隨選提供。 請前往章節整合，深入了解如何整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則整合應使用具有API的外部產品快取。 範例 [Magento開放原始碼](https://business.adobe.com/products/magento/open-source.html).

## 透過AEM轉譯提供產品目錄體驗

如果您搭配Classic CIF使用目錄藍圖，則需要更新產品目錄工作流程。 CIF附加元件現在會使用AEM目錄範本即時轉譯產品目錄體驗。 不再需要複製產品資料或產品頁面。

## 無法快取的資料和購物互動

用戶端對無法快取的資料和互動（例如加到購物車、搜尋）的請求，應透過CDN/Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除AEM只是Proxy的任何呼叫。
