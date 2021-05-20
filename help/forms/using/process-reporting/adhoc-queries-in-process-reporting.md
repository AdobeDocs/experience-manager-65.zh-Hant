---
title: 流程報告中的臨機查詢
seo-title: 流程報告中的臨機查詢
description: 建立自訂查詢，以在JEE流程上搜尋AEM Forms，以及在流程報表中搜尋任務詳細資訊
seo-description: 建立自訂查詢，以在JEE流程上搜尋AEM Forms，以及在流程報表中搜尋任務詳細資訊
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
exl-id: a096eea0-b2fb-4d86-b729-ca47611135b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 0%

---

# 進程報告中的臨機查詢{#ad-hoc-queries-in-process-reporting}

## 進程報告中的臨機查詢{#ad-hoc-queries-in-process-reporting-1}

「處理報告」中的臨機查詢可讓您建立自訂查詢，以便搜尋在您的AEM Forms環境中定義之AEM Forms處理例項的處理程式和任務詳細資訊。

此外，可以使用進程和任務屬性篩選器來定義Ad Hoc查詢。 然後，可儲存這些篩選器，並用於稍後執行報表。

[**流程搜索**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p):根據流程屬性使用用戶定義的搜索篩選器搜索流程實例。

[**流程詳細資訊**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p):通過指定進程ID查看進程實例的詳細資訊。

**任務搜索**:根據任務屬性使用用戶定義的搜索篩選器搜索任務實例。

**任務詳細資訊**:通過指定任務ID查看任務實例的詳細資訊。

### 進程和任務{#processes-and-tasks}

建立篩選器和運行進程詳細資訊查詢所遵循的步驟與任務的步驟相同。

這表示「進程搜索」和「任務搜索」的用戶介面僅在可搜索的欄位和搜索結果中返回的欄位中不同。 這只是因為，雖然許多欄位相同，但某些欄位是流程專屬的，而某些欄位是任務專屬的。

本文詳細說明了「流程/任務搜索」和「流程/任務詳細資訊」各節的說明。 在適當的位置，會明確提出任何特定差異。

## 進程/任務搜索{#process-task-search}

您可以使用「流程/任務搜索」來定義查詢流程/任務實例的篩選器。

### 建立進程/任務搜索查詢{#to-create-a-process-task-search-query}

1. 要查看保存的進程/任務搜索查詢或要建立查詢，請按一下&#x200B;**臨機查詢**，然後按一下&#x200B;**進程/任務搜索**。

   ![search_nodes](assets/search_nodes.png)

   「**我的篩選器**」面板顯示在樹視圖的右側。

   在&#x200B;**我的篩選器**&#x200B;面板中，您可以建立新的臨機查詢，然後按一下以執行先前儲存的查詢。

   ![my_filters_panel](assets/my_filters_panel.png)

1. 要執行現有查詢，只需按一下&#x200B;**我的篩選器**&#x200B;面板中的查詢。
1. 若要建立查詢，請按一下&#x200B;**Add**(+)。

   隨即顯示&#x200B;**建立篩選器**&#x200B;面板。

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

   1. 若要新增其他篩選器至查詢，請按一下篩選器列右側的&#x200B;**新增(+)**。

      若要從查詢中移除篩選器，請按一下篩選器列右側的&#x200B;**刪除(-)**。

      ![filter_add_del](assets/filter_add_del.png)

建立查詢後，請使用&#x200B;**建立篩選器**&#x200B;面板右上角的選項來執行下列操作：

* **取消**:取消更改，然後返回「我的 **Filterspanel** 」。
* **執行**:執行當前查詢以查看和/或驗證結果。在這種情況下，您無需在執行查詢之前保存查詢。 您可以驗證結果、根據需要進行更改，然後在對輸出滿意時保存查詢。
* **儲存**:儲存篩選器。接著，您就可以從&#x200B;**我的篩選器**&#x200B;面板檢視並執行篩選器。

### 「我的篩選器」面板中的選項{#options-in-my-filters-panel}

使用「**我的篩選器**」面板中的選項到&#x200B;**Add** ![lc_pr_add_filter](assets/lc_pr_add_filter.png)、**Edit** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png)或&#x200B;**Delete** ![lc_pr_edit_filter](assets/lc_pr_edit_filter.png)a-hoc查詢。

![my_filters_options](assets/my_filters_options.png)

### 要執行搜索查詢{#to-execute-a-search-query}

1. 要執行查詢，請按一下&#x200B;**「我的篩選器」**&#x200B;面板中的篩選器，或按一下&#x200B;**運行**&#x200B;按鈕（如果要建立或編輯篩選器）。
1. 查詢結果顯示在&#x200B;**Process Reporting**&#x200B;窗口的&#x200B;**Report**&#x200B;面板中。

   ![process_search_result](assets/process_search_result.png)

   您可以透過顯示於報表底部的分頁面板來分頁搜尋結果。

   ![process_result_pgn](assets/process_result_pgn.png)

   在&#x200B;**Display**&#x200B;下拉式清單中，選擇每頁要顯示的結果數。

   在&#x200B;**Page**&#x200B;文字方塊中，輸入要直接前往該頁面的頁碼。

