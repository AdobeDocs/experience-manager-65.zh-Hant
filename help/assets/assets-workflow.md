---
title: 將工作流程套用至資產
description: 瞭解如何將工作流程套用至AEM Assets中的資產、檔案夾和系列。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 將工作流程套用至處理資產 {#applying-workflows-to-assets}

將工作流程套用至數位資產與網站頁面相同。 如需如何在AEM中建立和使用工作流程的完整指南，請參閱「開 [始工作流程](/help/sites-authoring/workflows-participating.md)」。

在數位資產中使用工作流程來啟用資產或建立浮水印。 資產的許多工作流程都會自動開啟。 例如，編輯影像後自動建立轉譯的工作流程會自動開啟。

如果傳統UI中的工作流程在啟用觸控的UI中不可用，例如「要求啟用」和「要求停用」，請參閱 [建立工作流程模型](/help/sites-developing/workflows-models.md#classic2touchui)。

## 套用工作流程至AEM資產 {#applying-a-workflow-to-an-aem-asset}

如需將工作流程套用至AEM資產的詳細資訊，請參 [閱「啟動資產的工作流程」](/help/assets/managing-assets-touch-ui.md#starting-a-workflow-on-an-asset)。

## 將工作流程套用至多個資產 {#applying-a-workflow-to-multiple-assets}

1. 從「資產」主控台，導覽至您要啟動工作流程的資產所在的位置，然後選取資產。
1. 按一下／點選Experience Manager標誌，然後從選單選擇「時 **[!UICONTROL 間軸]** 」以顯示時間軸。

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 按一下／點選 **[!UICONTROL 底部的]** 「動作」。

   ![chlimage_1-30](assets/chlimage_1-137.png)

1. 點選「開 **[!UICONTROL 始工作流程]**」。
1. 在「開 **[!UICONTROL 始工作流]** 」(Start Workflow)對話框中，從清單中選擇工作流模型。

   ![chlimage_1-31](assets/chlimage_1-138.png)

1. （可選）指定工作流的標題，可用來參考工作流實例。
1. 點選「 **[!UICONTROL 開始]** 」，然後點選 **[!UICONTROL 對話方塊中的「確認]** 」。 工作流程會在您選取的所有資產上執行。

## 將工作流程套用至多個檔案夾 {#applying-a-workflow-to-multiple-folders}

將工作流程套用至多個檔案夾的程式，類似於將工作流程套用至多個資產的程式。 在「資產」主控台中選取資料夾，並執行將工作流程套用至多 [個資產的程式步驟2-7](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets)。

## 將工作流程套用至系列 {#applying-a-workflow-to-a-collection}

請參 [閱套用系列的工作流程](/help/assets/managing-collections-touch-ui.md#running-a-workflow-on-a-collection)。
