---
title: 流程報告中的臨機查詢
seo-title: Ad-hoc Queries in Process Reporting
description: 建立自訂查詢，以在JEE流程上搜尋AEM Forms，以及在流程報表中搜尋任務詳細資訊
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

# 流程報告中的臨機查詢{#ad-hoc-queries-in-process-reporting}

## 進程報告中的臨機查詢 {#ad-hoc-queries-in-process-reporting-1}

「處理報告」中的臨機查詢可讓您建立自訂查詢，以便搜尋在您的AEM Forms環境中定義之AEM Forms處理例項的處理程式和任務詳細資訊。

此外，可以使用進程和任務屬性篩選器來定義Ad Hoc查詢。 然後，可儲存這些篩選器，並用於稍後執行報表。

[**進程搜索**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p):根據流程屬性使用用戶定義的搜索篩選器搜索流程實例。

[**流程詳細資訊**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p):通過指定進程ID查看進程實例的詳細資訊。

**任務搜索**:根據任務屬性使用用戶定義的搜索篩選器搜索任務實例。

**任務詳細資訊**:通過指定任務ID查看任務實例的詳細資訊。

### 流程和任務 {#processes-and-tasks}

建立篩選器和運行進程詳細資訊查詢所遵循的步驟與任務的步驟相同。

這表示「進程搜索」和「任務搜索」的用戶介面僅在可搜索的欄位和搜索結果中返回的欄位中不同。 這只是因為，雖然許多欄位相同，但某些欄位是流程專屬的，而某些欄位是任務專屬的。

本文詳細說明了「流程/任務搜索」和「流程/任務詳細資訊」各節的說明。 在適當的位置，會明確提出任何特定差異。

## 進程/任務搜索 {#process-task-search}

您可以使用「流程/任務搜索」來定義查詢流程/任務實例的篩選器。

### 建立流程/任務搜索查詢 {#to-create-a-process-task-search-query}

1. 要查看保存的流程/任務搜索查詢或要建立查詢，請按一下 **臨機查詢** 然後按一下 **進程/任務搜索**.

   ![search_nodes](assets/search_nodes.png)

   此 **我的篩選器** 面板會顯示在樹視圖的右側。

   在 **我的篩選器** 面板中，您可以建立新的臨機查詢，然後按一下以執行先前儲存的查詢。

   ![my_filters_panel](assets/my_filters_panel.png)

1. 若要執行現有查詢，只需按一下 **我的篩選器** 中。
1. 若要建立查詢，請按一下 **新增** (+)。

   此 **建立篩選** 面板隨即顯示。

   ![create_filter_panel](assets/create_filter_panel.png)

   查詢由一個或多個查詢篩選器組成。 若要建立篩選器，請新增篩選器列至查詢。 依預設，會將一個篩選列新增至查詢。

   **定義篩選**

   1. 選取欄位。

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >欄位清單包含AEM Forms流程/任務專屬的欄位。

   1. 選取條件。

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >列出的條件取決於要篩選的屬性。

   1. 輸入值。

      ![filter_value](assets/filter_value.png)

   1. 若要新增其他篩選器至查詢，請按一下 **添加(+)** 在篩選列的右側。

      若要從查詢中移除篩選器，請按一下 **刪除(-)** 在篩選列的右側。

      ![filter_add_del](assets/filter_add_del.png)

建立查詢後，請使用 **建立篩選** 面板至：

* **取消**:取消變更，然後返回 **我的篩選器** 中。
* **執行**:執行當前查詢以查看和/或驗證結果。 在這種情況下，您無需在執行查詢之前保存查詢。 您可以驗證結果、根據需要進行更改，然後在對輸出滿意時保存查詢。
* **儲存**:儲存篩選器。 然後，您就可以從 **我的篩選器** 中。

### 「我的篩選器」面板中的選項 {#options-in-my-filters-panel}

在 **我的篩選器** 面板 **新增** ![lc_pr_add_filter](assets/lc_pr_add_filter.png), **編輯** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png)，或 **刪除** ![lc_pr_edit_filter](assets/lc_pr_edit_filter.png)臨機查詢。

![my_filters_options](assets/my_filters_options.png)

### 執行搜索查詢 {#to-execute-a-search-query}

1. 若要執行查詢，請按一下 **我的篩選器** 或按一下 **執行** 按鈕。
1. 查詢的結果會顯示在 **報表** 面板 **流程報告** 窗口。

   ![process_search_result](assets/process_search_result.png)

   您可以透過顯示於報表底部的分頁面板來分頁搜尋結果。

   ![process_result_pgn](assets/process_result_pgn.png)

   在 **顯示** 下拉式清單中，選擇每頁要顯示的結果數。

   在 **頁面** 框中，輸入要直接訪問該頁的頁碼。

