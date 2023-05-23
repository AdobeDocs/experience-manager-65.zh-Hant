---
title: 與Adobe Experience Cloud
description: 學習如何將Adobe Experience Manager與Adobe Experience Cloud整合。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: a51a863a4edf7e8b951a8361c5c7f0517b09f12a
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 1%

---

# 與Adobe Experience Cloud{#integrating-with-the-adobe-marketing-cloud}

的 [Adobe Experience Cloud](https://business.adobe.com/products/marketing-cloud/main.html)包括功能強大的web分析和網站優化產品，這些產品提供可操作、即時的資料和洞察力，以推動成功的線上計畫。 它為線上業務優化提供了一個整合和開放的平台。 雲由整合應用程式組成，可收集和釋放客戶洞察力，以優化客戶購買、轉換和保留工作以及內容的建立和分發。

通過Adobe Experience Manager(AEM)，您可以無縫整合Adobe Experience Cloud的以下產品：

* Adobe Analytics公司向營銷人員提供關於線上戰略和營銷計畫的可操作的即時情報。
* Adobe Target公司使營銷人員能夠不斷使他們的線上內容與客戶更相關，從而產生更大的轉換。
* Adobe Dynamic Media Classic自動化了媒體管理，優化了Web發佈，並增強了Web體驗，所有這些都是在一個托管環境中實現的。
* Adobe動態Tag Management公司為營銷人員提供了直觀的工具，可快速方便地管理無限數量的Adobe和第三方標籤。
<!-- Search&Promote is end of life as of September 1, 2022 * Adobe Search&Promote gives marketers the ability to control and optimize the search results on their sites. -->
* Adobe Campaign允許您直接在Adobe Experience Manager管理電子郵件傳遞內容。

此外，您 [與AEMCreative Cloud整合](/help/assets/aem-cc-integration-best-practices.md) 和 [第三方服務](/help/sites-administering/third-party-services.md)。

## 整合 Adobe Analytics {#integrating-with-adobe-analytics}

[Adobe Analytics](https://business.adobe.com/products/analytics/adobe-analytics.html) 是業界領先的解決方案，它為數字營銷人員提供了一個測量、分析和優化來自跨多個營銷渠道的所有線上計畫的整合資料的場所。 它為營銷人員提供了可操作的、即時的Web分析智慧，介紹數字戰略和營銷計畫。 Adobe Analytics公司幫助營銷人員快速確定通過網站獲得最多利潤的途徑，分段流量以發現高價值的網路訪問者，確定訪問者離開網站的位置，並確定線上營銷活動的關鍵成功指標。

您可以使用Adobe Analytics來分析站點的資料。

與Adobe Analytics整合允許您執行以下操作：

* 啟用分析用戶跟蹤。
* 將您的運行模式（例如，作者、發佈）映射到不同的報表套件。
* 將客戶端上下文變數作為轉換變數或通信屬性提交。
* 使用預定義的變數映射。
* 一次配置完整的站點節。
* 跟蹤自定義事件。

有關與Analytics整合AEM的資訊，請參見 [與Adobe Analytics整合](/help/sites-administering/adobeanalytics.md)。

您還可以使用 [選擇加入嚮導](/help/sites-administering/opt-in.md) 輕鬆執行整合。

## 整合 Adobe Target {#integrating-with-adobe-target}

[Adobe Target](https://business.adobe.com/products/target/adobe-target.html) 營銷人員使用它來設計和執行線上test、建立即時訪問群體（基於行為）並自動確定內容和線上體驗的目標。

如今，線上消費者需要不斷變化，期望從他們可以選擇的各種站點和內容來源中獲得相關、甚至是個性化的內容。 要吸引線上受眾，線上營銷人員必須快速確定哪些產品和內容對其受眾具有相關性和吸引力，這一點至關重要。 借助這些知識，營銷人員需要不斷改進其網站並將適當內容定向到不同受眾的能力。

[與Adobe Target整合](/help/sites-administering/target.md) 說明如何將站點與目標整合。

您還可以使用 [選擇加入嚮導](/help/sites-administering/opt-in.md) 輕鬆執行整合。

## 選擇分析和目標 {#opting-in-to-analytics-and-target}

提供AEM了與Adobe Analytics和Adobe Target融合的簡單選擇程式。 當您以管理員身份登錄並訪問「項目」控制台時，將顯示一個選擇加入嚮導。

![chlimage_1-107](assets/chlimage_1-107a.png)

選擇與分析和/或目標整合，以啟用其頁面跟蹤和分析功能以及個性化功能。 選擇加入時，請提供用戶帳戶資訊並指定要跟蹤的頁面。

有關詳細資訊，請參見 [選擇進入Adobe Analytics和Adobe Target。](/help/sites-administering/opt-in.md)

## 與Adobe Dynamic Media Classic整合 {#integrating-with-scene}

Adobe Dynamic Media Classic是一個托管解決方案，用於發佈、管理、增強和提供動態營銷資產和豐富的視覺商品銷售到web 、移動、電子郵件、社交媒體、網際網路顯示屏和印刷品。

在Adobe Experience Manager，你可以直接發佈從Adobe Experience Manager到Dynamic Media Classic的數字資產，也可以發佈從Dynamic Media Classic到Adobe Experience Manager的數字資產。

此外，您還可以通過Basic Zoom和Video等各種觀眾查看在Dynamic Media Classic發佈的Adobe Experience Manager資產。

有關Adobe Experience Manager如何與Dynamic Media Classic整合的詳細資訊，請參見 [與Dynamic Media Classic整合](/help/sites-administering/scene7.md) 文檔。

## 與Adobe動態Tag Management整合 {#integrating-with-adobe-dynamic-tag-management}

[Adobe力Tag Management](https://business.adobe.com/products/experience-platform/adobe-experience-platform.html) 為營銷人員提供了直觀的工具，可以快速方便地管理數量無限的Adobe和第三方標籤。 您擁有更大的控制力和靈活性，幾乎可以線上優化任何內容，同時減少對IT資源的依賴。

[整合Adobe動態Tag Management](/help/sites-administering/dtm.md) 以AEM便您使用動態Tag Management網站屬性跟蹤AEM網站。

## 與Adobe Audience Manager整合 {#integrating-with-adobe-audience-manager}

Audience Manager整合在6AEM.3中被取消。

<!-- Search&Promote is end of life as of September 1, 2022 ## Integrating with Search&Promote {#integrating-with-search-promote} -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote enables marketers to optimizehow visitors browse, find, compare, and select relevant products and content on web and mobile sites. Businesses can easily promote priority items based on business objectives and visitor intent, as well as automate merchandising and promotions activity via KPI-based triggers or metrics. -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote is a reliable and scalable hosted site search application, capable of scaling to millions of pages or products, for heavily visited online businesses ranging from retail to news sites. It offers unprecedented levels of marketer control and metrics-based relevance. -->

<!-- Search&Promote is end of life as of September 1, 2022 For information about integrating AEM and Search&Promote, see [Integrating with Adobe Search&Promote](/help/sites-administering/search-and-promote.md). -->

## 與 Adobe Campaign 整合 {#integrating-with-adobe-campaign}

[Adobe Campaign](https://business.adobe.com/products/campaign/adobe-campaign.html) 允許您直接在Adobe Experience Manager管理電子郵件傳遞內容。

有關如何與AEMAdobe Campaign整合的資訊，請參見 [與Adobe Campaign整合](/help/sites-administering/campaignstandard.md)。