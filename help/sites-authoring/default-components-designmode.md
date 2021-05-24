---
title: 在設計模式中配置元件
seo-title: 在設計模式中配置元件
description: 在設計模式中配置元件
seo-description: 'null'
uuid: b9c9792d-4398-446d-8767-44d4e7ce9a2e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8ae6817a-16d3-4740-b67a-498e75adf350
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 1%

---

# 在設計模式下配置元件{#configuring-components-in-design-mode}

當AEM執行個體安裝為現成可用時，元件瀏覽器即可立即提供一系列元件。

除此之外，您也可以使用各種其他元件。 您可以使用「設計」模式來[啟用/停用此類元件](#enable-disable-components)。 啟用後，在頁面上找到該屬性時，您可以編輯屬性參數，使用「設計」模式來[配置元件設計的各個方面。](#configuring-the-design-of-a-component)

>[!NOTE]
>
>編輯這些元件時請務必小心。 設計設定通常是整個網站設計的必要部分，因此只有具有適當權限和經驗的人才能變更這些設定，通常是管理員或開發人員。 如需詳細資訊，請參閱[開發元件](/help/sites-developing/components.md)。

>[!NOTE]
>
>設計模式僅適用於靜態範本。 使用可編輯的範本建立的範本，應使用[範本編輯器](/help/sites-authoring/templates.md)編輯。

>[!NOTE]
>
>設計模式僅適用於儲存為(`/etc`)下內容的設計配置。
>
>從AEM 6.4開始，建議將設計儲存為`/apps`下的配置資料，以支援連續部署情況。 儲存在`/apps`下的設計在運行時不可編輯，且此類模板的非管理員用戶將無法使用設計模式。

這包括新增或移除頁面的段落系統中允許的元件。 段落系統(`parsys`)是包含所有其他段落元件的複合元件。 段落系統允許作者將不同類型的元件添加到頁面中，因為它包含所有其他段落元件。 每個段落類型都以元件的形式表示。

例如，產品頁面的內容可能包含包含下列內容的段落系統：

* 產品的影像（以影像或文字時段的形式）
* 產品說明（作為文欄位落）
* 具有技術資料的表（作為表段）
* 表單使用者填寫（表單開始、表單元素和表單結束段落）

>[!NOTE]
>
>如需`parsys`的詳細資訊，請參閱[開發元件](/help/sites-developing/components.md)和[使用範本和元件的准則](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) 。

>[!CAUTION]
>
>使用本文所述的設計模式編輯設計是定義靜態模板設計的建議方法
>
>例如，在CRX DE中修改設計並非最佳作法，且此類設計的應用可能會與預期行為不同。 如需詳細資訊，請參閱開發人員檔案[頁面範本 — 靜態](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied)。

## 啟用/禁用元件{#enable-disable-components}

要啟用或禁用元件：

1. 選擇&#x200B;**Design**&#x200B;模式。

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. 點選或按一下元件。 選取時，元件會有藍色邊框。

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. 按一下或點選&#x200B;**Parent**&#x200B;圖示。

   ![](do-not-localize/screen_shot_2018-03-22at103204.png)

   這將選擇包含當前元件的段落系統。

1. 段落系統的&#x200B;**配置**&#x200B;表徵圖將顯示在父級的操作欄中。

   ![](do-not-localize/screen_shot_2018-03-22at103256.png)

   選取此選項以顯示對話方塊。

1. 編輯當前頁時，使用對話框定義元件瀏覽器中可用的元件。

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   對話方塊有兩個標籤：

   * 允許的元件
   * 設定

   **允許的元件**

   在&#x200B;**允許的元件**&#x200B;標籤上，定義可用於parsys的元件。

   * 元件會依其元件群組分組，可展開和收合。
   * 可以通過檢查組名稱來選擇整個組，而通過取消檢查可以取消選擇所有組。
   * 減號至少表示已選取一個組中的項目，但並非全部。
   * 可使用搜尋來依名稱篩選元件。
   * 元件組名稱右側列出的計數表示這些組中選定元件的總數（無論篩選器為何）。

   您可以定義每頁元件的設定。 如果子頁使用相同的模板和/或頁面元件（通常對齊），則相同的配置將應用於相應的段落系統。

   >[!NOTE]
   >
   >最適化表單元件專門設計為可在適用性表單容器內運作，以運用Forms生態系統。 因此，這些元件只能在最適化表單編輯器中使用，而無法在Sites頁面編輯器中運作。

   **設定**

   在&#x200B;**設定**&#x200B;標籤上，您可以定義其他選項，例如為每個元件繪製錨點，以及定義每個容器的儲存格邊框間距。

1. 選擇&#x200B;**Done**&#x200B;以保存配置。

## 配置元件{#configuring-the-design-of-a-component}的設計

1. 選擇&#x200B;**Design**&#x200B;模式。

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. 點選或按一下具有藍色邊框的元件。 在此範例中，選取了主圖影像元件。

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. 使用&#x200B;**Configure**&#x200B;圖示開啟對話方塊。

   ![](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   在「設計」(design)對話框中，可以根據可用的設計參數配置元件。

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   對話方塊有三個索引標籤：

   * 主要
   * 功能
   * 樣式

   **屬性**

   **Properties**&#x200B;標籤可讓您設定元件的重要設計參數。 例如，對於影像元件，您可以定義允許的影像大小上限和最小大小。

   **功能**

   **Features**&#x200B;標籤可讓您啟用或停用元件的其他功能。 例如，對於影像元件，您可以定義影像的方向、可用的裁切選項，以及是否可以上傳影像。

   **樣式**

   **Styles**&#x200B;標籤允許您定義要與元件一起使用的CSS類和樣式。

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   使用&#x200B;**Add**&#x200B;按鈕將其他條目添加到多條目對話框清單中。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   使用**刪除**表徵圖從多條目對話框清單中刪除條目。

   ![](do-not-localize/screen_shot_2018-03-22at103809.png)

   使用&#x200B;**移動**&#x200B;表徵圖重新排列多條目對話框清單中的條目順序。

   ![](do-not-localize/screen_shot_2018-03-22at103816.png)

1. 按一下或點選&#x200B;**Done**&#x200B;圖示，以儲存並關閉對話方塊。
