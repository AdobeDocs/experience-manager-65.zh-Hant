---
title: 示例ContextHub UI模組類型
seo-title: Sample ContextHub UI Module Types
description: ContextHub提供了幾個示例UI模組，您可以在解決方案中使用這些模組
seo-description: ContextHub provides several sample UI modules that you can use in your solutions
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: df28180f-7af4-437d-8e91-bfd305f73113
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 1%

---

# 示例ContextHub UI模組類型 {#sample-contexthub-ui-module-types}

ContextHub提供了幾個示例UI模組，您可以在解決方案中使用這些模組。 提供了以下資訊：

* UI模組的主要功能。
* 在何處查找原始碼，以便您可以開啟它以用於學習目的。
* 如何配置UI模組。

有關將UI模組添加到ContextHub的資訊，請參見 [添加UI模組](ch-configuring.md#adding-a-ui-module)。 有關開發UI模組的資訊，請參見 [建立ContextHub UI模組類型](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

## contexthub.base UI模組類型 {#contexthub-base-ui-module-type}

contexthub.base UI模組類型是所有其他UI模組類型的基類型。 因此，它提供了用於呈現儲存資料的通用功能。

以下功能可用：

* **標題和表徵圖：** 指定UI模組的標題和表徵圖。 可以使用URL或Coral UI表徵圖庫引用該表徵圖。
* **儲存資料：** 標識要從中檢索資料的一個或多個儲存。
* **內容：** 指定在UI模組中顯示的內容（如ContextHub工具欄中顯示的內容）。
* **跨距內容：** 指定按一下或點擊UI模組時在跨距中顯示的內容。
* **全屏模式：** 控制是否允許全屏模式。

原始碼位於/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。

### 設定 {#configuration}

使用JSON格式的Javascript對象配置contexthub.base UI模組。 包括以下任意屬性以配置UI模組功能：

* **影像：** 要作為表徵圖顯示的影像的URL。
* **表徵圖：** 名稱 [Coral UI表徵圖](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 類。 如果為表徵圖和影像屬性都指定值，則使用影像。

* **標題：** UI模組的標題。 當指針暫停在UI模組表徵圖上時，將顯示標題。
* **全屏：** 指示UI模組是否支援全屏模式的布爾值。 使用 `true` 支援全屏和 `false` 來防止全屏模式。

* **模板：** A [車把](https://handlebarsjs.com/) 指定要在ContextHub工具欄中呈現的內容的模板。 最多使用兩個 `<p>` 標籤。

* **storeMapping:** 密鑰/儲存映射。 使用Handlebar模板中的鍵訪問關聯的ContextHub儲存資料。
* **清單：** 按一下UI模組時，要作為跨距清單顯示的項陣列。 如果包括此項目，則不要包括popoverTemplate。 該值是具有以下鍵的對象陣列：

   * 標題：此項顯示的文本
   * 影像：（可選）應顯示在左側的影像的URL
   * 表徵圖：（可選）應顯示在左側的CUI表徵圖類；如果指定了映像，則忽略
   * 選定：（可選）一個布爾值，它指定是否應將此項目顯示為選定項(true=selected)。 預設情況下，選定項目使用粗體顯示。 使用 `listType` 屬性以配置其他外觀（請參閱下面）。

* **listType:** 用於跨距清單項的樣式。 使用以下值之一：

   * 複選標籤
   * 核取方塊
   * 無線電

* **popover模板：** Handlebars模板，它指定按一下UI模組時要在跨距中呈現的內容。 如果包括此項目，則不要包括 `list` 的子菜單。

### 範例 {#example}

以下示例將contexthub.base UI模組配置為顯示來自 [contexthub.模擬器](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) 商店。 的 `template` 項演示如何使用 `storeMapping` 項目已建立。

```xml
{
   "icon": "coral-Icon--move",
    "title": "Screen Resolution",
    "storeMapping": {
      "emulator": "emulators"
    },
    "template": "<p>{{{ i18n \"Resolution\"}}}</p><p>{{{emulator.currentDevice.width}}} x {{{emulator.currentDevice.height}}}</p>"
}
```

![chlimage_1-76](assets/chlimage_1-76a.png)

## contexthub.browserinfo UI模組類型 {#contexthub-browserinfo-ui-module-type}

contexthub.browserinfo UI模組顯示有關客戶端Web瀏覽器和作業系統的資訊。 根據SurferInfo儲存器 [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) 儲存候選。

![chlimage_1-77](assets/chlimage_1-77a.png)

UI模組的原始碼位於/libs/granite/contexthub/components/modules/browserinfo。 儘管contexthub.browserinfo擴展了contexthub.base UI模組，但它不覆蓋或提供其他功能。 該實現提供了用於呈現瀏覽器資訊的預設配置。

### 設定 {#configuration-1}

contexthub.browserinfo UI模組的實例不需要「詳細配置」的值。 以下JSON文本表示模組的預設配置。

```xml
{
   "icon":"coral-Icon--globe",
   "title":"Browser/OS Information",
   "storeMapping":{"surferinfo":"surferinfo"},
   "template":"<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p><p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>"
}
```

## contexthub.datetime UI模組類型 {#contexthub-datetime-ui-module-type}

contexthub.datetime UI模組顯示儲存在名為datetime的儲存中的日期和時間，該儲存基於 [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) 儲存候選。

![chlimage_1-78](assets/chlimage_1-78a.png)

模組提供了一個跨距表單，使您能夠更改儲存中的日期和時間。

contexthub.datetime UI模組的源位於/libs/granite/contexthub/components/modules/datetime。

### 設定 {#configuration-2}

contexthub.datetime UI模組的實例不需要詳細配置值。 以下JSON文本表示模組的預設配置。

```xml
{
   "icon":"coral-Icon--clock",
   "title":"DATE&TIME",
   "clickable":true,
   "storeMapping":{"d":"datetime"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Date&Time\"}}</p><p class=\"contexthub-module-line2\">{{d.formatted.locale.date}} {{d.formatted.locale.time}}</p>",
   "popoverTemplate":"<div class=\"datetime center\"><div class=\"coral-DatePicker-calendar\" data-init=\"datepicker\"><input class=\"coral-Textfield\" type=\"datetime\" value=\"{{d.formatted.iso}}\"><button class=\"coral-Button coral-Button--secondary coral-Button--square\" title=\"{{i18n \"Datetime picker\"}}\"><i class=\"coral-Icon coral-Icon--calendar coral-Icon--sizeS\"></i></button></div></div>"
}
```

## contexthub.location UI模組類型 {#contexthub-location-ui-module-type}

contexthub.location UI模組顯示客戶端的經度和緯度。 該模組提供一個跨距，顯示一個可按一下以更改當前位置的Google映射。 該模組從名為geolocation的ContextHub儲存中獲取資訊，該ContextHub儲存基於 [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) 儲存候選。

![chlimage_1-80](assets/chlimage_1-80a.png)

UI模組的源位於/etc/cloudsettings/default/contexthub/geolocation。

### 設定 {#configuration-4}

contexthub.location UI模組的實例不需要「詳細配置」的值。 以下JSON文本表示模組的預設配置。

```xml
{
 "icon":"coral-Icon--compass",
 "title":"Location",
 "clickable":true,
 "editable":{"key":"/geolocation","disabled":[],"hidden":["/geolocation/generatedThumbnail","/geolocation/city","/geolocation/country"]},
 "fullscreen":true,
 "storeMapping":{"g":"geolocation"},
 "template":"<p>{{i18n \"Location\"}}</p><p>{{g.address.postalCode}} {{g.address.city}}{{#if g.address.city}}{{#if g.address.region}},{{/if}}{{/if}} {{g.address.region}}</p>",
 "list":[
  {"title":"Basel, Switzerland",
  "data":{"longitude":7.58929,"latitude":47.554746,"city":"Basel","country":"Switzerland"}},
  {"title":"Melbourne, Australia",
  "data":{"longitude":144.96328,"latitude":-37.814107,"city":"Melbourne","country":"Australia"}},
  {"title":"Beijing, China",
  "data":{"longitude":116.407526,"latitude":39.90403,"city":"Beijing","country":"China"}},
  {"title":"New York, NY, USA",
  "data":{"longitude":-74.005973,"latitude":40.714353,"city":"New York","country":"United States"}},
  {"title":"Paris, France",
  "data":{"longitude":2.352222,"latitude":48.856614,"city":"Paris","country":"France"}},
  {"title":"Rio de Janeiro, Brazil",
  "data":{"longitude":-43.20071,"latitude":-22.913395,"city":"Rio","country":"Brazil"}},
  {"title":"San Jose, CA, USA",
  "data":{"longitude":-121.894955,"latitude":37.339386,"city":"San Jose","country":"United States"}},
  {"title":"Tokyo, Japan",
  "data":{"longitude":139.691706,"latitude":35.689487,"city":"Shinjuku","country":"Japan"}}
 ],
 "listType":"checkmark"
}
```

## contexthub.screen-orientation UI模組類型 {#contexthub-screen-orientation-ui-module-type}

contexthub.screen-orientation UI模組顯示客戶端的當前螢幕方向。 雖然在預設情況下禁用了該功能，但該模組提供了一個跨距，使您能夠選擇方向。 該模組從ContextHub儲存中獲取基於 [花崗岩。模擬器](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) 儲存候選。

![chlimage_1-81](assets/chlimage_1-81a.png)

UI模組的源位於/libs/granite/contexthub/components/modules/screen-orientation。

### 設定 {#configuration-5}

contexthub.screen-orientation UI模組的實例不需要「詳細配置」的值。 以下JSON文本表示模組的預設配置。 請注意 `clickable` 屬性 `false` 預設值。 如果覆蓋要設定的預設配置 `clickable` 至 `true`，按一下模組將顯示一個彈出窗口，您可以在其中選擇方向。

```xml
{
   "icon":"coral-Icon--rotateRight",
   "title":"Screen Orientation",
   "clickable":false,
   "storeMapping":{"emulator":"emulators"},
   "template":"<p>{{{ i18n \"Screen Orientation\" }}}</p><p>{{{ emulator.currentDevice.orientation }}}",
   "listReference":"/emulators/orientations",
   "listType":"checkmark"
}
```

## contexthub.tagcloud UI模組類型 {#contexthub-tagcloud-ui-module-type}

contexthub.tagcloud UI模組顯示有關標籤的資訊。 在工具欄上，UI模組顯示標籤數。 彈出菜單顯示了用於添加新標籤的標籤雲和文本框。 UI模組從名為tagcloud的ContextHub儲存中獲取資訊，該儲存基於 [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) 儲存候選。

![chlimage_1-82](assets/chlimage_1-82a.png)

UI模組的源位於/libs/granite/contexthub/components/modules/tagcloud。

### 設定 {#configuration-6}

contexthub.tagcloud UI模組的實例不需要「詳細配置」值。 以下JSON文本表示模組的預設配置。

```xml
{
   "icon":"coral-Icon--tag",
   "title":"TagCloud",
   "clickable":true,
   "storeMapping":{"t":"tagcloud"},
   "maxTags":20,
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"TagCloud\"}}</p><p class=\"contexthub-module-line2\">{{stats.total}} {{i18n \"Tags\"}}</p>",
   "popoverTemplate":"<div class=\"contexthub-popover-content center\"><p class=\"stats\">{{stats.total}} {{i18n \"Tags\"}} | {{stats.hits}} {{i18n \"Hits\"}} | {{i18n \"Last tag\"}}: {{#if stats.recent}}{{stats.recent}}{{else}}{{i18n \"Unknown\"}}{{/if}}</p><p class=\"tagcloud\">{{#each tags}}<span class=\"tag{{this.weight}}\">{{this.name}}</span> {{/each}}</p><div class=\"coral-InputGroup\"><input type=\"text\" class=\"coral-InputGroup-input coral-Textfield tag-name\" placeholder=\"{{i18n \"Add a namespace:my/tag\"}}\" pattern=\"^[A-Za-z0-9_\\-]+(:[A-Za-z0-9_\\-\\/]+)?$\" title=\"{{i18n \"namespace:my/tag\"}}\"><span class=\"coral-InputGroup-button\"><button class=\"coral-Button coral-Button--secondary coral-Button--square contexthub-new-tag\" type=\"button\" title=\"{{i18n \"increment\"}}\"><i class=\"coral-Icon coral-Icon--sizeS coral-Icon--add\"></i></button></span></div></div>"
}
```

## granite.profile UI模組類型 {#granite-profile-ui-module-type}

granite.profile ContextHub UI模組顯示當前用戶的顯示名稱。 彈出菜單顯示用戶的登錄名並允許您更改顯示名的值。 UI模組從ContextHub儲存庫獲取基於 [花崗岩/輪廓](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) 儲存候選。

![chlimage_1-83](assets/chlimage_1-83a.png)

UI模組的源位於/libs/granite/contexthub/components/modules/profile。

### 設定 {#configuration-7}

grantie.profile UI模組的實例不需要「詳細配置」的值。 以下JSON文本表示模組的預設配置。

```xml
{
   "icon":"coral-Icon--user",
   "title":"Profile",
   "clickable":true,
   "editable":{
      "key":"/profile",
      "disabled":["/profile/authorizableId"],
      "hidden":["/profile/avatar","/profile/path"]},
   "storeMapping":{"p":"profile"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Persona\"}}</p><p class=\"contexthub-module-line2\">{{p.displayName}}</p>",
   "listType":"checkmark"
}
```
