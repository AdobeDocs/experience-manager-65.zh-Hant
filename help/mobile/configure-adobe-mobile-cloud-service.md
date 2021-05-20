---
title: 設定您的AdobeMobile ServicesCloud Service
seo-title: 設定您的AdobeMobile ServicesCloud Service
description: 請依照本頁面設定您的AdobeMobile ServicesCloud Service。
seo-description: 請依照本頁面設定您的AdobeMobile ServicesCloud Service。
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 設定您的AdobeMobile ServicesCloud Service{#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

命令中心上的&#x200B;**行動量度圖磚**&#x200B;可為行動應用程式提供即時分析。

[AdobeMobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK可透過PhoneGap外掛程式使用。 系統會在裝置上收集和快取量度，直到裝置連線為止，此時資料會推送至AdobeMobile Services Cloud以供報告和分析。

AdobeMobile Analytics SDK提供下列功能：

1. **行動管道的資料收集**  — 收集所有主要作業系統上行動網站和應用程式的完整資料。
1. **行動參與分析**  — 了解您行動應用程式、網站或影片中的使用者參與，包括消費者啟動管道的頻率、是否透過該管道購買等。
1. **行動應用程式控制面板和報表**  — 取得使用狀況報表，其中包含應用程式的生命週期量度和應用程式商店量度 — 請參閱使用者趨勢、啟動、平均工作階段長度、保留時間長度和當機。
1. **行動行銷活動分析**  — 量化行動專屬行銷活動（例如簡訊、行動搜尋廣告、行動顯示廣告和QR碼）的成效。
1. **地理位置分析**  — 依GPS位置或地標，尋找應用程式使用者在何處啟動並與您的行動體驗互動。
1. **路徑分析**  — 查看使用者如何導覽您的應用程式，以判斷哪些畫面和UI元素吸引使用者，哪些元素會導致使用者流失。

>[!CAUTION]
>
>「**分析量度** 」圖磚只會在您已設定雲端服務時，才會顯示在控制面板中。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center量度圖磚

## 配置Cloud Service{#configuring-the-cloud-service}

若要利用Mobile Services AnalyticsAdobe，您必須使用您的Adobe Analytics帳戶資訊來設定AEM Mobile Analytics Cloud服務。

1. 按一下右上角圖示，從應用程式控制面板的&#x200B;**管理Cloud Services**&#x200B;方塊新增或編輯Cloud Services。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. **新增或編輯Cloud Services**&#x200B;畫面隨即顯示。 選取&#x200B;**AdobeMobile Services**&#x200B;並按一下&#x200B;**下一步**。

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 從&#x200B;**Mobile Services**&#x200B;中選擇現有配置，或選擇&#x200B;**建立配置**&#x200B;建立新配置。

   對於新配置，請輸入&#x200B;**Mobile Services屬性**，然後按一下&#x200B;**驗證。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果驗證了憑據，**Verify**&#x200B;按鈕將更改為&#x200B;**Verified**。 您可以從&#x200B;**選取行動應用程式服務**&#x200B;中選擇行動服務應用程式。

   按一下&#x200B;**Submit**&#x200B;以設定配置。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 設定雲端設定後，您就可以在控制面板中檢視相同的設定。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >設定雲端設定後，您就可以在應用程式控制面板中檢視「**分析量度** 」圖磚。

   ![chlimage_1-28](assets/chlimage_1-28.png)
