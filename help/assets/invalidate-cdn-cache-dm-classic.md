---
title: 透過Dynamic Media Classic使內容傳送網路快取失效
description: 使您的CDN（內容傳遞網路）快取內容失效可讓您快速更新由Dynamic Media Classic傳送的資產，而不必等待快取過期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDN Cache,Dynamic Media Classic
role: User, Admin
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
source-git-commit: b61157b0e9afa49ef72150ae0c1703a959d154be
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 13%

---

# 透過Dynamic Media Classic使內容傳送網路快取失效 {#invalidating-your-cdn-cached-content}

Dynamic Media資產由CDN（內容傳遞網路）快取，以便快速傳遞。 不過，當您更新資產時，請希望這些變更立即生效。 使CDN快取內容失效可讓您快速更新由Dynamic Media傳送的資產，而不必等待快取過期。

>[!NOTE]
>
>若要使用此功能，您必須使用隨Adobe Experience Manager Dynamic Media提供的現成可用CDN。 此功能不支援任何其他自訂CDN。

>[!IMPORTANT]
>
>下列步驟僅適用於Adobe Experience Manager 6.5、Service Pack 5(Experience Manager6.5.5)或更舊版本的Dynamic Media。<br>如果您在Experience Manager6.5、Service Pack 6(Experience Manager6.5.6)或更新版本中使用Dynamic Media，請依照 [透過Dynamic Media使CDN快取失效](/help/assets/invalidate-cdn-cache-dynamic-media.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**若要透過Dynamic Media Classic使CDN快取失效：**

1. 開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app)，然後登入您的帳戶。

   配置時Adobe提供了您的憑據和登錄。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 在頁面的右上角附近，導覽至 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**.
1. 在「應用程式一般設定」頁面的「伺服器」群組標題下，找出 **[!UICONTROL CDN失效範本]** 框。

1. 指定用於使CDN（內容傳遞網路）快取失效的範本。

   例如，假設您輸入參考的影像URL（包括影像預設集或修飾元） `<ID>`，而非下列範例中的特定影像ID:

   `https://server.com/is/image/Company/<ID>?$product$`

   如果範本僅包含 `<ID>`，則Dynamic Media填入 `https://<server>/is/image` where `<server>` 是在「一般設定」和 &lt;id> 是選取要失效的資產。

1. 在頁面的右下角，選取 **[!UICONTROL 關閉]**.
1. 在Dynamic Media Classic使用者介面中，選取一或多個資產，然後前往 **[!UICONTROL 檔案]** > **[!UICONTROL 使CDN失效]**. 您會看到從您建立的範本和您選取的資產產生的一或多個URL清單。 它使用「應用程式一般設定」下「已發佈伺服器名稱」下列的伺服器URL。

   例如，在上一個步驟中設定了「CDN失效範本」後，假設您選取了名為 `Backpack_B`. 當您前往 **[!UICONTROL 檔案]** > **[!UICONTROL 使CDN失效]**，會在CDN失效使用者介面中產生下列URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在URL清單方塊中，選取 **[!UICONTROL 繼續]** 來清除每個特定URL的快取。 您可以編輯URL，或輸入URL或貼到URL清單方塊，即可新增URL;您不需要預先設定CDN無效範本。

   選取 **[!UICONTROL 繼續]**，則會顯示指標，提供清除快取所需時間的預估值。

   如果您選取了多個資產，請前往 **[!UICONTROL 檔案]** > **[!UICONTROL 使CDN失效]**，則儲存的資產中會參照每個資產 **[!UICONTROL 範本URL]**. 因此，您可以定義 **[!UICONTROL CDN失效範本]** 參考網站上參考的每個URL影像預設集（例如產品詳細資料和搜尋結果）。 然後，當您從快取中選取一或影像以進行失效時，URL會自動填入介面。

   >[!NOTE]
   >
   >選取資產後，請前往 **[!UICONTROL 檔案]** > **[!UICONTROL 使CDN失效]**,Dynamic Media會使用無效的CDN範本，自動建立要使內容傳遞網路(CDN)無效的URL。 如果「 **[!UICONTROL CDN失效範本」文字方塊中沒有任何項目]** ，則會顯示空白的URL清單。CDN的快取並非以資產為基礎；它是以URL為基礎。因此，您必須注意您網站上的完整URL。在您決定這些URL後，可以在步驟的前面將它們新 **[!UICONTROL 增至「使CDN範本無效]** 」文字方塊。然後，您可以選取這些資產，並在單一步驟中使URL無效。
   >
   >另一個選項是將完整的URL新增至 **[!UICONTROL 使CDN失效]** 清單。 如果您依照此方法操作，則不必先在Dynamic Media Classic中選取資產，再前往 **[!UICONTROL 「檔案」>「使CDN失效」]** 選項。
