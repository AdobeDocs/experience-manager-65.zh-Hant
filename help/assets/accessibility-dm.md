---
title: 無障礙環境支援 [!DNL Dynamic Media]
description: 瞭解動態媒體和動態媒體檢視器中的協助功能
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 383f84b1a984683b3e2ce60f1a3f2191749a1561
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# 無障礙環境支援 [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] 跨製作使用者介面支援鍵盤控制和輔助技術，例如JAWS和NVDA螢幕閱讀器。

## 鍵盤協助工具支援 [!DNL Dynamic Media]

由於 [!DNL Dynamic Media] 是插件，因 [!DNL Adobe Experience Manager Assets]此大多數鍵盤控制行為與中完全相同 [!DNL Experience Manager Assets]。 例如，中的 `Cancel` 按鈕與 [!DNL Dynamic Media] 中的對焦反白顯示相同， [!DNL Experience Manager Assets]並且與中的鍵 `Spacebar` 產生反應 [!DNL Experience Manager Assets]。 請參 [閱「資產」中的鍵盤快速鍵](/help/assets/accessibility.md#keyboard-shortcuts)。

在大多數情況下，個別使用者介面元 [!DNL Dynamic Media] 素支援的按鍵操作都很明顯，而且易於發現。 中的鍵盤 [!DNL Dynamic Media] 控制項與下列相關：

* 能夠使用 `Tab` 和按 `Shift+Tab` 鍵來導覽頁面上的互動元素。
使用 `Tab` 將輸入焦點提前到Tabbing順序下一個用戶介面元素；使用 `Shift+Tab` 可將輸入焦點重新放回先前的使用者介面元素。
焦點遍歷會遵循畫面上自然的使用者介面元素位置，並依從左至右、從上至下的順序移動。 此外，如果有欄位有錯誤，您可以按 `Tab` 鍵將焦點移至該欄位。
* 能夠使用和 `Spacebar` 鍵 `Enter` 來啟動標準使用者介面元素，例如按鈕、下拉式清單等。
* 能夠查看活動元素上的鍵盤焦點反白顯示。 具有輸入焦點的用戶介面元件可接收視覺焦點指示，作為圍繞用戶介面元件呈現的邊框。
* 在熱點編輯器中，您可以使用一些自定義的按鍵操作（如箭頭鍵）來與複雜的用戶介面元素交互以重新定位熱點。
* 在互動式視訊編輯器中，您可 `Spacebar` 以使用來選取影像並將它新增至區段。 此外，您還可以使用索引鍵從「內 `Backspace` 容」索引標籤中刪除選取 **[!UICONTROL 的項]** 。 此外，按 `Tab` 下功能可視需要在頁面上的互動式元素之間導覽。
* 在「影像裁切／智慧型裁切」編輯器中，您可以執行下列動作：
   * 使用方向鍵裁切影格大小，或重新定位影像，或兩者皆可。
   * 第一個停 `Tab` 止會反白顯示整個影像影格。 然後，您可以使用鍵盤上的箭頭鍵重新定位框架。
   * 接下來的四 `Tab` 個停靠點是影格的四角。 將焦點放在框架拐角上時，該拐角會加亮。 同樣地，您可以使用鍵盤上的箭頭鍵來移動焦點轉角。
請參 [閱編輯單一影像的智慧裁切或智慧色票](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## 輔助技術支援： [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] 使用者介面元素可與輔助技術搭配使用，例如螢幕閱讀程式。 例如，當您使用鍵盤快速鍵導覽標誌時，它會識別頁面上的標誌，或使 `D` 用鍵盤快速鍵導覽區域 `R`。 它也會在使用標題鍵盤快速鍵導覽時說明標題 `H`。

## 檢視器中的鍵盤協助功 [!DNL Dynamic Media] 能 {#keyboard-accessibility-for-dm-viewers}

所有現成可用的檢視器元件都 [!DNL Dynamic Media] 支援為客戶提供鍵盤協助功能。

請參 [閱動態媒體檢視器參考指南](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) 中的鍵盤協助工具和導覽。

## 檢視器中的輔助技術支 [!DNL Dynamic Media] 援 {#assistive-technology-support-for-dm-viewers}

所有 [!DNL Dynamic Media] 檢視器元件都支援ARIA（可存取的Rich Internet Applications）角色和屬性，以改善與輔助技術（例如螢幕閱讀器）的整合。
請參閱動 **態媒體檢視器參考指南中自訂檢視器主題中的** 「輔助技術支援說明」主題。 例如，請參 [閱視訊檢視器的輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) ，或互動式影像檢視器 [的輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) 。

>[!MORELIKETHIS]
>
>* [Adobe解決方案的協助功能](https://www.adobe.com/accessibility.html)
>* [無障礙環境支援 [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

