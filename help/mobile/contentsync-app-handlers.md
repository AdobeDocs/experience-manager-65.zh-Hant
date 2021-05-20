---
title: 現成應用程式處理常式
seo-title: 現成應用程式處理常式
description: 請參照本頁面，了解使用AEM的Adobe PhoneGap Enterprise的現成可用處理常式。
seo-description: 請參照本頁面，了解使用AEM的Adobe PhoneGap Enterprise的現成可用處理常式。
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---

# 現成應用程式處理常式{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

請參閱以下開發內容同步處理常式的准則：

* 處理常式必須實作&#x200B;*com.day.cq.contentsync.handler.ContentUpdateHandler*（直接或延伸執行此操作的類）
* 處理常式可擴充&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 只有在處理常式更新ContentSync快取時，它們才必須報告true。 錯誤回報true會允許AEM建立更新。
* 只有在內容實際變更時，處理常式才應更新快取。 如果不需要白色，請勿寫入快取，並避免建立不必要的更新。

## 現成處理程式{#out-of-the-box-handlers}

下列為現成可用的應用程式處理常式：

**** mobileappagesRenders應用程式頁面。

* ***type - String***  - mobileappages
* ***路徑 — 字串***  — 頁面路徑
* ***擴充功能 — 字串***  — 要求中應使用的擴充功能。若是頁面，這幾乎一律為&#x200B;*html*，但其他仍可能。

* ***選取器 — 字串***  — 以點分隔的選用選取器。轉譯行動版頁面的常見範例為&#x200B;*touch*。

* ***deep — 布林值***  — 選用布林值屬性，決定是否應包含子頁面。預設值為&#x200B;*true。*

* ***includeImages — 布林***  — 選用布林屬性，決定是否應包含影像。預設值為&#x200B;*true*。

   * 預設情況下，僅考慮包含資源類型為foundation/components/image的影像元件。

* ***includeVideos — 布林值***  — 選用布林值屬性可判斷是否應包含視訊。預設值為&#x200B;*true*。

* ***includeModifiedPagesOnly — 布林值***  — 如果為false或省略，則轉譯所有頁面並檢查轉譯中的更新。如果為true，則根據對lastModified頁面的更改進行更改。
* ***+重寫（節點）***
   ***- relativeParentPath — 字串***  — 寫入相對於的所有其他路徑的路徑。

>[!NOTE]
>
>受此處理常式影響的影像和視訊元件的資源類型，是透過設定&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler*&#x200B;的屬性來設定。*MobilePagesUpdateHandler OSGi服務*。

**** mobilepageassets收集應用程式頁面資產。

**** mobilecontenlisting列出ContentSync zip的內容。裝置上的用戶端js會使用此ID執行AEM應用程式所需的初始檔案復本。

此處理常式應新增至任何AEM應用程式ContentSync設定。

* ***type - String - mobilecontenlisting***
* ***path***  — 字串 — 保留空白，必須顯示為有效的處理常式，但路徑推斷為目前的ContentSync快取。此值會被忽略。
* ***targetRootDirectory*  - **字串 — 可新增至路徑的前置詞，作為此處理常式內容更新的目標根。
* ***order - Long*  -**ContentSync執行此處理常式的順序。此數字應設定得比所有其他處理常式（如100）都高。 它應在傳統內容處理常式之後執行。

```xml
{
  "files": [
    "config.xml",
    "res/screens/ios/screen-ipad-portrait-2x.png",
    "res/screens/ios/screen-ipad-landscape.png",
    "res/screens/ios/screen-iphone-portrait-2x.png",
    "res/screens/ios/screen-iphone-landscape.png",
    "res/screens/ios/screen-iphone-portrait.png",
    "apps/weretail-app/components/splash-page/clientlibs.css",
    ...
    "pge-content-packages.json"
  ],
  "count": 382,
  "lastModified": 1422902754733
}
```

