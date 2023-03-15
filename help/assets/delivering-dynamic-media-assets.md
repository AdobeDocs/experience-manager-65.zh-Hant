---
title: 傳遞 Dynamic Media 資產
description: 了解如何傳送Dynamic Media資產
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 13%

---

# 傳遞 Dynamic Media 資產{#delivering-dynamic-media-assets}

如何傳送Dynamic Media資產（包括視訊和影像）取決於網站的實作方式。

有了Dynamic Media，您有數個選項：

* 如果您的網站托管於Adobe Experience Manager，則您想要直接將Dynamic Media資產新增至頁面。
* 如果您的網站未Experience Manager，您可以選擇：

   * 將您的視訊或影像嵌入網站。
   * 將 URL 連結至您的網頁應用程式. 當您想要以快顯視窗或強制回應視窗的形式傳送視訊播放器時，請使用連結。
   * 如果您的網站回應式，您可以 [傳遞最佳化的影像](/help/assets/responsive-site.md).

>[!NOTE]
>
>智慧型影像處理可與您現有的影像預設集搭配使用，並會在傳送時的最後毫秒內運用智慧，根據瀏覽器或網路連線速度進一步縮小影像檔案大小。 請參閱 [智慧型影像](/help/assets/imaging-faq.md) 以取得更多資訊。

如需詳細資訊，請參閱下列主題：

* [將Dynamic Media資產新增至網頁](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md)
* [在 Dynamic Media 中啟動直接連結保護](/help/assets/hotlink-protection.md)
* [將 URL 連結至您的網頁應用程式](/help/assets/linking-urls-to-yourwebapplication.md)
* [為回應式網站傳遞最佳化影像](/help/assets/responsive-site.md)
* [HTTP2 傳送內容](/help/assets/http2.md)
* [透過Dynamic Media Classic使您的CDN快取失效](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [使用規則集轉換 URL](/help/assets/using-rulesets-to-transform-urls.md)


## HTTP/2傳送Dynamic Media資產 {#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援透過HTTP/2傳送所有Dynamic Media內容（影像和影片）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可與接受託管資產的任何應用程式整合。 然後會透過HTTP/2通訊協定來傳送已發佈的資產。 此傳遞方法可改善瀏覽器和伺服器通訊的方式，讓所有Dynamic Media資產的回應和載入時間都更佳。

若要進一步了解，請參閱 [HTTP/2傳送內容常見問題](/help/sites-administering/scene7-http2faq.md).
