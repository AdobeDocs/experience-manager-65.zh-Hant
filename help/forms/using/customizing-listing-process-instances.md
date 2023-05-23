---
title: 自定義進程實例清單
seo-title: Customizing the listing of process instances
description: How-to自定義在AEM Forms工作區中的進程實例中顯示的屬性。
seo-description: How-to customize the properties displayed in process instance in AEM Forms workspace.
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
exl-id: b27ffe92-8491-43a0-bf42-613eb39a606e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 3%

---

# 自定義進程實例清單 {#customizing-the-listing-of-process-instances}

進程實例清單顯示在AEM Forms工作區的「跟蹤」(Tracking)頁籤中。

在進程實例清單中，對於每個進程實例，AEM Forms工作區顯示該實例的某些屬性。 以下屬性可用於每個進程實例。 這些屬性作為屬性儲存在流程實例元件模型中，並可在其視圖和模板中使用。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>說明</td>
   <td>流程實例的說明。</td>
  </tr>
  <tr>
   <td>啟動器</td>
   <td>進程實例的啟動器名稱。</td>
  </tr>
  <tr>
   <td>啟動器ID</td>
   <td>進程實例的啟動器ID。</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>進程完成時的時間戳。</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>進程實例的ID。</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 =啟動<br /> 1 =正在運行<br /> 2 =完成<br /> 3 =完成<br /> 4 =終止<br /> 5 =終止<br /> 6 =暫停<br /> 7 =掛起<br /> 8 =取消掛起</td>
  </tr>
  <tr>
   <td>進程名</td>
   <td>進程的名稱。</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>進程啟動時的時間戳。</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>進程變數的對象陣列。 每個進程變數對象都包含 <strong>名稱</strong> （進程變數的名稱）, <strong>值</strong> （進程變數的值），和<strong> 類型</strong> （進程變數的類型）。</td>
  </tr>
 </tbody>
</table>

**範例:**

顯示 `description` 進程實例卡中進程實例的屬性，請執行以下步驟。

1. 關注 [AEM Forms工作區定製的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 請執行下列動作：

   1. 將/libs/ws/js/runtime/templates/processinstance.html複製到/apps/ws/js/runtime/templates/（如果它不存在）。 按一下 **全部保存**。
   1. 在processinstance.html中添加具有類=「processDescription」的進程說明div。

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 請執行下列動作：

   1. 開啟/apps/ws/js/registry.js進行編輯。
   1. 搜索和替換 `text!/lc/libs/ws/js/runtime/templates/processinstance.html`與 `text!/lc/`**應用**/ws/js/runtime/templates/processinstance.html。

1. 通過以下方式在樣式表/apps/ws/css/newStyle.css中添加一個條目，上述更改可能需要更新CSS檔案：

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
