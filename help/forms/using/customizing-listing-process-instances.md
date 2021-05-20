---
title: 自定義進程實例清單
seo-title: 自定義進程實例清單
description: 在AEM Forms工作區中自訂處理例項中顯示屬性的方式。
seo-description: 在AEM Forms工作區中自訂處理例項中顯示屬性的方式。
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
exl-id: b27ffe92-8491-43a0-bf42-613eb39a606e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---

# 自定義進程實例清單{#customizing-the-listing-of-process-instances}

程式例項清單會顯示在AEM Forms工作區的「追蹤」標籤中。

在程式例項清單中，AEM Forms工作區會針對每個程式例項顯示該例項的某些屬性。 每個進程實例均可使用以下屬性。 這些屬性在進程實例元件模型中儲存為屬性，並可在其視圖和模板中使用。

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
   <td>發起人</td>
   <td>進程實例的啟動器名稱。</td>
  </tr>
  <tr>
   <td>initiatorId</td>
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
   <td>0 =起始<br /> 1 =運行<br /> 2 =完成<br /> 3 =完成<br /> 4 =終止<br /> 5 =終止<br /> 6 =暫停<br /> 7 =暫停<br /> 8 =取消暫停</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>程式名稱。</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>進程啟動時的時間戳。</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>進程變數的對象陣列。 每個進程變數對象都包含<strong>name</strong>（進程變數的名稱）、<strong>value</strong>（進程變數的值）和<strong> type</strong>（進程變數的類型）。</td>
  </tr>
 </tbody>
</table>

**範例:**

要在進程實例卡中顯示進程實例的`description`屬性，請執行以下步驟。

1. 請依照[AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md)操作。
1. 請執行下列動作：

   1. 將/libs/ws/js/runtime/templates/processinstance.html複製到/apps/ws/js/runtime/templates/（如果不存在）。 按一下「**全部保存**」。
   1. 在inprocessinstance.html中新增含有class = &#39;processDescription&#39;的程式說明div。

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 請執行下列動作：

   1. 開啟/apps/ws/js/registry.js進行編輯。
   1. 搜尋並將`text!/lc/libs/ws/js/runtime/templates/processinstance.html`取代為&#x200B;`text!/lc/`**apps**/ws/js/runtime/templates/processinstance.html。

1. 以上變更可能需要更新CSS檔案，方法是在樣式表/apps/ws/css/newStyle.css中新增項目，方法如下：

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
