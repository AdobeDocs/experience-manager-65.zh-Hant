---
title: 在設計模式中設定元件
seo-title: 在設計模式中設定元件
description: 在設計模式中設定元件
seo-description: 'null'
uuid: b9c9792d-4398-446d-8767-44d4e7ce9a2e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8ae6817a-16d3-4740-b67a-498e75adf350
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 1%

---


# 在設計模式下配置元件{#configuring-components-in-design-mode}

當實AEM例安裝在現成可用時，元件瀏覽器中會立即提供選取的元件。

除了這些外，還有各種其他元件可供使用。 您可以使用「設計」模式來[啟用／停用此類元件](#enable-disable-components)。 啟用並位於頁面上時，您可以使用「設計」模式來編輯屬性參數，以設定元件設計的各個方面。[](#configuring-the-design-of-a-component)

>[!NOTE]
>
>編輯這些元件時必須小心。 設計設定通常是整個網站設計的一部份，因此只有擁有適當權限和經驗的人才能變更這些設定，通常是管理員或開發人員。 如需詳細資訊，請參閱[開發元件](/help/sites-developing/components.md)。

>[!NOTE]
>
>設計模式僅適用於靜態範本。 使用可編輯的模板建立的模板應使用[模板編輯器](/help/sites-authoring/templates.md)進行編輯。

>[!NOTE]
>
>設計模式僅適用於儲存為(`/etc`)下的內容的設計配置。
>
>從AEM6.4開始，建議將設計儲存為`/apps`下的設定資料，以支援持續部署藍本。 儲存在`/apps`下的設計在執行時期無法編輯，非管理員使用者將無法使用設計模式來建立此類範本。

這包括添加或刪除頁面段落系統中允許的元件。 段落系統(`parsys`)是包含所有其他段落元件的複合元件。 段落系統可讓作者將不同類型的元件新增至包含所有其他段落元件的頁面。 每個段落類型都表示為元件。

例如，產品頁面的內容可能包含包含下列內容的段落系統：

* 產品的影像（影像或文欄位落的形式）
* 產品說明（文欄位）
* 具有技術資料的表（作為表段）
* 表單使用者填寫（表單開頭、表單元素和表單結尾段落）

>[!NOTE]
>
>如需`parsys`的詳細資訊，請參閱[開發元件](/help/sites-developing/components.md)和[使用範本和元件的准則](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components)。

>[!CAUTION]
>
>使用本文所述的設計模式編輯設計是定義靜態範本設計的建議方式
>
>例如，在CRX DE中修改設計並非最佳做法，而且這種設計的應用可能與預期行為不同。 如需詳細資訊，請參閱開發人員檔案[頁面範本- Static](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied)。

## 啟用／禁用元件{#enable-disable-components}

要啟用或禁用元件，請執行以下操作：

1. 選擇&#x200B;**Design**&#x200B;模式。

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. 點選或按一下元件。 選取此元件時，元件會有藍色邊框。

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. 按一下或點選&#x200B;**Parent**&#x200B;表徵圖。

   ![](do-not-localize/screen_shot_2018-03-22at103204.png)

   這將選擇包含當前元件的段落系統。

1. 段落系統的&#x200B;**Configure**&#x200B;圖示將顯示在父級的操作欄中。

   ![](do-not-localize/screen_shot_2018-03-22at103256.png)

   選擇此選項以顯示對話框。

1. 使用對話方塊定義在編輯目前頁面時，元件瀏覽器中可用的元件。

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   對話框有兩個頁籤：

   * 允許的元件
   * 設定

   **允許的元件**

   在&#x200B;**允許的元件**&#x200B;頁籤上，定義哪些元件可用於參數。

   * 這些元件依其元件群組分組，可展開和收合。
   * 您可以勾選整個群組，方法是勾選群組名稱，而取消勾選所有群組即可取消勾選。
   * 減號表示至少選取一個項目，但並非選取群組中的所有項目。
   * 可使用搜尋來依名稱篩選元件。
   * 列在元件群組名稱右側的計數代表這些群組中選取的元件總數，而不考慮篩選。

   您可以定義每個頁面元件的設定。 如果子頁面使用相同的範本和／或頁面元件（通常對齊），則相同的組態會套用至對應的段落系統。

   >[!NOTE]
   >
   >最適化表單元件設計為可在Adaptive Form Container中運作，以利用Forms生態系統。 因此，這些元件必須僅用於最適化表單編輯器中，而不能在「網站」頁面編輯器中運作。

   **設定**

   在&#x200B;**Settings**&#x200B;標籤上，您可以定義其他選項，例如為每個元件繪製錨點，以及定義每個容器的儲存格間距。

1. 選擇&#x200B;**Done**&#x200B;以保存配置。

## 配置元件{#configuring-the-design-of-a-component}的設計

1. 選擇&#x200B;**Design**&#x200B;模式。

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. 點選或按一下具有藍色邊框的元件。 在此示例中，選擇了英雄影像元件。

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. 使用&#x200B;**Configure**&#x200B;表徵圖開啟對話框。

   ![](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   在設計對話框中，可根據可用的設計參數配置元件。

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   對話方塊有三個標籤：

   * 主要
   * 功能
   * 樣式

   **屬性**

   使用&#x200B;**Properties**&#x200B;頁籤可以配置元件的重要設計參數。 例如，對於影像元件，您可以定義允許的影像最大和最小大小。

   **功能**

   **功能**&#x200B;標籤可讓您啟用或停用元件的其他功能。 例如，對於影像元件，您可以定義影像的方向、可用的裁切選項，以及是否可以上傳影像。

   **樣式**

   **Styles**&#x200B;標籤允許您定義要與元件一起使用的CSS類和樣式。

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   使用&#x200B;**Add**&#x200B;按鈕，將其他條目添加到多條目對話框清單。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   使用**刪除**表徵圖從多條目對話框清單中刪除條目。

   ![](do-not-localize/screen_shot_2018-03-22at103809.png)

   使用&#x200B;**移動**&#x200B;表徵圖重新排列多條目對話框清單中條目的順序。

   ![](do-not-localize/screen_shot_2018-03-22at103816.png)

1. 按一下或點選&#x200B;**Done**&#x200B;表徵圖以保存並關閉對話框。

