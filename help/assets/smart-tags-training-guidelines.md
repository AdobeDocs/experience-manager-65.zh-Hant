---
title: 智慧型內容服務訓練方針
description: 訓練Adobe Sensei的AI服務，將智慧標籤套用至資產
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 7%

---


# 智慧型內容服務訓練方針 {#smart-content-service-training-guidelines}

為了有效地標籤您的品牌影像，智慧型內容服務要求培訓影像符合特定准則。

## 培訓方針 {#guidelines-for-training}

為獲得最佳效果，您的訓練集中的影像應符合下列准則：

**** 數量和大小：每個標籤至少30個影像。長邊至少500像素。

**一致性**: 標籤的影像應類似視覺效果。

例如，將所有這些影像標籤為（用於訓練）並不 `my-party` 好，因為它們的視覺上不類似。

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/coherence.png)

**涵蓋範圍**: 培訓中的影像應該有足夠的多樣性。 其理念是提供幾個相當多樣化的範例，讓Experience Manager學會專注在正確的事物上。 如果您要在視覺上不相同的影像上套用相同的標籤，請至少包含5種不同類型的範例。

例如，對於標籤下模 *式姿勢*，請加入更多類似下方反白顯示影像的訓練影像，讓服務在標籤時更精確地識別類似影像。

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/coverage_1.png)

**干擾／妨礙**: 該服務更能訓練那些分散注意力的影像（突出的背景、不相關的伴奏，如主題的物體／人）。

例如，對於標籤休閒 *鞋*，第二張影像不是好的訓練候選影像。

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/distraction.png)

**** 完整性：如果影像符合多個標籤的資格，請先新增所有適用的標籤，再加入影像以進行訓練。For example, for tags, such as `raincoat` and `model-side-view`, add both the tags on the eligible asset before including it for training.

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/completeness.png)

## 限制 {#limitations}

增強的智慧型標籤是以學習影像模型及其標籤為基礎。 這些模型在識別標籤時並不總是十分完美。 智慧型內容服務的目前版本有下列限制：

* 無法辨識影像的細微差異。 例如，修身與普通襯衫。
* 無法根據影像的微小圖樣／部分來識別標籤。 例如，T恤上的標誌。
* 在中支援的地區設定中 [!DNL Experience Manager] 支援標籤。 如需語言清單，請參閱智 [慧型內容服務版本注意事項](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html)。

若要使用智慧型標籤（一般或增強功能）來搜尋資產，請使用 [!DNL Assets] Omnisearch（全文搜尋）。 智慧型標籤沒有個別的搜尋述詞。

>[!NOTE]
>
>智慧型內容服務是否能夠訓練您的標籤並將它們套用至其他影像，取決於您用於訓練的影像品質。 為獲得最佳效果，Adobe建議您使用視覺上類似的影像來訓練每個標籤的服務。
