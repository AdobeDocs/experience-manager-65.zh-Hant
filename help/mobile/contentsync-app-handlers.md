---
title: 開箱應用處理程式
seo-title: Out of the Box App Handlers
description: 有關Adobe PhoneGap企業的開箱處理程式，請訪問此頁AEM。
seo-description: Follow this page to learn about the out-of-the-box handlers for Adobe PhoneGap Enterprise with AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# 開箱應用處理程式{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

有關開發內容同步處理程式，請參閱以下准則：

* 處理程式必須實現 *com.day.cq.contentsync.handler.ContentUpdateHandler* （直接或擴展該類）
* 處理程式可以擴展 *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 只有更新了ContentSync快取時，處理程式才能報告為true。 錯誤報告true將允AEM許建立更新。
* 僅當內容實際發生更改時，處理程式才應更新快取。 如果不需要白色，請不要寫入快取，並避免不必要的更新建立。

## 開箱處理程式 {#out-of-the-box-handlers}

以下列出了現成的應用程式處理程式：

**移動設備** 呈現應用頁。

* ***類型 — 字串***  — 移動設備
* ***路徑 — 字串***  — 頁面路徑
* ***擴展 — 字串***  — 請求中應使用的擴展。 對於頁面，這幾乎總是 *html*&#x200B;但其他方面仍有可能。

* ***選擇器 — 字串***  — 可選選擇器以點分隔。 常見示例有 *觸摸* 用於呈現頁面的移動版本。

* ***deep — 布爾型***  — 可選布爾屬性，確定是否還應包括子頁。 預設值為 *是的。*

* ***includeImages — 布爾型***  — 確定是否應包括影像的可選布爾屬性。 預設值為 *真*。

   * 預設情況下，只考慮包含資源類型為foundation/components/image的映像元件。

* ***includeVideos — 布爾型***  — 可選布爾屬性確定是否應包括視頻。 預設值為 *真*。

* ***includeModifiedPagesOnly — 布爾型***  — 如果為false或省略，則呈現所有頁面並檢查呈現中的更新。 如果為true，則基於對lastModified頁面的更改進行差異。
* ***+重寫（節點）***
   ***- relativeParentPath — 字串***  — 寫入相對於的所有其他路徑的路徑。

>[!NOTE]
>
>通過配置以下屬性來設定受此處理程式影響的影像和視頻元件的資源類型 *com.adobe.cq.mobile.platform.impl.contentsync.handler*。*MobilePagesUpdateHandler OSGi服務*。

**移動資產** 收集應用頁面資產。

**移動連接清單** 列出ContentSynczip的內容。 設備上的客戶端js使用此功能執行應用程式所需的初始文AEM件副本。

應將此處理程式添加到任何AEMApps ContentSync配置中。

* ***類型 — 字串 — 移動連接清單***
* ***路徑***  — 字串 — 保持空，必須存在才能被視為有效的處理程式，但路徑被推斷為當前ContentSync快取。 此值被忽略。
* ***目標根目錄* -**String — 作為此處理程式內容更新的目標根添加到路徑的前置詞。
* ***訂單 — 長* -**ContentSync執行此處理程式的順序。 此數字應設定為高於所有其他處理程式（如100）。 它應該在傳統內容處理程式之後運行。

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

**移動連接包清單** 列出AEM給定應用中的內容包以及向其發出更新請求的serverURL。 這是使用設備上的客戶端j請求內容更新

處理程式應用於AEMApp Shell ContentSync配置（具有pge-type=app-instance的節點）

* ***類型 — 字串 — mobilecontentpackageslisting***
* ***路徑&#x200B;**-**字串***  — 應用shell（pge-type=app-instance的節點）的路徑。
* ***targetRootDirectory — 字串***  — 要作為此處理程式的內容更新的目標根添加到路徑的前置詞。
* ***訂單 — 長* -**ContentSync執行此處理程式的順序。 此數字應設定為高於所有其他處理程式（如100）。 它應該在傳統內容處理程式之後運行。

>[!NOTE]
>
>以下代碼塊不是精確的實現，應用作參考示例：

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

**widgetconfig** 包括已更新的config.xml，它將通過命令中心所做的任何編輯與提供的config.xml合併。 如果未包括此處理程式，則通過管理介面更改的任何應用程式詳細資訊都將不包括在快取中。

此處理程式應用於AEMApp Shell ContentSync配置（pge-type=的節點）[應用實例])。

* ***類型 — 字串* - **widgetconfig
* ***路徑&#x200B;**-**字串***  — 任何應用程式shell子節點（具有pge-type=的節點）的路徑[應用實例])。
* ***targetRootDirectory — 字串***  — 要作為此處理程式的內容更新的目標根添加到路徑的前置詞。
* ***targetIconDirectory — 字串***  — 用於放置應用程式表徵圖的目錄

**mobileADBMobileConfigJSON** 如果配置了AMS雲服務，則包括ADBMobileConfig.JSON檔案。

在編譯時使用此功能來配置AMS插件以用於分析支援。

處理程式應用於AEMApp Shell ContentSync配置（具有pge-type=app-instance的節點）

