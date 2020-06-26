---
title: '[!DNL Adobe Camera Raw]支援。'
description: 瞭解如何啟 [!DNL Adobe Camera Raw] 用中的支援 [!DNL Adobe Experience Manager Assets]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: bccc937c1e1a349ab292a748c3c7b9d0c68b6199
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 1%

---


# 使用Camera Raw處理影像 {#camera-raw-support}

您可以啟用 [!DNL Adobe Camera Raw] 支援來處理原始檔案格式，例如CR2、NEF和RAF，並以JPEG格式呈現影像。 使用「軟體散發」中 [!DNL Adobe Experience Manager Assets] 提供的 [Camera Raw套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) ，即支援此功能。

>[!NOTE]
>
>此功能僅支援JPEG轉譯。 它在Windows 64位元、Mac OS和RHEL 7.x上都受支援。

若要在中啟 [!DNL Camera Raw] 用支 [!DNL Experience Manager Assets]援，請遵循下列步驟：

1. 從「軟體 [散發」下載](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) 「Camera Raw」套件。
1. 存取 `https://[aem_server]:[port]/workflow`. 開啟「 **[!UICONTROL DAM更新資產」工作流程]** 。
1. 開啟「 **[!UICONTROL 處理縮圖]** 」步驟。
1. 在「縮圖」索引標籤中提 **[!UICONTROL 供下列設]** 定：

   * **[!UICONTROL 縮圖]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL 略過 Mime 類型]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 在「啟 **[!UICONTROL 用Web的影像]** 」標籤的「跳 **[!UICONTROL 過清單」欄位中]** ，指定 `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`。

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 從側面板，在「縮圖建立」 **[!UICONTROL 步驟下方新增「Camera Raw/DNG Handler]** 」 **[!UICONTROL 步驟]** 。
1. 在「 **[!UICONTROL Camera Raw/DNG處理常式]** 」步驟中，在「參數」標籤中新增下列 **[!UICONTROL 設定]** :

   * **[!UICONTROL Mime類型]**: `image/dng` 和 `image/x-raw-(.*)`
   * **[!UICONTROL 命令]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

>[!NOTE]
>
>請確定上述組態與Camera RAW和DNG處 **[!UICONTROL 理步驟組態的Sample DAM Update Asset]** 相同。

您現在可以將Camera Raw檔案匯入「資產」。 安裝Camera RAW套件並設定必要的工作流程後，「影像調整」選 **** 項會出現在側窗格的清單中。

![chlimage_1-131](assets/chlimage_1-337.png)

*圖： 側窗格中的選項。*

![chlimage_1-132](assets/chlimage_1-338.png)

*圖： 使用選項對影像進行輕量型編輯。*

在將編輯儲存至影 [!DNL Camera Raw] 像後，會為影像 `AdjustedPreview.jpg` 產生新的轉譯。 除了其他影像類型 [!DNL Camera Raw]外，變更會反映在所有轉譯中。

## 最佳實務、已知問題和限制 {#best-practices}

此功能有下列限制：

* 此功能僅支援JPEG轉譯。 它在Windows 64位元、Mac OS和RHEL 7.x上都受支援。
* RAW和DNG格式不支援中繼資料回寫。
* 程式 [!DNL Camera Raw] 庫在一次可處理的像素總數上有限制。 目前，不論先遇到何種條件，它都可處理檔案長邊最多65000像素，或512 MP。
