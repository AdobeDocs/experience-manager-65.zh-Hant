---
title: 如何架構目標內容的多網站管理
seo-title: How Multisite Management for Targeted Content is Structured
description: 圖表顯示如何架構目標內容的多網站支援
seo-description: A diagram shows how multisite support for targeted content is structured
uuid: 2d30cdf0-ab77-490d-aac0-db3a0d417a58
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 7dd851ab-3fa7-426e-89cb-08b67e9b5999
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 9%

---

# 如何架構目標內容的多網站管理{#how-multisite-management-for-targeted-content-is-structured}

下圖顯示如何架構目標內容的多網站支援。

區域顯示在下方 **/content/campaigns/&lt;brand>** 預設情況下，每個品牌都有自動建立的主版區域。 每個區域都包含其專屬的活動、體驗和選件集。

![chlimage_1-268](assets/chlimage_1-268.png)

若要尋找目標內容，頁面或網站可對應至某個區域。 如果未設定任何區域，AEM會回復至此特定品牌的主版區域。

下圖為邏輯在三個網站（稱為site1、site2和site3）中如何運作的範例。

![chlimage_1-269](assets/chlimage_1-269.png)

* site1會根據區域對應，為brand1尋找myarea1，為brand2尋找otherarea2。
* site2會針對brand1查詢myarea1，並針對brand2查詢主版區域，因為只定義brand1的區域對應。
* site3會查找brand1和brand2的主版區域，因為此網站完全未定義其他區域對應。
