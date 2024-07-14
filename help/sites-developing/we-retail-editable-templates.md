---
title: 在We.Retail中嘗試可編輯的範本
description: 瞭解如何使用We.Retail在Adobe Experience Manager中試用可編輯的範本。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---

# 在We.Retail中嘗試可編輯的範本{#trying-out-editable-templates-in-we-retail}

使用可編輯的範本，建立和維護範本不再是開發人員專屬的工作。 稱為範本作者的權力使用者現在可以建立範本。 開發人員仍需要設定環境、建立使用者端程式庫和建立要使用的元件，但是當這些基本功能準備就緒後，範本作者就可以彈性地建立和設定範本，而不需要開發專案。

We.Retail中的所有頁面都是以可編輯的範本為基礎，讓非開發人員能調整及自訂範本。

## 正在試用中 {#trying-it-out}

1. 編輯語言主分支的「裝置」頁面。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. 模式選取器不再提供設計模式。 We.Retail的所有頁面都以可編輯的範本為基礎，若要變更可編輯範本的設計，必須在範本編輯器中編輯這些頁面。
1. 從&#x200B;**頁面資訊**&#x200B;功能表選取&#x200B;**編輯範本**。
1. 您正在編輯主圖頁面範本。

   頁面的結構模式可讓您修改範本的結構。 例如，這包括配置容器中允許的元件。

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. 設定配置容器原則以定義容器中允許的元件。

   原則等同於設計組態。

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. 在配置容器的設計對話方塊中，您可以

   * 選取現有原則或建立容器的原則
   * 選取容器中允許的元件
   * 定義將資產拖曳至容器時要置入的預設元件

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. 回到範本編輯器中，您可以在版面配置容器中編輯文字元件的原則。

   這可讓您：

   * 選取現有原則或建立容器的原則
   * 定義頁面作者使用此元件時可用的功能，例如

      * 允許的貼上來源
      * 格式化選項
      * 允許的段落樣式
      * 允許的特殊字元

   許多以核心元件為基礎的元件，都允許透過可編輯的範本在元件層級設定選項，免除開發人員自訂的需求。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 回到範本編輯器，您可以使用模式選取器變更為&#x200B;**初始內容**&#x200B;模式，以定義頁面上所需的內容。

   **配置**&#x200B;模式可以使用，因為它位於定義範本配置的一般頁面。

## 更多資訊 {#more-information}

如需進一步資訊，請參閱撰寫檔案[建立頁面範本](/help/sites-authoring/templates.md)或開發人員檔案頁面[範本 — 可編輯](/help/sites-developing/page-templates-editable.md)，以取得可編輯範本的完整技術細節。

您可能也想要調查[核心元件](/help/sites-developing/we-retail-core-components.md)。 請參閱撰寫檔案[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)，以取得核心元件功能的概述，以及開發人員檔案[開發核心元件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)，以取得技術概述。
