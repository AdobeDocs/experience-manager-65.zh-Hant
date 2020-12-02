---
title: 立即可用的應用程式處理常式
seo-title: 立即可用的應用程式處理常式
description: 請依照本頁瞭解Adobe PhoneGap Enterprise與AEM的現成可用處理常式。
seo-description: 請依照本頁瞭解Adobe PhoneGap Enterprise與AEM的現成可用處理常式。
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---


# 立即可用的應用程式處理常式{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

請參閱以下開發內容同步處理常式的准則：

* 處理常式必須實作&#x200B;*com.day.cq.contentsync.handler.ContentUpdateHandler*（直接或擴充執行此動作的類別）
* 處理常式可擴充&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 如果處理常式更新了ContentSync快取，則只能報告true。 不實報告true可讓AEM建立更新。
* 處理常式只會在內容實際變更時更新快取。 如果不需要白色，請勿寫入快取，並避免建立不必要的更新。

## 出廠設定處理程式{#out-of-the-box-handlers}

下列列出現成可用的應用程式處理常式：

**Mobileappages** 轉譯應用程式頁面。

* ***type - String*** - mobileappages
* ***路徑——字串*** -頁面的路徑
* ***extension —— 字串*** -應用於請求的擴充功能。對於頁面，這幾乎總是&#x200B;*html*，但其他頁面仍然可能。

* ***selector —— 字串*** -選用選擇器以點分隔。常見的範例有&#x200B;*touch*，以呈現頁面的行動版本。

* ***deep - Boolean***  —— 可選的布林屬性，決定是否也應包含子頁面。預設值為&#x200B;*true。*

* ***includeImages - Boolean***  —— 可選布林屬性，決定是否應包含影像。預設值為&#x200B;*true*。

   * 預設情況下，僅考慮包含資源類型為foundation/components/image的映像元件。

* ***includeVideos - Boolean***  - Optional boolean屬性，決定是否應包含視訊。預設值為&#x200B;*true*。

* ***includeModifiedPagesOnly - Boolean***  —— 如果false或省略，則演算所有頁面並檢查演算中的更新。如果為true，則根據lastModified頁面的變更進行變更。
* ***+ rewrite（節點）***
   ***- relativeParentPath —— 字串*** -寫入相對的所有其他路徑的路徑。

>[!NOTE]
>
>通過配置&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler*&#x200B;的屬性，可設定受此處理程式影響的映像和視頻元件的資源類型。*MobilePagesUpdateHandler OSGi服務*。

**Mobilepageassets** 收集應用程式頁面資產。

**** Mobilecontentlisting列出ContentSync zip的內容。這是裝置上的用戶端js用來執行AEM應用程式所需的初始檔案復本。

此處理常式應新增至任何AEM應用程式ContentSync設定。

* ***type - String - mobilecontenlisting***
* ***path***  - String - keep empty，必須顯示為有效的處理常式，但路徑會推斷為目前的ContentSync快取。此值被忽略。
* ***targetRootDirectory* -**String —— 要作為此處理常式內容更新的目標根目錄添加到路徑的前置詞。
* ***order - Content* Sync的&#x200B;**長順序，以執行此處理常式。此數字應設定為高於所有其他處理程式（如100）。 它應在傳統內容處理常式後執行。

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

**Mobilecontentpackages** 清單列出指定應用程式中的AEM內容套件，以及要向其提出更新請求的serverURL。這是使用裝置上的用戶端js來請求內容更新

此處理常式應用於AEM App Shell ContentSync Config（含pge-type=app-instance的節點）

* ***type - String - mobilecontentpackageslisting***
* ***path **-**String***  —— 應用程式殼層的路徑（pge-type=app-instance的節點）。
* ***targetRootDirectory - String***  —— 要作為此處理常式內容更新的目標根目錄添加到路徑的前置詞。
* ***order — Content* Sync **執行此處理常式的長順序。此數字應設定為高於所有其他處理程式（如100）。 它應在傳統內容處理常式後執行。

>[!NOTE]
>
>下列程式碼區塊並非精確的實作，應當做參考範例使用：

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

**** widgetconfig包含更新的config.xml，可合併透過命令中心所做的任何編輯和提供的config.xml。如果此處理常式未包含任何透過「管理」介面變更的應用程式詳細資訊，則快取中將不會包含這些處理常式。

此處理常式應用於AEM App Shell ContentSync組態（pge-type=[app-instance]的節點）。

* ***type - String* - **widgetconfig
* ***path **-**String***  —— 指向任何應用程式殼層子節點的路徑(具有pge-type=[app-instance的節點])。
* ***targetRootDirectory - String***  —— 要作為此處理常式內容更新的目標根目錄添加到路徑的前置詞。
* ***targetIconDirectory - String***  —— 放置應用程式圖示的目錄

**** mobileADBMobileConfigJSONI如果已設定AMS cloud服務，則包含ADBMobileConfig.JSON檔案。

在編譯時，會使用它來設定AMS外掛程式以進行分析支援。

