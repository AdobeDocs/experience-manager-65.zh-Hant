---
title: ContextHub
description: ContextHub是一種用於儲存、操控和呈現內容資料的架構
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub是一種用於儲存、操控和呈現內容資料的架構。 使用者端JavaScript API可讓您存取資料，以將內容個人化。

>[!NOTE]
>
>此 [We.Retail參考實作](/help/sites-developing/we-retail.md) 會實作ContextHub，且可在您將ContextHub整合至您自己的專案時作為參考。

>[!CAUTION]
>
>包含用於的範例ContextHub設定的路徑 [We.Retail參考實作](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`)僅能作為建立您自己的設定的參考。
>
>請勿在專案中使用作為您自己的ContextHub設定。

## 持續性 {#persistence}

ContextHub會儲存使用者端上持續儲存的內容資料。 ContextHub JavaScript API可讓您視需要存取存放區以建立、更新和刪除資料。 因此，ContextHub代表頁面上的資料層。

每個ContextHub存放區都是預先定義的存放區型別例項：

* ContextHub提供數種 [範例存放區型別](/help/sites-developing/ch-samplestores.md).
* 使用AEM主控台 [建立存放區](ch-configuring.md#creating-a-contexthub-store).
* 開發人員可以 [建立自訂商店型別](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* 開發人員可以 [存取存放區資料](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) 透過JavaScript。

## Segmentation {#segmentation}

ContextHub包含區段引擎，可管理區段並決定針對目前內容解析哪些區段。 已定義數個區段。 您可以使用JavaScript API [決定已解析的區段](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## 簡報 {#presentation}

此 [contexthub工具列](/help/sites-authoring/ch-previewing.md) 可讓行銷人員和作者檢視及操控存放區資料，以便在編寫頁面時模擬使用者體驗。 工具列包含提供ContextHub存放區存取許可權的UI模組群組。

每個ContextHub UI模組都是預先定義模組型別的例項：

* ContextHub提供數種 [範例模組型別](/help/sites-developing/ch-samplemodules.md).
* 使用AEM主控台 [新增使用者介面模組](ch-configuring.md#adding-a-ui-module)，並至 [以UI模式將其分組](ch-configuring.md#adding-a-ui-mode).

* 開發人員可以 [建立自訂模組型別](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

開發人員需要 [將ContextHub元件新增至頁面](/help/sites-developing/ch-adding.md).
