---
title: 設定 ContextHub
seo-title: Configuring ContextHub
description: 了解如何設定Context Hub。
seo-description: Learn how to configure Context Hub.
uuid: f2988bb9-6878-42a2-bb51-c3f8683248c5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 61208bd5-475b-40be-ba00-31bbbc952adf
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1842'
ht-degree: 1%

---

# 設定 ContextHub {#configuring-contexthub}

ContextHub是儲存、操控和呈現內容資料的架構。 如需ContextHub的詳細資訊，請參閱 [開發人員檔案](/help/sites-developing/contexthub.md). ContextHub取代 [用戶端內容](/help/sites-administering/client-context.md) 在觸控式UI中。

設定 [ContextHub](/help/sites-developing/contexthub.md) 工具列，控制其是否顯示在預覽模式中、建立ContextHub存放區，以及使用觸控最佳化UI新增UI模組。

## 停用ContextHub {#disabling-contexthub}

依預設，AEM安裝中會啟用ContextHub。 您可以停用ContextHub，以防止其載入js/css及初始化。 停用ContextHub有兩個選項：

* 編輯ContextHub的設定並核取選項 **停用ContextHub**

   1. 在邊欄中按一下或點選 **工具>網站> ContextHub**
   1. 按一下或點選預設值 **組態容器**
   1. 選取 **ContextHub設定** 按一下或點選 **編輯所選元素**
   1. 按一下或點選 **停用ContextHub** 按一下或點選 **儲存**

或

* 使用CRXDE Lite來設定屬性 `disabled` to **true** 在 `/libs/settings/cloudsettings`

>[!NOTE]
>
>[由於AEM 6.4的存放庫重新調整架構，](/help/sites-deploying/repository-restructuring.md) ContextHub設定的位置已從 `/etc/cloudsettings` 至：
>
>* `/libs/settings/cloudsettings`
>* `/conf/global/settings/cloudsettings`
>* `/conf/<tenant>/settings/cloudsettings`


## 顯示和隱藏ContextHub UI {#showing-and-hiding-the-contexthub-ui}

設定AdobeGranite ContextHub OSGi服務以顯示或隱藏 [ContextHub UI](/help/sites-authoring/ch-previewing.md) 頁面上。 此服務的PID為 `com.adobe.granite.contexthub.impl.ContextHubImpl.`

