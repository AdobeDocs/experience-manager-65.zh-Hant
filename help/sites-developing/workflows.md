---
title: 開發和延伸工作流程
description: AEM提供了數種工具和資源，用於建立工作流程模型、開發工作流程步驟，以及以程式設計方式與工作流程互動
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '1460'
ht-degree: 3%

---


# 開發和延伸工作流程{#developing-and-extending-workflows}

AEM提供了數種工具和資源，用於建立工作流程模型、開發工作流程步驟，以及以程式設計方式與工作流程互動。

工作流程可讓您自動化在AEM環境中管理資源和發佈內容的流程。 工作流程由一系列步驟組成，每個步驟都完成一個離散的任務。 您可以使用邏輯和執行階段資料來決定程式何時可以繼續，並從多個可能的步驟之一中選取下一個步驟。

例如，建立和發佈網頁的業務流程包括不同參與者的核准和簽核工作。 這些流程可使用AEM工作流程進行模型化，並套用至特定內容。

主要內容涵蓋於下方，而下列頁面則涵蓋更多詳細資訊：

* [建立工作流模型](/help/sites-developing/workflows-models.md)
* [延伸工作流程功能](/help/sites-developing/workflows-customizing-extending.md)
* [以程式設計方式與工作流程互動](/help/sites-developing/workflows-program-interaction.md)
* [工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)
* [工作流程處理序參考](/help/sites-developing/workflows-process-ref.md)
* [工作流程最佳實務](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>如需下列相關資訊：
>
>* 參與工作流程，請參閱 [使用工作流程](/help/sites-authoring/workflows.md).
>* 管理工作流程與工作流程例項，請參閱 [管理工作流程](/help/sites-administering/workflows.md).
>* 如需端對端社群文章，請參閱 [使用Adobe Experience Manager工作流程修改數位資產。](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html)
>* 請參閱 [向AEM專家詢問工作流程網路研討會](https://communities.adobeconnect.com/p5s33iburd54/).
>* 資訊位置的變更請參閱 [AEM 6.5中的存放庫重組](/help/sites-deploying/repository-restructuring.md) 和 [工作流程最佳實務 — 位置](/help/sites-developing/workflows-best-practices.md#locations).
>

## 模型 {#model}

A `WorkflowModel` 代表工作流程的定義（模型）。 它由下列專案組成 `WorkflowNodes` 和 `WorkflowTransitions`. 轉接會連線節點並定義 *流量*. 模型一律有起始節點和結束節點。

### 執行階段模型 {#runtime-model}

工作流程模型的版本已設定。 當您執行工作流程例項時，它會使用並保留工作流程的執行階段模型（如工作流程啟動時可用）。

執行階段模型為 [產生時間 **同步** 在工作流程模型編輯器中觸發](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

編輯發生的工作流程模型、產生的執行階段模型或兩者， *晚於* 已啟動的特定執行個體未套用至該執行個體。

>[!CAUTION]
>
>執行的步驟由定義 [執行階段模型](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)，產生於 **同步** 動作會在工作流程模型編輯器中觸發。
>
>如果在此時間點之後變更工作流程模型(不含 **同步** )，則執行階段執行個體不會反映這些變更。 只有更新後產生的執行階段模型才會反映變更。 例外情況是基礎ECMA指令碼，這些指令碼只會保留一次，以便進行這些變更。

### 步驟 {#step}

每個步驟都會完成離散任務。 有不同型別的工作流程步驟：

* 參與者（使用者/群組）：這些步驟會產生工作專案並將其指派給使用者或群組。 使用者必須完成工作專案才能推進工作流程。
* 處理(指令碼、Java™方法呼叫)：這些步驟會由系統自動執行。 ECMA指令碼或Java™類別會實作該步驟。 可以開發服務以監聽特殊的工作流程事件，並根據商業邏輯執行任務。
* 容器（子工作流程）：此型別的步驟會啟動另一個工作流程模型。
* OR分割/聯結：使用邏輯來決定要在工作流程中執行下一個步驟。
* AND分割/聯結：允許同時執行多個步驟。

所有步驟共用以下通用屬性： `Autoadvance` 和 `Timeout` 警示（指令碼式）。

### 切換 {#transition}

A `WorkflowTransition` 代表兩個之間的轉變 `WorkflowNodes` 的 `WorkflowModel`.

* 它會定義兩個連續步驟之間的連結。
* 您可以套用規則。

### 工作項目 {#workitem}

A `WorkItem` 是通過 `Workflow` 例項 `WorkflowModel`. 它包含 `WorkflowData` 執行個體所作用的資訊，以及對 `WorkflowNode` 說明基礎工作流程步驟。

* 它可用來識別任務並放入各自的收件匣中。
* 工作流程例項可以有一或多個 `WorkItems` 同時（視工作流程模型而定）。
* 此 `WorkItem` 參考工作流程例項。
* 在存放庫中， `WorkItem` 會儲存在工作流程例項下方。

### 裝載 {#payload}

參考必須透過工作流程進行進階的資源。

裝載實施會參考存放庫中的資源（依路徑、UUID或URL）或依序列化Java™物件。 參考存放庫中的資源既靈活又富生產力。 例如，參照的節點可以呈現為表單。

### 生命週期 {#lifecycle}

在啟動新工作流程時建立（選擇個別工作流程模型並定義裝載），並在處理結束節點時結束。

可在工作流程例項上執行下列動作：

* 終止
* 暫停
* 繼續
* 重新啟動

已完成的和已終止的執行個體都會被封存。

### 收件匣 {#inbox}

每個使用者帳戶都有各自的工作流程收件匣，指派的工作流程收件匣位於這些收件匣中 `WorkItems` 可存取。

此 `WorkItems` 會直接指派給使用者帳戶，或指派給使用者所屬的群組。

### 工作流程型別 {#workflow-types}

「工作流程模型」主控台中顯示了各種型別的工作流程：

![wf-upgraded-03](assets/wf-upgraded-03.png)

* **預設**

  這些是標準AEM例項中包含的現成工作流程。

* 自訂工作流程（主控台中沒有指標）

  這些工作流程是全新建立的，或是從已覆蓋自訂功能的現成工作流程建立的。

* **舊版**

  在舊版AEM中建立的工作流程。 這些工作流程可以在升級期間保留，或匯出為先前版本的工作流程套件，然後匯入新版本。

### 暫時性工作流程 {#transient-workflows}

標準工作流程會在執行期間儲存執行階段（歷史記錄）資訊。 您也可以將工作流程模型定義為 **暫時性** 以避免此類歷史記錄持續存在。 此工作流程用於效能調整，因為它可節省用於儲存資訊的時間和資源。

暫時性工作流程可用於滿足以下條件的任何工作流程：

* 經常執行。
* 不需要工作流程歷史記錄。

在載入許多資產時引進了暫時性工作流程，其中資產資訊很重要，但工作流程執行階段歷史記錄並不重要。

>[!NOTE]
>
>另請參閱 [建立暫時性工作流程](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) 以取得更多詳細資料。

>[!CAUTION]
>
>當工作流程模型標示為暫時時，在少數情況下，執行階段資訊仍必須持續存在：
>
>* 裝載型別（例如視訊）需要外部步驟來處理；在這種情況下，需要執行階段歷史記錄來確認狀態。
>* 工作流程進入 **AND拆分**. 在這種情況下，需要執行階段歷史記錄才能確認狀態。
>* 當暫時性工作流程進入參與者步驟時，會在執行階段將模式變更為非暫時性。 由於任務正在傳遞給個人，歷史記錄必須持續存在。
>

>[!CAUTION]
>
>在暫時性工作流程中，請勿使用 **移至步驟**.
>
>原因在於 **移至步驟** 建立sling工作以在上繼續工作流程 `goto` 點。 這會讓工作流程變成暫時，並在記錄檔中產生錯誤。
>
>使用 **OR拆分** 在暫時性工作流程中進行選擇。

>[!NOTE]
>
>另請參閱 [Assets最佳實務](/help/assets/performance-tuning-guidelines.md#transient-workflows) 以進一步瞭解暫時性工作流程如何影響資產效能。

### 多重資源支援 {#multi-resource-support}

啟用 **多重資源支援** 對於您的工作流程模型，表示即使您選取多個資源，也會啟動單一工作流程例項。 每個檔案都會以套件形式附加。

如果 **多重資源支援** 不會為您的工作流程模型啟動，且已選取多個資源，然後會為每個資源啟動個別工作流程例項。

>[!NOTE]
>
>另請參閱 [設定多資源支援的工作流程](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) 以取得更多詳細資料。

### 工作流程階段 {#workflow-stages}

工作流程階段有助於在處理任務時視覺化工作流程的進度。 它們可用於提供工作流程處理過程的概觀。 工作流程執行時，使用者可以檢視以下說明的進度 **階段** （與個別步驟相反）。

由於各個步驟名稱可以是特定的且技術性的，因此可以定義階段名稱以提供工作流程進度的概念檢視。

例如，對於具有六個步驟和四個階段的工作流程：

1. 您可以 [設定工作流程階段（顯示工作流程進度），然後將適當的階段指派給工作流程中的每個步驟](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress)：

   * 可以建立多個階段名稱。
   * 然後為每個步驟指定個別的階段名稱（可為一個或多個步驟指定階段名稱）。

   | **步驟名稱** | **階段（指派給步驟）** |
   |---|---|
   | 步驟 1 | 建立 |
   | 步驟 2 | 建立 |
   | 步驟 3 | 評論 |
   | 步驟 4 | 批准 |
   | 步驟 5 | 完成 |
   | 步驟 6 | 完成 |

1. 執行工作流程時，使用者可以根據階段名稱（而不是步驟名稱）檢視進度。 工作流程進度會顯示在 [工作流程專案之任務詳細資訊視窗的工作流程資訊標籤](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) 列於 [收件匣](/help/sites-authoring/inbox.md).

### 工作流程和Forms {#workflows-and-forms}

通常使用工作流程來處理AEM中的表單提交。 它可以與 [核心元件表單元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html) 可在標準AEM例項中使用，或透過 [AEM Forms解決方案](/help/forms/using/aem-forms-workflow.md).

建立表單時，可輕鬆將表單提交與工作流程模型建立關聯。 例如，將內容儲存在存放庫的特定位置，或通知使用者表單提交及其內容。

### 工作流程和翻譯 {#workflows-and-translation}

工作流程也是 [翻譯](/help/sites-administering/translation.md) 程式。
