---
title: OSGi上的表單導向工作流程
seo-title: Rapidly build adaptive forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: 使用AEM Forms Workflow，自動化並快速建立審閱與核准，以開始檔案服務
seo-description: Use AEM Forms Workflow to automate and rapidly build review and approvals, to start document services (For example, to convert a PDF document to another format), integrate with Adobe Sign signature workflow, and more.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# OSGi上的表單導向工作流程{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

Enterprises collect data from hundreds and thousands of forms, various back-end systems, and online or offline data sources. They also have a dynamic set of users to take decisions on the data, which involves iterative review and approval processes.

大型組織和企業除了針對內部和外部受眾的審查和核准工作流程外，還有重複性工作。 例如，將PDF檔案轉換為其他格式。 When done manually, these tasks take up much time and resources. Enterprises also have legal requirements to digitally sign a document and archive form data for later use in pre-defined formats.

## Introduction to Forms-centric workflow on OSGi {#introduction-to-forms-centric-workflow-on-osgi}

You can use AEM Workflows to rapidly build adaptive forms-based workflows. These workflows can be used for review and approvals, business process flows, to start document services, integrate with Adobe Sign signature workflow, and similar operations. For example, credit card application processing, employee leave approval workflows, saving a form as a PDF document. Moreover, these workflows can be used within an organization or across network firewall.

With Forms-centric workflow on OSGi, you can rapidly build and deploy workflows for various tasks on the OSGi stack, without having to install the full-fledged Process Management capability on JEE stack. 工作流程的開發與管理使用熟悉的AEM Workflow和AEM Inbox功能。 Workflows form the basis of automating real-world business processes that span multiple software systems, networks, departments, and even organizations.

Once set up, these workflows can be triggered manually to complete a defined process or run programmatically when users submit a form or [correspondence management](/help/forms/using/cm-overview.md) letter. 透過這項增強的AEM Workflow功能，AEM Forms提供兩種不同但類似的功能。 As part of your deployment strategy, you need to decide which one works for you. See a [comparison](../../forms/using/capabilities-osgi-jee-workflows.md) of the Forms-centric AEM Workflows on OSGi and Process Management on JEE. 此外，如需部署拓撲，請參 [閱AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md)。

Forms-centric workflow on OSGi extends [AEM Inbox](/help/sites-authoring/inbox.md) and provides extra components (steps) for AEM Workflow editor to add support for AEM Forms-centric workflows. The extended AEM Inbox has functionalities similar to [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md). Along with managing human-centric workflows (Approval, Review, and so on), you can use AEM workflows to automate [document services](/help/sites-developing/workflows-step-ref.md)-related operations (for example, Generate PDF) and electronically signing (Adobe Sign) documents.

All AEM Forms workflow steps support the use of variables. Variables enable workflow steps to hold and pass metadata across steps at runtime. You can create different types of variables for storing different types of data. You can also create variable collections (array) for storing multiple instances of related, same-typed data. Typically, you use a variable or a collection of variables when you need to make a decision based on the value that it holds or to store information that you need later in a process. For more information on using variables in these Forms-centric workflow components (steps), see [Forms-centric workflow on OSGi - Step Reference](../../forms/using/aem-forms-workflow-step-reference.md). For information on creating and managing variables, see [Variables in AEM workflows](../../forms/using/variable-in-aem-workflows.md).

The following diagram depicts end-to-end procedure to create, run, and monitor a Forms-centric workflow on OSGi.

