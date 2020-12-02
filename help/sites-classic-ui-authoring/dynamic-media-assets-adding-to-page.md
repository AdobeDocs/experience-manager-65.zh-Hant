---
title: 將 Dynamic Media 資產新增至頁面
seo-title: 將 Dynamic Media 資產新增至頁面
description: 若要將動態媒體功能新增至您在網站上使用的資產，您可以直接在頁面上新增動態媒體或互動媒體元件。
seo-description: 若要將動態媒體功能新增至您在網站上使用的資產，您可以直接在頁面上新增動態媒體或互動媒體元件。
uuid: 650d0867-a079-4936-a466-55b7a30803a2
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 331f4980-5193-4546-a22e-f27e38bb8250
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 2%

---


# 將 Dynamic Media 資產新增至頁面{#adding-dynamic-media-assets-to-pages}

若要將動態媒體功能新增至您在網站上使用的資產，您可以直接在頁面上新增&#x200B;**[!UICONTROL 動態媒體]**&#x200B;或&#x200B;**[!UICONTROL 互動媒體]**&#x200B;元件。 您可以進入[!UICONTROL Design]模式並啟用動態媒體元件來完成此操作。 然後，您可以將這些元件新增至頁面，並新增資產至元件。動態媒體和互動式媒體元件是智慧型的——他們知道您要新增影像或視訊，而可用的選項也會隨之改變。

如果您使用AEM做為WCM，請直接將動態媒體資產新增至頁面。

>[!NOTE]
>
>影像地圖可在包裝盒外取得，供轉盤橫幅使用。

## 新增動態媒體元件至頁面{#adding-a-dynamic-media-component-to-a-page}

將[!UICONTROL 動態媒體]或[!UICONTROL 互動媒體]元件新增至頁面與將元件新增至任何頁面相同。 以下各節將詳細說明[!UICONTROL 動態媒體]和[!UICONTROL 互動媒體]元件。

若要將動態媒體元件／檢視器新增至頁面：

1. 在AEM中，開啟您要新增動態媒體元件的頁面。
1. 如果沒有可用的動態媒體元件，請按一下[!UICONTROL Sidekick]中的標尺進入&#x200B;**[!UICONTROL Design]**&#x200B;模式，按一下&#x200B;**[!UICONTROL Edit]** parsys，然後選擇&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;使動態媒體元件可用。

   >[!NOTE]
   >
   >如需詳細資訊，請參閱[在設計模式中設定元件](/help/sites-authoring/default-components-designmode.md)。

