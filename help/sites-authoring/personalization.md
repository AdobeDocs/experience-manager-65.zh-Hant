---
title: 個人化和內容目標鎖定
seo-title: Personalization and Content Targeting
description: 瞭解如何AEM建立個性化內容
seo-description: Learn how AEM can create personalized content
uuid: 3a1aaa3d-5f57-4fb7-a4be-523f0d274b79
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 850da0da-f7c3-4dd7-bb06-404c14a2a791
exl-id: be34760a-875b-419d-9fa4-2359b314a3b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 27%

---

# 個人化和內容目標鎖定 {#personalization}

## 個人化和內容目標鎖定 {#personalization-and-content-targeting}

提AEM供用於創作目標內容和呈現個性化體驗的工具框架。

## 目標模式 {#targeting-mode}

[作者目標內容](/help/sites-authoring/content-targeting-touch.md) 使用的目標模式AEM。 目標定位模式和目標元件提供用於建立行銷活動體驗內容的工具。

## 活動 {#activities}

活動定義和組織您的營銷工作。 活動包括您所針對的受眾以及應用目標的時間段。

例如，We.Retail產品目錄包含關注季節性產品的茶具。 夏季體育活動定義了茶具在夏季月份瞄準的市場細分。

活動還確定 [目標引擎](/help/sites-authoring/personalization.md#targeting-engine) 你的頁面所用。

使用 [活動控制台](/help/sites-authoring/activitylib.md) 建立和管理品牌的活動。 您還可以建立活動 [作者目標內容](/help/sites-authoring/content-targeting-touch.md)。

## 體驗 {#experiences}

對於每個活動，您都定義一個或多個體驗，這些體驗標識您所針對的受眾。 使您AEM能夠控制包含每種體驗的內容。

觀眾基於在Adobe Target或建立的營AEM銷部門。 當訪問者開啟網頁時，頁面邏輯將確定他們所屬的訪問群體並顯示您為該訪問群體建立的內容。

例如，活動定義兩個不同受眾的體驗：30歲以上婦女和30歲以下婦女。 We.Retail網站的Women&#39;s頁顯示每種體驗的不同產品。

定義活動的體驗。 您可以使用 [活動控制台](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) 或 [目標模式](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) 向活動添加體驗。

## 優惠 {#offers}

優惠是顯示在頁面上某個位置以獲得體驗的內容。 使用不同的服務來提供不同的體驗，以最大限度地提高內容對受眾的效率。

例如，We.Retail示例網站的「婦女」頁面可以將優惠用作顯示在頁面頂部的誘惑影像。 對於30歲以上的女性和30歲以下的女性，則採用不同的報價作為誘惑。

使用 [提供控制台](/help/sites-authoring/offerlib.md) 建立可在多種體驗中使用的優惠。 在以下情況下建立一次性優惠或從優惠庫中添加優惠 [創作目標內容](/help/sites-authoring/content-targeting-touch.md)。

## 目標定位引擎 {#targeting-engine}

目標引擎是驅動目標內容邏輯的機制。 [活動](/help/sites-authoring/activitylib.md)設定為使用兩個可用的目標定位引擎之一：AEM 和 Adobe Target。

### AEM {#aem}

提AEM供一個內置目標引擎，用於處理頁面請求並確定要顯示的內容。 使用 AEM 目標定位引擎時，您只能使用在 AEM 建立的區段來定義體驗的對象。

### Adobe Target {#adobe-target}

Adobe Target 目標定位引擎會使頁面被造訪時所收集的資訊在 Adobe Target 中被追蹤。

* 使用此目標定位引擎時，您可以使用從 Adobe Target 匯入的區段來定義體驗的對象。
* 使用 Adobe Target 引擎的活動[會同步到 Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target)。

如果[已整合 Adobe Target](/help/sites-administering/opt-in.md)，即可使用此引擎。
