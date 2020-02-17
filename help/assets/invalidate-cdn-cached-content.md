---
title: 使CDN快取內容無效
description: 停用CDN（內容傳送網路）快取內容可讓您快速更新由動態媒體傳送的資產，而不需等待快取過期。
uuid: 0fd88e31-9745-4c98-a245-9f5d0766cad4
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e6c9b50b-c27c-48bf-b3c0-9994e7bf6d7e
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 使CDN快取內容無效 {#invalidating-your-cdn-cached-content}

CDN會快取動態媒體資產，以便快速傳送。 不過，當您更新資產時，可能會希望這些變更立即生效。 停用CDN（內容傳送網路）快取內容可讓您快速更新由動態媒體傳送的資產，而不需等待快取過期。

另請參閱 [Dynamic Media Classic(Scene7)中的快取概觀](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**若要使CDN快取內容無效：**

1. 登入您的Dynamic Media Classic(Scene7)帳戶：

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   您的認證和登入是在布建時由Adobe提供。 如果您沒有此資訊，請聯絡技術支援。

1. 按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。
1. 在「應用程式一般設定」頁面的「伺服器」群組標題下，找出「 **[!UICONTROL CDN失效範本]** 」文字方塊。

1. 指定用於使CDN（內容傳送網路）快取失效的範本。

   例如，假設您輸入參照的影像URL（包括影像預設集或修飾元） `<ID>`，而不是像下列範例中的特定影像ID:

   `https://server.com/is/image/Company/<ID>?$product$`

   如果範本僅包 `<ID>`含，則動態媒體會填入 `https://<server>/is/image` , `<server>` 其中是「一般設定」中定義的發佈伺服器名稱，而&lt;ID>是選取無效的資產。

1. 在頁面的右下角，按一下「關閉 **[!UICONTROL 」]**。
1. 在Dynamic Media Classic(Scene7)UI中，選取一或多個資產，然後按一下「檔 **[!UICONTROL 案>使CDN失效]**」。 您會看到一個清單，列出您所建立的範本和選取的資產所產生的一或多個URL。 它使用「應用程式一般設定」下「已發佈伺服器名稱」下所列的伺服器URL。

   例如，在上一步驟中設定「CDN失效範本」時，假設您選取了名為的單一影像資產影像 `Backpack_B`。 當您按一下「 **[!UICONTROL 檔案>使CDN失效]** 」時，會在「CDN失效」使用者介面中產生下列產生的URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在「URL」清單方塊中，按一 **[!UICONTROL 下「繼續]** 」以清除每個特定URL的快取。 請注意，您可以編輯URL，或是透過輸入或貼入URL清單方塊來新增URL;您不需要事先設定CDN失效範本。

   按一下「繼 **[!UICONTROL 續]**」(Continue)後，將顯示一個指示器，用於估計清除快取所需的時間。

   如果您選取多個資產，然後按一下「 **[!UICONTROL 檔案>使CDN失效]**」，則儲存的範本URL會參照每個 **[!UICONTROL 資產]**。 因此，您可以定義 **[!UICONTROL CDN無效範本]** ，以參考網站上參考的每個URL影像預設集（例如產品詳細資訊、搜尋結果等）。 然後，當您從快取中選取一或影像以進行失效時，URL會自動填入介面。

   >[!NOTE]
   >
   >當您選取資產，然後按一下「檔案 **[!UICONTROL >使CDN無效]**」時，Dynamic media會使用無效的CDN範本，自動建立要使內容傳送網路(CDN)無效的URL。 如果「 **[!UICONTROL CDN失效範本」文字方塊中沒有任何項目]** ，則會顯示空白的URL清單。 CDN的快取並非以資產為基礎；它是以URL為基礎。 因此，您必須注意您網站上的完整URL。 在您決定這些URL後，可以在步驟的前面將它們新 **[!UICONTROL 增至「使CDN範本無效]** 」文字方塊。 然後，您可以選取這些資產，並在單一步驟中使URL無效。
   >
   >另一個選項是將完整的URL新增至「使 **[!UICONTROL CDN無效]** 」清單。 如果您遵循此方法，在前往「檔案>廢止CDN」選項之前，不必先在Dynamic Media Classic中選 **[!UICONTROL 取資產]** 。

