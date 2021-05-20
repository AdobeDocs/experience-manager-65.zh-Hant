---
title: 在AEM中開發行動應用程式
seo-title: 在AEM中開發行動應用程式
description: 請依照本頁面操作，開始使用Adobe PhoneGap Enterprise在AEM中開發行動應用程式。
seo-description: 請依照本頁面操作，開始使用Adobe PhoneGap Enterprise在AEM中開發行動應用程式。
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# 在AEM中開發行動應用程式{#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM運用Adobe PhoneGap和Adobe發佈解決方案，讓您建立和管理內容豐富且以公用程式為基礎的跨平台行動應用程式：

* 在一個位置管理所有公司的行動應用程式。
* 無需複雜的布建設定檔，且需額外努力來建立和上傳您的應用程式以供共用，即可檢閱開發和測試環境中的應用程式。
* 使用AEM製作環境來建立和管理您應用程式的豐富內容。
* 透過Adobe PhoneGap使用HTML5，以透過裝置原生功能建立豐富的體驗。
* 透過Cordova WebViews將HTML5 Webviews引入新的或預先存在的&#x200B;**native**&#x200B;應用程式。
* 在所有傳送通道（包括網頁、行動網路、行動應用程式和列印）建立、組織和共用豐富多媒體內容。

AEM與Adobe **[PhoneGap Build服務](https://build.phonegap.com/)**&#x200B;整合，以簡化應用程式建立和部署過程。

**Adobe** 內容同步功能可讓使用者輕鬆將頁面和內容更新透過空中(OTA)下載至其裝置，而不需重新安裝應用程式，或從appStore、Google Play或其他應用程式來源下載。

**Adobe** Analytics完全整合至AEM應用程式，並可詳細追蹤發佈、地理位置、作業系統、裝置、點按資料流、iBeacon追蹤等。

## 建立應用程式{#creating-apps}

開發人員可使用[AEM PhoneGap入門套件](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit)以及[https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps)中的其他資源，以透過PhoneGap引導AEM應用程式，包括執行Cordova Webviews的參考原生應用程式。

入門套件Git存放庫的自述檔案包含使用入門套件的教學課程：

* 自訂品牌
* Maven建置和部署目標範例
* 原始碼控制庫配置
* 安裝並部署至本機或遠端AEM執行個體
* 從AEM解除安裝

>[!NOTE]
>
>您可在GitHub [此處](https://github.com/adobe-marketing-cloud-apps)和「kitchen-sink」來源[此處](https://github.com/blefebvre/aem-phonegap-kitchen-sink)找到其他參考實作來源，包括labs。

## 針對IOS 9和HTTP主機{#developing-for-ios-and-http-hosts}開發

iOS開發人員應注意，iOS 9上執行的Cordova應用程式出現開啟問題。 此問題會防止向不安全的主機(例如&#x200B;*http://localhost:4502*)提出請求。 此問題將透過即將發行的cordova-ios版本（由Cordova CLI使用）解決，但同時提供兩種解決方法：

1. 若要立即解決，您仍可以直接使用任何iOS 8模擬器，而不會造成問題。
1. 如果您必須使用iOS 9，您的應用程式 — Info.plist（在「&lt;app root>/platforms/ios/&lt;app name>/&lt;app name>-Info.plist」中執行`cordova platform add ios`後找到）可以手動編輯，以包含下列屬性：

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>如需「App Transport Security」的詳細資訊，請參閱[Apple iOS9搶鮮版檔案](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14)和此[堆疊溢出討論](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)的下列章節。

## 在AEM中開發行動應用程式{#developing-mobile-applications-in-aem-1}

* [啟動AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [建立行動應用程式](/help/mobile/building-app-mobile-phonegap.md)
* [建構應用程式](/help/mobile/phonegap-structure-an-app.md)
* [使用Apps Console建立和編輯應用程式](/help/mobile/phonegap-apps-console.md)
* [單頁應用程式](/help/mobile/phonegap-single-page-applications.md)
* [使用PhoneGap CLI開發應用程式](/help/mobile/phonegap-apps-pg-cli.md)
* [訪問設備功能](/help/mobile/phonegap-access-device-features.md)
* [使用Adobe行動分析追蹤應用程式效能](/help/mobile/phonegap-intro-to-app-analytics.md)
* [將Adobe Analytics新增至行動應用程式](/help/mobile/phonegap-add-analytics-to-apps.md)
* [推播通知](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile內容個人化](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [應用程式的解剖](/help/mobile/phonegap-apps-arch.md)
* [您的混合應用程式已準備好迎接AEM Mobile嗎？](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他資源 {#additional-resources}

若要了解管理員和開發人員的角色和責任，請參閱下列資源：

* [使用AEM編寫Adobe PhoneGap Enterprise](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
