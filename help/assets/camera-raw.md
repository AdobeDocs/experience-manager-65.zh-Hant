---
title: '"[!DNL Adobe Camera Raw] 支援處理數字資產」'
description: 瞭解如何啟用 [!DNL Adobe Camera Raw] 支援 [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# 使用 [!DNL Adobe Camera Raw] {#camera-raw-support}

您可以啟用 [!DNL Adobe Camera Raw] 支援處理原始檔案格式（如CR2、NEF和RAF），並以JPEG格式呈現影像。 中支援此功能 [!DNL Adobe Experience Manager Assets] 使用 [Camera Raw包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) 可從軟體分發中獲得。

>[!NOTE]
>
>該功能僅支援JPEG格式副本。 在Windows 64位、MacOS和RHEL 7.x上支援此功能。

啟用 [!DNL Camera Raw] 支援 [!DNL Experience Manager Assets]，請執行以下步驟：

1. 下載 [[!DNL Camera Raw] 包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) 從 [!DNL Software Distribution]。
1. 存取 `https://[aem_server]:[port]/workflow`. 開啟 **[!UICONTROL DAM更新資產]** 工作流。
1. 編輯 **[!UICONTROL 處理縮略圖]** 的子菜單。
1. 在 **[!UICONTROL 縮略圖]** 頁籤：

   * **[!UICONTROL 縮略圖]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL 略過 Mime 類型]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 在 **[!UICONTROL 啟用Web的影像]** 的 **[!UICONTROL 跳過清單]** 欄位，指定 `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`。

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 從側面板中，添加 **[!UICONTROL Camera Raw/DNG處理程式]** 步驟 **[!UICONTROL 處理縮略圖]** 的子菜單。
1. 在 **[!UICONTROL Camera Raw/DNG處理程式]** 步驟，在 **[!UICONTROL 參數]** 頁籤：

   * **[!UICONTROL MIME類型]**: `image/dng` 和 `image/x-raw-(.*)`
   * **[!UICONTROL 命令]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 按一下「**[!UICONTROL 儲存]**」。

>[!NOTE]
>
>確保上述配置與 **[!UICONTROL 帶Camera Raw和DNG處理步驟的DAM更新資產示例]** 配置。

現在，您可以將相機原始檔案導入「資產」。 安裝Camera Raw包並配置所需工作流後， **[!UICONTROL 影像調整]** 的子菜單。

![chlimage_1-131](assets/chlimage_1-337.png)

*圖：側面窗格中的選項。*

![chlimage_1-132](assets/chlimage_1-338.png)

*圖：使用選項對影像進行輕量編輯。*

將編輯內容保存到 [!DNL Camera Raw] 影像，新格式副本 `AdjustedPreview.jpg` 生成。 對於其他影像類型，除 [!DNL Camera Raw]，更改將反映在所有格式副本中。

## 最佳做法、已知問題和限制 {#best-practices}

該功能具有以下限制：

* 該功能僅支援JPEG格式副本。 在Windows 64位、MacOS和RHEL 7.x上支援此功能。
* RAW和DNG格式不支援元資料寫回。
* 的 [!DNL Camera Raw] 庫在每次處理的總像素方面存在限制。 目前，它可以在檔案的長邊處理最多65000像素，或先遇到任何條件就處理512 MP。
