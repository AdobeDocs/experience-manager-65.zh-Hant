---
title: 使用 Dynamic Media
description: 瞭解如何使用Dynamic Media來提供資產，以便在網站、行動網站和社交網站上消耗。
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 9%

---

# 使用Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) 協助隨選提供豐富的視覺化銷售和行銷資產，並根據網路、行動和社交網站上的消費自動調整。 Dynamic Media使用一組主要來源資產，透過其全球性、可擴充、效能最佳化的網路即時產生並傳送多種多樣的豐富內容。

Dynamic Media提供互動式檢視體驗，包括縮放、360度旋轉和視訊。 Dynamic Media以獨特方式整合Adobe Experience Manager數位資產管理（資產）解決方案的工作流程，以簡化及簡化數位行銷活動管理流程。

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## 您可以使用Dynamic Media做什麼 {#what-you-can-do-with-dynamic-media}

Dynamic Media可讓您在發佈資產之前先管理資產。 中會詳細說明如何使用一般資產 [使用數位資產](manage-assets.md). 一般主題包括上傳、下載、編輯和發佈資產；檢視和編輯屬性以及搜尋資產。

僅限Dynamic Media的功能包括：

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

另請參閱 [設定Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>若要瞭解使用Dynamic Media與將Dynamic Media Classic與Adobe Experience Manager整合之間的差異，請參閱 [Dynamic Media Classic整合與Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## 啟用Dynamic Media與停用Dynamic Media {#dynamic-media-on-versus-dynamic-media-off}

您可以區分是否已透過下列特性啟用（開啟） Dynamic Media：

* 下載或預覽資產時，可使用動態轉譯。
* 影像集、迴轉集、混合媒體集可供使用。
* 已建立PTIFF轉譯。

當您選取影像資產時，資產的檢視與Dynamic Media不同 [已啟用](config-dynamic.md#enabling-dynamic-media). Dynamic Media使用隨選HTML5檢視器。

### 動態轉譯 {#dynamic-renditions}

動態轉譯，例如影像和檢視器預設集（在底下） **[!UICONTROL 動態]**)在啟用Dynamic Media時可用。

![chlimage_1-358](assets/chlimage_1-358.png)

### 影像集、旋轉集、混合媒體集 {#image-sets-spins-sets-mixed-media-sets}

如果啟用Dynamic Media，則會提供影像集、迴轉集及混合媒體集。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF轉譯 {#ptiff-renditions}

啟用Dynamic Media的資產包括 `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### 資產檢視變更 {#asset-views-change}

啟用Dynamic Media後，您可以按一下 `+` 和 `-` 按鈕。 您也可以按一下以放大特定區域。 「回覆」會將您帶至原始版本，而且您可以按一下對角線箭頭，讓影像變成全熒幕。 已啟用Dynamic Media看起來像這樣：

![chlimage_1-361](assets/chlimage_1-361.png)

停用Dynamic Media後，您就可以放大和縮小並回覆成原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
