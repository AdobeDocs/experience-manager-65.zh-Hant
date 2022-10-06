---
title: 使用JMX控制台監視伺服器資源
seo-title: Monitoring Server Resources Using the JMX Console
description: 了解如何使用JMX控制台監視伺服器資源。
seo-description: Learn how to monitor server resources using the JMX console.
uuid: 0a28aafe-61b2-472b-8f8f-2cd6540cbfee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 873ce073-0055-4e1b-b3c6-ae7967700894
docset: aem65
exl-id: eabd8335-6140-4c15-8cff-21608719aa5f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4957'
ht-degree: 1%

---

# 使用JMX控制台監視伺服器資源{#monitoring-server-resources-using-the-jmx-console}

JMX控制台允許您監視和管理CRX伺服器上的服務。 以下各節概述了通過JMX框架公開的屬性和操作。

如需如何使用主控台控制項的資訊，請參閱 [使用JMX控制台](#using-the-jmx-console). 有關JMX的背景資訊，請參見 [Java管理擴展(JMX)技術](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) 頁面。

有關使用JMX控制台建立MBean以管理服務的資訊，請參見 [將服務與JMX控制台整合](/help/sites-developing/jmx-integration.md).

## 工作流程維護 {#workflow-maintenance}

管理執行中、已完成、過時和失敗的工作流程例項的操作。

* 域：com.adobe.granite.workflow
* 類型：維護

>[!NOTE]
>
>請參閱 [工作流程控制台](/help/sites-administering/workflows-administering.md) 有關其他工作流管理工具，以及可能的工作流實例狀態的說明。

### 運作 {#operations}

**listRunningWorkflowsPerModel** 列出每個工作流模型正在運行的工作流實例數。

* 引數：無
* 傳回值：包含Count和ModelId列的表格資料。

**listCompletedWorkflowsPerModel** 列出每個工作流模型的已完成工作流實例數。

* 引數：無
* 傳回值：包含Count和ModelId列的表格資料。

**returnWorkflowQueueInfo** 列出已處理和已排入處理佇列的工作流程項目的相關資訊。

* 引數：無
* 傳回值：包含下列欄的表格資料：

   * 工作
   * 隊列名
   * 作用中的工作
   * 平均處理時間
   * 平均等待時間
   * 取消的工作
   * 失敗的工作
   * 已完成的作業
   * 已處理的作業
   * 排入佇列的作業

**returnWorkflowJobTopicInfo** 列出工作流作業的處理資訊，按主題組織。

* 引數：無
* 傳回值：包含下列欄的表格資料：

   * 主題名稱
   * 平均處理時間
   * 平均等待時間
   * 取消的工作
   * 失敗的工作
   * 已完成的作業
   * 已處理的作業

**returnFailedWorkflowCount** 顯示失敗的工作流實例數。 您可以指定工作流模型來查詢或檢索所有工作流模型的資訊。

* 引數:

   * 模型：要查詢的模型ID。 要查看所有工作流模型的失敗工作流實例計數，請指定不值。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：失敗的工作流實例數。

**returnFailedWorkflowCountPerModel** 顯示每個工作流模型失敗的工作流實例數。

* 引數：無。
* 傳回值：包含「計數」和「模型ID」欄的表格資料。

**terminateFailedInstances** 終止已失敗的工作流實例。 您可以終止所有失敗實例，或僅終止特定模型的失敗實例。 您可以選擇在執行個體終止後重新啟動。 您也可以測試操作，以查看結果而不實際執行操作。

* 引數:

   * 重新啟動執行個體：（選用）指定 `true` 以在執行個體終止後重新啟動。 預設值為 `false` 導致終止的工作流實例不重新啟動。
   * 乾跑：（選用）指定 `true` 來查看操作結果，而不實際執行操作。 預設值為 `false` 導致執行操作。
   * 模型：（可選）應用操作的模型ID。 指定任何模型以將操作應用於所有工作流模型的失敗實例。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：終止的例項的表格資料，包含下列各欄：

   * 發起人
   * InstanceId
   * ModelId
   * 裝載
   * StartComment
   * WorkflowTitle

**retryFailedWorkItems** 嘗試執行已失敗的工作項步驟。 您可以重試所有失敗的工作項，或僅重試特定工作流模型的失敗工作項。 您可以選擇測試工序以查看結果，而不實際執行工序。

* 引數:

   * 乾跑：（選用）指定 `true` 來查看操作結果，而不實際執行操作。 預設值為 `false` 導致執行操作。
   * 模型：（可選）應用操作的模型ID。 指定任何模型以將操作應用於所有工作流模型的失敗工作項。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：重試失敗工作項的表資料，包括以下列：

   * 發起人
   * InstanceId
   * ModelId
   * 裝載
   * StartComment
   * WorkflowTitle

**清除活動** 移除特定頁面的作用中工作流程例項。 您可以清除所有模型的活動實例，或僅清除特定模型的實例。 您可以選擇測試操作以查看結果，而不實際執行操作。

* 引數:

   * 模型：（可選）應用操作的模型ID。 指定任何模型以將操作應用於所有工作流模型的工作流實例。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 自工作流程開始的天數：要清除的工作流實例的年齡（以天為單位）。
   * 乾跑：（選用）指定 `true` 來查看操作結果，而不實際執行操作。 預設值為 `false` 導致執行操作。

* 傳回值：已清除的作用中工作流程例項的表格資料，包括下列欄：

   * 發起人
   * InstanceId
   * ModelId
   * 裝載
   * StartComment
   * WorkflowTitle

**countStaleWorkflows** 傳回過時的工作流程例項數。 您可以為所有工作流模型或特定模型擷取過時例項的數量。

* 引數:

   * 模型：（可選）應用操作的模型ID。 指定任何模型以將操作應用於所有工作流模型的工作流實例。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：過時的工作流實例數。

**restartStaleWorkflows** 重新啟動過時的工作流實例。 您可以重新啟動所有過時實例，或僅重新啟動特定型號的過時實例。 您也可以測試操作，以查看結果而不實際執行操作。

* 引數:

   * 模型：（可選）應用操作的模型ID。 指定任何模型以將操作應用於所有工作流模型的陳舊實例。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 乾跑：（選用）指定 `true` 來查看操作結果，而不實際執行操作。 預設值為 `false` 導致執行操作。

* 傳回值：重新啟動的工作流實例清單。

**fetchModelList** 列出所有工作流模型。

* 引數：無
* 傳回值：標識工作流模型（包括ModelId和ModelName列）的表格資料。

**countRunningWorkflows** 傳回執行中的工作流程例項數。 您可以為所有工作流模型或特定模型檢索正在運行的實例數。

* 引數:

   * 模型：（可選）傳回執行個體數的模型ID。 指定不要返回所有工作流模型的運行實例數的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：正在運行的工作流實例的數量。

**countCompletedWorkflows** 傳回已完成的工作流程例項數。 您可以為所有工作流模型或特定模型檢索已完成實例的數量。

* 引數:

   * 模型：（可選）傳回已完成例項數的模型ID。 指定不要返回所有工作流模型的已完成實例數的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：已完成的工作流實例數。

**purgeCompleted** 從存放庫中移除特定頁面已完成工作流程的記錄。 請定期使用此操作，以在大量使用工作流時最小化儲存庫的大小。 您可以清除所有模型的已完成實例，或僅清除特定模型的實例。 您可以選擇測試操作以查看結果，而不實際執行操作。

* 引數:

   * 模型：（可選）應用操作的模型ID。 指定任何模型以將操作應用於所有工作流模型的工作流實例。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 自工作流完成後的天數：工作流實例處於完成狀態的天數。
   * 乾跑：（選用）指定 `true` 來查看操作結果，而不實際執行操作。 預設值為 `false` 導致執行操作。

* 傳回值：關於已清除的已完成工作流實例的表格資料，包括以下列：

   * 發起人
   * InstanceId
   * ModelId
   * 裝載
   * StartComment
   * WorkflowTitle

## 存放庫 {#repository}

CRX存放庫相關資訊

* 域：com.adobe.granite
* 類型：存放庫

### 屬性 {#attributes}

**名稱** JCR存放庫實作的名稱。 唯讀.

**版本** 存放庫實作版本。 唯讀.

**HomeDir** 儲存庫所在的目錄。 預設位置為 &lt;quickstart_jar_location>/crx-quickstart/repository。 唯讀.

**客戶名稱** 向其頒發軟體許可證的客戶的名稱。 唯讀.

**LicenseKey** 用於此安裝儲存庫的唯一許可證密鑰。 唯讀.

**AvailableDiskSpace** 儲存庫的此實例可用的磁碟空間（以兆位元組為單位）。 唯讀.

**MaximumNumberOfOpenFiles** 一次可開啟的檔案數。 唯讀.

**SessionTracker** crx.debug.sessions系統變數的值。 true表示偵錯工作階段。 false表示正常會話。 讀/寫。

**描述符** 代表存放庫屬性的機碼值組集。 所有屬性均為唯讀。

<table>
 <tbody>
  <tr>
   <th>關鍵</th>
   <th>值</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>指示節點和節點的屬性是否可以具有相同的名稱。 true表示支援相同的名稱，false表示不支援。 </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>指示不可引用節點標識符的穩定性。 可能有下列值：
    <ul>
     <li>identifier.stability.indement.duration:識別碼不會變更。</li>
     <li>identifier.stability.method.duration:識別碼可在方法呼叫之間變更。</li>
     <li>identifier.stability.save.duration:識別碼在儲存/重新整理週期內不會變更。</li>
     <li>identifier.stability.session.duration:識別碼在工作階段期間不會變更。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>指示是否支援JCR 1.0 XPath查詢語言。 true表示支援，false表示不支援。</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>system.id檔案中的系統標識符。</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>指示是否支援JCR 1.0 XPath查詢語言。 true表示支援，false表示不支援。</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>存放庫實作的版本。</td>
  </tr>
  <tr>
   <td>option.update.primary.node.type.supported</td>
   <td>指示是否可以更改節點的主節點類型。 true表示可以更改主節點類型，false表示不支援更改。</td>
  </tr>
  <tr>
   <td>option.node.type.management.supported</td>
   <td>指示是否支援節點類型管理。 true表示支援，false表示不支援。</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>指示是否可以覆蓋節點類型的繼承屬性或子節點定義。 true表示支援覆蓋，而false表示不覆蓋。</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true表示支援非同步觀察存放庫變更。 支援非同步觀察使應用程式能夠接收和響應每次更改的通知。</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true指示jcr:score假屬性在XPath和SQL查詢中可用，這些查詢包含jcrfn:contains（在XPath中）或CONTAINS（在SQL中）函式以執行全文搜索。</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true表示儲存庫支援簡單的版本設定。 通過簡單的版本設定，儲存庫可維護一系列連續的節點版本。</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true表示儲存庫支援使用API建立和刪除工作區。</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true表示儲存庫支援添加和刪除現有節點的mixin節點類型。</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true表示儲存庫允許節點定義將主項作為子項包含。 您不需知道項目名稱，即可透過API存取主要項目。</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true表示LEVEL_1_SUPPORTED和OPTION_XML_IMPORT_SUPPORTED均為true。</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true表示存放庫使用API提供寫入存取。 false表示只讀訪問。</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true表示可以更改現有節點正在使用的節點定義。</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>儲存庫實作的JCR規範版本。</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true表示應用程式可以執行對儲存庫的日誌觀察。 通過日誌觀察，可以獲得一組特定時間段的更改通知。 </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>儲存庫支援的查詢語言。 沒有值表示不支援查詢。</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>true表示儲存庫支援將節點導出為XML代碼。</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>true表示儲存庫支援註冊具有多個二進位屬性的節點類型。 false表示節點類型支援單個二進位屬性。</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>true表示儲存庫支援訪問控制，用於設定和確定節點訪問的用戶權限。</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true表示儲存庫支援配置和基線。</td>
  </tr>
  <tr>
   <td>option.shareable.nodes.supported</td>
   <td>true表示儲存庫支援建立可共用節點。</td>
  </tr>
  <tr>
   <td>crx.cluster.id</td>
   <td>儲存庫群集的標識符。</td>
  </tr>
  <tr>
   <td>query.stored.queries.supported</td>
   <td>true表示儲存庫支援儲存的查詢。</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true表示儲存庫支援全文搜索。</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>指示對節點類型繼承的儲存庫支援級別。 可能有下列值：</p> <p>node.type.management.inheritation.minimal:主節點類型的註冊僅限於那些僅具有nt:base作為超類型的節點類型。 混合節點類型的註冊僅限於沒有超類型的節點類型。</p> <p>node.type.management.inheritation.single:主節點類型的註冊僅限於具有超類型的節點類型。 混合節點類型的註冊僅限於那些最多具有一個超類型的節點類型。</p> <p><br /> node.type.management.inheritation.multiple:主節點類型可註冊為一個或多個超類型。 Mixin節點類型可以用零個或多個超類型註冊。</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>true表示此群集節點是群集的首選主節點。</td>
  </tr>
  <tr>
   <td>option.transactions.supported</td>
   <td>true表示儲存庫支援事務。</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor.url</td>
   <td>儲存庫供應商的URL。</td>
  </tr>
  <tr>
   <td>node.type.management.value.constraints.supported</td>
   <td>true表示儲存庫支援節點屬性的值約束。</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>javax.jcr.PropertyType常數的陣列，它表示註冊節點類型可以指定的屬性類型。 零長陣清單示註冊的節點類型不能指定屬性定義。 屬性類型為字串、URI、布林值、長、雙精度、小數、二進位、日期、名稱、路徑、弱引用、引用和未定義（如果支援）</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true表示儲存庫支援保存子節點的順序。</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>儲存庫供應商的名稱。</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>查詢中對聯接的支援級別。 可能有下列值：</p>
    <ul>
     <li>query.joins.none:不支援加入。 查詢可使用一個選擇器。</li>
     <li>query.joins.inner:支援內連接。</li>
     <li>query.joins.inner.outer:對內連接和外連接的支援。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>org.apache.jackrabbit.spi.commons.AdditionalEventInfo</td>
   <td> </td>
  </tr>
  <tr>
   <td>query.xpath.doc.order</td>
   <td>true表示儲存庫支援XPath 1.0查詢語言。</td>
  </tr>
  <tr>
   <td>query.jcrpath</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.xml.import.supported</td>
   <td>true表示儲存庫支援將XML代碼作為內容導入。</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true表示儲存庫支援具有相同名稱的同級節點（具有相同父節點）。</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true表示儲存庫支援具有剩餘定義的名稱屬性。 如果支援，項目定義的名稱屬性可以是星號("*")。</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true表示建立節點時，儲存庫支援自動建立節點的子項（節點或屬性）。</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true表示此儲存庫節點是群集的主節點。</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>true表示option.xml.export.support為true，而query.languages的長度為非零。</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true表示儲存庫支援未歸檔的內容。 未歸檔節點不屬於儲存庫層次結構。</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>儲存庫實作的JCR規範的名稱。</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true表示儲存庫支援完全版本設定。</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>儲存庫的名稱。</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true表示儲存庫支援鎖定節點。 鎖定可讓使用者暫時阻止其他使用者進行變更。</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true表示儲存庫支援活動。 活動是一組在合併至其他工作區的工作區中執行的變更。</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true表示儲存庫支援的節點屬性可以有零個或多個值。</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true表示儲存庫支援使用外部保留管理應用程式將保留策略應用於內容，並支援保留和釋放。</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true表示儲存庫支援生命週期管理。</td>
  </tr>
 </tbody>
</table>

**工作區名稱** 儲存庫中工作區的名稱。 唯讀.

**DataStoreGarbageCollectionDelay** 垃圾收集在掃描每十個節點後所睡眠的時間（毫秒）。 讀/寫。

**BackupDelay** 備份進程在備份的每個步驟之間睡眠的時間（以毫秒為單位）。 讀/寫。

**BackupInProgress** 值為true表示正在執行備份進程。 唯讀.

**備份進度** 對於當前備份，已備份的所有檔案的百分比。 唯讀.

**CurrentBackupTarget** 對於當前備份，為儲存備份檔案的ZIP檔案。 當備份未進行時，不會顯示任何值。 唯讀.

**BackupWasSuccessful** 值true表示當前備份期間未發生任何錯誤，或未進行任何備份。 false表示當前備份期間出錯。 唯讀.

**BackupResult** 當前備份的狀態。 可能有下列值：

* 正在進行備份：當前正在執行備份。
* 已取消備份：已取消備份。
* 備份已完成，但出現錯誤：備份期間出錯。 錯誤消息提供有關原因的資訊。
* 備份已完成：備份成功。
* 迄今未執行任何備份：正在進行備份。

唯讀.

**TarOptimizationRunningSince** 當前TAR檔案優化過程開始的時間。 唯讀.

**TarOptimizationDelay** TAR最佳化程式在程式的每個步驟之間睡眠的時間（毫秒）。 讀/寫。

**ClusterProperties** 代表叢集屬性和值的鍵值值組集。 表中的每一行都表示群集屬性。 唯讀.

**ClusterNodes** 儲存庫群集的成員。

**ClusterId** 此儲存庫群集的標識符。 唯讀.

**ClusterMasterId** 此儲存庫群集的主節點的標識符。 唯讀.

**ClusterNodeId** 儲存庫群集的此節點的標識符。 唯讀.

### 運作 {#operations-1}

**createWorkspace** 在此儲存庫中建立工作區。

* 引數:

   * 名稱：代表新工作區名稱的字串值。

* 傳回值：無

**runDataStoreGarbageCollection** 在儲存庫節點上執行垃圾收集。

* 引數:

   * 刪除：指示是否刪除未使用的儲存庫項目的布爾值。 若值為true，則會刪除未使用的節點和屬性。 若值為false，則會掃描所有節點，但不會刪除任何節點。

* 傳回值：無

**stopDataStoreGarbageCollection** 停止運行中的資料儲存垃圾收集。

* 引數：無
* 傳回值：目前狀態的字串表示

**startBackup** 備份ZIP檔案中的儲存庫資料。

* 引數:

   * `target`:（可選）A `String` 值，表示要存檔儲存庫資料的ZIP檔案或目錄的名稱。 若要使用ZIP檔案，請加入ZIP檔案副檔名。 若要使用目錄，請不包含副檔名。

      要執行增量備份，請指定以前用於備份的目錄。

      您可以指定絕對路徑或相對路徑。 相對路徑相對於crx-quickstart目錄的父目錄。

      若未指定值，預設值為 `backup-currentdate.zip` ，其中 `currentdate` 為格式 `yyyyMMdd-HHmm`.

* 傳回值：無

**cancelBackup** 停止當前備份進程並刪除該進程為存檔資料而建立的臨時存檔。

* 引數：無
* 傳回值：無

**blockRepositoryWrites** 封鎖對存放庫資料的變更。 所有儲存庫備份偵聽器都會收到塊的通知。

* 引數：無
* 傳回值：無

**uncomplatRepositoryWrites** 從儲存庫中移除區塊。 所有儲存庫備份偵聽器都會收到塊刪除的通知。

* 引數：無
* 傳回值：無

**startTarOptimization** 使用tarOptimizationDelay的預設值啟動TAR檔案優化過程。

* 引數：無
* 傳回值：無

**stopTarOptimization** 停止TAR檔案優化。

* 引數：無
* 傳回值：無

**tarIndexMerge** 合併所有TAR集的頂級索引檔案。 頂級索引檔案是具有不同主要版本的檔案。 例如，以下檔案合併到檔案index_3_1.tar中：index_1_1.tar、index_2_0.tar、index_3_0.tar。 已合併的檔案將被刪除（在上一示例中，將刪除index_1_1.tar、index_2_0.tar和index_3_0.tar）。

* 引數:

   * `background`:一個布林值，指示是否在後台運行操作，以便在執行期間使用Web控制台。 true值會在背景執行操作。

* 傳回值：無

**becoClusterMaster** 將此儲存庫節點設定為群集的主節點。 如果尚未主，此命令將停止當前主實例的偵聽器，並在當前節點上啟動主監聽器。 然後，此節點將設定為主節點並重新啟動，導致群集中的所有其他節點（即由主節點控制的節點）連接到此實例。

* 引數：無
* 傳回值：無

**joinCluster** 將此儲存庫作為由群集主節點控制的節點添加到群集中。 您必須提供用戶名和密碼以用於身份驗證。 連線使用基本驗證。 在將安全憑證發送到伺服器之前，安全憑證是base-64編碼的。

* 引數:

   * `master`:表示運行主儲存庫節點的電腦的IP地址或電腦名稱的字串值。
   * `username`:用於對群集進行身份驗證的名稱。
   * `password`:用於驗證的密碼。

* 傳回值：無

**traversalCheck** 遍歷和可選地修復從特定節點開始的子樹中的不一致。 持久性管理器的文檔將詳細介紹此內容。

**consistencyCheck** 檢查並選擇性修正資料存放區中的一致性。 這在資料存放區的檔案中會詳細說明。

## 儲存庫統計資訊（時間系列） {#repository-statistics-timeseries}

TimeSeries欄位對於每個統計類型的值 `org.apache.jackrabbit.api.stats.RepositoryStatistics` 定義。

* 網域: `com.adobe.granite`
* 類型: `TimeSeries`
* 名稱：下列其中一個值來自 `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` 枚舉類：

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * BUNDLE_COUNTER
   * BUNDLE_READ_COUNTER
   * BUNDLE_WRITE_AVERAGE
   * BUNDLE_WRITE_COUNTER
   * BUNDLE_WRITE_DURATION
   * BUNDLE_WS_SIZE_COUNTER
   * QUERY_AVERAGE
   * QUERY_COUNT
   * QUERY_DURATION
   * SESSION_COUNT
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * SESSION_WRITE_DURATION

### 屬性 {#attributes-1}

針對報告的每個統計類型提供以下屬性：

* ValuePerSecond:最後一分鐘的每秒測量值。 唯讀.
* ValuePerMinute:前一小時每分鐘的測量值。 唯讀.
* ValuePerHour:上週的每小時測量值。 唯讀.
* ValuePerWeek:過去三年的每週測量值。 唯讀.

## 儲存庫查詢統計資料 {#repository-query-stats}

關於存放庫查詢的統計資訊。

* 域：com.adobe.granite
* 類型：QueryStat

### 屬性 {#attributes-2}

**慢速查詢** 已花費最長時間完成的儲存庫查詢的相關資訊。 唯讀.

**SlowQuerysQueueSize** 要包含在SlowQuerys清單中的查詢數上限。 讀寫。

**熱門查詢** 最常發生的存放庫查詢的相關資訊。 唯讀.

**熱門查詢隊列大小** PoporalQuerys清單中的查詢數上限。 讀寫。

### 運作 {#operations-2}

**clearSlowQuerysQueue** 從SlowQuerys清單中刪除所有查詢。

* 引數：無
* 傳回值：無

**clearPopalQueriesQueue** 從PopalQuerys清單中刪除所有查詢。

* 引數：無
* 傳回值：無

## 複寫代理程式 {#replication-agents}

監視每個複製代理的服務。 建立復寫代理時，該服務會自動出現在JMX控制台中。

* **域：** com.adobe.granite.replication
* **類型：** 代理
* **名稱：** 無值
* **屬性：** {id=&quot;*名稱*&quot;}，其中 *名稱* 是代理Name屬性的值。

### 屬性 {#attributes-3}

**Id** 表示複製代理配置標識符的字串值。 多個代理可以使用相同的配置。 唯讀.

**有效** 指示代理是否已正確配置的布爾值：

* `true`:配置有效。
* `false` :設定包含錯誤。

唯讀.

**已啟用** 指示是否啟用代理的布爾值：

* `true`: 已啟用.
* `false`: 已停用.

**QueueBlocked** 指示隊列是否存在且被阻止的布爾值：

* `true`: 已封鎖. 自動重試掛起。
* `false`:未阻止或不存在。

唯讀.

**QueuePaused** 指示是否暫停作業隊列的布爾值：

* `true`:暫停（暫停）
* `false`:未暫停或不存在。

讀寫。

**QueueNumEntries** 表示代理隊列中作業數的整數值。 唯讀.

**QueueStatusTime** 一個日期值，指示獲取顯示狀態值時伺服器上的時間。 值與頁面載入時間對應。 唯讀.

**QueueNextRetryTime** 對於被阻止的隊列，一個日期值，指示下次自動重試的時間。 如果沒有出現時間，則不會阻止隊列。 唯讀.

**QueueProcessingSince** 指出當前作業開始處理的日期值。 當未顯示任何時間時，隊列將被阻止或空閒。 唯讀.

**QueueLastProcessTime** 指示上一個作業完成時間的日期值。 唯讀.

### 運作 {#operations-3}

**queueForceRetry** 對於被阻止的隊列，向隊列發出重試命令。

* 引數：無
* 傳回值：無

**queueClear** 從隊列中刪除所有作業。

* 引數：無
* 傳回值：無

## Sling引擎 {#sling-engine}

提供HTTP要求的統計資料，以便您監控SlingRequestProcessor服務的效能。

* 域：org.apache.sling
* 類型：引擎
* 屬性：{service=RequestProcessor}

### 屬性 {#attributes-4}

**RequestsCount** 自上次重設統計資料後發生的請求數。

**MinRequestDurationMsec** 自上次重設統計資料以來，處理請求所需的最短時間（以毫秒為單位）。

**MaxRequestDuratioMsec** 自上次重設統計資料以來，處理請求所需的最長時間量（以毫秒為單位）。

**StandardDevarationDurationMsec** 處理請求所需時間量的標準差。 自上次重設統計資料後，標準差會使用所有請求來計算。

**MeanRequestDurationMsec** 處理請求所需的平均時間。 自上次重設統計資料後，平均值會使用所有請求計算

### 運作 {#operations-4}

**resetStatistics** 將所有統計資訊設為零。 在您需要分析特定時間範圍內的請求處理效能時，重設統計資料。

* 引數：無
* 傳回值：無

**id** 套件ID的字串表示法。

**已安裝** 指示是否已安裝包的布爾值：

* `true`: 已安裝.
* `false`: 未安裝.

**installedBy** 上次安裝套件的使用者ID。

**installedDate** 上次安裝包的日期。

**大小** 一個長值，它以位元組為單位保存包的大小。


## 快速啟動啟動器 {#quickstart-launcher}

有關啟動過程和快速啟動啟動器的資訊。

* 域：com.adobe.granite.quickstart
* 類型：啟動器

### 運作 {#operations-5}

**記錄**

在「快速啟動」窗口中顯示消息。

引數:

* p1:A `String` 代表要顯示的訊息的值。
* 傳回值：無

**startupFinished**

調用伺服器啟動器的startupFinished方法。 方法會嘗試在網頁瀏覽器中開啟歡迎頁面。

* 引數：無
* 傳回值：無

**startupProgress**

設定伺服器啟動進程的完成值。 QuickStart窗口上的進度欄表示完成值。

* 引數:
   * p1:浮點數值，以小數表示啟動過程的完成量。 值應介於零和1之間。 例如，0.3表示完成30%。
* 傳回值：無。

## 第三方服務 {#third-party-services}

多個第三方伺服器資源安裝MBean，這些MBean向JMX控制台公開屬性和操作。 下表列出協力廠商資源，並提供連結以取得詳細資訊。

<table>
 <tbody>
  <tr>
   <th>網域</th>
   <th>類型</th>
   <th>MBean類</th>
  </tr>
  <tr>
   <td>JMI實作</td>
   <td>MBeanServerDelegate</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerDelegate.html">javax.management.MBeanServerDelegate</a></td>
  </tr>
  <tr>
   <td>com.sun.management</td>
   <td>HotSpotDiagnostic</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/jre/api/management/extension/com/sun/management/HotSpotDiagnosticMXBean.html">com.sun.management.HotSpotDiagnosticMXBean</a></td>
  </tr>
  <tr>
   <td>java.lang</td>
   <td>
    <ul>
     <li>類載入</li>
     <li>編譯</li>
     <li>垃圾收集器</li>
     <li>記憶體</li>
     <li>MemoryManager</li>
     <li>記憶體池</li>
     <li>作業系統</li>
     <li>執行階段</li>
     <li>線程</li>
    </ul> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.management</a> 套件</td>
  </tr>
  <tr>
   <td>java.util.logging</td>
   <td> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/java/util/logging/LoggingMXBean.html">java.util.logging.LoggingMXBean</a></td>
  </tr>
  <tr>
   <td>osgi.core</td>
   <td>
    <ul>
     <li>bundleState</li>
     <li>框架</li>
     <li>packageState</li>
     <li>serviceState</li>
    </ul> </td>
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a> 套件</td>
  </tr>
 </tbody>
</table>

## 使用JMX控制台 {#using-the-jmx-console}

JMX控制台顯示有關伺服器上運行的多項服務的資訊：

* 屬性：服務屬性，如配置或運行時資料。 屬性可以是只讀的或是讀寫的。
* 操作：可在服務上調用的命令。

隨OSGi服務部署的MBean會將服務屬性和操作公開到控制台。 MBean確定公開的屬性和操作，以及屬性是只讀還是讀寫。

JMX控制台的首頁包含服務表。 表中的每一行代表由MBean公開的服務。

1. 開啟Web控制台，然後按一下「JMX」頁簽。 ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. 按一下服務的儲存格值，以查看服務的屬性和操作。
3. 要更改屬性值，請按一下該值，在出現的對話框中指定值，然後按一下「保存」。
4. 要調用服務操作，請按一下操作名，在出現的對話框中指定參數值，然後按一下調用。

## 使用外部JMX應用程式進行監控 {#using-external-jmx-applications-for-monitoring}

CRX允許外部應用程式通過 [Java管理擴展(JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html). 使用一般主控台，例如 [JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) 或特定於域的監控應用程式，允許獲取和設定CRX配置和屬性，以及監控效能和資源使用情況。

### 使用JConsole連接到CRX {#using-jconsole-to-connect-to-crx}

要使用JConsole連接到CRX，請執行以下步驟：

1. 開啟終端窗口。
1. 輸入以下命令：

   `jconsole`

JConsole將啟動，JConsole窗口將出現。

### 連接到本地CRX進程 {#connecting-to-a-local-crx-process}

JConsole將顯示本地Java虛擬機進程的清單。 該清單將包含兩個快速入門進程。 從本地進程清單（通常是PID較高的進程）中選擇快速啟動「CHILD」進程。

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### 連接到遠程CRX進程 {#connecting-to-a-remote-crx-process}

要連接到遠程CRX進程，承載遠程CRX進程的JVM必須啟用，以接受遠程JMX連接。

要啟用遠程JMX連接，在啟動JVM時必須設定以下系統屬性：

`com.sun.management.jmxremote.port=portNum`

在上述屬性中， `portNum` 是要啟用JMX RMI連接的埠號。 請務必指定未使用的埠號。 除了發佈用於本地訪問的RMI連接器外，設定此屬性還會使用眾所周知的名稱&quot;jmxrmi&quot;在指定埠的專用只讀註冊表中發佈一個附加的RMI連接器。

預設情況下，當啟用JMX代理進行遠程監視時，它將根據在啟動Java VM時需要使用以下系統屬性指定的密碼檔案使用密碼驗證：

`com.sun.management.jmxremote.password.file=pwFilePath`

請參閱 [相關JMX檔案](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html) 以了解有關設定密碼檔案的詳細說明。

範例:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### 使用CRX提供的MBean {#using-the-mbeans-provided-by-crx}

在連接到快速啟動進程後，JConsole為CRX正在運行的JVM提供了一系列常規監視工具。

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

若要存取CRX的內部監控和設定選項，請前往MBeans標籤，然後從左側的階層式內容樹狀結構中，選取您感興趣的屬性或操作區段。 例如， com.adobe.granite/Repository/Operations區段。

在該區段內，在左窗格中選取所需的屬性或操作。

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)
