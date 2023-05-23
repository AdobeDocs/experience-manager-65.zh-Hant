---
title: 360/VR視頻
description: 瞭解如何在Dynamic Media使用360和虛擬現實(VR)視頻。
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

# 360/VR視頻 {#vr-video}

360度視頻同時記錄每個方向的視圖。 它們是用全向相機或一組相機拍攝的。 在平面顯示器上回放期間，用戶對視角有控制；移動設備上的回放通常使用其內置的陀螺控制。

Dynamic Media-Scene7模式包括本機支援360個視頻資產的交付。 預設情況下，查看或回放不需要其他配置。 使用標準視頻擴展(如.mp4、.mkv和.mov)提供360視頻。 最常見的編解碼器是H.264。

本節介紹如何與360/VR視頻查看器協作，以呈現等長形視頻，讓您體驗房間、房產、位置、景觀、醫療程式等的沈浸式觀看體驗。

當前不支援空間音頻；如果立體聲中混合了音頻，則餘額(L/R)不會隨著客戶更改攝像機視角而改變。

另請參閱 [管理查看器預設](/help/assets/managing-viewer-presets.md)。

## 360視頻正在執行 {#video-in-action}

選擇 [360號空間站](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) 開啟瀏覽器窗口，觀看360度視頻。 在視頻回放期間，將滑鼠指針拖動到新位置以更改視角。

![360個視頻樣本，國際空間站漂浮在外太空，地球和太陽的背後。](assets/6_5_360videoiss_simplified.png)
*360空間站視頻幀*

## 360/VR視頻和Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用AdobePremier Pro查看和編輯360/VR素材。 例如，您可以將徽標和文本正確放置在場景中，並應用專門為等矩形介質設計的效果和過渡。

請參閱 [編輯360/VR視頻](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html)。

## 上載用於360視頻查看器的資產 {#uploading-assets-for-use-with-the-video-viewer}

上傳到Adobe Experience Manager的360個視頻資產標為 **多媒體** 在「資產」頁面上，與普通視頻資產類似。

![6_5_360視頻選擇預覽](assets/6_5_360video-selecttopreview.png)
*在「卡」視圖中看到已上傳的360視頻資產。 該資產被標籤為「多媒體」。*

**上載用於360視頻查看器的資產：**

