---
title: 「教學課程：建立範本」
seo-title: Create Print and Web templates for Interactive Communication
description: 建立用於互動式通信的打印和Web模板
seo-description: Create Print and Web templates for Interactive Communication
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1796'
ht-degree: 0%

---

# 教學課程：建立範本{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

本教學課程是 [建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md) 系列。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

若要建立互動式通訊，您必須在AEM伺服器上提供用於列印和網頁頻道的範本。

列印管道的範本是在AdobeForms Designer中建立，並上傳至AEM伺服器。 然後，這些模板便可在建立互動式通信時使用。

網頁管道的範本是在AEM中建立。 範本作者和管理員可以建立、編輯和啟用網頁範本。 建立並啟用後，這些範本便可在建立互動式通訊時使用。

本教學課程會逐步引導您完成建立列印和網頁頻道範本的步驟，以便在建立互動式通訊時使用。 在本教學課程結束時，您將能夠：

* 使用AdobeForms Designer為列印管道建立XDP範本
* 將XDP範本上傳至AEM Forms伺服器
* 建立和啟用Web通道的模板

## 建立列印管道的範本 {#create-template-for-print-channel}

使用以下任務建立和管理互動式通信的打印通道模板：

* [使用Forms Designer建立XDP範本](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [上傳XDP範本至AEM Forms伺服器](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [為版面片段建立XDP範本](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### 使用Forms Designer建立XDP範本 {#create-xdp-template-using-forms-designer}

根據 [使用案例](/help/forms/using/create-your-first-interactive-communication.md) 和 [解剖學](/help/forms/using/planning-interactive-communications.md)，在XDP範本中建立下列子表單：

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

1. 開啟Forms Designer，選取 **檔案** > **新增** > **使用空白表單，** 點 **下一個**，然後點選 **完成** 開啟建立模板的表單。

   確保 **物件程式庫** 和 **物件** 選項 **視窗** 功能表。

1. 拖放 **子表單** 元件 **物件程式庫** 到表單中。
1. 選取子表單，以在 **物件** 窗口。
1. 選取 **子表單** 索引標籤和選取 **流** 從 **內容** 下拉式清單。 拖動子表單的左端點以調整長度。
1. 在 **綁定** 標籤：

   1. 指定 **BillDetails** 在 **名稱** 欄位。

   1. 選擇 **無資料綁定** 從 **資料綁定** 下拉式清單。

   ![設計器子表單](assets/forms_designer_subform_new.png)

1. 同樣地，選取根子表單，選取 **子表單** ，然後選取 **流** 從 **內容** 下拉式清單。 在 **綁定** 標籤：

   1. 指定 **電信賬單** 在 **名稱** 欄位。

   1. 選擇 **無資料綁定** 從 **資料綁定** 下拉式清單。

   ![打印模板的子表單](assets/root_subform_print_template_new.png)

1. 重複步驟2 - 5以建立下列子表單：

   * BillDetails
   * 客戶詳細資訊
   * BillSummary
   * 摘要 — 選取 **子表單** 索引標籤和選取 **定位** 從 **內容** 下拉式清單。 在 **摘要** 子表單。

      * 費用
      * 圖表
   * ItemisedCalls
   * PayNow
   * ValueAddedServices

   為了節省時間，您也可以複製並貼上現有的子表單以建立新的子表單。

   若要移動 **圖表** 按一下「費用」子表單的右側，選擇 **圖表** 從左窗格選取子表單 **版面** ，並指定 **AnchorX** 欄位。 值必須大於 **寬度** 欄位 **費用** 子表單。 選取 **費用** 子表單並選取 **版面** 標籤來檢視 **寬度** 欄位。

1. 拖放 **文字** 物件 **物件程式庫** ，然後輸入 **撥打XXXX以訂閱** 文字。
1. 按一下右鍵左窗格中的文本對象，選擇 **更名對象**，並輸入文本對象的名稱作為 **訂閱**.

   ![XDP範本](assets/print_xdp_template_subform_new.png)

1. 選擇 **檔案** > **另存新檔** 要在本地檔案系統上保存檔案，請執行以下操作：

   1. 導覽至要儲存檔案的位置，並指定名稱為 **create_first_ic_print_template**.
   1. 選擇 **.xdp** 從 **另存為類型** 下拉式清單。

   1. 點選 **儲存**.

### 上傳XDP範本至AEM Forms伺服器 {#upload-xdp-template-to-the-aem-forms-server}

使用Forms Designer建立XDP範本後，必須將其上傳至AEM Forms伺服器，以便在建立互動式通訊時讓範本可供使用。

1. 選擇 **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **建立** > **檔案上傳**.

   導覽並選取 **create_first_ic_print_template** 範本(XDP)並點選 **開啟** 將XDP範本匯入AEM Forms伺服器。

### 為版面片段建立XDP範本 {#create-xdp-template-for-layout-fragments}

若要為互動式通訊的列印通道建立版面片段，請使用Forms Designer建立XDP，並將其上傳至AEM Forms伺服器。

1. 開啟Forms Designer，選取 **檔案** > **新增** > **使用空白表單，** 點 **下一個**，然後點選 **完成** 開啟建立模板的表單。

   確保 **物件程式庫** 和 **物件** 選項 **視窗** 功能表。

1. 拖放 **表格** 元件 **物件程式庫** 到表單中。
1. 在「插入表」(Insert Table)對話框中：

   1. 指定欄數為 **5**.
   1. 將內文列數指定為 **1**.
   1. 選取 **在表格中包含標題列** 核取方塊。
   1. 標籤 **確定**.

1. 點選 **+** 在旁邊的左窗格中 **表格** 1並按一下滑鼠右鍵 **Cell1** 選取 **更名對象** to **日期**.

   同樣地，請重新命名 **單元格2**, **Cell3**, **單元格4**，和 **單元5** to **時間**, **數字**, **持續時間**，和 **費用** 分別為5個。

1. 按一下 **設計器視圖** 將它們重新命名為 **時間**, **數字**, **持續時間**，和 **費用**.

   ![版面片段](assets/layout_fragment_print_new.png)

1. 選擇 **第1列** 從左窗格中選擇 **物件** > **綁定** > **對每個資料項重複行**.

   ![為佈局片段重複屬性](assets/layout_fragment_print_repeat_new.png)

1. 拖放 **文字欄位** 元件 **物件程式庫** 到 **設計器視圖**.

   ![版面片段的文字欄位](assets/layout_fragment_print_text_field_new.png)

   同樣地，拖放 **文字欄位** 元件 **時間**, **數字**, **持續時間**，和 **費用** 行。

1. 選擇 **檔案** > **另存新檔** 要在本地檔案系統上保存檔案，請執行以下操作：

   1. 導覽至要儲存檔案的位置，並指定名稱為 **table_lf**.
   1. 選擇 **.xdp** 從 **另存為類型** 下拉式清單。

   1. 點選 **儲存**.
   使用Forms設計工具建立版面片段的XDP範本後，您必須 [上傳](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) 傳送至AEM Forms伺服器，讓範本可在建立版面片段時使用。

## 建立網頁頻道範本 {#create-template-for-web-channel}

使用以下任務建立和管理互動式通信的Web通道的模板：

* [為範本建立資料夾](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [建立範本](../../forms/using/create-templates-print-web.md#create-the-template)
* [啟用範本](../../forms/using/create-templates-print-web.md#enable-the-template)
* [啟用互動式通訊中的按鈕](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 為範本建立資料夾 {#create-folder-for-templates}

若要建立Web管道範本，請定義資料夾，以儲存已建立的範本。 在該資料夾內建立模板後，請啟用該模板以允許表單用戶根據模板建立互動式通信的Web通道。

執行下列步驟為可編輯的範本建立資料夾：

1. 點選 **工具** ![錘子表徵圖](assets/hammer-icon.svg) > **配置瀏覽器**.
   * 請參閱 [配置瀏覽器](/help/sites-administering/configurations.md) 檔案以取得詳細資訊。
1. 在「設定瀏覽器」頁面中，點選 **建立**.
1. 在 **建立配置** 對話框，指定 **Create_First_IC_templates** 作為資料夾的標題，請核取 **可編輯的範本**，然後點選 **建立**.

   ![配置Web模板](assets/create_first_ic_web_template_new.png)

   此 **Create_First_IC_templates** 資料夾已建立並列於 **配置瀏覽器** 頁面。

### 建立範本 {#create-the-template}

根據 [使用案例](/help/forms/using/create-your-first-interactive-communication.md) 和 [解剖學](/help/forms/using/planning-interactive-communications.md)，在網頁範本中建立下列面板：

* 帳單詳細資訊：包含檔案片段
* 客戶詳細資訊：包含檔案片段
* 清單匯總：包含檔案片段
* 費用匯總：包含檔案片段和圖表（雙欄配置）
* 逐項呼叫：包括表
* 立即支付：包括 **立即支付** 按鈕和影像
* 增值服務：包括影像和 **訂閱** 按鈕。

![create_web_template](assets/create_web_template.gif)

建立互動式通信時，將添加所有實體，如文檔片段、圖表、表、影像和按鈕。

執行下列步驟，為 **Create_First_IC_templates** 資料夾：

1. 透過選取 **工具** > **範本** > **Create_First_IC_templates** 檔案夾。
1. 點選 **建立**.
1. 在 **選擇模板類型** 配置嚮導，選擇 **互動式通訊 — Web頻道** 點選 **下一個**.
1. 在 **範本詳細資料** 配置嚮導，指定 **Create_First_IC_Web_Template** 作為範本標題。 指定選擇性的說明並點選 **建立**.

   確認訊息顯示 **Create_First_IC_Web_Template** 的下界。

1. 點選 **開啟** 以在範本編輯器中開啟範本。
1. 選擇 **初始內容** 從 **預覽** 選項。

   ![範本編輯器](assets/template_editor_initial_content_new.png)

1. 點選 **根面板** 然後點選 **+** 查看可添加到模板的元件清單。
1. 選擇 **面板** 從清單中新增面板 **根面板**.
1. 選取 **內容** 頁簽。 步驟8中新增的新面板會顯示在 **根面板** 在內容樹中。

   ![內容樹](assets/content_tree_root_panel_new.png)

1. 選取面板並點選 ![configure_icon](assets/configure_icon.png) （配置）。
1. 在「屬性」窗格中：

   1. 指定 **帳單詳細資訊** 在「名稱」欄位中。
   1. 指定 **帳單詳細資訊** 在標題欄位中。
   1. 選擇 **1** 從 **欄數** 下拉式清單。

   1. 點選 ![](/help/forms/using/assets/done_icon.png) 以儲存屬性。

   面板的名稱會更新為 **帳單詳細資訊** 在內容樹中。

1. 重複步驟7 - 11將具有下列屬性的面板新增至範本：

   | 名稱 | 標題 | 欄數 |
   |---|---|---|
   | customerdetails | 客戶詳細資訊 | 1 |
   | 帳單摘要 | 清單匯總 | 1 |
   | 摘要費用 | 費用匯總 | 2 |
   | itemiedcalls | 逐項呼叫 | 1 |
   | paynow | 立即支付 | 2 |
   | vas | 增值服務 | 1 |

   將所有面板新增至範本後，下列影像會描繪內容樹狀結構：

   ![所有面板的內容樹](assets/content_tree_all_panels_new.png)

### 啟用範本 {#enable-the-template}

建立Web模板後，必須啟用該模板以在建立交互通信時使用該模板。

執行下列步驟以啟用Web模板：

1. 點選 **工具** ![錘子表徵圖](assets/hammer-icon.svg) > **範本**.
1. 導覽至 **Create_First_IC_Web_Template** 範本，選取它，然後點選 **啟用**.
1. 標籤 **啟用** 再次確認。

   範本已啟用，其狀態會顯示為已啟用。 在為Web通道建立互動式通信時，可以使用此模板。

### 啟用互動式通訊中的按鈕 {#enabling-buttons-in-interactive-communications}

根據使用案例，您必須包含 **立即支付** 和 **訂閱** 互動式通訊中的按鈕（最適化表單元件）。 要在互動式通信中啟用這些按鈕，請執行以下步驟：

1. 選擇 **結構** 從 **預覽** 選項。
1. 選取 **文檔容器** 使用內容樹並點選根面板 **原則** ，以選擇允許在交互通信中使用的元件。

   ![配置策略](assets/structure_configure_policy_new.png)

1. 在 **允許的元件** 標籤 **屬性** 部分，選擇 **按鈕** 從 **適用性表單** 元件。

   ![允許的元件](assets/allowed_components_af_new.png)

1. 點選 ![done_icon](assets/done_icon.png) 以儲存屬性。
