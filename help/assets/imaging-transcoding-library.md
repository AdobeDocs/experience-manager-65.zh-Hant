---
title: 影像轉碼程式庫
description: 瞭解如何設定和使用Adobe的影像轉碼程式庫。此影像處理解決方案可執行核心影像處理功能，包括編碼、轉碼、影像重新取樣和影像大小調整。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 影像轉碼程式庫 {#imaging-transcoding-library}

Adobe的影像轉碼程式庫是專屬的影像處理解決方案，可執行核心影像處理功能，包括：

* 編碼
* 轉碼（轉換支援的格式）
* 使用PS和英特爾IPP算法重新取樣影像
* 位元深度和色彩描述檔保留
* JPEG品質壓縮
* 調整影像大小

影像轉碼程式庫提供CMYK支援和完整alpha支援，但CMYK -Alpha除外。

除了支援多種檔案格式和設定檔外，在效能、延展性和品質方面，影像轉碼程式庫與其他協力廠商解決方案相比，有顯著的優勢。 以下是使用影像轉碼程式庫的主要優點：

* **隨檔案大小或解析度的增加而調整**:縮放主要是透過Imaging Coding Library的專利功能，在解碼檔案時重新調整大小。 此功能可確保執行時期記憶體的使用永遠是最佳的，而不是增加檔案大小或解析度百萬像素的二次函式。 影像轉碼程式庫可處理大型和高解析度（包含高百萬像素）的檔案。 協力廠商工具（例如ImageMagick）無法處理大型檔案，在處理這類檔案時會當機。
* **Photoshop品質壓縮和調整大小演算法**:在向下取樣（平滑、銳利且自動的雙立方體）和壓縮品質方面與業界標準一致。 影像轉碼程式庫進一步評估輸入影像的品質因數，並智慧地使用最佳的表格和品質設定來輸出影像。 此功能可產生最佳檔案大小，而不會影響視覺品質。
* **** 高吞吐量：響應時間較短，吞吐量始終高於ImageMagick。 因此，影像轉碼程式庫應會縮短使用者的等待時間並降低代管成本。
* **** 使用並行載入，可更佳地縮放：映像轉碼庫在並行負載條件下的效能最佳。 它以最佳的CPU效能、記憶體使用量和低的回應時間，提供高的總處理能力，有助於降低代管成本。

## 支援的平台 {#supported-platforms}

影像轉碼程式庫僅適用於RHEL 7和CentOS 7散發版本。

>[!NOTE]
>
>不支援Mac OS和其他*nix散發（例如Debian和Ubuntu）。

## 使用狀況 {#usage}

映像轉碼庫的命令行參數可以包括：

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

您可以為參數設定下列選 `-resize` 項：

* `X`: `Works similar to AEM. For example -resize 319.`
* `WxH`: `Aspect Ratio will not be maintained, For example -resize 319X319.`
* `Wx`: `Fixes the width and calculates the height maintaining the aspect ratio. For example -resize 319x.`
* `xH`: `Fixes the height and calculates the width maintaining the aspect ratio. For example -resize x319.`

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 配置映像轉碼庫 {#configuring-imaging-transcoding-library}

若要設定ITL處理，請建立設定檔案並更新工作流程以執行它。

### 為提取的包建立配置檔案 {#create-conf-file}

要配置庫，請建立。conf檔案，以使用以下步驟指示庫。 您需要管理員或根用戶權限。

1. 下載 [Imaging Rodcing Library軟體包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) ，並使用軟體包管理器進行安裝。 此套件與AEM 6.5相容。

1. 若要瞭解Bundle ID，請登 `com.day.cq.dam.cq-dam-switchengine`入Web Console並點選「 **[!UICONTROL OSGi > Bundles]**」。 或者，若要開啟組合主控台，請存取 `https://[aem_server:[port]/system/console/bundles/` URL。 找到 `com.day.cq.dam.cq-dam-switchengine` bundle及其ID。

1. 使用命令檢查資料夾，確保提取所有所需的庫 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`，其中資料夾名稱是使用包ID構建的。 例如，如果bundle `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` id為，則命令為 `588`。

1. 建立 `SWitchEngineLibs.conf` 要連結至程式庫的檔案。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 使用 `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` 命令將路徑添加到conf文 `cat SWitchEngineLibs.conf` 件。

1. 執行 `ldconfig` 命令以建立必要的連結和快取。

1. 在用來啟動AEM的帳戶中，編輯檔 `.bash_profile` 案。 新 `LD_LIBRARY_PATH` 增：

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. 要確保路徑的值設定為，請使 `.`用命 `echo $LD_LIBRARY_PATH` 令。 產出應該只是 `.`。 如果值未設定為，請 `.`重新啟動會話。

### 設定DAM更新資產工作流程 {#configure-dam-asset-update-workflow}

更新 [!UICONTROL DAM更新資產工作流程] ，以使用程式庫來處理影像。

1. 點選／按一下AEM標誌，然後前往「工具>工 **[!UICONTROL 作流程>模型」]**。

1. 在「工 **[!UICONTROL 作流程模型]** 」頁面中，以編輯模式開 **** 啟「DAM更新資產」工作流模型。

1. 開啟「流 **[!UICONTROL 程縮圖]** 」工作流流程步驟。 在「縮 **[!UICONTROL 圖]** 」標籤中，新增您要在「略過Mime類型」清單中略過預設縮圖產生程式的 **[!UICONTROL MIME類型]** 。
例如，如果您想要使用「影像轉碼程式庫」建立TIFF影像的縮圖，請在「跳過Mime類 `image/tiff` 型」欄 **[!UICONTROL 位中指定]** 。

1. 在「啟 **[!UICONTROL 用Web的影像]** 」索引標籤中，新增您要在「略過清單」中略過預設Web轉譯產生程式的 **[!UICONTROL MIME類型]**。 例如，如果您在上述步驟中跳 `image/tiff` 過MIME類型，請將 `image/tiff` 其添加到跳過清單。

1. 開啟 **[!UICONTROL EPS縮圖（由ImageMagick提供）步驟]** ，導覽至「 **[!UICONTROL Arguments]** 」標籤。 在「 **[!UICONTROL Mime類型]** 」清單中，添加要處理映像轉碼庫的MIME類型。 例如，如果您跳過上述步驟中 `image/tiff` 的MIME類型，請新增 `image/jpeg` 至 **[!UICONTROL Mime類型清單]** 。

1. 刪除預設命令（如果有）。

1. 切換側面板，並從步驟清單中新增 **[!UICONTROL SWitchEngine處理常式]**。

1. 根據您的自訂需 [!UICONTROL 求，將命令新增至SwitchEngine處理常式] 。 調整您指定的命令參數，以符合您的需求。 例如，如果要保留JPEG影像的顏色配置檔案，請將以下命令添加到「命 **[!UICONTROL 令]** 」清單：

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`
   ![石竹](assets/chlimage_1-199.png)

1. （可選）使用單一命令從中介轉譯產生縮圖。 中間轉譯充當源，以生成靜態和Web轉譯。 此方法比先前的方法快。 不過，您無法使用此方法將自訂參數套用至縮圖。

   ![石竹](assets/chlimage_1-200.png)

1. 若要產生Web轉譯，請在「啟用Web的影 **[!UICONTROL 像」標籤中設定參數]** 。

1. 同步更新的 [!UICONTROL DAM更新資產工作流程模] 型。 儲存工作流程。

驗證配置、上傳TIFF影像並監視error.log檔案。 您會注意到 `INFO` 訊息中提及的 `SwitchEngineHandlingProcess execute: executing command line`。 記錄檔提及產生的轉譯。 工作流程完成後，您就可以在AEM中檢視新的轉譯。

>[!MORELIKETHIS]
>
>* [支援的MIME類型文章](assets-formats.md#supported-image-transcoding-library)