---
title: Dynamic Media 無障礙內容
description: 了解Dynamic Media和Dynamic Media檢視器中的協助工具支援
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: 協助工具
role: Business Practitioner, Administrator
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# [!DNL Dynamic Media] {#working-with-three-d-assets-dm}中的輔助功能

[!DNL Dynamic Media] 在製作使用者介面上支援鍵盤控制和輔助技術，例如JAWS和NVDA螢幕閱讀器。

## [!DNL Dynamic Media]中的鍵盤輔助功能支援

由於[!DNL Dynamic Media]是[!DNL Adobe Experience Manager Assets]的外掛程式，因此大多數鍵盤控制行為與[!DNL Experience Manager Assets]中完全相同。 例如，[!DNL Dynamic Media]中的`Cancel`按鈕與[!DNL Experience Manager Assets]中的按鈕具有相同的焦點突出顯示，並且與[!DNL Experience Manager Assets]中的`Spacebar`鍵反應。 請參閱Assets](/help/assets/accessibility.md#keyboard-shortcuts)中的[鍵盤快速鍵。

[!DNL Dynamic Media]中由單個用戶介面元素支援的擊鍵在大多數情況下是顯而易見的，並且易於發現。 [!DNL Dynamic Media]中的鍵盤控制項與以下內容有關：

* 能夠使用`Tab`和`Shift+Tab`鍵擊在頁面上的互動元素之間導航。
使用`Tab`將輸入焦點按Tab鍵順序提前到下一個用戶介面元素；使用`Shift+Tab`將輸入焦點重新移回上一個使用者介面元素。
焦點周遊會遵循畫面上的自然使用者介面元素位置，並依從左至右、由上至下的順序移動。 此外，如果有欄位有錯誤，您可以按`Tab`將焦點移至該欄位。
* 可使用`Spacebar`和`Enter`鍵來啟用標準使用者介面元素，例如按鈕、下拉式清單等。
* 可在使用中元素上查看鍵盤焦點醒目提示。 具有輸入焦點的用戶介面元素可以接收視覺焦點指示，作為圍繞用戶介面元素呈現的邊框。
* 在熱點編輯器中，可以使用一些自定義鍵擊（如箭頭鍵）與複雜的用戶介面元素交互，以重新定位熱點。
* 在互動式視訊編輯器中，您可以使用`Spacebar`來選取影像，並將其新增至區段。 此外，您還可以使用`Backspace`鍵從&#x200B;**[!UICONTROL Content]**&#x200B;頁簽中刪除選定項。 此外，按`Tab`可視需要運作，以在頁面上的互動式元素之間導覽。
* 在影像裁切/智慧型裁切編輯器中，您可以執行下列操作：
   * 使用箭頭鍵裁切幀大小，或重新定位影像，或兩者。
   * 第一個`Tab`停止將突出顯示整個影像幀。 然後，可以使用鍵盤上的箭頭鍵重新定位框架。
   * 接下來的四個`Tab`停止是框架的四個角。 將焦點置於框架拐角時，該拐角將加亮。 同樣地，您可以使用鍵盤上的箭頭鍵來移動聚焦的角。
請參閱[編輯單個影像的智慧型裁切或智慧型色票](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## [!DNL Dynamic Media] {#assistive-technology-support-for-dm}中的輔助技術支援

[!DNL Dynamic Media] 使用者介面元素可搭配輔助技術使用，例如螢幕閱讀器。例如，當您使用鍵盤快捷鍵`D`導航地標時，它可識別頁面上的地標，或使用鍵盤快捷鍵`R`的區域。 它也會提供使用標題鍵盤快速鍵`H`導覽時的標題旁白。

## [!DNL Dynamic Media]檢視器{#keyboard-accessibility-for-dm-viewers}中的鍵盤協助工具支援

所有現成可用的[!DNL Dynamic Media]檢視器元件都支援客戶使用鍵盤輔助功能。

請參閱Dynamic Media檢視器參考指南中的[鍵盤協助工具和導覽](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)。

## [!DNL Dynamic Media]檢視器{#assistive-technology-support-for-dm-viewers}中的輔助技術支援

所有[!DNL Dynamic Media]檢視器元件都支援ARIA（可存取的豐富網際網路應用程式）角色和屬性，以改善與輔助技術（例如螢幕閱讀器）的整合。
請參閱Dynamic Media檢視器參考指南中任何自訂檢視器主題的**輔助技術支援**&#x200B;說明主題。 例如，請參閱視訊檢視器的[輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html)，或互動式影像檢視器的[輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only)。

>[!MORELIKETHIS]
>
>* [Adobe解決方案的協助工具](https://www.adobe.com/accessibility.html)
>* [ [!DNL Experience Manager Assets]中的輔助功能](/help/assets/accessibility.md)

