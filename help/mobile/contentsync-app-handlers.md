---
title: 開箱即用的應用程式處理常式
description: 請詳閱本頁面，瞭解搭配AEM的Adobe PhoneGap Enterprise適用的現成處理常式。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---

# 開箱即用的應用程式處理常式{#out-of-the-box-app-handlers}

{{ue-over-mobile}}

請參閱下列開發Content Sync處理常式的准則：

* 處理常式必須實作&#x200B;*com.day.cq.contentsync.handler.ContentUpdateHandler* （直接或擴充有此功能的類別）
* 處理常式可擴充&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 如果處理常式更新了ContentSync快取，則只能報告true。 錯誤報告true將允許AEM建立更新。
* 只有在內容實際變更時，處理常式才能更新快取。 如果不需要白色，請勿寫入快取，並避免建立不必要的更新。

## 現成可用的處理常式 {#out-of-the-box-handlers}

以下列出現成可用的應用程式處理常式：

**mobileapppages**&#x200B;轉譯應用程式頁面。

* ***型別 — 字串*** - mobileapppages
* ***路徑 — 字串*** — 頁面的路徑
* ***延伸模組 — 字串*** — 應在要求中使用的延伸模組。 對於頁面，這幾乎總是&#x200B;*html*，但其他仍然可能。

* ***選取器 — 字串*** — 以點分隔的選用選取器。 轉譯頁面行動版本的常見範例為&#x200B;*touch*。

* ***deep - Boolean*** — 決定是否也應該包含子頁面的選用布林屬性。 預設值為&#x200B;*true。*

* ***includeImages - Boolean*** — 決定是否應包含影像的選用布林屬性。 預設值為&#x200B;*true*。

   * 依預設，只有資源型別為foundation/components/image的影像元件才會被視為包含。

* ***includeVideos — 布林值*** — 選擇性布林值屬性決定是否應包含影片。 預設值為&#x200B;*true*。

* ***includeModifiedPagesOnly — 布林值*** — 如果為false或省略，則轉譯所有頁面並檢查轉譯中的更新。 如果為true，則根據對頁面lastModified的變更來變更。
* ***+重寫（節點）***
  ***- relativeParentPath — 字串*** — 寫入所有其他相對路徑的路徑。

>[!NOTE]
>
>設定&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler*&#x200B;的屬性，即可設定受此處理常式影響的影像與視訊元件的資源型別。*MobilePagesUpdateHandler OSGi服務*。

**mobilepageassets**&#x200B;收集應用程式頁面資產。

**mobilecontentlisting**&#x200B;列出ContentSync壓縮檔的內容。 裝置上的使用者端js會使用此檔案，執行AEM應用程式所需的初始檔案複製。

應該將此處理常式新增至任何AEM Apps ContentSync設定。

* ***型別 — 字串 — mobilecontentlisting***
* ***path*** — 字串 — 保持空白，必須存在才能被視為有效的處理常式，但路徑被推斷為目前的ContentSync快取。 此值會被忽略。
* ***targetRootDirectory* -**字串 — 新增至路徑的前置詞，作為此處理常式內容更新的目標根目錄。
* ContentSync要執行此處理常式的&#x200B;***順序 — Long* -**順序。 此數字應設定為高於所有其他處理常式，例如100。 它應在傳統內容處理常式之後執行。

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

**mobilecontentpackageslisting**&#x200B;列出指定應用程式中的AEM內容封裝，以及要向其提出更新請求的serverURL。 這會用於裝置上的使用者端js來請求內容更新

該處理常式應該用於AEM應用程式殼層ContentSync設定（具有pge-type=app-instance的節點）

* ***型別 — 字串 — mobilecontentpackageslisting***
* ***path **-**字串*** — 應用程式殼層（pge-type=app-instance的節點）的路徑。
* ***targetRootDirectory — 字串*** — 要新增至路徑的前置詞，作為此處理常式內容更新的目標根目錄。
* ContentSync要執行此處理常式的&#x200B;***順序 — Long* -**順序。 此數字應設定為高於所有其他處理常式，例如100。 它應在傳統內容處理常式之後執行。

>[!NOTE]
>
>下列程式碼區塊並非確切實施，應作為參考範例使用：

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

**widgetconfig**&#x200B;包含更新的config.xml，它會合併透過命令中心所做的任何編輯與提供的config.xml。 如果未包含此處理常式，則透過Administration介面變更的任何應用程式詳細資料都不會包含在快取中。

這個處理常式應該用於AEM App Shell ContentSync設定（具有pge-type=[app-instance]的節點）。

* ***型別 — 字串* - **widgetconfig
* ***path **-**字串*** — 任何應用程式殼層子節點（pge-type=[app-instance]的節點）的路徑。
* ***targetRootDirectory — 字串*** — 要新增至路徑的前置詞，作為此處理常式內容更新的目標根目錄。
* ***targetIconDirectory — 字串*** — 應用程式圖示放置目錄

**mobileADBMobileConfigJSON**&#x200B;如果已設定AMS cloudservice，請包含ADBMobileConfig.JSON檔案。

這會在編譯時用來設定AMS外掛程式以提供分析支援。

該處理常式應該用於AEM應用程式殼層ContentSync設定（具有pge-type=app-instance的節點）

