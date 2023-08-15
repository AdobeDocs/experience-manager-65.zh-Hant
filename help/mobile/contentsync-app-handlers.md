---
title: 開箱即用的應用程式處理常式
seo-title: Out of the Box App Handlers
description: 請詳閱本頁面，瞭解搭配AEM的Adobe PhoneGap Enterprise適用的現成處理常式。
seo-description: Follow this page to learn about the out-of-the-box handlers for Adobe PhoneGap Enterprise with AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# 開箱即用的應用程式處理常式{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md)。

請參閱下列開發Content Sync處理常式的准則：

* 處理常式必須實施 *com.day.cq.contentsync.handler.ContentUpdateHandler* （直接或擴充有此功能的類別）
* 處理常式可以擴充 *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 如果處理常式更新了ContentSync快取，則只能報告true。 錯誤報告true將允許AEM建立更新。
* 只有在內容實際變更時，處理常式才能更新快取。 如果不需要白色，請勿寫入快取，並避免建立不必要的更新。

## 現成可用的處理常式 {#out-of-the-box-handlers}

以下列出現成可用的應用程式處理常式：

**mobileapppages** 轉譯應用程式頁面。

* ***型別 — 字串*** - mobileapppages
* ***路徑 — 字串***  — 頁面路徑
* ***副檔名 — 字串***  — 請求中應使用的擴充功能。 對於頁面，這幾乎永遠都是 *html*，但仍可使用其他方法。

* ***選擇器 — 字串***  — 選用的選取器，以點分隔。 常見範例為 *觸控* 用於轉譯頁面的行動版本。

* ***deep — 布林值***  — 決定是否應包含子頁面的選用布林屬性。 預設值為 *true.*

* ***includeImages — 布林值***  — 決定是否應包含影像的選用布林屬性。 預設值為 *true*.

   * 依預設，只有資源型別為foundation/components/image的影像元件才會被視為包含。

* ***includeVideos — 布林值***  — 選用的布林值屬性可決定是否應包含影片。 預設值為 *true*.

* ***includeModifiedPagesOnly — 布林值***  — 如果為false或省略，則會轉譯所有頁面並在轉譯中檢查更新。 如果為true，則根據對頁面lastModified的變更來變更。
* ***+重寫（節點）***
  ***- relativeParentPath — 字串***  — 寫入所有其他相對路徑的路徑。

>[!NOTE]
>
>受此處理常式影響的影像和視訊元件的資源型別是透過設定 *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*MobilePagesUpdateHandler OSGi服務*.

**mobilepageassets** 收集應用程式頁面資產。

**mobilecontentlisting** 列出ContentSync壓縮檔的內容。 裝置上的使用者端js會使用此檔案，執行AEM應用程式所需的初始檔案複製。

應該將此處理常式新增至任何AEM Apps ContentSync設定。

* ***型別 — 字串 — mobilecontentlisting***
* ***路徑***  — 字串 — 保留空白，必須呈現以被視為有效的處理常式，但路徑被推斷為目前的ContentSync快取。 此值會被忽略。
* ***targetRootDirectory* -**字串 — 新增至路徑的前置詞，可作為此處理常式內容更新的目標根目錄。
* ***訂購 — 長* -**ContentSync執行此處理常式的順序。 此數字應設定為高於所有其他處理常式，例如100。 它應在傳統內容處理常式之後執行。

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

**mobilecontentpackageslisting** 列出指定應用程式中的AEM內容套件，以及提出更新請求的serverURL。 這會用於裝置上的使用者端js來請求內容更新

該處理常式應該用於AEM應用程式殼層ContentSync設定（具有pge-type=app-instance的節點）

* ***型別 — 字串 — mobilecontentpackageslisting***
* ***路徑&#x200B;**-**字串***  — 應用程式殼層的路徑（具有page-type=app-instance的節點）。
* ***targetRootDirectory — 字串***  — 新增至路徑的前置詞，可作為此處理常式內容更新的目標根目錄。
* ***訂購 — 長* -**ContentSync執行此處理常式的順序。 此數字應設定為高於所有其他處理常式，例如100。 它應在傳統內容處理常式之後執行。

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

**widgetconfig** 包含更新的config.xml，它將透過命令中心所做的任何編輯與提供的config.xml合併。 如果未包含此處理常式，則透過Administration介面變更的任何應用程式詳細資料都不會包含在快取中。

此處理常式應該用於AEM應用程式殼層ContentSync設定（具有pge-type=的節點）[app-instance])。

* ***型別 — 字串* - **widgetconfig
* ***路徑&#x200B;**-**字串***  — 任何應用程式殼層子節點的路徑（具有page-type=的節點）[app-instance])。
* ***targetRootDirectory — 字串***  — 新增至路徑的前置詞，可作為此處理常式內容更新的目標根目錄。
* ***targetIconDirectory — 字串***  — 用來放置應用程式圖示的目錄

**mobileADBMobileConfigJSON** 如果已設定AMS cloudservice，請包含ADBMobileConfig.JSON檔案。

這會在編譯時用來設定AMS外掛程式以提供分析支援。

該處理常式應該用於AEM應用程式殼層ContentSync設定（具有pge-type=app-instance的節點）

