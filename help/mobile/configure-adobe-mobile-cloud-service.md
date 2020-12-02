---
title: 設定您的Adobe Mobile Services Cloud服務
seo-title: 設定您的Adobe Mobile Services Cloud服務
description: 請依照本頁來設定您的Adobe Mobile Services Cloud服務。
seo-description: 請依照本頁來設定您的Adobe Mobile Services Cloud服務。
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# 設定您的Adobe Mobile Services Cloud服務{#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

命令中心的&#x200B;**行動量度圖格**&#x200B;為行動應用程式提供即時分析。

[Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK可透過PhoneGap外掛程式提供。 量度會在裝置上收集並快取，直到裝置連線為止，屆時資料會推送至Adobe Mobile Services Cloud以進行報告和分析。

Adobe Mobile Analytics SDK提供下列功能：

1. **針對行動通道收集資料** -針對所有主要作業系統的行動網站和應用程式收集完整的資料。
1. **行動互動分析** -瞭解您行動應用程式、網站或視訊中的使用者互動，包括消費者啟動渠道的頻率、他們是否從渠道購買等。
1. **行動應用程式控制面板和報表** -取得包含應用程式生命週期度量和應用程式商店度量的使用狀況報表— 檢視使用者、啟動、平均作業長度、保留長度和當機的趨勢。
1. **行動宣傳分析** -量化行動特定宣傳的成效，例如SMS、行動搜尋廣告、行動展示廣告和QR Code。
1. **地理位置分析** -根據GPS位置或興趣點，尋找應用程式使用者在何處啟動並與行動體驗互動。
1. **路徑分析** -瞭解使用者如何瀏覽您的應用程式，以判斷哪些螢幕和UI元素吸引使用者，以及哪些元素導致使用者流失。

>[!CAUTION]
>
>**分析量度**&#x200B;標題只會在您已設定雲端服務時顯示在控制面板中。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM命令中心量度圖格

## 設定雲端服務{#configuring-the-cloud-service}

為了善用Adobe Mobile Services Analytics，您需要使用您的Adobe Analytics帳戶資訊來設定AEM Mobile Analytics Cloud服務。

1. 按一下右上角的圖示，從應用程式儀表板的「管理雲端服務」方塊中新增或編輯雲端服務。****

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. 將顯示&#x200B;**新增或編輯雲端服務**&#x200B;畫面。 選擇&#x200B;**Adobe Mobile Services**，然後按一下&#x200B;**Next**。

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 從&#x200B;**Mobile Services**&#x200B;中選擇現有配置，或選擇&#x200B;**建立配置**&#x200B;建立新配置。

   對於新配置，請輸入&#x200B;**Mobile Services屬性**，然後按一下&#x200B;**驗證。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果認證通過，則&#x200B;**Verify**&#x200B;按鈕將更改為&#x200B;**Verified**。 您可以從&#x200B;**選擇行動應用程式服務**&#x200B;中選擇行動服務應用程式。

   按一下&#x200B;**Submit**&#x200B;設定配置。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 設定雲端設定後，您就可以在控制面板中檢視相同的設定。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >設定雲端設定後，您就可以在應用程式儀表板中檢視「分析量度&#x200B;**圖格」。**

   ![chlimage_1-28](assets/chlimage_1-28.png)

