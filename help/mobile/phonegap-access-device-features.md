---
title: 存取裝置功能
description: 請依照本頁所述操作，瞭解如何建置存取裝置功能的Adobe Experience Manager (AEM)元件。 AEM PhoneGap Kitchen Sink GitHub存放庫為開發人員提供功能性AEM應用程式，該應用程式可說明數個核心Cordova API的使用情況。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 385f7924-e8ab-4dcb-83f0-7b81bead3dda
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 3%

---

# 存取裝置功能{#access-device-features}

>[!NOTE]
>
>Adobe建議對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

## 建立存取裝置功能的Adobe Experience Manager (AEM)元件 {#building-aem-components-that-access-device-features}

此 [AEM PhoneGap廚房水槽](https://github.com/blefebvre/aem-phonegap-kitchen-sink) GitHub存放庫為開發人員提供功能性AEM應用程式，說明如何使用數個核心Cordova API。 透過PhoneGap CLI在iOS或Android™上執行時，應用程式會開啟至下列頁面，其中包括其示範之每個裝置API的連結：

![chlimage_1-107](assets/chlimage_1-107.png)

這些裝置API元件的原始碼都是 [適用於GitHub](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/apps/brucelefebvre/kitchen-sink/components).

如需每個API使用方式的詳細資訊，請參閱Cordova外掛程式檔案(`https://docs.phonegap.com/en/4.0.0/cordova_plugins_pluginapis.md.html`)。

## 後續步驟 {#the-next-steps}

另請參閱 [透過AdobeMobile Analytics追蹤應用程式效能](/help/mobile/phonegap-intro-to-app-analytics.md).
