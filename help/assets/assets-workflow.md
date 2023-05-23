---
title: 使用工作流處理資產
description: 資產處理：轉換格式、建立格式副本、管理資產、驗證資產和運行工作流。
contentOwner: AG
feature: Workflow, Renditions
role: User, Admin
exl-id: e7c84385-efb3-4997-83ff-7a7f31582469
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 3%

---

# 處理數字資產 {#process-assets}

[!DNL Adobe Experience Manager Assets] 允許您以多種方式處理數字資產，以便進行穩健的資產處理。 您可以使用預設或自定義的處理方法來確保端到端業務流程的完成、審核和法規遵從性、發現和分發，以及數字資產的基本健全性。 您可以在完成所需規模和自定義的同時執行資產管理任務。

## 瞭解工作流 {#understand-workflows}

對於資產處理， [!DNL Experience Manager] 使用工作流。 工作流有助於自動化業務邏輯或活動。 預設情況下提供完成特定任務的細粒度步驟，開發人員可以建立自己的自定義步驟。 這些步驟可以按邏輯順序組合，以建立工作流。 例如，工作流可以根據特定條件對上載的影像應用水印，如將其上載到的資料夾、影像的解析度等。 另一個示例是配置為加水印並同時添加元資料、建立格式副本、添加智慧標籤和發佈到資料儲存的工作流。

## 預設工作流可用於 [!DNL Experience Manager] {#default-workflows}

預設情況下，所有上載的資產都使用 [!UICONTROL DAM更新資產] 工作流。 該工作流為每個上載的資產執行，並完成基本的資產管理任務，如格式副本生成、元資料寫回、頁面提取、媒體提取和轉碼。

要查看預設情況下可用的各種工作流模型，請參閱 **[!UICONTROL 工具>工作流>模型]** 在 [!DNL Experience Manager]。

![某些預設工作流](assets/aem-default-workflows.png)

*圖：中提供的某些預設工作流 [!DNL Experience Manager]。*

## 將工作流應用於處理資產 {#applying-workflows-to-assets}

將工作流應用到數字資產與網站頁面相同。 有關如何建立和使用工作流的完整指南，請參見 [啟動工作流](/help/sites-authoring/workflows-participating.md)。

使用數字資產中的工作流激活資產或建立水印。 資產的許多工作流都會自動開啟。 例如，在編輯影像後自動建立格式副本的工作流會自動開啟。

>[!NOTE]
>
>如果「標準」UI中可用的工作流在啟用觸摸的UI中不可用，例如 [!UICONTROL 請求激活] 和 [!UICONTROL 請求停用]，請參閱 [建立工作流模型](/help/sites-developing/workflows-models.md#classic2touchui)。

## 將工作流應用於資產 {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
要將工作流應用於資產，請執行以下步驟：

1. 定位至要為其啟動工作流的資產的位置，然後按一下資產以開啟資產頁。 選擇 **[!UICONTROL 時間軸]** 的子菜單。

   ![時間軸1](assets/timeline.png)

1. 按一下 **[!UICONTROL 操作]** 按鈕，開啟可用於資產的操作清單。

1. 按一下 **[!UICONTROL 啟動工作流]** 清單中。

1. 在 **[!UICONTROL 啟動工作流]** 對話框，從清單中選擇工作流模型。

1. （可選）為可用於引用工作流實例的工作流指定標題。

   ![選擇工作流，提供標題並按一下「開始」](assets/start-workflow.png)

1. 按一下 **[!UICONTROL 開始]** 然後按一下 **[!UICONTROL 繼續]**。 工作流程的每個步驟都會以事件的形式顯示在時間軸中。

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 將工作流應用於多個資產 {#applying-a-workflow-to-multiple-assets}

1. 從 [!DNL Assets] 控制台，導航到要為其啟動工作流的資產的位置，然後選擇資產。 選擇 **[!UICONTROL 時間軸]** 的子菜單。

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 按一下 **[!UICONTROL 操作]** ![雪花](assets/do-not-localize/chevron-up-icon.png) 在底部。
1. 按一下 **[!UICONTROL 啟動工作流]**。 在 **[!UICONTROL 啟動工作流]** 對話框，從清單中選擇工作流模型。

   ![啟動工作流](assets/start-workflow.png)

1. （可選）指定工作流的標題，該標題可用於引用工作流實例。
1. 按一 **[!UICONTROL 下「開始]** 」，然後按一 **[!UICONTROL 下對話方塊中的「確認]** 」。工作流程會在您選取的所有資產上執行。

## 將工作流應用於多個資料夾 {#applying-a-workflow-to-multiple-folders}

將工作流應用於多個資料夾的過程與將工作流應用於多個資產的過程類似。 選擇 [!DNL Assets] 介面，並執行步驟2-7 [將工作流應用於多個資產](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets)。

## 將工作流應用於集合 {#applying-a-workflow-to-a-collection}

請參閱 [對集合應用工作流](/help/assets/manage-collections.md#running-a-workflow-on-a-collection)。

## 自動啟動工作流以有條件地處理資產 {#auto-execute-workflow-on-some-assets}

管理員可以配置工作流以根據預定義的條件自動執行和處理資產。 此功能對於業務線用戶和營銷人員非常有用，例如，在特定資料夾上建立自定義工作流。 假設某機構照片中的所有資產都可以加水印，或者自由撰稿人上傳的所有資產都可以被處理，以建立特定的格式副本。

對於工作流模型，用戶可以建立執行該模型的工作流啟動程式。 工作流啟動器監視內容儲存庫中的變化，並在滿足預定條件時執行該工作流。 管理員可以向營銷人員提供建立工作流和配置啟動程式的訪問權限。 用戶可以修改預設 [!UICONTROL DAM更新資產] 工作流，以添加處理特定資產所需的額外步驟。 工作流對所有新上載的資產執行。 使用以下方法之一限制對特定資產執行額外步驟：

* 複製 [!UICONTROL DAM更新資產] 並修改它以在特定資料夾層次結構上執行。 此方法對於一些資料夾非常有用。
* 可以使用 [或拆分](/help/sites-developing/workflows-step-ref.md#or-split) 根據需要可以對任意多個資料夾使用。

## 最佳做法和限制 {#best-practices-limitations-tips}

* 在設計工作流時考慮您對所有類型的格式副本的需求。 如果您預計將來不需要格式副本，請從工作流中刪除其建立步驟。 之後無法批量刪除格式副本。 長期使用後，不希望的格式副本可能佔用大量儲存空間 [!DNL Experience Manager]。 對於單個資產，您可以從用戶介面手動刪除格式副本。 對於多個資產，您可以自定義 [!DNL Experience Manager] 刪除特定格式副本或刪除資產並重新上載這些資產。
* 預設情況下， [!UICONTROL DAM更新資產] 工作流包括建立縮略圖和Web格式副本的一些步驟。 如果從工作流中刪除任何預設格式副本，則 [!DNL Assets] 無法正確呈現。

>[!MORELIKETHIS]
>
>* [應用和參與工作流](/help/sites-authoring/workflows.md)
>* [建立工作流模型並擴展工作流功能](/help/sites-developing/workflows.md)
>* [執行工作流的方法](/help/sites-administering/workflows-starting.md)
>* [工作流最佳實踐](/help/sites-developing/workflows-best-practices.md)

