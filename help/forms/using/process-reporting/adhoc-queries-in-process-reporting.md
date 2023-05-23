---
title: Oracle Process報告中的即席查詢
seo-title: Ad-hoc Queries in Process Reporting
description: 建立自定義查詢以在Process Reporting中搜索JEE流程和任務詳細資訊上的AEM Forms
seo-description: Create custom queries to search for AEM Forms on JEE  process and task details in Process Reporting
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
exl-id: a096eea0-b2fb-4d86-b729-ca47611135b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# Oracle Process報告中的即席查詢{#ad-hoc-queries-in-process-reporting}

## 進程報告中的即席查詢 {#ad-hoc-queries-in-process-reporting-1}

「流程報告」中的即席查詢允許您建立自定義查詢，您可以使用這些查詢來搜索在AEM Forms環境中定義的AEM Forms流程實例的流程和任務詳細資訊。

此外，可以使用進程和任務屬性篩選器定義即席查詢。 然後，可以保存這些篩選器並用於以後運行報告。

[**進程搜索**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p):使用基於進程屬性的用戶定義的搜索過濾器搜索進程實例。

[**流程詳細資訊**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p):通過指定進程ID查看進程實例的詳細資訊。

**任務搜索**:使用基於任務屬性的用戶定義的搜索篩選器搜索任務實例。

**任務詳細資訊**:通過指定任務ID查看任務實例的詳細資訊。

### 進程和任務 {#processes-and-tasks}

建立篩選器和運行流程詳細資訊查詢所遵循的步驟與任務的步驟相同。

這意味著「流程搜索」和「任務搜索」的用戶介面僅在您可以搜索的欄位和搜索結果中返回的欄位中不同。 這僅僅是因為，儘管許多欄位是相同的，但某些欄位是特定於進程的，某些欄位是特定於任務的。

本文詳細介紹了「流程/任務搜索」和「流程/任務詳細資訊」部分的說明。 在適當的地點，任何具體差異都將被特別地取消。

## 進程/任務搜索 {#process-task-search}

您可以使用「流程/任務搜索」來定義用於查詢流程/任務實例的篩選器。

### 建立「流程/任務搜索」查詢 {#to-create-a-process-task-search-query}

1. 要查看已保存的「流程/任務搜索」查詢或建立查詢，請按一下 **即席查詢** 然後按一下 **進程/任務搜索**。

   ![搜索節點](assets/search_nodes.png)

   的 **我的篩選器** 面板顯示在樹視圖的右側。

   在 **我的篩選器** 面板中，可以建立新的即席查詢，然後按一下以執行先前保存的查詢。

   ![my_filters_panel](assets/my_filters_panel.png)

1. 要執行現有查詢，只需按一下 **我的篩選器** 的子菜單。
1. 要建立查詢，請按一下 **添加** (+)。

   的 **建立篩選器** 顯示面板。

   ![create_filter_panel](assets/create_filter_panel.png)

   查詢由一個或多個查詢篩選器組成。 要建立篩選器，請向查詢添加篩選器行。 預設情況下，將向查詢添加一個篩選器行。

   **定義篩選器**

   1. 選擇一個欄位。

      ![篩選器欄位](assets/filter_field.png)

      >[!NOTE]
      >
      >欄位清單包含特定於AEM Forms進程/任務的欄位。

   1. 選擇條件。

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >列出的條件取決於選定進行篩選的屬性。

   1. 輸入值。

      ![filter_value](assets/filter_value.png)

   1. 要向查詢添加其他篩選器，請按一下 **添加(+)** 的上界。

      要從查詢中刪除篩選器，請按一下 **刪除(-)** 的上界。

      ![filter_add_del](assets/filter_add_del.png)

建立查詢後，使用 **建立篩選器** 面板：

* **取消**:取消更改並返回到 **我的篩選器** 的子菜單。
* **運行**:執行當前查詢以查看和/或驗證結果。 在這種情況下，您無需在執行查詢之前保存查詢。 您可以驗證結果，根據需要進行更改，然後在對輸出滿意時保存查詢。
* **保存**:保存篩選器。 然後，可從 **我的篩選器** 的子菜單。

### 「我的篩選器」面板中的選項 {#options-in-my-filters-panel}

使用 **我的篩選器** 面板 **添加** ![lc_pr_add_filter](assets/lc_pr_add_filter.png)。 **編輯** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png)或 **刪除** ![lc_pr_edit_filter](assets/lc_pr_edit_filter.png)即席查詢。

![my_filters_options](assets/my_filters_options.png)

### 執行搜索查詢 {#to-execute-a-search-query}

1. 要執行查詢，請按一下 **我的篩選器** 或按一下 **運行** 按鈕。
1. 查詢結果顯示在 **報告** 的 **流程報告** 的子菜單。

   ![process_search_result](assets/process_search_result.png)

   您可以借助報告底部顯示的分頁面板的幫助來分頁搜索結果。

   ![process_result_pgn](assets/process_result_pgn.png)

   在 **顯示** 下拉清單，選擇每頁顯示的結果數。

   在 **頁面** 的子菜單。

