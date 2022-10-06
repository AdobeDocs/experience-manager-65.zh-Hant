---
title: AEM Forms工作區自訂的一般步驟
seo-title: Generic steps for AEM Forms workspace customization
description: 如何開始自訂AEM Forms工作區使用者介面。
seo-description: How to get started customizing AEM Forms workspace user interface.
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
source-wordcount: '300'
ht-degree: 1%

---

# AEM Forms工作區自訂的一般步驟 {#generic-steps-for-aem-forms-workspace-customization}

執行任何自訂的一般步驟為：

1. 透過存取 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 建立 `sling:Folder` 資料夾已命名 `ws` at `/apps`，如果不存在。 建立 `sling:Folder` 資料夾，按一下右鍵 `apps` 資料夾和選取 **[!UICONTROL 建立]** > **[!UICONTROL 建立節點]**. 將名稱指定為 `ws`選取「 」作為 `sling:Folder` 按一下 **[!UICONTROL 確定]**. 按一下 **[!UICONTROL 全部儲存]**.
1. 瀏覽至 `/apps/ws`，並導覽至 **[!UICONTROL 存取控制]** 標籤。
1. 選取 **[!UICONTROL 存放庫]** 選項。 在 **[!UICONTROL 存取控制]** 清單，按一下 **[!UICONTROL +]** 來添加新條目。 按一下 **[!UICONTROL +]** 。
1. 搜尋並選取 **PERM_WORKSPACE_USER** 校長。

   ![選取PERM_WORKSPACE_USER主體，作為自訂HTML工作區的一般步驟的一部分](assets/perm_workspace_user.png)

1. 提供 `jcr:read` 特權給承擔者。
1. 按一下 **[!UICONTROL 全部儲存]**.
1. 複製 `GET.jsp`, `index`，和 `html.jsp` 檔案 `/libs/ws` 檔案夾 `/apps/ws` 檔案夾。
1. 複製 `/libs/ws/locales` 檔案夾 `/apps/ws` 檔案夾。 按一下 **[!UICONTROL 全部儲存]**.
1. 更新 `GET.jsp` 檔案，如下所示，然後按一下 **[!UICONTROL 全部儲存]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. 請針對CSS自訂執行下列動作：

   1. 導覽至 `/apps/ws` 資料夾和建立名為 `css`.

   1. 在 `css` 資料夾，建立名為 `newStyle.css`.

   1. 開啟 `/apps/ws/html`.jsp和更改

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

   1. 建立名為 `js` at `/apps/ws`. 按一下 **[!UICONTROL 全部儲存]**.

   1. 建立名為 `libs` at `/apps/ws/js`. 按一下 **[!UICONTROL 全部儲存]**.

   1. 複製 `/libs/ws/js/libs/jqueryui` 資料夾 `/apps/ws/js/libs`. 按一下 **[!UICONTROL 全部儲存]**.

1. 請針對HTML自訂執行下列動作：

   1. 在 `/apps/ws/js`，建立名為 `runtime`. 按一下 **[!UICONTROL 全部儲存]**.

   1. 在 `/apps/ws/js/runtime`，建立名為 `templates`. 按一下 **[!UICONTROL 全部儲存]**.

   1. 複製 `/libs/ws/js/main.js` to `/apps/ws/js/main.js`.

   1. 將/libs/ws/js/registry.js複製到 `/apps/ws/js/registry.js`.

1. 按一下 **[!UICONTROL 全部儲存]**、清除快取，以及重新整理AEM Forms工作區。

   存取URL `https://'[server]:[port]'/lc/ws` 並使用管理員/密碼憑據登錄。 瀏覽器重新導向至 `https://'[server]:[port]'/lc/apps/ws/index.html`.
