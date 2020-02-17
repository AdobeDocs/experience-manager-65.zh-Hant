---
title: 開發和擴充工作流程
seo-title: 開發和擴充工作流程
description: AEM提供數種工具和資源，以建立工作流程模型、開發工作流程步驟，以及以程式設計方式與工作流程互動
seo-description: AEM提供數種工具和資源，以建立工作流程模型、開發工作流程步驟，以及以程式設計方式與工作流程互動
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# 開發和擴充工作流程{#developing-and-extending-workflows}

AEM提供數種工具和資源，以建立工作流程模型、開發工作流程步驟，以及以程式設計方式與工作流程互動。

工作流程可讓您自動化在AEM環境中管理資源和發佈內容的程式。 工作流程由一系列步驟組成，每個步驟都可完成個別工作。 您可以使用邏輯和執行時期資料來決定何時可以繼續處理程式，並從多個可能的步驟中選擇下一步驟。

例如，建立和發佈網頁的商業程式包括不同參與者的核准和簽署工作。 這些程式可使用AEM工作流程建立模型，並套用至特定內容。

以下是主要方面，而下列頁面則涵蓋更多詳細資訊：

* [建立工作流模型](/help/sites-developing/workflows-models.md)
* [擴充工作流程功能](/help/sites-developing/workflows-customizing-extending.md)
* [以程式設計方式與工作流程互動](/help/sites-developing/workflows-program-interaction.md)
* [工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)
* [工作流進程參考](/help/sites-developing/workflows-process-ref.md)
* [工作流程最佳實務](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>如需下列相關資訊：
>
>* 參與工作流程，請參閱使 [用工作流程](/help/sites-authoring/workflows.md)。
>* 管理工作流和工作流實例，請參 [閱管理工作流](/help/sites-administering/workflows.md)。
>* 如需端對端社群文章，請參閱「使 [用Adobe Experience Manager工作流程修改數位資產」。](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* 請參閱「 [詢問AEM專家工作流程」網路研討會](https://bit.ly/ATACE218)。
>* 如需端對端社群文章，請參閱「 [建立自訂Adobe Experience Manager 6.3動態參與者」步驟](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html)。
>* 對資訊位置的變更請參閱「AEM 6.5中的 [儲存庫重組」和「工作流程最](/help/sites-deploying/repository-restructuring.md) 佳實務——位置」 [](/help/sites-developing/workflows-best-practices.md#locations)。
>



## 模型 {#model}

A `WorkflowModel` 表示工作流的定義（模型）。 它由和 `WorkflowNodes` 構成 `WorkflowTransitions`。 這些轉變會連接節點並定義 *流*。 「模型」始終具有起始節點和終止節點。

### 執行時期模型 {#runtime-model}

工作流模型版本化。 當您執行工作流程例項時，它會使用（並保留）工作流的執行階段模型（如啟動工作流時可用）。

當在工作流模型編 [輯器中觸 **發Sync** 時，將生成運行時模型](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)。

在啟動特定例項後，對所發生的工作流程模型和/ *或所產生的* 「執行時期模型」所做的編輯將不會套用至該例項。

>[!CAUTION]
>
>執行的步驟為由執行階段模型定 [義的步驟](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model);這是在工作流模型編輯器中 **觸發Sync** 操作時生成的。
>
>如果在此時間點之後(未觸發 **Sync** )變更了工作流程模型，則執行階段例項將不會反映這些變更。 只有更新後產生的執行時期模型才會反映變更。 除了基礎ECMA指令碼之外，它們僅保留一次，因此對它們進行了更改。

### 步驟 {#step}

每個步驟都完成一個離散任務。 工作流步驟類型不同：

* 參與者（使用者／群組）:這些步驟會產生工作項目並指派給使用者或群組。 使用者必須完成工作項目，才能進階工作流程。
* 進程（指令碼、Java方法調用）:這些步驟由系統自動執行。 ECMA指令碼或Java類實現該步驟。 服務可以根據業務邏輯進行開發，以監聽特殊工作流事件並執行任務。
* 容器（子工作流程）:此類型的步驟會啟動另一個工作流模型。
* OR拆分／聯接：使用邏輯來決定在工作流程中下一步執行的步驟。
* AND拆分／連接：允許同時執行多個步驟。

所有步驟都共用下列通用屬性：和 `Autoadvance` 警 `Timeout` 報（可編寫指令碼）。

### 切換 {#transition}

A代 `WorkflowTransition` 表兩個A之間 `WorkflowNodes` 的過渡 `WorkflowModel`。

* 它定義兩個連續步驟之間的連結。
* 您可以套用規則。

### 工作項目 {#workitem}

A `WorkItem` 是通過實例的 `Workflow` 單位 `WorkflowModel`。 它包含實 `WorkflowData` 例操作的參考，以及描述底層工作流 `WorkflowNode` 步驟的參考。

* 它用於標識任務，並放入相應的收件箱。
* 工作流實例可以同時具有一 `WorkItems` 個或多個（取決於工作流模型）。
* 參考 `WorkItem` 工作流實例。
* 在儲存庫中，將 `WorkItem` 儲存在工作流實例下方。

### 裝載 {#payload}

引用必須通過工作流進行高級的資源。

裝載實施引用儲存庫中的資源（通過路徑、UUID或URL）或序列化的java對象。 在資料庫中參照資源非常有彈性，而且與sling極具生產力；例如，可將引用節點呈現為表單。

### 生命週期 {#lifecycle}

在啟動新工作流時（通過選擇相應的工作流模型並定義負載）建立，並在處理結束節點時結束。

對於工作流實例，可執行以下操作：

* 終止
* 擱置
* 繼續
* 重新啟動

已完成和終止的實例將被存檔。

### 收件匣 {#inbox}

每個用戶帳戶都有其自己的工作流收件箱，可在其中訪 `WorkItems` 問分配的。

系統 `WorkItems` 會直接指派給使用者帳戶或使用者帳戶所屬的群組。

### 工作流程類型 {#workflow-types}

「工作流模型」控制台中指出了各種工作流類型：

![wf-upgraded-03](assets/wf-upgraded-03.png)

* **預設**

   這些是標準AEM例項中隨附的現成可用工作流程。

* 自訂工作流程（控制台中沒有指示器）

   這些工作流程已建立為新的工作流程，或是從現成可用的工作流程建立，這些工作流程已覆蓋自訂項目。

* **舊版**

   在舊版AEM中建立的工作流程。 這些功能可在升級期間保留，或從舊版匯出為工作流程套件，然後匯入新版本。

### 瞬態工作流程 {#transient-workflows}

標準工作流程會在執行期間儲存執行階段（歷史）資訊。 您也可以將工作流程模型定義為「暫 **時」** ，以避免此類歷史記錄持續存在。 這用於效能調整，因為它可節省／避免用於保存資訊的時間／資源。

過渡性工作流程可用於下列任何工作流程：

* 經常運行。
* 不需要工作流程記錄。

引入了瞬態工作流程來載入大量資產，其中資產資訊很重要，但工作流程執行階段歷史記錄則不重要。

>[!NOTE]
>
>如需詳 [細資訊，請參閱建立暫時工作流程](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) 。

>[!CAUTION]
>
>當工作流程模型已標示為「暫時」時，仍會保留執行階段資訊的一些情況：
>
>* 裝載類型（例如視訊）需要外部步驟來處理；在這種情況下，需要執行階段歷史記錄才能確認狀態。
>* 工作流進入 **AND Split**;在這種情況下，需要執行階段歷史記錄才能確認狀態。
>* 當過渡工作流進入參與者步驟時，它將模式（運行時）變為非過渡；當任務傳遞給需要保存歷史的人時
>



>[!CAUTION]
>
>在瞬態工作流程中，您不應使用「 **Goto步驟」**。
>
>這是因為 **Goto Step** 會建立sling job，以在點繼續工作 `goto` 流程。 這會破壞讓工作流程暫時化的目的，並在記錄檔中產生錯誤。
>
>要在瞬態工作流中做出決策，可以使用 **OR分割**。

>[!NOTE]
>
>如需 [暫時性工作流程如何影響資產效能的詳細資訊](/help/assets/performance-tuning-guidelines.md#transient-workflows) ，請參閱資產的最佳實務。

### 多重資源支援 {#multi-resource-support}

啟 **動工作流模型的多資源支援** ，意味著即使您選擇多個資源，也將啟動單個工作流實例；這些將作為包裝附加。

如果 **未為工作流模型激活多資源支援** ，並且選擇了多個資源，則將為每個資源啟動單個工作流實例。

>[!NOTE]
>
>如需詳 [細資訊，請參閱設定多資源支援的工作流程](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) 。

### 工作流程階段 {#workflow-stages}

「工作流階段」有助於在處理任務時直觀顯示工作流的進度。 它們可用來概述工作流程在處理過程中的作用，例如當工作流程執行時，使用者可檢視 **Stage** （而非個別步驟）所描述的進度。

由於各步驟名稱可以是特定的、技術性的，因此可以定義階段名稱，以提供工作流進度的概念性視圖。

例如，對於具有六個步驟和四個階段的工作流：

1. 您可以 [設定「工作流程階段」（顯示「工作流程進度」），然後將適當的階段指派給工作流程中的每個步驟](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * 可以建立多個階段名稱。
   * 然後，將單個階段名稱分配給每個步驟（可將階段名稱分配給一個或多個步驟）。
   | **步驟名稱** | **舞台（指派給步驟）** |
   |---|---|
   | 步驟 1 | 建立 |
   | 步驟 2 | 建立 |
   | 步驟 3 | 評論 |
   | 步驟 4 | 批准 |
   | 步驟 5 | 完成 |
   | 步驟 6 | 完成 |

1. 運行工作流時，用戶可以根據階段名稱（而不是步驟名稱）查看進度。 工作流進度將顯示在「收件箱」中所列工作項目的任務詳細資訊窗口的「工作流資訊 [」(](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) WORKFLOW INFO [)選](/help/sites-authoring/inbox.md)項卡中。

### 工作流程和表單 {#workflows-and-forms}

通常，工作流程會用來處理AEM中的表單提交。 這可以與標準AEM [例項中可用的核心元件](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) ，或與 [AEM Forms解決方案一起使用](/help/forms/using/aem-forms-workflow.md)。

建立新表單時，表單提交可輕鬆與工作流程模型關聯；例如，將內容儲存在儲存庫的特定位置，或通知用戶表單提交及其內容。

### 工作流程與翻譯 {#workflows-and-translation}

工作流程也是翻譯流程的一個 [組成部分](/help/sites-administering/translation.md) 。
