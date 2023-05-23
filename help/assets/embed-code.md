---
title: 將Dynamic Media視頻、影像查看器或維查看器嵌入網頁
description: 瞭解如何在網頁上嵌入Dynamic Media視頻、影像或3D影像
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
feature: Viewers
role: User, Admin
exl-id: 203ea349-ef4c-421c-b4b6-76ee9d46ec34
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 21%

---

# 將Dynamic Media視頻、影像查看器或維查看器嵌入網頁 {#embedding-the-video-or-image-viewer-on-a-web-page}

當您想 **** 要播放視訊或檢視內嵌在網頁上的資產時，請使用「內嵌代碼」功能。您可將內嵌代碼複製到剪貼簿，以便貼到網頁中。「內嵌代碼」對話方塊中不允許編 **[!UICONTROL 輯代碼]** 。

只有在以下情況下才嵌入URL *不* 用Adobe Experience Manager做WCM 如果你用Experience Manager做WCM, [您直接將資產添加到頁面](adding-dynamic-media-assets-to-pages.md)。

請參閱 [將URL連結到Web應用程式](linking-urls-to-yourwebapplication.md)。

請參閱 [為響應性站點提供優化的映像](responsive-site.md)。

>[!NOTE]
>
>在您發佈所選資產之前，嵌入代碼不可複製。 此外，還必須發佈查看器預設或影像預設。
>
>請參閱 [發佈資產](publishing-dynamicmedia-assets.md)。
>
>請參閱 [發佈查看器預設](managing-viewer-presets.md#publishing-viewer-presets)。
>
>請參閱 [發佈影像預設](managing-image-presets.md#publishing-image-presets)。

**要在網頁上嵌入Dynamic Media視頻、影像查看器或維查看器：**

1. 導航到 *出版* 要複製其嵌入代碼的視頻或影像資產。

   請記住，內嵌程式碼僅可在您首次 *發佈**資產後* 複製。此外，檢視器預設集或影像預設集也必須發佈。

   請參閱 [發佈資產](publishing-dynamicmedia-assets.md)。

   請參閱 [發佈查看器預設](managing-viewer-presets.md#publishing-viewer-presets)。

   請參閱 [發佈影像預設](managing-image-presets.md#publishing-image-presets)。

1. 在左滑軌中，選擇下拉菜單並選擇 **[!UICONTROL 查看者]**。
1. 在左滑軌中，選擇查看器預設名稱。 將查看器預設應用於資產。
1. 選擇 **[!UICONTROL 嵌入]**。
1. 在 **[!UICONTROL 嵌入代碼]** 對話框，將整個代碼複製到剪貼簿，然後選擇 **[!UICONTROL 關閉]**。
1. 將嵌入代碼貼上到網頁中。

## 使用HTTP/2傳遞您的Dynamic Media資產 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web協定，它改進了瀏覽器和伺服器的通信方式。 它提供了更快的資訊傳輸，並減少了所需的處理能力。 Dynamic Media資產的交付現在可以通過HTTP/2，從而提供更好的響應和載入時間。

請參閱 [HTTP2內容傳遞](http2.md) 有關使用HTTP/2和您的Dynamic Media帳戶入門的完整詳細資訊。
