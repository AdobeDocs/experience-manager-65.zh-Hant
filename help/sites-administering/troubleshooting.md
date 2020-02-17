---
title: 使用日誌
seo-title: 使用日誌
description: 瞭解如何使用記錄來疑難排解AEM。
seo-description: 瞭解如何使用記錄來疑難排解AEM。
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09

---


# 使用日誌{#working-with-logs}

本節包含可協助您疑難排解之記錄檔的詳細資訊。

CRX記錄詳細記錄。 開啟包裝並啟動快速啟動後，您可以在以下位置找到日誌：

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## 啟用DEBUG日誌級別 {#activating-the-debug-log-level}

預設日誌級別為INFO，即不記錄DEBUG消息。

若要啟用DEBUG記錄檔層級，請使用CRX檔案總管來設定

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

屬性進行除錯。 請勿將記錄檔保留在DEBUG記錄檔層級，因為它會產生許多記錄檔。

除錯檔案中的一行通常以DEBUG開頭，然後提供記錄檔層級、安裝程式動作和記錄檔訊息。 例如：

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日誌級別如下：

| 0 | 致命錯誤 | 動作失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 錯誤 | 動作失敗。 安裝將繼續，但CRX的某部分安裝不正確，因此無法正常工作。 |
| 2 | 警告 | 行動成功，但遇到問題。 CRX可能正常工作，也可能無法正常工作。 |
| 3 | 資訊 | 動作成功。 |

## 用於疑難排解的詳細選項 {#verbose-option-used-for-troubleshooting}

啟動CRX時，可以將-v（詳細）選項添加到命令行，如中所示：

` java -jar crx-<*version*>-<*edition*>.jar -v`

使用詳細選項進行故障排除，因為此選項顯示控制台上的一些快速啟動日誌輸出。