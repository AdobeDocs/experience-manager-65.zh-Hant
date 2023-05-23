---
title: 「教程：建立交互通信"
seo-title: Create an Interactive Communication for Print and Web
description: 使用所有構建塊建立互動式通信
seo-description: Create an Interactive Communication using all building blocks
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 0%

---

# 教程：建立互動式通信 {#tutorial-create-interactive-communication}

![09樣式自適應形式小](assets/09-style-your-adaptive-form-small.png)

本教程是 [建立您的第一個互動式通信](/help/forms/using/create-your-first-interactive-communication.md) 的下界。 建議按時間順序按系列進行操作，以瞭解、執行和演示完整的教程使用案例。

建立了Web版本的所有構建塊（如表單資料模型、文檔片段、模板和主題）後，可以開始建立互動式通信。

互動式通信可以通過兩種渠道進行：打印和Web。 還可以建立以打印通道為主的互動式通信。 作為Web頻道的主選項打印可確保Web頻道的內容、繼承和資料綁定是從打印頻道派生的。 它還確保在打印通道中所做的更改在Web通道中同步。 但是，允許交互通信作者中斷Web通道中特定元件的繼承。

本教程將指導您完成為打印和Web通道建立互動式通信的步驟。 在本教程的結束時，您將能夠：

* 為打印通道建立互動式通信
* 為Web通道建立互動式通信
* 建立以打印為主的打印和Web交互通信

## 建立無同步的打印和Web交互通信 {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 為打印通道建立互動式通信 {#create-interactive-communication-for-print-channel}

以下是本教程中已建立的、在為打印通道建立互動式通信時需要的資源清單：

**打印模板：** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**表單資料模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文檔片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_cherges_first_ic](../../forms/using/create-document-fragments.md)

**佈局片段：** [表_lf](../../forms/using/create-templates-print-web.md)

**影像：** PayNow和ValueAddedServices

1. 登錄到作AEM者實例並導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 點擊 **建立** 選擇 **互動式通信**。 的 **建立互動式通信** 的上界。
1. 指定 **create_first_ic** 的 **標題** 和 **名稱** 的子菜單。 選擇 **FDM_Create_First_IC** 表單資料模型並點擊 **下一個**。
1. 在 **頻道** 嚮導：

   1. 指定 **create_first_ic_print_template** 打印模板並點擊 **選擇**。 確保 **將打印作為Web通道的首頁** 複選框。

   1. 指定 **建立_第一_IC_模板** 資料夾> **Create_First_IC_Web_Template** 作為Web模板並點擊 **選擇**。

   1. 點擊 **建立**。

   將顯示一條確認消息，表明已成功建立交互通信。

1. 點擊 **編輯** 開啟右窗格中的「互動式通信」。
1. 轉到 **資產** 頁籤，然後應用篩選器以僅顯示左窗格中的文檔片段。
1. 在交互通信中將以下文檔片段拖放到其目標區域：

   | 文件片段 | 目標區域 |
   |---|---|
   | bill_details_first_ic | 帳單詳細資訊 |
   | customer_details_first_ic | 客戶詳細資訊 |
   | bill_summary_first_ic | 清單摘要 |
   | summary_charges_first_interactive_communication | 費用 |

   ![用於互動式通信的文檔片段](assets/create_first_ic_doc_fragments_new.png)

1. 點擊 **圖表** 目標區域，並點擊 **+** 添加 **圖表** 元件。
1. 點擊圖表元件並選擇 ![configure_icon](assets/configure_icon.png) （配置）。 圖表屬性顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 選擇 **餅** 從 **圖表類型** 的子菜單。
   1. 選擇 **調用類型** 屬性 **呼叫** 資料模型對象類型 **X軸** 的子菜單。 點擊 ![完成表徵圖](assets/done_icon.png)。
   1. 選擇 **頻率** 從 **函式** 的子菜單。
   1. 選擇 **調用類型** 屬性 **呼叫** 資料模型對象類型 **Y軸** 的子菜單。 點擊 ![完成表徵圖](assets/done_icon.png)。
   1. 點擊 ![完成表徵圖](assets/done_icon.png) 按鈕。

1. 轉到 **資產** 頁籤，然後應用篩選器以僅顯示左窗格中的佈局片段。 拖放 **表_lf** 佈局片段到 **明細調用** 目標區域。
1. 選擇 **日期** 列和點擊 ![configure_icon](assets/configure_icon.png) （配置）。
1. 選擇 **資料模型對象** 從 **綁定類型** 下拉清單並選擇 **呼叫** > **調用日期**。 點擊 ![完成表徵圖](assets/done_icon.png) 保存屬性。

   同樣，建立與 **調用時間**。 **呼叫號**。 **調用**, **催繳費** 中的文本欄位 **時間**。 **數字**。 **持續時間**, **費用** 列。

