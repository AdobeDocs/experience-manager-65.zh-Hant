---
title: 使用AdobeMobile分析跟蹤應用效能
seo-title: Track App Performance with Adobe Mobile Analytics
description: 通過Adobe移動服務，您可以通過跟蹤移動應用的使用情況、應用崩潰、設備詳細資訊和許多其他關鍵指標，瞭解用戶如何使用移動應用。 請按照此頁瞭解詳細資訊。
seo-description: With Adobe Mobile Services you can gain insight on how your users are using your mobile apps by tracking usage, app crashes, device details and so many other critical metrics for your mobile apps. Follow this page to learn more.
uuid: 139858c7-66a1-4fea-9f7e-4671b86f67e6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 377548fa-987a-4a59-84a3-067a3541b6b2
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 1%

---

# 使用AdobeMobile分析跟蹤應用效能{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

您希望提高客戶轉換和忠誠度。

您希望為客戶提供相關且引人入勝的體驗。

你的AEM Mobile應用為你的營銷活動做了什麼？

您如何調整移動應用程式，為用戶提供最佳體驗？

通過Adobe移動服務，您可以通過跟蹤移動應用的使用情況、應用崩潰、設備詳細資訊和許多其他關鍵指標，瞭解用戶如何使用移動應用。

Adobe Experience Manager Mobile直接從AEM Mobile應用程式儀表板瞭解您的移動分析的詳細資訊。 的 **移動度量平鋪** 在儀表板中為您的移動應用程式提供即時分析，使開發人員、作者和管理員能夠快速查看您的移動應用程式的運行狀況。 在分析的封面下 [Adobe移動分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK。 AdobeMobile Analytics SDK可以本機或通過PhoneGap網橋插件插入您的應用程式，用於Web視圖。 度量被收集並快取在設備上，直到設備被連接，資料被推送到Adobe移動服務雲以進行報告和分析。

AdobeMobile Analytics SDK提供以下功能：

1. **用於移動通道的資料收集**  — 收集所有主要作業系統上的移動網站和應用程式的全面資料。
1. **移動接洽分析**  — 瞭解您的移動應用、網站或視頻中的用戶參與，包括消費者啟動該渠道的頻率、他們是否從該渠道進行購買等。
1. **移動應用儀表板和報告**  — 獲取包含應用程式和應用商店度量的生命週期度量的使用情況報告 — 請參閱用戶趨勢、啟動、平均會話長度、保留長度和崩潰。
1. **移動活動分析**  — 量化特定移動活動（如簡訊、移動搜索廣告、移動顯示廣告和二維碼）的效果。
1. **地理位置分析**  — 查找應用程式用戶在何處啟動，並通過GPS位置或興趣點與您的移動體驗進行交互。
1. **路徑分析**  — 查看用戶如何在您的應用程式中導航，以確定哪些螢幕和UI元素正在吸引用戶，哪些會導致用戶退出。

本節介紹如何 [開發AEM人員](#developers) 然後學習如何利用分析跟蹤來測量AEM Mobile應用。

終於， [管AEM理員](#administrators) 學習：

* 建立雲服務以Adobe移動服務
* 建立移動服務配置並關聯報表套件
* 將移動服務配置與移動應用關聯
* 通過應用命令中AEM心查看度量
* 將AMS SDK配置分配給您的移動應用

## 面向開發人員 — 將分析整合到您的應用 {#for-developers-integrate-analytics-into-your-app}

**先決條件：** 管理AEM員需要配置Adobe移動服務雲配置， [下面討論](#amscloudserviceconfig)。

開發人員負責 [向AEM Mobile應用添加分析](/help/mobile/phonegap-add-analytics-to-apps.md) 根據需要跟蹤、報告和瞭解您的用戶如何使用您的移動應用程式內容，並衡量關鍵生命週期指標，如啟動、應用程式時間和崩潰率。

## 對於管理員 — 配置Adobe移動服務Cloud Service {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

為了利用Adobe移動服務，您需要使用您的Adobe Analytics帳AEM戶資訊配置Adobe移動服務Cloud Service。 應用命令中心提供 **分析度量** 在磁貼中，您可以建立雲服務並將其與移動應用關聯。

通過按一下「分析度量」磁貼上的齒輪表徵圖，開始將雲服務配置到您的移動應用。

![chlimage_1-125](assets/chlimage_1-125.png)

按一下「分析度量」磁貼中的齒輪表徵圖將開啟「配置移動服務分析」模式對話框。 從「選擇移動服務配置」下拉清單中選擇配置。 如果需要建立新配置，請按一下扳手按鈕。

要建立Adobe移動服務雲服務，需要執行兩個步驟：連接到服務並選擇要分配給配置的報告套件。

要開始，請按一下儀表板中「管理Cloud Services」磁貼上的「+」按鈕。

![chlimage_1-126](assets/chlimage_1-126.png)

按一下「 」**+**「按鈕， **添加Cloud Service** 的子菜單。

![chlimage_1-127](assets/chlimage_1-127.png)

通過填寫必填欄位來選擇或建立新的移動服務配置，如下所示。 您的AEM管理員將需要此資訊才能成功建立到Adobe移動服務的連接。

![chlimage_1-128](assets/chlimage_1-128.png)

完成移動服務帳戶設定後，系統將提示您選擇應用。 這樣可將AdobeMobile Service分析報告連接到該應用程式。

選擇所需的移動服務，然後按一下「更新」以分配移動服務配置並關閉對話框。

現在，您已將移動服務配置關聯到AEM Mobile應用，磁貼將開始獲取度量資料並開始報告。

![chlimage_1-129](assets/chlimage_1-129.png)

### Adobe移動服務SDK配置檔案 {#adobe-mobile-services-sdk-config-file}

此時，您的移動應用程式與雲服務相關聯，但移動應用程式尚不知道如何將收集到的移動指標傳回Adobe Analytics。 要將移動應用連接到Adobe Analytics，需要將Adobe移動服務SDK配置檔案添加到Adobe Experience Manager。

在「分析度量」磁貼中，按一下箭頭表徵圖以顯示「下載/上載AMS SDK配置」菜單條目。

![chlimage_1-130](assets/chlimage_1-130.png)

第一步是從Adobe移動服務獲取SDK配置，按一下「下載AMS SDK配置」會將您重定向到Adobe移動服務網站，您可以從中下載配置檔案。 獲取ADBMobileConfig.json檔案後，按一下「上載AMS SDK配置」將配置檔案上載到AEM。

![chlimage_1-131](assets/chlimage_1-131.png)

按一下「上載Adobe移動服務應用程式配置」按鈕，瀏覽ADBMobileConfig.json檔案，然後按一下「上載」。

現在，移動應用可以訪問ADBMobileConfig.json檔案，它已掌握了如何與Adobe Analytics通信並開始報告有助於推動應用成功的重要指標值的知識。

## 下一步? {#what-s-next}

1. [啟動我的AEM Mobile應用體驗](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的應用的內容](/help/mobile/phonegap-manage-app-content.md)
1. [構建我的應用程式](/help/mobile/building-app-mobile-phonegap.md)
1. [使用AdobeMobile Analytics跟蹤我的應用的效能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [通過Adobe Target提供個性化的應用體驗](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [向我的用戶發送重要消息](/help/mobile/phonegap-push-notifications.md)
