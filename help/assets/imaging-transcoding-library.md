---
title: 影像轉碼程式庫
description: 了解如何設定和使用Adobe的影像轉碼程式庫，此影像處理解決方案可執行核心影像處理功能，包括編碼、轉碼、影像重新取樣和影像大小調整。
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# 影像轉碼程式庫 {#imaging-transcoding-library}

Adobe的影像轉碼程式庫是專屬的影像處理解決方案，可執行核心影像處理功能，包括：

* 編碼
* 轉碼（轉換支援的格式）
* 影像重採樣，使用PS和英特爾IPP算法
* 位深度和顏色輪廓保留
* JPEG品質壓縮
* 調整影像大小

Imaging Condricing Library提供CMYK支援和完整Alpha支援，但CMYK -Alpha除外。

除了支援多種檔案格式和配置檔案外，影像轉碼庫在效能、可擴充性和質量方面比其他第三方解決方案具有顯著優勢。 以下是使用影像轉碼程式庫的主要優點：

* **隨檔案大小或解析度的增加而擴展**:擴充功能主要是透過影像轉碼程式庫的專利功能，在對檔案解碼時重新調整大小。 此功能可確保運行時記憶體使用始終是最佳的，而不是增加檔案大小或解析度百萬像素的二次函式。 影像轉碼程式庫可處理大型和高解析度（包含高百萬像素）檔案。 第三方工具（如ImageMagick）在處理此類檔案時無法處理大型檔案和當機。
* **Photoshop品質壓縮和調整大小演算法**:在下採樣質量（平滑、銳利和自動雙斜比克）和壓縮質量方面與行業標準一致。 影像轉碼庫進一步評估輸入影像的品質因數，並智慧地為輸出影像使用最佳的表格和質量設定。 此功能可產生最佳大小的檔案，而不會影響視覺品質。
* **高吞吐量：** 響應時間較短，吞吐量始終高於ImageMagick。 因此，影像轉碼程式庫應能減少使用者的等待時間和托管成本。
* **隨著同時負載的增加，擴展效果更好：** 影像轉碼程式庫在同時負載條件下，會以最佳方式執行。 它提供了高吞吐量、最佳CPU效能、記憶體使用率和低響應時間，從而有助於降低托管成本。

## 支援平台 {#supported-platforms}

影像轉碼程式庫僅適用於RHEL 7和CentOS 7發行。

>[!NOTE]
>
>不支援Mac OS和其他*nix分發（例如Debian和Ubuntu）。

## 使用狀況 {#usage}

影像轉碼程式庫的命令列引數可包含下列項目：

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

* `X`:類似 [!DNL Experience Manager]. 例如 — 調整大小319。
* `WxH`:外觀比例沒有維護，例如 `-resize 319x319`.
* `Wx`:固定寬度並計算保持長寬比的高度。 例如 `-resize 319x`。
* `xH`:固定高度並計算保持外觀比例的寬度。 例如 `-resize x319`。

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 配置影像轉碼庫 {#configuring-imaging-transcoding-library}

若要設定ITL處理，請建立設定檔案並更新工作流程以執行它。

### 為提取的捆綁包建立配置檔案 {#create-conf-file}

若要設定程式庫，請建立CONF檔案，使用下列步驟指出程式庫。 您需要管理員或根權限。

1. 下載 [從Software Distribution轉碼影像庫套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) 並使用軟體包管理器進行安裝。 該包與 [!DNL Experience Manager] 6.5。

1. 若要了解 `com.day.cq.dam.cq-dam-switchengine`，登入Web主控台，然後按一下 **[!UICONTROL OSGi]** > **[!UICONTROL 套件組合]**. 或者，若要開啟套件組合主控台，請存取 `https://[aem_server:[port]/system/console/bundles/` URL。 找出 `com.day.cq.dam.cq-dam-switchengine` 捆綁及其ID。

1. 使用命令檢查資料夾，確保擷取所有必要的程式庫 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`，其中使用套件ID建構資料夾名稱。 例如，命令為 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` 如果套件id為 `588`.

1. 建立 `SWitchEngineLibs.conf` 檔案來連結至程式庫。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 新增 `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` 路徑至「conf」檔案，使用 `cat SWitchEngineLibs.conf` 命令。

1. 執行 `ldconfig` 命令建立必要的連結和快取。

1. 在用於開始的帳戶中 [!DNL Experience Manager]，編輯 `.bash_profile` 檔案。 新增 `LD_LIBRARY_PATH` 新增下列項目。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. 確保路徑的值設定為 `.`，使用 `echo $LD_LIBRARY_PATH` 命令。 產出應該是 `.`. 如果值未設為 `.`，請重新啟動工作階段。

### 設定 [!UICONTROL DAM更新資產] 工作流程 {#configure-dam-asset-update-workflow}

更新 [!UICONTROL DAM更新資產] 工作流程，以使用程式庫處理影像。

1. 在 [!DNL Experience Manager] 用戶介面，選擇 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.

1. 從 **[!UICONTROL 工作流程模型]** 頁面，開啟 **[!UICONTROL DAM更新資產]** 工作流模型。

1. 開啟 **[!UICONTROL 處理縮圖]** 工作流程處理步驟。 在 **[!UICONTROL 縮圖]** 標籤，新增您要略過預設縮圖產生程式的MIME類型 **[!UICONTROL 跳過Mime類型]** 清單。
例如，如果您想使用「影像轉碼程式庫」建立TIFF影像的縮圖，請指定 `image/tiff` 在 **[!UICONTROL 跳過Mime類型]** 欄位。

1. 在 **[!UICONTROL 啟用Web的映像]** 頁簽，添加要跳過預設Web格式副本生成過程的MIME類型 **[!UICONTROL 略過清單]**. 例如，如果您略過MIME類型 `image/tiff` 在上述步驟中，新增 `image/tiff` 到跳過清單。

1. 開啟 **[!UICONTROL EPS縮圖（由ImageMagick提供）]** 步驟，導覽至 **[!UICONTROL 引數]** 標籤。 在 **[!UICONTROL Mime類型]** 清單中，新增您要影像轉碼程式庫處理的MIME類型。 例如，如果您略過MIME類型 `image/tiff` 在上述步驟中，新增 `image/jpeg` 到 **[!UICONTROL Mime類型]** 清單。

1. 刪除預設命令（如果存在）。

1. 切換側面板，並從新增步驟清單中 **[!UICONTROL SWitchEngine處理程式]**.

1. 將命令添加到 [!UICONTROL SwitchEngine處理程式] 根據您的自訂需求。 調整指定的命令參數以滿足您的要求。 例如，如果要保留JPEG影像的顏色配置檔案，請將以下命令添加到 **[!UICONTROL 命令]** 清單：

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![奇利馬奇](assets/chlimage_1-199.png)

1. （可選）使用單一命令從中間轉譯產生縮圖。 中間轉譯可作為來源，以產生靜態和Web轉譯。 此方法比先前的方法快。 不過，您無法使用此方法將自訂參數套用至縮圖。

   ![奇利馬奇](assets/chlimage_1-200.png)

1. 若要產生Web轉譯，請在 **[!UICONTROL 啟用Web的映像]** 標籤。

1. 同步更新的 [!UICONTROL DAM更新資產] 工作流程模型。 儲存工作流程。

驗證配置、上傳TIFF映像並監視error.log檔案。 您會注意到 `INFO` 含有提及次數的訊息 `SwitchEngineHandlingProcess execute: executing command line`. 記錄檔提及產生的轉譯。 工作流程完成後，您可以在 [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [支援的MIME類型文章](assets-formats.md#supported-image-transcoding-library)

