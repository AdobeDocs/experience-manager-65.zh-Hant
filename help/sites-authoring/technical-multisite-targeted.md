---
title: 如何架構目標內容的多網站管理
seo-title: How Multisite Management for Targeted Content is Structured
description: 圖表顯示了如何構建對目標內容的多站點支援
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

下圖顯示了如何構建對目標內容的多站點支援。

下面顯示區域 **/內容/活動/&lt;brand>** 預設情況下，每個品牌都有一個主區域，該主區域會自動建立。 每個區域都有自己的活動、經驗和優惠。

![chlimage_1-268](assets/chlimage_1-268.png)

要查找目標內容，頁面或站點可以映射到區域。 如果未配置區域，AEM則返回到此特定品牌的主區域。

下圖是邏輯在三個站點（稱為site1 、 site2和site3）中如何工作的示例。

![chlimage_1-269](assets/chlimage_1-269.png)

* site1根據區域映射查找brand1的myarea1和brand2的其它區域2。
* site2查找brand1的myarea1和brand2的主區域，因為只定義了brand1的區域映射。
* site3查找brand1和brand2的主區域，因為根本沒有為此站點定義其他區域映射。
