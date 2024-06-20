---
title: 用於AEM Forms工作區的API
description: 公用Java&Trade；和JavaScript API以及LiveCycleAEM Forms工作區的方法，公開用於自訂和自動化。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 9034f73a-83f3-498e-b6a6-ad6577aa1a3a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms, Adaptive Forms
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---

# 用於AEM Forms工作區的API {#apis-used-in-aem-forms-workspace}

下列API用於AEM Forms工作區。

<table>
 <tbody>
  <tr>
   <td><strong>JavaScript方法</strong></td>
   <td><strong>服務名稱</strong></td>
   <td><strong>API 名稱</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>搜尋群組。 如果未指定任何專案，則會傳回所有群組的清單，否則會傳回指定名稱的群組。</td>
  </tr>
  <tr>
   <td>getUsersAndGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroup</td>
   <td>搜尋使用者和群組。 如果未指定任何專案，則會傳回所有使用者和群組的清單，否則會傳回具有指定名稱的使用者和群組。</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>在透過DocumentSubmitServlet提交表單之前呼叫它。 它會在工作階段變數中設定任務ID （連同到期時間），實際提交期間會擷取該變數。</td>
  </tr>
  <tr>
   <td>submittask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>提交</td>
   <td>它會提交與任務相關聯的檔案物件（並依次提交流程）。</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>它會擷取伺服器上存在的所有根類別。</td>
  </tr>
  <tr>
   <td>getdirectchildcategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getdirectchildcategories2</td>
   <td>它會擷取某個類別的所有直接子項。</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>它會擷取伺服器上所有類別下的所有起點。</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>這會叫用起點，並建立與起點對應的任務</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableTasks</td>
   <td>它會擷取為登入使用者建立和轉送或諮詢、儲存、指派、指派和儲存的所有任務。</td>
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
   <td>它會轉譯工作並傳迴轉譯表單所需的資訊，例如表單URL、表單型別、資料URL （如有需要）。</td>
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
   <td>它會使用TaskManager的提交API來提交與工作相關聯的表單資料（以字串形式傳遞）。 它用於不呼叫TaskManager的提交API的Flex表單。</td>
  </tr>
  <tr>
   <td>儲存</td>
   <td>ProcessManagementTaskService</td>
   <td>儲存</td>
   <td>這會將工作儲存在伺服器上。</td>
  </tr>
  <tr>
   <td>complete</td>
   <td>ProcessManagementTaskService</td>
   <td>complete</td>
   <td>它會完成一項任務，然後按照流程設計將該任務傳遞到下一個步驟。</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>它會傳回可用附件的附件URL。</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableAttachments</td>
   <td>它會擷取任務的所有附件和附註。</td>
  </tr>
  <tr>
   <td>共用</td>
   <td>ProcessManagementTaskService</td>
   <td>共用</td>
   <td>它與其他使用者共用一個任務。 另一位使用者可以宣告該任務並成為該任務的所有者。</td>
  </tr>
  <tr>
   <td>前進</td>
   <td>ProcessManagementTaskService</td>
   <td>前進</td>
   <td>它會轉送工作給其他使用者。</td>
  </tr>
  <tr>
   <td>consult</td>
   <td>ProcessManagementTaskService</td>
   <td>consult</td>
   <td>它會向其他使用者諮詢任務。</td>
  </tr>
  <tr>
   <td>索賠</td>
   <td>ProcessManagementTaskService</td>
   <td>索賠</td>
   <td>它會宣告共用佇列中可用的工作。</td>
  </tr>
  <tr>
   <td>解除鎖定</td>
   <td>ProcessManagementTaskService</td>
   <td>解除鎖定</td>
   <td>它會解除鎖定任務。</td>
  </tr>
  <tr>
   <td>鎖定</td>
   <td>ProcessManagementTaskService</td>
   <td>鎖定</td>
   <td>它會鎖定任務，而且如果共用，其他使用者將無法要求該任務。</td>
  </tr>
  <tr>
   <td>拒絕</td>
   <td>ProcessManagementTaskService</td>
   <td>拒絕</td>
   <td>它會傳回一個任務給該任務的先前擁有者。</td>
  </tr>
  <tr>
   <td>捨棄</td>
   <td>ProcessManagementTaskService</td>
   <td>捨棄</td>
   <td>它會刪除任務。</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>它會設定任務的可見度。 如果可見性設定為false，則使用者之後不會看到任務。</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>它可用來搜尋使用者。 若未指定名稱，則會傳回所有使用者，否則會傳回指定名稱的使用者。</td>
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
   <td>它會授予指定使用者對登入使用者佇列的存取權。 基本上就是和其他使用者共用您自己的佇列。</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>它會向登入使用者的指定使用者佇列發出存取要求。 如果使用者核准請求，則會與登入使用者共用使用者的佇列。</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>它會傳回對登入使用者之佇列具有存取權的所有使用者。</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>它會傳回使用者可存取佇列的所有使用者。</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>它會從擁有登入使用者佇列存取許可權的使用者清單中移除使用者。</td>
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
   <td>它可取得登入使用者可存取的所有佇列（擁有、共用和群組佇列）。<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>它可取得使用者的休假設定。</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>這可儲存使用者的休假設定。</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>它會傳回所有流程的清單。</td>
  </tr>
  <tr>
   <td>getInteractivedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getInteractivedProcesses</td>
   <td>它會傳回由登入使用者參與的所有流程名稱清單。</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>它會擷取程式執行個體的詳細資訊。<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>它會擷取流程的所有流程例項。</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>它取得處理序執行個體的擱置中任務。</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>它會取得流程執行個體的所有任務。</td>
  </tr>
  <tr>
   <td>getAllSearchTemplates</td>
   <td>ProcessManagementQueryService</td>
   <td>getAllSearchTemplates</td>
   <td>它會傳回所有搜尋範本的清單。</td>
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
   <td>它會取得任務的所有指派。 例如，如果使用者轉送或諮詢另一個使用者的任務，則它是任務的指派。</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>工作管理員服務</td>
   <td>deleteAttachment</td>
   <td>它會刪除附件。</td>
  </tr>
  <tr>
   <td>初始化</td>
   <td>ProcessManagementClientSessionService</td>
   <td>初始化</td>
   <td>如有必要，它會更新判斷提示。 驗證使用者。 設定伺服器/使用者端資訊的工作階段引數。 傳回使用者資訊和輪詢間隔。</td>
  </tr>
  <tr>
   <td>getTasksForDirectreports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectreports</td>
   <td>它會傳回登入管理員直接下屬的所有任務。</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>它會傳回登入管理員的指定直接下屬任務。</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>它將直接報告的任務轉送給另一個使用者。</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>它會傳回直接報告的任務給前一個使用者。</td>
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
   <td>setproperty</td>
   <td>WorkspacePropertyService</td>
   <td>setproperty</td>
   <td>它會設定使用者的Workspace屬性。</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>它會取得登入使用者的使用者影像URL。</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>它會取得指定之使用者的影像URL。</td>
  </tr>
  <tr>
   <td>uploadnote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadnote</td>
   <td>它會為一項任務在伺服器上傳附註。</td>
  </tr>
  <tr>
   <td>uploadRMAToServer （也可以直接從html範本呼叫）<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>它會為一項任務上傳伺服器上的附件。</td>
  </tr>
  <tr>
   <td>getImageURL (也直接從HTML範本呼叫)</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>它會取得處理程式的影像。</td>
  </tr>
 </tbody>
</table>
