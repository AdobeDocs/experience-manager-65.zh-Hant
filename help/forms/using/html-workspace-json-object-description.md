---
title: AEM Forms工作區JSON物件說明
seo-title: AEM Forms工作區JSON物件說明
description: LiveCycle AEM Forms工作區中用於自訂、擴充、修改及重複使用之JSON javaScript物件的概念性資訊。
seo-description: LiveCycle AEM Forms工作區中用於自訂、擴充、修改及重複使用之JSON javaScript物件的概念性資訊。
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Forms工作區JSON物件說明 {#aem-forms-workspace-json-object-description}

AEM Forms工作區中使用的JSON物件說明如下。

1. 類別

   類別會出現在工作區的開始程式標籤中。 這些類別可用來分類起點。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限用戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>F</td>
   <td>類別名稱</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>類別ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>F</td>
   <td>類別說明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>包含父類別的oid<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>包含類別中所有起點的清單</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>包含類別的直接子類別清單<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>所有「起點」和「我的最愛」都是在用戶端定義的類別。 「我的最愛」類別包含使用者標示為我的最愛的所有起點。 「所有起點」類別包含所有起點。

1. 起點

   起點用於在調用時從工作區啟動進程。

   | **屬性** | **僅限用戶端** | **評論** |
   |---|---|---|
   | categoryId | F | 它包含起點所屬的類別的ID。 |
   | 說明 | F | 它包含起點的說明。 |
   | 名稱 | F | 它包含起點的名稱。 |
   | serializedImageTicket | F | 它包含與起點對應的影像票證。 此影像票證用於起始點的imageUrl欄位，以從伺服器取得起始點的影像。 |
   | serviceName | F | 它包含起點服務的名稱。 |
   | startpointId | F | 它包含起始點的ID。 |
   | isFavorite | T | 表示起點是否為收藏點。 如果startpoint是favorite，則返回true；否則返回false。 |
   | isDefaultImage | T | 表示是否為進程指定映像。 如果沒有與進程相關聯的影像，則返回true；否則返回false。 |
   | 任務 | T | 它包含調用起點時建立的任務。 |
   | imageUrl | T | 它包含與起點對應之影像的url。 |

1. 任務

   任務會指派給使用者／群組，並包含可填入資料的使用者介面(表單或指南（已過時）)。 當指派任務給使用者時，他們會收到表單或指南以完成並送出。

<table>
 <tbody>
  <tr>
   <td>屬性<br /> </td>
   <td>僅限用戶端<br /> </td>
   <td>評論<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>當任務為lc8任務時，任務類為「LC8」，否則為「標準」。<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>它包含任務完成時的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>它包含可咨詢任務的組的ID。 它是在工藝設計過程中設定的。<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>它包含建立任務時的時間戳。<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>F</td>
   <td>它包含建立任務的用戶的ID。<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>它包含有關當前任務分配的詳細資訊。<br /> </td>
  </tr>
  <tr>
   <td>期限<br /> </td>
   <td>F</td>
   <td>它包含任務到達期限的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>說明<br /> </td>
   <td>F</td>
   <td>它包含任務的說明。<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>它包含任務的顯示名稱。<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>它包含可轉發任務的組的ID。 它是在工藝設計過程中設定的。<br /> </td>
  </tr>
  <tr>
   <td>instructions<br /> </td>
   <td>F</td>
   <td>它包含任務的說明。<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>如果任務已鎖定，則返回true。<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>如果必須開啟任務表單才能完成任務，則返回true。<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>如果為true，則在開啟工作時，表單會首次顯示完整畫面。<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>如果為true，則必須選擇路由才能完成任務。<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>如果附件為真，則顯示附件。<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>如果為true，則從起點建立任務。<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>如果工作區中顯示任務，則返回true。<br /> </td>
  </tr>
  <tr>
   <td>nextRements<br /> </td>
   <td>F</td>
   <td>下次提醒的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>優先順序<br /> </td>
   <td>F</td>
   <td>它包含任務的優先順序。<br /> 1 =最高優先順序<br /> 2 =高優先順序<br /> 3 =正常優先順序<br /> 4 =低優先順序<br /> 5 =最低優先順序<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>任務所屬的進程實例的ID。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>任務的進程實例的狀態。<br /> </td>
  </tr>
  <tr>
   <td>rementCount<br /> </td>
   <td>F</td>
   <td>它包含任務的提醒計數。<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>它包含與任務相關的路由清單。 用戶可以通過從路由清單中選擇任一路由來完成任務。<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>它包含任務完成時所選路由的名稱。<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>它包含與任務對應的映像票證。 <br /> 此映像票證用於任務的imageUrl欄位中，以從伺服器獲取任務的映像。 <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>它包含任務服務的名稱。<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>它包含任務服務的標題。<br /> </td>
  </tr>
  <tr>
   <td>狀態<br /> </td>
   <td>F</td>
   <td>1 =已建立（任務是從起點建立的。）<br /> 2 =建立並保存（任務從起點建立並保存。）<br /> 3 =已分配（進程啟動後，任務將分配給用戶。）<br /> 4 =分配和保存（分配和保存任務。）<br /> 100 =已完成（任務已完成）。<br /> 101 =無效（任務已到期）。<br /> 102 =終止<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>它包含流程設計期間任務集的名稱。<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>它包含任務摘要URL。<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>它是任務的訪問控制清單。<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>任務的ID。<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>上次更新任務的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>它包含任務的表單URL。<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>它包含任務表單類型。 使用此欄位，在用戶端上會將工作轉譯為pdf for、swf表格等。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>如果為true，則在工作區中可看到路由操作。<br /> </td>
  </tr>
  <tr>
   <td>showACLAactions<br /> </td>
   <td>T</td>
   <td>如果為true，則可在工作區中看到向前、咨詢、共用等動作。<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>如果為true，表單可離線。 這僅適用於pdf表格。<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>T</td>
   <td>如果為true，則用戶可以保存任務。<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>此物件包含選項，當pdf表單不含提交按鈕時，這些選項會用來透過Reader提交pdf表單。<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>表示是否為進程指定映像。 如果沒有與進程相關聯的影像，則返回true；否則返回false。<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>它包含任務詳細資訊的歷史記錄頁籤中使用的任務清單。<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>如果登入的使用者是任務的擁有者，則為true。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>它包含可對任務執行的所有操作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>它包含可用於任務的所有路由操作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>它包含轉發、共用和查詢等命令（如果可用）。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>它包含鎖定、解除鎖定、放棄、返回、索賠等可用命令。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>它包含有關任務的進程實例的資訊。<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>它包含進程變數的對象陣列（如果存在）。<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>它包含任務進程實例的待定任務清單。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>它是物件的陣列。 每個對象都包含有關路由及其相應確認消息的詳細資訊（如果存在）。<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>它是任務形式資料的URL。<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>這是協力廠商應用程式表單的設定。<br /> </td>
  </tr>
  <tr>
   <td>submitted<br /> </td>
   <td>T</td>
   <td>如果任務已提交，則返回true。<br /> </td>
  </tr>
  <tr>
   <td>attachments<br /> </td>
   <td>T</td>
   <td>任務的附件清單。<br /> </td>
  </tr>
  <tr>
   <td>指定任務<br /> </td>
   <td>T</td>
   <td>任務的分配清單。<br /> </td>
  </tr>
 </tbody>
</table>

1. 篩選

   篩選器基本上是使用者或群組的佇列。 將任務分配給用戶／組時，該任務將添加到相應的隊列中。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限用戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>如果佇列是已登入使用者的預設佇列，則為true，否則為false。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>名稱<br type="_moz" /> </td>
   <td>F</td>
   <td>隊列所有者的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>佇列的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>類型</td>
   <td>F</td>
   <td>它包含隊列的類型。<br /> 0 —— 用戶隊列。<br /> 1. 共用佇列。<br /> 2. 群組佇列。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>T</td>
   <td>這包含與篩選器關聯的查詢。 此查詢用於從完整任務清單中搜索任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任務</td>
   <td>T</td>
   <td>它包含屬於篩選器的所有任務的清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 外出

   您可以管理離職時間表，並控制指派給您的工作流程。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong><br type="_moz" /> </td>
   <td><strong>僅限用戶端</strong><br type="_moz" /> </td>
   <td><strong>評論</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含用戶的不在辦公室時間表的陣列對象。 在每個計畫對象中，startDate欄位包含計畫的開始日期和dendDate欄位包含計畫的結束日期。 如果endDate在排程中為null，表示使用者尚未排程離職排程的結束日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>如果沒有主要指定，則返回true，以備用戶不在辦公室時使用。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>如果使用者不在辦公室，則為true。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含被用戶指定為主要指定的用戶的詳細資訊。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDistans<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含許多對象，用於指定流程特定的離職狀態。 在每個進程特定的指定對象中，processName包含進程的名稱；如果沒有為相應進程分配用戶，isNotDesignated為true；如果沒有為相應進程分配用戶的其他詳細資訊，userDesignated為null。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processes<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含用戶可用的所有進程的清單。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含最初提取的用戶的初始離職設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含已修改的離職設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含登入使用者搜尋到日期的使用者清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 流程實例

   通過工作區或工作台調用流程時，將建立流程實例。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限用戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>F</td>
   <td>流程實例說明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>啟動器</td>
   <td>F</td>
   <td>進程實例的啟動器名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>進程實例的啟動器ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>流程完成時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>進程實例的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 =已啟動<br /> 1 =運行<br /> 2 =完成3 =完成<br /> 4 =終止<br /> 5 =終止6 =暫停7 =暫停<br /><br /><br /><br /> 8 =取消暫停<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>進程的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>進程啟動時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>流程變數的對象陣列。 每個進程變數對象都包含進程變數名、進程變數值和進程變數類型。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任務清單<br type="_moz" /> </td>
   <td>T</td>
   <td>此進程實例生成的任務。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 處理名稱

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限用戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>流程的主要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>流程的次要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>進程的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>F</td>
   <td>流程的標題。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>此流程的流程實例清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任務分配對象

   任務分配對象包含有關任務分配的資訊。 以下是任務分配的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限用戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>建立任務的此分配時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 =初始分配<br /> 1 =轉發（任務已轉發給任務的當前所有者）。<br /> 2 =返回（任務已由任務的前一個所有者返回給任務的當前所有者。）<br /> 3 =已請求（任務的當前所有者已請求任務）。<br /> 4 =呈報（呈報後，任務已指派給任務的當前擁有者。）<br /> 5 =已分配管理員（管理員已將任務分配給當前任務的所有者。）<br /> 6 =已咨詢任務（已咨詢任務的當前責任人）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>更新此任務分配時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>任務當前所有者的隊列ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>任務的當前所有者的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>任務的當前所有者的ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任務ACL對象

   任務ACL對象包含有關權限的資訊，如轉發、共用、咨詢等。 任務。 以下是任務ACL的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限用戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可將附件添加到任務中。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可將附註新增至工作。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可聲明任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為真，可以咨詢任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可轉發任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可共用任務。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任務附件

   附件可以添加到任務中。 附件可以是附件和注釋類型。 以下是attachment對象的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限用戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>建立附件時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>新增附件的使用者ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>添加附件的用戶的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>F</td>
   <td>附件說明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>fileName<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>上次修改附件時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則附註為延伸（長）附註。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>permissions<br type="_moz" /> </td>
   <td>F</td>
   <td>與附件關聯的權限。 allowRead欄位是用於讀取權限，allowWrite是用於寫入權限，allowDelete是用於刪除權限。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>大小<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的大小（以位元組為單位）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>添加附件的任務的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>類型<br type="_moz" /> </td>
   <td>F</td>
   <td>「類型」(Type)是檔案的附件，「類型」(Type)是注釋的注釋。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含依據使用者UI設定的附件建立日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化附件說明。 用於在AEM Forms工作區中顯示附件說明中顯示的特殊字元。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化附件名稱。 用於在AEM Forms工作區中顯示附件名稱中的特殊字元。 僅供注釋。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 使用者

   以下是用戶對象的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅限用戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>address<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的常用名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者說明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者群組清單。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的顯示名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的電子郵件ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>如果使用者不在辦公室，則為true。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的姓氏。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的名字。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的組織名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>郵遞區號<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的郵遞區號。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephone<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的聯絡號碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephoneNumber<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的聯絡號碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>登入使用者的ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
