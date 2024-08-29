---
title: 影像轉碼程式庫
description: 瞭解如何設定和使用Adobe的影像轉碼資料庫，這是一個可執行核心影像處理功能（包括編碼、轉碼、影像重新取樣和影像調整大小）的影像處理解決方案。
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
solution: Experience Manager, Experience Manager Assets
source-git-commit: 9014a7dd3c9279a4da3944c1b095fd60352fdbeb
workflow-type: tm+mt
source-wordcount: '977'
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

影像轉碼程式庫提供CMYK支援和完整Alpha支援(CMYKAlpha除外)。

除了支援各式各樣的檔案格式與設定檔外，影像轉碼程式庫在效能、擴充能力及品質方面，較其他協力廠商解決方案都具備顯著優勢。 以下是使用「影像轉碼程式庫」的一些主要優點：

* **隨著檔案大小或解析度的增加而縮放**：縮放主要是透過影像轉碼程式庫的專利功能來實現，以便在解碼檔案時重新調整大小。 此功能可確保執行階段記憶體的使用永遠是最佳的，而不是增加檔案大小或解析度Mappixel的二次函式。 影像轉碼程式庫可處理較大且高解析度（包含較高百萬畫素）的檔案。 第三方工具（例如ImageMagick）無法處理大型檔案，且在處理這類檔案時當機。
* **Photoshop品質壓縮與調整演演算法大小**：向下取樣品質（平滑、銳利且自動的雙立方式）與壓縮品質符合業界標準。 「影像轉碼程式庫」會進一步評估輸入影像的品質因數，並聰明地使用輸出影像的最佳表格與品質設定。 此功能可產生最佳大小的檔案，而不會影響視覺品質。
* **高輸送量：**&#x200B;回應時間較低，而且輸送量始終高於ImageMagick。 因此，「影像轉碼程式庫」應可減少使用者的等待時間及託管成本。
* **同時載入時擴充效果更佳：**&#x200B;影像轉碼程式庫在同時載入時執行效果最佳。 透過最佳的CPU效能、記憶體使用率以及低回應時間，提供高傳輸量，有助於降低託管成本。

## 支援平台 {#supported-platforms}

影像轉碼資料庫僅適用於RHEL 8、RHEL 7和CentOS 7發行版本。

>[!NOTE]
>
>不支援Mac OS和其他*nix發行版本（例如Debian和Ubuntu）。

## 使用情況 {#usage}

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

您可以為`-resize`引數設定下列選項：