1. 點擊 **立即付款** 目標區域，並點擊 **+** 添加 **影像** 元件。
1. 按一下「Image（影像）」元件並選擇 ![configure_icon](assets/configure_icon.png) （配置）。 影像屬性顯示在左窗格中：

   1. 指定 **立即付款** 作為 **名稱** 的子菜單。
   1. 點擊 **上載**，選擇保存在本地檔案系統上的映像，然後點擊 **開啟**。
   1. 點擊 ![完成表徵圖](assets/done_icon.png) 的子菜單。

1. 重複步驟13和14以添加 **增值服務** 影像到 **增值服務** 目標區域。

### 為Web通道建立交互通信 {#create-interactive-communication-for-web-channel}

以下是本教程中已建立的、在為Web通道建立交互通信時需要的資源清單：

**Web模板：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**表單資料模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文檔片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_cherges_first_ic](../../forms/using/create-document-fragments.md)

**影像：** PayNowWeb和ValueAddedServicesWeb

1. 登錄到作AEM者實例並導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 點擊 **建立** 選擇 **互動式通信**。 的 **建立互動式通信** 的上界。
1. 指定 **create_first_ic** 的 **標題** 和 **名稱** 的子菜單。 選擇 **FDM_Create_First_IC** 表單資料模型並點擊 **下一個**。
1. 在 **頻道** 嚮導：

   1. 指定 **create_first_ic_print_template** 打印模板並點擊 **選擇**。 確保 **將打印作為Web通道的首頁** 複選框。

   1. 指定 **建立_第一_IC_模板** 資料夾> **Create_First_IC_Web_Template** 作為Web模板並點擊 **選擇**。

   1. 點擊 **建立**。

   將顯示一條確認消息，表明已成功建立交互通信。

1. 點擊 **編輯** 開啟右窗格中的「互動式通信」。
1. 點擊 **頻道** 頁籤，然後點擊 **Web**。
1. 轉到 **資產** 頁籤，然後應用篩選器以僅顯示左窗格中的文檔片段。
1. 在交互通信中將以下文檔片段拖放到其目標區域：

   | 文件片段 | 目標區域 |
   |---|---|
   | bill_details_first_ic | 帳單詳細資訊 |
   | customer_details_first_ic | 客戶詳細資訊 |
   | bill_summary_first_ic | 清單摘要 |
   | summary_charges_first_interactive_communication | 費用 |

1. 點擊 **費用匯總** 目標區域，並點擊 **+** 添加 **圖表** 元件。
1. 點擊圖表元件並選擇 ![configure_icon](assets/configure_icon.png) （配置）。 圖表屬性顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 選擇 **餅** 從 **圖表類型** 的子菜單。

   1. 選擇 **調用類型** 屬性 **呼叫** 資料模型對象類型 **X軸** 的子菜單。 點擊 ![完成表徵圖](assets/done_icon.png)。

   1. 選擇 **頻率** 從 **函式** 的子菜單。

   1. 選擇 **調用類型** 屬性 **呼叫** 資料模型對象類型 **Y軸** 的子菜單。 點擊 ![完成表徵圖](assets/done_icon.png)。

   1. 點擊 ![完成表徵圖](assets/done_icon.png) 按鈕。

1. 選擇 **資料源** 的子菜單。 **呼叫** 資料模型對象到 **明細調用** 目標區域。 中的所有屬性 **呼叫** 資料模型對象顯示為表列 **明細調用** 目標區域。

   根據使用情況，您需要表中的「呼叫日期」、「呼叫時間」、「呼叫號碼」、「呼叫持續時間」和「呼叫費用」列。

   ![互動式通信表](assets/table_ic_web_new.png)

1. 選擇 **移動枚舉** 表列標題和選擇 **更多選項** > **刪除列**。 同樣，刪除 **調用類型** 的雙曲餘切值。
1. 選擇 **調用日期** 表列標題和點擊 ![編輯](assets/edit.png) （編輯）將文本更名為 **呼叫日期**。 同樣，更名表中的其他列標題。
1. 根據使用案例，插入 **立即支付** 的子菜單。 執行以下步驟以插入按鈕：

   1. 點擊 **立即支付** 目標區域，並點擊 **+** 添加 **文本** 元件。

   1. 點擊文本元件並點擊 ![編輯](assets/edit.png) （編輯）。
   1. 將文本更名為 **立即支付**。
   1. 選擇文本並點擊「超連結」表徵圖。
   1. 在中指定付款URL **路徑** 的子菜單。
   1. 選擇 **新建頁籤** 從 **目標** 的子菜單。

   1. 點擊 ![完成表徵圖](assets/done_icon.png) 的子菜單。

