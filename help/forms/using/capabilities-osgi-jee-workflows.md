---
title: OSGi和AEM FormsJEE工作流中以AEM表單為中心的工作流的操作和功能
description: OSGi和AEM FormsJEE工作流中以AEM表單為中心的工作流的操作和功能
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 22%

---

# OSGi和AEM FormsJEE工作流中以AEM表單為中心的工作流的操作和功能 {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## 收AEM件箱和HTML工作區 {#aem-inbox-and-html-workspace}

您可以使AEM用收件箱在OSGi上運行和監AEM視以Forms為中心的工作流。 但是，HTML工作區允許您運行和監視AEM FormsJEE工作流。 下表幫助您瞭解在OSGi上以Forms為中心的工作流的收件箱AEM中以及在AEM FormsJEE工作流的HTML工作區AEM中提供的各種重要操作。

<table>
 <tbody>
  <tr>
   <td>動作</td>
   <td>AEM 收件匣</td>
   <td>HTML工作區</td>
  </tr>
  <tr>
   <td>啟動流程、任務或表單應用程式<br /> </td>
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
   <td>重新分配任務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>自適應表單的欄位級附件</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>日曆視圖</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>任務級別注釋</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>隊列（共用的個人隊列、來自隊列的聲明任務）</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>離職通知</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
    <tr>
   <td>自定義UI元素</td>
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

## OSGi和AEMAEM FormsJEE工作流中以表單為中心的工作流 {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi和AEM FormsAEM JEE工作流(JEE流程管理AEM Forms)上以表單為中心的工作流具有不同的功能集。 下表幫助您瞭解以表單為中心的工作流中AEM有關OSGi和AEM Forms的JEE工作流的重要功能：

<table>
 <tbody>
  <tr>
   <td>功能</td>
   <td>OSGi上以表AEM格為中心的工作流<br /> </td>
   <td>AEM FormsJEE工作流</td>
  </tr>
  <tr>
   <td>最適化表單</td>
   <td>支援</td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>與其他解決方AEM案整合</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>草寫簽名</td>
   <td>支援</td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>自定義電子郵件模板</td>
   <td>支援</td>
   <td>支援<br /> </td>
  </tr>
  <tr>
   <td>定義任務優先順序</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>在到期日期後超時任務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>工作流中的循環</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>動態選擇受分配方 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>使用自定義元資料</td>
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
   <td>將已完成的任務呈現為自適應表單或PDF文檔</td>
   <td>支援</td>
   <td>支援 [4]</td>
  </tr>
  <tr>
   <td>與函件管理的整合</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
   <tr>
   <td>網關，無等待 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
   <tr>
   <td>用於儲存資料的變數 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>或，並拆分</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>用戶虛擬形象</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>在工作流結束時發送電子郵件</td>
   <td>支援 <sup>[7]</sup></td>
   <td>支援</td>
  </tr>
  <tr>
   <td>從工作流調用Web服務</td>
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
   <td>工作流階段</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>只讀自適應表單</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>隱藏預設保存按鈕</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>對工作流詳細資訊部分的精細控制</td>
   <td>支援</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>輪詢/計畫服務</td>
   <td>開箱即用</td>
   <td>需要自定義實施</td>
  </tr>
  <tr>
   <td>自適應Forms應用</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>組合器服務</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>PDF生成器服務</td>
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
   <td>文檔保證</td>
   <td>支援</td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>執行指令碼</td>
   <td>支援ECMAScript</td>
   <td>支援Java代碼片段</td>
  </tr>
  <tr>
   <td>組合器</td>
   <td>支援</td>
   <td>支援</td>
  </tr>  
  <tr>
   <td>HTML5Forms，互動式PDF forms，表單集</td>
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
   <td>批量任務審批 </td>
   <td>不支援 </td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>使用自定義名稱保存草稿</td>
   <td>不支援 </td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>使用現有流程資料啟動流程<br /> </td>
   <td>不支援</td>
   <td>支援 </td>
  </tr>
  <tr>
   <td>將起始點另存為繪製</td>
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
   <td>與第三方應用程式整合</td>
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
   <td>有關任務委派和任務聲明的電子郵件</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>不相交的組之間的委派</td>
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
   <td>動態描述</td>
   <td>不支援</td>
   <td>不支援</td>
  </tr>
 </tbody>
</table>

1. 您可以在OSGi上使用以表AEM單為中心的工作流來簽署已填充的自適應表單。 OSGi上以表AEM單為中心的工作流支援表單簽名。 的 [表單簽名](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) 不支援體驗。

1. 您需要訪問收件箱AEM來運行和監視AEM FormsOSGi上以表單為中心的工作流，並需要HTML工作區來運行和監視AEM FormsJEE工作流。
1. 本機AEM Forms文檔服務可用於OSGi上以表AEM格為中心的工作流和JEE工作流上的AEM Forms。 工AEM作流在OSGi和AEM FormsJEE（流程管理）工作AEM流上使用本機文檔服務進行以表單為中心的工作流。
1. AEM FormsJEE工作流只能呈現自適應表單。 它不支援將自適應表單作為PDF文檔呈現。
1. 表AEM單JEE工作流沒有單獨的Adobe Sign步驟。 您需要為表單JEE工作流啟AEM用的自適應表單。 有關詳細資訊，請參閱 [Adobe Sign文檔](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)。
1. 您可以使用 [調用表單資料模型服務](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) 調用Web服務並從第三方應用程式發佈或檢索資料的步驟。
1. 您可以使用 [發送電子郵件](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) 發送電子郵件的步驟。

## 收件箱AEM和AEM Forms應用功能之間的差異 {#differences-between-aem-inbox-and-aem-forms-app-features}

啟動以Forms為中心的工作流的兩種主要方式都在使用 [收件箱AEM](../../forms/using/manage-applications-inbox.md) 和AEM Forms應用。 但是，Inbox和AEMAEM Forms應用的功能不同。 收AEM件箱僅與 [以Forms為中心的工作流](../../forms/using/aem-forms-workflow.md) 同時，AEM Forms應用可以與以Forms為中心的工作流程和流程管理配合使用。

下表列出了收件箱和AEMAEM Forms應用的功能：

<table>
 <tbody>
  <tr>
   <td><p><strong>動作</strong></p> </td>
   <td><p><strong>AEM 收件匣</strong></p> </td>
   <td><p><strong>AEM Forms 應用程式</strong></p> </td>
  </tr>
  <tr>
   <td><p>啟動窗體應用程式</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>提交任務</p> </td>
   <td><p>支援</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>委託任務</p> </td>
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
   <td><p>添加欄位級附件</p> </td>
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
