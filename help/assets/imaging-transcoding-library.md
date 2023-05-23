---
title: 映像轉碼庫
description: 瞭解如何配置和使用Adobe的映像轉碼庫，這是一種影像處理解決方案，可執行核心的映像處理功能，包括編碼、轉碼、影像重採樣和影像大小調整。
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# 映像轉碼庫 {#imaging-transcoding-library}

Adobe的映像轉碼庫是一種專有的影像處理解決方案，可執行核心映像處理功能，包括：

* 編碼
* 轉碼（轉換支援的格式）
* 影像重採樣，使用PS和英特爾IPP算法
* 位深度和顏色配置檔案保留
* JPEG質量壓縮
* 調整影像大小

成像轉碼庫提供CMYK支援和完全Alpha支援，CMYK -Alpha除外。

除了支援多種檔案格式和配置檔案外，在效能、可擴充性和質量方面，成像轉碼庫與其他第三方解決方案相比具有顯著優勢。 以下是使用映像轉碼庫的一些主要優點：

* **隨檔案大小或解析度的增加而擴展**:擴展主要通過映像轉碼庫的專利能力來實現，在對檔案進行解碼的同時重新調整大小。 此功能確保運行時記憶體使用始終是最佳的，而不是增加檔案大小或解析度百萬像素的二次函式。 映像轉碼庫可以處理更大、高解析度（包含更高百萬像素）的檔案。 第三方工具（如ImageMagick）在處理此類檔案時無法處理大型檔案和崩潰。
* **Photoshop質量壓縮和調整算法**:在下採樣質量（平滑、銳利和自動雙立方）和壓縮質量方面與行業標準一致。 成像轉碼庫進一步評估輸入影像的質量因子，並智慧地使用最佳表和質量設定來輸出影像。 此功能可生成大小最佳的檔案，而不會影響視覺質量。
* **高吞吐量：** 響應時間較短，吞吐量始終高於ImageMagick。 因此，映像轉碼庫應減少用戶等待時間和托管成本。
* **在併發負載下更好地擴展：** 映像轉碼庫在併發負載條件下執行最佳操作。 它提供了高吞吐量、最佳CPU效能、記憶體使用率和低響應時間，從而幫助降低托管成本。

## 支援的平台 {#supported-platforms}

映像轉碼庫僅適用於RHEL 7和CentOS 7發行版。

>[!NOTE]
>
>MacOS和其他*nix分發（例如Debian和Ubuntu）不受支援。

## 使用狀況 {#usage}

映像轉碼庫的命令行參數可以包括以下內容：

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

您可以為 `-resize` 參數：

* `X`:類似於 [!DNL Experience Manager]。 例如 — resize 319。
* `WxH`:不維護縱橫比，例如 `-resize 319x319`。
* `Wx`:固定寬度並計算保持長寬比的高度。 例如 `-resize 319x`。
* `xH`:固定高度並計算保持長寬比的寬度。 例如 `-resize x319`。

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 配置映像轉碼庫 {#configuring-imaging-transcoding-library}

要配置國際交易日誌處理，請建立配置檔案並更新工作流以執行它。

### 為提取的包建立配置檔案 {#create-conf-file}

要配置庫，請建立CONF檔案，以使用以下步驟指示庫。 您需要管理員或根權限。

1. 下載 [從軟體分發獲取映像轉碼庫包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) 並使用包管理器安裝。 包與 [!DNL Experience Manager] 6.5

1. 要瞭解捆綁ID `com.day.cq.dam.cq-dam-switchengine`，登錄到Web控制台，然後按一下 **[!UICONTROL OSGi]** > **[!UICONTROL 捆綁]**。 或者，要開啟捆綁控制台，請訪問 `https://[aem_server:[port]/system/console/bundles/` URL。 定位 `com.day.cq.dam.cq-dam-switchengine` 捆綁及其ID。

1. 通過使用命令檢查資料夾，確保提取所有所需的庫 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`，其中使用捆綁包ID構建資料夾名稱。 例如，命令為 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` 如果捆綁id `588`。

1. 建立 `SWitchEngineLibs.conf` 檔案以連結到庫。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 添加 `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` conf檔案的路徑 `cat SWitchEngineLibs.conf` 的子菜單。

1. 執行 `ldconfig` 命令建立必需的連結和快取。

1. 在用於啟動的帳戶中 [!DNL Experience Manager]編輯 `.bash_profile` 的子菜單。 添加 `LD_LIBRARY_PATH` 按鈕。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. 確保路徑的值設定為 `.`。 `echo $LD_LIBRARY_PATH` 的子菜單。 產出應該是 `.`。 如果未將值設定為 `.`，重新啟動會話。

### 配置 [!UICONTROL DAM更新資產] 工作流 {#configure-dam-asset-update-workflow}

更新 [!UICONTROL DAM更新資產] 工作流，使用庫處理影像。

1. 在 [!DNL Experience Manager] 用戶介面，選擇 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。

1. 從 **[!UICONTROL 工作流模型]** 的子菜單。 **[!UICONTROL DAM更新資產]** 工作流模型處於編輯模式。

1. 開啟 **[!UICONTROL 處理縮略圖]** 工作流進程步驟。 在 **[!UICONTROL 縮略圖]** 頁籤，添加要跳過預設縮略圖生成過程的MIME類型 **[!UICONTROL 跳過MIME類型]** 清單框。
例如，如果要使用映像轉碼庫為TIFF影像建立縮略圖，請指定 `image/tiff` 的 **[!UICONTROL 跳過MIME類型]** 的子菜單。

1. 在 **[!UICONTROL 啟用Web的影像]** 頁籤，添加要跳過預設Web格式副本生成過程的MIME類型 **[!UICONTROL 跳過清單]**。 例如，如果跳過MIME類型 `image/tiff` 在上述步驟中，添加 `image/tiff` 跳過清單。

1. 開啟 **[!UICONTROL EPS縮略圖（由ImageMagick提供）]** 步驟，導航到 **[!UICONTROL 參數]** 頁籤。 在 **[!UICONTROL MIME類型]** 清單，添加要處理映像轉碼庫的MIME類型。 例如，如果跳過了MIME類型 `image/tiff` 在上述步驟中，添加 `image/jpeg` 到 **[!UICONTROL MIME類型]** 清單框。

1. 如果存在預設命令，請刪除該命令。

1. 切換側面板和從步驟清單添加 **[!UICONTROL SWitchEngine處理程式]**。

1. 將命令添加到 [!UICONTROL SwitchEngine處理程式] 根據您的自定義要求。 調整您為滿足要求而指定的命令的參數。 例如，如果要保留JPEG影像的顏色配置檔案，請向 **[!UICONTROL 命令]** 清單：

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![漂](assets/chlimage_1-199.png)

1. （可選）使用單個命令從中間格式副本生成縮略圖。 中間格式副本用作源以生成靜態和Web格式副本。 該方法比較早的方法快。 但是，不能使用此方法將自定義參數應用於縮略圖。

   ![漂](assets/chlimage_1-200.png)

1. 要生成Web格式副本，請在 **[!UICONTROL 啟用Web的映像]** 頁籤。

1. 同步更新的 [!UICONTROL DAM更新資產] 工作流模型。 保存工作流。

驗證配置、上載TIFF映像和監視error.log檔案。 你會注意到 `INFO` 帶有提及的消息 `SwitchEngineHandlingProcess execute: executing command line`。 日誌提到生成的格式副本。 工作流完成後，您可以在 [!DNL Experience Manager]。

>[!MORELIKETHIS]
>
>* [支援的MIME類型項目](assets-formats.md#supported-image-transcoding-library)

