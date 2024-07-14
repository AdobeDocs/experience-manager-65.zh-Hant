---
title: 建立工作流模型
description: 您可以建立工作流程模型，以定義使用者啟動工作流程時所執行的一系列步驟。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 6790202f-0542-4779-b3ce-d394cdba77b4
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2462'
ht-degree: 2%

---

# 建立工作流模型{#creating-workflow-models}

>[!CAUTION]
>
>若要使用傳統UI，請參閱[AEM 6.3檔案](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/workflows-models.html)以取得參考。

您可以建立[工作流程模型](/help/sites-developing/workflows.md#model)，以定義使用者啟動工作流程時所執行的一系列步驟。 您也可以定義模型屬性，例如工作流程是暫時的或使用多個資源。

當使用者啟動工作流程時，會啟動執行個體；這是對應的執行階段模型，在您[同步](#sync-your-workflow-generate-a-runtime-model)您的變更時建立。

## 建立新工作流程 {#creating-a-new-workflow}

第一次建立工作流程模型時，模型會包含：

* 步驟&#x200B;**流程開始**&#x200B;和&#x200B;**流程結束**。
這些代表工作流程的開始和結束。 這些步驟為必要步驟，無法編輯/移除。
* 名為&#x200B;**步驟1**&#x200B;的範例&#x200B;**參與者**步驟。
此步驟設定為指派工作專案給工作流程發起人。 編輯或刪除此步驟，並視需要新增步驟。

使用編輯器建立工作流程：

1. 開啟&#x200B;**工作流程模型**&#x200B;主控台；透過&#x200B;**工具**、**工作流程**、**模型**&#x200B;或例如：[https://localhost:4502/aem/workflow](https://localhost:4502/aem/workflow)
1. 選取&#x200B;**建立**，然後選取&#x200B;**建立模型**。
1. **新增工作流程模型**&#x200B;對話方塊就會顯示。 在選取&#x200B;**完成**&#x200B;之前，請輸入&#x200B;**標題**&#x200B;和&#x200B;**名稱** （選擇性）。
1. 新模型列在&#x200B;**工作流程模型**&#x200B;主控台中。
1. 選取您的新工作流程，然後使用&#x200B;[**編輯**&#x200B;開啟它以進行設定](#editinganexistingworkflow)：
   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>如果以程式設計方式建立模型（使用crx套件），您也可以在中建立子資料夾：
>
>`/var/workflow/models`
>
>例如 `/var/workflow/models/prototypes`
>
>然後，此資料夾便可用於[管理該資料夾](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)中模型的存取權。

## 編輯工作流程 {#editing-a-workflow}

您可以編輯任何現有的工作流程模型以：

* [定義步驟](#addingasteptoamodel-)及其[引數](#configuring-a-workflow-step)
* 設定工作流程屬性，包括[階段](#configuring-workflow-stages-that-show-workflow-progress)、[工作流程是否為暫時性](#creatingatransientworkflow-)及/或[使用多個資源](#configuring-a-workflow-for-multi-resource-support)

編輯&#x200B;[**預設和/或舊版** （現成可用）工作流程](#editing-a-default-or-legacy-workflow-for-the-first-time)有一個額外的步驟，以確保在您進行變更之前已建立[安全復本](/help/sites-developing/workflows-best-practices.md#locations-workflow-models)。

工作流程更新完成時，您必須使用&#x200B;**同步**&#x200B;到&#x200B;**產生執行階段模型**。 如需詳細資訊，請參閱[同步處理工作流程](#sync-your-workflow-generate-a-runtime-model)。

### 同步處理工作流程 — 產生執行階段模型 {#sync-your-workflow-generate-a-runtime-model}

**Sync** （在編輯器工具列的右側）產生[執行階段模型](/help/sites-developing/workflows.md#runtime-model)。 執行階段模型是使用者啟動工作流程時實際使用的模型。 如果您未&#x200B;**同步**&#x200B;您的變更，則在執行階段將無法使用變更。

當您（或任何其他使用者）對工作流程進行任何變更時，您必須使用&#x200B;**同步**&#x200B;來產生執行階段模型 — 即使個別對話方塊（例如步驟）有自己的儲存選項。

當變更與執行階段（已儲存）模型同步時，會顯示&#x200B;**已同步**。

某些步驟具有必填欄位和/或內建驗證。 當這些條件不滿足時，當您嘗試&#x200B;**同步**&#x200B;模型時會顯示錯誤。 例如，若尚未為&#x200B;**參與者**&#x200B;步驟定義參與者：

![wf-21](assets/wf-21.png)

### 首次編輯預設或舊版工作流程 {#editing-a-default-or-legacy-workflow-for-the-first-time}

當您開啟[預設和/或舊版模型](/help/sites-developing/workflows.md#workflow-types)進行編輯時：

* 步驟瀏覽器無法使用（左側）。
* 工具列（右側）中有&#x200B;**編輯**&#x200B;動作可用。
* 最初，模型及其屬性會以唯讀模式顯示為：
   * 預設工作流程在`/libs`中
   * 舊版工作流程位於`/etc`
選取**編輯**&#x200B;將：
* 將工作流程復本帶入`/conf`
* 讓步驟瀏覽器可供使用
* 讓您進行變更

>[!NOTE]
>
>如需進一步資訊，請參閱[工作流程模型](/help/sites-developing/workflows-best-practices.md#locations-workflow-models)的位置。

![wf-22](assets/wf-22.png)

### 將步驟新增至模型 {#adding-a-step-to-a-model}

將步驟新增至模型以代表要執行的活動 — 每個步驟都會執行特定活動。 標準AEM例項中提供一組步驟元件。

當您編輯模型時，可用的步驟會顯示在&#x200B;**步驟瀏覽器**&#x200B;的各種群組中。 例如：

![wf-10](assets/wf-10.png)

>[!NOTE]
>
>如需有關隨AEM安裝的主要步驟元件的資訊，請參閱[工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)。

若要將步驟新增至工作流程模型：

1. 開啟現有的工作流程模型以進行編輯。 從&#x200B;**工作流程模型**&#x200B;主控台，選取所需的模型，然後選取&#x200B;**編輯**。
1. 開啟「步驟」瀏覽器；使用最左邊頂端工具列的&#x200B;**切換側面板**。 您可以在這裡：

   * **篩選**&#x200B;以取得特定步驟。
   * 使用下拉式選取器，將選取範圍限制在特定的步驟群組中。
   * 選取「顯示說明」圖示![wf-stepinfo-icon](assets/wf-stepinfo-icon.png)以顯示適當步驟的詳細資料。

   ![wf-02](assets/wf-02.png)

1. 將適當的步驟拖曳到模型中的所需位置。

   例如，**參與者步驟**。

   新增至流程後，您可以[設定步驟](#configuring-a-workflow-step)。

   ![wf-03](assets/wf-03.png)

1. 視需要新增任意數量的步驟或其他更新。

   在執行階段，步驟會按照它們在模型中出現的順序執行。 新增步驟元件後，可將其拖曳至模型中的不同位置。

   您也可以複製、剪下、貼上、分組或刪除現有步驟；就像使用[頁面編輯器一樣。](/help/sites-authoring/editing-content.md)

   也可以使用工具列選項摺疊/展開分割步驟： ![wf-collapseexpand-toolbar-icon](assets/wf-collapseexpand-toolbar-icon.png)

1. 使用&#x200B;**Sync** （編輯器工具列）確認變更，以產生執行階段模型。

   如需詳細資訊，請參閱[同步處理工作流程](#sync-your-workflow-generate-a-runtime-model)。

### 設定工作流程步驟 {#configuring-a-workflow-step}

您可以&#x200B;**設定**，並使用&#x200B;**步驟屬性**&#x200B;對話方塊來自訂工作流程步驟的行為。

1. 若要開啟步驟的&#x200B;**步驟屬性**&#x200B;對話方塊：

   * 按一下工作流程模型中的* *步驟，然後從元件工具列選取&#x200B;**設定**。

   * 連按兩下步驟。

   >[!NOTE]
   >
   >如需有關隨AEM安裝的主要步驟元件的資訊，請參閱[工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)。

1. 視需要設定&#x200B;**步驟屬性**；可用的屬性視步驟型別而定，可能也有數個可用的標籤。 例如，預設的&#x200B;**參與者步驟**&#x200B;在新工作流程中顯示為`Step 1`：

   ![wf-11](assets/wf-11.png)

1. 透過勾號確認您的更新。
1. 使用&#x200B;**Sync** （編輯器工具列）確認變更，以產生執行階段模型。

   如需詳細資訊，請參閱[同步處理工作流程](#sync-your-workflow-generate-a-runtime-model)。

### 建立暫時性工作流程 {#creating-a-transient-workflow}

建立模型或編輯現有模型時，您可以建立[暫時性](/help/sites-developing/workflows.md#transient-workflows)工作流程模型：

1. 開啟[編輯](#editinganexistingworkflow)的工作流程模型。
1. 從工具列選取&#x200B;**工作流程模型屬性**。
1. 在對話方塊中，啟動&#x200B;**暫時性工作流程** （或視需要停用）：

   ![wf-07](assets/wf-07.png)

1. 使用&#x200B;**儲存並關閉**&#x200B;確認變更；接著使用&#x200B;**同步** （編輯器工具列）以產生執行階段模型。

   如需詳細資訊，請參閱[同步處理工作流程](#sync-your-workflow-generate-a-runtime-model)。

>[!NOTE]
>
>當您以[暫時](/help/sites-developing/workflows.md#transient-workflows)模式執行工作流程時，AEM不會儲存任何工作流程歷史記錄。 因此，[時間表](/help/sites-authoring/basic-handling.md#timeline)不會顯示與該工作流程相關的任何資訊。

## 在觸控式UI中提供工作流程模型 {#classic2touchui}

如果傳統UI中出現工作流程模型，但在觸控式UI的&#x200B;**[!UICONTROL 時間軸]**&#x200B;邊欄的選取彈出式選單中缺少該模型，則請依照設定使其可用。 下列步驟說明如何使用名為&#x200B;**[!UICONTROL Request for Activation]**&#x200B;的工作流程模型。

1. 確認模型不適用於觸控式UI。 使用`/assets.html/content/dam`路徑存取資產。 選取資產。 在左側邊欄中開啟&#x200B;**[!UICONTROL 時間表]**。 按一下「**[!UICONTROL 啟動工作流程]**」，並確認快顯清單中沒有&#x200B;**[!UICONTROL 啟用請求]**&#x200B;模型。

1. 瀏覽&#x200B;**[!UICONTROL 工具>一般>標籤]**。 選取&#x200B;**[!UICONTROL 工作流程]**。

1. 選取&#x200B;**[!UICONTROL 建立>建立標籤]**。 將&#x200B;**[!UICONTROL Title]**&#x200B;設為`DAM`，並將&#x200B;**[!UICONTROL Name]**&#x200B;設為`dam`。 選取&#x200B;**[!UICONTROL 提交]**。
   ![在工作流程模型中建立標籤](assets/workflow_create_tag.png)

1. 導覽至&#x200B;**[!UICONTROL 工具>工作流程>模型]**。 選取「**[!UICONTROL 啟用請求]**」，然後選取「**[!UICONTROL 編輯]**」。

1. 選取「**[!UICONTROL 編輯]**」，開啟「**[!UICONTROL 頁面資訊]**」功能表，然後從那裡選取「**[!UICONTROL 開啟屬性]**」，並移至「**[!UICONTROL 基本]**」標籤（如果尚未開啟）。

1. 新增`Workflow : DAM`至&#x200B;**[!UICONTROL 標籤]**&#x200B;欄位。 使用核取方塊（勾號）確認選取。

1. 確認使用&#x200B;**[!UICONTROL 儲存並關閉]**新增標籤。
   ![編輯模型](assets/workflow_model_edit_activation1.png)的頁面屬性

1. 使用&#x200B;**[!UICONTROL 同步]**&#x200B;完成程式。 觸控式UI現在提供工作流程。

### 設定多資源支援的工作流程 {#configuring-a-workflow-for-multi-resource-support}

您可以在建立模型或編輯現有模型時，為[多重資源支援](/help/sites-developing/workflows.md#multi-resource-support)設定工作流程模型：

1. 開啟[編輯](#editinganexistingworkflow)的工作流程模型。
1. 從工具列選取&#x200B;**工作流程模型屬性**。

1. 在對話方塊中，啟動&#x200B;**多重資源支援** （或視需要停用）：

   ![wf-08](assets/wf-08.png)

1. 使用&#x200B;**儲存並關閉**&#x200B;確認變更；接著使用&#x200B;**同步** （編輯器工具列）以產生執行階段模型。

   如需詳細資訊，請參閱[同步處理工作流程](#sync-your-workflow-generate-a-runtime-model)。

### 設定工作流程階段（顯示工作流程進度） {#configuring-workflow-stages-that-show-workflow-progress}

[工作流程階段](/help/sites-developing/workflows.md#workflow-stages)有助於在處理任務時以視覺效果呈現工作流程進度。

>[!CAUTION]
>
>如果工作流程階段已在&#x200B;**頁面屬性**&#x200B;中定義，但未用於任何工作流程步驟，則進度列不會顯示任何進度（無論目前的工作流程步驟為何）。

可用的階段會在工作流程模型中定義；現有的工作流程模型可以更新以包含階段定義。 您可以為工作流程模型定義任意數量的階段。

若要定義工作流程的&#x200B;**階段**：

1. 開啟要編輯的工作流程模型。
1. 從工具列選取&#x200B;**工作流程模型屬性**。 然後開啟&#x200B;**階段**&#x200B;標籤。
1. 新增（及定位）您所需的&#x200B;**階段**。 您可以為工作流程模型定義任意數量的階段。

   例如：

   ![wf-08-1](assets/wf-08-1.png)

1. 按一下&#x200B;**儲存並關閉**&#x200B;以儲存屬性。
1. 將階段指派給工作流程模型中的每一個步驟。 例如：

   ![wf-09](assets/wf-09.png)

   一個階段可指派給多個步驟。 例如：

   | **步驟** | **階段** |
   |---|---|
   | 步驟 1 | 建立 |
   | 步驟 2 | 建立 |
   | 步驟 3 | 檢閱 |
   | 步驟 4 | 核准 |
   | 步驟 5 | 核准 |
   | 步驟 6 | 完成 |

1. 使用&#x200B;**Sync** （編輯器工具列）確認變更，以產生執行階段模型。

   如需詳細資訊，請參閱[同步處理工作流程](#sync-your-workflow-generate-a-runtime-model)。

## 在封裝中匯出工作流程模型 {#exporting-a-workflow-model-in-a-package}

若要匯出封裝中的工作流程模型：

1. 使用[封裝管理員](/help/sites-administering/package-manager.md#package-manager)建立封裝：

   1. 透過&#x200B;**工具**、**部署**、**封裝**&#x200B;瀏覽至封裝管理員。

   1. 按一下&#x200B;**建立封裝**。
   1. 指定&#x200B;**封裝名稱**，並視需要指定任何其他詳細資料。
   1. 按一下&#x200B;**「確定」**。

1. 按一下新封裝工具列上的&#x200B;**編輯**。

1. 開啟&#x200B;**篩選器**&#x200B;索引標籤。

1. 選取&#x200B;**新增篩選器**&#x200B;並指定工作流程模型&#x200B;*設計*&#x200B;的路徑：

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   按一下&#x200B;**「完成」**。

1. 選取&#x200B;**新增篩選器**&#x200B;並指定&#x200B;*執行階段*&#x200B;工作流程模型的路徑：

   `/var/workflow/models/<*your-model-name*>`

   按一下&#x200B;**「完成」**。

1. 為您的模型使用的任何自訂指令碼新增其他篩選器。
1. 按一下&#x200B;**儲存**&#x200B;以確認您的篩選器定義。
1. 從封裝定義的工具列選取&#x200B;**建置**。
1. 從封裝工具列選取&#x200B;**下載**。

## 使用工作流程處理表單提交 {#using-workflows-to-process-form-submissions}

您可以設定要由所選工作流程處理的表單。 使用者提交表單時，會建立新的工作流程例項，並將表單提交的資料當作其裝載。

若要設定要與表單搭配使用的工作流程：

1. 建立頁面並開啟以進行編輯。
1. 新增&#x200B;**表單**&#x200B;元件至頁面。
1. **設定**&#x200B;出現在頁面中的&#x200B;**表單開始**&#x200B;元件。
1. 使用&#x200B;**開始工作流程**&#x200B;從可用的工作流程中選取所需的工作流程：

   ![wf-12](assets/wf-12.png)

1. 勾選記號以確認新表單設定。

## 測試工作流程 {#testing-workflows}

測試工作流程時，良好的實務是使用各種裝載型別；包括與開發工作流程的不同型別。 例如，如果您打算讓工作流程處理Assets，請將頁面設定為裝載，以測試工作流程，確認工作流程不會擲回錯誤。

例如，測試您的新工作流程，如下所示：

1. [從主控台啟動您的工作流程模型](/help/sites-administering/workflows-starting.md)。
1. 定義&#x200B;**承載**&#x200B;並確認。

1. 視需要採取動作，以便進行工作流程。
1. 在工作流程執行時監視記錄檔。

您也可以設定AEM在記錄檔中顯示&#x200B;**DEBUG**&#x200B;訊息。 請參閱[記錄](/help/sites-deploying/configure-logging.md)以取得進一步資訊，當開發完成時，請將&#x200B;**記錄層級**&#x200B;設定回&#x200B;**資訊**。

## 範例 {#examples}

### 範例：建立（簡單）工作流程以接受或拒絕發佈請求 {#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

為了說明建立工作流程的一些可能性，以下範例會建立`Publish Example`工作流程的變數。

1. [建立工作流程模型](#creating-a-new-workflow)。

   新工作流程將包含：

   * **流程開始**
   * `Step 1`
   * **流程結束**

1. 刪除`Step 1` （因為此範例的步驟型別錯誤）：

   * 按一下步驟並從元件工具列選取&#x200B;**刪除**。 確認動作。

1. 從&#x200B;**工作流程**&#x200B;選取的步驟瀏覽器中，將&#x200B;**參與者步驟**&#x200B;拖曳到工作流程上，並將其置於&#x200B;**流程開始**&#x200B;和&#x200B;**流程結束**&#x200B;之間。
1. 若要開啟「屬性」對話方塊，請執行下列動作：

   * 按一下參與者步驟，然後從元件工具列選取&#x200B;**設定**。
   * 連按兩下參與者步驟。

1. 在&#x200B;**一般**&#x200B;索引標籤中，為&#x200B;**標題**&#x200B;和&#x200B;**描述**&#x200B;輸入`Validate Content`。
1. 開啟&#x200B;**使用者/群組**&#x200B;標籤：

   * 啟動&#x200B;**透過電子郵件**&#x200B;通知使用者。
   * 選取&#x200B;**使用者/群組**&#x200B;欄位的`Administrator` ( `admin`)。

   >[!NOTE]
   >
   >若要傳送電子郵件，[需要設定郵件服務和使用者帳戶詳細資料](/help/sites-administering/notification.md)。

1. 透過勾號確認更新。

   您將會返回工作流程模型的概觀，在此參與者步驟將會重新命名為`Validate Content`。

1. 將&#x200B;**或Split**&#x200B;拖曳到工作流程上，並將其置於`Validate Content`和&#x200B;**流程結束**&#x200B;之間。
1. 開啟&#x200B;**或分割**&#x200B;以進行設定。
1. 設定：

   * **一般**：指定分割名稱。
   * **分支1**：選取&#x200B;**預設路由**。

   * **分支2**：確定未選取&#x200B;**預設路由**。

1. 確認您的&#x200B;**OR Split**&#x200B;更新。
1. 將&#x200B;**參與者步驟**&#x200B;拖曳至左側分支、開啟屬性、指定下列值，然後確認變更：

   * **標題**： `Reject Publish Request`

   * **使用者/群組**：例如，`projects-administrators`

   * **透過電子郵件通知使用者**：啟動以透過電子郵件通知使用者。

1. 將&#x200B;**處理步驟**&#x200B;拖曳到右側分支、開啟屬性、指定下列值，然後確認變更：

   * **標題**： `Publish Page as Requested`

   * **處理序**：選取`Activate Page`。 此程式會將選取的頁面發佈至發佈者執行處理。

1. 按一下&#x200B;**同步** （編輯器工具列）以產生執行階段模型。

   如需詳細資訊，請參閱[同步處理工作流程](#sync-your-workflow-generate-a-runtime-model)。

   您的新工作流程模型看起來會像這樣：

   ![wf-13](assets/wf-13.png)

1. 將此工作流程套用至您的頁面，以便當使用者移至&#x200B;**完成** **驗證內容**&#x200B;步驟時，他們可以選擇是否要依要求&#x200B;**Publish頁面**，或&#x200B;**拒絕Publish要求**。

   ![chlimage_1-72](assets/chlimage_1-72.png)

### 範例：使用ECMA命令檔定義OR分割的規則 {#defineruleecmascript}

**OR分割**&#x200B;步驟可讓您在工作流程中匯入條件式處理路徑。

若要定義OR規則，請依照下列步驟進行：

1. 建立兩個指令碼並將它們儲存在存放庫中，例如，在下方：

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   >
   >指令碼必須有傳回布林值的[函式`check()`](#function-check)。

1. 編輯工作流程並將&#x200B;**OR Split**&#x200B;新增至模型。
1. 編輯&#x200B;**OR分割**&#x200B;的&#x200B;**分支1**&#x200B;的屬性：

   * 透過將&#x200B;**值**&#x200B;設定為`true`，將此定義為&#x200B;**預設路由**。

   * 作為&#x200B;**規則**，設定指令碼的路徑。 例如：
     `/apps/myapp/workflow/scripts/myscript1.ecma`

   >[!NOTE]
   >
   >您可以視需要切換分支順序。

1. 編輯&#x200B;**OR分割**&#x200B;的&#x200B;**分支2**&#x200B;的屬性。

   * 作為&#x200B;**規則**，設定其他指令碼的路徑。 例如：
     `/apps/myapp/workflow/scripts/myscript2.ecma`

1. 設定每個分支中個別步驟的屬性。 請確定已設定&#x200B;**使用者/群組**。
1. 按一下&#x200B;**同步** （編輯器工具列）以保留您對執行階段模型的變更。

   如需詳細資訊，請參閱[同步處理工作流程](#sync-your-workflow-generate-a-runtime-model)。

#### 函式Check() {#function-check}

>[!NOTE]
>
>請參閱[使用ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript)。

如果節點是位於`/content/we-retail/us/en`下的`JCR_PATH`，則下列範例指令碼會傳回`true`：

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

### 範例：自訂的啟用請求 {#example-customized-request-for-activation}

您可以自訂任何現成的工作流程。 若要使用自訂行為，請覆蓋適當工作流程的詳細資料。

例如，**要求啟用**。 此工作流程用於發佈&#x200B;**Sites**&#x200B;內的頁面，並在內容作者沒有適當的復寫許可權時自動觸發。 如需詳細資訊，請參閱[自訂頁面編寫 — 自訂啟動工作流程請求](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow)。
