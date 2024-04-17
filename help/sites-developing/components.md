---
title: 元件概觀
description: 元件是模組化單元，可實現特定功能以在您的網站上展示您的內容
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 44%

---

# 元件概觀{#components-overview}

此頁面概述了 Adobe Experience Manager (AEM) 元件，例如那些[用於頁面編寫](/help/sites-authoring/default-components-foundation.md)的元件。

## 元件有哪些？ {#what-exactly-is-a-component}

* 模組化單元，可實現特定功能以在您的網站上展示您的內容。
* 可重複使用。
* 在存放庫的一個資料夾中開發為獨立單元。
* 沒有隱藏的設定檔案。
* 可以包含其他元件。
* 可以在任何AEM系統中的任何地方執行。 它們也可以被限製為在特定元件下執行。
* 具有標準化的使用者介面。
* 具有可以設定的編輯行為。
* 使用根據Granite UI元件的子元素建置的對話方塊
* 使用開發 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) （建議）或JSP。
* 可以開發以建立擴充預設功能的自訂元件。

因為元件是模組化的，所以您可以：

* 在您的本機執行個體上開發新元件。
* 將其部署到測試環境。
* 將其部署到即時編寫環境，作者和/或管理員可以在其中新增和設定內容。
* 將其部署到您的即時發佈環境，在那裡它們用於呈現網站訪客的內容。 某些元件（例如Communities）也接受使用者的輸入。

每個 AEM 元件：

* 是資源類型。
* 是完整實現特定功能的指令碼集合。
* 可以在中運作 *隔離*，表示在AEM或入口網站中。

## AEM中的現成元件 {#out-of-the-box-components-within-aem}

AEM隨附多種多樣的 [現成可用的元件](/help/sites-authoring/default-components.md) 功能齊全，包括：

* 段落系統( `parsys`)
* 頁面( `responsivegrid`  — 僅限觸控式UI)
* 文字
* 影像，含隨附文字
* 工具列

提供的元件及其在 [範例We.Retail網站](/help/sites-developing/we-retail.md) 已提供如何實作和使用元件的說明。 這些元件隨附所有原始程式碼，可以按原狀使用，也可以做為修改或擴充元件的起點。

### 核心元件與基礎元件 {#core-components-and-foundation-components}

有兩組Adobe提供的AEM元件可供使用：

* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [基礎元件](/help/sites-authoring/default-components-foundation.md)

**核心元件** 推出AEM 6.3，提供有彈性且功能豐富的撰寫功能。 此 [We.Retail參考網站](/help/sites-developing/we-retail.md) 說明如何使用核心元件，並代表元件開發的目前最佳實務。

**基礎元件** 已經在AEM許多版本中提供，並且可在標準AEM安裝中立即使用。 雖然仍受支援，但大部分的功能已過時、不再強化，而且以舊版技術為基礎。

>[!NOTE]
>
>[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 代表元件設計和開發的目前最佳實務，並作為參考實作。
>
>[AEM現代化工具](modernization-tools.md) 可協助移轉至核心元件。

### 檢視可用元件 {#viewing-available-components}

如需AEM執行個體中所有可用元件的總覽，請使用 [元件主控台](/help/sites-authoring/default-components-console.md).

或者，您也可以使用 CRXDE Lite 取得存放庫中所有可用元件的清單。

1. 在 **[!UICONTROL CRXDE Lite]** 中，從工具列中選擇&#x200B;**[!UICONTROL 工具]**，然後選擇&#x200B;**[!UICONTROL 查詢]**，**[!UICONTROL 查詢]**&#x200B;索引標籤會隨即開啟。

1. 在&#x200B;**[!UICONTROL 查詢]**&#x200B;索引標籤中，選擇 `XPath` 作為 **[!UICONTROL 類型]**。

1. 在&#x200B;**[!UICONTROL 查詢]** 輸入欄位，輸入以下字串：

   `//element(*, cq:Component)`

1. 按一下&#x200B;**[!UICONTROL 執行]**，元件隨即列出。

## 其他資源 {#further-reading}

下列頁面提供有關開發這些元件及其他元件的更詳細資訊：

* [AEM元件 — 基本需知](/help/sites-developing/components-basics.md)
* [開發AEM元件](/help/sites-developing/developing-components.md)
* [開發AEM元件 — 程式碼範例](/help/sites-developing/developing-components-samples.md)
* [設定多個就地編輯器](/help/sites-developing/multiple-inplace-editors.md)
* [開發人員模式](/help/sites-developing/developer-mode.md)
* [測試您的UI](/help/sites-developing/hobbes.md)
* [內容片段的元件](/help/sites-developing/components-content-fragments.md)
* [取得JSON格式的頁面資訊](/help/sites-developing/pageinfo.md)
* [國際化元件](/help/sites-developing/i18n.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [使用隱藏條件](/help/sites-developing/hide-conditions.md)
* 傳統 UI

   * [AEM元件（傳統UI）](/help/sites-developing/developing-components-classic.md)
   * [使用和擴充Widget （傳統UI）](/help/sites-developing/widgets.md)
   * [使用xtype （傳統UI）](/help/sites-developing/xtypes.md)
   * [開發Forms (Classic UI)](/help/sites-developing/developing-forms.md)