1. 「流程搜索」結果中顯示以下欄位：

   * **程式ID**:程式ID。 欄位為超連結。 如果按一下此欄位中的程式ID，系統會將您重新導向至 **[!UICONTROL 流程詳細資訊]** 面板。
   * **啟動器**:啟動進程實例的AEM Forms用戶
   * **建立時間**:流程實例啟動的日期和時間
   * **完成時間**:流程實例完成的日期和時間
   * **持續時間**:流程實例從開始到完成的持續時間
   * **狀態**:進程實例的當前狀態。

   依預設，結果會依處理程式ID排序。 不過，若要依任何欄位來排序結果，請按一下欄位標題。

   由於排序是切換操作，按一下欄標題可遞增排序結果，再按一下以遞減排序。

   同樣地，「任務搜索結果」中顯示以下欄位：

   * **任務ID**:任務的ID。 欄位為超連結。 如果按一下此欄位中的任務ID，系統會將您重新導向至 **[!UICONTROL 任務詳細資訊]** 面板。
   * **啟動器**:啟動進程實例的AEM Forms用戶
   * **建立時間**:流程實例啟動的日期和時間
   * **完成時間**:流程實例完成的日期和時間
   * **持續時間**:流程實例從開始到完成的持續時間
   * **狀態**:進程實例的當前狀態。

   預設情況下，結果按任務ID排序。 不過，若要依任何欄位來排序結果，請按一下欄位標題。 結果按列排序，列標題旁邊的暗箭頭指示。

   由於排序是切換操作，按一下欄位標題可遞增排序結果，再按一下它可遞減排序。 當前排序順序（升序/降序）由列標題旁的暗箭頭方向指示。

   ![task_search_result](assets/task_search_result.png)

1. 按一下邊欄按鈕 ![lc_pr_rail_button](assets/lc_pr_rail_button.png) 在左上角折疊 **我的篩選器** 窗格，並展開 **報表** 中。
1. 使用**Report **面板右上角的選項對查詢結果執行操作。

   * **重新整理**:重新整理報表，將最新資料放在儲存中

   * **匯出至CSV**:將報表資料匯出至逗號分隔的檔案。
   >[!NOTE]
   >
   >匯出報表時，搜尋的整個結果會匯出為CSV檔案，而不只是目前頁面

## 進程/任務詳細資訊 {#process-task-details}

您使用 **流程詳細資訊** 面板來檢視特定程式的詳細資訊。

同樣地，您也會使用 **任務詳細資訊** 面板，查看特定任務的詳細資訊。

### 查看流程/任務詳細資訊 {#to-view-process-task-details}

您可以檢視特定AEM Forms程式/任務的詳細資訊：

* **從進程/任務搜索結果**
* **在「流程/任務詳細資訊」面板中輸入流程/任務ID**

#### 從進程/任務搜索結果 {#from-a-process-task-search-result}

1. 執行進程/任務搜索。 如需詳細資訊，請參閱 [執行進程搜索查詢](#to-execute-a-search-query).

   請注意，結果中傳回的顯示處理ID為超連結。

   ![process_id_list](assets/process_id_list.png)

1. 按一下清單中的程式ID，即可在 **流程詳細資訊** 中。

   此 **進程/任務詳細資訊** 查詢結果顯示流程/任務中包含的任務/表單的詳細資訊。

   依預設，結果會依任務/表單ID排序。 不過，若要依任何欄位來排序結果，請按一下欄位標題。 結果排序依據的列在列標題旁邊的暗箭頭中指示。

   由於排序是切換操作，按一下欄位標題可遞增排序結果，再按一下它可遞減排序。 當前排序順序（升序/降序）由列標題旁的暗箭頭方向指示。

   **流程詳細資訊結果**

   ![process_details](assets/process_details.png)

   **左面板：** 顯示所選進程的以下詳細資訊：

   * 進程名稱
   * 流程建立日期時間
   * 處理完成日期時間
   * 處理期間
   * 進程狀態
   * 進程啟動器

   **右上面板：** 顯示組成所選進程的任務的以下詳細資訊：

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
   * 處理更新日期時間
   * 處理完成日期時間
   * 進程狀態

   **任務詳細資訊結果**

   ![task_details](assets/task_details.png)

   **左面板：** 顯示所選任務的以下詳細資訊：

   * 任務名稱
   * 此任務所屬的進程ID
   * 任務說明
   * 任務建立日期時間
   * 任務完成日期時間
   * 任務持續時間
   * 任務狀態
   * 所選任務路由

   **右上面板：** 顯示組成所選任務的表單的以下詳細資訊：

   * 檔案ID
   * 表單建立日期時間
   * 表單更新日期時間
   * 表單範本Url

   **右下面板：** 顯示所選任務的進程歷史記錄的以下詳細資訊：

   * 任務分配類型
   * 任務所有者
   * 任務分配建立日期時間
   * 任務更新日期時間






1. 按一下 **返回進程/任務搜索** 返回搜索結果，從中細化流程/任務詳細資訊。

   ![back_to_search](assets/back_to_search.png)

   但是，如果通過輸入特定流程/任務ID找到了流程/任務詳細資訊，則按一下「返回流程/任務搜索」將返回 **進程/任務搜索**，不顯示任何搜尋結果。

#### 在「流程/任務詳細資訊」面板中輸入流程/任務ID {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. 前往 **進程/任務詳細資訊** 中。

   ![details_nodes](assets/details_nodes.png)

1. 在「流程/任務ID」文本框中，輸入流程/任務ID。

   ![process_details-1](assets/process_details-1.png)

   中的欄位 **進程/任務詳細資訊** 查詢結果是AEM Forms進程/任務的特定欄位。

   對於流程，查詢結果將顯示流程中包含的任務的詳細資訊。

   對於任務，查詢結果將顯示任務中包含的表單的詳細資訊。
