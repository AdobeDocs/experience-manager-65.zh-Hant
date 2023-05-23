---
title: HTML5表格簡介
seo-title: Introduction to HTML5 forms
description: HTML5表單是Adobe Experience Manager6.0(AEM6.0)軟體中的一項新功能，它提供以HTML5格式呈現XFA表單模板。
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

# HTML5表格簡介{#introduction-to-html-forms}

HTML5表單是Adobe Experience Manager6.0(AEM6.0)軟體中的一項新功能，它提供以HTML5格式呈現XFA表單模板。 此功能允許在不支援基於XFA的PDF的移動設備和案頭瀏覽器上呈現表單。 HTML5表單不僅支援XFA表單模板的現有功能，還為移動設備添加了新功能，如手寫簽名。

HTML5表單基於標準HTML5構造生成文檔。 您可以在支援HTML5的所有現代瀏覽器中查看HTML5窗體。 它不需要為瀏覽器安裝任何其他瀏覽器插件。 有關支援的瀏覽器的詳細資訊，請參見 [支援的客戶端平台](https://adobe.com/go/learn_aemforms_supportedplatforms_63)。

![](do-not-localize/mobile_form_on_an_ipad_date_14.png)

## HTML5表單的關鍵功能 {#key-capabilities-of-html-forms-br}

* 在所有相容瀏覽器上都支援HTML5中的現有XFA表單。
* 將標準XFA表單設計功能用於移動設備的目標表單。
* 使用HTML5格式的動態XFA功能。
* 使用高度準確的SVG文本佈局(SVG1.1)與PDF文本佈局匹配。
* 提供對JavaScript和FormCalc的支援。
* 基於資料驅動事件或用戶輸入將片段動態地組合成互動式表單。
* 支援自定義CSS以根據企業標準匹配表單的外觀。
* 使自定義小部件能夠提供豐富的資料捕獲體驗。
* 支援與Web應用整合。

### 多渠道發佈 {#multichannel-publishing}

表單開發人員可以使用XFA模板以PDF和HTML5格式呈現表單。 此功能在您擁有大量XFA表單的情形中非常有益，這些表單要求最少的更改，以適應HTML5表單設計實踐。 您可以將現有的XFA表單呈現為HTML5，以針對尚不支援基於XFA的PDF的各種設備。

## 管理HTML5窗體 {#manage-html-forms}

還提AEM供了使用AEM FormsUI列出和管理所有表單模板的統一視圖。 您可以激活、停用、發佈和預覽表單。 有關詳細資訊，請參見 [管理表單簡介](../../forms/using/introduction-managing-forms.md)。

### Forms定制 {#forms-customization}

HTML5表單使用標準HTML5構造呈現表單模板。 這使用Web技術（主要是CSS和JavaScript）以HTML5格式定制和擴展表單變得簡單。 您可以輕鬆地自定義現有小部件的外觀、建立自己的自定義小部件或在表單中使用自定義樣式。 有關建立自定義小部件和自定義現有小部件的詳細資訊，請參見 [使用HTML5窗體插入自定義小部件](../../forms/using/custom-widgets.md)。
