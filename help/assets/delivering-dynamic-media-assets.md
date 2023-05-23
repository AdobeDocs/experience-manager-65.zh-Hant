---
title: 傳遞 Dynamic Media 資產
description: 瞭解如何交付Dynamic Media資產
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

您如何交付您的Dynamic Media資產 — 包括視頻和影像 — 取決於您網站的實施方式。

對於Dynamic Media，你有幾種選擇：

* 如果您的網站位於Adobe Experience Manager，則您希望將Dynamic Media資產直接添加到您的頁面。
* 如果您的網站未Experience Manager，則您可以選擇：

   * 將視頻或影像嵌入到您的網站。
   * 將 URL 連結至您的網頁應用程式. 當要將視頻播放器作為彈出窗口或模式窗口傳送時，請使用連結。
   * 如果您的站點響應迅速，您可以 [提供優化的映像](/help/assets/responsive-site.md)。

>[!NOTE]
>
>智慧成像可與您現有的影像預設配合使用，並在傳輸的最後一毫秒使用智慧功能，以根據瀏覽器或網路連接速度進一步減小影像檔案大小。 請參閱 [智慧映像](/help/assets/imaging-faq.md) 的子菜單。

有關詳細資訊，請參閱以下主題：

* [將Dynamic Media資產添加到網頁](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [將視頻或影像查看器嵌入網頁](/help/assets/embed-code.md)
* [在 Dynamic Media 中啟動直接連結保護](/help/assets/hotlink-protection.md)
* [將 URL 連結至您的網頁應用程式](/help/assets/linking-urls-to-yourwebapplication.md)
* [為回應式網站傳遞最佳化影像](/help/assets/responsive-site.md)
* [HTTP2 傳送內容](/help/assets/http2.md)
* [通過Dynamic Media Classic使CDN快取無效](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [使用規則集轉換 URL](/help/assets/using-rulesets-to-transform-urls.md)


## HTTP/2交付Dynamic Media資產 {#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援通過HTTP/2傳遞所有Dynamic Media內容（影像和視頻）。 即，可將影像或視頻的已發佈URL或嵌入代碼與接受託管資產的任何應用程式整合。 然後，該已發佈資產將通過HTTP/2協定交付。 這種傳送方法改進了瀏覽器和伺服器之間的通信方式，使您的所有Dynamic Media資產都能得到更好的響應和載入時間。

要瞭解更多資訊，請參閱 [HTTP/2傳遞內容常見問題](/help/sites-administering/scene7-http2faq.md)。
