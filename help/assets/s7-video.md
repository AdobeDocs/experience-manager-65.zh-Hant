---
title: 影片
description: 了解集中式視訊資產管理AEM Assets，您可以在其中上傳視訊以自動編碼至Dynamic Media Classic，並直接從AEM Assets存取Dynamic Media Classic視訊。 Dynamic Media Classic視訊整合可將最佳化視訊的觸及範圍延伸至所有畫面。
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
role: Business Practitioner, Administrator
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: 影片
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 1%

---

# 影片 {#video}

Assets提供集中的視訊資產管理功能，您可以將視訊直接上傳至Assets，以自動編碼至Dynamic Media Classic，並直接從Assets存取Dynamic Media Classic視訊，以進行頁面編寫。

Dynamic Media Classic視訊整合將最佳化視訊的觸角延伸至所有畫面（自動裝置和頻寬偵測）。

* **[!UICONTROL Scene7視訊]**&#x200B;元件會自動執行裝置和頻寬偵測，以在桌上型電腦、平板電腦和行動裝置上播放適當的格式和適當品質的視訊。
* 資產 — 您可以包含最適化視訊集，而非僅包含單一視訊資產。 最適化視訊集是容器，可供在多個畫面間順暢播放視訊所需的所有視訊轉譯使用。 適用性視訊集將以不同位速率和格式（如400 kbps、800 kbps和1000 kbps）編碼的相同視訊的版本分組。 您可以使用最適化視訊集以及S7視訊元件，在多個畫面（包括桌上型電腦、iOS、Android、Blackberry和Windows行動裝置）間進行最適化視訊串流。
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## 關於FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

預設的視訊編碼程式是使用以FFMPEG為基礎的與視訊設定檔的整合為基礎。 因此，現成的DAM擷取工作流程包含以下兩個以ffmpeg為基礎的工作流程步驟：

* FFMPEG縮圖
* FFMPEG編碼

請注意，啟用和設定Dynamic Media Classic整合不會從現成的DAM擷取工作流程中自動移除或停用這兩個工作流程步驟。 如果您已在AEM中使用FFMPEG型視訊編碼，則您的製作環境很可能已安裝FFMPEG。 在此情況下，使用DAM擷取的新視訊會編碼兩次：一次來自FFMPEG編碼器，一次來自Dynamic Media Classic整合。

如果您已設定AEM中的FFMPEG型視訊編碼並安裝FFMPEG，則Adobe建議您從DAM擷取工作流程中移除兩個FFMPEG工作流程。

## 支援的格式 {#supported-formats}

Scene7視訊元件支援下列格式：

* F4V H.264
* MP4 H.264

## 決定要將視訊上傳到何處{#deciding-where-to-upload-your-video}

決定要將視訊資產上傳至何處取決於下列項目：

* 您是否需要視訊資產的工作流程？
* 您是否需要視訊資產的版本控制？

如果這兩個問題的答案皆為「是」，請直接將影片上傳至AdobeDAM。 如果兩個問題的答案都是「否」，請直接將影片上傳至Dynamic Media Classic。 以下章節將說明每個案例的工作流程。

### 如果您要直接將視訊上傳至AdobeDAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

如果您的資產需要工作流程或版本設定，應先上傳至AdobeDAM。 建議的工作流程如下：

1. 上傳視訊資產以AdobeDAM，並自動編碼並發佈至Dynamic Media Classic。
1. 在AEM中，在「內容尋找器」的&#x200B;**[!UICONTROL Movies]**&#x200B;標籤中存取WCM中的視訊資產。
1. 使用&#x200B;**[!UICONTROL Scene7 Video]**&#x200B;或&#x200B;**[!UICONTROL Foundation Video]**&#x200B;元件製作。

### 如果您要將視訊上傳至Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

如果您的資產不需要工作流程或版本設定，應將資產上傳至Scene7。 建議的工作流程如下：

