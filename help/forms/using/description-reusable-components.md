---
title: 可重複使用的元件說明
seo-title: 可重複使用的元件說明
description: 可重複使用的元件完整清單以及檔案名稱和相依性，可協助您將AEM Forms工作區元件整合在網頁應用程式中。
seo-description: 可重複使用的元件完整清單以及檔案名稱和相依性，可協助您將AEM Forms工作區元件整合在網頁應用程式中。
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 可重複使用的元件說明 {#description-of-reusable-components}

AEM Forms工作區由可重複使 [用的元件組成](/help/forms/using/integrating-html-ws-components-web.md) ，這些元件會組織在CRX [](/help/forms/using/folder-structure.md) ™的特定資料夾結構中。 每個元件在資料夾結構中指定的位置都有模型、檢視和範本檔案、與其他元件檔案的JavaScript™相依性、由元件監聽的事件，以及在AEM Forms工作區中觸發這些事件的JavaScript物件。 此處提供可重複使用的元件的完整清單，其中包含組成檔案名稱和相依性。

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
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td>
    <ul>
     <li><p>filterSelected —— 任務清單模型</p></li>
     <li><p>刪除——任務清單模型</p></li>
     <li><p>updateQueue —— 任務清單模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>只要您從自訂應用程式中觸發此元件的filterSelected事件，此元件就可獨立於AEM Forms工作區使用。

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
     <li><p>taskactions實用程式</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td>
    <ul>
     <li><p>submitComplete —— 任務模型</p></li>
     <li><p>拒絕——任務模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>工作區調用TaskList模型的fetchTasks函式以建立此元件的Task模型。

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
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td>
    <ul>
     <li><p>已獲取——任務清單模型 </p></li>
     <li><p>刪除——任務清單模型 </p></li>
     <li><p>updateQueue —— 任務清單模型 </p></li>
     <li><p>refreshedQueue —— 任務清單模型 </p></li>
     <li><p>filterSelected —— 任務清單模型</p></li>
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
     <li><p>欄位：parentView:過濾器清單視圖</p> </li>
     <li><p>欄位：parentModel:任務清單模型</p> </li>
     <li><p>欄位：實用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>聆聽的活動</p> </td>
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
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td>
    <ul>
     <li><p>已獲取——任務清單模型 </p></li>
     <li><p>刪除——任務清單模型 </p></li>
     <li><p>updateQueue —— 任務清單模型 </p></li>
     <li><p>teamQueuesReached - tasklist模型 </p></li>
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
     <li><p>欄位：parentView:過濾器清單視圖</p> </li>
     <li><p>欄位：parentModel:任務清單模型</p> </li>
     <li><p>欄位：實用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>聆聽的活動</p> </td>
   <td><p>不適用</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter獲取指示已從TaskList元件中選擇哪個任務的事件。 雖然這些元件共用模型類，但沒有其它相關性。

## TaskDetails {#taskdetails}

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
     <li><p>表單轉換實用程式</p> </li>
     <li><p>附註實用程式</p> </li>
     <li><p>附件實用程式</p> </li>
     <li><p>taskactions實用程式</p> </li>
     <li><p>歷史實用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p> </td>
   <td>
    <ul>
     <li><p>forwarded —— 任務模型</p> </li>
     <li><p>共用——任務模型</p> </li>
     <li><p>已咨詢——任務模型</p> </li>
     <li><p>拒絕——任務模型</p> </li>
     <li><p>放棄的任務模型</p> </li>
     <li><p>已解鎖——任務模型</p> </li>
     <li><p>鎖定的任務模型</p> </li>
     <li><p>聲明——任務模型</p> </li>
     <li><p>更改：選定任務——任務清單模型</p> </li>
     <li><p>change:formUrl —— 任務模型</p> </li>
     <li>attachmentURLFerketd —— 任務模型</li>
    </ul>
    <ul>
     <li>newAttachment —— 任務模型</li>
     <li><p>taskHistoryReacted —— 任務模型</p> </li>
     <li>prepareForSubmitComplete —— 任務模型</li>
     <li><p>submitComplete —— 任務模型</p> </li>
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
   <td><p>startprocess.html（在route資料夾中）</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>類別</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>favoritecategorfactory模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td>
    <ul>
     <li><p>allStartpointsReacted - categorylist模型 </p></li>
     <li><p>add - categorylist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此元件使用某些其它元件的模型類，如StartPointList、StartPoint和Task。 除了此相依性外，CategoryList還可獨立使用。

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
     <li><p>categorylist模型</p></li>
     <li><p>startpointlist模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td>
    <ul>
     <li><p>changed - category model </p></li>
     <li><p>childrenRecated - category模型 </p></li>
     <li><p>類別：選定——類別清單模型 </p></li>
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
   <td><p>startprocess.html（在route資料夾中）</p></td>
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
     <li><p>favoritecategorfactory模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
     <li><p>startpoint檢視</p></li>
     <li><p>startpointlist模型</p></li>
     <li><p>起點模型</p></li>
     <li><p>任務模型</p></li>
     <li><p>任務模型</p></li>
     <li><p>任務清單模型</p></li>
     <li><p>團隊任務模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td>
    <ul>
     <li><p>類別：選定——類別清單模型 </p></li>
     <li><p>allStartpointsReacted - categorylist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList和CategoryList元件共用模型類，因此前者取決於後者。 CategoryList可存取顯示哪些類別起點的相關資訊。 若要獨立使用StartPointList，請模擬CategoryList中的事件觸發器。

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
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td><p>change - startpoint model </p></td>
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
     <li><p>favoritecategorfactory模型</p> </li>
     <li><p>allcategoryfactory模型</p> </li>
     <li><p>表單轉換實用程式</p> </li>
     <li><p>附註實用程式</p> </li>
     <li><p>附件實用程式</p> </li>
     <li><p>taskactions實用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p> </td>
   <td>
    <ul>
     <li><p>類別：選定——類別清單模型</p> </li>
     <li><p>change:invokedTask - startpointlist模型</p> </li>
     <li><p>change:formUrl —— 任務模型</p> </li>
     <li><p>起點：選定——起點清單模型</p> </li>
     <li><p>forwarded —— 任務模型</p> </li>
     <li><p>放棄的任務模型</p> </li>
     <li><p>已解鎖——任務模型</p> </li>
     <li><p>鎖定的任務模型</p> </li>
     <li>attachmentURLFerketd —— 任務模型</li>
     <li>newAttachment —— 任務模型</li>
     <li>prepareForSubmitComplete —— 任務模型 </li>
     <li><p>submitComplete —— 任務模型</p> </li>
     <li><p>allStartpointsReacted - categorylist模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess和StartPointList元件共用模型類。 從StartPointList中選取起點時，此元件變得相關。

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
   <td><p>tracking.html（在route資料夾中）</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>processname模型</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td>
    <ul>
     <li><p>add - processnamelist模型 </p></li>
     <li><p>已獲取：processnames - processnamelist模型 </p></li>
     <li><p>change - processnamelist model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList不依賴於其他元件。 但是，它在內部取決於ProcessInstanceList模型類，而ProcessInstanceList模型類又取決於其他元件。 因此，ProcessNameList使用許多模型類，如ProcessInstanceList、ProcessInstance、TaskList、Teamtask和Task。 除了這些相依性外，ProcessNameList還可獨立使用。

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
   <td><p>過程實例清單模型</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td><p>change - processname model </p></td>
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
   <td><p>tracking.html（在route資料夾中）</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>processname模型</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td>
    <ul>
     <li><p>processname:selected - processnamelist模型 </p></li>
     <li><p>processname:instancesericated - processnamelist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList需要ProcessNameList中的事件，該事件指示用於讀取和顯示實例的進程名。 若要單獨使用ProcessInstanceList，請分別模擬事件觸發器。

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>processnamelist.js中的processname</p></td>
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
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td><p>change - processinstance model </p></td>
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
     <li><p>processname模型</p></li>
     <li><p>歷史實用程式</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td>
    <ul>
     <li><p>processname:selected - processnamelist模型 </p></li>
     <li><p>processinstance:selected - processinstancelist模型 </p></li>
     <li><p>tasksRechated - processinstance模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory期望ProcessInstanceList中的事件指示要顯示哪個進程實例的歷史記錄。 除了這種依賴性外，該元件還可以獨立使用。

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
   <td><p>用戶搜索視圖</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p> </td>
   <td>
    <ul>
     <li><p>outOfficeSettingsEchated - outofofice模型</p> </li>
     <li><p>outOfOfficeSettingsSaved - outofofice模型</p> </li>
     <li><p>processesReached - outofofice模型</p> </li>
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
   <td><p>用戶搜索視圖</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱——觸發器）</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - sharequeue模型</p> </li>
     <li><p>queueAccessRequested - sharequeue模型</p> </li>
     <li><p>grantedUsersReacted - sharequeue模型</p> </li>
     <li>accessibleUsersReacted - sharequeue模型</li>
     <li><p>queueAccessExpeded - sharequeue模型</p> </li>
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
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td>
    <ul>
     <li><p>preferencesRechated - uisettings模型 </p></li>
     <li><p>settingUpdated - uisettings模型 </p></li>
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
   <td><p>聆聽的活動</p></td>
   <td><p>不適用</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation可以單獨使用。

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
   <td><p>已監聽的事件（事件名稱——觸發器）</p> </td>
   <td>
    <ul>
     <li>userImageUrlRechated - userinfo模型</li>
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
   <td><p>已監聽的事件（事件名稱——觸發器）</p></td>
   <td><p>newWsError - wserror模型 </p></td>
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
   <td><p>已監聽的事件（事件名稱——觸發器）</p> </td>
   <td>
    <ul>
     <li>principalSearch - principalsearch模型</li>
     <li>outOfOfficeInfoRechated - usersearch模型</li>
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
   <td><p>已監聽的事件（事件名稱——觸發器）</p> </td>
   <td><p>templateReacted-searchtemplate模型</p> </td>
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
   <td><p>tracking.html（在route資料夾中）</p> </td>
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
   <td><p>已監聽的事件（事件名稱——觸發器）</p> </td>
   <td><p>change - searchtemplatelist model</p> </td>
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
   <td><p>已監聽的事件（事件名稱——觸發器）</p> </td>
   <td><p>searchTemplate:selected - searchtemplate模型</p> </td>
  </tr>
 </tbody>
</table>

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
