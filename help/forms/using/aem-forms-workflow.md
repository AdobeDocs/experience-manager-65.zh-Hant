---
title: 基於OSGi的以Forms為中心的工作流
seo-title: Rapidly build adaptive forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: 使用AEM Forms工作流自動化並快速構建審核和批准，以啟動文檔服務
seo-description: Use AEM Forms Workflow to automate and rapidly build review and approvals, to start document services (For example, to convert a PDF document to another format), integrate with Adobe Sign signature workflow, and more.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
exl-id: c3e5f8fc-d2b9-4f76-9a3d-4bc5733f5a5c
source-git-commit: d9608d584e822accc0c198fcf1d1b706d065938e
workflow-type: tm+mt
source-wordcount: '3681'
ht-degree: 1%

---

# 基於OSGi的以Forms為中心的工作流{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

企業從成百上千個表單、各種後端系統以及線上或離線資料源中收集資料。 他們還擁有一組動態的用戶來對資料做出決策，這涉及到反複的審核和批准過程。

除了針對內部和外部受眾的審核和批准工作流外，大型組織和企業還具有重複性任務。 例如，將PDF文檔轉換為其他格式。 手動完成這些任務時，需要耗費大量時間和資源。 企業還有法律要求對文檔和存檔表單資料進行數字簽名，以便以後以預定義格式使用。

## OSGi中以Forms為中心的工作流簡介 {#introduction-to-forms-centric-workflow-on-osgi}

您可以使用AEM工作流快速構建基於表單的自適應工作流。 這些工作流可用於審查和批准、業務流程流、啟動文檔服務、與Adobe Sign簽名工作流整合以及類似操作。 例如，信用卡申請處理、員工離職審批工作流、將表單另存為PDF單據。 此外，這些工作流可以在組織內或跨網路防火牆使用。

在OSGi上，使用以Forms為中心的工作流，您可以快速構建和部署OSGi堆棧上各種任務的工作流，而無需在JEE堆棧上安裝完整的進程管理功能。 工作流的開發和管理使用熟悉的工作AEM流和收件箱AEM功能。 工作流構成了自動化跨多個軟體系統、網路、部門甚至組織的真實業務流程的基礎。

設定後，這些工作流可以手動觸發，以完成定義的流程或在用戶提交表單或 [通信管理](/help/forms/using/cm-overview.md) 信。 通過這種增強AEM的工作流功能，AEM Forms提供了兩種截然不同但相似的功能。 作為部署策略的一部分，您需要決定哪一項適合您。 查看 [比較](capabilities-osgi-jee-workflows.md) 以Forms為AEM中心的OSGi工作流和JEE流程管理。 此外，有關部署拓撲，請參見， [用於AEM Forms的體系結構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md)。

基於OSGi的以Forms為中心的工作流擴展 [收件箱AEM](/help/sites-authoring/inbox.md) 並為工作流編輯器提供額外AEM的元件（步驟），以添加對以AEM Forms為中心的工作流的支援。 擴展的AEM收件箱具有類似 [AEM Forms工作區](introduction-html-workspace.md)。 除了管理以人為中心的工作流（批准、審查等）外，您還可以使用工作流AEM自動執行 [文檔服務](/help/sites-developing/workflows-step-ref.md) — 相關操作(例如，生成PDF)和電子簽名(Adobe Sign)文檔。

所有AEM Forms工作流步驟都支援使用變數。 變數允許工作流步驟在運行時保留和傳遞跨步驟的元資料。 您可以建立不同類型的變數來儲存不同類型的資料。 您還可以建立變數集合（陣列）來儲存相關、相同類型資料的多個實例。 通常，當需要根據變數所包含的值做出決策或儲存在以後流程中需要的資訊時，您會使用變數或變數集合。 有關在這些以Forms為中心的工作流元件中使用變數的詳細資訊（步驟），請參見 [以Forms為中心的OSGi工作流 — 步驟參考](../../forms/using/aem-forms-workflow-step-reference.md)。 有關建立和管理變數的資訊，請參見 [工作流中的AEM變數](../../forms/using/variable-in-aem-workflows.md)。

