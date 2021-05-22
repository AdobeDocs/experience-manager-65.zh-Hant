---
title: 與Adobe Marketing Cloud整合
description: 了解如何整合Adobe Experience Manager與Adobe Marketing Cloud。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: d19b203ffe75a5628f350113d4d74a2916beffc8
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# 與Adobe Marketing Cloud整合{#integrating-with-the-adobe-marketing-cloud}

[Adobe Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html)包含功能強大的網頁分析和網站最佳化產品，可提供可操作的即時資料和深入分析，以推動成功的線上計畫。 它為線上業務優化提供了整合而開放的平台。 雲包含整合式應用程式，可收集和釋放客戶洞察力，以優化客戶贏取、轉換和保留工作，以及內容的建立和分發。

透過Adobe Experience Manager(AEM)，您可以與下列Adobe Marketing Cloud產品順暢整合：

* Adobe Analytics為行銷人員提供關於線上策略和行銷活動的可操作、即時資訊。
* Adobe Target可讓行銷人員持續讓其線上內容與客戶更相關，進而提供更高的轉換。
* AdobeDynamic Media Classic可自動化媒體管理、簡化Web發佈，並增強Web體驗，所有這一切都是在托管環境中完成的。
* Adobe動態標籤管理為行銷人員提供直覺式工具，以快速輕鬆管理不限數量的Adobe和協力廠商標籤。
* AdobeSearch&amp;Promote可讓行銷人員控制並最佳化其網站上的搜尋結果。
* Adobe Campaign可讓您直接在Adobe Experience Manager中管理電子郵件傳送內容。

此外，您可以[將AEM與Creative Cloud](/help/assets/aem-cc-integration-best-practices.md)及與[第三方服務](/help/sites-administering/third-party-services.md)整合。

## 整合 Adobe Analytics {#integrating-with-adobe-analytics}

[Adobe](https://www.omniture.com/en/products/analytics/sitecatalyst) 分析是領先業界的解決方案，可讓數位行銷人員在多個行銷管道中，透過單一位置測量、分析和最佳化所有線上活動的整合式資料。它為行銷人員提供關於數位策略和行銷計畫的可操作、即時的網頁分析智慧。 Adobe Analytics可協助行銷人員快速找出網站中最有利可圖的路徑、劃分流量以找出高價值網站訪客、判斷訪客在何處離開網站，以及識別線上行銷活動的關鍵成功量度。

您可以使用Adobe Analytics來分析網站的資料。

與Adobe Analytics整合可讓您執行下列工作：

* 啟用Analytics使用者追蹤。
* 將您的執行模式（例如製作、發佈）對應至不同的報表套裝。
* 提交用戶端內容變數作為轉換變數或流量屬性。
* 使用預先定義的變數對應。
* 一次設定完整的網站區域。
* 追蹤自訂事件。

如需有關整合AEM與Analytics的資訊，請參閱[與Adobe Analytics整合](/help/sites-administering/adobeanalytics.md)。

您也可以使用[選擇加入精靈](/help/sites-administering/opt-in.md)輕鬆執行整合。

## 整合 Adobe Target {#integrating-with-adobe-target}

[Adobe](https://www.omniture.com/en/products/conversion/test-and-target) 定位，供行銷人員用來設計和執行線上測試、建立即時受眾區段（根據行為），以及自動鎖定內容和線上體驗。

當今的線上消費者有不斷變化的需求，並期望從他們可以選擇的各種網站和內容來源中獲得相關甚至個人化的內容。 若要吸引線上受眾，線上行銷人員必須快速找出哪些優惠方案和內容與其受眾相關且吸引人，這一點至關重要。 有了這些知識，行銷人員便需要能夠持續改進其網站，並將適當內容鎖定在不同的受眾。

[與Adobe整](/help/sites-administering/target.md) 合Target說明如何將您的網站與Target整合。

您也可以使用[選擇加入精靈](/help/sites-administering/opt-in.md)輕鬆執行整合。

## 選擇加入Analytics和Target {#opting-in-to-analytics-and-target}

AEM提供簡單的選擇加入程式，以整合Adobe Analytics和Adobe Target。 以管理員身分登入並造訪專案主控台時，畫面會顯示選擇加入精靈。

![chlimage_1-107](assets/chlimage_1-107a.png)

選擇加入與Analytics和/或Target的整合，以啟用其頁面追蹤和分析功能及個人化功能的使用。 選擇加入時，您需要提供使用者帳戶資訊，並指定要追蹤的頁面。

如需詳細資訊，請參閱[選擇加入Adobe Analytics和Adobe Target。](/help/sites-administering/opt-in.md)

## 與AdobeDynamic Media Classic整合{#integrating-with-scene}

AdobeDynamic Media Classic是托管解決方案，可發佈、管理、增強及傳遞動態行銷資產和豐富的視覺化銷售至網頁、行動裝置、電子郵件、社交媒體、網際網路連線顯示器及列印。

在Adobe Experience Manager中，您可以直接從Adobe Experience Manager發佈數位資產到Dynamic Media Classic，也可以從Dynamic Media Classic發佈數位資產到Adobe Experience Manager。

此外，您還可以在各種檢視器（例如「基本縮放」和「影片」）中檢視在Dynamic Media Classic中發佈的Adobe Experience Manager資產。

如需Adobe Experience Manager如何與Dynamic Media Classic整合的詳細資訊，請參閱[與Dynamic Media Classic整合](/help/sites-administering/scene7.md)檔案。

## 與Adobe動態標籤管理整合{#integrating-with-adobe-dynamic-tag-management}

[Adobe動態標](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) 簽管理為行銷人員提供直覺式工具，以快速輕鬆管理不限數量的Adobe和協力廠商標籤。您將擁有更多控制能力和靈活性，幾乎可以優化任何線上內容，同時減少對IT資源的依賴。

[將AdobeDynamic Tag ](/help/sites-administering/dtm.md) Management與AEM整合，以便您能使用Dynamic Tag Management Web屬性來追蹤AEM網站。

## 與Adobe Audience Manager整合{#integrating-with-adobe-audience-manager}

AEM 6.3已移除Audience Manager整合。

## 與Search&amp;Promote{#integrating-with-search-promote}整合

AdobeSearch&amp;Promote可讓行銷人員最佳化訪客在網站和行動網站上瀏覽、尋找、比較及選取相關產品和內容的方式。 企業可根據業務目標和訪客意圖輕鬆促銷優先項目，並透過KPI型觸發器或量度，將銷售和促銷活動自動化。

AdobeSearch&amp;Promote是可靠且可擴充的托管網站搜尋應用程式，可針對從零售到新聞網站等受到大量造訪的線上業務，擴充至數百萬個頁面或產品。 它提供前所未有的行銷人員控制和量度相關性。

如需整合AEM和Search&amp;Promote的相關資訊，請參閱[與AdobeSearch&amp;Promote整合](/help/sites-administering/search-and-promote.md)。

## 與Adobe Campaign整合{#integrating-with-adobe-campaign}

[Adobe](https://www.adobe.com/solutions/campaign-management.html) 促銷活動可讓您直接在Adobe Experience Manager中管理電子郵件傳遞內容。

如需AEM如何與Adobe Campaign整合的詳細資訊，請參閱[與Adobe Campaign整合](/help/sites-administering/campaignstandard.md)。

## 與 Livefyre 整合 {#integrating-with-livefyre}

了解AEM和Livefyre:

* [Livefyre快速入門](https://answers.livefyre.com/developers/getting-started)

* [Livefyre與AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)
