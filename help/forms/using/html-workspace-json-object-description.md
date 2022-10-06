---
title: AEM Forms工作區JSON物件說明
seo-title: AEM Forms workspace JSON object description
description: LiveCycleAEM Forms工作區以自訂、擴充、修改和重複使用所使用之JSON JavaScript物件的概念資訊。
seo-description: Conceptual information about the JSON JavaScript objects used in LiveCycle AEM Forms workspace for customization, extension, modification, and reuse.
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2109'
ht-degree: 2%

---

# AEM Forms工作區JSON物件說明 {#aem-forms-workspace-json-object-description}

AEM Forms工作區中使用的JSON物件說明如下。

1. 類別

   工作區的「開始進程」(start process)頁簽中存在類別。 這些類別用於分類起始點。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅客戶端</strong></td>
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
   <td>包含父類別的OID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>包含類別中所有起始點的清單</td>
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
>所有起始點和收藏夾都是在客戶端上定義的類別。 收藏夾類別包含用戶標籤為收藏夾的所有起始點。 所有起始點類別包含所有起始點。

1. 起始點

   起始點用於在調用時從工作區啟動進程。

   | **屬性** | **僅客戶端** | **評論** |
   |---|---|---|
   | categoryId | F | 它包含起始點所屬類別的id。 |
   | 說明 | F | 它包含起始點的說明。 |
   | 名稱 | F | 它包含起始點的名稱。 |
   | serializedImageTicket | F | 它包含與起始點對應的影像票證。 此映像票證用於起始點的imageUrl欄位，以從伺服器獲取起始點的映像。 |
   | serviceName | F | 它包含起始點服務的名稱。 |
   | startpointId | F | 它包含起始點的id。 |
   | isFavorite | T | 表示起始點是否為收藏夾。 如果起始點是收藏夾，則為true，否則為false。 |
   | isDefaultImage | T | 表示是否為進程指定了映像。 如果沒有與進程相關聯的影像，則返回true；否則返回false。 |
   | 任務 | T | 它包含調用起始點時建立的任務。 |
   | imageUrl | T | 它包含與起始點對應之影像的url。 |

1. 任務

   任務被分配給用戶/組，並包括可填入資料的用戶介面(表單或指南（已過時）)。 為用戶分配任務時，將向用戶提供完成和提交的表單或指南。

