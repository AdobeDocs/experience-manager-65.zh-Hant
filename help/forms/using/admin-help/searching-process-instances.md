---
title: 搜尋程式執行個體
description: 您可以在「程式搜尋」頁面輸入搜尋條件，以尋找程式執行處理。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 35f9acbf-7a82-43b1-9e17-9be4de666212
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# 搜尋程式執行個體{#searching-for-process-instances}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

您可以在「程式搜尋」頁面輸入搜尋條件，以尋找程式執行處理。 您可以從表單工作流程頁面存取「程式搜尋」頁面，或按一下「程式執行個體」頁面上的「搜尋」來存取。

您可以輸入執行一般搜尋的基本條件、執行詳細搜尋的特定屬性，或執行組合搜尋的基本條件和特定屬性的組合。

## 執行一般搜尋 {#perform-a-general-search}

如果您知道流&#39;b5&#39;7b執行個體的流&#39;b5&#39;7b識別碼、正在尋找一組相關的流&#39;b5&#39;7b執行個體，或只有少數幾個流&#39;b5&#39;7b執行個體正在執行，一般搜尋流&#39;b5&#39;7b是最適當的。

輸入執行一般搜尋的基本條件。 如果您輸入多個條件，則會以隱含的AND條件執行搜尋。

1. 在管理控制檯中，按一下「服務> Forms工作流程>程式搜尋」。
1. 在「程式搜尋」頁面的「一般搜尋」底下，提供下列條件：

   * **處理序識別碼：**&#x200B;識別每個唯一處理序執行個體的正整數。
   * **處理狀態：**&#x200B;從清單中選取狀態。
   * **應用程式：**&#x200B;從清單中選取應用程式。 只會顯示已部署的應用程式。
   * **處理程式名稱 — 版本：**&#x200B;從功能表選取處理程式名稱。 只顯示已部署的流程。

1. 按一下「搜尋」。 便會顯示「處理執行處理」頁面，列出找到的執行處理。

## 執行流程的詳細搜尋 {#perform-a-detailed-search-for-a-process}

您可以輸入特定屬性來執行詳細搜尋。 如果您有許多執行中的程式執行個體，而且需要依特定條件縮小可能的搜尋範圍，則詳細搜尋是最合適的選擇。

1. 在管理控制檯中，按一下「服務> Forms工作流程>程式搜尋」。
1. 在「程式搜尋」頁面的「詳細搜尋」底下，指定您的第一個條件集：

   * 在「屬性」清單中，選取屬性。
   * 在「篩選」清單中，選取運運算元。
   * 在「值」方塊中，鍵入適合所選屬性的值。

1. 若要新增其他列，請選取「更多篩選器」。 另一組「屬性」、「篩選」和「值」清單會出現，並出現一個「條件」清單。
1. 在「條件」下，選取AND或OR。 視需要重複步驟1到3，進一步縮小搜尋範圍。
1. 若要新增或移除列，請按一下「更多篩選器」或「更少篩選器」。 您可以有一到四列。
1. 按一下「搜尋」。 便會顯示「處理執行處理」頁面，列出找到的執行處理。

[關於流程例項狀態](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## 執行流程的組合搜尋 {#perform-a-combined-search-for-a-process}

若要根據一般搜尋和詳細搜尋建立搜尋，並在區域之間加上隱含的AND，請在「程式搜尋」頁面的「一般搜尋」和「詳細搜尋」區域中輸入搜尋條件。

如果搜尋太窄，則找不到任何例項。
