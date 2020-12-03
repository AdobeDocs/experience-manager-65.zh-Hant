---
title: 建立行動裝置的網站
seo-title: 建立行動裝置的網站
description: 建立行動網站與建立標準網站類似，因為它也涉及建立範本和元件
seo-description: 建立行動網站與建立標準網站類似，因為它也涉及建立範本和元件
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '3864'
ht-degree: 0%

---


# 建立行動裝置的網站{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

建立行動網站與建立標準網站類似，因為它也涉及建立範本和元件。 如需建立範本和元件的詳細資訊，請參閱下列頁面：[範本](/help/sites-developing/templates.md)、[元件](/help/sites-developing/components.md)和[開始開發AEM網站](/help/sites-developing/getting-started.md)。 主要差異在於啟用網站內的AEM內建行動功能。 建立依賴行動頁面元件的範本即可完成。

您也應考慮使用[回應式設計](/help/sites-developing/responsive.md)，建立可容納多種螢幕大小的單一網站。

若要開始使用，您可以檢視AEM中提供的&#x200B;**We.Retail Mobile展示網站**。

若要建立行動網站，請依照下列步驟進行：

1. 建立頁面元件：

   * 將`sling:resourceSuperType`屬性設為`wcm/mobile/components/page`
這樣，元件就依賴於行動頁面元件。

   * 使用專案特定邏輯建立`body.jsp`。

1. 建立頁面範本：

   * 將`sling:resourceType`屬性設為新建立的頁面元件。
   * 設定`allowedPaths`屬性。

1. 建立網站的設計頁面。
1. 在`/content`節點下建立站點根頁：

   * 設定`cq:allowedTemplates`屬性。
   * 設定`cq:designPath`屬性。

1. 在站點根頁面的頁面屬性中，在&#x200B;**Mobile**&#x200B;標籤中設定設備組。
1. 使用新範本建立網站頁面。

行動頁面元件(`/libs/wcm/mobile/components/page`):

* 將&#x200B;**Mobile**&#x200B;標籤新增至頁面屬性對話方塊。
* 透過其`head.jsp`，它會從請求中擷取目前的行動裝置群組，如果找到裝置群組，則會使用該群組的`drawHead()`方法來包含裝置群組的相關模擬器init元件（僅在作者模式中）和裝置群組的轉換CSS。

>[!NOTE]
>
>行動網站的根頁面必須位於節點階層的第1層，並建議位於/content節點下方。

## 使用多站點管理器{#creating-a-mobile-site-with-the-multi-site-manager}建立移動站點

使用Multi Site Manager(MSM)從標準網站建立行動即時副本。 標準網站會自動轉換成行動網站：行動網站具備行動網站的所有功能（例如在模擬器中編輯），並可與標準網站同步管理。 請參閱「多站點管理器」頁中的「為不同通道建立即時副本」一節。[](/help/sites-administering/msm.md)

## 伺服器端行動API {#server-side-mobile-api}

包含移動類的Java包包括：

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) -定義MobileConstants。
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) -定義裝置、裝置群組和裝置群組清單。
* [com.day.cq.wcm.mobile.api.device.capability](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) -定義DeviceCapability。
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - defines WurflQueryEngine。
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) -定義MobileUtil，它提供以WCM Mobile為中心的各種公用程式方法。

### 行動元件{#mobile-components}

**We.Retail Mobile展示網站**&#x200B;使用位於`/libs/foundation/components`下方的下列行動元件：

<table>
 <tbody>
  <tr>
   <td>名稱</td>
   <td>群組</td>
   <td>特性</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>隱藏</td>
   <td>-頁尾</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>行動</td>
   <td>-基於影像基礎元件<br /> —— 如果設備能夠<br />，則渲染影像 </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>行動</td>
   <td>-基於清單基礎元件<br /> - listitem_teaser.jsp，如果設備能夠<br />，則渲染影像 </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>隱藏</td>
   <td>-基於標誌基礎元件<br /> —— 如果設備可以<br />轉換影像 </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>行動</td>
   <td><p>-類似於參考基礎元件</p> <p>-將textimage元件對應至mobiletextimage 1，並將影像元件對應至mobileimage 1</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>行動</td>
   <td>-根據textimage基礎元件<br /> —— 如果設備可以，則渲染影像</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>隱藏</td>
   <td><p>-根據topnav基礎元件</p> <p>-僅轉換文字</p> </td>
  </tr>
 </tbody>
</table>

#### 建立移動元件{#creating-a-mobile-component}

