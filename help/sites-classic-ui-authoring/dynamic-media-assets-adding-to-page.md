---
title: 新增Dynamic Media資產至頁面
description: 若要將Dynamic Media功能新增至您在網站上使用的資產，您可以直接在頁面上新增Dynamic Media或互動式媒體元件。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 1%

---

# 新增Dynamic Media資產至頁面{#adding-dynamic-media-assets-to-pages}

若要將Dynamic Media功能新增至您在網站上使用的資產，您可以直接在頁面上新增&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;或&#x200B;**[!UICONTROL Interactive Media]**&#x200B;元件。 進入&#x200B;**[!UICONTROL Design]**&#x200B;模式並啟用Dynamic Media元件。 然後，您可以將這些元件新增至頁面，並新增資產至元件。Dynamic Media和互動式媒體元件是智慧型的，他們知道您是新增影像還是視訊，而可用的選項也會隨之變更。

如果您使用Dynamic Media做為WCM，請直接將Adobe Experience Manager資產新增至頁面。

>[!NOTE]
>
>影像地圖可立即用於輪播橫幅。

## 新增Dynamic Media元件至頁面 {#adding-a-dynamic-media-component-to-a-page}

將[!UICONTROL Dynamic Media]或[!UICONTROL 互動式媒體]元件新增至頁面，與將元件新增至任何頁面相同。 以下各節詳細說明[!UICONTROL Dynamic Media]和[!UICONTROL 互動式媒體]元件。

若要將Dynamic Media元件/檢視器新增至頁面：

1. 在Experience Manager中，開啟您要新增Dynamic Media元件的頁面。
1. 如果沒有可用的Dynamic Media元件，請在[!UICONTROL Sidekick]中選擇尺標以進入&#x200B;**[!UICONTROL Design]**&#x200B;模式。
1. 選擇&#x200B;**[!UICONTROL Edit]** parsys。
1. 選取&#x200B;**[!UICONTROL Dynamic Media]**，讓Dynamic Media元件可供使用。

   >[!NOTE]
   >
   >如需詳細資訊，請參閱[在設計模式中設定元件](/help/sites-authoring/default-components-designmode.md) 。

