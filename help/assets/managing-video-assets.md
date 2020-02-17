---
title: 管理視訊資產
description: 瞭解如何上傳、預覽、註解和發佈視訊資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 管理視訊資產 {#manage-video-assets}

瞭解如何在Adobe Experience Manager(AEM)Assets中管理和編輯視訊資產。 此外，如果您取得使用Dynamic media的授權，請參閱 [Dynamic Media視訊檔案](/help/assets/video.md)。

## 上傳和預覽視訊資產 {#upload-and-preview-video-assets}

Adobe Experience Manager Assets會使用擴充功能MP4產生視訊資產的預覽。 如果資產的格式不是MP4，請安裝FFmpeg套件以產生預覽。 Fmpeg會建立OGG和MP4類型的視訊轉譯。 您可以在AEM Assets使用者介面中預覽這些轉譯。

1. 在「數位資產」檔案夾或子檔案夾中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請按一下或點選工 **[!UICONTROL 具列中的]** 「建立」，然後選擇「 **[!UICONTROL 檔案」]**。 或者，直接將它拖曳至資產區域。 如需 [上傳作業的詳細資訊](managing-assets-touch-ui.md#uploading-assets) ，請參閱上傳資產。
1. 若要在「卡片」檢視中預覽影片，請點選影 **[!UICONTROL 片資產]** 上的「播放」按鈕。

   ![chlimage_1-65](assets/chlimage_1-201.png)

   您只能在卡片檢視中暫停或播放影片。 「播 [!UICONTROL 放] 」和「暫  停」按鈕在清單檢視中不可用。

1. 若要在資產詳細資訊頁面中預覽視訊，請按一下或點選資 **[!UICONTROL 訊卡上的]** 「編輯」圖示。

   視訊會在瀏覽器的原生視訊播放器中播放。 您可以播放、暫停、控制音量，以及將視訊縮放至全螢幕。

   ![chlimage_1-66](assets/chlimage_1-202.png)

## 上傳大於2 GB資產的設定 {#configuration-to-upload-assets-that-are-larger-than-gb}

根據預設，Experience Manager資產不會讓您上傳任何大於2 GB的資產，因為檔案大小限制。 不過，您可以進入CRXDE Lite並在目錄下建立節點，以覆蓋此限 `/apps` 制。 節點必須具有相同的節點名稱、目錄結構和順序的可比節點屬性。

除了Experience Manager Assets組態外，請變更下列組態以上傳大型資產：

* 增加代號過期時間。 請參 [!UICONTROL 閱網頁主控台中的] Adobe Granite CSRF Servlet `https://[aem_server]:[port]/system/console/configMgr`。 如需詳細資訊，請參 [閱CSRF保護](/help/sites-developing/csrf-protection.md)。
* 增加Dispatcher `receiveTimeout` 配置中的。 如需詳細資訊，請參 [閱Experience Manager Dispatcher設定](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)。

>[!NOTE]
>
>AEM Classic使用者介面沒有2 GB檔案大小限制。 此外，大型視訊的端對端工作流程也未完全受支援。

要配置較高的檔案大小限制，請在目錄中執行以下 `/apps` 步驟。

1. 在AEM中，點選「 **[!UICONTROL 工具]** >一般 **** > **[!UICONTROL CRXDE Lite]**」。
1. 在CRXDE Lite中，導覽至 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`。 要查看目錄窗口，請觸摸圖 `>>` 標。
1. 從工具列中點選「覆 **[!UICONTROL 蓋節點」]**。 或者，從上 **[!UICONTROL 下文選單選取]** 「覆蓋節點」。
1. 在「覆蓋 **[!UICONTROL 節點」對話方]** ，點選「 **[!UICONTROL 確定」]**。

   ![chlimage_1-67](assets/chlimage_1-203.png)

1. 重新整理瀏覽器。 覆蓋節點 `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 被選取。
1. 在「屬 **[!UICONTROL 性]** 」索引標籤中，輸入適當的值（以位元組為單位），將大小限制增加到所需大小。 例如，要將大小限制增加到30 GB，請輸入 `{sizeLimit : "32212254720"}` 值。

1. 從工具列，按一下「全 **[!UICONTROL 部儲存」]**。
1. 在AEM中，點選「 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web Console]**」。
1. 在「Adobe Experience Manager Web Console Bundles」頁面的表格「名稱」欄下方，找出並點選「 **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**」。
1. 在「Adobe Granite Workflow External Process Job Handler」（Adobe Granite工作流程外部流程作業處理程式）頁面中，將「 **[!UICONTROL Default Timeout]** 」(預設逾時 **[!UICONTROL )和「]** Max Timeout `18000` 」（最大逾時）欄位的秒數設為（5小時）。
1. 點選「 **[!UICONTROL 儲存]**」。
1. 在AEM中，點選「工 **[!UICONTROL 具]** >工 **[!UICONTROL 作流程]** > **[!UICONTROL 模型]**」。
1. 在「工作流程模型」頁面上，選取「 **[!UICONTROL 動態媒體編碼視訊]**」，然後點選「 **[!UICONTROL 編輯」]**。
1. 在工作流程頁面上，點選兩下 **[!UICONTROL Dynamic Media Video Service Process元件]** 。
1. 在「步 [!UICONTROL 驟屬性] 」對話框的「常用」頁籤下，展開「 **[!UICONTROL 高級設定」]******。
1. 在「逾 **[!UICONTROL 時]** 」欄位中，指定值 `18000`，然後點選「確定」以返回「動態媒體編碼 ******** 視訊」工作流程頁面。
1. 在頁面頂端的「動態媒體編碼視訊」頁面標題下方，點選「儲 **[!UICONTROL 存」]**。

## 發佈視訊資產 {#publish-video-assets}

發佈視訊資產後，您就可透過URL或內嵌在網頁上，將其加入網頁。 請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。

## 註解視訊資產 {#annotate-video-assets}

1. 在「資產」主控台中，按一下或點選資 [!UICONTROL 產卡片上的] 「編輯」圖示，以顯示資產詳細資訊頁面。
1. 若要播放影片，請按一下或點選「預 [!UICONTROL 覽] 」圖示。
1. 若要註解視訊，請按一下「注 **[!UICONTROL 解]** 」按鈕。 在視訊中的特定時點（畫格）加入註解。 在加上註解時，您可以在畫布上繪圖，並在繪圖中加入註解。 注釋會自動儲存。

   ![chlimage_1-68](assets/chlimage_1-204.png)

   要退出注釋嚮導，請按一下「關 **[!UICONTROL 閉」]**。

1. 尋找視訊中的特定點，在文字欄位中指定時間(以秒 **為單位** )，然後按一 **下Jump**。 例如，若要略過前10秒的視訊，請在文字欄位中輸入20。

   ![chlimage_1-69](assets/chlimage_1-205.png)

1. 要在時間軸中查看，請按一下注釋。 要從時間軸刪除注釋，請按一下「刪 **[!UICONTROL 除」]**。

   ![chlimage_1-70](assets/chlimage_1-206.png)
