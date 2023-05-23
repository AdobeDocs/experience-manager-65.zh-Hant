---
title: 使用 Dynamic Media
description: 瞭解如何使用Dynamic Media來在Web、移動和社交站點上為消費提供資產。
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 9%

---

# 使用 Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) 幫助按需提供豐富的視覺商品銷售和營銷資產，並自動擴展以在Web、移動和社交網站上消費。 使用一組主要源資產，Dynamic Media通過其全球、可擴展、效能優化的網路即時生成並提供多種豐富內容的變體。

Dynamic Media提供互動式觀看體驗，包括縮放、360度旋轉和視頻。 Dynamic Media獨一無二地納入了Adobe Experience Manager數字資產管理（資產）解決方案的工作流程，以簡化和簡化數字市場活動管理流程。

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## 用Dynamic Media做什麼 {#what-you-can-do-with-dynamic-media}

Dynamic Media允許您在發佈資產之前管理資產。 如何處理一般資產，將在 [使用數字資產](manage-assets.md)。 一般主題包括上載，下載，編輯和發佈資產；查看和編輯屬性，以及搜索資產。

僅Dynamic Media功能包括：

* [輪播橫幅](carousel-banners.md)
* [影像集](image-sets.md)
* [互動式影像](interactive-images.md)
* [互動式影片](interactive-videos.md)
* [混合媒體集](mixed-media-sets.md)
* [全景影像](panoramic-images.md)

* [迴轉集](spin-sets.md)
* [影片](video.md)
* [傳遞 Dynamic Media 資產](delivering-dynamic-media-assets.md)
* [管理資產](managing-assets.md)
* [使用 Quickview 建立自訂快顯視窗](custom-pop-ups.md)

另請參閱 [設定Dynamic Media](administering-dynamic-media.md)。

>[!NOTE]
>
>要瞭解使用Dynamic Media與將Dynamic Media Classic與Adobe Experience Manager整合在一起的區別，請參見 [Dynamic Media Classic一體化與Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media)。

## Dynamic Media啟用與Dynamic Media禁用 {#dynamic-media-on-versus-dynamic-media-off}

您可以通過以下特徵來判斷是否啟用（開啟）Dynamic Media:

* 在下載或預覽資產時，動態格式副本可用。
* 映像集、旋轉集、混合媒體集可用。
* 建立PTIFF格式副本。

選擇影像資產時，資產的視圖與Dynamic Media不同 [啟用](config-dynamic.md#enabling-dynamic-media)。 Dynamic Media用的是點播HTML5觀眾。

### 動態格式副本 {#dynamic-renditions}

動態格式副本（如影像和查看器預設）（下） **[!UICONTROL 動態]**)時可用。

![chlimage_1-358](assets/chlimage_1-358.png)

### 影像集、旋轉集、混合媒體集 {#image-sets-spins-sets-mixed-media-sets}

如果啟用了Dynamic Media，則映像集、旋轉集和混合媒體集可用。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF格式副本 {#ptiff-renditions}

Dynamic Media資產包括 `pyramid.tiffs`。

![chlimage_1-360](assets/chlimage_1-360.png)

### 資產視圖更改 {#asset-views-change}

啟用Dynamic Media後，可通過按一下 `+` 和 `-` 按鈕。 也可按一下/點擊以放大特定區域。 還原將使您進入原始版本，您可以通過按一下對角線箭頭使影像全屏。 Dynamic Media啟用如下：

![chlimage_1-361](assets/chlimage_1-361.png)

禁用Dynamic Media後，可放大和縮小並恢復為原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
