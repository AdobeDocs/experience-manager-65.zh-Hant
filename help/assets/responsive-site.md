---
title: 為響應性站點提供優化的映像
description: 如何使用響應代碼功能來提供優化的影像
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

當您希望與Web開發人員共用代碼以響應服務時，請使用響應代碼功能。 您複製響應(**[!UICONTROL RESS]**)的代碼，以便您可以與Web開發人員共用。

如果您的網站位於第三方WCM上，則使用此功能是有意義的。 但是，如果您的網站位於Adobe Experience Manager，則非現場映像伺服器將呈現該映像並將其提供到網頁。

另請參閱 [將視頻查看器嵌入網頁](embed-code.md)。

另請參閱 [將URL連結到Web應用程式](linking-urls-to-yourwebapplication.md)。

**為響應性站點提供優化的映像：**

1. 導航到要為其提供響應代碼的影像，並在下拉菜單中選擇 **[!UICONTROL 格式副本]**。

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. 選取回應式影像預設集。URL **[!UICONTROL 和]****[!UICONTROL RESS]** 按鈕出現。

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >必須發佈 *選取的資產* ，以及選取的影像預設集或檢視器預設集，才能使 **[!UICONTROL URL]** 或 **[!UICONTROL RESS]** 按鈕可用。
   >
   >Dynamic Media — 混合模式要求您發佈影像預設；Dynamic Media-Scene7模式自動發佈影像預設。

1. 選擇 **[!UICONTROL RESS]**。

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. 在 **[!UICONTROL 嵌入響應影像]** 對話框，選擇並複製響應代碼文本，然後將其貼上到網站中以訪問響應資產。
1. 編輯嵌入代碼中的預設斷點，以與響應網站的斷點匹配，直接在代碼中。 另外，test在不同頁面斷點處提供的不同影像解析度。

## 使用HTTP/2交付您的Dynamic Media資產 {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2是新的、更新的Web協定，它改進了瀏覽器和伺服器的通信方式。 它提供了更快的資訊傳輸，並減少了所需的處理能力。 使用HTTP/2支援Dynamic Media資產的交付，因為HTTP/2提供了更好的響應和載入時間。

請參閱 [HTTP2內容傳遞](http2.md) 有關使用HTTP/2和您的Dynamic Media帳戶入門的完整詳細資訊。
