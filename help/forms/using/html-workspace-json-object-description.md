---
title: AEM Forms工作區JSON物件說明
description: LiveCycleAEM Forms Workspace中所用JSON JavaScript物件的相關概念資訊，可供自訂、擴充功能、修改和重複使用。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2144'
ht-degree: 8%

---

# AEM Forms工作區JSON物件說明 {#aem-forms-workspace-json-object-description}

AEM Forms工作區中使用的JSON物件說明如下。

1. 類別

   類別會顯示在工作區的啟動流程標籤中。 這些類別是用來分類起點。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>五</td>
   <td>類別名稱</td>
  </tr>
  <tr>
   <td>id</td>
   <td>五</td>
   <td>類別識別碼<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>五</td>
   <td>類別描述<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>五</td>
   <td>包含父類別<br type="_moz" />的OID </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>二</td>
   <td>包含類別中存在的所有起點的清單</td>
  </tr>
  <tr>
   <td>categorylist</td>
   <td>二</td>
   <td>包含類別<br type="_moz" />的直接子類別清單 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>所有「起點」和「我的最愛」都是在使用者端定義的類別。 我的最愛類別包含使用者標示為我的最愛的所有起點。 「所有起點」類別包含所有起點。

1. 起點

   叫用時，可使用起點從工作區啟動程式。

   | **屬性** | **僅使用者端** | **個註解** |
   |---|---|---|
   | categoryId | 五 | 它包含起點所屬類別的ID。 |
   | 說明 | 五 | 它包含起點的描述。 |
   | 名稱 | 五 | 它包含起點的名稱。 |
   | serializedImageTicket | 五 | 它包含與起點對應的影像票證。 此影像票證用於起點的imageUrl欄位中，以從伺服器取得起點的影像。 |
   | serviceName | 五 | 它包含起點的服務名稱。 |
   | startpointId | 五 | 它包含起點ID。 |
   | isFavorite | 二 | 表示起點是否為我的最愛。 如果起點是我的最愛，則為True，否則為False。 |
   | isDefaultImage | 二 | 表示是否為處理指定影像。 如果沒有與處理序相關聯的影像，則為True，否則為false。 |
   | 任務 | 二 | 它包含呼叫起點時所建立的工作。 |
   | imageUrl | 二 | 它包含與起點對應的影像URL。 |

1. 任務

   任務會指派給使用者/群組，並包含使用者介面(表單或指南（已棄用）)，可填入資料。 當使用者被指派任務時，他們將獲得完成和提交的表單或指南。

