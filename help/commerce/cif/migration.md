---
title: 移轉至AEMCommerce integration framework(CIF)附加元件
description: 如何從舊版移轉至AEMCommerce integration framework(CIF)附加元件。
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 5%

---

# Experience Manager附加元件的移轉指南 {#cif-migration}

本指南協助識別您需要為Experience Manager附加元件移轉更新的區域。

## CIF附加元件

CIF附加元件可透過[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)用於AEM 6.5。 它是相容的，提供和適用於Experience Manageras a Cloud Service的CIF附加元件相同的功能。

請參閱[AEM內容與Commerce快速入門](getting-started.md)。

為支援部署 CIF 的專案，Adobe 提供了 [AEM CIF 核心元件](https://github.com/adobe/aem-core-cif-components)。

## 產品目錄

CIF附加元件不支援匯入產品目錄資料。 使用CIF附加元件主體，產品與目錄請求是透過對外部商務解決方案的即時呼叫隨選的。 前往整合一章以進一步瞭解整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則應使用具有API的外部產品快取進行整合。 範例[Magento開放原始碼](https://business.adobe.com/products/magento/open-source.html)。

## 具有AEM轉譯的產品目錄體驗

如果您使用包含Classic CIF的目錄Blueprint，則需要更新產品目錄工作流程。 CIF附加元件現在會使用AEM目錄範本即時轉譯產品目錄體驗。 不再需要複製產品資料或產品頁面。

## 無法快取的資料與購物互動

對不可快取資料和互動的使用者端請求（例如加入購物車、搜尋）應透過CDN/Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除AEM只是Proxy的任何呼叫。
