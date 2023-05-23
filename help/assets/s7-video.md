---
title: 影片
description: 瞭解集中式視頻資產管理Adobe Experience Manager資產，您可以在其中將視頻上傳到Dynamic Media Classic進行自動編碼，並直接從Experience Manager Assets訪問Dynamic Media Classic視頻。 Dynamic Media Classic視頻整合將優化視頻的覆蓋範圍擴展到所有螢幕。
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
role: User, Admin
mini-toc-levels: 3
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: Video
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 2%

---

# 影片 {#video}

Adobe Experience Manager資產提供集中的視頻資產管理，您可以將視頻直接上傳到資產中，以便自動編碼到Dynamic Media Classic，並直接從資產中訪問Dynamic Media Classic視頻以進行頁面創作。

Dynamic Media Classic視頻整合將優化視頻的覆蓋範圍擴展到所有螢幕（自動設備和頻寬檢測）。

* 的 **[!UICONTROL Scene7視頻]** 元件自動執行設備和頻寬檢測，以在案頭、平板電腦和移動設備上播放正確的格式和質量的視頻。
* 資產 — 您可以包括自適應視頻集，而不是僅包括單個視頻資產。 自適應視頻集包含在多個螢幕上無縫播放視頻所需的所有視頻格式副本。 自適應視頻集將以不同比特率和格式（如400 kbps、800 kbps和1000 kbps）編碼的同一視頻的版本分組。 您可以使用自適應視頻集和S7視頻元件，在多個螢幕(包括案頭、iOS、Android™、BlackBerry®和Windows移動設備)上進行自適應視頻流傳輸。
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## 關於FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

預設視頻編碼過程基於使用基於FFMPEG的與視頻簡檔的整合。 因此，現成的DAM接收工作流包含以下兩個基於ffmpeg的工作流步驟：

* FFMPEG縮略圖
* FFMPEG編碼

啟用和配置Dynamic Media Classic整合不會自動從現成的DAM接收工作流中刪除或停用這兩個工作流步驟。 如果您已在Adobe Experience Manager使用基於FFMPEG的視頻編碼，則您很可能在創作環境中安裝了FFMPEG。 在這種情況下，使用DAM接收的新視頻將被編碼兩次：一次來自FFMPEG編碼器，一次來自Dynamic Media Classic。

如果在Experience Manager中配置了基於FFMPEG的視頻編碼並安裝了FFMPEG,Adobe建議您從DAM接收工作流中刪除兩個FFMPEG工作流。

## 支援的格式 {#supported-formats}

Scene7視頻元件支援以下格式：

* F4V H.264
* MP4 H.264

## 決定上傳視頻的位置 {#deciding-where-to-upload-your-video}

確定在何處上載視頻資產取決於以下內容：

* 是否需要視頻資產的工作流？
* 是否需要視頻資產的版本控制？

如果對其中一個或兩個問題回答「是」，則將視頻直接上傳到AdobeDAM。 如果兩個問題的答案都是「否」，則直接將視頻上傳到Dynamic Media Classic。 以下部分介紹了每個方案的工作流。

### 如果您直接將視頻上傳到AdobeDAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

如果您需要資產的工作流或版本化，請先上載到AdobeDAM。 以下是推薦的工作流：

1. 將視頻資產上傳到AdobeDAM，並自動編碼和發佈到Dynamic Media Classic。
1. 在Experience Manager中，訪問WCM中的視頻資產 **[!UICONTROL 電影]** 的子菜單。
1. 作者 **[!UICONTROL Scene7視頻]** 或 **[!UICONTROL 基礎視頻]** 元件。

### 如果你正在將視頻上傳到Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

如果您不需要資產的工作流或版本化，請將資產上載到Scene7。 以下是推薦的工作流：

1. 在Dynamic Media Classic, [設定定時FTP上傳和編碼到Scene7（系統自動）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp)。
1. 在Experience Manager中，訪問WCM中的視頻資產 **[!UICONTROL Scene7]** 的子菜單。
1. 作者 **[!UICONTROL Scene7視頻]** 元件。

## 配置與Scene7視頻的整合 {#configuring-integration-with-scene-video}

1. 在 **[!UICONTROL Cloud Services]**，導航至 **[!UICONTROL Scene7]** 配置和選擇 **[!UICONTROL 編輯]**。
1. 選擇 **[!UICONTROL 視頻]** 頁籤。

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >的 **[!UICONTROL 視頻]** 如果頁面沒有雲配置，則不顯示頁籤。

1. 選擇自適應視頻編碼配置檔案、現成的單個視頻編碼配置檔案或自定義視頻編碼配置檔案。

   >[!NOTE]
   >
   >有關視頻預設含義的詳細資訊，請參閱 [Dynamic Media Classic文檔](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files)。
   >
   >Adobe建議在配置通用預設時同時選擇兩個自適應視頻集，或選擇 **[!UICONTROL 自適應視頻編碼]** 的雙曲餘切值。

1. 所選編碼配置檔案將自動應用於上載到您為此Scene7雲配置設定的CQ DAM目標資料夾的所有視頻。 您可以設定多個具有不同目標資料夾的Scene7雲配置，以根據需要應用不同的編碼配置檔案。

## 更新檢視器和編碼預設集 {#updating-viewer-and-encoding-presets}

若要更新視頻的查看器和編碼預設，因為預設已在Scene7更新，請導航至「雲配置」中的「Scene7配置」並選擇 **[!UICONTROL 更新查看器和編碼預設]**。

![chlimage_1-364](assets/chlimage_1-364.png)