* ***型別 — 字串*** - mobileADBMobileConfigJSON
* ***路徑 — 字串***  — 應用程式Shell的路徑（具有page-type=app-instance的節點或擴充/libs/mobileapps/core/components/instance的RT）
* ***targetRootDirectory — 字串***  — 新增至路徑的前置詞，可作為此處理常式內容更新的目標根目錄

**notificationsconfig** 擷取裝置上所需的通知設定。 屬性會從與應用程式關聯的個別推送服務雲端服務設定中擷取。

雲端服務jcr：content節點中的非AEM屬性會擷取並新增至 **pge-notifications-config.json** 要包含在應用程式內容的www根目錄中的JSON檔案。

AEM屬性是使用「cq」、「sling」或「jcr」建立名稱間距的屬性。 您可以使用content-sync設定節點上的「excludeProperties」屬性來排除其他屬性。

* ***型別 — 字串*** - notificationsconfig
* ***excludeProperties — 字串[]***  — 要排除的屬性

**contentsyncconfigcontent** 從現有的ContentSync設定收集內容。

* ***型別 — 字串*** - contentsynconfigcontent
* ***路徑 — 字串***  — 下列其中一個專案的路徑：

   * 另一個ContentSync設定
   * 至內容封裝（將使用其phonegap-exportTemplate屬性來尋找其ContentSync設定）
   * 至行動資源（若這些內容套件的page-includeInBuild屬性為true，則會使用phonegap-exportTemplate尋找其ContentSync設定）

* ***autoCreateFirstUpdateBeforeImport — 布林值***  — 如果為true，則建立初始 **更新** 在匯入之前的目標設定中（如果已經不存在）

* ***autoFillBeforeImport — 布林值***  — 如果為true，則在匯入之前更新/填寫目標設定
* ***configSuffix — 字串***  — 字串，可附加至app-content的「phonegap-exportTemplate」屬性所指示的路徑。 這可用來區分不同的匯出範本。 例如，此屬性可設為 **「 — dev」** 以表示 *&quot;/../../../appconfig-dev&quot;* 應使用(而非 *&quot;/../../../appconfig&quot;*)。

**應用程式資產** 包含與應用程式例項相關聯的所有資產。 此處理常式會包含在指定路徑下找到的任何資產，以及應用程式執行個體的appAssetPath屬性所參考的任何資產。

* ***型別 — 字串***  — 應用程式資產

* ***路徑&#x200B;**-**字串***  — 應用程式例項下儲存應用程式資產之位置的路徑

**mobileappoffers** 已為「個人化」使用案例引入新的內容同步處理常式，以便呈現目標內容。 「mobileappoffers」處理常式會知道如何呈現內容作者所建立的相關目標選件。 mobileappoffers處理常式會擴充抽象頁面更新處理常式，因此許多屬性都類似。 mobileappoffers處理常式的詳細資訊有下列屬性。

mobileappsoffers處理常式會擴充mobileappspages處理常式，並新增下列屬性：

* ***locationRoot — 字串***  — 指定行動應用程式的位置
* ***includePageTypes — 字串***  — 預設支援cq/personalization/components/teaserpage和cq/personalization/components/offerproxy
* ***選擇器 — 字串***  — 應設為tandt
* ***路徑 — 字串*** — 行銷活動品牌的路徑

**mobileappconfig** mobileappconfig內容同步處理常式可將JSON資料插入MobileAppsConfig.json。 若要註冊提供者類別，開發人員會在提供者清單中新增其MobileAppsInfoProvider類別。 處理常式會對MobileAppsInfoProviders清單進行反複運算，並允許提供者將資料插入產生的json檔案中。 此處理常式支援的屬性清單為：

* ***路徑&#x200B;**-**字串***  — 具有page-type=app-instance或擴充/libs/mobileapps/core/components/instance之RT的應用程式執行個體節點的路徑
* ***提供者 — 字串*** `[]`  — 完整限定的MobileAppsInfoProviders清單
* ***targetRootDirectory — 字串***  — 將MobileAppsConfig.json檔案寫入的目錄。
* **fileName — 字串**  — 要將JSON寫入的檔案選擇性名稱，預設為MobileAppsConfig.json

可能有多個mobileappconfig處理常式分別設定為一組寫入不同JSON檔案的唯一提供者。

### 測試內容同步處理常式 {#testing-content-sync-handlers}

**檢查完整性的步驟** 清除快取

* 清除快取
* 執行您的處理常式（已更新快取）
* 再次執行您的處理常式（不應更新快取）

**偵錯步驟**

* 執行您的設定
* 在裝置上匯出設定或檢閱
* 如果演算失敗，則檢查是否遺失 *樣式/資產/程式庫* 或檢查是否有錯誤的路徑 *樣式/資產/程式庫*

**記錄** 透過封裝上的OSGI記錄器設定啟用ContentSync偵錯記錄 `com.day.cq.contentsync` 這可讓您追蹤哪些處理常式已執行，以及它們是否更新快取並回報更新快取。

## 其他資源 {#additional-resources}

若要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise製作](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>若要開始使用AEM Mobile應用程式開發，請按一下 [此處](/help/mobile/getting-started-aem-mobile.md).
