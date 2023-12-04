---
title: 使用 ContextHub 資料預覽頁面
seo-title: Previewing Pages Using ContextHub Data
description: ContextHub工具列會顯示ContextHub存放區中的資料，並可讓您變更存放區資料，且可用於預覽內容
seo-description: The ContextHub toolbar displays data from ContextHub stores and enables you to change store data and  is useful for previewing content
uuid: 0150555a-0a92-4692-a706-bbe59fd34d6a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f281ef8c-0831-470c-acb7-189f20452a50
exl-id: 78673609-8cbc-4b4b-953e-56c31ea1b4ea
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 3%

---

# 使用 ContextHub 資料預覽頁面{#previewing-pages-using-contexthub-data}

此 [ContextHub](/help/sites-developing/contexthub.md) 工具列會顯示ContextHub存放區中的資料，並可讓您變更存放區資料。 ContextHub工具列可用於預覽由ContextHub存放區中的資料所決定的內容。

工具列包含一系列UI模式，其中包含一或多個UI模組。

* UI模式是出現在工具列左側的圖示。 按一下圖示時，工具列會顯示其中的UI模組。
* UI模組會顯示一或多個ContextHub存放區的資料。 有些UI模組也可讓您操控存放區資料。

ContextHub會安裝數個UI模式和UI模組。 您的管理員可能會 [已設定的ContextHub](/help/sites-developing/ch-configuring.md) 以顯示不同的值。

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## 顯示ContextHub工具列 {#revealing-the-contexthub-toolbar}

ContextHub工具列可在「預覽」模式中使用。 工具列僅在作者執行個體上可用，且僅當您的管理員啟用了它時才可用。

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. 開啟頁面進行編輯時，在工具列上按一下「預覽」 。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 若要顯示工具列，請按一下ContextHub圖示。

   ![內容中心](do-not-localize/screen_shot_2018-03-23at093621.png)

## UI模組功能 {#ui-module-features}

提供的每個UI模組都是一組不同的功能，但以下型別的功能很常見。 由於UI模組是可擴充的，因此您的開發人員可以視需要實作其他功能。

### 工具列內容 {#toolbar-content}

UI模組可以在工具列中顯示一或多個ContextHub存放區的資料。 UI模組使用圖示和標題來識別自身。

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### 快顯視窗內容 {#popup-content}

有些UI模組在點選或點選時會全面顯示快顯視窗。 通常，快顯視窗會包含其他資訊，而不是顯示在工具列上的資訊。

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### 快顯Forms {#popup-forms}

模組的快顯視窗覆蓋圖可包含可讓您變更ContextHub存放區中資料的表單元素。 如果頁面內容由商店資料決定，您可以使用表單並觀察頁面內容的變更。

### 全螢幕模式 {#fullscreen-mode}

彈出式覆蓋圖可以包含圖示，按一下即可展開彈出式內容，以涵蓋整個瀏覽器視窗或熒幕。

![全熒幕](do-not-localize/chlimage_1-18.png)
