---
title: 元件主控台
description: 「元件」主控台可讓您瀏覽針對執行個體定義的所有元件，並檢視每個元件的關鍵資訊。
exl-id: d79107b9-dfa4-4e80-870e-0b7ea72f0bc7
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 17%

---

# 元件主控台{#components-console}

「元件」主控台可讓您瀏覽針對執行個體定義的所有元件，並檢視每個元件的關鍵資訊。

可從下列位置存取： **工具>** **一般>** **元件**. 在主控台中，卡片和清單檢視可供使用。由於沒有元件的樹結構，因此列視圖不可用。

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>「元件主控台」會顯示系統中的所有元件。 此 [元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser) 顯示可供作者使用的元件，並隱藏任何以句點( `.`)。

## 搜尋 {#searching}

使用「 **僅內容****** 」圖示 (左上角)，您可以開啟「搜尋」面板以搜尋和/或篩選元件：

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### 元件詳細資料 {#component-details}

若要檢視特定元件的詳細資訊，請按一下所需資源。 三個索引標籤提供：

* **屬性**

  ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

  在「屬性」標籤上，您可以：

   * 檢視元件的一般屬性。
   * 檢視 [圖示或縮寫已定義](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) 用於元件。

      * 按一下圖示的來源會前往該元件。

   * 檢視 **資源型別** 和 **資源超級型別** （如果已定義）。

      * 按一下「資源超級型別」即可前往該元件。

  >[!NOTE]
  >
  >因為 `/apps` 無法在執行階段編輯，元件主控台為唯讀。

* **原則**

  ![原則](assets/chlimage_1-169.png)

* **即時使用情況**

  ![即時使用情況](assets/chlimage_1-170.png)

  >[!CAUTION]
  >
  >由於為此檢視收集之資訊的性質，它可能需要一段時間才能整理/顯示。

* **文件**

  如果開發人員已提供 [元件的檔案](/help/sites-developing/developing-components.md#documenting-your-component)，它會顯示在 **檔案** 標籤。 如果沒有可用的檔案， **檔案** 索引標籤不會顯示。

  ![文件](assets/chlimage_1-171.png)
