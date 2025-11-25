---
title: 個人化和內容目標鎖定
description: 瞭解Adobe Experience Manager 6.5如何建立個人化內容。
exl-id: be34760a-875b-419d-9fa4-2359b314a3b7
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 23%

---

# 個人化和內容目標鎖定 {#personalization}

## 個人化和內容目標鎖定 {#personalization-and-content-targeting}

AEM提供工具架構，用於製作目標內容和呈現個人化體驗。

## 目標定位模式 {#targeting-mode}

[使用AEM的鎖定模式製作鎖定內容](/help/sites-authoring/content-targeting-touch.md)。 目標定位模式和目標元件提供用於建立行銷活動體驗內容的工具。

## 活動 {#activities}

活動會定義並組織您的行銷工作。 活動包含您正在定位的對象，以及套用定位的時段。

例如，We.Retail產品目錄包含著重季節性產品的Teaser。 夏季運動活動會定義Teaser在夏季月份中鎖定的行銷區段。

活動也會識別您的頁面所使用的[目標定位引擎](/help/sites-authoring/personalization.md#targeting-engine)。

使用[活動主控台](/help/sites-authoring/activitylib.md)來建立和管理您品牌的活動。 您也可以[創作目標內容](/help/sites-authoring/content-targeting-touch.md)時建立活動。

## 體驗 {#experiences}

對於每個活動，您會定義一或多個體驗來識別您要鎖定的對象。 AEM可讓您控制包含每個體驗的內容。

對象是根據在AEM或Adobe Target中建立的行銷區段。 當訪客開啟網頁時，頁面邏輯會決定他們所屬的受眾，並顯示您為該受眾建立的內容。

例如，活動會為兩個不同對象定義體驗：30歲以上的女性和30歲以下的女性。 We.Retail網站的「女性」頁面針對每個體驗顯示不同的產品。

您可以為活動定義體驗。 您可以使用[活動主控台](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console)或[目標定位模式](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode)來新增體驗至活動。

## 產品建議 {#offers}

選件是出現在體驗頁面某個位置的內容。 針對不同的體驗使用不同的選件，以讓內容對您的對象產生最大成效。

例如，We.Retail範例網站的女性頁面可以使用選件作為出現在頁面頂端的Teaser影像。 不同的選件會用作30歲以上女性體驗和30歲以下女性體驗的Teaser。

使用[選件主控台](/help/sites-authoring/offerlib.md)建立您可在多個體驗中使用的選件。 在[編寫目標內容](/help/sites-authoring/content-targeting-touch.md)時，建立單一使用選件或從選件資料庫新增選件。

## 目標定位引擎 {#targeting-engine}

目標定位引擎是驅動目標內容邏輯的機制。 [活動](/help/sites-authoring/activitylib.md)設定為使用兩個可用的目標定位引擎之一：AEM 和 Adobe Target。

### AEM {#aem}

AEM提供內建定位引擎，可處理頁面請求並決定要顯示的內容。 使用 AEM 目標定位引擎時，您只能使用在 AEM 建立的細分群體來定義體驗的客群。

### Adobe Target {#adobe-target}

Adobe Target鎖定目標引擎會使系統在Adobe Target中追蹤從頁面瀏覽收集到的資訊。

* 使用此目標定位引擎時，您可以使用從 Adobe Target 匯入的細分群體來定義體驗的客群。
* 使用 Adobe Target 引擎的活動[會同步到 Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target)。

如果[已整合 Adobe Target](/help/sites-administering/opt-in.md)，即可使用此引擎。
