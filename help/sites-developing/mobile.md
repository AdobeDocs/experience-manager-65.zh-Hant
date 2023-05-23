---
title: 為移動設備建立站點
seo-title: Creating Sites for Mobile Devices
description: 建立移動站點與建立標準站點類似，因為它還涉及建立模板和元件
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

# 為移動設備建立站點{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

建立移動站點與建立標準站點類似，因為它還涉及建立模板和元件。 有關建立模板和元件的詳細資訊，請參閱以下頁： [模板](/help/sites-developing/templates.md)。 [元件](/help/sites-developing/components.md) 和 [開發AEM Sites](/help/sites-developing/getting-started.md)。 主要區別在於啟用AEM站點內內置的移動功能。 通過建立依賴於移動頁面元件的模板來實現。

您還應考慮使用 [響應設計](/help/sites-developing/responsive.md)，建立可容納多個螢幕大小的單個站點。

要開始，您可以查看 **We.Retail Mobile演示網站** 中可AEM用。

要建立移動站點，請按如下步驟操作：

1. 建立頁面元件：

   * 設定 `sling:resourceSuperType` 屬性 `wcm/mobile/components/page`
這樣，元件就依賴於移動頁面元件。

   * 建立 `body.jsp` 與項目特定邏輯的關係。

1. 建立頁面模板：

   * 設定 `sling:resourceType` 屬性。
   * 設定 `allowedPaths` 屬性。

1. 為站點建立設計頁。
1. 建立位於 `/content` 節點：

   * 設定 `cq:allowedTemplates` 屬性。
   * 設定 `cq:designPath` 屬性。

1. 在站點根頁的頁面屬性中，在 **移動** 頁籤。
1. 使用新模板建立網站頁。

移動頁面元件( `/libs/wcm/mobile/components/page`):

* 添加 **移動** 頁籤。
* 通過 `head.jsp`，它從請求中檢索當前移動設備組，如果找到設備組，則使用組 `drawHead()` 方法包括設備組的關聯模擬器init元件（僅在作者模式下）和設備組的呈現CSS。

>[!NOTE]
>
>移動站點的根頁面必須位於節點層次結構的第1級，建議位於/content節點下。

## 使用多站點管理器建立移動站點 {#creating-a-mobile-site-with-the-multi-site-manager}

使用多站點管理器(MSM)從標準站點建立移動即時拷貝。 標準站點自動轉換為移動站點：移動站點具有移動站點的所有功能（例如，在模擬器中的版本），並且可以與標準站點同步管理。 請參閱一節 [為不同渠道建立即時拷貝](/help/sites-administering/msm.md) 中。

## 伺服器端移動API {#server-side-mobile-api}

包含移動類的Java包包括：

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  — 定義MobileConstants。
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html)  — 定義設備、設備組和設備組清單。
* [com.day.cq.wcm.mobile.api.device.capability](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  — 定義DeviceCapability。
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html)  — 定義WurflQueryEngine。
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html)  — 定義MobileUtil，它提供圍繞WCM Mobile的各種實用方法。

### 移動元件 {#mobile-components}

