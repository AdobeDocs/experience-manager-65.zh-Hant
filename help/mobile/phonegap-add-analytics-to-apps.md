---
title: 將Adobe Analytics添加到您的移動應用程式
seo-title: Add Adobe Analytics to your Mobile Application
description: 通過與Adobe移動服務整合，可以瞭解如何在應用AEM中使用Mobile App Analytics。
seo-description: Follow this page to learn about how you can use Mobile App Analytics in your AEM Apps by integrating with Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---

# 將Adobe Analytics添加到您的移動應用程式{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

希望為您的移動應用程式用戶構建引人入勝且相關的體驗嗎？ 如果您沒有使用Adobe移動服務SDK來監視和衡量應用程式生命週期和使用情況，那麼您會根據您的決策做出什麼決定？ 您最忠誠的客戶在哪裡？ 如何確保保持相關性並優化轉換？

您的用戶是否訪問所有內容？ 他們是否會放棄應用，如果放棄了，又會在哪裡？ 他們在應用中呆多久，又多久回來使用應用？ 您可以引入哪些更改，然後衡量哪些更改可增加保留期？ 崩潰率如何，你的應用是否崩潰了？

利用 [移動應用分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) 通過AEM與 [Adobe移動服務](https://www.adobe.com/marketing-cloud/mobile-marketing.html)。

測AEM試您的應用以跟蹤、報告和瞭解用戶如何與您的移動應用和內容打交道，並衡量關鍵生命週期指標，如啟動、應用時間和崩潰率。

本節介紹如AEM何 *開發人員* 可以：

* 將Mobile Analytics整合到您的移動應用程式
* Test你用獵犬追蹤分析

## 預請求 {#prerequisties}

AEM Mobile需要一個Adobe Analytics帳戶來收集和報告你應用中的跟蹤資料。 作為配置的一AEM部分 *管理員* 首先需要：

* 設定Adobe Analytics帳戶並為移動服務中的應用程式建立報告套件。
* 在Adobe Experience Manager配置AMSCloud Service(AEM)。

## 面向開發人員 — 將Mobile Analytics整合到您的應用中 {#for-developers-integrate-mobile-analytics-into-your-app}

### 將ContentSync配置為拉入配置檔案 {#configure-contentsync-to-pull-in-configuration-file}

在設定Analytics帳戶後，您需要建立內容同步配置以將內容拉入移動應用程式。

有關其他詳細資訊，請參閱配置內容同步內容。 配置需要指示內容同步將ADBMobileConfig放入/www目錄。 例如，在Geometrixx Outdoors應用中，內容同步配置位於： */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig*。 還有發展的格局；但是，在Geometrixx Outdoors中，這與非開發配置相同。

有關如何從您的Mobile Application AEM Apps儀表板下載ADBMobileConfig的詳細資訊，請參閱分析 — 移動服務 — Adobe移動服務SDK配置檔案。

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

每個平台都要求將ADBMobileConfig複製到特定位置。

如果使用PhoneGap CLI構建，則可以使用cordova構建掛接指令碼來完成。 在Geometrixx Outdoors App中可以看到以下內容：*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js。*

對於iOS，需要將檔案複製到XCode項目的 **資源** 目錄(例如 「platforms/ios/Geometrixx/Resources/ADBMobileConfig.json」)。 如果App針對Android，則複製到的路徑是「platforms/android/assets/ADBMobileConfig.json」。 有關在PhoneGap CLI構建過程中使用掛接的詳細資訊，請參閱 [三個掛接Cordova/PhoneGap項目需要](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c)。

```xml
///////////////////////////
//          iOS
///////////////////////////
    ios : [
        {
            "www/ADBMobileConfig.json": "platforms/ios/<YOUR_APP_NAME>/Resources/ADBMobileConfig.json"
        }
    ],
///////////////////////////
//          ANDROID
///////////////////////////
    android: [
        {
            "www/ADBMobileConfig.json": "platforms/android/assets/ADBMobileConfig.json"
        }
    ]
```

### 在應用中添加AMS插件 {#add-the-ams-plugin-in-the-app}

要使應用程式收集資料，Adobe移動服務(AMS)插件需要作為應用程式的一部分包括。 通過將插件作為功能包含在應用的config.xml中，可以使用另一個Cordova掛接在PhoneGap生成過程中自動添加插件。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors應用程式config.xml位於 */content/phonegap/geometrixx/outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*。 上面的示例要求通過在插件URL後添加「#」和標籤值來使用特定版本的插件。 這是一個良好的做法，可確保在生成過程中添加未經測試的插件時不會出現意外問題。

執行這些步驟後，您的應用將能夠報告Adobe Analytics提供的所有生命週期度量。 這包括啟動、崩潰和安裝等資料。 如果這是你唯一關心的資料，那麼你就完成了。 如果要收集自定義資料，則需要測試代碼。

### 測試代碼以完整應用跟蹤 {#instrument-your-code-for-full-app-tracking}

中提供了幾個跟蹤API [AMS Phonegap插件API。](https://experienceleague.adobe.com/docs/mobile-services/ios/phonegap-ios/phonegap-methods.html)

這些功能將允許您跟蹤狀態和操作，例如用戶在應用中導航到的頁面的位置，這些控制項的使用最多。 使用AMS插件提供的分析API來測試應用進行跟蹤的最簡單方法。

* ADB.trackState()
* ADB.trackAction()

有關參考，您可以查看Geometrixx Outdoors應用中的代碼。 在Geometrixx Outdoors應用中，使用ADB.trackState()方法跟蹤所有頁面導航。 欲瞭解更多資訊，請訪問/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js的原始碼

通過使用這些方法調用檢測原始碼，您可以針對應用程式收集完整度量。

#### 用於連接到AMS的屬性 {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobilesservices.impl.service.MobileServicesHttpClientImp* l顯示以下用於連接到AMS的屬性：

| **標籤** | **說明** | **預設** |
|---|---|---|
| API終結點 | Adobe移動服務HTTP API的基URL | https://api.omniture.com |
| 配置終結點 | 用於檢索給定報告套件ID的ADB移動配置的URL | /ams/1.0/app/config/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// |
| 移動服務應用 | 獲取用戶公司內的應用清單 | /ams/1.0/apps |
