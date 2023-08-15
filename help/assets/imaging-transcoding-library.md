---
title: 影像轉碼程式庫
description: 瞭解如何設定和使用Adobe的影像轉碼資料庫，這是一個可執行核心影像處理功能（包括編碼、轉碼、影像重新取樣和影像調整大小）的影像處理解決方案。
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# 影像轉碼程式庫 {#imaging-transcoding-library}

Adobe的Imaging Transcoding Library是專屬的影像處理解決方案，可執行核心影像處理功能，包括：

* 編碼
* 轉碼（轉換支援的格式）
* 影像重新取樣，使用PS和Intel IPP演演算法
* 位元深度和色彩設定檔保留
* JPEG品質壓縮
* 調整影像大小

影像轉碼資料庫提供CMYK支援和完整Alpha支援，但CMYK -Alpha除外。

除了支援各式各樣的檔案格式與設定檔外，影像轉碼程式庫在效能、擴充能力及品質方面，較其他協力廠商解決方案都具備顯著優勢。 以下是使用「影像轉碼程式庫」的一些主要優點：

* **隨檔案大小或解析度的增加而縮放**：縮放主要是透過影像轉碼程式庫的專利功能達成，可在解碼檔案時重新調整大小。 此功能可確保執行階段記憶體的使用永遠是最佳的，而不是增加檔案大小或解析度Mappixel的二次函式。 影像轉碼程式庫可處理較大且高解析度（包含較高百萬畫素）的檔案。 第三方工具（例如ImageMagick）無法處理大型檔案，且在處理這類檔案時當機。
* **Photoshop品質壓縮和調整演演算法大小**：與向下取樣品質（平滑、銳利且自動的雙立方式）和壓縮品質的業界標準一致。 「影像轉碼程式庫」會進一步評估輸入影像的品質因數，並聰明地使用輸出影像的最佳表格與品質設定。 此功能可產生最佳大小的檔案，而不會影響視覺品質。
* **高輸送量：** 回應時間較低，處理量也始終高於ImageMagick。 因此，「影像轉碼程式庫」應可減少使用者的等待時間及託管成本。
* **同時載入時擴充效果更佳：** 「影像轉碼程式庫」在同時載入的條件下執行時效果最佳。 透過最佳的CPU效能、記憶體使用率以及低回應時間，提供高傳輸量，有助於降低託管成本。

## 支援平台 {#supported-platforms}

影像轉碼資料庫僅適用於RHEL 7和CentOS 7發行版本。

>[!NOTE]
>
>不支援Mac OS和其他*nix發行版本（例如Debian和Ubuntu）。

## 使用狀況 {#usage}

「影像轉碼程式庫」的命令列引數可包含下列專案：

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth '4' is automatically converted to '8'
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

您可以為以下專案設定下列選項： `-resize` 引數：

