---
title: 將Adobe Analytics新增至行動應用程式
seo-title: Add Adobe Analytics to your Mobile Application
description: 請詳閱本頁，了解如何透過與Mobile Services整合，在AEM應用程式中使用行動應用程式分析。
seo-description: Follow this page to learn about how you can use Mobile App Analytics in your AEM Apps by integrating with Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# 將Adobe Analytics新增至行動應用程式{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

想要為您的行動應用程式使用者建立吸引人且相關的體驗嗎？ 如果您沒有使用AdobeMobile Services SDK來監視和測量應用程式的生命週期和使用情形，則您的決策依據為何？ 您最忠誠的客戶在哪裡？ 如何確保保持相關性並最佳化轉換？

您的使用者是否可存取所有內容？ 他們是否正在放棄應用，如果是，在哪裡？ 他們多久停留在應用程式內，又多久回來使用應用程式？ 您可以引入哪些變更，然後衡量哪些變更可增加保留率？ 當機率如何？您的應用程式是否會因使用者而當機？

善用 [行動應用程式分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) 與整合，在AEM應用程式中 [AdobeMobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

測量您的AEM應用程式，以追蹤、報告及了解使用者如何與您的行動應用程式和內容互動，以及測量關鍵生命週期量度（例如啟動、應用程式內時間和當機率）。

本節說明AEM *開發人員* 可以：

* 將行動分析整合至您的行動應用程式
* 使用Bloodhound測試您的分析追蹤

## 必要性 {#prerequisties}

AEM Mobile需要Adobe Analytics帳戶，才能收集應用程式中的追蹤資料並製作報表。 作為設定的一部分，AEM *管理員* 首先需要：

* 設定Adobe Analytics帳戶，並在Mobile Services中為您的應用程式建立報表套裝。
* 在Adobe Experience Manager(AEM)中設定AMSCloud Service。

## 開發人員 — 將行動分析整合至您的應用程式 {#for-developers-integrate-mobile-analytics-into-your-app}

### 配置ContentSync以提取配置檔案 {#configure-contentsync-to-pull-in-configuration-file}

設定Analytics帳戶後，您需要建立「內容同步」設定，將內容提取至您的行動應用程式。

有關其他詳細資訊，請參閱配置內容同步內容。 配置需要指示「內容同步」將ADBMobileConfig放入/www目錄。 例如，在Geometrixx Outdoors應用程式中，內容同步設定位於： */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig*. 此外也有開發設定；不過，這與Geometrixx Outdoors中的非開發設定相同。

如需如何從行動應用程式AEM應用程式控制面板下載ADBMobileConfig的詳細資訊，請參閱Analytics - Mobile Services -Adobe行動服務SDK設定檔案。

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

每個平台都需將ADBMobileConfig複製到特定位置。

如果使用PhoneGap CLI建置，則可使用cordova建置掛接指令碼完成。 這可在Geometrixx Outdoors應用程式中查看：*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js。*

若為iOS，則需要將檔案複製到 **資源** 目錄(例如 &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;)。 如果應用程式鎖定Android目標，則複製至的路徑為「platforms/android/assets/ADBMobileConfig.json」。 有關在PhoneGap CLI構建期間使用掛接的詳細資訊，請參閱 [三個鈎點：Cordova/PhoneGap專案需求](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/).

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

AdobeMobile Services(AMS)外掛程式必須包含在應用程式中，應用程式才能收集資料。 將外掛程式納入應用程式的config.xml中作為功能後，便可使用另一個Cordova連結，在PhoneGap建置程式期間自動新增外掛程式。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors應用配置.xml位於 */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. 上述範例要求您先新增「#」，然後在外掛程式URL後面新增標籤值，以使用特定版本的外掛程式。 這是確保在建立期間新增未經測試的外掛程式時，不會出現非預期問題的理想作法。

執行這些步驟後，您的應用程式將啟用，以報告Adobe Analytics提供的所有生命週期量度。 這包括啟動、當機和安裝等資料。 如果這是您唯一關心的資料，則您已完成。 如果您想要收集自訂資料，則需要檢測您的程式碼。

### 測量您的程式碼以進行完整的應用程式追蹤 {#instrument-your-code-for-full-app-tracking}

中提供數個追蹤API [AMS Phonegap外掛程式API。](https://docs.adobe.com/content/help/en/mobile-services/ios/phonegap-ios/phonegap-methods.html)

這些功能可讓您追蹤狀態和動作，例如使用者在您的應用程式中導覽至的頁面位置，這些控制項的使用頻率最高。 要檢測您的應用程式以進行追蹤，最簡單的方式是使用AMS外掛程式提供的Analytics API。

* ADB.trackState()
* ADB.trackAction()

若需參考，您可以檢視Geometrixx Outdoors應用程式中的程式碼。 在Geometrixx Outdoors應用程式中，所有頁面導覽都使用ADB.trackState()方法來追蹤。 欲知更多詳情，請查看/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js的原始碼

透過這些方法呼叫檢測原始碼，您便能夠針對應用程式收集完整量度。

#### 連接到AMS的屬性 {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp* l會公開下列用於連線至AMS的屬性：

| **標籤** | **說明** | **預設** |
|---|---|---|
| API端點 | AdobeMobile Services HTTP API的基礎URL | https://api.omniture.com |
| 設定端點 | 用於擷取指定報表套裝ID之ADB行動設定的URL | /ams/1.0/app/config/ |
| 行動服務應用程式 | 取得使用者公司內的應用程式清單 | /ams/1.0/apps |
