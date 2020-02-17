---
title: 最適化表單的版面功能
seo-title: 最適化表單的版面功能
description: 各種裝置上最適化表單的版面配置和外觀都受版面配置設定所控制。 瞭解各種版面及如何套用。
seo-description: 各種裝置上最適化表單的版面配置和外觀都受版面配置設定所控制。 瞭解各種版面及如何套用。
uuid: 79022ac2-1aa3-47c5-b094-cbe83334ea62
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9459c414-eac9-4bd9-a773-cceaeb736c56
docset: aem65
translation-type: tm+mt
source-git-commit: 5a76200a573d95026e2347d2049a089d975b5619

---


# 最適化表單的版面功能{#layout-capabilities-of-adaptive-forms}

Adobe Experience Manager(AEM)可讓您建立簡單易用的調適性表單，為使用者提供動態體驗。 表單版面控制項目或元件在最適化表單中的顯示方式。

## 先決知識 {#prerequisite-knowledge}

在瞭解最適化表單的不同版面功能之前，請先閱讀下列文章，以進一步瞭解最適化表單。

[AEM Forms簡介](../../forms/using/introduction-aem-forms.md)

[製作表單簡介](../../forms/using/introduction-forms-authoring.md)

## 版面類型 {#types-of-layouts}

最適化表單提供下列類型的版面：

**面板配置** ：控制面板內的項目或元件在裝置上的顯示方式。

**行動版面** ：控制行動裝置上表單的導覽。 如果裝置寬度為768像素或以上，則版面會視為行動版面，並針對行動裝置最佳化。

**工具欄佈局** ：控制表單中工具欄或面板工具欄中的「操作」按鈕的位置。

所有這些面板版面都定義在下列位置：

`/libs/fd/af/layouts`.

>[!NOTE]
>
>若要變更最適化表單的版面配置，請使用AEM中的「編寫模式」。

![CRX儲存庫中的版面位置](assets/layouts_location_in_crx.png)

## 面板布局 {#panel-layout}

表單作者可以將版面與最適化表單的每個面板（包括根面板）建立關聯。

「面板」版面可在位 `/libs/fd/af/layouts/panel` 置使用。

![最適化表單根面板的面板版面清單](assets/layouts.png)

最適化表單中的面板版面清單

### Responsive - everything on one page without navigation {#responsive-everything-on-one-page-without-navigation-br}

使用此面板版面可建立回應式版面，可根據裝置的螢幕大小進行調整，而不需進行特殊導覽。

使用此版面，您可以在面板內 **[!UICONTROL 逐一放置多個面板最適化表單元]** 。

![使用回應式版面的表單，如小螢幕上所見](assets/responsive_layout_seen_on_small_screen.png)

使用回應式版面的表單，如小螢幕上所見

![使用回應式版面的表單，如大螢幕上所見](assets/responsive_layout_seen_on_large_screen.png)

使用回應式版面的表單，如大螢幕上所見

### 精靈——一次顯示一個步驟的多步驟表單 {#wizard-a-multi-step-form-showing-one-step-at-a-time}

使用此面板版面，在表單中提供引導導覽。 例如，當您想要在表單中擷取必要資訊，並逐步引導使用者時，請使用此版面。

使用 `Panel adaptive form` 元件在面板中提供逐步導覽。 當您使用此版面時，使用者只有在目前步驟完成後才會移至下一個步驟

