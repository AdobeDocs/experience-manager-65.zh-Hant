---
title: 建立行動裝置網站
description: 建立行動網站與建立標準網站類似，因為其中也涉及建立範本和元件
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '3701'
ht-degree: 0%

---

# 建立行動裝置網站{#creating-sites-for-mobile-devices}

{{ue-over-mobile}}

建立行動網站與建立標準網站類似，因為其中也涉及建立範本和元件。 如需建立範本和元件的詳細資訊，請參閱下列頁面： [範本](/help/sites-developing/templates.md)、[元件](/help/sites-developing/components.md)和[開始開發AEM Sites](/help/sites-developing/getting-started.md)。 主要差異在於啟用網站內建的Adobe Experience Manager (AEM)行動裝置功能。 這可透過建立依賴行動頁面元件的範本來達成。

請考慮使用[回應式設計](/help/sites-developing/responsive.md)，建立可容納多種熒幕大小的單一網站。

若要開始使用，您可以檢視AEM中提供的&#x200B;**We.Retail行動示範網站**。

若要建立行動網站，請依照下列步驟進行：

1. 建立頁面元件：

   * 將`sling:resourceSuperType`屬性設定為`wcm/mobile/components/page`
如此一來，元件需仰賴行動頁面元件。

   * 使用專案特定邏輯建立`body.jsp`。

1. 建立頁面範本：

   * 將`sling:resourceType`屬性設定為新建立的頁面元件。
   * 設定`allowedPaths`屬性。

1. 建立網站的設計頁面。
1. 在`/content`節點底下建立網站根目錄頁面：

   * 設定`cq:allowedTemplates`屬性。
   * 設定`cq:designPath`屬性。

1. 在網站根頁面的頁面屬性中，設定&#x200B;**行動裝置**&#x200B;索引標籤中的裝置群組。
1. 使用新範本建立網頁。

行動頁面元件( `/libs/wcm/mobile/components/page`)：

* 將&#x200B;**行動裝置**&#x200B;索引標籤新增至頁面屬性對話方塊。
* 透過其`head.jsp`，它會從要求中擷取目前的行動裝置群組，而且如果找到裝置群組，會使用群組的`drawHead()`方法來包含裝置群組的相關模擬器init元件（僅適用於作者模式）以及裝置群組的轉譯CSS。

>[!NOTE]
>
>行動網站的根頁面必須位於節點階層的第1層，且建議位於/content節點下方。

## 使用多網站管理員建立行動網站 {#creating-a-mobile-site-with-the-multi-site-manager}

使用多網站管理員(MSM)從標準網站建立行動即時副本。 標準網站會自動轉換為行動網站：行動網站具有行動網站的所有功能（例如，在模擬器中編輯），且可與標準網站同步管理。 請參閱多網站管理員頁面中的[為不同管道建立即時副本](/help/sites-administering/msm.md)一節。

## 伺服器端Mobile API {#server-side-mobile-api}

包含行動類別的Java™套件包括：

* [com.day.cq.wcm.mobile.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) — 定義MobileConstants。
* [com.day.cq.wcm.mobile.api.device](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) — 定義裝置、裝置群組和DeviceGroupList。
* [com.day.cq.wcm.mobile.api.device.capability](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) — 定義裝置功能。
* [com.day.cq.wcm.mobile.api.wurfl](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) — 定義WurflQueryEngine。
* [com.day.cq.wcm.mobile.core](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) — 定義MobileUtil，它提供各種圍繞WCM Mobile旋轉的公用程式方法。

### 行動元件 {#mobile-components}

