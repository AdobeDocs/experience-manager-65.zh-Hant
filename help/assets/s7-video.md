---
title: 視訊
description: 瞭解集中式視訊資產管理AEM Assets，您可在其中上傳視訊以自動編碼至Dynamic Media Classic，並直接從AEM Assets存取Dynamic Media Classic視訊。 Dynamic Media Classic視訊整合將最佳化視訊的觸及面延伸到所有螢幕。
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Video {#video}

Assets提供集中式視訊資產管理，您可以直接將視訊上傳至Assets，以便自動編碼至Dynamic Media Classic(Scene7)，並直接從Assets存取Dynamic Media Classic視訊，以進行頁面製作。

Dynamic Media Classic視訊整合將最佳化視訊的觸及面延伸到所有螢幕（自動裝置和頻寬偵測）。

* Scene7 Video **[!UICONTROL (]** Scene7視訊)元件會自動執行裝置和頻寬偵測，以在桌上型電腦、平板電腦和行動裝置上播放正確格式和正確品質的視訊。
* 資產——您可以包含可調式視訊集，而不只包含單一視訊資產。 最適化視訊集是所有必要視訊轉譯的容器，可在多種螢幕上順暢播放視訊。 「最適化視訊集」會針對以不同位元速率和格式（例如400 kbps、800 kbps和1000 kbps）編碼的相同視訊版本分組。 您使用Adaptive Video Set和S7視訊元件，在多種螢幕上（包括桌上型電腦、iOS、Android、Blackberry和Windows行動裝置）進行最適化視訊串流。 如需詳 [細資訊，請參閱Scene7檔案中有關最適化視訊集的說明](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html)。

## 關於FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

預設的視訊編碼程式是以使用FFMPEG與視訊設定檔整合為基礎。 因此，現成可用的DAM擷取工作流程包含下列兩個ffmpeg工作流程步驟：

* FFMPEG縮圖
* FFMPEG編碼

請注意，啟用和設定Dynamic Media Classic整合併不會從現成可用的DAM擷取工作流程自動移除或停用這兩個工作流程步驟。 如果您已在AEM中使用以FFMPEG為基礎的視訊編碼，則您可能已在製作環境中安裝FFMPEG。 在此例中，使用DAM擷取的新視訊會編碼兩次：一次是從FFMPEG編碼器，一次是從Dynamic Media Classic整合。

如果您已在AEM中設定FFMPEG視訊編碼並安裝FFMPEG,Adobe建議您從DAM擷取工作流程中移除兩個FFMPEG工作流程。

## 支援的格式 {#supported-formats}

Scene7 Video元件支援下列格式：

* F4V H.264
* MP4 H.264

## 決定要將視訊上傳到何處 {#deciding-where-to-upload-your-video}

決定上傳視訊資產的位置取決於下列項目：

* 您需要視訊資產的工作流程嗎？
* 您是否需要視訊資產的版本控制？

如果對上述任一問題或兩個問題都回答「是」，則直接將視訊上傳至Adobe DAM。 如果這兩個問題的答案都是「否」，則直接將視訊上傳至Dynamic Media Classic。 下節將說明每個藍本的工作流程。

### 如果您要直接將視訊上傳至Adobe DAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

如果您需要資產的工作流程或版本修訂，應先上傳至Adobe DAM。 建議的工作流程如下：

1. 將視訊資產上傳至Adobe DAM，並自動編碼和發佈至Dynamic Media Classic。
1. 在AEM中，在「內容搜尋器」的「影片」索引標籤中， **[!UICONTROL 存取]** WCM中的視訊資產。
1. 使用 **[!UICONTROL Scene7 Video]** 或 **[!UICONTROL Foundation Video元件製作]** 。

### 如果您要將視訊上傳至Scene7 {#if-you-are-uploading-your-video-to-scene}

如果您不需要資產的工作流程或版本修訂，則應將資產上傳至Scene7。 建議的工作流程如下：

1. 在Dynamic Media Classic中， [設定排程的FTP上傳和編碼至Scene7（系統自動化）](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html)。
1. 在AEM中，在「內容搜尋器」的「 **[!UICONTROL Scene7]** 」標籤中存取WCM中的視訊資產。
1. 使用 **[!UICONTROL Scene7 Video元件製作]** 。

## 設定與Scene7視訊的整合 {#configuring-integration-with-scene-video}

若要設定通用預設集：

1. 在 **[!UICONTROL Cloud Services]**，導覽至您的 **[!UICONTROL Scene7設定，然後按一下「]** 編輯 ****」。
1. 選擇「 **[!UICONTROL Video]** 」標籤。

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >如 **[!UICONTROL 果頁面沒有雲端設定]** ,「視訊」索引標籤就不會出現。

1. 選擇最適化視訊編碼設定檔、現成可用的單一視訊編碼設定檔或自訂視訊編碼設定檔。

   >[!NOTE]
   >
   >如需視訊預設集的詳細資訊，請參閱 [Dynamic Media Classic檔案](https://help.adobe.com/en_US/scene7/using/WSE86ACF2B-BD50-4c48-A1D7-9CD4405B62D0.html)。
   >
   >Adobe建議您在設定通用預設集時同時選取兩個最適化視訊集，或選取「最適化視訊編 **[!UICONTROL 碼」選項]** 。

1. 選取的編碼設定檔會自動套用至您為此Scene7雲端設定所設定之CQ DAM目標資料夾上傳的所有視訊。 您可以設定多個Scene7雲端設定，並使用不同的目標資料夾，以視需要套用不同的編碼設定檔。

## Updating viewer and encoding presets {#updating-viewer-and-encoding-presets}

如果您因為Scene7中的預設集已更新，所以需要更新AEM中視訊的檢視器和編碼預設集，請導覽至雲端設定中的Scene7設定，然後按一下「 **[!UICONTROL Update the viewer and encoding presets]**」。

![chlimage_1-364](assets/chlimage_1-364.png)

## 從Adobe DAM將您的主影片上傳至Scene7 {#uploading-your-master-video}

1. 導覽至您已使用Scene7編碼設定檔設定雲端設定的CQ DAM目標檔案夾。
1. 按一 **[!UICONTROL 下「上傳]** 」以上傳主影片。 視訊上傳和編碼在DAM更新資產工作流程完成後完成，而 **[!UICONTROL 「發佈至Scene7]** 」有核取標籤。

   >[!NOTE]
   >
   >產生視訊縮圖可能需要一些時間。

   將DAM主視訊拖曳至視訊元件時，會存取 *所有* Scene7編碼的Proxy轉譯以進行傳送。

## Foundation Video元件與Scene7 video元件 {#foundation-video-component-versus-scene-video-component}

使用AEM時，您可以存取Sites中可用的視訊元件和Scene7視訊元件。 這些元件不能互換。

Scene7視訊元件僅適用於Scene7視訊。 基礎元件可處理從AEM（使用ffmpeg）和Scene7視訊儲存的視訊。

下列矩陣說明何時應使用哪個元件：

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>S7視訊元件現成可用，使用通用視訊設定檔。 不過，您可以在Scene7中執行下列其中一項作業，取得AEM使用的HTML5視訊播放器：複製現成可用的HTML5視訊播放程式的內嵌程式碼，並將它放入您的AEM頁面。

## AEM Video元件 {#aem-video-component}

即使建議使用Scene7視訊元件來檢視Scene7視訊，為了完整起見，本節將說明如何搭配AEM中的Foundation Video元件使用Scene7視訊。

### AEM Video與Scene7 Video比較 {#aem-video-and-scene-video-comparison}

下表提供AEM Foundation video元件與Scene7 video元件之間支援功能的高階比較：

|  | AEM Foundation影片 | Scene7視訊 |
|---|---|---|
| 方法 | HTML5的第一種方式。 Flash僅用於非HTML5後援。 | 大部份的桌上型電腦都可使用Flash。 HTML5適用於行動裝置和平板電腦。 |
| 傳送 | 漸進式 | 最適化串流 |
| 追蹤 | 是 | 是 |
| 擴充性 | 是 | 是（使用Scene7檢視器SDK） |
| 行動視訊 | 是 | 是 |

### 設定 {#setting-up}

#### 建立視訊設定檔 {#creating-video-profiles}

根據S7雲端設定中選取的S7編碼預設集，建立各種視訊編碼。 為了讓基礎視訊元件能夠使用它們，必須為每個選取的S7編碼預設集建立視訊描述檔。 這可讓視訊元件依此選擇DAM轉譯。

>[!NOTE]
>
>必須啟動新視訊設定檔及對其所做的變更才能發佈。

1. 在AEM中，點選 **[!UICONTROL工具>設定控制台**。
1. 在「設 **[!UICONTROL 定控制台]** 」中，導 **[!UICONTROL 覽至導覽樹中的「工具> DAM >視訊描述檔]** 」。
1. 建立新的S7視訊設定檔。 **[!UICONTROL 在新]**...功能表中，選 **[!UICONTROL 取「建立頁面]** 」，然後選取「Scene7視訊描述檔」範本。 為新視訊描述檔頁面指定名稱，然後按一下「 **[!UICONTROL 建立]**」。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 編輯新視訊設定檔。 先選取雲端設定。 然後選取與雲端設定中選取的編碼預設集相同。

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | 屬性 | 說明 |
   |---|---|
   | Scene7 雲端設定 | 用於編碼預設集的雲端設定。 |
   | Scene7 編碼預設集 | 用來映射此視訊描述檔的編碼預設集。 |
   | HTML5 視訊類型 | 此屬性可讓您設定HTML5視訊來源元素的type屬性值。 S7編碼預設集不提供這項資訊，但是使用HTML5視訊元素正確轉譯視訊時，需要此項資訊。 提供常用格式的清單，但可以覆寫其它格式。 |

   對您要在視訊元件中使用的雲端設定中選取的所有編碼預設集，重複此步驟。

#### 設定設計 {#configuring-design}

Foundation Video **** component必須知道要使用哪些視訊描述檔才能建立視訊來源清單。 您必須開啟視訊元件設計對話方塊，並設定元件設計以使用新的視訊設定檔。

>[!NOTE]
>
>如果您在行動 **[!UICONTROL 頁面上使用Foundation Video]** （基礎視訊）元件，您可能需要在行動頁面的設計上重複這些步驟。

>[!NOTE]
>
>對設計所做的變更需要啟動設計，才能在發佈時生效。

1. 開啟 **[!UICONTROL Foundation Video]** （基礎視訊）元件的設計對話方塊，並變更至「描述檔 **** 」標籤。 然後刪除現成可用的設定檔，並新增S7視訊設定檔。 設計對話框中配置檔案清單的順序定義了渲染時視頻源元素的順序。
1. 對於不支援HTML5的瀏覽器，視訊元件可讓您設定Flash備援。 開啟視訊元件設計對話方塊，並變更至 **[!UICONTROL Flash]** 標籤。 設定Flash Player設定，並指派Flash Player的備援設定檔。

#### 檢查清單 {#checklist}

1. 建立S7雲端設定。 請確定已設定視訊編碼預設集，且匯入工具正在執行。
1. 為雲端設定中選取的每個視訊編碼預設集建立S7視訊設定檔。
1. 必須啟動視訊描述檔。
1. 在您的頁面上設 **[!UICONTROL 定基礎視訊]** 元件的設計。
1. 在完成設計變更後啟動設計。

