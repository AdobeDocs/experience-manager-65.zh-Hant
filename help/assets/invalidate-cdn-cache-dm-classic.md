---
title: 透過Dynamic Media Classic使內容傳遞網路快取失效
description: 使CDN （內容傳遞網路）快取內容失效可讓您快速更新Dynamic Media Classic所傳遞的資產，而不是等候快取過期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDN Cache,Dynamic Media Classic
role: User, Admin
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 13%

---

# 透過Dynamic Media Classic使內容傳遞網路快取失效 {#invalidating-your-cdn-cached-content}

CDN （內容傳遞網路）會快取Dynamic Media資產，以快速遞送。 不過，當您更新資產時，希望這些變更立即生效。 使CDN快取內容失效可讓您快速更新Dynamic Media傳送的資產，而不是等候快取過期。

>[!NOTE]
>
>此功能需要您使用Adobe Experience Manager Dynamic Media隨附的現成可用CDN。 此功能不支援任何其他自訂CDN。

>[!IMPORTANT]
>
>下列步驟僅適用於Adobe Experience Manager 6.5 Service Pack 5 (Experience Manager6.5.5)或更舊版本中的Dynamic Media。<br>如果您在Experience Manager6.5、Service Pack 6 (Experience Manager6.5.6)或更新版本中使用Dynamic Media，請依照[透過Dynamic Media使CDN快取失效](/help/assets/invalidate-cdn-cache-dynamic-media.md)中的步驟操作。

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**透過Dynamic Media Classic使CDN快取失效：**

1. 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=zh-Hant#system-requirements-dmc-app)，然後登入您的帳戶。

   您的認證和登入是由Adobe在布建時提供的。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 在頁面的右上角附近，瀏覽至&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**。
1. 在「應用程式一般設定」頁面的「伺服器」群組標題下，找到&#x200B;**[!UICONTROL CDN失效範本]**&#x200B;文字方塊。

1. 指定用來讓CDN （內容傳遞網路）快取失效的範本。

   例如，假設您輸入參照`<ID>`的影像URL （包括影像預設集或修飾元），而不是如以下範例所示輸入特定的影像ID：

   `https://server.com/is/image/Company/<ID>?$product$`

   如果範本僅包含`<ID>`，則Dynamic Media會填入`https://<server>/is/image`，其中`<server>`為一般設定中定義的Publish伺服器名稱，而&lt;ID>為選取要失效的資產。

1. 在頁面的右下角，選取&#x200B;**[!UICONTROL 關閉]**。
1. 在Dynamic Media Classic使用者介面中，選取一或多個資產，然後前往&#x200B;**[!UICONTROL 檔案]** > **[!UICONTROL 使CDN失效]**。 您會看到從您建立的範本和您選取的資產產生的一或多個URL清單。 它會使用「應用程式一般設定」下「已發佈的伺服器名稱」下列出的伺服器URL。

   例如，在上一步中設定CDN失效範本，假設您選取了名為`Backpack_B`的單一影像資產影像。 當您移至&#x200B;**[!UICONTROL 檔案]** > **[!UICONTROL 使CDN]**&#x200B;失效時，會在CDN失效使用者介面中產生下列產生的URL：

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在URL清單方塊中，選取&#x200B;**[!UICONTROL 繼續]**&#x200B;以清除每個特定URL的快取。 您可以編輯URL，也可以輸入URL或將其貼到URL清單方塊中來新增URL；您不需要事先設定「CDN失效範本」。

   選取&#x200B;**[!UICONTROL 繼續]**&#x200B;之後，會顯示指示器，提供清除快取所需的預估時間。

   如果您選取多個資產，則前往「**[!UICONTROL 檔案]** > **[!UICONTROL 使CDN失效]**」，每個資產都會在儲存的「**[!UICONTROL 範本URL]**」中參考。 因此，您可以定義&#x200B;**[!UICONTROL CDN無效範本]**，以參考網站上參考的每個URL影像預設集（例如產品詳細資料和搜尋結果）。 然後，當您從快取中選取一或影像以進行失效時，URL會自動填入介面。

   >[!NOTE]
   >
   >當您選取資產，然後前往「**[!UICONTROL 檔案]** > **[!UICONTROL 使CDN無效]**」時，Dynamic Media會使用無效的CDN範本，自動建立要使內容傳遞網路(CDN)無效的URL。 如果「 **[!UICONTROL CDN失效範本」文字方塊中沒有任何項目]** ，則會顯示空白的URL清單。CDN的快取並非以資產為基礎；它是以URL為基礎。因此，您必須注意您網站上的完整URL。在您決定這些URL後，可以在步驟的前面將它們新 **[!UICONTROL 增至「使CDN範本無效]** 」文字方塊。然後，您可以選取這些資產，並在單一步驟中使URL無效。
   >
   >另一個選項是將完整的URL新增到&#x200B;**[!UICONTROL 使CDN]**&#x200B;無效。 如果您依照這個方法，在移至&#x200B;**[!UICONTROL 檔案>使CDN]**&#x200B;無效之前，不必在Dynamic Media Classic中選取資產。
