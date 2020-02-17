---
title: 使用JMX控制台監控伺服器資源
seo-title: 使用JMX控制台監控伺服器資源
description: 瞭解如何使用JMX主控台監控伺服器資源。
seo-description: 瞭解如何使用JMX主控台監控伺服器資源。
uuid: 0a28aafe-61b2-472b-8f8f-2cd6540cbfee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 873ce073-0055-4e1b-b3c6-ae7967700894
docset: aem65
translation-type: tm+mt
source-git-commit: a268b7046430cc17c8b59b9306cf3533d73bb4a2

---


# 使用JMX控制台監控伺服器資源{#monitoring-server-resources-using-the-jmx-console}

JMX Console可讓您監控和管理CRX伺服器上的服務。 以下各節概述了通過JMX框架公開的屬性和操作。

如需如何使用主控台控制項的詳細資訊，請 [參閱使用JMX主控台](#using-the-jmx-console)。 有關JMX的背景資訊，請參 [閱Oracle網站上的](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) 「Java Management Extensions(JMX)技術」頁。

如需有關使用JMX主控台來建立MBean以管理您服務的詳細資訊，請參 [閱整合服務與JMX主控台](/help/sites-developing/jmx-integration.md)。

## 工作流程維護 {#workflow-maintenance}

管理運行、完成、過時和失敗的工作流實例的操作。

* 網域：com.adobe.granite.workflow
* 類型：維護

>[!NOTE]
>
>如需其他 [工作流程管理工具](/help/sites-administering/workflows-administering.md) ，以及可能的工作流程例項狀態說明，請參閱工作流程主控台。

### 作業 {#operations}

**listRunningWorkflowsPerModel** 列出每個工作流模型正在運行的工作流實例數。

* 引數：nown
* 傳回值：包含Count和ModelId列的表格式資料。

**listCompletedWorkflowsPerModel** 列出每個工作流模型的已完成工作流實例數。

* 引數：nown
* 傳回值：包含Count和ModelId列的表格式資料。

**returnWorkflowQueueInfo** 列出已處理和已排入處理佇列的工作流程項目的相關資訊。

* 引數：nown
* 傳回值：包含下列欄的表格資料：

   * 工作
   * 佇列名稱
   * 作用中的工作
   * 平均處理時間
   * 平均等待時間
   * 取消的工作
   * 失敗的工作
   * 完成的工作
   * 已處理作業
   * 已排隊的作業

**returnWorkflowJobTopicInfo** 列出按主題組織的工作流作業的處理資訊。

* 引數：nown
* 傳回值：包含下列欄的表格資料：

   * 主題名稱
   * 平均處理時間
   * 平均等待時間
   * 取消的工作
   * 失敗的工作
   * 完成的工作
   * 已處理作業

**returnFailedWorkflowCount** 顯示失敗的工作流實例數。 您可以指定工作流模型來查詢或檢索所有工作流模型的資訊。

* 引數:

   * 模型：要查詢的模型ID。 要查看所有工作流模型的失敗工作流實例計數，請不指定任何值。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：失敗的工作流程例項數。

**returnFailedWorkflowCountPerModel** 顯示每個工作流模型失敗的工作流實例數。

* 引數：沒有。
* 傳回值：包含「計數」和「模型ID」欄的表格式資料。

**terminateFailedInstances** 終止失敗的工作流實例。 您可以終止所有失敗實例，或僅終止特定模型的失敗實例。 （可選）您可以在終止實例後重新啟動實例。 您也可以測試操作，以查看結果，而不實際執行操作。

* 引數:

   * 重新啟動實例：（可選）指定值，以在 `true` 終止實例後重新啟動實例。 預設值會導致終止 `false` 的工作流實例不重新啟動。
   * 乾跑：（可選）指定值，以 `true` 查看操作的結果，而不實際執行操作。 預設值 `false` 將執行操作。
   * 型號：（可選）應用操作的模型的ID。 指定不要將操作應用於所有工作流模型的失敗實例的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：關於終止的實例的表資料，包含以下列：

   * 發起人
   * InstanceId
   * ModelId
   * 裝載
   * StartComment
   * WorkflowTitle

**retryFailedWorkItems** 嘗試執行失敗的工作項目步驟。 您可以重試所有失敗的工作項目，或僅針對特定工作流模型重試失敗的工作項目。 您可以選擇測試工序以查看結果，而不實際執行工序。

* 引數:

   * 乾跑：（可選）指定值，以 `true` 查看操作的結果，而不實際執行操作。 預設值 `false` 將執行操作。
   * 型號：（可選）應用操作的模型的ID。 指定不要將操作應用於所有工作流模型的失敗工作項目的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：重試失敗工作項目的表格資料，包括下列：

   * 發起人
   * InstanceId
   * ModelId
   * 裝載
   * StartComment
   * WorkflowTitle

**PurgeActive** Removes a active workflow instances of a specific age. 您可以清除所有模型的活動實例，或僅清除特定模型的實例。 您可以選擇性地測試工序以查看結果，而無需實際執行工序。

* 引數:

   * 型號：（可選）應用操作的模型的ID。 指定不要將操作應用於所有工作流模型的工作流實例的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 工作流程開始後的天數：要清除的工作流實例的年齡（以天為單位）。
   * 乾跑：（可選）指定值，以 `true` 查看操作的結果，而不實際執行操作。 預設值 `false` 將執行操作。

* 傳回值：有關已清除的活動工作流實例的表格式資料，包括以下列：

   * 發起人
   * InstanceId
   * ModelId
   * 裝載
   * StartComment
   * WorkflowTitle

**countStaleWorkflows** 傳回過時的工作流程例項數。 您可以檢索所有工作流模型或特定模型的過時實例數。

* 引數:

   * 型號：（可選）應用操作的模型的ID。 指定不要將操作應用於所有工作流模型的工作流實例的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：過時的工作流程例項數。

**restartStaleWorkflows** 重新啟動過時的工作流程例項。 您可以重新啟動所有過時實例，或僅重新啟動特定模型的過時實例。 您也可以測試操作，以查看結果，而不實際執行操作。

* 引數:

   * 型號：（可選）應用操作的模型的ID。 指定不要將操作應用於所有工作流模型的過時實例的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 乾跑：（可選）指定值，以 `true` 查看操作的結果，而不實際執行操作。 預設值 `false` 將執行操作。

* 傳回值：已重新啟動的工作流實例清單。

**fetchModelList** 列出所有工作流模型。

* 引數：nown
* 傳回值：用於標識包括ModelId和ModelName列的工作流模型的表格資料。

**countRunningWorkflows** 返回正在運行的工作流實例數。 您可以檢索所有工作流模型或特定模型的運行實例數。

* 引數:

   * 型號：（可選）傳回執行中例項數的模型ID。 指定不要模型，以傳回所有工作流程模型的執行中例項數。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：正在運行的工作流實例數。

**countCompletedWorkflows** 返回已完成的工作流實例數。 您可以檢索所有工作流模型或特定模型的已完成實例數。

* 引數:

   * 型號：（可選）傳回完成例項數的模型ID。 指定不要模型，以傳回所有工作流程模型的已完成例項數。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：已完成的工作流實例數。

**purgeCompleted** 從儲存庫中刪除特定年齡的已完成工作流的記錄。 定期使用此操作，在您大量使用工作流時最大限度地減少儲存庫的大小。 您可以清除所有模型的已完成實例，或僅清除特定模型的實例。 您可以選擇性地測試工序以查看結果，而無需實際執行工序。

* 引數:

   * 型號：（可選）應用操作的模型的ID。 指定不要將操作應用於所有工作流模型的工作流實例的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 工作流程完成後的天數：工作流實例已處於完成狀態的天數。
   * 乾跑：（可選）指定值，以 `true` 查看操作的結果，而不實際執行操作。 預設值 `false` 將執行操作。

* 傳回值：有關已清除的已完成工作流實例的表格式資料，包括以下列：

   * 發起人
   * InstanceId
   * ModelId
   * 裝載
   * StartComment
   * WorkflowTitle

## 存放庫 {#repository}

有關CRX儲存庫的資訊

* 網域：com.adobe.granite
* 類型：儲存庫

### 屬性 {#attributes}

**名稱** JCR儲存庫實施的名稱。 唯讀.

**版本** -儲存庫實施版本。 唯讀.

**HomeDir** 儲存庫所在的目錄。 預設位置為&lt;QuickStart_Jar_Location>/crx-quickstart/repository。 唯讀.

**CustomerName** （客戶名稱）軟體許可證發放給的客戶的名稱。 唯讀.

**LicenseKey** 此儲存庫安裝的唯一許可證密鑰。 唯讀.

**AvailableDiskSpace** 此儲存庫實例可用的磁碟空間（以兆位元組為單位）。 唯讀.

**MaximumNumberOfOpenFiles** 一次可開啟的檔案數。 唯讀.

**SessionTracker** crx.debug.sessions系統變數的值。 true表示調試會話。 false表示正常作業。 讀／寫。

**描述符** ：表示儲存庫屬性的一組鍵值對。 所有屬性都是唯讀的。

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
   <td>指示不可引用節點標識符的穩定性。 可以使用下列值：
    <ul>
     <li>identifier.stability.indugent.duration:識別碼不會變更。</li>
     <li>identifier.stability.method.duration:識別碼可在方法呼叫之間變更。</li>
     <li>identifier.stability.save.duration:標識符在保存／刷新週期中不會更改。</li>
     <li>identifier.stability.session.duration:識別碼在作業期間不會變更。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>指示是否支援JCR 1.0 XPath查詢語言。 true表示支援，false表示不支援。</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>在system.id檔案中找到的系統識別碼。</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>指示是否支援JCR 1.0 XPath查詢語言。 true表示支援，false表示不支援。</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>儲存庫實施的版本。</td>
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
   <td>指示可以覆蓋節點類型的繼承屬性還是子節點定義。 true表示支援覆寫，false表示無覆寫。</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true表示支援對儲存庫更改進行非同步觀察。 非同步觀察的支援可讓應用程式在每次變更發生時，接收並回覆通知。</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true表示jcr:score偽屬性可用於包含jcrfn:contains（在XPath中）或CONTAINS（在SQL中）函式的XPath和SQL查詢，以執行全文搜索。</p> </td>
  </tr>
  <tr>
   <td>option.simple.version.supported</td>
   <td>true表示儲存庫支援簡單的版本控制。 使用簡單的版本控制，儲存庫會維護節點的一系列連續版本。</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true表示儲存庫支援使用API建立和刪除工作區。</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true表示儲存庫支援添加和刪除現有節點的混合節點類型。</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true表示儲存庫使節點定義能夠將主項作為子項包含。 使用API可存取主要項目，而不需知道項目名稱。</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true表示LEVEL_1_SUPPORTED和OPTION_XML_IMPORT_SUPPORTED都為true。</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true表示儲存庫使用API提供寫訪問。 false表示唯讀存取。</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true表示您可以更改現有節點正在使用的節點定義。</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>儲存庫實施的JCR規範版本。</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true表示應用程式可以執行儲存庫的日誌觀察。 通過記錄的觀察，可以獲得一組特定時間段的更改通知。 </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>儲存庫支援的查詢語言。 無值表示沒有查詢支援。</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>true表示儲存庫支援將節點導出為XML代碼。</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>true表示儲存庫支援註冊具有多個二進位屬性的節點類型。 false表示節點類型支援單一二進位屬性。</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>true表示儲存庫支援訪問控制，用於設定和確定節點訪問的用戶權限。</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true表示儲存庫同時支援配置和基線。</td>
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
   <td>query.stored.querys.supported</td>
   <td>true表示儲存庫支援儲存查詢。</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true表示儲存庫支援全文搜索。</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>指示對節點類型繼承的儲存庫支援級別。 可以使用下列值：</p> <p>node.type.management.inheritance.minimal:主節點類型的註冊僅限於僅具有nt:base作為超類型的節點類型。 混合節點類型的配準被限制為沒有超類型的。</p> <p>node.type.management.inheritance.single:主節點類型的註冊限於具有一個超級類型的節點類型。 混合節點類型的配準被限制為具有最多一個超類型的節點類型。</p> <p><br /> node.type.management.inheritance.multiple:主節點類型可以註冊為一個或多個超類型。 Mixin節點類型可以用零個或多個超類型進行註冊。</p> </td>
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
   <td>javax.jcr.PropertyType常數的陣列，這些常數表示註冊節點類型可以指定的屬性類型。 零長陣列表示註冊的節點類型不能指定屬性定義。 屬性類型包括STRING、URI、BOOLEAN、LONG、DOUBLE、DECIMAL、BINARY、DATE、NAME、PATH、WEAKREFERENCE、REFERENCE和UNDEFINED（如果支援）</td>
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
   <td><p>查詢中連接的支援級別。 可以使用下列值：</p>
    <ul>
     <li>query.joins.none:不支援連接。 查詢可以使用一個選擇器。</li>
     <li>query.joins.inner:支援內連接。</li>
     <li>query.joins.inner.outer:支援內連接和外連接。</li>
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
   <td>true表示儲存庫支援將XML代碼導入為內容。</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true表示儲存庫支援具有相同名稱的同級節點（具有相同父代的節點）。</td>
  </tr>
  <tr>
   <td>node.type.management.residument.definitions.supported</td>
   <td>true表示儲存庫支援具有剩餘定義的名稱屬性。 支援時，項目定義的名稱屬性可以是星號("*")。</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true表示儲存庫支援在建立節點時自動建立節點的子項（節點或屬性）。</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true表示此儲存庫節點是群集的主節點。</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>true表示option.xml.export.support為true,query.languages為非零長度。</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true表示儲存庫支援未歸檔的內容。 未歸檔節點不屬於儲存庫層次結構。</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>儲存庫實施的JCR規範的名稱。</td>
  </tr>
  <tr>
   <td>option.version.supported</td>
   <td>true表示儲存庫支援完整的版本控制。</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>儲存庫的名稱。</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true表示儲存庫支援節點鎖定。 鎖定使用戶能夠暫時防止其他用戶進行更改。</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true表示儲存庫支援活動。 活動是一組在合併到另一個工作區的工作區中執行的更改。</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties受支援</td>
   <td>true表示儲存庫支援的節點屬性可以具有零或多個值。</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true表示儲存庫支援使用外部保留管理應用程式將保留策略應用於內容，並支援暫掛和釋放。</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true表示儲存庫支援生命週期管理。</td>
  </tr>
 </tbody>
</table>

**WorkspaceNames** 儲存庫中工作區的名稱。 唯讀.

**DataStoreGarbageCollectionDelay** GarbageCollectionDelay在掃描每十個節點後，廢棄項目收集所睡眠的時間量（以毫秒為單位）。 讀／寫。

**BackupDelay** 備份過程在備份的每個步驟之間休眠的時間（以毫秒為單位）。 讀／寫。

**BackupInProgress** 值為true表示正在執行備份進程。 唯讀.

**BackupProgress** 對於當前備份，所有已備份檔案的百分比。 唯讀.

**CurrentBackupTarget** 對於當前備份，是儲存備份檔案的ZIP檔案。 當備份未進行時，不會顯示任何值。 唯讀.

**BackupWasSuccessful** 值為true表示當前備份期間未發生錯誤，或未進行備份。 false表示當前備份期間發生錯誤。 唯讀.

**BackupResult** 當前備份的狀態。 可以使用下列值：

* 正在進行備份：當前正在執行備份。
* 備份已取消：備份已取消。
* 備份完成，但出現錯誤：備份期間發生錯誤。 錯誤資訊提供了有關原因的資訊。
* 備份已完成：備份成功。
* 目前未執行備份：沒有正在進行的備份。

唯讀.

**TarOptimizationRunningSince** 目前TAR檔案最佳化程式開始的時間。 唯讀.

**TarOptimizationDelay** TAR優化流程在流程的每個步驟之間休眠的時間（以毫秒為單位）。 讀／寫。

**ClusterProperties** 一組表示群集屬性和值的鍵值對。 表中的每一行都表示群集屬性。 唯讀.

**ClusterNodes** 儲存庫群集的成員。

**ClusterId** 此儲存庫群集的標識符。 唯讀.

**ClusterMasterId** 此儲存庫群集的主節點的標識符。 唯讀.

**ClusterNodeId** 儲存庫群集的此節點的標識符。 唯讀.

### 作業 {#operations-1}

**createWorkspace** 在此儲存庫中建立工作區。

* 引數:

   * 名稱：表示新工作區名稱的字串值。

* 傳回值：nown

**runDataStoreGarbageCollection** 在儲存庫節點上執行廢棄項目收集。

* 引數:

   * 刪除：指示是否刪除未使用的儲存庫項的布爾值。 值true會刪除未使用的節點和屬性。 值false會掃描所有節點，但不會刪除任何節點。

* 傳回值：nown

**stopDataStoreGarbageCollection** 停止執行中的資料儲存廢棄項目收集。

* 引數：nown
* 傳回值：目前狀態的字串表示法

**startBackup** 備份ZIP檔案中的儲存庫資料。

* 引數:

   * `target`:（可選）一 `String` 個值，它表示要在其中存檔儲存庫資料的ZIP檔案或目錄的名稱。 若要使用ZIP檔案，請加入ZIP檔案副檔名。 要使用目錄，請不包括檔案副檔名。

      要執行增量備份，請指定以前用於備份的目錄。

      您可以指定絕對路徑或相對路徑。 相對路徑相對於crx-quickstart目錄的父目錄。

      當您未指定值時，會使用預 `backup-currentdate.zip` 設值，其 `currentdate` 中為格式 `yyyyMMdd-HHmm`。

* 傳回值：nown

**cancelBackup** 停止當前備份進程，並刪除為存檔資料而建立的臨時存檔。

* 引數：nown
* 傳回值：nown

**blockRepositoryWrites** 對儲存庫資料的更改進行阻止。 所有儲存庫備份偵聽程式都會收到該塊的通知。

* 引數：nown
* 傳回值：nown

**unlockRepositoryWrites** 從儲存庫中刪除該塊。 所有儲存庫備份偵聽程式都會收到刪除塊的通知。

* 引數：nown
* 傳回值：nown

**startTarOptimization** 使用tarOptimizationDelay的預設值啟動TAR檔案優化過程。

* 引數：nown
* 傳回值：nown

**stopTarOptimization** Stops TAR file optimization.

* 引數：nown
* 傳回值：nown

**tarIndexMerge** 合併所有TAR集的頂部索引檔案。 頂級索引檔案是具有不同主要版本的檔案。 例如，以下檔案將合併到檔案index_3_1.tar中：index_1_1.tar、index_2_0.tar、index_3_0.tar。 已合併的檔案將被刪除（在上例中，將刪除index_1_1.tar、index_2_0.tar和index_3_0.tar）。

* 引數:

   * `background`:一個布爾值，指示是否在後台運行操作，以便在執行期間使用Web控制台。 值true在後台運行操作。

* 傳回值：nown

**bemocClusterMaster** 將此儲存庫節點設定為群集的主節點。 如果尚未主實例，此命令將停止當前主實例的偵聽器，並在當前節點上啟動主監聽器。 然後，此節點將設定為主節點並重新啟動，導致所有從節點連接到此實例。

* 引數：nown
* 傳回值：nown

**joinCluster** 將此儲存庫作為從節點添加到群集中。 您必須提供使用者名稱和密碼才能進行驗證。 連接使用基本驗證。 安全憑證在傳送至伺服器之前，先經過Base-64編碼。

* 引數:

   * `master`:一個字串值，它代表運行主資料庫節點的電腦的IP地址或電腦名。
   * `username`:用於向群集驗證的名稱。
   * `password`:用於驗證的密碼。

* 傳回值：nown

**traversalCheck** Traverses（遍歷）和（可選）修正從特定節點開始的子樹中的不一致。 這在持久性管理器文檔中有詳細說明。

**consistencyCheck** Checks（檢查）並選擇性地修正資料儲存中的一致性。 Datastore上的文檔將對此進行詳細介紹。

## 儲存庫統計資訊(TimeSeries) {#repository-statistics-timeseries}

定義的每個統計類型的「時間系列」欄位 `org.apache.jackrabbit.api.stats.RepositoryStatistics` 值。

* 網域: `com.adobe.granite`
* 類型: `TimeSeries`
* 名稱：來自 `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` Enum類的下列值之一：

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

為報告的每個統計類型提供以下屬性：

* ValuePerSecond:最後一分鐘的測量值每秒。 唯讀.
* ValuePerMinute:前一小時的每分鐘測量值。 唯讀.
* ValuePerHour:上週的每小時測量值。 唯讀.
* ValuePerWeek:過去三年的每週測量值。 唯讀.

## 資料庫查詢統計資料 {#repository-query-stats}

關於儲存庫查詢的統計資訊。

* 網域：com.adobe.granite
* 類型：QueryStat

### 屬性 {#attributes-2}

**SlowQueries** —有關已花費最長時間完成的儲存庫查詢的資訊。 唯讀.

**SlowQuerysQueueSize** SlowQuerys清單中要包含的查詢數上限。 讀寫。

**PopularQueries** Information about the repository queries that have have been. 唯讀.

**PopularQuerysQueueSize** PopularQuerys清單中的查詢數上限。 讀寫。

### 作業 {#operations-2}

**clearSlowQuerysQueue** 從SlowQuerys清單中移除所有查詢。

* 引數：nown
* 傳回值：nown

**clearPopularQuerysQueue** 從PopularQuerys清單中移除所有查詢。

* 引數：nown
* 傳回值：nown

## 複寫代理程式 {#replication-agents}

監視每個複製代理的服務。 建立複製代理時，該服務會自動出現在JMX控制台中。

* **** 網域：com.adobe.granite.replication
* **** 類型：代理
* **** 名稱：無值
* **** 屬性：{id=&quot;*Name*&quot;}，其中 *Name* 是代理Name屬性的值。

### 屬性 {#attributes-3}

**Id** ：表示複製代理配置標識符的字串值。 多個代理可以使用相同的配置。 唯讀.

**有效** ：一個布爾值，指示代理是否正確配置：

* `true`:有效的配置。
* `false` :配置包含錯誤。

唯讀.

**Enabled** （啟用）一個布爾值，它指示是否啟用代理：

* `true`: 已啟用.
* `false`: 停用.

**QueueBlocked** ：一個布爾值，它指示隊列是否存在且被阻止：

* `true`: 已封鎖. 自動重試擱置中。
* `false`:未阻止或不存在。

唯讀.

**QueuePaused** ：一個布林值，指示作業隊列是否暫停：

* `true`:暫停（暫停）
* `false`:未暫停或不存在。

讀寫。

**QueueNumEntries** —表示代理隊列中作業數的整數值。 唯讀.

**QueueStatusTime** A Date值，指示獲取顯示的狀態值時伺服器上的時間。 值與載入頁面的時間相對應。 唯讀.

**QueueNextRetryTime** 對於被阻止的隊列，一個日期值，指示下次自動重試的時間。 未顯示任何時間時，不會阻止隊列。 唯讀.

**QueueProcessingSince** A Date值，指示當前作業何時開始處理。 當沒有出現時間時，佇列會被封鎖或閒置。 唯讀.

**QueueLastProcessTime** ：一個日期值，用於指示上一個作業何時完成。 唯讀.

### 作業 {#operations-3}

**queueForceRetry** 對於被阻止的隊列，向隊列發出retry命令。

* 引數：nown
* 傳回值：nown

**queueClear** 從隊列中刪除所有作業。

* 引數：nown
* 傳回值：nown

## Sling Engine {#sling-engine}

提供有關HTTP請求的統計資料，以便您監控SlingRequestProcessor服務的效能。

* 網域：org.apache.sling
* 類型：引擎
* 屬性：{service=RequestProcessor}

### 屬性 {#attributes-4}

**RequestsCount** 自上次重設統計資料以來發生的請求數。

**MinRequestDurationMsec** 自上次重設統計資料以來，處理請求所需的最短時間（以毫秒為單位）。

**MaxRequestDuratioMsec** 自上次重設統計資料以來，處理請求所需的最長時間（以毫秒為單位）。

**StandardDevationDurationMsec** 處理請求所需時間量的標準差。 自上次重設統計資料起，標準差會使用所有請求來計算。

**MeanRequestDurationMsec** 處理請求所需的平均時間量。 平均值是使用統計資料上次重設後的所有請求計算

### 作業 {#operations-4}

**resetStatistics** 將所有統計資訊設定為零。 在您需要分析特定時段內的請求處理效能時，重設統計資料。

* 引數：nown
* 傳回值：nown

**id** 包ID的字串表示法。

**installed** A boolean value that indicated the package is installed:

* `true`: 已安裝.
* `false`: 未安裝.

**installedBy** 上次安裝軟體包的用戶的ID。

**installedDate** 上次安裝軟體包的日期。

**size** —一個長值，它以位元組為單位保存包的大小。


## 快速啟動程式 {#quickstart-launcher}

有關啟動過程和快速啟動啟動程式的資訊。

* 網域：com.adobe.granite.quickstart
* 類型：啟動程式

### 作業 {#operations-5}

**日誌**

在「快速啟動」窗口中顯示一條消息。

引數:

* p1:代 `String` 表要顯示的消息的值。 下圖顯示調用p1 `log` 值的結果 `this is a log message`。

![launcheruilog](assets/launcheruilog.png)

* 傳回值：nown

**startupFinished**

調用伺服器啟動器的startupFinished方法。 方法會嘗試在網頁瀏覽器中開啟「歡迎」頁面。

* 引數：nown
* 傳回值：nown

**startupProgress**

設定伺服器啟動進程的完成值。 「快速啟動」(QuickStart)窗口上的進度條表示完成值。

* 引數:

   * p1:浮點值，以分數表示啟動程式完成的程度。 值應介於零和一之間。 例如，0.3表示完成30%。

* 傳回值：沒有。

![launcherprogress](assets/launcherprogress.png)

## 協力廠商服務 {#third-party-services}

數個協力廠商伺服器資源會安裝MBeans，將屬性和作業公開至JMX主控台。 下表列出協力廠商資源，並提供更多資訊的連結。

<table>
 <tbody>
  <tr>
   <th>網域</th>
   <th>類型</th>
   <th>MBean類</th>
  </tr>
  <tr>
   <td>JMI實施</td>
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
     <li>類別載入</li>
     <li>編譯</li>
     <li>GarbageCollector</li>
     <li>記憶體</li>
     <li>MemoryManager</li>
     <li>記憶體池</li>
     <li>作業系統</li>
     <li>執行時期</li>
     <li>線程</li>
    </ul> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.management</a> package</td>
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
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a> package</td>
  </tr>
 </tbody>
</table>

## 使用JMX主控台 {#using-the-jmx-console}

JMX控制台顯示有關伺服器上運行的若干服務的資訊：

* 屬性：服務屬性，例如組態或執行時期資料。 屬性可以是只讀或讀寫。
* 操作：可在服務上調用的命令。

與OSGi服務一起部署的MBeans會將服務屬性和操作暴露到控制台。 MBean決定公開的屬性和操作，以及屬性是只讀還是讀寫。

JMX主控台的首頁包含服務表。 表中的每一行都代表由MBean公開的服務。

1. 開啟「Web主控台」，然後按一下「JMX」標籤。 ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. 按一下服務的單元格值可查看服務的屬性和操作。
3. 若要變更屬性值，請按一下值，在出現的對話方塊中指定值，然後按一下「儲存」。
4. 要調用服務操作，請按一下操作名稱，在出現的對話框中指定參數值，然後按一下調用。

## 使用外部JMX應用程式進行監控 {#using-external-jmx-applications-for-monitoring}

CRX允許外部應用程式通過 [Java管理擴展(JMX)與受管Bean(MBean)交互](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html)。 使用通用控制台(如 [JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) )或特定於域的監控應用程式，可以獲取和設定CRX配置和屬性，以及監視效能和資源使用情況。

### 使用JConsole連接到CRX {#using-jconsole-to-connect-to-crx}

要使用JConsole連接到CRX，請執行以下步驟：

1. 開啟終端窗口。
1. 輸入以下命令：

   `jconsole`

JConsole將啟動，並出現JConsole窗口。

### 連接到本地CRX進程 {#connecting-to-a-local-crx-process}

JConsole將顯示本地Java虛擬機進程的清單。 該清單將包含兩個快速啟動進程。 從本地進程清單（通常是PID較高的進程）中選擇快速啟動的「CHILD」進程。

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### 連接到遠程CRX進程 {#connecting-to-a-remote-crx-process}

為了連接到遠程CRX進程，需要啟用承載遠程CRX進程的JVM以接受遠程JMX連接。

要啟用遠程JMX連接，啟動JVM時必須設定以下系統屬性：

`com.sun.management.jmxremote.port=portNum`

在上述屬性中， `portNum` 是要啟用JMX RMI連接的埠號。 請務必指定未使用的埠號。 除了發佈RMI連接器以進行本地訪問外，設定此屬性還使用眾所周知的名稱&quot;jmxrmi&quot;在指定埠的專用只讀註冊表中發佈附加的RMI連接器。

預設情況下，啟用JMX代理進行遠程監視時，它會根據在啟動Java VM時需要使用以下系統屬性指定的口令檔案使用口令驗證：

`com.sun.management.jmxremote.password.file=pwFilePath`

請參閱相 [關的JMX檔案](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html) ，以取得設定密碼檔案的詳細指示。

範例:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### 使用CRX提供的MBean {#using-the-mbeans-provided-by-crx}

在連接到快速啟動進程後，JConsole為CRX正在運行的JVM提供了一系列常規監控工具。

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

要訪問CRX的內部監視和配置選項，請轉至「MBeans」(MBeans)頁籤，然後從左側的分層內容樹中選擇您感興趣的「屬性」(Attributes)或「操作」(Operations)部分。 例如，com.adobe.granite/Repository/Operations區段。

在該區段中，在左窗格中選擇所需的屬性或操作。

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)

