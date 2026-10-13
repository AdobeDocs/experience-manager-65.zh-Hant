---
title: 移轉至AEM Commerce Integration Framework (CIF)附加元件
description: 如何從舊版移轉至AEM Commerce Integration Framework (CIF)附加元件。
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 5%
---
# Experience Manager附加元件的移轉指南 {#cif-migration}

本指南協助識別您需要為Experience Manager附加元件移轉進行更新的區域。

## CIF附加元件

可透過[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=commerce*&2_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3Aversion&2_group.propertyvalues.operation=equals&2_group.propertyvalues.0_values=target-version%3Aaem%2F6-5&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=16)取得AEM 6.5的CIF附加元件。 它是相容的，提供和適用於Experience Manager as a Cloud Service的CIF附加元件相同的功能。

請參閱[開始使用AEM內容和Commerce](getting-started.md)。

為支援部署 CIF 的專案，Adobe 提供了 [AEM CIF 核心元件](https://github.com/adobe/aem-core-cif-components)。

## 產品目錄

CIF附加元件不支援匯入產品目錄資料。 使用CIF附加元件主體，產品與目錄請求是透過對外部商務解決方案的即時呼叫隨選的。 前往整合一章以進一步瞭解整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則應使用具有API的外部產品快取進行整合。 範例[Magento open-source](https://business.adobe.com/products/magento/open-source.html)。

## AEM轉譯的產品目錄體驗

如果您使用包含Classic CIF的目錄Blueprint，則需要更新產品目錄工作流程。 CIF附加元件現在會使用AEM目錄範本即時轉譯產品目錄體驗。 不再需要複製產品資料或產品頁面。

## 無法快取的資料與購物互動

對不可快取資料和互動的使用者端請求（例如加入購物車、搜尋）應透過CDN/Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除AEM只是Proxy的任何呼叫。
