---
title: 使用起點
description: 從Workbench中定義的行動裝置使用Adobe Experience Manager Forms程式的步驟。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%
---

# 使用起點{#working-with-startpoints}

>[!NOTE]
>
>AEM Forms應用程式目前已棄用。 如有疑問或需要協助，請連絡[aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com)。

起點會叫用在Workbench中建立的程式。 它與表單相關聯，在提交表單時會叫用流程。

>[!NOTE]
>
>在提及此概念時，術語起點、開始流程和表單可互換使用。

若要從Adobe Experience Manager (AEM) Forms應用程式起始程式，您程式的起點型別必須為&#x200B;**Workspace**。 此外，您必須選取&#x200B;**[!UICONTROL 在行動Workspace中可見]**&#x200B;選項作為起點。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**啟動Workbench中定義的程式**

1. 若要檢視AEM Forms應用程式中可用的起點，請移至[主畫面](../../forms/using/home-screen.md)。
1. 在&#x200B;**[!UICONTROL 首頁]**&#x200B;畫面上，預設會顯示&#x200B;**[!UICONTROL 所有Forms]**&#x200B;清單。

   起點與表單相關聯。 在清單中選取與表單關聯的起點以開啟它。

   與起點關聯的表單隨即開啟。

1. 在&#x200B;**[!UICONTROL 起點]**&#x200B;表單中輸入詳細資料。

   您可以使用[附件](../../forms/using/add-attachments.md)按鈕將註解新增至此工作。

1. 填寫表單之後，請選取&#x200B;**[!UICONTROL 提交]**&#x200B;按鈕。

如果應用程式離線，表單及其資料會儲存在「寄件匣」資料夾中。

如果應用程式線上上，工作會與AEM Forms伺服器同步，並指派給程式中指定的使用者。

若要使用工作清單中的工作，請參閱[開啟工作](/help/forms/using/open-task.md)。