* ***類型 — 字串*** - mobileADBMobileConfigJSON
* ***路徑 — 字串***  — 應用shell的路徑（具有pge-type=app-instance的節點或擴展/libs/mobileapps/core/components/instance的RT）
* ***targetRootDirectory — 字串***  — 要作為此處理程式的內容更新的目標根添加到路徑的前置詞

**通知配置** 提取設備上所需的通知配置。 從與應用相關聯的相應推送服務雲服務配置中提取屬性。

將提AEM取雲服務的jcr:content節點中的非屬性並添加到 **pge-notifications-config-json** 要包含在應用內容的www根目錄中的JSON檔案。

屬AEM性是與「cq」、「sling」或「jcr」隔開的名稱。 其他屬性可以使用內容同步配置節點上的「excludeProperties」屬性排除。

* ***類型 — 字串***  — 通知配置
* ***excludeProperties — 字串[]***  — 要排除的屬性

**內容syncconfigcontent** 從現有ContentSync配置收集內容。

* ***類型 — 字串***  — 內容syncconfigcontent
* ***路徑 — 字串***  — 指向以下之一的路徑：

   * 另一個ContentSync配置
   * 內容包（將使用其phonegap-exportTemplate屬性查找其ContentSync配置）
   * 到移動資源(應用內容將在該資源下找到，如果這些內容包具有pge-includeInBuild屬性（為true），則phonegap-exportTemplate將用於查找其ContentSync配置)

* ***autoCreateFirstUpdateBeforeImport — 布爾型***  — 如果為true，則建立初始 **更新** 在導入之前，目標配置中的

* ***autoFillBeforeImport — 布爾型***  — 如果為true，則在導入之前更新/填充目標配置
* ***configSuffix — 字串***  — 要附加到app-content的「phonegap-exportTemplate」屬性上指示的路徑的字串。 這可用於區分不同的導出模板。 例如，此屬性可設定為 **&quot;-dev&quot;** 表示 *&quot;/../../../appconfig-dev&quot;* 應使用(而不是 *&quot;/.././../appconfig&quot;*)。

**app資產** 包括與應用實例關聯的所有資產。 此處理程式將包括在指定路徑下找到的任何資產以及應用程式實例的appAssetPath屬性引用的任何資產。

* ***類型 — 字串***  — 應用程式資產

* ***路徑&#x200B;**-**字串***  — 應用程式實例下儲存應用程式資產的位置的路徑

**移動助理** 已為個性化用例引入新的內容同步處理程式來呈現目標內容。 「mobileapporfers」處理程式知道如何呈現由內容作者建立的關聯目標提供。 mobileapporfers處理程式擴展了抽象頁更新處理程式，因此許多屬性相似。 mobileapporfers處理程式的詳細資訊具有以下屬性。

mobileappsoffers處理程式擴展mobileappspages處理程式並添加以下屬性：

* ***locationRoot — 字串***  — 指定移動應用程式的位置
* ***includePageTypes — 字串***  — 預設支援cq/個性化/元件/續簽頁和cq/個性化/元件/服務代理
* ***選擇器 — 字串***  — 應設定為tandt
* ***路徑 — 字串*** — 通向該活動品牌的途徑

**移動appconfig** mobileappconfig內容同步處理程式提供了一種將JSON資料注入MobileAppsConfig.json的方法。 要註冊提供程式類開發者，會將其MobileAppsInfoProvider類添加到提供程式清單中。 處理程式將循環訪問MobileAppsInfoProviders的清單，並允許提供程式將資料注入結果的json檔案。 此處理程式支援的屬性清單包括：

* ***路徑&#x200B;**-**字串***  — 使用pge-type=app-instance的應用程式實例節點或擴展/libs/mobileapps/core/components/instance的RT的路徑
* ***提供程式 — 字串*** `[]`  — 完全限定的MobileAppsInfoProviders清單
* ***targetRootDirectory — 字串***  — 將MobileAppsConfig.json檔案寫入的目錄。
* **fileName — 字串**  — 要將JSON寫入的檔案的可選名稱，預設為MobileAppsConfig.json

可以配置多個mobileappconfig處理程式，每個處理程式都配置了一組唯一的提供程式，這些提供程式寫入到不同的JSON檔案。

### 測試內容同步處理程式 {#testing-content-sync-handlers}

**檢查完整性的步驟** 清除快取

* 清除快取
* 運行處理程式（已更新快取）
* 再次運行處理程式（不應更新快取）

**調試步驟**

* 運行配置
* 導出設備配置或查看
* 如果呈現失敗，請檢查是否缺少 *樣式/資產/lib* 或檢查到的錯誤路徑 *樣式/資產/lib*

**記錄** 通過包上的OSGI記錄器配置啟用ContentSync調試日誌記錄 `com.day.cq.contentsync` 這將允許您跟蹤運行的處理程式以及它們是否更新了快取和報告了更新快取。

## 其他資源 {#additional-resources}

要瞭解管理員和開發人員的角色和職責，請參閱以下資源：

* [為Adobe PhoneGap企業創AEM作](/help/mobile/phonegap.md)
* [為Adobe PhoneGap企業管理內AEM容](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>若要開始使用AEM Mobile應用程式開發，請按一下 [這裡](/help/mobile/getting-started-aem-mobile.md)。
