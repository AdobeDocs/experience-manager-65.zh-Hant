---
title: 影片
description: 瞭解集中式視訊資產管理Adobe Experience Manager Assets ，您可上傳視訊以自動編碼至Dynamic Media Classic，並直接從Experience Manager Assets存取Dynamic Media Classic視訊。 Dynamic Media Classic視訊整合可將最佳化的視訊延伸至所有熒幕。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
role: User, Admin
mini-toc-levels: 3
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: Video
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1551'
ht-degree: 2%

---

# 影片 {#video}

Adobe Experience Manager Assets提供集中式視訊資產管理，讓您可以直接將視訊上傳至Assets，以自動編碼至Dynamic Media Classic，並直接從Assets存取Dynamic Media Classic視訊以進行頁面製作。

Dynamic Media Classic視訊整合將最佳化視訊的範圍延伸至所有熒幕（自動裝置和頻寬偵測）。

* 此 **[!UICONTROL Scene7影片]** 元件會自動執行裝置和頻寬偵測，以在桌上型電腦、平板電腦和行動裝置上播放正確格式和正確品質的視訊。
* 資產 — 您可以包含最適化視訊集，而非單一視訊資產。 最適化視訊集包含流暢在多個熒幕播放視訊所需的所有視訊轉譯。 「最適化視訊集」會將使用不同位元速率和格式（例如400 kbps、800 kbps和1000 kbps）編碼的相同視訊版本分組。 您可使用最適化視訊集和S7視訊元件，在多個熒幕(包括桌上型電腦、iOS、Android™、BlackBerry®和Windows行動裝置)上執行最適化視訊串流。
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## 關於FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

預設的視訊編碼程式是以FFMPEG型整合與視訊設定檔整合為基礎。 因此，現成可用的DAM Ingestion工作流程包含下列兩個ffmpeg型工作流程步驟：

* FFMPEG縮圖
* FFMPEG編碼

啟用和設定Dynamic Media Classic整合不會自動從現成的DAM Ingestion工作流程中移除或停用這兩個工作流程步驟。 如果您在Adobe Experience Manager中已經使用FFMPEG型視訊編碼，則您的編寫環境很可能已安裝FFMPEG。 在此情況下，使用DAM擷取的新視訊會編碼兩次：一次來自FFMPEG編碼器，另一次來自Dynamic Media Classic整合。

如果您已設定Experience Manager的FFMPEG型視訊編碼並安裝FFMPEG，Adobe建議您從DAM擷取工作流程中移除兩個FFMPEG工作流程。

## 支援的格式 {#supported-formats}

Scene7視訊元件支援下列格式：

* F4V H.264
* MP4 H.264

## 決定上傳視訊的位置 {#deciding-where-to-upload-your-video}

要決定上傳視訊資產的位置，須視下列專案而定：

* 您是否需要視訊資產的工作流程？
* 您是否需要視訊資產的版本控制？

如果答案為是或兩個問題的其中一個「是」，則直接將您的影片上傳到AdobeDAM。 如果這兩個問題的答案都為「否」，則直接將您的影片上傳到Dynamic Media Classic。 下節將說明每個案例的工作流程。

### 如果您要將影片直接上傳到Adobe DAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

如果您需要資產的工作流程或版本設定，請先上傳至AdobeDAM。 以下是建議的工作流程：

1. 上傳視訊資產至AdobeDAM並自動編碼和發佈至Dynamic Media Classic。
1. 在Experience Manager中，存取位於WCM中的視訊資產 **[!UICONTROL 影片]** 「內容尋找器」的標籤。
1. 作者與 **[!UICONTROL Scene7影片]** 或 **[!UICONTROL Foundation影片]** 元件。

### 如果您要將影片上傳至Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

如果您不需要資產的工作流程或版本設定，請將資產上傳至Scene7。 以下是建議的工作流程：

1. 在Dynamic Media Classic中， [設定已排程的FTP上傳和編碼至Scene7 （系統自動化）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp).
1. 在Experience Manager中，存取位於WCM中的視訊資產 **[!UICONTROL Scene7]** 「內容尋找器」的標籤。
1. 使用進行創作 **[!UICONTROL Scene7影片]** 元件。

## 設定與Scene7影片整合 {#configuring-integration-with-scene-video}

1. 在 **[!UICONTROL Cloud Service]**，導覽至 **[!UICONTROL Scene7]** 設定並選取 **[!UICONTROL 編輯]**.
1. 選取 **[!UICONTROL 視訊]** 標籤。

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >此 **[!UICONTROL 視訊]** 如果頁面沒有雲端設定，索引標籤不會顯示。

