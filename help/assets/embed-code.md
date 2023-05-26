---
title: 將Dynamic Media視訊、影像檢視器或維度檢視器內嵌在網頁上
description: 瞭解如何在網頁上內嵌Dynamic Media影片、影像或3D影像
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

# 將Dynamic Media視訊、影像檢視器或維度檢視器內嵌在網頁上 {#embedding-the-video-or-image-viewer-on-a-web-page}

當您想 **** 要播放視訊或檢視內嵌在網頁上的資產時，請使用「內嵌代碼」功能。您可將內嵌代碼複製到剪貼簿，以便貼到網頁中。「內嵌代碼」對話方塊中不允許編 **[!UICONTROL 輯代碼]** 。

只有當您符合以下條件時，才可內嵌URL： *not* 使用Adobe Experience Manager做為WCM。 如果您使用Experience Manager做為WCM， [您直接在頁面上新增資產](adding-dynamic-media-assets-to-pages.md).

另請參閱 [將URL連結至您的網頁應用程式](linking-urls-to-yourwebapplication.md).

另請參閱 [為回應式網站傳送最佳化的影像](responsive-site.md).

>[!NOTE]
>
>您必須發佈選取的資產，才能複製內嵌程式碼。 此外，您也必須發佈檢視器預設集或影像預設集。
>
>另請參閱 [發佈資產](publishing-dynamicmedia-assets.md).
>
>另請參閱 [發佈檢視器預設集](managing-viewer-presets.md#publishing-viewer-presets).
>
>另請參閱 [發佈影像預設集](managing-image-presets.md#publishing-image-presets).

**若要將Dynamic Media視訊、影像檢視器或維度檢視器內嵌在網頁上：**

1. 導覽至 *已發佈* 您要複製其內嵌程式碼的視訊或影像資產。

   請記住，內嵌程式碼僅可在您首次 *發佈**資產後* 複製。此外，檢視器預設集或影像預設集也必須發佈。

   另請參閱 [發佈資產](publishing-dynamicmedia-assets.md).

   另請參閱 [發佈檢視器預設集](managing-viewer-presets.md#publishing-viewer-presets).

   另請參閱 [發佈影像預設集](managing-image-presets.md#publishing-image-presets).

1. 在左側欄中，選取下拉式功能表並選取 **[!UICONTROL 檢視者]**.
1. 在左側欄中，選取檢視器預設集名稱。 檢視器預設集已套用至資產。
1. 選取 **[!UICONTROL 內嵌]**.
1. 在 **[!UICONTROL 內嵌程式碼]** 對話方塊中，將整個程式碼複製到剪貼簿，然後選取 **[!UICONTROL 關閉]**.
1. 將內嵌程式碼貼入您的網頁。

## 使用HTTP/2傳遞您的Dynamic Media資產 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供更快速的資訊傳輸，並減少所需的處理能力。 Dynamic Media資產的傳送現在可透過HTTP/2進行，以提供更佳的回應和載入時間。

另請參閱 [HTTP2傳送內容](http2.md) 以取得開始使用HTTP/2與Dynamic Media帳戶的完整詳細資訊。
