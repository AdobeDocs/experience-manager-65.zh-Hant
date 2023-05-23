---
title: Dynamic Media 限制
description: 瞭解建立映像集或旋轉集或上載PDF時的最佳做法和強制限制。 還瞭解Dynamic Media不支援的Web瀏覽器和作業系統組合。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
source-git-commit: 9247a81a518b1bd6e037c234a6c67f95209bfde8
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 3%

---

# Dynamic Media限制

以下各節介紹Dynamic Media的限制。

本主題包括以下部分：

* [Dynamic Media對資產類型的最佳做法和強制限制](#best-practice-enforced-limits)
* [不支援的Web瀏覽器和作業系統組合，適用於Dynamic Media](#unsupported-browser-os)

## Dynamic Media對資產類型的最佳做法和強制限制 {#best-practice-enforced-limits}

在建立「旋轉集」或「映像集」或上載頁面提取PDF時，Adobe建議採用以下最佳做法並強制實施以下限制：

| 資產 — 限制類型 | 最佳實踐 | 強加的限制 |
| --- | --- | --- |
| **影像**  — 每個映像的智慧作物數 | 5 | 100 |
| **所有集**  — 每個集的重複資產數 | 無重複項 | 20 |
| **所有集**  — 每組資產的最大數量 | 每組5-10頁影像 | 1000 |
| **旋轉集**  — 每2D集的最大行/列數 | 每組12-18頁圖片 | 1000 |
| **PDF**  — 要考慮提取的PDF的最大頁數 |  | 100(所有PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## 不支援的Web瀏覽器和作業系統組合，適用於Dynamic Media {#unsupported-browser-os}

Dynamic Media不支援以下Web瀏覽器和作業系統組合。

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1更新
* Safari 6 +iOS6.0.1
* Safari 7 +iOS7.1
* Safari 7 + OS X 10.9小牛隊
* Safari 8 +iOS8.4
* Safari 8 + OS X 10.10 Yosemite

<!-- ## End of support for TLS 1.0 and 1.1 {#tls}

CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022)

Effective September 30, 2022, Adobe Dynamic Media will end support for the following:

* TLS (Transport Layer Security) 1.0 and 1.1
* The following weak ciphers in TLS 1.2:
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_RSA_WITH_AES_256_GCM_SHA384`
  * `TLS_RSA_WITH_AES_256_CBC_SHA256`
  * `TLS_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_AES_128_GCM_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
  * `TLS_RSA_WITH_SDES_EDE_CBC_SHA` -->

