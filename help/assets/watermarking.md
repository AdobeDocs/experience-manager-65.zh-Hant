---
title: 將浮水印新增至您的數位資產。
description: 瞭解如何使用浮水印功能將數位水印新增至資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 浮水印您的數位資產 {#watermarking}

[!DNL Adobe Experience Manager Assets] 可讓您在資產中加入數位浮水印，協助使用者驗證資產的真實性和版權所有權。 [!DNL Experience Manager Assets] 支援在PNG和JPEG檔案上用作浮水印的文字。

若要能夠套用資產上的浮水印，請在 [!UICONTROL DAM更新資產工作流程中新增浮水印步驟] 。

1. 存取使 [!DNL Experience Manager] 用者介面，並前往「工 **[!UICONTROL 具]** >工 **[!UICONTROL 作流程]** > **[!UICONTROL 模型]**」。
1. 在「工作 **[!UICONTROL 流模型]** 」頁面中，選擇「 **[!UICONTROL DAM更新資產」工作流]** ，然後按一下「 **[!UICONTROL 編輯」]**。

1. 從側面板，將「新增浮水印 **[!UICONTROL 」步驟拖曳至]** DAM更新資產工作流程  。

   ![拖曳「 [!UICONTROL 新增浮水印] 」步驟並新增至 [!UICONTROL DAM更新資產工作流程]](assets/add_watermark_step_aem_assets.png)2
   *圖：拖曳「[!UICONTROL 新增浮水印]」步驟並新增至[!UICONTROL DAM更新資產工作流程]。*

   >[!NOTE]
   >
   >將「新增 [!UICONTROL 浮水印] 」步驟放在「處理縮 [!UICONTROL 圖」步驟之前] 。

1. 開啟「 **[!UICONTROL 新增浮水印]** 」步驟以顯示其屬性。
1. 在「參 **[!UICONTROL 數]** 」標籤中，在各種欄位中指定有效值，包括文字、字型類型、大小、顏色、位置、方向等。 要確認更改，請按一下「 **[!UICONTROL 完成]**」。

   ![在「資產」的「新增浮水印」步驟中提供引數](assets/arguments_add_watermark_aem_assets.png)

   *圖：在中的添加水印步驟中提供參數[!DNL Assets]。*

1. Save the **[!UICONTROL DAM Update Asset]** workflow with the watermark step.
1. 從使用者 [!DNL Assets] 介面上傳範例資產。 浮水印會在您在上述步驟中設定的位置顯示字型大小、顏色等。
