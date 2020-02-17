---
title: Camera raw支援
description: 瞭解如何在Adobe Experience Manager Assets中啟用Camera raw支援。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0b8472dbfbfe326b4b5fe0d43b0f361318b37d16

---


# 支援使用Camera raw處理影像 {#camera-raw-support}

您可以啟用Camera raw支援來處理原始檔案格式，例如CR2、NEF和RAF，並以JPEG格式呈現影像。 Adobe Experience Manager Assets使用Camera Raw透過Package Share提供的 [Camera Raw套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) ，支援這項功能。

>[!NOTE]
>
>此功能僅支援JPEG轉譯。 它在Windows 64位元、Mac OS和RHEL 7.x上都受支援。

若要在Adobe Experience Manager Assets中啟用Camera raw支援，請依照下列步驟進行：

1. 從Package Share [下載Camera Raw](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) (Camera Raw)套件。
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

您現在可以將Camera Raw檔案匯入AEM Assets。 安裝Camera RAW套件並設定必要的工作流程後，「影像調整」選 **** 項會出現在側窗格的清單中。

![chlimage_1-131](assets/chlimage_1-337.png)


*圖：側窗格中的選項。*

![chlimage_1-132](assets/chlimage_1-338.png)


*圖：使用選項對影像進行輕量型編輯。*

將編輯儲存至Camera raw影像後，就會產生影 `AdjustedPreview.jpg` 像的新轉譯。 對於「Camera Raw」以外的其他影像類型，變更會反映在所有轉譯中。

## 最佳實務、已知問題和限制 {#best-practices}

此功能有下列限制：

* 此功能僅支援JPEG轉譯。 它在Windows 64位元、Mac OS和RHEL 7.x上都受支援。
* RAW和DNG格式不支援中繼資料回寫。
* Camera raw程式庫在每次處理的像素總數上有限制。 目前，不論先遇到何種條件，它都可處理檔案長邊最多65000像素，或512 MP。