**We.Retail行動示範網站**&#x200B;使用下列行動元件，這些元件位於`/libs/foundation/components`下方：

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
   <td> — 頁尾</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>行動</td>
   <td> — 以影像基礎元件<br />為基礎 — 如果裝置有能力，則會轉譯影像<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>行動</td>
   <td> — 根據list foundation元件<br /> — 如果裝置有能力，listitem_teaser.jsp會呈現影像<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>隱藏</td>
   <td> — 以標誌基礎元件<br />為基礎 — 如果裝置具備功能，則會轉譯影像<br /> </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>行動</td>
   <td><p> — 與reference foundation元件類似</p> <p> — 將textimage元件對應至mobiletextimage元件，並將影像元件對應至mobileimage元件</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>行動</td>
   <td> — 根據textimage foundation元件<br /> — 如果裝置有能力，則會呈現影像</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>隱藏</td>
   <td><p> — 根據topnav foundation元件</p> <p> — 僅轉譯文字</p> </td>
  </tr>
 </tbody>
</table>

#### 建立行動元件 {#creating-a-mobile-component}

AEM行動架構可讓您開發對發出請求的裝置敏感的元件。 下列程式碼範例說明如何在元件jsp中使用AEM行動API，尤其是如何：

* 從要求取得裝置：
  `Device device = slingRequest.adaptTo(Device.class);`

* 取得裝置群組：
  `DeviceGroup deviceGroup = device.getDeviceGroup();`

* 取得裝置群組功能：
  `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* 取得裝置屬性（原始功能索引鍵/值，來自WURFL資料庫）：
  `Map<String,String> deviceAttributes = device.getAttributes();`

* 取得裝置使用者代理程式：
  `String userAgent = device.getUserAgent();`

* 從目前頁面取得裝置群組清單（作者指派給網站的裝置群組）：
  `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* 檢查裝置群組是否支援影像
  `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
或
  `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>在JSP中，`slingRequest`可透過`<sling:defineObjects>`標籤使用，而透過`<cq:defineObjects>`標籤使用`currentPage`。

### 模擬器 {#emulators}

模擬器式製作為作者提供工具，可建立適用於行動使用者端的內容頁面。 行動內容製作遵循與就地WYSIWYG編輯相同的原則。 為了讓作者能在行動裝置上感知頁面外觀，可使用裝置模擬器編輯行動內容頁面。

行動裝置模擬器是以一般模擬器架構為基礎。 如需詳細資訊，請參閱[模擬器](/help/sites-developing/emulators.md)。

裝置模擬器會在頁面上顯示行動裝置，而一般的編輯（parsys、元件）會在裝置的畫面中進行。 裝置模擬器取決於為網站設定的裝置群組。 可以將數個模擬器指派給裝置群組。 然後，內容頁面上就會提供所有模擬器。 依預設，會顯示指派給場地之第一個裝置群組的第一個模擬器。 您可以透過頁面頂端的模擬器輪播或Sidekick的編輯按鈕來切換模擬器。

**正在建立模擬器**

若要建立模擬器，請參閱一般模擬器頁面中的[建立自訂行動模擬器](/help/sites-developing/emulators.md)。

**行動模擬器的主要特性**

* 裝置群組由一個或多個模擬器組成：裝置群組設定頁面，例如/etc/mobile/groups/touch，包含`jcr:content`節點下方的`emulators`屬性。
注意：雖然相同的模擬器可能屬於數個裝置群組，但是這不太合理。

* 透過裝置群組的設定對話方塊，`emulators`屬性會以所需模擬器的路徑設定。 例如：`/libs/wcm/mobile/components/emulators/iPhone4`。

* 模擬器元件（例如`/libs/wcm/mobile/components/emulators/iPhone4`）會擴充基本行動模擬器元件( `/libs/wcm/mobile/components/emulators/base`)。

* 設定裝置群組時，可選取擴充基本行動模擬器的每個元件。 因此，可以輕鬆建立或擴充自訂模擬器。
* 在編輯模式下的請求時間，會使用模擬器實作來轉譯頁面。
* 當頁面的範本仰賴行動頁面元件時，模擬器功能會自動整合到頁面中（透過行動頁面元件的`head.jsp`）。

### 裝置群組 {#device-groups}