* ***型別 — 字串*** - mobileADBMobileConfigJSON
* ***path — 字串*** — 應用程式殼層的路徑（具有pge-type=app-instance的節點或擴充/libs/mobileapps/core/components/instance的RT）
* ***targetRootDirectory — 字串*** — 要新增至路徑的前置詞，作為此處理常式內容更新的目標根目錄

**notificationsconfig**&#x200B;擷取裝置上所需的通知設定。 屬性會從與應用程式關聯的個別推送服務雲端服務設定中擷取。

已擷取雲端服務jcr：content節點中的非AEM屬性，並將其新增至&#x200B;**pge-notifications-config.json** JSON檔案，以包含在應用程式內容的www根中。

AEM屬性是使用「cq」、「sling」或「jcr」建立名稱間距的屬性。 您可以使用content-sync設定節點上的「excludeProperties」屬性來排除其他屬性。

* ***型別 — 字串*** - notificationsconfig
* ***excludeProperties — 字串[]*** — 要排除的屬性

**contentsyncconfigcontent**&#x200B;從現有的ContentSync設定收集內容。

* ***型別 — 字串*** - contentsyncconfigcontent
* ***path — 字串*** — 下列其中一個的路徑：

   * 另一個ContentSync設定
   * 至內容封裝（將使用其phonegap-exportTemplate屬性來尋找其ContentSync設定）
   * 至行動資源（若這些內容套件的page-includeInBuild屬性為true，則會使用phonegap-exportTemplate尋找其ContentSync設定）

* ***autoCreateFirstUpdateBeforeImport — 布林值*** — 如果為true，則在匯入之前先在目標設定中建立初始&#x200B;**更新** （如果一次不存在）

* ***autoFillBeforeImport — 布林值*** — 如果為true，請先更新/填入目標設定再匯入
* ***configSuffix - String*** — 要附加至app-content的「phonegap-exportTemplate」屬性上所指示的路徑的字串。 這可用來區分不同的匯出範本。 例如，此屬性可設為&#x200B;**&quot;-dev&quot;**，以表示應使用&#x200B;*&quot;/../../../appconfig-dev&quot;* （與&#x200B;*&quot;/../../../appconfig&quot;*&#x200B;相對）。

**app-assets**&#x200B;包含與應用程式執行個體相關聯的所有資產。 此處理常式會包含在指定路徑下找到的任何資產，以及應用程式執行個體的appAssetPath屬性所參考的任何資產。

* ***型別 — 字串*** — 應用程式資產

* ***path **-**字串*** — 應用程式執行個體下儲存應用程式資產之位置的路徑

**mobileappoffers**&#x200B;已為Personalization使用案例引入新的內容同步處理常式，以便呈現目標內容。 「mobileappoffers」處理常式會知道如何呈現內容作者所建立的相關目標選件。 mobileappoffers處理常式會擴充抽象頁面更新處理常式，因此許多屬性都類似。 mobileappoffers處理常式的詳細資訊有下列屬性。

mobileappsoffers處理常式會擴充mobileappspages處理常式，並新增下列屬性：

* ***locationRoot — 字串*** — 指定行動應用程式的位置
* ***includePageTypes — 字串*** — 預設為支援cq/personalization/components/teaserpage和cq/personalization/components/offerproxy
* ***選取器 — 字串*** — 應設為tandt
* ***路徑 — 字串*** — 行銷活動品牌的路徑

**mobileappconfig** mobileappconfig內容同步處理常式提供將JSON資料插入MobileAppsConfig.json的方法。 若要註冊提供者類別，開發人員會在提供者清單中新增其MobileAppsInfoProvider類別。 處理常式會對MobileAppsInfoProviders清單進行反複運算，並允許提供者將資料插入產生的json檔案中。 此處理常式支援的屬性清單為：

* ***path **-**String*** — 具有pge-type=app-instance或擴充/libs/mobileapps/core/components/instance之RT的應用程式執行個體節點的路徑
* ***提供者 — 字串*** `[]` — 完整限定的MobileAppsInfoProviders清單
* ***targetRootDirectory — 字串*** — 將MobileAppsConfig.json檔案寫入的目錄。
* **fileName — 字串** — 要將JSON寫入的檔案選擇性名稱，預設為MobileAppsConfig.json

可能有多個mobileappconfig處理常式分別設定為一組寫入不同JSON檔案的唯一提供者。

### 測試內容同步處理常式 {#testing-content-sync-handlers}

**檢查完整性的步驟**&#x200B;清除快取

* 清除快取
* 執行您的處理常式（已更新快取）
* 再次執行您的處理常式（不應更新快取）

偵錯的&#x200B;**步驟**

* 執行您的設定
* 在裝置上匯出設定或檢閱
* 如果演算失敗，請檢查遺失&#x200B;*樣式/資產/程式庫*，或檢查&#x200B;*樣式/資產/程式庫*&#x200B;的錯誤路徑

**記錄**&#x200B;透過封裝`com.day.cq.contentsync`上的OSGI記錄器設定啟用ContentSync偵錯記錄這將可讓您追蹤哪些處理常式已執行，以及它們是否更新快取並回報更新快取。

## 其他資源 {#additional-resources}

若要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise製作](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>若要開始使用AEM Mobile應用程式開發，請按一下[這裡](/help/mobile/getting-started-aem-mobile.md)。
