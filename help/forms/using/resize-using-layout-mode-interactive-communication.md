---
title: 使用版面模式調整互動式通訊的元件大小
description: 使用版面配置模式中可用的回應式格線來定義元件位置
feature: Interactive Communication
exl-id: 9534fcb2-4260-4dd0-9f7e-779b10fd3a22
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# 使用版面模式調整元件大小 {#use-layout-mode-to-resize-components}

互動式通訊Web Channel編寫介面可讓您使用「版面」模式調整元件大小。 在欄中拖放藍點以定義起始點和終止點來定位元件。 點選回應式格線中的元件後，系統會顯示藍點。 回應式格線由12個相等的欄組成。 替代欄中的白色和藍色陰影可區分一欄與另一欄。

您可以使用「配置」模式來調整所有裝置型別（例如桌上型電腦、平板電腦、手機和其他小型裝置）的元件大小。 平板電腦會自動從桌上型電腦版本衍生配置組態，而較小的裝置則會從手機衍生配置組態。 不過，您可以覆寫自動衍生的配置，以針對每種裝置型別定義不同的配置。

>[!NOTE]
>
>如果您使用建立Web channel [將頻道列印為主版](../../forms/using/create-interactive-communication.md) 對於互動式通訊，可用於調整大小的元件也包括在Web channel中使用Print channel自動產生的子表單和欄位。 Web Channel會保留「版面」模式中「列印」管道元素的版面。

## 存取配置模式 {#access-layout-mode}

選取 **版面** 下拉式清單中的「互動式通訊」編寫介面頂端的 **預覽** 選項。 表單會以「版面」模式顯示。

1. 登入AEM作者執行個體並導覽至 **Adobe Experience Manager** > **Forms** > **Forms與檔案**.
1. 建立 [互動式通訊](../../forms/using/create-interactive-communication.md) 或開啟現有的一個。
1. 選取 **版面** 下拉式清單(顯示於頁面上方的 **預覽** 選項。 表單會以「版面」模式顯示。

   ![互動式通訊的佈局模式](assets/layout_mode_ic_new.png)

## 調整元件大小 {#resize-components}

1. 在「版面」模式中，選取要調整大小的元件。 藍點會顯示在回應式格線的開始和結尾。
1. 拖放藍點以定義元件在回應式格線中的位置。

   ![使用版面模式調整大小](assets/layout_mode_resize_new_updated.png)

   點選元件後顯示的工具列包含下列選項：

   * **父系：** 選取元件的父項。
   * **浮動至新行：** 如果同一行中有多個元件，請將元件移至下一行。

   您可以復原所有調整大小變更，並使用將預設版面套用至包含已調整大小元件的面板 **[!UICONTROL 還原中斷點配置]** ( ![還原中斷點](assets/reverttopreviouslypublishedversion.png))選項。 選取已調整大小元件的父元件以檢視選項。

   >[!NOTE]
   >
   >您無法使用「版面」模式調整表格欄、工具列、工具列按鈕和目標區域元件的大小。 使用「樣式」模式調整這些元件的大小。

### 範例 {#example}

**目標：** 您想要插入表格元件和影像元件，並在互動式通訊中將它們彼此平行放置。

1. 在互動式通訊的Web channel中使用「編輯」模式插入表格和影像元件。 影像元件會顯示在表格元件之後。
1. 切換到佈局模式並選取表格元件。 要調整元件大小的藍點會顯示在欄1和12。
1. 將第12欄的藍色圓點拖放至回應式格線的第6欄。

   ![定義表格的端點](assets/layout_mode_end_point_table_new.png)

1. 同樣地，選取影像元件，並將回應式格線第1欄的藍色圓點拖放至第7欄。 表格和影像元件彼此平行顯示。

   ![在「版面」模式中同時顯示表格和影像](assets/table_image_parallel_new.png)

   您可以選取「影像」元件，然後選取 **浮動至新行** 工具列中的可用選項，將影像元件移至下一行。

## 調整面板大小 {#resize-panels-layout-mode}

如果您想要調整整個面板而非個別元件的大小，請執行下列步驟：

1. 在面板中選取您要調整大小的任何元件，然後選取 ![選取父系](assets/select_parent_icon.svg)，並選取下拉式清單中的第一個選項（如果面板為元件的直接父項）。

   藍點會顯示在回應式格線的開始和結尾。

1. 拖放藍點以定義面板在回應式格線中的位置。
您可以重複步驟1和2，然後選取 ![選取父系](assets/float_to_new_line_icon.svg) 將調整大小的面板移至下一行。

## 定義面板的多欄配置

執行以下步驟來定義面板的欄數：

1. 在 **[!UICONTROL 編輯]** 模式，選取面板，選取 ![設定](assets/configure_icon.png)，並選取 **[!UICONTROL 回應式 — 頁面上的所有內容，無需導覽]** 選項來自 **[!UICONTROL 面板配置]** 下拉式清單。

1. 選取 ![儲存](assets/save_icon.svg) 以儲存屬性。

1. 在 **[!UICONTROL 版面]** 模式，選取面板中的任何元件，然後選取 ![選取父系](assets/select_parent_icon.svg)，然後選取面板。

1. 選取 ![多欄](assets/multi-column.svg) 並從下拉式清單中選取欄數。 欄數可以介於1到12之間。 面板會分成多欄配置。

![佈局模式下的多欄](assets/multi-column-layout.png)

## 停用具有舊回應式佈局的表單的佈局模式 {#disable-layout-mode-for-forms-with-old-responsive-layout}

您可以編輯表單中所用範本的屬性，以停用具有舊回應式版面的表單版面模式。

執行以下步驟以停用「配置」模式：

1. 選取 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 範本]** 然後開啟表單中使用的範本，位置在 **[!UICONTROL 編輯]** 模式。
1. 在左窗格中選取檔案容器，然後選取 **[!UICONTROL 原則。]**

   ![停用佈局模式](assets/policy_disable_layout_mode.png)

1. 選取 **[!UICONTROL 版面設定]** 標籤並選取 **[!UICONTROL 停用佈局模式]**.
1. 選取 ![儲存變更](assets/save_icon.png) 以儲存範本屬性。
