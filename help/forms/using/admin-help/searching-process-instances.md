---
title: 搜索進程實例
seo-title: 搜索進程實例
description: 使用「流程搜索」頁可以輸入查找流程實例的搜索標準。
seo-description: 使用「流程搜索」頁可以輸入查找流程實例的搜索標準。
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# 搜索進程實例{#searching-for-process-instances}

使用「流程搜索」頁可以輸入查找流程實例的搜索標準。 您可以從表單工作流頁或按一下「流程實例」頁上的「搜索」訪問「流程搜索」頁。

您可以輸入基本標準來執行一般搜索、執行詳細搜索的特定屬性，或輸入基本標準和特定屬性的組合來執行組合搜索。

## 執行常規搜索{#perform-a-general-search}

如果您知道流程實例的流程ID、查找一組相關的流程實例，或者只運行了幾個流程實例，則最適合對流程進行常規搜索。

輸入基本標準以執行一般搜索。 如果輸入多個條件，則使用隱含的AND條件執行搜索。

1. 在管理控制台中，按一下「服務>表單工作流程>流程搜尋」。
1. 在「流程搜索」頁的「常規搜索」下，提供以下條件：

   * **流程ID：標** 識每個唯一流程實例的正整數。
   * **流程狀態：** 從清單中選擇狀態。
   * **應用程** 式：從清單中選取應用程式。僅顯示已部署的應用程式。
   * **流程名稱——版本：** 從菜單中選擇流程名稱。僅顯示已部署的進程。

1. 按一下「搜尋」。 此時將顯示「流程實例」頁，列出找到的實例。

## 對進程{#perform-a-detailed-search-for-a-process}執行詳細搜索

您可以輸入特定屬性來執行詳細搜索。 如果您有許多流程實例正在運行，並且需要根據特定條件縮小可能的查找範圍，則最適合進行詳細搜索。

1. 在管理控制台中，按一下「服務>表單工作流程>流程搜尋」。
1. 在「流程搜索」頁的「詳細搜索」下，指定您的第一個標準集：

   * 在「屬性」清單中，選擇一個屬性。
   * 在「篩選」清單中，選取運算子。
   * 在「值」(Value)框中，鍵入與所選屬性相適應的值。

1. 若要新增另一列，請選取更多篩選。 出現另一組「屬性」、「篩選」和「值」清單，以及「條件」清單。
1. 在「條件」(Condition)下，選擇「AND」(AND)或「OR」(OR)。 根據需要重複步驟1 - 3以進一步縮小搜索範圍。
1. 若要新增或移除列，請按一下更多篩選或更少篩選。 您可以有一至四列。
1. 按一下「搜尋」。 此時將顯示「流程實例」頁，列出找到的實例。

[關於流程實例狀態](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## 對進程{#perform-a-combined-search-for-a-process}執行組合搜索

要基於常規搜索和詳細搜索建立搜索，並在區域之間使用默示AND，請在「流程搜索」頁的「常規搜索」和「詳細搜索」區域中輸入搜索標準。

如果搜尋範圍太窄，將找不到任何例項。
