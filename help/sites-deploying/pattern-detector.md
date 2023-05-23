---
title: 用模式檢測器評估升級複雜度
seo-title: Assessing the Upgrade Complexity with the Pattern Detector
description: 瞭解如何使用模式檢測器來評估升級的複雜性。
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

# 用模式檢測器評估升級複雜度

## 概觀 {#overview}

此功能允許您通過檢測AEM使用的模式來檢查現有實例的可升級性：

1. 違反某些規則，並在受升級影響或覆蓋的區域內執行
1. 使用AEM6.x功能或API，該功能在6.5上向後不相容，AEM升級後可能中斷。

這可作為對升級至6.5所涉發展努力的AEM評估。

## 設定方法 {#how-to-set-up}

圖案檢測器作為 [一個包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65) 針對6.AEM5升級，處理從6.1到6.5AEM的任何源版本。 可以使用 [包管理器](/help/sites-administering/package-manager.md)。

## 使用方式 {#how-to-use}

>[!NOTE]
>
>模式檢測器可以在任何環境中運行，包括本地開發實例。 但是，為了：
>
>* 提高檢測率
>* 避免業務關鍵型實例出現任何減速
>
>同時建議運行 **在轉移環境中** 在用戶應用程式、內容和配置方面盡可能接近生產應用程式。

可以使用多種方法檢查陣列檢測器輸出：

* **通過Felix Inventory控制台：**

1. 通過瀏覽AEM到，轉到Web控制台 *https://serveraddress:serverport/system/console/configMgr*
1. 選擇 **狀態 — 模式檢測器** 如下圖所示：

   ![螢幕截圖–2018-2-5模式檢測器](assets/screenshot-2018-2-5pattern-detector.png)

* **通過基於反應文本或常規JSON介面**
* **通過反應JSON行介面**在每行中生成單獨的JSON文檔。

以下對這兩種方法進行了詳細介紹：

## 反應介面 {#reactive-interface}

該被動介面允許一旦檢測到懷疑就處理違規報告。

輸出當前可在2個URL下使用：

1. 純文字檔案介面
1. JSON介面

## 處理純文字檔案介面 {#handling-the-plain-text-interface}

輸出中的資訊被格式化為一系列事件條目。 有兩種渠道：一種是發佈違規，另一種是發佈當前進展。

可以使用以下命令獲取這些命令：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

輸出將如下所示：

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

可以使用 `grep` 命令：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

這將導致以下輸出：

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## 處理JSON介面 {#handling-the-json-interface}

同樣，JSON可以使用 [jq工具](https://stedolan.github.io/jq/) 一經發表，

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

輸出：

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

進度每5秒報告一次，可通過排除標籤為懷疑的郵件以外的其他郵件來獲取：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

輸出：

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
>建議的方法是將捲曲的整個輸出保存到檔案中，然後通過 `jq` 或 `grep` 按鈕。

## 檢測範圍 {#scope}

當前模式檢測器允許檢查：

* OSGi捆綁了進出口不匹配
* Sling資源類型和超類型（帶搜索路徑內容覆蓋）重疊使用
* Oak索引的定義（相容性）
* VLT包（超額使用）
* rep：用戶節點相容性（在OAuth配置上下文中）

>[!NOTE]
>
>請注意，模式檢測器試圖準確預測升級警告。 但是，在某些情況下，它可能會產生誤報。
