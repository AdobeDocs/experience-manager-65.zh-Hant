---
title: Dynamic Media 無障礙內容
description: 瞭解Dynamic Media和Dynamic Media檢視器中的協助工具支援。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
solution: Experience Manager, Experience Manager Assets
source-git-commit: ed7183efa57db6d97941e3acc99d126c2fc0f6c5
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# [!DNL Dynamic Media]中的協助工具 {#working-with-three-d-assets-dm}

[!DNL Dynamic Media]在編寫使用者介面中支援鍵盤控制和輔助技術，例如JAWS和NVDA熒幕閱讀器。

## [!DNL Dynamic Media]中的鍵盤協助工具支援

因為[!DNL Dynamic Media]是[!DNL Adobe Experience Manager Assets]的外掛程式，所以大部分的鍵盤控制項行為與[!DNL Experience Manager Assets]中的相同。 例如，[!DNL Dynamic Media]中的`Cancel`按鈕具有與[!DNL Experience Manager Assets]中相同的焦點反白顯示，並會回應[!DNL Experience Manager Assets]中的`Spacebar`索引鍵。 請參閱Assets](/help/assets/accessibility.md#keyboard-shortcuts)中的[鍵盤快速鍵。

[!DNL Dynamic Media]中個別使用者介面元素所支援的按鍵動作清晰且易於探索。 [!DNL Dynamic Media]中的鍵盤控制項與下列內容有關：

* 能夠使用`Tab`和`Shift+Tab`按鍵在頁面上的互動式元素之間導覽。
使用`Tab`將輸入焦點推進到Tab鍵順序中的下一個使用者介面元素；使用`Shift+Tab`將輸入焦點帶回上一個使用者介面元素。
焦點周遊會依循熒幕上的自然使用者介面元素位置，並依由左至右、由上到下的順序移動。 此外，如果任何欄位有錯誤，您可以按下`Tab`將焦點移至該欄位。
* 能夠使用`Spacebar`和`Enter`鍵來啟動標準使用者介面元素，例如按鈕和下拉式清單。
* 可在作用中元素上看到鍵盤焦點反白顯示。 具有輸入焦點之使用者介面元素會接收視覺焦點指示，作為呈現於使用者介面元素周圍的邊框。
* 在熱點編輯器中，您可以使用某些自訂按鍵（例如方向鍵）與複雜的使用者介面元素互動，以重新定位熱點。
* 在互動式視訊編輯器中，您可以使用`Spacebar`來選取影像並將其新增至區段。 此外，您可以使用`Backspace`索引鍵從&#x200B;**[!UICONTROL 內容]**&#x200B;索引標籤中刪除選取的專案。 此外，視需要按`Tab`功能可在頁面上的互動式元素之間導覽。
* 在影像裁切/智慧型裁切編輯器中，您可以執行下列動作：
   * 使用方向鍵來裁切框架大小、重新定位影像，或兩者皆使用。
   * 第一個`Tab`停止點會反白整個影像框架。 然後您可以使用鍵盤上的方向鍵來重新定位框架。
   * 接下來的4個`Tab`句號是框架的四個轉角。 將焦點放在框架轉角上時，轉角會反白顯示。 同樣地，您可以使用鍵盤上的方向鍵來移動焦點轉角。
請參閱[編輯單一影像的智慧裁切或智慧色票](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## [!DNL Dynamic Media]中的輔助技術支援 {#assistive-technology-support-for-dm}

[!DNL Dynamic Media]使用者介面元素可使用輔助技術，例如熒幕閱讀器。 例如，當您使用鍵盤快速鍵`D`瀏覽地標或使用鍵盤快速鍵`R`瀏覽區域時，它可以辨識頁面上的地標。 它也會在使用標題鍵盤快速鍵`H`導覽時提供標題旁白。

## [!DNL Dynamic Media]檢視器中的鍵盤協助工具支援 {#keyboard-accessibility-for-dm-viewers}

所有現成的[!DNL Dynamic Media]檢視器元件都支援客戶的鍵盤協助工具。

請參閱Dynamic Media檢視器參考指南中的[鍵盤協助工具與導覽](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)。

## [!DNL Dynamic Media]個檢視者的輔助技術支援 {#assistive-technology-support-for-dm-viewers}

所有[!DNL Dynamic Media]檢視器元件都支援ARIA （可存取的豐富網際網路應用程式）角色和屬性，以改進與熒幕閱讀器等輔助技術的整合。
請參閱Dynamic Media檢視器參考指南中任何自訂檢視器主題中的**輔助技術支援**&#x200B;說明主題。 例如，請參閱視訊檢視器的[輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html)，或互動式影像檢視器的[輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only)。

## Dynamic Media中的隱藏式字幕支援 {#closed-caption-support}

Dynamic Media支援以隱藏式字幕傳送視訊與最適化視訊集。 註解必須顯示在視訊內容的最上方。

檢視Dynamic Media中的[影片 — 新增隱藏式字幕至影片](/help/assets/video.md#adding-captions-to-video)。

>[!MORELIKETHIS]
>
>* [Adobe解決方案的協助工具](https://www.adobe.com/accessibility.html)
>*  [!DNL Experience Manager Assets]](/help/assets/accessibility.md)中的[協助工具
