---
title: 主題自訂
seo-title: 主題自訂
description: 如何自訂AEM Forms應用程式的主題。
seo-description: 如何自訂AEM Forms應用程式的主題。
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 主題自訂 {#theme-customization}

您可以自訂HTML程式碼和CSS檔案，為AEM Forms應用程式提供獨特的組織特定外觀和感覺。 例如，您可以變更工作或「起點」的背景顏色和高度。 以下範例提供變更的指示：

* 顯示說明以取代說明
* 顯示路由數
* 背景漸層色彩

## 步驟 {#steps}

1. 開啟您的專案。

   * 若為iOS，請在Xcode `Capture.xcodeproj` 中開啟
   * 若是Android，請在Eclipse中開啟Android專案。
   * 在Windows中，在Visual `MWSWindows.sln` Studio中開啟。

1. 導覽至範本檔案夾。

   * 在Xcode中，導覽至「 **Capture > www > wsmobile > js > runtime > templates** 」檔案夾。
   * 在Eclipse中，導覽至「資 **產> www > wsmobile > js >執行階段>範本」資料夾** 。
   * 在Visual studio中，導覽至「 **MWSwindows > www > wsmobile > js > runtime > templates」檔案夾** 。

1. 開啟檔 `template.html` 案以進行編輯。
1. 找到下列字串：

   ```
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   以取代 `<%`。

1. 在檔案中找到下列程 `template.html` 式碼：

   ```
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 注釋下列行並保存檔案。

   ```
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. 導覽至css資料夾。

   * 在Xcode中，導覽至「 **Capture > www > wsmobile > css」**。
   * 在Eclipse中，導覽至 **資產> www > wsmobile > css**。
   * 在Visual studio中，導覽至 **MWSwindows > www > wsmobile > css**。

1. 開啟檔 `_style.css` 案以進行編輯。
1. 對於「背景」影像，請 `#323232` 變更為 `#fff`。
1. 儲存變更並關閉 `_style.css` 檔案。
1. 開啟AEM Forms應用程式。

   AEM Forms應用程式現在會顯示指示而非說明。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
