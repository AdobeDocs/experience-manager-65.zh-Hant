---
title: 卸載作業
seo-title: 卸載作業
description: 瞭解如何在拓撲中設定和使用AEM例項，以執行特定類型的處理。
seo-description: 瞭解如何在拓撲中設定和使用AEM例項，以執行特定類型的處理。
uuid: e971d403-dfd2-471f-b23d-a67e35f1ed88
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 370151df-3b8e-41aa-b586-5c21ecb55ffe
translation-type: tm+mt
source-git-commit: 4ccaf401d561087f864c95e2be4c594cf34a7cb7

---


# 卸載作業{#offloading-jobs}

## 簡介 {#introduction}

卸載會在拓撲中分發包含Experience manager實例的處理任務。 借由卸載，您可以使用特定的Experience manager實例來執行特定類型的處理。 專業化的處理可讓您最大化可用伺服器資源的使用。

Offloading是以 [Apache Sling Discovery和Sling JobManager功能為基礎](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) 。 要使用卸載，請將Experience manager群集添加到拓撲中，並標識群集處理的作業主題。 叢集由一或多個Experience manager實例組成，因此單一實例被視為叢集。

有關向拓撲添加實例的資訊，請參見管 [理拓撲](/help/sites-deploying/offloading.md#administering-topologies)。

### 工作分發 {#job-distribution}

Sling JobManager和JobConsumer可建立在拓撲中處理的工作：

* JobManager:為特定主題建立作業的服務。
* JobConsumer:執行一個或多個主題的作業的服務。 可針對相同主題註冊多個JobConsumer服務。

當JobManager建立作業時，卸載框架在拓撲中選擇Experience Manager群集以執行該作業：

* 群集必須包含一個或多個運行為作業主題註冊的JobConsumer實例。
* 必須至少為群集中的一個實例啟用主題。

有關 [優化任務分配的資訊](/help/sites-deploying/offloading.md#configuring-topic-consumption) ，請參閱配置主題衝減。

![chlimage_1-109](assets/chlimage_1-109.png)

當Offloading架構選擇叢集以執行工作，而叢集由多個例項組成時，Sling Distribution會決定叢集中哪個例項執行工作。

### 工作負載 {#job-payloads}

卸載框架支援將作業與儲存庫中的資源關聯的作業裝載。 當為處理資源建立作業並且作業卸載到另一台電腦時，作業負載很有用。

在建立作業時，僅保證裝載位於建立作業的實例上。 卸載作業時，複製代理確保在最終佔用作業的實例上建立裝載。 作業執行完成後，反向複製會將裝載複製回建立作業的例項。

## 管理拓撲 {#administering-topologies}

拓撲是鬆散耦合的Experience manager群集，它們參與卸載。 群集由一個或多個Experience manager伺服器實例（單個實例被視為群集）組成。

每個Experience manager實例都運行以下卸載相關服務：

* 發現服務：向拓撲連接器發送請求以加入拓撲。
* 拓撲連接器：接收加入請求，並接受或拒絕每個請求。

拓撲的所有成員的發現服務指向其中一個成員的拓撲連接器。 在以下幾節中，此成員稱為根成員。

![chlimage_1-110](assets/chlimage_1-110.png)

拓撲中的每個群集都包含一個被識別為領導者的實例。 群集領導者代表群集的其他成員與拓撲交互。 當領導者離開群集時，會自動選擇群集的新領導者。

### 查看拓撲 {#viewing-the-topology}

使用拓撲瀏覽器來探索Experience manager實例參與的拓撲狀態。 拓撲瀏覽器顯示拓撲的群集和實例。

對於每個群集，您會看到一個群整合員清單，其中指明每個成員加入群集的順序以及哪個成員是「領導者」。 「目前」屬性會指出您目前管理的例項。

對於群集中的每個實例，您可以看到幾個與拓撲相關的屬性：

* 實例的工作使用者主題的白名單。
* 用於與拓撲連接的端點。
* 已註冊實例以卸載的作業主題。
* 實例處理的作業主題。

1. 使用Touch UI，按一下「工具」標籤。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. 在「Granite Operations」（花崗岩作業）區域中，按一下「Offloading Browser」（卸載瀏覽器）。
1. 在導航面板中，按一下拓撲瀏覽器。

   將出現參與拓撲的群集。

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. 按一下群集可查看集群中實例及其ID、當前狀態和領導狀態的清單。
1. 按一下例項ID以檢視更詳細的屬性。

您也可以使用Web控制台查看拓撲資訊。 控制台提供了拓撲群集的詳細資訊：

* 哪個實例是本地實例。
* 此實例用於連接到拓撲（傳出）的拓撲連接器服務，以及連接到此實例（傳入）的服務。
* 更改拓撲和實例屬性的歷史記錄。

請按下列步驟開啟Web控制台的「拓撲管理」頁：

1. 在瀏覽器中開啟Web Console。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 按一下主>拓撲管理。

   ![chlimage_1-112](assets/chlimage_1-112.png)

### 配置拓撲成員 {#configuring-topology-membership}

Apache Sling Resource-Based Discovery Service會在每個執行個體上執行，以控制Experience Manager執行個體與拓撲互動的方式。

Discovery service會定期向拓撲連接器服務發送POST請求（心跳），以建立和維護與拓撲的連接。 拓撲連接器服務維護允許加入拓撲的IP地址或主機名的白名單：

* 要將實例連接到拓撲，請指定根成員的拓撲連接器服務的URL。
* 要啟用實例加入拓撲，請將實例添加到根成員的拓撲連接器服務的白名單中。

使用Web Console或sling:OsgiConfig節點來設定org.apache.sling.discovery.impt.Config服務的下列屬性：

<table>
 <tbody>
  <tr>
   <th>屬性名稱</th>
   <th>OSGi名稱</th>
   <th>說明</th>
   <th>預設值</th>
  </tr>
  <tr>
   <td>心率逾時（秒）</td>
   <td>heartbeatTimeout</td>
   <td>等待心率回應的秒數量，以秒為單位，目標例項才會被視為無法使用。 </td>
   <td>20</td>
  </tr>
  <tr>
   <td>心率間隔（秒）</td>
   <td>heartbeatInterval</td>
   <td>心率之間的秒數。</td>
   <td>15</td>
  </tr>
  <tr>
   <td>最小事件延遲（秒）</td>
   <td>minEventDelay</td>
   <td><p>當拓撲發生變化時，將狀態從TOPOLOGY_CHANGING延遲到TOPOLOGY_CHANGED的時間。 當狀態為TOPOLOGY_CHANGING時，每次更改都會將延遲增加此時間量。</p> <p>這種延遲可防止監聽器被事件淹沒。 </p> <p>若要不使用延遲，請指定0或負數。</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>拓撲連接器URL</td>
   <td>topologyConnectorUrls</td>
   <td>用於發送心跳消息的拓撲連接器服務的URL。</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>拓撲連接器白名單</td>
   <td>topologyConnector白名單</td>
   <td>本地拓撲連接器服務允許的IP地址或主機名清單。 </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>儲存庫描述符名稱</td>
   <td>leaderElectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;無值&gt;</td>
  </tr>
 </tbody>
</table>

使用以下過程將CQ實例連接到拓撲的根成員。 該過程將實例指向根拓撲成員的拓撲連接器URL。 對拓撲的所有成員執行此過程。

1. 在瀏覽器中開啟Web Console。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 按一下主>拓撲管理。
1. 按一下配置發現服務。
1. 將項添加到拓撲連接器URL屬性中，並指定根拓撲成員的拓撲連接器服務的URL。 URL的格式為https://rootservername:4502/libs/sling/topology/connector。

對拓撲的根成員執行以下過程。 該過程將其他拓撲成員的名稱添加到其Discovery服務白名單中。

1. 在瀏覽器中開啟Web Console。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 按一下主>拓撲管理。
1. 按一下配置發現服務。
1. 對於拓撲的每個成員，將一個項添加到「拓撲連接器白名單」屬性，並指定拓撲成員的主機名或IP地址。

## 配置主題使用 {#configuring-topic-consumption}

使用卸載瀏覽器為拓撲中的Experience manager實例配置主題使用。 您可以針對每個例項指定其所使用的主題。 例如，要配置拓撲以便只有一個實例使用特定類型的主題，請禁用除一個實例以外的所有實例上的主題。

作業是使用循環邏輯啟用相關主題的分佈數量例項。

1. 使用Touch UI，按一下「工具」標籤。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. 在「Granite Operations」（花崗岩作業）區域中，按一下「Offloading Browser」（卸載瀏覽器）。
1. 在導覽面板中，按一下「卸載瀏覽器」。

   此時會顯示卸載主題和可使用主題的伺服器實例。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 要禁用實例的主題消耗，請在topc名稱下按一下實例旁邊的禁用。
1. 要配置實例的所有主題使用，請按一下任何主題下的實例標識符。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 按一下主題旁邊的以下按鈕之一以配置實例的衝減行為，然後按一下保存：

   * 啟用：此實例將使用此主題的作業。
   * 停用：此實例不會使用此主題的作業。
   * 獨家：此實例僅會使用此主題的作業。
   **** 注意：為主題選擇「獨佔」時，所有其它主題都會自動設定為「禁用」。

### 已安裝的作業使用者 {#installed-job-consumers}

Experience manager已安裝數個JobConsumer實作。 這些JobConsumers註冊的主題會顯示在卸載瀏覽器中。 出現的其他主題是自訂JobConsumers已註冊的主題。 下表說明預設的JobConsumers。

| 工作主題 | 服務PID | 說明 |
|---|---|---|
| / | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | 已與Apache Sling一起安裝。 處理OSGi事件管理員所產生的作業，以便向後相容。 |
| com/day/cq/replication/job/&amp;ast; | com.day.cq.replication.impl.AgentManagerImpl | 複製代理，用於復製作業負載。 |
| com/adobe/granite/workflow/offloading | com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer | 處理DAM更新資產卸載程式工作流生成的作業。 |

### 禁用和啟用實例的主題 {#disabling-and-enabling-topics-for-an-instance}

Apache Sling Job Consumer Manager服務提供主題白名單和黑名單屬性。 設定這些屬性，以啟用或停用Experience manager例項上特定主題的處理。

**** 注意：如果實例屬於拓撲，您也可以在拓撲中的任何電腦上使用卸載瀏覽器來啟用或禁用主題。

建立已啟用主題清單的邏輯首先允許白名單中的所有主題，然後刪除黑名單中的主題。預設情況下，所有主題都處於啟用狀態(白名單值為 `*`)且不禁用任何主題（黑名單沒有值）。

使用Web控制台或節 `sling:OsgiConfig` 點來配置以下屬性。 對 `sling:OsgiConfig` 於節點，Job Consumer Manager服務的PID是org.apache.sling.event.impl.jobs.JobConsumerManager。

| Web Console中的屬性名稱 | OSGi ID | 說明 |
|---|---|---|
| 主題白名單 | job.counsmermanager.whitelist | 本地JobManager服務處理的主題清單。 &amp;ast；的預設值使所有主題都發送到註冊的TopicConsumer服務。 |
| 主題黑名單 | job.counspermanager.blacklist | 本地JobManager服務不處理的主題清單。 |

## 建立用於卸載的複製代理 {#creating-replication-agents-for-offloading}

卸載框架使用複製在作者和工作者之間傳輸資源。 卸載框架會在實例加入拓撲時自動建立複製代理。 代理是使用預設值建立的。 您必須手動更改代理用於驗證的密碼。

>[!CAUTION]
>
>自動生成的複製代理的已知問題要求您手動建立新的複製代理。 在建立要卸載的 [代理之前，請遵循使用自動生成的複製代理](/help/sites-deploying/offloading.md#problems-using-the-automatically-generated-replication-agents) 「問題」中的過程。

建立在實例之間傳輸作業負載以卸載的複製代理。 下圖顯示了從作者卸載到工作實例所需的代理。 The author has a Sling ID of 1 and the worker instance has a Sling ID of 2:

![chlimage_1-115](assets/chlimage_1-115.png)

此設定需要以下三個代理：

1. 作者實例上的一個外發代理，它複製到該工作器實例。
1. 作者實例上的反向代理，從工作器實例的外框提取。
1. 工作器實例上的外框代理。

此複製方案類似於作者和發佈實例之間使用的複製方案。 但是，對於卸載情況，涉及的所有實例都是編寫實例。

>[!NOTE]
>
>卸載框架使用拓撲獲取卸載實例的IP地址。 然後，框架會根據這些IP地址自動建立複製代理。 如果卸載實例的IP地址稍後更改，則在實例重新啟動後，該更改會自動在拓撲上顯示。 但是，卸載框架不會自動更新複製代理以反映新的IP地址。 為避免這種情況，請對拓撲中的所有實例使用固定的IP地址。

### 命名要卸載的複製代理 {#naming-the-replication-agents-for-offloading}

對複製代理的 ***Name*** 屬性使用特定格式，以便卸載框架自動為特定工作器實例使用正確的代理。

**在作者實例上命名傳出代理：**

`offloading_<slingid>`，其 `<slingid>` 中是worker實例的Sling ID。

例如: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**在作者實例上命名反向代理：**

`offloading_reverse_<slingid>`，其 `<slingid>` 中是worker實例的Sling ID。

例如: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**在工作器實例上命名外框：**

`offloading_outbox`

### 建立傳出代理 {#creating-the-outgoing-agent}

1. 在作者 **上建立Replication Agent** 。 (請參見 [有關複製代理的文檔](/help/sites-deploying/replication.md))。 指定任何 **標題**。 名 **稱必** 須遵循命名慣例。
1. 使用以下屬性建立代理：

   | 屬性 | 值 |
   |---|---|
   | 設定>序列化類型 | 預設 |
   | 傳輸>傳輸URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | 傳輸>傳輸用戶 | 目標實例上的複製用戶 |
   | 運輸>運輸密碼 | 目標實例上的複製用戶密碼 |
   | 「延伸> HTTP方法」 | 貼文 |
   | 「觸發器」>「忽略預設值」 | True |

### 建立反向代理 {#creating-the-reverse-agent}

1. 在作者 **上建立反向複製** Agent。 (請參見 [有關複製代理的文檔](/help/sites-deploying/replication.md)。)指定任何 **標題**。 名 **稱必** 須遵循命名慣例。
1. 使用以下屬性建立代理：

   | 屬性 | 值 |
   |---|---|
   | 設定>序列化類型 | 預設 |
   | 傳輸>傳輸URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | 傳輸>傳輸用戶 | 目標實例上的複製用戶 |
   | 運輸>運輸密碼 | 目標實例上的複製用戶密碼 |
   | 「延伸> HTTP方法」 | 取得 |

### 建立外框代理 {#creating-the-outbox-agent}

1. 在工作 **器實例上建立複製代理** 。 (請參見 [有關複製代理的文檔](/help/sites-deploying/replication.md)。)指定任何 **標題**。 名 **稱必** 須 `offloading_outbox`。
1. 使用下列屬性建立代理。

   | 屬性 | 值 |
   |---|---|
   | 設定>序列化類型 | 預設 |
   | 傳輸>傳輸URI | repo://var/replication/outbox |
   | 觸發器>忽略預設值 | True |

### 尋找Sling ID {#finding-the-sling-id}

使用下列任一方法取得Experience manager例項的Sling ID:

* 開啟Web Console，然後在Sling Settings中尋找Sling ID屬性的值([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings))。 如果實例尚未屬於拓撲，則此方法可用。
* 如果實例已屬於拓撲的一部分，請使用拓撲瀏覽器。

## 卸載DAM資產的處理 {#offloading-the-processing-of-dam-assets}

配置拓撲實例，使特定實例執行在DAM中添加或更新的資產的後台處理。

依預設，當DAM資產變更或新增DAM時，Experience manager會執行DAM更新資產工作流程。 變更預設行為，讓Experience Manager改為執行DAM更新資產卸載程式工作流程。 此工作流將生成一個主題為的JobManager作業 `com/adobe/granite/workflow/offloading`。 然後，配置拓撲，以便將作業卸載到專用工作器。

>[!CAUTION]
>
>當與工作流卸載一起使用時，不應使工作流為瞬態。 例如，當用於資產卸載時，「DAM更新資產」工作流程不得是暫時的。 要在工作流中設定／取消設定臨時標誌，請參 [閱臨時工作流](/help/assets/performance-tuning-guidelines.md#workflows)。

以下過程假定卸載拓撲具有以下特徵：

* 一或多個Experience manager實例正在編寫使用者與之互動的例項，以新增或更新DAM資產。
* 使用者不需直接與處理DAM資產的一或多個Experience manager例項互動。 這些例項專用於DAM資產的背景處理。

1. 在每個Experience manager實例上，配置Discovery服務，使其指向根拓撲連接器。 (請參閱 [配置拓撲成員資格](#title4)。)
1. 配置根拓撲連接器，使連接實例位於白名單中。
1. 開啟「卸載瀏覽器」，並停 `com/adobe/granite/workflow/offloading` 用使用者與之互動以上傳或變更DAM資產之例項的主題。

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. 在使用者互動以上傳或變更DAM資產的每個例項上，設定工作流程啟動器以使用「DAM更新資產卸載」工作流程：

   1. 開啟「工作流程」主控台。
   1. 按一下「啟動器」標籤。
   1. 找到執行DAM更新資產工作流程的兩個啟動器配置。 一個啟動程式配置事件類型是「已建立節點」，另一個類型是「已修改節點」。
   1. 變更這兩種事件類型，以執行DAM更新資產卸載工作流程。 (有關啟動程式配置的資訊，請參 [閱Starting Workflows When Nodes Change](/help/sites-administering/workflows-starting.md))。

1. 在執行DAM資產背景處理的例項上，停用執行DAM更新資產工作流程的工作流程啟動器。

## 進一步閱讀 {#further-reading}

除了本頁上顯示的詳細資訊外，您也可以閱讀下列內容：

* 有關使用Java API建立作業和作業使用者的資訊，請參 [閱建立和使用卸載作業](/help/sites-developing/dev-offloading.md)。