AEM Mobile架構可讓您開發對發出請求的裝置敏感的元件。 下列程式碼範例說明如何在元件jsp中使用AEM Mobile API，尤其是如何：

* 從請求取得裝置：
   `Device device = slingRequest.adaptTo(Device.class);`

* 取得裝置群組：
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* 取得裝置群組功能：
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* 從WURFL資料庫取得裝置屬性（原始功能索引鍵／值）:
   `Map<String,String> deviceAttributes = device.getAttributes();`

* 取得裝置使用者代理：
   `String userAgent = device.getUserAgent();`

* 從目前頁面取得裝置群組清單（作者指派給網站的裝置群組）:
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* 檢查設備組是否支援映像
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
或

...   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>在jsp中，`slingRequest`可通過`<sling:defineObjects>`標籤使用，`currentPage`可通過`<cq:defineObjects>`標籤使用。

### 模擬器 {#emulators}

以模擬器為基礎的製作功能可讓作者建立適用於行動用戶端的內容頁面。 行動內容製作遵循與就地WYSIWYG編輯相同的原則。 為了讓作者在行動裝置上感知頁面外觀，使用裝置模擬器來編輯行動內容頁面。

行動裝置模擬器是以通用模擬器架構為基礎。 有關詳細資訊，請參閱[模擬器](/help/sites-developing/emulators.md)頁。

裝置模擬器會在頁面上顯示行動裝置，而通常的編輯（parsys、元件）則會在裝置的螢幕中進行。 設備模擬器取決於為站點配置的設備組。 可以為設備組分配多個模擬器。 然後，所有模擬器都可在內容頁面上使用。 預設情況下，將顯示分配給該站點的第一個設備組的第一個模擬器。 模擬器可以通過頁面頂部的模擬器轉盤切換，也可以通過Sidekick的編輯按鈕切換。

**建立模擬器**

要建立模擬器，請參閱通用模擬器頁中的[建立自定義移動模擬器](/help/sites-developing/emulators.md)部分。

**移動模擬器的主要特性**

* 設備組由多個模擬器之一組成：設備組配置頁，例如/etc/mobile/groups/touch，包含`jcr:content`節點下方的`emulators`屬性。
注意：雖然相同的模擬器可能屬於多個裝置群組，但是這並沒什麼意義。

* 通過設備組的配置對話框，`emulators`屬性將設定為所需模擬器的路徑。 例如：`/libs/wcm/mobile/components/emulators/iPhone4`。

* 模擬器元件(如`/libs/wcm/mobile/components/emulators/iPhone4`)擴充基本行動模擬器元件(`/libs/wcm/mobile/components/emulators/base`)。

* 在設定裝置群組時，每個擴充基本行動模擬器的元件都可供選擇。 因此，可輕鬆建立或擴充自訂模擬器。
* 在編輯模式下的請求時，會使用模擬器實作來呈現頁面。
* 當頁面的範本依賴於行動頁面元件時，模擬器功能會自動整合在頁面中（透過行動頁面元件的`head.jsp`）。

### 裝置群組 {#device-groups}

