---
title: 佈景主題自訂
description: 瞭解如何自訂AEM Forms應用程式的主題。 您可以自訂HTML程式碼和CSS檔案，以提供特定於組織的外觀和風格。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 4%

---

# 佈景主題自訂 {#theme-customization}

您可以自訂HTML程式碼和CSS檔案，為AEM Forms應用程式提供獨特的組織專屬外觀和風格。 例如，您可以變更任務或「起點」的背景顏色和高度。 下列範例提供變更的指示：

* 顯示指示以取代說明
* 顯示路由數目
* 背景漸層顏色

## 步驟 {#steps}

1. 開啟您的專案。

   * 若為iOS，請在Xcode中開啟`Capture.xcodeproj`
   * 針對Android，請在Eclipse中開啟Android專案。
   * 若是Windows，請在Visual Studio中開啟`MWSWindows.sln`。

1. 導覽至「範本」資料夾。

   * 在Xcode中，導覽至&#x200B;**Capture > www > wsmobile > js > runtime > templates**&#x200B;資料夾。
   * 在Eclipse中，導覽至&#x200B;**assets > www > wsmobile > js > runtime > templates**&#x200B;資料夾。
   * 在Visual Studio中，瀏覽至&#x200B;**MWSWindows > www > wsmobile > js > runtime > templates**&#x200B;資料夾。

1. 開啟 `template.html` 檔案進行編輯。
1. 找出下列字串：

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   以`<%`取代。

1. 在`template.html`檔案中找到下列程式碼：

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 註解下列行並儲存檔案。

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. 導覽至css資料夾。

   * 在Xcode中，瀏覽至&#x200B;**Capture > www > wsmobile > css**。
   * 在Eclipse中，導覽至&#x200B;**資產> www > wsmobile > css**。
   * 在Visual Studio中，瀏覽至&#x200B;**MWSWindows > www > wsmobile > css**。

1. 開啟 `_style.css` 檔案進行編輯。
1. 背景影像請將`#323232`變更為`#fff`。
1. 儲存變更並關閉`_style.css`檔案。
1. 開啟AEM Forms應用程式

   AEM Forms應用程式現在會顯示指示，而非說明。
