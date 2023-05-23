---
title: 版本清除
seo-title: Version Purging
description: 本文介紹了用於版本清除的可用選項。
seo-description: This article describes the available options for version purging.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# 版本清除{#version-purging}

在標準安裝AEM中，在更新內容後激活頁面時，將建立頁面或節點的新版本。

>[!NOTE]
>
>如果未進行任何內容更改，則您將看到一條消息，指出該頁面已激活，但不會建立新版本

您可以使用 **版本控制** 擊中了。 這些版本儲存在儲存庫中，如果需要，可以恢復。

這些版本從不被清除，因此儲存庫大小會隨著時間的推移而增長，因此需要進行管理。

隨附AEM了各種機制來幫助您管理儲存庫：

* 這樣 [版本管理器](#version-manager)
可以將其配置為在建立新版本時清除舊版本。

* 這樣 [清除版本](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) 工具此功能用於監視和維護儲存庫。
它允許您根據以下參數進行干預，以刪除舊版本的節點或節點層次結構：

   * 要保留在儲存庫中的最大版本數。
超過此數時，將刪除最舊的版本。

   * 儲存庫中保存的任何版本的最大年限。
當版本的使用年限超過此值時，會從儲存庫中清除該版本。

* 這樣 [版本清除維護任務](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks)。 您可以計畫「版本清除」維護任務以自動刪除舊版本。 因此，這將手動使用版本清除工具的需要降至最低。

>[!CAUTION]
>
>為了優化儲存庫大小，您應經常運行版本清除任務。 當流量有限時，應將任務安排在工作時間之外。

## 版本管理器 {#version-manager}

除了使用清除工具顯式清除外，還可以將版本管理器配置為在建立新版本時清除舊版本。

要配置版本管理器， [建立配置](/help/sites-deploying/configuring-osgi.md) 為：

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

以下選項可用：

* `versionmanager.createVersionOnActivation` (布爾值，預設值：true)指定是否在激活頁面時建立版本。
除非將複製代理配置為禁止建立版本，否則將建立版本，而版本管理器將遵守這些版本。
僅當激活發生在包含於 `versionmanager.ivPaths` （見下文）。

* `versionmanager.ivPaths`(字串[]，預設值： `{"/"}`)指定在激活時隱式建立版本的路徑(如果 `versionmanager.createVersionOnActivation` 設定為true。

* `versionmanager.purgingEnabled` (布爾值，預設值：false)定義是否在建立新版本時啟用清除。

* `versionmanager.purgePaths` (字串[]，預設值：{&quot;/content&quot;})指定在建立新版本時清除版本的路徑。

* `versionmanager.maxAgeDays` （int，預設值）30)在清除版本時，任何早於配置值的版本都將被刪除。 如果值小於1，則不會根據版本的年齡執行清除。

* `versionmanager.maxNumberVersions` （int，預設5）在清除版本時，任何早於第n個最新版本的版本都將被刪除。 如果值小於1，則不根據版本數執行清除。

* `versionmanager.minNumberVersions` （int，預設0）將保留的最小版本數，而不考慮使用時間。 如果將值設定為小於1的值，則不保留最小版本數。

>[!NOTE]
>
>建議不要在儲存庫中保留大量版本。 因此，在配置版本清除操作時要注意不要從清除中排除太多版本，否則系統資訊庫大小將無法正確優化。 如果您由於業務需要而保留大量版本，請與Adobe支援部門聯繫，以找到優化儲存庫大小的其他方法。

### 組合保留選項 {#combining-retention-options}

定義應如何保留哪些版本的選項( `maxAgeDays`。 `maxNumberVersions`。 `minNumberVersions`)，可根據您的要求組合。

例如，在定義要保留的最大版本數和要保留的最舊版本時：

* 設定:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* 使用：

   * 過去60天內製作的10個版本
   * 其中3個版本是過去30天內建立的

* 意思是：

   * 最後3個版本將保留

例如，在定義要保留的最大版本數和要保留的最舊版本數時：

* 設定:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 使用：

   * 60天前製作的5個版本

* 意思是：

   * 3個版本將保留

## 清除版本工具 {#purge-versions-tool}

的 [清除版本](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) 工具用於清除儲存庫中節點或節點層次結構的版本。 其主要目的是通過刪除節點的舊版本來幫助您減小儲存庫的大小。
