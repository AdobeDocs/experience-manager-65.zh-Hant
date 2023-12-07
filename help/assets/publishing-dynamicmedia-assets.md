---
title: 發佈Dynamic Media資產
description: 瞭解如何發佈Dynamic Media資產（例如影片和影像），包括此類資產的HTTP/2傳送。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publishing
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 4%

---

# 發佈 Dynamic Media 資產 {#publishing-dynamic-media-assets}

選取您已上傳的資產並點選，即可發佈您的Dynamic Media資產 **[!UICONTROL 發佈]** 或 **[!UICONTROL 快速發佈]**. 發佈Dynamic Media資產後，您就可以透過URL或內嵌程式碼至網頁，將資產加入網頁。

您也可立即發佈您上傳的資產，無需任何使用者介入。 另請參閱 [設定Dynamic Media - Scene7模式](config-dms7.md).
或者，您可以選擇將資產發佈至Dynamic Media或Adobe Experience Manager （兩者互斥），使用 **[!UICONTROL 選擇性發佈]** 在資料夾層級。 另請參閱 [在Dynamic Media中使用選擇性發佈](/help/assets/selective-publishing.md).

在 **[!UICONTROL 卡片檢視]**，資產名稱的正下方以及日期和時間左側會顯示一個小型全球圖示，以指出資產已發佈。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

>[!NOTE]
>
>如果資產已發佈，請使用Experience Manager將資產移至另一個檔案夾，然後從新位置重新發佈。 仍可使用原始發佈的資產位置，以及新重新發佈的資產。 然而，原始發佈的資產會因Experience Manager「遺失」而無法取消發佈。 因此，最佳做法是先取消發佈資產，然後再將其移至其他資料夾。

如果您打算在編碼視訊資產後立即發佈，請務必完成編碼。 當視訊編碼時，系統會告知您視訊處理工作流程正在進行中。 視訊編碼完成後，您可以預覽視訊轉譯。 如此一來，您就可以安全地發佈影片，而不會發生任何發佈錯誤。

另請參閱 [將URL連結至您的網頁應用程式](linking-urls-to-yourwebapplication.md).

另請參閱 [將Dynamic Media影片或影像檢視器內嵌在網頁上](embed-code.md)

>[!NOTE]
>
>* 必須發佈資產才能使用URL。 如果資產未發佈，將無法將URL複製並貼到網頁瀏覽器。
>* 影像預設集和檢視器預設集必須啟動並發佈，才能即時傳送。
>

如需發佈集合或資產的詳細資訊，請參閱 [發佈資產](manage-assets.md).

## Dynamic Media資產的HTTP/2傳送 {#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援透過HTTP/2傳送所有Dynamic Media內容（影像和視訊）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可整合至任何接受託管資產的應用程式。 該已發佈資產隨後會透過HTTP/2通訊協定傳送。 此傳送方式可改善瀏覽器和伺服器的通訊方式，讓您的所有Dynamic Media資產獲得更好的回應和載入時間。

若要深入瞭解，請參閱 [HTTP/2內容傳送常見問答](/help/sites-administering/scene7-http2faq.md).
