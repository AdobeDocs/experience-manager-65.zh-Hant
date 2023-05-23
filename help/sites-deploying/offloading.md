---
title: 卸載作業
seo-title: Offloading Jobs
description: 瞭解如何在拓撲中配AEM置和使用實例以執行特定類型的處理。
seo-description: Learn how to configure and use AEM instances in a topology in order to perform specific types of processing.
uuid: e971d403-dfd2-471f-b23d-a67e35f1ed88
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 370151df-3b8e-41aa-b586-5c21ecb55ffe
feature: Configuring
exl-id: 429c96ff-4185-4215-97e8-9bd2c130a9b1
source-git-commit: 08a6777bf1ff3abf62f45fe1e164ef2027996848
workflow-type: tm+mt
source-wordcount: '2364'
ht-degree: 2%

---

# 卸載作業{#offloading-jobs}

## 簡介 {#introduction}

卸載在拓撲中的Experience Manager實例之間分配處理任務。 在卸載時，可以使用特定的Experience Manager實例來執行特定類型的處理。 專用處理使您能夠最大限度地利用可用的伺服器資源。

卸載基於 [Apache Sling發現](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) 和Sling JobManager功能。 要使用卸載，可將Experience Manager群集添加到拓撲中並標識群集處理的作業主題。 群集由一個或多個Experience Manager實例組成，因此單個實例被視為群集。

