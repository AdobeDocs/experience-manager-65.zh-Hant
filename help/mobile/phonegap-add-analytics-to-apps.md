---
title: 將Adobe Analytics新增至您的行動應用程式
seo-title: 將Adobe Analytics新增至您的行動應用程式
description: 請依照本頁進行，瞭解如何透過與Adobe Mobile services整合，在AEM應用程式中使用Mobile App Analytics。
seo-description: 請依照本頁進行，瞭解如何透過與Adobe Mobile services整合，在AEM應用程式中使用Mobile App Analytics。
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 將Adobe Analytics新增至您的行動應用程式{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

想要為您的行動應用程式使用者建立引人入勝的相關體驗嗎？ 如果您不是使用Adobe Mobile Services SDK來監控和測量應用程式的生命週期和使用情形，那麼您的決策依據是什麼？ 您最忠誠的客戶在哪裡？ 如何保證您保持相關性並最佳化轉換？

您的使用者是否可存取所有內容？ 他們會放棄應用嗎？如果會，會在哪裡？ 他們多久會留在應用程式中，又多久會回來使用應用程式？ 您可以引入哪些更改，然後衡量這些更改是否提高了保留率？ 當機率呢？您的應用程式是否對您的使用者造成當機？

透過與 [Adobe Mobile Services](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) 整合，在您的AEM應用程式中運用 [Mobile App Analytics](https://www.adobe.com/marketing-cloud/mobile-marketing.html)。

利用您的AEM應用程式來追蹤、報告並瞭解您的使用者如何與行動應用程式和內容互動，以及測量關鍵生命週期度量，例如啟動、應用程式逗留時間和當機率。

本節說明AEM開發人 *員如何* :

* 將Mobile Analytics整合至您的行動應用程式
* 使用Bloodhound測試您的分析追蹤

## 先決條件 {#prerequisties}

AEM mobile需要Adobe Analytics帳戶才能收集和報告應用程式中的追蹤資料。 在設定中，AEM *Administrator* 將首先需要：

* 在Mobile services中設定Adobe Analytics帳戶並建立應用程式的報表套裝。
* 在Adobe Experience Manager(AEM)中設定AMS cloud服務。

## 針對開發人員——將Mobile Analytics整合至您的應用程式 {#for-developers-integrate-mobile-analytics-into-your-app}

### 配置ContentSync以提取配置檔案 {#configure-contentsync-to-pull-in-configuration-file}

在設定Analytics帳戶後，您將需要建立內容同步設定，以將內容納入您的行動應用程式。

如需詳細資訊，請參閱「設定內容同步內容」。 配置將需要指示「內容同步」將ADBMobileConfig放入/www目錄。 例如，在Geometrixx Outdoors應用程式中，內容同步設定位於： */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig*。 此外，還有一種發展配置；但是，它與Geometrixx Outdoors的非開發設定相同。

如需如何從「行動應用程式AEM應用程式」儀表板下載ADBMobileConfig的詳細資訊，請參閱「Analytics - Mobile Services - Adobe Mobile Services SDK設定檔」。

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

每個平台都需要將ADBMobileConfig複製至特定位置。

如果使用PhoneGap CLI建立，則可使用cordova建立掛接指令碼來完成。 這可在Geometrixx Outdoors應用程式中查看：*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js。*

對於iOS，需要將檔案複製到XCode項目的 **Resources** 目錄(如 「platforms/ios/Geometrixx/Resources/ADBMobileConfig.json」)。 如果應用程式已定位至Android，則要複製至的路徑是「platforms/android/assets/ADBMobileConfig.json」。 有關在PhoneGap CLI構建過程中使用掛接的詳細資訊，請參閱 [Three hooks your Cordova/PhoneGap項目需求](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/)。

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

### 在應用程式中新增AMS增效模組 {#add-the-ams-plugin-in-the-app}

App若要收集資料，Adobe Mobile Services(AMS)外掛程式必須包含在應用程式中。 將外掛程式加入應用程式的config.xml中做為功能，可在PhoneGap建立程式期間使用另一個Cordova掛接自動新增外掛程式。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors App config.xml位於 */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*。 上述範例會要求在外掛程式URL後新增「#」和標籤值，以使用特定版本的外掛程式。 這是一個很好的做法，可確保由於在構建過程中添加未經測試的插件，不會出現未預期的問題。

執行這些步驟後，您的應用程式將會啟用，以報告Adobe Analytics提供的所有生命週期度量。 這包括啟動、當機和安裝等資料。 如果這是您唯一關心的資料，您就完成了。 如果您想要收集自訂資料，則需要測量您的程式碼。

### 測量您的程式碼以進行完整的應用程式追蹤 {#instrument-your-code-for-full-app-tracking}

AMS Phonegap外掛程式API中提 [供數個追蹤API。](https://marketing.adobe.com/resources/help/en_US/mobile/ios/phonegap_methods.html)

這些功能可讓您追蹤狀態和動作，例如使用者在應用程式中瀏覽至的頁面位置，以及最常使用的控制項。 要測量應用程式進行追蹤，最簡單的方式就是使用AMS外掛程式提供的Analytics API。

* ADB.trackState()
* ADB.trackAction()

您可以參考Geometrixx Outdoors應用程式中的程式碼。 在Geometrixx Outdoors應用程式中，所有頁面導覽都會使用ADB.trackState()方法進行追蹤。 如需詳細資訊，請參閱/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js的原始碼

透過這些方法呼叫來檢測您的原始碼，您就可以針對您的應用程式收集完整量度。

### 使用Bloodhound測試Analytics追蹤 {#testing-analytics-tracking-with-bloodhound}

![](do-not-localize/chlimage_1.jpeg)

（可選）在部署至生產環境之前，您可以使用Adobe工具 [Bloodhound](https://marketing.adobe.com/developer/gallery/bloodhound-app-measurement-qa-tool-1) 來測試您的分析設定。 為測試您的分析設定，您需要編輯ADBMobileConfig.json檔案，以指向Bloodhound執行的伺服器，而非實際的Analytics伺服器。 若要進行此變更，請從您的ADBMobileConfig.json變更下列項目。

```xml
...
"analytics": {
    "rsids": "YOUR_RSID",
    "server": "YOUR_TRACKING_SERVER:YOUR_TRACKING_PORT",
...
```

變更以符合此項目：

```xml
...
"analytics": {
    "rsids": "YOUR_RSID",
    "server": "localhost:50000",
...
```

這會將AMS外掛程式收集的所有資料重新導向至Bloodhound，讓您檢視結果。

#### 用於連接到AMS的屬性。 {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.* MobileServicesHttpClientImpl公開下列用於連線至AMS的屬性：

| **標籤** | **說明** | **預設** |
|---|---|---|
| API端點 | Adobe Mobile Services HTTP API的基本URL | https://api.omniture.com |
| 配置端點 | 用於擷取指定報表套裝ID之ADB行動設定的URL | /ams/1.0/app/config/ |
| 行動服務應用程式 | 取得使用者公司內的應用程式清單 | /ams/1.0/apps |

