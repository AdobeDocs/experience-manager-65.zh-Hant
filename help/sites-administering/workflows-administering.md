---
title: 管理工作流程例項
seo-title: Administering Workflow Instances
description: 了解如何管理工作流程例項。
seo-description: Lear how to administer Workflow Instances.
uuid: 81e53ef5-fe62-4ed4-b2d4-132aa986d5aa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d9c96e7f-9416-48e1-a6af-47384f7bee92
exl-id: 90923d39-3ac5-4028-976c-d011f0404476
source-git-commit: 8b4459c69b73159ce5afd819dfb772df5c51cd16
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 0%

---

# 管理工作流程例項{#administering-workflow-instances}

工作流程控制台提供數種管理工作流程例項的工具，以確保這些例項可如預期般執行。

>[!NOTE]
>
>此 [JMX控制台](/help/sites-administering/jmx-console.md#workflow-maintenance) 提供其他工作流維護操作。

管理工作流程時可使用多種主控台。 使用 [全局導航](/help/sites-authoring/basic-handling.md#global-navigation) 開啟 **工具** 窗格，然後選擇 **工作流程**:

* **模型**:管理工作流程定義
* **例項**:檢視及管理執行中的工作流程例項
* **啟動器**:管理工作流程的啟動方式
* **封存**:檢視成功完成的工作流程記錄
* **失敗**:檢視已完成但有錯誤的工作流程的歷史記錄
* **自動指派**:設定為範本自動指派工作流程

## 監控工作流實例的狀態 {#monitoring-the-status-of-workflow-instances}

1. 使用導覽選取 **工具**，然後 **工作流程**.
1. 選擇 **例項** 顯示當前正在進行的工作流實例清單。

   ![wf-96](assets/wf-96.png)


## 搜尋工作流程例項 {#search-workflow-instances}

1. 使用導覽選取 **工具**，然後 **工作流程**.
1. 選擇 **例項** 顯示當前正在進行的工作流實例清單。 在頂端邊欄的左角，選取 **篩選器**. 或者，您可以使用鍵擊alt+1。 將顯示以下對話框：

   ![wf-99-1](assets/wf-99-1.png)

1. 在「篩選」對話方塊中，選取工作流程搜尋條件。 您可以根據以下輸入進行搜尋：

   * 裝載路徑：選取特定路徑
   * 工作流模型：選擇工作流模型
   * 受託人：選擇工作流受託人
   * 類型：任務、工作流項或工作流失敗
   * 任務狀態：活動、完成或終止
   * 我的位置：OWNER AND Assignee，僅限Owner，僅受託人
   * 開始日期：指定日期之前或之後的開始日期
   * 結束日期：指定日期之前或之後的結束日期
   * 到期日：指定日期之前或之後的到期日
   * 更新日期：在指定日期之前或之後更新日期

## 暫停、繼續和終止工作流實例 {#suspending-resuming-and-terminating-a-workflow-instance}

1. 使用導覽選取 **工具**，然後 **工作流程**.
1. 選擇 **例項** 顯示當前正在進行的工作流實例清單。

   ![wf-96-1](assets/wf-96-1.png)

1. 選取特定項目，然後使用 **終止**, **暫停**，或 **繼續**，酌情；確認，和/或更多詳細資訊是必要的：

   ![wf-97-1](assets/wf-97-1.png)

## 檢視封存的工作流程 {#viewing-archived-workflows}

1. 使用導覽選取 **工具**，然後 **工作流程**.
1. 選擇 **封存** 顯示成功完成的工作流實例清單。

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >中止狀態被視為成功終止，因為它是由於用戶操作而發生的；例如：
   >
   >* 使用 **終止** 動作
   >* 當受工作流約束的頁面被（強制）刪除時，工作流將被終止


1. 選取特定項目，然後 **開啟歷史記錄** 若要查看更多詳細資訊，請：

   ![wf-99](assets/wf-99.png)

## 修正工作流程執行個體失敗 {#fixing-workflow-instance-failures}

工作流程失敗時，AEM會提供 **失敗** 控制台，讓您在處理原始原因後調查並採取適當動作：

* **失敗詳細資訊**
開啟視窗以顯示 
**失敗訊息**, **步驟** 和 **失敗堆棧**.

* **開啟歷史記錄**
顯示工作流歷史記錄的詳細資訊。

* **重試步驟** 再次執行指令碼步驟元件實例。 修正了原始錯誤的原因後，請使用「重試步驟」命令。 例如，在您修正了「處理步驟」所執行指令碼中的錯誤後，請重試該步驟。
* **終止** 如果錯誤導致工作流的不可重複情況，則終止工作流。 例如，工作流可以依賴於環境條件，例如儲存庫中對工作流實例不再有效的資訊。
* **終止並重試** 類似 **終止** 除了使用原始裝載、標題和說明來啟動新的工作流程例項。

要調查失敗，然後恢復或之後終止工作流，請執行以下步驟：

1. 使用導覽選取 **工具**，然後 **工作流程**.
1. 選擇 **失敗** 顯示未成功完成的工作流實例清單。
1. 選擇特定項目，然後選擇相應的操作：

   ![wf-47](assets/wf-47.png)

## 定期清除工作流實例 {#regular-purging-of-workflow-instances}

將工作流實例數減到最少會提高工作流引擎的效能，因此您可以定期從儲存庫中清除已完成或正在運行的工作流實例。

設定 **AdobeGranite工作流程清除設定** 根據工作流實例的年齡和狀態來清除實例。 您也可以清除所有模型或特定模型的工作流實例。

您也可以建立服務的多個設定，以清除滿足不同標準的工作流實例。 例如，建立設定，在特定工作流程模型的執行個體執行時間長於預期時間時清除這些例項。 建立另一個設定，該設定在特定天數後清除所有已完成的工作流程，以將存放庫的大小降至最低。

若要設定服務，您可以使用 [Web主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [將OSGi設定新增至存放庫](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). 下表說明了任何一種方法所需的屬性。

>[!NOTE]
>
>若要將設定新增至存放庫，服務PID為：
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>因為服務是工廠服務，所以 `sling:OsgiConfig` 節點需要標識符尾碼，例如：
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>屬性名稱（Web主控台）</th>
   <th>OSGi屬性名稱</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>工作名稱</td>
   <td>scheduledpurge.name</td>
   <td>排程清除的描述性名稱。</td>
  </tr>
  <tr>
   <td>工作流程狀態</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>要清除的工作流實例的狀態。 下列值有效：</p>
    <ul>
     <li>已完成：已完成的工作流實例將被清除。</li>
     <li>正在運行：正在執行的工作流實例將被清除。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>要清除的模型</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>要清除的工作流模型的ID。 ID是指向模型節點的路徑，例如：<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> 指定不要清除所有工作流模型的實例的值。</p> <p>若要指定多個模型，請按一下Web控制台中的+按鈕。 </p> </td>
  </tr>
  <tr>
   <td>工作流程年齡</td>
   <td>scheduledpurge.daysold</td>
   <td>要清除的工作流實例的年齡（以天為單位）。</td>
  </tr>
 </tbody>
</table>

## 設定收件箱的最大大小 {#setting-the-maximum-size-of-the-inbox}

您可以設定收件匣的最大大小，方法是設定 **AdobeGranite工作流程服務**，使用 [Web主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [將OSGi設定新增至存放庫](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). 下表說明您為任一方法所設定的屬性。

>[!NOTE]
>
>若要將設定新增至存放庫，服務PID為：
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`。

| 屬性名稱（Web主控台） | OSGi屬性名稱 |
|---|---|
| 最大收件箱查詢大小 | granite.workflow.inboxQuerySize |

## 為客戶擁有的資料存放區使用工作流程變數 {#using-workflow-variables-customer-datastore}

由工作流程處理的資料儲存在提供的儲存(JCR)Adobe中。 這些資料在本質上是敏感的。 您可能希望將所有用戶定義的元資料/資料保存在自己的托管儲存中，而不是Adobe提供的儲存中。 以下章節說明如何為外部儲存設定這些變數。

### 將模型設定為使用外部元資料儲存 {#set-model-for-external-storage}

在工作流模型的級別，提供標誌以指示模型（及其運行時實例）具有元資料的外部儲存。 針對標示為外部儲存之模型的工作流程例項，工作流程變數不會保留在JCR中。

屬性 *userMetadataPersistenceEnabled* 將儲存在 *jcr:content節點* 工作流模型。 此標幟會以 *cq:userMetaDataCustomPersistenceEnabled*.

下圖顯示必須在工作流程上設定標幟。

![workflow-externalize-config](assets/workflow-externalize-config.png)

### 外部儲存中中繼資料的API {#apis-for-metadata-external-storage}

若要從外部儲存變數，您必須實作工作流程公開的API。

UserMetaDataPersistenceContext

下列範例會示範如何使用API。

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
} 
```
