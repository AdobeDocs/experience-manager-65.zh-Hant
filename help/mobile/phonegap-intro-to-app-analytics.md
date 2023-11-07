---
title: 透過AdobeMobile Analytics追蹤應用程式效能
description: 透過AdobeMobile Services，您可以追蹤使用情形、應用程式當機、裝置詳細資訊，以及其他許多行動應用程式的關鍵量度，深入瞭解使用者如何使用行動應用程式。 請依照此頁面瞭解更多資訊。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 1%

---

# 透過AdobeMobile Analytics追蹤應用程式效能{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md)。

您希望提高客戶轉換率和忠誠度。

您想要為客戶提供相關且吸引人的體驗。

您的AEM Mobile應用程式對行銷活動有何影響？

如何微調行動應用程式以提供使用者最佳體驗？

透過AdobeMobile Services，您可以追蹤使用情形、應用程式當機、裝置詳細資訊，以及其他許多行動應用程式的關鍵量度，深入瞭解使用者如何使用行動應用程式。

Adobe Experience Manager Mobile可讓您直接從AEM Mobile應用程式控制面板，快速瞭解行動分析的詳細資訊。 此 **行動量度圖磚** 儀表板為行動應用程式提供Real-Time Analytics，讓開發人員、作者和管理員快速瞭解行動應用程式的運作狀況。 在封面底下，為分析提供動力的是 [Adobe行動裝置資料分析](https://business.adobe.com/products/analytics/mobile-marketing.html) SDK. AdobeMobile Analytics SDK可以原生或透過PhoneGap Bridge外掛程式插入您的應用程式以進行網頁檢視。 系統會收集量度並在裝置上快取，直到裝置連線為止；資料會推送至AdobeMobile Services雲端，以便進行報表和分析。

Adobe Mobile Analytics SDK提供下列功能：

1. **行動頻道的資料收集**  — 收集您行動網站及所有主要作業系統應用程式的完整資料。
1. **行動參與分析**  — 瞭解使用者在您行動應用程式、網站或視訊中的參與情形，包括消費者啟動頻道的頻率、是否從中進行購買等等。
1. **行動應用程式控制面板和報表**  — 取得包含應用程式生命週期量度和應用程式商店量度的使用情況報表 — 檢視使用者、啟動次數、平均工作階段長度、保留時間長度和當機次數趨勢。
1. **行動促銷活動分析**  — 量化行動裝置特定行銷活動的有效性，例如SMS、行動搜尋廣告、行動顯示廣告和二維碼。
1. **地理位置分析**  — 透過GPS位置或地標，找出您的應用程式使用者從何處啟動並與行動體驗互動。
1. **路徑分析**  — 瞭解使用者如何導覽您的應用程式，以判斷哪些畫面和UI元素吸引使用者，以及哪些造成使用者流失。

本節說明如何進行 [AEM開發人員](#developers) 然後可以瞭解如何透過analytics追蹤來檢測AEM Mobile應用程式。

最後， [AEM管理員](#administrators) 瞭解：

* 建立雲端服務以Adobe行動服務
* 建立行動服務設定並關聯報表套裝
* 將行動服務設定與行動應用程式建立關聯
* 透過AEM應用程式命令中心檢視量度
* 將AMS SDK設定指派至您的行動應用程式

## 適用於開發人員 — 將Analytics整合至您的應用程式 {#for-developers-integrate-analytics-into-your-app}

**先決條件：** AEM管理員必須設定AdobeMobile Services雲端設定， [如下所述](#amscloudserviceconfig).

開發人員需負責 [將analytics新增至AEM Mobile應用程式](/help/mobile/phonegap-add-analytics-to-apps.md) 需要追蹤、報告及瞭解使用者如何與您的行動應用程式內容互動，以及測量啟動、應用程式逗留時間和當機率等關鍵生命週期量度。

## 適用於管理員 — 設定Adobe行動服務Cloud Service {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

若要妥善運用Adobe Mobile Services的優勢，您必須使用Adobe Analytics帳戶資訊設定AEM Adobe Mobile ServicesCloud Service。 應用程式命令中心提供 **分析量度** 您可在其中建立雲端服務並將其與行動應用程式建立關聯的圖磚。

若要設定行動應用程式的雲端服務，請從按一下「分析量度」圖磚上的齒輪圖示開始。

![chlimage_1-125](assets/chlimage_1-125.png)

按一下分析量度圖磚中的齒輪圖示，開啟「設定Mobile Services Analytics」強制回應對話方塊。 從「選取行動服務設定」下拉式清單中選取您的設定。 如果您必須建立組態，請按一下扳手按鈕。

若要建立Adobe Mobile Service雲端服務，有兩個相關步驟：連線至服務以及選取要指派給設定的報表套裝。

若要開始，請按一下控制面板中「管理Cloud Service」表徵圖上的「+」按鈕。

![chlimage_1-126](assets/chlimage_1-126.png)

按一下「**+**&#39;按鈕， **新增Cloud Service** 精靈隨即顯示。

![chlimage_1-127](assets/chlimage_1-127.png)

填寫下列必填欄位，以選取或建立行動服務設定。 您的AEM管理員需要此資訊才能成功建立與Adobe行動服務的連線。

![chlimage_1-128](assets/chlimage_1-128.png)

完成Mobile Services帳戶設定後，系統會提示您選取應用程式。 這麼做會將Adobe Mobile Service分析報表連線至該應用程式。

選取所需的行動服務，然後按一下「更新」以指派行動服務設定，並關閉對話方塊。

現在您已將行動服務設定與AEM Mobile應用程式建立關聯，圖磚會開始擷取量度資料並開始製作報表。

![chlimage_1-129](assets/chlimage_1-129.png)

### AdobeMobile Services SDK設定檔案 {#adobe-mobile-services-sdk-config-file}

此時，您的行動應用程式已與雲端服務相關聯，但行動應用程式還不知道如何將收集到的行動量度傳回Adobe Analytics。 若要將行動應用程式連線至Adobe Analytics，必須將Adobe Mobile Services SDK設定檔案新增至Adobe Experience Manager。

在分析量度圖磚中，按一下箭頭圖示，以顯示「下載/上傳AMS SDK設定」功能表專案。

![chlimage_1-130](assets/chlimage_1-130.png)

第一步是從Adobe Mobile Services取得SDK設定。 按一下「下載AMS SDK設定」重新導向至AdobeMobile Services網站，您可在其中下載設定檔案。 取得ADBMobileConfig.json檔案後，按一下「上傳AMS SDK設定」將設定檔案上傳至AEM。

![chlimage_1-131](assets/chlimage_1-131.png)

按一下「上傳AdobeMobile Services應用程式設定」按鈕，並瀏覽ADBMobileConfig.json檔案，然後按一下「上傳」。

行動應用程式現在已可存取ADBMobileConfig.json檔案，並已瞭解如何傳回Adobe Analytics及開始回報這些有助於促進應用程式成功的重要量度值。

## 下一步? {#what-s-next}

1. [開始我的AEM Mobile應用程式體驗](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的應用程式內容](/help/mobile/phonegap-manage-app-content.md)
1. [建置我的應用程式](/help/mobile/building-app-mobile-phonegap.md)
1. [透過AdobeMobile Analytics追蹤我的應用程式效能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [使用Adobe Target提供個人化應用程式體驗](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [傳送重要訊息給我的使用者](/help/mobile/phonegap-push-notifications.md)
