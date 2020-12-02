---
title: 自訂路由動作中使用的影像
seo-title: 自訂路由動作中使用的影像
description: How-to自訂LiveCycle AEM Forms工作區中用於路由動作的影像。
seo-description: How-to自訂LiveCycle AEM Forms工作區中用於路由動作的影像。
uuid: 42608376-587e-4b57-a9d5-8f9ebd981426
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 10158c13-47b4-43e3-ac47-690f3cbab158
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# 自訂路由動作{#customize-images-used-in-route-actions}中使用的影像

要自定義路由操作中使用的映像，請執行[自定義](/help/forms/using/generic-steps-html-workspace-customization.md)的一般步驟中所述的步驟，然後執行本文中所述的步驟。

## 路由動作的影像{#images-for-route-actions}

1. 在CSS中為新路由動作的下列位置新增定義影像的樣式：

   `/apps/ws/css/newStyle.css`

   例如：新增名為`myStyle1`的新樣式，如下所示，並使用WebDAV用戶端將影像檔案`myStyleIcon1.png`上傳至`/apps/ws/image`s資料夾。

   >[!NOTE]
   >
   >有關WebDAV訪問的詳細資訊，請參見[https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

   >[!NOTE]
   >
   >偏好使用樣式名稱與路由操作名稱相同。

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## 任務清單任務操作彈出菜單{#task-list-task-action-popup}

1. 建立工作清單動作快顯視窗，請參閱「建立AEM Forms工作區程式碼[」。 ](introduction-customizing-html-workspace.md#building-html-workspace-code)需要使用dev套件。

1. 將`/libs/ws/js/runtime/templates/task.html`複製到`/apps/ws/js/runtime/templates/task.html`。

1. 如果CSS樣式的名稱與來自伺服器的路由操作名稱相同，請在`/apps/ws/js/runtime/templates/task.html`中修改以下代碼：

   ```jsp
   <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   
   To
   
   <%if(routeList == null){%>
               <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li class="<%= availableCommands.directCommands[i]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   ```

1. 如果CSS樣式的名稱與來自伺服器的路由操作名稱不同，請在`/apps/ws/js/runtime/templates/task.html`中修改以下代碼。 它添加`if-else` servlet條件的堆棧，以用路由操作名映射樣式。

```jsp
<%if(routeList == null){%>
            <li>
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
            <li>
                <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
            </li>
            <%}%>
            <%}%>

To

<%if(routeList == null){%>
            <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
                <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                     <li class="myStyle1" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                     <li class="myStyle2" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}%>
            <%}%>
            <%}%>
```

## 任務詳細資訊任務操作彈出菜單{#task-details-task-action-popup}

1. 將`/libs/ws/js/runtime/templates/taskdetails.html`複製到`/apps/ws/js/runtime/templates/taskdetails.html`。

1. 如果CSS樣式的名稱與來自伺服器的路由操作名稱相同，請在`/apps/ws/js/runtime/templates/taskdetails.html`中修改以下代碼：

   ```jsp
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                       <%}%>
   ```

1. 如果CSS樣式的名稱與來自伺服器的路由操作名稱不同，請在`/apps/ws/js/runtime/templates/taskdetails.html`中修改以下代碼。 它添加`if-else` servlet條件堆棧，以用路由操作名映射樣式。

   ```jsp
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                   <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle1" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle2" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}%>
               <%}%>
   ```

1. 開啟`/apps/ws/js/registry.js`進行編輯，並尋找下列文字：
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. 將文字取代為：
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`
