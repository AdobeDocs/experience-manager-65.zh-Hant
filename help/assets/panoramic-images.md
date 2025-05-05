---
title: 全景影像
description: 瞭解如何在Dynamic Media中使用全景影像。
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Panoramic Images,Asset Management
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 全景影像{#panoramic-images}

本節說明如何使用「全景影像」檢視器來轉譯球面全景影像，以獲得房間、屬性、位置或橫向的360度沈浸式檢視體驗。

另請參閱[管理檢視器預設集](/help/assets/managing-viewer-presets.md)。

![panoramic-image2](assets/panoramic-image2.png)

## 上傳資產以與全景影像檢視器搭配使用 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

若要讓已上傳的資產符合您要與全景影像檢視器搭配使用的球形全景影像資格，該資產必須具備下列其中一項或兩項：

* 外觀比例為2。
您可以在下列位置以CRXDE Lite覆寫2的預設外觀比例設定：
  `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 以關鍵字`equirectangular`、`spherical`和`panorama`或`spherical`和`panoramic`標籤。 請參閱[使用標籤](/help/sites-authoring/tags.md)。

外觀比例和關鍵字條件都適用於資產詳細資料頁面和`Panoramic Media` WCM元件的全景資產。

若要上傳資產以與全景影像檢視器搭配使用，請參閱[上傳Assets](/help/assets/manage-assets.md#uploading-assets)。

## 設定Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

若要讓「全景影像」檢視器在Adobe Experience Manager中正常運作，請將「全景影像」檢視器預設集與Dynamic Media Classic和Dynamic Media Classic專屬的中繼資料同步，好讓JCR中的檢視器預設集得以更新。 若要完成此同步，請依照以下方式設定Dynamic Media Classic：

1. 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=zh-Hant#getting-started)，然後登入您的帳戶。

1. 在頁面的右上角附近，選取&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL Publish設定]** > **[!UICONTROL 影像伺服器]**。
1. 在「影像伺服器Publish」頁面上，從頂端附近的&#x200B;**[!UICONTROL Publish內容]**&#x200B;下拉式功能表中選取&#x200B;**[!UICONTROL 影像伺服]**。

1. 在同一個影像伺服器Publish頁面上，找到標題&#x200B;**[!UICONTROL 要求屬性]**。
1. 在「要求屬性」標題下，找出&#x200B;**[!UICONTROL 回覆影像大小限制]**。 然後，在關聯的「寬度」和「高度」欄位中，增加全景影像的最大允許影像大小。

   Dynamic Media Classic有25,000,000畫素的限制。 2:1外觀比例影像的最大允許大小為7000 x 3500。 然而，對於典型的桌上型電腦熒幕，4096 x 2048畫素就足夠了。

   >[!NOTE]
   >
   >僅支援位於允許影像大小上限內的影像。 對超過大小限制的影像的請求會導致403回應。

1. 在「請求屬性」標題下，執行下列動作：

   * 將要求模糊化模式設定為&#x200B;**[!UICONTROL 已停用]**。
   * 將要求鎖定模式設定為&#x200B;**[!UICONTROL 已停用]**。

   在Experience Manager中使用`Panoramic Media` WCM元件時，需要這些設定。

1. 在「影像伺服器Publish」頁面的底部，選取左側&#x200B;**[!UICONTROL 儲存]**。

1. 在右下角，選取&#x200B;**[!UICONTROL 關閉]**。

### 疑難排解全景媒體WCM元件 {#troubleshooting-the-panoramic-media-wcm-component}

如果您將影像放入WCM的全景媒體元件中，且元件預留位置已摺疊，請進行下列疑難排解：

* 如果您遇到403禁止錯誤，可能是要求的影像大小太大所造成。 檢閱[設定Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)中的&#x200B;**[!UICONTROL 回覆影像大小限制]**&#x200B;設定。

* 針對頁面上顯示的「資產鎖定無效」或「剖析錯誤」，請檢查「請求模糊化模式」和「請求鎖定模式」，以確保它們已停用。
* 對於汙染的畫布錯誤，請設定規則集定義檔案路徑，並讓影像資產先前的請求使CTN失效。
* 如果影像要求超過支援的限制後，影像品質變低，請檢查&#x200B;**[!UICONTROL JPEG編碼屬性>品質]**&#x200B;設定是否為空白。 **[!UICONTROL 品質]**&#x200B;欄位的典型設定為`95`。 您可以在影像伺服器Publish頁面上找到設定。 若要存取頁面，請參閱[設定Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)。

## 預覽全景影像 {#previewing-panoramic-images}

請參閱[預覽Assets](/help/assets/previewing-assets.md)。

## Publish全景影像 {#publishing-panoramic-images}

請參閱[Publish Assets](/help/assets/publishing-dynamicmedia-assets.md)。
