---
title: 站點中的視頻經典創作
description: 資產提供集中的視頻資產管理，您可以將視頻直接上傳到資產，以便自動編碼到Dynamic Media Classic，並直接從資產訪問Dy視頻，以進行頁面創作。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: 59e182c165f6fd4b822eaf0e34f6e4b3bb18eb14
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 1%

---

# 影片{#video}

資產提供集中的視頻資產管理，您可以將視頻直接上傳到資產中，以便自動編碼到Dynamic Media Classic，並直接從資產中訪問Dynamic Media Classic視頻以進行頁面創作。

Dynamic Media Classic視頻整合將優化視頻的覆蓋範圍擴展到所有螢幕（自動設備和頻寬檢測）。

* Dynamic Media Classic視頻元件自動執行設備和頻寬檢測，以在案頭、平板電腦和移動設備上播放正確的格式和質量的視頻。
* 資產 — 您可以包括自適應視頻集，而不是僅包括單個視頻資產。 自適應視頻集是所有視頻格式副本的容器，這些格式副本需要跨多個螢幕無縫地回放視頻。 自適應視頻集將以不同比特率和格式（如400 kbps、800 kbps和1000 kbps）編碼的同一視頻的版本分組。 您可以使用自適應視頻集和S7視頻元件，在多個螢幕(包括案頭、iOS、Android™、BlackBerry®和Windows移動設備)上進行自適應視頻流傳輸。 請參閱 [Dynamic Media Classic文檔關於自適應視頻集的詳細資訊](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video)。

## 關於FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

預設視頻編碼過程基於使用基於FFMPEG的與視頻簡檔的整合。 因此， [!UICONTROL DAM更新資產] 工作流包含以下兩個基於ffmpeg的工作流步驟：

* FFMPEG縮略圖
* FFMPEG編碼

啟用和配置Dynamic Media Classic整合不會自動從現成環境中刪除或停用這兩個工作流步驟 [!UICONTROL DAM更新資產] 接收工作流。 如果您已在Adobe Experience Manager使用基於FFMPEG的視頻編碼，則您很可能在創作環境中安裝了FFMPEG。 在這種情況下，使用Experience Manager Assets攝入的新視頻被編碼兩次：一次來自FFMPEG編碼器，一次來自Dynamic Media Classic。

如果在Experience Manager中配置了基於FFMPEG的視頻編碼並安裝了FFMPEG,Adobe建議您從 [!UICONTROL DAM更新資產] 工作流。

### 支援的格式 {#supported-formats}

Dynamic Media Classic視頻元件支援以下格式：

* F4V H.264
* MP4 H.264

### 決定上傳視頻的位置 {#deciding-where-to-upload-your-video}

確定在何處上載視頻資產取決於以下內容：

* 是否需要視頻資產的工作流？
* 是否需要視頻資產的版本控制？

如果對其中一個或兩個問題回答「是」，則將視頻直接上傳到AdobeDAM。 如果兩個問題的答案都是「否」，則直接將視頻上傳到Dynamic Media Classic。 以下部分介紹了每個方案的工作流。

#### 如果您直接將視頻上載到Adobe資產 {#if-you-are-uploading-your-video-directly-to-adobe-assets}

如果您需要資產的工作流或版本化，則應首先上載到Adobe資產。 以下是推薦的工作流：

1. 將視頻資產上載到Adobe資產，並自動編碼和發佈到Dynamic Media Classic。
1. 在Experience Manager中，訪問WCM中的視頻資產 **[!UICONTROL 電影]** 的子菜單。
1. 使用Dynamic Media Classic視頻或基礎視頻元件作者。

#### 如果你正在將視頻上傳到Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

如果您不需要資產工作流或版本化，則應將資產上載到Dynamic Media Classic。 以下是推薦的工作流：

