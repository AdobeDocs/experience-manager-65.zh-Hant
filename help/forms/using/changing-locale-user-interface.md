---
title: 變更AEM Forms工作區使用者介面的地區設定
description: 如何修改AEM Forms工作區以將文字、摺疊的類別、佇列和程式，以及介面上的日期選擇器當地語系化。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 9a069486-02a8-4058-adfb-4e0e49d8c0cf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# 變更AEM Forms工作區使用者介面的地區設定{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms工作區提供英文、法文、德文和日文的立即可用支援。 此外，它還能將AEM Forms工作區使用者介面本地化為任何其他語言。

若要將AEM Forms工作區使用者介面本地化為您選取的語言：

* 將AEM Forms工作區的文字當地語系化。
* 將收合的類別、佇列和程式當地語系化。
* 將日期選擇器本地化

在執行上述步驟之前，請確定您遵循列於[AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md)中的步驟。

>[!NOTE]
>
>若要變更AEM Forms工作區的登入畫面語言，請參閱[建立登入畫面](../../forms/using/creating-new-login-screen.md)。

## 本地化文字 {#localizing-text}

執行以下步驟，以便您可以新增對語言&#x200B;*New*&#x200B;和瀏覽器地區設定代碼&#x200B;*nw*&#x200B;的支援。

1. 登入CRXDE Lite。
CRXDE Lite的預設URL為`https://'[server]:[port]'/lc/crx/de/index.jsp`。
1. 導覽至位置`apps/ws/locales`並建立資料夾`nw.`
1. 將檔案`translation.json`從位置`/apps/ws/locales/en-US`複製到位置`/apps/ws/locales/nw` 。
1. 導覽至`/apps/ws/locales/nw`並開啟`translation.json`進行編輯。 對translation.json檔案進行地區設定的特定變更。

   下列範例包含AEM Forms工作區英文與法文地區設定的translation.json檔案。

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## 本地化收合的類別、佇列和程式 {#localizing-collapsed-categories-queues-and-processes}

AEM Forms工作區使用影像來顯示類別、佇列和程式的標題。 您需要開發套件將這些標頭當地語系化。 如需有關建立開發套件的詳細資訊，請參閱[建置AEM Forms工作區程式碼。](introduction-customizing-html-workspace.md#building-html-workspace-code)

在下列步驟中，假設新的當地語系化影像檔案為&#x200B;*Categories_nw.png*、*Queue_nw.png*&#x200B;和&#x200B;*Processes_nw.png*。 建議的影像寬度應設為19畫素。

>[!NOTE]
>
>尋找瀏覽器的瀏覽器語言地區設定代碼。 開啟`https://'[server]:[port]'/lc/libs/ws/Locale.html`。

![collapsing_panels_image](assets/collapsing_panels_image.png)

若要將影像當地語系化，請執行下列步驟：

1. 使用WebDAV使用者端，將影像檔案置於&#x200B;*/apps/ws/images*&#x200B;資料夾中。
1. 瀏覽至&#x200B;*/apps/ws/css*。 開啟&#x200B;*newStyle.css*&#x200B;進行編輯並新增下列專案：

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

1. 執行[Workspace Customization](../../forms/using/introduction-customizing-html-workspace.md)文章中列出的所有語意變更。
1. 導覽至&#x200B;*js/runtime/utility*&#x200B;資料夾，並開啟&#x200B;*usersession.js*&#x200B;檔案進行編輯。
1. 找出原始程式碼區塊中列出的程式碼，並新增條件&#x200B;*lang！將&#39;nw&#39;*==入if陳述式：

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

## 將日期選擇器本地化 {#localizing-date-picker}

您需要開發套件才能本地化&#x200B;*日期選擇器* API。 如需建立開發套件的詳細資訊，請參閱[建立AEM Forms工作區程式碼](introduction-customizing-html-workspace.md#building-html-workspace-code)。

1. 下載並解壓縮[jQuery UI套件](https://jqueryui.com/download/all/)，瀏覽至&#x200B;*&lt;解壓縮的jquery UI套件>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n。
1. 將地區設定代碼的jquery.ui.datepicker-nw.js檔案複製到apps/ws/js/libs/jqueryui，並對檔案進行地區設定特有的變更。
1. 導覽至`apps/ws/js`並開啟`jquery.ui.datepicker-nw.js`檔案進行編輯。
1. 在main.js檔案中，為`jquery.ui.datepicker-nw.js.`建立別名。為`jquery.ui.datepicker-nw.js`檔案建立別名的程式碼為：

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. 使用別名`jqueryuidatepickernw`，將`jquery.ui.datepicker-nw.js`檔案納入所有使用日期選擇器的檔案中。 日期選擇器用於下列檔案中：

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   下列範常式式碼顯示如何新增jquery.ui.datepicker-nw.js專案：

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

1. 在使用日期選擇器API的所有檔案中，變更預設的日期選擇器API設定。 日期選擇器API用於以下檔案：

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
