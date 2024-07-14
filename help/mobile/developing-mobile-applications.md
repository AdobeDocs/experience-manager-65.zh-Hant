---
title: 在AEM中開發行動應用程式
description: 請依照此頁面，開始使用Adobe PhoneGap Enterprise在AEM中開發行動應用程式。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# 在AEM中開發行動應用程式 {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

AEM使用Adobe PhoneGap和Adobe發佈解決方案，可讓您建立並管理內容豐富且以公用程式為基礎的跨平台行動應用程式：

* 在一個地方管理所有公司的行動應用程式。
* 檢閱開發和測試環境中的應用程式，而不需要複雜的布建設定檔，以及額外努力建置和上傳應用程式以進行共用。
* 使用AEM編寫環境為您的應用程式建立和管理豐富的內容。
* 搭配使用HTML5與Adobe PhoneGap，以裝置原生功能建立豐富的體驗。
* 透過Cordova WebViews將HTML5 Web檢視引進新的或預先存在的&#x200B;**原生**&#x200B;應用程式。
* 跨所有傳遞管道（包括網頁、行動網頁、行動應用程式和印刷品）建立、組織和分享豐富的多媒體內容。

AEM與Adobe PhoneGap Build服務(`https://build.phonegap.com/`)整合，以簡化應用程式建置和部署程式。

**AdobeContentSync**&#x200B;可讓使用者輕鬆將Over-The-Air (OTA)頁面和內容更新下載到他們的裝置，而不需要重新安裝應用程式，或是從appStore、Google Play或其他應用程式來源下載。

**Adobe Analytics**&#x200B;已完全整合至AEM應用程式，並允許詳細的散佈、地理位置、作業系統、裝置、點選串流、iBeacon追蹤等追蹤。

## 建立應用程式 {#creating-apps}

開發人員可以使用[AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit)以及[https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps)中的其他資源，透過PhoneGap啟動AEM應用程式，包括執行Cordova Webviews的參考原生應用程式。

Starter Kit Git存放庫的Readme包含使用入門套件的教學課程：

* 自訂品牌
* Maven範例建置和部署目標
* Source控制項存放庫設定
* 安裝並部署到本機或遠端AEM執行個體
* 從AEM解除安裝

>[!NOTE]
>
>其他參考實作來源（包括Labs）可以在GitHub [這裡](https://github.com/adobe-marketing-cloud-apps)和「廚房 — 水槽」來源[這裡](https://github.com/blefebvre/aem-phonegap-kitchen-sink)找到。

## 針對IOS 9和HTTP主機開發 {#developing-for-ios-and-http-hosts}

iOS開發人員應留意在iOS 9上執行Cordova應用程式的未完成問題。 此問題會防止對不安全的主機(例如&#x200B;*http://localhost:4502*)發出請求。 此問題將在即將發行的cordova-ios版本中解決（由Cordova CLI使用），但與此同時，有兩個可用的因應措施：

1. 作為立即的因應措施，您仍然可以使用任何iOS 8模擬器，而不會出現問題。
1. 如果您必須使用iOS 9，可以手動編輯您的apps -Info.plist （在「&lt;app root>/platforms/ios/&lt;app name>/&lt;app name>-Info.plist」）檔案中執行`cordova platform add ios`後找到)以包含下列屬性：

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>如需「App Transport Security」的詳細資訊，請參閱[Apple的iOS9發行前檔案](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14)的下列章節和此[棧疊溢位討論](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)。

## 在AEM中開發行動應用程式 {#developing-mobile-applications-in-aem-1}

* [啟動AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [建立行動應用程式](/help/mobile/building-app-mobile-phonegap.md)
* [建構應用程式](/help/mobile/phonegap-structure-an-app.md)
* [使用應用程式控制檯建立和編輯應用程式](/help/mobile/phonegap-apps-console.md)
* [單頁應用程式](/help/mobile/phonegap-single-page-applications.md)
* [使用PhoneGap CLI開發應用程式](/help/mobile/phonegap-apps-pg-cli.md)
* [存取裝置功能](/help/mobile/phonegap-access-device-features.md)
* [透過AdobeMobile Analytics追蹤應用程式效能](/help/mobile/phonegap-intro-to-app-analytics.md)
* [將Adobe Analytics新增至您的行動應用程式](/help/mobile/phonegap-add-analytics-to-apps.md)
* [推播通知](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile內容個人化](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [應用程式剖析](/help/mobile/phonegap-apps-arch.md)
* [您的混合式應用程式是否已準備好使用AEM Mobile？](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他資源 {#additional-resources}

若要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise製作](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
