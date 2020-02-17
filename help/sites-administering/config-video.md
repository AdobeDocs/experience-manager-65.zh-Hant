---
title: 設定視訊元件
seo-title: 設定視訊元件
description: 瞭解如何設定視訊元件。
seo-description: 瞭解如何設定視訊元件。
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定視訊元件 {#configure-the-video-component}

視訊 [元件](/help/sites-authoring/default-components-foundation.md#video) (Video component)可讓您在頁面上放置預先定義的OOTB（現成可用）視訊元素。

若要正確進行轉碼，您的管理員必須 [安裝FFmpeg並個別設定AEM](#install-ffmpeg) 。 您也可以 [設定您的視訊描述檔](#configure-video-profiles) ，以便搭配HTML5元素使用。

## 設定視訊設定檔 {#configure-video-profiles}

您可能想要定義要用於HTML5元素的視訊描述檔。 此處選擇的按順序使用。 若要存取，請使 [用「設計模式](/help/sites-authoring/default-components-designmode.md) 」（僅限Classic UI），然後選取「描述檔 **[!UICONTROL 」標籤]** :

![chlimage_1-317](assets/chlimage_1-317.png)

您也可以設定 [!UICONTROL Playback]、 [!UICONTROL Flash]和 [!UICONTROL Advanced]的視訊元件和參數。

## 安裝Fmpeg並設定AEM {#install-ffmpeg}

視訊元件依賴協力廠商的開放原始碼產品FFmpeg，以正確轉碼可從https://ffmpeg.org/下載的視 [訊](https://ffmpeg.org/)。 在安裝FFmpeg後，您必須設定AEM以使用特定的音訊codec和特定的執行時期選項。

**若要為您的平台安裝Fmpeg**:

* **在Windows上：**

   1. 將編譯的二進位檔下載為 `ffmpeg.zip`
   1. 解壓縮至資料夾。
   1. 將系統環境變數設定 `PATH` 為 `<*your-ffmpeg-locatio*n>\bin`
   1. 重新啟動AEM。

* **在Mac OS x上：**

   1. 安裝Xcode([https://developer.apple.com/technologies/tools/xcode.html](https://developer.apple.com/technologies/tools/xcode.html))
   1. 安裝XQuartz/X11。
   1. 安裝MacPorts([https://www.macports.org/](https://www.macports.org/))
   1. 在控制台中，運行以下命令並按照說明操作：

      `sudo port install ffmpeg`

      `FFmpeg` 必須在中， `PATH` AEM才能透過命令列擷取它。

* **使用OS X 10.6的預編譯版本：**

   1. 下載預編譯版本。
   1. 將其解壓到目 `/usr/local` 錄。
   1. 從終端執行：

      `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`

**若要設定AEM**:

1. 在您 [!UICONTROL 的網頁瀏覽器中開啟] CRXDE Lite。 ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))
1. 選擇節 `/libs/settings/dam/video/format_aac/jcr:content` 點並確保節點屬性如下：

   * 音訊轉碼器：

      ```
       aac
      ```

   * customArgs:

      ```
       -flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8
      ```

1. 若要自訂設定，請在節點中建立覆蓋 `/apps/settings/` 並在節點下移動相同 `/conf/global/settings/` 結構。 無法在節點中編 `/libs` 輯。 例如，若要覆蓋路徑， `/libs/settings/dam/video/fullhd-bp`請在中建立路徑 `/conf/global/settings/dam/video/fullhd-bp`。

   >[!NOTE]
   >
   >覆蓋並編輯整個描述檔節點，而不只是需要修改的屬性。 這些資源不會透過SlingResourceMergare解決。

1. 如果您變更了其中一個屬性，請按一下「全 **[!UICONTROL 部儲存」]**。

>[!NOTE]
>
>升級AEM例項時，OOTB工作流程模型不會保留。 Adobe建議您先複製OOTB工作流程模型，再加以編輯。 例如，在編輯DAM更新資產模型中的「FMPEG轉碼」步驟之前，請複製OOTB DAM更新資產模型，以挑選在升級前已存在的視訊描述檔名稱。 然後，您可以覆蓋節 `/apps` 點，讓AEM擷取對OOTB模型的自訂變更。

