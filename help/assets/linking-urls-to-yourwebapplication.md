---
title: 將 URL 連結至您的網頁應用程式
description: 如何在Dynamic Media中將URL連結至您的Web應用程式
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
role: User, Admin
exl-id: d62275f0-02a4-48c9-bfb1-e23d63b618c9
feature: Configuration
source-git-commit: 78aa7aac838dabc1c4f0329520092e4755541322
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 6%

---

# 將 URL 連結至您的網頁應用程式 {#linking-urls-to-your-web-application}

您的網站和應用程式會透過URL呼叫存取Dynamic Media服務。 發佈資產後，Dynamic Media會啟用參考資產的URL字串。 您可以將這些URL貼到網頁瀏覽器中以進行測試。

只有在 *not* 使用Experience Manager作為WCM。 當您想要以快顯視窗或強制回應視窗的形式傳送視訊播放器時，會使用連結 — 與內嵌。 如果您使用Experience Manager作為WCM, [直接在頁面上新增資產](adding-dynamic-media-assets-to-pages.md).

若要將這些URL字串放入您的網頁和應用程式中，請從Dynamic Media複製。

>[!NOTE]
>
>URL字串僅可用於資產的動態轉譯。 目前無法供存放在DAM中的靜態資產使用，無法供Dynamic Media伺服器使用。 對於靜態的轉譯，不會顯示URL按鈕。

另請參閱 [將視訊或影像檢視器內嵌在網頁上](embed-code.md).

另請參閱 [將YouTube URL連結至您的Web應用程式](video.md).

另請參閱 [為回應式網站提供最佳化的影像](responsive-site.md).

