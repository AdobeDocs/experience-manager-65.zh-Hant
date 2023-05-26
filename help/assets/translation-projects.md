---
title: 建立翻譯專案
description: 瞭解如何在中建立翻譯專案 [!DNL Adobe Experience Manager].
contentOwner: AG
role: Architect, Admin
feature: Translation
exl-id: 8990feca-cfda-4974-915e-27aa9d8f2ee1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 17%

---

# 建立翻譯專案 {#creating-translation-projects}

若要建立語言副本，請觸發下列「參考」邊欄下可用的語言副本工作流程之一： [!DNL Experience Manager] 使用者介面。

* **建立並翻譯**：在此工作流程中，要翻譯的資產會複製到您要翻譯之語言的語言根目錄。 此外，系統會根據您選擇的選項，在「專案」主控台中建立資產的翻譯專案。 根據設定，翻譯專案可以手動啟動，或允許在建立翻譯專案後立即自動執行。

* **更新語言副本**：執行此工作流程可翻譯其他資產群組，並將其納入特定地區設定的語言副本中。 在此情況下，已翻譯的資產會新增至已包含先前已翻譯資產的目標資料夾。

>[!PREREQUISITES]
>
>* 建立翻譯專案的使用者是群組的成員 `projects-administrators`.
>* 翻譯服務提供者支援二進位檔的翻譯。


## 建立及翻譯工作流程 {#create-and-translate-workflow}

您可使用建立及翻譯工作流程，首次產生特定語言的語言副本。 工作流程提供下列選項：

* 僅建立結構.
* 建立新的翻譯專案.
* 新增至現有翻譯專案.

### 僅建立結構 {#create-structure-only}

使用「 **[!UICONTROL 僅建立結構]** 」選項，在目標語言根目錄中建立目標資料夾層次結構，以匹配源語言根目錄中源資料夾的層次結構。在這種情況下，來源資產會複製到目標資料夾。但是，不會生成任何翻譯項目。

1. 在 [!DNL Assets] 介面中，選取您要在目標語言根目錄中建立結構的來源資料夾。

1. 開啟 **[!UICONTROL 引用]** 窗格並按一下 **[!UICONTROL 語言副本]** 在 **[!UICONTROL 份數]**.

   ![語言副本](assets/translation-language-copies.png)

1. 按一下 **[!UICONTROL 建立並翻譯]**. 從 **[!UICONTROL 目標語言]** 清單中，選取您要建立資料夾結構的語言。

1. 從「專 **[!UICONTROL 案]** 」清單中，選 **[!UICONTROL 擇「僅建立結構」]**。

1. 按一下&#x200B;**[!UICONTROL 建立]**。目標語言的新結構會列在 **[!UICONTROL 語言副本]**.

   ![語言副本](assets/lang-copy2.png)

1. 按一下清單中的結構，然後按一下 **[!UICONTROL 在資產中顯示]** 導覽至目標語言中的資料夾結構。

   ![reveal-in-assets](assets/reveal-in-assets.png)

### 建立新的翻譯專案 {#create-a-new-translation-project}

如果您使用此選項，要翻譯的資產會複製到您要翻譯之語言的語言根目錄中。 系統會根據您選擇的選項，在「專案」主控台中建立資產的翻譯專案。 根據設定，翻譯專案可以手動啟動，或在建立翻譯專案後立即自動執行。

1. 在 [!DNL Assets] 使用者介面，選取您要建立語言副本的來源資料夾。
1. 開啟 **[!UICONTROL 引用]** 窗格並按一下 **[!UICONTROL 語言副本]** 在 **[!UICONTROL 份數]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. 按一下 **[!UICONTROL 建立並翻譯]** 在底部。

1. 從「目 **[!UICONTROL 標語言]** 」清單中，選取您要建立檔案夾結構的語言。

1. 從 **[!UICONTROL 專案]** 清單，選取 **[!UICONTROL 建立新的翻譯專案]**.

1. 在「專 **[!UICONTROL 案標題]** 」欄位中，輸入專案標題。

1. 按一下&#x200B;**[!UICONTROL 建立]**。[!DNL Assets] 從來源資料夾複製到您在步驟4中所選地區設定的目標資料夾。

   ![語言副本](assets/lang-copy2.png)

1. 若要導覽至資料夾，請選取語言副本，然後按一下 **[!UICONTROL 在資產中顯示]**.

   ![reveal-in-assets](assets/reveal-in-assets.png)

