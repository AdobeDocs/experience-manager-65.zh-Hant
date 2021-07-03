---
title: 360/VR影片
description: 了解如何在Dynamic Media中使用360和虛擬現實(VR)視訊。
uuid: c21bf2c0-7acc-401f-857e-0186de86e7a1
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: aac3c850-ae84-4bff-80de-d370e150f675
docset: aem65
feature: 360 VR 影片
role: User, Admin
exl-id: 0c2077a7-bd16-484b-980f-4d4a1a681491
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 0%

---

# 360/VR影片 {#vr-video}

360度的視頻同時記錄每個方向的觀看。 它們是用全向攝像機或一組攝像機拍攝的。 在平面顯示器上播放期間，使用者可控制觀看角度；行動裝置上的播放通常使用其內建的陀螺控制項。

Dynamic Media - Scene7模式包含360個視訊資產的原生支援。 依預設，檢視或播放不需要其他設定。 您使用標準視訊副檔名（例如.mp4、.mkv和.mov）來傳送360視訊。 最常見的編解碼器為H.264。

本節說明如何使用360/VR視訊檢視器來轉譯等矩形視訊，以提供房間、屬性、位置、景觀、醫療程式等的沈浸式檢視體驗。

當前不支援空間音頻；如果音頻在立體聲中混合，則餘額(L/R)不會隨著客戶更改攝像機視角而改變。

另請參閱[管理檢視器預設集](/help/assets/managing-viewer-presets.md)。

## 360影片的實際運作 {#video-in-action}