1. 在Dynamic Media Classic中，[設定排程的FTP上傳和編碼至Scene7（系統自動化）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp)。
1. 在AEM中，在「內容尋找器」的&#x200B;**[!UICONTROL Scene7]**&#x200B;標籤中存取WCM中的視訊資產。
1. 使用&#x200B;**[!UICONTROL Scene7 Video]**&#x200B;元件製作。

## 設定與Scene7影片的整合{#configuring-integration-with-scene-video}

要配置通用預設集：

1. 在&#x200B;**[!UICONTROL Cloud Services]**&#x200B;中，導覽至您的&#x200B;**[!UICONTROL Scene7]**&#x200B;設定，然後按一下&#x200B;**[!UICONTROL 編輯]**。
1. 選擇&#x200B;**[!UICONTROL Video]**&#x200B;頁簽。

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >如果頁面沒有雲端設定，則不會顯示&#x200B;**[!UICONTROL Video]**&#x200B;標籤。

1. 選取最適化視訊編碼設定檔、現成可用的單一視訊編碼設定檔，或自訂視訊編碼設定檔。

   >[!NOTE]
   >
   >如需視訊預設集含義的詳細資訊，請參閱[Dynamic Media Classic檔案](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files)。
   >
   >Adobe建議您在設定通用預設集時同時選取兩個最適化視訊集，或選取&#x200B;**[!UICONTROL 最適化視訊編碼]**&#x200B;選項。

1. 選取的編碼設定檔會自動套用至您為此Scene7雲端設定所設定的CQ DAM目標資料夾中所上傳的所有視訊。 您可以使用不同的目標資料夾來設定多個Scene7雲端設定，以視需要套用不同的編碼設定檔。

## 更新查看器和編碼預設集{#updating-viewer-and-encoding-presets}

如果因為預設集已在Scene7中更新，而需要更新Experience Manager中視訊的檢視器和編碼預設集，請導覽至雲端設定中的Scene7設定，然後按一下「更新檢視器和編碼預設集」**[!UICONTROL 。]**

![chlimage_1-364](assets/chlimage_1-364.png)

## 從AdobeDAM {#uploading-your-master-video}上傳主要來源視訊至Scene7

1. 導覽至CQ DAM Target資料夾，您已在該資料夾中使用Scene7編碼設定檔設定雲端設定。
1. 按一下&#x200B;**[!UICONTROL Upload]**&#x200B;以上傳主要來源視訊。 視訊上傳和編碼在[!UICONTROL DAM更新資產]工作流程完成且&#x200B;**[!UICONTROL 發佈至Scene7]**&#x200B;有核取記號後完成。

   >[!NOTE]
   >
   >可能需要一些時間才能產生視訊縮圖。

   將DAM主要來源視訊拖曳至視訊元件時，會存取&#x200B;*所有* Scene7編碼的Proxy轉譯以供傳送。

## Foundation視訊元件與Scene7視訊元件{#foundation-video-component-versus-scene-video-component}

使用Experience Manager時，您可以同時存取Sites中可用的視訊元件和Scene7視訊元件。 這些元件不可互換。

Scene7視訊元件只適用於Scene7視訊。 基礎元件可處理從Experience Manager（使用ffmpeg）和Scene7影片儲存的影片。

下列矩陣說明何時應使用哪個元件：

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>S7視訊元件現成可使用通用視訊設定檔。 不過，您可以在Scene7中執行下列其中一項操作，以取得以HTML5為基礎的視訊播放器，供Experience Manager使用：複製現成可用HTML5視訊播放器的內嵌程式碼，並將其放入您的Experience Manager頁面。

## AEM視訊元件{#aem-video-component}

即使建議使用Scene7視訊元件來檢視Scene7視訊，為了完整起見，本節說明如何將Scene7視訊與Foundation視訊元件搭配Experience Manager使用。

### AEM視訊和Scene7視訊比較{#aem-video-and-scene-video-comparison}

下表提供AEM Foundation Video元件與Scene7 Video元件之間所支援功能的高階比較：

