---
title: 手勢自定義
seo-title: Gesture customization
description: 自定義你的AEM Forms應用上的手勢
seo-description: Customize the gestures on your AEM Forms app
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 手勢自定義 {#gesture-customization}

你可以自定義AEM Forms應用的手勢，以提供與應用交互的獨特方法。 例如，可以添加新手勢以開啟或關閉任務或起點。

## 自定義AEM Forms應用中的手勢 {#to-customize-gestures-in-aem-forms-app}

在AEM Forms應用中，左輕掃可開啟新任務或Startpoint，而右輕掃則無效。 以下示例提供了在AEM Forms應用中執行右刷手勢時開啟新任務或Startpoint的步驟。

1. 開啟項目。

   * iOS，開門 `Capture.xcodeproj` 在Xcode中
   * 對於Android，在Eclipse中開啟Android項目。
   * 對於Windows，開啟 `MWSWindows.sln` 的子菜單。

1. 導航到視圖資料夾並開啟 `task.js` 檔案。

   * 在Xcode中，導航到 **捕獲> www > wsmobile > js >運行時>視圖** 的子菜單。
   * 在Eclipse中，導航到 **資產> www > wmobile > js >運行時>視圖** 的子菜單。
   * 在Visual Studio中，導航到 **MWSwindows > www > wsmobile > js > runtime >視圖** 的子菜單。

   >[!NOTE]
   >
   >task.js檔案包含與任務清單或起始點清單中列出的每個任務或起始點相關聯的主幹視圖。

1. 在 `task.js` 檔案，搜索視圖的事件屬性。

   events屬性是一個映射，每個條目的格式如下：

   `"EventName Selector": "Function"`

   觸發名為的Javascript事件時 `EventName`指定的HTML元素 `Selector`，也請參見Wiki頁。 `Function`。

1. 尋找

   * &quot;點擊.taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;點擊.taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;點擊.task內容&quot;:&quot;onTaskClick&quot;,

      &quot;點擊.last_empty_div&quot;:&quot;onTaskClick&quot;,
   替換

   * &quot;輕掃.taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;輕掃.taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;輕掃.task內容&quot;:&quot;onTaskClick&quot;,

      &quot;輕掃.last_empty_div&quot;:&quot;onTaskClick&quot;,


1. 保存並關閉 `task.js` 的子菜單。
1. 生成並運行AEM Forms應用。 現在，您可以使用左輕掃和右輕掃開啟使用。

同樣，您可以對手勢、HTML元素和函式的各種組合在其它視圖中進行更改。
