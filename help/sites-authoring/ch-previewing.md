---
title: 使用ContextHub資料預覽頁面
seo-title: 使用ContextHub資料預覽頁面
description: ContextHub工具列顯示來自ContextHub商店的資料，並讓您變更商店資料，對於預覽內容非常有用
seo-description: ContextHub工具列顯示來自ContextHub商店的資料，並讓您變更商店資料，對於預覽內容非常有用
uuid: 0150555a-0a92-4692-a706-bbe59fd34d6a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f281ef8c-0831-470c-acb7-189f20452a50
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用ContextHub資料預覽頁面{#previewing-pages-using-contexthub-data}

ContextHub工 [具列顯示](/help/sites-developing/contexthub.md) ContextHub儲存區的資料，並讓您變更儲存區資料。 ContextHub工具列對於預覽由ContextHub商店中的資料所決定的內容非常有用。

工具列由一系列包含一或多個UI模組的UI模式組成。

* UI模式是顯示在工具列左側的圖示。 當您按一下或點選圖示時，工具列會顯示其包含的UI模組。
* UI模組顯示來自一個或多個ContextHub儲存的資料。 部分UI模組也可讓您控制儲存資料。

ContextHub會安裝數種UI模式和UI模組。 您的管理員可能已 [設定ContextHub](/help/sites-administering/contexthub-config.md) ，以顯示不同的ContextHub。

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## 顯示ContextHub工具列 {#revealing-the-contexthub-toolbar}

ContextHub工具列可在「預覽」模式下使用。 工具列僅適用於作者例項，且僅在管理員啟用時才可用。

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. 當您的頁面開啟以進行編輯時，在工具列上按一下或點選「預覽」。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 若要顯示工具列，請按一下或點選ContextHub圖示。

   ![](do-not-localize/screen_shot_2018-03-23at093621.png)

## UI模組功能 {#ui-module-features}

每個UI模組提供的功能組不同，但是下列功能類型是常見的。 由於UI模組具有可擴充性，因此您的開發人員可視需要建置其他功能。

### 工具列內容 {#toolbar-content}

UI模組可顯示工具列中一或多個ContextHub儲存區的資料。 UI模組使用圖示和標題來識別自己。

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### 快顯內容 {#popup-content}

有些UI模組在點按或點選時會整體顯示彈出畫面。 通常，快顯功能表包含的工具列上顯示的其他資訊。

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### 彈出式表單 {#popup-forms}

模組的彈出式覆蓋可包含表單元素，可讓您變更ContextHub儲存區中的資料。 如果頁面內容是由儲存資料決定，您可以使用表單並觀察頁面內容的變更。

### 全螢幕模式 {#fullscreen-mode}

快顯覆蓋可包含您按一下或點選以展開快顯內容的圖示，以涵蓋整個瀏覽器視窗或畫面。

![](do-not-localize/chlimage_1-18.png)

