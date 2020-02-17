---
title: 用模式檢測器評估升級複雜度
seo-title: 用模式檢測器評估升級複雜度
description: 瞭解如何使用模式偵測器來評估升級的複雜性。
seo-description: 瞭解如何使用模式偵測器來評估升級的複雜性。
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 用模式檢測器評估升級複雜度{#assessing-the-upgrade-complexity-with-the-pattern-detector}

## 概覽 {#overview}

此功能可讓您偵測使用中的模式，以檢查現有AEM例項是否可升級：

1. 違反特定規則，並在受升級影響或覆寫的區域執行
1. 使用AEM 6.x功能或API，在AEM 6.5上無法向後相容，而且升級後可能會中斷。

這可作為對升級至AEM 6.5所涉及的開發工作的評估。

## 如何設定 {#how-to-set-up}

Pattern Detector會以單一套件的形 [式個別發行](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/pd-all-aem65) ，適用於以AEM 6.5升級為目標的6.1到6.5的任何來源AEM版本。 它可以使用「包管理器」( [Package Manager)安裝](/help/sites-administering/package-manager.md)。

## 如何使用 {#how-to-use}

>[!NOTE]
>
>模式偵測器可在任何環境上執行，包括本機開發執行個體。 但是，為了：
>
>* 提高檢測率
>* 避免業務關鍵型實例出現任何慢速


>同時，建議在與生產環境 **最接近的測試環境** （在使用者應用程式、內容和設定方面）上執行它。
>
您可以使用數種方法來檢查圖樣檢測器輸出：

* **透過Felix Inventory主控台：**

1. 瀏覽至https://serveraddress:serverport/system/console/configMgr以前往「AEM Web Console」（AEM網頁主控台） *。*
1. 選擇 **狀態——模式檢測器** ，如下圖所示：

   ![screapth-2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **透過以反應文字為基礎的或一般的JSON介面**

* **透過反應式JSON線條介面，**可在每行中產生個別的JSON檔案。

以下兩種方法均詳述：

## 無功介面 {#reactive-interface}

該被動介面允許在檢測到懷疑時立即處理違規報告。

輸出目前可在2個URL下使用：

1. 純文字介面
1. JSON介面

## 處理純文字檔案介面 {#handling-the-plain-text-interface}

輸出中的資訊被格式化為一系列事件條目。 有兩個渠道——一個用於發佈違規，另一個用於發佈當前進度。

您可使用下列指令來取得這些指令：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

輸出將如下所示：

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

使用以下命令可以過濾進 `grep` 度：

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

同樣地，JSON在發佈時也 [可以使用jq工具](https://stedolan.github.io/jq/) 。

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

每5秒報告一次進度，可排除標籤為懷疑的其他訊息以擷取進度：

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
建議的方法是將捲動的整個輸出儲存到檔案中，然後透過或篩選 `jq` 資訊 `grep` 類型加以處理。

## 檢測範圍 {#scope}

Currently Pattern Detector允許檢查：

* OSGi捆綁了導出和導入不匹配
* Sling資源類型和超類型（含search-path內容覆蓋）覆蓋使用實例
* Oak索引的定義（相容性）
* VLT包（超額使用）
* rep：用戶節點相容性（在OAuth配置的上下文中）

>[!NOTE]
請注意，模式偵測器會嘗試準確預測升級警告。 但是，在某些情況下可能會產生誤報。

