---
title: 如何架構目標內容的多網站管理
description: 圖表顯示如何架構目標內容的多網站支援
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 11%
---
# 如何架構目標內容的多網站管理{#how-multisite-management-for-targeted-content-is-structured}

下圖顯示如何架構目標內容的多網站支援。

**/content/campaigns/&lt;brand>**&#x200B;下方會顯示區域，依預設，每個品牌都有自動建立的主區域。 每個區域都包含自身的一組活動、體驗和選件。

![chlimage_1-268](assets/chlimage_1-268.png)

若要查詢目標內容，頁面或網站可以對應至某個區域。 如果沒有設定區域，AEM會退回此特定品牌的主區域。

下圖是該邏輯如何為三個網站（稱為site1、site2及site3）運作的範例。

![chlimage_1-269](assets/chlimage_1-269.png)

* 網站1會根據區域對應查詢myarea1以尋找brand1，並查詢otherarea2以尋找brand2。
* 網站2會查詢brand1的myarea1和brand2的主區域，因為只有brand1的區域對應已定義。
* 網站3會查詢brand1和brand2的主要區域，因為此網站完全沒有定義其他區域對應。