## 從AdobeDAM將主源視頻上載到Scene7 {#uploading-your-master-video}

1. 導航至CQ DAM目標資料夾，在該資料夾中您已使用Scene7編碼配置檔案設定雲配置。
1. 選擇 **[!UICONTROL 上載]** 上載主源視頻。 視頻上載和編碼在 [!UICONTROL DAM更新資產] 工作流已完成， **[!UICONTROL 發佈到Scene7]** 有複選標籤。

   >[!NOTE]
   >
   >生成視頻縮略圖需要時間。

   將DAM主源視頻拖到視頻元件訪問 *全部* Scene7編碼了代理格式副本以供遞送。

## 基礎視頻元件與Scene7視頻元件 {#foundation-video-component-versus-scene-video-component}

使用Experience Manager時，您可以訪問「站點」中可用的視頻元件和Scene7視頻元件。 這些元件不能互換。

Scene7視頻元件只適用於Scene7視頻。 該基礎元件使用從Experience Manager（使用ffmpeg）和Scene7視頻儲存的視頻。

以下矩陣說明了何時使用哪個元件：

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>S7視頻元件現成使用通用視頻配置檔案。 但是，您可以獲得基於HTML5的視頻播放器，供Experience Manager使用。 在Scene7，複製現成HTML5視頻播放器的嵌入代碼，並將其放入Experience Manager頁面。

## Experience Manager視頻元件 {#aem-video-component}

即使建議使用Scene7視頻元件來觀看Scene7視頻，但為了完整起見，本節將介紹為了使用Scene7視頻與Experience Manager中的基金會視頻元件一起使用視頻。

### Experience Manager視頻與Scene7視頻比較 {#aem-video-and-scene-video-comparison}

下表提供了Experience Manager基金會視頻元件和Scene7視頻元件之間支援的功能的高級比較：

|  | Experience Manager基金會視頻 | Scene7視頻 |
|---|---|---|
| 方法 | HTML5第一步。 Flash僅用於非HTML5回退。 | Flash在大多數台式機上。 HTML5用於移動和平板電腦。 |
| 傳送 | 累進 | 自適應流 |
| 跟蹤 | 是 | 是 |
| 擴展性 | 是 | 否 |
| 行動視訊 | 是 | 是 |

### 設定 {#setting-up}

#### 建立視頻配置檔案 {#creating-video-profiles}

根據S7雲配置中選擇的S7編碼預設來建立各種視頻編碼。 要使用基礎視頻元件，必須為每個選定的S7編碼預設建立視頻配置檔案。 此方法允許視頻元件相應地選擇DAM格式副本。

>[!NOTE]
>
>必須激活新視頻配置檔案及對它們所做的更改才能發佈。

1. 在Experience Manager中，選擇 **[!UICONTROL 工具]** > **[!UICONTROL 配置控制台]**。
1. 在 **[!UICONTROL 配置控制台]**，導航 **[!UICONTROL 工具]** > **[!UICONTROL 水壩]** > **[!UICONTROL 視頻配置檔案]** 的子菜單。
1. 建立S7視頻配置檔案。 在 **[!UICONTROL 新建]**。 菜單，選擇 **[!UICONTROL 建立頁]** 然後選擇「Scene7視頻配置檔案」模板。 為新視頻配置檔案頁面指定名稱並選擇 **[!UICONTROL 建立]**。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 編輯新視頻配置檔案。 首先選擇雲配置。 然後選擇與雲配置中選擇的編碼預設相同。

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | 屬性 | 說明 |
   |---|---|
   | Scene7 雲端設定 | 用於編碼預設的雲配置。 |
   | Scene7 編碼預設集 | 用於映射此視頻配置檔案的編碼預設。 |
   | HTML5 視訊類型 | 此屬性用於設定HTML5視頻源元素的type屬性的值。 S7編碼預設不提供此資訊，但是使用HTML5視頻元素正確呈現視頻時需要此資訊。 提供了通用格式的清單，但可以覆蓋其它格式。 |

   對要在視頻元件中使用的雲配置中選擇的所有編碼預設重複此步驟。

#### 配置設計 {#configuring-design}

的 **[!UICONTROL 基礎視頻]** 元件必須知道要構建視頻源清單要使用哪些視頻配置檔案。 開啟視頻元件設計對話框並配置元件設計以使用新視頻配置檔案。

>[!NOTE]
>
>如果使用 **[!UICONTROL 基礎視頻]** 元件，在移動頁面的設計中重複這些步驟。

>[!NOTE]
>
>對設計所做的更改需要激活設計以便對發佈生效。

1. 開啟 **[!UICONTROL 基礎視頻]** 元件的「設計」對話框，並更改為 **[!UICONTROL 配置檔案]** 頁籤。 然後刪除現成配置檔案，並添加新的S7視頻配置檔案。 「設計」對話框中配置檔案清單的順序定義渲染時視頻源元素的順序。
1. 對於不支援HTML5的瀏覽器，視頻元件允許您配置Flash回退。 開啟視頻元件設計對話框，並更改到 **[!UICONTROL Flash]** 頁籤。 配置Flash播放器設定並為Flash播放器分配備用配置檔案。

#### 核對表 {#checklist}

1. 建立S7雲配置。 確保已設定視頻編碼預設且導入程式正在運行。
1. 為雲配置中選擇的每個視頻編碼預設建立S7視頻配置檔案。
1. 必須激活視頻配置檔案。
1. 配置 **[!UICONTROL 基礎視頻]** 元件。
1. 完成設計更改後激活設計。