**** mobilecontentpackagelisting列出指定應用程式中的AEM內容套件，以及要提出更新請求的serverURL。這是用於裝置上的用戶端js，以要求內容更新

處理常式應用於AEM App Shell ContentSync設定（含pge-type=app-instance的節點）

* ***type - String - mobilecontentpackageslisting***
* ***path **-**字串***  — 應用程式殼層的路徑（含pge-type=app-instance的節點）。
* ***targetRootDirectory — 字串***  — 可新增至路徑的前置詞，作為此處理常式內容更新的目標根。
* ***order - Long*  - **Order for ContentSync執行此處理常式。此數字應設定得比所有其他處理常式（如100）都高。 它應在傳統內容處理常式之後執行。

>[!NOTE]
>
>下列程式碼區塊並非確切的實作，應作為參考範例使用：

```xml
{
  "content": [
    {
      "name": "en",
      "title": "We Retail Mobile App - English",
      "type": "CONTENT",
      "path": "/content/phonegap/weretail-outdoors/en",
      "updatePath": "/content/phonegap/weretail/en/jcr:content/pge-app/app-config"
    },
    {
      "name": "shell",
      "title": "We Retail Mobile App",
      "type": "INSTANCE",
      "path": "/content/phonegap/weretail-outdoors/shell",
      "updatePath": "/content/phonegap/weretail/shell/jcr:content/pge-app/app-config"
    }
  ],
  "serverURL": "http://localhost:4503/"
}
```

**** widgetconfig包含更新的config.xml，該config.xml將通過命令中心所做的任何編輯與提供的config.xml合併。如果此處理常式未包含任何透過管理介面變更的應用程式詳細資料，則快取中不會包含這些詳細資料。

此處理常式應用於AEM App Shell ContentSync設定（具有pge-type=[app-instance]的節點）。

* ***type — 字串* - **widgetconfig
* ***path **-**字串***  — 任何應用程式殼層子節點(具有pge-type=[app-instance]的節點)的路徑。
* ***targetRootDirectory — 字串***  — 可新增至路徑的前置詞，作為此處理常式內容更新的目標根。
* ***targetIconDirectory — 字串***  — 放置應用程式圖示的目錄

**** mobileADBMobileConfigJSONI若已設定AMS雲端服務，則包含ADBMobileConfig.JSON檔案。

這用於編譯時配置AMS插件以獲得分析支援。

處理常式應用於AEM App Shell ContentSync設定（含pge-type=app-instance的節點）

* ***type - String***  - mobileADBMobileConfigJSON
* ***path — 字串***  — 應用程式殼層的路徑（含pge-type=app-instance的節點，或延伸/libs/mobileapps/core/components/instance的RT）
* ***targetRootDirectory — 字串***  — 可新增至路徑的前置詞，作為此處理常式內容更新的目標根

**** notificationconfigextracts裝置上需要的通知設定。屬性會從與應用程式相關聯的個別推送服務雲端服務設定中擷取。

雲端服務的jcr:content節點中的非AEM屬性會擷取，並新增至&#x200B;**pge-notifications-config.json** JSON檔案，以便包含在應用程式內容的www根中。

AEM屬性是使用「cq」、「sling」或「jcr」建立命名空間的屬性。 其他屬性可使用內容同步設定節點上的「excludeProperties」屬性來排除。

* ***type — 字串***  - notificationsconfig
* ***excludeProperties - String[]***  — 要排除的屬性

**** contentsyncconfigcontentContels內容從現有的ContentSync配置收集。

* ***type - String***  - contentsyncconfigcontent
* ***路徑 — 字串***  — 指向以下任一路徑的路徑：

   * 另一個ContentSync配置
   * 內容套件（將使用其phonegap-exportTemplate屬性來尋找其ContentSync設定）
   * 至行動資源（在該資源下會找到app-content的，如果這些內容套件具有pge-includeInBuild屬性為true，則phonegap-exportTemplate將用於尋找其ContentSync設定）

