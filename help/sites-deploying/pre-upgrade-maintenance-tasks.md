---
title: 升級前維護任務
seo-title: 升級前維護任務
description: 瞭解中的升級前任務AEM。
seo-description: 瞭解中的升級前任務AEM。
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2159'
ht-degree: 0%

---


# 升級前維護任務{#pre-upgrade-maintenance-tasks}

在開始升級之前，請務必執行這些維護任務，以確保系統已就緒，並且如果出現以下問題，可以回滾：

* [確保有足夠的磁碟空間](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [完全備份AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [備份/etc的更改](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [生成quickstart.properties檔案](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [配置工作流和審核日誌清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [安裝、配置和運行升級前任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [禁用自定義登錄模組](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [從/install目錄中刪除更新](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [停止任何冷備用實例](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [停用自訂排程工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [執行離線修訂清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [執行資料儲存廢棄項目收集](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [視需要升級資料庫模式](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [刪除可能妨礙升級的用戶](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [旋轉日誌檔案](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 確保有足夠的磁碟空間{#ensure-sufficient-disk-space}

執行升級時，除了內容和代碼升級活動外，還需要執行儲存庫遷移。 遷移將以新的段Tar格式建立儲存庫的副本。 因此，您需要足夠的磁碟空間來保留第二個可能更大的儲存庫版本。

## 完全備AEM份{#fully-back-up-aem}

應AEM在開始升級之前完全備份。 請務必備份您的儲存庫、應用程式安裝、資料儲存和Mongo實例（如果適用）。 有關備份和恢復實例的詳AEM細資訊，請參見[備份和恢復](/help/sites-administering/backup-and-restore.md)。

## 備份對/etc {#backup-changes-etc}的更改

升級過程在維護和合併儲存庫中`/apps`和`/libs`路徑下的現有內容和配置方面做得很好。 對於對`/etc`路徑所做的更改（包括上下文集線器配置），通常需要在升級後重新應用這些更改。 雖然升級將會對`/var`下無法合併的任何更改進行備份，但建議在開始升級之前手動備份這些更改。

## 生成快速啟動。properties檔案{#generate-quickstart-properties}

從jarAEM檔案啟動時，將在`crx-quickstart/conf`下生成`quickstart.properties`檔案。 如AEM果以前只使用啟動指令碼啟動，則此檔案將不存在，並且升級將失敗。 請確保檢查此檔案是否存在，並從jarAEM檔案（如果不存在）重新啟動。

## 配置工作流和審核日誌清除{#configure-wf-audit-purging}

`WorkflowPurgeTask`和`com.day.cq.audit.impl.AuditLogMaintenanceTask`任務需要單獨的OSGi配置，沒有這些配置將無法工作。 如果在升級前任務執行期間失敗，則最可能的原因是缺少配置。 因此，如果您不想運行這些任務，請務必為這些任務添加OSGi配置，或將它們從升級前優化任務清單中完全刪除。 有關配置工作流清除任務的文檔，請訪問[管理工作流實例](/help/sites-administering/workflows-administering.md) ，並可在[6](/help/sites-administering/operations-audit-log.md)的審核日誌維護中找到審核日誌維護任務配置AEM。

有關CQ 5.6上的工作流和審核日誌清除以及6.0上的審核日誌清除AEM，請參閱[清除工作流和審核節點](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html)。

## 安裝、配置和運行升級前任務{#install-configure-run-pre-upgrade-tasks}

由於定制級別允許AEM，環境通常不遵循統一的升級方式。 因此，建立標準化的升級程式是個困難的程式。

在舊版中，停止或無法AEM安全恢復的升級也很困難。 這會導致需要重新啟動完整升級程式或執行有缺陷的升級而未觸發任何警告的情況。

為瞭解決這些問題，Adobe在升級程式中增加了幾項增強功能，使其更具彈性，而且使用起來更方便。 以前必須手動執行的升級前維護任務正在優化和自動化。 此外，已新增升級後報表，讓程式可以完全審查，以期更容易發現任何問題。

升級前維護任務目前分散在手動執行部分或全部的各種介面上。 6.3中引入的升級前維護優化AEM功能，可讓您以統一的方式觸發這些工作，並可視需要檢查結果。

升級前最佳化步驟中包含的所有工作都與6.0以AEM後的所有版本相容。

### 如何設定{#how-to-set-it-up}

在AEM6.3和更高版本中，升級前維護優化任務包含在快速啟動jar中。 如果您從舊版6升級，AEM則可透過個別的套件使用，您可從「套件管理員」下載。

您可以在以下位置找到包：

* [從AEM6.0升級](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [從AEM6.1升級](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [從AEM6.2升級](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### 如何使用{#how-to-use-it}

`PreUpgradeTasksMBean` OSGI元件預配置了可一次運行的升級前維護任務清單。 您可以按照以下過程配置任務：

1. 瀏覽至&#x200B;*https://serveraddress:serverport/system/console/configMgr*，前往Web主控台

1. 搜索「**預升級任務**」，然後按一下第一個匹配元件。 元件的全名為`com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. 修改需要運行的維護任務清單，如下所示：

   ![1487758925984](assets/1487758925984.png)

根據用於啟動實例的運行模式，任務清單會有所不同。 以下是每個維護任務的運行模式說明。

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
   <td>會進行標籤和掃描。 對於共用資料儲存，請刪除此步驟，然後在執行前手動或正確地準備實例。<br /></td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>必須在運行前配置AdobeGranite Workflow Purge Configuration OSGi。</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>對於6.0到6.2AEM上的TarMK實例，請改為手動運行離線修訂清除。</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>必須在運行前配置Audit Log Purge Scheduler OSGi配置。</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>`DataStoreGarbageCollectionTask` 正在調用帶有標籤和掃描階段的資料儲存廢棄項目收集操作（如果使用）。對於使用共用資料儲存的部署，請確保重新配置或正確地準備實例，以避免刪除其他實例引用的項。 這可能需要在觸發此升級前任務之前，在所有實例上手動運行標籤階段。

### Default Configuration of the Pre-Upgrade Health Checks {#default-configuration-of-the-pre-upgrade-health-checks}

`PreUpgradeTasksMBeanImpl` OSGI元件預配置了升級前運行狀況檢查標籤清單，在調用`runAllPreUpgradeHealthChecks`方法時執行：

* **system** - granite維護健康檢查所使用的標籤

* **pre-upgrade**  —— 這是自訂標籤，可新增至所有可設定為在升級前執行的健康狀態檢查

可編輯清單。 您可以使用標籤以外的加號&#x200B;**(+)**&#x200B;和減號&#x200B;**(-)**&#x200B;按鈕來新增更多自訂標籤，或移除預設標籤。

**MBean方法**

可使用[JMX控制台](/help/sites-administering/jmx-console.md)訪問受管理的Bean功能。

您可以通過以下方式訪問MBean:

1. 前往JMX控制台&#x200B;*https://serveraddress:serverport/system/console/jmx*
1. 搜索&#x200B;**PreUpgradeTasks**&#x200B;並按一下結果

1. 從&#x200B;**Operations**&#x200B;區段中選擇任何方法，並在以下窗口中選擇&#x200B;**Invoke**。

以下是`PreUpgradeTasksMBeanImpl`公開的所有可用方法的清單：

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
   <td>以參數的名稱運行升級前維護任務。</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>檢查<code>runAllPreUpgradeTasksmaintenance</code>任務當前是否正在運行。</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>檢查是否當前正在運行任何升級前維護任務，並<br />返回包含當前運行任務名稱的陣列。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>動作</td>
   <td>顯示升級前維護任務的確切運行時間，其名稱為參數。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>動作</td>
   <td>顯示升級前維護任務的上次運行狀態，其名稱為參數。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>動作</td>
   <td><p>執行所有升級前的健康狀況檢查，並將其狀態儲存在位於sling home路徑中名為<code>preUpgradeHCStatus.properties</code>的檔案中。 如果<code>shutDownOnSuccess</code>參數設為<code>true</code>，則會關AEM閉實例，但僅當所有升級前運行狀況檢查都具有OK狀態時。</p> <p>屬性檔案將用作任何以後升級的先決條件<br /> ，如果升級前運行狀況檢查<br />執行失敗，則升級過程將停止。 如果您要忽略升級前的<br />運行狀況檢查的結果並且仍要啟動升級，則可以刪除該檔案。</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>動作</td>
   <td>列出當<br />升級到指定版本時，將不再滿足的所有導入包AEM。 目標AEM版本必須<br />作為參數。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>MBean方法可以通過以下方式調用：
>
>* JMX主控台
>* 連線至JMX的任何外部應用程式
>* cURL

>



## 禁用自定義登錄模組{#disable-custom-login-modules}

>[!NOTE]
>
>只有從5版升級時，才需要此AEM步驟。 您可完全略過它，以取得舊版AEM6的升級。

在Apache Oak中，自訂`LoginModules`在儲存庫層級的驗證配置方式已發生根本性改變。

在使AEM用CRX2組態的版本中，`repository.xml`檔案中會放置CRX2組態，而從AEM6歲起，則會透過Web Console在Apache Felix JAAS組態工廠服務中進行。

因此，升級後，必須停用並重新建立Apache Oak的任何現有組態。

要禁用`repository.xml`的JAAS配置中定義的自定義模組，您需要修改配置以使用預設`LoginModule`，如本例所示：

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
>如需詳細資訊，請參閱[使用外部登入模組進行驗證](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)。
>
>有關6中`LoginModule`配置的示例AEM，請參見[使用AEM6](/help/sites-administering/ldap-config.md)配置LDAP。

## 從/install目錄{#remove-updates-install-directory}中刪除更新

>[!NOTE]
>
>在關閉實例後，僅從crx-quickstart/install目錄中刪除包AEM。 這是開始就地升級程式之前的最後步驟之一。

刪除通過本地檔案系統上的`crx-quickstart/install`目錄部署的所有服務包、功能包或修補程式。 如此可避免在更新完成後，在新版本之上無意中安裝舊的修補程式和AEMService Pack。

## 停止任何冷備用實例{#stop-tarmk-coldstandby-instance}

如果使用TarMK冷備用，請停止任何冷備用實例。 這些功能可確保在升級時有效率地回到線上。 升級成功後，需要從升級的主實例重建冷備用實例。

## 停用自訂排程工作{#disable-custom-scheduled-jobs}

停用應用程式程式碼中包含的任何OSGi排程工作。

## 執行離線修訂清除{#execute-offline-revision-cleanup}

>[!NOTE]
>
>此步驟僅對於TarMK安裝是必要的

如果使用TarMK，您應在升級前執行離線修訂清除。 這將使儲存庫遷移步驟和後續升級任務的執行速度大大加快，並有助於確保線上修訂清除功能在升級完成後能夠成功執行。 有關運行離線修訂清除的資訊，請參閱[執行離線修訂清除](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup)。

## 執行資料儲存廢棄項目收集{#execute-datastore-garbage-collection}

>[!NOTE]
>
>只有執行crx3的例項才需要此步驟

對CRX3實例運行修訂清除後，您應運行資料儲存廢棄項目收集來刪除資料儲存中任何未引用的blob。 如需指示，請參閱[Data Store Garbage Collection](/help/sites-administering/data-store-garbage-collection.md)上的說明檔案。

## 如果需要，請升級資料庫模式{#upgrade-the-database-schema-if-needed}

通常，用於持久性的基AEM礎Apache Oak堆棧將在需要時負責升級資料庫架構。

但是，當模式無法自動升級時，可能會發生這種情況。 這些環境大多是高安全性環境，資料庫在權限非常有限的用戶下運行。 如果發生此情況，AEM將繼續使用舊模式。

為防止這種情況發生，您需要按照以下過程升級模式：

1. 關閉需AEM要升級的實例。
1. 升級資料庫模式。 請查閱您的資料庫類型檔案，以瞭解您要達到此目的，需要使用哪些工具。

   如需Oak如何處理架構升級的詳細資訊，請參閱Apache網站](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade)上的[本頁。

1. 繼續升級AEM。

## 刪除可能妨礙升級的用戶{#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>只有在下列情況下，才需要執行此升級前維護任務：
>
>* 您是從6.3AEM以AEM前的版本升級
>* 在升級期間，您會遇到下列任何錯誤。

>



有些例外情況是，服務使用者可能會在舊版中被不當AEM標籤為一般使用者。

如果發生此情況，升級將失敗，並出現如下訊息：

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

為瞭解決此問題，請確定您執行下列動作：

1. 將例項與生產流量分離
1. 建立導致問題的用戶的備份。 您可以通過「包管理器」執行此操作。 有關詳細資訊，請參閱[如何使用包。](/help/sites-administering/package-manager.md)
1. 刪除導致問題的用戶。 以下是可能屬於此類別的使用者清單：

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## 旋轉日誌檔案{#rotate-log-files}

建議您在開始升級之前，先封存您目前的記錄檔。 這樣，在升級期間和升級後監視和掃描日誌檔案將更加容易，以識別和解決可能發生的任何問題。
