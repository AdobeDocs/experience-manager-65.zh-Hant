---
title: 配置視頻元件
seo-title: Configure the Video component
description: 瞭解如何配置視頻元件。
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

# 配置視頻元件 {#configure-the-video-component}

的 [視頻元件](/help/sites-authoring/default-components-foundation.md#video) 允許您將預定義的現成(OOTB)視頻資源放置到頁面上。

為了進行適當的轉碼，管理員將單獨安裝FFmpeg。 請參閱 [安裝FFmpeg並配AEM置](#install-ffmpeg)。 管理員也 [配置視頻配置檔案](#configure-video-profiles) 用於HTML5元素。

>[!CAUTION]
>
>此Foundation元件已棄用。 Adobe建議利用 [核心元件嵌入元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html) 的雙曲餘切值。

>[!CAUTION]
>
>如果不進行廣泛的項目級定制，此元件將不再需要開箱即用。

## 配置視頻配置檔案 {#configure-video-profiles}

要使用HTML5元素，請定義視頻配置檔案。 這裡選擇的按順序使用。 要訪問，請使用 [設計模式](/help/sites-authoring/default-components-designmode.md) （僅限經典UI）並選擇 **[!UICONTROL 配置檔案]** 頁籤：

![chlimage_1-317](assets/chlimage_1-317.png)

從此對話框中，還可以配置視頻元件的設計和參數 [!UICONTROL 播放]。 [!UICONTROL Flash], [!UICONTROL 高級]。

## 安裝FFmpeg並配AEM置 {#install-ffmpeg}

視頻元件依靠第三方開源產品FFmpeg進行視頻轉碼。 從 [https://ffmpeg.org/](https://ffmpeg.org/)。 安裝FFmpeg後，配置AEM為使用特定的音頻編解碼器和特定的運行時選項。

在上安裝FFmpeg **窗口**，請執行以下步驟：

1. 將編譯的二進位檔案下載為 `ffmpeg.zip`。
1. 取消存檔到資料夾。
1. 設定系統環境變數 `PATH` &lt;*您的ffmpeg位置*>`\bin`。
1. 重新啟AEM動。

在上安裝FFmpeg **MacOS X**，請執行以下步驟：

1. 安裝Xcode可在 [developer.apple.com/xcode](https://developer.apple.com/xcode/)。
1. 安裝可用於 [XQuartz](https://www.xquartz.org) 要 [X11](https://support.apple.com/en-us/HT201341)。
1. 安裝MacPorts，可從 [www.macports.org](https://www.macports.org/)。
1. 在控制台中執行 `sudo port install ffmpeg` 命令，並按照螢幕說明進行操作。 確保 `FFmpeg` 執行檔已添加到 `PATH` 系統變數。

在上安裝FFmpeg **MacOS X 10.6**，使用預編譯版本，請執行以下步驟：

1. 下載預編譯的版本。
1. 取消存檔到 `/usr/local` 的子菜單。
1. 在控制台中，執行 `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`。 根據需要更改路徑。

至 **配AEM置**，請執行以下步驟：

>[!NOTE]
>
>只有在需要進一步定制編解碼器時，才需要執行這些步驟。

1. 開啟 [!UICONTROL CRXDE Lite] 的子菜單。 訪問 [http://localhost:4502/crx/de](http://localhost:4502/crx/de)。
2. 選擇 `/libs/settings/dam/video/format_aac/jcr:content` 並確保節點屬性如下所示：

   * `audioCodec` 是 `aac`.
   * `customArgs` 是 `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. 要自定義配置，請在中建立覆蓋 `/apps/settings/` 並在 `/conf/global/settings/` 的下界。 無法在中編輯 `/libs` 的下界。 例如，要覆蓋路徑 `/libs/settings/dam/video/fullhd-bp`，在 `/conf/global/settings/dam/video/fullhd-bp`。

   >[!NOTE]
   >
   >覆蓋並編輯整個配置檔案節點，而不只是需要修改的屬性。 此類資源不會通過SlingResourceMobare解決。

4. 如果更改了其中一個屬性，請按一下 **[!UICONTROL 全部保存]**。

>[!NOTE]
>
>升級實例時，不會保留對預設出廠設定(OOTB)工作流模型的更AEM改。 Adobe建議在編輯修改的工作流模型之前先複製這些模型。 例如，複製OOTB [!UICONTROL DAM更新資產] 在編輯FFmpeg轉碼步驟之前的模型 [!UICONTROL DAM更新資產] 模型，用於選擇升級前存在的視頻配置檔案名稱。 然後，你可以 `/apps` 節點，AEM以檢索對OOTB模型的自定義更改。
