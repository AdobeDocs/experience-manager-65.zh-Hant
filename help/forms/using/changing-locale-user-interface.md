---
title: 更改AEM Forms工作區用戶介面的區域設定
seo-title: Changing the locale of AEM Forms workspace user interface
description: 如何修改AEM Forms工作區以本地化介面上的文本、折疊的類別、隊列和進程以及日期選取器。
seo-description: How to modify the AEM Forms workspace to localize text, collapsed categories, queues, and processes, and the date picker on the interface.
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
exl-id: 9a069486-02a8-4058-adfb-4e0e49d8c0cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# 更改AEM Forms工作區用戶介面的區域設定{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms工作區為英語、法語、德語和日語提供開箱即用支援。 它還提供將AEM Forms工作區用戶介面本地化為任何其他語言的功能。

要將AEM Forms工作區用戶介面本地化為您選擇的語言，請執行以下操作：

* 本地化AEM Forms工作區的文本。
* 本地化折疊的類別、隊列和進程。
* 本地化日期選取器

在執行上述步驟之前，請確保遵循中列出的步驟 [AEM Forms工作區定製的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md)。

>[!NOTE]
>
>要更改AEM Forms工作區登錄螢幕的語言，請參見 [建立新登錄螢幕](../../forms/using/creating-new-login-screen.md)。

## 本地化文本 {#localizing-text}

執行以下步驟以添加對語言的支援 *新建* 和瀏覽器區域設定代碼 *西*。

1. 登錄到CRXDE Lite。
預設CRXDE LiteURL為 `https://'[server]:[port]'/lc/crx/de/index.jsp`。
1. 導航到位置 `apps/ws/locales` 建立新資料夾 `nw.`
1. 複製檔案 `translation.json`從位置 `/apps/ws/locales/en-US` 到位置 `/apps/ws/locales/nw` 。
1. 導航到 `/apps/ws/locales/nw` 開啟 `translation.json` 的子菜單。 對translation.json檔案進行特定於區域設定的更改。

   以下示例包含用於AEM Forms工作區的英文和法文語言環境的translation.json檔案。

   ![轉換_json_in_en](assets/translation_json_in_en.png) ![轉換_json_in_fr](assets/translation_json_in_fr.png)

## 本地化折疊的類別、隊列和進程 {#localizing-collapsed-categories-queues-and-processes}

AEM Forms工作區使用影像來顯示類別、隊列和進程的標題。 您需要開發包來本地化這些標頭。 有關建立開發包的詳細資訊，請參見 [正在生成AEM Forms工作區代碼。](introduction-customizing-html-workspace.md#building-html-workspace-code)

在以下步驟中，假定新的本地化影像檔案 *類別_nw.png*。 *Queue_nw.png*, *進程_nw.png*。 建議的影像寬度為19像素。

>[!NOTE]
>
>查找瀏覽器的瀏覽器語言區域設定代碼。 開啟 `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![折疊_面板_影像](assets/collapsing_panels_image.png)

執行以下步驟來本地化映像：

1. 使用WebDAV客戶端，將映像檔案放在 */apps/ws/images* 的子菜單。
1. 導航到 */apps/ws/css*。 開啟 *newStyle.css* 編輯和添加以下條目：

   ```css
   #categoryListBar .content.nw {
        background: #3e3e3e url(../images/Categories_nw.png) no-repeat 10px 10px;
    }
   
   #filterListBar .content.nw {
       background: #3e3e3e url(../images/Queues_nw.png) no-repeat 10px 10px;
   }
   
   #processNameListBar .content.nw {
       background: #3e3e3e url(../images/Processes_nw.png) no-repeat 10px 10px;
   }
   ```

1. 執行中列出的所有語義更改 [工作區自定義](../../forms/using/introduction-customizing-html-workspace.md) 文章。
1. 導航到 *js/runtime/utility* 資料夾並開啟 *usersession.js* 檔案。
1. 找到原始代碼塊中列出的代碼並添加條件 *郎！== &#39;nw&#39;* 至if語句：

   ```javascript
   // Orignal code
   setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

   ```javascript
   //new code
    setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP' && lang !== 'nw')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

## 本地化日期選取器 {#localizing-date-picker}

您需要開發包來本地化 *日期選擇器* API。 有關建立開發包的詳細資訊，請參見 [正在生成AEM Forms工作區代碼](introduction-customizing-html-workspace.md#building-html-workspace-code)。

1. 下載並解壓 [jQuery UI包](https://jqueryui.com/download/all/)，導航 *&lt;extracted jquery=&quot;&quot; ui=&quot;&quot; package=&quot;&quot;>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n。
1. 將區域設定代碼nw的jquery.ui.datepicker-nw.js檔案複製到apps/ws/js/libs/jquerui，並對檔案進行特定於區域設定的更改。
1. 導航到 `apps/ws/js` 開啟 `jquery.ui.datepicker-nw.js` 檔案。
1. 在main.js檔案中，為 `jquery.ui.datepicker-nw.js.` 為 `jquery.ui.datepicker-nw.js` 檔案為：

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. 使用別名 `jqueryuidatepickernw` 包含 `jquery.ui.datepicker-nw.js` 檔案。 日期選取器用於以下檔案：

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   下面的示例代碼說明如何添加jquery.ui.datepicker-nw.js的條目：

   ```json
   //Original Code
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, slimScroll, UserSearch, LogManager, Logger) {
   ```

   ```json
   // Code with Date Picker alias for new language
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'jqueryuidatepickernw', // Date Picker alias
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, jQueryUIDatePickerNW, slimScroll, UserSearch, LogManager, Logger) {
   ```

1. 在使用datepicker API的所有檔案中，更改預設datepicker API設定。 日期選取器API用於以下檔案：

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   更改以下代碼以添加新區域設定：

   ```javascript
   if (locale === 'ja-JP') {
      $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
      $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
      $.datepicker.setDefaults($.datepicker.regional.fr);
   } else {
      $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```

   ```javascript
   if (locale === 'ja-JP') {
       $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
       $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
       $.datepicker.setDefaults($.datepicker.regional.fr);
   } else if (locale === 'nw') {
       $.datepicker.setDefaults($.datepicker.regional.nw);
   } else {
       $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```