1. 選取最適化視訊編碼設定檔、現成可用的單一視訊編碼設定檔，或自訂視訊編碼設定檔。

   >[!NOTE]
   >
   >如需視訊預設集含義的詳細資訊，請參閱 [Dynamic Media Classic檔案](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe建議您在設定通用預設集時，選取兩個最適化視訊集，或選取 **[!UICONTROL 自我調整視訊編碼]** 選項。

1. 選取的編碼設定檔會自動套用至上傳至您為此Scene7雲端設定所設定CQ DAM目標資料夾的所有影片。 您可以使用不同的目標資料夾來設定多個Scene7雲端設定，以視需要套用不同的編碼設定檔。

## 更新檢視器和編碼預設集 {#updating-viewer-and-encoding-presets}

若要更新視訊的檢視器和編碼預設集，因為這些預設集已在Scene7中更新，請導覽至「雲端設定」中的Scene7設定，然後選取「 」 **[!UICONTROL 更新檢視器和編碼預設集]**.

![chlimage_1-364](assets/chlimage_1-364.png)

## 從AdobeDAM將主要來源影片上傳至Scene7 {#uploading-your-master-video}

1. 導覽至CQ DAM目標資料夾，您已在該資料夾中使用Scene7編碼設定檔設定您的雲端設定。
1. 選取 **[!UICONTROL 上傳]** 上傳主要來源視訊。 影片上傳和編碼於以下時間後完成： [!UICONTROL DAM更新資產] 工作流程已完成，且 **[!UICONTROL 發佈至Scene7]** 有核取記號。

   >[!NOTE]
   >
   >產生視訊縮圖需要一點時間。

   將DAM主要來源視訊拖曳至視訊元件存取 *全部* Scene7編碼的Proxy轉譯以進行傳送。

## Foundation視訊元件與Scene7視訊元件 {#foundation-video-component-versus-scene-video-component}

使用Experience Manager時，您可以同時存取Sites中可用的視訊元件和Scene7視訊元件。 這些元件不可互換。

Scene7視訊元件僅適用於Scene7視訊。 基礎元件可處理從Experience Manager （使用ffmpeg）儲存的視訊和Scene7視訊。

下列矩陣說明何時使用哪個元件：

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>S7視訊元件可立即使用通用視訊設定檔。 不過，您可以取得供Experience Manager使用的HTML5型影片播放程式。 在Scene7中，複製現成可用HTML5視訊播放器的內嵌程式碼，並將其放入您的Experience Manager頁面中。

## Experience Manager視訊元件 {#aem-video-component}

即使檢視Scene7影片時建議使用Scene7影片元件，本節也說明如何在Experience Manager中將Scene7影片與Foundation影片元件搭配使用，以達完整目的。

### Experience Manager影片和Scene7影片比較 {#aem-video-and-scene-video-comparison}

下表提供Experience Manager Foundation視訊元件和Scene7視訊元件之間支援功能的高階比較：

|   | Experience Manager Foundation影片 | Scene7影片 |
|---|---|---|
| 方針 | HTML5優先方法。 Flash僅用於非HTML5遞補。 | 在大部分的桌上型電腦上Flash。 HTML5適用於行動裝置和平板電腦。 |
| 傳遞 | 漸進式 | 最適化串流 |
| 追蹤 | 是 | 是 |
| 擴充性 | 是 | 否 |
| 行動視訊 | 是 | 是 |

### 設定 {#setting-up}

#### 建立視訊設定檔 {#creating-video-profiles}

根據S7雲端設定中選取的S7編碼預設集建立各種視訊編碼。 為了讓foundation視訊元件能夠使用這些視訊元件，必須為選取的每個S7編碼預設集建立視訊設定檔。 此方法可讓視訊元件據以選取DAM轉譯。

>[!NOTE]
>
>新視訊設定檔及其變更必須啟動才能發佈。

1. 在Experience Manager中選取 **[!UICONTROL 工具]** > **[!UICONTROL 設定主控台]**.
1. 在 **[!UICONTROL 設定主控台]**，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL DAM]** > **[!UICONTROL 視訊設定檔]** 在導覽樹狀結構中。
1. 建立S7視訊設定檔。 在 **[!UICONTROL 新增]**. 功能表，選取 **[!UICONTROL 建立頁面]** 然後選取Scene7視訊設定檔範本。 為新的視訊設定檔頁面命名，然後選取 **[!UICONTROL 建立]**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 編輯新的視訊設定檔。 請先選取雲端設定。 接著，選取在雲端設定中選取的相同編碼預設集。

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | 屬性 | 說明 |
   |---|---|
   | Scene7 雲端設定 | 用於編碼預設集的雲端設定。 |
   | Scene7 編碼預設集 | 對應此視訊設定檔的編碼預設集。 |
   | HTML5 視訊類型 | 此屬性可讓您設定HTML5視訊來源元素的type屬性值。 S7編碼預設集不提供這項資訊，但使用HTML5視訊元素正確轉譯視訊時需要此資訊。 提供常見格式的清單，但其他格式可以覆寫。 |

   對雲端設定中選取要用於視訊元件的所有編碼預設集重複此步驟。

#### 設定設計 {#configuring-design}

此 **[!UICONTROL Foundation影片]** 元件必須知道要使用哪些視訊設定檔來建立視訊來源清單。 開啟視訊元件設計對話方塊，並使用新的視訊設定檔來設定元件設計。

>[!NOTE]
>
>如果您使用 **[!UICONTROL Foundation影片]** 元件時，請在行動頁面的設計上重複這些步驟。

>[!NOTE]
>
>對設計所做的變更需要啟動設計才能在發佈時生效。

1. 開啟 **[!UICONTROL Foundation影片]** 元件的「設計」對話方塊並變更為 **[!UICONTROL 設定檔]** 標籤。 然後刪除現成的設定檔，並新增新的S7視訊設定檔。 在「設計」對話方塊中，設定檔清單的順序會定義視訊來源元素在彩現時的順序。
1. 對於不支援HTML5的瀏覽器，視訊元件可讓您設定Flash遞補。 開啟視訊元件設計對話方塊，並變更為 **[!UICONTROL Flash]** 標籤。 設定Flash播放器設定，並指派Flash播放器的遞補設定檔。

#### 檢查清單 {#checklist}

1. 建立S7雲端設定。 請確定已設定視訊編碼預設集，且匯入工具在執行中。
1. 針對在雲端設定中選取的每個視訊編碼預設集，建立S7視訊設定檔。
1. 必須啟動視訊設定檔。
1. 設定設計 **[!UICONTROL Foundation影片]** 元件時。
1. 完成設計變更後啟動設計。
