---
title: 使用Adobe行動分析追蹤應用程式效能
seo-title: Track App Performance with Adobe Mobile Analytics
description: 透過AdobeMobile Services，您可以透過追蹤使用情形、應用程式當機、裝置詳細資訊，以及行動應用程式的其他許多重要量度，深入了解使用者使用您行動應用程式的方式。 請詳閱本頁以了解更多。
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
ht-degree: 0%

---

# 使用Adobe行動分析追蹤應用程式效能{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

您想要提高客戶轉換率和忠誠度。

您想要為客戶提供相關且吸引人的體驗。

您的AEM Mobile應用程式對行銷活動有何作用？

如何微調行動應用程式，為使用者提供最佳體驗？

透過AdobeMobile Services，您可以透過追蹤使用情形、應用程式當機、裝置詳細資訊，以及行動應用程式的其他許多重要量度，深入了解使用者使用您行動應用程式的方式。

Adobe Experience Manager Mobile可直接從AEM Mobile Application Dashboard ，一窺您的行動分析詳細資訊。 此 **行動量度圖磚** 在控制面板中，為您的行動應用程式提供即時分析，讓開發人員、作者和管理員快速了解行動應用程式的運作狀況。 在封面下方，加強分析的功能 [AdobeMobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK. 您可以透過原生或PhoneGap橋接器將AdobeMobile Analytics SDK插入應用程式，以供網頁檢視。 系統會在裝置上收集和快取量度，直到連線裝置為止，資料便會推送至AdobeMobile Services Cloud以供報告和分析。

AdobeMobile Analytics SDK提供下列功能：

1. **行動頻道的資料收集**  — 收集所有主要作業系統上行動網站和應用程式的完整資料。
1. **行動參與分析**  — 了解您行動應用程式、網站或影片中的使用者參與度，包括消費者啟動管道的頻率、是否透過該管道購買等。
1. **行動應用程式控制面板和報表**  — 取得使用狀況報表，其中包含應用程式和應用程式商店量度的生命週期量度 — 請參閱使用者、啟動、平均工作階段長度、保留長度和當機趨勢。
1. **行動促銷活動分析**  — 量化行動專屬行銷活動（例如簡訊、行動搜尋廣告、行動顯示廣告和QR碼）的成效。
1. **地理位置分析**  — 根據GPS位置或地標，尋找應用程式使用者啟動並與行動體驗互動的位置。
1. **路徑分析**  — 了解使用者如何導覽您的應用程式，以判斷哪些畫面和UI元素吸引使用者，哪些元素會導致使用者流失。

本節說明如何 [AEM開發人員](#developers) 接著，您就可以學習如何使用analytics追蹤來檢測AEM Mobile應用程式。

最後， [AEM管理員](#administrators) 了解：

* 建立雲端服務以AdobeMobile Services
* 建立行動服務設定並建立報表套裝的關聯
* 將行動服務設定關聯至行動應用程式
* 透過AEM Apps Command Center檢視量度
* 將AMS SDK設定指派至您的行動應用程式

## 針對開發人員 — 將Analytics整合至您的應用程式 {#for-developers-integrate-analytics-into-your-app}

**先決條件：** AEM管理員需要設定AdobeMobile Services雲端設定， [如下所述](#amscloudserviceconfig).

開發人員負責 [將analytics新增至AEM Mobile應用程式](/help/mobile/phonegap-add-analytics-to-apps.md) 必要時，追蹤、報告及了解使用者與行動應用程式內容的互動方式，以及測量關鍵生命週期量度（例如啟動次數、應用程式逗留時間和當機率）。

## 管理員 — 設定AdobeMobile ServicesCloud Service {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

若要利用AdobeMobile Services，您需使用您的Adobe Analytics帳戶資訊來設定AEMAdobeMobile ServicesCloud Service。 Apps Command Center提供 **分析量度** 圖磚，可讓您建立雲端服務與行動應用程式的關聯。

按一下「分析量度」方塊上的齒輪圖示，即可開始將雲端服務設定至您的行動應用程式。

![chlimage_1-125](assets/chlimage_1-125.png)

按一下「分析量度」方塊中的齒輪圖示，會開啟「設定Mobile Services Analytics」強制回應對話方塊。 從「選取行動服務設定」下拉式清單中選取您的設定。 如果您需要建立新配置，請按一下扳手按鈕。

若要建立AdobeMobile Service雲端服務，需執行兩個步驟：連線至服務，以及選取要指派給設定的報表套裝。

若要開始，請按一下控制面板中「管理Cloud Services」方塊上的「+」按鈕。

![chlimage_1-126](assets/chlimage_1-126.png)

按一下「**+**「按鈕， **新增Cloud Service** 精靈。

![chlimage_1-127](assets/chlimage_1-127.png)

填寫必填欄位，選取或建立新的行動服務設定，如下所示。 您的AEM管理員需要此資訊才能成功建立與AdobeMobile Services的連線。

![chlimage_1-128](assets/chlimage_1-128.png)

完成Mobile Services帳戶設定後，系統會提示您選取應用程式。 這麼做會將Adobe行動服務分析報表連結至該應用程式。

選擇所需的移動服務，然後按一下「更新」以分配移動服務配置並關閉對話框。

現在您已將行動服務設定與AEM Mobile應用程式建立關聯，圖磚將開始擷取量度資料並開始建立報表。

![chlimage_1-129](assets/chlimage_1-129.png)

### AdobeMobile Services SDK設定檔案 {#adobe-mobile-services-sdk-config-file}

此時，您的行動應用程式已與雲端服務建立關聯，但行動應用程式尚不知道如何將收集的行動量度傳回Adobe Analytics。 若要將行動應用程式連線至Adobe Analytics,AdobeMobile Services SDK設定檔案必須新增至Adobe Experience Manager。

在「分析量度」方塊中，按一下箭頭圖示以公開「下載/上傳AMS SDK設定」功能表項目。

![chlimage_1-130](assets/chlimage_1-130.png)

第一步是從AdobeMobile Services取得SDK設定，按一下「下載AMS SDK設定」會將您重新導向至AdobeMobile Services網站，您可從該網站下載設定檔案。 取得ADBMobileConfig.json檔案後，按一下「上傳AMS SDK設定」，將設定檔案上傳至AEM。

![chlimage_1-131](assets/chlimage_1-131.png)

按一下「上傳AdobeMobile Services應用程式設定」按鈕，並瀏覽ADBMobileConfig.json檔案，然後按一下「上傳」。

現在，行動應用程式可存取ADBMobileConfig.json檔案，且已具備如何傳回Adobe Analytics通訊的相關知識，並開始報告有助於促進應用程式成功的重要量度值。

## 下一步? {#what-s-next}

1. [開始我的AEM Mobile應用程式體驗](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我應用程式的內容](/help/mobile/phonegap-manage-app-content.md)
1. [構建我的應用程式](/help/mobile/building-app-mobile-phonegap.md)
1. [使用Adobe行動分析追蹤我應用程式的效能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [使用Adobe Target提供個人化應用程式體驗](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [傳送重要訊息給我的使用者](/help/mobile/phonegap-push-notifications.md)
