---
title: 使用日誌
seo-title: Working with Logs
description: 通過使用日誌AEM瞭解如何排除故障。
seo-description: Learn how to troubleshoot AEM by working with logs.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 3%

---

# 使用日誌{#working-with-logs}

本部分包括有關可幫助您排除故障的日誌的詳細資訊。

CRX記錄詳細日誌。 開啟包裝並啟動Quickstart後，可以在以下位置找到日誌：

* crx quickstart/launchpad/logs
* crx quickstart/server/logs
* crx快速啟動/日誌

## 激活DEBUG日誌級別 {#activating-the-debug-log-level}

預設日誌級別為INFO，即DEBUG消息未記錄。

要激活DEBUG日誌級別，請使用CRX瀏覽器設定

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

要調試的屬性。 不要將日誌保留在DEBUG日誌級別，因為它會生成大量日誌。

調試檔案中的一行通常以DEBUG開頭，然後提供日誌級別、安裝程式操作和日誌消息。 例如：

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日誌級別如下：

| 0 | 錯誤 | 操作失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 錯誤 | 操作失敗。 安裝將繼續，但CRX的一部分安裝不正確，無法正常工作。 |
| 2 | 警告 | 操作已成功，但遇到問題。 CRX可能正確工作，也可能不正確。 |
| 3 | 資訊 | 操作已成功。 |

## 用於故障排除的詳細選項 {#verbose-option-used-for-troubleshooting}

啟動CRX時，可將 — v(verbose)選項添加到命令行中，如中所示：

` java -jar crx-<*version*>-<*edition*>.jar -v`

使用詳細選項進行故障排除，因為此選項顯示控制台上的一些快速啟動日誌輸出。
