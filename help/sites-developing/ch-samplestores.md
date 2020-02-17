---
title: 範例ContextHub商店候選者
seo-title: 範例ContextHub商店候選者
description: ContextHub提供數種範例商店候選，供您在解決方案中使用
seo-description: ContextHub提供數種範例商店候選，供您在解決方案中使用
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: e37ff1c9e657c580c607f2656adca01a2b39f81f

---


# 範例ContextHub商店候選者{#sample-contexthub-store-candidates}

ContextHub提供數種範例商店候選項目，供您在解決方案中使用。 每個範例都提供下列資訊：

* 在何處尋找原始碼，以便您開啟它以用於學習。
* 如何設定您從商店候選者建立的商店。
* 儲存資料的結構，以便您訪問。

>[!WARNING]
>
>範例商店候選項目會作為參考設定提供，以協助您為專案建立專屬的設定，因此不應直接使用。

## aem.segmentation範例商店候選人 {#aem-segmentation-sample-store-candidate}

儲存已解決和未解析的ContextHub區段。 自動從ContextHub SegmentManager中擷取區段。

### 源位置 {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### 基本實作 {#base-implementation-segmentation}

aem.segmentation儲存區候選項已延伸 [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 設定 {#configuration-segmentation}

當您建立aem.segmentation商店時，不需要提供詳細的設定。 預設配置指定ContextHub段定義的位置。

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation Store Candicate {#contexthub-geolocation-sample-store-candidate}

contexthub.geolocation範例商店候選者使用Google地圖來取得並儲存有關用戶端位置的資訊。

### 源位置 {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### 基本實作 {#base-implementation-geolocation}

contexthub.geolocation儲存候選項會延伸 [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 設定 {#configuration-geolocation}

預設設定會指定Google服務的相關資訊以及初始經緯度座標。

```xml
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### 資料項目 {#data-items-geolocation}

商店使用類似下列範例的資料樹：

```xml
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Chrome 50.x中引入的安全性政策要求所有與地理位置相關的呼叫都必須透過安全連線進行。 因此，如果AEM也在https上執行，AEM會強制將https用於地理位置API呼叫。 否則，會使用http來符合相同來源的原則。 如需 [Chrome變更的詳細資訊](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) ，請參閱此Google部落格文章。

## contexthub.surferinfo範例商店候選項 {#contexthub-surferinfo-sample-store-candidate}

儲存有關目前用戶端環境的資訊，例如裝置、視窗、瀏覽器、日期和時間。

### 來源位置{#source-location-surferinfo

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### 基本實作 {#base-implementation-surferinfo}

contexthub.datetime儲存候選項已擴展 [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)。

### 設定 {#configuration-surferinfo}

預設配置繼承自 `ContextHub.Store.PersistedStore`。

### 資料項目 {#data-items-surferinfo}

使用此儲存候選項的儲存具有類似以下示例的資料樹：

```xml
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## granite.emulators Sample Store Candicate {#granite-emulators-sample-store-candidate}

granite.emulators示例儲存候選儲存有關客戶機設備的資訊。

### 源位置 {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### 基本實作 {#base-implementation-emulators}

contexthub.geolocation儲存候選項會延伸 [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)。

### 設定 {#configuration-emulators}

預設配置包含名為的陣列， `defaultEmulators` 該陣列包含有關不同設備的資訊。 建立商店時，請根據需要在「詳細配置」屬性中使用以下示例中說明的格式提供不同的設備配置檔案：

```xml
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### 資料項目 {#data-items-emulators}

儲存資料樹與以下示例類似：

```xml
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## granite.profile Sample Store Candicate {#granite-profile-sample-store-candidate}

儲存目前使用者的相關資訊。

### 源位置 {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### 基本實作 {#base-implementation-profile}

contexthub.datetime儲存候選項已擴展 [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 設定 {#configuration-profile}

使用下列預設設定。 您不應變更此設定。

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### 資料項目 {#data-items-profile}

使用此儲存候選項的儲存具有類似以下示例的資料樹：

```xml
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
