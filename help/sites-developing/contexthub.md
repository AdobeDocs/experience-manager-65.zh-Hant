---
title: ContextHub
seo-title: ContextHub
description: ContextHub是儲存、控制和呈現上下文資料的架構
seo-description: ContextHub是儲存、控制和呈現上下文資料的架構
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# ContextHub{#contexthub}

ContextHub是儲存、控制和呈現上下文資料的架構。 用戶端Javascript API可讓您存取資料，以個人化內容。

>[!NOTE]
>
>We. [Retail參考實作實作](/help/sites-developing/we-retail.md) ，可實作ContextHub，並當您將ContextHub整合至您自己的專案時，做為參考。

>[!CAUTION]
>
>包含 [We.Retail參考實作](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`)所使用之範例ContextHub組態的路徑，僅能用作建立您自己組態的參考。
>
>它不應用於專案中，做為您自己的ContextHub設定。

## 永續性 {#persistence}

ContextHub會在用戶端上儲存持續的上下文資料。 ContextHub Javascript API可讓您存取商店，以視需要建立、更新和刪除資料。 因此，ContextHub代表您頁面上的資料層。

每個ContextHub儲存都是預定義儲存類型的實例：

* ContextHub提供數種 [範例商店類型](/help/sites-developing/ch-samplestores.md)。
* 使用AEM主控台 [建立商店](/help/sites-administering/contexthub-config.md#creating-a-contexthub-store)。
* 開發人員可 [以建立自訂商店類型](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)。
* 開發人員可 [以透過Javascript存取](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) 儲存資料。

## Segmentation {#segmentation}

ContextHub包含區段引擎，可管理區段並判斷哪些區段可針對目前的上下文加以解析。 已定義數個區段。 您可以使用Javascript API來判斷已解 [決的區段](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)。

## 簡報 {#presentation}

ContextHub工 [](/help/sites-authoring/ch-previewing.md) 具列可讓行銷人員和作者查看和控制儲存資料，以模擬在製作頁面時的使用者體驗。 工具列由UI模組群組組成，這些UI模組可讓您存取ContextHub商店。

每個ContextHub UI模組都是預先定義模組類型的例項：

* ContextHub提供了幾 [種模組類型](/help/sites-developing/ch-samplemodules.md)。
* 使用AEM主控台 [新增UI模組](/help/sites-administering/contexthub-config.md#adding-a-ui-module)，並 [在UI模式中分組](/help/sites-administering/contexthub-config.md#adding-a-ui-mode)。

* 開發人員可 [以建立自訂模組類型](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

開發人員需 [要將ContextHub元件新增至頁面](/help/sites-developing/ch-adding.md)。
