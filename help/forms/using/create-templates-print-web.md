---
title: 「教學課程：建立範本」
seo-title: 建立互動式通訊的列印和網頁範本
description: 建立互動式通訊的列印和網頁範本
seo-description: 建立互動式通訊的列印和網頁範本
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
feature: 互動式通訊
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1814'
ht-degree: 0%

---


# 教學課程：建立範本{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

本教學課程是[建立您第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md)系列中的步驟。 建議依序依序依序排列，以瞭解、執行和展示完整的教學課程使用案例。

若要建立互動式通訊，您必須在伺服器上提供列印和網AEM路頻道的範本。

列印渠道的範本是在AdobeForms設計人員中建立，並上傳至伺AEM服器。 然後，這些範本便可在建立互動式通訊時使用。

網頁渠道的範本是在中建立AEM的。 範本作者和管理員可以建立、編輯和啟用Web範本。 在建立並啟用後，這些範本就可在建立互動式通訊時使用。

本教學課程會逐步帶您建立列印和網路頻道的範本，以便在建立互動式通訊時使用。 在本教學課程結束時，您將能夠：

* 使用AdobeForms設計師為印刷渠道建立XDP模板
* 將XDP範本上傳至AEM Forms伺服器
* 建立並啟用網頁頻道的範本

## 建立列印頻道的範本{#create-template-for-print-channel}

使用下列工作建立和管理互動式通訊列印頻道的範本：

