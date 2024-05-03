---
title: AEM Forms工作區JSON物件說明
description: LiveCycleAEM Forms工作區中使用的JSON JavaScript物件的相關概念資訊，用於自訂、擴充功能、修改和重複使用。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
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
   <td>類別ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>五</td>
   <td>類別說明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>五</td>
   <td>包含父類別的OID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointList<br type="_moz" /> </td>
   <td>二</td>
   <td>包含類別中存在的所有起點的清單</td>
  </tr>
  <tr>
   <td>categorylist</td>
   <td>二</td>
   <td>包含類別的直接子類別清單<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>所有「起點」和「我的最愛」都是在使用者端定義的類別。 我的最愛類別包含使用者標示為我的最愛的所有起點。 「所有起點」類別包含所有起點。

1. 起點

   叫用時，可使用起點從工作區啟動程式。

   | **屬性** | **僅限使用者端** | **註解** |
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
   <td>其中包含建立任務時的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>五</td>
   <td>它包含建立任務的使用者ID。<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>五</td>
   <td>它包含有關目前任務指派的詳細資訊。<br /> </td>
  </tr>
  <tr>
   <td>期限<br /> </td>
   <td>五</td>
   <td>其中包含任務即將到達截止日期的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>說明<br /> </td>
   <td>五</td>
   <td>它包含任務的說明。<br /> </td>
  </tr>
  <tr>
   <td>顯示名稱<br /> </td>
   <td>五</td>
   <td>它包含任務的顯示名稱。<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>五</td>
   <td>它包含可轉送任務的群組ID。 它在流程設計期間設定。<br /> </td>
  </tr>
  <tr>
   <td>指示<br /> </td>
   <td>五</td>
   <td>它包含任務的指示。<br /> </td>
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
   <td>如果為true，則開啟任務時，表單會首次採用完整熒幕。<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>五</td>
   <td>如果為true，則必須選取路由以完成任務。<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>五</td>
   <td>如果為true，則會顯示附件。<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>五</td>
   <td>如果為true，則從起點建立任務。<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>五</td>
   <td>如果任務顯示在工作區中，則為True。<br /> </td>
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
   <td>工作所屬之程式執行個體的ID。<br /> </td>
  </tr>
  <tr>
   <td>processinstancestatus<br /> </td>
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
   <td>選定路由<br /> </td>
   <td>五</td>
   <td>它包含任務完成時所選取路由的名稱。<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>五</td>
   <td>它包含與任務對應的影像票證。 此影像票證用於任務的imageUrl欄位中，以從伺服器取得任務的影像。<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>五</td>
   <td>它包含任務的服務名稱。<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>五</td>
   <td>它包含任務的服務標題。<br /> </td>
  </tr>
  <tr>
   <td>狀態<br /> </td>
   <td>五</td>
   <td>1 =已建立（從起點建立任務。）<br /> 2 =建立與儲存（從起始點建立並儲存任務）。<br /> 3 =已指派（任務在流程啟動後指派給使用者。）<br /> 4 =指派並儲存（指派並儲存任務）。<br /> 100 =已完成（任務已完成。）<br /> 101 =已截止（任務已到截止日期）。<br /> 102 =已終止<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>五</td>
   <td>它包含流程設計期間的工作集名稱。<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>五</td>
   <td>它包含任務摘要url。<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>五</td>
   <td>它是任務的存取控制清單。<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>五</td>
   <td>任務的ID。<br /> </td>
  </tr>
  <tr>
   <td>updatetime<br /> </td>
   <td>五</td>
   <td>上次更新任務的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>二</td>
   <td>它包含任務的表單url。<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>二</td>
   <td>它包含任務表單型別。 使用此欄位，任務會在使用者端上呈現為PDF、SWF表單等。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>二</td>
   <td>如果為true，則可在工作區中看到路由動作。<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>二</td>
   <td>如果為true，則工作區中會顯示前進、諮詢、共用等動作。<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>二</td>
   <td>如果為True，則可將表單離線。 這僅適用於pdf表單。<br /> </td>
  </tr>
  <tr>
   <td>supportssave<br /> </td>
   <td>二</td>
   <td>如果為true，則使用者可以儲存任務。<br /> </td>
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
   <td>它包含在任務詳細資訊的歷史記錄標籤中使用的任務清單。<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>二</td>
   <td>如果登入的使用者是任務的擁有者，則為True。<br /> </td>
  </tr>
  <tr>
   <td>availablecommands<br /> </td>
   <td>二</td>
   <td>其中包含可對任務執行的所有動作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>二</td>
   <td>它包含任務可用的所有路由動作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>二</td>
   <td>它包含forward、share和consult等命令（如果可用於任務）。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>二</td>
   <td>它包含鎖定、解鎖、放棄、傳回、宣告等可用命令。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>二</td>
   <td>它包含有關任務的流程例項的資訊。<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>其中包含流程變數的物件陣列（如果有的話）。<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>二</td>
   <td>它包含任務之程式執行個體的擱置任務清單。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>二</td>
   <td>它是物件的陣列。 每個物件都包含有關路由及其對應確認訊息（如果有的話）的詳細資訊。<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>二</td>
   <td>它是任務表單資料的URL。<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>二</td>
   <td>這是協力廠商應用程式表單的設定。<br /> </td>
  </tr>
  <tr>
   <td>已提交<br /> </td>
   <td>二</td>
   <td>如果任務已提交，則為真。<br /> </td>
  </tr>
  <tr>
   <td>附件<br /> </td>
   <td>二</td>
   <td>工作的附件清單。<br /> </td>
  </tr>
  <tr>
   <td>指定任務<br /> </td>
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
   <td>它包含屬於篩選器的所有任務清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 郵件答錄機

   您可以管理您的休假排程，並控制您休假時指派給您的工作流程。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong><br type="_moz" /> </td>
   <td><strong>僅限使用者端</strong><br type="_moz" /> </td>
   <td><strong>註解</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期範圍<br type="_moz" /> </td>
   <td>五</td>
   <td>它包含使用者休假排程的陣列物件。 在每個排程物件中，startDate欄位包含排程的開始日期，而dendDate欄位包含排程的結束日期。 如果排程中的endDate為Null，表示使用者尚未排程休假排程的結束日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesigned<br type="_moz" /> </td>
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
   <td>其中包含使用者指派為主要指定的使用者的詳細資訊。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>五</td>
   <td>它包含專屬於處理序的「不在辦公室」指定的物件陣列。 在每個流程特定的指定物件中，processName包含流程的名稱，如果沒有為對應的流程指派使用者，則isNotDesigned為true，如果沒有為對應的流程指派使用者，則userDesigned為null。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>程式<br type="_moz" /> </td>
   <td>二</td>
   <td>它包含使用者可用的所有程式清單。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>二</td>
   <td>它包含最初擷取之使用者的初始休假設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>二</td>
   <td>它包含已修改的「休假中」設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>二</td>
   <td>它包含由登入使用者在截止日期前搜尋的使用者清單。<br type="_moz" /> </td>
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
   <td>說明<br type="_moz" /> </td>
   <td>五</td>
   <td>程式執行個體的說明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>發起人</td>
   <td>五</td>
   <td>程式執行個體的啟動器名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>五</td>
   <td>處理序執行個體啟動器的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>五</td>
   <td>處理完成時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>五</td>
   <td>程式執行個體的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processinstancestatus<br type="_moz" /> </td>
   <td>五</td>
   <td>0 =已啟動<br /> 1 =執行中<br /> 2 =完成<br /> 3 =完成<br /> 4 =已終止<br /> 5 =終止<br /> 6 =已暫停<br /> 7 =暫停<br /> 8 =取消暫停<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>五</td>
   <td>處理序的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>五</td>
   <td>處理序啟動時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>五</td>
   <td>程式變數的物件陣列。 每個流'b5'7b變數物件都包含名稱，即流'b5'7b變數的名稱、值'b5'7b變數的值以及型別'b5'7b變數的型別。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>工作清單<br type="_moz" /> </td>
   <td>二</td>
   <td>此程式執行個體產生的任務。<br type="_moz" /> </td>
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
   <td>流程的主要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>五</td>
   <td>程式的次要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>五</td>
   <td>處理序的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>五</td>
   <td>流程的標題。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>二</td>
   <td>此流程的流程例項清單。<br type="_moz" /> </td>
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
   <td>建立任務的指派時的時戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmenttype<br type="_moz" /> </td>
   <td>五</td>
   <td>0 =初始指派<br /> 1 =轉寄（任務已轉寄給目前的任務擁有者。）<br /> 2 =已傳回（任務已由任務的先前所有者傳回至任務的目前所有者。）<br /> 3 =已申請（任務已由任務的目前所有者申請）。<br /> 4 =提升（提升後已將任務指派給目前的任務擁有者。）<br /> 5 =管理員已指派（任務已由管理員指派給任務的目前擁有者。）<br /> 6 =已諮詢（已諮詢任務給任務的目前所有者。）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>五</td>
   <td>更新此任務指派時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>五</td>
   <td>任務目前擁有者的佇列識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>五</td>
   <td>任務目前擁有者的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>五</td>
   <td>任務目前擁有者的ID。<br type="_moz" /> </td>
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
   <td>如果為True，則可將附註新增至任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>五</td>
   <td>如果為true，則可申請任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>五</td>
   <td>如果為true，則可參閱任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>五</td>
   <td>如果為true，則可轉送任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>五</td>
   <td>如果為true，則可共用工作。<br type="_moz" /> </td>
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
   <td>說明<br type="_moz" /> </td>
   <td>五</td>
   <td>附件的說明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>檔案名稱<br type="_moz" /> </td>
   <td>五</td>
   <td>附件的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>五</td>
   <td>附件識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>五</td>
   <td>上次修改附件時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>附註擴展<br type="_moz" /> </td>
   <td>五</td>
   <td>如果為true，則附註為延伸（長）附註。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>許可權<br type="_moz" /> </td>
   <td>五</td>
   <td>與附件相關聯的許可權。 allowRead欄位適用於讀取許可權，allowWrite適用於寫入許可權，allowDelete適用於刪除許可權。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>大小<br type="_moz" /> </td>
   <td>五</td>
   <td>附件的大小（位元組）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>五</td>
   <td>要新增附件的任務識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type<br type="_moz" /> </td>
   <td>五</td>
   <td>型別是檔案的附件，型別是註記的註記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>二</td>
   <td>根據使用者的UI設定，其中包含附件建立日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>二</td>
   <td>已格式化的附件說明。 用於顯示AEM Forms工作區附件說明中出現的特殊字元。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>二</td>
   <td>格式化附件名稱。 用於顯示AEM Forms工作區附件名稱中出現的特殊字元。 這僅供附註使用。<br type="_moz" /> </td>
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
   <td>地址<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的位址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的一般名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的說明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMembership<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者群組的清單。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>顯示名稱<br type="_moz" /> </td>
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
   <td>使用者的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的組織名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>郵寄地址<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的郵寄地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>電話<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的聯絡電話。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephoneNumber<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的聯絡電話。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>五</td>
   <td>使用者的登入識別碼。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