行動裝置群組會根據裝置功能提供行動裝置的細分。 裝置群組提供在製作執行個體上以模擬器為基礎製作以及在發佈執行個體上正確呈現內容所需的資訊：當作者將內容新增到行動頁面並發佈後，即可在發佈執行個體上請求頁面。 在那裡，使用其中一個已設定的裝置群組來呈現內容頁面，而非模擬器編輯檢視。 裝置群組的選取是根據[行動裝置偵測](#devicedetection)進行。 然後，相符的裝置群組會提供必要的樣式資訊。

裝置群組定義為`/etc/mobile/devices`下的內容頁面，並使用&#x200B;**行動裝置群組**&#x200B;範本。 裝置群組範本可做為內容頁面形式之裝置群組定義的設定範本。 其主要特性包括：

* 位置： `/libs/wcm/mobile/templates/devicegroup`
* 允許的路徑： `/etc/mobile/groups/*`
* 頁面元件： `wcm/mobile/components/devicegroup`

#### 指派裝置群組至您的網站 {#assigning-device-groups-to-your-site}

建立行動網站時，您必須將裝置群組指派給網站。 AEM根據裝置的HTML和JavaScript轉譯功能提供三個裝置群組：

* **功能**&#x200B;手機，適用於Sony Ericsson W800這類功能裝置，支援基本HTML，但不支援影像和JavaScript。
* **智慧型**&#x200B;手機，適用於BlackBerry®之類的裝置，支援基本HTML和影像，但不支援JavaScript。

* **觸控式**&#x200B;手機，適用於像iPad這類裝置，並完全支援HTML、影像、JavaScript和裝置旋轉。

由於模擬器可以與裝置群組相關聯（請參閱[建立裝置群組](#creating-a-device-group)小節），將裝置群組指派至網站可讓作者在與裝置群組相關聯的模擬器之間選取，以編輯頁面。

若要將裝置群組指派給您的網站：

1. 在您的瀏覽器中，移至&#x200B;**Siteadmin**&#x200B;主控台。
1. 在&#x200B;**網站**&#x200B;底下開啟行動網站的根頁面。
1. 開啟頁面屬性。
1. 選取&#x200B;**行動裝置**&#x200B;索引標籤：

   * 定義裝置群組。
   * 按一下&#x200B;**「確定」**。

>[!NOTE]
>
>為網站定義裝置群組後，網站的所有頁面都會繼承這些裝置群組。

#### 裝置群組篩選器 {#device-group-filters}

裝置群組篩選器會定義功能型條件，用以判斷裝置是否屬於群組。 建立裝置群組時，您可以選取用來評估裝置的篩選器。

在執行階段，當AEM收到來自裝置的HTTP要求時，與群組關聯的每個篩選器都會將裝置功能與特定條件比較。 當裝置具備篩選器所需的所有功能時，即視為屬於群組。 功能會從WURFL™資料庫擷取。

裝置群組可使用零個或多個篩選器進行功能偵測。 此外，篩選器也可以用於多個裝置群組。 AEM提供預設的篩選器，可判斷裝置是否具備為群組選取的功能：

* CSS
* JPG和PNG影像
* JavaScript
* 裝置旋轉

如果裝置群組未使用篩選器，則為該群組設定的選取功能是裝置唯一需要的功能。

如需詳細資訊，請參閱[建立裝置群組篩選器](/help/sites-developing/groupfilters.md)。

#### 建立裝置群組 {#creating-a-device-group}

當AEM安裝的群組不符合您的需求時，請建立裝置群組。

1. 在您的瀏覽器中，前往&#x200B;**工具**&#x200B;主控台。
1. 在&#x200B;**工具** > **行動裝置** > **裝置群組**&#x200B;下方建立頁面。 在&#x200B;**建立頁面**&#x200B;對話方塊中：

   * 以&#x200B;**標題**&#x200B;的形式，輸入`Special Phones`。

   * 以&#x200B;**名稱**&#x200B;的形式，輸入`special`。

   * 選取&#x200B;**行動裝置群組範本**。
   * 按一下&#x200B;**建立**。

1. 在CRXDE中，在`/etc/mobile/groups/special`節點下方新增包含裝置群組樣式的&#x200B;**static.css**&#x200B;檔案。

1. 開啟&#x200B;**特殊電話**&#x200B;頁面。
1. 若要設定裝置群組，請按一下&#x200B;**設定**&#x200B;旁的&#x200B;**編輯**按鈕。
在**一般**&#x200B;標籤上：

   * **標題**：行動裝置群組的名稱。
   * **描述**：群組的描述。
   * **使用者代理程式**：符合裝置的使用者代理字串。 這是選擇性的，而且可以是規則運算式。 範例： `BlackBerryZ10`
   * **功能**：定義群組是否可處理影像、CSS、JavaScript或裝置旋轉。
   * **最小熒幕寬度**&#x200B;和&#x200B;**高度**
   * **停用模擬器**：在內容編輯期間啟用/停用模擬器。

   在&#x200B;**模擬器**&#x200B;標籤上：

   * **模擬器**：選取指派給此裝置群組的模擬器。

   在&#x200B;**篩選器**&#x200B;索引標籤上：

   * 若要新增篩選器，請按一下「新增專案」 ，然後從下拉式清單中選取篩選器。
   * 篩選器會依照其顯示順序進行評估。 當裝置不符合篩選條件時，將不會評估清單上的後續篩選器。

1. 按一下「確定」。

行動裝置群組設定對話方塊如下所示：

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### 每個裝置群組的自訂CSS {#custom-css-per-device-group}

如前所述，可以將自訂CSS與裝置群組頁面建立關聯，就像設計頁面的CSS一樣。 此CSS用於影響作者及發佈時裝置群組特定頁面內容的轉譯。 接著會自動包含此CSS：

* 在製作執行個體的頁面中，此裝置群組使用的每個模擬器。
* 在發佈執行個體的頁面中，如果請求的使用者代理符合此特定裝置群組中的行動裝置。

## 伺服器端裝置偵測 {#server-side-device-detection}

使用篩選器和裝置規格庫來判斷執行HTTP要求的裝置功能。

### 開發裝置群組篩選器 {#develop-device-group-filters}

建立裝置群組篩選器，以定義一組裝置功能需求。 建立您需要的篩選器數，以鎖定所需的裝置功能群組。

設計您的篩選器，以便使用它們的組合來定義功能群組。 通常，不同裝置群組的功能會重疊。 因此，您可能會使用具有多個裝置群組定義的篩選器。

建立篩選器後，您可以在群組設定中使用它。

如需詳細資訊，請前往[建立裝置群組篩選器](/help/sites-developing/groupfilters.md)。

### 使用WURFL™資料庫 {#using-the-wurfl-database}

AEM使用截斷版本的[WURFL](https://wurfl.sourceforge.net/)™資料庫，根據裝置的使用者代理程式查詢裝置功能，例如熒幕解析度或JavaScript支援。

透過剖析`/libs/wcm/mobile/devicespecs/wurfl.xml.`的`wurfl.xml`檔案，WURFL™資料庫的XML程式碼表示為`/var/mobile/devicespecs`以下的節點。在第一次啟動`cq-mobile-core`組合時，會展開至節點。

裝置功能會儲存為節點屬性，而節點代表裝置模型。 您可以使用查詢來擷取裝置或使用者代理程式的功能。

隨著WURFL™資料庫不斷演化，您可能需要加以自訂或取代。 若要更新行動裝置資料庫，您有以下選項：

* 如果您有允許此使用的授權，請以最新版本取代檔案。 請參閱安裝其他WURFL資料庫。
* 使用AEM中可用的版本，並設定符合使用者代理程式字串且指向現有WURFL™裝置的regexp。 請參閱[新增regexp型使用者代理程式比對](#adding-a-regexp-based-user-agent-matching)。

#### 測試使用者代理程式與WURFL™功能的對應 {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

當裝置存取您的行動網站時，AEM會偵測該裝置、根據其功能將其對應至裝置群組，並傳送對應至裝置群組的頁面檢視。 相符的裝置群組可提供必要的樣式資訊。 您可在「行動使用者代理程式測試」頁面上測試對應：

`https://localhost:4502/etc/mobile/useragent-test.html`

#### 安裝其他WURFL™資料庫 {#installing-a-different-wurfl-database}

與AEM一起安裝的截斷WURFL™資料庫是預先發佈的版本
2011年8月30日。 如果您的WURFL版本是在2011年8月30日之後發行，請確定您的使用方式符合授權規範。

若要安裝WURFL™資料庫：

1. 在CRXDE Lite中建立下列資料夾： `/apps/wcm/mobile/devicespecs`
1. 將WURFL™檔案複製到資料夾。
1. 將檔案重新命名為`wurfl.xml`。

AEM會自動剖析`wurfl.xml`檔案並更新`/var/mobile/devicespecs`下的節點。

>[!NOTE]
>
>啟用完整的WURFL™資料庫時，剖析和啟動可能需要幾分鐘的時間。 您可以檢視記錄檔以取得進度資訊。

#### 新增regexp型使用者代理程式比對 {#adding-a-regexp-based-user-agent-matching}

將使用者代理程式新增為/apps/wcm/mobile/devicespecs/wurfl/regexp底下的規則運算式，以指向現有的WURFL™裝置型別。

1. 在&#x200B;**CRXDE Lite**&#x200B;中，在/apps/wcm/mobile/devicespecs/regexp下方建立節點，例如`apple_ipad_ver1`。
1. 將下列屬性新增至節點：

   * **regexp**：定義使用者代理的規則運算式，例如。&#42;Mozilla。&#42;iPad。&#42;AppleWebKit。&#42;Safari.&#42;
   * **deviceId**： wurfl.xml中定義的裝置識別碼，例如`apple_ipad_ver1`

上述設定會讓使用者代理程式符合提供之規則運算式的裝置對應至apple_ipad_ver1 WURFL™裝置ID （如果存在）。

## 使用者端裝置偵測 {#client-side-device-detection}

本節說明如何使用AEM的裝置使用者端偵測來最佳化頁面呈現，或向使用者端提供替代網站版本。

AEM支援以`BrowserMap`為基礎的裝置使用者端偵測。 `BrowserMap`已在AEM中出貨作為`/etc/clientlibs/browsermap`下的使用者端程式庫。

`BrowserMap`提供您三種策略，可用於為使用者端提供替代網站，其使用順序如下：

1. [替代連結](#providing-alternate-links)
1. [裝置群組特定URL](#definingdevicegroupspecificurl)
1. [選擇器型URL](#defining-selector-based-urls)

>[!NOTE]
>
>如需使用者端資料庫整合的詳細資訊，請參閱[使用使用者端HTML資料庫](/help/sites-developing/clientlibs.md)。

### 提供替代連結 {#providing-alternate-links}

`PageVariantsProvider` OSGi服務能夠為屬於相同系列的網站產生替代連結。 若要設定服務要考量的站台，必須從站台的根將`cq:siteVariant`節點新增到`jcr:content`節點。

`cq:siteVariant`節點必須有下列屬性：

* `cq:childNodesMapTo` — 決定子節點將對應至連結元素的哪個屬性；建議以這種方式組織網站的內容，讓根節點的子節點代表全域網站的語言變體的根（例如，`/content/mysite/en`， `/content/mysite/de`），在此情況下`cq:childNodesMapTo`的值應該是`hreflang`；
* `cq:variantDomain` — 指出使用哪些`Externalizer`網域來產生頁面變體絕對URL；如果未設定此值，則將會使用相對連結產生頁面變體；
* `cq:variantFamily` — 指出此網站屬於哪個網站系列；相同網站的多重灌置特定代表應屬於相同系列；
* `media` — 儲存連結專案的媒體屬性值；建議使用已登入的`BrowserMap`名稱`DeviceGroups`，讓`BrowserMap`資料庫可以自動將使用者端轉送至正確的網站變體。

#### PageVariantsProvider和Externalizer {#pagevariantsprovider-and-externalizer}

當`cq:siteVariant`節點的`cq:variantDomain`屬性值不是空白時，`PageVariantsProvider`服務會使用此值做為`Externalizer`服務的設定網域來產生絕對連結。 請務必設定`Externalizer`服務以反映您的設定。

>[!NOTE]
>
>使用AEM時，有數種方法可管理此類服務的組態設定；請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)以取得詳細資訊和建議的作法。

### 定義裝置群組特定URL {#defining-a-device-group-specific-url}

如果您不想使用替代連結，您可以為每個`DeviceGroup`設定全域URL。 Adobe建議您建立自己的使用者端程式庫，其中包含`browsermap.standard`使用者端程式庫，但會重新定義裝置群組。

BrowserMap的設計方式是，透過從自訂使用者端程式庫建立相同名稱的裝置群組並新增至`BrowserMap`物件，來覆寫裝置群組定義。

>[!NOTE]
>
>如需詳細資訊，請參閱[自訂瀏覽器地圖](#creatingacustomisedbrowsermap)。

### 定義以選取器為基礎的URL {#defining-selector-based-urls}

如果先前未使用任何機制來指定`BrowserMap`的替代網站，則會將使用`DeviceGroups`名稱的選取器新增到`URL`，在這種情況下，您應該提供自己的可處理請求的servlet。

例如，由BrowserMap識別為`smartphone`的裝置瀏覽`www.example.com/index.html`已轉送至`www.example.com/index.smartphone.html.`

### 在網頁上使用瀏覽器地圖 {#using-browsermap-on-your-pages}

若要在頁面中使用標準BrowserMap使用者端資料庫，您必須在頁面的`head`區段中使用`cq:include`標籤加入`/libs/wcm/core/browsermap/browsermap.jsp`檔案。

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

除了在`JSP`檔案中新增`BrowserMap`使用者端程式庫之外，您還必須將設為`client-side`的`cq:deviceIdentificationMode`字串屬性新增至網站根目錄下的`jcr:content`節點。

### 覆寫BrowserMap的預設行為 {#overriding-browsermap-s-default-behaviour}

如果您要自訂`BrowserMap` — 透過覆寫`DeviceGroups`或新增更多探查 — 則應建立您自己的使用者端程式庫，並在其中內嵌`browsermap.standard`使用者端程式庫。

此外，您必須手動呼叫`JavaScript`程式碼中的`BrowserMap.forwardRequest()`方法。

>[!NOTE]
>
>如需使用者端資料庫整合的詳細資訊，請參閱[使用使用者端HTML資料庫](/help/sites-developing/clientlibs.md)。

建立自訂的`BrowserMap`使用者端程式庫後，Adobe會建議下列方法：

1. 在您的應用程式中建立`browsermap.jsp`檔案

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

1. 在您的head區段中包含`broswermap.jsp`檔案。

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 從某些頁面排除瀏覽器地圖 {#excluding-browsermap-from-certain-pages}

如果您想從某些不需要使用者端偵測的頁面中排除BrowserMap程式庫，可以新增request屬性：

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

這會使`/libs/wcm/core/browsermap/browsermap.jsp`指令碼將meta標籤新增至頁面，使`BrowserMap`不執行任何偵測：

```xml
<meta name="browsermap.enabled" content="false">
```

### 測試網站的特定版本 {#testing-a-specific-version-of-a-web-site}

通常，BrowserMap指令碼會一律將訪客重新導向至最適合的網站版本，通常會在需要時將訪客重新導向案頭或行動網站。

您可以將`device`引數新增至您的URL，以強制任何要求的裝置測試網站的特定版本。 以下URL會轉譯Geometrixx Outdoors網站的行動版本。

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>`wcmmode`引數設定為`disabled`以模擬發佈執行個體的行為。

覆寫裝置值儲存在Cookie中，因此您可以瀏覽您的網站，而無需將`device`引數新增至每個`URL`。

因此，您必須呼叫相同的`URL`，並將`device`設為`browser`，才能返回網站的案頭版本。

>[!NOTE]
>
>BrowserMap會將覆寫裝置值儲存在名為`BMAP_device`的Cookie中。 刪除此Cookie可確保CQ會根據您目前的裝置（例如桌上型電腦或行動裝置）提供適當版本的網站。

## 行動請求處理 {#mobile-request-processing}

AEM會依下列方式處理屬於觸控裝置群組的行動裝置所發出的請求：

1. iPad傳送要求給AEM發佈執行個體，例如`https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM判斷請求頁面的網站是否為行動網站（透過檢查第一層頁面`/content/geometrixx_mobile`是否延伸行動頁面元件）。 如果是：
1. AEM會根據請求標頭中的使用者代理程式查詢裝置功能。
1. AEM將裝置功能對應至裝置群組，並將`touch`設定為裝置群組選擇器。
1. AEM將要求重新導向至`https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM會將回應傳送至iPad：

   * `products.touch.html`會以一般方式轉譯，且可快取。
   * 演算元件會使用選取器來調整簡報。
   * AEM會自動將行動裝置選擇器新增至頁面中的所有內部連結。

### 統計資料 {#statistics}

您可以取得有關行動裝置向AEM伺服器提出之要求數目的統計資料。 可劃分的要求數目：

* 每個裝置群組與裝置
* 每年、每月與日

若要檢視統計資料，請執行下列動作：

1. 移至&#x200B;**工具**&#x200B;主控台。
1. 開啟&#x200B;**工具** > **行動裝置**&#x200B;下方的&#x200B;**裝置統計資料**&#x200B;頁面。
1. 按一下連結，即可檢視特定年、月或日的統計資料。

**統計資料**&#x200B;頁面如下所示：

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>**統計資料**&#x200B;頁面是在行動裝置第一次存取AEM並偵測到時建立的。 在此之前，無法使用。

如果您需要在統計資料中產生專案，可以依照下列步驟進行：

1. 使用行動裝置或模擬器(例如Firefox上的https://chrispederick.com/work/user-agent-switcher/)。
1. 停用編寫模式，例如在編寫執行個體上請求行動頁面：
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

**統計資料**&#x200B;頁面現已可用。

### 支援「將連結傳送至朋友」連結的頁面快取 {#supporting-page-caching-for-send-link-to-a-friend-links}

在Dispatcher上可快取行動頁面，因為呈現給裝置群組的頁面會在頁面URL中由裝置群組選擇器區分，例如`/content/mobilepage.touch.html`。 絕不會快取沒有選擇器的行動頁面請求，因為在此情況下，裝置偵測會運作，最後會重新導向至相符的裝置群組（或就此而言的「nomatch」）。 連結重寫程式會處理以裝置群組選擇器呈現的行動頁面，重寫程式會重寫頁面中的所有連結，使其也包含裝置群組選擇器，以防止在每次點按已合格的頁面時，都重新執行裝置偵測。

因此，您可能會遇到下列情況：

使用者Alice被重新導向至`coolpage.feature.html`，並傳送該URL給朋友Bob，後者透過屬於`touch`裝置群組的不同使用者端存取該URL。

如果從前端快取中提供`coolpage.feature.html`，AEM就沒有機會分析請求以找出行動選擇器不符合新的使用者代理，並且Bob取得錯誤的表示。

若要解決此問題，您可以在頁面上包含簡單的選取UI，使用者可以在其中覆寫AEM選取的裝置群組。 在上述範例中，如果使用者認為他們的裝置足夠好，頁面上的連結（或圖示）可讓使用者切換至`coolpage.touch.html`。
