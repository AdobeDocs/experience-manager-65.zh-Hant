---
title: 移轉至AEM Commerce integration framework (CIF)附加元件
description: 如何從舊版移轉至AEM Commerce integration framework (CIF)附加元件。
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: b4056a4c1483dc8dcedc3c0f8f6b42f8dead0847
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 4%

---

# Experience Manager附加元件的移轉指南 {#cif-migration}

本指南協助識別您需要為Experience Manager附加元件移轉進行更新的區域。

## CIF附加元件

可透過[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=commerce*&amp;2_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3Aversion&amp;2_group.propertyvalues.operation=equals&amp;2_group.propertyvalues.0_values=target-version%3Aaem%2F6-5&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=16)取得AEM 6.5的CIF附加元件。 它是相容的，提供和適用於Experience Manager as a Cloud Service的CIF附加元件相同的功能。

請參閱[開始使用AEM內容和Commerce](getting-started.md)。

為支援部署 CIF 的專案，Adobe 提供了 [AEM CIF 核心元件](https://github.com/adobe/aem-core-cif-components)。

## 產品目錄

CIF附加元件不支援匯入產品目錄資料。 使用CIF附加元件主體，產品與目錄請求是透過對外部商務解決方案的即時呼叫隨選的。 前往整合一章以進一步瞭解整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則應使用具有API的外部產品快取進行整合。 範例[Magento開放原始碼](https://business.adobe.com/tw/products/magento/open-source.html)。

## AEM轉譯的產品目錄體驗

如果您使用包含Classic CIF的目錄Blueprint，則需要更新產品目錄工作流程。 CIF附加元件現在會使用AEM目錄範本即時轉譯產品目錄體驗。 不再需要複製產品資料或產品頁面。

## 無法快取的資料與購物互動

對不可快取資料和互動的使用者端請求（例如加入購物車、搜尋）應透過CDN/Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除AEM只是Proxy的任何呼叫。
