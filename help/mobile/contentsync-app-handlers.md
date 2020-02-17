---
title: 立即可用的應用程式處理常式
seo-title: 立即可用的應用程式處理常式
description: 請依照本頁瞭解Adobe phoneGap Enterprise與AEM的現成可用處理常式。
seo-description: 請依照本頁瞭解Adobe phoneGap Enterprise與AEM的現成可用處理常式。
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 立即可用的應用程式處理常式{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

請參閱以下開發內容同步處理常式的准則：

* 處理常式必 *須實作com.day.cq.contentsync.handler.ContentUpdateHandler* （直接或擴充可執行的類別）
* 處理常式可 *以擴充com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 如果處理常式更新了ContentSync快取，則只能報告true。 不實報告true可讓AEM建立更新。
* 處理常式只會在內容實際變更時更新快取。 如果不需要白色，請勿寫入快取，並避免建立不必要的更新。

## 出廠設定處理程式 {#out-of-the-box-handlers}

下列列出現成可用的應用程式處理常式：

**mobileapppages** 轉譯應用程式頁面。

* ***type - String*** - mobileappages
* ***path —— 字串*** -頁面的路徑
* ***extension —— 字串*** -請求中應使用的擴充功能。 對於頁面，這幾乎總是 *html*，但其他頁面仍有可能。

* ***selector —— 字串*** -選用選擇器以點分隔。 常見的例 *子是* ，以觸控方式呈現頁面的行動版本。

* ***deep - Boolean*** —— 可選的布林屬性，決定是否也應包含子頁面。 預設值 *為true。*

* ***includeImages - Boolean*** —— 可選布林屬性，決定是否應包含影像。 預設值 *為true*。

   * 預設情況下，僅考慮包含資源類型為foundation/components/image的映像元件。

* ***includeVideos - Boolean*** - Optional boolean屬性可決定是否應包含視訊。 預設值 *為true*。

* ***includeModifiedPagesOnly - Boolean*** —— 如果false或省略，則會演算所有頁面並檢查演算中的更新。 如果為true，則根據lastModified頁面的變更進行變更。
* ***+ rewrite（節點）***
   ***- relativeParentPath —— 字串*** -寫入相對的所有其他路徑的路徑。

>[!NOTE]
>
>受此處理常式影響的影像和視訊元件的資源類型是透過設定 *com.adobe.cq.mobile.platform.impl.contentsync.handler的屬性來設定*。*MobilePagesUpdateHandler OSGi服務*。

**mobilepageassets** 收集應用程式頁面資產。

**mobilecontentlisting** Lists the contentSync zip. 這是裝置上的用戶端js用來執行AEM應用程式所需的初始檔案復本。

此處理常式應新增至任何AEM應用程式ContentSync設定。

* ***type - String - mobilecontenlisting***
* ***path*** —— 字串——保留空白，必須顯示為有效的處理常式，但路徑會推斷為目前的ContentSync快取。 此值被忽略。
* ***targetRootDirectory ***- String —— 要作為此處理常式內容更新的目標根目錄添加到路徑的前置詞。
* ***order - Long ***- Order for ContentSync to exture this handler. 此數字應設定為高於所有其他處理程式（如100）。 它應在傳統內容處理常式後執行。

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

**mobilecontentpackageslisting** Lists the AEM content package in a given app and the serverURL to make update requests to. 這是使用裝置上的用戶端js來請求內容更新

此處理常式應用於AEM App Shell ContentSync Config（含pge-type=app-instance的節點）

* ***type - String - mobilecontentpackageslisting***
* ***path **-**String*** —— 應用程式殼層的路徑（pge-type=app-instance的節點）。
* ***targetRootDirectory - String*** —— 要作為此處理常式內容更新的目標根目錄添加到路徑的前置詞。
* ***order - Long *-**Order for ContentSync to execute this handler. 此數字應設定為高於所有其他處理程式（如100）。 它應在傳統內容處理常式後執行。

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

**widgetconfig** 包含更新的config.xml，可合併透過命令中心所做的任何編輯和提供的config.xml。 如果此處理常式未包含任何透過「管理」介面變更的應用程式詳細資訊，則快取中將不會包含這些處理常式。

此處理常式應用於AEM App Shell ContentSync組態(pge-type=[app-instance的節點])。

* ***type —— 字串* - **widgetconfig
* ***path **-**String*** —— 任何應用程式殼層子節點的路徑(pge-type=[app-instance]的節點)。
* ***targetRootDirectory - String*** —— 要作為此處理常式內容更新的目標根目錄添加到路徑的前置詞。
* ***targetIconDirectory - String*** —— 放置應用程式圖示的目錄

**mobileADBMobileConfigJSON** Include the ADBMobileConfig.JSON file if the AMS cloudservice is configured.

在編譯時，會使用它來設定AMS外掛程式以進行分析支援。

此處理常式應用於AEM App Shell ContentSync Config（含pge-type=app-instance的節點）

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String*** —— 應用程式殼層的路徑（pge-type=app-instance的節點，或延伸/libs/mobileapps/core/components/instance的RT）
* ***targetRootDirectory - String*** —— 要作為此處理常式內容更新的目標根目錄添加到路徑的前置詞

**通知config** 提取設備上需要的通知配置。 屬性從與應用程式相關聯的各個推送服務雲端服務組態中擷取。

雲端服務jcr:content節點中的非AEM屬性會解壓縮並新增至 **pge-notifications-config.json** JSON檔案，以便包含在應用程式內容的www根目錄中。

AEM屬性是以&quot;cq&quot;、&quot;sling&quot;或&quot;jcr&quot;隔開名稱的屬性。 其他屬性可以使用content-sync配置節點上的&quot;excludeProperties&quot;屬性來排除。

* ***type - String*** - notificationsconfig
* ***excludeProperties - String[]*** —— 要排除的屬性

**contentsyncconfigcontent** 從現有的ContentSync配置收集內容。

* ***type - String*** - contentsyncconfigcontent
* ***路徑——字串*** -指向以下任一路徑的路徑：

   * 另一個ContentSync設定
   * 至內容套件（將使用其phonegap-exportTemplate屬性來尋找其ContentSync設定）
   * 至行動資源（應用程式內容將在該資源下找到，如果這些內容套件具有pge-includeInBuild屬性，則為true，則phonegap-exportTemplate將用來尋找其ContentSync設定）

* ***autoCreateFirstUpdateBeforeImport - Boolean*** —— 如果為true，請在匯入之前，先在目標設定中建立初始 **更新** ，如果尚未匯入

* ***autoFillBeforeImport - Boolean*** —— 如果為true，請在匯入前更新／填寫目標設定
* ***configSuffix —— 字串*** -要附加至app-content「phonegap-exportTemplate」屬性上所指路徑的字串。 這可用來區分不同的匯出範本。 例如，此屬性可設為 **&quot;-dev&quot;** ，以指出應使用 *&quot;/.../.././appconfig-dev&quot;(與* &quot;/..././../../appconfig&quot;相反 **)。

**app-assets** 包含與應用程式例項關聯的所有資產。 此處理常式將包含在指定路徑下找到的任何資產，以及應用程式例項的appAssetPath屬性所參照的任何資產。

* ***type - String*** - app-assets

* ***path **-**String*** —— 應用程式例項下儲存應用程式資產之位置的路徑

**mobileapporfers** Personalization使用案例已引入新的內容同步處理常式，以呈現目標內容。 「mobileappoffers」處理常式瞭解如何轉譯由內容作者建立的相關目標選件。 Mobileapporfers處理常式會延伸抽象頁面更新處理常式，因此許多屬性都類似。 mobileapporfers處理常式的詳細資料包含下列屬性。

mobileappsoffers處理常式會延伸mobileappspages處理常式並新增下列屬性：

* ***locationRoot —— 字串*** -指定行動應用程式的位置
* ***includePageTypes - String*** —— 預設值，以支援cq/personalization/components/teaserpage和cq/personalization/components/offerproxy
* ***selector —— 字串*** -應設為tand
* ***路徑——字串***-促銷活動品牌的路徑

**mobileappconfig** Mobileappconfig內容同步處理常式提供將JSON資料插入MobileAppsConfig.json的方式。 若要註冊提供者類別，開發人員會將其MobileAppsInfoProvider類別新增至提供者清單。 處理常式會重複MobileAppsInfoProviders的清單，並允許提供者將資料插入產生的json檔案。 此處理程式支援的屬性清單包括：

* ***path **-**String*** —— 使用pge-type=app-instance的應用程式例項節點，或延伸/libs/mobileapps/core/components/instance的RT的路徑
* ***提供者——字串*** -完全限定 `[]` 的MobileAppsInfoProviders清單
* ***targetRootDirectory - String*** —— 要寫入MobileAppsConfig.json檔案的目錄。
* **fileName - String** —— 要寫入JSON的檔案的選用名稱，預設為MobileAppsConfig.json

您可以設定多個mobileappconfig處理常式，每個處理常式都有一組唯一的提供者寫入不同的JSON檔案。

### 測試內容同步處理常式 {#testing-content-sync-handlers}

**檢查完整性** Clear快取的步驟

* 清除快取
* 執行處理常式（快取已更新）
* 再次運行處理程式（不應更新快取）

**除錯步驟**

* 執行您的設定
* 在裝置上匯出您的設定或檢閱
* 如果轉換失敗，請檢查 *樣式／資產/lib是否遺失* ，或檢查樣式／資產/lib *的不良路徑*

**記錄**`com.day.cq.contentsync` 透過OSGI記錄程式組態在套件上啟用ContentSync除錯記錄這可讓您追蹤執行的處理常式，以及處理常式是否更新快取並報告更新快取。

## 其他資源 {#additional-resources}

要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM製作Adobe PhoneGap Enterprise](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>若要開始使用AEM mobile應用程式開發，請按一 [下這裡](/help/mobile/getting-started-aem-mobile.md)。