<table>
 <tbody>
  <tr>
   <td>屬性<br /> </td>
   <td>僅限使用者端<br /> </td>
   <td>註解<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>五</td>
   <td>當任務為lc8任務時，任務類別為「LC8」，否則為「標準」。<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>五</td>
   <td>它包含任務完成時的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>五</td>
   <td>它包含可向其諮詢任務的群組ID。 它在流程設計期間設定。<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>五</td>
   <td>它包含建立任務時的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>五</td>
   <td>它包含建立工作之使用者的識別碼。<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>五</td>
   <td>它包含目前任務指派的詳細資料。<br /> </td>
  </tr>
  <tr>
   <td>期限<br /> </td>
   <td>五</td>
   <td>其中包含任務到達截止日期的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>描述<br /> </td>
   <td>五</td>
   <td>它包含工作的描述。<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>五</td>
   <td>它包含工作的顯示名稱。<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>五</td>
   <td>它包含可轉送任務的群組ID。 它在流程設計期間設定。<br /> </td>
  </tr>
  <tr>
   <td>指示<br /> </td>
   <td>五</td>
   <td>它包含工作的指示。<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>五</td>
   <td>如果工作已鎖定，則為True。<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>五</td>
   <td>如果必須開啟工作表單才能完成工作，則為True。<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>五</td>
   <td>如果為True，則開啟任務時，表單會首次完成熒幕。<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>五</td>
   <td>若為True，則必須選取路由以完成工作。<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>五</td>
   <td>如果為True，則會顯示附件。<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>五</td>
   <td>若為True，則會從起始點建立任務。<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>五</td>
   <td>如果工作顯示在工作區中，則為True。<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>五</td>
   <td>下一個提醒的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>優先順序<br /> </td>
   <td>五</td>
   <td>它包含任務的優先順序。<br /> 1 =最高優先順序<br /> 2 =高優先順序<br /> 3 =一般優先順序<br /> 4 =低優先順序<br /> 5 =最低優先順序<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>五</td>
   <td>工作所屬之處理序執行個體的識別碼。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>五</td>
   <td>任務的程式執行個體的狀態。<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>五</td>
   <td>它包含任務的提醒計數。<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>五</td>
   <td>它包含與任務關聯的路由清單。 使用者可以從路由清單中選取任一路由，以完成此工作。<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>五</td>
   <td>它包含任務完成時所選取路由的名稱。<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>五</td>
   <td>它包含與任務對應的影像票證。 此影像票證用於任務的imageUrl欄位中，以從伺服器取得任務的影像。<br /> <br /> </td>
  </tr>
  <tr>
   <td>服務名稱<br /> </td>
   <td>五</td>
   <td>它包含工作的服務名稱。<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>五</td>
   <td>它包含工作的服務標題。<br /> </td>
  </tr>
  <tr>
   <td>狀態<br /> </td>
   <td>五</td>
   <td>1 =已建立（從起點建立任務。）<br /> 2 =建立並儲存（從起點建立並儲存任務）。<br /> 3 =已指派（任務在處理序啟動後指派給使用者。）<br /> 4 =指派並儲存（已指派並儲存任務）。<br /> 100 =已完成（工作已完成。）<br /> 101 =已逾期（任務已到期限）。<br /> 102 =已終止<br /> </td>
  </tr>
  <tr>
   <td>步驟名稱<br /> </td>
   <td>五</td>
   <td>它包含處理序設計期間的工作集名稱。<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>五</td>
   <td>它包含任務摘要URL。<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>五</td>
   <td>它是工作的存取控制清單。<br /> </td>
  </tr>
  <tr>
   <td>任務識別碼<br /> </td>
   <td>五</td>
   <td>工作的識別碼。<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>五</td>
   <td>上次更新任務時的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>二</td>
   <td>它包含任務的表單URL。<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>二</td>
   <td>它包含任務表單型別。 使用此欄位，工作會在使用者端上呈現為PDF、SWF表單等。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>二</td>
   <td>如果為True，則可在工作區中看到路由動作。<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>二</td>
   <td>若為True，工作區中會顯示向前、諮詢、共用等動作。<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>二</td>
   <td>如果為True，則可將表單離線。 這僅適用於pdf表單。<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>二</td>
   <td>若為True，則使用者可儲存工作。<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>二</td>
   <td>此物件包含用於透過Reader提交PDF表單的選項，以防PDF表單不包含提交按鈕。<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>二</td>
   <td>表示是否為處理指定影像。 如果沒有與處理序相關聯的影像，則為True，否則為false。<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>二</td>
   <td>它包含用於任務詳細資訊歷史記錄標籤中的任務清單。<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>二</td>
   <td>如果登入使用者是任務的擁有者，則為True。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>二</td>
   <td>它包含可以對任務執行的所有動作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>二</td>
   <td>它包含可用於任務的所有路由動作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>二</td>
   <td>它包含forward、share和consult等命令（若可用於工作）。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>二</td>
   <td>它包含lock、unlock、absout、return、claim等可用命令。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>二</td>
   <td>它包含有關工作的程式執行個體的資訊。<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>它包含處理序變數的物件陣列（如果有的話）。<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>二</td>
   <td>它包含任務之程式執行個體的擱置任務清單。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>二</td>
   <td>它是物件的陣列。 每個物件都包含路由及其對應確認訊息（如果有的話）的詳細資料。<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>二</td>
   <td>它是工作表單資料的URL。<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>二</td>
   <td>這是協力廠商應用程式表單的組態。<br /> </td>
  </tr>
  <tr>
   <td>已提交<br /> </td>
   <td>二</td>
   <td>如果任務已提交，則為True。<br /> </td>
  </tr>
  <tr>
   <td>附件<br /> </td>
   <td>二</td>
   <td>工作的附件清單。<br /> </td>
  </tr>
  <tr>
   <td>指派<br /> </td>
   <td>二</td>
   <td>任務的指派清單。<br /> </td>
  </tr>
 </tbody>
