---
title: 建立工作流模型
seo-title: 建立工作流模型
description: 您可以建立工作流模型，以定義當使用者啟動工作流時執行的一系列步驟。
seo-description: 您可以建立工作流模型，以定義當使用者啟動工作流時執行的一系列步驟。
uuid: 31071d3a-d6d5-4476-9ac0-7b335de406d9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c097b60f-bcdf-45de-babe-b4c2e2b746a1
docset: aem65
translation-type: tm+mt
source-git-commit: 9f260d3ccb98409790cd18b2540329fc36a07c05
workflow-type: tm+mt
source-wordcount: '2485'
ht-degree: 1%

---


# 建立工作流模型{#creating-workflow-models}

>[!CAUTION]
>
>如需使用傳統UI，請參閱[AEM 6.3檔案](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/workflows-models.html)以取得參考。

您可以建立[工作流模型](/help/sites-developing/workflows.md#model)，以定義使用者啟動工作流時執行的一系列步驟。 您也可以定義模型屬性，例如工作流程是暫時性的，還是使用多個資源。

當用戶啟動工作流時，會啟動一個實例；這是在您[Sync](#sync-your-workflow-generate-a-runtime-model)變更時建立的對應執行階段模型。

## 建立新工作流{#creating-a-new-workflow}

首次建立新的工作流模型時，它包含：

* 步驟：**流開始**&#x200B;和&#x200B;**流結束**。
這些代表工作流程的開始和結束。 這些步驟是必要的，無法編輯／移除。
* **Participant**&#x200B;步驟範例，名為&#x200B;**Step 1**。
此步驟配置為將工作項目分配給工作流啟動器。 編輯或刪除此步驟，並視需要新增步驟。

要使用編輯器建立新工作流，請執行以下操作：

1. 開啟&#x200B;**工作流模型**&#x200B;控制台；通過&#x200B;**Tools**、**Workflow**、**Models**&#x200B;或例如：[https://localhost:4502/aem/workflow](https://localhost:4502/aem/workflow)
1. 選擇&#x200B;**建立**，然後選擇&#x200B;**建立模型**。
1. 此時將顯示&#x200B;**添加工作流模型**&#x200B;對話框。 在選擇&#x200B;**Done**&#x200B;之前，輸入&#x200B;**Title**&#x200B;和&#x200B;**Name**（可選）。
1. 新型號列在&#x200B;**Workflow Models**&#x200B;控制台中。
1. 選擇新的工作流，然後使用&#x200B;[**Edit**&#x200B;開啟它以進行配置：](#editinganexistingworkflow)
   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>如果以寫程式方式建立模型（使用crx包），則還可以在以下位置建立子資料夾：
>
>`/var/workflow/models`
>
>例如， `/var/workflow/models/prototypes`
>
>然後，此資料夾可用於[管理對該資料夾](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)中模型的訪問。

## 編輯工作流{#editing-a-workflow}

您可以編輯任何現有的工作流模型，以：

* [定義步](#addingasteptoamodel-) 驟及其參 [數](#configuring-a-workflow-step)
* 配置工作流屬性，包括[stages](#configuring-workflow-stages-that-show-workflow-progress)、[是否是transient](#creatingatransientworkflow-)和／或[使用多個資源](#configuring-a-workflow-for-multi-resource-support)

編輯&#x200B;[**預設和／或舊版**（現成可用）工作流程](#editing-a-default-or-legacy-workflow-for-the-first-time)有額外的步驟，以確保在您進行變更之前先執行[安全副本](/help/sites-developing/workflows-best-practices.md#locations-workflow-models)。

完成對工作流的更新後，必須使用&#x200B;**Sync**&#x200B;到&#x200B;**生成運行時模型**。 如需詳細資訊，請參閱[同步您的工作流程](#sync-your-workflow-generate-a-runtime-model)。

### 同步您的工作流程——產生執行階段模型{#sync-your-workflow-generate-a-runtime-model}

**Sync** （位於編輯器工具列中）會產生執行 [時期模型](/help/sites-developing/workflows.md#runtime-model)。執行時期模型是使用者啟動工作流程時實際使用的模型。 如果您未&#x200B;**Sync**&#x200B;您所做的變更，則這些變更將無法在執行時期使用。

當您（或任何其他使用者）對工作流程進行任何變更時，您必須使用&#x200B;**Sync**&#x200B;來產生執行階段模型——即使個別對話方塊（例如，步驟）有其自己的儲存選項。

當變更與執行階段（儲存）模型同步時，會改為顯示&#x200B;**Synched**。

有些步驟包含必填欄位和／或內建驗證。 當這些條件不滿足時，當您嘗試&#x200B;**Sync**&#x200B;模型時，將顯示錯誤。 例如，當&#x200B;**Participant**&#x200B;步驟未定義參與者時：

![wf-21](assets/wf-21.png)

### 首次編輯預設或舊工作流{#editing-a-default-or-legacy-workflow-for-the-first-time}

當您開啟[Default和／或Legacy model](/help/sites-developing/workflows.md#workflow-types)進行編輯時：

* 「步驟」瀏覽器不可用（左側）。
* 工具列（右側）有&#x200B;**Edit**&#x200B;動作。
* 最初，模型及其屬性以只讀模式顯示為：
   * 預設工作流程位於`/libs`
   * 舊式工作流程位於`/etc`
選擇 
**編** 輯：
* 將工作流程的副本放入`/conf`
* 使步驟瀏覽器可用
* 可讓您進行變更

>[!NOTE]
>
>如需詳細資訊，請參閱[工作流程模型位置](/help/sites-developing/workflows-best-practices.md#locations-workflow-models)。

![wf-22](assets/wf-22.png)

### 將步驟添加到模型{#adding-a-step-to-a-model}

您需要將步驟新增至模型以表示要執行的活動——每個步驟都會執行特定活動。 標準AEM例項中提供一系列步驟元件。

編輯模型時，可用步驟會顯示在&#x200B;**步驟瀏覽器**&#x200B;的各組中。 例如：

![wf-10](assets/wf-10.png)

>[!NOTE]
>
>如需隨AEM安裝的主要步驟元件的詳細資訊，請參閱[工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)。

要向工作流模型添加步驟：

1. 開啟現有的工作流程模型以進行編輯。 從&#x200B;**工作流模型**&#x200B;控制台中，選擇所需的模型，然後選擇&#x200B;**編輯**。
1. 開啟「步驟」瀏覽器；使用&#x200B;**在頂端工具列最左側切換側面板**。 您可以：

   * **篩** 選特定步驟。
   * 使用下拉式選擇器，將選取範圍限制為特定的步驟群組。
   * 選擇「顯示說明」表徵圖![wf-stepinfo-icon](assets/wf-stepinfo-icon.png)以顯示有關相應步驟的詳細資訊。

   ![wf-02](assets/wf-02.png)

1. 將適當的步驟拖動到模型中的所需位置。

   例如，**參與者步驟**。

   將步驟添加到流後，您可以[配置步驟](#configuring-a-workflow-step)。

   ![wf-03](assets/wf-03.png)

1. 視需要新增多個步驟或其他更新。

   在運行時，會按照步驟在模型中的顯示順序執行步驟。 添加步驟元件後，可將它們拖動到模型中的不同位置。

   您也可以複製、剪下、貼上、群組或刪除現有步驟；與[頁面編輯器一樣。](/help/sites-authoring/editing-content.md)

   使用工具欄選項也可折疊／展開拆分步驟：![wf-coverlanseexpand-toolbar-icon](assets/wf-collapseexpand-toolbar-icon.png)

1. 使用&#x200B;**Sync**（編輯器工具列）確認變更，以產生執行階段模型。

   如需詳細資訊，請參閱[同步您的工作流程](#sync-your-workflow-generate-a-runtime-model)。

### 配置工作流步驟{#configuring-a-workflow-step}

您可以使用&#x200B;**「步驟屬性」對話框，來配置**&#x200B;並自定義工作流步驟的行為。****

1. 要開啟步驟的&#x200B;**步驟屬性**&#x200B;對話框，請執行以下操作：

   * 按一下／點選工作流模型中的* *步驟，然後從元件工具欄中選擇&#x200B;**Configure**。

   * 按兩下該步驟。
   >[!NOTE]
   >
   >如需隨AEM安裝的主要步驟元件的詳細資訊，請參閱[工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)。

1. 根據需要配置&#x200B;**步驟屬性**;可用的屬性取決於步驟類型，可能還有幾個頁籤可用。 例如，新工作流中預設的&#x200B;**參與者步驟**&#x200B;顯示為`Step 1`:

   ![wf-11](assets/wf-11.png)

1. 以勾號確認更新。
1. 使用&#x200B;**Sync**（編輯器工具列）確認變更，以產生執行階段模型。

   如需詳細資訊，請參閱[同步您的工作流程](#sync-your-workflow-generate-a-runtime-model)。

### 建立臨時工作流{#creating-a-transient-workflow}

在建立新模型或通過編輯現有模型時，可以建立[Transient](/help/sites-developing/workflows.md#transient-workflows)工作流模型：

1. 開啟[編輯](#editinganexistingworkflow)的工作流程模型。
1. 從工具欄中選擇&#x200B;**Workflow Model Properties**。
1. 在對話框中激活&#x200B;**瞬態工作流**（如果需要，則禁用）:

   ![wf-07](assets/wf-07.png)

1. 使用&#x200B;**Save &amp; Close**&#x200B;確認變更；後跟&#x200B;**Sync**（編輯器工具列），以產生執行時期模型。

   如需詳細資訊，請參閱[同步您的工作流程](#sync-your-workflow-generate-a-runtime-model)。

>[!NOTE]
>
>當您在[transient](/help/sites-developing/workflows.md#transient-workflows)模式中執行工作流程時，AEM不會儲存任何工作流程記錄。 因此，[時間軸](/help/sites-authoring/basic-handling.md#timeline)不會顯示任何與該工作流程相關的資訊。[](/help/sites-authoring/basic-handling.md#timeline)

## 在Touch UI {#classic2touchui}中提供工作流程模型

如果Classic UI中存在工作流程模型，但Touch UI的&#x200B;**[!UICONTROL Timeline]**&#x200B;邊欄中的選擇彈出式選單中遺失，則請依照設定進行，以便使用。 以下步驟說明如何使用名為&#x200B;**[!UICONTROL 啟動要求]**&#x200B;的工作流程模型。

1. 確認該型號未在啟用觸控的UI中使用。 使用`/assets.html/content/dam`路徑存取資產。 選取資產。 在左側導軌中開啟&#x200B;**[!UICONTROL 時間軸]**。 按一下「啟動工作流程」**[!UICONTROL 並確認彈出式清單中未顯示**[!UICONTROL &#x200B;啟動要求&#x200B;]**模型。]**

1. 瀏覽&#x200B;**[!UICONTROL 工具>一般>標籤]**。 選擇&#x200B;**[!UICONTROL Workflow]**。

1. 選擇&#x200B;**[!UICONTROL 「建立」>「建立標籤」]**。 將&#x200B;**[!UICONTROL Title]**&#x200B;設為`DAM`，將&#x200B;**[!UICONTROL Name]**&#x200B;設為`dam`。 選擇&#x200B;**[!UICONTROL 提交]**。
   ![在工作流程模型中建立標籤](assets/workflow_create_tag.png)

1. 導覽至「**[!UICONTROL 工具>工作流程>模型]**」。 選擇&#x200B;**[!UICONTROL 請求激活]**，然後選擇&#x200B;**[!UICONTROL 編輯]**。

1. 選擇&#x200B;**[!UICONTROL 編輯]**，開啟&#x200B;**[!UICONTROL 頁面資訊]**&#x200B;菜單，然後從中選擇&#x200B;**[!UICONTROL 開啟屬性]**&#x200B;並轉至&#x200B;**[!UICONTROL 基本]**&#x200B;頁籤（如果尚未開啟）。

1. 將`Workflow : DAM`新增至&#x200B;**[!UICONTROL Tags]**&#x200B;欄位。 使用勾選（勾選）確認選取範圍。

1. 確認添加標籤時使用&#x200B;**[!UICONTROL 保存並關閉]**。
   ![編輯模型的頁面屬性](assets/workflow_model_edit_activation1.png)

1. 使用&#x200B;**[!UICONTROL Sync]**&#x200B;完成該過程。 現在可在觸控式UI中使用工作流程。

### 為多資源支援配置工作流{#configuring-a-workflow-for-multi-resource-support}

建立新模型或編輯現有模型時，可以為[多資源支援](/help/sites-developing/workflows.md#multi-resource-support)配置工作流模型：

1. 開啟[編輯](#editinganexistingworkflow)的工作流程模型。
1. 從工具欄中選擇&#x200B;**Workflow Model Properties**。

1. 在對話框中激活&#x200B;**多資源支援**（如果需要，則禁用）:

   ![wf-08](assets/wf-08.png)

1. 使用&#x200B;**Save &amp; Close**&#x200B;確認變更；後跟&#x200B;**Sync**（編輯器工具列），以產生執行時期模型。

   如需詳細資訊，請參閱[同步您的工作流程](#sync-your-workflow-generate-a-runtime-model)。

### 配置工作流階段（顯示工作流進度）{#configuring-workflow-stages-that-show-workflow-progress}

[工作](/help/sites-developing/workflows.md#workflow-stages) 流程階段可協助在處理工作時視覺化工作流程的進度。

>[!CAUTION]
>
>如果在&#x200B;**頁面屬性**&#x200B;中定義了工作流階段，但未用於任何工作流步驟，則進度欄將不顯示任何進度（無論當前工作流步驟如何）。

可用階段在工作流模型中定義；可更新現有的工作流程模型，以包含階段定義。 可以為工作流模型定義任意數量的階段。

要為工作流定義&#x200B;**階段**:

1. 開啟您的工作流程模型以進行編輯。
1. 從工具欄中選擇&#x200B;**Workflow Model Properties**。 然後開啟&#x200B;**階段**&#x200B;頁籤。
1. 添加（並定位）所需的&#x200B;**階段**。 可以為工作流模型定義任意數量的階段。

   例如：

   ![wf-08-1](assets/wf-08-1.png)

1. 按一下&#x200B;**保存並關閉**&#x200B;以保存屬性。
1. 為工作流模型中的每個步驟指定一個階段。 例如：

   ![wf-09](assets/wf-09.png)

   一個階段可指派給多個步驟。 例如：

   | **步驟** | **分段** |
   |---|---|
   | 步驟 1 | 建立 |
   | 步驟 2 | 建立 |
   | 步驟 3 | 評論 |
   | 步驟 4 | 批准 |
   | 步驟 5 | 批准 |
   | 步驟 6 | 完成 |

1. 使用&#x200B;**Sync**（編輯器工具列）確認變更，以產生執行階段模型。

   如需詳細資訊，請參閱[同步您的工作流程](#sync-your-workflow-generate-a-runtime-model)。

## 導出包{#exporting-a-workflow-model-in-a-package}中的工作流模型

要導出包中的工作流模型，請執行以下操作：

1. 使用[Package Manager](/help/sites-administering/package-manager.md#package-manager)建立新包：

   1. 通過&#x200B;**工具**、**部署**、**軟體包**&#x200B;導航到軟體包管理器。

   1. 按一下「建立包」。****
   1. 根據需要指定&#x200B;**軟體包名稱**&#x200B;和任何其他詳細資訊。
   1. 按一下&#x200B;**「確定」**。

1. 按一下新包工具欄上的&#x200B;**編輯**。

1. 開啟&#x200B;**Filters**&#x200B;標籤。

1. 選擇&#x200B;**添加過濾器**&#x200B;並指定工作流模型&#x200B;*design*&#x200B;的路徑：

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   按一下&#x200B;**Done**。

1. 選擇&#x200B;**添加篩選器**&#x200B;並指定&#x200B;*runtime*&#x200B;工作流模型的路徑：

   `/var/workflow/models/<*your-model-name*>`

   按一下&#x200B;**Done**。

1. 為模型使用的任何自訂指令碼新增其他篩選器。
1. 按一下&#x200B;**Save**&#x200B;以確認您的篩選定義。
1. 從軟體包定義的工具欄中選擇&#x200B;**Build**。
1. 從軟體包工具欄中選擇&#x200B;**Download**。

## 使用工作流處理表單提交{#using-workflows-to-process-form-submissions}

您可以設定表單，以便由選取的工作流程處理。 當使用者送出表單時，會建立新的工作流程例項，並將表單提交的資料當做其負載。

要配置要與表單一起使用的工作流，請執行以下操作：

1. 建立新頁面並開啟以供編輯。
1. 將&#x200B;**Form**&#x200B;元件新增至頁面。
1. **配** 置在頁 **面** 中顯示的Form Start元件。
1. 使用&#x200B;**啟動工作流**&#x200B;從可用工作流中選擇所需的工作流：

   ![wf-12](assets/wf-12.png)

1. 使用勾號確認新表格設定。

## 測試工作流程{#testing-workflows}

在測試工作流使用多種負載類型時，這是一個很好的做法；包括與已開發的不同類型。 例如，如果您想要處理「資產」的工作流程，請將「頁面」設為裝載來測試，並確定不會擲回錯誤。

例如，請依下列方式測試您的新工作流程：

1. [從主控台啟](/help/sites-administering/workflows-starting.md) 動您的工作流程模型。
1. 定義&#x200B;**Payload**&#x200B;並確認。

1. 視需要採取動作，以便工作流程繼續進行。
1. 在工作流程執行時監控記錄檔。

您也可以設定AEM，在記錄檔中顯示&#x200B;**DEBUG**&#x200B;訊息。 如需詳細資訊，請參閱[記錄](/help/sites-deploying/configure-logging.md)，當開發完成時，將&#x200B;**記錄層級**&#x200B;設回&#x200B;**資訊**。

## 範例{#examples}

### 範例：建立（簡單）工作流以接受或拒絕發佈請求{#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

為了說明建立工作流的一些可能性，以下示例建立了`Publish Example`工作流的變化。

1. [建立新的工作流程模型](#creating-a-new-workflow)。

   新工作流程將包含：

   * **流程啟動**
   * `Step 1`
   * **流程結束**

1. 刪除`Step 1`（因為此示例的步驟類型錯誤）:

   * 按一下該步驟，然後從元件工具欄中選擇&#x200B;**Delete**。 確認動作。

1. 從步驟瀏覽器的&#x200B;**Workflow**&#x200B;選擇中，將&#x200B;**參與者步驟**&#x200B;拖曳到工作流上，並將它定位在&#x200B;**Flow Start**&#x200B;和&#x200B;**Flow End**&#x200B;之間。
1. 要開啟屬性對話框，請執行以下操作：

   * 按一下參與者步驟，然後從元件工具欄中選擇&#x200B;**Configure**。
   * 按兩下參與者步驟。

1. 在&#x200B;**Common**&#x200B;標籤中，輸入`Validate Content`**Title**&#x200B;和&#x200B;**Description**。
1. 開啟&#x200B;**用戶／組**&#x200B;頁籤：

   * 啟用&#x200B;**透過電子郵件**&#x200B;通知使用者。
   * 選擇`Administrator`(`admin`)作為&#x200B;**用戶／組**&#x200B;欄位。

   >[!NOTE]
   >
   >對於要發送的電子郵件，[需要配置郵件服務和用戶帳戶詳細資訊](/help/sites-administering/notification.md)。

1. 用勾號確認更新。

   您將返回至工作流模型的概述，此處參與者步驟將重新命名為`Validate Content`。

1. 將&#x200B;**Or Split**&#x200B;拖曳至工作流程，並將它置於`Validate Content`和&#x200B;**Flow End**&#x200B;之間。
1. 開啟&#x200B;**Or Split**&#x200B;進行配置。
1. 設定：

   * **常見**:指定拆分名稱。
   * **分支1**:選擇 **預設路由**。

   * **分支2**:確保 **未選** 擇預設路由。

1. 確認您對&#x200B;**OR Split**&#x200B;的更新。
1. 將&#x200B;**參與者步驟**&#x200B;拖曳至左側分支，開啟屬性，指定下列值，然後確認變更：

   * **標題**: `Reject Publish Request`

   * **使用者／群組**:例如，  `projects-administrators`

   * **透過電子郵件通知使用者**:啟用，讓使用者透過電子郵件獲得通知。

1. 將&#x200B;**處理步驟**&#x200B;拖曳至右側的分支，開啟屬性，指定下列值，然後確認變更：

   * **標題**: `Publish Page as Requested`

   * **流程**:選擇「 `Activate Page`Select（選擇）」。此程式會將選取的頁面發佈至發佈者例項。

1. 按一下&#x200B;**Sync**（編輯器工具欄）以生成運行時模型。

   如需詳細資訊，請參閱[同步您的工作流程](#sync-your-workflow-generate-a-runtime-model)。

   您的新工作流程模型如下：

   ![wf-13](assets/wf-13.png)

1. 將此工作流程套用至您的頁面，如此當使用者移至&#x200B;**完成**「驗證內容」步驟時，他們可以選取要「依請求發佈頁面」或「拒絕發佈請求」。************

   ![chlimage_1-72](assets/chlimage_1-72.png)

### 範例：使用ECMA指令碼{#defineruleecmascript}定義OR拆分的規則

**OR拆分** 步驟可讓您在工作流程中引入條件式處理路徑。

要定義OR規則，請按如下步驟進行：

1. 建立兩個指令碼並將其保存到儲存庫中，例如：

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   >
   >指令碼必須具有[函式`check()`](#function-check)，該函式返回布爾值。

1. 編輯工作流並將&#x200B;**OR Split**&#x200B;添加到模型中。
1. 編輯&#x200B;**OR Split**&#x200B;的&#x200B;**Branch 1**&#x200B;屬性：

   * 通過將&#x200B;**Value**&#x200B;設定為`true`，將此定義為&#x200B;**預設路由**。

   * 以&#x200B;**Rule**的形式，設定指令碼的路徑。 例如：
      `/apps/myapp/workflow/scripts/myscript1.ecma`
   >[!NOTE]
   >
   >您可以視需要切換分支順序。

1. 編輯&#x200B;**OR Split**&#x200B;的&#x200B;**Branch 2**&#x200B;的屬性。

   * 以&#x200B;**Rule**的形式，將路徑設定為其他指令碼。 例如：
      `/apps/myapp/workflow/scripts/myscript2.ecma`

1. 設定每個分支中各步驟的屬性。 請確定已設定&#x200B;**User/Group**。
1. 按一下&#x200B;**Sync**（編輯器工具列），將變更保留至執行階段模型。

   如需詳細資訊，請參閱[同步您的工作流程](#sync-your-workflow-generate-a-runtime-model)。

#### 函式檢查(){#function-check}

>[!NOTE]
>
>請參閱[使用ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript)。

如果節點位於`/content/we-retail/us/en`下方的`JCR_PATH`，則以下示例指令碼返回`true`:

```
function check() {
    if (workflowData.getPayloadType() == "JCR_PATH") {
      var path = workflowData.getPayload().toString();
      var node = jcrSession.getItem(path);

      if (node.getPath().indexOf("/content/we-retail/us/en") >= 0) {
       return true;
      } else {
       return false;
      }
     } else {
      return false;
     }
}
```

### 範例：自訂啟動要求{#example-customized-request-for-activation}

您可以自訂任何現成可用的工作流程。 若要進行自訂行為，請覆蓋適當工作流程的詳細資訊。

例如，**啟動要求**。 此工作流程用於發佈&#x200B;**Sites**&#x200B;內的頁面，當內容作者沒有適當的複製權限時會自動觸發。 如需詳細資訊，請參閱[自訂頁面編寫——自訂啟動工作流程的要求](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow)。
