---
title: AEM Forms工作區自訂的一般步驟
description: 如何開始自訂Adobe Experience Manager Forms工作區使用者介面。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 45e50b47-1b36-4937-9e1a-cc7bfb953861
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 9%

---

# AEM Forms工作區自訂的一般步驟 {#generic-steps-for-aem-forms-workspace-customization}

執行任何自訂的一般步驟為：

1. 存取`https://'[server]:[port]'/lc/crx/de/index.jsp`以登入CRXDE Lite。
1. 在`/apps`建立名為`ws`的`sling:Folder`資料夾（如果不存在）。 若要建立`sling:Folder`資料夾，請在`apps`資料夾上按一下滑鼠右鍵，然後選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 建立節點]**。 將名稱指定為`ws`，選取型別為`sling:Folder`，然後按一下&#x200B;**[!UICONTROL 確定]**。 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。
1. 瀏覽至`/apps/ws`，並瀏覽至&#x200B;**[!UICONTROL 存取控制]**&#x200B;標籤。
1. 選取&#x200B;**[!UICONTROL 存放庫]**&#x200B;選項。 在&#x200B;**[!UICONTROL 存取控制]**&#x200B;清單中，按一下&#x200B;**[!UICONTROL +]**&#x200B;以新增專案。 再按一下&#x200B;**[!UICONTROL +]**。
1. 搜尋並選取&#x200B;**PERM_WORKSPACE_USER**&#x200B;主體。

   ![選取PERM_WORKSPACE_USER主體作為自訂HTMLWorkspace的一般步驟的一部分](assets/perm_workspace_user.png)

1. 將`jcr:read`許可權授與主體。
1. 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。
1. 將`GET.jsp`、`index`和`html.jsp`檔案從`/libs/ws`資料夾複製到`/apps/ws`資料夾。
1. 複製`/apps/ws`資料夾中的`/libs/ws/locales`資料夾。 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。
1. 更新`GET.jsp`檔案中的參照和相對路徑，如下所示，然後按一下[儲存全部]。**&#x200B;**

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. 請對CSS自訂執行下列動作：

   1. 瀏覽至`/apps/ws`資料夾，並建立名為`css`的資料夾。

   1. 在`css`資料夾中，建立名為`newStyle.css`的檔案。

   1. 開啟`/apps/ws/html`.jsp並變更來源

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   至

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >將使用者定義的CSS檔案專案放在style.css專案之後，如上所示。

1. 在/apps/ws/html.jsp檔案中，從

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   至

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 請執行下列動作：

   1. 在`/apps/ws`建立名為`js`的資料夾。 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

   1. 在`/apps/ws/js`建立名為`libs`的資料夾。 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

   1. 將`/libs/ws/js/libs/jqueryui`資料夾複製到`/apps/ws/js/libs`。 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

1. 請針對HTML自訂執行以下動作：

   1. 在`/apps/ws/js`下，建立名為`runtime`的資料夾。 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

   1. 在`/apps/ws/js/runtime`下，建立名為`templates`的資料夾。 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

   1. 將`/libs/ws/js/main.js`複製到`/apps/ws/js/main.js`。

   1. 將/libs/ws/js/registry.js複製到`/apps/ws/js/registry.js`。

1. 按一下「儲存全部&#x200B;**[!UICONTROL 」]**，清除快取，然後重新整理AEM Forms工作區。

   存取URL `https://'[server]:[port]'/lc/ws`並使用管理員/密碼認證登入。 瀏覽器重新導向至`https://'[server]:[port]'/lc/apps/ws/index.html`。
