---
title: 最適化表單的版面功能
seo-title: Layout capabilities of adaptive forms
description: 各種裝置上最適化表單的版面和外觀由版面設定控制。 了解各種版面及如何套用。
seo-description: Layout and appearances of adaptive forms on various devices are governed by the layout settings. Understand the various layouts and how to apply them.
uuid: 79022ac2-1aa3-47c5-b094-cbe83334ea62
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9459c414-eac9-4bd9-a773-cceaeb736c56
docset: aem65
feature: Adaptive Forms
exl-id: 3db623a4-f1ad-4b7f-97e8-0be138aa8b26
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---

# 最適化表單的版面功能{#layout-capabilities-of-adaptive-forms}

Adobe Experience Manager(AEM)可讓您建立簡單易用的最適化表單，為使用者提供動態體驗。 表單版面會控制項目或元件在最適化表單中的顯示方式。

## 必備知識 {#prerequisite-knowledge}

了解最適化表單的不同版面功能之前，請先閱讀下列文章，深入了解最適化表單。

[AEM Forms簡介](../../forms/using/introduction-aem-forms.md)

[製作表單簡介](../../forms/using/introduction-forms-authoring.md)

## 版面類型 {#types-of-layouts}

適用性表單提供下列類型的配置：

**面板版面** 控制面板內的項目或元件在裝置上的顯示方式。

**行動版面** 控制行動裝置上表單的導覽。 如果裝置寬度為768像素或以上，則版面會視為行動版面，並針對行動裝置最佳化。

**工具列版面** 控制窗體中工具欄或面板工具欄中的操作按鈕的放置。

所有這些面板佈局都在以下位置定義：

`/libs/fd/af/layouts`。

>[!NOTE]
>
>若要變更最適化表單的版面，請使用AEM中的「製作模式」。

![CRX儲存庫中的佈局位置](assets/layouts_location_in_crx.png)

## 面板版面配置 {#panel-layout}

表單作者可將版面配置與適用性表單的每個面板（包括根面板）建立關聯。

面板佈局位於 `/libs/fd/af/layouts/panel` 位置。

![最適化表單的根面板面板配置清單](assets/layouts.png)

適用性表單中的面板配置清單

### 回應式 — 單一頁面上的所有項目，無需導覽 {#responsive-everything-on-one-page-without-navigation-br}

使用此面板配置建立回應式配置，可根據裝置的螢幕大小進行調整，而不需進行特殊導覽。

使用此版面，您可以放置多個 **[!UICONTROL 面板最適化表單]** 元件在面板內逐一顯示。

![使用回應式版面的表單，如小螢幕上所示](assets/responsive_layout_seen_on_small_screen.png)

使用回應式版面的表單，如小螢幕上所示

![使用回應式版面的表單，如同在大螢幕上看到的](assets/responsive_layout_seen_on_large_screen.png)

使用回應式版面的表單，如同在大螢幕上看到的

### 精靈 — 多步驟表單，一次顯示一個步驟 {#wizard-a-multi-step-form-showing-one-step-at-a-time}

使用此面板佈局在表單內提供引導式導航。 例如，當您想要在表單中擷取必填資訊，同時逐步引導使用者時，可使用此版面。

使用 `Panel adaptive form` 元件，在面板內提供逐步導覽。 使用此版面時，使用者只有在目前步驟完成後才會移至下一個步驟

