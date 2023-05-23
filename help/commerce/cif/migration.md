---
title: 遷移到AEMCommerce Integration Framework(CIF)附加項
description: 如何從舊版AEM本遷移到Commerce Integration Framework(CIF)附加模組
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 4%

---

# Experience Manager載入項遷移指南 {#cif-migration}

本指南幫助確定需要更新的Experience Manager附加遷移區域。

## CIF附加模組

CIF附加模組可AEM通過 [軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。 它相容，提供與Experience Manageras a Cloud Service的CIF附加模組相同的功能。

請參閱 [內容和商AEM務入門](getting-started.md)。

要支援部署CIF的項目，Adobe提供 [AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components)。

## 產品目錄

CIF載入項不支援導入產品目錄資料。 使用CIF附加主體，產品和目錄請求通過即時呼叫外部商業解決方案而按需提供。 請轉至「整合」一章，瞭解有關整合商務解決方案的詳細資訊。

>[!TIP]
>
>如果沒有可用的即時API，則應使用帶API的外部產品快取進行整合。 示例 [Magento開源](https://business.adobe.com/products/magento/open-source.html)。

## 使用渲染的產品目錄體AEM驗

如果將目錄藍圖與經典CIF一起使用，則需要更新產品目錄工作流。 CIF附加模組現在使用目錄模板即時提供產品目AEM錄體驗。 不再需要複製產品資料或產品頁。

## 不可快取資料與購物互動

客戶端請求不可快取的資料和交互（例如，添加到購物車、搜索）應通過CDN/Dispatcher直接轉到商業終結點（商業解決方案或整合層）。 刪除僅是代AEM理的任何呼叫。
