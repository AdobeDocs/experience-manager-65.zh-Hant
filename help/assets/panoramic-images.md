---
title: 全景影像
description: 學習如何處理Dynamic Media的全景影像。
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

本節介紹如何與全景影像查看器一起渲染球形全景影像，以便在房間、屬性、位置或景觀中享受360°的沈浸式觀看體驗。

另請參閱 [管理查看器預設](/help/assets/managing-viewer-presets.md)。

![panoramic-image2](assets/panoramic-image2.png)

## 上載用於全景影像查看器的資源 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

要使上載的資產符合球形全景影像的要求，您要在全景影像查看器中使用該資產，該資產必須具有以下一項或兩項：

* 縱橫比為2。
您可以在以下CRXDE Lite中覆蓋預設長寬比設定2:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 用關鍵字標籤 `equirectangular`或 `spherical`和 `panorama`或 `spherical` 和 `panoramic`。 請參閱 [使用標籤](/help/sites-authoring/tags.md)。

縱橫比和關鍵字條件都適用於資產詳細資訊頁面和 `Panoramic Media` WCM元件。

要上載用於全景影像查看器的資產，請參閱 [上載資產](/help/assets/manage-assets.md#uploading-assets)。

## 配置Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

要使全景影像查看器在Adobe Experience Manager內正常工作，請將全景影像查看器預設與特定於Dynamic Media Classic和Dynamic Media Classic的元資料同步，以便查看器預設在JCR中更新。 要完成此同步，請按如下方式配置Dynamic Media Classic:

1. 開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的帳戶。

1. 在頁面右上角附近，選擇 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 發佈設定]** > **[!UICONTROL 映像伺服器]**。
1. 在「影像伺服器發佈」頁上， **[!UICONTROL 發佈上下文]** 下拉菜單，選擇 **[!UICONTROL 影像服務]**。

1. 在同一「映像伺服器發佈」頁上，找到標題 **[!UICONTROL 請求屬性]**。
1. 在「請求屬性」標題下，查找 **[!UICONTROL 答復影像大小限制]**。 然後，在關聯的「寬度」和「高度」欄位中，增加全景影像的最大允許影像大小。

   Dynamic Media Classic有2500萬像素的限制。 寬高比為2:1的影像的最大允許大小為7000 x 3500。 但是，對於典型的台式機螢幕，4096 x 2048像素就足夠了。

   >[!NOTE]
   >
   >僅支援最大允許影像大小範圍內的影像。 對超過大小限制的影像的請求會導致403響應。

1. 在「請求屬性」標題下，執行以下操作：

   * 將請求模糊處理模式設定為 **[!UICONTROL 已禁用]**。
   * 將請求鎖定模式設定為 **[!UICONTROL 已禁用]**。

   使用 `Panoramic Media` Experience Manager中的WCM元件。

1. 在「影像伺服器發佈」頁面的底部，在左側選擇 **[!UICONTROL 保存]**。

1. 在右下角，選擇 **[!UICONTROL 關閉]**。

### 對Panoramic Media WCM元件進行故障排除 {#troubleshooting-the-panoramic-media-wcm-component}

如果將影像放入WCM中的Panoramic Media元件中，且元件佔位符已折疊，請排除以下故障：

* 如果遇到「403禁止」錯誤，則可能是由於請求的影像大小太大。 查看 **[!UICONTROL 答復影像大小限制]** 設定 [配置Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)。

* 對於顯示在頁面上的資產上的「無效鎖定」或「分析錯誤」，請選中「請求模糊處理模式」和「請求鎖定模式」以確保它們被禁用。
* 對於受污染的畫布錯誤，請設定規則集定義檔案路徑並使先前對影像資產的請求失效CTN。
* 如果在影像請求的大小超過支援的限制後影像質量變低，請檢查 **[!UICONTROL JPEG編碼屬性>質量]** 設定不為空。 的典型設定 **[!UICONTROL 質量]** 欄位 `95`。 可以在「映像伺服器發佈」頁上找到該設定。 要訪問該頁面，請參見 [配置Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)。

## 預覽全景影像 {#previewing-panoramic-images}

請參閱 [預覽資產](/help/assets/previewing-assets.md)。

## 發佈全景影像 {#publishing-panoramic-images}

請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。
