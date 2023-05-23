---
title: 在We.Retail中嘗試可編輯模板
seo-title: Trying out Editable Templates in We.Retail
description: 在We.Retail中嘗試可編輯模板
seo-description: null
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 10%

---

# 在We.Retail中嘗試可編輯模板{#trying-out-editable-templates-in-we-retail}

使用可編輯模板，建立和維護模板不再是僅面向開發人員的任務。 一種稱為模板作者的高級用戶現在可以建立模板。 開發人員仍需要設定環境、建立用戶端程式庫和建立要使用的元件，但是當這些基本功能準備就緒後，範本作者就可以彈性地建立和設定範本，而不需要開發專案。

We.Retail中的所有頁面都基於可編輯的模板，允許非開發人員調整和自定義模板。

## 嘗試 {#trying-it-out}

1. 編輯語言主分支的「設備」頁。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. 請注意，模式選擇器不再提供「設計」模式。 We.Retail的所有頁面都基於可編輯模板，要改變可編輯模板的設計，必須在模板編輯器中編輯這些模板。
1. 從 **頁面資訊** 菜單 **編輯模板**。
1. 您現在正在編輯「英雄頁面」模板。

   頁面的結構模式允許您修改模板的結構。 這包括例如佈局容器中允許的元件。

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. 配置佈局容器的策略以定義容器中允許的元件。

   策略與設計配置相當。

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. 在佈局容器的設計對話框中，可以

   * 選擇現有策略或為容器建立新策略
   * 選擇容器中允許的元件
   * 定義將資產拖至容器時要放置的預設元件

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. 返回到模板編輯器中，可以編輯佈局容器中文本元件的策略。

   這允許您：

   * 選擇現有策略或為容器建立新策略
   * 定義使用此元件時頁面作者可用的功能，如

      * 允許貼上源
      * 格式設定選項
      * 允許的段落樣式
      * 允許的特殊字元

   許多基於核心元件的元件都允許通過可編輯模板在元件級別配置選項，從而消除了開發人員進行定製的需要。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 返回到模板編輯器中，可以使用模式選擇器更改為 **初始內容** 的子菜單。

   **佈局** 模式可以使用，因為它位於普通頁面上，以定義模板的佈局。

## 更多資訊 {#more-information}

有關詳細資訊，請參閱創作文檔 [建立頁面模板](/help/sites-authoring/templates.md) 或開發人員文檔頁面 [模板 — 可編輯](/help/sites-developing/page-templates-editable.md) 的子菜單。

您可能還希望調查 [核心元件](/help/sites-developing/we-retail-core-components.md)。 請參閱創作文檔 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 查看核心元件和開發人員文檔的功能 [開發核心元件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 的子菜單。