1. 導覽至「專案」主控台。 翻譯資料夾會複製到專案主控台。

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. 開啟資料夾以檢視翻譯專案。

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. 按一下專案以開啟詳細資訊頁面。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 若要檢視翻譯工作的狀態，請按一下 **[!UICONTROL 翻譯工作]** 圖磚。

   ![chlimage_1-73](assets/chlimage_1-73.png)

   如需有關工作狀態的詳細資訊，請參閱 [監控翻譯工作的狀態](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. 導覽至 [!DNL Assets] 使用者介面，並開啟 [!UICONTROL 屬性] 每個已翻譯資產的頁面，用於檢視已翻譯的中繼資料。

   ![在資產屬性頁面中檢視翻譯的中繼資料](assets/translated-metadata-asset-properties.png)

   *圖：資產屬性頁面中的翻譯後中繼資料。*

   >[!NOTE]
   >
   >資產和資料夾皆可使用此功能。 選取資產而非資料夾時，會複製至語言根目錄為止的資料夾整個階層，以建立資產的語言副本。

### 新增至現有翻譯專案 {#add-to-existing-translation-project}

如果您使用此選項，則會在執行先前的翻譯工作流程後，為您新增至來源資料夾的資產執行翻譯工作流程。 只有新新增的資產會複製到包含先前翻譯的資產的目標資料夾。 在此情況下不會建立新的翻譯專案。

1. 在 [!DNL Assets] 在UI中，導覽至包含未翻譯資產的來源資料夾。
1. 選取您要轉換的資產，並開啟「參考」 **[!UICONTROL 窗格]**。「語 **[!UICONTROL 言副本]** 」部分顯示當前可用的翻譯副本數。
1. 按一下 **[!UICONTROL 語言副本]** 在 **[!UICONTROL 份數]**. 將顯示可用翻譯副本的清單。
1. 按一下 **[!UICONTROL 建立並翻譯]** 在底部。

1. 從「目 **[!UICONTROL 標語言]** 」清單中，選取您要建立檔案夾結構的語言。

1. 從「項 **[!UICONTROL 目]** 」清單中，選擇「 **[!UICONTROL 添加到現有翻譯項目」]** ，以在資料夾中運行翻譯工作流。

   >[!NOTE]
   >
   >如果您選擇 **[!UICONTROL 新增至現有翻譯專案]** 選項，則僅當您的專案設定完全符合預先存在的專案的設定時，才會將翻譯專案新增至預先存在的專案。 否則，會建立新專案。

1. 從 **[!UICONTROL 現有翻譯專案]** 清單中，選取要新增資產以進行翻譯的專案。

1. 按一下&#x200B;**[!UICONTROL 建立]**。要翻譯的資產會新增至目標資料夾。更新的資料夾會列在「語言復 **[!UICONTROL 本」區段下]** 。

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. 導覽至「專案」主控台，並開啟您新增的現有翻譯專案。
1. 按一下翻譯專案，即可檢視專案詳細資訊頁面。

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 按一下底部的省略符號 **翻譯工作** 並排顯示，以在翻譯工作流程中檢視資產。 翻譯工作清單也會顯示資產中繼資料和標記項目。這些項目表示資產中繼資料和標記也已翻譯。

   >[!NOTE]
   >
   >如果您刪除標籤或中繼資料的專案，則不會為任何資產翻譯標籤或中繼資料。

   >[!NOTE]
   >
   >如果您新增至翻譯工作的資產包含子資產，請選取子資產並移除它們，翻譯才能順利進行。

1. 若要開始資產的翻譯，請按一下 **[!UICONTROL 翻譯工作]** 並選取 **[!UICONTROL 開始]** 從清單中。

   ![chlimage_1-81](assets/chlimage_1-81.png)

   訊息會通知翻譯工作已開始。

1. 若要檢視翻譯工作的狀態，請按一下 **[!UICONTROL 翻譯工作]** 圖磚。

   ![chlimage_1-83](assets/chlimage_1-83.png)

   如需詳細資訊，請參閱 [監控翻譯工作的狀態](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. 翻譯完成後，狀態會變更為「準備好檢閱」。 導覽至 [!DNL Assets] 使用者介面，並開啟每個已翻譯資產的「屬性」頁面，以檢視已翻譯的中繼資料。

## 更新語言副本 {#update-language-copies}

執行此工作流程可翻譯任何其他資產集，並將其納入特定地區設定的語言副本中。 在此情況下，已翻譯的資產會新增至已包含先前已翻譯資產的目標資料夾。 根據選項選擇，會建立翻譯專案或更新新資產的現有翻譯專案。 更新語言副本工作流程包含以下選項：

* 建立新的翻譯專案
* 新增至現有翻譯專案

### 建立新的翻譯專案 {#create-a-new-translation-project-1}

如果您使用此選項，將會為您要更新語言副本的資產集建立翻譯專案。

1. 從 [!DNL Assets] UI中，選取您新增資產的來源資料夾。
1. 開啟 **[!UICONTROL 引用]** 窗格，然後按一下 **[!UICONTROL 語言副本]** 在 **[!UICONTROL 份數]** 以顯示語言副本清單。
1. 選中「語言副本」 **[!UICONTROL 之前的複選框]**，然後選擇與相應地區對應的目標資料夾。

   ![選取語言副本](assets/lang-copy1.png)

1. 按一下 **[!UICONTROL 更新語言副本]** 在底部。

1. 從 **[!UICONTROL 專案]** 清單，選擇 **[!UICONTROL 建立新的翻譯專案]**.

1. 在「專 **[!UICONTROL 案標題]** 」欄位中，輸入專案標題。

1. 按一下 **[!UICONTROL 開始]**.
1. 導覽至「專案」主控台。 翻譯資料夾會複製到專案主控台。

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 開啟資料夾以檢視翻譯專案。

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. 按一下專案以開啟詳細資訊頁面。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 若要開始資產的翻譯，請按一下 **[!UICONTROL 翻譯工作]** 並選取 **[!UICONTROL 開始]** 從清單中。

   ![chlimage_1-91](assets/chlimage_1-91.png)

   訊息會通知翻譯工作已開始。

1. 若要檢視翻譯工作的狀態，請按一下 **[!UICONTROL 翻譯工作]** 圖磚。

   ![chlimage_1-93](assets/chlimage_1-93.png)

   如需有關工作狀態的詳細資訊，請參閱 [監控翻譯工作的狀態](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. 導覽至 [!DNL Assets] 使用者介面，並開啟每個已翻譯資產的「屬性」頁面，以檢視已翻譯的中繼資料。

### 新增至現有翻譯專案 {#add-to-existing-translation-project-1}

如果您使用此選項，資產集會新增至現有的翻譯專案，以更新您選擇之地區設定的語言副本。

1. 從 [!DNL Assets] 在UI中，選取您新增資產資料夾的來源資料夾。
1. 開啟 **[!UICONTROL 引用窗格]**，然後按一下 **[!UICONTROL 語言副本]** 在 **[!UICONTROL 份數]** 以顯示語言副本清單。

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 在「語言副本」之前選 **[!UICONTROL 取核取方塊]**，以選取所有語言副本。取消選擇與要翻譯的語言環境相對應的語言副本 (副本) 以外的其他副本。

   ![選取語言副本](assets/lang-copy1.png)

1. 按一下 **[!UICONTROL 更新語言副本]** 在底部。

1. 從 **[!UICONTROL 專案]** 清單，選擇 **[!UICONTROL 新增至現有翻譯專案]**.

1. 從 **[!UICONTROL 現有翻譯專案]** 清單中，選取要新增資產以進行翻譯的專案。

1. 按一下 **[!UICONTROL 開始]**.
1. 請參閱步驟9-14 / [新增至現有翻譯專案](translation-projects.md#add-to-existing-translation-project) 以完成其餘程式。

## 建立暫存語言副本 {#creating-temporary-language-copies}

當您執行翻譯工作流程，以使用原始資產的編輯版本更新語言副本時，現有的語言副本會保留，直到您核准翻譯的資產為止。 [!DNL Adobe Experience Manager Assets] 會將新翻譯的資產儲存在暫存位置，並在您明確核准資產後更新現有的語言副本。 如果您拒絕資產，則語言副本保持不變。

1. 按一下下的來源根資料夾 **[!UICONTROL 語言副本]** 已為其建立語言副本，然後按一下 **[!UICONTROL 在資產中顯示]** 以開啟資料夾 [!DNL Experience Manager Assets].

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. 從 [!DNL Assets] 介面，選取您已翻譯的資產並按一下 **[!UICONTROL 編輯]** ，以在編輯模式下開啟資產。
1. 編輯資產，然後儲存變更。
1. 執行步驟2-14 [新增至現有翻譯專案](#add-to-existing-translation-project) 更新語言副本的程式。
1. 按一下底部的省略符號 **[!UICONTROL 翻譯工作]** 圖磚。 從「 」中的資產清單 **[!UICONTROL 翻譯工作]** 頁面，您可以清楚檢視儲存資產翻譯版本的暫時位置。

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. 選取旁邊的核取方塊 **[!UICONTROL 標題]**.
1. 在工具列中按一下 **[!UICONTROL 接受翻譯]** ![接受翻譯](assets/do-not-localize/thumb-up.png) 然後按一下 **[!UICONTROL Accept]** ，以使用已編輯資產的翻譯版本覆寫目標資料夾中的翻譯資產。

   >[!NOTE]
   >
   >若要啟用翻譯工作流程以更新目標資產，請接受資產和中繼資料。

   按一下 **[!UICONTROL 拒絕翻譯]** ![拒絕翻譯](assets/do-not-localize/thumb-down.png) 保留目標地區設定根目錄中資產的原始翻譯版本，並拒絕編輯的版本。

1. 若要檢視翻譯的中繼資料，請導覽至 [!DNL Assets] 主控台並開啟 [!UICONTROL 屬性] 每個已翻譯資產的頁面。

## 提示和限制 {#tips-limitations}

* 如果您啟動複雜資產的翻譯工作流程，例如PDF和 [!DNL Adobe InDesign] 不會提交檔案、其子資產或轉譯（若有）以供翻譯。
* 如果您使用機器翻譯，資產二進位檔將不會翻譯。
