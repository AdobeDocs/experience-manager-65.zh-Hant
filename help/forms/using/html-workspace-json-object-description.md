---
title: AEM Forms工作區JSON對象說明
seo-title: AEM Forms workspace JSON object description
description: 有關在LiveCycleAEM Forms工作區中用於自定義、擴展、修改和重用的JSON JavaScript對象的概念性資訊。
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

# AEM Forms工作區JSON對象說明 {#aem-forms-workspace-json-object-description}

下面介紹了在AEM Forms工作區中使用的JSON對象。

1. 類別

   類別在工作區的「開始進程」(start process)頁籤中存在。 這些類別用於對起始點進行分類。

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
   <td>ID</td>
   <td>F</td>
   <td>類別ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>F</td>
   <td>類別說明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>父Oid<br type="_moz" /> </td>
   <td>F</td>
   <td>包含父類別的oid<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>起始點清單<br type="_moz" /> </td>
   <td>T</td>
   <td>包含類別中所有起始點的清單</td>
  </tr>
  <tr>
   <td>類別清單</td>
   <td>T</td>
   <td>包含類別的直接子類別清單<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>所有起始點和收藏夾都是在客戶端定義的類別。 收藏夾類別包含用戶標籤為收藏夾的所有起始點。 「所有起始點」類別包含所有起始點。

1. 起點

   在調用時，起點用於從工作區啟動進程。

   | **屬性** | **僅客戶端** | **評論** |
   |---|---|---|
   | 類別ID | F | 它包含起始點所屬類別的ID。 |
   | 說明 | F | 它包含起點的說明。 |
   | 名稱 | F | 它包含起始點的名稱。 |
   | 序列化ImageTicket | F | 它包含與起始點對應的影像票證。 此影像票證用於起始點的imageUrl欄位，以從伺服器獲取起始點的影像。 |
   | 服務名稱 | F | 它包含startpoint的服務名稱。 |
   | 起始點ID | F | 它包含起始點ID。 |
   | 是收藏夾 | T | 表示起始點是否為收藏夾。 如果startpoint是收藏夾，則返回true；否則返回false。 |
   | 是DefaultImage | T | 表示是否為進程指定了映像。 如果沒有與進程關聯的影像，則返回true，否則返回false。 |
   | 任務 | T | 它包含調用起始點時建立的任務。 |
   | 影像URL | T | 它包含與起始點對應的影像的url。 |

1. 任務

   任務被分配給用戶/組，並包括一個用戶介面(表單或指南（已棄用）)，該用戶介面可以填充資料。 為用戶分配任務時，將提供表單或指南以完成和提交。

