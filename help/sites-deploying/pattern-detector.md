---
title: 使用模式檢測器評估升級複雜性
seo-title: Assessing the Upgrade Complexity with the Pattern Detector
description: 了解如何使用模式偵測器來評估升級的複雜性。
seo-description: Learn how to use the Pattern Detector to assess the complexity of your upgrade.
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
feature: Upgrading
exl-id: c42373e9-712e-4c11-adbb-4e3626e0b217
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# 使用模式檢測器評估升級複雜性

## 概觀 {#overview}

此功能可讓您偵測使用中的模式，以檢查現有AEM例項的升級性：

1. 違反某些規則，並在受升級影響或覆寫的區域中執行
1. 使用AEM 6.x功能或AEM 6.5上向後不相容的API，且在升級後可能會中斷。

這可作為對升級至AEM 6.5所涉發展努力的評估。

## 設定方法 {#how-to-set-up}

模式偵測器會以 [一個包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65) 使用以AEM 6.5升級為目標的任何來源AEM 6.1到6.5版。 可使用 [封裝管理員](/help/sites-administering/package-manager.md).

## 使用方式 {#how-to-use}

>[!NOTE]
>
>模式偵測器可在任何環境中執行，包括本機開發例項。 不過，為了：
>
>* 提高檢測率
>* 避免業務關鍵型實例出現任何延遲
>
>同時建議執行 **在測試環境中** 在使用者應用程式、內容和設定方面，與生產環境盡可能接近。

您可以使用數種方法來檢查「模式偵測器」輸出：

* **透過Felix Inventory主控台：**

1. 瀏覽至，前往AEM Web Console *https://serveraddress:serverport/system/console/configMgr*
1. 選擇 **狀態 — 模式偵測器** 如下圖所示：

   ![螢幕截圖 — 2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **透過以反應文字為基礎或一般JSON介面**
* **透過反應式JSON行介面，**會在每行產生個別的JSON檔案。

以下詳細說明這兩種方法：

## 無功介面 {#reactive-interface}

被動介面允許在檢測到懷疑時立即處理違規報告。

輸出目前可在2個URL下使用：

1. 純文字介面
1. JSON介面

## 處理純文字介面 {#handling-the-plain-text-interface}

輸出中的資訊將格式化為一系列事件條目。 有兩個管道：一個用於發佈違規，另一個用於發佈當前進度。

可使用下列命令取得這些值：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

輸出如下所示：

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

可使用 `grep` 命令：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

這會產生下列輸出：

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## 處理JSON介面 {#handling-the-json-interface}

同樣地，您也可以使用 [jq工具](https://stedolan.github.io/jq/) 一發佈。

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

使用輸出：

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

進度每5秒報告一次，可借由排除標籤為懷疑以外的其他訊息來擷取：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

使用輸出：

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
>
>建議的方法是將整個輸出從curl儲存至檔案，然後透過 `jq` 或 `grep` 來篩選資訊類型。

## 檢測範圍 {#scope}

目前模式偵測器允許檢查：

* OSGi套件組合導出和導入不匹配
* Sling資源類型和超類型（含搜尋路徑內容覆蓋）覆蓋使用方式
* Oak索引的定義（相容性）
* VLT包（過度使用）
* rep：用戶節點相容性（在OAuth配置中）

>[!NOTE]
>
>請注意，模式偵測器會嘗試準確預測升級警告。 但在某些情況下，這可能會產生誤判。
