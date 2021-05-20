---
title: AEM Forms工作區自訂的一般步驟
seo-title: AEM Forms工作區自訂的一般步驟
description: 如何開始自訂AEM Forms工作區使用者介面。
seo-description: 如何開始自訂AEM Forms工作區使用者介面。
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
exl-id: 45e50b47-1b36-4937-9e1a-cc7bfb953861
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---

# AEM Forms工作區自訂的一般步驟{#generic-steps-for-aem-forms-workspace-customization}

執行任何自訂的一般步驟為：

1. 通過訪問`https://'[server]:[port]'/lc/crx/de/index.jsp`登錄CRXDE Lite。
1. 在`/apps`建立名為`ws`的`sling:Folder`資料夾（如果不存在）。 要建立`sling:Folder`資料夾，請按一下右鍵`apps`資料夾，然後選擇&#x200B;**[!UICONTROL Create]** > **[!UICONTROL Create Node]**。 指定名稱為`ws`，選擇類型為`sling:Folder`，然後按一下&#x200B;**[!UICONTROL 確定]**。 按一下「**[!UICONTROL 全部保存]**」。
1. 瀏覽至`/apps/ws`，並導覽至&#x200B;**[!UICONTROL 存取控制]**&#x200B;標籤。
1. 選擇&#x200B;**[!UICONTROL Repository]**&#x200B;選項。 在&#x200B;**[!UICONTROL 訪問控制]**&#x200B;清單中，按一下&#x200B;**[!UICONTROL +]**&#x200B;以添加新條目。 再次按一下&#x200B;**[!UICONTROL +]**。
1. 搜索並選擇&#x200B;**PERM_WORKSPACE_USER**&#x200B;主體。

   ![選取PERM_WORKSPACE_USER主體，作為自訂HTML工作區一般步驟的一部分](assets/perm_workspace_user.png)

1. 為主體授予`jcr:read`權限。
1. 按一下「**[!UICONTROL 全部保存]**」。
1. 將`GET.jsp`、`index`和`html.jsp`檔案從`/libs/ws`資料夾複製到`/apps/ws`資料夾。
1. 複製`/apps/ws`資料夾中的`/libs/ws/locales`資料夾。 按一下「**[!UICONTROL 全部保存]**」。
1. 更新`GET.jsp`檔案中的引用和相對路徑，如下所示，然後按一下&#x200B;**[!UICONTROL Save all]**。

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. 請針對CSS自訂執行下列動作：

   1. 導覽至`/apps/ws`資料夾，並建立名為`css`的新資料夾。

   1. 在`css`資料夾中，建立名為`newStyle.css`的新檔案。

   1. 開啟`/apps/ws/html`.jsp並從

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
   >將使用者定義的CSS檔案的項目放置在style.css的項目之後，如上所示。

1. 在/apps/ws/html.jsp檔案中，從

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   至

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 請執行下列動作：

   1. 在`/apps/ws`建立名為`js`的資料夾。 按一下「**[!UICONTROL 全部保存]**」。

   1. 在`/apps/ws/js`建立名為`libs`的資料夾。 按一下「**[!UICONTROL 全部保存]**」。

   1. 將`/libs/ws/js/libs/jqueryui`資料夾複製到`/apps/ws/js/libs`。 按一下「**[!UICONTROL 全部保存]**」。

1. 請針對HTML自訂執行下列動作：

   1. 在`/apps/ws/js`下，建立名為`runtime`的資料夾。 按一下「**[!UICONTROL 全部保存]**」。

   1. 在`/apps/ws/js/runtime`下，建立名為`templates`的資料夾。 按一下「**[!UICONTROL 全部保存]**」。

   1. 將`/libs/ws/js/main.js`複製到`/apps/ws/js/main.js`。

   1. 將/libs/ws/js/registry.js複製到`/apps/ws/js/registry.js`。

1. 按一下「**[!UICONTROL 儲存全部]**」、清除快取，然後重新整理AEM Forms工作區。

   訪問URL `https://'[server]:[port]'/lc/ws`並使用管理員/密碼憑據登錄。 瀏覽器會重新導向至`https://'[server]:[port]'/lc/apps/ws/index.html`。
