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
source-git-commit: 071f4a292343f0ad52ca3700c95bf60f03c307cc
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# 設定視訊元件 {#configure-the-video-component}

視訊 [元件](/help/sites-authoring/default-components-foundation.md#video) (Video component)可讓您將預先定義、現成可用的(OOTB)視訊資產置於您的頁面上。

為了正確進行轉碼，管理員需要個別安裝FFmpeg。 請參 [閱「安裝FFmpeg和設定AEM](#install-ffmpeg)」。 管理員 [也可設定視訊設定檔](#configure-video-profiles) ，以搭配HTML5元素使用。

## 設定視訊設定檔 {#configure-video-profiles}

若要使用HTML5元素，請定義視訊描述檔。 此處選擇的按順序使用。 若要存取，請使 [用「設計模式](/help/sites-authoring/default-components-designmode.md) 」（僅限Classic UI），然後選取「描述檔 **[!UICONTROL 」標籤]** :

![chlimage_1-317](assets/chlimage_1-317.png)

在此對話方塊中，您也可以設定 [!UICONTROL Playback]、 [!UICONTROL Flash]和 [!UICONTROL Advanced的視訊元件和參數]。

## 安裝Fmpeg並設定AEM {#install-ffmpeg}

視訊元件依賴協力廠商的開放原始碼產品FFmpeg來轉碼視訊。 從https://ffmpeg.org/下 [載](https://ffmpeg.org/)。 安裝FFmpeg後，請設定AEM以使用特定的音訊codec和特定的執行時期選項。

若要在 **Windows上安裝FFmpeg**，請遵循下列步驟：

1. 將編譯的二進位檔案下載為 `ffmpeg.zip`。
1. 取消封存至資料夾。
1. 將系統環境變 `PATH` 量設&#x200B;*置為&lt;your-ffmpeg-location*>`\bin`。
1. 重新啟動AEM。

若要在 **Mac OS X上安裝FFmpeg**，請依照下列步驟進行：

1. 請在developer.apple.com/xcode上安裝 [Xcode](hhttps://developer.apple.com/xcode/)。
1. 請在 [XQuartz安裝](https://www.xquartz.org) ，以 [獲得X11](https://support.apple.com/en-us/HT201341)。
1. 安裝MacPorts，網址 [為www.macports.org](https://www.macports.org/)。
1. 在控制台中，執 `sudo port install ffmpeg` 行命令並遵循螢幕上的說明。 確保將執行檔 `FFmpeg` 的路徑添加到系統 `PATH` 變數中。

若要使用預編 **譯版本在Mac OS X 10.6**&#x200B;上安裝FFmpeg，請依照下列步驟進行：

1. 下載預編譯版本。
1. 將其取消封存至 `/usr/local` 目錄。
1. 在控制台中，執行 `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`。 視需要變更路徑。

若要 **設定AEM**，請依照下列步驟：

>[!NOTE]
>
>只有當需要進一步自訂轉碼器時，才需要這些步驟。

1. 在您 [!UICONTROL 的網頁瀏覽器中開啟] CRXDE Lite。 存取 [http://localhost:4502/crx/de](http://localhost:4502/crx/de)。
2. 選擇節 `/libs/settings/dam/video/format_aac/jcr:content` 點並確保節點屬性如下：

   * `audioCodec` 是 `aac`.
   * `customArgs` 是 `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. 若要自訂設定，請在節點中建立覆蓋 `/apps/settings/` 並在節點下移動相同 `/conf/global/settings/` 結構。 無法在節點中編 `/libs` 輯。 例如，若要覆蓋路徑， `/libs/settings/dam/video/fullhd-bp`請在中建立路徑 `/conf/global/settings/dam/video/fullhd-bp`。

   >[!NOTE]
   >
   >覆蓋並編輯整個描述檔節點，而不只是需要修改的屬性。 這些資源不會透過SlingResourceMergare解決。

4. 如果您變更了其中一個屬性，請按一下「全 **[!UICONTROL 部儲存」]**。

>[!NOTE]
>
>升級AEM例項時，不會保留預設現成可用(OOTB)工作流程模型的變更。 Adobe建議您先複製已修改的工作流程模型，再加以編輯。 例如，在編輯 [!UICONTROL DAM Update Asset] model中的「 [!UICONTROL FFmpeg轉碼」步驟之前，請複製OOTB] DAM更新資產模型，以挑選在升級前已存在的視訊描述檔名稱。 然後，您可以覆蓋節 `/apps` 點，讓AEM擷取對OOTB模型的自訂變更。
