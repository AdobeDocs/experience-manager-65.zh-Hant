---
title: 可重用元件的說明
seo-title: Description of reusable components
description: 包含檔案名和依賴項的可重用元件的完整清單，可幫助您將AEM Forms工作區元件整合到Web應用程式中。
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

# 可重用元件的說明 {#description-of-reusable-components}

AEM Forms工作區由 [可重用](/help/forms/using/integrating-html-ws-components-web.md) 組織成特定元件 [資料夾結構](/help/forms/using/folder-structure.md) 在CRX™中。 每個元件都在資料夾結構中指定的位置具有模型、視圖和模板檔案、JavaScript™對其他元件檔案的依賴關係、元件偵聽的事件以及在AEM Forms工作區中觸發這些事件的JavaScript對象。 此處提供了包含組成檔案名和依賴項的可重用元件的完整清單。

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
     <li><p>用戶搜索</p></li>
     <li><p>任務</p></li>
     <li><p>團隊任務</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>JS依賴項</p></td>
   <td>
    <ul>
     <li><p>任務模型</p></li>
     <li><p>團隊任務模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>filterSelected — 任務清單模型</p></li>
     <li><p>刪除 — 任務清單模型</p></li>
     <li><p>updateQueue — 任務清單模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此元件可以獨立於AEM Forms工作區使用，前提是您從自定義應用程式中觸發此元件的filterSelected事件。

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
   <td><p>JS依賴項</p></td>
   <td>
    <ul>
     <li><p>任務清單模型</p></li>
     <li><p>taskactions實用程式</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
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
>工作區調用TaskList模型的fetchTasks函式為此元件建立Task模型。

## 篩選器清單 {#filterlist}

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
   <td><p>JS依賴項</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>已提取 — 任務清單模型 </p></li>
     <li><p>刪除 — 任務清單模型 </p></li>
     <li><p>updateQueue — 任務清單模型 </p></li>
     <li><p>refreshedQueue — 任務清單模型 </p></li>
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
   <td><p>JS依賴項</p> </td>
   <td>
    <ul>
     <li><p>欄位：隊列：{ name, qid, isDefault, type}</p> </li>
     <li><p>欄位：查詢：字串</p> </li>
     <li><p>欄位：父視圖：過濾器清單視圖</p> </li>
     <li><p>欄位：parentModel:任務清單模型</p> </li>
     <li><p>欄位：實用</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已聽取的事件</p> </td>
   <td><p>不適用</p> </td>
  </tr>
 </tbody>
</table>

## 團隊隊列 {#teamqueues}

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
   <td><p>JS依賴項</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>已提取 — 任務清單模型 </p></li>
     <li><p>刪除 — 任務清單模型 </p></li>
     <li><p>updateQueue — 任務清單模型 </p></li>
     <li><p>teamQueuesEchidd — 任務清單模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## 團隊篩選器 {#teamfilter}

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
   <td><p>JS依賴項</p> </td>
   <td>
    <ul>
     <li><p>擴展：篩選器視圖</p> </li>
     <li><p>欄位：隊列：{ name, qid, isDefault, type }</p> </li>
     <li><p>欄位：查詢：字串</p> </li>
     <li><p>欄位：父視圖：過濾器清單視圖</p> </li>
     <li><p>欄位：parentModel :任務清單模型</p> </li>
     <li><p>欄位：實用</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已聽取的事件</p> </td>
   <td><p>不適用</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter獲取指示從TaskList元件中選擇的任務的事件。 雖然這些元件共用模型類，但沒有其他依賴關係。

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
   <td><p>JS依賴項</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>賦形實用程式</p> </li>
     <li><p>注釋實用程式</p> </li>
     <li><p>附件實用程式</p> </li>
     <li><p>taskactions實用程式</p> </li>
     <li><p>歷史實用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>已轉發 — 任務模型</p> </li>
     <li><p>共用 — 任務模型</p> </li>
     <li><p>已咨詢 — 任務模型</p> </li>
     <li><p>拒絕 — 任務模型</p> </li>
     <li><p>放棄 — 任務模型</p> </li>
     <li><p>已解鎖 — 任務模型</p> </li>
     <li><p>鎖定 — 任務模型</p> </li>
     <li><p>聲明 — 任務模型</p> </li>
     <li><p>更改：任務選定 — 任務清單模型</p> </li>
     <li><p>change:formUrl — 任務模型</p> </li>
     <li>附件URLFetd — 任務模型</li>
    </ul>
    <ul>
     <li>newAttachment — 任務模型</li>
     <li><p>taskHistoryRected — 任務模型</p> </li>
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
   <td><p>JS依賴項</p></td>
   <td>
    <ul>
     <li><p>收藏夾工廠模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFicted - categorylist模型 </p></li>
     <li><p>添加 — 類別清單模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此元件使用某些其他元件（如StartPointList、StartPoint和Task）的模型類。 除此依賴項外，CategoryList可獨立使用。

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
   <td><p>JS依賴項</p></td>
   <td>
    <ul>
     <li><p>類別清單模型</p></li>
     <li><p>起始點清單模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>更改 — 類別模型 </p></li>
     <li><p>childrenEcted — 類別模型 </p></li>
     <li><p>類別：選定 — 類別清單模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## 起點清單 {#startpointlist}

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
   <td><p>JS依賴項</p></td>
   <td>
    <ul>
     <li><p>類別模型</p></li>
     <li><p>收藏夾工廠模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
     <li><p>起始點視圖</p></li>
     <li><p>起始點清單模型</p></li>
     <li><p>起始點模型</p></li>
     <li><p>任務模型</p></li>
     <li><p>任務模型</p></li>
     <li><p>任務清單模型</p></li>
     <li><p>團隊任務模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>類別：選定 — 類別清單模型 </p></li>
     <li><p>allStartpointsFicted - categorylist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList和CategoryList元件共用模型類，因此前者依賴於後者。 CategoryList訪問有關顯示哪個類別起始點的資訊。 要獨立使用StartPointList，請從CategoryList模擬事件觸發器。

