---
title: 升級前維護任務
seo-title: Pre-Upgrade Maintenance Tasks
description: 了解AEM中的升級前工作。
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

開始升級之前，請務必遵循這些維護任務，以確保系統已就緒，並且一旦出現問題，可以回滾：

* [確保有足夠的磁碟空間](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [完全備份AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [備份對/etc的更改](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [生成quickstart.properties檔案](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [配置工作流和審核日誌清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [安裝、配置和運行升級前任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [停用自訂登入模組](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [從/install目錄中刪除更新](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [停止任何冷備用實例](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [停用自訂排程作業](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [執行離線修訂清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [執行資料儲存垃圾收集](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [視需要升級資料庫架構](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [刪除可能阻礙升級的用戶](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [旋轉日誌檔案](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 確保有足夠的磁碟空間 {#ensure-sufficient-disk-space}

執行升級時，除了內容和程式碼升級活動外，還必須執行存放庫移轉。 移轉會以新的區段Tar格式建立存放庫復本。 因此，您需要足夠的磁碟空間來保留儲存庫的第二個版本（可能更大）。

## 完全備份AEM {#fully-back-up-aem}

AEM應在開始升級前完全備份。 請務必備份儲存庫、應用程式安裝、資料存放區和Mongo例項（如果適用）。 如需備份和還原AEM執行個體的詳細資訊，請參閱 [備份和還原](/help/sites-administering/backup-and-restore.md).

## 備份對/etc的更改 {#backup-changes-etc}

升級程式能妥善維護及合併下方的現有內容和設定 `/apps` 和 `/libs` 儲存庫中的路徑。 針對 `/etc` 路徑（包括Context Hub設定）通常需在升級後重新套用這些變更。 升級會製作任何無法合併的變更的備份副本 `/var`,Adobe建議您在開始升級前手動備份這些變更。

## 生成quickstart.properties檔案 {#generate-quickstart-properties}

從jar檔案啟動AEM時， `quickstart.properties` 檔案在 `crx-quickstart/conf`. 如果AEM過去只是使用啟動指令碼啟動，則此檔案不存在，且升級失敗。 請務必檢查此檔案是否存在，並從jar檔案重新啟動AEM（如果不存在）。

## 配置工作流和審核日誌清除 {#configure-wf-audit-purging}

此 `WorkflowPurgeTask` 和 `com.day.cq.audit.impl.AuditLogMaintenanceTask` 任務需要單獨的OSGi配置，沒有這些配置就無法工作。 如果在升級前任務執行期間失敗，則最可能的原因是缺少配置。 因此，如果您不想執行這些任務，請務必為這些任務新增OSGi設定，或從升級前最佳化任務清單中完全移除這些設定。 有關配置工作流清除任務的文檔，請參見 [管理工作流程例項](/help/sites-administering/workflows-administering.md) 和審核日誌維護任務配置可在 [AEM 6中的稽核記錄維護](/help/sites-administering/operations-audit-log.md).

如需CQ 5.6的工作流程和稽核記錄清除，以及AEM 6.0的稽核記錄清除，請參閱 [清除工作流和審核節點](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## 安裝、配置和運行升級前任務 {#install-configure-run-pre-upgrade-tasks}

由於AEM允許的自訂層級，環境通常不會遵循執行升級的統一方式。 因此，建立升級的標準化程式是一個困難的過程。

在舊版中，停止或無法安全恢復的AEM升級也相當困難。 此問題導致需要重新啟動完整升級過程，或執行有缺陷的升級而未觸發任何警告的情況。

為了解決這些問題，Adobe已對升級程式新增數項增強功能，使其更具彈性且方便使用。 必須手動執行的升級前維護任務正在優化和自動化。 此外，還添加了升級後報告，以便能夠充分審查該過程，希望更容易發現任何問題。

預升級維護任務目前分散在手動執行的部分或全部介面上。 AEM 6.3中推出的升級前維護最佳化可讓您以統一方式觸發這些工作，並可依需求檢查其結果。

升級前最佳化步驟中包含的所有工作都與AEM 6.0以後的所有版本相容。

### 如何設定 {#how-to-set-it-up}

在AEM 6.3和更新版本中，升級前維護優化任務包含在quickstart Jar中。

<!-- URLs below are all 404s. This content should probably be removed because it is entirely obsolete.

If you are upgrading from an older version of AEM 6, they are made available through separate packages that you can download from the Package Manager.

You can find the packages at these locations:

* [For upgrading from AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [For upgrading from AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [For upgrading from AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62) -->

### 如何使用 {#how-to-use-it}

此 `PreUpgradeTasksMBean` OSGI元件已預先設定升級前維護任務清單，可一次執行所有任務。 您可以依照下列程式來設定工作：

1. 瀏覽至 *https://serveraddress:serverport/system/console/configMgr*

1. 搜索「**預升級任務**「 」，然後按一下第一個相符的元件。 元件的完整名稱為 `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. 修改必須運行的維護任務清單，如下所示：

   ![1487758925984](assets/1487758925984.png)

任務清單會因用於啟動實例的運行模式而異。 以下是每個維護任務所針對的運行模式的說明。

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
   <td>執行標籤和掃描。 對於共用資料儲存區，請移除此步驟並執行<br /> 在執行前手動或正確準備執行個體。</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>在執行前，必須先設定AdobeGranite工作流程清除設定OSGi。</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>對於AEM 6.0到6.2上的TarMK例項，請改為手動執行離線修訂清除。</td>
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
>此 `DataStoreGarbageCollectionTask` 使用標籤和掃描階段調用「資料儲存垃圾收集」操作（如果使用）。 對於使用共用資料存放區的部署，請務必正確重新設定或準備執行個體，以避免刪除其他執行個體所參考的項目。 在觸發此升級前任務之前，此過程可能需要在所有實例上手動運行標籤階段。

### 升級前運行狀況檢查的預設配置 {#default-configuration-of-the-pre-upgrade-health-checks}

此 `PreUpgradeTasksMBeanImpl` OSGI元件已預先設定升級前健康狀態檢查標籤清單，以在 `runAllPreUpgradeHealthChecks` 方法呼叫：

* **系統** - granite維護狀況檢查所使用的標籤

* **預升級**  — 可新增至所有健康狀況檢查的自訂標籤，您可設定在升級前執行

清單是可編輯的。 您可以使用加號 **(+)** 減 **(-)** 按鈕，以新增更多自訂標籤，或移除預設標籤。

**MBean方法**

可使用 [JMX控制台](/help/sites-administering/jmx-console.md).

您可以通過以下方式訪問MBean:

1. 前往JMX主控台，網址為 *https://serveraddress:serverport/system/console/jmx*
1. 搜尋 **PreUpgradeTasks** 然後按一下結果

1. 從 **操作** 區段，然後選取 **叫用** 中。

以下列出 `PreUpgradeTasksMBeanImpl` 公開：

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
   <td>以參數指定的名稱運行升級前維護任務。</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>檢查 <code>runAllPreUpgradeTasksmaintenance</code> 任務正在運行。</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>檢查是否有任何預升級維護任務正在運行和<br /> 返回包含當前運行任務名稱的陣列。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>動作</td>
   <td>顯示升級前維護任務的確切運行時間，並將名稱指定為參數。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>動作</td>
   <td>顯示升級前維護任務的最後運行狀態，並將名稱指定為參數。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>動作</td>
   <td><p>運行所有預升級運行狀況檢查，並將其狀態保存在名為的檔案中 <code>preUpgradeHCStatus.properties</code> 在sling首頁路徑上。 若 <code>shutDownOnSuccess</code> 參數設為 <code>true</code>，則AEM執行個體會關閉，但唯有所有預先升級的健全狀態檢查都具備「確定」狀態時。</p> <p>屬性檔案是將來任何升級的先決條件<br /> 如果升級前運行狀況檢查，則停止升級過程<br /> 執行失敗。 如果要忽略預升級的結果<br /> 無論如何，運行狀況檢查並啟動升級，您都可以刪除該檔案。</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>動作</td>
   <td>列出所有在<br /> 升級至指定的AEM版本。 目標AEM版本必須<br /> 參數。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>MBean方法可通過以下方式調用：
>
>* JMX控制台
>* 連接到JMX的任何外部應用程式
>* cURL
>


## 停用自訂登入模組 {#disable-custom-login-modules}

>[!NOTE]
>
>只有從AEM 5版本升級時才需要此步驟。 您可以完全略過此選項，以從舊版AEM 6升級。

自訂方式 `LoginModules` 已設定為在存放庫層級進行驗證，但Apache Oak已根本變更。

在使用CRX2設定的AEM版本中， `repository.xml` 檔案，但從AEM 6開始，可透過Web主控台在Apache Felix JAAS Configuration Factory服務中完成。

因此，升級後必須停用任何現有設定，並針對Apache Oak重新建立。

若要停用JAAS設定中定義的自訂模組，請執行以下操作： `repository.xml`，您必須編輯設定才能使用預設 `LoginModule`，如下列範例所示：

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
>如需詳細資訊，請參閱 [使用外部登錄模組進行身份驗證](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>例如 `LoginModule` 在AEM 6中進行設定，請參閱 [使用AEM 6配置LDAP](/help/sites-administering/ldap-config.md).

## 從/install目錄中刪除更新 {#remove-updates-install-directory}

>[!NOTE]
>
>關閉AEM執行個體後，僅從crx-quickstart/install目錄中移除套件。 此步驟是開始就地升級程式之前的最後一個步驟。

移除透過 `crx-quickstart/install` 目錄。 這麼做可避免在更新完成後，無意中將舊的Hotfix和Service Pack安裝在新的AEM版本之上。

## 停止任何冷備用實例 {#stop-tarmk-coldstandby-instance}

如果使用TarMK冷備，請停止任何冷備實例。 如果升級中出現問題，這麼做可確保重新上線的有效方式。 成功完成升級後，必須從升級的主實例重建冷備用實例。

## 停用自訂排程作業 {#disable-custom-scheduled-jobs}

停用應用程式程式碼中包含的任何OSGi排程作業。

## 執行離線修訂清除 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>此步驟僅對TarMK安裝是必要的

若使用TarMK，您應在升級前執行離線修訂清除。 如此可讓存放庫移轉步驟和後續的升級工作執行得更快，並有助於確保升級完成後線上修訂清除可成功執行。 如需執行離線修訂清除的詳細資訊，請參閱 [執行離線修訂清除](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## 執行資料儲存垃圾收集 {#execute-datastore-garbage-collection}

>[!NOTE]
>
>只有執行crx3的例項才需要此步驟

在CRX3例項上執行修訂清除後，您應執行「資料存放區垃圾收集」以移除資料存放區中任何未參考的Blob。 如需指示，請參閱 [資料儲存垃圾收集](/help/sites-administering/data-store-garbage-collection.md).

## 視需要升級資料庫架構 {#upgrade-the-database-schema-if-needed}

AEM用於永續性的基礎Apache Oak堆疊通常會視需要負責升級資料庫架構。

但是，當無法自動升級架構時，可能會發生案例。 此類情況大多是高安全性環境，在這些環境中，資料庫在權限有限的用戶下運行。 如果發生此情況，AEM會繼續使用舊結構。

若要防止發生此類情況，請執行下列操作來升級架構：

1. 關閉必須升級的AEM執行個體。
1. 升級資料庫架構。 請查閱資料庫類型的文檔，以了解實現結果所需的工具。

   如需Oak如何處理架構升級的詳細資訊，請參閱 [Apache網站上的此頁面](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. 繼續升級AEM。

## 刪除可能阻礙升級的用戶 {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>只有符合以下條件時才需要此升級前維護任務：
>
>* 您從AEM 6.3之前的版本升級
>* 在升級期間，您會遇到下列任何錯誤。
>


有些特殊情況下，服務使用者最終可能會遇到較舊的AEM版本，而未正確標示為一般使用者。

如果發生此情況，升級會失敗並出現下列訊息：

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

若要解決此問題，請務必執行下列動作：

1. 將執行個體與生產流量分離
1. 建立導致問題的一個或多個用戶的備份。 您可以通過包管理器執行此任務。 如需詳細資訊，請參閱 [如何使用套件。](/help/sites-administering/package-manager.md)
1. 刪除導致問題的一個或多個用戶。 以下是可能屬於此類別的使用者清單：

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## 旋轉日誌檔案 {#rotate-log-files}

Adobe建議您在開始升級前先封存目前的記錄檔。 這樣可讓您在升級期間和升級後更輕鬆地監視和掃描日誌檔案，以識別和解決可能發生的任何問題。
