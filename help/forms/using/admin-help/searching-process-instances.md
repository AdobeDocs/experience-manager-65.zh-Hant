---
title: 搜索進程實例
seo-title: Searching for process instances
description: 使用「流程搜索」頁可以輸入查找流程實例的搜索標準。
seo-description: Use the Process Search page to enter search criteria for finding a process instance.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
exl-id: 35f9acbf-7a82-43b1-9e17-9be4de666212
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 搜索進程實例{#searching-for-process-instances}

使用「流程搜索」頁可以輸入查找流程實例的搜索標準。 您可以從表單工作流頁或按一下「流程實例」頁上的「搜索」來訪問「流程搜索」頁。

您可以輸入基本條件以執行一般搜索，輸入要執行詳細搜索的特定屬性，或輸入基本條件和特定屬性的組合以執行組合搜索。

## 執行一般搜索 {#perform-a-general-search}

如果您知道進程實例的進程ID、要查找一組相關進程實例，或者只運行了幾個進程實例，則最適合對進程進行一般搜索。

輸入基本標準以執行一般搜索。 如果您輸入多個條件，則會使用隱含的AND條件執行搜尋。

1. 在管理控制台中，按一下「服務>Forms工作流程>處理搜尋」。
1. 在「流程搜索」頁的「一般搜索」下，提供以下條件：

   * **進程ID:** 標識每個唯一進程實例的正整數。
   * **進程狀態：** 從清單中選取狀態。
   * **應用程式：** 從清單中選取應用程式。 僅顯示已部署的應用程式。
   * **進程名稱 — 版本：** 從菜單中選擇進程名。 只顯示已部署的進程。

1. 按一下「搜尋」。 此時將出現「進程實例」頁，列出找到的實例。

## 對流程執行詳細搜索 {#perform-a-detailed-search-for-a-process}

您可以輸入特定屬性以執行詳細搜索。 如果您有許多執行中的程式例項，且您需要依特定條件縮小可能的尋找範圍，則最適合進行詳細搜尋。

1. 在管理控制台中，按一下「服務>Forms工作流程>處理搜尋」。
1. 在「流程搜索」頁的「詳細搜索」下，指定您的第一個標準集：

   * 在「屬性」清單中，選擇一個屬性。
   * 在「篩選」清單中，選取運算子。
   * 在「值」(Value)框中，鍵入與所選屬性相應的值。

1. 若要新增另一列，請選取「更多篩選」。 另一組「屬性」、「篩選」和「值」清單以及「條件」清單隨即出現。
1. 在「條件」下，選擇「和」或「或」。 視需要重複步驟1 - 3以進一步縮小搜尋範圍。
1. 若要新增或移除列，請按一下「更多篩選器」或「更少篩選器」。 您可以有一至四列。
1. 按一下「搜尋」。 此時將出現「進程實例」頁，列出找到的實例。

[關於流程實例狀態](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## 對流程執行組合搜索 {#perform-a-combined-search-for-a-process}

要根據常規搜索和詳細搜索建立搜索，並在區域之間加上隱含的AND，請在「流程搜索」頁的「常規搜索」和「詳細搜索」區域中輸入搜索標準。

如果搜索範圍太窄，則找不到任何實例。
