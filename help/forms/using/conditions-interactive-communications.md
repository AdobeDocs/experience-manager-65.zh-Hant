---
title: 互動式通訊中的條件
seo-title: Conditions in Interactive Communications
description: 建立和編輯要在互動式通訊中使用的條件片段 — 條件是用來建立互動式通訊的四種檔案片段類型之一。 另外三個是文字、清單和版面片段。
seo-description: Creating and editing conditions to be used in Interactive Communications
uuid: c98f02d5-1769-46dd-ab35-6e8145a24939
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fe59d260-d392-4d6f-bb7e-2f2a1d701f51
docset: aem65
feature: Interactive Communication
exl-id: 0c0dc6a2-b889-4516-8e08-1e9d31be2cce
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# 互動式通訊中的條件{#conditions-in-interactive-communications}

建立和編輯要在互動式通訊中使用的條件片段 — 條件是用來建立互動式通訊的四種檔案片段類型之一。 另外三個是文字、清單和版面片段。

## 概觀 {#overview}

條件是可包含在互動式通訊中的檔案片段。 其他檔案片段為 [文字](../../forms/using/texts-interactive-communications.md)、清單和版面片段。 條件可讓您根據提供的資料和規則，定義包含在互動式通訊中的一或多個內容資產。

範例：

* 在信用卡對帳單中，根據客戶的信用卡類型顯示信用卡年費和信用卡影像。
* 在保險費到期提醒中，根據客戶州的稅顯示稅的計算。

根據套用的規則和傳遞至規則的值，呈現條件中的資產。 條件中的規則可檢查下列資料類型中的值：

* 關聯表單資料模型的屬性
* 您在條件中建立的任何變數
* 字串
* 數字
* 數學表達式
* 日期

## 建立條件 {#createcondition}

1. 選擇 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.
1. 選擇 **[!UICONTROL 建立]** > **[!UICONTROL 條件]**.
1. 指定下列資訊：

   * **[!UICONTROL 標題]**:（選用）輸入條件的標題。 標題不一定唯一，可以有特殊字元和非英文字元。 條件會以其標題（如果有）來參照，例如縮圖和屬性中。
   * **[!UICONTROL 名稱]**:資料夾內條件的唯一名稱。 任何狀態中都不能有兩個檔案片段（文字、條件或清單）在資料夾中以相同名稱存在。 在「名稱」欄位中，您只能輸入英文字元、數字和連字型大小。 系統會根據「標題」欄位自動填入「名稱」欄位。 在「標題」欄位中輸入的特殊字元、空格、數字和非英文字元在「名稱」欄位中會以連字型大小取代。 雖然「標題」欄位中的值會自動複製到「名稱」，但您可以編輯值。

   * **[!UICONTROL 說明]**:鍵入文檔片段的說明。
   * **[!UICONTROL 表單資料模型]**:（可選）選擇「表單資料模型」單選按鈕，以根據表單資料模型建立條件。 選擇「表單資料模型」單選按鈕時， **[!UICONTROL 表單資料模型]** 欄位。 瀏覽並選取表單資料模型。 為互動式通訊建立條件時，請確定您使用的資料模型與要用於互動式通訊的資料模型相同。 如需表單資料模型的詳細資訊，請參閱 [資料整合](../../forms/using/data-integration.md).

   * **[!UICONTROL 標籤]**:（可選）要建立自定義標籤，請在文本欄位中輸入值，然後點選Enter。 儲存此條件時，會建立新新增的標籤。

1. 點選 **[!UICONTROL 下一個]**.

   「建立條件」頁面。

   ![createcondition](assets/createcondition.png)

1. 點選 **[!UICONTROL 新增資產]**.

   選取資產頁面隨即顯示可用的文字、清單、條件和影像，這些可供新增至條件中。

   >[!NOTE]
   >
   >「選取資產」頁面中只會顯示無基礎、新建立的資產和FDM基礎的資產（使用與所建立條件相同的FDM建立）。

1. 點選適當的資產，以選取要包含在條件中的資產，然後點選 **[!UICONTROL 完成]**.

   「建立條件」頁面隨即顯示，並列出新增的資產。

   ![createconditionassetadd](assets/createconditionassetsadd.png)

   您可以使用下列選項來管理條件中的資產：

   ![createconditionscreenassetsaddedandon](assets/createconditionscreenassetsaddedannotated.png)

   **[A] 拒絕更改。** 點選此圖示以拒絕您對資產和條件中的規則所做的變更。
   **[B] 接受更改。** 點選此圖示以接受您在資產中所做的變更，並在條件中使用規則。
   **[C] 複製資產。** 點選此圖示即可在條件中建立資產副本以及套用的規則（如果有）。 接著，您可以繼續編輯重複資產的規則和資產。 複製資產對於建立類似規則以根據特定內容顯示替代資產很實用。
   **[D] 顯示預覽。** 點選此圖示即可在「建立\編輯條件」頁面內顯示資產的預覽。
   **「server」重新排序。** 點選並按住此圖示以拖放資產，以在條件中重新排序資產。

   您可以選取下列選項，以指定條件在執行階段的行為：

   * **禁用多個結果評估\啟用多個結果評估**:啟用此選項時（顯示為「已啟用多個結果評估」），將評估所有規則，結果是所有真規則的總和。 如果禁用此選項（顯示為「已禁用多個結果評估」），則僅評估發現為true的第一個規則，並成為條件的輸出。

   * **分頁符**:選取此選項( ![分隔](assets/break.png))，在條件的資產之間新增分頁符。 未選取此選項時( ![nobreak](assets/nobreak.png))，如果條件溢出至列印輸出中的下一頁，則整個條件會移至下一頁，而非中斷條件中資產之間的頁面。