另請參閱 [上傳資產](manage-assets.md#uploading-assets).

## 取得資產的URL {#obtaining-a-url-for-an-asset}

您可以取得影像預設集或檢視器預設集產生的URL字串。 複製URL後，剪貼簿會隨即開啟，您可以視需要將其貼至網站或應用程式中的頁面。

>[!NOTE]
>
>在您發佈所選資產之前，無法複製URL。 此外，您也必須發佈檢視器預設集或影像預設集。
>
>請參閱 [發佈資產](publishing-dynamicmedia-assets.md).
>
>請參閱 [發佈檢視器預設集](managing-viewer-presets.md#publishing-viewer-presets).
>
>請參閱 [發佈影像預設集](managing-image-presets.md#publishing-image-presets).

您可透過數種不同方式取得URL字串。 不過，下列步驟只顯示一個可使用的方法。

**若要取得資產的URL:**

1. 導覽至 *已發佈* 您要複製其影像預設集URL或檢視器預設集URL的資產，然後選取要開啟的資產。

   請記住，URL僅可在您首次發 *布資產* 後 *複製* 。此外，檢視器預設集或影像預設集也必須發佈。

   請參閱 [發佈資產](publishing-dynamicmedia-assets.md).

   請參閱 [發佈檢視器預設集](managing-viewer-presets.md#publishing-viewer-presets).

   請參閱 [發佈影像預設集](managing-image-presets.md#publishing-image-presets).

1. 根據您選取的資產，執行下列其中一項操作：

   * 如果您選取了影像，請在下拉式功能表中選取 **[!UICONTROL 轉譯]**.

      在 **[!UICONTROL 動態]** 標題，選擇預設集名稱以在右框架中查看其格式副本。 如有必要，請捲動「轉譯」清單以查看「動態」標題。

      在左側邊欄底部，選取 **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * 如果您在下拉式功能表中選取回轉集、影像集、轉盤集或視訊，請選取 **[!UICONTROL 檢視器]**.

      在左側邊欄中，選取檢視器預設集名稱。 集或視訊的預覽會在個別頁面中開啟。

      在左側邊欄的底部，選取 **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. 選取文字並複製到您的網頁瀏覽器，以便預覽資產或將其新增至您的網頁內容頁面。

   若要退出URL視窗，請選取 **[!UICONTROL X]** 或選取 **[!UICONTROL 關閉]**.

## 取得靜態資產的URL {#obtaining-a-url-for-a-static-asset}

Dynamic Media支援靜態資產的傳送，除了影像和視訊，這是其他資產。 支援的靜態資產格式用於傳送，包括下列內容：

* 3D檔案
* 動畫GIF
* 音訊檔案
* CSS
* JavaScript（當貴公司設定了自己的網域時）
* PDF
* SVG
* XML
* ZIP

**若要取得靜態資產的URL:**

1. 導覽至 *已發佈* 您要複製其URL的靜態資產，然後選取要開啟的資產。

   請記住，URL僅可複製 *after* 你先 *已發佈* 靜態資產。

   請參閱 [發佈資產](publishing-dynamicmedia-assets.md).

1. 使用下列任一方法來取得已發佈靜態資產的URL:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         例如, `https://aem.com/is/content/adobe/image.gif`.
   * 選擇 **[!UICONTROL 資產]** > **[!UICONTROL 動態轉譯]**，然後選取靜態資產的動態轉譯並複製URL。

      變更複製的URL以使用 `is/content` （而非） `is/image/`.


## 取得已發佈視訊轉譯的視訊URL {#obtaining-a-video-url-for-a-published-video-rendition}

1. 在Experience Manager中，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 雲]** > **[!UICONTROL Cloud Services]**.
1. 在 **[!UICONTROL Cloud Services]** 頁面，向下捲動至 **[!UICONTROL Dynamic MediaCloud Services]** 標題，然後選取 **[!UICONTROL 顯示配置]**.
1. 在 **[!UICONTROL 可用配置]**，選取您要的設定名稱。

1. 在 **[!UICONTROL Dynamic Media Cloud設定]** 頁面下方 **[!UICONTROL 視訊服務URL]**，複製整個URL路徑。 您稍後需要在步驟中前往複製的URL路徑。

   例如，URL路徑可能顯示如下：

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (以上路徑僅為範例；它不是您複製的實際路徑。)

1. 在「 **[!UICONTROL 註冊ID]**」下方，複製ID最後一部分中找到的客戶名稱。

   例如，如果註冊ID是 `87654321|MyCompany`，客戶名稱為 `MyCompany`.

1. 在頁面左上角附近，選取 **[!UICONTROL Cloud Services]**，然後選取Experience Manager標誌並導覽至 **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 從JCR(Java™ Content Repository)下復整個視訊轉譯路徑。

   例如，視訊的轉譯路徑可能顯示如下：

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (以上路徑僅為範例；它不是您複製的實際路徑。)

1. 依下列順序排列複製的資訊，以形成完整的URL路徑：

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   例如，使用上述步驟中的範例路徑和範例客戶名稱，完整路徑會顯示如下：

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   此範例是已發佈視訊轉譯的完整視訊URL。

## 取得適用位元速率串流（DASH或HLS）的視訊URL {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. 在Experience Manager中，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 雲]** > **[!UICONTROL Cloud Services]**.
1. 在 **[!UICONTROL Cloud Services]** 頁面，向下捲動至 **[!UICONTROL Dynamic MediaCloud Services]** 標題，然後選取 **[!UICONTROL 顯示配置]**.
1. 在 **[!UICONTROL 可用配置]**，選取您要的設定名稱。
1. 在 **[!UICONTROL Dynamic MediaCloud Services設定]** 頁面，請執行下列動作：

   * 在 **[!UICONTROL 視訊服務URL]**，複製整個URL路徑。 您稍後需要這些步驟中的複製URL路徑。 例如，URL路徑可能顯示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/`

   (以上路徑僅為範例；它不是您複製的實際路徑。)

   * 在「 **[!UICONTROL 註冊ID]**」下方，複製ID最後一部分中找到的客戶名稱。您稍後需要這些步驟中複製的客戶名稱。

      例如，如果註冊ID是 `87654321|demoCo`，您複製的客戶名稱為 `demoCo`.


1. 根據您使用的視訊傳送通訊協定，複製個別的通訊協定選取器。 您稍後需要這些步驟中複製的通訊協定選取器。

   | 您使用的視訊傳送通訊協定 | 要使用的協定選擇器 |
   |---|---|
   | HTTP <br> 如果您使用HTTP（非安全視訊傳送），請務必在先前複製的視訊服務URL值中，將https變更為http。 | `public/` |
   | HTTPS | `public-ssl/` |

1. 以Experience Manager複製完整的視訊資產路徑，由Dynamic Media處理。 您稍後需要這些步驟中的此複製視訊資產路徑。

   例如：

   `/content/dam/marketing/MyVideo.mp4`

1. 合併先前複製的所有片段，依下列順序建立字串：

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   例如，使用這些步驟中範例中複製的資訊，字串會顯示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. 透過附加 `.m3u8` 到字串結尾。 例如，附加 `.m3u8` 至上一步的字串，完整URL路徑將顯示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## 使用HTTP/2傳遞Dynamic Media資產 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是全新、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供了更快的資訊傳輸，並降低了所需的處理能力。 Dynamic Media資產的傳送現在可透過HTTP/2，提供更理想的回應和載入時間。

請參閱 [HTTP2內容傳送](http2.md) 如需開始使用HTTP/2搭配您的Dynamic Media帳戶的完整詳細資訊。
