---
title: 開發和延伸工作流程
seo-title: Developing and Extending Workflows
description: AEM提供數種工具和資源，用於建立工作流程模型、開發工作流程步驟，以及以程式設計方式與工作流程互動
seo-description: AEM provides several tools and resources for creating workflow models, developing workflow steps, and for programmatically interacting with workflows
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: 82b9b852fa3134f140f8de0bad229282979c8a30
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 3%

---


# 開發和延伸工作流程{#developing-and-extending-workflows}

AEM提供數種工具和資源，用於建立工作流程模型、開發工作流程步驟，以及以程式設計方式與工作流程互動。

工作流程可讓您自動化在AEM環境中管理資源和發佈內容的程式。 工作流程由一系列步驟組成，每個步驟都會完成個別工作。 您可以使用邏輯和執行階段資料來決定何時可以繼續處理，並從多個可能步驟之一中選取下一步。

例如，建立和發佈網頁的業務流程包括由不同參與者進行審批和簽核任務。 這些程式可使用AEM工作流程建模，並套用至特定內容。

主要方面如下所述，而下列各頁則涵蓋更多詳情：

* [建立工作流模型](/help/sites-developing/workflows-models.md)
* [延伸工作流程功能](/help/sites-developing/workflows-customizing-extending.md)
* [以程式設計方式與工作流程互動](/help/sites-developing/workflows-program-interaction.md)
* [工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)
* [工作流程處理序參考](/help/sites-developing/workflows-process-ref.md)
* [工作流程最佳實務](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>關於後述資訊：:
>
>* 參與工作流程，請參閱 [使用工作流程](/help/sites-authoring/workflows.md).
>* 管理工作流程和工作流程例項，請參閱 [管理工作流程](/help/sites-administering/workflows.md).
>* 如需端對端社群文章，請參閱 [使用Adobe Experience Manager工作流程修改數位資產。](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* 請參閱 [向AEM專家提問工作流程網路研討會](https://bit.ly/ATACE218).
>* 如需端對端社群文章，請參閱 [建立自訂Adobe Experience Manager 6.3動態參與者步驟](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html).
>* 資訊位置的變更請參閱 [AEM 6.5中的存放庫重新調整架構](/help/sites-deploying/repository-restructuring.md) 和 [工作流程最佳實務 — 位置](/help/sites-developing/workflows-best-practices.md#locations).
>


## 模型 {#model}

A `WorkflowModel` 代表工作流程的定義（模型）。 是由 `WorkflowNodes` 和 `WorkflowTransitions`. 轉變會連結節點並定義 *流量*. 「模型」(Model)始終包含起始節點和終止節點。

### 運行時模型 {#runtime-model}

工作流程模型版本化。 當您運行工作流實例時，它將使用（並保留）工作流的運行時模型（在啟動工作流時可用）。

運行時模型是 [產生時間 **同步** 在工作流程模型編輯器中觸發](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

對發生的工作流模型和/或產生的執行階段模型進行編輯， *after* 已啟動的特定實例將不會應用於該實例。

>[!CAUTION]
>
>執行的步驟為 [運行時模型](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model);這是在 **同步** 動作會在工作流程模型編輯器中觸發。
>
>如果在此時間點後更改了工作流模型(不包括 **同步** 觸發)，則執行階段例項不會反映這些變更。 只有更新後產生的執行階段模型才會反映變更。 除了基礎ECMA指令碼之外，它們僅保留一次，因此會對這些指令碼進行更改。

### 步驟 {#step}

每個步驟都完成一個離散任務。 有不同類型的工作流步驟：

* 參與者（用戶/組）:這些步驟將生成工作項並將其分配給用戶或組。 用戶必須完成工作項以推進工作流。
* 進程（指令碼、Java方法調用）:這些步驟由系統自動執行。 ECMA指令碼或Java類實施此步驟。 可開發服務，以監聽特殊的工作流程事件，並根據業務邏輯執行任務。
* 容器（子工作流）:此類型的步驟將啟動另一個工作流模型。
* 或分割/連接：使用邏輯決定要在工作流程中執行下一個步驟。
* 和分割/連接：允許同時執行多個步驟。

所有步驟共用下列共同屬性： `Autoadvance` 和 `Timeout` 警報（可編寫指令碼）。

### 切換 {#transition}

A `WorkflowTransition` 代表兩個 `WorkflowNodes` a `WorkflowModel`.

* 它定義了兩個連續步驟之間的連結。
* 可以套用規則。

### 工作項目 {#workitem}

A `WorkItem` 是通過 `Workflow` 例項 `WorkflowModel`. 它包含 `WorkflowData` 該案件對 `WorkflowNode` 說明基礎工作流程步驟。

* 它用於識別任務，並放入相應的收件箱。
* 工作流例項可以有一或多個 `WorkItems` 同時（視工作流程模型而定）。
* 此 `WorkItem` 參考工作流程例項。
* 在存放庫中， `WorkItem` 儲存在工作流程例項下。

### 裝載 {#payload}

參考必須透過工作流程進階的資源。

裝載實作會參照存放庫中的資源（依路徑、UUID或URL），或依序列化的Java物件。 在存放庫中參考資源非常有彈性，與Sling搭配使用可產生非常高的生產力；例如，引用的節點可以呈現為表單。

### 生命週期 {#lifecycle}

會在啟動新工作流程時建立（方法是選擇個別工作流程模型並定義裝載），並在處理結束節點時結束。

可在工作流程例項上執行下列動作：

* 終止
* 暫停
* 繼續
* 重新啟動

封存已完成和終止的執行個體。

### 收件匣 {#inbox}

每個使用者帳戶都有其專屬的工作流程收件匣，指派給 `WorkItems` 即可存取。

此 `WorkItems` 會直接指派給使用者帳戶，或指派給使用者所屬的群組。

### 工作流程類型 {#workflow-types}

工作流模型控制台中指出了各種類型的工作流：

![wf-upgraded-03](assets/wf-upgraded-03.png)

* **預設**

   這些是標準AEM例項中隨附的現成可用工作流程。

* 自訂工作流程（主控台中無指標）

   這些工作流程已建立為全新工作流程，或是來自已覆蓋自訂的現成可用工作流程。

* **舊版**

   在舊版AEM中建立的工作流程。 可在升級期間保留這些檔案，或從舊版匯出為工作流程套件，然後匯入至新版本。

### 暫時性工作流程 {#transient-workflows}

標準工作流程在執行期間會儲存執行階段（歷史記錄）資訊。 您也可以將工作流模型定義為 **暫時** 以避免這種歷史持續存在。 這用於效能調整，因為它可節省/避免用於保存資訊的時間/資源。

暫時性工作流程可用於任何具備下列條件的工作流程：

* 經常執行。
* 不需要工作流程歷史記錄。

導入了暫時性工作流程以載入大量資產，其中資產資訊很重要，但工作流程執行階段歷史記錄則不重要。

>[!NOTE]
>
>請參閱 [建立暫時性工作流程](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) 以取得詳細資訊。

>[!CAUTION]
>
>當工作流程模型已標示為「暫時」時，有些情況會持續保存執行階段資訊：
>
>* 裝載類型（例如視訊）需要外部步驟來處理；在這種情況下，需要運行時歷史記錄才能確認狀態。
>* 工作流程會輸入 **和分割**;在這種情況下，需要運行時歷史記錄才能確認狀態。
>* 當臨時工作流進入參與者步驟時，它將模式（在運行時）更改為非臨時工作流；當任務傳遞給某個人時，歷史需要持續存在
>


>[!CAUTION]
>
>在暫時性工作流程中，您不應使用 **轉至步驟**.
>
>這是 **轉至步驟** 會建立sling作業，以在 `goto` 指向。 這否定了讓工作流程暫時性的目的，並在記錄檔中產生錯誤。
>
>若要在暫時性工作流程中進行決策，您可以使用 **或分割**.

>[!NOTE]
>
>請參閱 [資產最佳實務](/help/assets/performance-tuning-guidelines.md#transient-workflows) 如需暫時性工作流程如何影響資產效能的詳細資訊。

### 多重資源支援 {#multi-resource-support}

啟用 **多資源支援** 對於工作流模型，表示即使您選取多個資源，也會啟動單一工作流例項；這些會以套件形式附加。

若 **多資源支援** 不會為工作流模型啟用，且會選取多個資源，然後會為每個資源啟動個別的工作流程例項。

>[!NOTE]
>
>請參閱 [為多資源支援配置工作流](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) 以取得詳細資訊。

### 工作流程階段 {#workflow-stages}

工作流程階段有助於視覺化處理任務時的工作流程進度。 它們可用來提供工作流程經過處理的程度概覽，例如當執行工作流程時，使用者可以檢視 **階段** （而非個別步驟）。

由於各個步驟名稱可以是特定的、技術的，因此可以定義階段名稱以提供工作流進程的概念視圖。

例如，對於具有六個步驟和四個階段的工作流程：

1. 您可以 [配置工作流階段（顯示工作流進度），然後將適當的階段分配給工作流中的每個步驟](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * 可以建立多個階段名稱。
   * 然後，將單個階段名稱分配給每個步驟（階段名稱可分配給一個或多個步驟）。

   | **步驟名稱** | **階段（分配給步驟）** |
   |---|---|
   | 步驟 1 | 建立 |
   | 步驟 2 | 建立 |
   | 步驟 3 | 評論 |
   | 步驟 4 | 批准 |
   | 步驟 5 | 完成 |
   | 步驟 6 | 完成 |

1. 運行工作流時，用戶可以根據階段名稱（而非步驟名稱）查看進度。 工作流程進度會顯示在 [工作項的任務詳細資訊窗口的「工作流資訊」頁簽](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) 列於 [收件匣](/help/sites-authoring/inbox.md).

### 工作流程與Forms {#workflows-and-forms}

工作流程通常用於在AEM中處理表單提交。 這可以是 [核心元件表單元件](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) 標準AEM例項中提供，或 [AEM Forms解決方案](/help/forms/using/aem-forms-workflow.md).

建立新表單時，表單提交可輕鬆與工作流模型關聯；例如，將內容儲存在儲存庫的特定位置，或通知使用者表單提交及其內容。

### 工作流程和翻譯 {#workflows-and-translation}

工作流程也是 [翻譯](/help/sites-administering/translation.md) 程式。