![簡介——至aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## 開始之前 {#before-you-start}

* 工作流程是實際商業程式的表現。 Keep your real-world business process and list of the participants of the business process ready. 此外，在開始建立工作流程之前，請先準備好文宣（最適化表單、PDF檔案等）。
* 工作流程可以有多個階段。 These stages are displayed in the AEM Inbox and help report progress of the workflow. 將業務流程劃分為邏輯階段。
* 您可以設定AEM工作流程的指派工作步驟，以傳送電子郵件通知給使用者或受指派者。 因此，請啟 [用電子郵件通知](#configure-email-service)。
* 工作流程也可以使用Adobe Sign進行數位簽名。 如果您打算在工作流程中使用Adobe Sign，請在 [工作流程中使用Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) 之前，先為AEM Forms設定Adobe Sign。

## Create a workflow model {#create-a-workflow-model}

工作流模型由業務流程的邏輯和流程組成。 它由一系列步驟組成。 這些步驟是AEM元件。 您可以視需要使用參數和指令碼來擴充工作流程步驟，以提供更多功能和控制功能。 AEM Forms除了提供現成可用的AEM步驟外，還提供一些步驟。 如需AEM和AEM Forms步驟的詳細清單，請參閱「 [OSGi —— 步驟參考」上的「](/help/sites-developing/workflows-step-ref.md) AEM Workflow Step Reference [and](../../forms/using/aem-forms-workflow.md)Forms-centric workflow」。

AEM提供直覺式使用者介面，可使用提供的工作流程步驟來建立工作流程模型。 有關建立工作流模型的逐步說明，請參閱創 [建工作流模型](/help/sites-developing/workflows-models.md)。 下列範例提供逐步指示，以建立核准和審核工作流程的工作流程模型：

>[!NOTE]
>
>您必須是工作流編輯器組的成員，才能建立或編輯工作流模型。

### 建立核准和審核工作流程的模型 {#create-a-model-for-an-approval-and-review-workflow}

審批和審核工作流程適用於需要人為干預才能做出決策的任務。 下面的示例為由前台銀行代理填充的抵押貸款申請建立工作流模型。 填妥申請後，即會傳送申請核准。 之後，核准的申請會以Adobe Sign傳送給申請人進行電子簽名。

此示例以下附加的包的形式提供。 使用套件管理器匯入並安裝範例。 您也可以執行以下步驟，為應用程式手動建立工作流模型：

此範例會建立由前台銀行代理所填寫的抵押申請工作流程模型。 填寫完申請後，會傳送申請以供核准。 稍後，核准的應用程式會傳送給客戶，以利用Adobe Sign進行電子簽名。 You can import and install the example using the package manager.

[取得檔案](assets/example-mortgage-loan-application.zip)

1. Open the Workflow Models console. The default URL is https://&#39;[server]:[port]&#39;/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models
1. Select **Create**, then **Create Model**. 將出現「添加工作流模型」(Add Workflow Model)對話框。
1. 輸入 **Title** and **Name** （可選）。 For example, a mortgage application. 點選「 **完成**」。
1. Select the newly created workflow model and tap **Edit**. Now, you can add workflow steps to build business logic. 首次建立工作流模型時，它包含：

   * The steps: Flow Start and Flow End. 這些步驟代表工作流程的開始和結束。 These steps are required and cannot be edited or removed.
   * An example Participant step named Step 1. This step is configured to assign a work item to the admin user. Remove this step.

1. Enable email notifications. You can configure Forms-centric workflow on OSGi to send email notifications to the users or assignees. 執行下列設定以啟用電子郵件通知：

   1. Go to AEM configuration manager at https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. 開啟 **[!UICONTROL Day CQ Mail Service設定]** 。 Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port,]** and **[!UICONTROL &quot;From&quot; address]** fields. 按一下&#x200B;**[!UICONTROL 「儲存」]**。
   1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual hostname/IP address and port number for local, author, and publish instances. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

1. 建立工作流程階段。 A workflow can have multiple stages. 這些階段會顯示在「AEM收件匣」中，並報告工作流程的進度。

   To define a stage, tap the ![info-circle](assets/info-circle.png) icon to open workflow model properties, open the **Stages** tab, add stages for the workflow model, and tap **Save &amp; Close**. For the example mortgage application, create stages: loan request, loan request status, to be signed documents, and signed loan document.

1. 將「指定任務」步驟 **瀏覽器拖放到工作流模型中** 。 Make it the first step of the model.

   The assign task component assigns the task, created by workflow, to a user or group. Along with assigning the task, you can use the component to specify an adaptive form or a non-interactive PDF for the task. The adaptive form is required to accept input from users and non-interactive PDF or a read-only adaptive form is used for review only workflows.

   You can also use the step to control the behavior of the task. For example, creating an automatic document of record, assign the task to a specific user or group, the path of the submitted data, the path of data to be pre-populated, and default actions. For detailed information about the options of the assign task step, see [Forms-centric workflow on OSGi - Step Reference](../../forms/using/aem-forms-workflow.md) document.

   ![workflow-editor](assets/workflow-editor.png)

   對於抵押申請示例，請將指派任務步驟配置為使用只讀自適應表單，並在任務完成後顯示PDF文檔。 此外，選擇允許批准貸款請求的用戶組。 On the **Actions** tab, disable the **Submit** option. Create an **actionTaken** variable of String data type and specify the variable as the **Route Variable**. For example, actionTaken. Also, add the Approve and Reject routes. The routes are displayed as separate actions (buttons) in AEM Inbox. 工作流程會根據使用者點選的動作（按鈕）來選取分支。

   您可以導入示例包，該示例包可在章節的開頭部分下載，以獲得為例如抵押貸款應用程式配置的分配任務步驟的所有欄位的完整值集。

1. Drag-and-drop the OR Split component from step browser to the workflow model. The OR Split creates a split in the workflow, after which only one branch is active. This step enables you to introduce conditional processing paths into your workflow. You add workflow steps to each branch as required.

   您可以使用規則定義、ECMA指令碼或外部指令碼為分支定義路由表達式。

   使用表達式編輯器為Branch 1和Branch 2建立路由表達式。 這些路由運算式可協助您根據AEM收件匣中的使用者動作來選擇分支。

   **分支1的路由表達式**

   When a user taps **Approve** in AEM Inbox, Branch 1 is activated.

   ![OR Split example](assets/orsplit_branch1_active_new.png)

   **Routing expression for Branch 2**

   當使用者點選「 **AEM收件匣中** 」時，Branch 2就會啟動。

   ![OR Split example](assets/orsplit_branch2_active_new.png)

   如需使用變數建立路由運算式的詳細資訊，請參閱「AEM表 [單工作流程中的變數」](../../forms/using/variable-in-aem-workflows.md)。

1. Add other workflow steps to build the business logic.

   For the mortgage example, add a generate document of record, two assign task steps, and a sign document step to Branch 1 of the model, as displayed in the image below. 一個指派任務步驟是顯示待簽署 **的貸款檔案並傳送給申請人** ，另一個指派任務元件 **是顯示已簽署的檔案**。 Also, add an assign task component to branch 2. 當使用者在AEM收件匣中點選「拒絕」時，就會啟動它。

   對於為例如抵押貸款應用程式配置的分配任務步驟、記錄步驟文檔和簽署文檔步驟的所有欄位的完整值集，請導入示例包，該示例包可在本節的開頭下載。

   The workflow model is ready. 您可以透過各種方法啟動工作流程。 如需詳細資訊，請 [參閱「在OSGi上啟動以表單為中心的工作流程」](../../forms/using/aem-forms-workflow.md#main-pars-header)。

   ![workflow-editor-mortgage](assets/workflow-editor-mortgage.png)

## 建立以表單為中心的工作流程應用程式 {#create-a-forms-centric-workflow-application}

應用程式是與工作流程相關聯的最適化表單。 When an application is submitted through Inbox, it launches the associated workflow. 若要將表單工作流程設為AEM Inbox和AEM Forms應用程式中的應用程式，請執行下列動作以建立工作流程應用程式：

>[!NOTE]
>
>您必須是fd-administrator組的成員，才能建立和管理工作流應用程式。

1. 在您的AEM作者例項上，請前往 ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]**> Manage Workflow Application **[!UICONTROL ，然後點選]****** CreateCreate。
1. 在「建立工作流應用程式」窗口中，為以下欄位提供輸入，然後點選「創 **建**」。 會建立新應用程式，並列在「工作流程應用程式」畫面中。

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>說明</td>
  </tr>
  <tr>
   <td>標題</td>
   <td>標題會顯示在「AEM收件匣」中，並協助使用者選擇應用程式。 Keep it descriptive. 例如，儲蓄帳戶開立應用程式。<br /> </td>
  </tr>
  <tr>
   <td>名稱 </td>
   <td>指定應用程式的名稱。 除字母、數字、連字型大小和底線以外的所有字元都將替換為連字型大小。 </td>
  </tr>
  <tr>
   <td>說明</td>
   <td>說明會顯示在「AEM收件匣」中。 在說明欄位中提供應用程式的詳細資訊。 例如，應用程式的用途。<br /> </td>
  </tr>
  <tr>
   <td>最適化表單</td>
   <td><p>指定最適化表單的路徑。 當使用者啟動應用程式時，會顯示指定的最適化表單。</p> <p><strong>注意</strong>:工作流程應用程式不支援長度超過一頁或需要在Apple iPad上捲動的表單和PDF檔案。 當應用程式在Apple iPad上開啟時，當最適化表單或PDF檔案長於頁面時，第二個頁面的表單欄位和內容會遺失。</p> </td>
  </tr>
  <tr>
   <td>存取群組</td>
   <td><p>選取群組。 應用程式只會顯示在「AEM收件匣」中，顯示給所選群組的成員。 訪問組選項使工作流用戶組的所有組都可供選擇。 </p> <br /> </td>
  </tr>
  <tr>
   <td>預填服務</td>
   <td>為最適 <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">化表單選擇</a> 「預填」服務。<br /> </td>
  </tr>
  <tr>
   <td>工作流程模型</td>
   <td>為應用程 <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">式選取工作</a> 流程模型。 工作流模型由業務流程的邏輯和流程組成。 </td>
  </tr>
  <tr>
   <td>資料檔案路徑</td>
   <td>在crx-repository中指定資料檔案的路徑。 路徑與最適化表單裝載相關，並包含資料檔案的名稱。 請務必包含檔案的完整名稱，包括副檔名（如果適用）。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>附件路徑</td>
   <td>在crx-repository中指定附件資料夾的路徑。 附件路徑相對於裝載位置。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>記錄文件路徑</td>
   <td>在crx-repository中指定記錄檔案的路徑。 該路徑相對於自適應表單有效載荷位置。 請務必包含檔案的完整名稱，包括副檔名（如果適用）。 例如，[payload]/DOR/creditcard.pdf。</td>
  </tr>
 </tbody>
</table>

## 在OSGi上啟動以表單為中心的工作流程 {#launch}

您可以透過下列方式啟動或觸發以表單為中心的工作流程：

* [從AEM收件匣提交應用程式](#inbox)
* [從AEM Forms應用程式送出應用程式](#afa)

* [提交最適化表單](#af)
* [使用監視資料夾](#watched)

* [提交互動式通訊或信函](#letter)

### 從AEM收件匣提交應用程式 {#inbox}

您建立的工作流應用程式作為「收件箱」中的應用程式可用。 屬於工作流程使用者群組的使用者可以填寫並送出觸發相關工作流程的應用程式。 如需使用AEM Inbox來送出應用程式及管理工作的詳細資訊，請參閱「 [在AEM收件匣中管理表單應用程式和工作」](../../forms/using/manage-applications-inbox.md)。

### 從AEM Forms應用程式送出應用程式 {#afa}

AEM Forms應用程式與AEM Forms伺服器同步，可讓您變更帳戶中的表單資料、工作、工作流程應用程式和儲存的資訊（草稿／範本）。 如需詳細資訊，請參 [閱「AEM Forms應用程式](/help/forms/using/aem-forms-app.md) 」和相關文章。

### 提交最適化表單 {#af}

您可以設定最適化表單的提交動作，以在提交最適化表單時啟動工作流程。 最適化表單提 **供「叫用AEM Workflow** submit」動作，以在提交最適化表單時啟動工作流程。 如需提交動作的詳細資訊，請參 [閱設定提交動作](../../forms/using/configuring-submit-actions.md)。 若要透過AEM Forms應用程式提交最適化表單，請啟用最適化表單屬性中的「與AEM表單應用程式同步」。

您可以設定最適化表單，以便從AEM Forms應用程式同步、送出和觸發工作流程。 如需詳細資訊，請 [參閱使用表格](/help/forms/using/working-with-form.md)。

### 使用監視的資料夾 {#watched}

管理員（fd-administrators組的成員）可以配置網路資料夾，以在用戶將檔案（如PDF檔案）放在資料夾中時運行預配置的工作流。 工作流完成後，它可以將結果檔案保存到指定的輸出資料夾。 此類資料夾稱為「 [Watched Folder」](../../forms/using/watched-folder-in-aem-forms.md)。 請執行下列程式，以設定受監視的資料夾以啟動工作流程：

1. 在您的AEM作者例項上，前往 ![tools-1](assets/tools-1.png) > **Forms ****> Configure Watched Folder。** 將顯示已配置的監視資料夾的清單。
1. 點選 **[!UICONTROL 新]**。 隨即顯示欄位清單。 指定下列欄位的值，以設定工作流程的「監看資料夾」:

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>說明</td>
  </tr>
  <tr>
   <td><span class="uicontrol">名稱</code></td>
   <td>指定「Watched」檔案夾的名稱。 此欄位僅支援英數字元。</td>
  </tr>
  <tr>
   <td><span class="uicontrol">路徑</code></td>
   <td>指定「監視資料夾」的實際位置。 在叢集環境中，使用可從AEM叢集節點存取的共用網路資料夾。</td>
  </tr>
  <tr>
   <td><span class="uicontrol">處理檔案使用</code></td>
   <td>選擇「工 <span class="uicontrol">作流 </code>」選項。 </code></td>
  </tr>
  <tr>
   <td><span class="uicontrol">工作流程模型</code></td>
   <td>Select a workflow model.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">輸出檔案模式</code></td>
   <td>指定輸出檔案和目錄的目錄結構。 您也可以指定輸 <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">出檔案和目錄的模式</a>。</td>
  </tr>
 </tbody>
</table>

1. 點選「 **進階**」。 為下列欄位指定值，然後點選「 **建立**」。 「Watched Folder」（監視資料夾）已配置為啟動工作流。 現在，每當檔案置於「Watched資料夾」的輸入目錄時，就會觸發指定的工作流程。

   | 欄位 | 說明 |
   |---|---|
   | 承載對應程式篩選條件 | 當您建立受監視的檔案夾時，會在crx-repository中建立檔案夾結構。 資料夾結構可當成工作流程的裝載。 您可以編寫指令碼來對應AEM Workflow，以接受來自受監視檔案夾結構的輸入。 現成可用的實施，並列在「裝載映射器過濾器」中。 如果您沒有自訂實作，請選取預設實作。 |

   「進階」標籤包含更多欄位。 這些欄位中，大部分都包含預設值。 若要瞭解所有欄位，請參閱「建立 [或設定受監視的檔案夾](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md) 」文章。

### 提交互動式通訊或信函 {#letter}

在提交互動式通訊或信函時，您可在OSGi上建立關聯並執行以表單為中心的工作流程。 在信件管理工作流程中，用於後處理互動式通訊和信件。 例如，以電子郵件傳送、列印、傳真或封存最終信件。 如需詳細步驟，請參 [閱互動式通訊和信件的後置處理](../../forms/using/submit-letter-topostprocess.md)。

## 其他配置 {#additional-configurations}

### 設定電子郵件服務 {#configure-email-service}

您可以使用「AEM工作流程」的「指派工作」和「傳送電子郵件」步驟來傳送電子郵件。 執行以下步驟來指定電子郵件伺服器和發送電子郵件所需的其他配置：

1. 請前往https://&#39;[server]:[port]&#39;/system/console/configMgr的AEM組態管理器。
1. 開啟 **[!UICONTROL Day CQ Mail Service設定]** 。 指定 **[!UICONTROL SMTP伺服器主機名、]** SMTP伺服器埠 **[!UICONTROL 、]** 「寄件者」地址欄位 **** 。 按一下&#x200B;**[!UICONTROL 「儲存」]**。
1. 開啟 **[!UICONTROL Day CQ Link Externalizer設定]** 。 在「網 **[!UICONTROL 域]** 」欄位中，指定本機、作者和發佈例項的實際主機名稱/IP位址和埠號。 按一下&#x200B;**[!UICONTROL 「儲存」]**。

### 清除工作流實例 {#purge-workflow-instances}

最小化工作流實例數可提高工作流引擎的效能，因此您可以定期從儲存庫中清除已完成或正在運行的工作流實例。 有關詳細資訊，請參 [閱：定期清除工作流實例](/help/sites-administering/workflows-administering.md#定期清除工作流實例)。