```
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![精靈版面中多步驟表單的步驟完成運算式](assets/layout-sidebar.png)

精靈版面中多步驟表單的步驟完成運算式

![使用精靈版面的表單](assets/wizard-layout.png)

使用精靈的表單

### 手風琴設計的版面 {#layout-for-accordion-design}

使用此版面，您可以使用accordion `Panel adaptive form` 樣式導覽將元件置於面板中。 使用此版面配置，您也可以建立可重複的面板。 可重複的面板可讓您視需要動態新增或移除面板。 您可以定義面板重複的最小和最大次數。 此外，根據在面板項目中提供的資訊，可以動態地確定面板的標題。

摘要運算式可用來在最小化面板的標題中顯示使用者提供的值。

![在可調式表單中使用Accordion版面配置的可重複面板](assets/repeatable_panels_using_accordion_layout.png)

使用Accordion版面建立的可重複面板

### 標籤式版面——標籤會出現在左側 {#tabbed-layout-tabs-appear-on-the-left}

使用此版面，您可以將元件置 `Panel adaptive form` 於具有標籤導覽的面板中。 標籤會置於面板內容的左側。

![在標籤式版面中，標籤會出現在左側](assets/tabbed_layout_left.png)

顯示在面板左側的標籤

### 標籤式版面——標籤會出現在頂端 {#tabbed-layout-tabs-appear-on-the-top}

使用此版面，您可將「元件」 `Panel adaptive form` 置於具有標籤導覽的面板中。 標籤會置於面板內容的頂端。

![在最適化表單中的標籤式版面配置，其頂端有標籤](assets/tabbed_layout_top.png)

顯示在面板頂部的標籤

## 行動版面 {#mobile-layouts}

行動版面可讓使用者在螢幕較小的行動裝置上輕鬆導覽。 行動版面使用標籤式或精靈樣式來導覽表單。 套用行動版面為整個表單提供單一版面。

此版面會使用導覽列和導覽選單來控制導覽。 導覽列會顯示&lt; **and** >圖示，以指 **示表單中** 的下一 ******** 個和先前導覽步驟。

您可在位置取得行動版 `/libs/fd/af/layouts/mobile/` 面。 依預設，下列行動版面會以最適化表單提供。

![最適化表單中的行動版面清單](assets/mobile-navigation.png)

最適化表單中的行動版面清單

使用行動版面時，可點選 ![aem6forms_form_menu圖示來使用表單選單，以存取各種表單面板](assets/aem6forms_form_menu.png) 。

### 在表格標題中包含面板標題的版面 {#layout-with-panel-titles-in-the-form-header}

如名稱所示，此版面會顯示面板標題以及導覽選單和導覽列。 此版面也提供「下一頁」和「上一頁」圖示以進行導覽。

![在表格標題中包含面板標題的行動版面](assets/mobile_layout_with.png)

在表格標題中包含面板標題的行動版面

### 在表格標題中不含面板標題的版面 {#layout-without-panel-titles-in-the-form-header}

如名稱所示，此版面僅顯示導覽選單和導覽列，而無面板標題。 此版面也提供「下一頁」和「上一頁」圖示以進行導覽。

![在表格標題中不含面板標題的行動版面](assets/mobile_layout_without.png)

在表格標題中不含面板標題的行動版面

## 工具列版面 {#toolbar-layouts}

「工具列配置」可控制您新增至最適化表單的任何動作按鈕的定位和顯示。 您可在表單層級或面板層級新增版面。

![以最適化表單控制按鈕版面的工具列版面清單](assets/toolbar-layouts.png)

最適化表單中的工具列版面清單

工具列的版面可在位 `/libs/fd/af/layouts/toolbar` 置使用。 最適化表單預設提供下列工具列版面。

### 工具列的預設版面 {#default-layout-for-toolbar}

當您在最適化表單中新增任何動作按鈕時，此版面會選取為預設版面。 選取此版面會針對桌上型電腦和行動裝置顯示相同的版面。

此外，您也可以新增多個工具列，其中包含使用此配置設定的動作按鈕。 動作按鈕與表單控制項相關聯。 您可以將工具列設定為在面板之前或之後。

![工具列的預設檢視](assets/toolbar_layout_default.png)

工具列的預設檢視

### 工具列的行動固定版面 {#mobile-fixed-layout-for-toolbar}

選取此版面，為桌上型電腦和行動裝置提供替代版面。

對於案頭版面，您可以使用某些特定標籤來新增動作按鈕。 只能使用此版面配置一個工具列。 如果使用此版面配置了多個工具列，則行動裝置會有重疊，而且只會顯示一個工具列。 例如，您可以在表格底部或上方有工具列，或在表格中的面板後或之前。

對於行動版面，您可以使用圖示來新增動作按鈕。

![工具列的行動固定版面](assets/toolbar_layout_mobile_fixed.png)

工具列的行動固定版面