<table>
 <tbody>
  <tr>
   <td>屬性<br /> </td>
   <td>僅客戶端<br /> </td>
   <td>評論<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>任務為lc8任務，而任務為「標準」時，任務類為「LC8」。<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>它包含任務完成時的時間戳。<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>它包含可以咨詢任務的組的ID。 在設計過程中設定。<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>它包含建立任務時的時間戳。<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>F</td>
   <td>它包含建立任務的用戶ID。<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>它包含有關當前任務分配的詳細資訊。<br /> </td>
  </tr>
  <tr>
   <td>截止日期<br /> </td>
   <td>F</td>
   <td>它包含任務達到其截止時間的時間戳記。<br /> </td>
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
   <td>它包含可轉發任務的組的ID。 在設計過程中設定。<br /> </td>
  </tr>
  <tr>
   <td>說明<br /> </td>
   <td>F</td>
   <td>它包含任務的說明。<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>如果任務被鎖定，則為true。<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>如果必須開啟任務表單才能完成任務，則為true。<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>如果為true，則在開啟任務時，表單將首次顯示完整螢幕。<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>如果為true，則必須選擇路由以完成任務。<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>如果為true，則會顯示附件。<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>如果為true，則從起始點建立任務。<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>如果工作區中顯示任務，則返回true。<br /> </td>
  </tr>
  <tr>
   <td>nextTimmer<br /> </td>
   <td>F</td>
   <td>下次提醒的時間戳。<br /> </td>
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
   <td>menternCount<br /> </td>
   <td>F</td>
   <td>它包含任務的提醒計數。<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>它包含與任務關聯的路由清單。 用戶可以通過從路由清單中選擇任何一條路由來完成該任務。<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>它包含任務完成時所選路由的名稱。<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>它包含與任務對應的影像票證。 此映像票證用於任務的imageUrl欄位中，以從伺服器獲取任務的映像。<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>它包含任務的服務名稱。<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>它包含任務服務的標題。<br /> </td>
  </tr>
  <tr>
   <td>狀態<br /> </td>
   <td>F</td>
   <td>1 =已建立（任務是從起始點建立的。）<br /> 2 =建立並保存（任務從起始點建立並保存。）<br /> 3 =已分配（在進程啟動後，將任務分配給用戶。）<br /> 4 =分配並保存（分配並保存任務。）<br /> 100 =已完成（任務已完成。）<br /> 101 =無條件（任務已到期）。<br /> 102 =終止<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>它包含流程設計期間任務集的名稱。<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>它包含任務摘要url。<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>它是任務的訪問控制清單。<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>任務ID。<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>上次更新任務時的時間戳。<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>它包含任務的表單URL。<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>它包含任務表單類型。 使用此欄位，任務在用戶端上會呈現為的PDF、swf表單等。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>如果為true，則在工作區中顯示路由操作。<br /> </td>
  </tr>
  <tr>
   <td>showACLAactions<br /> </td>
   <td>T</td>
   <td>若為true，則後續、諮詢、共用等動作會顯示在工作區中。<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>如果為true，則表單可離線。 這僅適用於pdf表單。<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>T</td>
   <td>如果為true，則用戶可以保存任務。<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>此對象包含的選項用於在pdf表單不包含提交按鈕時通過讀取器提交pdf表單。<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>表示是否為進程指定了映像。 如果沒有與進程相關聯的影像，則返回true；否則返回false。<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>它包含任務詳細資訊的歷史記錄頁簽中使用的任務清單。<br /> </td>
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
   <td>它包含轉發、共用和查詢等命令（如果可用於任務）。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>它包含諸如鎖定、解鎖、放棄、返回、聲明等可用命令。<br /> </td>
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
   <td>它包含任務進程實例的掛起任務清單。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>它是物件陣列。 每個對象包含有關路由及其相應確認消息的詳細資訊（如果存在）。<br /> </td>
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
   <td>已提交<br /> </td>
   <td>T</td>
   <td>如果提交了任務，則返回true。<br /> </td>
  </tr>
  <tr>
   <td>附件<br /> </td>
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

   篩選器基本上是使用者或群組的佇列。 將任務分配給用戶/組時，任務將添加到相應的隊列中。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅客戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>如果佇列是登入使用者的預設佇列，則為true，否則為false。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>名稱<br type="_moz" /> </td>
   <td>F</td>
   <td>隊列所有者的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>隊列的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>類型</td>
   <td>F</td>
   <td>它包含佇列的類型。<br /> 0 — 使用者佇列。<br /> 1. 共用佇列。<br /> 2. 組隊列。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>T</td>
   <td>這包含與篩選器相關聯的查詢。 此查詢用於從完整任務清單中搜索任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任務</td>
   <td>T</td>
   <td>它包含屬於篩選器的所有任務的清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 外部

   您可以管理離職時間表，並控制在您缺勤時分配給您的任務流。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong><br type="_moz" /> </td>
   <td><strong>僅客戶端</strong><br type="_moz" /> </td>
   <td><strong>評論</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含使用者不在辦公室的排程的陣列物件。 在每個計畫對象中， startDate欄位包含計畫的開始日期和dendDate欄位包含計畫的結束日期。 如果排程中的endDate為null，表示使用者尚未排程離職排程的結束日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>若使用者不在辦公室，則沒有主要指定值，則為true。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>如果使用者不在辦公室，則為true。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含被用戶指定為主要指定的用戶的詳細資訊。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDistant<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含特定於進程的離職指定的對象陣列。 在每個特定於進程的指定對象中，processName包含進程的名稱；如果未為相應進程分配用戶，則isNotDesignated為true；如果未為相應進程分配用戶的其他詳細資訊，則userDesignated為null。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>流程<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含用戶可用的所有進程的清單。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含最初擷取的使用者初始離職設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含已修改的非辦公設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含登入使用者截至日期所搜尋的使用者清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 進程實例

   透過工作區或工作台叫用程式時，會建立程式例項。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅客戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>F</td>
   <td>流程實例的說明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>發起人</td>
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
   <td>進程完成時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>進程實例的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 =起始<br /> 1 =執行中<br /> 2 =完成<br /> 3 =完成<br /> 4 =終止<br /> 5 =終止<br /> 6 =暫停<br /> 7 =暫停<br /> 8 =取消暫停<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>程式名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>進程啟動時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>進程變數的對象陣列。 每個進程變數對象都包含進程變數的名稱、進程變數值和進程變數類型。<br type="_moz" /> </td>
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
   <td><strong>僅客戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>程式的主要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>程式的次要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>程式名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>F</td>
   <td>程式的標題。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>此進程的進程實例清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任務分配對象

   任務分配對象包含有關任務分配的資訊。 以下是任務分配的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅客戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>建立任務分配時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 =初始分配<br /> 1 =轉發（任務已轉發到任務的當前所有者。）<br /> 2 =已返回（任務已按任務的前一個責任人返回給當前任務責任人。）<br /> 3 =已申請（任務的當前所有者已申請任務）。<br /> 4 =呈報（呈報後已將任務指派給目前的任務擁有者。）<br /> 5 =已分配管理員（管理員已將任務分配給當前任務的所有者。）<br /> 6 =已咨詢任務（已向當前任務所有者咨詢任務）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>更新任務的此分配時的時間戳。<br type="_moz" /> </td>
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
   <td>任務當前所有者的ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任務ACL對象

   任務ACL對象包含有關權限的資訊，如轉發、共用、查詢等。 任務。 以下是任務ACL的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅客戶端</strong></td>
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
   <td>如果為true，則可將附註添加到任務中。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可申請任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>如果是真的，可以咨詢任務。<br type="_moz" /> </td>
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

   可以將附件添加到任務中。 附件可以是附件和注釋類型。 以下是附件對象的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅客戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>建立附件時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>新增附件的使用者ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>新增附件的使用者名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的說明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>fileName<br type="_moz" /> </td>
   <td>F</td>
   <td>附件名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>F</td>
   <td>附件ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>上次修改附件時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則注釋為擴展（長）注釋。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>權限<br type="_moz" /> </td>
   <td>F</td>
   <td>與附件相關聯的權限。 allowRead欄位用於讀取權限，allowWrite用於寫入權限，allowDelete用於刪除權限。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>大小<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的大小（以位元組為單位）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>添加附件的任務ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>類型<br type="_moz" /> </td>
   <td>F</td>
   <td>「類型」是檔案的附件，「類型」是注釋的注釋。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>它會根據使用者的UI設定包含附件建立日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化附件說明。 用於顯示AEM Forms工作區中附件說明中出現的特殊字元。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化附件名稱。 用於顯示AEM Forms工作區中附件名稱中出現的特殊字元。 這僅供注釋。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 使用者

   以下是使用者物件的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅客戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>地址<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的一般名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的說明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者群組的清單。<br type="_moz" /> </td>
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
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>如果使用者不在辦公室，則為true。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的姓氏。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的名字。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的組織名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>郵遞區號<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的郵遞區號。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>電話<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的聯繫電話。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>電話號碼<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的聯繫電話。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>登入使用者的id。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
