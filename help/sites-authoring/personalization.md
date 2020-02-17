---
title: 個人化與內容定位
seo-title: 個人化與內容定位
description: 瞭解AEM如何建立個人化內容
seo-description: 瞭解AEM如何建立個人化內容
uuid: 3a1aaa3d-5f57-4fb7-a4be-523f0d274b79
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 850da0da-f7c3-4dd7-bb06-404c14a2a791
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 個人化與內容定位 {#personalization}

## 個人化與內容定位 {#personalization-and-content-targeting}

AEM提供工具架構，以製作目標內容並呈現個人化體驗。

## 定位模式 {#targeting-mode}

[使用AEM的「定位](/help/sites-authoring/content-targeting-touch.md) 」模式來製作目標內容。 定位模式和Target元件提供工具，讓您建立行銷活動體驗的內容。

## 活動 {#activities}

活動可定義並組織您的行銷工作。 活動包括您要定位的對象，以及套用定位的時段。

例如，We.Retail產品目錄包含的茶具會著重於季節性產品。 「夏季運動」活動定義了茶具在夏季月份鎖定的行銷區段。

活動也會識別 [您的頁面](/help/sites-authoring/personalization.md#targeting-engine) 所使用的定位引擎。

使用「 [活動」主控台](/help/sites-authoring/activitylib.md) ，建立並管理您品牌的活動。 您也可以在製作目標內容時 [建立活動](/help/sites-authoring/content-targeting-touch.md)。

## 體驗 {#experiences}

針對每個活動，您定義一或多個體驗，以識別您所鎖定的對象。 AEM可讓您控制包含每個體驗的內容。

觀眾是以在AEM或Adobe target中建立的行銷區段為基礎。 當訪客開啟網頁時，頁面邏輯會決定其所屬的對象，並顯示您為該對象建立的內容。

例如，活動會定義兩個不同對象的體驗：30歲以上婦女和30歲以下婦女。 We.Retail網站的「女性」頁面會針對每個體驗顯示不同的產品。

您定義活動的體驗。 您可以使用「活 [動」主控台](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) 或「 [定位」模式](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) ，將體驗新增至活動。

## 選件 {#offers}

選件是顯示在頁面上體驗位置的內容。 針對不同的體驗使用不同的選件，為您的受眾提供最佳的內容效果。

例如，We.Retail範例網站的「女性」頁面可以使用選件作為顯示在頁面頂端的摘要影像。 不同的選件會用作「女性30歲以上（女性30歲以下）」體驗和「女性30歲以下（女性30歲以下）」體驗的摘要。

使用選 [件主控台](/help/sites-authoring/offerlib.md) ，建立可用於多個體驗的選件。 在製作目標內容時，從選件程式庫建立單一用途的選件或 [新增選件](/help/sites-authoring/content-targeting-touch.md)。

## Targeting Engine {#targeting-engine}

定位引擎是驅動定位內容邏輯的機制。 [活動](/help/sites-authoring/activitylib.md) 」設定為使用兩個可用的定位引擎之一：AEM和Adobe Target。

### AEM {#aem}

AEM提供內建定位引擎，可處理頁面請求並決定要顯示的內容。 使用AEM定位引擎時，您只能使用在AEM中建立的區段來定義體驗的觀眾。

### Adobe Target {#adobe-target}

Adobe target定位引擎會在Adobe target中追蹤從頁面瀏覽收集到的資訊。

* 使用此定位引擎時，您會使用從Adobe Target匯入的區段來定義體驗的觀眾。
* 使用Adobe target引擎的活動會 [同步至Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target)。

當您與Adobe Target整合時， [即可使用此引擎](/help/sites-administering/opt-in.md)。