有關向拓撲添加實例的資訊，請參見 [管理拓撲](/help/sites-deploying/offloading.md#administering-topologies)。

### 作業分配 {#job-distribution}

Sling JobManager和JobConsumer可建立拓撲中處理的作業：

* 作業管理器：為特定主題建立作業的服務。
* 作業消費者：執行一個或多個主題的作業的服務。 可以為同一主題註冊多個JobConsumer服務。

當JobManager建立作業時，卸載框架將在拓撲中選擇Experience Manager群集以執行作業：

* 群集必須包括一個或多個運行為作業主題註冊的JobConsumer的實例。
* 必須至少為群集中的一個實例啟用主題。

請參閱 [配置主題消耗](/help/sites-deploying/offloading.md#configuring-topic-consumption) 的子菜單。

![chlimage_1-109](assets/chlimage_1-109.png)

當卸載框架選擇群集以執行作業，並且該群集由多個實例組成時，Sling Distribution將確定群集中哪個實例執行該作業。

### 作業負載 {#job-payloads}

卸載框架支援將作業與儲存庫中的資源相關聯的作業負載。 當為處理資源建立作業並將作業卸載到另一台電腦時，作業負載非常有用。

在建立作業時，僅保證負載位於建立作業的實例上。 卸載作業時，複製代理確保在最終佔用作業的實例上建立負載。 作業執行完成後，反向複製將導致負載被複製回建立作業的實例。

## 管理拓撲 {#administering-topologies}

拓撲是鬆散耦合的Experience Manager群集，參與卸載。 群集由一個或多個Experience Manager伺服器實例（單個實例被視為群集）組成。

每個Experience Manager實例都運行以下與卸載相關的服務：

* 發現服務：向拓撲連接器發送加入拓撲的請求。
* 拓撲連接器：接收加入請求，並接受或拒絕每個請求。

拓撲的所有成員的發現服務指向其中一個成員上的拓撲連接器。 在下面的各節中，此成員稱為根成員。

![chlimage_1-110](assets/chlimage_1-110.png)

拓撲中的每個群集都包含一個被識別為領導者的實例。 群集領導者代表群集的其他成員與拓撲交互。 當引線離開群集時，會自動選擇群集的新引線。

### 查看拓撲 {#viewing-the-topology}

使用拓撲瀏覽器瀏覽Experience Manager實例所參與的拓撲的狀態。 拓撲瀏覽器顯示拓撲的簇和實例。

對於每個群集，都會看到一個群整合員清單，該清單指示每個成員加入群集的順序以及哪個成員是領導者。 「當前」屬性指明當前管理的實例。

對於群集中的每個實例，您可以看到幾個與拓撲相關的屬性：

* 實例的作業使用者的允許主題清單。
* 為與拓撲連接而暴露的端點。
* 註冊實例以卸載的作業主題。
* 實例處理的作業主題。

1. 使用「Touch UI（觸摸UI）」 ，按一下「Tools（工具）」頁籤。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. 在「花崗岩操作」(Granite Operations)區域中，按一下「卸載瀏覽器」(Offloading Browser)。
1. 在導航面板中，按一下拓撲瀏覽器。

   將出現參與拓撲的群集。

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. 按一下群集可查看群集中實例及其ID、當前狀態和領導狀態的清單。
1. 按一下實例ID以查看更詳細的屬性。

您還可以使用Web控制台查看拓撲資訊。 控制台提供了有關拓撲群集的詳細資訊：

* 哪個實例是本地實例。
* 此實例用於連接到拓撲（傳出）的拓撲連接器服務，以及連接到此實例（傳入）的服務。
* 更改拓撲和實例屬性的歷史記錄。

請按下列步驟開啟Web控制台的「拓撲管理」頁：

1. 在瀏覽器中開啟Web控制台。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 按一下「主」>「拓撲管理」。

   ![chlimage_1-112](assets/chlimage_1-112.png)

### 配置拓撲成員身份 {#configuring-topology-membership}

基於Apache Sling資源的發現服務在每個實例上運行，以控制Experience Manager實例與拓撲交互的方式。

發現服務將定期向拓撲連接器服務發送POST請求（心跳），以建立和維護與拓撲的連接。 拓撲連接器服務維護允許加入拓撲的IP地址或主機名清單：

* 要將實例加入拓撲，請指定根成員的拓撲連接器服務的URL。
* 要啟用實例加入拓撲，請將實例添加到根成員的拓撲連接器服務的允許清單中。

使用Web控制台或sling:OsgiConfig節點配置org.apache.sling.discovery.impt.Config服務的以下屬性：

<table>
 <tbody>
  <tr>
   <th>屬性名稱</th>
   <th>OSGi名稱</th>
   <th>說明</th>
   <th>預設值</th>
  </tr>
  <tr>
   <td>心跳超時（秒）</td>
   <td>心跳超時</td>
   <td>在目標實例被視為不可用之前等待心跳響應的時間（秒）。 </td>
   <td>20</td>
  </tr>
  <tr>
   <td>心跳間隔（秒）</td>
   <td>心跳間隔</td>
   <td>心跳之間的時間（秒）。</td>
   <td>15</td>
  </tr>
  <tr>
   <td>最小事件延遲（秒）</td>
   <td>minEventDelay</td>
   <td><p>當拓撲發生更改時，將狀態從TOPOLOGY_CHANGING延遲到TOPOLOGY_CHANGED的時間。 當狀態為TOPOLOGY_CHANGING時，每次更改都會將延遲增加此時間量。</p> <p>這種延遲防止監聽器被事件淹沒。 </p> <p>要不使用延遲，請指定0或負數。</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>拓撲連接器URL</td>
   <td>拓撲連接器URL</td>
   <td>用於發送心跳消息的拓撲連接器服務的URL。</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>拓撲連接器允許清單</td>
   <td>拓撲連接器白名單</td>
   <td>本地拓撲連接器服務允許的IP地址或主機名清單。 </td>
   <td><p>本地主機</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>儲存庫描述符名稱</td>
   <td>leaderElectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;無值&gt;</td>
  </tr>
 </tbody>
</table>

請按下列步驟將CQ實例連接到拓撲的根成員。 該過程將實例指向根拓撲成員的拓撲連接器URL。 對拓撲的所有成員執行此過程。

1. 在瀏覽器中開啟Web控制台。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 按一下「主」>「拓撲管理」。
1. 按一下配置發現服務。
1. 將項添加到拓撲連接器URL屬性，並指定根拓撲成員的拓撲連接器服務的URL。 URL的格式為https://rootservername:4502/libs/sling/topology/connector。

對拓撲的根成員執行以下過程。 該過程將其他拓撲成員的名稱添加到其發現服務允許清單中。

1. 在瀏覽器中開啟Web控制台。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 按一下「主」>「拓撲管理」。
1. 按一下配置發現服務。
1. 對於拓撲的每個成員，將項添加到拓撲連接器允許清單屬性，並指定拓撲成員的主機名或IP地址。

## 配置主題消耗 {#configuring-topic-consumption}

使用卸載瀏覽器為拓撲中的Experience Manager實例配置主題消耗。 對於每個實例，可以指定它使用的主題。 例如，要配置拓撲，以便只有一個實例使用特定類型的主題，請在除一個實例之外的所有實例上禁用該主題。

作業在使用循環邏輯啟用關聯主題的實例之間分配。

1. 使用「Touch UI（觸摸UI）」 ，按一下「Tools（工具）」頁籤。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. 在「花崗岩操作」(Granite Operations)區域中，按一下「卸載瀏覽器」(Offloading Browser)。
1. 在導航面板中，按一下「卸載瀏覽器」。

   此時將顯示卸載主題以及可使用主題的伺服器實例。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 要禁用實例的主題消耗，請在主題名稱下按一下實例旁邊的禁用。
1. 要配置實例的所有主題消耗，請按一下任何主題下的實例標識符。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 按一下主題旁邊的以下按鈕之一以配置實例的消耗行為，然後按一下「保存」：

   * 已啟用：此實例將消耗此主題的作業。
   * 已禁用：此實例不使用此主題的作業。
   * 獨家：此實例僅使用此主題的作業。

   **注：** 為主題選擇「排它」時，所有其它主題將自動設定為「禁用」。

### 已安裝的作業使用者 {#installed-job-consumers}

安裝了多個JobConsumer實現，並帶有Experience Manager。 註冊這些JobConsumer的主題顯示在卸載瀏覽器中。 出現的其他主題是自定義JobConduser已註冊的主題。 下表介紹了預設的JobConsuler。

| 作業主題 | 服務PID | 說明 |
|---|---|---|
| / | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | 已安裝Apache Sling。 處理OSGi事件管理員生成的作業，以實現向後相容性。 |
| com/day/cq/replication/job/&amp;ast; | com.day.cq.replication.impl.AgentManagerImpl | 復製作業負載的複製代理。 |

<!--
| com/adobe/granite/workflow/offloading |com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer |Processes jobs that the DAM Update Asset Offloader workflow generates. |
-->

### 禁用和啟用實例的主題 {#disabling-and-enabling-topics-for-an-instance}

Apache Sling作業使用者管理器服務提供主題允許清單和阻止清單屬性。 配置這些屬性以啟用或禁用對Experience Manager實例的特定主題的處理。

**注：** 如果實例屬於拓撲，您還可以在拓撲中的任何電腦上使用「卸載瀏覽器」來啟用或禁用主題。

建立啟用主題清單的邏輯首先允許允許清單中的所有主題，然後刪除塊清單上的主題。 預設情況下，所有主題都處於啟用狀態(允許清單值為 `*`)且未禁用任何主題（阻止清單沒有值）。

使用Web控制台或 `sling:OsgiConfig` 節點以配置以下屬性。 對於 `sling:OsgiConfig` 節點，作業使用者管理器服務的PID為org.apache.sling.event.impl.jobs.JobConsumerManager。

| Web控制台中的屬性名稱 | OSGi ID | 說明 |
|---|---|---|
| 主題允許清單 | job.consumermanager.whitelist | 本地JobManager服務處理的主題清單。 &amp;ast；的預設值使所有主題都發送到註冊的TopicConsumer服務。 |
| 主題塊清單 | job.consumermanager.blacklist | 本地JobManager服務未處理的主題清單。 |

## 建立複製代理以卸載 {#creating-replication-agents-for-offloading}

卸載框架使用複製在作者和工作者之間傳輸資源。 卸載框架會在實例加入拓撲時自動建立複製代理。 使用預設值建立代理。 您必須手動更改代理用於身份驗證的密碼。

>[!CAUTION]
>
>自動生成的複製代理存在一個已知問題，需要您手動建立新的複製代理。

建立在實例之間傳輸作業負載以便卸載的複製代理。 下圖顯示了從作者卸載到工作實例所需的代理。 作者的Sling ID為1，工作實例的Sling ID為2:

![chlimage_1-115](assets/chlimage_1-115.png)

此安裝程式需要以下三個代理：

1. 作者實例上的傳出代理，該代理複製到工作實例。
1. 作者實例上的反向代理，它從工作者實例的發件箱中拉出。
1. 工作實例上的發件箱代理。

此複製方案與作者實例和發佈實例之間使用的複製方案類似。 但是，對於卸載情況，涉及的所有實例都是創作實例。

>[!NOTE]
>
>卸載框架使用拓撲獲取卸載實例的IP地址。 然後，該框架會根據這些IP地址自動建立複製代理。 如果卸載實例的IP地址稍後更改，則在實例重新啟動後，更改將自動傳播到拓撲上。 但是，卸載框架不會自動更新複製代理以反映新的IP地址。 為避免這種情況，請為拓撲中的所有實例使用固定IP地址。

### 命名複製代理以卸載 {#naming-the-replication-agents-for-offloading}

為 ***名稱*** 複製代理的屬性，以便卸載框架自動為特定工作實例使用正確的代理。

**在作者實例上命名傳出代理：**

`offloading_<slingid>`，也請參見Wiki頁。 `<slingid>` 是工作器實例的Sling ID。

範例: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**在作者實例上命名反向代理：**

`offloading_reverse_<slingid>`，也請參見Wiki頁。 `<slingid>` 是工作器實例的Sling ID。

範例: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**命名工作實例上的發件箱：**

`offloading_outbox`

### 建立傳出代理 {#creating-the-outgoing-agent}

1. 建立 **複製代理** 作者。 (請參閱 [複製代理文檔](/help/sites-deploying/replication.md))。 指定任意 **標題**。 的 **名稱** 必須遵循命名約定。
1. 使用以下屬性建立代理：

   | 屬性 | 值 |
   |---|---|
   | 設定>序列化類型 | 預設 |
   | 傳輸>傳輸URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | 傳輸>傳輸用戶 | 目標實例上的複製用戶 |
   | 傳輸>傳輸密碼 | 目標實例上的複製用戶密碼 |
   | 「擴展」>「HTTP方法」 | POST |
   | 觸發器>忽略預設值 | True |

### 建立反向代理 {#creating-the-reverse-agent}

1. 建立 **反向複製代理** 作者。 (請參閱 [複製代理文檔](/help/sites-deploying/replication.md)。) 指定任意 **標題**。 的 **名稱** 必須遵循命名約定。
1. 使用以下屬性建立代理：

   | 屬性 | 值 |
   |---|---|
   | 設定>序列化類型 | 預設 |
   | 傳輸>傳輸URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | 傳輸>傳輸用戶 | 目標實例上的複製用戶 |
   | 傳輸>傳輸密碼 | 目標實例上的複製用戶密碼 |
   | 「擴展」>「HTTP方法」 | GET |

### 建立發件箱代理 {#creating-the-outbox-agent}

1. 建立 **複製代理** 在工作實例上。 (請參閱 [複製代理文檔](/help/sites-deploying/replication.md)。) 指定任意 **標題**。 的 **名稱** 必須 `offloading_outbox`。
1. 使用以下屬性建立代理。

   | 屬性 | 值 |
   |---|---|
   | 設定>序列化類型 | 預設 |
   | 傳輸>傳輸URI | repo://var/replication/outbox |
   | 觸發器>忽略預設值 | True |

### 查找吊帶ID {#finding-the-sling-id}

使用以下任一方法獲取Experience Manager實例的Sling ID:

* 開啟Web控制台，在「Sling設定」中查找Sling ID屬性的值([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings))。 如果實例尚未成為拓撲的一部分，則此方法非常有用。
* 如果實例已是拓撲的一部分，則使用拓撲瀏覽器。

<!--
## Offloading the Processing of DAM Assets {#offloading-the-processing-of-dam-assets}

Configure the instances of a topology so that specific instances perform the background processing of assets that are added or updated in DAM.

By default, Experience Manager executes the [!UICONTROL DAM Update Asset] workflow when a DAM asset changes or one is added to DAM. Change the default behavior so that Experience Manager instead executes the [!UICONTROL DAM Update Asset Offloader] workflow. This workflow generates a JobManager job that has a topic of `com/adobe/granite/workflow/offloading`. Then, configure the topology so that the job is offloaded to a dedicated worker.

>[!CAUTION]
>
>No workflow should be transient when used with workflow offloading. For example, the [!UICONTROL DAM Update Asset] workflow must not be transient when used for asset offloading. To set/unset the transient flag on a workflow, see [Transient Workflows](/help/assets/performance-tuning-guidelines.md#workflows).

The following procedure assumes the following characteristics for the offloading topology:

* One or more Experience Manager instance are authoring instances that users interact with for adding or updating DAM assets.
* Users to do not directly interact with one or more Experience Manager instances that process the DAM assets. These instances are dedicated to the background processing of DAM assets.

1. On each Experience Manager instance, configure the Discovery Service so that it points to the root Topography Connector. (See [Configuring Topology Membership](#title4).)
1. Configure the root Topography Connector so that the connecting instances are on the allow list.
1. Open Offloading Browser and disable the `com/adobe/granite/workflow/offloading` topic on the instances with which users interact to upload or change DAM assets.

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. On each instance that users interact with to upload or change DAM assets, configure workflow launchers to use the [!UICONTROL DAM Update Asset Offloading] workflow:

    1. Open the Workflow console.
    1. Click the Launcher tab.
    1. Locate the two Launcher configurations that execute the [!UICONTROL DAM Update Asset] workflow. One launcher configuration event type is Node Created, and the other type is Node Modified.
    1. Change both event types so that they execute the [!UICONTROL DAM Update Asset Offloading] workflow. (For information about launcher configurations, see [Starting Workflows When Nodes Change](/help/sites-administering/workflows-starting.md).)

1. On the instances that perform the background processing of DAM assets, disable the workflow launchers that execute the [!UICONTROL DAM Update Asset] workflow.
-->

## 延伸閱讀 {#further-reading}

除了此頁上提供的詳細資訊外，您還可以閱讀以下內容：

* 有關使用Java API建立作業和作業使用者的資訊，請參見 [建立和使用卸載作業](/help/sites-developing/dev-offloading.md)。
