---
title: 使用Dynamic Media Classic驗證CDN快取
description: 使CDN（內容傳送網路）快取內容失效可讓您快速更新由Dynamic Media Classic傳送的資產，而不需等待快取過期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 729fbf3a97d3ae3bc91204f8831fd115d9d77f20
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 17%

---


# 透過Dynamic Media Classic {#invalidating-your-cdn-cached-content}使CDN快取失效

動態媒體資產由CDN（內容傳送網路）快取，以快速傳送。 不過，當您更新資產時，您會希望這些變更立即生效。 停用CDN快取內容可讓您快速更新由Dynamic Media傳送的資產，而不需等待快取過期。

>[!NOTE]
>
>客戶必須使用與Adobe Experience Manager Dynamic Media搭售的CDN，才能從CDN快取失效中獲益。

>[!IMPORTANT]
>
>下列步驟僅適用於AEM 6.5、Service Pack 5(AEM 6.5.5)或更舊版本的Dynamic Media。<br>如果您在AEM 6.5、Service Pack 6(AEM 6.5.6)或更新版本中使用Dynamic Media，請依照 [Invalidating the CDN cache by Dynamic Media中的步驟進行。](/help/assets/invalidate-cdn-cache-dynamic-media.md)

另請參閱Dynamic Media Classic(Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)中的「快取概觀」。[

**若要透過Dynamic Media Classic使CDN快取失效：**

1. 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=en#system-requirements-dmc-app)，然後登入您的帳戶。

   您的認證和登入是在布建時由Adobe提供。 如果您沒有此資訊，請聯絡技術支援。

1. 在頁面的右上角，點選&#x200B;**[!UICONTROL 設定>應用程式設定>一般設定。]**
1. 在「應用程式一般設定」頁面的「伺服器」群組標題下，找到&#x200B;**[!UICONTROL CDN失效範本]**&#x200B;文字方塊。

1. 指定用於使CDN（內容傳送網路）快取失效的範本。

   例如，假設您輸入參照`<ID>`的影像URL（包括影像預設集或修飾元），而不是像下列範例中的特定影像ID:

   `https://server.com/is/image/Company/<ID>?$product$`

   如果範本僅包含`<ID>`，則動態媒體會填入`https://<server>/is/image`，其中`<server>`是「一般設定」中定義的發佈伺服器名稱，而&lt;ID>是選取無效的資產。

1. 在頁面的右下角，按一下&#x200B;**[!UICONTROL 關閉。]**
1. 在Dynamic Media Classic使用者介面中，選取一或多個資產，然後按一下「檔案>使CDN失效」。**** 您會看到從您建立的範本和所選資產產生的一或多個URL清單。它使用「應用程式一般設定」下「已發佈伺服器名稱」下所列的伺服器URL。

   例如，在上一步驟中設定「CDN失效範本」時，假設您選取了名為`Backpack_B`的單一影像資產影像。 當您點選「**[!UICONTROL 檔案>廢止CDN]**」時，會在「CDN失效」使用者介面中產生下列產生的URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在「URL」清單方塊中，點選「**[!UICONTROL 繼續]**」以清除每個特定URL的快取。 您可以編輯URL，也可以輸入URL或貼到URL清單方塊中，以新增URL;您不需要事先設定CDN失效範本。

   按一下&#x200B;**[!UICONTROL 繼續]**&#x200B;後，將顯示一個指示器，用於估計清除快取所需的時間。

   如果您選取多個資產，然後點選「**[!UICONTROL 檔案>使CDN]**&#x200B;失效」，則儲存的&#x200B;**[!UICONTROL 範本URL會參照每個資產。]** 因此，您可以定義 **** CDN失效範本，引用您網站上參考的每個URL影像預設集（例如產品詳細資料和搜尋結果）。然後，當您從快取中選取一或影像以進行失效時，URL會自動填入介面。

   >[!NOTE]
   >
   >當您選取資產，然後按一下「檔案 **[!UICONTROL >使CDN無效]**」時，Dynamic media會使用無效的CDN範本，自動建立要使內容傳送網路(CDN)無效的URL。如果「 **[!UICONTROL CDN失效範本」文字方塊中沒有任何項目]** ，則會顯示空白的URL清單。CDN的快取並非以資產為基礎；它是以URL為基礎。因此，您必須注意您網站上的完整URL。在您決定這些URL後，可以在步驟的前面將它們新 **[!UICONTROL 增至「使CDN範本無效]** 」文字方塊。然後，您可以選取這些資產，並在單一步驟中使URL無效。
   >
   >另一個選項是將完整的URL新增至&#x200B;**[!UICONTROL 使CDN]**&#x200B;清單無效。 如果您遵循此方法，在前往&#x200B;**[!UICONTROL 檔案>廢止CDN]**&#x200B;選項之前，不必先在Dynamic Media Classic中選取資產。