```javascript
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![嚮導佈局中多步驟表單的步驟完成表達式](assets/layout-sidebar.png)

嚮導佈局中多步驟表單的步驟完成表達式

![使用精靈版面的表單](assets/wizard-layout.png)

使用精靈的表單

### 折疊式面板設計的版面配置 {#layout-for-accordion-design}

使用此版面，您可以將 `Panel adaptive form` 元件（在具有折疊式面板樣式導覽的面板中）。 使用此配置，您也可以建立可重複的面板。 可重複的面板可讓您視需要動態新增或移除面板。 您可以定義面板重複的次數下限和上限。 此外，基於在面板項中提供的資訊，可動態地確定面板的標題。

摘要運算式可用來顯示使用者在最小化面板的標題中提供的值。

![在最適化表單中使用折疊式功能表配置的可重複面板](assets/repeatable_panels_using_accordion_layout.png)

使用折疊式功能表配置建立的可重複面板

### 頁簽式佈局 — 頁簽顯示在左側 {#tabbed-layout-tabs-appear-on-the-left}

使用此版面，您可以將 `Panel adaptive form` 元件（位於面板中），並搭配Tab導覽。 標籤會放置在面板內容的左側。

![在「頁簽式佈局」中，頁簽顯示在左側](assets/tabbed_layout_left.png)

顯示在面板左側的標籤

### 頁簽式佈局 — 頁簽顯示在頂部 {#tabbed-layout-tabs-appear-on-the-top}

使用此版面，您可以將 `Panel adaptive form` 面板中的元件，帶有定位導航。 標籤會放置在面板內容上方。

![適用性表單中的標籤式版面，頂端有標籤](assets/tabbed_layout_top.png)

顯示在面板頂端的標籤

## 行動版面 {#mobile-layouts}

行動配置可讓使用者在螢幕相對較小的行動裝置上輕鬆導覽。 行動版面使用標籤樣式或嚮導樣式進行表單導航。 套用行動版面可提供整個表單的單一版面。

此版面會使用導覽列和導覽功能表來控制導覽。 導覽列隨即顯示 **&lt;** 和 **>** 圖示表示 **next** 和 **上一個** 導覽表單中的步驟。

行動版面位於 `/libs/fd/af/layouts/mobile/` 位置。 依預設，適用性表單中提供下列行動配置。

![最適化表單中的行動配置清單](assets/mobile-navigation.png)

最適化表單中的行動配置清單

使用行動版面時，若要存取各種表單面板，點選即可使用表單功能表 ![aem6forms_form_menu](assets/aem6forms_form_menu.png) 表徵圖。

### 表單標題中具有面板標題的版面 {#layout-with-panel-titles-in-the-form-header}

如名稱所示，此版面會顯示面板標題以及導覽功能表和導覽列。 此版面也提供「下一步」和「上一步」導覽圖示。

![在表單標題中含有面板標題的行動版面](assets/mobile_layout_with.png)

在表單標題中含有面板標題的行動版面

### 表單標題中不包含面板標題的佈局 {#layout-without-panel-titles-in-the-form-header}

如名稱所示，此版面只會顯示導覽功能表和導覽列，而不顯示面板標題。 此版面也提供「下一步」和「上一步」導覽圖示。

![表單標題中沒有面板標題的行動版面](assets/mobile_layout_without.png)

表單標題中沒有面板標題的行動版面

## 工具欄佈局 {#toolbar-layouts}

工具列版面控制您新增至最適化表單的任何動作按鈕的定位和顯示。 可在表單層級或面板層級新增版面。

![控制按鈕佈局的最適化表單中的工具欄佈局清單](assets/toolbar-layouts.png)

適用性表單中的工具列配置清單

工具欄佈局位於 `/libs/fd/af/layouts/toolbar` 位置。 適用性表單預設提供下列工具列配置。

### 工具列的預設版面 {#default-layout-for-toolbar}

在最適化表單中新增任何動作按鈕時，系統會選取此版面作為預設版面。 選取此版面會針對桌上型電腦和行動裝置顯示相同的版面。

此外，還可以添加包含使用此佈局配置的操作按鈕的多個工具欄。 動作按鈕與表單控制項相關聯。 您可以將工具列設定為面板之前或之後。

![工具列的預設檢視](assets/toolbar_layout_default.png)

工具列的預設檢視

### 工具列的行動版面固定 {#mobile-fixed-layout-for-toolbar}

選取此版面以提供案頭和行動裝置的替代版面。

對於案頭版面，可以使用某些特定標籤添加操作按鈕。 只能使用此配置配置一個工具欄。 如果使用此版面配置了多個工具列，行動裝置會有重疊，且只會顯示一個工具列。 例如，您可以在表單底部或頂端擁有工具列，或在表單中的面板後面或前面。

對於行動版面，您可以使用圖示來新增動作按鈕。

![工具列的行動版面固定](assets/toolbar_layout_mobile_fixed.png)

工具列的行動版面固定
