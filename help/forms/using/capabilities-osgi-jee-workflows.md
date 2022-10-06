---
title: OSGi和AEM Forms JEE工作流程上以表單為中心的AEM工作流程的動作和功能
description: OSGi和AEM Forms JEE工作流程上以表單為中心的AEM工作流程的動作和功能
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 22%

---

# OSGi和AEM Forms JEE工作流程上以表單為中心的AEM工作流程的動作和功能 {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM收件匣和HTML工作區 {#aem-inbox-and-html-workspace}

您可以使用AEM收件匣，在OSGi上執行和監控以Forms為中心的AEM工作流程。 而HTML工作區可讓您執行和監控AEM Forms JEE工作流程。 下表可協助您了解OSGi上以AEM為中心的AEM工作流程的Forms收件匣，以及AEM Forms JEE工作流程的HTML工作區中提供的各種重要動作。

<table>
 <tbody>
  <tr>
   <td>動作</td>
   <td>AEM 收件匣</td>
   <td>HTML工作區</td>
  </tr>
  <tr>
   <td>啟動進程、任務或表單應用程式<br /> </td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>提交任務</td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>為組分配任務</td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>向多條路由提交</td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>跟蹤任務歷史記錄和任務摘要</td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>電子郵件通知</td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>重新指派任務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>適用性表單的欄位層級附件</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>日曆檢視</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>任務級注釋</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>隊列（共用的個人隊列，來自隊列的聲明任務）</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>離職通知</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
    <tr>
   <td>自訂UI元素</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>將任務分配給多個用戶</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
 </tbody>
</table>

## OSGi和AEM Forms JEE工作流程上的表單導向AEM工作流程 {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi和AEM Forms JEE工作流程上的表單導向AEM工作流程(JEE流程管理上的AEM Forms)有不同的功能集。 下表可協助您了解OSGi和JEE上AEM Forms的表單導向AEM工作流程中提供的重要功能：

<table>
 <tbody>
  <tr>
   <td>功能</td>
   <td>OSGi上以表單為中心的AEM工作流程<br /> </td>
   <td>AEM Forms JEE工作流程</td>
  </tr>
  <tr>
   <td>調適型表單</td>
   <td>支援</td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>與其他AEM解決方案整合</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>草寫簽名</td>
   <td>支援</td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>自訂電子郵件範本</td>
   <td>支援</td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>定義任務優先順序</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>在到期日後超時任務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>工作流程內的回圈</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>動態選擇受託人 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>使用自訂中繼資料</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>電子簽名(Adobe Sign)</td>
   <td>支援 <sup>[1]</sup></td>
   <td>支援 <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>管理任務和表單應用程式</td>
   <td>支援 <sup>[2]</sup><br /> </td>
   <td>支援 <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>文件服務</td>
   <td>支援 <sup>[3]</sup></td>
   <td>支援 <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>將完成的任務呈現為最適化表單或PDF文檔</td>
   <td>支援</td>
   <td>支援 [4]</td>
  </tr>
  <tr>
   <td>與通信管理整合</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
   <tr>
   <td>網關，無等待 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
   <tr>
   <td>儲存資料的變數 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>或，並分割</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>使用者頭像</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>在工作流程結束時傳送電子郵件</td>
   <td>支援 <sup>[7]</sup></td>
   <td>支援</td>
  </tr>
  <tr>
   <td>從工作流程呼叫Web服務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>數位簽章</td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>重設按鈕</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>工作流程階段</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>唯讀適用性表單</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>隱藏預設的儲存按鈕</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>對工作流程詳細資訊區段的精細控制</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>輪詢/排程服務</td>
   <td>現成可用</td>
   <td>需要自訂實作</td>
  </tr>
  <tr>
   <td>適用性Forms應用程式</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>組合器服務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>PDF產生器服務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>Forms 服務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>輸出服務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>檔案保證</td>
   <td>支援</td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>執行指令碼</td>
   <td>支援ECMAScript</td>
   <td>支援Java程式碼片段</td>
  </tr>
  <tr>
   <td>組合器</td>
   <td>支援</td>
   <td>支援</td>
  </tr>  
  <tr>
   <td>HTML5 Forms，互動式PDF forms，表單集</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>程序報告</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>數位簽章</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>起始點類別</td>
   <td>不支援 </td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>批量任務批准 </td>
   <td>不支援 </td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>以自訂名稱儲存草稿</td>
   <td>不支援 </td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>使用現有流程資料啟動流程<br /> </td>
   <td>不支援</td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>將起始點另存為草稿</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>管理器視圖</td>
   <td>不支援</td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>搜尋範本</td>
   <td>不支援</td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>與協力廠商應用程式整合</td>
   <td>不支援 <sup>[6]</sup></td>
   <td>支援</td>
  </tr>
  <tr>
   <td>工作流應用程式或起始點的任務級附件</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>提醒電子郵件</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>更改任務超時的標題</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>關於任務委派和任務聲明的電子郵件</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>不相交的團體之間的委派</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>XSLT轉換</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>動態任務優先順序</td>
   <td>不支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>動態標題</td>
   <td>不支援</td>
   <td>不支援</td>
  </tr>
    <tr>
   <td>動態說明</td>
   <td>不支援</td>
   <td>不支援</td>
  </tr>
 </tbody>
