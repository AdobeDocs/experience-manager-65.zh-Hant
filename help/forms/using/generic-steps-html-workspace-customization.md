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
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4

---


# AEM Forms工作區自訂的一般步驟{#generic-steps-for-aem-forms-workspace-customization}

執行任何自訂的一般步驟包括：

1. 存取以登入CRXDE Lite `https://[server]:[port]/lc/crx/de/index.jsp`。
1. 如果資料夾不存 `ws`在 `/apps`，請建立名為的資料夾。 按一下「 **[!UICONTROL 全部儲存]**」。
1. 瀏覽至 `/apps/ws`「存取控制」索 **[!UICONTROL 引標籤]** 。
1. 在「存 **[!UICONTROL 取控制]** 」清單中，按 **** 一下+以新增項目。 再按 **[!UICONTROL 一下]** +。
1. 搜索並選擇 **PERM_WORKSPACE_USER** Principal。

   ![選擇「PERM_WORKSPACE_USER承擔者」作為定制HTML工作區的一般步驟的一部分](assets/perm_workspace_user.png)

1. 給 `jcr:read` 校長特權。
1. 按一下「 **[!UICONTROL 全部儲存]**」。
1. 將和文 `GET.jsp` 件 `html.jsp`從資料夾 `/libs/ws`複製到文 `/apps/ws` 件夾。
1. 複製資 `/libs/ws/locales` 料夾中的資 `/apps/ws` 料夾。 按一下「 **[!UICONTROL 全部儲存]**」。
1. 更新檔案中的參照和相對路徑(如 `GET.jsp` 下所示)，然後按一下「 **[!UICONTROL 全部保存」]**。

   ```
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. 請針對CSS自訂執行下列動作：

   1. 導覽至資 `/apps/ws` 料夾並建立新資料夾 `css`。

   1. 在檔案 `css`夾資料夾中，建立名為的新檔案 `newStyle.css`。

   1. 開啟 `/apps/ws/html`.jsp並從

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   至

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >將使用者定義的CSS檔案項目置於newStyle.css項目之後，如上所示。

1. 在/apps/ws/html.jsp檔案中，從

   ```css
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   至

   ```css
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 執行下列動作：

   1. 建立名為的 `js`資料夾 `/apps/ws`。 按一下「 **[!UICONTROL 全部儲存]**」。

   1. 建立名為的 `libs`資料夾 `/apps/ws/js`。 按一下「 **[!UICONTROL 全部儲存]**」。

   1. 建立名為的 `jqueryui`資料夾 `/apps/ws/js/libs`。 按一下「 **[!UICONTROL 全部儲存]**」。

   1. 複製 `/libs/ws/js/libs/jqueryui/jquery.ui.datepicker-ja.js` 至 `/apps/ws/js/libs/jqueryui`。 按一下「 **[!UICONTROL 全部儲存]**」。

1. 請針對HTML自訂執行下列動作：

   1. 在下 `/apps/ws/js`面，建立名為的資料夾 `runtime`。 按一下「 **[!UICONTROL 全部儲存]**」。

   1. 在下 `/apps/ws/js/runtime`面，建立名為的資料夾 `templates`。 按一下「 **[!UICONTROL 全部儲存]**」。

   1. 複製 `/libs/ws/js/main.js` 至 `/apps/ws/js/main.js`。

   1. 將/libs/ws/js/registry.js複製至 `/apps/ws/js/registry.js`。

1. 按一 **[!UICONTROL 下「全部儲存]**」、清除快取並重新整理AEM Forms工作區。

   存取URL並 `https://[server]:[port]/lc/ws` 使用管理員／密碼憑證登入。 瀏覽器會重新導向 `https://[server]:[port]/lc/apps/ws/index.html`至。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
