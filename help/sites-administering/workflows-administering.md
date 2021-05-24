---
title: 管理工作流程例項
seo-title: 管理工作流程例項
description: 了解如何管理工作流程例項。
seo-description: 了解如何管理工作流程例項。
uuid: 81e53ef5-fe62-4ed4-b2d4-132aa986d5aa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d9c96e7f-9416-48e1-a6af-47384f7bee92
exl-id: 90923d39-3ac5-4028-976c-d011f0404476
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---

# 管理工作流程例項{#administering-workflow-instances}

工作流程控制台提供數種管理工作流程例項的工具，以確保這些例項可如預期般執行。

>[!NOTE]
>
>[JMX控制台](/help/sites-administering/jmx-console.md#workflow-maintenance)提供其他工作流維護操作。

管理工作流程時可使用多種主控台。 使用[全局導航](/help/sites-authoring/basic-handling.md#global-navigation)開啟&#x200B;**工具**&#x200B;窗格，然後選擇&#x200B;**工作流**:

* **模型**:管理工作流程定義
* **例項**:檢視及管理執行中的工作流程例項
* **啟動器**:管理工作流程的啟動方式
* **封存**:檢視成功完成的工作流程記錄
* **失敗**:檢視已完成但有錯誤的工作流程的歷史記錄

## 監控工作流實例的狀態{#monitoring-the-status-of-workflow-instances}

1. 使用導航選擇&#x200B;**工具**，然後選擇&#x200B;**工作流**。
1. 選擇&#x200B;**實例**&#x200B;以顯示當前正在進行的工作流實例清單。

   ![wf-96](assets/wf-96.png)

1. 選擇特定項目，然後選擇&#x200B;**開啟歷史記錄**&#x200B;以查看更多詳細資訊：

   ![wf-97](assets/wf-97.png)

## 暫停、繼續和終止工作流實例{#suspending-resuming-and-terminating-a-workflow-instance}

1. 使用導航選擇&#x200B;**工具**，然後選擇&#x200B;**工作流**。
1. 選擇&#x200B;**實例**&#x200B;以顯示當前正在進行的工作流實例清單。

   ![wf-96-1](assets/wf-96-1.png)

1. 選擇特定項目，然後根據需要使用&#x200B;**終止**、**掛起**&#x200B;或&#x200B;**恢復**;確認，和/或更多詳細資訊是必要的：

   ![wf-97-1](assets/wf-97-1.png)

## 查看存檔的工作流{#viewing-archived-workflows}

1. 使用導航選擇&#x200B;**工具**，然後選擇&#x200B;**工作流**。
1. 選擇&#x200B;**Archive**&#x200B;以顯示成功完成的工作流實例清單。

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >中止狀態被視為成功終止，因為它是由於用戶操作而發生的；例如：
   >
   >* **終止**&#x200B;操作的使用
   >* 當受工作流約束的頁面被（強制）刪除時，工作流將被終止


1. 選擇特定項目，然後選擇&#x200B;**開啟歷史記錄**&#x200B;以查看更多詳細資訊：

   ![wf-99](assets/wf-99.png)

## 修正工作流實例失敗{#fixing-workflow-instance-failures}

當工作流失敗時，AEM會提供&#x200B;**Failures**&#x200B;控制台，讓您在處理原始原因後調查並採取適當動作：

* **失敗詳**
細資訊開啟一個窗口以顯示 
**失敗訊息**、 **** 步驟 **和失敗堆疊**。

* **開啟**
歷史記錄顯示工作流歷史記錄的詳細資訊。

* **重試** 步驟再次執行指令碼步驟元件實例。修正了原始錯誤的原因後，請使用「重試步驟」命令。 例如，在您修正了「處理步驟」所執行指令碼中的錯誤後，請重試該步驟。
* **** 終止如果錯誤導致工作流的不可協調情況，則終止工作流。例如，工作流可以依賴於環境條件，例如儲存庫中對工作流實例不再有效的資訊。
* **終止和重** 試類似 **** 於終止，只是使用原始裝載、標題和說明啟動了新的工作流實例。

要調查失敗，然後恢復或之後終止工作流，請執行以下步驟：

1. 使用導航選擇&#x200B;**工具**，然後選擇&#x200B;**工作流**。
1. 選擇&#x200B;**Failures**&#x200B;以顯示未成功完成的工作流實例清單。
1. 選擇特定項目，然後選擇相應的操作：

   ![wf-47](assets/wf-47.png)

## 定期清除工作流實例{#regular-purging-of-workflow-instances}

將工作流實例數減到最少會提高工作流引擎的效能，因此您可以定期從儲存庫中清除已完成或正在運行的工作流實例。

配置&#x200B;**AdobeGranite工作流清除配置**&#x200B;以根據其年齡和狀態清除工作流實例。 您也可以清除所有模型或特定模型的工作流實例。

您也可以建立服務的多個設定，以清除滿足不同標準的工作流實例。 例如，建立設定，在特定工作流程模型的執行個體執行時間長於預期時間時清除這些例項。 建立另一個設定，該設定在特定天數後清除所有已完成的工作流程，以將存放庫的大小降至最低。

要配置服務，可以使用[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[將OSGi配置添加到儲存庫](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)。 下表說明了任何一種方法所需的屬性。

>[!NOTE]
>
>若要將設定新增至存放庫，服務PID為：
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>由於服務是工廠服務，`sling:OsgiConfig`節點的名稱需要標識符尾碼，例如：
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
   <td><p>要清除的工作流模型的ID。 ID是模型節點的路徑，例如：<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br />指定不要清除所有工作流模型的實例的值。</p> <p>若要指定多個模型，請按一下Web控制台中的+按鈕。 </p> </td>
  </tr>
  <tr>
   <td>工作流程年齡</td>
   <td>scheduledpurge.daysold</td>
   <td>要清除的工作流實例的年齡（以天為單位）。</td>
  </tr>
 </tbody>
</table>

## 設定收件箱的最大大小{#setting-the-maximum-size-of-the-inbox}

您可以通過配置&#x200B;**AdobeGranite工作流服務**，使用[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[將OSGi配置添加到儲存庫](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)來設定收件箱的最大大小。 下表說明您為任一方法所設定的屬性。

>[!NOTE]
>
>若要將設定新增至存放庫，服務PID為：
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`。

| 屬性名稱（Web主控台） | OSGi屬性名稱 |
|---|---|
| 最大收件箱查詢大小 | granite.workflow.inboxQuerySize |