的 **We.Retail Mobile演示網站** 使用下面的以下移動元件 `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>名稱</td>
   <td>群組</td>
   <td>特徵</td>
  </tr>
  <tr>
   <td>移動頁腳</td>
   <td>隱藏</td>
   <td> — 頁腳</td>
  </tr>
  <tr>
   <td>移動影像</td>
   <td>行動</td>
   <td> — 基於影像基礎元件<br />  — 如果設備可以，則呈現影像<br /> </td>
  </tr>
  <tr>
   <td>移動</td>
   <td>行動</td>
   <td> — 基於清單基礎元件<br /> - listitem_teaser.jsp在設備可用時呈現影像<br /> </td>
  </tr>
  <tr>
   <td>移動標誌</td>
   <td>隱藏</td>
   <td> — 基於徽標基礎元件<br />  — 如果設備可以，則呈現影像<br /> </td>
  </tr>
  <tr>
   <td>移動參考</td>
   <td>行動</td>
   <td><p> — 類似於參考基礎元件</p> <p> — 將文本時間元件映射到移動文本時間元件，將影像元件映射到移動影像元件</p> </td>
  </tr>
  <tr>
   <td>移動時間</td>
   <td>行動</td>
   <td> — 基於文本時間基礎元件<br />  — 如果設備可以，則呈現影像</td>
  </tr>
  <tr>
   <td>移動導航</td>
   <td>隱藏</td>
   <td><p> — 基於topnav foundation元件</p> <p> — 僅呈現文本</p> </td>
  </tr>
 </tbody>
</table>

#### 建立移動元件 {#creating-a-mobile-component}

移AEM動框架允許開發對發出請求的設備敏感的元件。 以下代碼示例說明如何在元件jspAEM中使用移動API，尤其是如何：

* 從請求獲取設備：
   `Device device = slingRequest.adaptTo(Device.class);`

* 獲取設備組：
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* 獲取設備組功能：
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* 獲取設備屬性（WURFL資料庫中的原始功能鍵/值）:
   `Map<String,String> deviceAttributes = device.getAttributes();`

* 獲取設備用戶代理：
   `String userAgent = device.getUserAgent();`

* 從當前頁面獲取設備組清單（由作者分配給站點的設備組）:
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* 檢查設備組是否支援映像
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
或

...   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>在JSP中， `slingRequest` 可通過 `<sling:defineObjects>` 標籤和 `currentPage` 通過 `<cq:defineObjects>` 標籤。

### 模擬器 {#emulators}

基於模擬器的創作為作者提供了為移動客戶端建立內容頁面的方法。 移動內容創作遵循原則，即地WYSIWYG編輯。 為了使作者感知移動設備上的頁面外觀，使用設備模擬器編輯移動內容頁面。

移動設備模擬器基於通用模擬器框架。 有關詳細資訊，請參閱 [模擬器](/help/sites-developing/emulators.md) 的子菜單。

設備模擬器在頁面上顯示移動設備，而通常的編輯(parsys、components)在設備的螢幕中進行。 設備模擬器取決於為站點配置的設備組。 可以將多個模擬器分配給設備組。 然後，所有模擬器都可在內容頁面上使用。 預設情況下，將顯示分配給分配給站點的第一個設備組的第一個模擬器。 模擬器可以通過頁面頂部的模擬器旋轉傳送器或通過Sidekick的編輯按鈕進行切換。

**建立模擬器**

要建立模擬器，請參閱 [建立自定義移動模擬器](/help/sites-developing/emulators.md) 「模擬器」(generic Emulators)頁面中的「模擬器」(section)。

**移動模擬器的主要特點**

* 設備組由多個模擬器之一組成：設備組配置頁，例如/etc/mobile/groups/touch，包含 `emulators` 下面的屬性 `jcr:content` 的下界。
注：雖然同一模擬器可能屬於多個設備組，但這沒有什麼意義。

* 通過設備組的配置對話框， `emulators` 使用所需模擬器的路徑設定屬性。 例如：`/libs/wcm/mobile/components/emulators/iPhone4`。

* 模擬器元件(例如 `/libs/wcm/mobile/components/emulators/iPhone4`)擴展基本移動模擬器元件( `/libs/wcm/mobile/components/emulators/base`)。

* 在配置設備組時，擴展基本移動模擬器的每個元件都可供選擇。 因此，可以輕鬆地建立或擴展自定義模擬器。
* 在編輯模式下的請求時，模擬器實現用於呈現頁面。
* 當頁面的模板依賴於移動頁面元件時，模擬器功能自動整合在頁面中(通過 `head.jsp` )。

### 裝置群組 {#device-groups}

移動設備組基於設備能力提供移動設備的分段。 設備組提供在作者實例上基於模擬器的創作和在發佈實例上正確呈現內容所需的資訊：一旦作者將內容添加到移動頁面並已發佈該頁面，就可以在發佈實例上請求該頁面。 在此，使用配置的設備組之一來呈現內容頁面，而不是模擬器編輯視圖。 根據 [移動設備檢測](#devicedetection)。 然後，匹配設備組提供必要的造型資訊。

設備組定義為下面的內容頁 `/etc/mobile/devices` 並使用 **移動設備組** 的下界。 設備組模板用作內容頁面形式的設備組定義的配置模板。 其主要特點是：

* 位置: `/libs/wcm/mobile/templates/devicegroup`
* 允許的路徑： `/etc/mobile/groups/*`
* 頁面元件： `wcm/mobile/components/devicegroup`

#### 將設備組分配給您的站點 {#assigning-device-groups-to-your-site}

建立移動站點時，需要將設備組分配給站點。 根AEM據設備的HTML和JavaScript呈現能力提供三個設備組：

* **功能** 手機，用於索尼愛立信W800等功能設備，支援基本HTML，但不支援影像和JavaScript。
* **智慧** 手機，適用於像黑莓這樣支援基本HTML和影像的設備，但不支援JavaScript。

* **觸摸** 手機，像iPad這樣完全支援HTML、影像、JavaScript和設備輪換的設備。

由於模擬器可以與設備組關聯(請參見 [建立設備組](#creating-a-device-group))，將設備組分配給站點使作者能夠在與設備組關聯的模擬器之間進行選擇，以編輯該頁。

要將設備組分配給您的站點：

1. 在瀏覽器中，轉到 **站點管理** 控制台。
1. 在下面開啟移動站點的根頁 **網站**。
1. 開啟頁面屬性。
1. 選擇 **移動** 頁籤：

   * 定義設備組。
   * 按一下&#x200B;**「確定」**。

>[!NOTE]
>
>為站點定義設備組後，站點的所有頁面都會繼承這些設備組。

#### 裝置群組篩選器 {#device-group-filters}

設備組過濾器定義基於功能的標準以確定設備是否屬於該組。 建立設備組時，可以選擇用於評估設備的篩選器。

在從設備接AEM收HTTP請求的運行時，與組相關聯的每個過濾器將設備能力與特定標準進行比較。 當設備具有篩選器所需的所有功能時，設備被視為屬於組。 功能從WURFL™資料庫檢索。

設備組可以使用零個或多個篩選器進行功能檢測。 此外，過濾器可與多個設備組一起使用。 提AEM供預設篩選器，確定設備是否具有為組選擇的功能：

* CSS
* JPG和PNG影像
* JavaScript
* 設備旋轉

如果設備組未使用篩選器，則為組配置的選定功能是設備所需的唯一功能。

有關詳細資訊，請參見 [建立設備組篩選器](/help/sites-developing/groupfilters.md)。

#### 建立設備組 {#creating-a-device-group}

當安裝的組不符合您的要AEM求時建立設備組。

1. 在瀏覽器中，轉到 **工具** 控制台。
1. 在下面建立新頁面 **工具** > **移動** > **設備組**。 在 **建立頁** 對話框：

   * 作為 **標題** 輸入 `Special Phones`。

   * 作為 **名稱** 輸入 `special`。

   * 選擇 **移動設備組模板**。
   * 按一下&#x200B;**建立**。

1. 在CRXDE中，添加 **static.css** 包含以下設備組樣式的檔案 `/etc/mobile/groups/special` 的下界。

1. 開啟 **特殊電話** 的子菜單。
1. 要配置設備組，請按一下 **編輯** 按鈕 **設定**。
在 **常規** 頁籤：

   * **標題**:移動設備組的名稱。
   * **說明**:組的說明。
   * **用戶代理**:與設備匹配的用戶代理字串。 它是可選的，可以是規則運算式。 範例: `BlackBerryZ10`
   * **功能**:定義組是否可以處理影像、CSS、JavaScript或設備旋轉。
   * **最小螢幕寬度**&#x200B;和&#x200B;**高度**
   * **禁用模擬器**:在內容編輯期間啟用/禁用模擬器。

   在 **模擬器** 頁籤：

   * **模擬器**:選擇分配給此設備組的模擬器。

   在 **篩選器** 頁籤：

   * 要添加篩選器，請按一下添加項，然後從下拉清單中選擇篩選器。
   * 按過濾器的顯示順序計算過濾器。 當設備不符合篩選器的條件時，將不評估清單中後續的篩選器。



1. 按一下「確定」。

移動設備組配置對話框如下所示：

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### 每個設備組的自定義CSS {#custom-css-per-device-group}

如前所述，可以將自定義CSS與設備組頁關聯，與設計頁的CSS非常相似。此CSS用於影響頁面內容在作者和發佈時的設備組特定呈現。然後自動包括此CSS:

* 在此設備組使用的每個模擬器的作者實例的頁面中。
* 在發佈實例上的頁面中，如果請求的用戶代理與此特定設備組中的移動設備匹配。

## 伺服器端設備檢測 {#server-side-device-detection}

使用篩選器和設備規範庫來確定執行HTTP請求的設備的功能。

### 開發設備組篩選器 {#develop-device-group-filters}

建立設備組篩選器以定義一組設備功能要求。 根據需要建立任意數量的篩選器以針對所需的設備功能組。

設計篩選器，以便您可以使用它們的組合來定義權能組。 通常，不同設備組的功能會有重疊。 因此，您可能會將某些篩選器用於多個設備組定義。

建立篩選器後，可以在組配置中使用它。

有關資訊，請轉至 [建立設備組篩選器](/help/sites-developing/groupfilters.md)。

### 使用WURFL™資料庫 {#using-the-wurfl-database}

使AEM用截斷版本 [武爾夫](https://wurfl.sourceforge.net/)(TM)資料庫，以根據設備的User-Agent查詢設備功能（如螢幕解析度或javascript支援）。

WURFL™資料庫的XML代碼表示為以下節點 `/var/mobile/devicespecs` 通過分析 `wurfl.xml`檔案 `/libs/wcm/mobile/devicespecs/wurfl.xml.` 擴展到節點時， `cq-mobile-core` 綁定已啟動。

設備功能儲存為節點屬性，節點表示設備型號。 您可以使用查詢來檢索設備或用戶代理的功能。

隨著WURFL™資料庫的發展，您可能需要自定義或替換它。 要更新移動設備資料庫，您有以下選項：

* 如果您擁有允許此使用的許可證，請將檔案替換為最新版本。 請參見Installing a Different WURFL Database。
* 使用中提供的版AEM本並配置與User-Agent字串匹配且指向現有WURFL™設備的regexp。 請參閱 [添加基於regexp的用戶 — 代理匹配](#adding-a-regexp-based-user-agent-matching)。

#### 測試用戶代理到WURFL™功能的映射 {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

當設備訪問您的移動站點時，AEM檢測設備，根據其功能將其映射到設備組，併發送與設備組對應的頁面視圖。 匹配設備組提供必要的樣式資訊。 可以在「移動用戶 — 代理Test」頁上測試映射：

`https://localhost:4502/etc/mobile/useragent-test.html`

#### 安裝其他WURFL™資料庫 {#installing-a-different-wurfl-database}

隨附的截斷的WURFL™資料AEM庫是2011年8月30日之前的版本。 如果您的WURFL版本在2011年8月30日之後發佈，請確保您的使用符合您的許可證。

要安裝WURFL™資料庫：

1. 在CRXDE Lite中，建立以下資料夾： `/apps/wcm/mobile/devicespecs`
1. 將WURFL™檔案複製到資料夾。
1. 將檔案更名為 `wurfl.xml`。

自AEM動解析 `wurfl.xml` 檔案並更新下面的節點 `/var/mobile/devicespecs`。

>[!NOTE]
>
>啟用完整的WURFL™資料庫後，分析和激活可能需要幾分鐘時間。 您可以查看日誌以獲取進度資訊。

#### 添加基於regexp的用戶 — 代理匹配 {#adding-a-regexp-based-user-agent-matching}

在/apps/wcm/mobile/devices/wurfl/regexp下添加一個user-agent作為規則運算式，以指向現有的WURFL™設備類型。

1. 在 **CRXDE Lite**，在/apps/wcm/mobile/devices/regexp下建立節點，例如apple_ipad_ver1。
1. 將以下屬性添加到節點：

   * **regexp**:定義用戶代理的規則運算式，例如：。&#42;Mozilla。&#42;iPad.&#42;AppleWebKit。&#42;薩法里。&#42;
   * **設備ID**:在wurfl.xml中定義的設備ID，例如：apple_ipad_ver1

上述配置將使用戶代理與提供的規則運算式匹配的設備映射到appleipadver1 WURFL™設備ID（如果存在）。

## 客戶端設備檢測 {#client-side-device-detection}

本節介紹如何使用設備客戶端檢測來AEM優化頁面呈現或為客戶端提供備用網站版本。

AEM支援基於的設備客戶端檢測 `BrowserMap`。 `BrowserMap` 作為客戶端AEM庫在 `/etc/clientlibs/browsermap`。

`BrowserMap` 為您提供了三種策略，您可以使用這些策略為客戶提供備用網站，其使用順序如下：

1. [備用連結](#providing-alternate-links)
1. [設備組特定URL](#definingdevicegroupspecificurl)
1. [基於選擇器的URL](#defining-selector-based-urls)

>[!NOTE]
>
>有關客戶端庫整合的詳細資訊，請閱讀 [使用客戶端HTML庫](/help/sites-developing/clientlibs.md) 的子菜單。

### 提供備用連結 {#providing-alternate-links}

的 `PageVariantsProvider` OSGi服務能夠為屬於同一家族的站點生成備用連結。 為了配置要由服務考慮的站點， `cq:siteVariant` 節點必須添加到 `jcr:content` 從站點的根節點。

的 `cq:siteVariant` 節點需要具有以下屬性：

* `cq:childNodesMapTo`  — 確定子節點將映射到的連結元素的屬性；建議以這樣的方式組織網站的內容，以便根節點的子代表示全局網站語言變體的根(例如， `/content/mysite/en`。 `/content/mysite/de`)，在這種情況下， `cq:childNodesMapTo` 應該 `hreflang`;
* `cq:variantDomain`  — 表示 `Externalizer` 域將用於生成頁面變型絕對URL;如果未設定此值，則使用相對連結生成頁面變型；
* `cq:variantFamily`  — 指明此網站所屬的網站家族；同一網站的多個特定設備表示應屬於同一家庭；
* `media`  — 儲存連結元素的媒體屬性值；建議使用 `BrowserMap` 註冊 `DeviceGroups`，所以 `BrowserMap` 庫可以自動將客戶端轉發到網站的正確變型。

#### PageVariantsProvider和Externalizer {#pagevariantsprovider-and-externalizer}

當 `cq:variantDomain` 屬性 `cq:siteVariant` 節點不為空， `PageVariantsProvider` 服務將使用此值生成絕對連結，作為為 `Externalizer` 服務。 確保配置 `Externalizer` 服務以反映您的設定。

>[!NOTE]
>
>使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

### 定義設備組特定URL {#defining-a-device-group-specific-url}

如果不想使用備用連結，可以為每個連結配置全局URL `DeviceGroup`。 我們建議建立您自己的客戶端庫，以嵌入 `browsermap.standard` 客戶端庫，但重新定義設備組。

BrowserMap的設計方式是，通過建立和向Browser Map中添加同名的新設備組，可以覆蓋設備組定義 `BrowserMap` 自定義客戶端庫中的對象。

>[!NOTE]
>
>有關詳細資訊，請閱讀 [自定義瀏覽器映射](#creatingacustomisedbrowsermap) 的子菜單。

### 定義基於選擇器的URL {#defining-selector-based-urls}

如果以前沒有採用任何機制來指示替代地點 `BrowserMap`，然後選擇將使用 `DeviceGroups` 將添加到 `URL`s，在這種情況下，您應提供自己的Servlet來處理請求。

例如設備瀏覽 `www.example.com/index.html` 識別 `smartphone` 按瀏覽器映射轉發到 `www.example.com/index.smartphone.html.`

### 在頁面上使用BrowserMap {#using-browsermap-on-your-pages}

要在頁面中使用標準的BrowserMap客戶端庫，必須包括 `/libs/wcm/core/browsermap/browsermap.jsp` 檔案 `cq:include`頁面中的標籤 `head` 的子菜單。

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

除了 `BrowserMap` 客戶端庫 `JSP` 檔案，您還必須添加 `cq:deviceIdentificationMode` 字串屬性設定為 `client-side` 到 `jcr:content` 的子目錄下。

### 覆蓋BrowserMap的預設行為 {#overriding-browsermap-s-default-behaviour}

如果要自定義 `BrowserMap`  — 覆蓋 `DeviceGroups` 或添加更多探測器 — 然後應建立自己的客戶端庫，在其中嵌入 `browsermap.standard`客戶端庫。

此外，您必須手動調用 `BrowserMap.forwardRequest()` 方法 `JavaScript` 代碼。

>[!NOTE]
>
>有關客戶端庫整合的詳細資訊，請閱讀 [使用客戶端HTML庫](/help/sites-developing/clientlibs.md) 的子菜單。

建立自定義後 `BrowserMap` 客戶端庫，我們提出以下方法：

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

1. 包括 `broswermap.jsp` 檔案。

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 從某些頁面中排除BrowserMap {#excluding-browsermap-from-certain-pages}

如果要從某些不需要客戶端檢測的頁面中排除BrowserMap庫，則可以添加請求屬性：

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

這將使 `/libs/wcm/core/browsermap/browsermap.jsp` 指令碼，將元標籤添加到將生成 `BrowserMap` 不執行任何檢測：

```xml
<meta name="browsermap.enabled" content="false">
```

### 測試網站的特定版本 {#testing-a-specific-version-of-a-web-site}

通常，BrowserMap指令碼始終將訪問者重定向到網站的最合適版本，通常在需要時將訪問者重定向到案頭或移動站點。

通過添加以下命令，您可以強制任何請求的設備以test網站的特定版本 `device` 的子菜單。 以下URL將呈現Geometrixx Outdoors網站的移動版本。

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>的 `wcmmode` 參數設定為 `disabled` 以模擬發佈實例的行為。

覆蓋的設備值儲存在Cookie中，這樣您就可以瀏覽您的網站，而無需添加 `device` 參數 `URL`。

因此，你需要調用 `URL` 和 `device` 設定為 `browser` 以便返回網站的案頭版本。

>[!NOTE]
>
>瀏覽器映射將覆蓋的設備值儲存在名為 `BMAP_device`。 刪除此Cookie將確保CQ根據您當前的設備（如案頭或移動設備）提供相應版本的網站。

## 移動請求處理 {#mobile-request-processing}

按如AEM下方式處理由屬於觸摸設備組的移動設備發出的請求：

1. iPad向發佈實例AEM發送請求，例如 `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. 確AEM定所請求頁面的站點是否是移動站點(通過檢查第一級頁面 `/content/geometrixx_mobile` 擴展移動頁面元件)。 如果是：
1. 根AEM據請求標頭中的User-Agent查找設備功能。
1. 將AEM設備功能映射到設備組並設定 `touch` 作為設備組選擇器。
1. 將AEM請求重定向到 `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. 向AEMiPad發送響應：

   * `products.touch.html` 是平易近人的。
   * 呈現元件使用選擇器來調整呈現。
   * 自AEM動將mobile選擇器添加到頁面中的所有內部連結。

### 統計資料 {#statistics}

您可以獲取有關移動設備向伺服器發出的請AEM求數的統計資訊。 可以細分請求數：

* 每設備組和設備
* 每年，月和日

要查看統計資訊，請執行以下操作：

1. 轉到 **工具** 控制台。
1. 開啟 **設備統計** 頁 **工具** > **移動**。
1. 按一下該連結可查看特定年份、月份或日的統計資訊。

的 **統計** 的下一頁。

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>的 **統計** 首次訪問並檢測到移動設AEM備時建立頁面。 在此之前，它不可用。

如果需要在統計資訊中生成條目，可以按如下方式進行：

1. 使用移動設備或模擬器(例如，Firefox上的https://chrispederick.com/work/user-agent-switcher/)。
1. 通過禁用創作模式(例如：
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

的 **統計** 的子菜單。

### 支援「向朋友發送連結」連結的頁面快取 {#supporting-page-caching-for-send-link-to-a-friend-links}

Dispatcher上通常可訪問移動頁面，因為為設備組呈現的頁面在頁面URL中由設備組選擇器（例如）區分 `/content/mobilepage.touch.html`。 對沒有選擇器的移動頁面的請求從不被快取，如在這種情況下，設備檢測操作並最終重定向到匹配設備組（或「無匹配」）。 由連結重寫器處理用設備組選擇器呈現的移動頁面，該連結重寫器重寫頁面內的所有連結以同時包含設備組選擇器，從而防止對已限定頁面上的每次按一下重新執行設備檢測。

因此，您可能會遇到以下情形：

用戶Alice被重定向到 `coolpage.feature.html`，並將該URL發送給朋友Bob,Bob將與位於 `touch` 設備組。

如果 `coolpage.feature.html` 從前端快取中提供，AEM無法分析請求以發現移動選擇器與新的User-Agent不匹配，Bob得到錯誤的表示。

要解決此問題，您可以在頁面上包含一個簡單的選擇UI，最終用戶可以覆蓋由選擇的設備AEM組。 在上例中，頁面上的連結（或表徵圖）允許最終用戶切換到 `coolpage.touch.html` 如果他認為他的裝置足夠好的話。