## 起點 {#startpoint}

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
   <td><p>JS依賴項</p></td>
   <td><p>任務模型</p></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>更改 — 起始點模型 </p></td>
  </tr>
 </tbody>
</table>

## 啟動進程 {#startprocess}

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
     <li><p>用戶搜索</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JS依賴項</p> </td>
   <td>
    <ul>
     <li><p>類別模型</p> </li>
     <li><p>收藏夾工廠模型</p> </li>
     <li><p>allcategoryfactory模型</p> </li>
     <li><p>賦形實用程式</p> </li>
     <li><p>注釋實用程式</p> </li>
     <li><p>附件實用程式</p> </li>
     <li><p>taskactions實用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>類別：選定 — 類別清單模型</p> </li>
     <li><p>change:invokedTask -startpointlist模型</p> </li>
     <li><p>change:formUrl — 任務模型</p> </li>
     <li><p>起始點：選定 — 起始點清單模型</p> </li>
     <li><p>已轉發 — 任務模型</p> </li>
     <li><p>放棄 — 任務模型</p> </li>
     <li><p>已解鎖 — 任務模型</p> </li>
     <li><p>鎖定 — 任務模型</p> </li>
     <li>附件URLFetd — 任務模型</li>
     <li>newAttachment — 任務模型</li>
     <li>prepareForSubmitComplete — 任務模型 </li>
     <li><p>submitComplete — 任務模型</p> </li>
     <li><p>allStartpointsFicted - categorylist模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess和StartPointList元件共用模型類。 此元件將變得相關，您可以從StartPointList中選擇起點。

## 進程名稱清單 {#processnamelist}

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
   <td><p>JS依賴項</p></td>
   <td><p>進程名模型</p></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>添加 — 進程名清單模型 </p></li>
     <li><p>獲取的：進程名稱 — 進程名表模型 </p></li>
     <li><p>更改 — 進程名稱清單模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList不依賴於其他元件。 但是，在內部，它取決於ProcessInstanceList模型類，而ProcessInstanceList模型類又取決於其他元件。 因此，ProcessNameList使用許多模型類，如ProcessInstanceList、ProcessInstance、TaskList、Teamtask和Task。 除了這些依賴項外，ProcessNameList還可以獨立使用。

## 進程名 {#processname}

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
   <td><p>JS依賴項</p></td>
   <td><p>過程實例清單模型</p></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>更改 — 進程名模型 </p></td>
  </tr>
 </tbody>
</table>

