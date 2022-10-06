---
title: HTML5表單簡介
seo-title: Introduction to HTML5 forms
description: HTML5表單是Adobe Experience Manager 6.0(AEM 6.0)軟體中的新功能，可以呈現HTML5格式的XFA表單範本。
seo-description: HTML5 forms is a new capability in Adobe Experience Manager 6.0 (AEM 6.0) software that offers rendering of XFA form templates in HTML5 format.
uuid: 63a2f000-c4c5-40e8-ab3f-c7c44c79ec09
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 672ee050-63d1-46ed-bef2-f55800208d78
docset: aem65
feature: Mobile Forms
exl-id: 0facca18-ffa1-420c-859a-6f1f2c449d71
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# HTML5表單簡介{#introduction-to-html-forms}

HTML5表單是Adobe Experience Manager 6.0(AEM 6.0)軟體中的新功能，可以呈現HTML5格式的XFA表單範本。 此功能可讓您在不支援XFA型PDF的行動裝置和案頭瀏覽器上轉譯表單。 HTML5表單不僅支援XFA表單範本的現有功能，還為行動裝置新增了新功能，例如手寫簽名。

HTML5表單根據標準HTML5結構生成文檔。 您可以在所有支援HTML5的現代瀏覽器中檢視HTML5表單。 不需要為瀏覽器安裝任何其他瀏覽器外掛程式。 如需支援瀏覽器的詳細資訊，請參閱 [支援的用戶端平台](https://adobe.com/go/learn_aemforms_supportedplatforms_63).

![](do-not-localize/mobile_form_on_an_ipad_date_14.png)

## HTML5表單的主要功能 {#key-capabilities-of-html-forms-br}

* 在所有相容的瀏覽器上，都支援以HTML5轉譯現有XFA表單。
* 運用標準XFA表單設計功能，將表單鎖定在行動裝置上。
* 以HTML5格式使用動態XFA功能。
* 使用高度精確的SVG文字版面(SVG1.1)來比對PDF文字版面。
* 提供JavaScript和FormCalc的支援。
* 根據資料導向事件或使用者輸入，以動態方式將片段組合為互動式表單。
* 支援自訂CSS，以根據您的企業標準比對表單的外觀。
* 啟用自訂Widget，以提供豐富的資料擷取體驗。
* 支援與網頁應用程式整合。

### 多頻道發佈 {#multichannel-publishing}

表單開發人員可使用XFA範本，以PDF和HTML5格式轉譯表單。 若您有大量XFA表單，且需進行最少變更，才能適應HTML5表單設計實務，則此功能非常實用。 您可以將現有的XFA表單轉譯為「HTML5」，以鎖定目前不支援XFA型PDF的各種裝置。

## 管理HTML5表單 {#manage-html-forms}

AEM也提供使用AEM Forms UI統一清單和管理所有表單範本的檢視。 您可以啟用、停用、發佈和預覽表單。 如需詳細資訊，請參閱 [管理表單簡介](../../forms/using/introduction-managing-forms.md).

### Forms自訂 {#forms-customization}

HTML5表單使用標準HTML5結構轉譯表單範本。 這可讓您透過網頁技術（主要是CSS和JavaScript），輕鬆自訂及擴充HTML5格式的表單。 您可以輕鬆自訂現有小工具的外觀、建立您自己的自訂小工具，或在表單中使用自訂樣式。 有關建立自定義小部件和自定義現有小部件的詳細資訊，請參閱 [使用HTML5表單插入自訂Widget](../../forms/using/custom-widgets.md).
