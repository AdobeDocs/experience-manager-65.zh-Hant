---
title: '[!DNL Adobe Camera Raw] 支援處理數位資產'
description: 了解如何在 [!DNL Adobe Experience Manager Assets]中啟用 [!DNL Adobe Camera Raw] 支援
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: 73e53f516d8e10b548f913db079c7e9812deb907
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%

---

# 使用[!DNL Adobe Camera Raw]處理影像 {#camera-raw-support}

您可以啟用[!DNL Adobe Camera Raw]支援以處理原始檔案格式（如CR2、NEF和RAF），並以JPEG格式呈現影像。 在[!DNL Adobe Experience Manager Assets]中，使用Software Distribution提供的[Camera Raw套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)支援此功能。

>[!NOTE]
>
>此功能僅支援JPEG轉譯。 Windows 64位元、Mac OS和RHEL 7.x均支援此功能。

要在[!DNL Experience Manager Assets]中啟用[!DNL Camera Raw]支援，請執行以下步驟：

1. 從[!DNL Software Distribution]下載[Camera Raw套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)。
1. 存取 `https://[aem_server]:[port]/workflow`. 開啟&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程。
1. 編輯&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟。
1. 在&#x200B;**[!UICONTROL 縮圖]**&#x200B;標籤中提供下列配置：

   * **[!UICONTROL 縮圖]**:  `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL 略過 Mime 類型]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 在&#x200B;**[!UICONTROL Web Enabled Image]**&#x200B;頁簽的&#x200B;**[!UICONTROL Skip List]**&#x200B;欄位中，指定`audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`。

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 從側面板，在&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟下方新增&#x200B;**[!UICONTROL Camera Raw/DNG處理常式]**&#x200B;步驟。
1. 在&#x200B;**[!UICONTROL Camera Raw/DNG處理常式]**&#x200B;步驟中，在&#x200B;**[!UICONTROL Arguments]**&#x200B;標籤中新增下列設定：

   * **[!UICONTROL Mime類型]**: `image/dng` 和  `image/x-raw-(.*)`
   * **[!UICONTROL 命令]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 按一下「**[!UICONTROL 儲存]**」。

>[!NOTE]
>
>請確定上述設定與&#x200B;**[!UICONTROL 使用Camera Raw和DNG處理步驟]**&#x200B;設定的範例DAM更新資產相同。

您現在可以將相機原始檔案匯入「資產」。 安裝Camera Raw包並配置所需的工作流後，側窗格清單中將顯示&#x200B;**[!UICONTROL Image Adjust]**&#x200B;選項。

![chlimage_1-131](assets/chlimage_1-337.png)

*圖：側窗格中的選項。*

![chlimage_1-132](assets/chlimage_1-338.png)

*圖：使用選項對影像進行輕量型編輯。*

將編輯內容儲存到[!DNL Camera Raw]影像後，會為該影像產生新的轉譯`AdjustedPreview.jpg`。 對於[!DNL Camera Raw]以外的其他影像類型，所有轉譯都會反映變更。

## 最佳實務、已知問題和限制 {#best-practices}

功能有下列限制：

* 此功能僅支援JPEG轉譯。 Windows 64位元、Mac OS和RHEL 7.x均支援此功能。
* RAW和DNG格式不支援中繼資料回寫。
* [!DNL Camera Raw]程式庫對一次可處理的總像素有限制。 目前，無論先遇到什麼條件，最多都可處理檔案長邊的65000像素，或512 MP。
