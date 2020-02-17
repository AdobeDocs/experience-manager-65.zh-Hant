---
title: 設定ContextHub
seo-title: 設定ContextHub
description: 瞭解如何設定內容中樞。
seo-description: 瞭解如何設定內容中樞。
uuid: f2988bb9-6878-42a2-bb51-c3f8683248c5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: e37ff1c9e657c580c607f2656adca01a2b39f81f

---


# 設定ContextHub {#configuring-contexthub}

ContextHub是儲存、控制和呈現上下文資料的架構。 如需ContextHub的詳細資訊，請參閱開發 [人員檔案](/help/sites-developing/contexthub.md)。 ContextHub會取 [代觸控UI中的](/help/sites-administering/client-context.md) 「用戶端內容」。

設定 [](/help/sites-developing/contexthub.md) ContextHub工具列以控制它是否出現在「預覽」模式中、建立ContextHub儲存區，並使用「最佳化觸控式」UI新增UI模組。

## 停用ContextHub {#disabling-contexthub}

依預設，ContextHub會在AEM安裝中啟用。 ContextHub可停用，以防止它載入js/css並初始化。 要禁用ContextHub，有兩個選項：

* 編輯ContextHub的設定並勾選「停用ContextHub」 **選項**

   1. 在邊欄中按一下或點選「工 **具>網站> ContextHub」**
   1. 按一下或點選預設的「設 **定容器」**
   1. 選取「 **ContextHub設定」** ，然後按一下或點選「編 **輯選取的元素」**
   1. 按一下或點選「 **停用ContextHub** 」，然後按一下或點選「 **儲存」**

或

* 使用CRXDE Lite將屬性設 `disabled` 為 **true** , `/libs/settings/cloudsettings`

>[!NOTE]
>
>[由於AEM 6.4中的儲存庫重組](/help/sites-deploying/repository-restructuring.md) ,ContextHub組態的位置從 `/etc/cloudsettings` 變更為：
>
> * `/libs/settings/cloudsettings`
> * `/conf/global/settings/cloudsettings`
> * `/conf/<tenant>/settings/cloudsettings`


## 顯示和隱藏ContextHub UI {#showing-and-hiding-the-contexthub-ui}

設定Adobe Granite ContextHub OSGi服務，在您的頁面上顯示或 [隱藏ContextHub](/help/sites-authoring/ch-previewing.md) UI。 此服務的PID是 `com.adobe.granite.contexthub.impl.ContextHubImpl.`

