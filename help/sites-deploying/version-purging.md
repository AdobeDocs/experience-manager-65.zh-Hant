---
title: 版本清除
seo-title: 版本清除
description: 本文說明版本清除的可用選項。
seo-description: 本文說明版本清除的可用選項。
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: 設定
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---

# 版本清除{#version-purging}

在標準安裝中，當您在更新內容後啟動頁面時，AEM會建立新版本的頁面或節點。

>[!NOTE]
>
>如果未進行任何內容變更，您會看到訊息，指出頁面已啟用，但不會建立新版本

您可以使用sidekick的&#x200B;**Versioning**&#x200B;標籤，依請求建立其他版本。 這些版本儲存在儲存庫中，並可視需要還原。

這些版本永遠不會清除，因此儲存庫大小會隨著時間而增長，因此需要管理。

AEM隨附多種機制，可協助您管理存放庫：

* [版本管理器](#version-manager)
這可在建立新版本時設定為清除舊版本。

* [清除版本](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)工具
這是監控和維護存放庫的一部分。
它可讓您干預，根據以下參數移除舊版節點或節點階層：

   * 要保留在儲存庫中的最大版本數。
超過此數目時，會移除最舊的版本。

   * 存放在存放庫中任何版本的最大存留期。
版本的年齡超過此值時，系統會從存放庫中清除該值。

* [版本清除維護任務](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks)。 您可以安排「版本清除」維護任務以自動刪除舊版本。 因此，這將手動使用版本清除工具的需求降至最低。

>[!CAUTION]
>
>要優化儲存庫大小，應經常運行版本清除任務。 當流量有限時，應在工作時間之外排程該任務。

## 版本管理器{#version-manager}

除了使用清除工具來明確清除外，還可以配置版本管理器在建立新版本時清除舊版本。

要配置版本管理器，請[為以下項目建立配置](/help/sites-deploying/configuring-osgi.md):

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

可使用下列選項：

* `versionmanager.createVersionOnActivation` (布林值，預設值：true)指定是否在頁面啟動時建立版本。除非將復寫代理配置為禁止建立版本，否則將建立版本，該版本由版本管理器執行。
只有在啟動發生在`versionmanager.ivPaths`中的路徑上時，才會建立版本（請參閱下方）。

* `versionmanager.ivPaths`(字串[]，預設值： `{"/"}`)指定若設為true，在啟用時隱含建立版本 `versionmanager.createVersionOnActivation` 的路徑。

* `versionmanager.purgingEnabled` (布林值，預設值：false)定義建立新版本時是否啟用清除。

* `versionmanager.purgePaths` (字串[]，預設值：{&quot;/content&quot;})指定建立新版本時要清除版本的路徑。

* `versionmanager.maxAgeDays` (int，預設值：30)版本清除時，任何版本若比設定值還舊，都將移除。如果值小於1，則不會根據版本的年齡執行清除。

* `versionmanager.maxNumberVersions` （int，預設5）版本清除時，任何早於第n個最新版本的版本都將被移除。如果值小於1，則不會根據版本數量執行清除。

* `versionmanager.minNumberVersions` （int，預設0）無論年齡為何，將保留的最低版本數。如果值設為小於1，則不會保留最低版本數量。

>[!NOTE]
>
>不建議將大量版本保留在儲存庫中。 因此，在配置版本清除操作時，請注意不要從清除中排除太多版本，否則系統無法正確最佳化儲存庫大小。 如果您因業務需求而保留大量版本，請聯絡Adobe支援，以尋找最佳化存放庫大小的其他方法。

### 組合保留選項{#combining-retention-options}

定義應如何保留版本的選項(`maxAgeDays`、`maxNumberVersions`、`minNumberVersions`)，可以根據您的需求組合。

例如，定義要保留的版本數目上限時，定義要保留的最舊版本時：

* 設定:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* 使用:

   * 過去60天內製作的10個版本
   * 過去30天內建立的3個版本

* 將表示：

   * 最後3個版本將會保留

例如，定義要保留的最大和最小版本數時，定義要保留的最舊版本時：

* 設定:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 使用:

   * 60天前製作的5個版本

* 將表示：

   * 將保留3個版本

## 清除版本工具{#purge-versions-tool}

[清除版本](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)工具用於清除儲存庫中節點版本或節點層次結構。 其主要用途是透過移除舊版節點，協助您縮小存放庫的大小。
