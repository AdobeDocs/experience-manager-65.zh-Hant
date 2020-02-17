---
title: AEM Forms工作區中使用的API
seo-title: AEM Forms工作區中使用的API
description: LiveCycle AEM Forms工作區的公用Java和JavaScript API和方法，公開供自訂和自動化使用。
seo-description: LiveCycle AEM Forms工作區的公用Java和JavaScript API和方法，公開供自訂和自動化使用。
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Forms工作區中使用的API {#apis-used-in-aem-forms-workspace}

AEM Forms工作區中會使用下列API。

<table>
 <tbody>
  <tr>
   <td><strong>Javascript方法</strong></td>
   <td><strong>服務名稱</strong></td>
   <td><strong>API名稱</strong></td>
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
   <td>在透過DocumentSubmitServlet提交表單之前，會先呼叫它。 它會在實際提交期間擷取的作業變數（連同到期時間）中設定工作ID。</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>提交</td>
   <td>它提交與任務相關聯的文檔對象（並依次提交流程）。</td>
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
   <td>它為類別提取所有直接子代。</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>它讀取所有類別下伺服器上的所有起點。</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>這會叫用「起點」，並建立對應於「起點」的新工作</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllCoptableTasks</td>
   <td>它讀取為登錄用戶建立和轉發或咨詢、保存、分配、分配和保存的所有任務。</td>
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
   <td>渲染</td>
   <td>它會轉譯工作並傳回轉譯表單所需的資訊，例如表單URL、表單類型、資料URL等。</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPriorData</td>
   <td>它會使用結果金鑰傳回TaskManager提交API的結果。</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>它使用TaskManager的提交API提交與任務關聯的表單資料（作為字串傳遞）。 它用於不呼叫TaskManager送出API的flex表單。</td>
  </tr>
  <tr>
   <td>儲存</td>
   <td>ProcessManagementTaskService</td>
   <td>儲存</td>
   <td>它將任務保存在伺服器上。</td>
  </tr>
  <tr>
   <td>完整</td>
   <td>ProcessManagementTaskService</td>
   <td>完整</td>
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
   <td>getAllPocaptableAttachments</td>
   <td>它會為任務提取所有附件和注釋。</td>
  </tr>
  <tr>
   <td>分享</td>
   <td>ProcessManagementTaskService</td>
   <td>分享</td>
   <td>它與另一個用戶共用任務。 另一個用戶可以聲明該任務，並成為該任務的所有者。</td>
  </tr>
  <tr>
   <td>前進</td>
   <td>ProcessManagementTaskService</td>
   <td>前進</td>
   <td>它將任務轉發給另一個用戶。</td>
  </tr>
  <tr>
   <td>consult</td>
   <td>ProcessManagementTaskService</td>
   <td>consult</td>
   <td>它會與另一個用戶協商任務。</td>
  </tr>
  <tr>
   <td>索賠</td>
   <td>ProcessManagementTaskService</td>
   <td>索賠</td>
   <td>它聲明共用隊列中有一個可用任務。</td>
  </tr>
  <tr>
   <td>解鎖</td>
   <td>ProcessManagementTaskService</td>
   <td>解鎖</td>
   <td>它可以解鎖任務。</td>
  </tr>
  <tr>
   <td>鎖</td>
   <td>ProcessManagementTaskService</td>
   <td>鎖</td>
   <td>它鎖定任務，如果共用，則其他用戶無法聲明任務。</td>
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
   <td>它設定任務的可見性。 如果可見度設為false，則使用者將不會在之後看到任務。</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>用於搜索用戶。 如果未指定名稱，則返回所有用戶，否則返回具有指定名稱的用戶。</td>
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
   <td>它將登錄用戶隊列的訪問權限授予指定用戶。 它基本上是與其他使用者共用自己的佇列。</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>它對登錄用戶的指定用戶的隊列發出訪問請求。 如果使用者核准請求，則使用者的佇列會與登入的使用者共用。</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
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
   <td>它會從有權存取已登入使用者佇列的使用者清單中移除使用者。</td>
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
   <td>它可獲得登錄用戶可訪問的所有隊列（擁有、共用和組隊列）。<br /> </td>
  </tr>
  <tr>
   <td>getOutOfficeSettings</td>
   <td>ProcessManagementOutOfficeService</td>
   <td>getOutOfficeSettings</td>
   <td>它會從使用者的辦公室設定中移除。</td>
  </tr>
  <tr>
   <td>saveOutOfficeSettingsJson</td>
   <td>ProcessManagementOutOfficeService</td>
   <td>saveOutOfficeSettingsJson</td>
   <td>它會將使用者的辦公室設定儲存在外。</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>它返回所有進程的清單。</td>
  </tr>
  <tr>
   <td>getEnterpetedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getEnterpetedProcesses</td>
   <td>它返回由登錄用戶參與的所有進程名的清單。</td>
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
   <td>它讀取進程的所有進程實例。</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>它獲取進程實例的暫掛任務。</td>
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
   <td>它搜索並返回滿足搜索模板所有條件的所有任務。</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>它獲取任務的所有分配。 例如：-如果用戶轉發任務或咨詢其他用戶的任務，則它是任務的分配。</td>
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
   <td>如有必要，這會重新宣佈。 驗證使用者。 設定伺服器／客戶機資訊的會話參數。 傳回使用者資訊和輪詢間隔。</td>
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
   <td>它會將直接報告的任務轉發給另一個用戶。</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>它會將直接報表的工作傳回給先前的使用者。</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>它取得使用者的「工作區」屬性。</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>刪除</td>
   <td>它會移除使用者的「工作區」屬性。</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>它會傳回使用者的所有工作區屬性。</td>
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
   <td>它取得登入使用者的使用者影像URL。</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>它會取得指定使用者的使用者影像URL。</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>它會在伺服器上上傳工作的附註。</td>
  </tr>
  <tr>
   <td>uploadRMAToServer（也直接從html範本呼叫）<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>它在伺服器上為任務上載一個附件。</td>
  </tr>
  <tr>
   <td>getImageURL（也直接從html範本呼叫）</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>它可為流程取得影像。</td>
  </tr>
 </tbody>
</table>

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)

