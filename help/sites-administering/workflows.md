---
title: 管理工作流程
seo-title: Administering Workflows
description: 瞭解如何在中管理工作AEM流。
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
ht-degree: 2%

---

# 管理工作流程{#administering-workflows}

工作流使您能夠自動執行Adobe Experience Manager(AEM)活動。 工作流程:

* 由一系列按特定順序執行的步驟組成。

   * 每個步驟都執行不同的活動；如等待用戶輸入、激活頁面或發送電子郵件。

* 可以與儲存庫、用戶帳戶和服務中的資AEM產交互。
* 可協調涉及任何方面的複雜活AEM動。

您的組織已建立的業務流程可以表示為工作流。 例如，發佈網站內容的過程通常包括各利益相關方的批准和註銷等步驟。 這些過程可以作為工作AEM流實施，並應用於內容頁面和資產。

* [開始工作流程](/help/sites-administering/workflows-starting.md)
* [管理工作流程例項](/help/sites-administering/workflows-administering.md)
* [管理工作流程存取權](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>如需進一步詳細資訊，請參閱：
>
>* 應用和參與工作流： [使用工作流](/help/sites-authoring/workflows.md)。
>* 建立工作流模型和擴展工作流功能： [開發和擴展工作流](/help/sites-developing/workflows.md)。
>* 提高使用大量伺服器資源的工作流的效能： [併發工作流處理](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing)。
>


## 工作流模型和實例 {#workflow-models-and-instances}

[工作流模型](/help/sites-developing/workflows.md#model) 其中AEM包括業務流程的表示和實施：

* 通常，它們會在頁面或資產上採取行動以取得特定結果。
* 這些頁面和/或資產稱為工作流負載。
* 工作流模型由執行特定任務的一系列步驟組成。
* 隨著工作流的推進，負載會逐步傳遞。

啟動（執行）工作流模型時，將建立工作流實例。 可以多次啟動工作流模型，每次生成不同的工作流實例。 對於每個實例，執行工作流模型定義的步驟。

>[!CAUTION]
>
>執行的步驟是由工作流模型定義的步驟 *生成實例時*。 請參閱 [開發工作流](/help/sites-developing/workflows.md#model) 的上界。

工作流實例在以下生命週期中進行：

1. 啟動工作流模型並建立並運行工作流實例。

   1. 在啟動模型時標識工作流實例的負載。
   1. 實例實際上是模型的副本（與建立時一樣）。
   1. 作AEM者、管理員或服務可以啟動工作流模型。

1. 執行工作流模型的第一步。
1. 該步驟已完成，工作流引擎使用模型確定要執行的下一步。
1. 執行並完成工作流模型中的後續步驟。
1. 完成最終步驟後，將完成工作流實例，從而存檔。

提供了許多有用的工作流模AEM型。 此外，您公司中的開發人員可以建立定製的工作流模型，這些模型可以根據您業務流程的特定需求進行定制。

## 工作流步驟 {#workflow-steps}

執行工作流步驟時，這些步驟與工作流實例相關聯。 工作流實例的歷史記錄包括有關為該實例執行的每個步驟的資訊。 此資訊對於調查執行過程中出現的問題非常有用。

用戶或服務執行工作流步驟，具體取決於步驟類型：

* 當用戶執行步驟時，會為他們分配一個放在其收件箱中的工作項目。 用戶負責手動完成該步驟，以便工作流實例進行。
* 當服務執行步驟時，完成後，工作流實例將自動進入下一步。

>[!NOTE]
>
>如果發生錯誤，服務/步驟實現應處理錯誤情形的行為。 工作流引擎本身將重試該作業，然後記錄錯誤並停止該實例。

## 工作流狀態和操作 {#workflow-status-and-actions}

工作流可以具有以下狀態之一：

* **正在運行**:工作流實例正在運行。
* **已完成**:工作流實例已成功結束。

* **掛起**:將工作流標籤為已掛起。 但是，有關此狀態的已知問題，請參閱下面的「警告」說明。
* **中止**:工作流實例已終止。
* **過時**:工作流實例的進展要求執行後台作業，但在系統中找不到該作業。 當執行工作流時出錯時，可能會出現這種情況。

>[!NOTE]
>
>當執行「流程步驟」導致錯誤時，該步驟將出現在管理員的「收件箱」中，工作流狀態為 **正在運行**。

根據當前狀態，當需要干預工作流實例的正常進展時，您可以對運行的工作流實例執行操作：

* **掛起**:掛起將工作流狀態更改為「掛起」。 請參閱下面的警告：

>[!CAUTION]
>
>將工作流狀態標籤為「掛起」有已知問題。 在此狀態下，可以對收件箱中掛起的工作流項目執行操作。

* **繼續**:使用相同的配置在掛起的執行點重新啟動掛起的工作流。
* **終止**:結束工作流執行並將狀態更改為 **中止**。 無法重新啟動中止的工作流實例。
