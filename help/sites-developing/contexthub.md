---
title: ContextHub
seo-title: ContextHub
description: ContextHub是儲存、操控和呈現內容資料的架構
seo-description: ContextHub是儲存、操控和呈現內容資料的架構
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub是儲存、操控和呈現內容資料的架構。 用戶端Javascript API可讓您存取資料，以個人化內容。

>[!NOTE]
>
>[We.Retail參考實作](/help/sites-developing/we-retail.md)實作ContextHub，並可在您將ContextHub整合至您自己的專案時作為參考。

>[!CAUTION]
>
>包含[We.Retail參考實作](/help/sites-developing/we-retail.md)(`/libs/settings/cloudsettings/legacy`)所使用之範例ContextHub設定的路徑，僅應當用作建立您自己設定的參考。
>
>在專案中，不應將其用作您自己的ContextHub設定。

## 持久性 {#persistence}

ContextHub會在用戶端上儲存保留的內容資料。 ContextHub Javascript API可讓您視需要存取儲存區，以建立、更新和刪除資料。 因此，ContextHub代表您頁面上的資料層。

每個ContextHub存放區都是預先定義的存放區類型的例項：

* ContextHub提供數種[範例存放區類型](/help/sites-developing/ch-samplestores.md)。
* 使用AEM主控台建立[儲存](ch-configuring.md#creating-a-contexthub-store)。
* 開發人員可以[建立自訂商店類型](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)。
* 開發人員可以透過Javascript存取[儲存資料](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores)。

## Segmentation {#segmentation}

ContextHub包含區段引擎，可管理區段並判斷要針對目前內容解析哪些區段。 已定義數個區段。 您可以使用Javascript API來[判斷已解析的區段](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)。

## 簡報 {#presentation}

[ContextHub工具列](/help/sites-authoring/ch-previewing.md)可讓行銷人員和作者查看和操控存放區資料，以模擬製作頁面時的使用者體驗。 工具列由提供ContextHub存放區存取權的UI模組群組組成。

每個ContextHub UI模組都是預先定義模組類型的例項：

* ContextHub提供數種[範例模組類型](/help/sites-developing/ch-samplemodules.md)。
* 使用AEM主控台來[新增UI模組](ch-configuring.md#adding-a-ui-module)，以及在UI模式](ch-configuring.md#adding-a-ui-mode)中將它們分組。[

* 開發人員可以[建立自訂模組類型](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

開發人員需要[將ContextHub元件新增至頁面](/help/sites-developing/ch-adding.md)。
