---
title: '[!DNL Adobe Camera Raw]支援處理數位資產'
description: 瞭解如何啟用 [!DNL Adobe Experience Manager Assets]中的 [!DNL Adobe Camera Raw] 支援
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 3%

---

# 使用[!DNL Adobe Camera Raw]處理影像 {#camera-raw-support}

您可以啟用[!DNL Adobe Camera Raw]支援，以處理原始檔案格式（例如CR2、NEF和RAF），並以JPEG格式轉譯影像。 使用Software Distribution提供的[Camera Raw套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)的[!DNL Adobe Experience Manager Assets]支援此功能。

>[!NOTE]
>
>功能僅支援JPEG轉譯。 Windows 64位元、Mac作業系統和RHEL 7.x都支援此功能。

若要在[!DNL Experience Manager Assets]中啟用[!DNL Camera Raw]支援，請遵循下列步驟：

1. 從[!DNL Software Distribution]下載[[!DNL Camera Raw] 封裝](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip)。
1. 存取`https://[aem_server]:[port]/workflow`。 開啟&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程。
1. 編輯&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟。
1. 在&#x200B;**[!UICONTROL 縮圖]**&#x200B;索引標籤中提供下列設定：

   * **[!UICONTROL 縮圖]**： `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL 略過Mime型別]**： `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 在&#x200B;**[!UICONTROL 啟用網頁的影像]**&#x200B;索引標籤的&#x200B;**[!UICONTROL 略過清單]**&#x200B;欄位中，指定`audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`。

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 從側面板，在&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟下方新增&#x200B;**[!UICONTROL Camera Raw/DNG處理常式]**&#x200B;步驟。
1. 在&#x200B;**[!UICONTROL Camera Raw/DNG處理常式]**&#x200B;步驟中，在&#x200B;**[!UICONTROL 引數]**&#x200B;索引標籤中新增下列設定：

   * **[!UICONTROL Mime型別]**： `image/dng`和`image/x-raw-(.*)`
   * **[!UICONTROL 命令]**：

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 按一下「**[!UICONTROL 儲存]**」。

>[!NOTE]
>
>確定上述設定與&#x200B;**[!UICONTROL 具有Camera Raw和DNG處理步驟]**&#x200B;的範例DAM更新資產設定相同。

您現在可以將Camera Raw檔案匯入Assets。 安裝Camera Raw封裝並設定必要的工作流程後，**[!UICONTROL 影像調整]**&#x200B;選項會出現在側邊窗格清單中。

![chlimage_1-131](assets/chlimage_1-337.png)

*圖：側邊窗格中的選項。*

![chlimage_1-132](assets/chlimage_1-338.png)

*圖：使用選項對影像進行輕量型編輯。*

將編輯儲存至[!DNL Camera Raw]影像後，會為該影像產生新的轉譯`AdjustedPreview.jpg`。 對於[!DNL Camera Raw]以外的其他影像型別，變更會反映在所有轉譯中。

## 最佳實務、已知問題和限制 {#best-practices}

功能有下列限制：

* 功能僅支援JPEG轉譯。 Windows 64位元、Mac作業系統和RHEL 7.x都支援此功能。
* RAW和DNG格式不支援中繼資料回寫。
* [!DNL Camera Raw]資料庫一次可處理的畫素總數有限。 目前，它最多可在檔案的長邊處理65000個畫素，或處理先遇到的任何條件的512 MP。
