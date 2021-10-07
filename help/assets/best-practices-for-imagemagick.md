---
title: 安裝和配置ImageMagick
description: 了解ImageMagick軟體、如何安裝、設定命令列處理步驟，以及使用它來編輯、撰寫和從影像產生縮圖。
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools
exl-id: 6c149d31-1e64-4d29-a32a-58bd69e9fa98
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%

---

# 安裝並配置ImageMagick以與[!DNL Experience Manager Assets]一起使用 {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick是用於建立、編輯、合成或轉換點陣圖影像的軟體插件。 它可以讀取和寫入各種格式（超過200個）的影像，包括PNG、JPEG、JPEG-2000、GIF、TIFF、DPX、EXR、WebP、Postscript、PDF和SVG。 使用ImageMagick調整影像大小、翻轉、鏡像、旋轉、扭曲、剪切和轉換影像。 您還可以使用ImageMagick調整影像顏色、應用各種特殊效果，或繪製文本、線、多邊形、橢圓和曲線。

使用命令行中的[!DNL Adobe Experience Manager]介質處理程式通過ImageMagick處理影像。 若要使用ImageMagick使用各種檔案格式，請參閱[Assets檔案格式最佳實務](/help/assets/assets-file-format-best-practices.md)。 若要了解所有支援的檔案格式，請參閱[Assets supported formats](/help/assets/assets-formats.md)。

要使用ImageMagick處理大型檔案，請考慮高於通常的記憶體要求、IM策略所需的潛在更改以及對效能的整體影響。 記憶體需求取決於各種因素，如解析度、位深度、顏色配置檔案和檔案格式。 如果要使用ImageMagick處理非常大的檔案，請正確對[!DNL Experience Manager]伺服器進行基準測試。 最後提供一些實用的資源。

>[!NOTE]
>
>如果您在[!DNL Adobe Managed Services](AMS)上使用[!DNL Experience Manager]，如果您打算處理許多高解析度PSD或PSB檔案，請聯絡Adobe客戶支援。 [!DNL Experience Manager] 可能無法處理超過30000 x 23000像素的高解析度PSB檔案。

## 安裝ImageMagick {#installing-imagemagick}

各種作業系統均提供多個版本的ImageMagic安裝檔案。 使用適合您作業系統的版本。

1. 下載適合您作業系統的[ImageMagick安裝檔案](https://www.imagemagick.org/script/download.php)。
1. 要在[!DNL Experience Manager]伺服器所在的磁碟上安裝ImageMagick，請啟動安裝檔案。

1. 將路徑環境變數設定為ImageMagic安裝目錄。
1. 要檢查安裝是否成功，請執行`identify -version`命令。

## 設定命令行處理步驟 {#set-up-the-command-line-process-step}

您可以為您的特定使用案例設定命令列處理步驟。 每次在[!DNL Experience Manager]伺服器上將JPEG影像檔案新增至`/content/dam`時，執行下列步驟以產生翻轉的影像和縮圖（140x100、48x48、319x319和1280）:

1. 在[!DNL Experience Manager]伺服器上，前往工作流程主控台(`https://[aem_server]:[port]/workflow`)，並開啟&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程模型。
1. 從&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程模型中，開啟&#x200B;**[!UICONTROL EPS縮圖（由ImageMagick提供技術）]**&#x200B;步驟。
1. 在&#x200B;**[!UICONTROL 參數頁簽]**&#x200B;中，將`image/jpeg`添加到&#x200B;**[!UICONTROL Mime類型]**&#x200B;清單中。

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. 在&#x200B;**[!UICONTROL Commands]**&#x200B;框中，輸入以下命令：

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. 選擇&#x200B;**[!UICONTROL Delete Generated Rendition]**&#x200B;和&#x200B;**[!UICONTROL Generate Web Rendition]**&#x200B;標幟。

   ![select_flags](assets/select_flags.png)

1. 在&#x200B;**[!UICONTROL Web Enabled Image]**&#x200B;標籤中，指定尺寸為1280x1280像素的格式副本的詳細資訊。 此外，在&#x200B;**[!UICONTROL Mimetype]**&#x200B;框中指定`image/jpeg`。

   ![web_enabled_image](assets/web_enabled_image.png)

1. 按一下&#x200B;**[!UICONTROL OK]**&#x200B;以儲存變更。

   >[!NOTE]
   >
   >`convert`命令可能不在某些Windows版本（例如Windows SE）中運行，因為它與Windows安裝中的本機`convert`實用程式衝突。 在此案例中，請提及ImageMagick公用程式的完整路徑。 例如，指定
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. 開啟&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟，並在&#x200B;**[!UICONTROL 跳過Mime類型]**&#x200B;下添加MIME類型`image/jpeg`。

   ![skip_mime_types](assets/skip_mime_types.png)

1. 在&#x200B;**[!UICONTROL Web Enabled Image]**&#x200B;標籤中，在&#x200B;**[!UICONTROL Skip List]**&#x200B;下添加MIME類型`image/jpeg`。 按一下&#x200B;**[!UICONTROL OK]**&#x200B;以儲存變更。

   ![web_enabled](assets/web_enabled.png)

1. 儲存工作流程。

1. 若要驗證處理是否正確，請將JPG影像上傳至[!DNL Assets]。 處理完成後，檢查是否產生翻轉的影像和轉譯。

## 降低安全漏洞 {#mitigating-security-vulnerabilities}

使用ImageMagick處理映像時存在多個安全漏洞。 例如，處理使用者提交的影像時，可能會有遠端程式碼執行(RCE)的風險。

此外，各種影像處理插件依賴於ImageMagick庫，包括但不限於PHP的影像、Ruby的影像和回形夾，以及nodejs的影像。

如果您使用ImageMagick或受影響的程式庫，Adobe建議您透過執行下列至少一項工作（但最好同時執行兩項工作），以緩解已知弱點：

1. 在將所有影像檔案發送到ImageMagick進行處理之前，請先確認所有影像檔案的開頭都是與您支援的影像檔案類型對應的預期[&quot;magic bytes&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures)。
1. 使用策略檔案禁用有漏洞的ImageMagick編碼器。 在`/etc/ImageMagick`找到ImageMagick的全局策略。
