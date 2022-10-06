---
title: 使用工作流程處理資產
description: 資產處理功能，可轉換格式、建立轉譯、管理資產、驗證資產及執行工作流程。
contentOwner: AG
feature: Workflow, Renditions
role: User, Admin
exl-id: e7c84385-efb3-4997-83ff-7a7f31582469
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 3%

---

# 處理數位資產 {#process-assets}

[!DNL Adobe Experience Manager Assets] 可讓您以多種方式處理數位資產，以執行強大的資產處理功能。 您可以使用預設或定製的處理方法來確保端到端業務流程的完成、審核和合規性、發現和分發，以及數字資產的基本健全性。 您可以執行資產管理任務，同時實現所需的規模和定制。

## 了解工作流程 {#understand-workflows}

針對資產處理， [!DNL Experience Manager] 使用工作流程。 工作流程可協助自動化業務邏輯或活動。 預設會提供完成特定工作的詳細步驟，而開發人員可建立自己的自訂步驟。 這些步驟可依邏輯順序結合，以建立工作流程。 例如，工作流程可以根據特定條件對上傳的影像套用浮水印，例如上傳至的資料夾、影像解析度等。 另一個範例是設定為浮水印和同時新增中繼資料、建立轉譯、新增智慧標籤，以及發佈至資料存放區的工作流程。

## 預設工作流程(於 [!DNL Experience Manager] {#default-workflows}

依預設，所有上傳的資產都會使用 [!UICONTROL DAM更新資產] 工作流程。 工作流程會對每個上傳的資產執行，並完成基本資產管理工作，例如產生轉譯、中繼資料回寫、頁面擷取、媒體擷取和轉碼。

若要查看預設可用的各種工作流程模型，請參閱 **[!UICONTROL 「工具」>「工作流」>「模型」]** in [!DNL Experience Manager].

![部分預設工作流程](assets/aem-default-workflows.png)

*圖：中提供的部分預設工作流程 [!DNL Experience Manager].*

## 套用工作流程以處理資產 {#applying-workflows-to-assets}

將工作流程套用至數位資產與網站頁面的相同。 如需如何建立和使用工作流程的完整指南，請參閱 [開始工作流程](/help/sites-authoring/workflows-participating.md).

使用數位資產中的工作流程來啟用資產或建立浮水印。 資產的許多工作流程都會自動開啟。 例如，編輯影像後自動建立轉譯的工作流程會自動開啟。

>[!NOTE]
>
>如果傳統UI中可用的工作流程在觸控式UI中不可用，例如 [!UICONTROL 請求啟用] 和 [!UICONTROL 停用請求]，請參閱 [建立工作流程模型](/help/sites-developing/workflows-models.md#classic2touchui).

## 將工作流程套用至資產 {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
若要將工作流程套用至資產，請執行下列步驟：

1. 導覽至您要啟動工作流程的資產位置，然後按一下資產以開啟資產頁面。 選擇 **[!UICONTROL 時間表]** 顯示時間軸。

   ![時間軸–1](assets/timeline.png)

1. 按一下 **[!UICONTROL 動作]** ，開啟資產可用動作清單。

1. 按一下 **[!UICONTROL 開始工作流程]** 從清單中。

1. 在 **[!UICONTROL 開始工作流程]** 對話框，從清單中選取工作流模型。

1. （選用）指定可用來參考工作流程例項的工作流程標題。

   ![選取工作流程，提供標題並按一下「開始」](assets/start-workflow.png)

1. 按一下 **[!UICONTROL 開始]** 然後按一下 **[!UICONTROL 繼續]**. 工作流程的每個步驟都會以事件的形式顯示在時間軸中。

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 將工作流程套用至多個資產 {#applying-a-workflow-to-multiple-assets}

1. 從 [!DNL Assets] 主控台，導覽至您要啟動工作流程的資產位置，然後選取資產。 選擇 **[!UICONTROL 時間表]** 顯示時間軸。

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 按一下 **[!UICONTROL 動作]** ![雪佛龍](assets/do-not-localize/chevron-up-icon.png) 在底部。
1. 按一下 **[!UICONTROL 開始工作流程]**. 在 **[!UICONTROL 開始工作流程]** 對話框，從清單中選取工作流模型。

   ![開始工作流程](assets/start-workflow.png)

1. （可選）指定工作流的標題，可用於參考工作流實例。
1. 按一 **[!UICONTROL 下「開始]** 」，然後按一 **[!UICONTROL 下對話方塊中的「確認]** 」。工作流程會在您選取的所有資產上執行。

## 將工作流程套用至多個資料夾 {#applying-a-workflow-to-multiple-folders}

將工作流程套用至多個資料夾的程式，與將工作流程套用至多個資產的程式類似。 在 [!DNL Assets] 介面，並執行過程的步驟2-7 [將工作流程套用至多個資產](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## 將工作流程套用至集合 {#applying-a-workflow-to-a-collection}

請參閱 [對集合套用工作流程](/help/assets/manage-collections.md#running-a-workflow-on-a-collection).

## 自動啟動工作流程以有條件地處理資產 {#auto-execute-workflow-on-some-assets}

管理員可以設定工作流程，以根據預先定義的條件自動執行和處理資產。 此功能對於業務線使用者和行銷人員非常實用，例如在特定資料夾上建立自訂工作流程。 假設某個機構拍攝的所有資產都可以加上水印，或者自由職業者上傳的所有資產都可以經過處理，以建立特定的轉譯。

對於工作流模型，用戶可以建立執行該模型的工作流啟動器。 工作流程啟動器會監控內容存放庫中的變更，並在符合預先定義的條件時執行工作流程。 管理員可以向行銷人員提供建立工作流程和設定啟動器的存取權。 使用者可修改預設值 [!UICONTROL DAM更新資產] 工作流程，新增處理特定資產所需的額外步驟。 工作流程會對所有新上傳的資產執行。 使用下列其中一種方法來限制特定資產上額外步驟的執行：

* 製作 [!UICONTROL DAM更新資產] 工作流程並加以修改，以在特定資料夾階層上執行。 此方法對一些資料夾非常有用。
* 您可以使用 [或分割](/help/sites-developing/workflows-step-ref.md#or-split) 根據需要適用於任意數量的資料夾。

## 最佳實務和限制 {#best-practices-limitations-tips}

* 設計工作流程時，請考量您對所有轉譯類型的需求。 如果您預計未來不需要轉譯，請從工作流程移除其建立步驟。 之後無法大量刪除轉譯。 長時間使用後，您可能會佔用大量儲存空間 [!DNL Experience Manager]. 對於個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自訂 [!DNL Experience Manager] 刪除特定轉譯或刪除資產，然後再次上傳這些資產。
* 依預設， [!UICONTROL DAM更新資產] 工作流程包含建立縮圖和網頁轉譯的部分步驟。 如果從工作流程移除任何預設轉譯，請使用 [!DNL Assets] 無法正確呈現。

>[!MORELIKETHIS]
>
>* [套用並參與工作流程](/help/sites-authoring/workflows.md)
>* [建立工作流模型並擴展工作流功能](/help/sites-developing/workflows.md)
>* [執行工作流程的方法](/help/sites-administering/workflows-starting.md)
>* [工作流程最佳實務](/help/sites-developing/workflows-best-practices.md)