1. 在Dynamic Media Classic的案頭應用里， [設定定時FTP上傳和編碼到Dynamic Media Classic（系統自動）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-options)。
1. 在Experience Manager中，訪問WCM中的視頻資產 **[!UICONTROL Dynamic Media Classic]** 的子菜單。
1. 編寫Dynamic Media Classic視頻元件。

### 配置與Dynamic Media Classic視頻的整合 {#configuring-integration-with-scene-video}

1. 在 **[!UICONTROL Cloud Services]**，導航至 **[!UICONTROL Dynamic Media Classic]** 配置和選擇 **[!UICONTROL 編輯]**。
1. 選擇 **[!UICONTROL 視頻]** 頁籤。

   >[!NOTE]
   >
   >的 **[!UICONTROL 視頻]** 如果頁面沒有雲配置，則不顯示頁籤。 請參閱 [為WCM啟用Dynamic Media Classic](#enablingscene7forwcm)。

1. 選擇自適應視頻編碼配置檔案、現成的單個視頻編碼配置檔案或自定義視頻編碼配置檔案。

   >[!NOTE]
   >
   >有關視頻預設含義的詳細資訊，請參見 [用於編碼視頻檔案的視頻預設](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files)。
   >
   >Adobe建議在配置通用預設時同時選擇兩個自適應視頻集，或選擇 **[!UICONTROL 自適應視頻編碼]** 的雙曲餘切值。

1. 所選編碼配置檔案將自動應用於上載到您為此Dynamic Media Classic雲配置設定的CQ DAM目標資料夾的所有視頻。 您可以設定多個具有不同目標資料夾的Dynamic Media Classic雲配置，以根據需要應用不同的編碼配置檔案。

### 更新查看器和編碼預設 {#updating-viewer-and-encoding-presets}

如果預設在Dynamic Media Classic更新，則更新Experience Manager中視頻的查看器和編碼預設。 在這種情況下，導航到雲配置中的Dynamic Media Classic配置並選擇 **更新查看器和編碼預設**。

![chlimage_1-131](assets/chlimage_1-131.png)

### 上載主源視頻 {#uploading-your-master-video}

要從AdobeDAM將主源視頻上傳到Dynamic Media Classic，請執行以下操作：

1. 導航至CQ DAM目標資料夾，在該資料夾中您已使用Dynamic Media Classic編碼配置檔案設定雲配置。
1. 選擇 **[!UICONTROL 上載]** 上載主源視頻。 視頻上載和編碼在 [!UICONTROL DAM更新資產] 工作流已完成， **[!UICONTROL 發佈到Dynamic Media Classic]** 有複選標籤。

   >[!NOTE]
   >
   >生成視頻縮略圖可能需要一些時間。

   將DAM主源視頻拖到視頻元件上時，將訪問 *全部* Dynamic Media Classic編碼了代理格式副本以供遞送。

### 基礎視頻元件與Dynamic Media Classic視頻元件 {#foundation-video-component-versus-scene-video-component}

使用Experience Manager時，您可以訪問「站點」中可用的視頻元件和Dynamic Media Classic視頻元件。 這些元件不能互換。

Dynamic Media Classic視頻元件只適用於Dynamic Media Classic視頻。 該基礎元件使用從Experience Manager（使用ffmpeg）和Dynamic Media Classic視頻儲存的視頻。

下表說明了何時應使用哪個元件：

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>開箱後，Dynamic Media Classic視頻元件使用通用視頻配置檔案。 但是，您可以獲得基於HTML5的視頻播放器，供Experience Manager使用。 在Dynamic Media Classic，複製現成HTML5視頻播放器的嵌入代碼，並將其放入Experience Manager頁面。

## Experience Manager視頻元件 {#aem-video-component}

即使建議使用Dynamic Media Classic視頻元件來查看Dynamic Media Classic視頻，本節也介紹使用Dynamic Media Classic視頻與 [!UICONTROL 基礎視頻元件] 為完整Experience Manager。

### Experience Manager視頻與Dynamic Media Classic視頻比較 {#aem-video-and-scene-video-comparison}

下表提供了Experience Manager基金會視頻元件和Dynamic Media Classic視頻元件之間支援的功能的高級比較：

|  | Experience Manager基金會視頻 | Dynamic Media Classic視頻 |
|---|---|---|
| 方法 | HTML5第一步。 Flash僅用於非HTML5回退。 | Flash在大多數台式機上。 HTML5用於移動和平板電腦。 |
| 傳送 | 累進 | 自適應流 |
| 跟蹤 | 是 | 是 |
| 擴展性 | 是 | 否 |
| 行動視訊 | 是 | 是 |

### 設定 {#setting-up}

#### 建立視頻配置檔案 {#creating-video-profiles}

根據在Dynamic Media Classic雲配置中選擇的Dynamic Media Classic編碼預設建立各種視頻編碼。 要使用基礎視頻元件，必須為每個選定的Dynamic Media Classic編碼預設建立視頻配置檔案。 它允許視頻元件相應地選擇DAM格式副本。

>[!NOTE]
>
>必須激活新視頻配置檔案及對它們所做的更改才能發佈。

1. 在Experience Manager中，轉到 **[!UICONTROL 工具]**，然後選擇 **[!UICONTROL 配置控制台]**。
1. 在配置控制台中，導航到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視頻配置檔案]** 的子菜單。
1. 建立Dynamic Media Classic視頻配置檔案。 在 **[!UICONTROL 新建]** 菜單，選擇 **[!UICONTROL 建立頁]**。
1. 選擇Dynamic Media Classic視頻配置檔案模板。 為新視頻配置檔案頁面指定名稱並選擇 **[!UICONTROL 建立]**。

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. 編輯新視頻配置檔案。 首先選擇雲配置。 然後選擇與雲配置中選擇的編碼預設相同。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | 屬性 | 說明 |
   |---|---|
   | Dynamic Media Classic雲配置 | 用於編碼預設的雲配置。 |
   | Dynamic Media Classic編碼預設 | 用於映射此視頻配置檔案的編碼預設。 |
   | HTML5 視訊類型 | 此屬性用於設定HTML5視頻源元素的type屬性的值。 Dynamic Media Classic編碼預設不提供此資訊，但使用HTML5視頻元素正確呈現視頻時需要此資訊。 提供了通用格式的清單，但可以覆蓋其它格式。 |

   對要在視頻元件中使用的雲配置中選擇的所有編碼預設重複此步驟。

