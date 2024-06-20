---
title: 手勢自訂
description: 瞭解如何在AEM Forms應用程式上自訂手勢。 您可以自訂手勢，以提供與應用程式互動的獨特方法。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 手勢自訂 {#gesture-customization}

您可以自訂AEM Forms應用程式的手勢，以提供與應用程式互動的不同方法。 例如，您可以新增手勢以開啟或關閉任務或起點。

## 若要在AEM Forms應用程式中自訂手勢 {#to-customize-gestures-in-aem-forms-app}

在AEM Forms應用程式中，向左撥動可開啟新任務或起點，而向右撥動則不會執行任何動作。 下列範例提供在AEM Forms應用程式中執行滑鼠右鍵手勢時，開啟新任務或起點的步驟。

1. 開啟您的專案。

   * 針對iOS，請開啟 `Capture.xcodeproj` 在Xcode中
   * 若是Android，請在Eclipse中開啟Android專案。
   * 若是Windows，請開啟 `MWSWindows.sln` 在Visual Studio中。

1. 導覽至檢視資料夾，並開啟 `task.js` 檔案進行編輯。

   * 在Xcode中，導覽至 **擷取> www > wsmobile > js >執行階段>檢視** 資料夾。
   * 在Eclipse中，導覽至 **資產> www > wsmobile > js >執行階段>檢視** 資料夾。
   * 在Visual Studio中，導覽至 **MWSWindows > www > wsmobile > js > runtime >檢視** 資料夾。

   >[!NOTE]
   >
   >task.js檔案包含與任務或「起點」清單中列出的每個任務或「起點」相關聯的骨幹檢視。

1. 在 `task.js` 檔案中，搜尋檢視表的events屬性。

   events屬性是一個對應，每個專案的格式為：

   `"EventName Selector": "Function"`

   當您觸發名為的JavaScript事件時 `EventName`於指定的HTML元素上，指定者： `Selector`，則 `Function`稱為。

1. 尋找

   * &quot;select .taskContentArea&quot; ： &quot;onTaskClick&quot;，

     &quot;select .taskOpenArea&quot; ： &quot;onTaskClick&quot;，

     &quot;select .task-content&quot; ： &quot;onTaskClick&quot;，

     &quot;select .last_empty_div&quot; ： &quot;onTaskClick&quot;，

   和取代為

   * &quot;撥動.taskContentArea&quot; ： &quot;onTaskClick&quot;，

     &quot;swipe .taskOpenArea&quot; ： &quot;onTaskClick&quot;，

     &quot;撥動.task-content&quot; ： &quot;onTaskClick&quot;，

     &quot;swipe .last_empty_div&quot; ： &quot;onTaskClick&quot;，

1. 儲存並關閉 `task.js` 檔案。
1. 建置並執行AEM Forms應用程式。 現在您可以使用向左撥動和向右撥動來開啟。

同樣地，您可以針對各種手勢、HTML元素和函式的組合，在其他檢視中進行變更。
