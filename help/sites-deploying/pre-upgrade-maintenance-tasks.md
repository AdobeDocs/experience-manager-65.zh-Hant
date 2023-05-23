---
title: 升級前維護任務
seo-title: Pre-Upgrade Maintenance Tasks
description: 瞭解中的升級前任務AEM。
seo-description: Learn about the pre-upgrade tasks in AEM.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
feature: Upgrading
exl-id: 37d4aee4-15eb-41ab-ad71-dfbd5c7910f8
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '2030'
ht-degree: 0%

---

# 升級前維護任務{#pre-upgrade-maintenance-tasks}

在開始升級之前，必須執行這些維護任務以確保系統準備就緒，並且在出現以下問題時可以回滾：

* [確保足夠的磁碟空間](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [完全備份AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [備份對/etc的更改](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [生成quickstart.properties檔案](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [配置工作流和審核日誌清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [安裝、配置和運行升級前任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [禁用自定義登錄模組](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [從/install目錄中刪除更新](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [停止任何冷備用實例](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [禁用自定義計畫作業](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [執行離線修訂版清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [執行資料儲存垃圾收集](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [如果需要，升級資料庫架構](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [刪除可能阻礙升級的用戶](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [旋轉日誌檔案](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 確保足夠的磁碟空間 {#ensure-sufficient-disk-space}

執行升級時，除了內容和代碼升級活動外，還必須執行儲存庫遷移。 遷移將以新的段Tar格式建立儲存庫的副本。 因此，您需要足夠的磁碟空間來保留第二個可能更大的儲存庫版本。

## 完全備份AEM {#fully-back-up-aem}

應AEM在開始升級之前完全備份。 確保備份儲存庫、應用程式安裝、資料儲存和Mongo實例（如果適用）。 有關備份和恢復實例的詳細信AEM息，請參見 [備份和恢復](/help/sites-administering/backup-and-restore.md)。

## 備份對/etc的更改 {#backup-changes-etc}

升級過程很好地維護和合併了以下現有內容和配置 `/apps` 和 `/libs` 儲存庫中的路徑。 對於對 `/etc` 路徑（包括上下文中心配置）通常需要在升級後重新應用這些更改。 當升級生成任何無法合併的更改的備份副本時 `/var`,Adobe建議您在開始升級之前手動備份這些更改。

## 生成quickstart.properties檔案 {#generate-quickstart-properties}

從jarAEM檔案啟動時， `quickstart.properties` 檔案生成於 `crx-quickstart/conf`。 如AEM果以前只使用啟動指令碼啟動，則此檔案不存在，升級失敗。 確保檢查此檔案是否存在，並從jar文AEM件重新啟動（如果不存在）。

## 配置工作流和審核日誌清除 {#configure-wf-audit-purging}

的 `WorkflowPurgeTask` 和 `com.day.cq.audit.impl.AuditLogMaintenanceTask` 任務需要單獨的OSGi配置，如果沒有這些配置，則無法工作。 如果在升級前任務執行期間失敗，則最可能的原因是缺少配置。 因此，請確保為這些任務添加OSGi配置，或者如果不希望運行這些配置，則從升級前優化任務清單中將其完全刪除。 有關配置工作流清除任務的文檔，請參見 [管理工作流實例](/help/sites-administering/workflows-administering.md) 和審核日誌維護任務配置，可在 [6中的審核日誌維AEM護](/help/sites-administering/operations-audit-log.md)。

有關CQ 5.6上的工作流和審核日誌清除以及6.0上的審核日誌清AEM除，請參閱 [清除工作流和審核節點](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html)。

## 安裝、配置和運行升級前任務 {#install-configure-run-pre-upgrade-tasks}

由於定制級別允許AEM，環境通常不遵循統一的升級方式。 因此，建立標準化的升級程式是一個困難的過程。

在以前版本中，停止或AEM無法安全恢復的升級也很困難。 此問題導致需要重新啟動完整升級過程或執行有缺陷的升級而未觸發任何警告的情況。

為瞭解決這些問題，Adobe在升級過程中添加了幾項增強功能，使其更具彈性和用戶友好性。 之前必須手動執行的升級前維護任務正在優化和自動執行。 此外，還增加了升級後報告，以便能夠充分審查該進程，希望更容易發現任何問題。

升級前維護任務當前分散在部分或全部手動執行的各種介面上。 6.3中引入的升級前維護優AEM化使用統一的方法觸發這些任務，並能夠根據需要檢查其結果。

升級前優化步驟中包含的所有任務都與6.0以AEM後的所有版本相容。

### 如何設定 {#how-to-set-it-up}

在AEM6.3及更高版本中，快速啟動jar中包含升級前維護優化任務。

<!-- URLs below are all 404s. This content should probably be removed because it is entirely obsolete.

If you are upgrading from an older version of AEM 6, they are made available through separate packages that you can download from the Package Manager.

You can find the packages at these locations:

* [For upgrading from AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [For upgrading from AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [For upgrading from AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62) -->

### 如何使用 {#how-to-use-it}

的 `PreUpgradeTasksMBean` OSGI元件預配置了可同時運行的升級前維護任務清單。 您可以按照以下步驟配置任務：

1. 通過瀏覽到 *https://serveraddress:serverport/system/console/configMgr*

1. 搜索「」**預升級任務**，然後按一下第一個匹配的元件。 元件的全名為 `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. 修改必須運行的維護任務清單，如下所示：

   ![1487758925984](assets/1487758925984.png)

根據用於啟動實例的運行模式，任務清單不同。 下面是每個維護任務的運行模式描述。

<table>
 <tbody>
  <tr>
   <td><strong>任務</strong></td>
   <td><strong>執行模式</strong></td>
   <td><strong>附註</strong></td>
  </tr>
  <tr>
   <td><code>TarIndexMergeTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>DataStoreGarbageCollectionTask</code></td>
   <td>crx2</td>
   <td>運行標籤和掃描。 對於共用資料儲存，刪除此步驟並運行<br /> 在執行前手動或正確準備實例。</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>運行前必須配置Adobe花崗岩工作流清除配置OSGi。</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>對於6.0到6.2AEM上的TarMK實例，請手動運行離線修訂版清除。</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>運行前必須配置審核日誌清除計畫程式OSGi配置。</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>的 `DataStoreGarbageCollectionTask` 使用標籤和掃描階段調用資料儲存垃圾收集操作。 對於使用共用資料儲存的部署，請確保正確重新配置該資料儲存或準備該實例以避免刪除由另一個實例引用的項目。 此過程可能需要在觸發此升級前任務之前，在所有實例上手動運行標籤階段。

### 升級前運行狀況檢查的預設配置 {#default-configuration-of-the-pre-upgrade-health-checks}

的 `PreUpgradeTasksMBeanImpl` OSGI元件預配置了升級前運行狀況檢查標籤清單，當 `runAllPreUpgradeHealthChecks` 方法調用：

* **系統**  — 花崗岩維護健康檢查使用的標籤

* **預升級**  — 可添加到升級前可設定為運行的所有運行狀況檢查的自定義標籤

清單是可編輯的。 可以使用 **(+)** 減 **(-)** 按鈕，以添加更多自定義標籤，或刪除預設標籤。

**MBean方法**

可以使用 [JMX控制台](/help/sites-administering/jmx-console.md)。

您可以通過以下方式訪問MBean:

1. 轉到JMX控制台 *https://serveraddress:serverport/system/console/jmx*
1. 搜索 **升級前任務** 按一下結果

1. 從 **操作** 選擇 **調用** 的上界。

下面是所有可用方法的清單 `PreUpgradeTasksMBeanImpl` 暴露：

<table>
 <tbody>
  <tr>
   <td><strong>方法名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeTasksNames()</code></td>
   <td>資訊</td>
   <td>顯示可用的升級前維護任務名稱清單。</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>資訊</td>
   <td>顯示升級前運行狀況檢查標籤名稱的清單。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>動作</td>
   <td>運行清單中的所有升級前維護任務。</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>動作</td>
   <td>運行以參數命名的升級前維護任務。</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>操作資訊</td>
   <td>檢查 <code>runAllPreUpgradeTasksmaintenance</code> 任務正在運行。</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>操作資訊</td>
   <td>檢查是否正在運行任何升級前維護任務，<br /> 返回包含當前正在運行的任務名稱的陣列。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>動作</td>
   <td>顯示升級前維護任務的準確運行時間，並將指定的名稱作為參數。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>動作</td>
   <td>顯示升級前維護任務的上次運行狀態，其名稱為參數。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>動作</td>
   <td><p>運行所有升級前運行狀況檢查並將其狀態保存在名為 <code>preUpgradeHCStatus.properties</code> 在吊帶回家的路上。 如果 <code>shutDownOnSuccess</code> 參數設定為 <code>true</code>，實例AEM將關閉，但前提是所有升級前運行狀況檢查都處於「正常」狀態。</p> <p>屬性檔案用作以後任何升級的前提條件<br /> 如果升級前運行狀況檢查，則升級過程將停止<br /> 執行失敗。 如果要忽略預升級的結果<br /> 運行狀況檢查並啟動升級，您可以刪除該檔案。</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>動作</td>
   <td>列出在以下情況下不再滿足的所有導入包<br /> 升級到指定的AEM版本。 目標AEM版本必須為<br /> 作為參數。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>可通過以下方式調用MBean方法：
>
>* JMX控制台
>* 連接到JMX的任何外部應用程式
>* cURL
>


## 禁用自定義登錄模組 {#disable-custom-login-modules}

>[!NOTE]
>
>只有從5版本升級時，才需AEM要此步驟。 可以完全跳過它以從舊版本AEM進行升級。

自定義方式 `LoginModules` 在Apache Oak中，在儲存庫級別進行身份驗證時已發生根本更改。

在使AEM用CRX2配置的版本中， `repository.xml` 檔案，而從AEM6開始，則通過Web控制台在Apache Felix JAAS Configuration Factory服務中完成。

因此，升級後必須禁用並重新為Apache Oak建立任何現有配置。

禁用在JAAS配置中定義的自定義模組 `repository.xml`，必須編輯配置以使用預設 `LoginModule`，如下例所示：

```xml
<Security >
             ....
          <!--
                 Use LoginModule authenticating against repository itself
                 -->
                 <LoginModule class = "com.day.crx.core.CRXLoginModule" >
                     <param name = "anonymousId" value = "anonymous" />
                     <param name = "adminId" value ="admin" />
                     <param name = "disableNTLMAuth" value = "true" />
                     <param name = "tokenExpiration" value = "43200000" />
                     <!-- param name="trust_credentials_attribute" value="d5b9167e95dad6e7d3b5d6fa8df48af8"/
                -->
                 </LoginModule >
         </ Security>
```

>[!NOTE]
>
>有關詳細資訊，請參見 [使用外部登錄模組進行身份驗證](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)。
>
>例如 `LoginModule` 6中的AEM配置，請參見 [配置LDAPAEM 6](/help/sites-administering/ldap-config.md)。

## 從/install目錄中刪除更新 {#remove-updates-install-directory}

>[!NOTE]
>
>在關閉實例後，僅從crx-quickstart/install目錄中刪除AEM包。 此步驟是啟動就地升級過程之前的最後步驟之一。

刪除通過 `crx-quickstart/install` 的子目錄。 這樣可防止在更新完成後，在新版本上意外安裝AEM舊修補程式和Service Pack。

## 停止任何冷備用實例 {#stop-tarmk-coldstandby-instance}

如果使用TarMK冷備用實例，請停止任何冷備用實例。 這樣，在升級中出現問題時，就可以保證重新聯機的高效方式。 升級成功完成後，必須從升級的主實例重建冷備用實例。

## 禁用自定義計畫作業 {#disable-custom-scheduled-jobs}

禁用應用程式碼中包含的所有OSGi計畫作業。

## 執行離線修訂版清除 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>此步驟僅對TarMK安裝是必需的

如果使用TarMK，則應在升級前運行離線修訂版清除。 這樣，儲存庫遷移步驟和後續升級任務的執行速度會快得多，並有助於確保在升級完成後線上修訂版清除能夠成功執行。 有關運行離線修訂版清除的資訊，請參見 [正在執行離線修訂版清除](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup)。

## 執行資料儲存垃圾收集 {#execute-datastore-garbage-collection}

>[!NOTE]
>
>此步驟僅對運行crx3的實例是必需的

對CRX3實例運行修訂版清理後，應運行資料儲存垃圾收集以刪除資料儲存中任何未引用的Blob。 有關說明，請參閱 [資料儲存垃圾收集](/help/sites-administering/data-store-garbage-collection.md)。

## 如果需要，升級資料庫架構 {#upgrade-the-database-schema-if-needed}

通常，用於持久性的基礎Apache OakAEM堆棧會根據需要來升級資料庫架構。

但是，當模式無法自動升級時，可能會出現這種情況。 此類情況大多是高安全性環境，在這些環境中，資料庫以具有有限權限的用戶運行。 如果出現這種情況，AEM則繼續使用舊模式。

要防止出現此情形，請執行以下操作來升級架構：

1. 關閉AEM必須升級的實例。
1. 升級資料庫架構。 請查閱資料庫類型的文檔，以瞭解實現結果所需的工具。

   有關Oak如何處理架構升級的詳細資訊，請參見 [Apache網站上的此頁](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade)。

1. 繼續升級AEM。

## 刪除可能阻礙升級的用戶 {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>只有在以下情況下才需要執行此升級前維護任務：
>
>* 您正在從AEM6.AEM3版以前的版本升級
>* 在升級過程中遇到以下任何錯誤。
>


服務用戶最終可能被錯誤地標籤為常AEM規用戶的舊版本時，會出現例外情況。

如果出現這種情況，升級將失敗，並顯示如下消息：

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

要解決此問題，請確保執行以下操作：

1. 將實例與生產流量分離
1. 建立導致問題的一個或多個用戶的備份。 可以通過包管理器來執行此任務。 有關詳細資訊，請參見 [如何使用包。](/help/sites-administering/package-manager.md)
1. 刪除導致問題的一個或多個用戶。 以下是可能屬於此類別的用戶清單：

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## 旋轉日誌檔案 {#rotate-log-files}

Adobe建議在開始升級之前存檔當前的日誌檔案。 這樣，在升級期間和升級後可以更輕鬆地監視和掃描日誌檔案，以識別和解決可能發生的任何問題。
