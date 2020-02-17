---
title: 發佈動態媒體資產
description: 如何發佈動態媒體資產
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 發佈動態媒體資產 {#publishing-dynamic-media-assets}

您可以選取資產並點選「發佈」，以發佈您的動態 **[!UICONTROL 媒體資產]**。 發佈動態媒體資產後，您就可透過URL或內嵌方式，將其加入網頁。

您也可以立即發佈上傳的資產，不需任何使用者干預。 請參 [閱設定動態媒體- Scene7模式](config-dms7.md)。

在「資 **[!UICONTROL 訊卡檢視]**」中，資產名稱正下方會顯示一個小型全球圖示，以指出資產已發佈。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

>[!NOTE]
>
>如果資產已發佈，則您會使用AEM將資產移至另一個檔案夾，並從其新位置重新發佈，則原始發佈的資產位置仍可使用，以及新重新發佈的資產。 不過，原始發佈的資產會「遺失」至AEM，無法解除發佈。 因此，在將資產移至其他資料夾之前，請先解除發佈資產，這是最佳作法。

如果您想在編碼後立即發佈視訊資產，請確定已完成編碼。 當視訊仍在編碼時，系統會讓您知道視訊處理工作流程正在進行中。 完成視訊編碼後，您應該可以預覽視訊轉譯。 此時，您可以放心地發佈視訊，而不會發生任何發佈錯誤。

另請參 [閱將URL連結至您的Web應用程式](linking-urls-to-yourwebapplication.md)。

另請參 [閱將視訊檢視器內嵌在網頁上。](embed-code.md)

>[!NOTE]
>
>* 必須發佈資產才能使用URL。 如果資產未發佈，則複製URL並貼至網頁瀏覽器將無法運作。
>* 必須啟用並發佈影像預設集和檢視器預設集，才能即時傳送。
>



如需發佈集合或資產的詳細資訊，請參閱發 [布資產。](managing-assets-touch-ui.md)

## HTTP/2傳送動態媒體資產 {#http-delivery-of-dynamic-media-assets}

AEM現在支援透過HTTP/2傳送所有動態媒體內容（影像和視訊）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可與任何接受代管資產的應用程式整合。 然後，該已發佈資產會透過HTTP/2通訊協定傳送。 此傳送方式改善了瀏覽器和伺服器通訊的方式，讓您的所有動態媒體資產都能獲得較佳的回應和載入時間。

請參 [閱HTTP/2內容傳送常見問題](/help/sites-administering/scene7-http2faq.md) ，以進一步瞭解。
