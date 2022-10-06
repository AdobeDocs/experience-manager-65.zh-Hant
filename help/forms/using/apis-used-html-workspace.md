---
title: AEM Forms工作區中使用的API
seo-title: APIs used in AEM Forms workspace
description: 公開的Java和JavaScript API與LiveCycleAEM Forms工作區的方法，這些API公開供自訂和自動化使用。
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

# AEM Forms工作區中使用的API {#apis-used-in-aem-forms-workspace}

下列API用於AEM Forms工作區。

<table>
 <tbody>
  <tr>
   <td><strong>Javascript方法</strong></td>
   <td><strong>服務名稱</strong></td>
   <td><strong>API 名稱</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>搜尋群組。 如果未指定，則返回所有組的清單，否則返回具有指定名稱的組。</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>搜尋使用者和群組。 如果未指定，則返回所有用戶和組的清單，否則返回具有指定名稱的用戶和組。</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>在通過DocumentSubmitServlet提交表單之前，將調用它。 它會在實際提交期間擷取的工作階段變數（連同到期時間）中設定任務ID。</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>提交</td>
   <td>它提交與任務關聯的文檔對象（並依次提交進程）。</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>它會擷取伺服器上存在的所有根類別。</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>它會為某個類別擷取所有直接子項。</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>它會擷取所有類別中伺服器上出現的所有起始點。</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>這會調用起始點並建立與起始點對應的新任務</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllPolatedTasks</td>
   <td>它會擷取為登入使用者建立、轉送或諮詢、儲存、指派、指派及儲存的所有工作。</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getTask</td>
   <td>它會擷取特定任務。</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ProcessManagementTaskService</td>
   <td>轉譯</td>
   <td>它會轉譯任務並傳回轉譯表單所需的資訊，例如表單url、表單類型、資料url（如有需要）。</td>
  </tr>
  <tr>
   <td>submitWithPrierData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPrierData</td>
   <td>它使用結果密鑰返回TaskManager提交API的結果。</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>它使用TaskManager的提交API提交與任務關聯的表單資料（以字串形式傳遞）。 它用於不調用TaskManager提交API的Flex表單。</td>
  </tr>
  <tr>
   <td>儲存</td>
   <td>ProcessManagementTaskService</td>
   <td>儲存</td>
   <td>它會在伺服器上儲存任務。</td>
  </tr>
  <tr>
   <td>complete</td>
   <td>ProcessManagementTaskService</td>
   <td>complete</td>
   <td>它完成了一個任務，並根據流程設計將任務傳遞到下一步。</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>它會傳回附件可用的附件URL。</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllPolatedAttachments</td>
   <td>它會擷取任務的所有附件和附註。</td>
  </tr>
  <tr>
   <td>分享</td>
   <td>ProcessManagementTaskService</td>
   <td>分享</td>
   <td>它與其他使用者共用任務。 另一個用戶可以聲明該任務並成為該任務的所有者。</td>
  </tr>
  <tr>
   <td>前進</td>
   <td>ProcessManagementTaskService</td>
   <td>前進</td>
   <td>它將任務轉發給另一個用戶。</td>
  </tr>
  <tr>
   <td>諮詢</td>
   <td>ProcessManagementTaskService</td>
   <td>諮詢</td>
   <td>它會與其他使用者協商任務。</td>
  </tr>
  <tr>
   <td>索賠</td>
   <td>ProcessManagementTaskService</td>
   <td>索賠</td>
   <td>它聲明共用隊列中可用的任務。</td>
  </tr>
  <tr>
   <td>解除鎖定</td>
   <td>ProcessManagementTaskService</td>
   <td>解除鎖定</td>
   <td>它解鎖任務。</td>
  </tr>
  <tr>
   <td>鎖</td>
   <td>ProcessManagementTaskService</td>
   <td>鎖</td>
   <td>它會鎖定任務，而如果共用，則其他用戶無法申請任務。</td>
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
   <td>它會刪除任務。</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>它設定任務的可見性。 如果可見性設為false，則之後使用者將看不到任務。</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>用於搜索用戶。 如果未指定名稱，則會傳回所有使用者，否則會傳回具有指定名稱的使用者。</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>它會傳回群組中的所有使用者。</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>它授予指定使用者對已登入使用者佇列的存取權。 它基本上是與其他使用者共用自己的佇列。</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>它會針對登入的使用者提出指定使用者佇列的存取請求。 如果使用者核准請求，則使用者的佇列會與登入的使用者共用。</td>
  </tr>
  <tr>
   <td>getGratedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGratedUsers</td>
   <td>它會傳回所有有權存取已登入使用者佇列的使用者。</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>它會傳回其佇列可供使用者存取的所有使用者。</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>它會從可存取登入使用者佇列的使用者清單中移除使用者。</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>它會從登入使用者可存取其佇列的使用者清單中移除使用者。</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>它獲得可登錄用戶訪問的所有隊列（擁有、共用和組隊列）。<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>會從使用者的辦公室設定傳出。</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>它會儲存使用者的辦公室設定。</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>它返回所有進程的清單。</td>
  </tr>
  <tr>
   <td>getEppertedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getEppertedProcesses</td>
   <td>它返回由登錄用戶參與的所有進程名的清單。</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>它會擷取處理程式例項的詳細資訊。<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>它會擷取一個程式的所有程式例項。</td>
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
   <td>它會傳回搜尋範本的內容。</td>
  </tr>
  <tr>
   <td>findTasksJson<br /> </td>
   <td>ProcessManagementQueryService</td>
   <td>findTasksJson</td>
   <td>它會搜尋並傳回滿足搜尋範本所有條件的所有任務。</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>它獲取任務的所有分配。 例如： — 如果用戶轉發或咨詢任務給其他用戶，則該任務是任務的分配。</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>TaskManagerService</td>
   <td>deleteAttachment</td>
   <td>它會刪除附件。</td>
  </tr>
  <tr>
   <td>初始化</td>
   <td>ProcessManagementClientSessionService</td>
   <td>初始化</td>
   <td>如果必要，它會重新發表聲明。 驗證用戶。 設定伺服器/客戶端資訊的會話參數。 返回用戶資訊和輪詢間隔。</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>它會傳回登入管理員之直接報表的所有工作。</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>它會傳回已登入管理員指定之直接報表的任務。</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>它會將直接報告的任務轉發給另一個用戶。</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>它會傳回直接報表的任務給先前的使用者。</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>它會取得使用者的Workspace屬性。</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>刪除</td>
   <td>它會移除使用者的Workspace屬性。</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>它會傳回使用者的所有Workspace屬性。</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>它會為使用者設定Workspace屬性。</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>它會取得登入使用者的影像url。</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>它會取得指定使用者的使用者影像url。</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>它會在伺服器上上傳任務的附註。</td>
  </tr>
  <tr>
   <td>uploadRMAToServer（也直接從html範本呼叫）<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>它上載伺服器上的任務附件。</td>
  </tr>
  <tr>
   <td>getImageURL（也直接從html範本呼叫）</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>它會為程式取得影像。</td>
  </tr>
 </tbody>
</table>
