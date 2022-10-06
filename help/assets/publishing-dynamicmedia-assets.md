---
title: 發佈Dynamic Media Assets
description: 如何發佈Dynamic Media資產
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publishing
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 3%

---

# 發佈Dynamic Media資產 {#publishing-dynamic-media-assets}

您可以選取已上傳的資產並點選，以發佈Dynamic Media資產 **[!UICONTROL 發佈]** 或 **[!UICONTROL 快速發佈]**. 發佈Dynamic Media資產後，您就可以透過URL或將程式碼嵌入頁面，將其加入網頁。

您也可以立即發佈上傳的資產，不需任何使用者干預。 請參閱 [設定Dynamic Media - Scene7模式](config-dms7.md).
或者，您可以選擇性地將資產發佈至Dynamic Media或Adobe Experience Manager，彼此互斥，使用 **[!UICONTROL 選擇性發佈]** 在資料夾層級。 請參閱 [在Dynamic Media中使用選擇性發佈](/help/assets/selective-publishing.md).

在 **[!UICONTROL 卡片檢視]**，資產名稱正下方以及日期與時間左側會顯示一個小型全球圖示，以指出資產已發佈。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

>[!NOTE]
>
>如果資產已發佈，請使用Experience Manager將資產移至其他資料夾，然後從其新位置重新發佈。 仍可使用原始發佈的資產位置，以及新重新發佈的資產。 但原始已發佈的資產「遺失」至Experience Manager，無法取消發佈。 因此，最佳作法是先取消發佈資產，再將其移至其他資料夾。

如果您想在對視訊資產進行編碼後立即發佈，請確定已完成編碼。 在對視訊進行編碼時，系統可讓您知道視訊處理工作流程正在進行中。 完成視訊編碼時，您可以預覽視訊轉譯。 此時，您就可以安全地發佈視訊，而不會發生任何發佈錯誤。

另請參閱 [將URL連結至您的Web應用程式](linking-urls-to-yourwebapplication.md).

另請參閱 [將Dynamic Media視訊或影像檢視器內嵌在網頁上](embed-code.md)

>[!NOTE]
>
>* 必須發佈資產才能使用URL。 如果資產未發佈，則複製URL及將其貼入網頁瀏覽器無法運作。
>* 必須啟用並發佈影像預設集和檢視器預設集，才能即時傳送。
>


如需發佈集或資產的詳細資訊，請參閱 [發佈資產](manage-assets.md).

## HTTP/2傳送Dynamic Media資產 {#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援透過HTTP/2傳送所有Dynamic Media內容（影像和影片）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可與接受託管資產的任何應用程式整合。 然後會透過HTTP/2通訊協定來傳送已發佈的資產。 此傳遞方法可改善瀏覽器和伺服器通訊的方式，讓所有Dynamic Media資產的回應和載入時間都更佳。

若要進一步了解，請參閱 [HTTP/2傳送內容常見問題](/help/sites-administering/scene7-http2faq.md).