要配置服務，您可以使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ，或在儲存庫 [中使用JCR節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* **** Web控制台：若要顯示UI，請選取「顯示UI」屬性。 若要隱藏UI，請清除「隱藏UI」屬性。
* **** JCR節點：若要顯示UI，請將布林屬 `com.adobe.granite.contexthub.show_ui` 性設為 `true`。 若要隱藏UI，請將屬性設為 `false`。

當顯示ContextHub UI時，它只會出現在AEM作者例項的頁面上。 UI不會顯示在發佈例項的頁面上。

## 添加ContextHub UI模式和模組 {#adding-contexthub-ui-modes-and-modules}

在「預覽」模式下配置ContextHub工具列中顯示的UI模式和模組：

* UI模式：相關模組組
* 模組：可從商店公開內容資料並讓作者控制內容的Widget

UI模式會以一系列圖示的形式出現在工具列的左側。 選取後，UI模式的模組會出現在右側。

![chlimage_1-319](assets/chlimage_1-319.png)

圖示是 [Coral UI圖示庫的參考](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)。

### 新增UI模式 {#adding-a-ui-mode}

新增UI模式至群組相關的ContextHub模組。 當您建立UI模式時，您會提供顯示在ContextHub工具列中的標題和圖示。

1. 在Experience manager邊欄上，按一下或點選「工具>網站>內容中樞」。
1. 按一下或點選預設的「設定容器」。
1. 按一下或點選「內容中樞設定」。
1. 按一下或點選「建立」按鈕，然後按一下或點選「內容中樞UI模式」。

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. 提供下列屬性的值：

   * UI模式標題：識別UI模式的標題
   * 模式圖示：例如，要使 [用的Coral UI圖示](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) (Coral UI)選擇器 `coral-Icon--user`
   * 啟用：選擇以在ContextHub工具列中顯示UI模式

1. 按一下或點選「儲存」。

### 添加UI模組 {#adding-a-ui-module}

將ContextHub UI模組新增至UI模式，以便顯示在ContextHub工具列中，以預覽頁面內容。 當您新增UI模組時，您會建立已在ContextHub中註冊的模組類型例項。 要添加UI模組，您必須知道關聯模組類型的名稱。

AEM提供基本UI模組類型以及數種範例UI模組類型，您可依此類型建立UI模組。 下表提供每個表格的簡要說明。 如需開發自訂UI模組的詳細資訊，請參 [閱建立ContextHub UI模組](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

UI模組屬性包括詳細配置，您可以在其中為模組特定屬性提供值。 您提供JSON格式的詳細設定。 表格中的「模組類型」欄提供每個UI模組類型所需JSON程式碼的相關資訊連結。

| 模組類型 | 說明 | 存放 |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | 通用UI模組類型 | 在UI模組屬性中配置 |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | 顯示瀏覽器的相關資訊 | surferinfo |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | 顯示日期和時間資訊 | 日期時間 |
| [contexthub.device](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | 顯示客戶端設備 | 模擬器 |
| [contexthub.location](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | 顯示用戶端的經緯度，以及地圖上的位置。 可讓您變更位置。 | 地理位置 |
| [contexthub.screen-orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | 顯示裝置的螢幕方向（橫向或縱向） | 模擬器 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | 顯示頁面標籤的統計資料 | tagcloud |
| [granite.profile](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | 顯示目前使用者的設定檔資訊，包括authorizedID、displayName和familyName。 可以更改displayName和familyName的值。 | 側面像 |

1. 在Experience manager邊欄上，按一下或點選「工具>網站> ContextHub」。
1. 按一下或點選您要新增UI模組的「設定容器」。
1. 按一下或輸入您要新增UI模組的ContextHub設定。
1. 按一下或點選您要新增UI模組的UI模式。
1. 按一下或點選「建立」按鈕，然後按一下或點選「ContextHub UI Module（一般）」。

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. 提供下列屬性的值：

   * UI模組標題：識別UI模組的標題
   * 模組類型：模組類型
   * 啟用：選擇以在ContextHub工具列中顯示UI模組

1. （可選）若要覆寫預設商店設定，請輸入JSON物件以設定UI模組。
1. 按一下或點選「儲存」。

## 建立ContextHub商店 {#creating-a-contexthub-store}

建立內容中樞儲存區，以保存使用者資料並視需要存取資料。 ContextHub儲存區是以註冊的儲存區候選項為基礎。 當您建立商店時，需要註冊商店候選者的storeType值。 (請參 [閱建立自訂商店候選](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)。)

### 詳細的商店設定 {#detailed-store-configuration}

在配置儲存時，Detail Configuration屬性允許您為儲存特定屬性提供值。 該值基於儲存 `config` 器函式的參 `init` 數。 因此，是否需要提供此值和值的格式取決於儲存。

「詳細資料設定」屬性的值是JSON格 `config` 式的物件。

### 商店候選人範例 {#sample-store-candidates}

AEM提供下列範例商店候選者，供您建立商店的基礎。

| 商店類型 | 說明 |
|---|---|
| [aem.segmentation](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | 儲存已解決和未解析的ContextHub區段。 自動從ContextHub SegmentManager中擷取區段 |
| [aem.resolvedsegments](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | 儲存目前解析的區段。 監聽ContextHub SegmentManager服務以自動更新商店 |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | 儲存瀏覽器位置的經緯度。 |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | 儲存瀏覽器位置的目前日期、時間和季節 |
| [granite.emulator](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | 定義多個設備的屬性和功能，並檢測當前客戶端設備 |
| [contexthub.generic-jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | 從JSONP服務檢索和儲存資料 |
| [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | 儲存目前使用者的描述檔資料 |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | 儲存用戶端的相關資訊，例如裝置資訊、瀏覽器類型和視窗方向 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | 儲存頁面標籤和標籤計數 |

1. 在Experience manager邊欄上，按一下或點選「工具>網站> ContextHub」。
1. 按一下或點選預設設定容器。
1. 按一下或點選「Contexthub Configuration」（內容圖布組態）
1. 若要新增商店，請按一下或點選「建立」圖示，然後按一下或點選「ContexHub商店設定」。

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. 提供基本配置屬性的值，然後按一下或點選「下一步」:

   * **** 配置標題：識別商店的標題
   * **** 商店類型：要作為儲存基礎的儲存候選項的storeType屬性的值
   * **** 必要：選擇
   * **** 啟用：選擇以啟用商店

1. （可選）若要覆寫預設的商店設定，請在「詳細設定(JSON)」方塊中輸入JSON物件。
1. 按一下或點選「儲存」。

## 範例：使用JSONP服務 {#example-using-a-jsonp-service}

此範例說明如何設定儲存區並在UI模組中顯示資料。 在此範例中，jsontest.com網站的MD5服務會用作商店的資料來源。 服務會傳回指定字串的MD5雜湊代碼，格式為JSON。

配置contexthub.generic-jsonp儲存器，以便儲存服務呼叫的資料 `https://md5.jsontest.com/?text=%22text%20to%20md5%22`。 服務返回UI模組中顯示的以下資料：

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### 建立contexthub.generic-jsonp儲存 {#creating-a-contexthub-generic-jsonp-store}

contexthub.generic-jsonp範例儲存候選項可讓您從傳回JSON資料的JSONP服務或網站服務擷取資料。 對於此商店候選項，請使用商店配置來提供要使用的JSONP服務的詳細資訊。

Javascript [類的init](/help/sites-developing/contexthub-api.md#init-name-config) 函式定義一個對 `ContextHub.Store.JSONPStore``config` 像，用於初始化此儲存候選項。 對 `config` 像包含 `service` 包含JSONP服務詳細資訊的對象。 若要設定商店，請以JSON格 `service` 式提供物件作為「詳細資料設定」屬性的值。

要保存jsontest.com站點的MD5服務中的資料，請使用以下屬性 [建立ContextHub儲存](/help/sites-administering/contexthub-config.md#creating-a-contexthub-store) :

* **** 配置標題：md5
* **** 商店類型：contexthub.generic-jsonp
* **** 必要：選擇
* **** 啟用：選擇
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

將UI模組新增至ContextHub工具列，以顯示儲存在範例md5商店的資料。 在此範例中，contexthub.base模組用於產生下列UI模組：

![chlimage_1-323](assets/chlimage_1-323.png)

使用「新增 [UI模組」中的程式](/help/sites-administering/contexthub-config.md#adding-a-ui-module) ，將UI模組新增至現有的UI模式，例如範例Perona UI模式。 對於UI模組，請使用下列屬性值：

* **** UI模組標題：MD5
* **** 模組類型：contexthub.base
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

## 除錯ContextHub {#debugging-contexthub}

ContextHub的除錯模式可啟用，以允許疑難排解。 除錯模式可以透過ContextHub組態或CRXDE來啟用。

### 透過設定 {#via-the-configuration}

編輯ContextHub的設定並勾選「除錯」選 **項**

1. 在邊欄中按一下或點選「工 **具>網站> ContextHub」**
1. 按一下或點選預設的「設 **定容器」**
1. 選取「 **ContextHub設定」** ，然後按一下或點選「編 **輯選取的元素」**
1. 按一下或點選「 **除錯** 」，然後按一下或點選「儲 **存」**

### 透過CRXDE {#via-crxde}

使用CRXDE Lite將屬性設 `debug` 為 **true** :

* `/conf/global/settings/cloudsettings` 或
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>對於仍位於其舊路徑下的ContextHub配置，設定位置 `debug property` 為 `/libs/settings/cloudsettings/legacy/contexthub`。

### 靜默模式 {#silent-mode}

靜默模式會隱藏所有調試資訊。 與常規調試選項（可單獨為每個ContextHub配置設定）不同，silent模式是全局設定，它優先於ContextHub配置級別上的任何調試設定。

這對您的發佈例項非常有用，因為您完全不需要任何除錯資訊。 因為它是全域設定，所以會透過OSGi啟用。

1. 開啟 **Adobe Experience Manager Web Console設定** : `http://<host>:<port>/system/console/configMgr`
1. 搜尋 **Adobe Granite ContextHub**
1. 按一下 **Adobe Granite ContextHub組態** ，以編輯其屬性
1. 選中「靜默模 **式」選項** ，然後按一下「 **保存」**

## 升級後恢復ContextHub配置 {#recovering-contexthub-configurations-after-upgrading}

執行 [AEM升級時](/help/sites-deploying/upgrade.md) ,ContextHub組態會備份並儲存在安全位置。 在升級期間，將安裝預設的ContextHub配置，替換現有配置。 需要備份才能保留您所做的任何更改或添加。

ContextHub組態會儲存在下列節點下 `contexthub` 的資料夾中：

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

升級後，備份儲存在名為的節點下 `contexthub` 的資料夾中：

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` 或
`/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`

節 `yyyymmdd` 點名稱的部分是執行升級的日期。

要恢復ContextHub配置，請使用CRXDE Lite將代表您的儲存、UI模式和UI模組的節點從節點下複製到 `default-pre-upgrade_yyyymmdd_xxxxxx` 以下節點：

* `/conf/global/settings/cloudsettings` 或
* `/conf/<tenant>/settings/cloudsettings`