下圖描述了在OSGi上建立、運行和監視以Forms為中心的工作流的端到端過程。

![工作流簡介](assets/introduction-to-aem-forms-workflow.jpg)

## 開始之前 {#before-you-start}

* 工作流是真實世界業務流程的表示。 讓您的實際業務流程和業務流程參與者清單保持就緒狀態。 另外，在開始建立工作流之前，請保持宣傳資料(自適應表單、PDF文檔等)的就緒性。
* 工作流可以具有多個階段。 這些階段顯示在「收件箱」AEM中，並幫助報告工作流的進度。 將業務流程分為邏輯階段。
* 您可以配置工作流的分配任AEM務步驟，以向用戶或受分配者發送電子郵件通知。 所以， [啟用電子郵件通知](#configure-email-service)。
* 工作流還可以使用Adobe符號進行數字簽名。 如果您計畫在工作流中使用Adobe Sign, [配置Adobe SignAEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) 在工作流中使用。

## 建立工作流模型 {#create-a-workflow-model}

工作流模型由業務流程的邏輯和流程組成。 它由一系列步驟組成。 這些步驟是AEM元件。 您可以根據需要擴展包含參數和指令碼的工作流步驟，以提供更多功能和控制。 AEM Forms提供了除現成步驟AEM之外的幾個步驟。 有關步驟和AEM FormsAEM步驟的詳細清單，請參見 [工作AEM流步驟參考](/help/sites-developing/workflows-step-ref.md) 和 [以Forms為中心的OSGi工作流 — 步驟參考](../../forms/using/aem-forms-workflow.md)。

提AEM供直觀的用戶介面，以使用提供的工作流步驟建立工作流模型。 有關建立工作流模型的逐步說明，請參閱 [建立工作流模型](/help/sites-developing/workflows-models.md)。 以下示例提供了逐步說明，用於為審批和複查工作流建立工作流模型：

>[!NOTE]
>
>必須是工作流編輯器組的成員才能建立或編輯工作流模型。

### 為審批和複查工作流建立模型 {#create-a-model-for-an-approval-and-review-workflow}

審批和審核工作流是針對需要人工干預才能做出決策的任務。 下面的示例為由前台銀行代理填寫的抵押貸款申請建立工作流模型。 申請填寫後，即發送審批。 隨後，核准的申請將發給申請人，請其使用Adobe Sign進行電子簽名。

該示例作為附加在下面的包提供。 使用包管理器導入並安裝示例。 您還可以執行以下步驟為應用程式手動建立工作流模型：

該示例建立由前台銀行代理填寫的抵押申請的工作流模型。 填寫完申請後，將發送審批。 稍後，將批准的應用程式發送給客戶，以便使用Adobe Sign進行電子簽名。 可以使用包管理器導入和安裝示例。

[取得檔案](assets/example-mortgage-loan-application.zip)

1. 開啟「工作流模型」控制台。 預設URL為 `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. 選擇 **建立**，則 **建立模型**。 將出現「添加工作流模型」對話框。
1. 輸入 **標題** 和 **名稱** （可選）。 例如，抵押貸款申請。 點擊 **完成**。
1. 選擇新建立的工作流模型並點擊 **編輯**。 現在，您可以添加工作流步驟來構建業務邏輯。 首次建立工作流模型時，它包含：

   * 步驟：流開始和流結束。 這些步驟表示工作流的開始和結束。 這些步驟是必需的，不能編輯或刪除。
   * 名為步驟1的「參與者」步驟示例。 此步驟配置為將工作項分配給管理員用戶。 刪除此步驟。

1. 啟用電子郵件通知。 您可以在OSGi上配置以Forms為中心的工作流，以向用戶或受分配者發送電子郵件通知。 執行以下配置以啟用電子郵件通知：

   1. 轉到AEM配置管理器 `https://[server]:[port]/system/console/configMgr`。
   1. 開啟 **[!UICONTROL 第CQ天郵件服務]** 配置。 為 **[!UICONTROL SMTP伺服器主機名]**。 **[!UICONTROL SMTP伺服器埠，]** 和 **[!UICONTROL &quot;發件人&quot;地址]** 的子菜單。 按一下「**[!UICONTROL 儲存]**」。
   1. 開啟 **[!UICONTROL 第CQ天連結外部化程式]** 配置。 在 **[!UICONTROL 域]** 欄位，指定本地、作者和發佈實例的實際主機名/IP地址和埠號。 按一下「**[!UICONTROL 儲存]**」。

1. 建立工作流階段。 工作流可以具有多個階段。 這些階段顯示在工AEM作流的收件箱和報告進度中。

   要定義舞台，請點擊 ![資訊圓](assets/info-circle.png) 表徵圖以開啟工作流模型屬性，開啟 **階段** 頁籤，為工作流模型添加階段，然後按一下 **保存並關閉**。 對於抵押申請示例，請建立階段：貸款申請、貸款申請狀態、待簽檔案和已簽貸款檔案。

1. 拖放 **分配任務** 步驟瀏覽到工作流模型。 將其作為模型的第一步。

   分配任務元件將由工作流建立的任務分配給用戶或組。 在分配任務的同時，可以使用元件為任務指定自適應表單或非互動式PDF。 需要自適應表單來接受來自用戶的輸入，而非互動式PDF或只讀自適應表單用於僅查看工作流。

   也可以使用步驟來控制任務的行為。 例如，建立記錄的自動文檔，將任務分配給特定用戶或組、已提交資料的路徑、要預填充的資料路徑以及預設操作。 有關分配任務步驟選項的詳細資訊，請參閱 [以Forms為中心的OSGi工作流 — 步驟參考](../../forms/using/aem-forms-workflow.md) 的子菜單。

   ![工作流編輯器](assets/workflow-editor.png)

   對於抵押申請示例，將分配任務步驟配置為在任務完成後使用只讀自適應表單和顯示PDF文檔。 此外，選擇允許審批貸款請求的用戶組。 在 **操作** 頁籤 **提交** 的雙曲餘切值。 建立 **已採取的操作** 字串資料類型的變數，並將該變數指定為 **路由變數**。 例如，actionTaked。 另外，添加「批准」和「拒絕」路由。 路由在收件箱中顯示為單獨的操作(按AEM鈕)。 工作流根據用戶點擊的操作（按鈕）選擇分支。

   您可以導入示例包，該示例包可在節的開頭下載，以用於為例如抵押申請配置的分配任務步驟的所有欄位的完整值集。

1. 將「或拆分」元件從步驟瀏覽器拖放到工作流模型。 「或拆分」(OR Split)在工作流中建立一個拆分，之後只有一個分支處於活動狀態。 此步驟使您能夠將條件處理路徑引入工作流。 根據需要將工作流步驟添加到每個分支。

   可以使用規則定義、ECMA指令碼或外部指令碼為分支定義路由表達式。

   使用表達式編輯器為Branch 1和Branch 2建立路由表達式。 這些路由表達式有助於根據收件箱中的用戶操作選擇AEM分支。

   **分支1的路由表達式**

   用戶點擊時 **批准** 在收AEM件箱中，Branch 1被激活。

   ![OR拆分示例](assets/orsplit_branch1_active_new.png)

   **分支2的路由表達式**

   用戶點擊時 **拒絕** 在收AEM件箱中，將激活Branch 2。

   ![OR拆分示例](assets/orsplit_branch2_active_new.png)

   有關使用變數建立路由表達式的資訊，請參見 [AEM Forms工作流中的變數](../../forms/using/variable-in-aem-workflows.md)。

1. 添加其他工作流步驟以構建業務邏輯。

   對於抵押示例，將生成記錄文檔、兩個分配任務步驟和一個簽名文檔步驟添加到模型的分支1，如下圖所示。 一個分配任務步驟是顯示和發送 **要簽署貸款檔案** 另一個分配任務元件 **顯示簽名文檔**。 另外，將分配任務元件添加到分支2。 當用戶點擊收件箱中的拒絕時，將激AEM活它。

   對於為例如抵押申請配置的分配任務步驟、記錄步驟的文檔和簽名文檔步驟的所有欄位的完整值集，請導入示例包，該示例包可在本節的開頭下載。

   工作流模型已就緒。 您可以通過各種方法啟動工作流。 有關詳細資訊，請參閱 [在OSGi上啟動以Forms為中心的工作流](#launch)。

   ![工作流編輯器 — 抵押](assets/workflow-editor-mortgage.png)

## 建立以Forms為中心的工作流應用程式 {#create-a-forms-centric-workflow-application}

應用程式是與工作流關聯的自適應表單。 當應用程式通過收件箱提交時，它將啟動關聯的工作流。 要使Forms工作流作為「收件箱」和AEM「AEM Forms應用」中的應用程式可用，請執行以下操作建立工作流應用程式：

>[!NOTE]
>
>您必須是fd-administrator組的成員才能建立和管理工作流應用程式。

1. 在您的AEM作者實例上，轉到 ![工具–1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL 管理工作流應用程式]** 和水龍頭 **[!UICONTROL 建立]**。
1. 在「建立工作流應用程式」窗口中，為以下欄位提供輸入，並抽取 **建立**。 將建立新應用程式，並在「工作流應用程式」螢幕中列出。

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>說明</td>
  </tr>
  <tr>
   <td>標題</td>
   <td>標題在收件箱中可AEM見，並幫助用戶選擇應用程式。 保持描述性。 例如，儲蓄帳戶開戶應用程式。<br /> </td>
  </tr>
  <tr>
   <td>名稱 </td>
   <td>指定應用程式的名稱。 除字母、數字、連字元和下划線以外的所有字元都用連字元替換。 </td>
  </tr>
  <tr>
   <td>說明</td>
   <td>說明在收件箱中AEM可見。 在說明欄位中提供有關應用程式的詳細資訊。 例如，應用程式的目的。<br /> </td>
  </tr>
  <tr>
   <td>自適應窗體</td>
   <td><p>指定自適應表單的路徑。 當用戶啟動應用程式時，將顯示指定的自適應表單。</p> <p><strong>注釋</strong>:工作流應用程式不支援超過一頁或需要在AppleiPad上滾動的表單和PDF文檔。 當在AppleiPad上開啟應用程式，並且自適應表單或PDF文檔長於頁面時，表單欄位和第二頁的內容將丟失。</p> </td>
  </tr>
  <tr>
   <td>存取群組</td>
   <td><p>選擇組。 該應用程式在「收AEM件箱」中僅對選定組的成員可見。 訪問組選項使工作流用戶組的所有組都可供選擇。 </p> <br /> </td>
  </tr>
  <tr>
   <td>預填服務</td>
   <td>選擇 <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">預填充服務</a> 的上界。<br /> </td>
  </tr>
  <tr>
   <td>工作流程模型</td>
   <td>選擇 <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">工作流模型</a> 的雙曲餘切值。 工作流模型由業務流程的邏輯和流程組成。 </td>
  </tr>
  <tr>
   <td>資料檔案路徑</td>
   <td>指定crx-repository中資料檔案的路徑。 該路徑與自適應表單負載相關，並包含資料檔案的名稱。 始終包括檔案的完整名稱（包括副檔名）（如果適用）。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>附件路徑</td>
   <td>指定crx-repository中附件資料夾的路徑。 附件路徑相對於負載位置。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>記錄文件路徑</td>
   <td>指定crx-repository中記錄檔案的文檔路徑。 該路徑相對於自適應形式有效負載位置。 始終包括檔案的完整名稱（包括副檔名）（如果適用）。 例如，[payload]/DOR/creditcard.pdf。</td>
  </tr>
 </tbody>
</table>

## 在OSGi上啟動以Forms為中心的工作流 {#launch}

您可以通過以下方式啟動或觸發以Forms為中心的工作流：

* [從收件箱提交應AEM用程式](#inbox)
* [從AEM Forms應用提交應用程式](#afa)

* [提交自適應表單](#af)
* [使用監視資料夾](#watched)

* [提交互動式通信或信函](#letter)

### 從收件箱提交應AEM用程式 {#inbox}

您建立的工作流應用程式可以作為收件箱中的應用程式使用。 作為工作流 — 用戶組成員的用戶可以填寫和提交觸發關聯工作流的應用程式。 有關使用收件箱AEM提交應用程式和管理任務的資訊，請參閱 [在收件箱中管理Forms應用程式AEM和任務](../../forms/using/manage-applications-inbox.md)。

### 從AEM Forms應用提交應用程式 {#afa}

AEM Forms應用與AEM Forms伺服器同步，允許您更改帳戶中的表單資料、任務、工作流應用程式和保存的資訊（草稿/模板）。 有關詳細資訊，請參見 [AEM Forms應用](/help/forms/using/aem-forms-app.md) 以及相關文章。

### 提交自適應表單 {#af}

您可以配置自適應表單的提交操作，以便在提交自適應表單時啟動工作流。 自適應表單提供 **調用工AEM作流** 提交操作以在提交自適應表單時啟動工作流。 有關提交操作的詳細資訊，請參閱 [配置提交操作](../../forms/using/configuring-submit-actions.md)。 要通過AEM Forms應用提交自適應表單，請在自適應表單屬性中啟用與AEM Forms應用同步。

您可以配置自適應表單以同步、提交和觸發來自AEM Forms應用的工作流。 有關詳細資訊，請參閱 [使用表單](/help/forms/using/working-with-form.md)。

### 使用監視資料夾 {#watched}

管理員（fd-administrators組的成員）可以配置網路資料夾，以便在用戶將檔案(如PDF檔案)放在資料夾中時運行預配置的工作流。 工作流完成後，可以將結果檔案保存到指定的輸出資料夾。 此類資料夾稱為 [監視資料夾](../../forms/using/watched-folder-in-aem-forms.md)。 執行以下過程以配置監視資料夾以啟動工作流：

1. 在您的AEM作者實例上，轉到 ![工具–1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL 配置監視資料夾]**。 將顯示已配置的監視資料夾的清單。
1. 點擊 **[!UICONTROL 新建]**。 將顯示欄位清單。 指定以下欄位的值以配置工作流的監視資料夾：

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>說明</td>
  </tr>
  <tr>
   <td><span class="uicontrol">名稱</code></td>
   <td>指定監視資料夾的名稱。 此欄位僅支援字母數字。</td>
  </tr>
  <tr>
   <td><span class="uicontrol">路徑</code></td>
   <td>指定「監視資料夾」的物理位置。 在群集環境中，使用可從群集節點訪問的共AEM享網路資料夾。</td>
  </tr>
  <tr>
   <td><span class="uicontrol">處理檔案使用</code></td>
   <td>選擇 <span class="uicontrol">工作流 </code>的雙曲餘切值。 </code></td>
  </tr>
  <tr>
   <td><span class="uicontrol">工作流程模型</code></td>
   <td>選擇工作流模型。<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">輸出檔案模式</code></td>
   <td>指定輸出檔案和目錄的目錄結構。 也可以指定 <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">輸出檔案和目錄的模式</a>。</td>
  </tr>
 </tbody>
</table>

1. 點擊 **高級**。 為以下欄位和分路器指定值 **建立**。 已將「監視資料夾」配置為啟動工作流。 現在，每當檔案被放在「監視資料夾」的輸入目錄中時，就會觸發指定的工作流。

   | 欄位 | 說明 |
   |---|---|
   | 承載對應程式篩選條件 | 建立受監視資料夾時，它會在crx-repository中建立資料夾結構。 資料夾結構可用作工作流的負載。 您可以編寫指令碼來映射AEM工作流以接受受監視資料夾結構的輸入。 「負載映射器」過濾器中列出了現成實現。 如果沒有自定義實現，請選擇預設實現。 |

   「高級」頁籤包含更多欄位。 這些欄位中的大多數都包含預設值。 要瞭解所有欄位，請參閱 [建立或配置監視資料夾](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md) 文章。

### 提交互動式通信或信函 {#letter}

在提交互動式通信或信函時，可以在OSGi上關聯並執行以Forms為中心的工作流。 在通信管理工作流中，用於後處理互動式通信和信件。 例如，發送電子郵件、打印、傳真或存檔最終信件。 有關詳細步驟，請參見 [互動式通信和信函的後處理](../../forms/using/submit-letter-topostprocess.md)。

## 其他配置 {#additional-configurations}

### 配置電子郵件服務 {#configure-email-service}

您可以使用工作流的「分配任務」和「發送電子郵件」AEM步驟來發送電子郵件。 執行以下步驟以指定電子郵件伺服器和發送電子郵件所需的其他配置：

1. 轉到AEM配置管理器 `https://[server]:[port]/system/console/configMgr`。
1. 開啟 **[!UICONTROL 第CQ天郵件服務]** 配置。 為 **[!UICONTROL SMTP伺服器主機名]**。 **[!UICONTROL SMTP伺服器埠，]** 和 **[!UICONTROL &quot;發件人&quot;地址]** 的子菜單。 按一下「**[!UICONTROL 儲存]**」。
1. 開啟 **[!UICONTROL 第CQ天連結外部化程式]** 配置。 在 **[!UICONTROL 域]** 欄位，指定本地、作者和發佈實例的實際主機名/IP地址和埠號。 按一下「**[!UICONTROL 儲存]**」。

### 清除工作流實例 {#purge-workflow-instances}

最大限度地減少工作流實例的數量會提高工作流引擎的效能，因此您可以定期從儲存庫中清除已完成或正在運行的工作流實例。 有關詳細資訊，請參見 [定期清除工作流實例](/help/sites-administering/workflows-administering.md#regular) 清除工作流實例。

## 將敏感資料參數化到工作流變數並儲存在外部資料儲存中 {#externalize-wf-variables}

從自適應表單提交到 [!DNL Experience Manager] 工作流可以包含企業最終用戶的PII（個人身份資訊）或SPD（敏感個人資料）。 但是，並非強制將資料儲存在 [!DNL Adobe Experience Manager] [JCR儲存庫](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr.html)。 通過將資訊參數化到 [工作流變數](/help/forms/using/variable-in-aem-workflows.md)。

在 [!DNL Adobe Experience Manager] Forms工作流，通過工作流變數對資料進行處理和傳遞一系列工作流步驟。 這些變數是儲存在工作流實例元資料節點中的命名屬性或鍵值對；例如 `/var/workflow/instances/<serverid>/<datebucket>/<uniquenameof model>_<id>/data/metaData`。 這些工作流變數可以外部化到JCR以外的單獨儲存庫中，然後由 [!DNL Adobe Experience Manager] 工作流。 [!DNL Adobe Experience Manager] 提供API `[!UICONTROL UserMetaDataPersistenceProvider]` 將工作流變數儲存到托管外部儲存中。 要瞭解有關在中使用客戶擁有的資料儲存的工作流變數的更多資訊 [!DNL Adobe Experience Manager]，請參閱 [管理外部資料儲存的工作流變數](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore)。
[!DNL Adobe] 提供了以下內容 [樣本](https://github.com/adobe/workflow-variable-externalizer) 使用API將變數從工作流元資料映射儲存到Azure Blob儲存 [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md)。 在類似的行上，您可以將示例用作參考 [UserMetaDataPersistenceProvider] API，用於將外部的任何其他資料儲存中的工作流變數外部化 [!DNL Adobe Experience Manager] 並管理同樣的問題。

>[!NOTE]
>
>將工作流變數儲存到外部資料儲存時，請參考 [工作流外部資料儲存指南](#guidelines-workflows-external-data-storage)。

### 安裝工作流API示例實現

要將工作流變數儲存在托管Azure Blob儲存中：
1. 安裝 [樣本](https://github.com/adobe/workflow-variable-externalizer) 工作流API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md) 如下：

   1. 在項目根目錄中運行 `mvn clean install` 命令。

   1. 要部署要創作的包和內容包，請運行 `mvn clean install -PautoInstallPackage`。

   1. 要僅將包部署到作者，請運行 `mvn clean install -PautoInstallBundle`。

1. 初始化外部化程式OSGi配置檔案中的以下屬性 `ui.config` 內容包：

   ```JQL
      accountKey=""
      accountName=""
      endpointSuffix=""
      containerName=""
      protocol=""
   ```

以下是這些屬性的用途（和示例）:

* **帳戶密鑰** 是授權訪問的密鑰。

* **帳戶名** 是必須儲存資料的azure帳戶。

* **終結點尾碼**，例如 `core.windows.net`。

* **容器名稱** 是帳戶中需要儲存資料的容器。 該示例假定容器已存在。

* **協定**，例如 `https` 或 `http`。

1. 在中配置工作流模型 [!DNL Adobe Experience Manager]。 要瞭解如何為外部儲存配置工作流模型，請參見 [配置工作流模型](#configure-aem-wf-model)。

### 在中配置工作流模型 [!DNL Adobe Experience Manager] 用於外部資料儲存 {#configure-aem-wf-model}

要為外部數AEM據儲存配置工作流模型，請執行以下操作：

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。

1. 選取模型名稱並選取 **[!UICONTROL 編輯]**。

1. 選擇「頁面資訊」表徵圖並選擇 **[!UICONTROL 開啟屬性]**。

1. 選擇 **[!UICONTROL 將工作流資料儲存外部化]**。

1. 選擇 **[!UICONTROL 保存並關閉]** 的子菜單。

### 外部資料AEM儲存的工作流指南 {#guidelines-workflows-external-data-storage}

以下是您使用 [!DNL Adobe Experience Manager] 工作流和將資料儲存到外部資料儲存(例如MicrosoftAzure儲存伺服器):

* 在工作流模型步驟中定義輸入和輸出資料檔案和附件時，使用變數來儲存資料。 不選擇 **[!UICONTROL 相對於負載]** 和 **[!UICONTROL 在絕對路徑上可用]** 頁籤 的 **[!UICONTROL 相對於負載]** 和 **[!UICONTROL 在絕對路徑上可用]** 選項在您 [配置 [!DNL Adobe Experience Manager] 外部資料儲存的工作流模型](#configure-aem-wf-model)。

* 在向工作流提交自適應表單時，使用變數來儲存資料檔案和附AEM件。 不選擇 **[!UICONTROL 相對於負載]** 選項 [!DNL Adobe Experience Manager] 工作流。 的 **[!UICONTROL 相對於負載]** 選項在 [配置 [!DNL Adobe Experience Manager] 外部資料儲存的工作流模型](#configure-aem-wf-model)。

* 不使用自定義 [!DNL Adobe Experience Manager] 工作流模型中用於儲存資料的工作流步驟 [!UICONTROL CRX DE] 儲存庫。

* 當你 [配置 [!DNL Adobe Experience Manager] 外部資料儲存的工作流模型](#configure-aem-wf-model)，不建立自定義列 [!DNL Adobe Experience Manager] [!UICONTROL 收件箱] 因為如果自定義列中的工作項位於 [!DNL Adobe Experience Manager] [!UICONTROL 收件箱] 屬於標籤為外部儲存的工作流。
