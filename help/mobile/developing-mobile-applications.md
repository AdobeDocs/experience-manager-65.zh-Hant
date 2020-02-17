---
title: 在AEM中開發行動應用程式
seo-title: 在AEM中開發行動應用程式
description: 請依照本頁開始使用Adobe phoneGap Enterprise在AEM中開發行動應用程式。
seo-description: 請依照本頁開始使用Adobe phoneGap Enterprise在AEM中開發行動應用程式。
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在AEM中開發行動應用程式 {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

AEM運用Adobe PhoneGap和Adobe Publishing Solutions，讓您建立和管理內容豐富的跨平台和以公用程式為基礎的跨平台行動應用程式：

* 集中管理您所有的公司行動應用程式。
* 在開發和測試環境中檢視應用程式，毋需複雜的布建設定檔，也不需花太多心力來建立和上傳您的應用程式以進行分享。
* 使用AEM製作環境，為您的應用程式建立和管理多樣化內容。
* 搭配使用HTML5和Adobe phoneGap，透過裝置原生功能建立豐富的體驗。
* 透過Cordova webViews，將HTML5 Webviews引入新的或預先存 **在的** 原生應用程式。
* 跨所有傳送通道（包括網頁、行動裝置網頁、行動裝置應用程式和印刷品）建立、組織和分享豐富的多媒體內容。

AEM與Adobe **[PhoneGap Build服務整合](https://build.phonegap.com/)**，以簡化應用程式建立和部署程式。

**Adobe ContentSync** 可讓使用者輕鬆將Over-the-Air(OTA)的頁面和內容更新下載至其裝置，而不需重新安裝應用程式或從appStore、Google play或其他應用程式來源下載。

**Adobe Analytics已完全整合** 至AEM應用程式，可詳細追蹤散發、地理位置、作業系統、裝置、點按串流、iBeacon追蹤等。

## 建立應用程式 {#creating-apps}

開發人員可以使用 [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) ，以及 [](https://github.com/adobe-marketing-cloud-apps) https://github.com/adobe-marketing-cloud-apps中的其他資源，將AEM應用程式引導至使用PhoneGap，包括執行Cordova Webviews的參考原生應用程式。

Starter Kit Git儲存庫的自述檔案包含使用Starter Kit的教程：

* 自訂品牌
* 建立和部署目標範例
* 源控制儲存庫配置
* 安裝並部署至本機或遠端AEM例項
* 從AEM解除安裝

>[!NOTE]
>
>其他參考實作來源，包括實驗室，可在GitHub [和](https://github.com/adobe-marketing-cloud-apps) 「廚房水池」來源 [中找到](https://github.com/blefebvre/aem-phonegap-kitchen-sink)。

## 針對IOS 9和HTTP主機進行開發 {#developing-for-ios-and-http-hosts}

IOS開發人員應注意到在iOS 9上執行的Cordova應用程式有未解決的問題。 此問題會防止請求被提交給不安全的主機(例如 *http://localhost:4502*)。 此問題將透過即將發行的cordova-ios版本（由Cordova CLI使用）來解決，但同時有兩種解決方法：

1. 立即因應措施，您仍然可以無問題地使用任何iOS 8模擬器。
1. 如果您必須使用iOS 9，您的應用程式-Info.plist（在「&lt;app root>/platforms/ios/&lt;app name>/&lt;app name>-Info.plist」中執行後找到）檔案可以手動編輯，以包含下列屬性： `cordova platform add ios`

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>如需「App Transport Security」的詳細資訊，請參閱 [Apple iOS9搶鮮版檔案的下列章節](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) ，以及此 [「堆疊溢位」討論](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)。

## 在AEM中開發行動應用程式 {#developing-mobile-applications-in-aem-1}

* [啟動AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [建立行動應用程式](/help/mobile/building-app-mobile-phonegap.md)
* [建構應用程式](/help/mobile/phonegap-structure-an-app.md)
* [使用Apps Console建立和編輯應用程式](/help/mobile/phonegap-apps-console.md)
* [單頁應用程式](/help/mobile/phonegap-single-page-applications.md)
* [使用PhoneGap CLI開發應用程式](/help/mobile/phonegap-apps-pg-cli.md)
* [存取裝置功能](/help/mobile/phonegap-access-device-features.md)
* [使用Adobe Mobile Analytics追蹤應用程式效能](/help/mobile/phonegap-intro-to-app-analytics.md)
* [將Adobe Analytics新增至您的行動應用程式](/help/mobile/phonegap-add-analytics-to-apps.md)
* [推播通知](/help/mobile/phonegap-push-notifications.md)
* [AEM mobile內容個人化](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [應用程式的剖析](/help/mobile/phonegap-apps-arch.md)
* [您的混合應用程式是否已準備好適用於AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他資源 {#additional-resources}

要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM製作Adobe PhoneGap Enterprise](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
