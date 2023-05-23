---
title: 在AEM Forms工作區中使用的API
seo-title: APIs used in AEM Forms workspace
description: 公用Java和JavaScript API和LiveCycleAEM Forms工作區的方法，這些方法公開用於自定義和自動化。
seo-description: Public Java and JavaScript APIs and methods of LiveCycle AEM Forms workspace, exposed for customization and automation.
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
exl-id: 9034f73a-83f3-498e-b6a6-ad6577aa1a3a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 1%

---

# 在AEM Forms工作區中使用的API {#apis-used-in-aem-forms-workspace}

以下API用於AEM Forms工作區。

<table>
 <tbody>
  <tr>
   <td><strong>Javascript方法</strong></td>
   <td><strong>服務名稱</strong></td>
   <td><strong>API 名稱</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>get組</td>
   <td>ProcessManagementUserProxyService</td>
   <td>get組</td>
   <td>搜索組。 如果未指定，則返回所有組的清單，否則返回具有指定名稱的組。</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>搜索用戶和組。 它返回所有用戶和組的清單（如果未指定），否則返回具有指定名稱的用戶和組。</td>
  </tr>
  <tr>
   <td>準備提交</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>準備提交</td>
   <td>在通過DocumentSubmitServlet提交表單之前調用它。 它設定在實際提交期間檢索的會話變數（連同到期時間）中的任務ID。</td>
  </tr>
  <tr>
   <td>提交任務</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>提交</td>
   <td>它提交與任務關聯的文檔對象（並依次提交流程）。</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>它讀取伺服器上存在的所有根類別。</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>它為類別提取所有直接子級。</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>它讀取所有類別下伺服器上的所有起始點。</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>此操作將調用起始點並建立與起始點對應的新任務</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllAppolitableTask</td>
   <td>它讀取建立並轉發或咨詢、保存、分配、分配和保存給登錄用戶的所有任務。</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getTask</td>
   <td>它讀取特定任務。</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ProcessManagementTaskService</td>
   <td>呈現</td>
   <td>它會呈現任務並返回呈現表單所需的資訊，如表單url、表單類型、資料url（如果需要）等。</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPriorData</td>
   <td>它使用結果鍵返回TaskManager的提交API的結果。</td>
  </tr>
  <tr>
   <td>提交WithData</td>
   <td>ProcessManagementTaskService</td>
   <td>提交WithData</td>
   <td>它使用TaskManager的提交API提交與任務關聯的表單資料（以字串形式傳遞）。 它用於不調用TaskManager的提交API的flex表單。</td>
  </tr>
  <tr>
   <td>保存</td>
   <td>ProcessManagementTaskService</td>
   <td>保存</td>
   <td>它在伺服器上保存任務。</td>
  </tr>
  <tr>
   <td>完整</td>
   <td>ProcessManagementTaskService</td>
   <td>完整</td>
   <td>它完成一個任務，並根據流程設計將任務傳遞到下一步。</td>
  </tr>
  <tr>
   <td>get附件</td>
   <td>ProcessManagementTaskService</td>
   <td>get附件</td>
   <td>它返回附件可用的附件的url。</td>
  </tr>
  <tr>
   <td>getAll附件</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllPuactibleAttachments</td>
   <td>它可讀取任務的所有附件和注釋。</td>
  </tr>
  <tr>
   <td>股份</td>
   <td>ProcessManagementTaskService</td>
   <td>股份</td>
   <td>它與其他用戶共用一個任務。 另一個用戶可以聲明該任務並成為該任務的所有者。</td>
  </tr>
  <tr>
   <td>前進</td>
   <td>ProcessManagementTaskService</td>
   <td>前進</td>
   <td>它將任務轉發給其他用戶。</td>
  </tr>
  <tr>
   <td>咨詢</td>
   <td>ProcessManagementTaskService</td>
   <td>咨詢</td>
   <td>它將咨詢另一個用戶的任務。</td>
  </tr>
  <tr>
   <td>索賠</td>
   <td>ProcessManagementTaskService</td>
   <td>索賠</td>
   <td>它聲明共用隊列中的任務可用。</td>
  </tr>
  <tr>
   <td>解鎖</td>
   <td>ProcessManagementTaskService</td>
   <td>解鎖</td>
   <td>它解鎖任務。</td>
  </tr>
  <tr>
   <td>鎖</td>
   <td>ProcessManagementTaskService</td>
   <td>鎖</td>
   <td>它鎖定任務，如果共用，則其他用戶無法聲明該任務。</td>
  </tr>
  <tr>
   <td>拒絕</td>
   <td>ProcessManagementTaskService</td>
   <td>拒絕</td>
   <td>它將任務返回給任務的前一個所有者。</td>
  </tr>
  <tr>
   <td>放棄</td>
   <td>ProcessManagementTaskService</td>
   <td>放棄</td>
   <td>它刪除任務。</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>它設定任務的可見性。 如果可見性設定為false，則用戶以後將看不到任務。</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>它用於搜索用戶。 如果未指定名稱，則返回所有用戶，否則返回具有指定名稱的用戶。</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>它返回組中的所有用戶。</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>它授予指定用戶對已登錄用戶隊列的訪問權限。 它基本上是與另一個用戶共用自己的隊列。</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>它對已登錄用戶的指定用戶的隊列發出訪問請求。 如果用戶批准該請求，則用戶的隊列將與登錄的用戶共用。</td>
  </tr>
  <tr>
   <td>getGragedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGragedUsers</td>
   <td>它返回有權訪問已登錄用戶隊列的所有用戶。</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>它返回用戶可訪問其隊列的所有用戶。</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>它從有權訪問已登錄用戶隊列的用戶清單中刪除用戶。</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>它從登錄用戶可訪問其隊列的用戶清單中刪除用戶。</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>它獲取登錄用戶可訪問的所有隊列（擁有、共用和組隊列）。<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>它從用戶的辦公室設定中取出。</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>它將用戶的辦公室設定保存在外。</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>它返回所有進程的清單。</td>
  </tr>
  <tr>
   <td>getContertedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getContertedProcesses</td>
   <td>它返回登錄用戶參與的所有進程名稱的清單。</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>它讀取進程實例的詳細資訊。<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>它為進程提取所有進程實例。</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>它獲取進程實例的掛起任務。</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>它獲取進程實例的所有任務。</td>
  </tr>
  <tr>
   <td>getAllSearchTemplates</td>
   <td>ProcessManagementQueryService</td>
   <td>getAllSearchTemplates</td>
   <td>它返回所有搜索模板的清單。</td>
  </tr>
  <tr>
   <td>getTemplate</td>
   <td>ProcessManagementQueryService</td>
   <td>getTemplate</td>
   <td>它返回搜索模板的內容。</td>
  </tr>
  <tr>
   <td>findTasksJson<br /> </td>
   <td>ProcessManagementQueryService</td>
   <td>findTasksJson</td>
   <td>它搜索並返回滿足搜索模板所有條件的所有任務。</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>它獲取任務的所有分配。 例如： — 如果用戶轉發或咨詢另一個用戶的任務，則它是任務的分配。</td>
  </tr>
  <tr>
   <td>刪除附件 </td>
   <td>TaskManager服務</td>
   <td>刪除附件</td>
   <td>它刪除附件。</td>
  </tr>
  <tr>
   <td>初始化</td>
   <td>ProcessManagementClientSessionService</td>
   <td>初始化</td>
   <td>如有必要，它會重新宣佈。 驗證用戶。 設定伺服器/客戶端資訊的會話參數。 返回用戶資訊和輪詢間隔。</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>它返回登錄管理器的直接報告的所有任務。</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>它返回已登錄管理器的指定直接報告的任務。</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>它將直接報告的任務轉發給其他用戶。</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>它將直接報告的任務返回給前一個用戶。</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>它獲取用戶的Workspace屬性。</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>刪除</td>
   <td>它將刪除用戶的Workspace屬性。</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>它返回用戶的所有Workspace屬性。</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>它為用戶設定Workspace屬性。</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>它獲取登錄用戶的用戶影像URL。</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>它獲取指定用戶的用戶影像URL。</td>
  </tr>
  <tr>
   <td>上載附註</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>上載附註</td>
   <td>它會在伺服器上上載任務的注釋。</td>
  </tr>
  <tr>
   <td>uploadRMAToServer（也直接從html模板調用）<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>上載附件</td>
   <td>它會在伺服器上上載任務的附件。</td>
  </tr>
  <tr>
   <td>getImageURL（也直接從html模板調用）</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>它獲取進程的影像。</td>
  </tr>
 </tbody>
</table>
