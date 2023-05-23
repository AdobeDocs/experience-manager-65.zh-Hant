---
title: 配置Adobe移動服務Cloud Service
seo-title: Configure your Adobe Mobile Services Cloud Service
description: 按照此頁配置Adobe移動服務Cloud Service。
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

# 配置Adobe移動服務Cloud Service {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

的 **移動度量平鋪** 命令中心為移動應用程式提供即時分析。

的 [Adobe移動分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK通過PhoneGap插件提供。 度量被收集並快取在設備上，直到設備被連接，此時資料被推送到Adobe移動服務雲以用於報告和分析。

AdobeMobile Analytics SDK提供以下功能：

1. **用於移動通道的資料收集**  — 收集所有主要作業系統上的移動網站和應用程式的全面資料。
1. **移動接洽分析**  — 瞭解您的移動應用、網站或視頻中的用戶參與，包括消費者啟動該渠道的頻率、他們是否從該渠道進行購買等。
1. **移動應用儀表板和報告**  — 獲取包含應用程式和應用商店度量的生命週期度量的使用情況報告 — 請參閱用戶趨勢、啟動、平均會話長度、保留長度和崩潰。
1. **移動活動分析**  — 量化特定移動活動（如簡訊、移動搜索廣告、移動顯示廣告和二維碼）的效果。
1. **地理位置分析**  — 查找應用程式用戶在何處啟動，並通過GPS位置或興趣點與您的移動體驗進行交互。
1. **路徑分析**  — 查看用戶如何在您的應用程式中導航，以確定哪些螢幕和UI元素正在吸引用戶，哪些會導致用戶退出。

>[!CAUTION]
>
>的 **分析度量** 磁貼僅在配置了雲服務後才顯示在儀表板中。

![chlimage_1-22](assets/chlimage_1-22.png)

命AEM令中心度量平鋪

## 配置Cloud Service {#configuring-the-cloud-service}

為了利用Adobe移動服務分析，您需要使用您的Adobe Analytics帳戶資訊配置AEM MobileAnalytics Cloud服務。

1. 按一下右上角的表徵圖可添加或編輯Cloud Services **管理Cloud Services** 從應用儀表板中平鋪。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. 的 **添加或編輯Cloud Services** 螢幕。 選擇 **Adobe移動服務** 按一下 **下一個**。

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 從 **移動服務** 或 **建立配置** 的雙曲餘切值。

   對於新配置，請輸入 **移動服務屬性**&#x200B;按一下&#x200B;**驗證。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果驗證憑據， **驗證** 按鈕更改 **已驗證**。 可以從中選擇移動服務應用 **選擇移動應用服務**。

   按一下 **提交** 設定配置。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 設定雲配置後，您可以在儀表板中查看相同的配置。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >設定雲配置後，您可以查看 **分析度量** 在應用儀表板中平鋪。

   ![chlimage_1-28](assets/chlimage_1-28.png)