行動裝置群組根據裝置功能提供行動裝置的區段。 裝置群組提供在作者執行個體上進行模擬器製作以及在發佈執行個體上進行正確內容轉換所需的資訊：一旦作者將內容新增至行動頁面並發佈後，就可以在發佈例項上要求頁面。 內容頁面會使用其中一個已設定的裝置群組呈現，而非模擬器編輯檢視。 根據[移動設備檢測](#devicedetection)來選擇設備組。 然後，比對的裝置群組會提供必要的樣式資訊。

裝置群組定義為`/etc/mobile/devices`下方的內容頁面，並使用&#x200B;**行動裝置群組**&#x200B;範本。 裝置群組範本可當成內容頁面形式之裝置群組定義的設定範本。 其主要特點是：

* 位置: `/libs/wcm/mobile/templates/devicegroup`
* 允許的路徑：`/etc/mobile/groups/*`
* 頁面元件：`wcm/mobile/components/devicegroup`

#### 將設備組分配給您的站點{#assigning-device-groups-to-your-site}

當您建立行動網站時，需要將裝置群組指派給您的網站。 AEM根據裝置的HTML和JavaScript轉譯功能提供三個裝置群組：

* **功** 能手機，適用於功能裝置，例如Sony Ericsson W800，支援基本HTML，但不支援影像和JavaScript。
* **智慧** 型手機，適用於支援基本HTML和影像的Blackberry等裝置，但不支援JavaScript。

* **適用於** iPad等裝置的Touchphone，完全支援HTML、影像、JavaScript和裝置旋轉。

由於模擬器可以與設備組關聯（請參閱[建立設備組](#creating-a-device-group)一節），因此將設備組分配給站點可讓作者在與設備組關聯的模擬器之間進行選擇，以編輯頁。

若要將裝置群組指派給您的網站：

1. 在您的瀏覽器中，前往&#x200B;**網站管理**&#x200B;主控台。
1. 在&#x200B;**Websites**&#x200B;下方開啟行動網站的根頁面。
1. 開啟頁面屬性。
1. 選擇&#x200B;**Mobile**&#x200B;標籤：

   * 定義裝置群組。
   * 按一下&#x200B;**「確定」**。

>[!NOTE]
>
>為網站定義裝置群組後，網站的所有頁面都會繼承這些裝置群組。

#### 裝置群組篩選器 {#device-group-filters}

設備組過濾器定義基於功能的標準，以確定設備是否屬於該組。 當您建立裝置群組時，可以選取用於評估裝置的篩選器。

當AEM從裝置收到HTTP要求時，與群組相關聯的每個篩選器都會將裝置功能與特定條件進行比較。 當裝置具備篩選條件所需的所有功能時，即視為屬於群組。 功能是從WURFL™資料庫檢索的。

裝置群組可使用零個或多個篩選器來進行功能偵測。 此外，篩選器可與多個裝置群組搭配使用。 AEM提供預設篩選，可判斷裝置是否具備為群組選取的功能：

* CSS
* JPG和PNG影像
* JavaScript
* 裝置旋轉

如果設備組不使用過濾器，則為組配置的所選功能是設備所需的唯一功能。

如需詳細資訊，請參閱[建立裝置群組篩選器](/help/sites-developing/groupfilters.md)。

#### 建立設備組{#creating-a-device-group}

當AEM安裝的群組不符合您的需求時，請建立裝置群組。

1. 在瀏覽器中，轉至&#x200B;**工具**&#x200B;控制台。
1. 在&#x200B;**工具** > **行動** > **裝置群組**&#x200B;下建立新頁面。 在&#x200B;**建立頁面**&#x200B;對話方塊中：

   * 在&#x200B;**Title**&#x200B;中輸入`Special Phones`。

   * 在&#x200B;**名稱**&#x200B;中輸入`special`。

   * 選擇&#x200B;**行動裝置群組範本**。
   * 按一下&#x200B;**建立**。

1. 在CRXDE中，添加一個&#x200B;**static.css**&#x200B;檔案，該檔案包含`/etc/mobile/groups/special`節點下設備組的樣式。

1. 開啟&#x200B;**特殊電話**&#x200B;頁面。
1. 要配置設備組，請按一下&#x200B;**設定**&#x200B;旁邊的&#x200B;**編輯**按鈕。
在**General**&#x200B;標籤上：

   * **標題**:行動裝置群組的名稱。
   * **說明**:群組的說明。
   * **用戶代理**:與裝置相符的使用者代理字串。它是可選的，可以是規則運算式。 範例: `BlackBerryZ10`
   * **功能**:定義群組是否可處理影像、CSS、JavaScript或裝置旋轉。
   * **最小螢幕寬度****和高度**
   * **禁用模擬器**:可在內容編輯期間啟用／停用模擬器。

   在&#x200B;**模擬器**&#x200B;標籤上：

   * **模擬器**:選擇分配給此設備組的模擬器。

   在&#x200B;**Filters**&#x200B;標籤上：

   * 若要新增篩選，請按一下「新增項目」並從下拉式清單中選取篩選。
   * 篩選器會依其顯示順序進行評估。 當裝置不符合篩選條件時，不會評估清單上的後續篩選。



1. 按一下「確定」。

行動裝置群組設定對話方塊的外觀如下：

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### 每個裝置群組的自訂CSS {#custom-css-per-device-group}

如前所述，可以將自訂CSS與裝置群組頁面建立關聯，就像設計頁面的CSS。此CSS可用來影響裝置群組對頁面內容在作者和發佈時的呈現。此CSS會自動包含：

* 在此設備組使用的每個模擬器的作者實例頁面上。
* 在發佈例項的頁面中，如果請求的使用者代理與此特定裝置群組中的行動裝置相符，請在此頁面中。

## 伺服器端設備檢測{#server-side-device-detection}

使用篩選器和裝置規格庫來判斷執行HTTP要求之裝置的功能。

### 開發設備組過濾器{#develop-device-group-filters}

建立裝置群組篩選以定義一組裝置功能需求。 根據您的需求建立任意數量的篩選器，以鎖定所需的裝置功能群組。

設計您的篩選器，以便使用其組合來定義功能群組。 通常，不同裝置群組的功能會重疊。 因此，您可能會針對多個裝置群組定義使用某些篩選器。

建立篩選器後，即可在群組設定中使用。

有關資訊，請轉至[建立設備組過濾器](/help/sites-developing/groupfilters.md)。

### 使用WURFL™資料庫{#using-the-wurfl-database}

AEM使用截斷版本的[WURFL](https://wurfl.sourceforge.net/)™資料庫，根據裝置的User-Agent來查詢裝置功能，例如螢幕解析度或javascript支援。

WURFL™資料庫的XML代碼通過解析`wurfl.xml`檔案（位於`/libs/wcm/mobile/devicespecs/wurfl.xml.`）以`/var/mobile/devicespecs`下的節點表示。對節點的擴展是首次啟動`cq-mobile-core`包時進行的。

設備功能儲存為節點屬性，節點表示設備型號。 您可以使用查詢來檢索設備或用戶代理的功能。

隨著WURFL™資料庫的不斷發展，您可能需要定制或替換它。 若要更新行動裝置資料庫，您有下列選項：

* 如果您擁有允許此用途的授權，請將檔案取代為最新版本。 請參閱安裝不同的WURFL資料庫。
* 使用AEM中提供的版本，並設定符合您的User-Agent字串並指向現有WURFL™裝置的regexp。 請參閱[添加基於regexp的User-Agent匹配](#adding-a-regexp-based-user-agent-matching)。

#### 測試User-Agent與WURFL™功能的映射{#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

當裝置存取您的行動網站時，AEM會偵測到裝置，並根據其功能將其對應至裝置群組，並傳送與裝置群組對應之頁面的檢視。 相符的裝置群組提供必要的樣式資訊。 可在「Mobile User-Agent測試」頁上測試映射：

`https://localhost:4502/etc/mobile/useragent-test.html`

#### 安裝不同的WURFL™資料庫{#installing-a-different-wurfl-database}

隨AEM安裝的截斷的WURFL™資料庫是預先更新的版本
2011年8月30日。 如果您的WURFL版本是在2011年8月30日之後發行，請確定您的使用符合您的授權。

要安裝WURFL™資料庫：

1. 在CRXDE Lite中，建立下列資料夾：`/apps/wcm/mobile/devicespecs`
1. 將WURFL™檔案複製到資料夾。
1. 將檔案更名為`wurfl.xml`。

AEM會自動剖析`wurfl.xml`檔案並更新`/var/mobile/devicespecs`下方的節點。

>[!NOTE]
>
>啟用完整的WURFL™資料庫時，可能需要幾分鐘的解析和啟動。 您可以監視日誌以獲取進度資訊。

#### 添加基於regexp的User-Agent匹配{#adding-a-regexp-based-user-agent-matching}

在/apps/wcm/mobile/devicespecs/wurfl/regexp下新增user-agent作為規則運算式，以指向現有的WURFL™裝置類型。

1. 在&#x200B;**CRXDE Lite**&#x200B;中，在/apps/wcm/mobile/devicespecs/regexp下建立節點，例如apple_ipad_ver1。
1. 將以下屬性添加到節點：

   * **regexp**:規則表達式定義用戶代理，例如：.*Mozilla。*iPad.*AppleWebKit。*Safari。*
   * **deviceId**:在wurfl.xml中定義的裝置ID，例如：apple_ipad_ver1

上述組態會使User-Agent符合隨附規則運算式的裝置對應至apple_ipad_ver1 WURFL™裝置ID（如果存在）。

## 客戶端設備檢測{#client-side-device-detection}

本節說明如何使用裝置用戶端偵測AEM，以最佳化頁面轉換或為用戶端提供替代網站版本。

AEM支援以`BrowserMap`為基礎的裝置用戶端偵測。 `BrowserMap` 在AEM中以用戶端資料庫的形式提供 `/etc/clientlibs/browsermap`。

`BrowserMap` 提供三種策略，您可用來為客戶提供替代網站，其採用順序如下：

1. [替代連結](#providing-alternate-links)
1. [裝置群組特定URL](#definingdevicegroupspecificurl)
1. [選取器型URL](#defining-selector-based-urls)

>[!NOTE]
>
>有關客戶端庫整合的詳細資訊，請閱讀[使用客戶端HTML庫](/help/sites-developing/clientlibs.md)部分。

### 提供備用連結{#providing-alternate-links}

`PageVariantsProvider` OSGi服務能夠為屬於同一系列的站點生成備用連結。 為了配置要由服務考慮的站點，必須從站點的根節點向`jcr:content`節點添加`cq:siteVariant`節點。

`cq:siteVariant`節點必須具有以下屬性：

* `cq:childNodesMapTo` -確定子節點將映射到哪個連結元素的屬性；建議您組織網站內容的方式，讓根節點的子系代表全域網站語言變體的根(例如 `/content/mysite/en`、 `/content/mysite/de`)，在此情況下，值 `cq:childNodesMapTo` 應為 `hreflang`;
* `cq:variantDomain` -指出將 `Externalizer` 使用哪些網域來產生頁面變數絕對URL;如果未設定此值，則會使用相對連結產生頁面變數；
* `cq:variantFamily` -表示此網站屬於哪一類網站；同一網站的多種特定裝置表示應屬於同一家族；
* `media` -儲存連結元素的媒體屬性值；建議您使用已註冊的名 `BrowserMap` 稱 `DeviceGroups`，讓程式 `BrowserMap` 庫自動將用戶端轉送至正確的網站變體。

#### PageVariantsProvider和Externalizer {#pagevariantsprovider-and-externalizer}

當`cq:siteVariant`節點的`cq:variantDomain`屬性值不為空時，`PageVariantsProvider`服務將使用此值作為`Externalizer`服務的配置域生成絕對鏈路。 請務必設定`Externalizer`服務以反映您的設定。

>[!NOTE]
>
>使用AEM時，有幾種方法可管理此類服務的組態設定；如需詳細資訊和建議的實務，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

### 定義設備組特定URL {#defining-a-device-group-specific-url}

如果您不想使用替代連結，可以為每個`DeviceGroup`設定全域URL。 我們建議您建立自己的用戶端程式庫，內嵌`browsermap.standard`用戶端程式庫，但重新定義裝置群組。

BrowserMap的設計方式是，透過從自訂用戶端程式庫建立名稱相同的新裝置群組並新增至`BrowserMap`物件，來覆蓋裝置群組定義。

>[!NOTE]
>
>如需詳細資訊，請閱讀[自訂BrowserMap](#creatingacustomisedbrowsermap)一節。

### 定義以選擇器為基礎的URL {#defining-selector-based-urls}

如果之前未採用任何機制來指示`BrowserMap`的備用站點，則將使用`DeviceGroups`名稱的選擇器將添加到`URL`中，此時您應提供自己的servlet來處理請求。

例如，BrowserMap識別為`smartphone`的裝置瀏覽`www.example.com/index.html`會轉送至`www.example.com/index.smartphone.html.`

### 在您的頁面上使用BrowserMap {#using-browsermap-on-your-pages}

若要在頁面中使用標準BrowserMap用戶端程式庫，您必須在頁面的`head`區段中使用`cq:include`標籤來加入`/libs/wcm/core/browsermap/browsermap.jsp`檔案。

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

除了在`JSP`檔案中新增`BrowserMap`用戶端程式庫外，您還必須將`cq:deviceIdentificationMode`字串屬性設為`client-side`，新增至網站根目錄下的`jcr:content`節點。

### 覆寫BrowserMap的預設行為{#overriding-browsermap-s-default-behaviour}

如果要自定義`BrowserMap` —— 通過覆蓋`DeviceGroups`或添加更多探測器——則應建立自己的客戶端庫，在其中嵌入`browsermap.standard`客戶端庫。

此外，您必須在`JavaScript`程式碼中手動呼叫`BrowserMap.forwardRequest()`方法。

>[!NOTE]
>
>有關客戶端庫整合的詳細資訊，請閱讀[使用客戶端HTML庫](/help/sites-developing/clientlibs.md)部分。

在您建立自訂的`BrowserMap`用戶端程式庫後，我們建議使用下列方法：

1. 在應用程式中建立`browsermap.jsp`檔案

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

1. 將`broswermap.jsp`檔案加入您的標題區段。

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 從特定頁面{#excluding-browsermap-from-certain-pages}排除BrowserMap

如果您想要從不需要用戶端偵測的頁面中排除BrowserMap程式庫，可以新增請求屬性：

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

這會使`/libs/wcm/core/browsermap/browsermap.jsp`指令碼將meta標籤新增至頁面，使`BrowserMap`不執行任何偵測：

```xml
<meta name="browsermap.enabled" content="false">
```

### 測試網站的特定版本{#testing-a-specific-version-of-a-web-site}

通常，BrowserMap指令碼會將訪客重新導向至最適合的網站版本，通常會視需要將訪客重新導向至案頭或行動網站。

您可以透過將`device`參數新增至URL，強制任何請求的裝置以測試網站的特定版本。 下列URL會轉譯Geometrixx Outdoors網站的行動版本。

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>`wcmmode`參數設為`disabled`以模擬發佈實例的行為。

覆蓋的裝置值會儲存在Cookie中，因此您可以瀏覽您的網站，而不需將`device`參數新增至每個`URL`。

因此，您必須呼叫相同的`URL`，並將`device`設為`browser`，才能返回網站的案頭版本。

>[!NOTE]
>
>BrowserMap將覆蓋的裝置值儲存在名為`BMAP_device`的Cookie中。 刪除此Cookie將確保CQ會根據您目前的裝置（例如桌上型電腦或行動裝置）提供適當的網站版本。

## 行動請求處理{#mobile-request-processing}

AEM會處理屬於觸控裝置群組的行動裝置發出的要求，如下所示：

1. iPad會傳送請求至AEM發佈例項，例如`https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM會判斷所請求頁面的網站是否為行動網站（透過檢查第一級頁面`/content/geometrixx_mobile`是否延伸行動頁面元件）。 如果是：
1. AEM會根據請求標題中的「使用者代理」來尋找裝置功能。
1. AEM會將裝置功能對應至裝置群組，並將`touch`設為裝置群組選擇器。
1. AEM將請求重新導向至`https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM會將回應傳送至iPad:

   * `products.touch.html` 以平常的方式呈現，而且容易操作。
   * 所述呈現元件使用選擇器來調整呈現。
   * AEM會自動將行動選擇器新增至頁面中的所有內部連結。

### 統計資料 {#statistics}

您可以取得行動裝置對AEM伺服器提出之請求數的統計資料。 可劃分的請求數：

* 每個設備組和設備
* 每年、每月和每日

要查看統計資訊，請執行以下操作：

1. 前往&#x200B;**工具**&#x200B;主控台。
1. 開啟&#x200B;**工具** > **Mobile**&#x200B;下方的&#x200B;**設備統計**&#x200B;頁。
1. 按一下連結，檢視特定年份、月份或日的統計資料。

**統計**&#x200B;頁的外觀如下：

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>在行動裝置第一次存取AEM時建立&#x200B;**統計**&#x200B;頁面，並偵測到該頁面。 在此之前，它不可用。

如果需要在統計資訊中生成條目，可以按如下步驟進行：

1. 使用行動裝置或模擬器(例如，在Firefox上使用https://chrispederick.com/work/user-agent-switcher/)。
1. 停用編寫模式，以在作者實例上請求行動頁面，例如：
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

**統計**&#x200B;頁現在可用。

### 支援「傳送連結至朋友」連結的頁面快取{#supporting-page-caching-for-send-link-to-a-friend-links}

Dispatcher通常可使用行動頁面，因為裝置群組選擇器會在頁面URL中區分為裝置群組轉譯的頁面，例如`/content/mobilepage.touch.html`。 不會快取對不含選擇器的行動頁面的要求，就像在本例中，裝置偵測會運作，最後重新導向至相符的裝置群組（或針對該問題「不符合」）。 使用裝置群組選擇器呈現的行動頁面由連結重寫器處理，連結重寫器會重寫頁面內的所有連結，以便也包含裝置群組選擇器，以防止對已限定頁面上的每次點按重新執行裝置偵測。

因此，您可能會遇到以下情況：

使用者Alice會重新導向至`coolpage.feature.html`，並將該URL傳送給朋友Bob，該朋友Bob會透過位於`touch`裝置群組中的不同用戶端存取該URL。

如果從前端快取提供`coolpage.feature.html`,AEM將無法分析請求，以找出行動選擇器不符合新的使用者代理，而Bob會收到錯誤的陳述。

若要解決這個問題，您可以在頁面上加入簡單的選擇UI，使用者可在此覆寫由AEM選取的裝置群組。 在上述範例中，頁面上的連結（或圖示）可讓使用者在認為裝置適合時切換至`coolpage.touch.html`。
