---
title: 使用起點
seo-title: 使用起點
description: 從「工作台」中定義的行動裝置處理AEM Forms程式的步驟。
seo-description: 從「工作台」中定義的行動裝置處理AEM Forms程式的步驟。
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 使用起點{#working-with-startpoints}

起始點會叫用在「工作台」中建立的流程。 它與表單關聯，表單提交時會叫用流程。

>[!NOTE]
>
>提及此概念時，詞語的起點、開始程式和表單會互動使用。

若要從AEM Forms應用程式啟動程式，您必須在程式中具有類型&#x200B;**Workspace**&#x200B;的起點。 此外，您還需要為起點選擇「行動工作區中的&#x200B;**[!UICONTROL 訪客]**」選項。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**要啟動在Workbench中定義的流程，請執行以下操作：**

1. 若要檢視AEM Forms應用程式中的「起點」，請前往[首頁畫面](../../forms/using/home-screen.md)。
1. 預設情況下，在&#x200B;**[!UICONTROL Home]**&#x200B;螢幕上，將顯示&#x200B;**[!UICONTROL 所有表單]**&#x200B;清單。

   起始點與表單相關聯。 點選清單中的起點關聯表單以開啟它。

   與起點關聯的表單隨即開啟。

1. 在&#x200B;**[!UICONTROL Startpoint]**&#x200B;表單中輸入詳細資訊。

   可以使用[attachment](../../forms/using/add-attachments.md)按鈕將注釋添加到此任務中。

1. 填寫表單後，點選&#x200B;**[!UICONTROL Submit]**&#x200B;按鈕。

如果應用程式已離線，表單及其資料會儲存在「輸出方塊」檔案夾中。

如果應用程式已連線，則工作會與AEM Forms伺服器同步，並指派給流程中指定的使用者。

要處理任務清單中的任務，請參閱[開啟任務](/help/forms/using/open-task.md)。