此處理常式應用於AEM App Shell ContentSync Config（含pge-type=app-instance的節點）

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String***  —— 應用程式殼層的路徑（具有pge-type=app-instance的節點，或延伸/libs/mobileapps/core/components/instance的RT）
* ***targetRootDirectory - String***  —— 要作為此處理常式內容更新的目標根目錄添加到路徑的前置詞

**通知** config提取設備上所需的通知配置。屬性從與應用程式相關聯的各個推送服務雲端服務組態中擷取。

雲端服務的jcr:content節點中的非AEM屬性會解壓縮並新增至&#x200B;**pge-notifications-config.json** JSON檔案，以便包含在應用程式內容的www根目錄中。

AEM屬性是以&quot;cq&quot;、&quot;sling&quot;或&quot;jcr&quot;隔開名稱的屬性。 其他屬性可以使用content-sync配置節點上的&quot;excludeProperties&quot;屬性來排除。

* ***type —— 字串*** -通知config
* ***excludeProperties —— 要排除的字串[]*** -屬性

**contentsyncconfigcontent** 從現有的ContentSync設定收集內容。

* ***type - String***  - contentsyncconfigcontent
* ***路徑——字串*** -指向以下任一路徑：

   * 另一個ContentSync設定
   * 至內容套件（將使用其phonegap-exportTemplate屬性來尋找其ContentSync設定）
   * 至行動資源（應用程式內容將在該資源下找到，如果這些內容套件具有pge-includeInBuild屬性，則為true，則phonegap-exportTemplate將用來尋找其ContentSync設定）

* ***autoCreateFirstUpdateBeforeImport - Boolean*** - if true, create a nitial  **** updatein the target config before importing if once not exist

* ***autoFillBeforeImport - Boolean*** - if true, update/fill the target config before importing
* ***configSuffix - String***  —— 一個字串，可附加至app-content的「phonegap-exportTemplate」屬性上指示的路徑。這可用來區分不同的匯出範本。 例如，此屬性可設為&#x200B;**&quot;-dev&quot;**，以指出應使用&#x200B;*&quot;/../../../appconfig-dev&quot;*（與&#x200B;*&quot;/../../../appconfig&quot;*&#x200B;相反）。

**app-** assets包含與應用程式例項相關聯的所有資產。此處理常式將包含在指定路徑下找到的任何資產，以及應用程式例項的appAssetPath屬性所參照的任何資產。

* ***type - String*** - app-assets

* ***path **-**String*** -應用程式例項下儲存應用程式資產之位置的路徑

**Mobileappoffers** 個人化使用案例已引入新的內容同步處理常式，以呈現目標內容。「mobileappoffers」處理常式瞭解如何轉譯由內容作者建立的相關目標選件。 Mobileapporfers處理常式會延伸抽象頁面更新處理常式，因此許多屬性都類似。 mobileapporfers處理常式的詳細資料包含下列屬性。

mobileappsoffers處理常式會延伸mobileappspages處理常式並新增下列屬性：

* ***locationRoot —— 字串*** -指定行動應用程式的位置
* ***includePageTypes - String***  —— 預設值，可支援cq/personalization/components/teaserpage和cq/personalization/components/offerproxy
* ***selector —— 字串*** -應設為tand
* ***路徑——字串***-促銷活動品牌的路徑

**** mobileappconfigmobileappconfig內容同步處理常式提供將JSON資料插入MobileAppsConfig.json的方式。若要註冊提供者類別，開發人員會將其MobileAppsInfoProvider類別新增至提供者清單。 處理常式會重複MobileAppsInfoProviders的清單，並允許提供者將資料插入產生的json檔案。 此處理程式支援的屬性清單包括：

* ***path **-**String***  —— 使用pge-type=app-instance的應用程式例項節點的路徑，或是延伸/libs/mobileapps/core/components/instance的RT
* ***提供者——字串*** `[]` -完全限定的MobileAppsInfoProviders清單
* ***targetRootDirectory - String***  —— 要寫入MobileAppsConfig.json檔案的目錄。
* **fileName - String** -要寫入JSON的檔案的選用名稱，預設為MobileAppsConfig.json

您可以設定多個mobileappconfig處理常式，每個處理常式都有一組唯一的提供者寫入不同的JSON檔案。

### 測試內容同步處理常式{#testing-content-sync-handlers}

**檢查完整性的步** 驟Clear快取

* 清除快取
* 執行處理常式（快取已更新）
* 再次運行處理程式（不應更新快取）

**除錯步驟**

* 執行您的設定
* 在裝置上匯出您的設定或檢閱
* 如果轉換失敗，請檢查缺少&#x200B;*樣式／資產/libs*，或檢查&#x200B;*樣式／資產/libs*&#x200B;的不良路徑

**記** 錄透過OSGI記錄程式組態在封裝上啟用ContentSync除錯記錄 `com.day.cq.contentsync` 這可讓您追蹤執行的處理常式，以及處理常式是否更新快取並報告更新快取。

## 其他資源 {#additional-resources}

要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM製作Adobe PhoneGap Enterprise](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>若要開始使用AEM Mobile應用程式開發，請按一下[這裡](/help/mobile/getting-started-aem-mobile.md)。

