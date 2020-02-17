---
title: OSGi和AEM Forms JEE工作流程中表單導向AEM工作流程的動作和功能
seo-title: OSGi和AEM Forms JEE工作流程中表單導向AEM工作流程的動作和功能
description: 'null'
seo-description: 'null'
uuid: 8af9527d-fa5e-4fcb-88e1-49571528fca6
contentOwner: khsingh
topic-tags: publish
discoiquuid: 89bcc76d-122f-4a3f-b857-16e5376e1624
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe

---


# OSGi和AEM Forms JEE工作流程中表單導向AEM工作流程的動作和功能 {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM收件匣和HTML工作區 {#aem-inbox-and-html-workspace}

AEM Inbox可用來在OSGi上執行和監控以表單為中心的AEM工作流程。 HTML工作區可讓您執行和監視AEM Forms JEE工作流程。 下表列出OSGi上的「AEM Inbox for Forms-centric AEM Workflows」和「AEM Forms JEE Workflows的HTML Workspace」中可用的重要動作。

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
   <td>將任務分配給組</td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>提交到多條路由</td>
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
   <td>重新指派工作</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>適應性表單的欄位層級附件</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>日曆檢視</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>任務級別注釋</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>隊列（共用的個人隊列，從隊列中聲明任務）</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>離職通知</td>
   <td>不支援</td>
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

OSGi和AEM Forms JEE的表單導向AEM工作流程(AEM Forms on JEE Process Management)有不同的功能集。 下表列出OSGi和AEM Forms on JEE Workflows中以表單為中心的AEM Workflows的重要功能與支援：

<table>
 <tbody>
  <tr>
   <td>功能</td>
   <td>OSGi上的表單導向AEM工作流程<br /> </td>
   <td>AEM Forms JEE工作流程</td>
  </tr>
  <tr>
   <td>適用性表單</td>
   <td>支援</td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>與其他AEM解決方案整合</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>（已過時）塗鴉簽名</td>
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
   <td>到期日後超時任務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>工作流程中的回圈</td>
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
   <td>支援 <sup>的[1]</sup></td>
   <td>支援 <sup>的[5]</sup></td>
  </tr>
  <tr>
   <td>管理任務和表單應用程式</td>
   <td>支援 <sup>的[2]</sup><br /> </td>
   <td>支援 <sup>的[2]</sup></td>
  </tr>
  <tr>
   <td>檔案服務</td>
   <td>支援 <sup>的[3]</sup></td>
   <td>支援 <sup>的[3]</sup></td>
  </tr>
  <tr>
   <td>將完成的工作演算為最適化表單或PDF檔案</td>
   <td>支援</td>
   <td>支援[4]</td>
  </tr>
  <tr>
   <td>與信件管理整合</td>
   <td>支援</td>
   <td>支援</td>
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
   <td>唯讀可調式表單</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>隱藏預設保存按鈕</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>詳細控制工作流程詳細資訊區段</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>HTML5表格、互動式PDF表格、表格集<br /> </td>
   <td>Not Supported<br /> </td>
   <td>支援</td>
  </tr>
  <tr>
   <td>流程報告</td>
   <td>Not Supported<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>數位簽章</td>
   <td>支援<br /> </td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>起點類別</td>
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
   <td>將起點另存為草稿</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>使用者頭像</td>
   <td>支援</td>
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
   <td>Not Supported <sup>[6]</sup></td>
   <td>支援</td>
  </tr>
  <tr>
   <td>工作流應用程式或起點的任務級附件</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>提醒電子郵件</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>變更任務逾時的標題</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>關於任務委派和任務聲明的電子郵件</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>在工作流程結束時傳送電子郵件</td>
   <td>支援 <sup>的[7]</sup></td>
   <td>支援</td>
  </tr>
  <tr>
   <td>分散團體之間的委派</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>從工作流程呼叫Web服務</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>XSLT轉換</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>網關，無等待 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>或，並分割</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>動態任務優先順序</td>
   <td>不支援</td>
   <td>不支援</td>
  </tr>
 </tbody>
</table>

1. 您可以在OSGi上使用表單導向的AEM工作流程來簽署已填妥的最適化表單。 OSGi上的表單導向AEM工作流程支援表單簽署。 不 [支援表單簽署](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) 。

1. 您需要存取AEM Inbox才能執行和監視AEM Forms OSGi AEM Workflows和HTML Workspace，以執行和監視AEM Forms JEE Workflows。
1. 原生AEM Forms Document services適用於OSGi上的表單導向AEM工作流程和JEE工作流程上的AEM Forms。 AEM Workflow使用原生檔案服務，在OSGi和AEM Forms JEE（流程管理）工作流程中使用表單導向的AEM工作流程。
1. AEM Forms JEE Workflows只能轉譯最適化表單。 它不支援將最適化表單轉換為PDF檔案。
1. AEM表單JEE工作流程沒有Adobe Sign的個別步驟。 您需要AEM表單JEE工作流程中啟用Adobe Sign的最適化表單。 如需詳細資訊，請參 [閱Adobe Sign檔案](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)。
1. 您可以使用「調 [用表單資料模型服務](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) 」步驟來叫用web-service服務，並張貼或擷取第三方應用程式的資料。
1. 您可以使用「傳送 [電子郵件](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) 」步驟來傳送電子郵件。

## AEM Inbox和AEM Forms應用程式功能的差異 {#differences-between-aem-inbox-and-aem-forms-app-features}

啟動「表單導向」工作流程的兩種主要方式是使用 [AEM Inbox](../../forms/using/manage-applications-inbox.md) 和AEM Forms應用程式。 不過，AEM Inbox和AEM Forms應用程式的功能不同。 AEM Inbox只能與 [Forms導向的工作流程搭配使用](../../forms/using/aem-forms-workflow.md) ，而AEM Forms應用程式則可與Forms導向的工作流程以及流程管理搭配使用。

下表列出AEM Inbox和AEM Forms應用程式的功能：

<table>
 <tbody>
  <tr>
   <td><p><strong>動作</strong></p> </td>
   <td><p><strong>AEM 收件匣</strong></p> </td>
   <td><p><strong>AEM Forms應用程式</strong></p> </td>
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
   <td><p>添加任務層附件</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>查看任務層附件</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>添加欄位層附件</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>顯示日曆視圖</p> </td>
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

