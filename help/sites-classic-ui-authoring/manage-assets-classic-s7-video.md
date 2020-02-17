---
title: 視訊
seo-title: 視訊
description: Assets提供集中式視訊資產管理，您可以直接將視訊上傳至Assets，以便自動編碼至Scene7，並直接從Assets存取Scene7視訊，以進行頁面製作。
seo-description: Assets提供集中式視訊資產管理，您可以直接將視訊上傳至Assets，以便自動編碼至Scene7，並直接從Assets存取Scene7視訊，以進行頁面製作。
uuid: 46da7a0d-d17b-4716-a304-ce5496421b5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Video{#video}

Assets提供集中式視訊資產管理，您可以直接將視訊上傳至Assets，以便自動編碼至Dynamic Media Classic，並直接從Assets存取Dynamic Media Classic視訊，以進行頁面製作。

Dynamic Media Classic視訊整合將最佳化視訊的觸及面延伸到所有螢幕（自動裝置和頻寬偵測）。

* Dynamic Media Classic(Scene7)視訊元件會自動執行裝置和頻寬偵測，以在桌上型電腦、平板電腦和行動裝置上播放正確格式和適當品質的視訊。
* 資產——您可以包含可調式視訊集，而不只包含單一視訊資產。 最適化視訊集是所有必要視訊轉譯的容器，可在多種螢幕上順暢播放視訊。 「最適化視訊集」會針對以不同位元速率和格式（例如400 kbps、800 kbps和1000 kbps）編碼的相同視訊版本分組。 您使用Adaptive Video Set和S7視訊元件，在多種螢幕上（包括桌上型電腦、iOS、Android、Blackberry和Windows行動裝置）進行最適化視訊串流。 如需詳 [細資訊，請參閱Scene7檔案中有關最適化視訊集的說明](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html)。

## 關於FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

預設的視訊編碼程式是以使用FFMPEG與視訊設定檔整合為基礎。 因此，現成可用的DAM更新資產工作流程包含下列兩個ffmpeg工作流程步驟：

* FFMPEG縮圖
* FFMPEG編碼

請注意，啟用和設定Dynamic Media Classic整合併不會從現成可用的DAM更新資產擷取工作流程自動移除或停用這兩個工作流程步驟。 如果您已在AEM中使用以FFMPEG為基礎的視訊編碼，則您可能已在製作環境中安裝FFMPEG。 在此例中，使用「資產」收錄的新視訊會編碼兩次：一次是從FFMPEG編碼器，一次是從Dynamic Media Classic整合。

如果您已在AEM中設定FFMPEG視訊編碼並安裝FFMPEG,Adobe建議您從DAM更新資產工作流程中移除兩個FFMPEG工作流程。

### 支援的格式 {#supported-formats}

Dynamic Media Classic視訊元件支援下列格式：

* F4V H.264
* MP4 H.264

### 決定要將視訊上傳到何處 {#deciding-where-to-upload-your-video}

決定上傳視訊資產的位置取決於下列項目：

* 您需要視訊資產的工作流程嗎？
* 您是否需要視訊資產的版本控制？

如果對上述兩種問題的答案皆為「是」，則直接將視訊上傳至Adobe DAM。 如果這兩個問題的答案都是「否」，則直接將視訊上傳至Dynamic Media Classic。 下節將說明每個藍本的工作流程。

#### 如果您要直接將視訊上傳至Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

如果您需要資產的工作流程或版本修訂，您應先上傳至Adobe Assets。 建議的工作流程如下：

1. 將視訊資產上傳至Adobe Assets，並自動編碼及發佈至Dynamic Media Classic。
1. 在AEM中，在「內容搜尋器」的「影片」索引標籤中， **[!UICONTROL 存取]** WCM中的視訊資產。
1. 使用Dynamic Media Classic視訊或基礎視訊元件製作。

#### 如果您要將視訊上傳至Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

如果您不需要資產的工作流程或版本修訂，則應將資產上傳至Dynamic Media Classic。 建議的工作流程如下：

1. 在Dynamic Media Classic中， [設定排程的FTP上傳和編碼至Dynamic Media Classic（系統自動化）](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html)。
1. 在AEM中，在「內容搜尋器」的「動態媒體經典」標籤 **[!UICONTROL 中存取WCM中的視訊資產]** 。
1. 使用Dynamic Media Classic視訊元件製作。

### 設定與Dynamic Media Classic視訊的整合 {#configuring-integration-with-scene-video}

**要配置通用預設集**:

1. 在 **[!UICONTROL Cloud Services]**，導覽至您的 **[!UICONTROL Dynamic Media Classic設定，然後按一下「]** 編輯 ****」。
1. 選擇「 **[!UICONTROL Video]** 」標籤。

   >[!NOTE]
   >
   >如 **[!UICONTROL 果頁面沒有雲端設定]** ,「視訊」索引標籤就不會出現。 請參 [閱啟用WCM的Dynamic Media Classic](#enablingscene7forwcm)。

1. 選擇最適化視訊編碼設定檔、現成可用的單一視訊編碼設定檔或自訂視訊編碼設定檔。

   >[!NOTE]
   >
   >如需視訊預設集的詳細資訊，請參閱 [Dynamic Media Classic檔案](https://help.adobe.com/en_US/scene7/using/WSE86ACF2B-BD50-4c48-A1D7-9CD4405B62D0.html)。
   >
   >Adobe建議您在設定通用預設集時同時選取兩個最適化視訊集，或選取「最適化視訊編 **[!UICONTROL 碼」選項]** 。

1. 選取的編碼設定檔會自動套用至您為此Dynamic Media Classic雲端設定所設定之CQ DAM目標資料夾上傳的所有視訊。 您可以設定多個Dynamic Media Classic雲端組態，並使用不同的目標資料夾，以視需要套用不同的編碼設定檔。

### Updating viewer and encoding presets {#updating-viewer-and-encoding-presets}

如果您因為Dynamic Media Classic中的預設集已更新，所以需要更新AEM中視訊的檢視器和編碼預設集，請導覽至雲端設定中的Dynamic Media Classic設定，然後按一下「 **Update the viewer and encoding presets**」。

![chlimage_1-131](assets/chlimage_1-131.png)

### 上傳您的主影片 {#uploading-your-master-video}

若要從Adobe DAM將您的主影片上傳至Dynamic Media Classic:

1. 導覽至CQ DAM目標資料夾，您已在該資料夾中使用Dynamic Media Classic編碼設定檔設定雲端設定。
1. 按一 **[!UICONTROL 下「上傳]** 」以上傳主影片。 視訊上傳和編碼在 [!UICONTROL DAM Update Asset] ( **[!UICONTROL DAM更新資產)工作流程完成後完成，]** 「發佈至動態媒體經典(Publish to Dynamic Media Classic)」有核取標籤。

   >[!NOTE]
   >
   >產生視訊縮圖可能需要一些時間。

   將DAM主視訊拖曳至視訊元件時，會存 *取所有* Dynamic Media Classic編碼的Proxy轉譯以進行傳送。

### Foundation Video元件與Dynamic Media Classic video元件 {#foundation-video-component-versus-scene-video-component}

使用AEM時，您可以存取Sites中的Video元件和Dynamic Media Classic(Scene7)視訊元件。 這些元件不能互換。

Dynamic Media Classic視訊元件僅適用於Dynamic Media Classic視訊。 基礎元件可處理從AEM（使用ffmpeg）和Dynamic Media Classic視訊儲存的視訊。

下列矩陣說明何時應使用哪個元件：

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Dynamic Media Classic視訊元件立即可用，使用通用視訊設定檔。 不過，您可以取得AEM使用的HTML5視訊播放器。 在Dynamic Media Classic中，複製現成可用的HTML5視訊播放器的內嵌程式碼，並將它放在您的AEM頁面中。


## AEM Video元件 {#aem-video-component}

即使建議使用Dynamic Media Classic視訊元件來檢視Dynamic Media Classic視訊，本節也會說明在AEM中搭配 [!UICONTROL Foundation Video Component] ，以取得完整性。

### AEM video與Dynamic Media Classic video比較 {#aem-video-and-scene-video-comparison}

下表提供AEM Foundation video元件與Scene7 video元件之間支援功能的高階比較：

|  | AEM Foundation影片 | Dynamic Media Classic視訊 |
|---|---|---|
| 方法 | HTML5的第一種方式。 Flash僅用於非HTML5後援。 | 大部份的桌上型電腦都可使用Flash。 HTML5適用於行動裝置和平板電腦。 |
| 傳送 | 漸進式 | 最適化串流 |
| 追蹤 | 是 | 是 |
| 擴充性 | 是 | 是（使用Dynamic Media Classic檢視器SDK） |
| 行動視訊 | 是 | 是 |

### 設定 {#setting-up}

#### 建立視訊設定檔 {#creating-video-profiles}

視訊編碼是根據Dynamic Media Classic雲端設定中選取的Dynamic Media Classic編碼預設集建立。 為了讓基礎視訊元件能夠使用它們，必須為每個選取的動態媒體經典編碼預設集建立視訊描述檔。 這可讓視訊元件依此選擇DAM轉譯。

>[!NOTE]
>
>必須啟動新視訊設定檔及對其所做的變更才能發佈。

1. 在AEM中，前往「工 **[!UICONTROL 具]**」，然後選 **[!UICONTROL 取「設定控制台」]**。 在設定控制台中，導覽至導 **[!UICONTROL 覽樹狀]** 結構中的 **[!UICONTROL 「工具]** >資 **[!UICONTROL 產]** >視訊描述檔」。
1. 建立新的Dynamic Media Classic視訊設定檔。 **[!UICONTROL 在新]**...菜單，選 **[!UICONTROL 擇「建立頁面]** 」，然後選擇「動態媒體經典視頻配置檔案」模板。 為新視訊描述檔頁面指定名稱，然後按一下「 **[!UICONTROL 建立]**」。

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. 編輯新視訊設定檔。 先選取雲端設定。 然後選取與雲端設定中選取的編碼預設集相同。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | 屬性 | 說明 |
   |---|---|
   | Dynamic Media Classic(Scene7)雲端設定 | 用於編碼預設集的雲端設定。 |
   | Dynamic Media Classic(Scene7)編碼預設集 | 用來映射此視訊描述檔的編碼預設集。 |
   | HTML5 視訊類型 | 此屬性可讓您設定HTML5視訊來源元素的type屬性值。 Dynamic Media Classic編碼預設集不提供這項資訊，但是使用HTML5視訊元素正確轉譯視訊時，需要此項資訊。 提供常用格式的清單，但可以覆寫其它格式。 |

   對您要在視訊元件中使用的雲端設定中選取的所有編碼預設集，重複此步驟。

#### 設定設計 {#configuring-design}

基礎視訊元件必須知道要使用哪些視訊描述檔才能建立視訊來源清單。 您必須開啟視訊元件設計對話方塊，並設定元件設計以使用新的視訊設定檔。

>[!NOTE]
>
>如果您在行動頁面上使用基礎視訊元件，您可能需要在行動頁面的設計上重複這些步驟。

>[!NOTE]
>
>對設計所做的變更需要啟動設計，才能在發佈時生效。

1. 開啟基礎視訊元件的設計對話方塊，並變更至「描述檔 **[!UICONTROL 」標籤]** 。 然後刪除現成可用的描述檔，並新增新的Dynamic Media Classic視訊描述檔。 設計對話方塊中描述檔清單的順序，也會定義在轉換時視訊來源元素的順序。
1. 對於不支援HTML5的瀏覽器，視訊元件可讓您設定flash備援。 開啟視訊元件設計對話方塊，並變更 **[!UICONTROL 至Flash]** 標籤。 設定Flash Player設定，並指派Flash Player的備援設定檔。

#### 檢查清單 {#checklist}

1. 建立Dynamic Media Classic(Scene7)雲端設定。 請確定已設定視訊編碼預設集，且匯入工具正在執行。
1. 為雲端設定中選取的每個視訊編碼預設集建立Dynamic Media Classic視訊設定檔。
1. 必須啟動視訊描述檔。
1. 在您的頁面上設定基礎視訊元件的設計。
1. 在完成設計變更後啟動設計。

