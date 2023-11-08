---
title: 將Adobe Analytics新增至您的行動應用程式
description: 請詳閱本頁面，瞭解如何透過與Analytics Mobile Services整合，在Adobe Experience Manager應用程式中使用行動應用程式Adobe。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 0%

---

# 將Adobe Analytics新增至您的行動應用程式{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md)。

想要為您的行動應用程式使用者建立吸引人且相關的體驗嗎？ 如果您沒有使用AdobeMobile Services SDK來監控和測量應用程式的生命週期和使用量，那麼您的決策依據是什麼？ 您最忠實的客戶在哪？ 如何保證您保持相關度並最佳化轉換？

您的使用者是否存取所有內容？ 他們是否正在放棄應用程式？如果是，在哪裡放棄？ 他們會在應用程式中停留的頻率，以及回訪使用應用程式的頻率？ 您可以引入哪些變更，然後測量增加保留率的程度？ 當機率如何呢？您的應用程式會針對使用者當機嗎？

充分運用 [行動應用程式分析](https://business.adobe.com/products/analytics/mobile-marketing.html) 在您的Adobe Experience Manager (AEM)應用程式中，透過與整合 [Adobe行動服務](https://business.adobe.com/products/campaign/mobile-marketing.html).

檢測您的AEM應用程式，以追蹤、報告並瞭解使用者如何與您的行動應用程式和內容互動，並測量關鍵生命週期量度，例如啟動次數、應用程式內時間和當機率。

本節說明AEM如何執行 *開發人員* 可以：

* 將Mobile Analytics整合至行動應用程式
* 使用Bloodhound測試您的Analytics追蹤

## 先決條件 {#prerequisties}

AEM Mobile需要Adobe Analytics帳戶，才能在您的應用程式中收集和報告追蹤資料。 在設定過程中， AEM *管理員* 必須首先：

* 設定Adobe Analytics帳戶，並在Mobile Services中為您的應用程式建立報表套裝。
* 在Adobe Experience Manager (AEM)中設定AMSCloud Service。

## 適用於開發人員 — 將行動裝置分析整合至您的應用程式 {#for-developers-integrate-mobile-analytics-into-your-app}

### 設定ContentSync以提取設定檔 {#configure-contentsync-to-pull-in-configuration-file}

設定Analytics帳戶後，請建立Content Sync設定，將內容提取至您的行動應用程式。

如需其他詳細資訊，請參閱「設定內容同步內容」。 設定必須指示Content Sync將ADBMobileConfig放入/www目錄。 例如，在Geometrixx Outdoors應用程式中，內容同步設定為： */content/phonegap/geometrixx-outdoors/shell/jcr：content/pge-app/app-config/ams-ADBMobileConfig*. 也有開發設定。 不過，如果有Geometrixx Outdoors，則與非開發設定相同。

如需如何從行動應用程式AEM應用程式儀表板下載ADBMobileConfig的詳細資訊，請參閱Analytics - Mobile Services -AdobeMobile Services SDK設定檔案。

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

每個平台都需要將ADBMobileConfig複製到特定位置。

如果使用PhoneGap CLI建置，則可使用cordova建置勾點指令碼來完成。 您可以在Geometrixx Outdoors應用程式中看到以下內容：*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

針對iOS，檔案必須複製到XCode專案的 **資源** 目錄(例如「platforms/ios/Geometrixx/Resources/ADBMobileConfig.json」)。 如果應用程式的目標為Android™，則複製的目的地路徑為「platforms/android/assets/ADBMobileConfig.json」。 如需在PhoneGap CLI建置期間使用鉤點的詳細資訊，請參閱 [勾選您的Cordova/PhoneGap專案需求](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c).

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

### 在應用程式中新增AMS外掛程式 {#add-the-ams-plugin-in-the-app}

應用程式若要收集資料，必須將Adobe Mobile Services (AMS)外掛程式納入應用程式中。 將外掛程式作為功能加入應用程式的config.xml中，就能在PhoneGap Build程式期間使用另一個Cordova勾點來自動新增外掛程式。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors App config.xml位於 */content/phonegap/geometrixx-outdoors/shell/jcr：content/pge-app/app-content/phonegap/www/config.xml*. 上述範例會要求使用特定版本的外掛程式，方法是新增「#」，然後在外掛程式URL後面加上標籤值。 此為遵循的良好做法，可確保不會因在建置期間新增未經測試的外掛程式而出現未預期的問題。

執行這些步驟後，您的應用程式將可報告Adobe Analytics提供的所有生命週期量度。 這包括啟動、當機和安裝等資料。 如果這是您唯一關心的資料，則表示您已完成。 如果您想要收集自訂資料，則您必須檢測程式碼。

### 檢測您的程式碼以進行完整應用程式追蹤 {#instrument-your-code-for-full-app-tracking}

中提供數個追蹤API [AMS Phonegap外掛程式API。](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/phonegap/phonegap-methods.md)

這些功能可讓您追蹤狀態和動作，例如使用者在應用程式中導覽至的頁面、最常使用哪些控制項。 要檢測應用程式以進行追蹤，最簡單的方式是使用AMS外掛程式提供的Analytics API。

* ADB.trackState()
* ADB.trackAction()

如需參考資訊，請檢視Geometrixx Outdoors應用程式中的程式碼。 在Geometrixx Outdoors應用程式中，所有頁面導覽都會使用ADB.trackState()方法進行追蹤。 如需詳細資訊，請參閱/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js的原始程式碼

透過使用此方法呼叫來檢測您的原始程式碼，您就可以收集應用程式的完整量度。

#### 連線至AMS的屬性 {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp*&#x200B;我公開下列屬性以連線至AMS：

| **標籤** | **說明** | **預設** |
|---|---|---|
| API端點 | AdobeMobile Services HTTP API的基本URL | https://api.omniture.com |
| 設定端點 | 用於擷取給定報表套裝ID之ADB行動設定的URL | /ams/1.0/app/config/ |
| 行動服務應用程式 | 取得使用者公司內的應用程式清單 | /ams/1.0/apps |