* ***autoCreateFirstUpdateBeforeImport - Boolean***  — 如果為true，請在匯入前在 **** 目標設定中建立初始更新（如果尚未存在）

* ***autoFillBeforeImport — 布林值***  — 如果為true，請在匯入前更新/填入目標設定
* ***configSuffix — 字串***  — 附加至app-content之「phonegap-exportTemplate」屬性上所指路徑的字串。這可用來區分不同的匯出範本。 例如，此屬性可設為&#x200B;**&quot;-dev&quot;**，以指出應使用&#x200B;*&quot;/../../../appconfig-dev&quot;*（與&#x200B;*&quot;/../../../appconfig&quot;*&#x200B;相對）。

**app-** assets包含與應用程式例項相關聯的所有資產。此處理常式將包含指定路徑下找到的任何資產，以及應用程式執行個體的appAssetPath屬性所參考的任何資產。

* ***類型 — 字串***  - app-assets

* ***路徑&#x200B;**-**字串***  — 儲存應用程式資產之應用程式例項下位置的路徑

**** mobileappoffers為「個人化」使用案例導入了新的內容同步處理常式，以呈現目標內容。「mobileappoffers」處理常式知道如何呈現由內容作者建立的相關目標選件。 Mobileappoffers處理常式會延伸抽象頁面更新處理常式，因此許多屬性相似。 Mobileappoffers處理常式的詳細資訊具有下列屬性。

mobileappsoffers處理常式會擴充mobileappspages處理常式，並新增下列屬性：

* ***locationRoot — 字串***  — 指定行動應用程式的位置
* ***includePageTypes — 字串***  — 預設值可支援cq/personalization/components/teaserpage和cq/personalization/components/offerproxy
* ***選取器 — 字串***  — 應設為標準
* ***路徑 — 字串*** — 促銷活動品牌的路徑

**** mobileappconfigmobileappconfig內容同步處理常式提供將JSON資料插入MobileAppsConfig.json的方式。要註冊提供程式類，開發人員將將其MobileAppsInfoProvider類添加到提供程式清單中。 處理常式會反覆查看MobileAppsInfoProviders清單，並允許提供者將資料插入產生的json檔案。 此處理程式支援的屬性清單為：

* ***path **-**String***  — 使用pge-type=app-instance的應用程式執行個體節點或延伸/libs/mobileapps/core/components/instance的RT的路徑
* ***providers - String*** `[]`  — 完全限定的MobileAppsInfoProviders清單
* ***targetRootDirectory — 字串***  — 要將MobileAppsConfig.json檔案寫入的目錄。
* **fileName - String**  — 要寫入JSON的檔案選用名稱，預設為MobileAppsConfig.json

可以有多個mobileappconfig處理常式，分別以寫入不同JSON檔案的一組唯一提供者來設定。

### 測試內容同步處理程式{#testing-content-sync-handlers}

**檢查IntegrityClear快取** 的步驟

* 清除快取
* 執行處理常式（已更新快取）
* 再次運行處理程式（不應更新快取）

**除錯步驟**

* 執行您的設定
* 匯出設定或在裝置上檢閱
* 如果呈現無法檢查遺失的&#x200B;*styles/assets/libs*，或檢查&#x200B;*styles/assets/libs*&#x200B;的不良路徑

**** 記錄透過套件上的OSGI記錄器設定啟用ContentSync除錯記錄 `com.day.cq.contentsync` 將可讓您追蹤已執行的處理常式，以及它們是否更新快取及回報更新快取。

## 其他資源 {#additional-resources}

若要了解管理員和開發人員的角色和責任，請參閱下列資源：

* [使用AEM編寫Adobe PhoneGap Enterprise](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>若要開始使用AEM Mobile應用程式開發，請按一下[這裡](/help/mobile/getting-started-aem-mobile.md)。
