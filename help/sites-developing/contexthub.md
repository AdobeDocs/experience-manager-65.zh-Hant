---
title: ContextHub
seo-title: ContextHub
description: ContextHub是用於儲存、操作和呈現上下文資料的框架
seo-description: ContextHub is a framework for storing, manipulating, and presenting context data
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub是用於儲存、操作和呈現上下文資料的框架。 客戶端Javascript API使您能夠訪問資料以個性化內容。

>[!NOTE]
>
>的 [We.零售參考實施](/help/sites-developing/we-retail.md) 實現ContextHub，並可在將ContextHub整合到您自己的項目中時用作參考。

>[!CAUTION]
>
>包含由 [We.零售參考實施](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`)只應用作建立自己配置的引用。
>
>不應將它用作您自己的ContextHub配置。

## 持久性 {#persistence}

ContextHub在客戶端上儲存持續的上下文資料。 ContextHub Javascript API使您能夠訪問儲存，以根據需要建立、更新和刪除資料。 因此，ContextHub表示頁面上的資料層。

每個ContextHub儲存都是預定義儲存類型的實例：

* ContextHub提供了 [示例儲存類型](/help/sites-developing/ch-samplestores.md)。
* 使用控AEM制台 [建立儲存](ch-configuring.md#creating-a-contexthub-store)。
* 開發人員可以 [建立自定義儲存類型](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)。
* 開發人員可以 [訪問儲存資料](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) 通過Javascript。

## Segmentation {#segmentation}

ContextHub包括分段引擎，用於管理段並確定為當前上下文解析哪些段。 定義了若干段。 可以使用Javascript API [確定已解析的段](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)。

## 簡報 {#presentation}

的 [ContextHub工具欄](/help/sites-authoring/ch-previewing.md) 使營銷人員和作者能夠查看和操作儲存資料，以在創作頁面時模擬用戶體驗。 工具欄由提供對ContextHub儲存的訪問的UI模組組組成。

每個ContextHub UI模組都是預定義模組類型的實例：

* ContextHub提供了 [示例模組類型](/help/sites-developing/ch-samplemodules.md)。
* 使用控AEM制台 [添加UI模組](ch-configuring.md#adding-a-ui-module), [在UI模式下對它們進行分組](ch-configuring.md#adding-a-ui-mode)。

* 開發人員可以 [建立自定義模組類型](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

開發人員需要 [將ContextHub元件添加到頁面](/help/sites-developing/ch-adding.md)。
