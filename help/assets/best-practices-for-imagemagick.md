---
title: 安裝和配置ImageMagick
description: 瞭解ImageMagick軟體，如何安裝它，設定命令行處理步驟，並使用它編輯、合成和從影像生成縮略圖。
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools
exl-id: 6c149d31-1e64-4d29-a32a-58bd69e9fa98
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# 安裝並配置ImageMagick以使用 [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick是用於建立、編輯、合成或轉換點陣圖影像的軟體插件。 它可以以各種格式（超過200個）讀寫影像，包括PNG、JPEG、JPEG-2000、GIF、TIFF、DPX、EXR、WebP、Postscript、PDF和SVG。 使用ImageMagick調整影像大小、翻轉、鏡像、旋轉、扭曲、剪切和變換影像。 還可以使用ImageMagick調整影像顏色、應用各種特殊效果，或繪製文本、線、多邊形、橢圓和曲線。

使用 [!DNL Adobe Experience Manager] 從命令行處理媒體處理程式，通過ImageMagick處理影像。 要使用ImageMagick處理各種檔案格式，請參見 [資產檔案格式最佳做法](/help/assets/assets-file-format-best-practices.md)。 要瞭解所有支援的檔案格式，請參見 [資產支援的格式](/help/assets/assets-formats.md)。

要使用ImageMagick處理大型檔案，請考慮記憶體要求高於通常要求、IM策略需要的潛在更改以及對效能的總體影響。 記憶體要求取決於各種因素，如解析度、位深度、顏色配置檔案和檔案格式。 如果要使用ImageMagick處理非常大的檔案，請正確對 [!DNL Experience Manager] 伺服器。 最後提供了一些有益的資源。

>[!NOTE]
>
>如果您使用 [!DNL Experience Manager] 上 [!DNL Adobe Managed Services] (AMS)，如果您計畫處理許多高解析度Adobe或PSB檔案，請與PSD客戶支援聯繫。 [!DNL Experience Manager] 可能無法處理超過 30000 x 23000 像素的極高解析度 PSB 檔案。

## 安裝ImageMagick {#installing-imagemagick}

ImageMagic安裝檔案的多個版本可用於各種作業系統。 為作業系統使用相應的版本。

1. 下載相應的 [ImageMagick安裝檔案](https://www.imagemagick.org/script/download.php) 作業系統。
1. 在承載ImageMagick的磁碟上安裝ImageMagick [!DNL Experience Manager] 伺服器，啟動安裝檔案。

1. 將路徑環境變數設定為ImageMagic安裝目錄。
1. 要檢查安裝是否成功，請執行 `identify -version` 的子菜單。

## 設定命令行進程步驟 {#set-up-the-command-line-process-step}

您可以為特定用例設定命令行處理步驟。 每次將JPEG影像檔案添加到時，執行這些步驟以生成翻轉影像和縮略圖（140x100、48x48、319x319和1280） `/content/dam` 的 [!DNL Experience Manager] 伺服器：

1. 在 [!DNL Experience Manager] 伺服器，轉到工作流控制台(`https://[aem_server]:[port]/workflow`)並開啟 **[!UICONTROL DAM更新資產]** 工作流模型。
1. 從 **[!UICONTROL DAM更新資產]** 工作流模型，開啟 **[!UICONTROL EPS縮略圖（由ImageMagick提供）]** 的子菜單。
1. 在 **[!UICONTROL 「參數」頁籤]**&#x200B;添加 `image/jpeg` 到 **[!UICONTROL MIME類型]** 清單框。

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. 在 **[!UICONTROL 命令]** 框中，輸入以下命令：

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. 選擇 **[!UICONTROL 刪除生成的格式副本]** 和 **[!UICONTROL 生成Web格式副本]** 標籤。

   ![選擇標誌](assets/select_flags.png)

1. 在 **[!UICONTROL 啟用Web的影像]** 頁籤，指定尺寸為1280x1280像素的格式副本的詳細資訊。 此外，指定 `image/jpeg` 的 **[!UICONTROL 米梅類型]** 框。

   ![web_enabled_image](assets/web_enabled_image.png)

1. 按一下 **[!UICONTROL 確定]** 的子菜單。

   >[!NOTE]
   >
   >的 `convert` 命令不能與某些Windows版本（例如Windows SE）一起運行，因為它與本機版本衝突 `convert` 作為Windows安裝一部分的實用程式。 在本例中，請提及ImageMagick實用程式的完整路徑。 例如，指定
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. 開啟 **[!UICONTROL 處理縮略圖]** 步驟，並添加MIME類型 `image/jpeg` 在 **[!UICONTROL 跳過MIME類型]**。

   ![skip_mime_types](assets/skip_mime_types.png)

1. 在 **[!UICONTROL 啟用Web的影像]** 頁籤，添加MIME類型 `image/jpeg` 下 **[!UICONTROL 跳過清單]**。 按一下 **[!UICONTROL 確定]** 的子菜單。

   ![已啟用Web](assets/web_enabled.png)

1. 保存工作流。

1. 要驗證處理是否正確，請將JPG映像上載到 [!DNL Assets]。 處理完成後，檢查是否生成翻轉的影像和格式副本。

## 減輕安全漏洞 {#mitigating-security-vulnerabilities}

使用ImageMagick處理映像時存在多個安全漏洞。 例如，處理用戶提交的映像涉及遠程代碼執行(RCE)的風險。

此外，各種影像處理插件都依賴於ImageMagick庫，包括但不限於PHP的影像、Ruby的影像和回形針以及nodejs的影像。

如果使用ImageMagick或受影響的庫，Adobe建議您至少執行以下任務之一（但最好同時執行兩項任務）來緩解已知的漏洞：

1. 驗證所有映像檔案是否以預期的 [&quot;魔術位元組&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) 與您支援的影像檔案類型相對應，然後將它們發送到ImageMagick進行處理。
1. 使用策略檔案禁用易受攻擊的ImageMagick編碼器。 ImageMagick的全局策略位於 `/etc/ImageMagick`。
