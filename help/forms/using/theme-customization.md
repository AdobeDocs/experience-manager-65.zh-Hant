---
title: 主題自定義
seo-title: Theme Customization
description: 如何自定義您的AEM Forms應用的主題。
seo-description: How to customize the theme of your AEM Forms app.
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 主題自定義 {#theme-customization}

您可以自定義HTML代碼和CSS檔案，為AEM Forms應用提供獨特的組織特定外觀。 例如，可更改任務或起點的背景顏色和高度。 以下示例提供了更改的說明：

* 顯示說明以代替說明
* 顯示路由數
* 背景漸變色

## 步驟 {#steps}

1. 開啟項目。

   * iOS，開門 `Capture.xcodeproj` 在Xcode中
   * 對於Android，在Eclipse中開啟Android項目。
   * 對於Windows，開啟 `MWSWindows.sln` 的子菜單。

1. 導航到模板資料夾。

   * 在Xcode中，導航到 **捕獲> www > wsmobile > js > runtime >模板** 的子菜單。
   * 在Eclipse中，導航到 **資產> www > wmobile > js >運行時>模板** 的子菜單。
   * 在Visual Studio中，導航到 **MWSwindows > www > wsmobile > js > runtime >模板** 的子菜單。

1. 開啟 `template.html` 檔案。
1. 找到以下字串：

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   替換為 `<%`。

1. 在 `template.html` 檔案：

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 注釋下一行並保存檔案。

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. 導航到css資料夾。

   * 在Xcode中，導航到 **捕獲> www > wsmobile > css**。
   * 在Eclipse中，導航到 **資產> www > wmobile > css**。
   * 在Visual Studio中，導航到 **MWSwindows > www > wsmobile > css**。

1. 開啟 `_style.css` 檔案。
1. 對於背景影像，更改 `#323232` 至 `#fff`。
1. 保存更改並關閉 `_style.css` 的子菜單。
1. 開啟AEM Forms應用。

   AEM Forms應用現在顯示說明而不是說明。