1. 點選 **[!UICONTROL 建立規則]** 新增規則以顯示或隱藏資產（視需要）。 若要在規則中使用變數，請參閱 [建立變數](#variables). 如需詳細資訊，請參閱 [將規則新增至條件](#ruleeditor).

   建立的規則會出現在「建立條件」畫面的「規則」欄中。

   ![createconditionscreenrulesadded](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >您可以在已套用規則或重複套用的條件中插入資產。

1. 點選 **[!UICONTROL 儲存]**.

   條件隨即建立。 現在，您可以在建立互動式通訊時，繼續將條件當作建置區塊。

   >[!NOTE]
   >
   >若要儲存新或已編輯的條件，條件中每個新增的資產必須至少有一個規則。

## 編輯條件 {#edit-a-condition}

您可以使用下列步驟來編輯條件。 您也可以選取彈出式功能表中的「編輯片段」 ，從互動式通訊中選擇編輯條件。

1. 選擇 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.
1. 導覽至條件並選取它。
1. 點選 **[!UICONTROL 編輯]**.
1. 在條件中進行必要的變更。 如需可在條件中變更之資訊的詳細資訊，請參閱 [建立條件](#createcondition).
1. 點選 **[!UICONTROL 儲存]** 然後點選 **[!UICONTROL 關閉]**.

## 在條件中建立規則 {#ruleeditor}

您可以在條件中使用規則編輯器，建立規則以根據 **預設條件**. 這些條件可以根據：

* 字串
* 數字
* 數學表達式
* 日期
* 關聯表單資料模型的屬性
* 任何 [變數](#variables) 您可能建立的

### 在條件中建立規則 {#create-rule-in-condition}

1. 建立或編輯條件時，點選 ![規則編輯器圖示](assets/ruleeditoricon.png) （規則編輯器）圖示。

   將出現「建立規則」對話框。 除了字串、數字、數學運算式和日期之外，規則編輯器中也提供下列項目，用於建立規則的陳述式：

   * 關聯表單資料模型的屬性
   * 任何 [變數](#variables) 你可能已經建立的。

   ![createrledialog](assets/createruledialog.png)

   選擇要評估的適當選項。

   >[!NOTE]
   >
   >建立顯示資產的規則不支援集合屬性。

1. 選取適當的運算子以評估規則，例如「等於」、「包含」和「開頭為」。
1. 插入評估表達式、字串、資料模型屬性、變數或日期。

   ![在策略類型為標準時顯示資產的規則](assets/ruleincondition.png)

   在策略類型為標準時顯示資產的規則

   * 在建立或編輯規則時，您也可以點選 ![icon_resize](assets/icon_resize.png) （調整大小）以展開「建立規則/編輯規則」對話方塊。 展開的全視窗對話方塊可讓您建立 [變數](#variables) 來構建規則。 再次點選「調整大小」，返回一般的「建立規則」對話方塊。

   * 您也可以在規則中建立多個條件。

1. 點選 **[!UICONTROL 完成]**.

   規則會套用至資產。

## 在條件中建立和使用變數 {#variables}

在條件中建立或編輯規則時，您可以點選 ![icon_resize](assets/icon_resize.png) （調整大小）以展開「建立規則\編輯規則」對話框。 展開的全視窗對話方塊可讓您：

* 在規則中建立和使用變數
* 在規則中拖放表單資料模型的屬性和變數

再次點選「調整大小」，返回「建立規則\編輯規則」對話方塊。

### 建立變數 {#create-variables}

1. 在條件中建立或編輯規則時，您可以點選 ![icon_resize](assets/icon_resize.png) （調整大小）以展開「建立規則\編輯規則」對話框。

   將出現「展開的、全窗口」對話框。

   ![expandeditruledialog](assets/expandededitruledialog.png)

1. 在左窗格中，點選 **[!UICONTROL 變數]**.

   「變數」窗格隨即出現。

   ![expandeditrulevariables](assets/expandededitrulevariables.png)

1. 點選 **[!UICONTROL 建立]**.

   「建立變數」窗格隨即出現。

1. 輸入下列資訊並點選 **[!UICONTROL 建立]**:

   * **[!UICONTROL 名稱]**:變數的名稱。
   * **[!UICONTROL 說明]**:（可選）輸入有關變數的說明。
   * **[!UICONTROL 類型]**:選取變數類型：字串、數字、布林或日期。
   * **[!UICONTROL 僅允許特定值]**:對於字串和數字變數，您可以確保代理從特定值集中為代理UI中的預留位置進行選擇。 若要指定值集，請選取此選項，然後指定 **[!UICONTROL 值]** 欄位。

1. 點選 **[!UICONTROL 建立]**.

   變數會建立並列在「變數」窗格中。

1. 若要在規則中插入變數，請將變數拖放至規則中選項的預留位置。
1. 建立有效規則後，點選 **[!UICONTROL 完成]**.

   視需要，繼續在條件中進行進一步變更並儲存。
