---
title: 將浮水印新增至您的數位資產
description: 瞭解如何使用浮水印功能將數位水印新增至資產。
contentOwner: AG
role: 業務從業人員、管理員
feature: 資產管理
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# 浮水印您的數位資產{#watermarking}

[!DNL Adobe Experience Manager Assets] 可讓您在資產中加入數位浮水印，協助使用者驗證資產的真實性和版權所有權。[!DNL Experience Manager Assets] 支援在PNG和JPEG檔案上用作浮水印的文字。

若要能夠套用資產上的浮水印，請在[!UICONTROL DAM更新資產]工作流程中新增浮水印步驟。

1. 訪問[!DNL Experience Manager]用戶介面，並轉到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 從「**[!UICONTROL 工作流模型]**」頁面中，選擇「**[!UICONTROL DAM更新資產]**」工作流，然後按一下「編輯&#x200B;**[!UICONTROL 」。]**

1. 從側面板，將「添加水印」步驟拖動到「DAM更新資產」工作流程。****

   ![拖曳「 [!UICONTROL 新增] 水標步驟」並新增至 [!UICONTROL DAM更新資] 料流](assets/add_watermark_step_aem_assets.png)

   *圖：拖曳「 [!UICONTROL 新增] 水標步驟」並新增至 [!UICONTROL DAM更新] 資產流。*

   >[!NOTE]
   >
   >將[!UICONTROL Add Watermark]步驟置於[!UICONTROL Process Thumbnail]步驟之前的任意位置。

1. 開啟&#x200B;**[!UICONTROL 新增浮水印]**&#x200B;步驟以顯示其屬性。
1. 在&#x200B;**[!UICONTROL 參數]**&#x200B;標籤中，在各種欄位中指定有效值，包括文字、字型類型、大小、顏色、位置、方向等。 要確認更改，請按一下&#x200B;**[!UICONTROL Done]**。

   ![在中的新增浮水印步驟中提供引數  [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *圖：在中的添加水印步驟中提供參數 [!DNL Assets]。*

1. 使用浮水印步驟儲存&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程。
1. 從[!DNL Assets]使用者介面上傳範例資產。 浮水印會在您在上述步驟中設定的位置顯示字型大小、顏色等。

若要以程式設計方式或使用動態資訊加上PDF檔案的水印，請考慮使用[Experience Manager檔案服務](/help/forms/using/overview-aem-document-services.md)方案。

## 提示和限制{#tips-limitations}

* 僅支援文字浮水印。 雖然您可以在建立[!UICONTROL 新增浮水印處理]時上傳影像，但影像不會當做浮水印使用。
* 僅支援PNG和JPEG檔案加浮水印。 其他資產格式不會浮水印。
