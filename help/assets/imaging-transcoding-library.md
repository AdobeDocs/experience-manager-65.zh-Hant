---
title: 影像轉碼程式庫
description: 瞭解如何設定和使用Adobe的影像轉碼程式庫。此影像處理解決方案可執行核心影像處理功能，包括編碼、轉碼、影像重新取樣和影像大小調整。
contentOwner: AG
role: Administrator
feature: Renditions,Developer Tools,Asset Processing
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 0%

---


# 影像轉碼程式庫{#imaging-transcoding-library}

Adobe的影像轉碼程式庫是專屬的影像處理解決方案，可執行核心影像處理功能，包括：

* 編碼
* 轉碼（轉換支援的格式）
* 使用PS和英特爾IPP算法重新取樣影像
* 位元深度和色彩描述檔保留
* JPEG品質壓縮
* 調整影像大小

影像轉碼程式庫提供CMYK支援和完整alpha支援，但CMYK -Alpha除外。

除了支援多種檔案格式和設定檔外，在效能、延展性和品質方面，影像轉碼程式庫與其他協力廠商解決方案相比，有顯著的優勢。 以下是使用影像轉碼程式庫的主要優點：

* **隨檔案大小或解析度的增加而調整**:縮放主要是透過Imaging Coding Library的專利功能，在解碼檔案時重新調整大小。此功能可確保執行時期記憶體的使用永遠是最佳的，而不是增加檔案大小或解析度百萬像素的二次函式。 影像轉碼程式庫可處理大型和高解析度（包含高百萬像素）的檔案。 協力廠商工具（例如ImageMagick）無法處理大型檔案，在處理這類檔案時會當機。
* **Photoshop品質壓縮和調整大小演算法**:在向下取樣（平滑、銳利且自動的雙立方體）和壓縮品質方面與業界標準一致。影像轉碼程式庫進一步評估輸入影像的品質因數，並智慧地使用最佳的表格和品質設定來輸出影像。 此功能可產生最佳檔案大小，而不會影響視覺品質。
* **高吞吐量：** 響應時間較短，吞吐量始終高於ImageMagick。因此，影像轉碼程式庫應會縮短使用者的等待時間並降低代管成本。
* **使用並行負載時可以更好地擴展：** 映像轉碼庫在並行負載條件下能夠最佳地執行。它以最佳的CPU效能、記憶體使用量和低的回應時間，提供高的總處理能力，有助於降低代管成本。

## 支援的平台{#supported-platforms}

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

您可以為`-resize`參數配置以下選項：

* `X`:工作方式類似 [!DNL Experience Manager]。例如-resize 319。
* `WxH`:例如，外觀比例不會維持 `-resize 319x319`。
* `Wx`:修正寬度並計算維持長寬比的高度。例如`-resize 319x`。
* `xH`:修正高度並計算維持長寬比的寬度。例如`-resize x319`。

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 配置映像轉碼庫{#configuring-imaging-transcoding-library}

若要設定ITL處理，請建立設定檔案並更新工作流程以執行它。

### 為提取的包{#create-conf-file}建立配置檔案

要配置庫，請建立CONF檔案，以使用以下步驟指示庫。 您需要管理員或根用戶權限。

1. 從軟體分發下載[映像轉碼庫軟體包，然後使用軟體包管理器安裝它。 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg)軟體包與[!DNL Experience Manager] 6.5相容。

1. 要瞭解`com.day.cq.dam.cq-dam-switchengine`的包ID，請登錄到Web控制台，然後按一下&#x200B;**[!UICONTROL OSGi]** > **[!UICONTROL Bundles]**。 或者，若要開啟Bundles主控台，請存取`https://[aem_server:[port]/system/console/bundles/` URL。 找到`com.day.cq.dam.cq-dam-switchengine`包及其ID。

1. 使用命令`ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`檢查資料夾，確保提取所有必需的庫，其中資料夾名稱是使用包ID構建的。 例如，如果bundle id為`588`，則命令為`ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/`。

1. 建立`SWitchEngineLibs.conf`檔案以連結到庫。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 使用`cat SWitchEngineLibs.conf`命令將`/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`路徑添加到conf檔案。

1. 執行`ldconfig`命令以建立必要的連結和快取。

1. 在用於啟動[!DNL Experience Manager]的帳戶中，編輯`.bash_profile`檔案。 新增`LD_LIBRARY_PATH`，方法如下。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. 要確保路徑的值設定為`.` ，請使用`echo $LD_LIBRARY_PATH`命令。 輸出應為`.`。 如果值未設定為`.`，請重新啟動會話。

### 設定[!UICONTROL DAM更新資產]工作流程{#configure-dam-asset-update-workflow}

更新[!UICONTROL DAM更新資產]工作流程，以使用程式庫來處理影像。

1. 在[!DNL Experience Manager]用戶介面中，選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 型號]**。

