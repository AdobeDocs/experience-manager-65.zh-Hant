---
title: 元件主控台
seo-title: Components Console
description: 元件主控台
seo-description: null
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
exl-id: d79107b9-dfa4-4e80-870e-0b7ea72f0bc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 23%

---

# 元件主控台{#components-console}

元件控制台可讓您瀏覽為執行個體定義的所有元件，並檢視每個元件的金鑰資訊。

您可從「工具」->「一 **般」->「元件」** 存取它 ********。在主控台中，卡片和清單檢視可供使用。由於沒有元件的樹結構，因此列視圖不可用。

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>元件控制台顯示系統中的所有元件。 此 [元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser) 顯示可供作者使用的元件，並隱藏以句點( `.`)。

## 搜尋 {#searching}

使用「 **僅內容****** 」圖示 (左上角)，您可以開啟「搜尋」面板以搜尋和/或篩選元件：

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### 元件詳細資訊 {#component-details}

若要檢視特定元件的詳細資訊，請點選/按一下所需資源。 提供三個標籤：

* **屬性**

   ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

   在「屬性」索引標籤上，您可以：

   * 查看元件的常規屬性。
   * 檢視 [已定義表徵圖或縮寫](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) （元件）。

      * 按一下圖示的來源即會將您導向該元件。
   * 檢視 **資源類型** 和 **資源超類型** （若已定義）。

      * 按一下「資源超類型」(Resource Super Type)會將您導向該元件。
   >[!NOTE]
   >
   >因為 `/apps` 在運行時無法編輯，元件控制台是只讀的。

* **原則**

   ![chlimage_1-169](assets/chlimage_1-169.png)

* **即時使用情況**

   ![chlimage_1-170](assets/chlimage_1-170.png)

   >[!CAUTION]
   >
   >由於為此檢視收集的資訊性質的緣故，可能需要一段時間才能加以整理/顯示。

* **文件**

   如果開發人員已提供 [元件的檔案](/help/sites-developing/developing-components.md#documenting-your-component)，則會顯示在 **檔案** 標籤。 如果沒有可用的檔案，則 **檔案** 標籤。

   ![chlimage_1-171](assets/chlimage_1-171.png)
