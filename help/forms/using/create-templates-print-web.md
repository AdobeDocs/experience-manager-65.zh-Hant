---
title: 教學課程：建立範本
description: 建立互動式通訊的列印和Web範本
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 1%

---

# 教學課程：建立範本{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

此教學課程是[建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md)系列中的步驟。 建議您依照時間順序來瞭解、執行和示範完整的教學課程使用案例。

若要建立互動式通訊，您必須在AEM伺服器上為「列印」和「Web管道」提供範本。

列印管道的範本是在AdobeForms Designer中建立並上傳至AEM伺服器。 然後，這些範本便可在建立互動式通訊時使用。

Web channel的範本是在AEM中建立。 範本作者和管理員可以建立、編輯及啟用網頁範本。 建立並啟用後，這些範本便可在建立互動式通訊時使用。

本教學課程將逐步帶您瞭解如何建立列印和Web管道範本，以便您在建立互動式通訊時使用這些範本。 在本教學課程結束時，您將能夠：

* 使用AdobeForms Designer為列印頻道建立XDP範本
* 將XDP範本上傳至AEM Forms伺服器
* 建立和啟用網頁管道的範本

## 為列印管道建立範本 {#create-template-for-print-channel}

使用下列工作建立並管理互動式通訊列印頻道的範本：