1. 「流程搜索」結果中顯示以下欄位：

   * **程式ID**:程式ID。欄位為超連結。 如果按一下此欄位中的進程ID，系統會將您重定向到該進程的&#x200B;**[!UICONTROL 進程詳細資訊]**&#x200B;面板。
   * **啟動器**:啟動進程實例的AEM Forms用戶
   * **建立時間**:流程實例啟動的日期和時間
   * **完成時間**:流程實例完成的日期和時間
   * **持續時間**:流程實例從開始到完成的持續時間
   * **狀態**:進程實例的當前狀態。

   依預設，結果會依處理程式ID排序。 不過，若要依任何欄位來排序結果，請按一下欄位標題。

   由於排序是切換操作，按一下欄標題可遞增排序結果，再按一下以遞減排序。

   同樣地，「任務搜索結果」中顯示以下欄位：

   * **任務ID**:任務的ID。欄位為超連結。 如果按一下此欄位中的任務ID，則系統會將您重定向到該任務的&#x200B;**[!UICONTROL 任務詳細資訊]**&#x200B;面板。
   * **啟動器**:啟動進程實例的AEM Forms用戶
   * **建立時間**:流程實例啟動的日期和時間
   * **完成時間**:流程實例完成的日期和時間
   * **持續時間**:流程實例從開始到完成的持續時間
   * **狀態**:進程實例的當前狀態。

   預設情況下，結果按任務ID排序。 不過，若要依任何欄位來排序結果，請按一下欄位標題。 結果按列排序，列標題旁邊的暗箭頭指示。

   由於排序是切換操作，按一下欄位標題可遞增排序結果，再按一下它可遞減排序。 當前排序順序（升序/降序）由列標題旁的暗箭頭方向指示。

   ![task_search_result](assets/task_search_result.png)

1. 按一下左上角的邊欄按鈕![lc_pr_rail_button](assets/lc_pr_rail_button.png)以折疊&#x200B;**我的篩選器**&#x200B;窗格並展開&#x200B;**報表**&#x200B;面板的可用空間。
1. 使用**Report **面板右上角的選項對查詢結果執行操作。

   * **重新整理**:重新整理報表，將最新資料放在儲存中

   * **匯出至CSV**:將報表資料匯出至逗號分隔的檔案。
   >[!NOTE]
   >
   >匯出報表時，搜尋的整個結果會匯出為CSV檔案，而不只是目前頁面

## 進程/任務詳細資訊{#process-task-details}

使用「**進程詳細資訊**」面板可以查看特定進程的詳細資訊。

同樣，您也可以使用&#x200B;**任務詳細資訊**&#x200B;面板來查看特定任務的詳細資訊。

### 查看進程/任務詳細資訊{#to-view-process-task-details}

您可以檢視特定AEM Forms程式/任務的詳細資訊：

* **從進程/任務搜索結果**
* **在「流程/任務詳細資訊」面板中輸入流程/任務ID**

#### 從進程/任務搜索結果{#from-a-process-task-search-result}

1. 執行進程/任務搜索。 有關詳細資訊，請參閱[執行進程搜索查詢](#to-execute-a-search-query)。

   請注意，結果中傳回的顯示處理ID為超連結。

   ![process_id_list](assets/process_id_list.png)

1. 按一下清單中的進程ID，在&#x200B;**進程詳細資訊**&#x200B;面板中查看此進程的詳細資訊。

   **進程/任務詳細資訊**&#x200B;查詢結果顯示進程/任務中包含的任務/表單的詳細資訊。

   依預設，結果會依任務/表單ID排序。 不過，若要依任何欄位來排序結果，請按一下欄位標題。 結果排序依據的列在列標題旁邊用暗箭頭指示。

   由於排序是切換操作，按一下欄位標題可遞增排序結果，再按一下它可遞減排序。 當前排序順序（升序/降序）由列標題旁的暗箭頭方向指示。

   **流程詳細資訊結果**

   ![process_details](assets/process_details.png)

   **左側面板：** 顯示所選取程式的下列詳細資料：

   * 進程名稱
   * 流程建立日期時間
   * 處理完成日期時間
   * 處理期間
   * 進程狀態
   * 進程啟動器

   **右上方面板：** 顯示組成所選程式之工作的下列詳細資料：

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

   **右上角面板：** 顯示組成所選任務的表單的下列詳細資訊：

   * 檔案ID
   * 表單建立日期時間
   * 表單更新日期時間
   * 表單範本Url

   **右下面板：** 顯示所選任務的進程歷史記錄的以下詳細資訊：

   * 任務分配類型
   * 任務所有者
   * 任務分配建立日期時間
   * 任務更新日期時間






1. 按一下&#x200B;**返回到進程/任務搜索**&#x200B;以返回從中細化進程/任務詳細資訊的搜索結果。

   ![back_to_search](assets/back_to_search.png)

   但是，如果通過輸入特定流程/任務ID找到了流程/任務詳細資訊，則按一下返回流程/任務搜索將返回&#x200B;**流程/任務搜索**，而不顯示任何搜索結果。

#### 通過在「流程/任務詳細資訊」面板{#by-entering-the-process-task-id-in-the-process-task-details-panel-br}中輸入流程/任務ID

1. 轉到&#x200B;**進程/任務詳細資訊**&#x200B;面板。

   ![details_nodes](assets/details_nodes.png)

1. 在「流程/任務ID」文本框中，輸入流程/任務ID。

   ![process_details-1](assets/process_details-1.png)

   **Process/Task Details**&#x200B;查詢結果中的欄位是AEM Forms進程/任務的特定欄位。

   對於流程，查詢結果將顯示流程中包含的任務的詳細資訊。

   對於任務，查詢結果將顯示任務中包含的表單的詳細資訊。
