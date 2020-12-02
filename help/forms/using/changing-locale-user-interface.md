---
title: 變更AEM Forms工作區使用者介面的地區設定
seo-title: 變更AEM Forms工作區使用者介面的地區設定
description: 如何修改AEM Forms工作區，以當地語系化介面上的文字、收合的類別、佇列和程式，以及日期選擇器。
seo-description: 如何修改AEM Forms工作區，以當地語系化介面上的文字、收合的類別、佇列和程式，以及日期選擇器。
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# 變更AEM Forms工作區使用者介面的地區設定{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms工作區提供現成可用的英文、法文、德文和日文支援。 它也提供將AEM Forms工作區使用者介面當地語系化為其他語言的功能。

若要將AEM Forms工作區使用者介面當地語系化為您選擇的語言：

* 將AEM Forms工作區的文字當地語系化。
* 將收合的類別、佇列和程式當地語系化。
* 本地化日期選擇器

在執行上述步驟之前，請確定您遵循[AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md)中所列的步驟。

>[!NOTE]
>
>若要變更AEM Forms工作區登入畫面的語言，請參閱[建立新的登入畫面](../../forms/using/creating-new-login-screen.md)。

## 本地化文本{#localizing-text}

執行以下步驟以添加對語言&#x200B;*New*&#x200B;和瀏覽器語言環境代碼&#x200B;*nw*&#x200B;的支援。

1. 登入CRXDE Lite。
CRXDE Lite的預設URL為`https://'[server]:[port]'/lc/crx/de/index.jsp`。
1. 導覽至`apps/ws/locales`位置並建立新資料夾`nw.`
1. 將檔案`translation.json`從`/apps/ws/locales/en-US`位置複製到`/apps/ws/locales/nw`位置。
1. 導覽至`/apps/ws/locales/nw`並開啟`translation.json`以進行編輯。 對translation.json檔案進行地區設定特定的變更。

   下列範例包含AEM Forms工作區英文和法文地區設定的translation.json檔案。

   ![translation_json_in_](assets/translation_json_in_en.png) ![entranslation_json_in_fr](assets/translation_json_in_fr.png)

## 本地化折疊的類別、隊列和進程{#localizing-collapsed-categories-queues-and-processes}

AEM Forms工作區使用影像來顯示類別、佇列和程式的標題。 您需要開發套件才能將這些標題當地語系化。 如需建立開發套件的詳細資訊，請參閱「建立AEM Forms工作區程式碼」。[](introduction-customizing-html-workspace.md#building-html-workspace-code)

在下列步驟中，假設新的本地化影像檔案為&#x200B;*Categories_nw.png*、*Queue_nw.png*&#x200B;和&#x200B;*Processes_nw.png*。 建議的影像寬度為19像素。

>[!NOTE]
>
>若要尋找瀏覽器的瀏覽器語言地區設定程式碼。 開啟 `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![collapsing_panels_image](assets/collapsing_panels_image.png)

執行下列步驟來本地化影像：

1. 使用WebDAV用戶端，將影像檔案置於&#x200B;*/apps/ws/images*&#x200B;資料夾中。
1. 導覽至&#x200B;*/apps/ws/css*。 開啟&#x200B;*newStyle.css*&#x200B;以進行編輯，並新增下列項目：

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

1. 執行[ Workspace Customization](../../forms/using/introduction-customizing-html-workspace.md)文章中列出的所有語義變更。
1. 導覽至&#x200B;*js/runtime/utility*&#x200B;檔案夾，並開啟&#x200B;*usersession.js*&#x200B;檔案以進行編輯。
1. 找到原始代碼塊中列出的代碼並添加條件&#x200B;*lang !== &#39;nw&#39;*&#x200B;到if陳述式：

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

## 本地化日期選擇器{#localizing-date-picker}

您需要開發套件來本地化&#x200B;*datepicker* API。 如需建立開發套件的詳細資訊，請參閱[建立AEM Forms工作區程式碼](introduction-customizing-html-workspace.md#building-html-workspace-code)。

1. 下載並解壓[jQuery UI包](https://jqueryui.com/download/all/)，導覽至&#x200B;*&lt;解壓縮jquery UI包>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n。
1. 將jquery.ui.datepicker-nw.js檔案的地區設定程式碼新複製到apps/ws/js/libs/jquerui，並對檔案進行地區設定特定變更。
1. 導覽至`apps/ws/js`並開啟`jquery.ui.datepicker-nw.js`檔案以進行編輯。
1. 在main.js檔案中為`jquery.ui.datepicker-nw.js.`建立別名。為`jquery.ui.datepicker-nw.js`檔案建立別名的代碼為：

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. 使用別名`jqueryuidatepickernw`將`jquery.ui.datepicker-nw.js`檔案包含在所有使用日期選擇器的檔案中。 日期選擇器用於下列檔案：

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   以下范常式式碼說明如何新增jquery.ui.datepicker-nw.js項目：

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

1. 在所有使用日期選擇器API的檔案中，變更預設的日期選擇器API設定。 日期選擇器API用於下列檔案：

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   變更下列程式碼以新增地區設定：

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
