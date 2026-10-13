---
title: 使用記錄檔
description: 瞭解如何使用記錄檔來疑難排解AEM。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%
---
# 使用記錄檔{#working-with-logs}

本節包含可協助您進行疑難排解的記錄詳細資訊。

>[!NOTE]
>
>如需有關記錄的進一步資訊，請參閱：
>
>* 在AEM中進行[稽核記錄維護](/help/sites-administering/operations-audit-log.md)
>* [使用稽核記錄和記錄檔](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)

CRX會記錄詳細的記錄。 拆開包裝並啟動「快速入門」後，您可在下列位置找到記錄：

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## 啟動DEBUG記錄層級 {#activating-the-debug-log-level}

預設記錄層級為INFO，亦即，不會記錄DEBUG訊息。

若要啟用DEBUG記錄層級，請使用CRX檔案總管設定

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

要偵錯的屬性。 請勿將記錄保留在DEBUG記錄層級的時間超過所需時間，因為它會產生許多記錄。

偵錯檔案中的某一行通常以DEBUG開頭，然後提供記錄層級、安裝程式動作和記錄訊息。 例如：

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

記錄層級如下：

| 0 | 嚴重錯誤 | 動作已失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 錯誤 | 動作已失敗。 安裝會繼續，但部分CRX未正確安裝，將無法運作。 |
| 2 | 警告 | 動作成功但發生問題。 CRX可能正常運作，也可能無法正常運作。 |
| 3 | 資訊 | 動作已成功。 |

## 用於疑難排解的詳細選項 {#verbose-option-used-for-troubleshooting}

啟動CRX時，您可以將 — v （詳細資訊）選項新增至命令列，如下所示：

` java -jar crx-<*version*>-<*edition*>.jar -v`

使用詳細資訊選項進行疑難排解，因為此選項會在主控台上顯示部分快速入門記錄輸出。
