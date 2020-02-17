---
title: 目標內容的多網站管理結構
seo-title: 目標內容的多網站管理結構
description: 圖表顯示多網站對目標內容的支援結構
seo-description: 圖表顯示多網站對目標內容的支援結構
uuid: 2d30cdf0-ab77-490d-aac0-db3a0d417a58
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 7dd851ab-3fa7-426e-89cb-08b67e9b5999
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 目標內容的多網站管理結構{#how-multisite-management-for-targeted-content-is-structured}

下圖說明如何建構針對目標內容的多網站支援。

區域會出現在 **/content/campaigns/&lt;brand>下方** ，而且依預設，每個品牌都有一個主區域，會自動建立。 每個區域都包含其專屬的活動、體驗和選件集。

![chlimage_1-268](assets/chlimage_1-268.png)

若要尋找目標內容，頁面或網站可對應至某個區域。 如果沒有設定區域，AEM會回到此特定品牌的主要區域。

下圖為邏輯在三個網站（稱為site1、site2和site3）上運作的範例。

![chlimage_1-269](assets/chlimage_1-269.png)

* site1會根據區域對應，針對brand1尋找myarea1，針對brand2尋找其他區域2。
* site2會針對brand1尋找myarea1，並針對brand2尋找主要區域，因為只定義了brand1的區域對應。
* site3會為brand1和brand2尋找主要區域，因為此網站完全未定義其他區域對應。

