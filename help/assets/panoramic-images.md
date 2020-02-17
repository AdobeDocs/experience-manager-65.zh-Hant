---
title: 全景影像
description: 瞭解如何在動態媒體中處理全景影像。
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 全景影像{#panoramic-images}

本節將說明如何與全景影像檢視器搭配使用，以呈現球面全景影像，提供如臨現場的360°房間、屬性、位置或風景觀賞體驗。

另請參閱「 [管理檢視器預設集」](/help/assets/managing-viewer-presets.md)。

![panoramic-image2](assets/panoramic-image2.png)

## 上傳資產以搭配全景影像檢視器使用 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

若要將已上傳的資產視為要搭配全景影像檢視器使用的球形全景影像，該資產必須具備下列其中一項或兩項：

* 寬高比為2。
您可以在以下位置覆寫CRXDE Lite中預設的2外觀比例設定：
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 使用關鍵字 `equirectangular`、 `spherical`和 `panorama`、或 `spherical` 和標籤 `panoramic`。 請參 [閱使用標籤](/help/sites-authoring/tags.md)。

外觀比例和關鍵字條件都適用於資產詳細資料頁面和 `Panoramic Media` WCM元件的全景資產。

若要上傳資產以搭配全景影像檢視器使用，請參閱「上 [傳資產」](/help/assets/managing-assets-touch-ui.md#uploading-assets)。

## 設定Dynamic Media Classic(Scene7) {#configuring-dynamic-media-classic-scene}

若要讓全景影像檢視器在AEM中正常運作，您必須將全景影像檢視器預設集與Dynamic Media Classic(Scene7)和Dynamic Media Classic(Scene7)特定中繼資料同步化，如此檢視器預設集就會在JCR中更新。 若要完成此作業，請依下列方式設定Dynamic Media Classic(Scene7):

1. [請針對每個公司帳戶登入您的Dynamic Media Classic(Scene7)](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) 。

1. 在頁面的右上角附近，按一下「設定>應 **[!UICONTROL 用程式設定>發佈設定>影像伺服器」]**。
1. 在「影像伺服器發佈」頁面上，從上方 **[!UICONTROL 附近的「發佈內容]** 」下拉式選單中，選取「 **[!UICONTROL 影像伺服」]**。

1. 在相同的「影像伺服器發佈」頁面上，找到標題「請 **[!UICONTROL 求屬性」]**。
1. 在「請求屬性」標題下，找出「 **[!UICONTROL 回覆影像大小限制」]**。 然後，在相關的「寬度」和「高度」欄位中，增加全景影像的最大允許影像大小。

   Dynamic Media Classic(Scene7)的像素上限為25,000,000像素。 寬高比為2:1的影像允許的最大大小為7000 x 3500。 不過，對於一般的桌上型電腦螢幕，4096 x 2048像素就足夠了。

   >[!NOTE]
   >
   >僅支援符合允許影像大小上限的影像。 若要求的影像大小超過限制，將會產生403個回應。

1. 在「請求屬性」標題下，執行下列動作：

   * 將「請求模糊化模式」設 **[!UICONTROL 為「停用]**」。
   * 將「請求鎖定模式」設 **[!UICONTROL 置為「禁用]**」。
   在AEM中使用 `Panoramic Media` WCM元件時，必須進行這些設定。

1. 在「影像伺服器發佈」頁面的左側，按一下「儲存」 ****。

1. 在右下角，按一下「關閉 **[!UICONTROL 」]**。

### 全景媒體WCM元件故障排除 {#troubleshooting-the-panoramic-media-wcm-component}

如果您將影像放入WCM的Panoramic media元件中，而元件預留位置已收合，您可能會想要疑難排解下列問題：

* 如果您遇到403 Forbidden錯誤，可能是由於要求的影像大小過大所致。 檢閱「設 **[!UICONTROL 定動態媒體經典]** (Scene7)」 [中的「回覆影像大小限制」設定](/help/assets/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7))。

* 對於頁面上顯示的資產上的「無效鎖定」或「剖析錯誤」，請勾選「請求模糊化模式」和「請求鎖定模式」，以確保它們已停用。
* 對於受污染的畫布錯誤，請為影像資產的先前請求設定規則集定義檔案路徑並使CTN無效。
* 如果影像要求的大小超過支援的限制，影像品質變得非常低，請檢查 **** JPEG編碼屬性>品質設定是否不為空。 「品質」( **[!UICONTROL Quality]** )欄位的典型設定為 `95`。 您可以在「影像伺服器發佈」頁面上找到設定。 若要存取頁面，請參 [閱設定動態媒體經典(Scene7)](/help/assets/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7))。

## 預覽全景影像 {#previewing-panoramic-images}

請參閱 [預覽資產](/help/assets/previewing-assets.md)。

## 發佈全景影像 {#publishing-panoramic-images}

請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。
