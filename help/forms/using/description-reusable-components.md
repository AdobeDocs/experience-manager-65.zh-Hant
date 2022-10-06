---
title: 可重複使用元件的說明
seo-title: Description of reusable components
description: 可重複使用元件的完整清單，包含檔案名稱和相依性，可協助您將AEM Forms工作區元件整合在網頁應用程式中。
seo-description: A complete list of reusable components with filenames and dependencies, to help you integrate AEM Forms workspace component in your web applications.
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 9%

---

# 可重複使用元件的說明 {#description-of-reusable-components}

AEM Forms工作區由 [可重複](/help/forms/using/integrating-html-ws-components-web.md) 組織在特定 [資料夾結構](/help/forms/using/folder-structure.md) 在CRX™。 每個元件在資料夾結構中指定的位置都有模型、檢視和範本檔案、其他元件檔案的JavaScript™相依性、元件監聽的事件，以及在AEM Forms工作區中觸發這些事件的JavaScript物件。 此處提供了具有組成檔案名和依賴項的可重複使用元件的完整清單。

## 任務清單 {#tasklist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>tasklist.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td>
    <ul>
     <li><p>UserSearch</p></li>
     <li><p>任務</p></li>
     <li><p>團隊任務</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>任務模型</p></li>
     <li><p>團隊任務模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>filterSelected — 任務清單模型</p></li>
     <li><p>刪除 — 任務清單模型</p></li>
     <li><p>updateQueue - tasklist模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>只要您從自訂應用程式中觸發此元件的filterSelected事件，則此元件可獨立於AEM Forms工作區使用。

## 任務 {#task}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>task.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>任務清單模型</p></li>
     <li><p>takactions實用程式</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>submitComplete — 任務模型</p></li>
     <li><p>拒絕 — 任務模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>工作區調用TaskList模型的fetchTasks函式以為此元件建立Task模型。

## FilterList {#filterlist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>filterlist.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>filterlist.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>已提取任務清單模型 </p></li>
     <li><p>刪除 — 任務清單模型 </p></li>
     <li><p>updateQueue - tasklist模型 </p></li>
     <li><p>refreshedQueue - tasklist模型 </p></li>
     <li><p>filterSelected — 任務清單模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## 篩選 {#filter}

<table>
 <tbody>
  <tr>
   <td><p>檢視</p> </td>
   <td><p>filter.js</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>filter.html</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td>
    <ul>
     <li><p>欄位：佇列：{ name, qid, isDefault, type}</p> </li>
     <li><p>欄位：查詢：字串</p> </li>
     <li><p>欄位：parentView:filterlist視圖</p> </li>
     <li><p>欄位：parentModel:任務清單模型</p> </li>
     <li><p>欄位：實用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已監聽事件</p> </td>
   <td><p>不適用</p> </td>
  </tr>
 </tbody>
</table>

## TeamQueues {#teamqueues}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>teamqueues.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>teamqueues.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>已提取任務清單模型 </p></li>
     <li><p>刪除 — 任務清單模型 </p></li>
     <li><p>updateQueue - tasklist模型 </p></li>
     <li><p>teamQueuesRechated - tasklist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## TeamFilter {#teamfilter}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>檢視</p> </td>
   <td><p>teamfilter.js</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>teamfilter.html</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td>
    <ul>
     <li><p>延伸：篩選檢視</p> </li>
     <li><p>欄位：佇列：{ name, qid, isDefault, type }</p> </li>
     <li><p>欄位：查詢：字串</p> </li>
     <li><p>欄位：parentView :filterlist視圖</p> </li>
     <li><p>欄位：parentModel :任務清單模型</p> </li>
     <li><p>欄位：實用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已監聽事件</p> </td>
   <td><p>不適用</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter獲取指明已從TaskList元件中選擇了哪個任務的事件。 雖然這些元件共用模型類，但沒有其它依賴項。