#### 配置設計 {#configuring-design}

基礎視頻元件必須知道要使用哪些視頻配置檔案才能生成視頻源清單。 開啟視頻元件設計對話框並配置元件設計以使用新視頻配置檔案。

>[!NOTE]
>
>如果在移動頁面上使用基礎視頻元件，請在移動頁面的設計上重複這些步驟。

>[!NOTE]
>
>對設計所做的更改需要激活設計以便對發佈生效。

1. 開啟基礎視頻元件的設計對話框並更改到 **[!UICONTROL 配置檔案]** 頁籤。 然後刪除現成配置檔案，並添加新的Dynamic Media Classic視頻配置檔案。 設計對話框中配置檔案清單的順序以及渲染時視頻源元素的順序。
1. 對於不支援HTML5的瀏覽器，Video元件允許您配置Flash回退。 開啟視頻元件設計對話框並更改到 **[!UICONTROL Flash]** 頁籤。 配置Flash Player設定並為Flash Player分配備用配置檔案。

#### 核對表 {#checklist}

1. 建立Dynamic Media Classic雲配置。 確保已設定視頻編碼預設且導入程式正在運行。
1. 為雲配置中選擇的每個視頻編碼預設建立Dynamic Media Classic視頻配置檔案。
1. 必須激活視頻配置檔案。
1. 在頁面上配置基礎視頻元件的設計。
1. 完成設計更改後激活設計。