|  | AEM Foundation影片 | Scene7影片 |
|---|---|---|
| 方法 | HTML5的第一種方法。 Flash僅用於非HTML5後援。 | Flash在大多數案頭上。 HTML5用於行動裝置和平板電腦。 |
| 傳送 | 漸進式 | 最適化串流 |
| 追蹤 | 是 | 是 |
| 擴充性 | 是 | 否 |
| 行動視訊 | 是 | 是 |

### 設定{#setting-up}

#### 建立視訊設定檔{#creating-video-profiles}

系統會根據S7雲端設定中選取的S7編碼預設集來建立各種視訊編碼。 為了讓基礎視訊元件能夠加以使用，必須為選取的每個S7編碼預設集建立視訊設定檔。 這可讓視訊元件據以選取DAM轉譯。

>[!NOTE]
>
>必須啟動新視訊設定檔及其變更才能發佈。

1. 在AEM中，點選「**[!UICONTROL 工具]** > **[!UICONTROL 設定主控台]**」。
1. 在&#x200B;**[!UICONTROL Configuration Console]**&#x200B;導覽至導覽樹狀結構中的&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL DAM]** > **[!UICONTROL Video Profiles]**。
1. 建立新的S7視訊設定檔。 在&#x200B;**[!UICONTROL New]**&#x200B;中。 功能表，選取「建立頁面」，然後選取「Scene7視訊描述檔」範本。 ****&#x200B;為新視訊設定檔頁面命名，然後按一下「**[!UICONTROL 建立]**」。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 編輯新的視訊設定檔。 先選取雲端設定。 然後選取與雲端設定中選取的編碼預設集相同。

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | 屬性 | 說明 |
   |---|---|
   | Scene7 雲端設定 | 用於編碼預設集的雲端設定。 |
   | Scene7 編碼預設集 | 用來對應此視訊設定檔的編碼預設集。 |
   | HTML5 視訊類型 | 此屬性可設定HTML5視訊來源元素的type屬性值。 S7編碼預設集未提供此資訊，但使用HTML5視訊元素正確轉譯視訊時需要此資訊。 提供了常用格式的清單，但可以覆蓋其他格式。 |

   對您要在視訊元件中使用的雲端設定中選取的所有編碼預設集，重複此步驟。

#### 配置設計{#configuring-design}

**[!UICONTROL Foundation Video]**&#x200B;元件必須知道要使用哪些視訊設定檔，才能建立視訊來源清單。 您必須開啟視訊元件設計對話方塊，並使用新視訊設定檔來設定元件設計。

>[!NOTE]
>
>如果您在行動頁面上使用&#x200B;**[!UICONTROL Foundation Video]**&#x200B;元件，則可能需要在行動頁面的設計上重複這些步驟。

>[!NOTE]
>
>對設計所做的變更需要啟動設計，才能對發佈生效。

1. 開啟&#x200B;**[!UICONTROL Foundation Video]**&#x200B;元件的設計對話框，並更改為&#x200B;**[!UICONTROL Profiles]**&#x200B;頁簽。 然後刪除現成可用的設定檔，並新增新的S7視訊設定檔。 設計對話方塊中描述檔清單的順序會定義轉譯時視訊來源元素的順序。
1. 針對不支援HTML5的瀏覽器，視訊元件可讓設定Flash後援。 開啟視訊元件設計對話方塊，並變更為&#x200B;**[!UICONTROL Flash]**&#x200B;標籤。 配置Flash播放器設定，並為Flash播放器指派後援設定檔。

#### 檢查清單 {#checklist}

1. 建立S7雲端設定。 請確定已設定視訊編碼預設集且匯入工具正在執行。
1. 為雲端設定中選取的每個視訊編碼預設集建立S7視訊設定檔。
1. 必須啟動視訊設定檔。
1. 在頁面上配置&#x200B;**[!UICONTROL 基礎視訊]**&#x200B;元件的設計。
1. 完成設計變更後，啟動設計。