若要設定服務，您可以使用 [Web主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或使用 [儲存庫中的JCR節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* **Web控制台：** 若要顯示UI，請選取「顯示UI」屬性。 若要隱藏UI，請清除「隱藏UI」屬性。
* **JCR節點：** 若要顯示UI，請設定布林值 `com.adobe.granite.contexthub.show_ui` 屬性 `true`. 若要隱藏UI，請將屬性設為 `false`.

顯示ContextHub UI時，它只會顯示在AEM製作例項的頁面上。 UI不會出現在發佈執行個體的頁面上。

## 新增ContextHub UI模式和模組 {#adding-contexthub-ui-modes-and-modules}

設定在「預覽」模式中顯示於ContextHub工具列的UI模式和模組：

* UI模式：相關模組組
* 模組：從儲存區公開內容資料並讓作者操控內容的介面工具集

UI模式會以一系列圖示的形式顯示在工具列左側。 選取後，UI模式的模組會顯示在右側。

![chlimage_1-319](assets/chlimage_1-319.png)

圖示是 [Coral UI圖示程式庫](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### 新增UI模式 {#adding-a-ui-mode}

新增UI模式以將相關的ContextHub模組分組。 建立UI模式時，您會提供顯示在ContextHub工具列中的標題和圖示。

1. 在Experience Manager邊欄中，按一下或點選「工具>網站>內容中樞」。
1. 按一下或點選預設的「設定容器」。
1. 按一下或點選「Context Hub Configuration」。
1. 按一下或點選「建立」按鈕，然後按一下或點選「內容中樞UI模式」。

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. 提供下列屬性的值：

   * UI模式標題：識別UI模式的標題
   * 模式表徵圖：的選取器 [Coral UI圖示](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) 例如 `coral-Icon--user`
   * 已啟用：選取「 」，在ContextHub工具列中顯示UI模式

1. 按一下或點選「儲存」。

### 新增UI模組 {#adding-a-ui-module}

將ContextHub UI模組新增至UI模式，使其顯示在ContextHub工具列中以預覽頁面內容。 新增UI模組時，您會建立已向ContextHub註冊的模組類型例項。 若要新增UI模組，您必須知道相關模組類型的名稱。

AEM提供基本UI模組類型以及數種範例UI模組類型，您可以依據這些類型來建立UI模組。 下表提供每個項目的簡短說明。 如需開發自訂UI模組的相關資訊，請參閱 [建立ContextHub UI模組](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

UI模組屬性包含詳細設定，您可在此提供模組特定屬性的值。 您提供JSON格式的詳細設定。 表格中的「模組類型」欄提供每個UI模組類型所需JSON程式碼的相關資訊連結。

| 模組類型 | 說明 | 存放 |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | 一般UI模組類型 | 在UI模組屬性中設定 |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | 顯示瀏覽器的相關資訊 | surferinfo |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | 顯示日期和時間資訊 | 日期時間 |
| [contexthub.device](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | 顯示客戶端設備 | 模擬器 |
| [contexthub.location](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | 顯示用戶端的經緯度，以及地圖上的位置。 可讓您變更位置。 | 地理位置 |
| [contexthub.screen-orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | 顯示裝置的螢幕方向（橫向或直向） | 模擬器 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | 顯示頁面標籤的統計資料 | tagcloud |
| [granite.profile](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | 顯示當前用戶的配置檔案資訊，包括可授權的ID、displayName和familyName。 您可以更改displayName和familyName的值。 | 側面像 |

1. 在Experience Manager邊欄中，按一下或點選「工具>網站> ContextHub」。
1. 按一下或點選「設定容器」，以新增UI模組。
1. 按一下或輸入您要新增UI模組的ContextHub設定。
1. 按一下或點選您要新增UI模組的UI模式。
1. 按一下或點選「建立」按鈕，然後按一下或點選「 ContextHub UI模組（一般）」。

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. 提供下列屬性的值：

   * UI模組標題：識別UI模組的標題
   * 模組類型：模組類型
   * 已啟用：選取「 」，在ContextHub工具列中顯示UI模組

1. （選用）若要覆寫預設的存放區設定，請輸入JSON物件以設定UI模組。
1. 按一下或點選「儲存」。

## 建立ContextHub存放區 {#creating-a-contexthub-store}

建立Context Hub存放區以保留使用者資料並視需要存取資料。 ContextHub存放區是根據已註冊的存放區候選項。 建立商店時，需要註冊商店候選商店的storeType值。 (請參閱 [建立自訂商店候選項](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).)

### 詳細的儲存配置 {#detailed-store-configuration}

配置儲存時，「詳細配置」屬性允許您為儲存特定屬性提供值。 值以 `config` 商店的參數 `init` 函式。 因此，您是否需要提供此值和值的格式取決於儲存區。

Detail Configuration屬性的值是 `config` 物件。

### 範例商店候選者 {#sample-store-candidates}

AEM提供下列範例存放區候選項，供您建立存放區。

| 商店類型 | 說明 |
|---|---|
| [aem.segmentation](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | 儲存已解析和未解析的ContextHub區段。 自動從ContextHub SegmentManager中擷取區段 |
| [aem.resolvedsegments](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | 儲存目前解析的區段。 監聽ContextHub SegmentManager服務以自動更新儲存 |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | 儲存瀏覽器位置的經緯度。 |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | 儲存瀏覽器位置的目前日期、時間和季數 |
| [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | 定義多個設備的屬性和功能，並檢測當前客戶端設備 |
| [contexthub.generic-jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | 從JSONP服務擷取和儲存資料 |
| [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | 儲存目前使用者的設定檔資料 |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | 儲存用戶端的相關資訊，例如裝置資訊、瀏覽器類型和視窗方向 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | 儲存頁面標籤和標籤計數 |

1. 在Experience Manager邊欄中，按一下或點選「工具>網站> ContextHub」。
1. 按一下或點選預設設定容器。
1. 按一下或點選「Contexthub設定」
1. 若要新增商店，請按一下或點選「建立」圖示，然後按一下或點選「 ContexHub商店設定」。

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. 提供基本配置屬性的值，然後按一下或點選「下一步」：

   * **配置標題：** 識別商店的標題
   * **商店類型：** 要作為儲存基礎的儲存候選項的storeType屬性的值
   * **必要：** 選擇
   * **已啟用：** 選擇以啟用儲存

1. （選用）若要覆寫預設的存放區設定，請在「詳細設定(JSON)」方塊中輸入JSON物件。
1. 按一下或點選「儲存」。

## 範例：使用JSONP服務  {#example-using-a-jsonp-service}

此範例說明如何設定儲存區，以及在UI模組中顯示資料。 在此示例中，jsontest.com站點的MD5服務用作儲存的資料源。 服務會傳回指定字串的MD5雜湊代碼（JSON格式）。

已設定contexthub.generic-jsonp存放區，以便儲存服務呼叫的資料 `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. 服務會傳回下列顯示在UI模組中的資料：

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### 建立contexthub.generic-jsonp商店 {#creating-a-contexthub-generic-jsonp-store}

contexthub.generic-jsonp範例存放區候選項可讓您從傳回JSON資料的JSONP服務或網站服務擷取資料。 對於此儲存候選項，請使用儲存配置提供有關要使用的JSONP服務的詳細資訊。

此 [init](/help/sites-developing/contexthub-api.md#init-name-config) 函式 `ContextHub.Store.JSONPStore` Javascript類別定義 `config` 初始化此儲存候選項的對象。 此 `config` 物件包含 `service` 包含JSONP服務詳細資訊的物件。 若要設定商店，請提供 `service` JSON格式的物件，作為「詳細設定」屬性的值。

若要從jsontest.com網站的MD5服務儲存資料，請使用 [建立ContextHub存放區](/help/sites-developing/ch-configuring.md#creating-a-contexthub-store) 使用下列屬性：

* **配置標題：** md5
* **商店類型：** contexthub.generic-jsonp
* **必要：** 選擇
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

### 新增md5資料的UI模組 {#adding-a-ui-module-for-the-md-data}

將UI模組新增至ContextHub工具列，以顯示儲存在範例md5商店中的資料。 在此範例中，contexthub.base模組用於產生下列UI模組：

![chlimage_1-323](assets/chlimage_1-323.png)

在 [新增UI模組](#adding-a-ui-module) 若要將UI模組新增至現有的UI模式，例如範例Perona UI模式。 對於UI模組，請使用下列屬性值：

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

## 偵錯ContextHub {#debugging-contexthub}

ContextHub的除錯模式可啟用，以允許疑難排解。 偵錯模式可透過ContextHub設定或透過CRXDE啟用。

### 透過設定 {#via-the-configuration}

編輯ContextHub的設定並核取選項 **除錯**

1. 在邊欄中按一下或點選 **工具>網站> ContextHub**
1. 按一下或點選預設值 **組態容器**
1. 選取 **ContextHub設定** 按一下或點選 **編輯所選元素**
1. 按一下或點選 **除錯** 按一下或點選 **儲存**

### 通過CRXDE {#via-crxde}

使用CRXDE Lite來設定屬性 `debug` to **true** 在下：

* `/conf/global/settings/cloudsettings` 或
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>若為ContextHub設定，請使用設定 `debug property` 為 `/libs/settings/cloudsettings/legacy/contexthub`.

### 靜默模式 {#silent-mode}

靜默模式隱藏所有調試資訊。 與可針對每個ContextHub配置獨立設定的一般除錯選項不同，靜默模式是全局設定，在ContextHub配置級別上取代任何調試設定。

這對您的發佈執行個體很實用，因為您完全不需要任何除錯資訊。 因為這是全域設定，所以會透過OSGi啟用。

1. 開啟 **Adobe Experience Manager Web主控台設定** at `http://<host>:<port>/system/console/configMgr`
1. 搜尋 **AdobeGranite ContextHub**
1. 按一下設定 **AdobeGranite ContextHub** 編輯其屬性
1. 核取選項 **靜默模式** 按一下 **儲存**

## 升級後恢復ContextHub配置 {#recovering-contexthub-configurations-after-upgrading}

當 [升級至AEM](/help/sites-deploying/upgrade.md) 執行後， ContextHub配置會備份並儲存在安全位置。 在升級期間，會安裝預設的ContextHub設定，取代現有設定。 必須進行備份，才能保留您所做的任何更改或添加。

ContextHub設定儲存在名為 `contexthub` 在以下節點下：

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

升級後，備份儲存在名為 `contexthub` 在名為的節點下：

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` 或
`/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`

此 `yyyymmdd` 節點名稱的一部分是執行升級的日期。

若要復原ContextHub設定，請使用CRXDE Lite，從下方複製代表您商店、UI模式和UI模組的節點 `default-pre-upgrade_yyyymmdd_xxxxxx` 節點至下方：

* `/conf/global/settings/cloudsettings` 或
* `/conf/<tenant>/settings/cloudsettings`
