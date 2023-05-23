---
title: AEM Forms工作區定製的一般步驟
seo-title: Generic steps for AEM Forms workspace customization
description: 如何開始自定義AEM Forms工作區用戶介面。
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

# AEM Forms工作區定製的一般步驟 {#generic-steps-for-aem-forms-workspace-customization}

執行任何自定義的一般步驟包括：

1. 通過訪問登錄CRXDE Lite `https://'[server]:[port]'/lc/crx/de/index.jsp`。
1. 建立 `sling:Folder` 資料夾 `ws` 在 `/apps`，也請參見Wiki頁。 建立 `sling:Folder` 資料夾，按一下右鍵 `apps` 資料夾和 **[!UICONTROL 建立]** > **[!UICONTROL 建立節點]**。 將名稱指定為 `ws`按鈕 `sling:Folder` 按一下 **[!UICONTROL 確定]**。 按一下 **[!UICONTROL 全部保存]**。
1. 瀏覽到 `/apps/ws`，並導航至 **[!UICONTROL 訪問控制]** 頁籤。
1. 選擇 **[!UICONTROL 儲存庫]** 的雙曲餘切值。 在 **[!UICONTROL 訪問控制]** 清單，按一下 **[!UICONTROL +]** 的子菜單。 按一下 **[!UICONTROL +]** 的雙曲餘切值。
1. 搜索並選擇 **PERM_WORKSPACE_USER** 校長。

   ![選擇PERM_WORKSPACE_USER承擔者作為定制HTML工作區的一般步驟的一部分](assets/perm_workspace_user.png)

1. 提供 `jcr:read` 權限。
1. 按一下 **[!UICONTROL 全部保存]**。
1. 複製 `GET.jsp`。 `index`, `html.jsp` 檔案 `/libs/ws` 資料夾 `/apps/ws` 的子菜單。
1. 複製 `/libs/ws/locales` 資料夾 `/apps/ws` 的子菜單。 按一下 **[!UICONTROL 全部保存]**。
1. 更新中的參照和相對路徑 `GET.jsp` 檔案，如下所示，然後按一下 **[!UICONTROL 全部保存]**。

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. 對CSS自定義項執行以下操作：

   1. 導航到 `/apps/ws` 資料夾，並建立名為 `css`。

   1. 在 `css` 資料夾，建立名為 `newStyle.css`。

   1. 開啟 `/apps/ws/html`.jsp和更改自

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
   >將用戶定義的CSS檔案的條目置於style.css條目之後，如上所示。

1. 在/apps/ws/html.jsp檔案中，更改

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   至

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 請執行下列動作：

   1. 建立名為 `js` 在 `/apps/ws`。 按一下 **[!UICONTROL 全部保存]**。

   1. 建立名為 `libs` 在 `/apps/ws/js`。 按一下 **[!UICONTROL 全部保存]**。

   1. 複製 `/libs/ws/js/libs/jqueryui` 資料夾 `/apps/ws/js/libs`。 按一下 **[!UICONTROL 全部保存]**。

1. 執行以下HTML自定義：

   1. 下 `/apps/ws/js`，建立名為 `runtime`。 按一下 **[!UICONTROL 全部保存]**。

   1. 下 `/apps/ws/js/runtime`，建立名為 `templates`。 按一下 **[!UICONTROL 全部保存]**。

   1. 複製 `/libs/ws/js/main.js` 至 `/apps/ws/js/main.js`。

   1. 將/libs/ws/js/registry.js複製到 `/apps/ws/js/registry.js`。

1. 按一下 **[!UICONTROL 全部保存]**、清除快取並刷新AEM Forms工作區。

   訪問URL `https://'[server]:[port]'/lc/ws` 並使用管理員/密碼憑據登錄。 瀏覽器重定向到 `https://'[server]:[port]'/lc/apps/ws/index.html`。
