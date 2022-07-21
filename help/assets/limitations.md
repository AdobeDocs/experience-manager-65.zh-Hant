---
title: Dynamic Media限制
description: 瞭解建立映像集或旋轉集或上載PDF時的最佳做法和強制限制。 還瞭解Dynamic Media查看器不支援的Web瀏覽器和作業系統組合。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
source-git-commit: d4eae7774cb657713a06261deeef0fd2ad542836
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 4%

---

# Dynamic Media限制

以下各節介紹Dynamic Media的限制。

本主題包括以下部分：

* [Dynamic Media對資產類型的最佳做法和強制限制](#best-practice-enforced-limits)
* [不支援的Web瀏覽器和Dynamic Media查看器的作業系統組合](#unsupported-browser-os)

## Dynamic Media對資產類型的最佳做法和強制限制 {#best-practice-enforced-limits}

在建立「旋轉集」或「映像集」或上載頁面提取PDF時，Adobe建議採用以下最佳做法並強制實施以下限制：

| 資產 — 限制類型 | 最佳實踐 | 強加的限制 | 2022年12月31日變更上限 |
| --- | --- | --- | --- |
| **影像**  — 每個映像的智慧作物數 | 5 | 100 | 20 |
| **所有集**  — 每個集的重複資產數 | 無重複項 | 20 | 不適用 |
| **所有集**  — 每組資產的最大數量 | 每組5-10頁影像 | 1000 | 不適用 |
| **旋轉集**  — 每2D集的最大行/列數 | 每組12-18頁圖片 | 1000 | 不適用 |
| **PDF**  — 要考慮提取的PDF的最大頁數 |  | 5000（用於新上載） | 100(所有PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## 不支援的Web瀏覽器和Dynamic Media查看器的作業系統組合 {#unsupported-browser-os}

Dynamic Media查看器不支援以下Web瀏覽器和作業系統組合。

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1更新
* Safari 6 +iOS6.0.1
* Safari 7 +iOS7.1
* Safari 7 + OS X 10.9小牛隊
* Safari 8 +iOS8.4
* Safari 8 + OS X 10.10 Yosemite
