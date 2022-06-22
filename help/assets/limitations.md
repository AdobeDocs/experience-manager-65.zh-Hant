---
title: Dynamic Media限制
description: '瞭解建立映像集或旋轉集或上載PDF時的最佳做法和強制限制。 還瞭解Dynamic Media查看器不支援的Web瀏覽器和作業系統組合。 '
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
source-git-commit: cd3dcd0232e1ecf69c79b03ab960cfbfc283ee76
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# Dynamic Media限制

以下各節介紹Dynamic Media的限制。

本主題包括以下部分：

* Dynamic Media對資產類型的最佳做法和強制限制

<!-- * Unsupported web browser and operating system combinations for Dynamic Media Viewers -->

## Dynamic Media對資產類型的最佳做法和強制限制

在建立「旋轉集」或「映像集」或上載頁面提取PDF時，Adobe建議採用以下最佳做法並強制實施以下限制：

| 資產 — 限制類型 | 最佳實踐 | 已實現的限制 | 2022年12月31日限額變動 |
| --- | --- | --- | --- |
| **影像**  — 每個映像的智慧作物數 | 5 | 100 |  |
| **影像集**  — 每個集的重複資產數 | 無重複項 | 100 | 20 |
| **影像集**  — 每個集的最大影像數 | 每組5-10頁影像 | 1000 |
| **旋轉集**  — 每2D集的最大行/列數 | 每組12-18頁圖片 | 1000 |
| **PDF**  — 要考慮提取的PDF的最大頁數 |  | 5000（用於新上載） | 100 |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

<!-- ## Unsupported web browser and operating system combinations for Dynamic Media Viewers

Dynamic Media Viewers do not support following combinations of web browser and operating system.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 Update
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + macOS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + macOS X 10.10 Yosemite -->