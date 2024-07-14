---
title: 電子商務概觀
description: AEM一般電子商務是作為標準安裝的一部分提供，為您提供電子商務框架的完整功能。
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 2%

---

# 電子商務概觀{#ecommerce-overview}

AEM一般電子商務是作為標準安裝的一部分提供，為您提供電子商務架構的完整功能。

Adobe提供兩個版本的Commerce integration framework：

|                         | CIF內部部署 | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 支援的 AEM 版本 | AEM內部部署或AMS 6.x | AEM AMS 6.4和6.5 |
| 後端 | - AEM， Java™ <br> — 整體整合，建置前對應（範本）<br> - JCR存放庫 | - Adobe Commerce <br>- Java和JavaScript <br> — 沒有儲存在JCR存放庫中的Commerce資料 |
| 前端 | AEM伺服器端轉譯頁面 | 混合頁面應用程式（混合呈現） |
| 產品目錄 | - AEM <br>中的產品匯入工具、編輯器、快取 — 具有AEM或Proxy頁面的一般目錄 |  — 無產品匯入<br> — 通用範本<br> — 透過聯結器的隨選資料 |
| 擴充性 |  — 最多可支援幾百萬項產品（取決於使用案例） <br> — 在Dispatcher上快取 |  — 無磁碟區限制<br> — 在Dispatcher或CDN上快取 |
| 標準化資料模型 | 否 | 是，Adobe Commerce GraphQL結構描述 |
| 可用性 | 是：<br> - SAPCommerce Cloud(擴充功能已更新，以支援AEM 6.4和Hybris 5 （預設）)，並維持與Hybris 4 <br>- SalesforceCommerce Cloud的相容性(聯結器開放來源以支援AEM 6.4) | 是，透過GitHub的開放原始碼。 <br> Adobe Commerce (支援2.3.2 （預設）並與2.3.1相容)。 |
| 使用時機 | 有限的使用案例：針對小型案例，視需要匯入靜態目錄 | 大部分使用案例中偏好的解決方案 |


## 部署其他實作 {#deploying-other-implementations}

若為AEM和Adobe Commerce，請參閱[使用[Commerce integration framework](/help/commerce/cif/introduction.md)的AEM和Adobe Commerce整合](/help/commerce/cif/integrating/magento.md)。

>[!NOTE]
>
>如需有關概念和管理電子商務實作的資訊，請參閱[管理電子商務](/help/commerce/cif-classic/administering/ecommerce.md)。
>
>如需有關擴充電子商務功能的資訊，請參閱[開發電子商務](/help/commerce/cif-classic/developing/ecommerce.md)。
