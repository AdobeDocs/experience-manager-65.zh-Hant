---
title: 互動式通訊的條件
description: 建立和編輯用於互動式通訊的條件片段 — 條件是用於建立互動式通訊的四種檔案片段型別之一。 其他三個是文字、清單和佈局片段。
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 0c0dc6a2-b889-4516-8e08-1e9d31be2cce
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 1%

---

# 互動式通訊的條件{#conditions-in-interactive-communications}

建立和編輯用於互動式通訊的條件片段 — 條件是用於建立互動式通訊的四種檔案片段型別之一。 其他三個是文字、清單和佈局片段。

## 概觀 {#overview}

條件是可包含在互動式通訊中的檔案片段。 其他檔案片段為[文字](../../forms/using/texts-interactive-communications.md)、清單和佈局片段。 條件可讓您定義一或多個內容資產，這些資產會根據提供的資料和規則包含在互動式通訊中。

範例：

* 在信用卡對帳單中，根據客戶的信用卡型別，顯示信用卡年費和信用卡影像。
* 在保險費到期提醒中，顯示根據客戶州稅的稅捐計算。

條件中的資產，會根據套用的規則和傳遞至規則的值轉譯。 條件中的規則可檢查下列資料型別的值：

* 關聯的表單資料模型屬性
* 您在條件中建立的任何變數
* 字串
* 數字
* 數學運算式
* 日期

## 建立條件 {#createcondition}

1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**。
1. 選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 條件]**。
1. 指定下列資訊：

   * **[!UICONTROL 標題]**： （選擇性）輸入條件的標題。 標題不需要是唯一的，而且可以有特殊字元和非英文字元。 條件會透過其標題（可用時）參照，例如在縮圖和屬性中。
   * **[!UICONTROL 名稱]**：資料夾中條件的唯一名稱。 資料夾中不能存在任何狀態下具有相同名稱的兩個檔案片段（文字、條件或清單）。 在「名稱」欄位中，您只能輸入英文字元、數字和連字型大小。 「名稱」欄位會根據「標題」欄位自動填入。 在「標題」欄位中輸入的特殊字元、空格、數字和非英文字元，會由「名稱」欄位中的連字型大小取代。 雖然「標題」欄位中的值會自動複製到「名稱」，但您可以編輯值。

   * **[!UICONTROL 描述]**：輸入檔案片段的描述。
   * **[!UICONTROL 表單資料模型]**：選擇性地選取[表單資料模型]選項按鈕，以根據表單資料模型建立條件。 當您選取[表單資料模型]選項按鈕時，會出現&#x200B;**[!UICONTROL 表單資料模型]**&#x200B;欄位。 瀏覽並選取表單資料模型。 建立互動式通訊的條件時，請確定您使用與互動式通訊相同的資料模型。 如需表單資料模型的詳細資訊，請參閱[資料整合](../../forms/using/data-integration.md)。

   * **[!UICONTROL 標籤]**：若要建立自訂標籤，可選擇在文字欄位中輸入值，然後選取[輸入]。 儲存此條件時，會建立新新增的標籤。

1. 選取&#x200B;**[!UICONTROL 「下一步」]**。

   便會顯示「建立條件」頁面。

   ![createcondition](assets/createcondition.png)

1. 選取&#x200B;**[!UICONTROL 新增Assets]**。

   選取Assets頁面隨即顯示，並顯示可在條件中新增的可用文字、清單、條件和影像。

   >[!NOTE]
   >
   >「選取Assets」頁面中只會顯示沒有依據、新建立的資產，以及（以與正在建立的條件相同的FDM建立的）以FDM為基礎的資產。

1. 選取適當的資產，以選取要包含在條件中的資產，然後選取&#x200B;**[!UICONTROL 完成]**。

   「建立條件」頁面便會出現，並列出新增的資產。

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   您可以使用以下選項來管理條件中的資產：

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[A]拒絕變更。**&#x200B;選取此圖示以拒絕您對條件中的資產和規則可能進行的變更。
   **[B]接受變更。**&#x200B;選取此圖示以接受您在條件中的資產和規則中所做的變更。
   **[C]重複資產。**&#x200B;選取此圖示以建立資產復本以及在條件中套用的規則（如果有的話）。 接著，您可以繼續編輯重複資產的規則和資產。 複製資產有助於建立類似規則，以根據特定內容顯示替代資產。
   **[D]節目預覽。**&#x200B;選取此圖示以在「建立\編輯條件」頁面中顯示資產的預覽。
   **&#39;server&#39;重新排序。**&#x200B;選取並按住此圖示以拖放資產，在條件中重新排序。

   您可以選取下列選項，指定條件在執行階段的行為：

   * **已停用多重結果評估\已啟用多重結果評估**：啟用此選項時（顯示為「已啟用多重結果評估」），會評估所有規則，結果為所有True規則的總和。 如果停用此選項（顯示為「已停用多項結果評估」），則只會評估發現為true的第一個規則，並成為條件的輸出。

   * **分頁符號**：選取此選項（![分頁符號](assets/break.png)）可在條件的資產之間新增分頁符號。 未選取此選項( ![nobreak](assets/nobreak.png))時，如果條件溢位至列印輸出的下一頁，則整個條件會移至下一頁，而不是在條件中資產之間的頁面中中斷。

