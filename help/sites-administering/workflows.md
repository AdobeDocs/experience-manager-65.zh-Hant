---
title: 管理工作流程
seo-title: Administering Workflows
description: 了解如何在AEM中管理工作流程。
seo-description: Learn how to administer workflows in AEM.
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
exl-id: 10eecfb8-d43d-4f01-9778-87c752dee64c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 1%

---

# 管理工作流程{#administering-workflows}

工作流程可讓您自動執行Adobe Experience Manager(AEM)活動。 工作流程:

* 由一系列以特定順序執行的步驟組成。

   * 每個步驟都會執行不同的活動；例如等候使用者輸入、啟動頁面或傳送電子郵件訊息。

* 可與存放庫、使用者帳戶和AEM服務中的資產互動。
* 可協調涉及AEM任何方面的複雜活動。

貴組織已建立的業務流程可以表示為工作流。 例如，發佈網站內容的程式通常包括多個步驟，例如核准和由各利害關係人簽核。 這些程式可以實作為AEM工作流程，並套用至內容頁面和資產。

* [開始工作流程](/help/sites-administering/workflows-starting.md)
* [管理工作流程例項](/help/sites-administering/workflows-administering.md)
* [管理工作流程存取權](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* 套用和參與工作流程： [使用工作流程](/help/sites-authoring/workflows.md).
>* 建立工作流模型並擴展工作流功能： [開發和擴充工作流程](/help/sites-developing/workflows.md).
>* 改善使用大量伺服器資源的工作流程的效能： [同時處理工作流程](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).
>


## 工作流程模型和例項 {#workflow-models-and-instances}

[工作流程模型](/help/sites-developing/workflows.md#model) 在AEM中，表示和實施業務流程：

* 通常它們會在頁面或資產上運作，以取得特定結果。
* 這些頁面和/或資產稱為工作流程裝載。
* 工作流模型由執行特定任務的一系列步驟組成。
* 隨著工作流程進行，裝載會逐步傳遞。

啟動（執行）工作流模型時，會建立工作流實例。 工作流模型可以多次啟動，每次都會產生不同的工作流例項。 對於每個實例，執行工作流模型定義的步驟。

>[!CAUTION]
>
>執行的步驟是由工作流模型定義的步驟 *在產生例項時*. 請參閱 [開發工作流程](/help/sites-developing/workflows.md#model) 以取得詳細資訊。

工作流程例項會在下列生命週期中進行：

1. 工作流模型已啟動，並且已建立並運行工作流實例。

   1. 啟動模型時，會識別工作流程例項的裝載。
   1. 例項實際上是模型的復本（如同建立時）。
   1. AEM作者、管理員或服務可以啟動工作流程模型。

1. 執行工作流程模型的第一個步驟。
1. 此步驟已完成，而工作流程引擎會使用模型來決定要執行的下一個步驟。
1. 工作流程模型中的後續步驟會執行並完成。
1. 完成最後一個步驟時，工作流程例項即會完成並封存。

許多實用的工作流程模型都隨AEM提供。 此外，您組織的開發人員可以根據您業務流程的特定需求，建立自訂的工作流模型。

## 工作流程步驟 {#workflow-steps}

執行工作流程步驟時，這些步驟會與工作流程例項相關聯。 工作流程例項的歷史記錄包含針對該例項執行之每個步驟的相關資訊。 此資訊對於調查執行期間發生的問題非常有用。

使用者或服務會根據步驟類型執行工作流程步驟：

* 當用戶執行步驟時，系統會為他們分配一個放在其收件箱中的工作項。 使用者負責手動完成步驟，以便工作流程例項繼續進行。
* 當服務執行步驟時，工作流程例項會在完成時自動進入下一個步驟。

>[!NOTE]
>
>如果發生錯誤，服務/步驟實作應處理錯誤情境的行為。 工作流程引擎本身將重試該作業，然後記錄錯誤並停止執行個體。

## 工作流程狀態和動作 {#workflow-status-and-actions}

工作流程可具有下列其中一個狀態：

* **執行中**:工作流實例正在運行。
* **已完成**:已成功結束工作流實例。

* **已暫停**:將工作流程標示為暫停。 不過，請參閱下方的警告說明，了解此狀態的已知問題。
* **已中止**:工作流實例已終止。
* **過時**:工作流實例的推進要求執行後台作業，但在系統中找不到該作業。 執行工作流程時發生錯誤時，可能會發生此情況。

>[!NOTE]
>
>當執行「進程步驟」導致錯誤時，該步驟會出現在管理員的「收件箱」中，工作流狀態為 **執行中**.

根據當前狀態，當您需要干預工作流實例的正常進展時，可以對運行的工作流實例執行操作：

* **暫停**:暫停會將工作流程狀態變更為暫停。 請參閱下列警告：

>[!CAUTION]
>
>將工作流程狀態標示為「暫停」有已知問題。 在此狀態下，可以對收件箱中掛起的工作流項執行操作。

* **繼續**:使用相同的配置在暫停的執行點重新啟動暫停的工作流。
* **終止**:結束工作流程執行並將狀態變更為 **已中止**. 無法重新啟動中止的工作流實例。