點選[空間站360](https://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS)以開啟瀏覽器窗口並觀看360度視頻。 在視頻播放期間，將滑鼠指針拖到新位置以更改觀看角度。

![360視頻](assets/6_5_360videoiss_simplified.png)
*示例來自空間站的視頻幀360*

## 360/VR影片和Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用AdobePremier Pro來查看和編輯360/VR素材。 例如，您可以將標誌和文字正確放置在場景中，並套用專為等矩形媒體而設計的效果和轉變。

請參閱[編輯360/VR視訊](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html)。

## 上傳資產以便與360視訊檢視器搭配使用 {#uploading-assets-for-use-with-the-video-viewer}

上傳至Adobe Experience Manager的360個視訊資產在「資產」頁面上會標示為&#x200B;**Multimedia**，與一般視訊資產類似。

![6_5_360視訊 — ](assets/6_5_360video-selecttopreview.png)
*selecttopreview在「卡片」檢視中看到已上傳的360視訊資產。資產標籤為多媒體。*

**上傳要與360視訊檢視器搭配使用的資產：**

1. 已建立專屬於360視訊資產的資料夾。
1. [將最適化視訊設定檔套用至資料夾](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)。

   轉譯360視訊內容比標準非360視訊內容對來源視訊解析度和編碼轉譯解析度的要求更高。

   您可以使用Dynamic Media隨附的現成可用最適化視訊設定檔。 但是，這會導致360視訊品質明顯低於使用非360視訊檢視器轉譯之相同設定所編碼的非360視訊。 因此，如果需要高品質的360視訊，請執行下列動作：

   * 理想情況下，您原始的360視訊內容最好具備下列其中一種解析度：

      * 1080p - 1920 x 1080，稱為全高清或全高清解析度，或
      * 2160p - 3840 x 2160，稱為4k、UHD或UltraHD解析度。 這種大螢幕解析度通常在高端電視機和電腦顯示器上。 2160p的解析度通常稱為「4k」，因為寬度接近4000像素。 換句話說，它提供的像素是1080p的4倍。
   * [建立自訂適用性視訊設](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 定檔及更高品質的轉譯。例如，建立包含下列三個設定的適用性視訊設定檔：

      * width=auto;height=720;bitrate=2500 kbps
      * width=auto;height=1080;bitrate=5000 kbps
      * width=auto;height=1440;bitrate=6600 kbps
   * 在專屬於360個視訊資產的資料夾中處理360個視訊內容。

   這種方法對最終用戶的網路和CPU提出了更大的要求。

1. [將影片上傳至資料夾](/help/assets/managing-video-assets.md#upload-and-preview-video-assets)。

## 覆寫360個視訊的預設外觀比例  {#overriding-the-default-aspect-ratio-of-videos}

若要讓上傳的資產符合360視訊檢視器使用的360視訊資格，資產的外觀比例必須為2。

預設情況下，如果視頻的長寬比（寬/高）為2.0,Experience Manager將視頻檢測為「360」。如果您是管理員，則可以通過在以下位置設定CRXDE Lite中的可選`s7video360AR`屬性來覆蓋預設長寬比設定2:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **屬性類型**  — 雙精度
   * **值**  — 浮點外觀比例，預設為2.0。

設定此屬性後，該屬性會立即對現有視訊和新上傳的視訊生效。

外觀比例適用於資產詳細資訊頁面和[ Video 360 Media WCM元件](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components)的360視訊資產。

首先，上傳360個影片。

## 預覽360影片 {#previewing-video}

您可以使用「預覽」來查看360影片對客戶的外觀，並確保其如預期般運作。

另請參閱[編輯查看器預設集](/help/assets/managing-viewer-presets.md#editing-viewer-presets)。

當您對360影片感到滿意時，即可發佈影片。

請參閱[將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md)。
請參閱[將URL連結到您的Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md)。 如果您的互動式內容有連結與相對URL，尤其是連結至Experience Manager網站頁面的連結，則無法使用以URL為基礎的連結方法。
請參閱[將Dynamic Media資產新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

**若要預覽360個影片：**

1. 在&#x200B;**[!UICONTROL Assets]**&#x200B;中，導覽至您已建立的現有360視訊。 點選「 360視訊」資產，以便在預覽模式中開啟資產。

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   點選360視訊資產，以便預覽視訊。

1. 在預覽頁面上，在頁面左上角附近，點選下拉式清單，然後選取「**[!UICONTROL 檢視器]**」。

   ![6_5_360視訊預覽檢視器](assets/6_5_360video-preview-viewers.png)

   從「檢視器」清單中，點選&#x200B;**[!UICONTROL Video360_social]**，然後執行下列其中一項作業：

   * 如果要更改靜態場景的觀看角度，請將滑鼠指針拖過視頻。
   * 如果您要開始播放，請點選視訊的&#x200B;**[!UICONTROL 播放]**&#x200B;按鈕。 當視訊播放時，將滑鼠指標拖曳到視訊上，以變更您的檢視角度。

   ![6_5_360 video-preview-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360影片螢幕擷圖。*

   * 從「檢視器」清單中，點選&#x200B;**[!UICONTROL Video360VR]**。

      虛擬現實(VR)視訊是沈浸式視訊內容，可透過虛擬現實頭戴式裝置存取。 和普通視訊一樣，當您使用360度的攝像頭來記錄或擷取視訊時，您一開始就會建立VR視訊。
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *360 VR視訊螢幕擷圖。*

1. 在預覽頁面的右上方附近，點選&#x200B;**[!UICONTROL 關閉]**。

## 發佈360影片 {#publishing-video}

發佈360影片，方便您使用。 發佈360影片會啟用URL和內嵌程式碼。 此外，也會將360視訊發佈至Dynamic Media雲端，與CDN整合，以提供可擴充且高效能的傳遞。

如需如何發佈360影片的詳細資訊，請參閱[發佈Dynamic Media資產](/help/assets/publishing-dynamicmedia-assets.md)。
另請參閱[在網頁上嵌入視頻或影像查看器](/help/assets/embed-code.md)。
另請參閱[將URL連結到Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md)。 如果您的互動式內容有連結與相對URL，尤其是連結至Experience Manager網站頁面的連結，則無法使用以URL為基礎的連結方法。
另請參閱[將Dynamic Media資產新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)。
