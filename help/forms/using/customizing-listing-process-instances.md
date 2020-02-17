---
title: 自定義流程實例清單
seo-title: 自定義流程實例清單
description: How-to customize the properties displayed in process instance in AEM Forms workspace.
seo-description: How-to customize the properties displayed in process instance in AEM Forms workspace.
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 自定義流程實例清單 {#customizing-the-listing-of-process-instances}

流程例項清單會顯示在AEM Forms工作區的「追蹤」標籤中。

在流程例項清單中，對於每個流程例項，AEM Forms工作區會顯示該例項的某些屬性。 以下屬性適用於每個進程實例。 這些屬性作為屬性儲存在進程實例元件模型中，可用於其視圖和模板中。

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
   <td>initiatorId</td>
   <td>進程實例的啟動器ID。</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>流程完成時的時間戳記。</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>進程實例的ID。</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 =已啟動<br /> 1 =運行<br /> 2 =完成3 =完成<br /> 4 =終止<br /> 5 =終止6 =暫停7 =暫停<br /><br /><br /><br /> 8 =取消暫停</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>進程的名稱。</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>進程啟動時的時間戳記。</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>流程變數的對象陣列。 每個流程變數 <strong>對象都包含</strong> name <strong>（流程變數的名稱）、</strong> value<strong> （流程變數的值）和type</strong> （流程變數的類型）。</td>
  </tr>
 </tbody>
</table>

**範例:**

要在流程 `description` 實例卡中顯示流程實例的屬性，請執行以下步驟。

1. 請遵循「 [AEM Forms工作區自訂的一般步驟」](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 執行下列動作：

   1. 複製/libs/ws/js/runtime/templates/processinstance.html至/apps/ws/js/runtime/templates/（如果不存在）。 按一下「 **全部儲存**」。
   1. 添加進程說明div，其類= &#39;processDescription&#39; inprocessinstance.html。

   ```
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 執行下列動作：

   1. 開啟/apps/ws/js/registry.js進行編輯。
   1. 以應用程式 `text!/lc/libs/ws/js/runtime/templates/processinstance.html`/ws/js/runtime/templates/processinstance.html搜尋 `text!/lc/`**並取&#x200B;**代。

1. 以上變更可能需要以下列方式在樣式表/apps/ws/css/newStyle.css中新增項目，以更新CSS檔案：

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
