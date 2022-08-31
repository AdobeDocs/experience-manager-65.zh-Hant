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
feature: 360 VR Video
role: User, Admin
exl-id: 0c2077a7-bd16-484b-980f-4d4a1a681491
source-git-commit: c0a60ec39e35fa8113ce9e1795561709b9c7e289
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 0%

---

# 360/VR影片 {#vr-video}

360度的視頻同時記錄每個方向的觀看。 它們是用全向攝像機或一組攝像機拍攝的。 在平面顯示器上播放期間，使用者可控制觀看角度；行動裝置上的播放通常使用其內建的陀螺控制項。

Dynamic Media - Scene7模式包含360個視訊資產的原生支援。 依預設，檢視或播放不需要其他設定。 您使用標準視訊副檔名（例如.mp4、.mkv和.mov）來傳送360視訊。 最常見的編解碼器為H.264。

本節說明如何使用360/VR視訊檢視器來轉譯等矩形視訊，以提供房間、屬性、位置、景觀、醫療程式等的沈浸式檢視體驗。

當前不支援空間音頻；如果音頻在立體聲中混合，則餘額(L/R)不會隨著客戶更改攝像機視角而改變。

另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

## 360影片的實際運作 {#video-in-action}

選擇 [空間站360](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) 開啟瀏覽器視窗並觀看360度影片。 在視頻播放期間，將滑鼠指針拖到新位置以更改觀看角度。

![360個視頻樣本，國際空間站漂浮在外太空，地球和太陽的後面。](assets/6_5_360videoiss_simplified.png)
*360號空間站的視頻幀*

## 360/VR影片和Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用AdobePremier Pro來查看和編輯360/VR素材。 例如，您可以將標誌和文字正確放置在場景中，並套用專為等矩形媒體而設計的效果和轉變。

請參閱 [編輯360/VR影片](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## 上傳資產以便與360視訊檢視器搭配使用 {#uploading-assets-for-use-with-the-video-viewer}

上傳至Adobe Experience Manager的360個視訊資產會標示為 **多媒體** 在「資產」頁面上，類似於一般視訊資產。

![6_5_360video-selecttopreview](assets/6_5_360video-selecttopreview.png)
*卡片檢視中顯示的已上傳360視訊資產。 資產標示為多媒體。*

**上傳要與360視訊檢視器搭配使用的資產：**

1. 已建立專屬於360視訊資產的資料夾。
1. [將最適化視訊設定檔套用至資料夾](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   呈現360視訊內容比標準非360視訊內容對來源視訊解析度和編碼轉譯解析度的要求更高。

   您可以使用Dynamic Media隨附的現成可用最適化視訊設定檔。 但是，這會導致360視訊品質明顯低於使用非360視訊檢視器轉譯之相同設定所編碼的非360視訊的品質。 因此，如果需要高品質的360視訊，請執行下列動作：

   * 理想情況下，您原始的360視訊內容最好具備下列其中一種解析度：

      * 1080p - 1920 x 1080，稱為全高清或全高清解析度，或
      * 2160p - 3840 x 2160，稱為4k、UHD或UltraHD解析度。 這種大螢幕解析度通常在高端電視機和電腦顯示器上。 2160p的解析度通常稱為「4k」，因為寬度接近4000像素。 換句話說，它提供的像素是1080p的4倍。
   * [建立自訂最適化視訊設定檔](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 以更高品質的轉譯。 例如，建立包含下列三個設定的適用性視訊設定檔：

      * width=auto;height=720;bitrate=2500 kbps
      * width=auto;height=1080;bitrate=5000 kbps
      * width=auto;height=1440;bitrate=6600 kbps
   * 在專屬於360個視訊資產的資料夾中處理360個視訊內容。

   這種方法對最終用戶的網路和CPU提出了更大的要求。

1. [將影片上傳至資料夾](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

## 覆寫360個視訊的預設外觀比例  {#overriding-the-default-aspect-ratio-of-videos}

若要讓上傳的資產符合360視訊檢視器使用的360視訊資格，資產的外觀比例必須為2。

預設情況下，如果視頻的長寬比（寬/高）為2.0，則Experience Manager將視頻檢測為「360」。如果您是管理員，則可以通過設定可選的 `s7video360AR` CRXDE Lite中的屬性（如下所示）:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **屬性類型**  — 雙倍
   * **值**  — 浮點外觀比例，預設值2.0。

設定此屬性後，該屬性會立即對現有視訊和新上傳的視訊生效。

外觀比例適用於資產詳細資訊頁面和 [視訊360媒體WCM元件](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

首先，上傳360個影片。

## 預覽360影片 {#previewing-video}

您可以使用「預覽」來查看360影片對客戶的外觀，並確保其如預期般運作。

另請參閱 [編輯檢視器預設集](/help/assets/managing-viewer-presets.md#editing-viewer-presets).

當您對360影片感到滿意時，即可發佈影片。

請參閱 [將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md).
請參閱 [將URL連結至您的Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md). 如果您的互動式內容有連結與相對URL(尤其是連結至Experience Manager Sites頁面)，則無法使用以URL為基礎的連結方法。
請參閱 [將Dynamic Media Assets新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md).

**若要預覽360影片：**

1. 在 **[!UICONTROL 資產]**，導覽至您建立的現有360影片。 選取「360視訊」資產，以便在預覽模式中開啟資產。

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   選取360視訊資產，以便預覽視訊。

1. 在預覽頁面的左上角附近，選取下拉式清單，然後選取 **[!UICONTROL 檢視器]**.

   ![6_5_360視訊預覽檢視器](assets/6_5_360video-preview-viewers.png)

   從「檢視器」清單中，選取 **[!UICONTROL Video360_social]**，然後執行下列其中一項操作：

   * 如果要更改靜態場景的觀看角度，請將滑鼠指針拖過視頻。
   * 選取視訊的 **[!UICONTROL 播放]** 按鈕。 當視訊播放時，將滑鼠指標拖曳到視訊上，以變更您的檢視角度。

   ![地球和太陽背景下漂浮在外層空間的國際空間站螢幕截圖&#x200B;](assets/6_5_360video-preview-video360-social.png)*360視頻螢幕截圖。*

   * 從「檢視器」清單中，選取 **[!UICONTROL Video360VR]**.

      虛擬現實(VR)視訊是沈浸式視訊內容，可透過虛擬現實頭戴式裝置存取。 和普通視訊一樣，當您使用360度的攝像頭來記錄或擷取視訊時，您一開始就會建立VR視訊。
   ![一個螢幕截圖，顯示了在外層空間漂浮的國際空間站的特寫，地球和太陽在背景部分可見](assets/6_5_360video-preview-video360vr.png)
   *360 VR視訊螢幕擷圖。*

1. 在預覽頁面的右上方附近，選取 **[!UICONTROL 關閉]**.

## 發佈360影片 {#publishing-video}

發佈360影片，方便您使用。 發佈360影片會啟用URL和內嵌程式碼。 此外，也會將360視訊發佈至Dynamic Media雲端，與CDN整合，以提供可擴充且高效能的傳遞。

請參閱 [發佈Dynamic Media資產](/help/assets/publishing-dynamicmedia-assets.md) 以取得如何發佈360影片的詳細資訊。
另請參閱 [將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md).
另請參閱 [將URL連結至您的Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md). 如果您的互動式內容有連結與相對URL(尤其是連結至Experience Manager Sites頁面)，則無法使用以URL為基礎的連結方法。
另請參閱 [新增Dynamic Media資產至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md).
