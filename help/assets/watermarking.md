---
title: 將水印添加到數字資產
description: 瞭解如何使用水印功能向資產中添加數字水印。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 3%

---

# 為數字資產加水印 {#watermarking}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/watermarking.html?lang=en) |

[!DNL Adobe Experience Manager Assets] 允許您向資產中添加數字水印，以幫助用戶驗證資產的真實性和版權所有權。 [!DNL Experience Manager Assets] 支援文本，以用作PNG和JPEG檔案上的水印。

要能夠對資產應用水印，請在 [!UICONTROL DAM更新資產] 工作流。

1. 訪問 [!DNL Experience Manager] 用戶介面，然後轉到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 從 **[!UICONTROL 工作流模型]** ，選擇 **[!UICONTROL DAM更新資產]** 工作流，按一下 **[!UICONTROL 編輯]**。

1. 從側面板中，拖動 **[!UICONTROL 添加水印]** 的 [!UICONTROL DAM更新資產] 工作流。

   ![拖動 [!UICONTROL 添加水印] 步驟並添加到 [!UICONTROL DAM更新資產] 工作流](assets/add_watermark_step_aem_assets.png)

   *圖：拖動 [!UICONTROL 添加水印] 步驟並添加到 [!UICONTROL DAM更新資產] 工作流。*

   >[!NOTE]
   >
   >放置 [!UICONTROL 添加水印] 在前面的任何位置 [!UICONTROL 進程縮略圖] 的子菜單。

1. 開啟 **[!UICONTROL 添加水印]** 顯示其屬性的步驟。
1. 在 **[!UICONTROL 參數]** 頁籤，在各個欄位中指定有效值，包括文本、字型類型、大小、顏色、位置、方向等。 要確認更改，請按一下 **[!UICONTROL 完成]**。

   ![在中添加水印步驟中提供參數 [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *圖：在中添加水印步驟中提供參數 [!DNL Assets]。*

1. 保存 **[!UICONTROL DAM更新資產]** 帶水印步驟的工作流。
1. 從 [!DNL Assets] 用戶介面，上載示例資產。 在您在上述步驟中配置的位置顯示水印，其字型大小、顏色等。

要以寫程式方式或使用動態資訊對PDF文檔進行水印，請考慮使用 [Experience Manager文檔服務](/help/forms/using/overview-aem-document-services.md) 提供。

## 提示和限制 {#tips-limitations}

* 僅支援基於文本的水印。 影像不用作水印，即使在建立 [!UICONTROL 添加水印進程]。
* 只支援對PNG和JPEG檔案加水印。 其他資產格式不加水印。