1. 選取&#x200B;**[!UICONTROL 建立規則]**，視需要新增顯示或隱藏資產的規則。 若要在規則中使用變數，請參閱[建立變數](#variables)。 如需詳細資訊，請參閱[將規則新增至條件](#ruleeditor)。

   建立的規則會顯示在「建立條件」畫面的「規則」欄中。

   ![createconditionscreenrulesadded](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >您可以在已套用規則或重複專案的條件中插入資產。

1. 選取「**[!UICONTROL 儲存]**」。

   條件已建立。 現在當您建立互動式通訊時，可以繼續使用條件作為建置區塊。

   >[!NOTE]
   >
   >若要儲存新或編輯的條件，條件中新增的每個資產都必須至少有一個規則。

## 編輯條件 {#edit-a-condition}

您可以使用下列步驟編輯條件。 您也可以選取彈出式選單中的「編輯片段」，從互動式通訊中編輯條件。

1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**。
1. 導覽至條件並加以選取。
1. 選取&#x200B;**[!UICONTROL 編輯]**。
1. 在條件中進行所需的變更。 如需可在條件中變更之資訊的詳細資訊，請參閱[建立條件](#createcondition)。
1. 選取&#x200B;**[!UICONTROL 儲存]**，然後選取&#x200B;**[!UICONTROL 關閉]**。

## 在條件中建立規則 {#ruleeditor}

在條件中使用規則編輯器，您可以建立規則以根據&#x200B;**預設條件**&#x200B;顯示或隱藏資產。 這些條件可建構於：

* 字串
* 數字
* 數學運算式
* 日期
* 關聯的表單資料模型屬性
* 您可能已建立的任何[變數](#variables)

### 在條件中建立規則 {#create-rule-in-condition}

1. 在建立或編輯條件時，請選取相關資產的![ruleeditoricon](assets/ruleeditoricon.png) （規則編輯器）圖示。

   「建立規則」對話方塊隨即顯示。 除了字串、數字、數學運算式和日期之外，規則編輯器中也提供下列專案來建立規則的陳述式：

   * 關聯的表單資料模型屬性
   * 您可能已建立的任何[變數](#variables)。

   ![createruledialog](assets/createruledialog.png)

   選取要評估的適當選項。

   >[!NOTE]
   >
   >集合屬性不支援建立顯示資產的規則。

1. 選取適當的運運算元以評估規則，例如「等於」、「包含」和「開頭為」。
1. 插入評估運算式、字串、資料模型屬性、變數或日期。

   ![當原則型別為標準時顯示資產的規則](assets/ruleincondition.png)

   原則型別為標準時顯示資產的規則

   * 在建立或編輯規則時，您也可以選取![icon_resize](assets/icon_resize.png) （調整大小）以展開「建立規則/編輯規則」對話方塊。 展開的完整視窗對話方塊可讓您建立[變數](#variables)來建構規則。 再次選取調整大小以返回一般的建立規則對話方塊。

   * 您也可以在規則中建立多個條件。

1. 選取「**[!UICONTROL 完成]**」。

   該規則將套用至資產。

## 在條件中建立和使用變數 {#variables}

在條件中建立或編輯規則時，您可以選取![icon_resize](assets/icon_resize.png) （調整大小）以展開「建立規則\編輯規則」對話方塊。 展開的完整視窗對話方塊可讓您：

* 在規則中建立和使用變數
* 在規則中拖放表單資料模型的屬性和變數

再次選取調整大小以返回「建立規則\編輯規則」對話方塊。

### 建立變數 {#create-variables}

1. 在條件中建立或編輯規則時，您可以選取![icon_resize](assets/icon_resize.png) （調整大小）以展開「建立規則\編輯規則」對話方塊。

   「已展開，全視窗」對話方塊隨即顯示。

   ![expandeditruledialog](assets/expandededitruledialog.png)

1. 在左窗格中，選取&#x200B;**[!UICONTROL 變數]**。

   「變數」窗格隨即顯示。

   ![expandeditrulevariables](assets/expandededitrulevariables.png)

1. 選取「**[!UICONTROL 建立]**」。

   「建立變數」窗格隨即顯示。

1. 輸入下列資訊並選取&#x200B;**[!UICONTROL 建立]**：

   * **[!UICONTROL 名稱]**：變數的名稱。
   * **[!UICONTROL 描述]**：可選擇輸入變數的描述。
   * **[!UICONTROL 型別]**：選取變數的型別：字串、數字、布林值或日期。
   * **[!UICONTROL 僅允許特定值]**：對於String和Number變數，您可以確保代理程式從代理程式UI中預留位置的特定值集合中進行選擇。 若要指定一組值，請選取此選項，然後指定允許在&#x200B;**[!UICONTROL 值]**&#x200B;欄位中使用逗號分隔的值。

1. 選取「**[!UICONTROL 建立]**」。

   變數隨即建立並列於「變數」窗格中。

1. 若要在規則中插入變數，請將變數拖放至規則中某個選項的預留位置。
1. 在您建構有效的規則之後，請選取&#x200B;**[!UICONTROL 完成]**。

   如有必要，請繼續在條件中進行進一步變更並儲存。
