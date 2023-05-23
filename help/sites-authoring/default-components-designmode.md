---
title: 在設計模式下配置預設元件
description: 在設計模式下配置元件
uuid: b9c9792d-4398-446d-8767-44d4e7ce9a2e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8ae6817a-16d3-4740-b67a-498e75adf350
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 1%

---

# 在設計模式下配置預設元件{#configuring-components-in-design-mode}

當實AEM例在出廠時安裝時，元件瀏覽器中會立即提供一系列元件。

除此之外，還提供各種其它元件。 可以使用「設計」模式 [啟用/禁用此類元件](#enable-disable-components)。 啟用並位於您的頁面上後，您可以使用「設計」模式 [配置元件設計的各個方面](#configuring-the-design-of-a-component) 編輯屬性參數。

>[!NOTE]
>
>編輯這些元件時必須小心。 設計設定通常是整個網站設計的一個組成部分，因此只應由具有適當權限和經驗的人更改，通常是管理員或開發人員。 請參閱 [開發元件](/help/sites-developing/components.md) 的子菜單。

>[!NOTE]
>
>設計模式僅適用於靜態模板。 使用可編輯模板建立的模板應使用 [模板編輯器](/help/sites-authoring/templates.md)。

>[!NOTE]
>
>設計模式僅適用於儲存為以下內容的設計配置( `/etc`)。
>
>從6.AEM4開始，建議將設計儲存為以下配置資料 `/apps` 支援連續部署方案。 儲存在 `/apps` 運行時不可編輯，非管理員用戶將無法使用此類模板的設計模式。

這包括添加或刪除頁面的段落系統中允許的元件。 段落制度( `parsys`)是包含所有其它段落元件的複合元件。 段落系統允許作者將不同類型的元件添加到包含所有其他段落元件的頁面中。 每個段落類型都表示為元件。

例如，產品頁面的內容可能包含包含以下內容的段落系統：

* 產品的影像（以影像或文本時間段的形式）
* 產品說明（作為文本段落）
* 具有技術資料的表（表段）
* 表單用戶填寫（在表單開始、表單元素和表單結束段落時）

>[!NOTE]
>
>請參閱 [開發元件](/help/sites-developing/components.md) 和 [使用模板和元件的指南](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) 有關 `parsys`。

>[!CAUTION]
>
>使用本文所述的設計模式編輯設計是定義靜態模板設計的推薦方法
>
>例如，在CRX DE中修改設計不是最佳做法，這種設計的應用可能與預期行為不同。 請參閱開發人員文檔 [頁面模板 — 靜態](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied) 的子菜單。

## 啟用/禁用元件 {#enable-disable-components}

要啟用或禁用元件：

1. 選擇 **設計** 的子菜單。

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. 點擊或按一下某個元件。 選定後，元件將具有藍色邊框。

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. 按一下或點擊 **父級** 表徵圖

   ![](do-not-localize/screen_shot_2018-03-22at103204.png)

   這將選擇包含當前元件的段落系統。

1. 的 **配置** 段落系統的表徵圖將顯示在父項的操作欄中。

   ![](do-not-localize/screen_shot_2018-03-22at103256.png)

   選擇此選項可顯示對話框。

1. 編輯當前頁面時，使用該對話框定義元件瀏覽器中可用的元件。

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   該對話框有兩個頁籤：

   * 允許的元件
   * 設定

   **允許的元件**

   在 **允許的元件** 頁籤，定義可用於parsys的元件。

   * 元件按其元件組分組，這些元件組可展開和折疊。
   * 可以通過檢查組名稱來選擇整個組，並且可以通過取消檢查來取消選擇所有組。
   * 減號表示至少選擇了組中的一個項目，但不是所有項目。
   * 可通過搜索按名稱篩選元件。
   * 元件組名稱右側列出的計數表示這些組中選定元件的總數，而與篩選器無關。

   可以定義每頁元件的配置。 如果子頁使用相同的模板和/或頁面元件（通常對齊），則相同的配置將應用於相應的段落系統。

   >[!NOTE]
   >
   >自適應表單元件設計為在自適應表單容器內工作以利用Forms生態系統。 因此，這些元件必須僅在自適應表單編輯器中使用，並且它們不能在「站點」頁面編輯器中工作。

   **設定**

   在 **設定** 頁籤，您可以定義附加選項，例如為每個元件繪製錨點以及定義每個容器的單元格填充。

1. 選擇 **完成** 保存配置。

## 配置元件的設計 {#configuring-the-design-of-a-component}

1. 選擇 **設計** 的子菜單。

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. 按一下或按一下具有藍色邊框的元件。 在此示例中，選擇英雄影像元件。

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. 使用 **配置** 表徵圖開啟對話框。

   ![](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   在「設計」(design)對話框中，可以根據可用的設計參數配置元件。

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   該對話框有三個頁籤：

   * 主要
   * 功能
   * 樣式

   **屬性**

   的 **屬性** 頁籤，用於配置元件的重要設計參數。 例如，對於影像元件，可以定義允許的影像最大和最小大小。

   **功能**

   的 **功能** 頁籤允許您啟用或禁用元件的其他功能。 例如，對於影像元件，可以定義影像的方向、可用的裁剪選項以及是否可以上載影像。

   **樣式**

   的 **樣式** 頁籤，用於定義要與元件一起使用的CSS類和樣式。

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   使用 **添加** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   使用**刪除**表徵圖從多條目對話框清單中刪除條目。

   ![](do-not-localize/screen_shot_2018-03-22at103809.png)

   使用 **移動** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。

   ![](do-not-localize/screen_shot_2018-03-22at103816.png)

1. 按一下或點擊 **完成** 表徵圖以保存和關閉對話框。
