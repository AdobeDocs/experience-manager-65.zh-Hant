---
title: 版本清除
description: 本文介紹版本清除的可用選項。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# 版本清除{#version-purging}

在標準安裝中，當您在更新內容後啟動頁面時，Adobe Experience Manager (AEM)會建立頁面或節點的版本。

>[!NOTE]
>
>如果未進行任何內容變更，則會看到一則訊息，指出頁面已啟動，但未建立新版本。

您可以使用sidekick的&#x200B;**版本設定**&#x200B;索引標籤，依請求建立其他版本。 這些版本儲存在存放庫中，可視需要還原。

這些版本永遠不會清除，因此存放庫大小會隨著時間增長，因此必須加以管理。

AEM隨附多種機制，可協助您管理存放庫：

* [版本管理員](#version-manager)
這可設定為在建立新版本時清除舊版本。

* [清除版本](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)工具
這可用來當作監控和維護存放庫的一部分。
它可讓您根據下列引數，介入以移除舊版本的節點或節點階層：

   * 要保留在存放庫中的版本最大數量。
超過此數目時，會移除最舊的版本。

   * 任何版本保留在存放庫中的最大期限。
當版本的使用期限超過此值時，就會從存放庫中清除該版本。

* [版本清除維護任務](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks)。 您可以排定「版本永久刪除」維護作業，以自動刪除舊版本。 如此一來，手動使用「版本清除」工具的需求便降至最低。

>[!CAUTION]
>
>若要最佳化存放庫大小，請經常執行版本清除工作。 當流量有限時，應該將任務排程在營業時間以外。

## 版本管理員 {#version-manager}

除了使用清除工具來明確清除外，也可以將「版本管理員」設定為在建立新版本時清除舊版本。

若要設定版本管理員，請[為下列專案建立設定](/help/sites-deploying/configuring-osgi.md)：

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

下列選項可供使用：

* `versionmanager.createVersionOnActivation` （布林值，預設： true）
指定啟動頁面時是否要建立版本。
除非將復寫代理設定為抑製版本的建立，否則會建立版本，而版本管理員會遵循此設定。
只有當啟動發生在`versionmanager.ivPaths`中包含的路徑上時，才會建立版本（請參閱下文）。

* `versionmanager.ivPaths`（字串[]，預設： `{"/"}`）
指定當`versionmanager.createVersionOnActivation`設定為true時，會在哪一個路徑上以隱含方式建立版本。

* `versionmanager.purgingEnabled` （布林值，預設： false）
定義在建立新版本時是否啟用永久刪除。

* `versionmanager.purgePaths` （字串[]，預設： {&quot;/content&quot;}）
指定建立新版本時要在哪些路徑上清除版本。

* `versionmanager.maxAgeDays` （int，預設值： 30）
在版本清除時，會移除設定值之前的任何版本。 如果值小於1，則不會根據版本的期限執行永久刪除。

* `versionmanager.maxNumberVersions` （int，預設5）
在版本清除時，會移除任何早於第n個最新版本的版本。 如果值小於1，則不會根據版本數執行永久刪除。

* `versionmanager.minNumberVersions` （int，預設0）
無論年齡為何，保留的最低版本數量。 如果該值設定為小於1的值，則不會保留版本的最小數量。

>[!NOTE]
>
>不建議在存放庫中保留許多版本。 因此，在設定版本清除操作時，請注意不要從清除中排除太多版本，否則存放庫大小未正確最佳化。 如果您因業務需求而保留大量版本，請聯絡Adobe支援以尋找其他方法以最佳化存放庫大小。

### 結合保留選項 {#combining-retention-options}

定義應如何保留哪些版本(`maxAgeDays`、`maxNumberVersions`、`minNumberVersions`)的選項可以根據您的要求合併。

例如，在定義要保留的版本數目上限以及要保留的最舊版本時：

* 設定：

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* 替換為：

   * 在過去60天內製作了10個版本
   * 其中三個版本是在過去30天內建立的

* 這表示：

   * 會保留最後三個版本

例如，在定義要保留的最大AND最小版本數以及要保留的最舊版本時：

* 設定：

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 替換為：

   * 有5個版本是60天前製作的

* 這表示：

   * 保留三個版本

## 清除版本工具 {#purge-versions-tool}

[清除版本](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)工具旨在清除存放庫中節點或節點階層的版本。 其主要用途是協助您移除舊版節點，以縮小存放庫的大小。
