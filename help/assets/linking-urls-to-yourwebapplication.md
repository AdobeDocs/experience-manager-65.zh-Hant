---
title: 將 URL 連結至您的網頁應用程式
description: 如何將URL連結到您在Dynamic Media的Web應用程式
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

您的網站和應用程式通過URL呼叫訪問Dynamic Media服務。 發佈資產後，Dynamic Media將激活引用該資產的URL字串。 您可以將這些URL貼上到Web瀏覽器中以進行測試。

只有在您是 *不* 使用Experience Manager作為WCM。 連結 — 與嵌入 — 用於將視頻播放器作為彈出窗口或模式窗口傳送。 如果你用Experience Manager做WCM, [您直接將資產添加到頁面](adding-dynamic-media-assets-to-pages.md)。

要將這些URL字串放置到網頁和應用程式中，請從Dynamic Media複製。

>[!NOTE]
>
>URL字串僅可用於資產的動態格式副本。 它們目前不可用於駐留在DAM中的靜態資產，而不是駐留在Dynamic Media伺服器中。 「URL」按鈕不顯示靜態格式副本。

另請參閱 [將視頻或影像查看器嵌入網頁](embed-code.md)。

另請參閱 [將YouTubeURL連結到Web應用程式](video.md)。

另請參閱 [為響應性站點提供優化的映像](responsive-site.md)。