<table>
 <tbody>
  <tr>
   <td>屬性<br /> </td>
   <td>僅客戶端<br /> </td>
   <td>評論<br /> </td>
  </tr>
  <tr>
   <td>類任務</td>
   <td>F</td>
   <td>任務類為「LC8」時，任務為lc8，否則為「標準」。<br /> </td>
  </tr>
  <tr>
   <td>完成時間<br /> </td>
   <td>F</td>
   <td>它包含任務完成時的時間戳。<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>它包含可咨詢任務的組的ID。 在工藝設計過程中設定。<br /> </td>
  </tr>
  <tr>
   <td>建立時間<br /> </td>
   <td>F</td>
   <td>它包含建立任務時的時間戳。<br /> </td>
  </tr>
  <tr>
   <td>建立ID<br /> </td>
   <td>F</td>
   <td>它包含建立任務的用戶的ID。<br /> </td>
  </tr>
  <tr>
   <td>當前分配<br /> </td>
   <td>F</td>
   <td>它包含有關當前任務分配的詳細資訊。<br /> </td>
  </tr>
  <tr>
   <td>截止<br /> </td>
   <td>F</td>
   <td>它包含任務到達其截止時間的時間戳。<br /> </td>
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
   <td>它包含可轉發任務的組的ID。 在工藝設計過程中設定。<br /> </td>
  </tr>
  <tr>
   <td>說明<br /> </td>
   <td>F</td>
   <td>它包含任務的說明。<br /> </td>
  </tr>
  <tr>
   <td>已鎖定<br /> </td>
   <td>F</td>
   <td>如果任務已鎖定，則返回true。<br /> </td>
  </tr>
  <tr>
   <td>是MustOpenToComplete<br /> </td>
   <td>F</td>
   <td>如果必須開啟任務表單才能完成任務，則返回true。<br /> </td>
  </tr>
  <tr>
   <td>是OpenFullScreen<br /> </td>
   <td>F</td>
   <td>如果為true，則在開啟任務時，表單將首次顯示完整螢幕。<br /> </td>
  </tr>
  <tr>
   <td>是RouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>如果為true，則必須選擇路由以完成任務。<br /> </td>
  </tr>
  <tr>
   <td>是ShowAttachments<br /> </td>
   <td>F</td>
   <td>如果為真，則顯示附件。<br /> </td>
  </tr>
  <tr>
   <td>是StartTask<br /> </td>
   <td>F</td>
   <td>如果為true，則從起點建立任務。<br /> </td>
  </tr>
  <tr>
   <td>可見<br /> </td>
   <td>F</td>
   <td>如果任務在工作區中可見，則返回true。<br /> </td>
  </tr>
  <tr>
   <td>下一提醒<br /> </td>
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
   <td>提醒計數<br /> </td>
   <td>F</td>
   <td>它包含任務的提醒計數。<br /> </td>
  </tr>
  <tr>
   <td>路由清單<br /> </td>
   <td>F</td>
   <td>它包含與任務關聯的路由清單。 用戶可以通過從路由清單中選擇任何一條路由來完成任務。<br /> </td>
  </tr>
  <tr>
   <td>所選路由<br /> </td>
   <td>F</td>
   <td>它包含任務完成時所選路由的名稱。<br /> </td>
  </tr>
  <tr>
   <td>序列化ImageTicket<br /> </td>
   <td>F</td>
   <td>它包含與任務對應的影像票證。 此影像票證用於任務的imageUrl欄位，以從伺服器獲取任務的影像。<br /> <br /> </td>
  </tr>
  <tr>
   <td>服務名稱<br /> </td>
   <td>F</td>
   <td>它包含任務的服務名稱。<br /> </td>
  </tr>
  <tr>
   <td>服務標題<br /> </td>
   <td>F</td>
   <td>它包含任務的服務標題。<br /> </td>
  </tr>
  <tr>
   <td>狀態<br /> </td>
   <td>F</td>
   <td>1 =已建立（從起點建立任務。）<br /> 2 =已建立並保存（任務從起點建立並保存。）<br /> 3 =已分配（任務在進程啟動後分配給用戶。）<br /> 4 =已分配並保存（任務已分配並保存。）<br /> 100 =已完成（任務已完成。）<br /> 101 =已掛起（任務已到期）<br /> 102 =終止<br /> </td>
  </tr>
  <tr>
   <td>步驟名稱<br /> </td>
   <td>F</td>
   <td>它包含在流程設計期間的任務集的名稱。<br /> </td>
  </tr>
  <tr>
   <td>摘要URL<br /> </td>
   <td>F</td>
   <td>它包含任務摘要URL。<br /> </td>
  </tr>
  <tr>
   <td>任務ACL<br /> </td>
   <td>F</td>
   <td>它是任務的訪問控制清單。<br /> </td>
  </tr>
  <tr>
   <td>任務ID<br /> </td>
   <td>F</td>
   <td>任務的ID。<br /> </td>
  </tr>
  <tr>
   <td>更新時間<br /> </td>
   <td>F</td>
   <td>上次更新任務的時間戳。<br /> </td>
  </tr>
  <tr>
   <td>窗體URL<br /> </td>
   <td>T</td>
   <td>它包含任務的表單URL。<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>它包含任務表單類型。 使用此欄位，任務在客戶端上以pdf形式呈現，用於swf表單等。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>如果為true，則在工作區中可見路由操作。<br /> </td>
  </tr>
  <tr>
   <td>showACLAactions<br /> </td>
   <td>T</td>
   <td>如果為true，則在工作區中可看到向前、查詢、共用等操作。<br /> </td>
  </tr>
  <tr>
   <td>支援離線<br /> </td>
   <td>T</td>
   <td>如果為true，則表單可離線。 這僅用於pdf表單。<br /> </td>
  </tr>
  <tr>
   <td>支援保存<br /> </td>
   <td>T</td>
   <td>如果為true，則用戶可以保存任務。<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>此對象包含用於通過閱讀器提交pdf表單的選項，以防pdf表單不包含提交按鈕。<br /> </td>
  </tr>
  <tr>
   <td>是DefaultImage<br /> </td>
   <td>T</td>
   <td>表示是否為進程指定了映像。 如果沒有與進程關聯的影像，則返回true，否則返回false。<br /> </td>
  </tr>
  <tr>
   <td>歷史記錄任務清單<br /> </td>
   <td>T</td>
   <td>它包含在任務詳細資訊的歷史記錄頁籤中使用的任務清單。<br /> </td>
  </tr>
  <tr>
   <td>是所有者<br /> </td>
   <td>T</td>
   <td>如果登錄用戶是任務的所有者，則返回true。<br /> </td>
  </tr>
  <tr>
   <td>可用命令<br /> </td>
   <td>T</td>
   <td>它包含可以對任務執行的所有操作。<br /> </td>
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
   <td>掛起任務<br /> </td>
   <td>T</td>
   <td>它包含任務的進程實例的掛起任務清單。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>它是對象的陣列。 每個對象都包含有關路由的詳細資訊及其相應的確認消息（如果存在）。<br /> </td>
  </tr>
  <tr>
   <td>資料URL<br /> </td>
   <td>T</td>
   <td>它是任務表單資料的url。<br /> </td>
  </tr>
  <tr>
   <td>外部AppConfig<br /> </td>
   <td>T</td>
   <td>這是第三方應用程式表單的配置。<br /> </td>
  </tr>
  <tr>
   <td>提交<br /> </td>
   <td>T</td>
   <td>如果提交任務，則返回true。<br /> </td>
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

   篩選器基本上是用戶或組的隊列。 將任務分配給用戶/組後，將該任務添加到相應的隊列中。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅客戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>為預設 <br type="_moz" /> </td>
   <td>F</td>
   <td>如果隊列是登錄用戶的預設隊列，則返回true；否則返回false。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>名稱<br type="_moz" /> </td>
   <td>F</td>
   <td>隊列所有者的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>QID</td>
   <td>F</td>
   <td>隊列的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>類型</td>
   <td>F</td>
   <td>它包含隊列類型。<br /> 0 — 用戶隊列。<br /> 1. 共用隊列。<br /> 2. 組隊列。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>T</td>
   <td>該查詢與篩選器關聯。 此查詢用於從完整任務清單中搜索任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任務</td>
   <td>T</td>
   <td>它包含屬於篩選器的所有任務的清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 外出

   您可以管理離職時間表，並控制在缺勤時分配給您的任務流。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong><br type="_moz" /> </td>
   <td><strong>僅客戶端</strong><br type="_moz" /> </td>
   <td><strong>評論</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期範圍<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含用戶的非辦公時間表的陣列對象。 在每個計畫對象中，startDate欄位包含計畫的開始日期和dendDate欄位包含計畫的結束日期。 如果endDate在計畫中為null，則表示用戶尚未計畫離職計畫的結束日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>是NoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>如果用戶不在辦公室，則沒有主要指定，則為True。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>未辦公<br type="_moz" /> </td>
   <td>F</td>
   <td>如果用戶不在辦公室，則為True。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>OfOfficeDesignate外<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含被用戶指定為主要指定用戶的詳細資訊。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDistments<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含特定於流程的指定外部對象的陣列。 在每個特定於進程的指定對象中，processName包含進程的名稱，如果沒有為相應進程分配用戶，則isNotDesignated為true；如果沒有為相應進程分配用戶的其他詳細資訊，則userDesignated為null。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>進程<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含用戶可用的所有進程的清單。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>初始OutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含最初提取的用戶的初始外出設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>OfOfficeSettings外<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含修改的外出設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>用戶搜索歷史記錄<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含登錄用戶搜索到的用戶清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 進程實例

   通過工作區或工作台調用流程時，將建立流程實例。

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
   <td>流程實例說明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>啟動器</td>
   <td>F</td>
   <td>進程實例的啟動器名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>啟動器ID</td>
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
   <td>0 =啟動<br /> 1 =正在運行<br /> 2 =完成<br /> 3 =完成<br /> 4 =終止<br /> 5 =終止<br /> 6 =暫停<br /> 7 =掛起<br /> 8 =取消掛起<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>進程名<br type="_moz" /> </td>
   <td>F</td>
   <td>進程的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>進程啟動時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>進程變數的對象陣列。 每個進程變數對象都包含進程變數名稱、進程變數值和進程變數類型。<br type="_moz" /> </td>
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
   <td>進程的主版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>進程的次要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>進程名<br type="_moz" /> </td>
   <td>F</td>
   <td>進程的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>進程標題<br type="_moz" /> </td>
   <td>F</td>
   <td>流程的標題。<br type="_moz" /> </td>
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
   <td>建立任務的此分配時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>賦值類型<br type="_moz" /> </td>
   <td>F</td>
   <td>0 =初始分配<br /> 1 =轉發（任務已轉發給任務的當前所有者。）<br /> 2 =已返回（任務已由任務的前一個所有者返回給任務的當前所有者。）<br /> 3 =已聲明（任務的當前所有者已聲明任務。）<br /> 4 =升級（升級後已將任務分配給任務的當前所有者。）<br /> 5 =已分配管理員（管理員已將任務分配給任務的當前所有者。）<br /> 6 =已咨詢（已咨詢任務的當前所有者。）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>更新任務的此分配時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>隊列ID<br type="_moz" /> </td>
   <td>F</td>
   <td>任務當前所有者的隊列ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>隊列所有者<br type="_moz" /> </td>
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

   任務ACL對象包含有關前向、共用、查詢等權限的資訊。 任務。 以下是任務ACL的屬性。

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
   <td>如果為true，則可以將附件添加到任務中。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可將注釋添加到任務中。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim（可聲明）<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可聲明任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可以咨詢任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>可轉發<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可以轉發任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>可共用<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可以共用任務。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任務附件

   附件可以添加到任務。 附件可以是附件和注釋類型。 以下是附件對象的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>僅客戶端</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>建立日期<br type="_moz" /> </td>
   <td>F</td>
   <td>建立附件時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>建立者ID<br type="_moz" /> </td>
   <td>F</td>
   <td>添加附件的用戶的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>建立者名稱<br type="_moz" /> </td>
   <td>F</td>
   <td>添加附件的用戶的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的說明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>檔案名<br type="_moz" /> </td>
   <td>F</td>
   <td>附件名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>ID<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>上次修改日期<br type="_moz" /> </td>
   <td>F</td>
   <td>上次修改附件時的時間戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>注釋擴展<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則注釋是擴展（長）注釋。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>權限<br type="_moz" /> </td>
   <td>F</td>
   <td>與附件關聯的權限。 allowRead欄位用於讀取權限，allowWrite用於寫入權限，allowDelete用於刪除權限。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>大小<br type="_moz" /> </td>
   <td>F</td>
   <td>附件大小（以位元組為單位）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任務ID<br type="_moz" /> </td>
   <td>F</td>
   <td>添加附件的任務的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>類型<br type="_moz" /> </td>
   <td>F</td>
   <td>「類型」(Type)是檔案的附件，「類型」(Type)是注釋的注釋。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>格式化建立日期<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含根據用戶UI設定建立附件的日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>格式化描述<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化附件說明。 用於顯示AEM Forms工作區附件說明中的特殊字元。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>格式化檔案名<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化附件名稱。 用於顯示AEM Forms工作區中附件名稱中的特殊字元。 這僅供注釋使用。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 使用者

   以下是用戶對象的屬性。

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
   <td>用戶的地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>公用名<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的公用名。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>說明<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的說明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberss<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶組清單。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的顯示名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的電子郵件ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>未辦公<br type="_moz" /> </td>
   <td>F</td>
   <td>如果用戶不在辦公室，則為True。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>姓氏<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的姓。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>名字<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的名。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>曲面<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>組織<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的組織名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>郵政地址<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的郵政地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>電話<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的聯繫人號碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>電話號碼<br type="_moz" /> </td>
   <td>F</td>
   <td>用戶的聯繫人號碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>用戶ID<br type="_moz" /> </td>
   <td>F</td>
   <td>登錄用戶的ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
