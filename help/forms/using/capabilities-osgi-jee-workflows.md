---
title: OSGi和AEM Forms JEE工作流程中表單中心AEM工作流程的動作和功能
description: OSGi和AEM Forms JEE工作流程中表單中心AEM工作流程的動作和功能
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 22%

---

# OSGi和AEM Forms JEE工作流程中表單中心AEM工作流程的動作和功能 {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM收件匣和HTML工作區 {#aem-inbox-and-html-workspace}

您可以使用AEM收件匣在OSGi上執行和監視以Forms為中心的AEM工作流程。 而HTML Workspace可讓您執行和監視AEM Forms JEE Workflow。 下表可協助您瞭解OSGi上AEM收件匣中，以Forms為中心的AEM工作流程以及AEM Forms JEE工作流程的HTML Workspace中可用的各種重要動作。

<table>
 <tbody>
  <tr>
   <td>動作</td>
   <td>AEM 收件匣</td>
   <td>HTML工作區</td>
  </tr>
  <tr>
   <td>啟動程式、工作或表單應用程式<br /> </td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>提交任務</td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>將任務指派給群組</td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>提交至多個路由</td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>追蹤任務歷史記錄和任務摘要</td>
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
   <td>行事曆檢視</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>任務層級註解</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>佇列（共用的個人佇列、來自佇列的索賠工作）</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>休假通知</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
    <tr>
   <td>自訂UI元素</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>將任務指派給多位使用者</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
 </tbody>
</table>

## OSGi和AEM Forms JEE工作流程上的表單中心AEM工作流程 {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi和AEM Forms JEE Workflows (JEE流程管理上的AEM Forms)以表單為中心的AEM Workflow有一組不同的功能。 下表可協助您瞭解OSGi和AEM Forms on JEE Workflow中表單中心AEM工作流程可用的重要功能：

<table>
 <tbody>
  <tr>
   <td>功能</td>
   <td>OSGi上的表單中心AEM工作流程<br /> </td>
   <td>AEM Forms JEE工作流程</td>
  </tr>
  <tr>
   <td>最適化表單</td>
   <td>支援</td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>與其他AEM解決方案的整合</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>草寫簽名</td>
   <td>支援</td>
   <td>支援<br />。 </td>
  </tr>
  <tr>
   <td>自訂電子郵件範本</td>
   <td>支援</td>
   <td>支援<br />。 </td>
  </tr>
  <tr>
   <td>定義任務優先順序</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>任務在到期日後逾時</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>工作流程中的回圈</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>動態選擇被指定者 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>使用自訂中繼資料</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>電子簽章(Adobe Sign)</td>
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
   <td>將已完成的任務演算為最適化表單或PDF檔案</td>
   <td>支援</td>
   <td>支援 [4]</td>
  </tr>
  <tr>
   <td>與通訊管理整合</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
   <tr>
   <td>閘道，不等待 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
   <tr>
   <td>儲存資料的變數 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>OR， AND拆分</td>
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
   <td>唯讀調適型表單</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>隱藏預設儲存按鈕</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>管理工作流程詳細資訊區段的精細控制</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>輪詢/排程服務</td>
   <td>立即可用</td>
   <td>需要自訂實施</td>
  </tr>
  <tr>
   <td>最適化Forms應用程式</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>組合器服務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>PDF Generator服務</td>
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
   <td>HTML5 Forms、互動式PDF forms、表單集</td>
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
   <td>起點類別</td>
   <td>不支援 </td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>大量任務核准 </td>
   <td>不支援 </td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>使用自訂名稱儲存草稿</td>
   <td>不支援 </td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>使用現有流程資料起始流程<br /> </td>
   <td>不支援</td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>將起點儲存為草稿</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>管理員檢視</td>
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
   <td>工作流程應用程式或起點的任務層級附件</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>提醒電子郵件</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>在任務逾時時變更標題</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>關於任務委派和任務宣告的電子郵件</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>委託於不相交群組之間</td>
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

1. 您可以在OSGi上使用以表單為中心的AEM工作流程，以簽署已填的最適化表單。 OSGi上的以表單為中心的AEM工作流程支援表單以外的簽名。 此 [表單內簽署](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) 不支援體驗。

1. 您需要存取AEM收件匣，才能在AEM Forms OSGi和HTML Workspace上執行和監視以表單為中心的工作流程，以執行和監視AEM Forms JEE工作流程。
1. 原生AEM Forms檔案服務適用於OSGi上的表單中心AEM工作流程和JEE工作流程上的AEM Forms 。 AEM Workflow在OSGi和AEM Forms JEE （流程管理）工作流程中，使用原生檔案服務進行以表單為中心的AEM工作流程。
1. AEM Forms JEE工作流程只能轉譯最適化表單。 不支援將最適化表單轉譯為PDF檔案。
1. AEM forms JEE Workflow沒有適用於Adobe Sign的個別步驟。 您需要啟用Adobe Sign的最適化表單以用於AEM Forms JEE工作流程。 如需詳細資訊，請參閱 [Adobe Sign檔案](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. 您可以使用 [啟動表單資料模型服務](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) 啟動網站服務並從協力廠商應用程式張貼或擷取資料的步驟。
1. 您可以使用 [傳送電子郵件](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) 步驟以傳送電子郵件。

## AEM收件匣與AEM Forms應用程式功能之間的差異 {#differences-between-aem-inbox-and-aem-forms-app-features}

啟動以Forms為中心的工作流程的兩個顯著方法是使用 [AEM收件匣](../../forms/using/manage-applications-inbox.md) 和AEM Forms應用程式。 不過，AEM收件匣和AEM Forms應用程式的功能有所不同。 AEM收件匣僅適用於 [以Forms為中心的工作流程](../../forms/using/aem-forms-workflow.md) 而AEM Forms應用程式可搭配以Forms為中心的工作流程以及程式管理。

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
   <td><p>追蹤任務歷史記錄和任務摘要</p> </td>
   <td><p>支援</p> </td>
   <td><p>不支援</p> </td>
  </tr>
  <tr>
   <td><p>新增工作層級附件</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>檢視工作層次附件</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>新增欄位層級附件</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>顯示行事曆檢視</p> </td>
   <td><p>支援</p> </td>
   <td><p>不支援</p> </td>
  </tr>
  <tr>
   <td><p>新增註解</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
 </tbody>
</table>
