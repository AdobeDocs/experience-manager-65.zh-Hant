---
title: 管理工作流程
seo-title: 管理工作流程
description: 瞭解如何在AEM中管理工作流程。
seo-description: 瞭解如何在AEM中管理工作流程。
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
translation-type: tm+mt
source-git-commit: 5a99daa208d1d109d2736525fdca3accdcfb4dd1
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 2%

---


# 管理工作流程{#administering-workflows}

工作流程可讓您自動化Adobe Experience Manager(AEM)活動。 工作流程:

* 由一系列按特定順序執行的步驟組成。

   * 每個步驟都會執行不同的活動；例如等待使用者輸入、啟動頁面或傳送電子郵件訊息。

* 可以與儲存庫、使用者帳戶和AEM服務中的資產互動。
* 可協調涉及AEM任何方面的複雜活動。

您組織建立的業務流程可以表示為工作流。 例如，發佈網站內容的程式通常包括許可和由不同利害關係人簽署等步驟。 這些程式可以實作為AEM工作流程，並套用至內容頁面和資產。

* [開始工作流程](/help/sites-administering/workflows-starting.md)
* [管理工作流程例項](/help/sites-administering/workflows-administering.md)
* [管理工作流程存取權](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* 套用和參與工作流程：[使用工作流](/help/sites-authoring/workflows.md)。
>* 建立工作流程模型並擴充工作流程功能：[開發與擴充工作流程](/help/sites-developing/workflows.md)。
>* 改善使用大量伺服器資源的工作流程的效能：[並行工作流處理](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing)。

>



## 工作流模型和實例{#workflow-models-and-instances}

[AEM中](/help/sites-developing/workflows.md#model) 的工作流模型是業務流程的表示和實現：

* 通常，他們會在頁面或資產上行動，以達成特定結果。
* 這些頁面和／或資產稱為工作流程裝載。
* 工作流模型由執行特定任務的一系列步驟組成。
* 當工作流程進行時，裝載會從步驟傳遞至步驟。

啟動（執行）工作流模型時，將建立工作流實例。 工作流模型可以多次啟動，每次都生成不同的工作流實例。 對於每個實例，將執行工作流模型定義的步驟。

>[!CAUTION]
>
>執行的步驟是當生成實例時由工作流模型&#x200B;*定義的步驟。*&#x200B;如需詳細資訊，請參閱[開發工作流程](/help/sites-developing/workflows.md#model)。

工作流程例項會在下列生命週期中進行：

1. 工作流模型已啟動，並且建立並運行工作流實例。

   1. 當啟動模型時，會識別工作流實例的裝載。
   1. 實例實際上是模型的副本（如建立時）。
   1. AEM作者、管理員或服務可以啟動工作流程模型。

1. 執行工作流模型的第一步。
1. 步驟已完成，工作流引擎使用模型來確定要執行的下一步。
1. 工作流模型中的後續步驟將執行並完成。
1. 完成最終步驟後，將完成工作流實例並因此進行歸檔。

AEM提供許多有用的工作流程模型。 此外，您組織中的開發人員也可以根據您業務流程的特定需求，建立自訂的工作流程模型。

## 工作流步驟{#workflow-steps}

執行工作流步驟時，這些步驟與工作流實例相關聯。 工作流程例項的歷史記錄包含為例項執行之每個步驟的相關資訊。 這些資訊對於調查執行期間發生的問題非常有用。

用戶或服務執行工作流步驟，具體取決於步驟類型：

* 當用戶執行步驟時，系統會為他們分配一個放在收件箱中的工作項目。 使用者負責手動完成步驟，讓工作流程例項繼續進行。
* 當服務執行步驟時，工作流實例在完成後會自動進入下一步。

>[!NOTE]
>
>如果發生錯誤，服務／步驟實作應處理錯誤情景的行為。 工作流引擎本身將重試作業，然後記錄錯誤並停止例項。

## 工作流狀態和操作{#workflow-status-and-actions}

工作流可以具有以下狀態之一：

* **正在運行**:工作流實例正在運行。
* **完成**:工作流實例已成功結束。

* **暫停**:將工作流標籤為暫停。不過，請參閱以下有關此狀態的已知問題的警告說明。
* **中止**:工作流實例已終止。
* **過時**:工作流實例的推進需要執行後台作業，但是在系統中找不到該作業。當執行工作流程時發生錯誤時，可能會發生這種情況。

>[!NOTE]
>
>當執行「流程步驟」導致錯誤時，該步驟將出現在管理員的收件箱中，工作流狀態為&#x200B;**RUNNING**。

根據當前狀態，當需要干預工作流實例的正常進展時，您可以對運行的工作流實例執行操作：

* **暫停**:暫停會將工作流程狀態變更為「暫停」。請參閱下列注意事項：

>[!CAUTION]
>
>將工作流程狀態標示為「暫停」有已知問題。 在此狀態下，可以對收件箱中暫停的工作流項採取操作。

* **繼續**:使用相同的配置在暫停的執行點重新啟動暫停的工作流。
* **終止**:結束工作流執行並將狀態更改為 **ABORTED**。無法重新啟動中止的工作流程實例。

