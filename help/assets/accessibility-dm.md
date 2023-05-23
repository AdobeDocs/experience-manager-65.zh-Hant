---
title: Dynamic Media 無障礙內容
description: 瞭解Dynamic Media和Dynamic Media觀眾對輔助功能的支援。
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

[!DNL Dynamic Media] 通過創作用戶介面支援鍵盤控制和輔助技術，如JAWS和NVDA螢幕閱讀器。

## 在中支援鍵盤輔助功能 [!DNL Dynamic Media]

因為 [!DNL Dynamic Media] 是 [!DNL Adobe Experience Manager Assets]，大多數鍵盤控制行為與中相同 [!DNL Experience Manager Assets]。 例如， `Cancel` 按鈕 [!DNL Dynamic Media] 與中的焦點相同 [!DNL Experience Manager Assets]，並對 `Spacebar` 鍵 [!DNL Experience Manager Assets]。 請參閱 [資產中的鍵盤快捷鍵](/help/assets/accessibility.md#keyboard-shortcuts)。

中單個用戶介面元素支援的擊鍵 [!DNL Dynamic Media] 清晰易見。 鍵盤控制項 [!DNL Dynamic Media] 關於以下內容：

* 使用能力 `Tab` 和 `Shift+Tab` 在頁面上的交互元素之間導航。
使用 `Tab` 將輸入焦點提前到下一個用戶介面元素的Tabbing順序；使用 `Shift+Tab` 將輸入焦點返回到上一個用戶介面元素。
焦點遍歷遵循螢幕上的自然用戶介面元素位置，然後按從左到右、從上到下的順序移動。 此外，如果有欄位出錯，可按 `Tab` 把焦點移到它上。
* 使用 `Spacebar` 和 `Enter` 鍵以激活標準用戶介面元素，如按鈕和下拉清單。
* 能夠查看活動元素上鍵盤焦點的突出顯示。 具有輸入焦點的用戶介面元件接收可視焦點指示作為呈現在用戶介面元件周圍的邊界。
* 在熱點編輯器中，可以使用一些自定義擊鍵（如箭頭鍵）與複雜的用戶介面元素交互，以重新定位熱點。
* 在互動式視頻編輯器中，您可以使用 `Spacebar` 來修改選定線條的屬性。 此外，您還可以 `Backspace` 鍵，從 **[!UICONTROL 內容]** 頁籤。 還有，按 `Tab` 在頁面上的交互元素之間導航時所需的函式。
* 在「影像裁剪/智慧裁剪」編輯器中，可以執行以下操作：
   * 使用箭頭鍵裁剪幀大小，或重新定位影像，或兩者。
   * 第一個 `Tab` 停止將加亮整個影像幀。 然後，可使用鍵盤上的箭頭鍵重新定位框架。
   * 接下來的四個 `Tab` 停止是框架的四個角。 將焦點放在框架拐角上時，拐角將加亮。 同樣，您可以使用鍵盤上的箭頭鍵移動聚焦的拐角。
請參閱 [編輯單個影像的智慧裁剪或智慧色板](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## 在 [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] 用戶介面元素與輔助技術（如螢幕閱讀器）配合使用。 例如，當您使用鍵盤快捷鍵導航地標時，它會識別頁面上的地標 `D` 或使用鍵盤快捷鍵的區域 `R`。 它還使用標題鍵盤快捷鍵導航時敘述標題 `H`。

## 在中支援鍵盤輔助功能 [!DNL Dynamic Media] 觀眾 {#keyboard-accessibility-for-dm-viewers}

現成 [!DNL Dynamic Media] 查看器元件支援客戶的鍵盤輔助功能。

請參閱 [鍵盤輔助功能和導航](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) 在《Dynamic Media觀眾參考指南》中。

## 在 [!DNL Dynamic Media] 觀眾 {#assistive-technology-support-for-dm-viewers}

全部 [!DNL Dynamic Media] 查看器元件支援ARIA（可訪問的富網際網路應用程式）角色和屬性，以改進與輔助技術（如螢幕閱讀器）的整合。
查看 **輔助技術支援** 《Dynamic Media觀眾參考指南》中任何自定義查看器主題的幫助主題。 例如，請參見 [輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) 或 [輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) 表徵圖。

## Dynamic Media的隱藏字幕支援 {#closed-caption-support}

Dynamic Media支援提供帶有隱藏字幕的視頻和自適應視頻集。 字幕必須顯示在視頻內容的頂部。

請參閱 [Dynamic Media視頻 — 在視頻中添加隱藏字幕或字幕](/help/assets/video.md#adding-captions-to-video)。

>[!MORELIKETHIS]
>
>* [Adobe解決方案的可訪問性](https://www.adobe.com/accessibility.html)
>* [ [!DNL Experience Manager Assets]](/help/assets/accessibility.md) 中的協助工具

