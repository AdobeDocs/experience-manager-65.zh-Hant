---
title: 變更AEM Forms工作區使用者介面的地區設定
seo-title: Changing the locale of AEM Forms workspace user interface
description: 如何修改AEM Forms工作區，將介面上的文字、折疊的類別、佇列和程式，以及日期選取器當地化。
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

# 變更AEM Forms工作區使用者介面的地區設定{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms工作區提供英文、法文、德文和日文語言的立即可用支援。 此外，還提供將AEM Forms工作區使用者介面當地化為任何其他語言的功能。

若要將AEM Forms工作區使用者介面當地化為您所選擇的語言：

* 將AEM Forms工作區的文字本地化。
* 將折疊的類別、佇列和程式本地化。
* 本地化日期選擇器

執行上述步驟之前，請務必遵循 [AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md).

>[!NOTE]
>
>若要變更AEM Forms工作區登入畫面的語言，請參閱 [建立新登入畫面](../../forms/using/creating-new-login-screen.md).

## 將文本本地化 {#localizing-text}

執行下列步驟以新增對語言的支援 *新增* 和瀏覽器地區代碼 *nw*.

1. 登入CRXDE Lite。
預設的CRXDE LiteURL為 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 導覽至位置 `apps/ws/locales` 建立新資料夾 `nw.`
1. 複製檔案 `translation.json`從位置 `/apps/ws/locales/en-US` 位置 `/apps/ws/locales/nw` .
1. 導覽至 `/apps/ws/locales/nw` 開啟 `translation.json` 編輯。 對translation.json檔案進行地區特定變更。

   下列範例包含AEM Forms工作區的英文和法文地區設定的translation.json檔案。

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## 將折疊的類別、佇列和程式本地化 {#localizing-collapsed-categories-queues-and-processes}

AEM Forms工作區使用影像來顯示類別、佇列和程式的標題。 您需要開發套件才能將這些標題當地化。 如需建立開發套件的詳細資訊，請參閱 [建立AEM Forms工作區程式碼。](introduction-customizing-html-workspace.md#building-html-workspace-code)

在下列步驟中，會假設新的本地化影像檔案為 *Categories_nw.png*, *Queue_nw.png*，和 *Processes_nw.png*. 建議的影像寬度為19px。

>[!NOTE]
>
>查找瀏覽器語言區域代碼。 開啟 `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![collapping_panels_image](assets/collapsing_panels_image.png)

執行下列步驟將影像本地化：

1. 使用WebDAV客戶端，將映像檔案放置在 */apps/ws/images* 檔案夾。
1. 導覽至 */apps/ws/css*. 開啟 *newStyle.css* 編輯和添加以下條目：

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

1. 執行 [工作區自訂](../../forms/using/introduction-customizing-html-workspace.md) 文章。
1. 導覽至 *js/runtime/utility* 資料夾並開啟 *usersession.js* 檔案進行編輯。
1. 找出原始程式碼區塊中列出的程式碼，並新增條件 *朗！== &#39;nw&#39;* 至if陳述式：

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

## 本地化日期選擇器 {#localizing-date-picker}

您需要開發套件，才能將 *datepicker* API。 如需建立開發套件的詳細資訊，請參閱 [建立AEM Forms工作區程式碼](introduction-customizing-html-workspace.md#building-html-workspace-code).

1. 下載並解壓縮 [jQuery UI套件](https://jqueryui.com/download/all/)，導覽至 *&lt;extracted jquery=&quot;&quot; ui=&quot;&quot; package=&quot;&quot;>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n。
1. 將區域設定代碼的jquery.ui.datepicker-nw.js檔案複製到apps/ws/js/libs/jqueryui，並對檔案進行區域設定特定的變更。
1. 導覽至 `apps/ws/js` 然後開啟 `jquery.ui.datepicker-nw.js` 檔案進行編輯。
1. 在main.js檔案中，為 `jquery.ui.datepicker-nw.js.` 為 `jquery.ui.datepicker-nw.js` 檔案為：

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. 使用別名 `jqueryuidatepickernw` 包括 `jquery.ui.datepicker-nw.js` 檔案。 日期選擇器用於下列檔案：

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   下列范常式式碼顯示如何新增jquery.ui.datepicker-nw.js項目：

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

1. 在使用日期挑選器API的所有檔案中，變更預設的日期挑選器API設定。 日期挑選器API用於下列檔案：

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
