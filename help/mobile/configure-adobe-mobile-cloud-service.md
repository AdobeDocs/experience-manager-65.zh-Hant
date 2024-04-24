---
title: 設定您的Adobe Mobile ServicesCloud Service
description: 請依照本頁面的說明設定您的Adobe Mobile ServicesCloud Service。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 3%

---

# 設定您的Adobe Mobile ServicesCloud Service {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

此 **行動量度圖磚** 指揮中心為您的行動應用程式提供即時分析。

此 [Adobe行動裝置資料分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK可透過PhoneGap外掛程式使用。 系統會在裝置上收集量度並加以快取，直到裝置連線為止，此時資料會推送至AdobeMobile Services雲端，以供報表和分析。

Adobe Mobile Analytics SDK提供下列功能：

1. **行動頻道的資料收集**  — 收集您行動網站及所有主要作業系統應用程式的完整資料。
1. **行動參與分析**  — 瞭解使用者在您行動應用程式、網站或視訊中的參與情形，包括消費者啟動頻道的頻率、是否從中進行購買等等。
1. **行動應用程式控制面板和報表**  — 取得包含應用程式生命週期量度和應用程式商店量度的使用情況報表 — 檢視使用者、啟動次數、平均工作階段長度、保留時間長度和當機次數趨勢。
1. **行動促銷活動分析**  — 量化行動裝置特定行銷活動的有效性，例如SMS、行動搜尋廣告、行動顯示廣告和二維碼。
1. **地理位置分析**  — 透過GPS位置或地標，找出您的應用程式使用者從何處啟動並與行動體驗互動。
1. **路徑分析**  — 瞭解使用者如何導覽您的應用程式，以判斷哪些畫面和UI元素吸引使用者，以及哪些造成使用者流失。

>[!CAUTION]
>
>此 **分析量度** 只有在您已設定雲端服務時，控制面板中才會顯示圖磚。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center度量圖磚

## 設定Cloud Service {#configuring-the-cloud-service}

若要利用Adobe Mobile Services Analytics的優勢，您需要使用Adobe Analytics帳戶資訊設定AEM Mobile Analytics Cloud Service 。

1. 按一下右上角的圖示，從新增或編輯Cloud Service **管理Cloud Service** 從應用程式儀表板中動態磚。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. 此 **新增或編輯Cloud Service** 熒幕顯示。 選取 **Adobe行動服務** 並按一下 **下一個**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 從中選擇現有設定 **行動服務** 或選擇 **建立設定** 以建立一個。

   若為新組態，請輸入 **行動服務屬性**&#x200B;並按一下&#x200B;**驗證。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果認證已驗證， **驗證** 按鈕變更為 **已驗證**. 您可從中選擇行動服務應用程式 **選取行動應用程式服務**.

   按一下 **提交** 以設定您的設定。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 設定雲端設定後，您即可在控制面板中檢視相同的設定。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >設定雲端設定後，您就可以檢視 **分析量度** 在您應用程式儀表板中的動態磚。

   ![chlimage_1-28](assets/chlimage_1-28.png)
