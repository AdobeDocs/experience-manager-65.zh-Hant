---
title: 為您的數位資產新增浮水印
description: 瞭解如何使用浮水印功能為資產新增數位浮水印。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---

# 為您的數位資產加上浮水印 {#watermarking}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

[!DNL Adobe Experience Manager Assets]可讓您為資產新增數位浮水印，協助使用者驗證資產的真實性和版權所有權。 [!DNL Experience Manager Assets]支援在PNG和JPEG檔案中做為浮水印使用的文字。

若要在資產上套用浮水印，請在[!UICONTROL DAM更新資產]工作流程中新增浮水印步驟。

1. 存取[!DNL Experience Manager]使用者介面，並移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**。
1. 從&#x200B;**[!UICONTROL 工作流程模型]**&#x200B;頁面，選取&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程，然後按一下&#x200B;**[!UICONTROL 編輯]**。

1. 從側面板，將&#x200B;**[!UICONTROL 新增浮水印]**&#x200B;步驟拖曳至[!UICONTROL DAM更新資產]工作流程。

   ![拖曳[!UICONTROL 新增浮水印]步驟並新增至[!UICONTROL DAM更新資產]工作流程](assets/add_watermark_step_aem_assets.png)

   *圖：拖曳[!UICONTROL 新增浮水印]步驟並新增至[!UICONTROL DAM更新資產]工作流程。*

   >[!NOTE]
   >
   >將[!UICONTROL 新增浮水印]步驟置於[!UICONTROL 處理縮圖]步驟之前的任何位置。

1. 開啟&#x200B;**[!UICONTROL 新增浮水印]**&#x200B;步驟以顯示其屬性。
1. 在&#x200B;**[!UICONTROL 引數]**&#x200B;索引標籤中，指定各種欄位中的有效值，包括文字、字型型別、大小、顏色、位置、方向等。 若要確認變更，請按一下&#x200B;**[!UICONTROL 完成]**。

   ![在[!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)的加入浮水印步驟中提供引數

   *圖：在[!DNL Assets].*&#x200B;的加入浮水印步驟中提供引數

1. 使用浮水印步驟儲存&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程。
1. 從[!DNL Assets]使用者介面上傳範例資產。 浮水印會以字型大小、顏色等顯示在您在上述步驟中設定的位置。

若要以程式設計方式或動態資訊為PDF檔案加上浮水印，請考慮使用[Experience Manager檔案服務](/help/forms/using/overview-aem-document-services.md)產品。

## 提示和限制 {#tips-limitations}

* 僅支援文字浮水印。 即使您在建立[!UICONTROL 新增浮水印程式]時可以上傳影像，影像也不會用作浮水印。
* 僅支援PNG和JPEG檔案加注水印。 其他資產格式不會加上浮水印。
