---
title: 「教程：建立模板"
seo-title: Create Print and Web templates for Interactive Communication
description: 為交互通信建立打印和Web模板
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

# 教程：建立模板{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

本教程是 [建立您的第一個互動式通信](/help/forms/using/create-your-first-interactive-communication.md) 的下界。 建議按時間順序按系列進行操作，以瞭解、執行和演示完整的教程使用案例。

要建立互動式通信，必須在伺服器上提供用於打AEM印和Web通道的模板。

打印通道的模板是在AdobeForms設計器中建立並上載到服AEM務器。 然後，這些模板在建立交互通信時可用。

Web通道的模板是在中建立AEM的。 模板作者和管理員可以建立、編輯和啟用Web模板。 建立並啟用後，這些模板可在建立交互通信時使用。

本教程將指導您完成建立打印和Web通道模板的步驟，以便在建立互動式通信時使用這些模板。 在本教程的結束時，您將能夠：

* 使用AdobeForms設計器為打印通道建立XDP模板
* 將XDP模板上載到AEM Forms伺服器
* 為Web渠道建立和啟用模板

## 為打印通道建立模板 {#create-template-for-print-channel}

使用以下任務為互動式通信的打印通道建立和管理模板：

* [使用Forms設計器建立XDP模板](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [將XDP模板上載到AEM Forms伺服器](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [為佈局片段建立XDP模板](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### 使用Forms設計器建立XDP模板 {#create-xdp-template-using-forms-designer}

基於 [用例](/help/forms/using/create-your-first-interactive-communication.md) 和 [解剖](/help/forms/using/planning-interactive-communications.md)，在XDP模板中建立以下子窗體：

* 帳單詳細資訊：包括文檔片段
* 客戶詳細資訊：包括文檔片段
* 清單摘要：包括文檔片段
* 摘要：包括文檔片段（費用子窗體）和圖表（圖表子窗體）
* 明細調用：包括表（佈局片段）
* 立即支付：包括影像
* 增值服務：包括影像

![create_print_template](assets/create_print_template.gif)

將XDP檔案上載到Forms伺服器後，這些子表單在打印模板中顯示為目標區域。 建立交互通信時，所有實體（如文檔片段、圖表、佈局片段和影像）都會添加到目標區域。

執行以下步驟為打印通道建立XDP模板：

1. 開啟Forms設計器，選擇 **檔案** > **新建** > **使用空白表格，** 點擊 **下一個**，然後按一下 **完成** 開啟表單以建立模板。

   確保 **對象庫** 和 **對象** 選項 **窗口** 的子菜單。

1. 拖放 **子窗體** 元件 **對象庫** 的下界。
1. 選擇子窗體以在 **對象** 的上界。
1. 選擇 **子窗體** 頁籤 **流** 從 **內容** 的子菜單。 拖動子窗體的左端點以調整長度。
1. 在 **綁定** 頁籤：

   1. 指定 **帳單詳細資訊** 的 **名稱** 的子菜單。

   1. 選擇 **無資料綁定** 從 **資料綁定** 的子菜單。

   ![設計器子窗體](assets/forms_designer_subform_new.png)

1. 同樣，選擇根子窗體，選擇 **子窗體** ，然後選擇 **流** 從 **內容** 的子菜單。 在 **綁定** 頁籤：

   1. 指定 **電話賬單** 的 **名稱** 的子菜單。

   1. 選擇 **無資料綁定** 從 **資料綁定** 的子菜單。

   ![打印模板的子窗體](assets/root_subform_print_template_new.png)

1. 重複步驟2 - 5以建立以下子表單：

   * 帳單詳細資訊
   * 客戶詳細資訊
   * 清單摘要
   * 摘要 — 選擇 **子窗體** 頁籤 **定位** 從 **內容** 下拉清單。 在 **摘要** 的子菜單。

      * 費用
      * 圖表
   * ItemisedCalls
   * 立即付款
   * 增值服務

   為節省時間，您還可以複製和貼上現有子表單以建立新子表單。

   要轉換 **圖表** 在「費用」子窗體右側的子窗體中，選擇 **圖表** 從左窗格中，選擇 **佈局** 頁籤，並指定 **錨X** 的子菜單。 值必須大於 **寬度** 的 **費用** 的子菜單。 選擇 **費用** 並選擇 **佈局** 的子菜單。 **寬度** 的子菜單。

1. 拖放 **文本** 對象 **對象庫** 輸入 **撥打XXXX以訂閱** 的子菜單。
1. 按一下右鍵左窗格中的文本對象，選擇 **更名對象**，並輸入文本對象的名稱 **訂閱**。

   ![XDP模板](assets/print_xdp_template_subform_new.png)

1. 選擇 **檔案** > **另存為** 將檔案保存到本地檔案系統：

   1. 導航到要保存檔案的位置並指定名稱為 **create_first_ic_print_template**。
   1. 選擇 **.xdp** 從 **另存為類型** 的子菜單。

   1. 點擊 **保存**。

### 將XDP模板上載到AEM Forms伺服器 {#upload-xdp-template-to-the-aem-forms-server}

使用Forms設計器建立XDP模板後，必須將其上載到AEM Forms伺服器，以便在建立交互通信時使用該模板。

1. 選擇 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 點擊 **建立** > **檔案上載**。

   導航並選擇 **create_first_ic_print_template** 模板(XDP)和點擊 **開啟** 將XDP模板導入到AEM Forms伺服器。

### 為佈局片段建立XDP模板 {#create-xdp-template-for-layout-fragments}

要為交互通信的打印通道建立佈局片段，請使用Forms設計器建立XDP並將其上載到AEM Forms伺服器。

1. 開啟Forms設計器，選擇 **檔案** > **新建** > **使用空白表格，** 點擊 **下一個**，然後按一下 **完成** 開啟表單以建立模板。

   確保 **對象庫** 和 **對象** 選項 **窗口** 的子菜單。

1. 拖放 **表格** 元件 **對象庫** 的下界。
1. 在「插入表」對話框中：

   1. 將列數指定為 **5**。
   1. 將正文行數指定為 **1**。
   1. 選擇 **在表中包括標題行** 複選框。
   1. 頁籤 **確定**。

1. 點擊 **+** 在左側窗格中， **表格** 1並按一下右鍵 **細胞1** 選擇 **更名對象** 至 **日期**。

   同樣，更名 **細胞2**。 **細胞3**。 **細胞4**, **細胞5** 至 **時間**。 **數字**。 **持續時間**, **費用** 分別進行。

1. 按一下 **設計器視圖** 並將其更名 **時間**。 **數字**。 **持續時間**, **費用**。

   ![佈局片段](assets/layout_fragment_print_new.png)

1. 選擇 **第1行** 從左窗格中選擇 **對象** > **綁定** > **為每個資料項重複行**。

   ![重複佈局片段的屬性](assets/layout_fragment_print_repeat_new.png)

1. 拖放 **文本欄位** 元件 **對象庫** 到 **設計器視圖**。

   ![佈局片段的文本欄位](assets/layout_fragment_print_text_field_new.png)

   同樣，拖放 **文本欄位** 元件 **時間**。 **數字**。 **持續時間**, **費用** 行。

1. 選擇 **檔案** > **另存為** 將檔案保存到本地檔案系統：

   1. 導航到要保存檔案的位置並指定名稱為 **表_lf**。
   1. 選擇 **.xdp** 從 **另存為類型** 的子菜單。

   1. 點擊 **保存**。
   使用Forms設計器為佈局片段建立XDP模板後，必須 [上載](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) 將其發送到AEM Forms伺服器，以便在建立佈局片段時可使用該模板。

## 為Web通道建立模板 {#create-template-for-web-channel}

使用以下任務為交互通信的Web通道建立和管理模板：

* [為模板建立資料夾](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [建立模板](../../forms/using/create-templates-print-web.md#create-the-template)
* [啟用模板](../../forms/using/create-templates-print-web.md#enable-the-template)
* [在交互通信中啟用按鈕](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 為模板建立資料夾 {#create-folder-for-templates}

要建立Web通道模板，請定義一個資料夾，可在其中保存建立的模板。 在該資料夾內建立模板後，啟用該模板以允許表單用戶基於該模板建立互動式通信的Web通道。

執行以下步驟為可編輯模板建立資料夾：

1. 點擊 **工具** ![錘子表徵圖](assets/hammer-icon.svg) > **配置瀏覽器**。
   * 查看 [配置瀏覽器](/help/sites-administering/configurations.md) 的子菜單。
1. 在「配置瀏覽器」頁中，按一下 **建立**。
1. 在 **建立配置** 對話框，指定 **建立_第一_IC_模板** 作為資料夾的標題，選中 **可編輯模板**，然後點擊 **建立**。

   ![配置Web模板](assets/create_first_ic_web_template_new.png)

   的 **建立_第一_IC_模板** 資料夾已建立並列在 **配置瀏覽器** 的子菜單。

### 建立模板 {#create-the-template}

基於 [用例](/help/forms/using/create-your-first-interactive-communication.md) 和 [解剖](/help/forms/using/planning-interactive-communications.md)，在Web模板中建立以下面板：

* 帳單詳細資訊：包括文檔片段
* 客戶詳細資訊：包括文檔片段
* 清單摘要：包括文檔片段
* 費用匯總：包括文檔片段和圖表（雙列佈局）
* 明細調用：包括表
* 立即支付：包括 **立即支付** 按鈕和影像
* 增值服務：包括影像和 **訂閱** 按鈕

![create_web_template](assets/create_web_template.gif)

建立交互通信時，會添加所有實體，如文檔片段、圖表、表、影像和按鈕。

執行以下步驟，為 **建立_第一_IC_模板** 資料夾：

1. 通過選擇 **工具** > **模板** > **建立_第一_IC_模板** 的子菜單。
1. 點擊 **建立**。
1. 在 **選擇模板類型** 配置嚮導，選擇 **互動式通信 — Web通道** 點擊 **下一個**。
1. 在 **模板詳細資訊** 配置嚮導，指定 **Create_First_IC_Web_Template** 的子菜單。 指定可選說明並點擊 **建立**。

   確認消息： **Create_First_IC_Web_Template** 的上界。

1. 點擊 **開啟** 開啟模板編輯器中的模板。
1. 選擇 **初始內容** 從 **預覽** 的雙曲餘切值。

   ![範本編輯器](assets/template_editor_initial_content_new.png)

1. 點擊 **根面板** 然後點擊 **+** 查看可添加到模板的元件清單。
1. 選擇 **面板** 從清單中添加面板 **根面板**。
1. 選擇 **內容** 的子菜單。 在步驟8中添加的新面板顯示在 **根面板** 的子菜單。

   ![內容樹](assets/content_tree_root_panel_new.png)

1. 選擇面板並點擊 ![configure_icon](assets/configure_icon.png) （配置）。
1. 在「屬性」窗格中：

   1. 指定 **開單詳細資訊** 的子菜單。
   1. 指定 **清單詳細資訊** 的子菜單。
   1. 選擇 **1** 從 **列數** 的子菜單。

   1. 點擊 ![](/help/forms/using/assets/done_icon.png) 的子菜單。

   面板的名稱將更新為 **清單詳細資訊** 的子菜單。

1. 重複步驟7 - 11將具有以下屬性的面板添加到模板：

   | 名稱 | 標題 | 欄數 |
   |---|---|---|
   | customerdetails（客戶詳細資訊） | 客戶詳細資訊 | 1 |
   | 開單匯總 | 清單摘要 | 1 |
   | 匯總費用 | 費用匯總 | 2 |
   | 特米斯呼叫 | 明細調用 | 1 |
   | 付款 | 立即支付 | 2 |
   | 增值服務 | 增值服務 | 1 |

   下圖顯示了將所有面板添加到模板後的內容樹：

   ![所有面板的內容樹](assets/content_tree_all_panels_new.png)

### 啟用模板 {#enable-the-template}

建立Web模板後，必須使其在建立交互通信時使用模板。

執行以下步驟以啟用Web模板：

1. 點擊 **工具** ![錘子表徵圖](assets/hammer-icon.svg) > **模板**。
1. 導航到 **Create_First_IC_Web_Template** 模板，選擇它，然後點擊 **啟用**。
1. 頁籤 **啟用** 確認。

   模板已啟用，其狀態顯示為「已啟用」。 您可以在為Web通道建立交互通信時使用此模板。

### 在交互通信中啟用按鈕 {#enabling-buttons-in-interactive-communications}

根據使用案例，必須包括 **立即支付** 和 **訂閱** 按鈕（自適應窗體元件）。 要在交互通信中啟用這些按鈕，請執行以下步驟：

1. 選擇 **結構** 從 **預覽** 的雙曲餘切值。
1. 選擇 **文檔容器** 使用內容樹並點擊的根面板 **策略** 選擇允許在交互通信中使用的元件。

   ![配置策略](assets/structure_configure_policy_new.png)

1. 在 **允許的元件** 頁籤 **屬性** 選擇 **按鈕** 從 **自適應窗體** 元件。

   ![允許的元件](assets/allowed_components_af_new.png)

1. 點擊 ![完成表徵圖](assets/done_icon.png) 的子菜單。
