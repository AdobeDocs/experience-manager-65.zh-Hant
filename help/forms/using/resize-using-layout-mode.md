---
title: 使用佈局模式調整自適應表單的元件大小
description: 使用「佈局」模式下可用的響應網格定義元件的位置
feature: Adaptive Forms
exl-id: 5cf76cb1-c92c-4aed-9945-37494fef2d29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---

# 使用版面模式調整元件大小 {#use-layout-mode-to-resize-components}

通過自適應表單創作介面，您可以使用「佈局」模式調整元件大小。 在列內拖放藍點以定義起始點和終點以定位元件。 在響應柵格中敲擊元件後，藍點顯示。 響應網格由12個等列組成。 交替列中的白色和藍色底紋將一列與另一列區分開。

您可以使用佈局模式調整所有設備類型（如案頭、平板電腦、電話和其他較小設備）的元件大小。 平板電腦自動從案頭版本導出佈局配置，而較小的設備從電話導出佈局配置。 但是，您可以覆蓋自動派生的配置以為每個設備類型定義不同的配置。

## 訪問佈局模式 {#access-layout-mode}

選擇 **佈局** 從位於自適應表單創作介面頂部的下拉清單中 **預覽** 的雙曲餘切值。 窗體將以「佈局」模式顯示。

1. 登錄到作AEM者實例並導航到 **Adobe Experience Manager** > **Forms** > **Forms和文檔**。
1. 新建或開啟現有 [自適應形式](../../forms/using/creating-adaptive-form.md)。
1. 選擇 **佈局** 下拉清單中的 **預覽** 的雙曲餘切值。 窗體將以「佈局」模式顯示。

   ![佈局模式](assets/layout_mode_ic_new.png)

## 調整元件大小 {#resize-components}

1. 在「佈局」模式下，按一下元件以調整大小。 藍點顯示在響應柵格的開始和結束處。
1. 拖放藍點以定義元件在響應網格中的位置。

   ![使用佈局模式調整大小](assets/layout_mode_resize_new_updated1.png)

   攻絲元件後顯示的工具欄由以下選項組成：

   * **[!UICONTROL 父級]**:選擇元件的父項。
   * **[!UICONTROL 還原斷點佈局]**:撤消所有調整大小的更改，並將預設佈局應用於元件。
   * **[!UICONTROL 浮動到新行]**:如果同一行中有多個元件，則將元件移至下一行。

   您還可以使用 **[!UICONTROL 還原斷點佈局]** ( ![還原斷點](assets/reverttopreviouslypublishedversion.png))選項，撤消所有調整大小的更改。

   >[!NOTE]
   >
   >不能使用「佈局」模式調整表列、工具欄、工具欄按鈕和目標區域元件的大小。 使用「樣式」模式調整這些元件的大小。

### 範例 {#example}

**目標：** 要插入表元件和影像元件，並以自適應形式將它們平行放置。

1. 在自適應窗體中使用「編輯」模式插入表和影像元件。 影像元件顯示在表元件之後。
1. 切換到佈局模式，然後按一下「表」元件。 要調整元件大小的藍點顯示在第1和第12列。
1. 將第12列的藍點拖放到響應網格的第6列。

   ![定義表的端點](assets/layout_mode_end_point_table_new.png)

1. 同樣，選擇影像元件，並將響應網格的第1列到第7列處的藍點拖放。 表和影像元件彼此平行顯示。

   ![表和影像在佈局模式下並行](assets/table_image_parallel_new.png)

   可以選擇「影像」元件並點擊 **浮動到新行** 的子菜單。

## 調整面板大小 {#resize-panels-layout-mode}

如果要調整整個面板的大小而不是單個元件的大小，請執行以下步驟：

1. 按一下面板中要調整大小的任何元件，選擇 ![選擇父項](assets/select_parent_icon.svg)，並在下拉清單中選擇第一個選項（如果面板是元件的直接父項）。

   藍點顯示在響應柵格的開始和結束處。

1. 拖放藍點以定義面板在響應網格中的位置。
可重複步驟1和2並選擇 ![選擇父項](assets/float_to_new_line_icon.svg) 按鈕，將選定控制項在Tab鍵次序中下移一個位置。

## 定義面板的多列佈局

執行以下步驟來定義面板的列數：

1. 在 **[!UICONTROL 編輯]** 模式，點擊面板，選擇 ![配置](assets/configure_icon.png)，然後選擇 **[!UICONTROL 響應 — 頁面上的所有內容，無需導航]** 的 **[!UICONTROL 面板佈局]** 的子菜單。

1. 點擊 ![保存](assets/save_icon.svg) 的子菜單。

1. 在 **[!UICONTROL 佈局]** 模式，點擊面板中的任何元件，選擇 ![選擇父項](assets/select_parent_icon.svg)，然後選擇面板。

1. 點擊 ![多列](assets/multi-column.svg) 並從下拉清單中選擇列數。 列數可以從1到12。 該面板被分成多列佈局。

![佈局模式下的多列](assets/multi-column-layout.png)

## 為舊響應佈局啟用新響應網格 {#enableresponsivegrid}

為您使用AEM Forms6.4或更低版本建立的表單啟用新的響應網格，以調整元件大小。

>[!NOTE]
>
>切換到新的響應網格會丟棄已為表單中使用的元件定義的佈局屬性。

執行以下步驟以啟用新的響應網格：

1. 選擇 **佈局** 下拉清單中的 **預覽** 的雙曲餘切值。 將顯示啟用佈局模式的確認。
1. 點擊 **是** 啟用 **佈局** 的子菜單。

### 在具有新響應佈局的自適應表單中嵌入舊片段 {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

自適應表單的新響應佈局允許您添加具有對表單的舊響應佈局的自適應表單片段。 但是，新佈局會放棄已為片段中使用的元件定義的佈局屬性。 可以切換到「佈局」模式，以定義片段中使用的元件的佈局屬性。

### 以舊自適應形式嵌入具有新響應佈局的片段 {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

如果將具有新響應佈局的片段嵌入到具有舊響應佈局的自適應表單中，則系統會提示您為表單啟用「佈局」模式並重新嵌入片段。

要啟用佈局模式，請選擇 **佈局** 下拉清單中的 **預覽** 選項和點擊 **是** 確認。 選擇 **編輯** 的子菜單。

## 禁用具有舊響應佈局的表單的佈局模式 {#disable-layout-mode-for-forms-with-old-responsive-layout}

通過編輯表單中使用的模板的屬性，可以禁用具有舊響應佈局的表單的佈局模式。

執行以下步驟以禁用佈局模式：

1. 選擇 **[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL 模板]** 開啟窗體中使用的模板 **[!UICONTROL 編輯]** 的子菜單。
1. 在左窗格中選擇「文檔容器」，然後點擊 **[!UICONTROL 策略。]**

   ![禁用佈局模式](assets/policy_disable_layout_mode.png)

1. 點擊 **[!UICONTROL 佈局設定]** 頁籤 **[!UICONTROL 禁用佈局模式]**。
1. 點擊 ![保存更改](assets/save_icon.png) 的子菜單。
