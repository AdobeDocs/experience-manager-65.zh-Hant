---
title: 使用起點
description: 從Workbench中定義的行動裝置使用Adobe Experience Manager Forms程式的步驟。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
source-git-commit: 60924e7ee204e43a2ff833fbc394beca8db9c9d9
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 使用起點{#working-with-startpoints}

起點會叫用在Workbench中建立的程式。 它與表單相關聯，在提交表單時會叫用流程。

>[!NOTE]
>
>在提及此概念時，術語起點、開始流程和表單可互換使用。

若要從Adobe Experience Manager (AEM) Forms應用程式起始程式，您必須有型別的起點 **Workspace** 在您的程式中。 此外，您必須選取 **[!UICONTROL 在行動工作區中可見]** 起點的選項。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**若要啟動在「維護作業」中定義的處理，請執行下列步驟：**

1. 若要檢視AEM Forms應用程式中可用的起點，請前往 [主畫面](../../forms/using/home-screen.md).
1. 於 **[!UICONTROL 首頁]** 畫面，預設情況下 **[!UICONTROL 所有Forms]** 清單隨即顯示。

   起點與表單相關聯。 點選清單中與表單相關聯的起點以開啟。

   與起點相關聯的表單隨即開啟。

1. 在「 」中輸入詳細資料 **[!UICONTROL 起點]** 表單。

   您可以使用將註解新增至此任務 [附件](../../forms/using/add-attachments.md) 按鈕。

1. 填妥表單後，點選 **[!UICONTROL 提交]** 按鈕。

如果應用程式離線，表單及其資料會儲存在Outbox資料夾中。

如果應用程式上線，則會與AEM Forms伺服器同步處理工作，並指派給程式中指定的使用者。

若要使用您任務清單中的任務，請參閱 [開啟任務](/help/forms/using/open-task.md).