1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;頁面中，以編輯模式開啟&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流模型。

1. 開啟&#x200B;**[!UICONTROL 處理縮略圖]**&#x200B;工作流處理步驟。 在&#x200B;**[!UICONTROL 縮圖]**&#x200B;標籤中，在&#x200B;**[!UICONTROL 跳過Mime類型]**清單中新增您要略過預設縮圖產生程式的MIME類型。
例如，如果您想要使用影像轉碼程式庫建立TIFF影像的縮圖，請在**[!UICONTROL 跳過Mime類型]**&#x200B;欄位中指定`image/tiff`。

1. 在&#x200B;**[!UICONTROL Web Enabled Image]**&#x200B;標籤中，添加要跳過&#x200B;**[!UICONTROL Skip List]**&#x200B;中預設Web轉譯生成過程的MIME類型。 例如，如果您在上述步驟中跳過MIME類型`image/tiff`，請將`image/tiff`添加到跳過清單。

1. 開啟&#x200B;**[!UICONTROL EPS縮圖（由ImageMagick提供）]**&#x200B;步驟，導航至&#x200B;**[!UICONTROL 參數]**&#x200B;頁籤。 在&#x200B;**[!UICONTROL Mime類型]**&#x200B;清單中，添加您希望映像轉碼庫處理的MIME類型。 例如，如果您跳過上述步驟中的MIME類型`image/tiff`，請將`image/jpeg`添加到&#x200B;**[!UICONTROL Mime類型]**&#x200B;清單中。

1. 刪除預設命令（如果有）。

1. 切換側面板，並從步驟清單中新增&#x200B;**[!UICONTROL SWitchEngine處理常式]**。

1. 根據您的自定義要求，向[!UICONTROL SwitchEngine處理程式]添加命令。 調整您指定的命令參數，以符合您的需求。 例如，如果要保留JPEG影像的顏色配置檔案，請將以下命令添加到&#x200B;**[!UICONTROL Commands]**&#x200B;清單：

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![石竹](assets/chlimage_1-199.png)

1. （可選）使用單一命令從中介轉譯產生縮圖。 中間轉譯充當源，以生成靜態和Web轉譯。 此方法比先前的方法快。 不過，您無法使用此方法將自訂參數套用至縮圖。

   ![石竹](assets/chlimage_1-200.png)

1. 若要產生Web轉譯，請在&#x200B;**[!UICONTROL 啟用Web的Image]**&#x200B;標籤中設定參數。

1. 同步更新的[!UICONTROL DAM更新資產]工作流程模型。 儲存工作流程。

驗證配置、上傳TIFF影像並監視error.log檔案。 您會注意到`INFO`訊息中提及`SwitchEngineHandlingProcess execute: executing command line`。 記錄檔提及產生的轉譯。 工作流程完成後，您可以在[!DNL Experience Manager]中檢視新轉譯。

>[!MORELIKETHIS]
>
>* [支援的MIME類型文章](assets-formats.md#supported-image-transcoding-library)

