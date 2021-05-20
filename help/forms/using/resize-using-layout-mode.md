---
title: 使用「版面」模式調整最適化表單的元件大小
description: '使用「配置」模式中可用的回應式格線來定義元件的位置 '
feature: 適用性表單
exl-id: 5cf76cb1-c92c-4aed-9945-37494fef2d29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---

# 使用「佈局」模式調整元件大小{#use-layout-mode-to-resize-components}

最適化表單製作介面可讓您使用「版面」模式來調整元件大小。 在欄中拖放藍點，以定義要定位元件的起點和終點。 點選回應式格線內的元件後，藍點隨即顯示。 回應式格線包含12個相等欄。 替換列中的白色和藍色底紋區分了一列和另一列。

您可以使用「版面」模式來調整所有裝置類型（例如桌上型電腦、平板電腦、手機和其他較小裝置）的元件大小。 平板電腦會自動從案頭版本衍生配置，而較小的裝置則從手機衍生配置。 不過，您可以覆寫自動衍生的設定，以定義每種裝置類型的不同設定。

## 訪問佈局模式{#access-layout-mode}

從顯示在&#x200B;**預覽**&#x200B;選項旁的最適化表單製作介面頂端的下拉式清單中，選取&#x200B;**版面**。 表單會以「配置」模式顯示。

1. 登入AEM製作例項，並導覽至&#x200B;**Adobe Experience Manager** > **Forms** > **Forms與檔案**。
1. 建立新表單或開啟現有的[適用性表單](../../forms/using/creating-adaptive-form.md)。
1. 從顯示在&#x200B;**預覽**&#x200B;選項旁邊的頂部的下拉清單中選擇&#x200B;**佈局**。 表單會以「配置」模式顯示。

   ![版面模式](assets/layout_mode_ic_new.png)

## 調整元件大小{#resize-components}

1. 在「版面」模式中，點選元件以調整大小。 藍點顯示在回應式格線的開始和結束處。
1. 拖放藍點，以定義元件在回應式格線中的位置。

   ![使用版面模式調整大小](assets/layout_mode_resize_new_updated1.png)

   點選元件後顯示的工具列包含下列選項：

   * **[!UICONTROL 父項]**:選取元件的父項。
   * **[!UICONTROL 恢復斷點佈局]**:撤消所有調整大小的更改，並將預設佈局應用到元件。
   * **[!UICONTROL 浮點到新行]**:如果同一行中有多個元件，請將元件移至下一行。

   您也可以使用面板級別的&#x200B;**[!UICONTROL 還原斷點佈局]**（![還原斷點](assets/reverttopreviouslypublishedversion.png)）選項來還原所有調整大小的更改。

   >[!NOTE]
   >
   >無法使用「佈局」模式調整表列、工具欄、工具欄按鈕和目標區域元件的大小。 使用樣式模式調整這些元件的大小。

### 範例 {#example}

**目標：** 您想要插入表格元件和影像元件，並以最適化表單彼此平行放置。

1. 在最適化表單中使用「編輯」模式插入表格和影像元件。 影像元件會顯示在表格元件之後。
1. 切換至「版面」模式，然後點選「表格」元件。 在第1欄和第12欄顯示的藍點可調整元件大小。
1. 將第12欄的藍點拖放至回應式格線的第6欄。

   ![定義表的端點](assets/layout_mode_end_point_table_new.png)

1. 同樣地，選取影像元件，並拖放回應式格線中第1欄至第7欄的藍點。 表格和影像元件彼此平行顯示。

   ![在「佈局」模式下並行處理表和影像](assets/table_image_parallel_new.png)

   您可以選取「影像」元件，然後點選工具列中可用的&#x200B;**「浮點到新行**」選項，將「影像」元件移至下一行。

## 調整面板大小{#resize-panels-layout-mode}

如果要調整整個面板的大小，而不是個別元件，請執行下列步驟：

1. 點選面板中要調整大小的任何元件，選取「![選取父項](assets/select_parent_icon.svg)」，然後在下拉式清單中選取第一個選項（如果面板是元件的直接父項）。

   藍點顯示在回應式格線的開始和結束處。

1. 拖放藍點，以定義回應式格線中面板的位置。
您可以重複步驟1和2，然後選擇![選擇父級](assets/float_to_new_line_icon.svg)以將調整大小的面板移至下一行。

## 定義面板的多欄配置

執行下列步驟以定義面板的欄數：

1. 在&#x200B;**[!UICONTROL 編輯]**&#x200B;模式中，點選面板，選取![設定](assets/configure_icon.png)，然後從&#x200B;**[!UICONTROL 面板配置]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 回應式 — 頁面上的所有項目，而不導覽]**&#x200B;選項。

1. 點選![儲存](assets/save_icon.svg)以儲存屬性。

1. 在&#x200B;**[!UICONTROL Layout]**&#x200B;模式中，點選面板中的任何元件，選擇![Select Parent](assets/select_parent_icon.svg)，然後選擇面板。

1. 點選![多欄](assets/multi-column.svg)並從下拉式清單中選取欄數。 欄數的範圍可從1到12。 面板會分為多欄版面。

![佈局模式下的多列](assets/multi-column-layout.png)

## 為舊的回應式配置啟用新的回應式格線 {#enableresponsivegrid}

為您使用AEM Forms 6.4或更低版本建立的表單啟用新的回應式格線，以調整元件大小。

>[!NOTE]
>
>切換至新的回應格線會捨棄已針對表單中使用之元件定義的版面屬性。

執行下列步驟以啟用新的回應式格線：

1. 從顯示在&#x200B;**預覽**&#x200B;選項旁邊的頂部的下拉清單中選擇&#x200B;**佈局**。 隨即顯示啟用「配置」模式的確認。
1. 點選&#x200B;**Yes**&#x200B;以啟用表單的&#x200B;**Layout**&#x200B;模式。

### 將舊片段內嵌在具有新回應式版面{#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}的適用性表單中

最適化表單的全新回應式版面可讓您使用舊的回應式版面，新增最適化表單片段至表單。 但是，新佈局會捨棄已為片段中使用的元件定義的佈局屬性。 您可以切換到「佈局」模式，以定義片段中所用元件的佈局屬性。

### 在舊的最適化表單{#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}中內嵌具有新回應式版面的片段

如果您將片段與新回應式版面內嵌於具有舊回應式版面的適用性表單中，系統會提示您為表單啟用「版面」模式，並重新內嵌片段。

若要啟用「配置」模式，請從出現在&#x200B;**預覽**&#x200B;選項旁頂端的下拉式清單中選取&#x200B;**配置**，然後點選&#x200B;**是**&#x200B;以確認。 選取&#x200B;**Edit**&#x200B;模式以重新內嵌片段。

## 停用具有舊回應式版面{#disable-layout-mode-for-forms-with-old-responsive-layout}的表單的「版面」模式

您可以編輯表單中使用範本的屬性，以停用具有舊回應式版面的表單的「版面」模式。

執行下列步驟以停用「配置」模式：

1. 選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 範本]**&#x200B;並以&#x200B;**[!UICONTROL 編輯]**&#x200B;模式開啟表單中使用的範本。
1. 在左窗格中選擇「Document Container（文檔容器）」，然後點選「**[!UICONTROL Policy（策略）」。]**

   ![停用配置模式](assets/policy_disable_layout_mode.png)

1. 點選「**[!UICONTROL Layout Settings]**」標籤，然後選取「**[!UICONTROL Disable Layout Mode]**」。
1. 點選![儲存變更](assets/save_icon.png)以儲存範本屬性。