1. 按一下[!UICONTROL Sidekick]中的鉛筆圖示，返回&#x200B;**[!UICONTROL Edit]**&#x200B;模式。
1. 將&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;或&#x200B;**[!UICONTROL 互動式媒體]**&#x200B;元件從sidekick中的&#x200B;**[!UICONTROL 其他]**&#x200B;群組拖曳至所需位置的頁面。
1. 選擇&#x200B;**[!UICONTROL Edit]**&#x200B;以開啟元件。
1. [視需要](#dynamic-media-component) 編輯元件。
1. 選擇&#x200B;**[!UICONTROL OK]**&#x200B;以保存更改。

## Dynamic Media元件 {#dynamic-media-components}

 Sidekick底下 [!UICONTROL 的] Dynamic Media和Interactive   Media可 **[!UICONTROL 用Dynamic Media]**。您可以對任何互動式資產（例如互動式視訊、互動式影像或轉盤集）使用&#x200B;**[!UICONTROL 互動式媒體]**&#x200B;元件。 對於所有其他Dynamic Media元件，請使用&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;元件。

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>預設情況下，這些元件不可用，在使用之前必須在「設計」模式下選取這些元件。 [在「設計」模式中使用元件後](/help/sites-authoring/default-components-designmode.md)，您可以像新增任何其他Experience Manager元件一樣，將元件新增至頁面。

### Dynamic Media元件 {#dynamic-media-component}

Dynamic Media元件是智慧型的，視您新增影像或影片而定，您有各種選項。 元件支援影像預設集、以影像為基礎的檢視器，例如影像集、回轉集、混合媒體集和視訊。 此外，檢視器回應速度快。 也就是說，螢幕的大小會根據螢幕大小自動變更。 所有檢視器都是以HTML5為基礎的檢視器。

>[!NOTE]
>
>新增[!UICONTROL Dynamic Media]元件且&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;空白或無法正確新增資產時，請檢查下列項目：
>
>* 您已啟用[Dynamic Media](/help/assets/config-dynamic.md)。 Dynamic Media預設為停用。
>* 影像具有金字塔Tiff檔案。 在啟用Dynamic Media之前匯入的影像沒有金字塔Tiff檔案。

>



#### 使用影像時 {#when-working-with-images}

[!UICONTROL Dynamic Media]元件可讓您新增動態影像，包括影像集、回轉集和混合媒體集。 您可以放大、縮小，如果適用，可以在回轉集內開啟影像，或從另一類型的集合中選取影像。

您也可以直接在元件中設定檢視器預設集、影像預設集或影像格式。 若要讓影像具有回應性，您可以設定斷點或套用回應式影像預設集。

![chlimage_1-72](assets/chlimage_1-72a.png)

您可以按一下元件中的&#x200B;**[!UICONTROL Edit]**，然後按一下&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;標籤，以編輯下列Dynamic Media設定。

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>依預設，動態媒體影像元件是可調式的。如果要將其設定為固定大小，請在&#x200B;**[!UICONTROL Advanced]**&#x200B;頁簽的元件中，使用&#x200B;**[!UICONTROL Width]**&#x200B;和&#x200B;**[!UICONTROL Height]**&#x200B;屬性進行設定。

**[!UICONTROL 檢視器預設集]**  — 從下拉式選單中選取現有的檢視器預設集。如果您要尋找的檢視器預設集未顯示，您必須使其顯示。 請參閱[管理檢視器預設集](/help/assets/managing-viewer-presets.md)。 如果您使用影像預設集，則無法選取檢視器預設集，反之則無法選取。

只有在檢視影像集、回轉集或混合媒體集時，才可使用此選項。 顯示的檢視器預設集是智慧型的。 也就是說，只會顯示相關的檢視器預設集。

**[!UICONTROL 影像預設]**  — 從下拉式選單中選取現有的影像預設集。如果您要尋找的影像預設集未顯示，則必須使其可見。 請參閱[管理影像預設集](/help/assets/managing-image-presets.md)。 如果您使用影像預設集，則無法選取檢視器預設集，反之則無法選取。

如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

**[!UICONTROL 影像修飾元]**  — 您可以提供其他影像命令來變更影像效果。這些命令在[管理影像預設集](/help/assets/managing-viewer-presets.md)和[命令引用](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)中進行了說明。

如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

**[!UICONTROL 中斷點]**  — 如果您在回應式網站上使用此資產，則必須新增頁面中斷點。影像斷點以逗號分隔(,)。 當影像預設集中未定義高度或寬度時，此選項即可運作。

如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

您可以按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;編輯以下[!UICONTROL 進階設定]。

**[!UICONTROL 標題]**  — 變更影像的標題。

**[!UICONTROL 替代文字]**  — 為關閉圖形的使用者新增影像標題。

如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

**[!UICONTROL URL，在]** 中開啟 — 您可以從設定資產以開啟連結。設定&#x200B;**[!UICONTROL URL]**&#x200B;和&#x200B;**[!UICONTROL 在]**&#x200B;中開啟，以指示您要在相同視窗還是在新視窗中開啟它。

如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

**[!UICONTROL 寬度和高度]**  — 如果您希望影像大小固定，請輸入像素值。將這些值保留為空白，可讓資產具有適用性。

#### 使用視訊時 {#when-working-with-video}

使用&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;元件將動態視訊新增至網頁。 編輯元件時，您可以選擇使用預先定義的視訊檢視器預設集來在頁面上播放視訊。

![chlimage_1-74](assets/chlimage_1-74a.png)

您可以按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;編輯以下[!UICONTROL Dynamic Media設定]。

>[!NOTE]
>
>依預設，Dynamic Media視訊元件是最適化的。 如果要將其設定為固定大小，請在元件中以&#x200B;**[!UICONTROL Advanced]**&#x200B;標籤中的&#x200B;**[!UICONTROL Width]**&#x200B;和&#x200B;**[!UICONTROL Height]**&#x200B;設定它。

**[!UICONTROL 檢視器預設集]**  — 從下拉式選單中選取現有的視訊檢視器預設集。如果您要尋找的檢視器預設集未顯示，您必須使其顯示。 請參閱[管理檢視器預設集](/help/assets/managing-viewer-presets.md)。

您可以按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;編輯以下[!UICONTROL Advanced]設定。

**[!UICONTROL 標題]**  — 變更視訊的標題。

**[!UICONTROL 寬度和高度]**  — 如果您希望視訊大小固定，請輸入像素值。將這些值保留為空白，可使其變得最適化。

#### 傳送安全視訊 {#how-to-delivery-secure-video}

在Experience Manager6.2中，安裝[FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480)時，您可以控制視訊是透過安全SSL連線(HTTPS)或不安全連線(HTTP)傳送。 依預設，視訊傳送通訊協定會自動從內嵌網頁的通訊協定繼承。 如果網頁透過HTTPS載入，視訊也會透過HTTPS傳送。 反之，如果網頁是在HTTP上，視訊會透過HTTP傳送。 通常，此預設行為正常，不需要進行任何設定變更。 不過，您可以覆寫此預設行為。 將`VideoPlayer.ssl=on`附加至URL路徑的結尾，或內嵌程式碼片段中其他檢視器設定參數的清單。 任一動作都會強制確保視訊傳送安全。

如需安全視訊傳送及在URL路徑中使用`VideoPlayer.ssl`設定屬性的詳細資訊，請參閱檢視器參考指南中的[安全視訊傳送](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html)。 除了視訊檢視器，混合媒體檢視器和互動式視訊檢視器也提供安全的視訊傳送。

### 互動式媒體元件 {#interactive-media-component}

互動式媒體元件適用於在這些資產上具有互動的熱點或影像地圖。 如果您有互動式影像、互動式視訊或輪播橫幅，請使用&#x200B;**[!UICONTROL 互動式媒體]**&#x200B;元件。

[!UICONTROL 互動式媒體]元件是智慧型的 — 視您新增影像或視訊而定，有多種選項。 此外，檢視器回應速度快。 也就是說，螢幕的大小會根據螢幕大小自動變更。 所有檢視器都是以HTML5為基礎的檢視器。

![chlimage_1-75](assets/chlimage_1-75a.png)

您可以按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;編輯以下&#x200B;**[!UICONTROL 一般]**&#x200B;設定。

**[!UICONTROL 檢視器預設集]**  — 從下拉式選單中選取現有的檢視器預設集。如果您要尋找的檢視器預設集未顯示，您必須使其顯示。 必須先發佈檢視器預設集，才能使用。 請參閱[管理檢視器預設集](/help/assets/managing-viewer-presets.md)。

**[!UICONTROL 標題]**  — 變更視訊的標題。

**[!UICONTROL 寬度和高度]**  — 如果您希望視訊大小固定，請輸入像素值。將這些值保留為空白，可使其變得最適化。

您可以按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;編輯下列&#x200B;**[!UICONTROL 新增至購物車]**&#x200B;設定。

**[!UICONTROL 顯示產品資產]**  — 依預設，會選取此值。產品資產會依照商務模組中的定義顯示產品的影像。 清除勾號以不顯示產品資產。

**[!UICONTROL 顯示產品價格]**  — 依預設，此值會選取。產品價格顯示商務模組中定義的項目價格。 清除勾號以不顯示產品價格。

**[!UICONTROL 顯示產品表單]**  — 依預設，未選取此值。產品表單包含任何產品變體，例如大小和顏色。 清除勾號以不顯示產品變體。
