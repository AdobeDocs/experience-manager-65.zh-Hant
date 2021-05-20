---
title: 「教學課程：建立範本」
seo-title: 建立用於互動式通信的打印和Web模板
description: 建立用於互動式通信的打印和Web模板
seo-description: 建立用於互動式通信的打印和Web模板
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
feature: 互動式通訊
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1814'
ht-degree: 0%

---

# 教學課程：建立模板{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

本教學課程是[建立第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md)系列中的步驟。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

若要建立互動式通訊，您必須在AEM伺服器上提供用於列印和網頁頻道的範本。

列印管道的範本是在AdobeForms Designer中建立，並上傳至AEM伺服器。 然後，這些模板便可在建立互動式通信時使用。

網頁管道的範本是在AEM中建立。 範本作者和管理員可以建立、編輯和啟用網頁範本。 建立並啟用後，這些範本便可在建立互動式通訊時使用。

本教學課程會逐步引導您完成建立列印和網頁頻道範本的步驟，以便在建立互動式通訊時使用。 在本教學課程結束時，您將能夠：

* 使用AdobeForms Designer為列印管道建立XDP範本
* 將XDP範本上傳至AEM Forms伺服器
* 建立和啟用Web通道的模板

## 建立打印通道的模板{#create-template-for-print-channel}

使用以下任務建立和管理互動式通信的打印通道模板：

