---
title: 為行動裝置建立網站
seo-title: Creating Sites for Mobile Devices
description: 建立行動網站與建立標準網站類似，因為它也涉及建立範本和元件
seo-description: Creating a mobile site is similar to creating a standard site as it also involves creating templates and components
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3840'
ht-degree: 0%

---

# 為行動裝置建立網站{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

建立行動網站與建立標準網站類似，因為它也涉及建立範本和元件。 如需建立範本和元件的詳細資訊，請參閱下列頁面： [範本](/help/sites-developing/templates.md), [元件](/help/sites-developing/components.md) 和 [開始開發AEM Sites](/help/sites-developing/getting-started.md). 主要差異在於在網站內啟用AEM內建的行動功能。 這需透過建立仰賴行動頁面元件的範本來達成。

您也應考慮使用 [回應式設計](/help/sites-developing/responsive.md)，建立可因應多種螢幕大小的單一網站。

若要開始使用，請查看 **We.Retail行動示範網站** 可在AEM中使用。

若要建立行動網站，請繼續進行：

1. 建立頁面元件：

   * 設定 `sling:resourceSuperType` 屬性 `wcm/mobile/components/page`
如此一來，元件便需仰賴行動頁面元件。

   * 建立 `body.jsp` 以及專案特定邏輯。

1. 建立頁面範本：

   * 設定 `sling:resourceType` 屬性至新建立的頁面元件。
   * 設定 `allowedPaths` 屬性。

1. 建立網站的設計頁面。
1. 建立下方的網站根頁面 `/content` 節點：

   * 設定 `cq:allowedTemplates` 屬性。
   * 設定 `cq:designPath` 屬性。

1. 在網站根頁面的頁面屬性中，於 **行動** 標籤。
1. 使用新範本建立網站頁面。

行動頁面元件( `/libs/wcm/mobile/components/page`):

* 新增 **行動** 頁簽到「頁面屬性」對話框。
* 透過 `head.jsp`，則會從請求中擷取目前的行動裝置群組，如果找到裝置群組，則會使用群組的 `drawHead()` 包括設備組的關聯模擬器init元件（僅在作者模式中）和設備組的呈現CSS的方法。

>[!NOTE]
>
>行動網站的根頁面必須位於節點階層的第1層，並建議位於/content節點下方。

## 使用多網站管理員建立行動網站 {#creating-a-mobile-site-with-the-multi-site-manager}

使用Multi Site Manager(MSM)從標準網站建立行動即時副本。 標準網站會自動轉換為行動網站：行動網站具有行動網站的所有功能（例如在模擬器內進行版本），並可與標準網站同步管理。 請參閱區段 [為不同管道建立即時副本](/help/sites-administering/msm.md) （在「多站點管理器」頁中）。

## 伺服器端行動API {#server-side-mobile-api}

包含行動類別的Java套件包括：

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  — 定義MobileConstants。
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html)  — 定義Device、DeviceGroup和DeviceGroupList。
* [com.day.cq.wcm.mobile.api.device.capability](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  — 定義DeviceCapability。
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html)  — 定義WurflQueryEngine
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html)  — 定義MobileUtil，它提供圍繞WCM Mobile運行的各種實用程式方法。

### 行動元件 {#mobile-components}

