---
title: 將Dynamic Media視訊、影像檢視器或維度檢視器內嵌在網頁上
description: 瞭解如何將動態媒體影片、影像或3D影像內嵌在網頁上
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Viewers
role: User, Admin
exl-id: 203ea349-ef4c-421c-b4b6-76ee9d46ec34
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: d17d085a-e808-49dd-b9a6-85a996b999bd
    internal-label: Viewers
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 20%
---
# 將Dynamic Media視訊、影像檢視器或維度檢視器內嵌在網頁上 {#embedding-the-video-or-image-viewer-on-a-web-page}

當您想 **&#x200B;**&#x200B;要播放視訊或檢視嵌入在網頁上的資產時，請使用「嵌入代碼」功能。 您可將嵌入代碼複製到剪貼簿，以便貼到網頁中。 「嵌入代碼」對話方塊中不允許編 **[!UICONTROL 輯代碼]** 。

只有在您&#x200B;*不是*&#x200B;使用Adobe Experience Manager做為WCM時才內嵌URL。 如果您使用Experience Manager做為WCM，[請直接在頁面上新增資產](adding-dynamic-media-assets-to-pages.md)。

檢視[將URL連結至您的網頁應用程式](linking-urls-to-yourwebapplication.md)。

請參閱[傳送回應式網站的最佳化影像](responsive-site.md)。

>[!NOTE]
>
>您必須先發佈選取的資產，才能複製內嵌程式碼。 此外，您也必須發佈檢視器預設集或影像預設集。
>
>請參閱[發佈資產](publishing-dynamicmedia-assets.md)。
>
>請參閱[發佈檢視器預設集](managing-viewer-presets.md#publishing-viewer-presets)。
>
>請參閱[發佈影像預設集](managing-image-presets.md#publishing-image-presets)。

**若要將Dynamic Media視訊、影像檢視器或維度檢視器內嵌在網頁上：**

1. 導覽至您要複製其內嵌程式碼的&#x200B;*已發佈*&#x200B;視訊或影像資產。

   請記住，嵌入程式碼僅可在您首次 *發佈**資產後* 複製。 此外，檢視器預設集或影像預設集也必須發佈。

   請參閱[發佈資產](publishing-dynamicmedia-assets.md)。

   請參閱[發佈檢視器預設集](managing-viewer-presets.md#publishing-viewer-presets)。

   請參閱[發佈影像預設集](managing-image-presets.md#publishing-image-presets)。

1. 在左側邊欄中，選取下拉式功能表，然後選取&#x200B;**[!UICONTROL 檢視器]**。
1. 在左側欄中，選取檢視器預設集名稱。 檢視器預設集已套用至資產。
1. 選取&#x200B;**[!UICONTROL 內嵌]**。
1. 在&#x200B;**[!UICONTROL 內嵌程式碼]**&#x200B;對話方塊中，將整個程式碼複製到剪貼簿，然後選取&#x200B;**[!UICONTROL 關閉]**。
1. 將內嵌程式碼貼入您的網頁。

## 使用HTTP/2傳送您的Dynamic Media資產 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供更快速的資訊傳輸，並減少所需的處理能力。 Dynamic Media資產的傳送現在可透過HTTP/2進行，以提供更理想的回應和載入時間。

請參閱[HTTP2內容傳送](http2.md)，以取得有關透過您的Dynamic Media帳戶開始使用HTTP/2的完整詳細資料。
