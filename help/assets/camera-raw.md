---
title: '"[!DNL Adobe Camera Raw] 支援處理數位資產」'
description: 了解如何啟用 [!DNL Adobe Camera Raw] 支援 [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 2%

---

# 使用 [!DNL Adobe Camera Raw] {#camera-raw-support}

您可以啟用 [!DNL Adobe Camera Raw] 支援處理原始檔案格式（如CR2、NEF和RAF），並以JPEG格式呈現影像。 支援以下功能： [!DNL Adobe Experience Manager Assets] 使用 [Camera Raw套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) 可從Software Distribution取得。

>[!NOTE]
>
>功能僅支援JPEG轉譯。 Windows 64位元、Mac OS和RHEL 7.x均支援此功能。

啟用 [!DNL Camera Raw] 支援 [!DNL Experience Manager Assets]，請遵循下列步驟：

1. 下載 [[!DNL Camera Raw] 套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) 從 [!DNL Software Distribution].
1. 存取 `https://[aem_server]:[port]/workflow`. 開啟 **[!UICONTROL DAM更新資產]** 工作流程。
1. 編輯 **[!UICONTROL 處理縮圖]** 步驟。
1. 在 **[!UICONTROL 縮圖]** 標籤：

   * **[!UICONTROL 縮圖]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL 略過 Mime 類型]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 在 **[!UICONTROL 啟用Web的映像]** 標籤中 **[!UICONTROL 略過清單]** 欄位，指定 `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 從側面板，新增 **[!UICONTROL Camera Raw/DNG處理常式]** 在 **[!UICONTROL 處理縮圖]** 步驟。
1. 在 **[!UICONTROL Camera Raw/DNG處理常式]** 步驟，在 **[!UICONTROL 引數]** 標籤：

   * **[!UICONTROL Mime類型]**: `image/dng` 和 `image/x-raw-(.*)`
   * **[!UICONTROL 命令]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 按一下「**[!UICONTROL 儲存]**」。

>[!NOTE]
>
>請確定上述設定與 **[!UICONTROL 使用Camera Raw和DNG處理步驟更新資產範例]** 設定。

您現在可以將相機原始檔案匯入「資產」。 安裝Camera Raw套件並設定所需的工作流程後， **[!UICONTROL 影像調整]** 選項。

![chlimage_1-131](assets/chlimage_1-337.png)

*圖：側窗格中的選項。*

![chlimage_1-132](assets/chlimage_1-338.png)

*圖：使用選項對影像進行輕量型編輯。*

將編輯儲存至 [!DNL Camera Raw] 影像，新格式副本 `AdjustedPreview.jpg` 會為影像產生。 適用於除 [!DNL Camera Raw]，變更會反映在所有轉譯中。

## 最佳實務、已知問題和限制 {#best-practices}

功能有下列限制：

* 功能僅支援JPEG轉譯。 Windows 64位元、Mac OS和RHEL 7.x均支援此功能。
* RAW和DNG格式不支援中繼資料回寫。
* 此 [!DNL Camera Raw] 程式庫一次可處理的總像素有限。 目前，無論先遇到什麼條件，最多都可以處理65000個檔案長邊的像素，或512 MP。
