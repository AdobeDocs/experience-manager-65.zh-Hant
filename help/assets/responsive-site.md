---
title: 為回應式網站傳送最佳化影像
description: 如何使用回應式程式碼功能來傳送最佳化的影像
uuid: 7c6baef5-7513-4644-94ed-2383e8724c17
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5edcc765-c374-4368-a0d9-e02a713a24f2
feature: Asset Management
role: User, Admin
exl-id: 753d806f-5f44-4d73-a3a3-a2a0fc3e154b
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 12%

---

# 為回應式網站傳遞最佳化影像 {#delivering-optimized-images-for-a-responsive-site}

當您想要與網頁開發人員共用程式碼以進行回應式服務時，請使用回應式程式碼功能。 您複製回應式(**[!UICONTROL RESS]**)程式碼，以便與網頁開發人員共用。

如果您的網站位於協力廠商WCM，則使用此功能有意義。 不過，如果您的網站改用Adobe Experience Manager,Offsite影像伺服器會轉譯影像並提供給網頁。

另請參閱 [將視訊檢視器內嵌在網頁上](embed-code.md).

另請參閱 [將URL連結至您的Web應用程式](linking-urls-to-yourwebapplication.md).

**若要為回應式網站提供最佳化的影像：**

1. 導覽至您要為提供回應式程式碼的影像，然後在下拉式功能表中選取 **[!UICONTROL 轉譯]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. 選取回應式影像預設集。URL **[!UICONTROL 和]****[!UICONTROL RESS]** 按鈕出現。

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >必須發佈 *選取的資產* ，以及選取的影像預設集或檢視器預設集，才能使 **[!UICONTROL URL]** 或 **[!UICONTROL RESS]** 按鈕可用。
   >
   >Dynamic Media — 混合模式需要您發佈影像預設集；Dynamic Media - Scene7模式會自動發佈影像預設集。

1. 選擇 **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. 在 **[!UICONTROL 內嵌回應式影像]** 對話方塊，選取並複製回應式程式碼文字，然後貼到您的網站以存取回應式資產。
1. 編輯內嵌程式碼中的預設中斷點，以直接在程式碼中符合回應式網站的中斷點。 此外，測試在不同頁面斷點處提供的不同影像解析度。

## 使用HTTP/2來傳送Dynamic Media資產 {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2是全新、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供了更快的資訊傳輸，並降低了所需的處理能力。 支援使用HTTP/2來傳送Dynamic Media資產，以提供更理想的回應和載入時間。

請參閱 [HTTP2內容傳送](http2.md) 如需開始使用HTTP/2搭配您的Dynamic Media帳戶的完整詳細資訊。