1. 「流程搜索」結果中顯示以下欄位：

   * **進程ID**:進程的ID。 該欄位是超連結的。 如果按一下此欄位中的進程ID，則會將您重定向到 **[!UICONTROL 流程詳細資訊]** 的子菜單。
   * **啟動器**:啟動進程實例的AEM Forms用戶
   * **建立時間**:流程實例啟動的日期和時間
   * **完成時間**:流程實例完成的日期和時間
   * **持續時間**:流程實例從開始到完成的持續時間
   * **狀態**:進程實例的當前狀態。

   預設情況下，結果按「進程ID」排序。 但是，要按任何欄位對結果進行排序，請按一下欄位標題。

   由於排序是切換操作，因此按一下列標題以升序對結果進行排序，然後再次按一下它以降序排序。

   同樣，「任務搜索」結果中顯示以下欄位：

   * **任務ID**:任務的ID。 該欄位是超連結的。 如果按一下此欄位中的任務ID，則會將您重定向到 **[!UICONTROL 任務詳細資訊]** 的子菜單。
   * **啟動器**:啟動進程實例的AEM Forms用戶
   * **建立時間**:流程實例啟動的日期和時間
   * **完成時間**:流程實例完成的日期和時間
   * **持續時間**:流程實例從開始到完成的持續時間
   * **狀態**:進程實例的當前狀態。

   預設情況下，結果按任務ID排序。 但是，要按任何欄位對結果進行排序，請按一下欄位標題。 結果按列排序，列標題旁邊的一個暗箭頭指示。

   由於排序是切換操作，因此按一下欄位標題以升序對結果進行排序，然後再次按一下它以降序排序。 當前排序順序（升序/降序）由列標題旁邊的下箭頭方向指示。

   ![task_search_result](assets/task_search_result.png)

1. 按一下滑軌按鈕 ![lc_pr_rail_button](assets/lc_pr_rail_button.png) 在左上角折疊 **我的篩選器** 並擴展可用於 **報告** 的子菜單。
1. 使用**報表**面板右上角的選項對查詢結果執行操作。

   * **刷新**:使用儲存中的最新資料刷新報表

   * **導出為CSV**:將報告資料導出到逗號分隔的檔案。
   >[!NOTE]
   >
   >導出報告時，搜索的整個結果將導出為CSV檔案，而不僅僅是當前頁面

## 流程/任務詳細資訊 {#process-task-details}

使用 **流程詳細資訊** 查看特定流程的詳細資訊。

同樣，您使用 **任務詳細資訊** 查看特定任務的詳細資訊。

### 查看流程/任務詳細資訊 {#to-view-process-task-details}

您可以查看特定AEM Forms進程/任務的詳細資訊：

* **從流程/任務搜索結果**
* **通過在「流程/任務詳細資訊」面板中輸入流程/任務ID**

#### 從流程/任務搜索結果 {#from-a-process-task-search-result}

1. 執行進程/任務搜索。 有關詳細資訊，請參閱 [執行進程搜索查詢](#to-execute-a-search-query)。

   請注意，結果中返回的顯示進程ID是超連結的。

   ![進程_id_list](assets/process_id_list.png)

1. 按一下清單中的進程ID，在 **流程詳細資訊** 的子菜單。

   的 **流程/任務詳細資訊** 查詢結果顯示流程/任務中包含的任務/表單的詳細資訊。

   預設情況下，結果按任務/表單ID排序。 但是，要按任何欄位對結果進行排序，請按一下欄位標題。 對結果排序所依據的列由列標題旁邊的一個暗箭頭指示。

   由於排序是切換操作，因此按一下欄位標題以升序對結果進行排序，然後再次按一下它以降序排序。 當前排序順序（升序/降序）由列標題旁邊的下箭頭方向指示。

   **流程詳細資訊結果**

   ![進程詳細資訊](assets/process_details.png)

   **左面板：** 顯示所選進程的以下詳細資訊：

   * 進程名稱
   * 流程建立日期時間
   * 處理完成日期時間
   * 進程持續時間
   * 進程狀態
   * 進程啟動器

   **右上面板：** 顯示組成選定流程的任務的以下詳細資訊：

   * 任務ID
   * 任務名稱
   * 任務所有者
   * 任務建立日期時間
   * 任務更新日期時間
   * 任務完成日期時間
   * 任務持續時間
   * 任務狀態

   **右下面板：** 顯示所選進程的進程歷史記錄的以下詳細資訊：

   * 進程名稱
   * 進程啟動器
   * 進程更新日期時間
   * 處理完成日期時間
   * 進程狀態

   **任務詳細資訊結果**

   ![任務詳細資訊](assets/task_details.png)

   **左面板：** 顯示所選任務的以下詳細資訊：

   * 任務名稱
   * 此任務所屬進程的ID
   * 任務描述
   * 任務建立日期時間
   * 任務完成日期時間
   * 任務持續時間
   * 任務狀態
   * 選定的任務路線

   **右上面板：** 顯示組成選定任務的表單的以下詳細資訊：

   * 檔案ID
   * 表單建立日期時間
   * 表單更新日期時間
   * 表單模板URL

   **右下面板：** 顯示所選任務的流程歷史記錄的以下詳細資訊：

   * 任務分配類型
   * 任務所有者
   * 任務分配建立日期時間
   * 任務更新日期時間






1. 按一下 **返回進程/任務搜索** 返回到從中向下鑽取流程/任務詳細資訊的搜索結果。

   ![返回_搜索](assets/back_to_search.png)

   但是，如果通過輸入特定流程/任務ID找到流程/任務詳細資訊，則按一下「返回至流程/任務搜索」將返回至 **進程/任務搜索**，而不顯示任何搜索結果。

#### 通過在「流程/任務詳細資訊」面板中輸入流程/任務ID {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. 轉到 **流程/任務詳細資訊** 的子菜單。

   ![詳細資訊_節點](assets/details_nodes.png)

1. 在「流程/任務標識」文本框中，輸入流程/任務標識。

   ![process_details-1](assets/process_details-1.png)

   中的欄位 **流程/任務詳細資訊** 查詢結果是特定於AEM Forms進程/任務的欄位。

   對於流程，查詢結果將顯示流程中包含的任務的詳細資訊。

   對於任務，查詢結果將顯示任務中包含的表單的詳細資訊。
