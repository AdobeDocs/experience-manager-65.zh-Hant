---
title: 使用JMX控制台監視伺服器資源
seo-title: Monitoring Server Resources Using the JMX Console
description: 瞭解如何使用JMX控制台監視伺服器資源。
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

JMX控制台使您能夠監視和管理CRX伺服器上的服務。 下面的部分概述了通過JMX框架公開的屬性和操作。

有關如何使用控制台控制項的資訊，請參見 [使用JMX控制台](#using-the-jmx-console)。 有關JMX的背景資訊，請參見 [Java管理擴展(JMX)技術](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) 頁。

有關建立MBean以使用JMX控制台管理服務的資訊，請參見 [將服務與JMX控制台整合](/help/sites-developing/jmx-integration.md)。

## 工作流維護 {#workflow-maintenance}

用於管理運行、已完成、過時和失敗的工作流實例的操作。

* 域：com.adobe.granite.workflow
* 類型：維護

>[!NOTE]
>
>查看 [工作流控制](/help/sites-administering/workflows-administering.md) 用於其他工作流管理工具以及可能的工作流實例狀態的說明。

### 運作 {#operations}

**listRunningWorkflowsPerModel** 列出每個工作流模型正在運行的工作流實例數。

* 參數：無
* 返回值：包含Count和ModelId列的表格資料。

**listCompletedWorkflowsPerModel** 列出每個工作流模型的已完成工作流實例數。

* 參數：無
* 返回值：包含Count和ModelId列的表格資料。

**returnWorkflowQueueInfo** 列出有關已處理和排隊等待處理的工作流項的資訊。

* 參數：無
* 返回值：包含以下列的表格資料：

   * 工作
   * 隊列名稱
   * 作用中的工作
   * 平均處理時間
   * 平均等待時間
   * 取消的工作
   * 失敗的工作
   * 已完成的作業
   * 已處理的作業
   * 已排隊的作業

**returnWorkflowJobTopicInfo** 列出按主題組織的工作流作業的處理資訊。

* 參數：無
* 返回值：包含以下列的表格資料：

   * 主題名稱
   * 平均處理時間
   * 平均等待時間
   * 取消的工作
   * 失敗的工作
   * 已完成的作業
   * 已處理的作業

**returnFailedWorkflowCount** 顯示失敗的工作流實例數。 您可以指定工作流模型以查詢或檢索所有工作流模型的資訊。

* 引數:

   * 模型：要查詢的模型的ID。 要查看所有工作流模型的失敗工作流實例計數，請不指定值。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：失敗的工作流實例數。

**returnFailedWorkflowCountPerModel** 顯示每個工作流模型失敗的工作流實例數。

* 參數：沒有。
* 返回值：包含計數和模型ID列的表格資料。

**terminateFailedInstances** 終止失敗的工作流實例。 您可以終止所有失敗實例或僅終止特定模型的失敗實例。 （可選）您可以在實例終止後重新啟動它們。 您還可以test操作，以查看結果，而不實際執行該操作。

* 引數:

   * 重新啟動實例：（可選）指定值 `true` 以在實例終止後重新啟動它們。 預設值 `false` 導致終止的工作流實例無法重新啟動。
   * 乾運行：（可選）指定值 `true` 查看操作結果而不實際執行該操作。 預設值 `false` 導致操作被執行。
   * 型號：（可選）應用操作的模型的ID。 指定不將操作應用於所有工作流模型失敗實例的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：有關終止實例的表格資料，包含以下列：

   * 發起人
   * 實例ID
   * 模型ID
   * 裝載
   * 開始注釋
   * 工作流標題

**retryFailedWorkItems** 嘗試執行失敗的工作項步驟。 您可以重試所有失敗的工作項，或只重試特定工作流模型的失敗工作項。 您可以根據需要test工序，以查看結果，而不實際執行工序。

* 引數:

   * 乾運行：（可選）指定值 `true` 查看操作結果而不實際執行該操作。 預設值 `false` 導致操作被執行。
   * 型號：（可選）應用操作的模型的ID。 指定不將操作應用於所有工作流模型的失敗工作項的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：有關重試的失敗工作項的表格資料，包括以下列：

   * 發起人
   * 實例ID
   * 模型ID
   * 裝載
   * 開始注釋
   * 工作流標題

**清除活動** 刪除特定年齡的活動工作流實例。 可清除所有模型的活動實例，或僅清除特定模型的實例。 您可以根據需要test工序，以查看結果，而不實際執行工序。

* 引數:

   * 型號：（可選）應用操作的模型的ID。 指定不將操作應用於所有工作流模型的工作流實例的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 自工作流啟動以來的天數：要清除的工作流實例的時間（天）。
   * 乾運行：（可選）指定值 `true` 查看操作結果而不實際執行該操作。 預設值 `false` 導致操作被執行。

* 返回值：有關已清除的活動工作流實例的表格資料，包括以下列：

   * 發起人
   * 實例ID
   * 模型ID
   * 裝載
   * 開始注釋
   * 工作流標題

**countStaleWorkflows** 返回過時的工作流實例數。 可檢索所有工作流模型或特定模型的過時實例數。

* 引數:

   * 型號：（可選）應用操作的模型的ID。 指定不將操作應用於所有工作流模型的工作流實例的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：過時的工作流實例數。

**重新啟動StaleWorkflows** 重新啟動過時的工作流實例。 可以重新啟動特定模型的所有陳舊實例或僅舊實例。 您還可以test操作，以查看結果，而不實際執行該操作。

* 引數:

   * 型號：（可選）應用操作的模型的ID。 指定不將操作應用於所有工作流模型的陳舊實例的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 乾運行：（可選）指定值 `true` 查看操作結果而不實際執行該操作。 預設值 `false` 導致操作被執行。

* 返回值：重新啟動的工作流實例清單。

**fetchModelList** 列出所有工作流模型。

* 參數：無
* 返回值：標識工作流模型（包括ModelId和ModelName列）的表格資料。

**計數運行工作流** 返回正在運行的工作流實例數。 可檢索所有工作流模型或特定模型的運行實例數。

* 引數:

   * 型號：（可選）返回其運行實例數的模型的ID。 指定任何模型以返回所有工作流模型的運行實例數。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：正在運行的工作流實例數。

**countCompletedWorkflows** 返回已完成的工作流實例數。 可檢索所有工作流模型或特定模型的已完成實例數。

* 引數:

   * 型號：（可選）返回已完成實例數的模型的ID。 指定任何模型以返回所有工作流模型的已完成實例數。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：已完成的工作流實例數。

**清除已完成** 從儲存庫中刪除特定年齡的已完成工作流的記錄。 定期使用此操作可在大量使用工作流時將儲存庫的大小降至最低。 可清除所有模型的已完成實例，或僅清除特定模型的實例。 您可以根據需要test工序，以查看結果，而不實際執行工序。

* 引數:

   * 型號：（可選）應用操作的模型的ID。 指定不將操作應用於所有工作流模型的工作流實例的模型。 ID是指向模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 工作流完成後的天數：工作流實例已處於完成狀態的天數。
   * 乾運行：（可選）指定值 `true` 查看操作結果而不實際執行該操作。 預設值 `false` 導致操作被執行。

* 返回值：有關已清除的已完成工作流實例的表格資料，包括以下列：

   * 發起人
   * 實例ID
   * 模型ID
   * 裝載
   * 開始注釋
   * 工作流標題

## 存放庫 {#repository}

有關CRX儲存庫的資訊

* 域：com.adobe.granite
* 類型：儲存庫

### 屬性 {#attributes}

**名稱** JCR儲存庫實現的名稱。 唯讀.

**版本** 儲存庫實施版本。 唯讀.

**主目錄** 儲存庫所在的目錄。 預設位置為 &lt;quickstart_jar_location>/crx-quickstart/repository。 唯讀.

**客戶名稱** 向其頒發軟體許可證的客戶的名稱。 唯讀.

**許可證密鑰** 此儲存庫安裝的唯一許可證密鑰。 唯讀.

**可用磁碟空間** 此儲存庫實例可用的磁碟空間（以MB為單位）。 唯讀.

**MaximumNumberOfOpenFiles** 一次可開啟的檔案數。 唯讀.

**會話跟蹤器** crx.debug.sessions系統變數的值。 true表示調試會話。 false表示正常會話。 讀/寫。

**描述符** 一組表示儲存庫屬性的鍵值對。 所有屬性均為只讀。

<table>
 <tbody>
  <tr>
   <th>金鑰</th>
   <th>值</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>指示節點和節點的屬性是否可以具有相同的名稱。 true表示支援相同的名稱，false表示不支援。 </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>指示非可引用節點標識符的穩定性。 可以使用以下值：
    <ul>
     <li>identifier.stability.indignet.duration:標識符不會更改。</li>
     <li>identifier.stability.method.duration:標識符可以在方法調用之間更改。</li>
     <li>identifier.stability.save.duration:標識符在保存/刷新週期內不會更改。</li>
     <li>identifier.stability.session.duration:在會話期間，標識符不會更改。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>指示是否支援JCR 1.0 XPath查詢語言。 true表示支援，false表示不支援。</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>在system.id檔案中找到的系統標識符。</td>
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
   <td>指示是否可以覆蓋節點類型的繼承屬性或子節點定義。 true表示支援替代，false表示不支援替代。</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true表示支援對儲存庫更改進行非同步觀察。 支援非同步觀察使應用程式能夠在每次更改發生時接收並響應有關其的通知。</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true表示jcr:score偽屬性在包含jcrfn:contains（在XPath中）或CONTAINS（在SQL中）函式的XPath和SQL查詢中可用，以執行全文搜索。</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true表示儲存庫支援簡單版本控制。 通過簡單的版本控制，儲存庫維護節點的一系列連續版本。</td>
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
   <td>true表示儲存庫允許節點定義將主項作為子項包含。 使用API可訪問主項，而不知道項名。</td>
  </tr>
  <tr>
   <td>level.2.受支援</td>
   <td>true表示LEVEL_1_SUPPORTED和OPTION_XML_IMPORT_SUPPORTED均為true。</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true表示儲存庫使用API提供寫訪問。 false表示只讀訪問。</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true表示可以更改現有節點正在使用的節點定義。</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>儲存庫實施的JCR規範的版本。</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true表示應用程式可以執行對儲存庫的日誌觀察。 利用日誌觀察，可以在特定時間段內獲得一組改變通知。 </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>儲存庫支援的查詢語言。 無值表示不支援查詢。</td>
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
   <td>query.stored.queries.supported</td>
   <td>true表示儲存庫支援儲存的查詢。</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true表示儲存庫支援全文搜索。</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>指示對節點類型繼承的儲存庫支援級別。 可以使用以下值：</p> <p>node.type.management.inheritance.minimal:主節點類型的註冊僅限於那些僅具有nt:base超類型的節點類型。 混合節點類型的配準被限制在沒有超類型的節點類型。</p> <p>node.type.management.inheritance.single:主節點類型的註冊僅限於具有一個超類型的節點類型。 混合節點類型的配準被限制到最多具有一個超類型的類型。</p> <p><br /> node.type.management.inheritance.multiple:可以使用一個或多個超級類型註冊主節點類型。 混合節點類型可以註冊為零個或多個超類型。</p> </td>
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
   <td>avax.jcr.PropertyType常數陣列，它表示註冊節點類型可以指定的屬性類型。 零長陣列表示註冊的節點類型無法指定屬性定義。 屬性類型包括STRING、URI、BOOLEAN、LONG、DOUBLE、DECIMAL、BINARY、DATE、NAME、PATH、WEAKREFERENCE、REFERENCE和UNDEFINED（如果支援）</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true表示儲存庫支援保留子節點的順序。</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>儲存庫供應商的名稱。</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>查詢中對聯接的支援級別。 可以使用以下值：</p>
    <ul>
     <li>query.joins.none:不支援加入。 查詢可以使用一個選擇器。</li>
     <li>query.joins.inner:支援內部連接。</li>
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
   <td>true表示儲存庫支援將XML代碼作為內容導入。</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true表示儲存庫支援具有相同名稱的同級節點（具有相同父節點的節點）。</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true表示儲存庫支援具有剩餘定義的名稱屬性。 支援時，項定義的名稱屬性可以是星號("*")。</td>
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
   <td>level.1.支援</td>
   <td>true表示option.xml.export.support為true且query.languages的長度不為零。</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true表示儲存庫支援未歸檔的內容。 未歸檔節點不是儲存庫層次結構的一部分。</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>儲存庫實施的JCR規範的名稱。</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true表示儲存庫支援完全版本控制。</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>儲存庫的名稱。</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true表示儲存庫支援鎖定節點。 鎖定使用戶能夠臨時阻止其他用戶進行更改。</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true表示儲存庫支援活動。 活動是在合併到另一個工作區的工作區中執行的一組更改。</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true表示儲存庫支援可具有零個或多個值的節點屬性。</td>
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

**DataStoreGarbageCollectionDelay** 每十個節點掃描後垃圾收集休眠的時間（毫秒）。 讀/寫。

**備份延遲** 備份進程在每個備份步驟之間休眠的時間（毫秒）。 讀/寫。

**BackupInProgress** 值為true表示正在執行備份進程。 唯讀.

**備份進度** 對於當前備份，已備份的所有檔案的百分比。 唯讀.

**當前備份目標** 對於當前備份，為儲存備份檔案的ZIP檔案。 當備份未進行時，不顯示值。 唯讀.

**BackupWasSuccessful** 值為true表示當前備份期間未發生任何錯誤，或者未進行任何備份。 false表示當前備份期間出錯。 唯讀.

**備份結果** 當前備份的狀態。 可以使用以下值：

* 正在進行備份：當前正在執行備份。
* 已取消備份：已取消備份。
* 備份已完成，但出現錯誤：備份期間出錯。 錯誤消息提供有關原因的資訊。
* 備份已完成：備份成功。
* 迄今未執行任何備份：沒有正在進行備份。

唯讀.

**TarOptimizationRunningSince** 當前TAR檔案優化過程開始的時間。 唯讀.

**TarOptimization延遲** TAR優化進程在進程的每個步驟之間休眠的時間（毫秒）。 讀/寫。

**群集屬性** 一組表示群集屬性和值的鍵值對。 表中的每一行都表示一個群集屬性。 唯讀.

**群集節點** 儲存庫群集的成員。

**群集ID** 此儲存庫群集的標識符。 唯讀.

**群集主ID** 此資料庫群集的主節點的標識符。 唯讀.

**群集節點ID** 儲存庫群集的此節點的標識符。 唯讀.

### 運作 {#operations-1}

**建立工作區** 在此儲存庫中建立工作區。

* 引數:

   * 名稱：表示新工作區名稱的字串值。

* 返回值：無

**runDataStoreGarbageCollection** 對儲存庫節點執行垃圾收集。

* 引數:

   * 刪除：指示是否刪除未使用的儲存庫項的布爾值。 如果值為true，則刪除未使用的節點和屬性。 如果值為false，則會掃描所有節點，但不會刪除任何節點。

* 返回值：無

**stopDataStoreGarbageCollection** 停止正在運行的資料儲存垃圾收集。

* 參數：無
* 返回值：當前狀態的字串表示

**啟動備份** 備份ZIP檔案中的儲存庫資料。

* 引數:

   * `target`:（可選）A `String` 值，它表示要在其中存檔儲存庫資料的ZIP檔案或目錄的名稱。 要使用ZIP檔案，請包括ZIP檔案副檔名。 要使用目錄，請不包括檔案副檔名。

      要執行增量備份，請指定以前用於備份的目錄。

      可以指定絕對路徑或相對路徑。 相對路徑相對於crx-quickstart目錄的父目錄。

      當未指定值時，預設值為 `backup-currentdate.zip` 的 `currentdate` 的 `yyyyMMdd-HHmm`。

* 返回值：無

**取消備份** 停止當前備份過程並刪除該過程為存檔資料而建立的臨時存檔。

* 參數：無
* 返回值：無

**blockRepositoryWrites** 阻止對儲存庫資料的更改。 系統會通知所有儲存庫備份偵聽器該塊。

* 參數：無
* 返回值：無

**取消阻止儲存庫寫入** 從儲存庫中刪除該塊。 將通知所有儲存庫備份偵聽器該塊刪除。

* 參數：無
* 返回值：無

**startTarOptimization** 使用tarOptimizationDelay的預設值啟動TAR檔案優化過程。

* 參數：無
* 返回值：無

**stopTarOptimization** 停止TAR檔案優化。

* 參數：無
* 返回值：無

**tarIndexMerge** 合併所有TAR集的頂級索引檔案。 頂級索引檔案是具有不同主要版本的檔案。 例如，以下檔案合併到檔案index_3_1.tar中：index_1_1.tar、index_2_0.tar、index_3_0.tar。 已合併的檔案將被刪除（在上例中， index1_1.tar 、 index2_0.tar和index3_0.tar將被刪除）。

* 引數:

   * `background`:一個布爾值，指示是否在後台運行該操作，以便Web控制台在執行期間可用。 值為true將在後台運行該操作。

* 返回值：無

**成為群集主** 將此儲存庫節點設定為群集的主節點。 如果尚未主節點，則此命令將停止當前主實例的偵聽器並在當前節點上啟動主監聽器。 然後，此節點被設定為主節點並重新啟動，從而導致群集中的所有其他節點（即由主節點控制的節點）連接到此實例。

* 參數：無
* 返回值：無

**joinCluster** 將此儲存庫作為由群集主節點控制的節點添加到群集。 必須提供用戶名和密碼以用於驗證目的。 連接使用基本身份驗證。 安全憑證在被發送到伺服器之前被編碼為base-64。

* 引數:

   * `master`:表示運行主資料庫節點的電腦的IP地址或電腦名稱的字串值。
   * `username`:用於向群集進行身份驗證的名稱。
   * `password`:用於驗證的密碼。

* 返回值：無

**遍歷檢查** 遍歷並（可選）修復從特定節點開始的子樹中的不一致。 這在持久性管理器文檔中作了詳細介紹。

**一致性檢查** 檢查並（可選）修復資料儲存中的一致性。 資料儲存上的文檔中詳細介紹了這一點。

## 儲存庫統計資訊(TimeSeries) {#repository-statistics-timeseries}

每個統計類型的TimeSeries欄位的值 `org.apache.jackrabbit.api.stats.RepositoryStatistics` 定義。

* 網域: `com.adobe.granite`
* 類型: `TimeSeries`
* 名稱：以下值之一 `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` 枚舉類：

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * 捆綁計數器
   * BUNDLE_READ_COUNTER
   * 捆綁包_寫入_平均
   * BUNDLE_WRITE_COUNTER
   * 捆綁包寫入持續時間
   * 束_WS_SIZE_COUNTER
   * 查詢平均值
   * 查詢計數
   * 查詢持續時間
   * 會話計數
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * 會話寫持續時間

### 屬性 {#attributes-1}

為報告的每個統計類型提供以下屬性：

* ValuePerSecond:在最後一分鐘內每秒測量的值。 唯讀.
* ValuePerMinute:過去一小時的每分鐘測量值。 唯讀.
* ValuePerHour:上週的每小時測量值。 唯讀.
* ValuePerWeek:過去三年中每週的測量值。 唯讀.

## 資料庫查詢統計 {#repository-query-stats}

有關儲存庫查詢的統計資訊。

* 域：com.adobe.granite
* 類型：查詢統計

### 屬性 {#attributes-2}

**慢速查詢** 有關已花費最長時間完成的儲存庫查詢的資訊。 唯讀.

**慢查詢隊列大小** 要包括在SlowQueries清單中的最大查詢數。 讀寫。

**熱門查詢** 有關發生次數最多的儲存庫查詢的資訊。 唯讀.

**熱門查詢隊列大小** PopulalQueries清單中的最大查詢數。 讀寫。

### 運作 {#operations-2}

**clearSlowQueriesQueue** 從SlowQuerys清單中刪除所有查詢。

* 參數：無
* 返回值：無

**clearPopulQueriesQueue** 從PopulQueries清單中刪除所有查詢。

* 參數：無
* 返回值：無

## 複寫代理程式 {#replication-agents}

監視每個複製代理的服務。 建立複製代理時，該服務將自動顯示在JMX控制台中。

* **域：** com.adobe.granite.replication
* **類型：** 代理
* **名稱：** 無值
* **屬性：** {id=&quot;*名稱*&quot;}，其中 *名稱* 是代理名稱屬性的值。

### 屬性 {#attributes-3}

**ID** 表示複製代理配置標識符的字串值。 多個代理可以使用相同的配置。 唯讀.

**有效** 一個布爾值，它指示代理是否配置正確：

* `true`:有效配置。
* `false` :配置包含錯誤。

唯讀.

**已啟用** 一個布爾值，指示是否啟用代理：

* `true`: 已啟用.
* `false`: 已停用.

**隊列已阻止** 一個布爾值，它指示隊列是否存在且已被阻止：

* `true`: 已封鎖. 自動重試掛起。
* `false`:未阻止或不存在。

唯讀.

**暫停隊列** 指示作業隊列是否已暫停的布爾值：

* `true`:已暫停（掛起）
* `false`:未暫停或不存在。

讀寫。

**QueueNumEntries** 表示代理隊列中作業數的int值。 唯讀.

**隊列狀態時間** 一個日期值，它指示獲取顯示狀態值時伺服器上的時間。 該值與載入頁面的時間相對應。 唯讀.

**QueueNextRetryTime** 對於阻止的隊列，指示下次自動重試的時間的日期值。 如果沒有時間顯示，則不會阻止隊列。 唯讀.

**QueueProcessingSince** 一個日期值，指示當前作業的處理開始時間。 當沒有時間出現時，隊列將被阻止或空閒。 唯讀.

**QueueLastProcessTime** 一個日期值，它指示上一個作業完成的時間。 唯讀.

### 運作 {#operations-3}

**queueForceRetry** 對於被阻止的隊列，向隊列發出重試命令。

* 參數：無
* 返回值：無

**隊列清除** 從隊列中刪除所有作業。

* 參數：無
* 返回值：無

## 吊索引擎 {#sling-engine}

提供有關HTTP請求的統計資訊，以便您可以監視SlingRequestProcessor服務的效能。

* 域：org.apache.sling
* 類型：引擎
* 屬性：{service=RequestProcessor}

### 屬性 {#attributes-4}

**請求計數** 自上次重置統計資訊後發生的請求數。

**最小請求持續時間毫秒** 自上次重置統計資訊以來處理請求所需的最短時間（毫秒）。

**最大請求持續時間毫秒** 自上次重置統計資訊以來處理請求所需的最長時間（毫秒）。

**標準偏差持續時間毫秒** 處理請求所需時間量的標準偏差。 使用自上次重置統計資訊以來的所有請求計算標準偏差。

**平均請求持續時間毫秒** 處理請求所需的平均時間。 平均值是使用自上次重置統計資訊以來的所有請求計算的

### 運作 {#operations-4}

**重置統計資訊** 將所有統計資訊設定為零。 在特定時間範圍內需要分析請求處理效能時重置統計資訊。

* 參數：無
* 返回值：無

**ID** 包ID的字串表示法。

**已安裝** 一個布爾值，它指示是否安裝了包：

* `true`: 已安裝.
* `false`: 未安裝.

**安裝者** 上次安裝軟體包的用戶的ID。

**安裝日期** 上次安裝包的日期。

**大小** 一個長值，它以位元組為單位保存包的大小。


## 快速啟動啟動程式 {#quickstart-launcher}

有關啟動過程和Quickstart啟動程式的資訊。

* 域：com.adobe.granite.quickstart
* 類型：啟動程式

### 運作 {#operations-5}

**日誌**

在「快速啟動」窗口中顯示一條消息。

引數:

* p1:A `String` 表示要顯示的消息的值。
* 返回值：無

**啟動已完成**

調用伺服器啟動程式的startupFinished方法。 該方法嘗試在Web瀏覽器中開啟「歡迎」頁。

* 參數：無
* 返回值：無

**啟動進度**

設定伺服器啟動進程的完成值。 「快速啟動」(QuickStart)窗口中的進度條表示完成值。

* 引數:
   * p1:一個浮點值，它表示啟動過程的完成量（以分數形式）。 值應介於零和1之間。 例如，0.3表示完成30%。
* 返回值：沒有。

## 第三方服務 {#third-party-services}

若干第三方伺服器資源安裝MBean，這些MBean向JMX控制台公開屬性和操作。 下表列出了第三方資源並提供指向詳細資訊的連結。

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
   <td>熱點診斷</td>
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
     <li>記憶體管理器</li>
     <li>記憶體池</li>
     <li>作業系統</li>
     <li>運行時</li>
     <li>線程</li>
    </ul> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.management</a> 包</td>
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
     <li>捆綁狀態</li>
     <li>框架</li>
     <li>包狀態</li>
     <li>服務狀態</li>
    </ul> </td>
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a> 包</td>
  </tr>
 </tbody>
</table>

## 使用JMX控制台 {#using-the-jmx-console}

JMX控制台顯示有關伺服器上運行的若干服務的資訊：

* 屬性：服務屬性，如配置或運行時資料。 屬性可以是只讀的或讀寫的。
* 操作：可以在服務上調用的命令。

使用OSGi服務部署的MBean向控制台顯示服務屬性和操作。 MBean確定公開的屬性和操作，以及屬性是只讀還是讀寫。

JMX控制台的首頁包含服務表。 表中的每一行都表示由MBean公開的服務。

1. 開啟Web控制台，然後按一下JMX頁籤。 ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. 按一下服務的單元格值以查看服務的屬性和操作。
3. 要更改屬性值，請按一下該值，在顯示的對話框中指定值，然後按一下「保存」。
4. 要調用服務操作，請按一下操作名稱，在顯示的對話框中指定參數值，然後按一下調用。

## 使用外部JMX應用程式進行監控 {#using-external-jmx-applications-for-monitoring}

CRX允許外部應用程式通過 [Java管理擴展(JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html)。 使用通用控制台，如 [JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) 或特定於域的監視應用程式，允許獲取和設定CRX配置和屬性，以及監視效能和資源使用情況。

### 使用JConsole連接到CRX {#using-jconsole-to-connect-to-crx}

要使用JConsole連接到CRX，請執行以下步驟：

1. 開啟終端窗口。
1. 輸入以下命令：

   `jconsole`

將啟動JConsole，並出現JConsole窗口。

### 連接到本地CRX進程 {#connecting-to-a-local-crx-process}

JConsole將顯示本地Java虛擬機進程的清單。 清單將包含兩個快速啟動進程。 從本地進程清單中選擇快速啟動「CHILD」進程（通常是PID較高的進程）。

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### 連接到遠程CRX進程 {#connecting-to-a-remote-crx-process}

為了連接到遠程CRX進程，需要啟用承載遠程CRX進程的JVM以接受遠程JMX連接。

要啟用遠程JMX連接，啟動JVM時必須設定以下系統屬性：

`com.sun.management.jmxremote.port=portNum`

在上述財產中， `portNum` 是要啟用JMX RMI連接的埠號。 請確保指定未使用的埠號。 除了發佈用於本地訪問的RMI連接器外，設定此屬性還使用眾所周知的名稱「jmxrmi」在指定埠的專用只讀註冊表中發佈附加的RMI連接器。

預設情況下，啟用JMX代理進行遠程監視時，它使用基於密碼檔案的密碼身份驗證，在啟動Java VM時，需要使用以下系統屬性指定該密碼檔案：

`com.sun.management.jmxremote.password.file=pwFilePath`

查看 [相關JMX文檔](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html) 的子菜單。

範例:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### 使用CRX提供的MBean {#using-the-mbeans-provided-by-crx}

在連接到快速啟動進程後，JConsole為CRX正在運行的JVM提供一系列常規監視工具。

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

要訪問CRX的內部監視和配置選項，請轉到MBeans頁籤，然後從左側的分層內容樹中選擇您感興趣的屬性或操作部分。 例如，com.adobe.granite/Repository/Operations節。

在該部分中，在左窗格中選擇所需的屬性或操作。

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)
