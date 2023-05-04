---
title: 為您的數位資產加上浮水印
description: 了解如何使用浮水印功能為資產加上數位浮水印。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 2%

---

# 為您的數位資產加上浮水印 {#watermarking}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 可讓您為資產加上數位浮水印，協助使用者驗證資產的真實性和版權所有權。 [!DNL Experience Manager Assets] 支援在PNG和JPEG檔案上用作浮水印的文本。

若要對資產套用浮水印，請在 [!UICONTROL DAM更新資產] 工作流程。

1. 存取 [!DNL Experience Manager] 使用者介面，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 從 **[!UICONTROL 工作流程模型]** 頁面，選擇 **[!UICONTROL DAM更新資產]** 工作流程，按一下 **[!UICONTROL 編輯]**.

1. 從側面板拖動 **[!UICONTROL 添加浮水印]** 步驟至 [!UICONTROL DAM更新資產] 工作流程。

   ![拖曳 [!UICONTROL 添加浮水印] 步驟並新增至 [!UICONTROL DAM更新資產] 工作流程](assets/add_watermark_step_aem_assets.png)

   *圖：拖曳 [!UICONTROL 添加浮水印] 步驟並新增至 [!UICONTROL DAM更新資產] 工作流程。*

   >[!NOTE]
   >
   >放置 [!UICONTROL 添加浮水印] 在 [!UICONTROL 處理縮圖] 步驟。

1. 開啟 **[!UICONTROL 添加浮水印]** 顯示其屬性的步驟。
1. 在 **[!UICONTROL 引數]** 頁簽，在各種欄位中指定有效值，包括文本、字型類型、大小、顏色、位置、方向等。 若要確認變更，請按一下 **[!UICONTROL 完成]**.

   ![在中的新增浮水印步驟中提供引數 [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *圖：在中的新增浮水印步驟中提供引數 [!DNL Assets].*

1. 儲存 **[!UICONTROL DAM更新資產]** 使用浮水印步驟的工作流程。
1. 從 [!DNL Assets] 使用者介面上傳範例資產。 浮水印會隨字型大小、顏色等一起出現在您在上述步驟中設定的位置。

要以寫程式方式或使用動態資訊為PDF文檔加水印，請考慮使用 [Experience Manager檔案服務](/help/forms/using/overview-aem-document-services.md) 提供。

## 提示和限制 {#tips-limitations}

* 僅支援基於文本的水印。 影像不會作為水印使用，即使您在建立 [!UICONTROL 添加水印過程].
* 僅支援對PNG和JPEG檔案加上水印。 其他資產格式不會加上浮水印。