另請參閱 [上載資產](manage-assets.md#uploading-assets)。

## 獲取資產的URL {#obtaining-a-url-for-an-asset}

可以獲取由「影像預設」或「查看器預設」生成的URL字串。 複製URL後，它會降落到剪貼簿上，以便您可以根據需要貼上到網站或應用程式中的頁面。

>[!NOTE]
>
>在您發佈所選資產之前，URL不可複製。 此外，還必須發佈查看器預設或影像預設。
>
>請參閱 [發佈資產](publishing-dynamicmedia-assets.md)。
>
>請參閱 [發佈查看器預設](managing-viewer-presets.md#publishing-viewer-presets)。
>
>請參閱 [發佈影像預設](managing-image-presets.md#publishing-image-presets)。

有幾種不同的方法可獲取URL字串。 但是，下面的步驟只顯示一個可以使用的方法。

**要獲取資產的URL，請執行以下操作：**

1. 導航到 *出版* 要複製其影像預設URL或查看器預設URL的資產，然後選擇要開啟該資產。

   請記住，URL僅可在您首次發 *布資產* 後 *複製* 。此外，檢視器預設集或影像預設集也必須發佈。

   請參閱 [發佈資產](publishing-dynamicmedia-assets.md)。

   請參閱 [發佈查看器預設](managing-viewer-presets.md#publishing-viewer-presets)。

   請參閱 [發佈影像預設](managing-image-presets.md#publishing-image-presets)。

1. 根據您選擇的資產，執行以下操作之一：

   * 如果選擇了影像，請在下拉菜單中選擇 **[!UICONTROL 格式副本]**。

      在 **[!UICONTROL 動態]** 標題中，選擇一個預設名稱以在右框架中查看其格式副本。 如有必要，滾動「格式副本」清單以查看「動態」標題。

      在左滑軌底部，選擇 **[!UICONTROL URL]**。

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * 如果在下拉菜單中選擇了旋轉集、影像集、旋轉軸集或視頻，請選擇 **[!UICONTROL 查看者]**。

      在左滑軌中，選擇查看器預設名稱。 集或視頻的預覽在單獨的頁面中開啟。

      在左滑軌底部，選擇 **[!UICONTROL URL]**。

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. 選擇文本並將其複製到Web瀏覽器，以便您可以預覽資產或將其添加到Web內容頁面。

   要退出URL窗口，請選擇 **[!UICONTROL X]** 或 **[!UICONTROL 關閉]**。

## 獲取靜態資產的URL {#obtaining-a-url-for-a-static-asset}

Dynamic Media支援靜態資產的交付，這些資產不僅僅是影像和視頻。 支援的靜態資產格式用於交付，包括：

* 3D檔案
* 動畫GIF
* 音頻檔案
* CSS
* JavaScript（當公司配置了自己的域時）
* PDF
* SVG
* XML
* ZIP

**要獲取靜態資產的URL，請執行以下操作：**

1. 導航到 *出版* 要複製其URL的靜態資產，然後選擇要開啟該資產。

   請記住，URL僅可複製 *後* 你先 *出版* 靜態資產。

   請參閱 [發佈資產](publishing-dynamicmedia-assets.md)。

1. 使用下列任何方法獲取已發佈靜態資產的URL:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         比如說， `https://aem.com/is/content/adobe/image.gif`。
   * 選擇 **[!UICONTROL 資產]** > **[!UICONTROL 動態格式副本]**，然後選擇靜態資產的動態格式副本並複製URL。

      更改要使用的複製URL `is/content` 而不是 `is/image/`。


## 獲取已發佈視頻格式副本的視頻URL {#obtaining-a-video-url-for-a-published-video-rendition}

1. 在Experience Manager中，導航到 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 雲]** > **[!UICONTROL Cloud Services]**。
1. 在 **[!UICONTROL Cloud Services]** 頁面，向下滾動到 **[!UICONTROL Dynamic MediaCloud Services]** 標題，然後選擇 **[!UICONTROL 顯示配置]**。
1. 下 **[!UICONTROL 可用配置]**，選擇所需配置的名稱。

1. 在 **[!UICONTROL Dynamic Media雲設定]** 頁，下 **[!UICONTROL 視頻服務URL]**，複製整個URL路徑。 您需要在步驟的稍後部分複製URL路徑。

   例如，URL路徑可能與以下內容類似：

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (上面的路徑僅是一個示例；它不是您複製的實際路徑。)

1. 在「 **[!UICONTROL 註冊ID]**」下方，複製ID最後一部分中找到的客戶名稱。

   例如，如果註冊ID是 `87654321|MyCompany`，客戶名稱 `MyCompany`。

1. 在頁面左上角附近，選擇 **[!UICONTROL Cloud Services]**，然後選擇Experience Manager徽標並導航至 **[!UICONTROL 常規]** > **[!UICONTROL CRXDE Lite]**。
1. 從JCR（Java™內容儲存庫）中複製整個視頻格式副本路徑。

   例如，視頻的格式副本路徑可能與以下內容類似：

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (上面的路徑僅是一個示例；它不是您複製的實際路徑。)

1. 按以下順序排列複製的資訊，以便形成完整的URL路徑：

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   例如，使用上述步驟中的示例路徑和示例客戶名稱，完整路徑如下所示：

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   此示例是已發佈視頻格式副本的完整視頻URL。

## 獲取用於自適應比特率流（DASH或HLS）的視頻URL {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. 在Experience Manager中，導航到 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 雲]** > **[!UICONTROL Cloud Services]**。
1. 在 **[!UICONTROL Cloud Services]** 頁面，向下滾動到 **[!UICONTROL Dynamic MediaCloud Services]** 標題，然後選擇 **[!UICONTROL 顯示配置]**。
1. 下 **[!UICONTROL 可用配置]**，選擇所需配置的名稱。
1. 在 **[!UICONTROL Dynamic MediaCloud Services設定]** 頁，執行以下操作：

   * 下 **[!UICONTROL 視頻服務URL]**，複製整個URL路徑。 您需要稍後在這些步驟中複製的URL路徑。 例如，URL路徑可能與以下內容類似：

   `https://gateway-na.assetsadobe.com/DMGateway/`

   (上面的路徑僅是一個示例；它不是您複製的實際路徑。)

   * 在「 **[!UICONTROL 註冊ID]**」下方，複製ID最後一部分中找到的客戶名稱。您需要稍後在這些步驟中複製的客戶名稱。

      例如，如果註冊ID是 `87654321|demoCo`，您複製的客戶名稱 `demoCo`。


1. 根據您使用的視頻傳送協定，複製相應的協定選擇器。 在這些步驟後面需要複製的協定選擇器。

   | 您正在使用的視頻傳送協定 | 要使用的協定選擇器 |
   |---|---|
   | HTTP <br> 如果使用HTTP（非安全視頻傳遞），請確保在先前複製的視頻服務URL值中將https更改為http。 | `public/` |
   | HTTPS | `public-ssl/` |

1. 按照Dynamic Media的處理，以Experience Manager方式複製完整視頻資產路徑。 在以後的這些步驟中，您需要此複製的視頻資產路徑。

   例如：

   `/content/dam/marketing/MyVideo.mp4`

1. 將先前複製的所有段組合，按以下順序建立字串：

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   例如，使用這些步驟中示例中複製的資訊，字串將顯示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. 通過附加完成URL `.m3u8` 到字串的結尾。 例如，附加 `.m3u8` 到上一步的字串，完整的URL路徑將顯示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## 使用HTTP/2交付您的Dynamic Media資產 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web協定，它改進了瀏覽器和伺服器的通信方式。 它提供了更快的資訊傳輸，並減少了所需的處理能力。 Dynamic Media資產的交付現在可以通過HTTP/2，從而提供更好的響應和載入時間。

請參閱 [HTTP2內容傳遞](http2.md) 有關使用HTTP/2和您的Dynamic Media帳戶入門的完整詳細資訊。