</table>

1. 篩選條件

   篩選器基本上是使用者或群組的佇列。 當任務指派給使用者/群組時，任務會新增到對應的佇列中。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>五</td>
   <td>如果佇列是登入使用者的預設佇列，則為True，否則為false。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>名稱<br type="_moz" /> </td>
   <td>五</td>
   <td>佇列擁有者的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>五</td>
   <td>佇列的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>類型</td>
   <td>五</td>
   <td>它包含佇列的型別。<br /> 0 — 使用者佇列。<br /> 1. 共用佇列。<br /> 2. 群組佇列。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>二</td>
   <td>這包含與篩選器關聯的查詢。 此查詢用於從完整工作清單中搜尋工作。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任務</td>
   <td>二</td>
   <td>它包含屬於篩選器的所有工作清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 郵件答錄機

   您可以管理您的休假排程，並控制您休假時指派給您的工作流程。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong><br type="_moz" /> </td>
   <td><strong>僅使用者端</strong><br type="_moz" /> </td>
   <td><strong>個註解</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期範圍<br type="_moz" /> </td>
   <td>五</td>
   <td>它包含使用者休假排程的陣列物件。 在每個排程物件中，startDate欄位包含排程的開始日期，而dendDate欄位包含排程的結束日期。 如果排程中的endDate為Null，表示使用者尚未排定休假排程的結束日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>五</td>
   <td>如果使用者不在辦公室時沒有主要指定，則為True。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>五</td>
   <td>如果使用者不在辦公室，則為True。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>五</td>
   <td>它包含被使用者指派為主要指定的使用者的詳細資訊。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>五</td>
   <td>它包含專屬於處理序的「不在辦公室」指定的物件陣列。 在每個流程特定指定物件中，processName包含流程的名稱，如果沒有指派使用者給對應的流程，則isNotDesigned為true，如果沒有指派使用者給對應的流程，則userDesigned為null。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>處理程式<br type="_moz" /> </td>
   <td>二</td>
   <td>它包含使用者可用的所有處理序清單。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>二</td>
   <td>它包含最初擷取之使用者的初始郵件答錄機設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>二</td>
   <td>它包含修改過的外出設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>二</td>
   <td>它包含由登入使用者搜尋的使用者清單，直到日期為止。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 程式執行個體

   當透過工作區或Workbench叫用流程時，會建立流程例項。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>五</td>
   <td>處理程式執行個體<br type="_moz" />的說明 </td>
  </tr>
  <tr>
   <td>發起人</td>
   <td>五</td>
   <td>處理程式執行個體的啟動器名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>五</td>
   <td>處理程式執行個體的啟動器識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>五</td>
   <td>處理序完成時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>五</td>
   <td>處理程式執行個體的識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>五</td>
   <td>0 =已起始<br /> 1 =正在執行<br /> 2 =完成<br /> 3 =正在完成<br /> 4 =已終止<br /> 5 =正在終止<br /> 6 =已暫停<br /> 7 =正在暫停<br /> 8 =正在取消暫停<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>五</td>
   <td>處理序的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>五</td>
   <td>處理程式啟動時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>五</td>
   <td>程式變數的物件陣列。 每個程式變數物件都包含名稱（即程式變數的名稱）、值（即程式變數的值）和型別（即程式變數的型別）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>工作清單<br type="_moz" /> </td>
   <td>二</td>
   <td>此處理序執行個體產生的工作。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 處理名稱

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>五</td>
   <td>處理程式的主要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>五</td>
   <td>處理序的次要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>五</td>
   <td>處理序的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>五</td>
   <td>處理序的標題。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>二</td>
   <td>此處理序的處理序執行個體清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任務指派物件

   任務指派物件包含有關任務指派的資訊。 以下是任務指派的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>五</td>
   <td>建立此任務指派時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>五</td>
   <td>0 =初始工作分派<br /> 1 =轉寄（任務已轉寄給目前的任務擁有者。）<br /> 2 =已傳回（任務已由任務的先前擁有者傳回至任務的目前擁有者。）<br /> 3 =已申請（任務已由任務的目前所有者申請）。<br /> 4 =提升（提升後任務已指派給目前的任務所有者）。<br /> 5 =已指派管理員（任務已由管理員指派給任務的目前所有者）。<br /> 6 =已諮詢（已諮詢任務給目前的任務所有者。）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>五</td>
   <td>更新此任務指派時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>五</td>
   <td>工作目前擁有者的佇列識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>五</td>
   <td>工作的目前擁有者名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>五</td>
   <td>工作目前擁有者的識別碼。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 工作ACL物件

   任務ACL物件包含任務的轉送、共用、諮詢等許可權相關資訊。 以下是工作ACL的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>五</td>
   <td>若為True，則可將附件新增至工作。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>五</td>
   <td>若為True，便可將備註新增至工作。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>五</td>
   <td>若為True，則可宣告工作。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>五</td>
   <td>若為True，則可查閱任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>五</td>
   <td>若為True，則可轉送工作。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>五</td>
   <td>若為True，則可共用工作。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 工作附件

   附件可新增至任務。 附件可以是附件和附註型別。 以下是附件物件的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>五</td>
   <td>建立附件時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>五</td>
   <td>新增附件的使用者識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>五</td>
   <td>新增附件的使用者名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>五</td>
   <td>附件的描述。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>檔案名稱<br type="_moz" /> </td>
   <td>五</td>
   <td>附件的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>識別碼<br type="_moz" /> </td>
   <td>五</td>
   <td>附件識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>五</td>
   <td>上次修改附件時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>五</td>
   <td>若為True，則附註為延伸（長）附註。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>許可權<br type="_moz" /> </td>
   <td>五</td>
   <td>與附件相關聯的許可權。 allowRead欄位用於讀取許可權，allowWrite用於寫入許可權，allowDelete用於刪除許可權。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>大小<br type="_moz" /> </td>
   <td>五</td>
   <td>附件大小（位元組）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任務識別碼<br type="_moz" /> </td>
   <td>五</td>
   <td>要新增附件的工作識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>型別<br type="_moz" /> </td>
   <td>五</td>
   <td>型別是檔案的附件，型別是備註的備註。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>二</td>
   <td>根據使用者的UI設定，它包含附件建立日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>二</td>
   <td>已格式化的附件說明。 用於顯示AEM Forms工作區附件說明中出現的特殊字元。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>二</td>
   <td>格式化附件名稱。 用於顯示AEM Forms工作區附件名稱中出現的特殊字元。 這僅供筆記使用。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 使用者

   以下是使用者物件的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>位址<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的位址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的通用名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的描述。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者群組的清單。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的顯示名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>電子郵件<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的電子郵件識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>五</td>
   <td>如果使用者不在辦公室，則為True。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>姓氏<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的姓氏。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>名字<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的名字。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>組織<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的組織名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的郵寄地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>電話<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的連絡電話。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephoneNumber<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的連絡電話。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>使用者ID<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的登入識別碼。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
