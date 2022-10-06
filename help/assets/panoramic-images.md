---
title: 全景影像
description: 了解如何在Dynamic Media中使用全景影像。
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
feature: Panoramic Images,Asset Management
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# 全景影像{#panoramic-images}

本節介紹如何使用全景影像查看器來呈現球形全景影像，以提供沈浸式360°的房間、屬性、位置或景觀的觀看體驗。

另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

![panoramic-image2](assets/panoramic-image2.png)

## 上傳資產以與全景影像檢視器搭配使用 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

若要讓上傳的資產符合要與全景影像檢視器搭配使用之球面全景影像的資格，資產必須具備下列其中一項或兩項：

* 長寬比為2。
您可以在以下位置覆寫CRXDE Lite中2的預設外觀比例設定：
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 使用關鍵字加上標籤 `equirectangular`，或 `spherical`和 `panorama`，或 `spherical` 和 `panoramic`. 請參閱 [使用標籤](/help/sites-authoring/tags.md).

外觀比例和關鍵字條件都適用於資產詳細資訊頁面和 `Panoramic Media` WCM元件。

若要上傳資產以搭配全景影像檢視器使用，請參閱 [上傳資產](/help/assets/manage-assets.md#uploading-assets).

## 設定Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

為了讓全景影像檢視器在Adobe Experience Manager中正常運作，請將全景影像檢視器預設集與Dynamic Media Classic和Dynamic Media Classic專用中繼資料同步，以便在JCR中更新檢視器預設集。 若要完成此同步，請依下列方式設定Dynamic Media Classic:

1. 開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

1. 在頁面的右上角附近，選取 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 發佈設定]** > **[!UICONTROL 影像伺服器]**.
1. 在「影像伺服器發佈」頁面上，從 **[!UICONTROL 發佈內容]** 下拉式功能表（位於頂端附近），選取 **[!UICONTROL 影像提供]**.

1. 在相同的「影像伺服器發佈」頁面上，找出標題 **[!UICONTROL 請求屬性]**.
1. 在「請求屬性」標題下，找出 **[!UICONTROL 回覆影像大小限制]**. 然後，在相關的「寬度」和「高度」欄位中，增加全景影像的最大允許影像大小。

   Dynamic Media Classic的限制為25,000,000像素。 寬高比為2:1的影像的最大允許大小為7000 x 3500。 但是，對於一般的案頭螢幕，4096 x 2048像素就足夠了。

   >[!NOTE]
   >
   >僅支援最大允許影像大小範圍內的影像。 若要求的影像大小超過上限，則會產生403回應。

1. 在「請求屬性」標題下，執行下列動作：

   * 將要求模糊化模式設為 **[!UICONTROL 已停用]**.
   * 將請求鎖定模式設定為 **[!UICONTROL 已停用]**.

   使用 `Panoramic Media` Experience Manager中的WCM元件。

1. 在「影像伺服器發佈」頁面的左側，選取 **[!UICONTROL 儲存]**.

1. 在右下角，選取 **[!UICONTROL 關閉]**.

### 疑難排解全景媒體WCM元件 {#troubleshooting-the-panoramic-media-wcm-component}

如果您將影像放置到WCM的全景媒體元件中，且元件預留位置已收合，請疑難排解下列問題：

* 如果您遇到403 Forbidden錯誤，可能是因為請求的影像大小太大。 檢閱 **[!UICONTROL 回覆影像大小限制]** 設定 [設定Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* 如需資產的「無效鎖定」或頁面上顯示的「剖析錯誤」，請勾選「請求模糊化模式」和「請求鎖定模式」，以確保已停用。
* 針對污染的畫布錯誤，請為影像資產的先前請求設定「規則集定義檔案路徑」和「使CTN無效」。
* 如果影像要求的大小超過支援的限制，影像品質變得低，請檢查 **[!UICONTROL JPEG編碼屬性>品質]** 設定不為空。 的典型設定 **[!UICONTROL 品質]** 欄位為 `95`. 您可以在「影像伺服器發佈」頁面上找到設定。 若要存取頁面，請參閱 [設定Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## 預覽全景影像 {#previewing-panoramic-images}

請參閱 [預覽資產](/help/assets/previewing-assets.md).

## 發佈全景影像 {#publishing-panoramic-images}

請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md).
