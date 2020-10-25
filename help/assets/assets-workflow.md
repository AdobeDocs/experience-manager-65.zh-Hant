---
title: 使用工作流程處理資產
description: 資產處理，以轉換格式、建立轉譯、管理資產、驗證資產，以及執行工作流程。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d5a48be283484005013ef3ed7ad015b43f6398b
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 3%

---


# 處理數位資產 {#process-assets}

[!DNL Adobe Experience Manager Assets] 可讓您以多種方式處理您的數位資產，以便進行強穩的資產處理。 您可以使用預設或自訂的處理方法來確保端對端業務流程的完成、稽核和合規性、發現和分發，以及數位資產的基本健全性。 您可以執行資產管理任務，同時達到所需的規模和定制。

## 瞭解工作流程 {#understand-workflows}

對於資產處理，請使 [!DNL Experience Manager] 用工作流程。 工作流程可協助自動化商業邏輯或活動。 預設會提供完成特定工作的詳細步驟，而開發人員可建立其自訂步驟。 這些步驟可依邏輯順序組合，以建立工作流程。 例如，工作流程可以根據特定條件對上傳的影像套用浮水印，例如上傳到的資料夾、影像解析度等。 另一個範例是設定為浮水印和同時新增中繼資料、建立轉譯、新增智慧標籤和發佈至資料儲存區的工作流程。

## 預設工作流程可在 [!DNL Experience Manager] {#default-workflows}

依預設，所有上傳的資產都會使用 [!UICONTROL DAM更新資產工作流程] 。 工作流程會針對每個上傳的資產執行，並完成基本的資產管理工作，例如轉譯產生、中繼資料回寫、頁面擷取、媒體擷取和轉碼。

要查看預設情況下可用的各種工作流模型，請參 **[!UICONTROL 閱中的「工具」>「工作流」]** >「模型 [!DNL Experience Manager]」。

![部分預設工作流程](assets/aem-default-workflows.png)

*圖：中提供的部分預設工作流程 [!DNL Experience Manager]。*

## 將工作流程套用至處理資產 {#applying-workflows-to-assets}

將工作流程套用至數位資產與網站頁面相同。 如需如何建立和使用工作流程的完整指南，請參閱「開始工 [作流程」](/help/sites-authoring/workflows-participating.md)。

在數位資產中使用工作流程來啟用資產或建立浮水印。 資產的許多工作流程都會自動開啟。 例如，編輯影像後自動建立轉譯的工作流程會自動開啟。

>[!NOTE]
>
>如果傳統UI中的工作流程不適用於啟用觸控的UI，例如「 [!UICONTROL Request to Activate] 」（請求啟用）和「 [!UICONTROL Request to Deactivate」(請求]停用) [，請參閱](/help/sites-developing/workflows-models.md#classic2touchui)建立工作流程模型。

## 將工作流程套用至資產 {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
若要將工作流程套用至資產，請依照下列步驟進行：

1. 導覽至您要啟動工作流程的資產所在位置，然後按一下資產以開啟資產頁面。 從菜 **[!UICONTROL 單中選擇]** 「時間軸」(Timeline)以顯示時間軸。

   ![timeline-1](assets/timeline.png)

1. 按一 **[!UICONTROL 下底部的]** 「動作」，開啟資產可用動作清單。

1. 從清 **[!UICONTROL 單中按一下「開始工作流程]** 」。

1. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

1. （可選）指定可用於參考工作流實例的工作流標題。

   ![選取工作流程，提供標題並按一下「開始」](assets/start-workflow.png)

1. 按一 **[!UICONTROL 下「開始]** 」，然後按一 **[!UICONTROL 下「繼續]**」。 工作流程的每個步驟都會以事件的形式顯示在時間軸中。

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 將工作流程套用至多個資產 {#applying-a-workflow-to-multiple-assets}

1. 從控 [!DNL Assets] 制台導覽至您要啟動工作流程的資產所在位置，然後選取資產。 從菜 **[!UICONTROL 單中選擇]** 「時間軸」(Timeline)以顯示時間軸。

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 按一 **[!UICONTROL 下底]** 部的 ![](assets/do-not-localize/chevron-up-icon.png) 「動作(Actions)」。
1. 按一下「 **[!UICONTROL 開始工作流程]**」。 In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![啟動工作流程](assets/start-workflow.png)

1. （可選）指定工作流的標題，可用來參考工作流實例。
1. 按一 **[!UICONTROL 下「開始]** 」，然後按一 **[!UICONTROL 下對話方塊中的「確認]** 」。工作流程會在您選取的所有資產上執行。

## 將工作流程套用至多個檔案夾 {#applying-a-workflow-to-multiple-folders}

將工作流程套用至多個檔案夾的程式，類似於將工作流程套用至多個資產的程式。 在介面中選取資 [!DNL Assets] 料夾，並執行將工作流程套用至多 [個資產的程式步驟2-7](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets)。

## 將工作流程套用至系列 {#applying-a-workflow-to-a-collection}

請參 [閱套用系列的工作流程](/help/assets/manage-collections.md#running-a-workflow-on-a-collection)。

## 自動啟動工作流程，有條件地處理資產 {#auto-execute-workflow-on-some-assets}

管理員可以設定工作流程，根據預先定義的條件自動執行和處理資產。 此功能對於業務線使用者和行銷人員非常有用，例如，在特定資料夾上建立自訂工作流程。 說明機構像片拍攝的所有資產都可以浮水印，或是自由工作者上傳的所有資產都可以處理，以建立特定的轉譯。

對於工作流模型，用戶可以建立執行該模型的工作流啟動程式。 工作流啟動器監視內容儲存庫中的更改並在滿足預定義條件時執行工作流。 管理員可讓行銷人員存取建立工作流程和設定啟動程式。 使用者可修改預設的 [!UICONTROL DAM更新資產工作流程] ，以新增處理特定資產所需的額外步驟。 工作流程會對所有新上傳的資產執行。 使用下列方法之一來限制特定資產上額外步驟的執行：

* 製作 [!UICONTROL DAM更新資產工作流程的副本] ，並加以修改以在特定資料夾階層上執行。 此方法對於一些資料夾非常有用。
* 可以使用 [OR拆分來添加額外的處理步驟](/help/sites-developing/workflows-step-ref.md#or-split) ，該OR拆分條件性地適用於所需數量的資料夾。

## 最佳做法和限制 {#best-practices-limitations-tips}

* 在設計工作流程時，請考慮您對所有類型轉譯的需求。 如果您未預見未來需要轉譯，請從工作流程中移除其建立步驟。 之後無法大量刪除轉譯。 長期使用後，不需要的轉譯可能會佔用大量儲存空間 [!DNL Experience Manager]。 對於個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自訂以 [!DNL Experience Manager] 刪除特定轉譯，或刪除資產並再次上傳這些資產。
* 依預設，  DAM更新資產工作流程包含一些建立縮圖和網頁轉譯的步驟。 如果從工作流程移除任何預設轉譯，則其使用者介面 [!DNL Assets] 無法正確呈現。

>[!MORELIKETHIS]
>
>* [套用並參與工作流程](/help/sites-authoring/workflows.md)
>* [建立工作流程模型並擴充工作流程功能](/help/sites-developing/workflows.md)
>* [執行工作流程的方法](/help/sites-administering/workflows-starting.md)
>* [工作流程最佳實務](/help/sites-developing/workflows-best-practices.md)
>* [使用工作流程修改資產的社群文章](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)

