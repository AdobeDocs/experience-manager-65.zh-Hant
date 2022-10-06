---
title: 在We.Retail中試用可編輯的範本
seo-title: Trying out Editable Templates in We.Retail
description: 在We.Retail中試用可編輯的範本
seo-description: null
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 10%

---

# 在We.Retail中試用可編輯的範本{#trying-out-editable-templates-in-we-retail}

使用可編輯的範本，建立和維護範本不再是開發人員專屬的工作。 一種稱為模板作者的超級用戶現在可以建立模板。 開發人員仍需要設定環境、建立用戶端程式庫和建立要使用的元件，但是當這些基本功能準備就緒後，範本作者就可以彈性地建立和設定範本，而不需要開發專案。

We.Retail中的所有頁面都以可編輯的範本為基礎，讓非開發人員能夠調整和自訂範本。

## 試試 {#trying-it-out}

1. 編輯語言主分支的「設備」頁。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. 請注意，模式選取器不再提供設計模式。 We.Retail的所有頁面都以可編輯的範本為基礎，而要更改可編輯範本的設計，必須在範本編輯器中編輯這些範本。
1. 從 **頁面資訊** 功能表選取 **編輯範本**.
1. 您現在正在編輯「主圖頁面」範本。

   頁面的結構模式允許您修改模板的結構。 例如，這包括版面容器中允許的元件。

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. 配置「佈局容器」的策略以定義容器中允許的元件。

   策略等同於設計配置。

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. 在版面容器的設計對話方塊中，您可以

   * 選擇現有策略或為容器建立新策略
   * 選取容器中允許的元件
   * 定義拖曳資產至容器時要放置的預設元件

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. 返回範本編輯器時，您可以在版面容器內編輯文字元件的原則。

   這可讓您：

   * 選擇現有策略或為容器建立新策略
   * 定義使用此元件時頁面作者可用的功能，例如

      * 允許的貼上來源
      * 格式選項
      * 允許的段落樣式
      * 允許的特殊字元

   許多以核心元件為基礎的元件都可透過可編輯的範本，在元件層級設定選項，讓開發人員不再需要自訂。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 回到範本編輯器中，您可以使用模式選取器來變更為 **初始內容** 模式來定義頁面上需要的內容。

   **版面** 模式可在正常頁面上使用，以定義範本的配置。

## 更多資訊 {#more-information}

有關詳細資訊，請參閱創作文檔 [建立頁面範本](/help/sites-authoring/templates.md) 或開發人員文檔頁面 [範本 — 可編輯](/help/sites-developing/page-templates-editable.md) 以取得可編輯範本的完整技術詳細資訊。

您也可能希望調查 [核心元件](/help/sites-developing/we-retail-core-components.md). 請參閱編寫檔案 [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 以概略了解核心元件的功能，以及開發人員檔案 [開發核心元件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 以取得技術概觀。
