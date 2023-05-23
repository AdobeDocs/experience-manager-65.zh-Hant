---
title: 元件概觀
seo-title: Components
description: 元件是模組化單元，可實現特定功能以在您的網站上展示您的內容
seo-description: Components are modular units which realize specific functionality to present your content on your website
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 52%

---

# 元件概觀{#components-overview}

此頁面概述了 Adobe Experience Manager (AEM) 元件，例如那些[用於頁面編寫](/help/sites-authoring/default-components-foundation.md) 的元件。

## 元件有哪些？ {#what-exactly-is-a-component}

* 一種模組化單元，可實現特定功能以在您的網站上展示您的內容。
* 可重複使用。
* 在存放庫的一個資料夾中開發為獨立單元。
* 沒有隱藏的設定檔案。
* 可以包含其他元件。
* 可以在任何系統內的任AEM何位置運行。 它們也可以限制在特定元件下運行。
* 具有標準化的使用者介面。
* 具有可以設定的編輯行為。
* 使用基於Granite UI元件使用子元素構建的對話框
* 使用 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) （推薦）或JSP。
* 可以開發以建立擴充預設功能的自訂元件。

因為元件是模組化的，所以您可以：

* 在您的本機執行個體上開發新元件。
* 將其部署到測試環境。
* 將其部署到即時編寫環境，作者和/或管理員可以在其中新增和設定內容。
* 將其部署到即時發佈環境，它們用於為您網站訪客呈現內容。某些元件（例如社區）也接受用戶的輸入。

每個 AEM 元件：

* 是資源類型。
* 是完整實現特定功能的指令碼集合。
* 可以在 *隔離*，意思是在AEM門戶或門戶中。

## 內的出廠設定組AEM件 {#out-of-the-box-components-within-aem}

AEM有多種 [現成元件](/help/sites-authoring/default-components.md) 提供全面功能，包括：

* 段落系統 ( `parsys`)
* 頁( `responsivegrid`  — 僅支援觸摸的UI)
* 文字
* 影像，附帶文本
* 工具列

所提供的元件及其在 [We.Retail網站示例](/help/sites-developing/we-retail.md) 提供了如何實現和使用元件的說明。 這些元件隨附所有原始程式碼，可以按原狀使用，也可以做為修改或擴充元件的起點。

### 核心元件和基礎元件 {#core-components-and-foundation-components}

有兩組Adobe提供AEM的元件：

* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [基礎元件](/help/sites-authoring/default-components-foundation.md)

**核心元件** 6.AEM3推出，提供靈活且功能豐富的創作功能。 的 [We.Retail參考網站](/help/sites-developing/we-retail.md) 說明了如何使用核心元件並表示元件開發的當前最佳做法。

**基礎元件** 已在許AEM多版本中提供，並且在標準安裝中提供現AEM成。 儘管仍受支援，但大多數已棄用，不再增強，並基於舊式技術。

>[!NOTE]
>
>[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 代表元件設計和開發的當前最佳做法，並作為參考實施。
>
>[現代化AEM工具](modernization-tools.md) 可幫助遷移至核心元件。

### 檢視可用元件 {#viewing-available-components}

如需 AEM 執行個體中所有可用元件的概觀，請使用[元件主控台](/help/sites-authoring/default-components-console.md)。

或者，您也可以使用 CRXDE Lite 取得存放庫中所有可用元件的清單。

1. 在 **[!UICONTROL CRXDE Lite]** 中，從工具列中選擇&#x200B;**[!UICONTROL 工具]**，然後選擇&#x200B;**[!UICONTROL 查詢]**，**[!UICONTROL 查詢]**&#x200B;索引標籤會隨即開啟。

1. 在&#x200B;**[!UICONTROL 查詢]**&#x200B;索引標籤中，選擇 `XPath` 作為 **[!UICONTROL 類型]**。

1. 在&#x200B;**[!UICONTROL 查詢]** 輸入欄位，輸入以下字串：

   `//element(*, cq:Component)`

1. 按一下&#x200B;**[!UICONTROL 執行]**，元件隨即列出。

## 其他資源 {#further-reading}

以下頁提供了有關開發這些元件和其它元件的詳細資訊：

* [組AEM件 — 基礎](/help/sites-developing/components-basics.md)
* [開發組AEM件](/help/sites-developing/developing-components.md)
* [開發AEM元件 — 代碼示例](/help/sites-developing/developing-components-samples.md)
* [配置多個就地編輯器](/help/sites-developing/multiple-inplace-editors.md)
* [開發人員模式](/help/sites-developing/developer-mode.md)
* [測試您的UI](/help/sites-developing/hobbes.md)
* [內容片段的元件](/help/sites-developing/components-content-fragments.md)
* [獲取JSON格式的頁資訊](/help/sites-developing/pageinfo.md)
* [國際化元件](/help/sites-developing/i18n.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [使用隱藏條件](/help/sites-developing/hide-conditions.md)
* 傳統 UI

   * [組AEM件（經典UI）](/help/sites-developing/developing-components-classic.md)
   * [使用和擴展小部件（經典UI）](/help/sites-developing/widgets.md)
   * [使用xtypes（經典UI）](/help/sites-developing/xtypes.md)
   * [開發Forms（經典UI）](/help/sites-developing/developing-forms.md)
