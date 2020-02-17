---
title: 與Adobe Marketing cloud整合
seo-title: 與Adobe Marketing cloud整合
description: 瞭解如何將AEM與Adobe Marketing cloud整合。
seo-description: 瞭解如何將AEM與Adobe Marketing cloud整合。
uuid: 36d71dd3-7fb0-4237-99d3-4fbb2e162e7b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ba496f6a-c9aa-49b5-8207-8633748d2c17
translation-type: tm+mt
source-git-commit: 471b57a52efc849eb57201e6397221fa4f88c746

---


# 與Adobe Marketing cloud整合{#integrating-with-the-adobe-marketing-cloud}

Adobe Marketing Cloud [](https://www.adobe.com/solutions/digital-marketing.html)，包含功能強大的網頁分析和網站最佳化產品，可提供可操作的即時資料和見解，以推動成功的線上活動。 它為線上業務最佳化提供整合式開放平台。 Cloud包含整合式應用程式，可收集和釋放客戶洞察力，以最佳化客戶獲取、轉化和維繫，以及內容的建立和發佈。

有了Adobe Experience Manager(AEM)，您就可以與下列Adobe Marketing cloud產品完美整合：

* Adobe Analytics為行銷人員提供有關線上策略和行銷舉措的可操作、即時智慧。
* Adobe Target讓行銷人員能夠持續提升其線上內容與客戶的關聯性。 產生更高的轉換率。
* Adobe Scene7可在代管環境中自動化媒體管理、簡化網頁發佈並增強網頁體驗。
* Adobe動態標籤管理為行銷人員提供直覺式工具，可快速輕鬆管理不限數量的Adobe和協力廠商標籤。
* Adobe Search&amp;Promote讓行銷人員能夠控制並最佳化其網站上的搜尋結果。
* Adobe Campaign可讓您直接在Adobe Experience manager中管理電子郵件傳送內容。

此外，您還可 [以將AEM與Creative cloud及協力廠](/help/assets/aem-cc-folder-sharing-best-practices.md) 商服務整合 [](/help/sites-administering/third-party-services.md)。

## 與Adobe Analytics整合 {#integrating-with-adobe-analytics}

[Adobe Analytics是領先業界的解決方案](https://www.omniture.com/en/products/analytics/sitecatalyst) ，為數位行銷人員提供一個集中位置，來測量、分析和最佳化來自多個行銷通道上所有線上活動的整合資料。 它為行銷人員提供有關數位策略和行銷舉措的可操作、即時的網頁分析智慧。 Adobe Analytics可協助行銷人員快速識別網站中獲利最多的路徑、區隔流量以找出高價值網站訪客、判斷訪客離開網站的位置，以及識別線上行銷活動的關鍵成功度量。

您可以使用Adobe Analytics來分析網站的資料。

與Adobe Analytics整合可讓您執行下列工作：

* 啟用Analytics使用者追蹤。
* 將您的執行模式（例如作者、發佈）對應至不同的報表套裝。
* 提交用戶端內容變數作為轉換變數或流量屬性。
* 使用預先定義的變數映射。
* 一次設定完整網站區域。
* 追蹤自訂事件。

如需有關整合AEM與Analytics的詳細資訊，請參 [閱「與Adobe Analytics整合」](/help/sites-administering/adobeanalytics.md)。

您也可以使用 [選擇加入精靈](/help/sites-administering/opt-in.md) ，輕鬆執行整合。

## 與Adobe Target整合 {#integrating-with-adobe-target}

[行銷人員使用Adobe Target](https://www.omniture.com/en/products/conversion/test-and-target) ，來設計和執行線上測試、建立即時受眾細分（根據行為）並自動鎖定內容和線上體驗。

現今的線上消費者有不斷演變的需求，並期望從各種網站和內容來源獲得相關、甚至個人化的內容。 若要吸引線上受眾，線上行銷人員必須快速找出哪些優惠和內容對受眾有關聯且有吸引力，這一點至關重要。 有了這些知識，行銷人員需要不斷改進其網站並針對不同受眾鎖定適當內容的能力。

[與Adobe Target整合](/help/sites-administering/target.md) ，說明如何將網站與Target整合。

您也可以使用 [選擇加入精靈](/help/sites-administering/opt-in.md) ，輕鬆執行整合。

## 選擇加入Analytics和Target {#opting-in-to-analytics-and-target}

AEM提供簡單的加入程式，可與Adobe Analytics和Adobe Target整合。 當您以管理員身分登入並造訪「專案」主控台時，會顯示選擇加入精靈。

![chlimage_1-107](assets/chlimage_1-107a.png)

選擇與Analytics和／或Target整合，以啟用其頁面追蹤和分析功能以及個人化功能。 當您選擇加入時，您需要提供您的使用者帳戶資訊並指定要追蹤的頁面。

如需詳細資訊，請 [參閱「選擇加入Adobe Analytics和Adobe Target」。](/help/sites-administering/opt-in.md)

## 與Scene7整合 {#integrating-with-scene}

[Adobe Scene7是代管解決方案](https://www.adobe.com/products/scene7.html) ，適用於發佈、管理、增強和提供動態行銷資產和豐富視覺化銷售至網頁、行動裝置、電子郵件、社交媒體、網際網路連線的顯示器和印刷品。

在AEM中，您可以直接從AEM發佈數位資產至Scene7，也可以從Scene7發佈數位資產至AEM。

此外，您也可以在各種檢視器中檢視發佈於Scene7的AEM資產：

* 基本縮放
* DHTML 彈出式縮放
* Flash 彈出式縮放
* 視訊
* Flash 範本
* 影像範本

如需AEM如何與Scene7整合的詳細資訊，請參閱「與 [Scene7整合」檔案](/help/sites-administering/scene7.md)。

## 與Adobe動態標籤管理整合 {#integrating-with-adobe-dynamic-tag-management}

[Adobe動態標籤管理](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) (Dynamic Tag Management)為行銷人員提供直覺式工具，讓他們快速輕鬆地管理不限數量的Adobe和協力廠商標籤。 您將擁有更多的控制能力和靈活性，可以優化幾乎任何線上內容，同時減少對IT資源的依賴。

[將Adobe Dynamic Tag Management與AEM整合](/help/sites-administering/dtm.md) ，讓您可以使用「動態標籤管理」網頁屬性來追蹤AEM網站。

## 與Adobe Audience manager整合 {#integrating-with-adobe-audience-manager}

AEM 6.3已移除Audience manager整合。

## 與Search&amp;Promote整合 {#integrating-with-search-promote}

[Adobe Search&amp;Promote可讓行銷人員最佳化訪客在網站和行動網站上瀏覽、尋找、比較及選擇相關產品和內容的方式。](https://www.omniture.com/en/products/conversion/search-and-promote) 企業可以根據業務目標和訪客意願輕鬆促銷優先項目，並透過KPI型觸發器或量度自動化銷售和促銷活動。

Adobe Search&amp;Promote是可靠且可擴充的代管網站搜尋應用程式，可擴充至數百萬個頁面或產品，適用於從零售到新聞網站等造訪頻繁的線上企業。 它提供前所未有的行銷人員控制與量度相關性。

如需整合AEM和Search&amp;Promote的詳細資訊，請參 [閱「與Adobe Search&amp;Promote整合」](/help/sites-administering/search-and-promote.md)。

## 與Adobe Campaign整合 {#integrating-with-adobe-campaign}

[Adobe Campaign可讓](https://www.adobe.com/solutions/campaign-management.html) 您直接在Adobe Experience manager中管理電子郵件傳送內容。

如需AEM如何與Adobe Campaign整合的詳細資訊，請參 [閱「與Adobe Campaign整合」](/help/sites-administering/campaignstandard.md)。

## 與Livefyre整合 {#integrating-with-livefyre}

瞭解AEM和Livefyre:

* [Livefyre快速入門](https://answers.livefyre.com/developers/getting-started)

* [Livefyre與AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