## 任務詳細資訊 {#taskdetails}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>tasklist.js</p> </td>
  </tr>
  <tr>
   <td><p>檢視</p> </td>
   <td><p>taskdetails.js</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>taskdetails.html</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>大多數實用程式類</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>表單轉譯公用程式</p> </li>
     <li><p>附註實用程式</p> </li>
     <li><p>附件實用程式</p> </li>
     <li><p>takactions實用程式</p> </li>
     <li><p>歷史記錄實用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>轉發 — 任務模型</p> </li>
     <li><p>共用 — 任務模型</p> </li>
     <li><p>已咨詢 — 任務模型</p> </li>
     <li><p>已拒絕 — 任務模型</p> </li>
     <li><p>放棄 — 任務模型</p> </li>
     <li><p>未鎖定 — 任務模型</p> </li>
     <li><p>鎖定 — 任務模型</p> </li>
     <li><p>已聲明 — 任務模型</p> </li>
     <li><p>更改：任務選定 — 任務清單模型</p> </li>
     <li><p>change:formUrl — 任務模型</p> </li>
     <li>attachmentURLFechted — 任務模型</li>
    </ul>
    <ul>
     <li>newAttachment — 任務模型</li>
     <li><p>taskHistoryRechated — 任務模型</p> </li>
     <li>prepareForSubmitComplete — 任務模型</li>
     <li><p>submitComplete — 任務模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 類別清單 {#categorylist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>startprocess.html（在路由資料夾中）</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>類別</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>favoritecategoryfactory模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>allStartpointsRechated - categorylist模型 </p></li>
     <li><p>新增 — categorylist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此元件使用某些其他元件（如StartPointList、StartPoint和Task）的模型類。 除了此相依性外， CategoryList也可獨立使用。

## 類別 {#category}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>category.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>categorlist模型</p></li>
     <li><p>startpointlist模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>已更改 — 類別模型 </p></li>
     <li><p>childrenRected — 類別模型 </p></li>
     <li><p>category:selected - categorylist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## StartPointList {#startpointlist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>startpointlist.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>startprocess.html（在路由資料夾中）</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>類別模型</p></li>
     <li><p>favoritecategoryfactory模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
     <li><p>startpoint視圖</p></li>
     <li><p>startpointlist模型</p></li>
     <li><p>起始點模型</p></li>
     <li><p>任務模型</p></li>
     <li><p>任務模型</p></li>
     <li><p>任務清單模型</p></li>
     <li><p>團隊任務模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>category:selected - categorylist模型 </p></li>
     <li><p>allStartpointsRechated - categorylist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList和CategoryList元件共用模型類，因此前者取決於後者。 CategoryList訪問有關顯示哪個類別起始點的資訊。 要單獨使用StartPointList，請從CategoryList模擬事件觸發器。

## StartPoint {#startpoint}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>startpoint.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>任務模型</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>更改 — 起始點模型 </p></td>
  </tr>
 </tbody>
</table>

## StartProcess {#startprocess}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>categorylist.js</p> </td>
  </tr>
  <tr>
   <td><p>檢視</p> </td>
   <td><p>startprocess.js</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>startprocess.html</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td>
    <ul>
     <li><p>大多數實用程式類</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td>
    <ul>
     <li><p>類別模型</p> </li>
     <li><p>favoritecategoryfactory模型</p> </li>
     <li><p>allcategoryfactory模型</p> </li>
     <li><p>表單轉譯公用程式</p> </li>
     <li><p>附註實用程式</p> </li>
     <li><p>附件實用程式</p> </li>
     <li><p>takactions實用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>category:selected - categorylist模型</p> </li>
     <li><p>change:invokedTask - startpointlist模型</p> </li>
     <li><p>change:formUrl — 任務模型</p> </li>
     <li><p>startpoint:selected - startpointlist模型</p> </li>
     <li><p>轉發 — 任務模型</p> </li>
     <li><p>放棄 — 任務模型</p> </li>
     <li><p>未鎖定 — 任務模型</p> </li>
     <li><p>鎖定 — 任務模型</p> </li>
     <li>attachmentURLFechted — 任務模型</li>
     <li>newAttachment — 任務模型</li>
     <li>prepareForSubmitComplete — 任務模型 </li>
     <li><p>submitComplete — 任務模型</p> </li>
     <li><p>allStartpointsRechated - categorylist模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess和StartPointList元件共用模型類。 從StartPointList中選擇起始點時，此元件將變得相關。

## ProcessNameList {#processnamelist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>tracking.html（在路由資料夾中）</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>processname model</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>add - processnamelist model </p></li>
     <li><p>已獲取：processnames - processnamelist模型 </p></li>
     <li><p>更改 — processnamelist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList不依賴於其他元件。 但在內部，它取決於ProcessInstanceList模型類，而ProcessInstanceList模型類又取決於其他元件。 因此，ProcessNameList使用許多模型類，如ProcessInstanceList、ProcessInstance、TaskList、Teamtask和Task。 除了這些依賴項外，ProcessNameList還可單獨使用。

## ProcessName {#processname}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>processname（在processnamelist.js中）</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>processname.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>processinstancelist模型</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>change - processname模型 </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceList {#processinstancelist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>processinstancelist.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>tracking.html（在路由資料夾中）</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>processname model</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>processname:selected -processnamelist模型 </p></li>
     <li><p>processname:instancesechatted - processnamelist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList需要ProcessNameList中的一個事件，該事件指示用於提取和顯示實例的進程名。 要單獨使用ProcessInstanceList，請單獨模擬事件觸發。

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>processnamelist.js內的processname</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>processinstance.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>任務清單模型</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>更改 — 處理實例模型 </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceHistory {#processinstancehistory}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>processinstancehistory.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>processinstancehistory.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>processname model</p></li>
     <li><p>歷史記錄實用程式</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>processname:selected -processnamelist模型 </p></li>
     <li><p>processinstance:selected -processinstancelist模型 </p></li>
     <li><p>tasksRechated - processinstance模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory需要ProcessInstanceList中的一個事件，該事件指明要顯示哪個進程實例的歷史記錄。 除此相依性外，元件也可獨立使用。

## OutofOffice {#outofoffice}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>檢視</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>outofoffice.html</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>usersearch檢視</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>outOfficeSettingsRechited - outofofice模型</p> </li>
     <li><p>outOfficeSettingsSaved - outoffice模型</p> </li>
     <li><p>processesRected - outofoffice模型</p> </li>
     <li><p>principalSelected - principalsearch視圖</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice可獨立使用。

## ShareQueue {#sharequeue}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>檢視</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>sharequeue.html</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>usersearch檢視</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGrated - sharequeue模型</p> </li>
     <li><p>queueAccessRequested - sharequeue模型</p> </li>
     <li><p>grantedUsersRechated - sharequeue模型</p> </li>
     <li>accessibleUsersRechited - sharequeue模型</li>
     <li><p>queueAccessLevesed - sharequeue模型</p> </li>
     <li><p>queueAccessRemoved - sharequeue模型</p> </li>
     <li><p>principalSelected - principalsearch視圖</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue可單獨使用。

## UISettings {#uisettings}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>uisettings.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>preferencesRected - uisetings模型 </p></li>
     <li><p>settingUpdated - uisetings模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings可獨立使用。

## AppNavigation {#appnavigation}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>appnavigation.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>已監聽事件</p></td>
   <td><p>不適用</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation可獨立使用。

## UserInfo {#userinfo}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>檢視</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>userinfo.html</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li>userImageUrlRechitd - userinfo模型</li>
     <li>sessionRenewed - userinfo模型 <br /> </li>
     <li>sessionExpired - userinfo模型 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo可獨立使用。

## WSError {#wserror}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>範本</p></td>
   <td><p>wserror.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>newWsError — 錯誤模型 </p></td>
  </tr>
 </tbody>
</table>

## UserSearch {#usersearch}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>檢視</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>usersearch.html</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li>principalSearch - principalsearch模型</li>
     <li>outOfOfficeInfoEchated - usersearch模型</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SearchTemplate {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>檢視</p> </td>
   <td><p>searchtemplate（在searchtemplatelist.js中） </p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>searchtemplate.html</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td><p>templateRechated-searchtemplate模型</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateList {#searchtemplatelist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>檢視</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>tracking.html（在路由資料夾中）</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>searchtemplate model</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td><p>變更 — searchtemplatelist模型</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateDetails {#searchtemplatedetails}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>檢視</p> </td>
   <td><p>searchtemplatedetails.js</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>searchtemplatedetails.html</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td>不適用<br /> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td><p>searchTemplate:selected - searchtemplate模型</p> </td>
  </tr>
 </tbody>
</table>
