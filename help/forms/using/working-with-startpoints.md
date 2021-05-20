---
title: 使用起始點
seo-title: 使用起始點
description: 從Workbench中定義的行動裝置使用AEM Forms程式的步驟。
seo-description: 從Workbench中定義的行動裝置使用AEM Forms程式的步驟。
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 使用起始點{#working-with-startpoints}

起始點調用在Workbench中建立的進程。 它與表單關聯，表單提交時該表單將調用該流程。

>[!NOTE]
>
>提及此概念時，術語起始點、開始程式和表單可交互使用。

若要從AEM Forms應用程式啟動程式，您的程式中必須有&#x200B;**Workspace**&#x200B;類型的起始點。 此外，您還需要為起始點選取&#x200B;**[!UICONTROL 行動工作區中的可見度]**&#x200B;選項。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**要啟動在Workbench中定義的流程，請執行以下操作**

1. 若要檢視AEM Forms應用程式中可用的起始點，請前往[主畫面](../../forms/using/home-screen.md)。
1. 依預設，在&#x200B;**[!UICONTROL Home]**&#x200B;畫面上，會顯示&#x200B;**[!UICONTROL 所有Forms]**&#x200B;清單。

   起始點與表單相關聯。 點選清單中的起始點關聯表單以開啟它。

   將開啟與起始點關聯的表單。

1. 在&#x200B;**[!UICONTROL 起始點]**&#x200B;表單中輸入詳細資訊。

   您可以使用[attachment](../../forms/using/add-attachments.md)按鈕向此任務添加註釋。

1. 填寫表單後，點選&#x200B;**[!UICONTROL Submit]**&#x200B;按鈕。

如果應用程式離線，表單及其資料會儲存在「寄件匣」資料夾中。

如果應用程式上線，則任務會與AEM Forms伺服器同步，並指派給程式中指定的使用者。

要處理任務清單中的任務，請參閱[開啟任務](/help/forms/using/open-task.md)。
