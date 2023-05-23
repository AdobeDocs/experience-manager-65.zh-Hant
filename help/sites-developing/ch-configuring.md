---
title: 設定 ContextHub
seo-title: Configuring ContextHub
description: 瞭解如何配置上下文中心。
seo-description: Learn how to configure Context Hub.
uuid: f2988bb9-6878-42a2-bb51-c3f8683248c5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 61208bd5-475b-40be-ba00-31bbbc952adf
source-git-commit: 78ec31362f3aceb5cfc9cc0735bccb88082b8e2d
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 1%

---

# 設定 ContextHub {#configuring-contexthub}

ContextHub是用於儲存、操作和呈現上下文資料的框架。 有關ContextHub的詳細資訊，請參閱 [開發者文檔](/help/sites-developing/contexthub.md)。 ContextHub替換 [客戶端上下文](/help/sites-administering/client-context.md) 的子菜單。

配置 [上下文中心](/help/sites-developing/contexthub.md) 工具欄，用於控制它是否出現在預覽模式、建立ContextHub儲存庫以及使用「觸控優化」用戶介面添加用戶介面模組。

## 禁用ContextHub {#disabling-contexthub}

預設情況下，在安裝中啟AEM用ContextHub。 可以禁用ContextHub，以阻止它載入js/css和初始化。

<!--
There are two options to disable ContextHub:

* Edit the ContextHub's configuration and check the option **Disable ContextHub**

    1. In the rail click or tap **Tools &gt; Sites &gt; ContextHub**
    1. Click or tap the appropriate **Configuration Container**
    1. Select the **ContextHub Configuration** and click or tap **Edit Selected Element**
    1. Click or tap **Disable ContextHub** and click or tap **Save**

or
-->

* 使用CRXDE Lite設定屬性 `disabled` 至 **真** 在 `/libs/settings/cloudsettings/legacy/contexthub`

>[!NOTE]
>
>[由於6.4中的AEM儲存庫重組，](/help/sites-deploying/repository-restructuring.md) ContextHub配置的位置從 `/etc/cloudsettings` 至：
>
>* `/libs/settings/cloudsettings`
>* `/conf/global/settings/cloudsettings`
>* `/conf/<tenant>/settings/cloudsettings`


## 顯示和隱藏ContextHub UI {#showing-and-hiding-the-contexthub-ui}

配置AdobeGranite ContextHub OSGi服務以顯示或隱藏 [上下文集線器UI](/help/sites-authoring/ch-previewing.md) 在你的網頁上。 此服務的PID為 `com.adobe.granite.contexthub.impl.ContextHubImpl.`