## 進程實例清單 {#processinstancelist}

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
   <td><p>JS依賴項</p></td>
   <td><p>進程名模型</p></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>進程名稱：選定 — 進程名稱清單模型 </p></li>
     <li><p>processname（進程名稱）：實例提取 — 進程名稱清單模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList需要ProcessNameList中的事件，該事件指示用於讀取和顯示實例的進程名稱。 要獨立使用ProcessInstanceList，請單獨模擬事件觸發器。

## 進程實例 {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>檢視</p></td>
   <td><p>進程名稱在processnamelist中</p></td>
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
   <td><p>JS依賴項</p></td>
   <td><p>任務清單模型</p></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>更改 — 流程實例模型 </p></td>
  </tr>
 </tbody>
</table>

## 進程實例歷史記錄 {#processinstancehistory}

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
   <td><p>JS依賴項</p></td>
   <td>
    <ul>
     <li><p>進程名模型</p></li>
     <li><p>歷史實用程式</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>進程名稱：選定 — 進程名稱清單模型 </p></li>
     <li><p>進程實例：選定 — 進程實例清單模型 </p></li>
     <li><p>tasksRected — 進程實例模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory需要ProcessInstanceList中的事件，該事件指示要顯示哪個進程實例的歷史記錄。 除此依賴外，元件可獨立使用。

## 外部 {#outofoffice}

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
   <td><p>用戶搜索</p> </td>
  </tr>
  <tr>
   <td><p>JS依賴項</p> </td>
   <td><p>用戶搜索視圖</p> </td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>outOfficeSettingsEctidd — 外出模型</p> </li>
     <li><p>outOfficeSettingsSaved — 外出模型</p> </li>
     <li><p>processesRected — 出站模型</p> </li>
     <li><p>principalSelected - principalsearch視圖</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice可獨立使用。

## 共用隊列 {#sharequeue}

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
   <td><p>用戶搜索</p> </td>
  </tr>
  <tr>
   <td><p>JS依賴項</p> </td>
   <td><p>用戶搜索視圖</p> </td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGreated — 共用隊列模型</p> </li>
     <li><p>queueAccessRequested — 共用隊列模型</p> </li>
     <li><p>greadedUsersEchidd — 共用隊列模型</p> </li>
     <li>accessibleUsersEchidd — 共用隊列模型</li>
     <li><p>queueAccessReveded — 共用隊列模型</p> </li>
     <li><p>queueAccessRemoved — 共用隊列模型</p> </li>
     <li><p>principalSelected - principalsearch視圖</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue可以獨立使用。

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
   <td><p>JS依賴項</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>首選項已獲取 — 合併模型 </p></li>
     <li><p>settingUpdated - Uisettings模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings可以獨立使用。

## 應用導航 {#appnavigation}

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
   <td><p>JS依賴項</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>已聽取的事件</p></td>
   <td><p>不適用</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation可以獨立使用。

## 用戶資訊 {#userinfo}

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
   <td><p>JS依賴項</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li>userImageUrlEchitd - userinfo模型</li>
     <li>sessionRenewed - userinfo模型 <br /> </li>
     <li>sessionExpired — 用戶資訊模型 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo可以獨立使用。

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
   <td><p>JS依賴項</p></td>
   <td><p>不適用</p></td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>newWsError - wserror模型 </p></td>
  </tr>
 </tbody>
</table>

## 用戶搜索 {#usersearch}

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
   <td><p>JS依賴項</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li>principalSearch - principalsearch模型</li>
     <li>outOfOfficeInfoEctidd — 用戶搜索模型</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 搜索模板 {#searchtemplate}

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
   <td><p>JS依賴項</p> </td>
   <td><p>不適用</p> </td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p> </td>
   <td><p>templateRecated-searchtemplate模型</p> </td>
  </tr>
 </tbody>
</table>

## 搜索模板清單 {#searchtemplatelist}

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
   <td><p>JS依賴項</p> </td>
   <td><p>searchtemplate模型</p> </td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p> </td>
   <td><p>更改 — 搜索模板清單模型</p> </td>
  </tr>
 </tbody>
</table>

## 搜索模板詳細資訊 {#searchtemplatedetails}

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
   <td><p>JS依賴項</p> </td>
   <td>不適用<br /> </td>
  </tr>
  <tr>
   <td><p>偵聽的事件（事件名稱 — 觸發器）</p> </td>
   <td><p>searchTemplate:selected -searchtemplate模型</p> </td>
  </tr>
 </tbody>
</table>