1. 按一下[!UICONTROL Sidekick]中的鉛筆圖示，返回&#x200B;**[!UICONTROL 編輯]**&#x200B;模式。
1. 將側鍵中的&#x200B;**[!UICONTROL 動態媒體]**&#x200B;或&#x200B;**[!UICONTROL 互動媒體]**&#x200B;元件從&#x200B;**[!UICONTROL 其他]**&#x200B;群組拖曳至所需位置的頁面。
1. 按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;以開啟元件。
1. [視需要編](#dynamic-media-component) 輯元件，然後按一下「 **** 確定」以儲存變更。

## 動態媒體元件{#dynamic-media-components}

[!UICONTROL 動態] 媒體和 [!UICONTROL 互動] 媒體可從Sidekick底下的  動態媒 **[!UICONTROL 體取得。]** 您可將 **[!UICONTROL Interactive]** Media元件用於任何互動式資產，例如互動式視訊、互動式影像或轉盤集。對於所有其他動態媒體元件，請使用&#x200B;**[!UICONTROL 動態媒體]**&#x200B;元件。

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>這些元件預設不可用，在使用之前必須在設計模式中選取。 [在「設計」模式中提供元件後](/help/sites-authoring/default-components-designmode.md)，您可以像新增其他AEM元件一樣，將元件新增至頁面。

### 動態媒體元件{#dynamic-media-component}

動態媒體元件是智慧型的——視您新增影像或視訊而定，您有各種選項。 此元件支援影像預設集、影像檢視器，例如影像集、回轉集、混合媒體集和視訊。 此外，檢視器回應速度快。 也就是說，螢幕大小會根據螢幕大小自動變更。 所有檢視器都是以HTML5為基礎的檢視器。

>[!NOTE]
>
>當您新增[!UICONTROL 動態媒體]元件，而&#x200B;**[!UICONTROL 動態媒體設定]**&#x200B;為空白或無法正確新增資產時，請勾選下列項目：
>
>* 您已啟用[動態媒體](/help/assets/config-dynamic.md)。 動態媒體預設為停用。
>* 該影像具有金字塔tiff檔案。 在啟用動態媒體之前匯入的影像沒有金字塔tiff檔案。

>



#### 使用影像{#when-working-with-images}時

[!UICONTROL 動態媒體]元件可讓您新增動態影像，包括影像集、回轉集和混合媒體集。 您可以放大、縮小，如果適用，則可以在回轉集內旋轉影像，或從其他類型的回轉集選取影像。

您也可以直接在元件中設定檢視器預設集、影像預設集或影像格式。 若要讓影像回應，您可以設定中斷點或套用回應式影像預設集。

![chlimage_1-72](assets/chlimage_1-72a.png)

您可以按一下元件中的&#x200B;**[!UICONTROL 編輯]**，然後按一下&#x200B;**[!UICONTROL 動態媒體設定]**&#x200B;標籤，編輯下列動態媒體設定。

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>依預設，動態媒體影像元件是可調式的。如果要使其成為固定大小，請在&#x200B;**[!UICONTROL Advanced]**&#x200B;標籤的元件中設定它，並使用&#x200B;**[!UICONTROL Width]**&#x200B;和&#x200B;**[!UICONTROL Height]**&#x200B;屬性。

**[!UICONTROL 檢視器預設]** -從下拉式選單中選取現有的檢視器預設。如果您所尋找的檢視器預設集不可見，您可能需要將它顯示。 請參閱[管理檢視器預設集](/help/assets/managing-viewer-presets.md)。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

如果您要檢視影像集、回轉集或混合媒體集，這是唯一可用的選項。 顯示的檢視器預設集也很聰明——只會顯示相關的檢視器預設集。

**[!UICONTROL 影像預設]** -從下拉式選單中選取現有的影像預設。如果您要尋找的影像預設集不可見，您可能需要將它顯示。 請參閱[管理影像預設集](/help/assets/managing-image-presets.md)。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

**[!UICONTROL 影像修飾元]** -您可以提供額外的影像指令來變更影像效果。這些說明在[管理影像預設集](/help/assets/managing-viewer-presets.md)和[命令參考](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)中。

如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

**[!UICONTROL 中斷點]** -如果您在回應式網站上使用此資產，則需要新增頁面中斷點。影像中斷點必須以逗號(,)分隔。 當影像預設集中未定義高度或寬度時，此選項便可運作。

如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

按一下元件中的&#x200B;**[!UICONTROL 編輯]**&#x200B;可以編輯以下[!UICONTROL 高級設定]。

**[!UICONTROL 標題]** -變更影像的標題。

**[!UICONTROL 替代文字]** -為關閉圖形的使用者新增影像標題。

如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

**[!UICONTROL URL, Open in]** - You can set an asset from to open a link.設定&#x200B;**[!UICONTROL URL]**&#x200B;和&#x200B;**[!UICONTROL 在]**&#x200B;中開啟，以指出您要在相同視窗或新視窗中開啟。

如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

**[!UICONTROL 寬度和高度]** -如果希望影像大小固定，請輸入像素值。將這些值留空可讓資產具適應性。

#### 使用視頻{#when-working-with-video}時

使用[!UICONTROL 動態媒體]元件，將動態視訊新增至您的網頁。 當您編輯元件時，您可以選擇使用預先定義的視訊檢視器預設集來播放頁面上的視訊。

![chlimage_1-74](assets/chlimage_1-74a.png)

按一下元件中的&#x200B;**[!UICONTROL 編輯]**&#x200B;可編輯以下[!UICONTROL 動態媒體設定]。

>[!NOTE]
>
>依預設，動態媒體視訊元件是可調式的。 如果要使其成為固定大小，請在元件中將其設定為&#x200B;**[!UICONTROL Width]**&#x200B;和&#x200B;**[!UICONTROL Height]**(**[!UICONTROL Advanced]**)頁籤。

**[!UICONTROL 檢視器預設]** -從下拉式選單中選取現有的視訊檢視器預設。如果您所尋找的檢視器預設集不可見，您可能需要將它顯示。 請參閱[管理檢視器預設集](/help/assets/managing-viewer-presets.md)。

按一下元件中的&#x200B;**[!UICONTROL 編輯]**&#x200B;可以編輯以下[!UICONTROL 高級]設定。

**[!UICONTROL 標題]** -變更影片標題。

**[!UICONTROL 寬度和高度]** -如果您希望視訊大小固定，請輸入像素值。將這些值留空可讓其適應性。

#### 如何傳送安全視訊{#how-to-delivery-secure-video}

在AEM 6.2中，當您安裝[FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480)時，您可以控制視訊是透過安全SSL連線(HTTPS)還是不安全的連線(HTTP)傳送。 依預設，視訊傳送通訊協定會自動從內嵌網頁的通訊協定繼承。 如果網頁是透過HTTPS載入，視訊也會透過HTTPS傳送。 反之亦然，如果網頁位於HTTP上，則視訊會透過HTTP傳送。 在大多數情況下，此預設行為是正確的，無需進行任何配置更改。 不過，您可以將`VideoPlayer.ssl=on`附加至URL路徑的結尾或內嵌程式碼片段中其他檢視器組態參數的清單，以覆寫此預設行為，以強制安全傳送視訊。

如需有關安全視訊傳送和使用URL路徑中`VideoPlayer.ssl`組態屬性的詳細資訊，請參閱檢視器參考指南中的[安全視訊傳送](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html)。 除了視訊檢視器外，混合媒體檢視器和互動式視訊檢視器也能提供安全的視訊傳送。

### 互動式媒體元件{#interactive-media-component}

互動式媒體元件適用於這些資產上具有互動功能的熱點或影像地圖。 如果您有互動式影像、互動式視訊或轉盤橫幅，請使用&#x200B;**[!UICONTROL 互動式媒體]**&#x200B;元件。

[!UICONTROL 互動式媒體]元件是智慧型的——視您新增影像或視訊而定，您有各種選項。 此外，檢視器回應速度快。 也就是說，螢幕大小會根據螢幕大小自動變更。 所有檢視器都是以HTML5為基礎的檢視器。

![chlimage_1-75](assets/chlimage_1-75a.png)

按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;可以編輯以下&#x200B;**[!UICONTROL General]**&#x200B;設定。

**[!UICONTROL 檢視器預設]** -從下拉式選單中選取現有的檢視器預設。如果您所尋找的檢視器預設集不可見，您可能需要將它顯示。 檢視器預設集必須先發佈，才能使用。 請參閱管理檢視器預設集。

**[!UICONTROL 標題]** -變更影片標題。

**[!UICONTROL 寬度和高度]** -如果您希望視訊大小固定，請輸入像素值。將這些值留空可讓其適應性。

您可以按一下元件中的&#x200B;**[!UICONTROL 編輯]**，編輯下列「新增至購物車」**[!UICONTROL 設定。]**

**[!UICONTROL 顯示產品資產]** -依預設，此值會選取。產品資產會依「商務」模組中的定義，顯示產品的影像。 清除核取標籤，不會顯示產品資產。

**[!UICONTROL 顯示產品價格]** -依預設，此值會選取。產品價格顯示「商務」模組中定義的項目價格。 清除勾號以不顯示產品價格。

**[!UICONTROL 顯示產品表單]** -依預設，此值未選取。「產品表單」包含任何產品變體，例如尺寸和顏色。 清除勾號，不顯示產品變數。
