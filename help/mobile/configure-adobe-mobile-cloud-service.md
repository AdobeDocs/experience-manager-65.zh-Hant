---
title: 設定您的AdobeMobile ServicesCloud Service
seo-title: Configure your Adobe Mobile Services Cloud Service
description: 請依照本頁面設定您的AdobeMobile ServicesCloud Service。
seo-description: Follow this page to configure your Adobe Mobile Services Cloud Service.
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
source-wordcount: '450'
ht-degree: 2%

---

# 設定您的AdobeMobile ServicesCloud Service {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

此 **行動量度圖磚** 在命令中心，為您的行動應用程式提供即時分析。

此 [AdobeMobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK可透過PhoneGap外掛程式使用。 系統會在裝置上收集和快取量度，直到裝置連線為止，此時資料會推送至AdobeMobile Services Cloud以供報告和分析。

AdobeMobile Analytics SDK提供下列功能：

1. **行動頻道的資料收集**  — 收集所有主要作業系統上行動網站和應用程式的完整資料。
1. **行動參與分析**  — 了解您行動應用程式、網站或影片中的使用者參與度，包括消費者啟動管道的頻率、是否透過該管道購買等。
1. **行動應用程式控制面板和報表**  — 取得使用狀況報表，其中包含應用程式和應用程式商店量度的生命週期量度 — 請參閱使用者、啟動、平均工作階段長度、保留長度和當機趨勢。
1. **行動促銷活動分析**  — 量化行動專屬行銷活動（例如簡訊、行動搜尋廣告、行動顯示廣告和QR碼）的成效。
1. **地理位置分析**  — 根據GPS位置或地標，尋找應用程式使用者啟動並與行動體驗互動的位置。
1. **路徑分析**  — 了解使用者如何導覽您的應用程式，以判斷哪些畫面和UI元素吸引使用者，哪些元素會導致使用者流失。

>[!CAUTION]
>
>此 **分析量度** 圖磚會顯示在控制面板中，唯有在您已設定雲端服務時。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center量度圖磚

## 設定Cloud Service {#configuring-the-cloud-service}

若要利用Mobile Services AnalyticsAdobe，您必須使用您的Adobe Analytics帳戶資訊來設定AEM Mobile Analytics Cloud服務。

1. 按一下右上角的圖示，即可新增或編輯Cloud Services **管理Cloud Services** 圖磚。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. 此 **新增或編輯Cloud Services** 畫面隨即顯示。 選擇 **AdobeMobile Services** 按一下 **下一個**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 從 **Mobile Services** 或選擇 **建立配置** 來建立新的。

   若為新設定，請輸入 **Mobile Services屬性**&#x200B;按一下&#x200B;**驗證。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果驗證了憑據，則 **驗證** 按鈕變更為 **已驗證**. 您可以選擇行動服務應用程式，從 **選取行動應用程式服務**.

   按一下 **提交** 來設定您的設定。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 設定雲端設定後，您就可以在控制面板中檢視相同的設定。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >設定雲端設定後，即可檢視 **分析量度** 在應用程式控制面板中平鋪。

   ![chlimage_1-28](assets/chlimage_1-28.png)
