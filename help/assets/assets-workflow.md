---
title: 使用工作流程處理資產
description: 資產處理，以轉換格式、建立轉譯、管理資產、驗證資產，以及執行工作流程。
contentOwner: AG
feature: 工作流程、轉譯
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 3%

---


# 處理數位資產{#process-assets}

[!DNL Adobe Experience Manager Assets] 可讓您以多種方式處理您的數位資產，以便進行強穩的資產處理。您可以使用預設或自訂的處理方法來確保端對端業務流程的完成、稽核和合規性、發現和分發，以及數位資產的基本健全性。 您可以執行資產管理任務，同時達到所需的規模和定制。

## 瞭解工作流程{#understand-workflows}

對於資產處理，[!DNL Experience Manager]使用工作流程。 工作流程可協助自動化商業邏輯或活動。 預設會提供完成特定工作的詳細步驟，而開發人員可建立其自訂步驟。 這些步驟可依邏輯順序組合，以建立工作流程。 例如，工作流程可以根據特定條件對上傳的影像套用浮水印，例如上傳到的資料夾、影像解析度等。 另一個範例是設定為浮水印和同時新增中繼資料、建立轉譯、新增智慧標籤和發佈至資料儲存區的工作流程。

## [!DNL Experience Manager] {#default-workflows}中提供的預設工作流程

依預設，所有上傳的資產都會使用[!UICONTROL DAM更新資產]工作流程來處理。 工作流程會針對每個上傳的資產執行，並完成基本的資產管理工作，例如轉譯產生、中繼資料回寫、頁面擷取、媒體擷取和轉碼。

要查看預設可用的各種工作流模型，請參閱[!DNL Experience Manager]中的&#x200B;**[!UICONTROL 工具>工作流>模型]**。

![部分預設工作流程](assets/aem-default-workflows.png)

*圖：中提供的部分預設工作流程 [!DNL Experience Manager]。*

## 套用工作流程以處理資產{#applying-workflows-to-assets}

將工作流程套用至數位資產與網站頁面相同。 有關如何建立和使用工作流的完整指南，請參閱[啟動工作流](/help/sites-authoring/workflows-participating.md)。

在數位資產中使用工作流程來啟用資產或建立浮水印。 資產的許多工作流程都會自動開啟。 例如，編輯影像後自動建立轉譯的工作流程會自動開啟。

>[!NOTE]
>
>如果Classic UI中的工作流程在啟用觸控的UI中不可用，例如[!UICONTROL 請求啟用]和[!UICONTROL 請求停用]，請參閱[make workflow models](/help/sites-developing/workflows-models.md#classic2touchui)。

## 將工作流程套用至資產{#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
若要將工作流程套用至資產，請依照下列步驟進行：

1. 導覽至您要啟動工作流程的資產所在位置，然後按一下資產以開啟資產頁面。 從菜單中選擇&#x200B;**[!UICONTROL 時間軸]**&#x200B;以顯示時間軸。

   ![timeline-1](assets/timeline.png)

1. 按一下底部的&#x200B;**[!UICONTROL 動作]**&#x200B;以開啟資產可用動作清單。

1. 按一下清單中的&#x200B;**[!UICONTROL 啟動工作流]**。

1. 在&#x200B;**[!UICONTROL 啟動工作流]**&#x200B;對話框中，從清單中選擇工作流模型。

1. （可選）指定可用於參考工作流實例的工作流標題。

   ![選取工作流程，提供標題並按一下「開始」](assets/start-workflow.png)

1. 按一下&#x200B;**[!UICONTROL 開始]** ，然後按一下&#x200B;**[!UICONTROL 繼續]**。 工作流程的每個步驟都會以事件的形式顯示在時間軸中。

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 將工作流程套用至多個資產{#applying-a-workflow-to-multiple-assets}

1. 從[!DNL Assets]主控台，導覽至您要啟動工作流程的資產所在的位置，然後選取資產。 從菜單中選擇&#x200B;**[!UICONTROL 時間軸]**&#x200B;以顯示時間軸。

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 按一下底部的&#x200B;**[!UICONTROL Actions]** ![chevron up](assets/do-not-localize/chevron-up-icon.png)。
1. 按一下&#x200B;**[!UICONTROL 啟動工作流]**。 在&#x200B;**[!UICONTROL 啟動工作流]**&#x200B;對話框中，從清單中選擇工作流模型。

   ![啟動工作流程](assets/start-workflow.png)

1. （可選）指定工作流的標題，可用來參考工作流實例。
1. 按一 **[!UICONTROL 下「開始]** 」，然後按一 **[!UICONTROL 下對話方塊中的「確認]** 」。工作流程會在您選取的所有資產上執行。

## 將工作流應用於多個資料夾{#applying-a-workflow-to-multiple-folders}

將工作流程套用至多個檔案夾的程式，類似於將工作流程套用至多個資產的程式。 在[!DNL Assets]介面中選擇資料夾，並執行[過程中的步驟2-7將工作流應用到多個資產](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets)。

## 將工作流程套用至系列{#applying-a-workflow-to-a-collection}

請參閱[在系列上套用工作流程](/help/assets/manage-collections.md#running-a-workflow-on-a-collection)。

## 自動啟動工作流程，有條件地處理資產{#auto-execute-workflow-on-some-assets}

管理員可以設定工作流程，根據預先定義的條件自動執行和處理資產。 此功能對於業務線使用者和行銷人員非常有用，例如，在特定資料夾上建立自訂工作流程。 說明機構像片拍攝的所有資產都可以浮水印，或是自由工作者上傳的所有資產都可以處理，以建立特定的轉譯。

對於工作流模型，用戶可以建立執行該模型的工作流啟動程式。 工作流啟動器監視內容儲存庫中的更改並在滿足預定義條件時執行工作流。 管理員可讓行銷人員存取建立工作流程和設定啟動程式。 使用者可修改預設的[!UICONTROL DAM更新資產]工作流程，以新增處理特定資產所需的額外步驟。 工作流程會對所有新上傳的資產執行。 使用下列方法之一來限制特定資產上額外步驟的執行：

* 製作[!UICONTROL DAM更新資產]工作流程的副本，並加以修改以在特定資料夾階層上執行。 此方法對於一些資料夾非常有用。
* 可以使用[OR split](/help/sites-developing/workflows-step-ref.md#or-split)添加附加處理步驟，作為條件性地適用於所需數量的資料夾。

## 最佳做法和限制{#best-practices-limitations-tips}

* 在設計工作流程時，請考慮您對所有類型轉譯的需求。 如果您未預見未來需要轉譯，請從工作流程中移除其建立步驟。 之後無法大量刪除轉譯。 長期使用[!DNL Experience Manager]後，不需要的轉譯可能佔用大量儲存空間。 對於個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自訂[!DNL Experience Manager]以刪除特定轉譯，或刪除資產並再次上傳這些資產。
* 依預設，[!UICONTROL DAM更新資產]工作流程包含一些建立縮圖和網頁轉譯的步驟。 如果從工作流中刪除了任何預設轉譯，則[!DNL Assets]的用戶介面無法正確顯示。

>[!MORELIKETHIS]
>
>* [套用並參與工作流程](/help/sites-authoring/workflows.md)
>* [建立工作流程模型並擴充工作流程功能](/help/sites-developing/workflows.md)
>* [執行工作流程的方法](/help/sites-administering/workflows-starting.md)
>* [工作流程最佳實務](/help/sites-developing/workflows-best-practices.md)

