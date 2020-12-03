---
title: 元件概觀
seo-title: 元件
description: 元件是可實現特定功能的模組，可在您的網站上呈現您的內容
seo-description: 元件是可實現特定功能的模組，可在您的網站上呈現您的內容
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 7%

---


# 元件概述{#components-overview}

本頁概述Adobe Experience Manager(AEM)元件，例如用於製作頁面的[元件。](/help/sites-authoring/default-components-foundation.md)

## 什麼是元件？{#what-exactly-is-a-component}

* 可實現特定功能的模組，以在您的網站上呈現您的內容。
* 可重複使用。
* 開發為儲存庫的一個資料夾中的自含單元。
* 沒有隱藏的配置檔案。
* 可包含其他元件。
* 可在任何AEM系統內的任何位置執行。 也可以限制在特定元件下執行。
* 擁有標準化的使用者介面。
* 具有可設定的編輯行為。
* 使用以Granite UI元件為基礎的子元素所建立的對話方塊
* 使用[HTL](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html)（建議）或JSP進行開發。
* 可開發來建立可擴充預設功能的自訂元件。

由於元件是模組化的，因此您可以：

* 在您的本機執行個體上開發新元件。
* 將它部署至您的測試環境。
* 將它部署至您的即時製作環境，讓作者和／或管理員可在其中新增及設定內容。
* 將它部署至即時發佈環境，以便用來為網站的訪客呈現內容。 某些元件（例如Communities）也接受使用者的輸入。

每個AEM元件：

* 是資源類型。
* 是完全實現特定功能的指令碼集合。
* 可在&#x200B;*isolation*&#x200B;中運作，亦即在AEM或入口網站中運作。

## AEM內的現成可用元件{#out-of-the-box-components-within-aem}

AEM隨附多種[現成可用的元件](/help/sites-authoring/default-components.md)，提供完整的功能，包括：

* 段落系統 ( `parsys`)
* 頁面（`responsivegrid` —— 僅限觸控式UI）
* 文字
* 影像，加上隨附的文字
* 工具列

提供的元件及其在[示例We.Retail網站](/help/sites-developing/we-retail.md)中的使用說明了如何實施和使用元件。 這些元件提供了所有原始碼，可以按原樣使用，或作為修改或擴展元件的起點。

### 核心元件和基礎元件{#core-components-and-foundation-components}

目前提供兩組Adobe提供的AEM元件：

* [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)
* [基礎元件](/help/sites-authoring/default-components-foundation.md)

**核心** 元件已隨AEM 6.3推出，並提供有彈性且功能豐富的製作功能。[We.Retail參考網站](/help/sites-developing/we-retail.md)說明如何使用核心元件並代表元件開發的目前最佳實務。

**Foundation** Components已隨AEM提供許多版本，而且標準AEM安裝中現成可用的Foundation Components。雖然仍受支援，但大部分已過時，不再增強，而且以舊有技術為基礎。

>[!NOTE]
>
>[核心元](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 件代表元件設計與開發的目前最佳範例，並做為參考實作。
>
>[AEM Meduration ](modernization-tools.md) Toolscan可協助您移轉至核心元件。

### 查看可用元件{#viewing-available-components}

如需AEM例項中所有可用元件的概觀，請使用[元件主控台](/help/sites-authoring/default-components-console.md)。

或者，您也可以使用CRXDE Lite來獲取儲存庫中所有可用元件的清單。

1. 在&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;中，從工具列中選擇&#x200B;**[!UICONTROL 工具]**，然後選擇&#x200B;**[!UICONTROL 查詢]**，以開啟&#x200B;**[!UICONTROL 查詢]**&#x200B;頁籤。

1. 在&#x200B;**[!UICONTROL Query]**&#x200B;標籤中，選擇`XPath`作為&#x200B;**[!UICONTROL 類型]**。

1. 在&#x200B;**[!UICONTROL Query]**&#x200B;輸入欄位中，輸入下列字串：

   `//element(*, cq:Component)`

1. 按一下&#x200B;**[!UICONTROL 執行]**&#x200B;並列出元件。

## 其他資源{#further-reading}

以下頁面提供有關開發這些元件和其他元件的詳細資訊：

* [AEM元件——基本概念](/help/sites-developing/components-basics.md)
* [開發AEM元件](/help/sites-developing/developing-components.md)
* [開發AEM元件——程式碼範例](/help/sites-developing/developing-components-samples.md)
* [設定多個就地編輯器](/help/sites-developing/multiple-inplace-editors.md)
* [開發人員模式](/help/sites-developing/developer-mode.md)
* [測試您的UI](/help/sites-developing/hobbes.md)
* [內容片段的元件](/help/sites-developing/components-content-fragments.md)
* [以JSON格式取得頁面資訊](/help/sites-developing/pageinfo.md)
* [國際化元件](/help/sites-developing/i18n.md)
* [核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [使用隱藏條件](/help/sites-developing/hide-conditions.md)
* 傳統 UI

   * [AEM元件(Classic UI)](/help/sites-developing/developing-components-classic.md)
   * [使用和擴充Widget(Classic UI)](/help/sites-developing/widgets.md)
   * [使用xtypes(Classic UI)](/help/sites-developing/xtypes.md)
   * [開發表單(Classic UI)](/help/sites-developing/developing-forms.md)

