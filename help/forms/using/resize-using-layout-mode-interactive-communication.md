---
title: 使用「佈局」模式調整互動式通信的元件大小
description: 使用「配置」模式中可用的回應式格線來定義元件的位置
feature: Interactive Communication
exl-id: 9534fcb2-4260-4dd0-9f7e-779b10fd3a22
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 使用版面模式調整元件大小 {#use-layout-mode-to-resize-components}

互動式通信Web通道創作介面允許您使用「佈局」模式調整元件大小。 在欄中拖放藍點，以定義要定位元件的起點和終點。 點選回應式格線內的元件後，藍點隨即顯示。 回應式格線包含12個相等欄。 替換列中的白色和藍色底紋區分了一列和另一列。

您可以使用「版面」模式來調整所有裝置類型（例如桌上型電腦、平板電腦、手機和其他較小裝置）的元件大小。 平板電腦會自動從案頭版本衍生配置，而較小的裝置則從手機衍生配置。 不過，您可以覆寫自動衍生的設定，以定義每種裝置類型的不同設定。

>[!NOTE]
>
>若您使用 [將通道打印為主](../../forms/using/create-interactive-communication.md) 對於互動式通信，可用於調整大小的元件還包括使用打印通道在網路通道中自動生成的子表單和欄位。 Web通道將保留「佈局」模式下「打印」通道元素的佈局。

## 存取配置模式 {#access-layout-mode}

選擇 **版面** 下拉清單中，該清單顯示在「交互通信」創作介面的 **預覽** 選項。 表單會以「配置」模式顯示。

1. 登入AEM製作例項並導覽至 **Adobe Experience Manager** > **Forms** > **Forms與檔案**.
1. 建立新或開啟現有 [互動式通訊](../../forms/using/create-interactive-communication.md).
1. 選擇 **版面** 從顯示於 **預覽** 選項。 表單會以「配置」模式顯示。

   ![互動式通訊的版面模式](assets/layout_mode_ic_new.png)

## 調整元件大小 {#resize-components}

1. 在「版面」模式中，點選元件以調整大小。 藍點顯示在回應式格線的開始和結束處。
1. 拖放藍點，以定義元件在回應式格線中的位置。

   ![使用版面模式調整大小](assets/layout_mode_resize_new_updated.png)

   點選元件後顯示的工具列包含下列選項：

   * **父級：** 選取元件的父項。
   * **浮點到新行：** 如果同一行中有多個元件，請將元件移至下一行。

   您可以還原所有重新調整大小的變更，並將預設版面套用至包含已調整大小元件的面板，使用 **[!UICONTROL 恢復斷點佈局]** ( ![還原斷點](assets/reverttopreviouslypublishedversion.png))選項。 點選已調整大小元件的父元件以檢視選項。

   >[!NOTE]
   >
   >無法使用「佈局」模式調整表列、工具欄、工具欄按鈕和目標區域元件的大小。 使用樣式模式調整這些元件的大小。

### 範例 {#example}

**目標：** 要插入表元件和影像元件，並在交互通信中將它們平行放置。

1. 在交互通信的Web通道中，使用「編輯」模式插入表和影像元件。 影像元件會顯示在表格元件之後。
1. 切換至「版面」模式，然後點選「表格」元件。 在第1欄和第12欄顯示的藍點可調整元件大小。
1. 將第12欄的藍點拖放至回應式格線的第6欄。

   ![定義表的端點](assets/layout_mode_end_point_table_new.png)

1. 同樣地，選取影像元件，並拖放回應式格線中第1欄至第7欄的藍點。 表格和影像元件彼此平行顯示。

   ![在「佈局」模式下並行處理表和影像](assets/table_image_parallel_new.png)

   您可以選取「影像」元件，然後點選 **浮點到新行** 選項，將「影像」元件移至下一行。

## 調整面板大小 {#resize-panels-layout-mode}

如果要調整整個面板的大小，而不是個別元件，請執行下列步驟：

1. 點選面板中要調整大小的任何元件，選取 ![選擇父級](assets/select_parent_icon.svg)，並在下拉式清單中選取第一個選項（如果面板是元件的直接父項）。

   藍點顯示在回應式格線的開始和結束處。

1. 拖放藍點，以定義回應式格線中面板的位置。
您可以重複步驟1和2，然後選取 ![選擇父級](assets/float_to_new_line_icon.svg) 將調整後的面板移至下一行。

## 定義面板的多欄配置

執行下列步驟以定義面板的欄數：

1. 在 **[!UICONTROL 編輯]** 模式，點選面板，選取 ![設定](assets/configure_icon.png)，然後選取 **[!UICONTROL 回應式 — 頁面上的所有項目，不需導覽]** 選項 **[!UICONTROL 面板版面]** 下拉式清單。

1. 點選 ![儲存](assets/save_icon.svg) 以儲存屬性。

1. 在 **[!UICONTROL 版面]** 模式，點選面板中的任何元件，然後選取 ![選擇父級](assets/select_parent_icon.svg)，然後選取面板。

1. 點選 ![多欄](assets/multi-column.svg) 並從下拉式清單中選取欄數。 欄數的範圍可從1到12。 面板會分為多欄版面。

![佈局模式下的多列](assets/multi-column-layout.png)

## 停用具有舊回應式版面的表單的「版面」模式 {#disable-layout-mode-for-forms-with-old-responsive-layout}

您可以編輯表單中使用之範本的屬性，以停用具有舊回應式版面的表單的「版面」模式。

執行下列步驟以停用「配置」模式：

1. 選擇 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 範本]** 並開啟表單中使用的範本，位於 **[!UICONTROL 編輯]** 模式。
1. 在左窗格中選擇「文檔容器」，然後點選 **[!UICONTROL 政策。]**

   ![停用配置模式](assets/policy_disable_layout_mode.png)

1. 點選 **[!UICONTROL 版面設定]** 索引標籤和選取 **[!UICONTROL 禁用佈局模式]**.
1. 點選 ![儲存變更](assets/save_icon.png) 以儲存範本屬性。
