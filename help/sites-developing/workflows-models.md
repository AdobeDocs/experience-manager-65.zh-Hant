---
title: 建立工作流模型
seo-title: Creating Workflow Models
description: 您可以建立工作流模型，以定義使用者啟動工作流程時執行的一系列步驟。
seo-description: You create a workflow model to define the series of steps executed when a user starts the workflow.
uuid: 31071d3a-d6d5-4476-9ac0-7b335de406d9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c097b60f-bcdf-45de-babe-b4c2e2b746a1
docset: aem65
exl-id: 6790202f-0542-4779-b3ce-d394cdba77b4
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '2464'
ht-degree: 1%

---

# 建立工作流模型{#creating-workflow-models}

>[!CAUTION]
>
>若要使用傳統UI，請參閱 [AEM 6.3檔案](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/workflows-models.html) 以供參考。

您建立 [工作流模型](/help/sites-developing/workflows.md#model) 定義使用者啟動工作流程時執行的一系列步驟。 您也可以定義模型屬性，例如工作流是暫時性的，還是使用多個資源。

使用者啟動工作流程時，會啟動例項；這是相應的運行時模型，建立於 [同步](#sync-your-workflow-generate-a-runtime-model) 您的變更。

## 建立新工作流程 {#creating-a-new-workflow}

首次建立新的工作流模型時，它包含：

* 步驟， **流量開始** 和 **流量結束**.
這些代表工作流程的開始和結束。 這些步驟為必要步驟，無法編輯/移除。
* 範例 **參與者** 已命名步驟 **步驟1**.
此步驟配置為將工作項分配給工作流啟動器。 編輯或刪除此步驟，並視需要新增步驟。

若要使用編輯器建立新工作流程：

1. 開啟 **工作流程模型** 主控台；via **工具**, **工作流程**, **模型** 或，例如： [https://localhost:4502/aem/workflow](https://localhost:4502/aem/workflow)
1. 選擇 **建立**，然後 **建立模型**.
1. 此 **添加工作流模型** 對話框。 輸入 **標題** 和 **名稱** （選用） **完成**.
1. 新模型會列於 **工作流程模型** 控制台。
1. 選取新的工作流程，然後使用 [**編輯** 開啟以進行設定](#editinganexistingworkflow):
   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>如果以寫程式方式建立模型（使用crx套件），您也可以在以下項目中建立子資料夾：
>
>`/var/workflow/models`
>
>例如， `/var/workflow/models/prototypes`
>
>然後，此資料夾可用於 [管理對該資料夾中模型的訪問](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that).

## 編輯工作流程 {#editing-a-workflow}

您可以編輯任何現有的工作流模型以：

* [定義步驟](#addingasteptoamodel-) 和 [參數](#configuring-a-workflow-step)
* 設定工作流程屬性，包括 [階段](#configuring-workflow-stages-that-show-workflow-progress), [工作流程是否為暫時性](#creatingatransientworkflow-) 和/或 [使用多個資源](#configuring-a-workflow-for-multi-resource-support)

編輯 [**預設和/或舊版** （現成）工作流程](#editing-a-default-or-legacy-workflow-for-the-first-time) 有額外的步驟，以確保 [安全副本](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) 會在您進行變更前擷取。

完成工作流程的更新時，您必須使用 **同步** to **生成運行時模型**. 請參閱 [同步您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

### 同步工作流 — 生成運行時模型 {#sync-your-workflow-generate-a-runtime-model}

**同步** （在編輯器工具列中右側）會產生 [運行時模型](/help/sites-developing/workflows.md#runtime-model). 執行階段模型是使用者啟動工作流程時實際使用的模型。 如果您沒有 **同步** 您的變更，則變更將無法在執行階段使用。

當您（或任何其他使用者）對您必須使用的工作流程進行任何變更時 **同步** 生成運行時模型 — 即使單個對話框（例如，步驟）具有自己的保存選項時也是如此。

當更改與運行時（已保存）模型同步時， **同步** 會改為顯示。

有些步驟包含必要欄位和/或內建驗證。 當這些條件不滿足時，將在嘗試 **同步** 模型。 例如，當未為 **參與者** 步驟：

![wf-21](assets/wf-21.png)

### 首次編輯預設或舊版工作流程 {#editing-a-default-or-legacy-workflow-for-the-first-time}

當您開啟 [預設和/或舊模型](/help/sites-developing/workflows.md#workflow-types) 編輯：

* 步驟瀏覽器不可用（左側）。
* 有 **編輯** 動作（右側）。
* 最初，模型及其屬性以只讀模式顯示為：
   * 預設工作流程位於 `/libs`
   * 舊版工作流程位於 `/etc`
選取 
**編輯** 會：
* 將工作流程副本帶入 `/conf`
* 使步驟瀏覽器可用
* 可讓您進行變更

>[!NOTE]
>
>請參閱 [工作流模型的位置](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) 以取得更多資訊。

![wf-22](assets/wf-22.png)

### 向模型添加步驟 {#adding-a-step-to-a-model}

您需要將步驟新增至模型以代表要執行的活動 — 每個步驟都會執行特定活動。 標準AEM例項中提供一系列步驟元件。

當編輯模型時，可用步驟將出現在 **步驟瀏覽器**. 例如：

![wf-10](assets/wf-10.png)

>[!NOTE]
>
>如需隨AEM安裝的主要步驟元件相關資訊，請參閱 [工作流程步驟參考資料](/help/sites-developing/workflows-step-ref.md).

若要將步驟新增至工作流程模型：

1. 開啟現有的工作流模型進行編輯。 從 **工作流程模型** 控制台，選擇所需的模型，然後 **編輯**.
1. 開啟步驟瀏覽器；使用 **切換側面板**，位於頂端工具列的最左側。 您可以在此：

   * **篩選** ，以了解特定步驟。
   * 使用下拉式選取器，將選取範圍限制為特定的一組步驟。
   * 選取「顯示說明」圖示 ![wf-stepinfo-icon](assets/wf-stepinfo-icon.png) 以顯示適當步驟的詳細資訊。

   ![wf-02](assets/wf-02.png)

1. 將適當的步驟拖曳至模型中的所需位置。

   例如， **參與者步驟**.

   新增至流程後，您就可以 [設定步驟](#configuring-a-workflow-step).

   ![wf-03](assets/wf-03.png)

1. 視需要新增多個步驟或其他更新。

   在運行時，按步驟在模型中的顯示順序執行步驟。 添加步驟元件後，可將它們拖動到模型中的不同位置。

   您也可以複製、剪下、貼上、分組或刪除現有步驟；和 [頁面編輯器。](/help/sites-authoring/editing-content.md)

   也可以使用工具欄選項收合/展開分割步驟： ![wf-complasseexpand-toolbar-icon](assets/wf-collapseexpand-toolbar-icon.png)

1. 使用確認變更 **同步** （編輯器工具欄）來產生執行階段模型。

   請參閱 [同步您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

### 設定工作流程步驟 {#configuring-a-workflow-step}

您可以 **設定** 和自訂工作流程步驟的行為，使用 **步驟屬性** 對話框。

1. 若要開啟 **步驟屬性** 對話方塊中的任一步驟：

   * 按一下/點選工作流程模型中的* *步驟，然後選取 **設定** （從元件工具欄）。

   * 按兩下步驟。
   >[!NOTE]
   >
   >如需隨AEM安裝的主要步驟元件相關資訊，請參閱 [工作流程步驟參考資料](/help/sites-developing/workflows-step-ref.md).

1. 設定 **步驟屬性** 視需要；可用的屬性視步驟類型而定，可能還有幾個可用的標籤。 例如，預設 **參與者步驟**，在新工作流程中顯示為 `Step 1`:

   ![wf-11](assets/wf-11.png)

1. 使用勾號確認更新。
1. 使用確認變更 **同步** （編輯器工具欄）來產生執行階段模型。

   請參閱 [同步您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

### 建立暫時性工作流程 {#creating-a-transient-workflow}

您可以建立 [暫時](/help/sites-developing/workflows.md#transient-workflows) 建立新模型時，或編輯現有模型時的工作流模型：

1. 開啟的工作流模型 [編輯](#editinganexistingworkflow).
1. 選擇 **工作流模型屬性** 的上界。
1. 在對話方塊中啟動 **暫時性工作流程** （或視需要停用）:

   ![wf-07](assets/wf-07.png)

1. 確認變更為 **儲存並關閉**;後跟 **同步** （編輯器工具欄）來產生執行階段模型。

   請參閱 [同步您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

>[!NOTE]
>
>當您在 [瞬態](/help/sites-developing/workflows.md#transient-workflows) 模式AEM不會儲存任何工作流程歷史記錄。 因此， [時間表](/help/sites-authoring/basic-handling.md#timeline) 不會顯示與該工作流程相關的任何資訊。

## 讓工作流程模型可在觸控式UI中使用 {#classic2touchui}

如果傳統UI中存在工作流模型，但在 **[!UICONTROL 時間表]** 觸控式UI邊欄，然後依照設定加以使用。 下列步驟將說明如何使用以下稱為的工作流程模型 **[!UICONTROL 啟動請求]**.

1. 確認模型無法在觸控式UI中使用。 使用 `/assets.html/content/dam` 路徑。 選取資產。 開啟 **[!UICONTROL 時間表]** 在左側邊欄。 按一下 **[!UICONTROL 開始工作流程]** 並確認 **[!UICONTROL 啟動請求]** 模型不存在於彈出式清單中。

1. 瀏覽 **[!UICONTROL 工具>一般>標籤]**. 選擇 **[!UICONTROL 工作流程]**.

1. 選擇 **[!UICONTROL 建立>建立標籤]**. 設定 **[!UICONTROL 標題]** as `DAM` 和 **[!UICONTROL 名稱]** as `dam`. 選擇 **[!UICONTROL 提交]**.
   ![在工作流程模型中建立標籤](assets/workflow_create_tag.png)

1. 導覽至 **[!UICONTROL 「工具」>「工作流」>「模型」]**. 選擇 **[!UICONTROL 啟動請求]**，然後選取 **[!UICONTROL 編輯]**.

1. 選擇 **[!UICONTROL 編輯]**，開啟 **[!UICONTROL 頁面資訊]** 菜單，然後從那裡選擇 **[!UICONTROL 開啟屬性]** 然後前往 **[!UICONTROL 基本]** 標籤（如果尚未開啟）。

1. 新增 `Workflow : DAM` to **[!UICONTROL 標籤]** 欄位。 使用勾選（勾選）確認選取項目。

1. 確認新增標籤，並搭配 **[!UICONTROL 儲存並關閉]**.
   ![編輯模型的頁面屬性](assets/workflow_model_edit_activation1.png)

1. 使用 **[!UICONTROL 同步]**. 現在，觸控式UI中提供工作流程。

### 為多資源支援配置工作流 {#configuring-a-workflow-for-multi-resource-support}

您可以為 [多資源支援](/help/sites-developing/workflows.md#multi-resource-support) 建立新模型時，或通過編輯現有模型時：

1. 開啟的工作流模型 [編輯](#editinganexistingworkflow).
1. 選擇 **工作流模型屬性** 的上界。

1. 在對話方塊中啟動 **多資源支援** （或視需要停用）:

   ![wf-08](assets/wf-08.png)

1. 確認變更為 **儲存並關閉**;後跟 **同步** （編輯器工具欄）來產生執行階段模型。

   請參閱 [同步您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

### 配置工作流階段（顯示工作流進度） {#configuring-workflow-stages-that-show-workflow-progress}

[工作流程階段](/help/sites-developing/workflows.md#workflow-stages) 可協助視覺化處理工作流程的進度。

>[!CAUTION]
>
>如果已在 **頁面屬性**，但不會用於任何工作流程步驟，則進度列不會顯示任何進度（無論目前的工作流程步驟為何）。

可用的階段在工作流模型中定義；可以更新現有的工作流模型以包含階段定義。 您可以為工作流模型定義任意數量的階段。

若要定義 **階段** 對於工作流：

1. 開啟工作流程模型以進行編輯。
1. 選擇 **工作流模型屬性** 的上界。 然後開啟 **階段** 標籤。
1. 新增（和定位）您的必要 **階段**. 您可以為工作流模型定義任意數量的階段。

   例如：

   ![wf-08-1](assets/wf-08-1.png)

1. 按一下 **儲存並關閉** 以儲存屬性。
1. 為工作流模型中的每個步驟分配一個階段。 例如：

   ![wf-09](assets/wf-09.png)

   可以將一個階段分配給多個步驟。 例如：

   | **步驟** | **分段** |
   |---|---|
   | 步驟 1 | 建立 |
   | 步驟 2 | 建立 |
   | 步驟 3 | 評論 |
   | 步驟 4 | 批准 |
   | 步驟 5 | 批准 |
   | 步驟 6 | 完成 |

1. 使用確認變更 **同步** （編輯器工具欄）來產生執行階段模型。

   請參閱 [同步您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

## 導出包中的工作流模型 {#exporting-a-workflow-model-in-a-package}

要導出包中的工作流模型，請執行以下操作：

1. 使用 [封裝管理員](/help/sites-administering/package-manager.md#package-manager):

   1. 導覽至封裝管理器，透過 **工具**, **部署**, **套件**.

   1. 按一下 **建立套件**.
   1. 指定 **套件名稱**，以及任何其他必要的詳細資料。
   1. 按一下&#x200B;**「確定」**。

1. 按一下 **編輯** 在新包的工具欄上。

1. 開啟 **篩選器** 標籤。

1. 選擇 **新增篩選** 和指定工作流模型的路徑 *設計*:

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   按一下 **完成**.

1. 選擇 **新增篩選** 並指定 *執行階段* 工作流模型：

   `/var/workflow/models/<*your-model-name*>`

   按一下 **完成**.

1. 為模型使用的任何自訂指令碼新增其他篩選器。
1. 按一下 **儲存** 以確認篩選器定義。
1. 選擇 **建置** 從包定義的工具欄。
1. 選擇 **下載** 從包工具欄。

## 使用工作流程處理表單提交 {#using-workflows-to-process-form-submissions}

您可以設定要由所選工作流程處理的表單。 當使用者提交表單時，會建立新的工作流程例項，並將表單提交的資料作為有效負載。

設定要與表單搭配使用的工作流程：

1. 建立新頁面並開啟它以進行編輯。
1. 新增 **表單** 元件。
1. **設定** the **表單開始** 元件。
1. 使用 **開始工作流程** 若要從這些可用工作流程中選取所需的工作流程：

   ![wf-12](assets/wf-12.png)

1. 使用勾號確認新的表單設定。

## 測試工作流程 {#testing-workflows}

在測試工作流程以使用各種裝載類型時，這是個好作法；包括與已開發的類型不同的類型。 例如，如果您想要處理資產，請將頁面設為裝載以測試工作流程，並確定其不會擲回錯誤。

例如，依照下列方式測試您的新工作流程：

1. [啟動工作流模型](/help/sites-administering/workflows-starting.md) 從主控台。
1. 定義 **裝載** 並確認。

1. 視需要採取動作，以便工作流程繼續進行。
1. 在工作流程執行時監控記錄檔。

您也可以設定AEM以顯示 **除錯** 記錄檔中的訊息。 請參閱 [記錄](/help/sites-deploying/configure-logging.md) 如需詳細資訊及開發完成時，請將 **記錄層級** 返回 **資訊**.

## 範例 {#examples}

### 範例：建立（簡單）工作流以接受或拒絕發佈請求 {#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

為了說明建立工作流程的一些可能性，以下範例會建立 `Publish Example` 工作流程。

1. [建立新的工作流模型](#creating-a-new-workflow).

   新工作流程將包含：

   * **流程啟動**
   * `Step 1`
   * **流程結束**

1. 刪除 `Step 1` （因為此範例的步驟類型錯誤）:

   * 按一下步驟並選取 **刪除** （從元件工具欄）。 確認動作。

1. 從 **工作流程** 選取步驟瀏覽器，拖曳 **參與者步驟** 放到工作流程上，並將其置於 **流量開始** 和 **流量結束**.
1. 要開啟屬性對話框，請執行以下操作：

   * 按一下參與者步驟並選擇 **設定** （從元件工具欄）。
   * 按兩下參與者步驟。

1. 在 **常見** 索引鍵 `Validate Content` 對於 **標題** 和 **說明**.
1. 開啟 **使用者/群組** 標籤：

   * 啟動 **通過電子郵件通知用戶**.
   * 選擇 `Administrator` ( `admin`) **使用者/群組** 欄位。

   >[!NOTE]
   >
   >若要傳送電子郵件， [需要配置郵件服務和用戶帳戶詳細資訊](/help/sites-administering/notification.md).

1. 使用勾號確認更新。

   您將返回至工作流模型的概述，在此處參與者步驟將更名為 `Validate Content`.

1. 拖曳 **或分割** 放到工作流程上，並將其置於 `Validate Content` 和 **流量結束**.
1. 開啟 **或分割** ，以進行設定。
1. 設定:

   * **常見**:指定拆分名稱。
   * **分支1**:選取 **預設路由**.

   * **分支2**:確保 **預設路由** 未選取。

1. 確認更新至 **或分割**.
1. 拖曳 **參與者步驟** 在左側分支中，開啟屬性，指定下列值，然後確認變更：

   * **標題**: `Reject Publish Request`

   * **使用者/群組**:例如， `projects-administrators`

   * **通過電子郵件通知用戶**:啟動，透過電子郵件通知使用者。

1. 拖曳 **處理步驟** 在右側分支中，開啟屬性，指定下列值，然後確認變更：

   * **標題**: `Publish Page as Requested`

   * **程式**:選取 `Activate Page`. 此程式會將選取的頁面發佈至發佈者例項。

1. 按一下 **同步** （編輯器工具欄）來產生執行階段模型。

   請參閱 [同步您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

   您的新工作流程模型將如下所示：

   ![wf-13](assets/wf-13.png)

1. 將此工作流程套用至您的頁面，以便當使用者移至 **完成** the **驗證內容** 步驟，可選取是否要 **按請求發佈頁面**，或 **拒絕發佈請求**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

### 範例：使用ECMA指令碼定義OR拆分的規則 {#defineruleecmascript}

**或分割** 步驟可讓您將條件式處理路徑引入工作流程中。

若要定義OR規則，請依照下列步驟進行：

1. 建立兩個指令碼並儲存在存放庫中，例如：

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   >
   >指令碼必須具有 [函式 `check()`](#function-check) 會傳回布林值。

1. 編輯工作流程並新增 **或分割** 到模型。
1. 編輯 **分支1** 的 **或分割**:

   * 將此定義為 **預設路由** 設定 **值** to `true`.

   * As **規則**，請將路徑設為指令碼。 例如：
      `/apps/myapp/workflow/scripts/myscript1.ecma`
   >[!NOTE]
   >
   >您可以視需要切換分支順序。

1. 編輯 **分支2** 的 **或分割**.

   * As **規則**，請將路徑設定至其他指令碼。 例如：
      `/apps/myapp/workflow/scripts/myscript2.ecma`

1. 設定每個分支中各個步驟的屬性。 請確定 **使用者/群組** 已設定。
1. 按一下 **同步** （編輯器工具列），將變更保留至執行階段模型。

   請參閱 [同步您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

#### 函式檢查() {#function-check}

>[!NOTE]
>
>請參閱 [使用ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).

以下示例指令碼返回 `true` 如果節點是 `JCR_PATH` 位於 `/content/we-retail/us/en`:

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

### 範例：自訂的啟動請求 {#example-customized-request-for-activation}

您可以自訂任何現成可用的工作流程。 若要具有自訂行為，請覆蓋適當工作流程的詳細資訊。

例如， **啟動請求**. 此工作流程用於發佈內的頁面 **網站** 和會在內容作者沒有適當的復寫權限時自動觸發。 請參閱 [自訂頁面編寫 — 自訂啟動工作流程請求](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow) 以取得詳細資訊。
