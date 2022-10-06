---
title: 個人化和內容鎖定
seo-title: Personalization and Content Targeting
description: 了解AEM如何建立個人化內容
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
ht-degree: 1%

---

# 個人化和內容鎖定 {#personalization}

## 個人化和內容鎖定 {#personalization-and-content-targeting}

AEM提供工具架構，用於編寫目標內容及呈現個人化體驗。

## 定位模式 {#targeting-mode}

[製作目標內容](/help/sites-authoring/content-targeting-touch.md) 使用AEM的目標定位模式。 定位模式和Target元件提供工具，用於建立行銷活動體驗的內容。

## 活動 {#activities}

活動可定義並組織您的行銷工作。 活動包含您要鎖定的對象，以及套用鎖定目標的時段。

例如，We.Retail產品目錄包含茶匙，它們關注季節性產品。 「夏季運動」活動會定義茶具在夏季月份鎖定的行銷區段。

活動也會識別 [目標引擎](/help/sites-authoring/personalization.md#targeting-engine) 頁面所使用。

使用 [活動主控台](/help/sites-authoring/activitylib.md) 來建立和管理您品牌的活動。 您也可以像您一樣建立活動 [作者目標內容](/help/sites-authoring/content-targeting-touch.md).

## 體驗 {#experiences}

您會針對每個活動定義一或多個體驗，以識別您要鎖定的對象。 AEM可讓您控制包含每個體驗的內容。

受眾是根據在AEM或Adobe Target中建立的行銷區段。 訪客開啟網頁時，頁面邏輯會決定其所屬的對象，並顯示您為該對象建立的內容。

例如，活動會定義兩個不同對象的體驗：30歲以上婦女和30歲以下婦女。 We.Retail網站的「女性」頁面會針對每個體驗顯示不同的產品。

您定義活動的體驗。 您可以使用 [活動主控台](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) 或 [定位模式](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) 將體驗新增至活動。

## 選件 {#offers}

選件是顯示在體驗之頁面上某個位置的內容。 針對不同的體驗使用不同的選件，以最大化內容對對象的效益。

例如，We.Retail範例網站的「女性」頁面可以使用選件作為預告影像，顯示在頁面頂端。 另一個優惠方案則用作30歲以上女性體驗和30歲以下女性體驗的預告。

使用 [選件主控台](/help/sites-authoring/offerlib.md) 來建立可在多個體驗中使用的選件。 建立單一使用選件，或在 [製作目標內容](/help/sites-authoring/content-targeting-touch.md).

## 定位引擎 {#targeting-engine}

定位引擎是驅動目標內容邏輯的機制。 [活動](/help/sites-authoring/activitylib.md) 已設定為使用兩個可用定位引擎之一：AEM和Adobe Target。

### AEM {#aem}

AEM提供內建的定位引擎，可處理頁面要求並決定要顯示的內容。 使用AEM定位引擎時，您只能使用在AEM中建立的區段來定義體驗的對象。

### Adobe Target {#adobe-target}

Adobe Target定位引擎會使從頁面造訪收集到的資訊在Adobe Target中受到追蹤。

* 使用此定位引擎時，您會使用從Adobe Target匯入的區段來定義體驗的對象。
* 使用Adobe Target引擎的活動包括 [已同步到Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

若您有 [與Adobe Target整合](/help/sites-administering/opt-in.md).
