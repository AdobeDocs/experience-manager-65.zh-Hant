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
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306

---


# 版本清除{#version-purging}

在標準安裝中，當您在更新內容後啟動頁面時，AEM會建立新版本的頁面或節點。

>[!NOTE]
>
>如果未進行任何內容變更，您會看到訊息，指出頁面已啟動，但不會建立新版本

您可以使用側點的「版本控制」標籤， **在要求時** ，建立其他版本。 這些版本儲存在儲存庫中，並可以根據需要進行還原。

這些版本不會清除，因此儲存庫大小會隨著時間而增長，因此需要進行管理。

AEM隨附各種機制，可協助您管理您的儲存庫：

* 版本管 [理器](#version-manager)：可以將此配置為在建立新版本時清除舊版本。

* 清除版 [本工具](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) ：此工具用於監視和維護儲存庫。
它允許您根據以下參數進行干預，以刪除節點的舊版本或節點層次：

   * 儲存庫中要保存的最大版本數。
超過此數目時，會移除最舊的版本。

   * 儲存庫中任何版本的最大存留期。
當版本的年齡超過此值時，會從儲存庫中清除它。

* 「版 [本清除」維護任務](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks)。 您可以計畫「版本清除」維護任務，以自動刪除舊版。 因此，這將手動使用「版本清除」工具的需求降至最低。

>[!CAUTION]
>
>為了優化儲存庫大小，您應經常運行版本清除任務。 當流量有限時，應排程工作在營業時間以外的時間。

## 版本管理員 {#version-manager}

除了使用清除工具明確清除外，還可以將「版本管理器」配置為在建立新版本時清除舊版本。

要配置版本管理器，請 [為以下項目建立配置](/help/sites-deploying/configuring-osgi.md) :

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

可使用下列選項：

* `versionmanager.createVersionOnActivation` (布林值，預設值：true)指定在啟動頁面時是否要建立版本。
除非將複製代理配置為禁止建立版本，否則將建立版本，而版本管理器將遵守此配置。
只有在啟動發生在包含於的路徑上時(請參閱 `versionmanager.ivPaths` 下文)，才會建立版本。

* `versionmanager.ivPaths`(字串[]，預設值： `{"/"}`)指定在啟動時隱式建立版本的路徑(如 `versionmanager.createVersionOnActivation` 果設為true)。

* `versionmanager.purgingEnabled` (布林值，預設值：false)定義是否在建立新版本時啟用清除。

* `versionmanager.purgePaths` (字串[]，預設值：{&quot;/content&quot;})指定在建立新版本時要清除版本的路徑。

* `versionmanager.maxAgeDays` (int，預設值：30)在清除版本時，將刪除任何比配置值更舊的版本。 如果值小於1，則不會根據版本的年齡執行清除。

* `versionmanager.maxNumberVersions` （int，預設5）在清除版本時，除第n個最新版本以外的任何版本都將被移除。 如果值小於1，則不會根據版本數執行清除。

* `versionmanager.minNumberVersions` （int，預設0）不論使用年齡為何，將保留的最低版本數。 如果值設為小於1的值，則不會保留最低版本數。

>[!NOTE]
>
>建議不要在儲存庫中保留大量版本。 因此，在配置版本清除操作時請注意不要從清除中排除太多版本，否則儲存庫大小將無法正確優化。 如果您因業務需求而保留大量版本，請聯絡Adobe支援以尋找最佳化儲存庫大小的其他方法。

### 結合保留選項 {#combining-retention-options}

定義應如何保留的版本( `maxAgeDays`、 `maxNumberVersions`、 `minNumberVersions`)的選項，可根據您的需求加以組合。

例如，定義要保留的最大版本數AND要保留的最舊版本時：

* 設定:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* 使用:

   * 過去60天內製作了10個版本
   * 其中3個版本是在過去30天內建立

* Will means that:

   * 最後3個版本將會保留

例如，在定義要保留的最大AND最小版本數和要保留的最舊版本時：

* 設定:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 使用:

   * 60天前製作的5個版本

* Will means that:

   * 3個版本將保留

## 清除版本工具 {#purge-versions-tool}

清除 [版本工具](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) ，用於清除儲存庫中節點版本或節點層次結構。 其主要用途是通過刪除節點的舊版本來幫助您減小儲存庫的大小。
