---
title: 發佈Dynamic Media Assets
description: 如何發佈Dynamic Media資產
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
role: Business Practitioner, Administrator
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: 發佈
source-git-commit: 99230f2b9ce8179de4034d8bd739a5535b2cc0da
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 3%

---

# 發佈Dynamic Media資產{#publishing-dynamic-media-assets}

您可以選取已上傳的資產，然後點選&#x200B;**[!UICONTROL Publish]**&#x200B;或&#x200B;**[!UICONTROL Quick Publish]**，以發佈Dynamic Media資產。 發佈Dynamic Media資產後，您就可以透過URL或將程式碼嵌入頁面，將其加入網頁。

您也可以立即發佈上傳的資產，不需任何使用者干預。 請參閱[設定Dynamic Media - Scene7模式](config-dms7.md)。
或者，您可以使用資料夾層級的**[!UICONTROL 選擇性發佈]**，選擇性地將資產發佈至彼此互斥的Dynamic Media或AEM。 請參閱[在Dynamic Media中使用選擇性發佈](/help/assets/selective-publishing.md)。

在&#x200B;**[!UICONTROL 卡片檢視]**&#x200B;中，資產名稱正下方以及日期與時間左側會顯示一個小型全球圖示，以指出資產已發佈。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

>[!NOTE]
>
>如果資產已發佈，則您可以使用AEM將資產移至其他資料夾，然後從新位置重新發佈，仍可使用原始發佈的資產位置，以及新重新發佈的資產。 但原始已發佈資產「遺失」至AEM，無法取消發佈。 因此，最佳作法是先取消發佈資產，再將其移至其他資料夾。

如果您想在對視訊資產進行編碼後立即發佈，請確定編碼已完成。 當視訊仍在編碼時，系統可讓您知道視訊處理工作流程正在進行中。 完成視訊編碼後，您應該可以預覽視訊轉譯。 此時，您就可以安全地發佈視訊，而不會發生任何發佈錯誤。

另請參閱[將URL連結到Web應用程式](linking-urls-to-yourwebapplication.md)。

另請參閱[將Dynamic Media視訊或影像檢視器內嵌在網頁上](embed-code.md)

>[!NOTE]
>
>* 必須發佈資產才能使用URL。 如果資產未發佈，則複製URL並貼入網頁瀏覽器將無法運作。
>* 必須啟用並發佈影像預設集和檢視器預設集，才能即時傳送。

>



如需發佈集或資產的詳細資訊，請參閱[發佈資產](manage-assets.md)。

## HTTP/2傳送Dynamic Media資產{#http-delivery-of-dynamic-media-assets}

AEM現在支援透過HTTP/2傳送所有Dynamic Media內容（影像和影片）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可與接受託管資產的任何應用程式整合。 然後會透過HTTP/2通訊協定來傳送已發佈的資產。 此傳遞方法可改善瀏覽器和伺服器通訊的方式，讓所有Dynamic Media資產的回應和載入時間都更佳。

請參閱[HTTP/2傳送內容常見問題](/help/sites-administering/scene7-http2faq.md)以深入了解。