要配置服務，您可以使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或使用 [儲存庫中的JCR節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* **Web控制台：** 要顯示UI，請選擇「顯示UI」屬性。 要隱藏UI，請清除「隱藏UI」屬性。
* **JCR節點：** 要顯示UI，請設定布爾值 `com.adobe.granite.contexthub.show_ui` 屬性 `true`。 要隱藏UI，請將屬性設定為 `false`。

當顯示ContextHub UI時，它只出現在作者實例AEM的頁面上。 UI不出現在發佈實例的頁面上。

## 添加ContextHub UI模式和模組 {#adding-contexthub-ui-modes-and-modules}

在預覽模式下配置ContextHub工具欄中顯示的UI模式和模組：

* UI模式：相關模組組
* 模組：用於從儲存中公開上下文資料並使作者能夠處理上下文的小部件

UI模式在工具欄左側顯示為一系列表徵圖。 選中後，UI模式的模組將顯示在右側。

![chlimage_1-319](assets/chlimage_1-319.png)

表徵圖是 [Coral UI表徵圖庫](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)。

### 添加UI模式 {#adding-a-ui-mode}

將UI模式添加到與ContextHub模組相關的組。 建立UI模式時，將提供顯示在ContextHub工具欄中的標題和表徵圖。

1. 在Experience Manager導軌上，按一下或點擊「工具」>「站點」>「上下文集線器」。
1. 按一下或點擊預設配置容器。
1. 按一下或點擊「Context Hub Configuration（上下文集線器配置）」。
1. 按一下或點擊「Create（建立）」按鈕，然後按一下或點擊「Context Hub UI Mode（上下文中心UI模式）」。

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. 為以下屬性提供值：

   * UI模式標題：標識UI模式的標題
   * 模式表徵圖：選擇器 [Coral UI表徵圖](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) 例如 `coral-Icon--user`
   * 已啟用：選擇以在ContextHub工具欄中顯示UI模式

1. 按一下或點擊「保存」。

### 添加UI模組 {#adding-a-ui-module}

將ContextHub UI模組添加到UI模式，以便它顯示在用於預覽頁面內容的ContextHub工具欄中。 添加UI模組時，將建立在ContextHub中註冊的模組類型實例。 要添加UI模組，必須知道關聯模組類型的名稱。

提AEM供基本UI模組類型以及幾種示例UI模組類型，您可以在這些類型上基於UI模組。 下表對每個選項提供了簡要說明。 有關開發自定義UI模組的資訊，請參見 [建立ContextHub UI模組](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

UI模組屬性包括詳細配置，您可以在其中為模組特定的屬性提供值。 您以JSON格式提供詳細配置。 表中的「模組類型」列提供了指向每個UI模組類型所需JSON代碼資訊的連結。

| 模組類型 | 說明 | 存放 |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | 通用UI模組類型 | 在UI模組屬性中配置 |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | 顯示有關瀏覽器的資訊 | 捨費 |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | 顯示日期和時間資訊 | 日期 |
| [contexthub設備](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | 顯示客戶端設備 | 模擬器 |
| [contexthub.位置](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | 顯示客戶端的經緯度以及地圖上的位置。 允許您更改位置。 | 地理位置 |
| [contexthub.screen orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | 顯示設備的螢幕方向（橫向或縱向） | 模擬器 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | 顯示有關頁標籤的統計資訊 | 塔格雲 |
| [花崗岩/輪廓](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | 顯示當前用戶的配置檔案資訊，包括authorizedID、displayName和familyName。 可以更改displayName和familyName的值。 | 側面像 |

1. 在Experience Manager欄上，按一下或按一下「工具」>「站點」>「上下文集線」。
1. 按一下或點擊要添加UI模組的配置容器。
1. 按一下或鍵入要添加UI模組的ContextHub配置。
1. 按一下或點擊要添加UI模組的UI模式。
1. 按一下或點擊「Create（建立）」按鈕，然後按一下或點擊「ContextHub UI Module（一般）」。

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. 為以下屬性提供值：

   * UI模組標題：標識UI模組的標題
   * 模組類型：模組類型
   * 已啟用：選擇以在ContextHub工具欄中顯示UI模組

1. （可選）要覆蓋預設儲存配置，請輸入JSON對象以配置UI模組。
1. 按一下或點擊「保存」。

## 建立ContextHub儲存 {#creating-a-contexthub-store}

建立上下文中心儲存以保留用戶資料並根據需要訪問資料。 ContextHub儲存基於註冊的儲存候選。 建立儲存區時，需要註冊儲存區候選區的storeType值。 (請參閱 [建立自定義儲存候選](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)。)

### 詳細儲存配置 {#detailed-store-configuration}

配置儲存時，「詳細資訊配置」屬性允許您提供特定於儲存的屬性的值。 該值基於 `config` 儲存的參數 `init` 的子菜單。 因此，是否需要提供此值和值的格式取決於儲存。

Detail Configuration屬性的值是 `config` JSON格式的對象。

### 範例商店候選者 {#sample-store-candidates}

提AEM供以下樣例儲存候選項，您可以在其上建立儲存。

| 儲存類型 | 說明 |
|---|---|
| [aem分割](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | 儲存已解析和未解析的ContextHub段。 自動從ContextHub SegmentManager檢索段 |
| [aem.resolved段](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | 儲存當前解析的段。 偵聽ContextHub SegmentManager服務以自動更新儲存 |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | 儲存瀏覽器位置的經緯度。 |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | 儲存瀏覽器位置的當前日期、時間和季節 |
| [花崗岩。模擬器](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | 定義多個設備的屬性和功能，並檢測當前客戶端設備 |
| [contexthub.generic.jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | 從JSONP服務檢索和儲存資料 |
| [花崗岩/輪廓](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | 儲存當前用戶的配置檔案資料 |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | 儲存有關客戶端的資訊，如設備資訊、瀏覽器類型和窗口方向 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | 儲存頁面標籤和標籤計數 |

1. 在Experience Manager欄上，按一下或按一下「工具」>「站點」>「上下文集線」。
1. 按一下或點擊預設配置容器。
1. 按一下或點擊「Contexthub Configuration（上下文配置）」
1. 要添加儲存區，請按一下或點擊「建立」表徵圖，然後按一下或點擊「ContexHub儲存區配置」。

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. 提供基本配置屬性的值，然後按一下或點擊「下一步」：

   * **配置標題：** 標識儲存的標題
   * **儲存類型：** 要作為儲存基礎的儲存候選的storeType屬性的值
   * **必需：** 選擇
   * **已啟用：** 選擇以啟用儲存

1. （可選）要覆蓋預設儲存配置，請在「詳細配置(JSON)」框中輸入JSON對象。
1. 按一下或點擊「保存」。

## 示例：使用JSONP服務  {#example-using-a-jsonp-service}

此示例說明如何配置儲存並在UI模組中顯示資料。 在本示例中，jsontest.com站點的MD5服務用作儲存的資料源。 服務以JSON格式返回給定字串的MD5哈希代碼。

配置contexthub.generic-jsonp儲存，以便它儲存用於服務呼叫的資料 `https://md5.jsontest.com/?text=%22text%20to%20md5%22`。 服務返回UI模組中顯示的以下資料：

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### 建立contexthub.generic-jsonp儲存 {#creating-a-contexthub-generic-jsonp-store}

contexthub.generic-jsonp示例儲存候選項使您能夠從返回JSON資料的JSONP服務或Web服務中檢索資料。 對於此儲存候選，請使用儲存配置來提供有關要使用的JSONP服務的詳細資訊。

的 [初始化](/help/sites-developing/contexthub-api.md#init-name-config) 函式 `ContextHub.Store.JSONPStore` Javascript類定義 `config` 初始化此儲存候選項的對象。 的 `config` 對象包含 `service` 包含有關JSONP服務的詳細資訊的對象。 要配置儲存，請提供 `service` JSON格式的對象，作為Detail Configuration屬性的值。

要保存jsontest.com站點的MD5服務中的資料，請使用中的過程 [建立ContextHub儲存](/help/sites-developing/ch-configuring.md#creating-a-contexthub-store) 使用以下屬性：

* **配置標題：** md5
* **儲存類型：** contexthub.generic.jsonp
* **必需：** 選擇
* **已啟用：** 選擇
* **詳細資料組態 (JSON):**

   ```xml
   {
    "service": {
    "jsonp": false,
    "timeout": 1000,
    "ttl": 1800000,
    "secure": false,
    "host": "md5.jsontest.com",
    "port": 80,
    "params":{
    "text":"text to md5"
        }
      }
    }
   ```

### 為md5資料添加UI模組 {#adding-a-ui-module-for-the-md-data}

將UI模組添加到ContextHub工具欄，以顯示儲存在示例md5儲存中的資料。 在本示例中，contexthub.base模組用於生成以下UI模組：

![chlimage_1-323](assets/chlimage_1-323.png)

使用中的過程 [添加UI模組](#adding-a-ui-module) 將UI模組添加到現有UI模式，如示例Perona UI模式。 對於UI模組，請使用以下屬性值：

* **UI模組標題：** MD5
* **模組類型：** contexthub.base
* **詳細資料組態 (JSON):**

   ```xml
   {
    "icon": "coral-Icon--data",
    "title": "MD5 Converstion",
    "storeMapping": { "md5": "md5" },
    "template": "<p> {{md5.original}}</p>;
                 <p>{{md5.md5}}</p>"
   }
   ```

## 調試ContextHub {#debugging-contexthub}

可以啟用ContextHub的調試模式，以允許進行故障排除。 可以通過ContextHub配置或通過CRXDE啟用調試模式。

### 通過配置 {#via-the-configuration}

編輯ContextHub的配置並檢查選項 **調試**

1. 在滑軌中按一下或點擊 **「工具」>「站點」>「上下文中心」**
1. 按一下或點擊預設 **配置容器**
1. 選擇 **ContextHub配置** 點擊 **編輯選定元素**
1. 按一下或點擊 **調試** 點擊 **保存**

### 通過CRXDE {#via-crxde}

使用CRXDE Lite設定屬性 `debug` 至 **真** 下：

* `/conf/global/settings/cloudsettings` 或
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>對於仍位於其舊路徑下的ContextHub配置，設定 `debug property` 是 `/libs/settings/cloudsettings/legacy/contexthub`。

### 靜默模式 {#silent-mode}

靜默模式會隱藏所有調試資訊。 與普通調試選項不同，靜默模式是全局設定，它取代了ContextHub配置級別上的任何調試設定。

這對您的發佈實例非常有用，因為您根本不需要任何調試資訊。 因為它是全局設定，所以通過OSGi啟用它。

1. 開啟 **Adobe Experience ManagerWeb控制台配置** 在 `http://<host>:<port>/system/console/configMgr`
1. 搜索 **Adobe花崗岩上下文樞紐**
1. 按一下配置 **Adobe花崗岩上下文樞紐** 編輯其屬性
1. 選中選項 **靜默模式** 按一下 **保存**

## 升級後恢復ContextHub配置 {#recovering-contexthub-configurations-after-upgrading}

當 [升AEM級](/help/sites-deploying/upgrade.md) 執行時，將備份ContextHub配置並將其儲存在安全位置。 在升級過程中，將安裝預設的ContextHub配置，以替換現有配置。 需要備份以保留您所做的任何更改或添加。

ContextHub配置儲存在名為 `contexthub` 在以下節點下：

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

升級後，備份儲存在名為 `contexthub` 位於以下節點下：

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` 或
`/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`

的 `yyyymmdd` 節點名稱的一部分是執行升級的日期。

要恢復ContextHub配置，請使用CRXDE Lite從以下位置複製表示儲存、UI模式和UI模組的節點 `default-pre-upgrade_yyyymmdd_xxxxxx` 節點到以下位置：

* `/conf/global/settings/cloudsettings` 或
* `/conf/<tenant>/settings/cloudsettings`
