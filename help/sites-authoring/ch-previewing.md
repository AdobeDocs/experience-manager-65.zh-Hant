---
title: 使用 ContextHub 資料預覽頁面
seo-title: Previewing Pages Using ContextHub Data
description: ContextHub工具欄顯示ContextHub儲存中的資料，並允許您更改儲存資料，對預覽內容非常有用
seo-description: The ContextHub toolbar displays data from ContextHub stores and enables you to change store data and  is useful for previewing content
uuid: 0150555a-0a92-4692-a706-bbe59fd34d6a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f281ef8c-0831-470c-acb7-189f20452a50
exl-id: 78673609-8cbc-4b4b-953e-56c31ea1b4ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 3%

---

# 使用 ContextHub 資料預覽頁面{#previewing-pages-using-contexthub-data}

的 [上下文中心](/help/sites-developing/contexthub.md) 工具欄顯示ContextHub儲存中的資料，並允許您更改儲存資料。 ContextHub工具欄對預覽由ContextHub儲存中的資料確定的內容非常有用。

工具欄由包含一個或多個UI模組的一系列UI模式組成。

* UI模式是工具欄左側顯示的表徵圖。 按一下或點擊表徵圖時，工具欄將顯示其包含的UI模組。
* UI模組顯示來自一個或多個ContextHub儲存的資料。 某些UI模組還允許您操作儲存資料。

ContextHub安裝多個UI模式和UI模組。 您的管理員可能 [已配置ContextHub](/help/sites-developing/ch-configuring.md) 來顯示不同的。

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## 顯示ContextHub工具欄 {#revealing-the-contexthub-toolbar}

「預覽」模式下可使用ContextHub工具欄。 工具欄僅在作者實例上可用，並且僅當管理員啟用了它時才可用。

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. 開啟頁面進行編輯時，在工具欄上按一下或點擊「預覽」。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 要顯示工具欄，請按一下或點擊「上下文中心」表徵圖。

   ![](do-not-localize/screen_shot_2018-03-23at093621.png)

## UI模組功能 {#ui-module-features}

每個UI模組提供的功能集不同，但以下類型的功能是通用的。 因為UI模組是可擴展的，所以開發人員可以根據需要實現其他功能。

### 工具欄內容 {#toolbar-content}

UI模組可以顯示工具欄中一個或多個ContextHub儲存中的資料。 UI模組使用表徵圖和標題來標識自己。

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### 彈出內容 {#popup-content}

某些UI模組在按一下或點擊時會過度顯示彈出窗口。 通常，彈出菜單包含的資訊比工具欄上顯示的資訊還要多。

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### 彈出式Forms {#popup-forms}

模組的彈出式覆蓋可以包括表單元素，這些元素使您能夠更改ContextHub儲存中的資料。 如果頁面內容由儲存資料確定，則可以使用表單並觀察頁面內容的更改。

### 全螢幕模式 {#fullscreen-mode}

彈出式疊加可以包含一個表徵圖，您按一下或點擊該表徵圖可展開彈出式內容以覆蓋整個瀏覽器窗口或螢幕。

![](do-not-localize/chlimage_1-18.png)