此 **We.Retail行動示範網站** 使用下列位於下方的行動元件 `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>名稱</td>
   <td>群組</td>
   <td>特徵</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>隱藏</td>
   <td> — 頁尾</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>行動</td>
   <td> — 根據影像基礎元件<br />  — 如果設備可以，則呈現影像<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>行動</td>
   <td> — 根據list foundation元件<br /> - listitem_teaser.jsp如果設備可用，則會呈現影像<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>隱藏</td>
   <td> — 以標誌基礎元件為基礎<br />  — 如果設備可以，則呈現影像<br /> </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>行動</td>
   <td><p> — 類似於參考基礎元件</p> <p> — 將textimage元件對應至mobiletextimage 1，並將影像元件對應至mobileimage 1</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>行動</td>
   <td> — 根據文字時間基礎元件<br />  — 如果設備可以，則呈現影像</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>隱藏</td>
   <td><p> — 根據topnav foundation元件</p> <p> — 僅呈現文本</p> </td>
  </tr>
 </tbody>
</table>

#### 建立行動元件 {#creating-a-mobile-component}

AEM行動架構可開發對發出請求的裝置敏感的元件。 下列程式碼範例說明如何在元件jsp中使用AEM行動API，尤其是如何：

* 從請求中取得裝置：
   `Device device = slingRequest.adaptTo(Device.class);`

* 獲取設備組：
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* 獲取設備組功能：
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* 從WURFL資料庫獲取設備屬性（原始功能鍵/值）:
   `Map<String,String> deviceAttributes = device.getAttributes();`

* 獲取設備用戶代理：
   `String userAgent = device.getUserAgent();`

* 從目前頁面取得裝置群組清單（由作者指派給網站的裝置群組）:
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* 檢查設備組是否支援映像
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
或

...   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>用jsp `slingRequest` 可透過 `<sling:defineObjects>` 標籤和 `currentPage` 通過 `<cq:defineObjects>` 標籤。

### 模擬器 {#emulators}

以模擬器為基礎的製作功能可讓作者建立適用於行動用戶端的內容頁面。 行動內容製作遵循就地WYSIWYG編輯的相同原則。 為了讓作者對行動裝置上的頁面外觀有感覺，使用裝置模擬器來編輯行動內容頁面。

行動裝置模擬器以一般模擬器架構為基礎。 如需更多詳細資訊，請參閱 [模擬器](/help/sites-developing/emulators.md) 頁面。

裝置模擬器會在頁面上顯示行動裝置，而通常的編輯（parsys、元件）則發生在裝置的畫面中。 設備模擬器取決於為站點配置的設備組。 可以為設備組分配多個模擬器。 然後，內容頁面上會提供所有模擬器。 預設情況下，將顯示分配給該站點的第一個設備組的第一個模擬器。 模擬器可透過頁面頂端的模擬器輪播或透過Sidekick的編輯按鈕進行切換。

**建立模擬器**

若要建立模擬器，請參閱 [建立自訂行動模擬器](/help/sites-developing/emulators.md) 部分。

**移動模擬器的主要特性**

* 設備組由以下多個模擬器之一組成：設備組配置頁，例如/etc/mobile/groups/touch，包含 `emulators` 屬性下方 `jcr:content` 節點。
注意：雖然同一模擬器可能屬於多個設備組，但這沒什麼意義。

* 通過設備組的配置對話框， `emulators` 屬性是使用所需模擬器的路徑設定。 例如： `/libs/wcm/mobile/components/emulators/iPhone4`.

* 模擬器元件(例如 `/libs/wcm/mobile/components/emulators/iPhone4`)擴充基本行動模擬器元件( `/libs/wcm/mobile/components/emulators/base`)。

* 配置設備組時，可選擇擴展基本移動模擬器的每個元件。 因此，可輕鬆建立或擴展自定義模擬器。
* 在編輯模式下的請求時，模擬器實作會用於呈現頁面。
* 當頁面的範本仰賴行動頁面元件時，模擬器功能會自動整合至頁面(透過 `head.jsp` )。

### 裝置群組 {#device-groups}

行動裝置群組會根據裝置功能提供行動裝置的分段。 裝置群組提供在製作執行個體上以模擬器為基礎製作以及在發佈執行個體上正確呈現內容所需的資訊：一旦作者將內容新增至行動頁面並發佈後，即可在發佈例項上請求頁面。 在那裡，內容頁面不是模擬器編輯視圖，而是使用其中一個配置的設備組呈現。 設備組的選擇基於 [行動裝置偵測](#devicedetection). 然後，相符的裝置群組會提供必要的樣式資訊。

裝置群組定義為下方的內容頁面 `/etc/mobile/devices` 並使用 **行動裝置群組** 範本。 裝置群組範本可作為內容頁面形式之裝置群組定義的設定範本。 其主要特點是：

* 位置: `/libs/wcm/mobile/templates/devicegroup`
* 允許的路徑： `/etc/mobile/groups/*`
* 頁面元件： `wcm/mobile/components/devicegroup`

#### 為網站指派裝置群組 {#assigning-device-groups-to-your-site}

建立行動網站時，您需要將裝置群組指派給您的網站。 AEM會根據裝置的HTML和JavaScript轉譯功能，提供三個裝置群組：

* **功能** 手機，適用於支援基本HTML但不支援影像和JavaScript的功能裝置，如Sony Ericsson W800。
* **智慧** 手機，適用於支援基本HTML和影像的Blackberry等裝置，但不支援JavaScript。

* **觸控** 手機，適用於iPad等完全支援HTML、影像、JavaScript和裝置輪換的裝置。

因為模擬器可以與設備組關聯(請參閱 [建立裝置群組](#creating-a-device-group))，將裝置群組指派給網站，可讓作者在與裝置群組相關聯的模擬器之間進行選取，以編輯頁面。

若要將裝置群組指派給您的網站：

1. 在您的瀏覽器中，前往 **網站管理員** 控制台。
1. 在下方開啟行動網站的根頁面 **網站**.
1. 開啟頁面屬性。
1. 選取 **行動** 標籤：

   * 定義裝置群組。
   * 按一下&#x200B;**「確定」**。

>[!NOTE]
>
>為網站定義裝置群組後，網站的所有頁面都會繼承這些裝置群組。

#### 裝置群組篩選器 {#device-group-filters}

設備組篩選器定義基於功能的標準，以確定設備是否屬於該組。 建立裝置群組時，您可以選取用於評估裝置的篩選器。

在AEM收到來自裝置的HTTP要求時，與群組相關聯的每個篩選器都會將裝置功能與特定條件進行比較。 當裝置具備篩選器所需的所有功能時，即視為屬於群組。 功能從WURFL™資料庫中檢索。

裝置群組可使用零個或多個篩選器來偵測功能。 此外，篩選器可與多個裝置群組搭配使用。 AEM提供預設篩選條件，可判斷裝置是否具備為群組選取的功能：

* CSS
* JPG和PNG影像
* JavaScript
* 裝置旋轉

如果設備組未使用篩選器，則為組配置的選定功能是設備所需的唯一功能。

如需詳細資訊，請參閱 [建立裝置群組篩選器](/help/sites-developing/groupfilters.md).

#### 建立裝置群組 {#creating-a-device-group}

當AEM安裝的群組不符合您的需求時，建立裝置群組。

1. 在您的瀏覽器中，前往 **工具** 控制台。
1. 在下方建立新頁面 **工具** > **行動** > **裝置群組**. 在 **建立頁面** 對話框：

   * As **標題** 輸入 `Special Phones`.

   * As **名稱** 輸入 `special`.

   * 選取 **行動裝置群組範本**.
   * 按一下&#x200B;**建立**。

1. 在CRXDE中，新增 **static.css** 檔案，其中包含下方設備組的樣式 `/etc/mobile/groups/special` 節點。

1. 開啟 **特殊電話** 頁面。
1. 若要設定裝置群組，請按一下 **編輯** 按鈕 **設定**.
在 **一般** 標籤：

   * **標題**:行動裝置群組的名稱。
   * **說明**:群組的說明。
   * **User-Agent**:與裝置相符的使用者代理字串。 此為選用項目，可以是規則運算式。 範例: `BlackBerryZ10`
   * **功能**:定義群組是否可以處理影像、CSS、JavaScript或裝置旋轉。
   * **最小螢幕寬度**&#x200B;和&#x200B;**高度**
   * **禁用模擬器**:在內容編輯期間啟用/停用模擬器。

   在 **模擬器** 標籤：

   * **模擬器**:選擇分配給此設備組的模擬器。

   在 **篩選器** 標籤：

   * 若要新增篩選器，請按一下「新增項目」並從下拉式清單中選取篩選器。
   * 系統會依篩選器的顯示順序來評估篩選器。 當裝置不符合篩選器的條件時，系統不會評估清單上的後續篩選器。



1. 按一下「確定」。

行動裝置群組設定對話方塊的外觀如下：

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### 每個裝置群組的自訂CSS {#custom-css-per-device-group}

如前所述，可以將自定義CSS與設備組頁建立關聯，這與設計頁的CSS非常相似。此CSS用於影響設備組特定的頁面內容在作者和發佈時的呈現。然後，將自動包括此CSS:

* 在製作例項的頁面中，針對此裝置群組使用的每個模擬器。
* 在發佈例項的頁面中，如果請求的使用者代理與此特定裝置群組中的行動裝置相符，則顯示該請求。

## 伺服器端裝置偵測 {#server-side-device-detection}

使用篩選器和裝置規格庫，判斷執行HTTP要求的裝置功能。

### 開發裝置群組篩選器 {#develop-device-group-filters}

建立設備組篩選器以定義一組設備功能需求。 建立您所需的篩選器，以鎖定所需的裝置功能群組。

設計您的篩選器，以便使用篩選器的組合來定義功能群組。 通常，不同裝置群組的功能會有重疊之處。 因此，您可能會對多個裝置群組定義使用某些篩選器。

建立篩選器後，即可在群組設定中使用它。

如需詳細資訊，請前往 [建立裝置群組篩選器](/help/sites-developing/groupfilters.md).

### 使用WURFL™資料庫 {#using-the-wurfl-database}

AEM使用截斷版本的 [沃夫爾](https://wurfl.sourceforge.net/)™資料庫，根據裝置的使用者代理來查詢裝置功能，例如螢幕解析度或javascript支援。

WURFL™資料庫的XML代碼表示為以下節點 `/var/mobile/devicespecs` 通過解析 `wurfl.xml`檔案位置 `/libs/wcm/mobile/devicespecs/wurfl.xml.` 對節點的擴增，是在 `cq-mobile-core` 套件組合已啟動。

設備功能以節點屬性的形式儲存，節點表示設備型號。 您可以使用查詢來檢索設備或用戶代理的功能。

隨著WURFL™資料庫的不斷發展，您可能需要定制或替換它。 要更新移動設備資料庫，您有以下選項：

* 如果您有允許此用途的授權，請將檔案取代為最新版本。 請參閱安裝其他WURFL資料庫。
* 使用AEM中可用的版本，並設定符合您的使用者代理字串且指向現有WURFL™裝置的regexp。 請參閱 [新增以regexp為基礎的使用者代理比對](#adding-a-regexp-based-user-agent-matching).

#### 測試用戶代理到WURFL™功能的映射 {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

當裝置存取您的行動網站時，AEM會偵測到裝置，並根據其功能將其對應至裝置群組，並傳送與裝置群組對應之頁面檢視。 相符的裝置群組提供必要的樣式資訊。 可在「行動使用者代理測試」頁面上測試對應：

`https://localhost:4502/etc/mobile/useragent-test.html`

#### 安裝不同的WURFL™資料庫 {#installing-a-different-wurfl-database}

隨AEM安裝的截斷WURFL™資料庫是2011年8月30日之前的版本。 如果您的WURFL版本在2011年8月30日之後發行，請確保您的使用符合您的許可證。

安裝WURFL™資料庫：

1. 在CRXDE Lite中，建立下列資料夾： `/apps/wcm/mobile/devicespecs`
1. 將WURFL™檔案複製到資料夾。
1. 將檔案重新命名為 `wurfl.xml`.

AEM會自動解析 `wurfl.xml` 檔案並更新以下節點 `/var/mobile/devicespecs`.

>[!NOTE]
>
>啟用完整的WURFL™資料庫時，可能需要幾分鐘的時間進行解析和激活。 您可以監視記錄以取得進度資訊。

#### 新增以regexp為基礎的使用者代理比對 {#adding-a-regexp-based-user-agent-matching}

將user-agent添加為/apps/wcm/mobile/devicespecs/wurfl/regexp下的規則表達式，以指向現有的WURFL™設備類型。

1. 在 **CRXDE Lite**，在/apps/wcm/mobile/devicespecs/regexp下建立節點，例如apple_ipad_ver1。
1. 將下列屬性新增至節點：

   * **regexp**:定義使用者代理的規則運算式，例如：.&#42;莫茲拉。&#42;iPad.&#42;AppleWebKit。&#42;Safari。&#42;
   * **deviceId**:在wurfl.xml中定義的裝置ID，例如：apple_ipad_ver1

上述設定會使User-Agent與提供的規則運算式相符的裝置對應至apple_ipad_ver1 WURFL™裝置ID（若存在）。

## 用戶端裝置偵測 {#client-side-device-detection}

本節說明如何使用AEM的裝置用戶端偵測，以最佳化頁面呈現或為用戶端提供替代的網站版本。

AEM支援以下為基礎的裝置用戶端偵測： `BrowserMap`. `BrowserMap` 在AEM中以用戶端程式庫的形式提供 `/etc/clientlibs/browsermap`.

`BrowserMap` 提供三種策略，您可以用來為客戶提供替代網站，其採用順序如下：

1. [替代連結](#providing-alternate-links)
1. [設備組特定URL](#definingdevicegroupspecificurl)
1. [選取器型URL](#defining-selector-based-urls)

>[!NOTE]
>
>如需用戶端程式庫整合的詳細資訊，請參閱 [使用用戶端HTML程式庫](/help/sites-developing/clientlibs.md) 區段。

### 提供替代連結 {#providing-alternate-links}

此 `PageVariantsProvider` OSGi服務能夠為屬於同一系列的網站產生替代連結。 為了配置要由服務考慮的站點， `cq:siteVariant` 節點必須新增至 `jcr:content` 節點。

此 `cq:siteVariant` 節點必須具備下列屬性：

* `cq:childNodesMapTo`  — 確定子節點將映射到的連結元素的屬性；建議您以這樣的方式組織網站的內容，讓根節點的子代代表全域網站語言變體的根(例如， `/content/mysite/en`, `/content/mysite/de`)，在此情況下， `cq:childNodesMapTo` 應該是 `hreflang`;
* `cq:variantDomain`  — 表示什麼 `Externalizer` 網域將用來產生頁面變體絕對URL;若未設定此值，則會使用相對連結產生頁面變體；
* `cq:variantFamily`  — 指明本站點屬於哪個網站系列；同一網站的多個特定裝置表示應屬於同一家族；
* `media`  — 儲存連結元素的媒體屬性值；建議使用 `BrowserMap` 註冊 `DeviceGroups`，因此 `BrowserMap` 程式庫會自動將用戶端轉送至網站的正確變體。

#### PageVariantsProvider和Externalizer {#pagevariantsprovider-and-externalizer}

當 `cq:variantDomain` 屬性a `cq:siteVariant` 節點不為空， `PageVariantsProvider` 服務會使用此值產生絕對連結，作為 `Externalizer` 服務。 請務必設定 `Externalizer` 服務，以反映您的設定。

>[!NOTE]
>
>使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議的實務。

### 定義裝置群組特定URL {#defining-a-device-group-specific-url}

如果您不想使用替代連結，可以為每個連結設定全域URL `DeviceGroup`. 建議您建立內嵌的專屬用戶端程式庫 `browsermap.standard` 用戶端程式庫，但會重新定義裝置群組。

BrowserMap的設計方式，是透過建立新裝置群組並將同名裝置群組新增至 `BrowserMap` 物件。

>[!NOTE]
>
>欲知更多詳情，請閱讀 [自訂的BrowserMap](#creatingacustomisedbrowsermap) 區段。

### 定義選取器型URL {#defining-selector-based-urls}

如果沒有採用任何先前的機制來指示 `BrowserMap`，則使用名稱的選取器 `DeviceGroups` 將新增至 `URL`s，在此情況下，您應提供將處理請求的專屬servlet。

例如裝置瀏覽 `www.example.com/index.html` 已識別為 `smartphone` 由BrowserMap轉送至 `www.example.com/index.smartphone.html.`

### 在您的頁面上使用BrowserMap {#using-browsermap-on-your-pages}

若要在頁面中使用標準的BrowserMap用戶端程式庫，您必須包含 `/libs/wcm/core/browsermap/browsermap.jsp` 檔案使用 `cq:include`標籤 `head` 區段。

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

除了新增 `BrowserMap` 您的 `JSP` 檔案，您也必須新增 `cq:deviceIdentificationMode` 字串屬性設為 `client-side` 到 `jcr:content` 節點。

### 覆寫BrowserMap的預設行為 {#overriding-browsermap-s-default-behaviour}

如果您想要自訂 `BrowserMap`  — 通過覆蓋 `DeviceGroups` 或添加更多探測器 — 則應建立自己的客戶端庫，在其中嵌入 `browsermap.standard`用戶端程式庫。

此外，您必須手動呼叫 `BrowserMap.forwardRequest()` 方法 `JavaScript` 程式碼。

>[!NOTE]
>
>如需用戶端程式庫整合的詳細資訊，請參閱 [使用用戶端HTML程式庫](/help/sites-developing/clientlibs.md) 區段。

建立自定義後 `BrowserMap` 用戶端程式庫，建議使用下列方法：

1. 建立 `browsermap.jsp` 檔案

   ```xml
   <%@include file="/libs/foundation/global.jsp" %>
   <%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
   <%@ page import="
       com.day.cq.wcm.api.variants.PageVariant,
       com.day.cq.wcm.api.variants.PageVariantsProvider,
       com.day.cq.wcm.api.devicedetection.DeviceIdentificationMode,
       com.day.cq.wcm.api.WCMMode"
   %>
   <%
       final PageVariantsProvider p = sling.getService(PageVariantsProvider.class);
       if(p == null) {
           throw new IllegalStateException("Missing PageVariantsProvider service");
       }
       for(PageVariant v : p.getVariants(currentPage, slingRequest)) {
           final String curVar = v.getAttributes().get("data-current-variant");
           String media = v.getAttributes().get("media");
           if (media != null) {
               media = media.replaceAll(" ", "");
           }
   %>
       <link
           rel="alternate"
           data-cq-role="site.variant"
           title="<%= xssAPI.encodeForHTMLAttr(v.getTitle()) %>"
           hreflang="<%= xssAPI.encodeForHTMLAttr(v.getAttributes().get("hreflang")) %>"
           media="<%= xssAPI.encodeForHTMLAttr(media) %>"
           href="<%= xssAPI.getValidHref(v.getURL()) %>"
           <% if(curVar != null) { %> data-current-variant="<%= curVar %>"<% } %>
       />
   <%
       }
       Boolean browserMapEnabled = true;
       final DeviceIdentificationMode dim = sling.getService(DeviceIdentificationMode.class);
       String[] selectors  = slingRequest.getRequestPathInfo().getSelectors();
       boolean isPortletRequest = false;
       for (int i = 0; i < selectors.length; i++) {
           if ("portlet".equals(selectors[i])) {
               isPortletRequest = true;
               break;
           }
       }
       if (isPortletRequest) {
           log.debug("Request was made by a portlet container - BrowserMap will not be embedded");
       } else {
           final WCMMode wcmMode = WCMMode.fromRequest(slingRequest);
           boolean shouldIncludeClientLib = false;
           if (WCMMode.EDIT != wcmMode && WCMMode.PREVIEW != wcmMode && WCMMode.DESIGN != wcmMode) {
               if (dim != null) {
                   final String mode = dim.getDeviceIdentificationModeForPage(currentPage);
                   shouldIncludeClientLib = DeviceIdentificationMode.CLIENT_SIDE.equals(mode);
                   if (shouldIncludeClientLib) {
                       browserMapEnabled = (Boolean) request.getAttribute("browsermap.enabled");
                       if (browserMapEnabled == null) {
                           browserMapEnabled = true;
                       }
                   }
               }
           }
   %>
           <c:if test="<%= !browserMapEnabled %>">
               <meta name="browsermap.enabled" content="false">
           </c:if>
           <c:if test="<%= shouldIncludeClientLib %>">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
               <cq:includeClientLib categories="browsermap.custom"/>
           </c:if>
   <%
       }
   %>
   ```

1. 納入 `broswermap.jsp` 檔案。

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 從特定頁面排除BrowserMap {#excluding-browsermap-from-certain-pages}

如果您想要從您不需要用戶端偵測的部分頁面中排除BrowserMap程式庫，可以新增請求屬性：

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

這會使 `/libs/wcm/core/browsermap/browsermap.jsp` 指令碼，將中繼標籤新增至要建立 `BrowserMap` 不執行任何檢測：

```xml
<meta name="browsermap.enabled" content="false">
```

### 測試網站的特定版本 {#testing-a-specific-version-of-a-web-site}

通常，BrowserMap指令碼會一律將訪客重新導向至最適合的網站版本，通常會視需要將訪客重新導向至案頭或行動網站。

您可以強制任何請求的裝置，借由新增 `device` 參數。 下列URL會轉譯Geometrixx Outdoors網站的行動版本。

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>此 `wcmmode` 參數設為 `disabled` 以模擬發佈例項的行為。

覆蓋的裝置值會儲存在Cookie中，以便您可以瀏覽您的網站，而不需新增 `device` 參數 `URL`.

因此，您需要呼叫相同的 `URL` 和 `device` 設為 `browser` 以便回到案頭版網站。

>[!NOTE]
>
>BrowserMap會將覆蓋的裝置值儲存在名為的Cookie中 `BMAP_device`. 刪除此Cookie將可確保CQ會根據您目前的裝置（例如案頭或行動裝置）提供適當版本的網站。

## 行動請求處理 {#mobile-request-processing}

AEM會依照下列方式處理由屬於觸控裝置群組的行動裝置發出的請求：

1. iPad會傳送要求至AEM發佈例項，例如 `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM會判斷所請求頁面的網站是否為行動網站（透過檢查第一層頁面是否為行動網站） `/content/geometrixx_mobile` 延伸行動頁面元件)。 如果是：
1. AEM會根據請求標題中的使用者代理來查閱裝置功能。
1. AEM會將裝置功能對應至裝置群組並設定 `touch` 作為裝置群組選取器。
1. AEM會將請求重新導向至 `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM會將回應傳送至iPad:

   * `products.touch.html` 都是平時的，平易近人。
   * 演算元件使用選取器來調整呈現方式。
   * AEM會自動將行動選擇器新增至頁面中的所有內部連結。

### 統計資料 {#statistics}

您可以取得行動裝置向AEM伺服器提出之請求數的統計資料。 可以劃分請求數：

* 每個設備組和設備
* 每年，月和日

要查看統計資訊，請執行以下操作：

1. 前往 **工具** 控制台。
1. 開啟 **設備統計資訊** 頁面下方 **工具** > **行動**.
1. 按一下連結可檢視特定年份、月份或日的統計資料。

此 **統計** 頁面外觀如下：

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>此 **統計** 頁面是在行動裝置首次存取AEM並偵測到時建立。 在此之前，它無法使用。

如果需要在統計資訊中生成條目，可以按如下方式繼續：

1. 使用行動裝置或模擬器(例如Firefox上的https://chrispederick.com/work/user-agent-switcher/)。
1. 停用製作模式，在製作例項上要求行動頁面，例如：
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

此 **統計** 頁面現已可用。

### 支援「傳送連結給朋友」連結的頁面快取 {#supporting-page-caching-for-send-link-to-a-friend-links}

Dispatcher通常可使用行動頁面，因為為裝置群組轉譯的頁面在頁面URL中可由裝置群組選取器加以區分，例如 `/content/mobilepage.touch.html`. 系統不會快取對沒有選取器的行動頁面的要求，在此情況下，裝置偵測會運作，最後重新導向至相符的裝置群組（或就此而言「不相符」）。 連結重寫器會處理呈現有裝置群組選擇器的行動頁面，該連結重寫器會重新寫入頁面內的所有連結以同時包含裝置群組選擇器，以防止對已合格頁面上的每次點按重新執行裝置偵測。

因此，您可能會遇到下列情況：

使用者Alice會重新導向至 `coolpage.feature.html`，並將該URL傳送給朋友Bob，該朋友Bob會透過位於 `touch` 設備組。

若 `coolpage.feature.html` 是從前端快取提供，AEM將無法分析請求，以找出行動選擇器與新的使用者代理不符，而Bob會獲得錯誤的表示。

若要解決此問題，您可以在頁面上加入簡單的選取UI，讓使用者可以覆寫AEM選取的裝置群組。 在上述範例中，頁面上的連結（或圖示）可讓使用者切換至 `coolpage.touch.html` 如果他認為他的設備足夠好。
