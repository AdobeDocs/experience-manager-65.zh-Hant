---
title: 搜索進程實例
seo-title: Searching for process instances
description: 使用「流程搜索」頁可以輸入搜索標準以查找流程實例。
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

使用「流程搜索」頁可以輸入搜索標準以查找流程實例。 您可以從表單工作流頁或按一下「流程實例」頁上的「搜索」來訪問「流程搜索」頁。

您可以輸入基本標準以執行常規搜索，輸入特定屬性以執行詳細搜索，或輸入基本標準和特定屬性的組合以執行組合搜索。

## 執行常規搜索 {#perform-a-general-search}

如果您知道進程實例的進程ID、要查找一組相關進程實例，或者只運行了幾個進程實例，則最適合對進程進行常規搜索。

輸入基本條件以執行常規搜索。 如果輸入多個條件，則使用隱含的AND條件執行搜索。

1. 在管理控制台中，按一下「服務」>「Forms」工作流>「進程搜索」。
1. 在「流程搜索」頁的「常規搜索」下，提供以下條件：

   * **進程ID:** 標識每個唯一進程實例的正整數。
   * **進程狀態：** 從清單中選擇狀態。
   * **應用程式：** 從清單中選擇應用程式。 只顯示已部署的應用程式。
   * **進程名稱 — 版本：** 從菜單中選擇進程名稱。 僅顯示已部署的進程。

1. 按一下「Search（搜索）」。 此時將顯示「進程實例」頁，其中列出了找到的實例。

## 對流程執行詳細搜索 {#perform-a-detailed-search-for-a-process}

您可以輸入特定屬性以執行詳細搜索。 如果您正在運行許多進程實例，並且需要按特定標準縮小可能的查找範圍，則最適合進行詳細搜索。

1. 在管理控制台中，按一下「服務」>「Forms」工作流>「進程搜索」。
1. 在「流程搜索」頁的「詳細搜索」下，指定第一個標準集：

   * 在「屬性」(Attribute)清單中，選擇一個屬性。
   * 在「篩選器」清單中，選擇一個運算子。
   * 在「值」(Value)框中，鍵入與所選屬性相適應的值。

1. 要添加另一行，請選擇「更多篩選器」。 另一組「屬性」、「篩選器」和「值」清單以及「條件」清單出現。
1. 在「條件」(Condition)下，選擇「與」(AND)或「或」(OR)。 根據需要重複步驟1 - 3以進一步縮小搜索範圍。
1. 要添加或刪除行，請按一下「更多」或「更少」。 您可以有一至四行。
1. 按一下「Search（搜索）」。 此時將顯示「進程實例」頁，其中列出了找到的實例。

[關於流程實例狀態](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## 對流程執行組合搜索 {#perform-a-combined-search-for-a-process}

要基於常規搜索和詳細搜索建立搜索，並在區域之間使用隱含的AND，請在「流程搜索」(Process Search)頁面的「常規搜索」(General Search)和「詳細搜索」(Detaile Search)區域中輸入搜索條件。

如果搜索範圍太窄，將找不到任何實例。