* `X`：作用類似於[!DNL Experience Manager]。 例如，-resize 319。
* `WxH`：未維護外觀比例，例如`-resize 319x319`。
* `Wx`：修正寬度並計算高度，以維持外觀比例。 例如，`-resize 319x`。
* `xH`：修正高度並計算維持外觀比例的寬度。 例如，`-resize x319`。

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 設定影像轉碼程式庫 {#configuring-imaging-transcoding-library}

若要設定ITL處理，請建立設定檔並更新工作流程以執行。

### 為擷取的套件組合建立設定檔 {#create-conf-file}

若要配置物件庫，請使用下列步驟建立CONF檔案以指示物件庫。 您需要管理員或根許可權。

1. 從Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg)下載[影像轉碼程式庫套件，並使用套件管理員進行安裝。 套件與[!DNL Experience Manager] 6.5相容。

1. 若要知道`com.day.cq.dam.cq-dam-switchengine`的套件組合ID，請登入網頁主控台，然後按一下&#x200B;**[!UICONTROL OSGi]** > **[!UICONTROL 套件組合]**。 或者，若要開啟套件組合主控台，請存取`https://[aem_server:[port]/system/console/bundles/` URL。 找到`com.day.cq.dam.cq-dam-switchengine`套件組合及其識別碼。

1. 透過使用命令`ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`檢查資料夾（其中資料夾名稱是使用組合ID建構），確保擷取了所有必要的資料庫。 例如，如果套件識別碼為`588`，則命令為`ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/`。

1. 建立`SWitchEngineLibs.conf`檔案以連結至資料庫。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 使用`cat SWitchEngineLibs.conf`命令將`/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`路徑新增至conf檔案。

1. 執行`ldconfig`命令以建立必要的連結和快取。

1. 在用來啟動[!DNL Experience Manager]的帳戶中，編輯`.bash_profile`檔案。 新增下列專案，以新增`LD_LIBRARY_PATH`。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. 若要確保路徑的值設定為`.`，請使用`echo $LD_LIBRARY_PATH`命令。 輸出應該只是`.`。 如果值未設定為`.`，請重新啟動工作階段。

### 設定[!UICONTROL DAM更新資產]工作流程 {#configure-dam-asset-update-workflow}

更新[!UICONTROL DAM更新資產]工作流程以使用資料庫處理影像。

1. 在[!DNL Experience Manager]使用者介面中，選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**。

1. 從&#x200B;**[!UICONTROL 工作流程模型]**&#x200B;頁面，在編輯模式下開啟&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程模型。

1. 開啟&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;工作流程處理步驟。 在&#x200B;**[!UICONTROL 縮圖]**&#x200B;索引標籤中，在&#x200B;**[!UICONTROL 略過MIME型別]**清單中，新增您要略過預設縮圖產生程式的MIME型別。
例如，如果您想要使用影像轉碼資料庫來建立TIFF影像的縮圖，請在**[!UICONTROL 略過MIME型別]**&#x200B;欄位中指定`image/tiff`。

1. 在&#x200B;**[!UICONTROL 啟用Web的影像]**&#x200B;索引標籤中，新增您要在&#x200B;**[!UICONTROL 略過清單]**&#x200B;中略過預設Web轉譯產生程式的MIME型別。 例如，如果您在上述步驟中略過MIME型別`image/tiff`，請新增`image/tiff`至略過清單。

1. 開啟&#x200B;**[!UICONTROL EPS縮圖（由ImageMagick支援）]**&#x200B;步驟，導覽至&#x200B;**[!UICONTROL 引數]**&#x200B;標籤。 在&#x200B;**[!UICONTROL Mime型別]**&#x200B;清單中，新增您想要「影像轉碼」程式庫處理的MIME型別。 例如，如果您在上一步中略過MIME型別`image/tiff`，請將`image/jpeg`新增到&#x200B;**[!UICONTROL Mime型別]**&#x200B;清單。

1. 移除預設命令（如果存在）。

1. 切換側面板，並從步驟清單中新增&#x200B;**[!UICONTROL SWitchEngine處理常式]**。

1. 根據您的自訂需求，將命令新增至[!UICONTROL SwitchEngine處理常式]。 調整您指定的指令引數，以符合您的需求。 例如，如果要保留JPEG影像的色彩設定檔，請將下列命令新增至&#x200B;**[!UICONTROL 命令]**&#x200B;清單：

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![chlimage](assets/chlimage_1-199.png)

1. （選用）使用單一命令從中繼轉譯產生縮圖。 中繼轉譯會作為產生靜態和Web轉譯的來源。 此方法比舊版方法速度更快。 不過，使用此方法時無法將自訂引數套用至縮圖。

   ![chlimage](assets/chlimage_1-200.png)

1. 若要產生Web轉譯，請在&#x200B;**[!UICONTROL 啟用Web的影像]**&#x200B;索引標籤中設定引數。

1. 同步處理更新的[!UICONTROL DAM更新資產]工作流程模型。 儲存工作流程。

若要驗證設定，請上傳TIFF影像並監視error.log檔案。 您將會注意到`INFO`則訊息中提及`SwitchEngineHandlingProcess execute: executing command line`。 記錄檔會提及產生的轉譯。 工作流程完成後，您可以在[!DNL Experience Manager]中檢視新的轉譯。

>[!MORELIKETHIS]
>
>* [支援的MIME型別文章](assets-formats.md#supported-image-transcoding-library)
