---
title: Dynamic Media 無障礙內容
description: 了解Dynamic Media和Dynamic Media檢視器中的協助工具支援。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
source-git-commit: 01de1d5064f5ebf00acd2fe9f138d852f41f7273
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 1%

---

# [!DNL Dynamic Media] 中的協助工具 {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] 在製作使用者介面上支援鍵盤控制和輔助技術，例如JAWS和NVDA螢幕閱讀器。

## 中的鍵盤協助工具支援 [!DNL Dynamic Media]

因為 [!DNL Dynamic Media] 是 [!DNL Adobe Experience Manager Assets]，大部分的鍵盤控制行為與 [!DNL Experience Manager Assets]. 例如， `Cancel` 按鈕 [!DNL Dynamic Media] 焦點與中的 [!DNL Experience Manager Assets]，並回應 `Spacebar` 索引鍵 [!DNL Experience Manager Assets]. 請參閱 [Assets中的鍵盤快速鍵](/help/assets/accessibility.md#keyboard-shortcuts).

中由單個用戶介面元素支援的擊鍵 [!DNL Dynamic Media] 清晰易懂。 鍵盤控制 [!DNL Dynamic Media] 是關於下列項目：

* 使用功能 `Tab` 和 `Shift+Tab` 鍵擊，以在頁面上的交互元素之間導航。
使用 `Tab` 將輸入焦點提前到Tab鍵順序中的下一個用戶介面元素；使用 `Shift+Tab` 將輸入焦點重新移回上一個使用者介面元素。
焦點周遊會遵循畫面上的自然使用者介面元素位置，並依從左至右、由上至下的順序移動。 此外，如果有任何欄位有錯誤，您可以按下 `Tab` 把焦點移到它上。
* 使用 `Spacebar` 和 `Enter` 啟用標準使用者介面元素（例如按鈕和下拉式清單）的鍵值。
* 可在使用中元素上查看鍵盤焦點醒目提示。 具有輸入焦點的用戶介面元素接收視覺焦點指示，作為圍繞用戶介面元素呈現的邊框。
* 在熱點編輯器中，可以使用一些自定義鍵擊（如箭頭鍵）與複雜的用戶介面元素交互，以重新定位熱點。
* 在互動式視訊編輯器中，您可以使用 `Spacebar` 來選取影像並將其新增至區段。 此外，您也可以使用 `Backspace` 從 **[!UICONTROL 內容]** 標籤。 另外，按 `Tab` 功能，以在頁面上的互動式元素之間導覽。
* 在影像裁切/智慧型裁切編輯器中，您可以執行下列操作：
   * 使用箭頭鍵裁切幀大小，或重新定位影像，或兩者。
   * 第一個 `Tab` stop會醒目顯示整個影像幀。 然後，可以使用鍵盤上的箭頭鍵來重新定位框架。
   * 接下來的四個 `Tab` 停止是框架的四個角。 將焦點置於框架拐角時，該拐角將加亮。 同樣地，您可以使用鍵盤上的箭頭鍵來移動聚焦的角。
請參閱 [編輯單一影像的智慧型裁切或智慧型色票](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## 中的輔助技術支援 [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] 使用者介面元素可搭配輔助技術使用，例如螢幕閱讀器。 例如，當您使用鍵盤快速鍵導覽地標時，它會識別頁面上的地標 `D` 或使用鍵盤快速鍵的區域 `R`. 它也會提供使用標題鍵盤快速鍵導覽時的標題旁白 `H`.

## 中的鍵盤協助工具支援 [!DNL Dynamic Media] 檢視器 {#keyboard-accessibility-for-dm-viewers}

現成可用 [!DNL Dynamic Media] 檢視器元件支援客戶的鍵盤協助工具。

請參閱 [鍵盤協助工具和導覽](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) (位於Dynamic Media檢視器參考指南中)。

## 中的輔助技術支援 [!DNL Dynamic Media] 檢視器 {#assistive-technology-support-for-dm-viewers}

全部 [!DNL Dynamic Media] 檢視器元件支援ARIA（可存取的豐富網際網路應用程式）角色和屬性，以改善與輔助技術（例如螢幕閱讀器）的整合。
請參閱 **輔助技術支援** Dynamic Media檢視器參考指南中任何自訂檢視器主題的說明主題。 例如，請參閱 [輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) 視訊檢視器，或 [輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) （用於互動式影像查看器）。

## Dynamic Media支援隱藏式字幕 {#closed-caption-support}

Dynamic Media支援透過隱藏式字幕傳送視訊和最適化視訊集。 標題必須顯示在視訊內容的頂端。

請參閱 [Dynamic Media中的影片 — 將隱藏式字幕或字幕加入影片](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Adobe解決方案的協助工具](https://www.adobe.com/accessibility.html)
>* [ [!DNL Experience Manager Assets]](/help/assets/accessibility.md) 中的協助工具