* [使用Forms Designer建立XDP範本](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [將XDP範本上傳至AEM Forms伺服器](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [為佈局片段建立XDP範本](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### 使用Forms Designer建立XDP範本 {#create-xdp-template-using-forms-designer}

根據[使用案例](/help/forms/using/create-your-first-interactive-communication.md)和[剖析](/help/forms/using/planning-interactive-communications.md)，在XDP範本中建立下列子表單：

* 帳單詳細資訊：包含檔案片段
* 客戶詳細資料：包含檔案片段
* 帳單摘要：包含檔案片段
* 摘要：包含檔案片段（費用子表單）和圖表（圖表子表單）
* 分項呼叫：包含表格（佈局片段）
* 立即付款：包含影像
* 增值服務：包含影像

![create_print_template](assets/create_print_template.gif)

將XDP檔案上傳至Forms伺服器後，這些子表單會在列印範本中顯示為目標區域。 建立互動式通訊時，所有實體（例如檔案片段、圖表、佈局片段和影像）都會新增到目標區域。

若要為列印管道建立XDP範本，請執行下列動作：

1. 開啟Forms Designer，選取&#x200B;**檔案** > **新增** > **使用空白表單，**&#x200B;選取&#x200B;**下一步**，然後選取&#x200B;**完成**&#x200B;以開啟範本建立表單。

   請確定已從&#x200B;**視窗**&#x200B;功能表選取&#x200B;**物件程式庫**&#x200B;和&#x200B;**物件**&#x200B;選項。

1. 將&#x200B;**Subform**&#x200B;元件從&#x200B;**物件庫**&#x200B;拖放至表單。
1. 選取子表單，以便在右窗格的&#x200B;**物件**&#x200B;視窗中檢視子表單的選項。
1. 選取「**子表單**」標籤，然後從「**內容**」下拉式清單中選取「**已流動**」。 若要調整長度，請拖曳子表單的左側端點。
1. 在&#x200B;**繫結**&#x200B;索引標籤中：

   1. 在&#x200B;**名稱**&#x200B;欄位中指定&#x200B;**帳單詳細資料**。

   1. 從&#x200B;**資料繫結**&#x200B;下拉式清單中選取&#x200B;**無資料繫結**。

   ![Designer子表單](assets/forms_designer_subform_new.png)

1. 同樣地，選取根子表單，選取&#x200B;**子表單**&#x200B;索引標籤，然後從&#x200B;**內容**&#x200B;下拉式清單中選取&#x200B;**流程**。 在&#x200B;**繫結**&#x200B;索引標籤中：

   1. 在&#x200B;**名稱**&#x200B;欄位中指定&#x200B;**TelecaBill**。

   1. 從&#x200B;**資料繫結**&#x200B;下拉式清單中選取&#x200B;**無資料繫結**。

   ![列印範本的子表單](assets/root_subform_print_template_new.png)

1. 重複步驟2至5以建立下列子表單：

   * 帳單詳細資訊
   * 客戶詳細資料
   * 帳單摘要
   * 摘要 — 選取&#x200B;**子表單**&#x200B;索引標籤，並從此子表單的&#x200B;**內容**&#x200B;下拉式清單中選取&#x200B;**定位**。 在&#x200B;**摘要**&#x200B;子表單中插入下列子表單。

      * 費用
      * 圖表

   * ItemisedCalls
   * Paynow
   * ValueAddedServices

   為了節省時間，您也可以複製並貼上現有的子表單，以建立其他子表單。

   若要將&#x200B;**Charts**&#x200B;子表單移至Charges子表單的右側，請從左窗格中選取&#x200B;**Charts**&#x200B;子表單，選取&#x200B;**配置**&#x200B;索引標籤，並指定&#x200B;**AnchorX**&#x200B;欄位的值。 值必須大於&#x200B;**Charges**&#x200B;子表單的&#x200B;**寬度**&#x200B;欄位值。 選取&#x200B;**Charges**&#x200B;子表單並選取&#x200B;**配置**&#x200B;標籤，以便您檢視&#x200B;**寬度**&#x200B;欄位的值。

1. 將&#x200B;**Text**&#x200B;物件從&#x200B;**物件庫**&#x200B;拖放至表單，並在方塊中輸入&#x200B;**撥號XXXX以訂閱**&#x200B;文字。
1. 在左窗格中的文字物件上按一下滑鼠右鍵，選取&#x200B;**重新命名物件**，然後輸入文字物件的名稱作為&#x200B;**訂閱**。

   ![XDP範本](assets/print_xdp_template_subform_new.png)

1. 選取&#x200B;**檔案** > **另存新檔**，將檔案儲存在本機檔案系統上：

   1. 瀏覽至可以儲存檔案的位置，並將名稱指定為&#x200B;**create_first_ic_print_template**。
   1. 從&#x200B;**另存為型別**&#x200B;下拉式清單中選取&#x200B;**.xdp**。

   1. 選取「**儲存**」。

### 將XDP範本上傳至AEM Forms伺服器 {#upload-xdp-template-to-the-aem-forms-server}

使用Forms Designer建立XDP範本後，您必須將其上傳到AEM Forms伺服器，以便該範本可在建立互動式通訊時使用。

1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 選取&#x200B;**建立** > **檔案上傳**。

   瀏覽並選取&#x200B;**create_first_ic_print_template**&#x200B;範本(XDP)，然後選取&#x200B;**開啟**&#x200B;將XDP範本匯入至AEM Forms伺服器。

### 為佈局片段建立XDP範本 {#create-xdp-template-for-layout-fragments}

若要為互動式通訊的列印管道建立佈局片段，請使用Forms Designer建立XDP並將其上傳到AEM Forms伺服器。

1. 開啟Forms Designer，選取&#x200B;**檔案** > **新增** > **使用空白表單，**&#x200B;選取&#x200B;**下一步**，然後選取&#x200B;**完成**&#x200B;以開啟範本建立表單。

   請確定已從&#x200B;**視窗**&#x200B;功能表選取&#x200B;**物件程式庫**&#x200B;和&#x200B;**物件**&#x200B;選項。

1. 將&#x200B;**Table**&#x200B;元件從&#x200B;**物件庫**&#x200B;拖放至表單。
1. 在「插入表格」對話方塊中：

   1. 指定資料行數目為&#x200B;**5**。
   1. 將本文列數指定為&#x200B;**1**。
   1. 選取&#x200B;**在資料表**&#x200B;中包含標題資料列核取方塊。
   1. 索引標籤&#x200B;**確定**。

1. 在&#x200B;**表格** 1旁的左窗格中選取&#x200B;**+**，然後按一下滑鼠右鍵&#x200B;**儲存格1**，並選取&#x200B;**將物件**&#x200B;重新命名為&#x200B;**日期**。

   同樣地，將&#x200B;**Cell2**、**Cell3**、**Cell4**&#x200B;和&#x200B;**Cell5**&#x200B;分別重新命名為&#x200B;**Time**、**Number**、**Duration**&#x200B;和&#x200B;**Charges**。

1. 按一下&#x200B;**Designer檢視**&#x200B;中的[標題]文字欄位，並將它們重新命名為&#x200B;**時間**、**數字**、**持續時間**&#x200B;和&#x200B;**費用**。

   ![佈局片段](assets/layout_fragment_print_new.png)

1. 從左窗格中選取&#x200B;**列1**，然後選取每個資料專案的&#x200B;**物件** > **繫結** > **重複列**。

   ![重複佈局片段的屬性](assets/layout_fragment_print_repeat_new.png)

1. 將&#x200B;**文字欄位**&#x200B;元件從&#x200B;**物件庫**&#x200B;拖放至&#x200B;**Designer檢視**。

   佈局片段的![文字欄位](assets/layout_fragment_print_text_field_new.png)

   同樣地，將&#x200B;**文字欄位**&#x200B;元件拖放至&#x200B;**時間**、**數字**、**持續時間**&#x200B;和&#x200B;**費用**&#x200B;列。

1. 選取&#x200B;**檔案** > **另存新檔**，將檔案儲存在本機檔案系統上：

   1. 瀏覽到可以儲存檔案的位置，並將名稱指定為&#x200B;**table_lf**。
   1. 從&#x200B;**另存為型別**&#x200B;下拉式清單中選取&#x200B;**.xdp**。

   1. 選取「**儲存**」。

   使用Forms Designer為版面片段建立XDP範本後，您必須[上傳](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)至AEM Forms伺服器，才能在建立版面片段時使用範本。

## 建立Web channel範本 {#create-template-for-web-channel}

使用下列工作建立並管理互動式通訊Web channel的範本：

* [建立範本的資料夾](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [建立範本](../../forms/using/create-templates-print-web.md#create-the-template)
* [啟用範本](../../forms/using/create-templates-print-web.md#enable-the-template)
* [啟用互動式通訊中的按鈕](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 建立範本的資料夾 {#create-folder-for-templates}

若要建立Web channel範本，請定義一個資料夾，您可在其中儲存建立的範本。 在該資料夾中建立範本後，請啟用範本以允許表單使用者根據範本建立互動式通訊的Web channel。

若要為可編輯的範本建立資料夾，請執行下列動作：

1. 選取&#x200B;**工具** ![槌子圖示](assets/hammer-icon.svg) > **設定瀏覽器**。
   * 如需詳細資訊，請參閱[設定瀏覽器](/help/sites-administering/configurations.md)檔案。
1. 在組態瀏覽器頁面中，選取&#x200B;**建立**。
1. 在&#x200B;**建立組態**&#x200B;對話方塊中，指定&#x200B;**Create_First_IC_templates**&#x200B;作為資料夾的標題，核取&#x200B;**可編輯的範本**，然後選取&#x200B;**建立**。

   ![設定Web範本](assets/create_first_ic_web_template_new.png)

   **Create_First_IC_templates**&#x200B;資料夾已建立並列於&#x200B;**組態瀏覽器**&#x200B;頁面。

### 建立範本 {#create-the-template}

根據[使用案例](/help/forms/using/create-your-first-interactive-communication.md)和[剖析](/help/forms/using/planning-interactive-communications.md)，在Web範本中建立下列面板：

* 帳單詳細資訊：包含檔案片段
* 客戶詳細資料：包含檔案片段
* 帳單摘要：包含檔案片段
* 費用摘要：包括檔案片段和圖表（兩欄式配置）
* 分項呼叫：包含表格
* 立即付款：包含&#x200B;**立即付款**&#x200B;按鈕與影像
* 增值服務：包含影像和&#x200B;**訂閱**&#x200B;按鈕。

![create_web_template](assets/create_web_template.gif)

建立互動式通訊時，會新增所有實體，例如檔案片段、圖表、表格、影像和按鈕。

若要在&#x200B;**Create_First_IC_templates**&#x200B;資料夾中建立Web channel的範本，請執行下列步驟：

1. 選取&#x200B;**Tools** > **Templates** > **Create_First_IC_templates**&#x200B;資料夾，以導覽至適當的範本資料夾。
1. 選取「**建立**」。
1. 在&#x200B;**挑選範本型別**&#x200B;設定精靈上，選取&#x200B;**互動式通訊 — Web Channel**&#x200B;並選取&#x200B;**下一步**。
1. 在&#x200B;**範本詳細資料**&#x200B;設定精靈中，指定&#x200B;**Create_First_IC_Web_Template**&#x200B;做為範本標題。 指定選擇性描述，並選取&#x200B;**建立**。

   顯示&#x200B;**Create_First_IC_Web_Template**&#x200B;的確認訊息。

1. 選取&#x200B;**開啟**&#x200B;以在範本編輯器中開啟範本。
1. 從&#x200B;**預覽**&#x200B;選項旁的下拉式清單中選取&#x200B;**初始內容**。

   ![範本編輯器](assets/template_editor_initial_content_new.png)

1. 選取「**根面板**」，然後選取「**+**」以檢視可新增至範本的元件清單。
1. 若要在&#x200B;**根面板**&#x200B;上方新增面板，請從清單中選取&#x200B;**面板**。
1. 在左窗格中選取&#x200B;**Content**&#x200B;標籤。 步驟8新增的新面板會顯示在內容樹狀結構的&#x200B;**根面板**&#x200B;下。

   ![內容樹](assets/content_tree_root_panel_new.png)

1. 選取面板，然後選取![configure_icon](assets/configure_icon.png) （設定）。
1. 在「屬性」窗格中：

   1. 在[名稱]欄位中指定&#x200B;**帳單詳細資料**。
   1. 在標題欄位中指定&#x200B;**帳單詳細資料**。
   1. 從&#x200B;**欄數**&#x200B;下拉式清單中選取&#x200B;**1**。

   1. 若要儲存屬性，請選取![儲存](/help/forms/using/assets/done_icon.png)。

   面板名稱在內容樹狀結構中更新為&#x200B;**帳單詳細資料**。

1. 重複步驟7至11，將具有以下屬性的面板新增至範本：

   | 名稱 | 標題 | 欄數 |
   |---|---|---|
   | customerdetails | 客戶詳細資料 | 1 |
   | 帳單摘要 | 帳單摘要 | 1 |
   | summarycharges | 費用摘要 | 2 |
   | itemisedcalls | 分項通話 | 1 |
   | paynow | 立即付款 | 2 |
   | vas | 增值服務 | 1 |

   下圖說明將所有面板新增至範本後的內容樹狀結構：

   所有面板的![內容樹狀結構](assets/content_tree_all_panels_new.png)

### 啟用範本 {#enable-the-template}

建立Web範本後，您必須啟用它，才能在建立互動式通訊時使用範本。

若要啟用Web範本，請執行下列動作：

1. 選取&#x200B;**工具** ![槌子圖示](assets/hammer-icon.svg) > **範本**。
1. 導覽至&#x200B;**Create_First_IC_Web_Template**&#x200B;範本，選取它，然後選取&#x200B;**啟用**。
1. 再次選取&#x200B;**啟用**&#x200B;以確認。

   範本已啟用，其狀態會顯示為「已啟用」。 建立Web channel的互動式通訊時，您可以使用此範本。

### 啟用互動式通訊中的按鈕 {#enabling-buttons-in-interactive-communications}

根據使用案例，您必須在互動式通訊中包含&#x200B;**立即付款**&#x200B;和&#x200B;**訂閱**&#x200B;按鈕（最適化表單元件）。 若要在互動式通訊中啟用這些按鈕，請執行下列動作：

1. 從&#x200B;**預覽**&#x200B;選項旁的下拉式清單中選取&#x200B;**結構**。
1. 使用內容樹狀結構選取&#x200B;**檔案容器**&#x200B;根面板，並選取&#x200B;**原則**&#x200B;以選取允許在互動式通訊中使用的元件。

   ![設定原則](assets/structure_configure_policy_new.png)

1. 在&#x200B;**屬性**&#x200B;區段的&#x200B;**允許的元件**&#x200B;標籤中，從&#x200B;**最適化表單**&#x200B;元件中選取&#x200B;**按鈕**。

   ![允許的元件](assets/allowed_components_af_new.png)

1. 若要儲存屬性，請選取![儲存](assets/done_icon.png)。
