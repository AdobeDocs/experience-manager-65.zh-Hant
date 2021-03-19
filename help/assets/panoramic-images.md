---
title: 全景影像
description: 瞭解如何在Dynamic Media處理全景影像。
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
feature: 全景影像，資產管理
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# 全景影像{#panoramic-images}

本節將說明如何與全景影像檢視器搭配使用，以呈現球面全景影像，提供如臨現場的360°房間、屬性、位置或風景觀賞體驗。

另請參閱[管理檢視器預設集](/help/assets/managing-viewer-presets.md)。

![panoramic-image2](assets/panoramic-image2.png)

## 上傳資產以搭配全景影像檢視器{#uploading-assets-for-use-with-the-panoramic-image-viewer}使用

若要將已上傳的資產視為要搭配全景影像檢視器使用的球形全景影像，該資產必須具備下列其中一項或兩項：

* 寬高比為2。
您可以在以下位置覆蓋CRXDE Lite中的預設外觀比例設定2:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 標籤有關鍵字`equirectangular`、`spherical`和`panorama`，或`spherical`和`panoramic`。 請參閱[使用標籤](/help/sites-authoring/tags.md)。

外觀比例和關鍵字准則都適用於資產詳細資料頁面和`Panoramic Media` WCM元件的全景資產。

若要上傳資產以搭配全景影像檢視器使用，請參閱[上傳資產](/help/assets/manage-assets.md#uploading-assets)。

## 配置Dynamic Media經典{#configuring-dynamic-media-classic-scene}

若要讓全景影像檢視器正常運作，AEM您必須將全景影像檢視器預設集與Dynamic Media經典和Dynamic Media經典中繼資料同步化，讓檢視器預設集在JCR中更新。 要實現此目的，請按以下方式配置Dynamic Media經典：

1. 開啟[Dynamic Media經典案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

1. 在頁面的右上角附近，按一下「設定」>「應用程式設定」>「發佈設定」>「影像伺服器」。]****[!UICONTROL 
1. 在「影像伺服器發佈」頁面上，從頂端附近的&#x200B;**[!UICONTROL 發佈內容]**&#x200B;下拉式選單中，選取「影像伺服」。]****[!UICONTROL 

1. 在相同的「影像伺服器發佈」頁面上，找到標題&#x200B;**[!UICONTROL 請求屬性。]**
1. 在「請求屬性」標題下，找到「回覆影像大小限制」。**** 然後，在相關的「寬度」和「高度」欄位中，增加全景影像的最大允許影像大小。

   Dynamic Media經典影像的限制為25,000,000像素。 寬高比為2:1的影像允許的最大大小為7000 x 3500。 不過，對於一般的桌上型電腦螢幕，4096 x 2048像素就足夠了。

   >[!NOTE]
   >
   >僅支援符合允許影像大小上限的影像。 若要求的影像大小超過限制，將會產生403個回應。

1. 在「請求屬性」標題下，執行下列動作：

   * 將「請求模糊化模式」設為「已停用」。]****[!UICONTROL 
   * 將「請求鎖定模式」設定為「已禁用」。]****[!UICONTROL 

   在中使用`Panoramic Media` WCM元件時，必須進行這些設定AEM。

1. 在「影像伺服器發佈」頁面的左側，按一下「儲存」。]****[!UICONTROL 

1. 在右下角，按一下&#x200B;**[!UICONTROL 關閉。]**

### 診斷全景媒體WCM元件{#troubleshooting-the-panoramic-media-wcm-component}

如果您將影像放入WCM的Panoramic Media元件中，而元件預留位置已收合，您可能會想要疑難排解下列問題：

* 如果您遇到403 Forbidden錯誤，可能是由於要求的影像大小過大所致。 查看[配置Dynamic Media經典](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)中的&#x200B;**[!UICONTROL 回復影像大小限制]**&#x200B;設定。

* 對於頁面上顯示的資產上的「無效鎖定」或「剖析錯誤」，請勾選「請求模糊化模式」和「請求鎖定模式」，以確保它們已停用。
* 對於受污染的畫布錯誤，請為影像資產的先前請求設定規則集定義檔案路徑並使CTN無效。
* 如果影像要求的大小超過支援的限制，影像品質變得非常低，請檢查「**[!UICONTROL JPEG編碼屬性>品質]**」設定是否不是空的。 **[!UICONTROL Quality]**&#x200B;欄位的典型設定為`95`。 您可以在「影像伺服器發佈」頁面上找到設定。 要訪問該頁，請參閱[配置Dynamic Media經典](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)。

## 預覽全景影像{#previewing-panoramic-images}

請參閱[預覽資產](/help/assets/previewing-assets.md)。

## 發佈全景影像{#publishing-panoramic-images}

請參閱[發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。