1. 選擇 **樣式** 從 **預覽** 的雙曲餘切值。

   ![選擇互動式通信的樣式模式](assets/select_style_ic_web_new.png)

1. 使用以下步驟，對超連結文本進行樣式化，以將其顯示為交互通信中的按鈕：

   1. 點擊文本元件並選擇 ![編輯](assets/edit.png) （編輯）。
   1. 在 **邊框** 部分，指定 **1.5像素** 如 **邊框寬度**&#x200B;選中 **實心** 如 **邊框樣式**，指定 **46px** 如 **邊框半徑**。

   1. 選擇「紅色」作為按鈕的背景顏色 **背景** 的子菜單。
   1. 在 **邊距** 欄位 **Dimension和職位** ，按一下 **同時編輯** ，然後設定 **右** 邊距 **450px**。 「頂部」(Top)、「底部」(Bottom)和「左側」(Left)欄位設定為空。

   ![在交互通信中插入超連結](assets/ic_web_hyperlink_new.png)

1. 點擊 **立即支付** 目標區域，並點擊 **+** 添加 **影像** 元件。
1. 按一下「Image（影像）」元件並選擇 ![configure_icon](assets/configure_icon.png) （配置）。 影像屬性顯示在左窗格中：

   1. 指定 **立即付款** 作為 **名稱** 的子菜單。

   1. 點擊 **上載**，選擇 **立即付費** 本地檔案系統上保存的映像，然後點擊 **開啟**。

   1. 點擊 ![完成表徵圖](assets/done_icon.png) 的子菜單。

1. 根據使用案例，插入 **訂閱** 的子菜單。

   重複步驟13 - 17以添加 **訂閱** 按鈕 **增值服務** 目標區域並添加 **增值服務Web** 影像。

## 使用自動同步建立用於打印和Web的交互通信 {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

還可以通過啟用打印通道和Web通道之間的自動同步來建立互動式通信。 要啟用自動同步，請在建立交互通信時選擇「打印為主」選項。 選擇「打印為主」選項可確保Web頻道的內容、繼承和資料綁定是從打印頻道派生的。 它還確保在打印通道中所做的更改反映在Web通道中。

執行以下步驟，使用「打印」頻道獲取Web頻道內容：

1. 登錄到作AEM者實例並導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 點擊 **建立** 選擇 **互動式通信**。 的 **建立互動式通信** 的上界。
1. 指定 **create_first_ic** 的 **標題** 和 **名稱** 的子菜單。 選擇 **FDM_Create_First_IC** 表單資料模型並點擊 **下一個**。
1. 在 **頻道** 嚮導：

   1. 指定 **create_first_ic_print_template** 打印模板並點擊 **選擇**。

   1. 選擇 **將打印作為Web通道的首頁** 複選框。
   1. 指定 **建立_第一_IC_模板** 資料夾> **Create_First_IC_Web_Template** 作為Web模板並點擊 **選擇**。

   1. 點擊 **建立**。

   將顯示一條確認消息，表明已成功建立交互通信。

1. 點擊 **編輯** 開啟右窗格中的「互動式通信」。
1. 執行步驟6 - 15 [為打印通道建立互動式通信](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) 的子菜單。
1. 點擊 **頻道** 頁籤，然後點擊 **Web** 從打印頻道為Web頻道自動生成內容。
1. 作為 **將打印作為Web通道的首頁** 複選框，內容和綁定將自動從「打印」頻道為Web頻道生成。

   打印頻道內容被插入到Web頻道模板內容的下方。 要修改從打印頻道自動生成的Web頻道內容，可以取消任何目標區域的繼承。

   將滑鼠懸停在Web通道中的相關目標區域上並選擇 ![取消繼承](assets/cancelinheritance.png) （取消繼承），然後 **取消繼承** 對話框，點擊 **是**。

   ![取消繼承](assets/cancel_inheritance_web_channel_new.png)

   如果已取消對元件的繼承，則可以重新啟用它。 要重新啟用繼承，請將滑鼠懸停在相關目標區域的邊界上，然後點擊 ![重新啟用繼承](assets/reenableinheritance.png)。

1. 選擇 **內容** 的子菜單。
1. 使用內容樹將自動生成的Web頻道內容拖放到Web模板中的現有面板。 以下是需要重新排列的元件清單：

   * 「清單詳細資訊」元件至「清單詳細資訊」面板
   * 「客戶詳細資訊」元件至「客戶詳細資訊」面板
   * 清單匯總元件至清單匯總面板
   * 「費用元件匯總至費用匯總」面板
   * 「明細調用」面板的佈局片段（表）

   ![Web內容樹](assets/ic_web_content_tree_new.png)

1. 重複步驟13 - 18 [為Web通道建立交互通信](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) 的子菜單。 **立即支付** 和 **訂閱** 交互通信的Web通道中的超連結。