* `X`：作用類似於 [!DNL Experience Manager]. 例如 — resize 319。
* `WxH`：未維護外觀比例，例如 `-resize 319x319`.
* `Wx`：修正寬度並計算高度，以維持外觀比例。 例如 `-resize 319x`。
* `xH`：修正高度並計算寬度，以維持外觀比例。 例如 `-resize x319`。

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 設定影像轉碼程式庫 {#configuring-imaging-transcoding-library}

若要設定ITL處理，請建立設定檔並更新工作流程以執行。

### 為擷取的套件組合建立設定檔 {#create-conf-file}

若要配置物件庫，請使用下列步驟建立CONF檔案以指示物件庫。 您需要管理員或根許可權。

1. 下載 [Software Distribution的Imaging Transcoding Library套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) 並使用封裝管理員進行安裝。 此套件相容於 [!DNL Experience Manager] 6.5.

1. 要瞭解的套件ID `com.day.cq.dam.cq-dam-switchengine`，登入網頁主控台並按一下 **[!UICONTROL osgi]** > **[!UICONTROL 組合]**. 或者，若要開啟套件組合主控台，請存取 `https://[aem_server:[port]/system/console/bundles/` URL。 尋找 `com.day.cq.dam.cq-dam-switchengine` 套件組合及其ID。

1. 使用命令檢查資料夾，確定已擷取所有必要的程式庫 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`，其中資料夾名稱是使用組合ID建構。 例如，指令為 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` 如果套件id為 `588`.

1. 建立 `SWitchEngineLibs.conf` 檔案以連結至程式庫。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 新增 `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` conf檔案的路徑，使用 `cat SWitchEngineLibs.conf` 命令。

1. 執行 `ldconfig` 命令來建立必要的連結和快取。

1. 在用於啟動的帳戶中 [!DNL Experience Manager]，編輯 `.bash_profile` 檔案。 新增 `LD_LIBRARY_PATH` 新增下列內容。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. 若要確保路徑的值設為 `.`，使用 `echo $LD_LIBRARY_PATH` 命令。 輸出應為 `.`. 如果值未設定為 `.`，重新啟動工作階段。

### 設定 [!UICONTROL DAM更新資產] 工作流程 {#configure-dam-asset-update-workflow}

更新 [!UICONTROL DAM更新資產] 使用資料庫處理影像的工作流程。

1. 在 [!DNL Experience Manager] 使用者介面，選取 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.

1. 從 **[!UICONTROL 工作流程模型]** 頁面，開啟 **[!UICONTROL DAM更新資產]** 編輯模式的工作流程模型。

1. 開啟 **[!UICONTROL 程式縮圖]** 工作流程程式步驟。 在 **[!UICONTROL 縮圖]** 標籤，新增要略過中預設縮圖產生程式的MIME型別 **[!UICONTROL 略過MIME型別]** 清單。
例如，如果您想使用「影像轉碼程式庫」建立TIFF影像的縮圖，請指定 `image/tiff` 在 **[!UICONTROL 略過MIME型別]** 欄位。

1. 在 **[!UICONTROL 啟用Web的影像]** 標籤，新增要略過預設Web轉譯產生程式的MIME型別 **[!UICONTROL 略過清單]**. 例如，如果您略過MIME型別 `image/tiff` 在上述步驟中，新增 `image/tiff` 跳至跳過清單。

1. 開啟 **[!UICONTROL EPS縮圖（ImageMagick提供）]** 步驟，導覽至 **[!UICONTROL 引數]** 標籤。 在 **[!UICONTROL Mime型別]** 清單，新增您想要「影像轉碼程式庫」處理的MIME型別。 例如，如果您略過MIME型別 `image/tiff` 在上述步驟中，新增 `image/jpeg` 至 **[!UICONTROL Mime型別]** 清單。

1. 移除預設命令（如果存在）。

1. 切換側面板並從步驟清單中新增 **[!UICONTROL SWitchEngine處理常式]**.

1. 將命令新增至 [!UICONTROL SwitchEngine處理常式] 根據您的自訂需求。 調整您指定的指令引數，以符合您的需求。 例如，如果要保留JPEG影像的色彩設定檔，請將下列指令新增至 **[!UICONTROL 命令]** 清單：

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![變更](assets/chlimage_1-199.png)

1. （選用）使用單一命令從中繼轉譯產生縮圖。 中繼轉譯會作為產生靜態和Web轉譯的來源。 此方法比舊版方法速度更快。 不過，使用此方法時無法將自訂引數套用至縮圖。

   ![變更](assets/chlimage_1-200.png)

1. 若要產生Web轉譯，請在 **[!UICONTROL 可支援Web的影像]** 標籤。

1. 同步處理更新的 [!UICONTROL DAM更新資產] 工作流程模型。 儲存工作流程。

若要驗證設定，請上傳TIFF影像並監視error.log檔案。 您會注意到 `INFO` 訊息中提及以下專案： `SwitchEngineHandlingProcess execute: executing command line`. 記錄檔會提及產生的轉譯。 工作流程完成後，您便可以在中檢視新的轉譯 [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [支援的MIME型別文章](assets-formats.md#supported-image-transcoding-library)
