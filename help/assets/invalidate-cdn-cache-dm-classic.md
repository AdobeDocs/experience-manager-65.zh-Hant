---
title: 通過Dynamic Media Classic使內容傳遞網路快取無效
description: 使您的CDN（內容分發網路）快取內容失效允許您快速更新由Dynamic Media Classic傳送的資產，而不是等待快取過期。
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

# 通過Dynamic Media Classic使內容傳遞網路快取無效 {#invalidating-your-cdn-cached-content}

Dynamic Media資產由CDN（內容交付網路）快取，以便快速交付。 但是，在對資產進行更新時，您希望這些更改立即生效。 使CDN快取內容失效允許您快速更新由Dynamic Media傳送的資產，而不是等待快取過期。

>[!NOTE]
>
>此功能要求您使用與Adobe Experience ManagerDynamic Media捆綁的現成CDN。 此功能不支援任何其他自定義CDN。

>[!IMPORTANT]
>
>以下步驟僅適用於Adobe Experience Manager的Dynamic Media6.5、Service Pack 5(6.5.5號Experience Manager)或更早版本。<br>如果您在Experience Manager6.5、Service Pack 6(Dynamic Media6.5.6)或更高版本中使用Experience Manager，請按照中的步驟操作 [通過Dynamic Media使CDN快取無效](/help/assets/invalidate-cdn-cache-dynamic-media.md)。

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**要通過Dynamic Media Classic使CDN快取失效：**

1. 開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app)，然後登錄到您的帳戶。

   您的憑據和登錄是在設定時由Adobe提供的。 如果您沒有此資訊，請與Adobe客戶支援聯繫。

1. 在頁面右上角附近，導航到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 常規設定]**。
1. 在「應用程式一般設定」頁的「伺服器」組標題下，找到 **[!UICONTROL CDN無效模板]** 的子菜單。

1. 指定用於使CDN（內容傳遞網路）快取失效的模板。

   例如，假設您輸入了引用的影像URL（包括影像預設或修飾符） `<ID>`，而不是像以下示例中所示的特定影像ID:

   `https://server.com/is/image/Company/<ID>?$product$`

   如果模板僅包含 `<ID>`然後Dynamic Media填滿 `https://<server>/is/image` 何處 `<server>` 是在常規設定中定義的發佈伺服器名稱， &lt;id> 是被選擇為無效的資產。

1. 在頁面的右下角，選擇 **[!UICONTROL 關閉]**。
1. 在Dynamic Media Classic用戶介面中，選擇一個或多個資產，然後轉到 **[!UICONTROL 檔案]** > **[!UICONTROL 無效CDN]**。 您會看到一個清單，其中包含根據您建立的模板和所選資產生成的一個或多個URL。 它使用「應用程式常規設定」下「已發佈伺服器名稱」下列出的伺服器URL。

   例如，在上一步中設定了CDN無效模板後，假設您選擇了名為 `Backpack_B`。 當您轉到 **[!UICONTROL 檔案]** > **[!UICONTROL 無效CDN]**&#x200B;在CDN失效用戶介面中生成以下URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在URL清單框中，選擇 **[!UICONTROL 繼續]** 清除每個特定URL的快取。 可以編輯URL，也可以通過鍵入或貼上到URL清單框中來添加URL;您無需預先設定CDN無效模板。

   選擇後 **[!UICONTROL 繼續]**，將顯示一個指示器，用於估計清除快取需要多長時間。

   如果您選擇了多個資產，則轉到 **[!UICONTROL 檔案]** > **[!UICONTROL 無效CDN]**，每個資產都在已保存中引用 **[!UICONTROL 模板URL]**。 因此，您可以定義 **[!UICONTROL CDN失效模板]** 引用網站上引用的每個URL影像預設（如產品詳細資訊和搜索結果）。 然後，當您從快取中選取一或影像以進行失效時，URL會自動填入介面。

   >[!NOTE]
   >
   >選擇資產後，轉到 **[!UICONTROL 檔案]** > **[!UICONTROL 無效CDN]**,Dynamic Media使用失效的CDN模板自動建立要從內容傳遞網路(CDN)失效的URL。 如果「 **[!UICONTROL CDN失效範本」文字方塊中沒有任何項目]** ，則會顯示空白的URL清單。CDN的快取並非以資產為基礎；它是以URL為基礎。因此，您必須注意您網站上的完整URL。在您決定這些URL後，可以在步驟的前面將它們新 **[!UICONTROL 增至「使CDN範本無效]** 」文字方塊。然後，您可以選取這些資產，並在單一步驟中使URL無效。
   >
   >另一個選項是將完整的URL添加到 **[!UICONTROL 無效CDN]** 清單框。 如果您遵循此方法，則不必在Dynamic Media Classic選擇資產，然後再轉到 **[!UICONTROL 檔案>失效CDN]** 的雙曲餘切值。
