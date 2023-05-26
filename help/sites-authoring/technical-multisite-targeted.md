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
ht-degree: 10%

---

# 如何架構目標內容的多網站管理{#how-multisite-management-for-targeted-content-is-structured}

下圖顯示如何架構目標內容的多網站支援。

區域會顯示在下方 **/content/campaigns/&lt;brand>** 依預設，每個品牌都有一個自動建立的主版區域。 每個區域都包含自己的一組活動、體驗和選件。

![chlimage_1-268](assets/chlimage_1-268.png)

若要查詢目標內容，頁面或網站可對應至某個區域。 如果沒有設定區域，AEM會退回此特定品牌的主區域。

下圖是三個網站（稱為site1、site2和site3）的邏輯運作方式範例。

![chlimage_1-269](assets/chlimage_1-269.png)

* site1會根據區域對應來查詢myarea1以取得brand1，並查詢otherarea2以取得brand2。
* 網站2會查詢myarea1 for brand1和master area for brand2 ，因為只定義brand1的區域對應。
* 網站3會查詢brand1和brand2的主要區域，因為此網站完全沒有定義其他區域對應。