1. 已建立專用於360視頻資產的資料夾。
1. [將自適應視頻配置檔案應用到資料夾](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)。

   與標準非360視頻內容相比，呈現360視頻內容對源視頻解析度和編碼格式副本解析度的要求更高。

   您可以使用現成的Adaptive Video Profile（自適應視頻配置檔案），該配置檔案已隨Dynamic Media提供。 但是，它會使360視頻質量明顯低於使用非360視頻查看器呈現的相同設定編碼的非360視頻。 因此，如果需要高質量360視頻，請執行以下操作：

   * 理想情況下，您的原始360視頻內容最好具備以下任一解析度：

      * 1080p - 1920 x 1080，稱為全高清或全高清解析度或，
      * 2160p - 3840 x 2160，稱為4k、UHD或Ultra高清解析度。 這種大的顯示解析度通常在高端電視機和電腦顯示器上找到。 2160p解析度通常稱為「4k」，因為寬度接近4000像素。 換句話說，它的像素是1080p的四倍。
   * [建立自定義自適應視頻配置檔案](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 以更高質量的格式副本。 例如，建立包含以下三種設定的自適應視頻配置檔案：

      * 寬度=自動；height=720;比特率=2500 kbps
      * 寬度=自動；height=1080;比特率=5000 kbps
      * 寬度=自動；height=1440;比特率=6600 kbps
   * 處理專用於360個視頻資產的資料夾中的360個視頻內容。

   這種方法對最終用戶的網路和CPU提出了更高的要求。

1. [將視頻上載到資料夾](/help/assets/managing-video-assets.md#upload-and-preview-video-assets)。

## 覆蓋360個視頻的預設長寬比  {#overriding-the-default-aspect-ratio-of-videos}

如果上載的資產符合與360視頻查看器一起使用的360視頻，則資產的長寬比必須為2。

預設情況下，如果視頻的長寬比（寬/高）為2.0，則Experience Manager會將其檢測為「360」。如果您是管理員，則可以通過設定可選項來覆蓋預設長寬比設定2 `s7video360AR` CRXDE Lite中的屬性：

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **屬性類型**  — 雙
   * **值**  — 浮點縱橫比，預設2.0

設定此屬性後，它將立即對現有視頻和新上載的視頻生效。

長寬比適用於資產詳細資訊頁面和 [視頻360媒體WCM元件](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components)。

首先上傳360個視頻。

## 預覽360視頻 {#previewing-video}

您可以使用預覽查看360視頻對客戶的外觀，並確保其正常運行。

另請參閱 [編輯查看器預設](/help/assets/managing-viewer-presets.md#editing-viewer-presets)。

如果您對360視頻滿意，可以發佈該視頻。

請參閱 [將視頻或影像查看器嵌入網頁](/help/assets/embed-code.md)。
請參閱 [將URL連結到Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md)。 如果您的交互內容具有與相對URL的連結，特別是與Experience Manager Sites頁面的連結，則無法使用基於URL的連結方法。
請參閱 [將Dynamic Media資產添加到頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

**預覽360視頻：**

1. 在 **[!UICONTROL 資產]**，導航到您建立的現有360視頻。 選擇「360視頻」資產，以便可以在預覽模式下開啟它。

   ![6_5_360視頻選擇預覽–1](assets/6_5_360video-selecttopreview-1.png)

   選擇360視頻資產，以便預覽視頻。

1. 在預覽頁面的左上角附近，選擇下拉清單，然後選擇 **[!UICONTROL 查看者]**。

   ![6_5_360視頻預覽 — 查看器](assets/6_5_360video-preview-viewers.png)

   從「查看者」清單中，選擇 **[!UICONTROL Video360_social]**，然後執行以下操作之一：

   * 如果要更改靜態場景的視角，請將滑鼠指針拖過視頻。
   * 選擇視頻 **[!UICONTROL 播放]** 按鈕。 播放視頻時，將滑鼠指針拖過視頻以改變視角。

   ![地球和太陽背景漂浮在外層空間的國際空間站螢幕截圖&#x200B;](assets/6_5_360video-preview-video360-social.png)*一個360視頻螢幕截圖。*

   * 從「查看者」清單中，選擇 **[!UICONTROL Video360VR]**。

      虛擬現實(VR)視頻是使用虛擬現實耳機訪問的沈浸式視頻內容。 與普通視頻一樣，在開始錄制或使用360度攝像機捕獲視頻時，您會建立VR視頻。
   ![一個螢幕截圖，顯示在外太空漂浮的國際空間站的特寫，背景中部分可以看到地球和太陽](assets/6_5_360video-preview-video360vr.png)
   *360 VR視頻螢幕截圖*

1. 在預覽頁面右上角附近，選擇 **[!UICONTROL 關閉]**。

## 發佈360視頻 {#publishing-video}

發佈360視頻，以便您使用。 發佈360視頻會激活URL和嵌入代碼。 它還將360視頻發佈到Dynamic Media雲，該雲與CDN整合，可進行可擴展和效能交付。

請參閱 [發佈Dynamic Media資產](/help/assets/publishing-dynamicmedia-assets.md) 有關如何發佈360視頻的詳細資訊。
另請參閱 [將視頻或影像查看器嵌入網頁](/help/assets/embed-code.md)。
另請參閱 [將URL連結到Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md)。 如果您的交互內容具有與相對URL的連結，特別是與Experience Manager Sites頁面的連結，則無法使用基於URL的連結方法。
另請參閱 [將Dynamic Media資產添加到頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)。