</table>

1. 您可以在OSGi上使用表單導向的AEM工作流程來簽署已填入的最適化表單。 OSGi上以表單為中心的AEM工作流程支援表單簽署功能。 此 [表單內簽署](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) 不支援體驗。

1. 您需要存取AEM收件匣，才能在AEM Forms OSGi上執行和監控表單中心工作流程，並需要HTML工作區來執行和監控AEM Forms JEE工作流程。
1. 原生AEM Forms檔案服務適用於OSGi上的表單導向AEM工作流程和JEE上的AEM Forms工作流程。 AEM Workflow(在OSGi和AEM Forms JEE（流程管理）工作流程上，使用以表單為中心的AEM Workflows（原生檔案服務）。
1. AEM Forms JEE工作流程只能轉譯最適化表單。 不支援將最適化表單轉譯為PDF檔案。
1. AEM forms JEE工作流程沒有針對Adobe Sign的個別步驟。 您需要已啟用Adobe Sign的AEM Forms JEE工作流程適用性表單。 如需詳細資訊，請參閱 [Adobe Sign檔案](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. 您可以使用 [調用表單資料模型服務](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) 調用web服務並發佈或檢索來自第三方應用程式的資料的步驟。
1. 您可以使用 [傳送電子郵件](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) 傳送電子郵件的步驟。

## AEM收件匣和AEM Forms應用程式功能之間的差異 {#differences-between-aem-inbox-and-aem-forms-app-features}

啟動以Forms為中心的工作流程的兩種主要方式為 [AEM收件匣](../../forms/using/manage-applications-inbox.md) 和AEM Forms應用程式。 不過，AEM收件匣和AEM Forms應用程式的功能則有所不同。 AEM收件匣僅適用於 [Forms工作流程](../../forms/using/aem-forms-workflow.md) 而AEM Forms應用程式可搭配以Forms為中心的工作流程和程式管理運作。

下表列出AEM收件匣和AEM Forms應用程式的功能：

<table>
 <tbody>
  <tr>
   <td><p><strong>動作</strong></p> </td>
   <td><p><strong>AEM 收件匣</strong></p> </td>
   <td><p><strong>AEM Forms 應用程式</strong></p> </td>
  </tr>
  <tr>
   <td><p>啟動表單應用程式</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>提交任務</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>委派任務</p> </td>
   <td><p>支援</p> </td>
   <td><p>不支援</p> </td>
  </tr>
  <tr>
   <td><p>跟蹤任務歷史記錄和任務摘要</p> </td>
   <td><p>支援</p> </td>
   <td><p>不支援</p> </td>
  </tr>
  <tr>
   <td><p>添加任務級附件</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>查看任務級附件</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>添加欄位級附件</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>顯示日曆檢視</p> </td>
   <td><p>支援</p> </td>
   <td><p>不支援</p> </td>
  </tr>
  <tr>
   <td><p>添加註釋</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
 </tbody>
</table>
