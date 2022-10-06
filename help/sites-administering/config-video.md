---
title: 設定視訊元件
seo-title: Configure the Video component
description: 了解如何設定視訊元件。
seo-description: Learn how to configure the Video Component.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# 設定視訊元件 {#configure-the-video-component}

此 [視訊元件](/help/sites-authoring/default-components-foundation.md#video) 可讓您將預先定義的現成可用(OOTB)視訊資產放在頁面上。

為了正確轉碼，管理員將單獨安裝FFmpeg。 請參閱 [安裝FFmpeg並配置AEM](#install-ffmpeg). 管理員也 [設定視訊設定檔](#configure-video-profiles) 用於HTML5元素。

>[!CAUTION]
>
>此基礎元件已淘汰。 Adobe建議使用 [核心元件內嵌元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html) 。

>[!CAUTION]
>
>若不進行廣泛的專案層級自訂，此元件將不再可立即運作。

## 設定視訊設定檔 {#configure-video-profiles}

若要使用HTML5元素，請定義視訊描述檔。 此處選擇的依序使用。 若要存取，請使用 [設計模式](/help/sites-authoring/default-components-designmode.md) （僅限傳統UI），並選取 **[!UICONTROL 設定檔]** 標籤：

![chlimage_1-317](assets/chlimage_1-317.png)

在此對話方塊中，您也可以設定視訊元件和參數的設計 [!UICONTROL 播放], [!UICONTROL Flash]，和 [!UICONTROL 進階].

## 安裝FFmpeg並配置AEM {#install-ffmpeg}

視訊元件依賴協力廠商的開放原始碼產品FFmpeg來轉碼視訊。 下載自 [https://ffmpeg.org/](https://ffmpeg.org/). 安裝FFmpeg後，請將AEM配置為使用特定的音頻編解碼器和特定的運行時選項。

在上安裝FFmpeg **Windows**，請遵循下列步驟：

1. 將編譯的二進位檔下載為 `ffmpeg.zip`.
1. 取消封存至資料夾。
1. 設定系統環境變數 `PATH` &lt;*your-ffmpeg-location*>`\bin`.
1. 重新啟動AEM。

在上安裝FFmpeg **Mac OS X**，請遵循下列步驟：

1. 安裝Xcode，可於 [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. 安裝可於 [XQuartz](https://www.xquartz.org) 取得 [X11](https://support.apple.com/en-us/HT201341).
1. 安裝MacPorts(可在 [www.macports.org](https://www.macports.org/).
1. 在主控台中執行 `sudo port install ffmpeg` 命令，並遵循螢幕上的指示。 請確定 `FFmpeg` 執行檔已新增至 `PATH` 系統變數。

在上安裝FFmpeg **Mac OS X 10.6**，請使用預編譯版本，請遵循下列步驟：

1. 下載預編譯版本。
1. 取消封存至 `/usr/local` 目錄。
1. 在主控台中，執行 `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. 視需要變更路徑。

結束日期 **設定AEM**，請遵循下列步驟：

>[!NOTE]
>
>只有在需要進一步定制編解碼器時，才需要執行這些步驟。

1. 開啟 [!UICONTROL CRXDE Lite] 在網頁瀏覽器中。 存取 [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. 選取 `/libs/settings/dam/video/format_aac/jcr:content` 節點，並確保節點屬性如下：

   * `audioCodec` 是 `aac`.
   * `customArgs` 是 `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. 若要自訂設定，請在中建立覆蓋 `/apps/settings/` 節點，並在 `/conf/global/settings/` 節點。 無法在中編輯 `/libs` 節點。 例如，若要覆蓋路徑 `/libs/settings/dam/video/fullhd-bp`，在建立 `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >覆蓋並編輯整個設定檔節點，而不只是需要修改的屬性。 這類資源不會透過SlingResourceMerger解決。

4. 如果您變更了其中一個屬性，請按一下 **[!UICONTROL 全部儲存]**.

>[!NOTE]
>
>升級AEM執行個體時，不會保留預設現成(OOTB)工作流程模型的變更。 Adobe建議您先複製修改後的工作流模型，再編輯這些模型。 例如，複製OOTB [!UICONTROL DAM更新資產] 在編輯FFmpeg轉碼步驟之前建立模型(在 [!UICONTROL DAM更新資產] 模型，用於選擇升級前存在的視訊描述檔名稱。 接著，您可以覆蓋 `/apps` 節點，讓AEM擷取對OOTB模型的自訂變更。
