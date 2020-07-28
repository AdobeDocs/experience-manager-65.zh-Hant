---
title: 在中管理視訊資產 [!DNL Adobe Experience Manager]。
description: 在中上傳、預覽、註解和發佈視訊資產 [!DNL Adobe Experience Manager]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8c481c9a5052ff057ae0857c2ac825cec2b26269
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 7%

---


# 管理影片資產 {#manage-video-assets}

視訊格式是組織數位資產的重要部分。 [!DNL Adobe Experience Manager] 提供成熟的產品和功能，以管理視訊資產在建立後的整個生命週期。

瞭解如何在中管理和編輯視訊資產 [!DNL Adobe Experience Manager Assets]。 此外，如果您有使用授權，請 [!DNL Dynamic Media]參閱動態 [媒體視訊檔案](/help/assets/video.md)。

## 上傳和預覽視訊資產 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 使用擴充功能MP4產生視訊資產的預覽。 如果資產的格式不是MP4，請安裝FFmpeg套件以產生預覽。 Fmpeg會建立OGG和MP4類型的視訊轉譯。 您可以在「資產」使用者介面中預覽轉譯。

1. 在「數位資產」檔案夾或子檔案夾中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請按一下工 **[!UICONTROL 具列中的]** 「建立」，然後選擇「 **[!UICONTROL 檔案」]**。 或者，直接將它拖曳至資產區域。 如需上 [傳作業的詳細資訊](managing-assets-touch-ui.md#uploading-assets) ，請參閱上傳資產。
1. 若要在「卡片」檢視中預覽視訊，請按一下 **[!UICONTROL 視訊資產]**![上的「播放](assets/do-not-localize/play.png) 」選項。 您只能在卡片檢視中暫停或播放影片。 「播 [!UICONTROL 放] 」和「暫 [!UICONTROL 停] 」選項在清單檢視中不可用。

1. 若要在資產詳細資訊頁面中預覽視訊，請按一 **[!UICONTROL 下資訊卡]** 上的編輯。 視訊會在瀏覽器的原生視訊播放器中播放。 您可以播放、暫停、控制音量，以及將視訊縮放至全螢幕。

   ![視訊播放控制項](assets/video-playback-controls.png)

## 上傳大於2 GB資產的設定 {#configuration-to-upload-assets-that-are-larger-than-gb}

根據預設， [!DNL Assets] 不會因為檔案大小限制而讓您上傳任何大於2 GB的資產。 不過，您可以進入CRXDE Lite並在目錄下建立節點，以覆蓋此限 `/apps` 制。 節點必須具有相同的節點名稱、目錄結構和順序的可比節點屬性。

除了設定 [!DNL Assets] 外，請變更下列設定以上傳大型資產：

* 增加代號過期時間。 請參 [!UICONTROL 閱網頁主控台中的] Adobe Granite CSRF Servlet `https://[aem_server]:[port]/system/console/configMgr`。 如需詳細資訊，請參 [閱CSRF保護](/help/sites-developing/csrf-protection.md)。
* 增加Dispatcher `receiveTimeout` 配置中的。 如需詳細資訊，請參 [閱Experience Manager Dispatcher設定](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)。

>[!NOTE]
>
>Classic [!DNL Experience Manager] 使用者介面沒有2-GB檔案大小限制。 此外，大型視訊的端對端工作流程也未完全受支援。

要配置較高的檔案大小限制，請在目錄中執行以下 `/apps` 步驟。

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. 在CRXDE Lite中，導覽至 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`。 要查看目錄窗口，請按一下 `>>`。
1. From the toolbar, click the **[!UICONTROL Overlay Node]**. 或者，從上 **[!UICONTROL 下文選單選取]** 「覆蓋節點」。
1. In the **[!UICONTROL Overlay Node]** dialog, click **[!UICONTROL OK]**.

   ![覆蓋節點](assets/overlay-node-path.png)

1. 重新整理瀏覽器。 覆蓋節點 `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 被選取。
1. 在「屬 **[!UICONTROL 性]** 」索引標籤中，輸入適當的值（以位元組為單位），將大小限制增加到所需大小。 例如，要將大小限制增加到30 GB，請輸入 `{sizeLimit : "32212254720"}` 值。

1. 在工具列中，按一下「全 **[!UICONTROL 部儲存」]**。
1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. 在「Web [!DNL Adobe Experience Manager] Console Bundles [!UICONTROL 」（Web控制台組合）頁面的表格「Name」（名稱）列下，找到並按一下] Adobe Granite Workflow External Process Job Handler ****。
1. On the [!UICONTROL Adobe Granite Workflow External Process Job Handler] page, set the seconds for both **[!UICONTROL Default Timeout]** and **[!UICONTROL Max Timeout]** fields to `18000` (five hours). 按一下&#x200B;**[!UICONTROL 「儲存」]**。
1. 在中， [!DNL Experience Manager]按一下「 **[!UICONTROL 工具]** 」(Tools)>「工 **[!UICONTROL 作流]** 」(Workflow **[!UICONTROL )]**>「模型」(Models)。
1. 在「工作流程模型」頁面上，選取「 **[!UICONTROL 動態媒體編碼視訊」]**，然後按一下「 **[!UICONTROL 編輯」]**。
1. 在工作流程頁面上，按兩下「動態媒 **[!UICONTROL 體視訊服務程式」元件]** 。
1. 在「步 [!UICONTROL 驟屬性] 」對話框的「常用」頁籤下，展開「 **[!UICONTROL 高級設定」]******。
1. In the **[!UICONTROL Timeout]** field, specify a value of `18000`, then click **[!UICONTROL OK]** to return to the **[!UICONTROL Dynamic Media Encode Video]** workflow page.
1. 在頁面頂端的「動態媒體編碼視訊」頁 [!UICONTROL 面標題下方] ，按一下「 **[!UICONTROL 儲存」]**。

## 發佈視訊資產 {#publish-video-assets}

發佈後，您可以將視訊資產加入網頁中做為URL，或直接內嵌資產。 如需詳細資訊，請參 [閱發佈動態媒體資產](/help/assets/publishing-dynamicmedia-assets.md)。

## 註解視訊資產 {#annotate-video-assets}

1. 在「資產」主控台中，按一 [!UICONTROL 下資產卡] 上的「編輯」，以顯示資產詳細資訊頁面。
1. 若要播放影片，請按一下「 [!UICONTROL 預覽]」。
1. 若要註解視訊，請按一下「注 **[!UICONTROL 解]** 」按鈕。 在視訊中的特定時間（畫格）加入註解。 在加上註解時，您可以在畫布上繪圖，並在繪圖中加入註解。 注釋會自動儲存。

   ![在視訊影格上繪圖和加上註解](assets/annotate-video.png)

   要退出注釋嚮導，請按一下「關 **[!UICONTROL 閉」]**。

1. 尋找視訊中的特定點，在&#x200B;**「文字」**&#x200B;欄位中指定時間 (以秒為單位)，然後按一下&#x200B;**「跳至」**。例如，若要略過前 10 秒的視訊，請在文字欄位中輸入 20。

   ![尋找視訊中要略過指定秒數的時間](assets/seek-in-video.png)

1. 要在時間軸中查看，請按一下注釋。 要從時間軸刪除注釋，請按一下「刪 **[!UICONTROL 除」]**。

   ![在時間軸中檢視註解和詳細資訊](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [在Experience Manager Assets中管理數位資產](/help/assets/managing-assets-touch-ui.md)
>* [在Experience Manager Assets中管理系列](/help/assets/managing-collections-touch-ui.md)

