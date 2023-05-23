---
title: 開發移動應用程AEM序
seo-title: Developing Mobile Applications in AEM
description: 按照本頁開始使用Adobe PhoneGap企業開AEM發移動應用程式。
seo-description: Follow this page to start developing mobile application in AEM using Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---

# 開發移動應用程AEM序 {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

利AEM用Adobe PhoneGap和Adobe發佈解決方案，使您能夠建立和管理內容豐富和基於實用工具的跨平台移動應用程式：

* 在一個位置管理您公司的所有移動應用。
* 在開發和暫存環境中查看應用程式，而不需要複雜的設定配置檔案，也無需額外努力構建和上載應用程式以進行共用。
* 使用創AEM作環境為您的應用建立和管理豐富內容。
* 使用與Adobe PhoneGap的HTML5，通過設備本機功能建立豐富的體驗。
* 將HTML5 Web視圖引入新的或預先存在的 **本地** 應用程式。
* 跨所有交付渠道（包括Web、Mobile-Web、Mobile-App和打印）建立、建立和共用豐富的多媒體內容。

與AEMAdobe整合 **[PhoneGap Build服務](https://build.phonegap.com/)** 簡化應用程式構建和部署過程。

**Adobe內容同步** 使用戶能夠輕鬆地將頁面和內容更新Over-the-Air(OTA)下載到其設備，而無需重新安裝應用程式或從appStore、Google Play或其他應用程式源下載。

**Adobe Analytics** 完全整合到應AEM用中，允許詳細跟蹤分佈、地理位置、作業系統、設備、按一下流、iBeacon跟蹤等。

## 建立應用 {#creating-apps}

開發人員可以 [AEMPhoneGap入門套件](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) 以及在 [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) 使用PhoneGap啟動應AEM用，包括運行Cordova Webviews的參考本機應用。

Starter Kit Git儲存庫的自述檔案包括使用Starter Kit的教程：

* 自定義品牌
* 生成和部署目標示例
* 原始碼管理儲存庫配置
* 安裝並部署到本地或遠程實AEM例
* 卸載AEM自

>[!NOTE]
>
>可在GitHub上找到其他參考實現源，包括實驗 [這裡](https://github.com/adobe-marketing-cloud-apps) 還有&quot;廚房水池&quot; [這裡](https://github.com/blefebvre/aem-phonegap-kitchen-sink)。

## 為IOS9和HTTP主機開發 {#developing-for-ios-and-http-hosts}

iOS開發者應該知道，iOS9上運行的Cordova應用程式存在一個開放問題。 此問題防止向不安全主機發出請求(如 *http://localhost:4502*)。 此問題將通過即將發佈的cordova-ios（由Cordova CLI使用）來解決，但與此同時，有兩種解決方法：

1. 作為一種立即的解決方法，您仍然可以無問題地使用任何iOS8模擬器。
1. 如果必須使用iOS9，則您的應用 — Info.plist（在運行後找到） `cordova platform add ios` 在&quot;&lt;app root=&quot;&quot;>/platforms/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>-Info.plist&quot;)檔案可以手動編輯，以包括以下屬性：

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>有關「應用傳輸安全性」的詳細資訊，請參閱 [AppleiOS9預發佈文檔](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) 和 [堆棧溢出討論](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)。

## 開發移動應用程AEM序 {#developing-mobile-applications-in-aem-1}

* [啟動AEMPhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [構建移動應用程式](/help/mobile/building-app-mobile-phonegap.md)
* [構造應用](/help/mobile/phonegap-structure-an-app.md)
* [使用應用控制台建立和編輯應用](/help/mobile/phonegap-apps-console.md)
* [單頁應用程式](/help/mobile/phonegap-single-page-applications.md)
* [使用PhoneGap CLI開發應用](/help/mobile/phonegap-apps-pg-cli.md)
* [訪問設備功能](/help/mobile/phonegap-access-device-features.md)
* [使用AdobeMobile分析跟蹤應用效能](/help/mobile/phonegap-intro-to-app-analytics.md)
* [將Adobe Analytics添加到您的移動應用程式](/help/mobile/phonegap-add-analytics-to-apps.md)
* [推播通知](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile內容個性化](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [應用剖析](/help/mobile/phonegap-apps-arch.md)
* [你的混合應用準備好迎接AEM Mobile了嗎？](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他資源 {#additional-resources}

要瞭解管理員和開發人員的角色和職責，請參閱以下資源：

* [為Adobe PhoneGap企業創AEM作](/help/mobile/phonegap.md)
* [為Adobe PhoneGap企業管理內AEM容](/help/mobile/administer-phonegap.md)