* [使用Forms設計師建立XDP模板](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [上傳XDP範本至AEM Forms伺服器](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [建立版面片段的XDP範本](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### 使用Forms設計器{#create-xdp-template-using-forms-designer}建立XDP模板

根據[使用案例](/help/forms/using/create-your-first-interactive-communication.md)和[解剖](/help/forms/using/planning-interactive-communications.md)，在XDP範本中建立下列子表單：

* 帳單詳細資訊：包含檔案片段
* 客戶詳細資訊：包含檔案片段
* 清單匯總：包含檔案片段
* 摘要：包含文檔片段（費用子表單）和圖表（圖表子表單）
* 明細呼叫：包含表格（版面片段）
* 立即付款：包含影像
* 增值服務：包含影像

![create_print_template](assets/create_print_template.gif)

將XDP檔案上傳至Forms伺服器後，這些子表單會在列印範本中顯示為目標區域。 建立互動式通訊時，所有實體（例如檔案片段、圖表、版面片段和影像）都會新增至目標區域。

執行以下步驟，為打印渠道建立XDP模板：

1. 開啟Forms設計器，選擇「**檔案** > **新建** > **使用空格表單」，按一下「**&#x200B;下一步」，然後按一下「完成」以開啟建立模板的表單。********

   確保從&#x200B;**窗口**&#x200B;菜單中選擇了&#x200B;**對象庫**&#x200B;和&#x200B;**對象**&#x200B;選項。

1. 將&#x200B;**Subform**&#x200B;元件從&#x200B;**對象庫**&#x200B;拖放到窗體中。
1. 選擇子表單，在右窗格的&#x200B;**Object**&#x200B;窗口中顯示子表單的選項。
1. 選擇&#x200B;**子表單**&#x200B;標籤，並從&#x200B;**內容**&#x200B;下拉式清單中選擇&#x200B;**Fled**。 拖動子表單的左端點以調整長度。
1. 在&#x200B;**綁定**&#x200B;頁籤中：

   1. 在&#x200B;**名稱**&#x200B;欄位中指定&#x200B;**BillDetails**。

   1. 從&#x200B;**資料綁定**&#x200B;下拉清單中選擇&#x200B;**無資料綁定**。

   ![設計人員子表單](assets/forms_designer_subform_new.png)

1. 同樣地，選擇根子表單，選擇&#x200B;**子表單**&#x200B;頁籤，並從&#x200B;**內容**&#x200B;下拉清單中選擇&#x200B;**流**。 在&#x200B;**綁定**&#x200B;頁籤中：

   1. 在&#x200B;**名稱**&#x200B;欄位中指定&#x200B;**TelecaBill**。

   1. 從&#x200B;**資料綁定**&#x200B;下拉清單中選擇&#x200B;**無資料綁定**。

   ![列印範本的子表單](assets/root_subform_print_template_new.png)

1. 重複步驟2 - 5以建立以下子表單：

   * BillDetails
   * 客戶詳細資訊
   * BillSummary
   * 摘要——選擇&#x200B;**子表單**&#x200B;標籤，並從&#x200B;**內容**&#x200B;下拉式清單中選擇&#x200B;**定位**。 在&#x200B;**Summary**&#x200B;子表單中插入以下子表單。

      * 費用
      * 圖表
   * ItemisedCalls
   * PayNow
   * ValueAddedServices

   為節省時間，您也可以複製並貼上現有的子表單，以建立新的子表單。

   要將&#x200B;**Charts**&#x200B;子表單移到Charges子表單的右側，請從左窗格選擇&#x200B;**Charts**&#x200B;子表單，選擇&#x200B;**Layout**&#x200B;標籤，並指定&#x200B;**AnchorX**&#x200B;欄位的值。 該值必須大於&#x200B;**Charges**&#x200B;子表單的&#x200B;**Width**&#x200B;欄位的值。 選擇&#x200B;**Charges**&#x200B;子表單，並選擇&#x200B;**Layout**&#x200B;頁籤以查看&#x200B;**Width**&#x200B;欄位的值。

1. 將&#x200B;**Text**&#x200B;對象庫&#x200B;**中的**&#x200B;對象拖放到窗體中，並在框中輸入&#x200B;**撥號XXXX以預訂**&#x200B;文本。
1. 按一下右鍵左窗格中的文本對象，選擇&#x200B;**更名對象** ，然後將文本對象的名稱輸入為&#x200B;**訂閱**。

   ![XDP範本](assets/print_xdp_template_subform_new.png)

1. 選擇「**檔案** > **另存為**」以在本地檔案系統中保存檔案：

   1. 導覽至儲存檔案的位置，並指定名稱為&#x200B;**create_first_ic_print_template**。
   1. 從&#x200B;**另存類型**&#x200B;下拉式清單中選擇&#x200B;**.xdp**。

   1. 點選&#x200B;**Save**。

### 將XDP模板上傳到AEM Forms伺服器{#upload-xdp-template-to-the-aem-forms-server}

使用Forms設計器建立XDP模板後，必須將其上載到AEM Forms伺服器，以便在建立交互通信時使用該模板。

1. 選擇&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 點選「**建立** > **檔案上傳**」。

   導覽並選取&#x200B;**create_first_ic_print_template**&#x200B;範本(XDP)，然後點選&#x200B;**Open**&#x200B;將XDP範本匯入AEM Forms伺服器。

### 建立版面片段{#create-xdp-template-for-layout-fragments}的XDP範本

若要為互動式通訊的列印頻道建立版面片段，請使用Forms設計人員建立XDP，並上傳至AEM Forms伺服器。

1. 開啟Forms設計器，選擇「**檔案** > **新建** > **使用空格表單」，按一下「**&#x200B;下一步」，然後按一下「完成」以開啟建立模板的表單。********

   確保從&#x200B;**窗口**&#x200B;菜單中選擇了&#x200B;**對象庫**&#x200B;和&#x200B;**對象**&#x200B;選項。

1. 將&#x200B;**Table**&#x200B;元件從&#x200B;**對象庫**&#x200B;拖放到窗體中。
1. 在「插入表」對話框中：

   1. 將列數指定為&#x200B;**5**。
   1. 將主體行數指定為&#x200B;**1**。
   1. 選中&#x200B;**在表**&#x200B;中包括標題行複選框。
   1. 頁籤&#x200B;**確定**。

1. 在&#x200B;**Table** 1旁的左窗格中點選&#x200B;**+**，然後在&#x200B;**Cell1**&#x200B;上按一下滑鼠右鍵，並選取「將物件&#x200B;**重新命名為** Date **」。**

   同樣地，將&#x200B;**單元2**、**單元3**、**單元4**&#x200B;和&#x200B;**單元5**&#x200B;更名為&#x200B;**時間**、**數字**、&lt;a12/持續時間&#x200B;**和**&#x200B;電荷&#x200B;**。**

1. 按一下&#x200B;**設計器視圖**&#x200B;中的「標題」文本欄位，並將它們更名為&#x200B;**Time**、**Number**、**Duration**&#x200B;和&#x200B;**Charges**。

   ![版面片段](assets/layout_fragment_print_new.png)

1. 從左窗格中選擇「**行1**」，然後選擇「**對象** > **綁定** > **對每個資料項**&#x200B;重複行」。

   ![重複版面片段的屬性](assets/layout_fragment_print_repeat_new.png)

1. 將&#x200B;**文本欄位**&#x200B;元件從&#x200B;**對象庫**&#x200B;拖放到&#x200B;**設計器視圖**。

   ![版面片段的文字欄位](assets/layout_fragment_print_text_field_new.png)

   同樣地，將&#x200B;**文本欄位**&#x200B;元件拖放到&#x200B;**Time**、**Number**、**Duration**&#x200B;和&#x200B;**Charges**&#x200B;行。

1. 選擇「**檔案** > **另存為**」以在本地檔案系統中保存檔案：

   1. 導覽至儲存檔案的位置，並指定名稱為&#x200B;**table_lf**。
   1. 從&#x200B;**另存類型**&#x200B;下拉式清單中選擇&#x200B;**.xdp**。

   1. 點選&#x200B;**Save**。
   使用Forms設計器為佈局片段建立XDP模板後，必須[upload](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)將其上載到AEM Forms伺服器，以便在建立佈局片段時使用該模板。

## 建立網路頻道{#create-template-for-web-channel}的範本

使用下列工作建立和管理互動式通訊網路頻道的範本：

* [為範本建立資料夾](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [建立範本](../../forms/using/create-templates-print-web.md#create-the-template)
* [啟用範本](../../forms/using/create-templates-print-web.md#enable-the-template)
* [在互動式通訊中啟用按鈕](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 為模板{#create-folder-for-templates}建立資料夾

若要建立Web頻道範本，請定義可儲存已建立範本的檔案夾。 在您在該資料夾內建立範本後，啟用範本，讓表單使用者能夠根據範本建立互動式通訊的網路頻道。

執行以下步驟為可編輯模板建立資料夾：

1. 點選「**工具** ![槌子圖示](assets/hammer-icon.svg) > **組態瀏覽器**」。
   * 如需詳細資訊，請參閱[Configuration Browser](/help/sites-administering/configurations.md)檔案。
1. 在「配置瀏覽器」頁中，按一下&#x200B;**建立**。
1. 在&#x200B;**建立配置**&#x200B;對話框中，指定&#x200B;**建立_First_IC_templates**&#x200B;作為資料夾的標題，選中&#x200B;**可編輯模板** ，然後點選&#x200B;**建立**。

   ![設定網頁範本](assets/create_first_ic_web_template_new.png)

   建立&#x200B;**Create_First_IC_templates**&#x200B;資料夾並列在&#x200B;**配置瀏覽器**&#x200B;頁面上。

### 建立模板{#create-the-template}

根據[使用案例](/help/forms/using/create-your-first-interactive-communication.md)和[解剖](/help/forms/using/planning-interactive-communications.md)，在Web範本中建立下列面板：

* 帳單詳細資訊：包含檔案片段
* 客戶詳細資訊：包含檔案片段
* 清單匯總：包含檔案片段
* 費用匯總：包含檔案片段和圖表（雙欄版面）
* 明細呼叫：包含表格
* 立即付款：包含&#x200B;**立即付費按鈕和影像**
* 增值服務：包含影像和&#x200B;**Subscribe**&#x200B;按鈕。

![create_web_template](assets/create_web_template.gif)

建立交互通信時，將添加所有實體，如文檔片段、圖表、表、影像和按鈕。

執行以下步驟，在&#x200B;**Create_First_IC_templates**&#x200B;資料夾中為Web通道建立模板：

1. 選擇&#x200B;**工具** > **模板** > **建立_First_IC_templates**&#x200B;資料夾，導航到相應的模板資料夾。
1. 點選&#x200B;**Create**。
1. 在&#x200B;**選擇模板類型**&#x200B;配置嚮導中，選擇&#x200B;**交互通信- Web通道**&#x200B;並按一下&#x200B;**下一步**。
1. 在&#x200B;**Template Details**&#x200B;配置嚮導中，指定&#x200B;**Create_First_IC_Web_Template**&#x200B;作為模板標題。 指定可選說明並點選&#x200B;**Create**。

   顯示確認消息，確認&#x200B;**Create_First_IC_Web_Template**。

1. 點選「**開啟**」，在範本編輯器中開啟範本。
1. 從&#x200B;**預覽**&#x200B;選項旁的下拉式清單中選擇&#x200B;**初始內容**。

   ![範本編輯器](assets/template_editor_initial_content_new.png)

1. 點選「**根面板**」，然後點選「**+**」以檢視您可新增至範本的元件清單。
1. 從清單中選擇&#x200B;**面板**&#x200B;以在&#x200B;**根面板**&#x200B;上方添加面板。
1. 在左窗格中選擇&#x200B;**Content**&#x200B;標籤。 在步驟8中新增的新面板會顯示在內容樹的&#x200B;**根面板**&#x200B;下。

   ![內容樹](assets/content_tree_root_panel_new.png)

1. 選擇面板並點選![configure_icon](assets/configure_icon.png)（設定）。
1. 在「屬性」窗格中：

   1. 在「名稱」欄位中指定&#x200B;**billdetails**。
   1. 在「標題」欄位中指定&#x200B;**清單詳細資訊**。
   1. 從&#x200B;**欄數**&#x200B;下拉式清單中選擇&#x200B;**1**。

   1. 點選![](/help/forms/using/assets/done_icon.png)以儲存屬性。

   面板的名稱將更新為內容樹中的&#x200B;**Bill Details**。

1. 重複步驟7 - 11，將具有下列屬性的面板新增至範本：

   | 名稱 | 標題 | 欄數 |
   |---|---|---|
   | customerdetails | 客戶詳細資訊 | 1 |
   | 開單匯總 | 清單摘要 | 3 |
   | 摘要費用 | 費用匯總 | 2 |
   | itimisedcalls | 明細呼叫 | 1 |
   | paynow | 立即付款 | 2 |
   | vas | 增值服務 | 3 |

   下圖顯示將所有面板新增至範本後的內容樹狀結構：

   ![所有面板的內容樹狀結構](assets/content_tree_all_panels_new.png)

### 啟用模板{#enable-the-template}

建立網頁範本後，您必須在建立互動式通訊時啟用範本。

執行以下步驟以啟用Web模板：

1. 點選「**工具** ![槌子圖示](assets/hammer-icon.svg) > **範本**」。
1. 導覽至&#x200B;**Create_First_IC_Web_Template**&#x200B;範本，選取範本，然後點選&#x200B;**Enable**。
1. 頁籤&#x200B;**再次啟用**&#x200B;以確認。

   範本已啟用，其狀態會顯示為「已啟用」。 您可以在建立適用於網路頻道的互動式通訊時使用此範本。

### 在互動式通信中啟用按鈕{#enabling-buttons-in-interactive-communications}

根據使用案例，您必須在「互動式通訊」中加入「立即付費」(Pay Now)**和「訂閱」(Subscribe)**&#x200B;按鈕（最適化表單元件）。 ****&#x200B;要在交互通信中啟用這些按鈕，請執行以下步驟：

1. 從&#x200B;**預覽**&#x200B;選項旁的下拉式清單中選擇&#x200B;**結構**。
1. 使用內容樹選擇&#x200B;**Document Container**&#x200B;根面板，然後點選&#x200B;**Policy**&#x200B;以選擇允許在交互通信中使用的元件。

   ![設定原則](assets/structure_configure_policy_new.png)

1. 在&#x200B;**屬性**&#x200B;部分的&#x200B;**允許的元件**&#x200B;頁籤中，從&#x200B;**最適化表單**&#x200B;元件中選擇&#x200B;**按鈕**。

   ![允許的元件](assets/allowed_components_af_new.png)

1. 點選![done_icon](assets/done_icon.png)以儲存屬性。