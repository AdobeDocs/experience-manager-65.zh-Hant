---
title: 管理影片資產
description: 在 [!DNL Adobe Experience Manager]中上傳、預覽、註解和發佈視訊資產。
contentOwner: AG
role: 業務從業人員
feature: 資產管理
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 8%

---


# 管理影片資產 {#manage-video-assets}

視訊格式是組織數位資產的重要部分。 [!DNL Adobe Experience Manager] 提供成熟的產品和功能，以管理視訊資產在建立後的整個生命週期。

瞭解如何在[!DNL Adobe Experience Manager Assets]中管理和編輯視訊資產。 使用[!DNL Dynamic Media]整合，就可進行視訊編碼和轉碼，例如FFmpeg轉碼。

## 上傳和預覽視訊資產{#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 使用擴充功能MP4產生視訊資產的預覽。如果資產的格式不是MP4，請安裝FFmpeg套件以產生預覽。 Fmpeg會建立OGG和MP4類型的視訊轉譯。 您可以在[!DNL Assets]使用者介面中預覽轉譯。

1. 在數位資產檔案夾或子檔案夾中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請從工具列按一下「建立」，然後選擇「檔案」。 ********&#x200B;或者，在用戶介面上拖動檔案。 如需詳細資訊，請參閱[上傳資產](manage-assets.md#uploading-assets)。
1. 若要在卡片檢視中預覽視訊，請按一下視訊資產上的&#x200B;**[!UICONTROL Play]** ![play選項](assets/do-not-localize/play.png)選項。 您只能在卡片檢視中暫停或播放影片。 清單檢視中不提供[!UICONTROL Play]和[!UICONTROL Pause]選項。

1. 若要在資產詳細資訊頁面中預覽視訊，請按一下卡片上的&#x200B;**[!UICONTROL Edit]**。 視訊會在瀏覽器的原生視訊播放器中播放。 您可以播放、暫停、控制音量，以及將視訊縮放至全螢幕。

   ![視訊播放控制項](assets/video-playback-controls.png)

## 上傳大於2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}的資產的設定

根據預設，[!DNL Assets]不允許您上傳任何大於2 GB的資產，因為檔案大小限制。 但是，您可以通過進入CRXDE Lite並在`/apps`目錄下建立節點來覆蓋此限制。 節點必須具有相同的節點名稱、目錄結構和可比的節點順序屬性。

除了[!DNL Assets]組態外，請變更下列組態以上傳大型資產：

* 增加代號過期時間。 請參閱`https://[aem_server]:[port]/system/console/configMgr`的「Web控制台」中的「Adobe花崗岩CSRF Servlet]」。 [!UICONTROL 如需詳細資訊，請參閱[CSRF保護](/help/sites-developing/csrf-protection.md)。
* 在Dispatcher配置中增加`receiveTimeout`。 有關詳細資訊，請參見[Experience ManagerDispatcher configuration](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)。

>[!NOTE]
>
>[!DNL Experience Manager] Classic使用者介面沒有2-GB檔案大小限制。 此外，大型視訊的端對端工作流程也未完全受支援。

要配置較高的檔案大小限制，請在`/apps`目錄中執行以下步驟。

1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**。
1. 在CRXDE Lite中，導航到`/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`。 要查看目錄窗口，請按一下`>>`。
1. 在工具列中，按一下「覆蓋節點」。 ****&#x200B;或者，從上 **[!UICONTROL 下文選單選取]** 「覆蓋節點」。
1. 在&#x200B;**[!UICONTROL 覆蓋節點]**&#x200B;對話方塊中，按一下&#x200B;**[!UICONTROL 確定]**。

   ![覆蓋節點](assets/overlay-node-path.png)

1. 重新整理瀏覽器。 已選取覆蓋節點`/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`。
1. 在&#x200B;**[!UICONTROL Properties]**&#x200B;標籤中，以位元組為單位輸入適當的值，以將大小限制增大到所需的大小。 例如，要將大小限制增加到30 GB，請輸入`32212254720`值。

1. 在工具列中，按一下「全部儲存」。****
1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 在[!DNL Adobe Experience Manager] [!UICONTROL Web控制台包]頁面的表的「名稱」列下，找到並按一下&#x200B;**[!UICONTROL Adobe花崗岩工作流外部進程作業處理程式]**。
1. 在[!UICONTROL Adobe花崗岩工作流外部進程作業處理程式]頁面上，將&#x200B;**[!UICONTROL 預設超時]**&#x200B;和&#x200B;**[!UICONTROL 最大超時]**&#x200B;欄位的秒數設定為`18000`（5小時）。 按一下「**[!UICONTROL 儲存]**」。
1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 在「工作流模型」頁面上，選擇&#x200B;**[!UICONTROL Dynamic Media編碼視頻]** ，然後按一下&#x200B;**[!UICONTROL 編輯]**。
1. 在工作流頁面上，按兩下&#x200B;**[!UICONTROL Dynamic Media視頻服務進程]**&#x200B;元件。
1. 在「步 [!UICONTROL 驟屬性] 」對話框的「常用」頁籤下，展開「 **[!UICONTROL 高級設定」]******。
1. 在&#x200B;**[!UICONTROL Timeout]**&#x200B;欄位中，指定`18000`值，然後按一下&#x200B;**[!UICONTROL OK]**&#x200B;返回&#x200B;**[!UICONTROL Dynamic Media編碼視訊]**&#x200B;工作流程頁面。
1. 在頁面頂部的[!UICONTROL Dynamic Media編碼視頻]頁面標題下，按一下&#x200B;**[!UICONTROL 保存]**。

## 發佈視訊資產{#publish-video-assets}

發佈後，您可以將視訊資產加入網頁中做為URL，或直接內嵌資產。 如需詳細資訊，請參閱[發佈Dynamic Media資產](/help/assets/publishing-dynamicmedia-assets.md)。

## 註解視訊資產{#annotate-video-assets}

1. 在[!DNL Assets]主控台中，選取資產卡上的&#x200B;**[!UICONTROL 編輯]**&#x200B;以顯示資產詳細資訊頁面。
1. 若要播放視訊，請按一下「預覽」。****
1. 若要註解視訊，請按一下「**[!UICONTROL 註解]**」。 在視訊中的特定時間（畫格）加入註解。 在加上註解時，您可以在畫布上繪圖，並在繪圖中加入註解。 注釋會自動儲存。 要退出注釋嚮導，請按一下&#x200B;**[!UICONTROL 關閉]**。

   ![在視訊影格上繪圖和加上註解](assets/annotate-video.png)

1. 尋找視訊中的特定點，在&#x200B;**「文字」**&#x200B;欄位中指定時間 (以秒為單位)，然後按一下&#x200B;**「跳至」**。例如，若要略過前 20 秒的視訊，請在文字欄位中輸入 20。

   ![尋找視訊中要略過指定秒數的時間](assets/seek-in-video.png)

1. 要在時間軸中查看，請按一下注釋。 要從時間軸刪除注釋，請按一下&#x200B;**[!UICONTROL Delete]**。

   ![在時間軸中檢視註解和詳細資訊](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [在Experience Manager資產中管理數位資產](/help/assets/manage-assets.md)
>* [在Experience Manager資產中管理系列](/help/assets/manage-collections.md)
>* [Dynamic Media視訊檔案](/help/assets/video.md)。

