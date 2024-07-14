---
title: 開發和延伸工作流程
description: AEM提供了數種工具和資源，用於建立工作流程模型、開發工作流程步驟，以及以程式設計方式與工作流程互動
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
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
>* 參與工作流程，請參閱[使用工作流程](/help/sites-authoring/workflows.md)。
>* 管理工作流程和工作流程執行個體，請參閱[管理工作流程](/help/sites-administering/workflows.md)。
>* 如需端對端社群文章，請參閱[使用Adobe Experience Manager工作流程修改數位Assets。](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html)
>* 請參閱[向AEM專家提問工作流程線上講座](https://communities.adobeconnect.com/p5s33iburd54/)。
>* 資訊位置的變更請參閱[AEM 6.5](/help/sites-deploying/repository-restructuring.md)中的存放庫重組[工作流程最佳實務 — 位置](/help/sites-developing/workflows-best-practices.md#locations)。
>

## 模型 {#model}

`WorkflowModel`代表工作流程的定義（模型）。 它由`WorkflowNodes`和`WorkflowTransitions`組成。 轉換會連線節點並定義&#x200B;*流程*。 模型一律有起始節點和結束節點。

### 執行階段模型 {#runtime-model}

工作流程模型的版本已設定。 當您執行工作流程例項時，它會使用並保留工作流程的執行階段模型（如工作流程啟動時可用）。

在工作流程模型編輯器](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)中觸發&#x200B;**Sync**&#x200B;時，產生執行階段模型[。

對發生的工作流程模型或產生的執行階段模型（或兩者皆有） *之後*&#x200B;特定執行個體啟動的編輯未套用至該執行個體。

>[!CAUTION]
>
>執行的步驟由[執行階段模型](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)定義，是在工作流程模型編輯器中觸發&#x200B;**同步**&#x200B;動作時產生的。
>
>如果在此時間點之後變更工作流程模型（未觸發&#x200B;**同步**），則執行階段執行個體不會反映這些變更。 只有更新後產生的執行階段模型才會反映變更。 例外情況是基礎ECMA指令碼，這些指令碼只會保留一次，以便進行這些變更。

### 步驟 {#step}

每個步驟都會完成離散任務。 有不同型別的工作流程步驟：

* 參與者（使用者/群組）：這些步驟會產生工作專案並將其指派給使用者或群組。 使用者必須完成工作專案才能推進工作流程。
* 處理(指令碼、Java™方法呼叫)：這些步驟會由系統自動執行。 ECMA指令碼或Java™類別會實作該步驟。 可以開發服務以監聽特殊的工作流程事件，並根據商業邏輯執行任務。
* 容器（子工作流程）：此型別的步驟會啟動另一個工作流程模型。
* OR分割/聯結：使用邏輯來決定要在工作流程中執行下一個步驟。
* AND分割/聯結：允許同時執行多個步驟。

所有步驟共用下列通用屬性： `Autoadvance`和`Timeout`警示（指令碼式）。

### 切換 {#transition}

`WorkflowTransition`代表`WorkflowModel`中兩個`WorkflowNodes`之間的轉換。

* 它會定義兩個連續步驟之間的連結。
* 您可以套用規則。

### 工作項目 {#workitem}

`WorkItem`是透過`WorkflowModel`的`Workflow`執行個體傳遞的單位。 它包含執行個體所作用的`WorkflowData`，以及描述基礎工作流程步驟的`WorkflowNode`的參考。

* 它可用來識別任務並放入各自的收件匣中。
* 工作流程執行個體可以同時有一個或多個`WorkItems` （視工作流程模型而定）。
* `WorkItem`參考工作流程執行個體。
* 在存放庫中，`WorkItem`儲存在工作流程執行個體下方。

### 總額 {#payload}

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

每個使用者帳戶都有各自的工作流程收件匣，指派的`WorkItems`可在此收件匣中存取。

`WorkItems`會直接指派給使用者帳戶或指派給使用者帳戶所屬的群組。

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

標準工作流程會在執行期間儲存執行階段（歷史記錄）資訊。 您也可以將工作流程模型定義為&#x200B;**暫時性**，以避免持續儲存此類歷史記錄。 此工作流程用於效能調整，因為它可節省用於儲存資訊的時間和資源。

暫時性工作流程可用於滿足以下條件的任何工作流程：

* 經常執行。
* 不需要工作流程歷史記錄。

在載入許多資產時引進了暫時性工作流程，其中資產資訊很重要，但工作流程執行階段歷史記錄並不重要。

>[!NOTE]
>
>如需詳細資訊，請參閱[建立暫時性工作流程](/help/sites-developing/workflows-models.md#creating-a-transient-workflow)。

>[!CAUTION]
>
>當工作流程模型標示為暫時時，在少數情況下，執行階段資訊仍必須持續存在：
>
>* 裝載型別（例如視訊）需要外部步驟來處理；在這種情況下，需要執行階段歷史記錄來確認狀態。
>* 工作流程進入&#x200B;**AND分割**。 在這種情況下，需要執行階段歷史記錄才能確認狀態。
>* 當暫時性工作流程進入參與者步驟時，會在執行階段將模式變更為非暫時性。 由於任務正在傳遞給個人，歷史記錄必須持續存在。
>

>[!CAUTION]
>
>在暫時性工作流程中，您不應該使用&#x200B;**移至步驟**。
>
>原因在於&#x200B;**跳到步驟**&#x200B;會建立Sling工作以在`goto`點繼續工作流程。 這會讓工作流程變成暫時，並在記錄檔中產生錯誤。
>
>使用&#x200B;**OR Split**&#x200B;在暫時性工作流程中進行選擇。

>[!NOTE]
>
>如需暫時性工作流程如何影響資產效能的詳細資訊，請參閱[Assets最佳實務](/help/assets/performance-tuning-guidelines.md#transient-workflows)。

### 多重資源支援 {#multi-resource-support}

為您的工作流程模型啟動&#x200B;**多重資源支援**&#x200B;表示即使您選取多個資源，也會啟動單一工作流程執行個體。 每個檔案都會以套件形式附加。

如果未為您的工作流程模型啟動&#x200B;**多重資源支援**，且已選取多個資源，則會為每個資源啟動個別的工作流程執行個體。

>[!NOTE]
>
>如需詳細資訊，請參閱[設定多重資源支援的工作流程](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)。

### 工作流程階段 {#workflow-stages}

工作流程階段有助於在處理任務時視覺化工作流程的進度。 它們可用於提供工作流程處理過程的概觀。 當工作流程執行時，使用者可以檢視&#x200B;**階段**&#x200B;描述的進度（與個別步驟相反）。

由於各個步驟名稱可以是特定的且技術性的，因此可以定義階段名稱以提供工作流程進度的概念檢視。

例如，對於具有六個步驟和四個階段的工作流程：

1. 您可以[設定工作流程階段（顯示工作流程進度），然後將適當的階段指派給工作流程中的每個步驟](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress)：

   * 可以建立多個階段名稱。
   * 然後為每個步驟指定個別的階段名稱（可為一個或多個步驟指定階段名稱）。

   | **步驟名稱** | **階段（指派給步驟）** |
   |---|---|
   | 步驟 1 | 建立 |
   | 步驟 2 | 建立 |
   | 步驟 3 | 檢閱 |
   | 步驟 4 | 核准 |
   | 步驟 5 | 完成 |
   | 步驟 6 | 完成 |

1. 執行工作流程時，使用者可以根據階段名稱（而不是步驟名稱）檢視進度。 工作流程進度顯示在[收件匣](/help/sites-authoring/inbox.md)中列出的工作流程專案](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions)的工作流程詳細資訊視窗的[工作流程資訊索引標籤中。

### 工作流程和Forms {#workflows-and-forms}

通常使用工作流程來處理AEM中的表單提交。 它可以是標準AEM執行個體中可用的[核心元件表單元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html)，或是[AEM Forms解決方案](/help/forms/using/aem-forms-workflow.md)。

建立表單時，可輕鬆將表單提交與工作流程模型建立關聯。 例如，將內容儲存在存放庫的特定位置，或通知使用者表單提交及其內容。

### 工作流程和翻譯 {#workflows-and-translation}

工作流程也是[翻譯](/help/sites-administering/translation.md)程式的一部分。