* [使用Forms Designer建立XDP範本](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [上傳XDP範本至AEM Forms伺服器](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [為版面片段建立XDP範本](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### 使用Forms Designer {#create-xdp-template-using-forms-designer}建立XDP範本

根據[使用案例](/help/forms/using/create-your-first-interactive-communication.md)和[anatogy](/help/forms/using/planning-interactive-communications.md)，在XDP範本中建立下列子表單：

* 帳單詳細資訊：包含檔案片段
* 客戶詳細資訊：包含檔案片段
* 清單匯總：包含檔案片段
* 摘要：包括文檔片段（費用子表單）和圖表（圖表子表單）
* 逐項呼叫：包括表（佈局片段）
* 立即支付：包含影像
* 增值服務：包含影像

![create_print_template](assets/create_print_template.gif)

上傳XDP檔案至Forms伺服器後，這些子表單會在列印範本中顯示為目標區域。 建立互動式通訊時，所有實體（如檔案片段、圖表、版面片段和影像）都會新增至目標區域。

執行下列步驟為列印通道建立XDP範本：

1. 開啟Forms Designer，選擇「**檔案** > **新建** > **使用空白表單」，點選「**&#x200B;下一步」，然後點選「**完成」以開啟用於建立範本的表單。******

   確保從&#x200B;**Window**&#x200B;菜單中選擇了&#x200B;**Object Library**&#x200B;和&#x200B;**Object**&#x200B;選項。

1. 將&#x200B;**Subform**&#x200B;元件從&#x200B;**Object Library**&#x200B;拖放至表單。
1. 在右窗格的&#x200B;**Object**&#x200B;窗口中，選擇子表單以顯示子表單的選項。
1. 選擇&#x200B;**Subform**&#x200B;頁簽，然後從&#x200B;**Content**&#x200B;下拉清單中選擇&#x200B;**Fluged**。 拖動子表單的左端點以調整長度。
1. 在&#x200B;**綁定**&#x200B;頁簽中：

   1. 在&#x200B;**名稱**&#x200B;欄位中指定&#x200B;**BillDetails**。

   1. 從&#x200B;**資料綁定**&#x200B;下拉清單中選擇&#x200B;**無資料綁定**。

   ![設計器子表單](assets/forms_designer_subform_new.png)

1. 同樣地，選擇根子表單，選擇&#x200B;**子表單**&#x200B;頁簽，然後從&#x200B;**內容**&#x200B;下拉清單中選擇&#x200B;**流**。 在&#x200B;**綁定**&#x200B;頁簽中：

   1. 在&#x200B;**Name**&#x200B;欄位中指定&#x200B;**TelecaBill**。

   1. 從&#x200B;**資料綁定**&#x200B;下拉清單中選擇&#x200B;**無資料綁定**。

   ![打印模板的子表單](assets/root_subform_print_template_new.png)

1. 重複步驟2 - 5以建立下列子表單：

   * BillDetails
   * 客戶詳細資訊
   * BillSummary
   * 摘要 — 選擇&#x200B;**子表單**&#x200B;頁簽，然後從&#x200B;**內容**&#x200B;下拉清單中選擇&#x200B;**定位**。 在&#x200B;**Summary**&#x200B;子表單中插入以下子表單。

      * 費用
      * 圖表
   * ItemisedCalls
   * PayNow
   * ValueAddedServices

   為了節省時間，您也可以複製並貼上現有的子表單以建立新的子表單。

   要將&#x200B;**Charts**&#x200B;子表單移到Charges子表單的右側，請從左窗格中選擇&#x200B;**Charts**&#x200B;子表單，選擇&#x200B;**Layout**&#x200B;頁簽，並指定&#x200B;**AnchorX**&#x200B;欄位的值。 值必須大於&#x200B;**Charges**&#x200B;子表單的&#x200B;**Width**&#x200B;欄位的值。 選擇&#x200B;**Charges**&#x200B;子表單並選擇&#x200B;**Layout**&#x200B;頁簽以查看&#x200B;**Width**&#x200B;欄位的值。

1. 將&#x200B;**Text**&#x200B;對象從&#x200B;**Object Library**&#x200B;拖放到表單中，並在框中輸入&#x200B;**Dial XXXX以訂閱**&#x200B;文本。
1. 按一下右鍵左窗格中的文本對象，選擇&#x200B;**更名對象**，然後輸入文本對象的名稱，作為&#x200B;**訂閱**。

   ![XDP範本](assets/print_xdp_template_subform_new.png)

1. 選擇&#x200B;**File** > **Save As**&#x200B;以在本地檔案系統上保存檔案：

   1. 導覽至要儲存檔案的位置，並指定名稱為&#x200B;**create_first_ic_print_template**。
   1. 從&#x200B;**另存為類型**&#x200B;下拉清單中選擇&#x200B;**.xdp**。

   1. 點選&#x200B;**儲存**。

### 將XDP範本上傳至AEM Forms伺服器{#upload-xdp-template-to-the-aem-forms-server}

使用Forms Designer建立XDP範本後，必須將其上傳至AEM Forms伺服器，以便在建立互動式通訊時讓範本可供使用。

1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 點選「**建立** > **檔案上傳**」。

   導覽並選取&#x200B;**create_first_ic_print_template**&#x200B;範本(XDP)，然後點選&#x200B;**開啟**&#x200B;以將XDP範本匯入AEM Forms伺服器。

### 為版面片段{#create-xdp-template-for-layout-fragments}建立XDP範本

若要為互動式通訊的列印通道建立版面片段，請使用Forms Designer建立XDP，並將其上傳至AEM Forms伺服器。

1. 開啟Forms Designer，選擇「**檔案** > **新建** > **使用空白表單」，點選「**&#x200B;下一步」，然後點選「**完成」以開啟用於建立範本的表單。******

   確保從&#x200B;**Window**&#x200B;菜單中選擇了&#x200B;**Object Library**&#x200B;和&#x200B;**Object**&#x200B;選項。

1. 將&#x200B;**表**&#x200B;元件從&#x200B;**對象庫**&#x200B;拖放到表單中。
1. 在「插入表」(Insert Table)對話框中：

   1. 指定列數&#x200B;**5**。
   1. 將內文行數指定為&#x200B;**1**。
   1. 選中「在表&#x200B;**中包括標題行」複選框。**
   1. 頁簽&#x200B;**OK**。

1. 點選&#x200B;**+** ，在&#x200B;**表** 1旁的左窗格中，按一下右鍵&#x200B;**Cell1**&#x200B;並選擇&#x200B;**將對象**&#x200B;更名為&#x200B;**Date**。

   同樣，將&#x200B;**單元2**、**單元3**、**單元4**&#x200B;和&#x200B;**單元5**&#x200B;分別更名為&#x200B;**時間**、**數字**、**持續時間**&#x200B;和&#x200B;**費用**。

1. 按一下&#x200B;**設計器視圖**&#x200B;中的「標題」文本欄位，然後將其更名為&#x200B;**Time**、**Number**、**Duration**&#x200B;和&#x200B;**Charges**。

   ![版面片段](assets/layout_fragment_print_new.png)

1. 從左窗格中選擇&#x200B;**行1**，然後選擇&#x200B;**對象** > **綁定** > **每個資料項的重複行**。

   ![為佈局片段重複屬性](assets/layout_fragment_print_repeat_new.png)

1. 將&#x200B;**文本欄位**&#x200B;元件從&#x200B;**對象庫**&#x200B;拖放到&#x200B;**設計器視圖**&#x200B;中。

   ![版面片段的文字欄位](assets/layout_fragment_print_text_field_new.png)

   同樣，將&#x200B;**文本欄位**&#x200B;元件拖放到&#x200B;**時間**、**數字**、**持續時間**&#x200B;和&#x200B;**費用**&#x200B;行。

1. 選擇&#x200B;**File** > **Save As**&#x200B;以在本地檔案系統上保存檔案：

   1. 導覽至要儲存檔案的位置，並指定名稱為&#x200B;**table_lf**。
   1. 從&#x200B;**另存為類型**&#x200B;下拉清單中選擇&#x200B;**.xdp**。

   1. 點選&#x200B;**儲存**。
   使用Forms設計工具為版面片段建立XDP範本後，您必須[上傳](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)至AEM Forms伺服器，讓範本可在建立版面片段時使用。

## 建立Web通道{#create-template-for-web-channel}的模板

使用以下任務建立和管理互動式通信的Web通道模板：

* [為範本建立資料夾](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [建立範本](../../forms/using/create-templates-print-web.md#create-the-template)
* [啟用範本](../../forms/using/create-templates-print-web.md#enable-the-template)
* [啟用互動式通訊中的按鈕](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 為模板{#create-folder-for-templates}建立資料夾

若要建立Web管道範本，請定義資料夾，以儲存已建立的範本。 在該資料夾內建立模板後，請啟用該模板以允許表單用戶根據模板建立互動式通信的Web通道。

執行下列步驟為可編輯的範本建立資料夾：

1. 點選&#x200B;**工具** ![槌子圖示](assets/hammer-icon.svg) > **配置瀏覽器**。
   * 如需詳細資訊，請參閱[設定瀏覽器](/help/sites-administering/configurations.md)檔案。
1. 在「設定瀏覽器」頁面中，點選&#x200B;**Create**。
1. 在&#x200B;**建立配置**&#x200B;對話框中，指定&#x200B;**Create_First_IC_templates**&#x200B;作為資料夾的標題，檢查&#x200B;**可編輯的模板**，然後點選&#x200B;**建立**。

   ![配置Web模板](assets/create_first_ic_web_template_new.png)

   建立&#x200B;**Create_First_IC_templates**&#x200B;資料夾並在&#x200B;**配置瀏覽器**&#x200B;頁面上列出。

### 建立範本{#create-the-template}

根據[使用案例](/help/forms/using/create-your-first-interactive-communication.md)和[解剖學](/help/forms/using/planning-interactive-communications.md)，在Web範本中建立下列面板：

* 帳單詳細資訊：包含檔案片段
* 客戶詳細資訊：包含檔案片段
* 清單匯總：包含檔案片段
* 費用匯總：包含檔案片段和圖表（雙欄配置）
* 逐項呼叫：包括表
* 立即支付：包含&#x200B;**立即支付**&#x200B;按鈕和影像
* 增值服務：包含影像和&#x200B;**Subscribe**&#x200B;按鈕。

![create_web_template](assets/create_web_template.gif)

建立互動式通信時，將添加所有實體，如文檔片段、圖表、表、影像和按鈕。

執行以下步驟為&#x200B;**Create_First_IC_templates**&#x200B;資料夾中的Web通道建立模板：

1. 通過選擇&#x200B;**工具** > **模板** > **Create_First_IC_templates**&#x200B;資料夾，導航到相應的模板資料夾。
1. 點選&#x200B;**建立**。
1. 在&#x200B;**選擇模板類型**&#x200B;配置嚮導中，選擇&#x200B;**互動式通信 — Web通道**&#x200B;並點選&#x200B;**下一步**。
1. 在&#x200B;**模板詳細資訊**&#x200B;配置嚮導中，將&#x200B;**Create_First_IC_Web_Template**&#x200B;指定為模板標題。 指定可選的說明，然後點選&#x200B;**Create**。

   顯示&#x200B;**Create_First_IC_Web_Template**&#x200B;的確認消息。

1. 點選&#x200B;**開啟**&#x200B;以在範本編輯器中開啟範本。
1. 從&#x200B;**預覽**&#x200B;選項旁的下拉式清單中選取&#x200B;**初始內容**。

   ![範本編輯器](assets/template_editor_initial_content_new.png)

1. 點選「**根面板**」，然後點選「**+**」以檢視可新增至範本的元件清單。
1. 從清單中選擇&#x200B;**面板**&#x200B;以在&#x200B;**根面板**&#x200B;上添加面板。
1. 在左窗格中選擇&#x200B;**Content**&#x200B;頁簽。 步驟8中新增的新面板會顯示在內容樹狀結構的&#x200B;**根面板**&#x200B;下。

   ![內容樹](assets/content_tree_root_panel_new.png)

1. 選取面板，然後點選![configure_icon](assets/configure_icon.png)(Configure)。
1. 在「屬性」窗格中：

   1. 在「名稱」欄位中指定&#x200B;**billdetails**。
   1. 在「標題」欄位中指定&#x200B;**清單詳細資訊**。
   1. 從&#x200B;**列數**&#x200B;下拉清單中選擇&#x200B;**1**。

   1. 點選![](/help/forms/using/assets/done_icon.png)以儲存屬性。

   面板的名稱會更新為內容樹中的&#x200B;**清單詳細資訊**。

1. 重複步驟7 - 11將具有下列屬性的面板新增至範本：

   | 名稱 | 標題 | 欄數 |
   |---|---|---|
   | customerdetails | 客戶詳細資訊 | 1 |
   | 帳單摘要 | 清單匯總 | 3 |
   | 摘要費用 | 費用匯總 | 2 |
   | itemiedcalls | 逐項呼叫 | 3 |
   | paynow | 立即支付 | 2 |
   | vas | 增值服務 | 3 |

   將所有面板新增至範本後，下列影像會描繪內容樹狀結構：

   ![所有面板的內容樹](assets/content_tree_all_panels_new.png)

### 啟用模板{#enable-the-template}

建立Web模板後，必須啟用該模板以在建立交互通信時使用該模板。

執行下列步驟以啟用Web模板：

1. 點選&#x200B;**工具** ![槌子圖示](assets/hammer-icon.svg) > **範本**。
1. 導覽至&#x200B;**Create_First_IC_Web_Template**&#x200B;範本，選取該範本，然後點選&#x200B;**啟用**。
1. 頁簽&#x200B;**再次啟用**&#x200B;以進行確認。

   範本已啟用，其狀態會顯示為已啟用。 在為Web通道建立互動式通信時，可以使用此模板。

### 啟用互動式通信中的按鈕{#enabling-buttons-in-interactive-communications}

根據使用案例，您必須在互動式通訊中包含&#x200B;**立即支付**&#x200B;和&#x200B;**訂閱**&#x200B;按鈕（最適化表單元件）。 要在互動式通信中啟用這些按鈕，請執行以下步驟：

1. 從&#x200B;**預覽**&#x200B;選項旁的下拉清單中選擇&#x200B;**結構**。
1. 使用內容樹選擇&#x200B;**Document Container**&#x200B;根面板，然後點選&#x200B;**Policy**&#x200B;以選擇允許在交互通信中使用的元件。

   ![配置策略](assets/structure_configure_policy_new.png)

1. 在&#x200B;**屬性**&#x200B;區段的&#x200B;**允許的元件**&#x200B;標籤中，從&#x200B;**適用性表單**&#x200B;元件中選擇&#x200B;**按鈕**。

   ![允許的元件](assets/allowed_components_af_new.png)

1. 點選![done_icon](assets/done_icon.png)以儲存屬性。
