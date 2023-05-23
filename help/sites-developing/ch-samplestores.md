---
title: 示例ContextHub儲存候選
seo-title: Sample ContextHub Store Candidates
description: ContextHub提供了幾個示例儲存候選，您可以在解決方案中使用
seo-description: ContextHub provides several sample store candidates that you can use in your solutions
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d8d9a799-3e30-442a-843b-d4d7ba70c557
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 示例ContextHub儲存候選{#sample-contexthub-store-candidates}

ContextHub提供了幾個示例儲存候選，您可以在解決方案中使用。 為每個示例提供以下資訊：

* 在何處查找原始碼，以便您可以開啟它以用於學習目的。
* 如何配置從候選儲存庫建立的儲存庫。
* 儲存資料的結構，以便您能夠訪問它。

>[!WARNING]
>
>示例儲存候選作為參考配置提供，以幫助您為項目構建自己的專用配置，因此不應直接使用。

## aem.分段樣本儲存候選 {#aem-segmentation-sample-store-candidate}

儲存已解析和未解析的ContextHub段。 自動從ContextHub SegmentManager中檢索段。

### 源位置 {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### 基本實施 {#base-implementation-segmentation}

aem.segmentation儲存候選擴展 [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 設定 {#configuration-segmentation}

建立aem.segmentation儲存時，無需提供詳細配置。 預設配置指定ContextHub段定義的位置。

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation示例儲存候選 {#contexthub-geolocation-sample-store-candidate}

contexthub.geolocation示例儲存候選項使用Google地圖來獲取和儲存有關客戶端位置的資訊。

### 源位置 {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### 基本實施 {#base-implementation-geolocation}

contexthub.geolocation儲存候選擴展 [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 設定 {#configuration-geolocation}

預設配置指定有關Google服務以及初始經緯度坐標的資訊。

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

### 資料項 {#data-items-geolocation}

儲存使用與以下示例類似的資料樹：

```xml
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Chrome 50.x中引入的安全策略要求所有與地理位置相關的呼叫都通過安全連接進行。 因此，AEM如果在https上運行，則強AEM制對地理位置API調用使用https。 否則，使用http來符合同一源的策略。 請參閱 [Google部落格](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) 的子菜單。

## contexthub.surferinfo示例儲存候選 {#contexthub-surferinfo-sample-store-candidate}

儲存有關當前客戶端環境的資訊，如設備、窗口、瀏覽器、日期和時間。

### 源位置 {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### 基本實施 {#base-implementation-surferinfo}

contexthub.datetime儲存候選擴展 [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)。

### 設定 {#configuration-surferinfo}

預設配置繼承自 `ContextHub.Store.PersistedStore`。

### 資料項 {#data-items-surferinfo}

使用此儲存候選的儲存具有與以下示例類似的資料樹：

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

## granite.emulators樣本儲存候選 {#granite-emulators-sample-store-candidate}

granite.emulators示例儲存候選儲存關於客戶端設備的資訊。

### 源位置 {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### 基本實施 {#base-implementation-emulators}

contexthub.geolocation儲存候選擴展 [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)。

### 設定 {#configuration-emulators}

預設配置包括名為 `defaultEmulators` 包含有關不同設備的資訊。 建立儲存時，請根據需要在「詳細配置」屬性中提供不同的設備配置檔案，格式如下例所示：

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

### 資料項 {#data-items-emulators}

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

## granite.profile樣例儲存候選 {#granite-profile-sample-store-candidate}

儲存有關當前用戶的資訊。

### 源位置 {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### 基本實施 {#base-implementation-profile}

contexthub.datetime儲存候選擴展 [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 設定 {#configuration-profile}

使用以下預設配置。 您不應更改此配置。

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

### 資料項 {#data-items-profile}

使用此儲存候選的儲存具有與以下示例類似的資料樹：

```xml
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
