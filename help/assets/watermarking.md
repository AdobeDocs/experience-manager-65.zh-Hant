---
title: 為您的數位資產加上浮水印
description: 了解如何使用浮水印功能為資產加上數位浮水印。
contentOwner: AG
role: Business Practitioner, Administrator
feature: 資產管理
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# 為您的數位資產加上浮水印 {#watermarking}

[!DNL Adobe Experience Manager Assets] 可讓您為資產加上數位浮水印，協助使用者驗證資產的真實性和版權所有權。[!DNL Experience Manager Assets] 支援在PNG和JPEG檔案上用作水印的文本。

若要對資產套用浮水印，請在[!UICONTROL DAM更新資產]工作流程中新增浮水印步驟。

1. 訪問[!DNL Experience Manager]用戶介面，然後轉至&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**。
1. 從「**[!UICONTROL 工作流模型]**」頁中，選擇「**[!UICONTROL DAM更新資產]**」工作流，然後按一下「**[!UICONTROL 編輯]**」。

1. 從側面板，將&#x200B;**[!UICONTROL 加上浮水印]**&#x200B;步驟拖曳至[!UICONTROL  DAM更新資產]工作流程。

   ![拖曳「 [!UICONTROL 新增] 水標步驟」並新增至DAM [!UICONTROL 更新] 資產流](assets/add_watermark_step_aem_assets.png)

   *圖：拖曳「 [!UICONTROL 新增] 水標步驟」並新增至DAM [!UICONTROL 更新] 資產流。*

   >[!NOTE]
   >
   >將[!UICONTROL 加水印]步驟放置在[!UICONTROL 處理縮圖]步驟之前的任意位置。

1. 開啟&#x200B;**[!UICONTROL 添加水印]**&#x200B;步驟以顯示其屬性。
1. 在&#x200B;**[!UICONTROL 參數]**&#x200B;頁簽中，在各種欄位中指定有效值，包括文本、字型類型、大小、顏色、位置、方向等。 要確認更改，請按一下&#x200B;**[!UICONTROL Done]**。

   ![在中的新增浮水印步驟中提供引數  [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *圖：在的新增浮水印步驟中提供引 [!DNL Assets]數。*

1. 使用浮水印步驟儲存&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程。
1. 從[!DNL Assets]使用者介面上傳範例資產。 浮水印會隨字型大小、顏色等一起出現在您在上述步驟中設定的位置。

若要以程式設計方式或使用動態資訊為PDF檔案加上浮水印，請考慮使用[Experience Manager檔案服務](/help/forms/using/overview-aem-document-services.md)產品。

## 提示和限制{#tips-limitations}

* 僅支援基於文本的水印。 即使在建立[!UICONTROL 添加水印過程]時可以上載影像，影像也不會用作水印。
* 僅支援對PNG和JPEG檔案加上水印。 其他資產格式不會加上浮水印。
