---
title: 手勢自訂
seo-title: 手勢自訂
description: 自訂AEM Forms應用程式上的手勢
seo-description: 自訂AEM Forms應用程式上的手勢
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 手勢自訂 {#gesture-customization}

您可以自訂AEM Forms應用程式的手勢，以提供與應用程式互動的不同方法。 例如，您可以新增手勢以開啟或關閉工作或「起點」。

## 若要在AEM Forms應用程式中自訂手勢 {#to-customize-gestures-in-aem-forms-app}

在AEM Forms應用程式中，左側滑動會開啟新工作或「起點」，而右側滑動則無效。 下列範例提供在AEM Forms應用程式中執行右滑動手勢時開啟新工作或「起點」的步驟。

1. 開啟您的專案。

   * 若為iOS，請在Xcode `Capture.xcodeproj` 中開啟
   * 若是Android，請在Eclipse中開啟Android專案。
   * 在Windows中，在Visual `MWSWindows.sln` Studio中開啟。

1. 導覽至檢視資料夾，並開啟檔 `task.js` 案以進行編輯。

   * 在Xcode中，導覽至「 **Capture > www > wsmobile > js >執行階段>檢視」資料夾** 。
   * 在Eclipse中，導覽至「資 **產> www > wsmobile > js >執行階段>檢視資料夾** 」。
   * 在Visual Studio中，導覽至「 **MWSwindows > www > wsmobile > js > runtime >檢視」檔案夾** 。
   >[!NOTE]
   >
   >task.js檔案包含與任務或「起點」清單中列出的每個任務或「起點」相關聯的主幹視圖。

1. 在檔 `task.js` 案中，搜尋檢視的events屬性。

   events屬性是一個映射，每個條目的格式如下：

   `"EventName Selector": "Function"`

   當您觸發在指定的HTML元 `EventName`素上命名的Javascript事件時， `Selector`會呼 `Function`叫該事件。

1. 尋找

   * &quot;tap .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;tap .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      「點選。task-content」:&quot;onTaskClick&quot;,

      &quot;tap .last_empty_div&quot; :&quot;onTaskClick&quot;,
   和

   * &quot;swipe .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      「滑動。task-content」:&quot;onTaskClick&quot;,

      &quot;swipe .last_empty_div&quot; :&quot;onTaskClick&quot;,


1. 儲存並關閉 `task.js` 檔案。
1. 建立並執行AEM Forms應用程式。 現在，您可以使用左滑動和右滑動來開啟使用。

同樣地，您也可以針對各種手勢、HTML元素和函陣列合，在其他檢視中進行變更。
