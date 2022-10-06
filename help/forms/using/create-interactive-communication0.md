---
title: 「教學課程：建立互動式通訊「
seo-title: Create an Interactive Communication for Print and Web
description: 使用所有構成要素建立互動式通訊
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

# 教學課程：建立互動式通訊 {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

本教學課程是 [建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md) 系列。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

在您為Web版本建立了所有構成塊（如表單資料模型、文檔片段、模板和主題）後，您就可以開始建立互動式通信。

互動式通訊可透過兩個通道提供：打印和Web。 您也可以建立以「打印」通道作為主資訊的互動式通信。 Web頻道的打印為主選項可確保從打印頻道派生Web頻道的內容、繼承和資料綁定。 它還確保在打印通道中所做的更改在Web通道中同步。 不過，互動式通訊作者可中斷網路通道中特定元件的繼承。

本教學課程會逐步帶您了解為列印和網頁頻道建立互動式通訊的步驟。 在本教學課程結束時，您將能夠：

* 為打印通道建立互動式通信
* 為Web通道建立互動式通信
* 以Print as Master建立打印和Web交互通信

## 建立無同步的打印和Web互動式通信 {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 建立打印通道的互動式通信 {#create-interactive-communication-for-print-channel}

以下是本教學課程中已建立且在為列印管道建立互動式通訊時所需的資源清單：

**打印模板：** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**表單資料模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文檔片段：** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**版面片段：** [table_lf](../../forms/using/create-templates-print-web.md)

**影像：** PayNow和ValueAddedServices

1. 登入AEM製作例項並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **建立** 選取 **互動式通訊**. 此 **建立互動式通訊** 嚮導。
1. 指定 **create_first_ic** 在 **標題** 和 **名稱** 欄位。 選擇 **FDM_Create_First_IC** 表單資料模型並點選 **下一個**.
1. 在 **管道** 嚮導：

   1. 指定 **create_first_ic_print_template** 作為「打印」模板並點選 **選擇**. 確保 **使用打印作為Web通道的主版** 未選取核取方塊。

   1. 指定 **Create_First_IC_templates** 資料夾> **Create_First_IC_Web_Template** 作為Web模板並點選 **選擇**.

   1. 點選 **建立**.

   將顯示一條確認消息，說明已成功建立互動式通信。

1. 點選 **編輯** 以開啟右窗格中的「互動式通訊」。
1. 前往 **資產** 頁簽，然後應用篩選器以在左窗格中僅顯示文檔片段。
1. 在互動式通訊中，將下列檔案片段拖放至其目標區域：

   | 文件片段 | 目標區域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 客戶詳細資訊 |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | 費用 |

   ![互動式通訊的檔案片段](assets/create_first_ic_doc_fragments_new.png)

1. 點選 **圖表** 目標區域，然後點選 **+** 新增 **圖表** 元件。
1. 點選圖表元件並選取 ![configure_icon](assets/configure_icon.png) （配置）。 圖表屬性顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 選擇 **派** 從 **圖表類型** 下拉式清單。
   1. 選取 **呼叫類型** 屬性 **呼叫** 資料模型物件類型，位於 **X軸** 區段。 點選 ![done_icon](assets/done_icon.png).
   1. 選擇 **頻率** 從 **函式** 下拉式清單。
   1. 選取 **呼叫類型** 屬性 **呼叫** 資料模型物件類型，位於 **Y軸** 區段。 點選 ![done_icon](assets/done_icon.png).
   1. 點選 ![done_icon](assets/done_icon.png) 以保存圖表屬性。

1. 前往 **資產** 標籤，然後套用篩選器以在左窗格中僅顯示版面片段。 拖放 **table_lf** 配置片段到 **逐項呼叫** 目標區域。
1. 選取 **日期** 欄和點選 ![configure_icon](assets/configure_icon.png) （配置）。
1. 選擇 **資料模型物件** 從 **綁定類型** 下拉式清單並選取 **呼叫** > **呼叫日期**. 點選 ![done_icon](assets/done_icon.png) 儲存屬性兩次。

   同樣地，使用建立綁定 **呼叫時間**, **呼叫數**, **配置**，和 **呼叫費** 中的文字欄位 **時間**, **數字**, **持續時間**，和 **費用** 欄。

1. 點選 **PayNow** 目標區域，然後點選 **+** 若要新增 **影像** 元件。
1. 點選「影像」元件並選取 ![configure_icon](assets/configure_icon.png) （配置）。 影像屬性會顯示在左窗格中：

   1. 指定 **PayNow** 作為 **名稱** 欄位。
   1. 點選 **上傳**，選擇保存在本地檔案系統上的影像，然後點選 **開啟**.
   1. 點選 ![done_icon](assets/done_icon.png) 以儲存影像屬性。

1. 重複步驟13和14以新增 **ValueAddedServices** 影像 **ValueAddedServices** 目標區域。

### 為Web通道建立互動式通信 {#create-interactive-communication-for-web-channel}

以下是本教學課程中已建立且為Web通道建立互動式通訊時所需的資源清單：

**網路模板：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**表單資料模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文檔片段：** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**影像：** PayNowWeb和ValueAddedServicesWeb

1. 登入AEM製作例項並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **建立** 選取 **互動式通訊**. 此 **建立互動式通訊** 嚮導。
1. 指定 **create_first_ic** 在 **標題** 和 **名稱** 欄位。 選擇 **FDM_Create_First_IC** 表單資料模型並點選 **下一個**.
1. 在 **管道** 嚮導：

   1. 指定 **create_first_ic_print_template** 作為「打印」模板並點選 **選擇**. 確保 **使用打印作為Web通道的主版** 未選取核取方塊。

   1. 指定 **Create_First_IC_templates** 資料夾> **Create_First_IC_Web_Template** 作為Web模板並點選 **選擇**.

   1. 點選 **建立**.

   將顯示一條確認消息，說明已成功建立互動式通信。

1. 點選 **編輯** 以開啟右窗格中的「互動式通訊」。
1. 點選 **管道** 標籤，然後點選 **Web**.
1. 前往 **資產** 頁簽，然後應用篩選器以在左窗格中僅顯示文檔片段。
1. 在互動式通訊中，將下列檔案片段拖放至其目標區域：

   | 文件片段 | 目標區域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 客戶詳細資訊 |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | 費用 |

1. 點選 **費用匯總** 目標區域，然後點選 **+** 新增 **圖表** 元件。
1. 點選圖表元件並選取 ![configure_icon](assets/configure_icon.png) （配置）。 圖表屬性顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 選擇 **派** 從 **圖表類型** 下拉式清單。

   1. 選取 **呼叫類型** 屬性 **呼叫** 資料模型物件類型，位於 **X軸** 區段。 點選 ![done_icon](assets/done_icon.png).

   1. 選擇 **頻率** 從 **函式** 下拉式清單。

   1. 選取 **呼叫類型** 屬性 **呼叫** 資料模型物件類型，位於 **Y軸** 區段。 點選 ![done_icon](assets/done_icon.png).

   1. 點選 ![done_icon](assets/done_icon.png) 以保存圖表屬性。

1. 選取 **資料來源** 標籤，並拖放 **呼叫** 資料模型物件 **逐項呼叫** 目標區域。 中的所有屬性 **呼叫** 資料模型對象在中顯示為表列 **逐項呼叫** 目標區域。

   根據使用案例，您需要表中的「呼叫日期」、「呼叫時間」、「呼叫號碼」、「呼叫持續時間」和「呼叫費用」列。

   ![互動式通訊表格](assets/table_ic_web_new.png)

1. 選擇 **Mobilenum** 表列標題和選擇 **更多選項** > **刪除欄**. 同樣地，請刪除 **呼叫類型** 欄。
1. 選取 **呼叫日期** 表格欄標題和點選 ![編輯](assets/edit.png) （編輯）將文字重新命名為 **通話日期**. 同樣地，更名表中的其他列標題。
1. 根據使用案例，插入 **立即支付** 按鈕，該按鈕為用戶提供通過按鈕進行付款的選項。 執行下列步驟以插入按鈕：

   1. 點選 **立即支付** 目標區域，然後點選 **+** 新增 **文字** 元件。

   1. 點選文字元件並點選 ![編輯](assets/edit.png) （編輯）。
   1. 將文字重新命名為 **立即支付**.
   1. 選取文字，然後點選「超連結」圖示。
   1. 在 **路徑** 欄位。
   1. 選擇 **新標籤** 從 **目標** 下拉式清單。

   1. 點選 ![done_icon](assets/done_icon.png) 以保存超連結屬性。

1. 選擇 **樣式** 從 **預覽** 選項。

   ![選擇互動式通信的樣式模式](assets/select_style_ic_web_new.png)

1. 使用以下步驟設定超連結文本的樣式，以將其顯示為「互動式通信」中的按鈕：

   1. 點選文字元件並選取 ![編輯](assets/edit.png) （編輯）。
   1. 在 **邊框** 區段，指定 **1.5px** as **邊框寬度**，選取 **實心** as **邊框樣式**，指定 **46px** as **邊框半徑**.

   1. 從「 」中選取「紅色」作為按鈕的背景顏色 **背景** 區段。
   1. 在 **利潤** 欄位 **Dimension與位置** 區段，點選 **同時編輯** ，然後設定 **右** 邊界 **450px**. 頂端、底部和左側欄位設為空白。

   ![在交互通信中插入超連結](assets/ic_web_hyperlink_new.png)

1. 點選 **立即支付** 目標區域，然後點選 **+** 若要新增 **影像** 元件。
1. 點選「影像」元件並選取 ![configure_icon](assets/configure_icon.png) （配置）。 影像屬性會顯示在左窗格中：

   1. 指定 **PayNow** 作為 **名稱** 欄位。

   1. 點選 **上傳**，請選取 **PayNowWeb** 儲存在本機檔案系統上的影像，然後點選 **開啟**.

   1. 點選 ![done_icon](assets/done_icon.png) 以儲存影像屬性。

1. 根據使用案例，插入 **訂閱** 按鈕，該按鈕通過按鈕為用戶提供訂購增值服務的選項。

   重複步驟13 - 17以新增 **訂閱** 按鈕 **增值服務** 目標區域並新增 **ValueAddedServicesWeb** 影像。

## 使用自動同步建立用於打印和Web的互動式通信 {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

您也可以啟用打印和Web通道之間的自動同步，以建立互動式通信。 要啟用自動同步，請在建立交互通信時選擇打印為主選項。 選擇「打印為主版」選項可確保從打印通道派生Web通道的內容、繼承和資料綁定。 它還可確保在「列印」管道所做的變更反映在Web管道中。

執行下列步驟以衍生使用列印頻道的網頁頻道內容：

1. 登入AEM製作例項並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **建立** 選取 **互動式通訊**. 此 **建立互動式通訊** 嚮導。
1. 指定 **create_first_ic** 在 **標題** 和 **名稱** 欄位。 選擇 **FDM_Create_First_IC** 表單資料模型並點選 **下一個**.
1. 在 **管道** 嚮導：

   1. 指定 **create_first_ic_print_template** 作為「打印」模板並點選 **選擇**.

   1. 選取 **使用打印作為Web通道的主版** 核取方塊。
   1. 指定 **Create_First_IC_templates** 資料夾> **Create_First_IC_Web_Template** 作為Web模板並點選 **選擇**.

   1. 點選 **建立**.

   將顯示一條確認消息，說明已成功建立互動式通信。

1. 點選 **編輯** 以開啟右窗格中的「互動式通訊」。
1. 執行步驟6 - 15，共 [建立打印通道的互動式通信](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) 區段。
1. 點選 **管道** 標籤，然後點選 **Web** 從「打印」頻道自動生成Web頻道的內容。
1. 作為 **使用打印作為Web通道的主版** 在步驟4中選中複選框，從「打印」頻道自動為Web頻道生成內容和綁定。

   打印頻道內容插入到Web頻道模板內容的下方。 若要修改已從列印頻道自動產生的網頁頻道內容，您可以取消任何目標區域的繼承。

   將滑鼠指標暫留在Web頻道中的相關目標區域上，然後選取 ![取消繼承](assets/cancelinheritance.png) （取消繼承），然後在 **取消繼承** 對話框，點選 **是**.

   ![取消繼承](assets/cancel_inheritance_web_channel_new.png)

   如果已取消元件的繼承，則可重新啟用它。 若要重新啟用繼承，請將滑鼠移至相關目標區域（包括元件）的邊界上，然後點選 ![重新啟用繼承](assets/reenableinheritance.png).

1. 選取 **內容** 頁簽。
1. 使用內容樹狀結構，將自動產生的網頁頻道內容拖放至網頁範本中的現有面板。 以下是需要重新排列的元件清單：

   * 清單詳細資訊元件至清單詳細資訊面板
   * 客戶詳細資訊元件至「客戶詳細資訊」面板
   * 清單匯總元件至清單匯總面板
   * 「費用匯總」元件至「費用匯總」面板
   * 配置片段（表格）至「分項呼叫」面板

   ![Web內容樹](assets/ic_web_content_tree_new.png)

1. 重複步驟13 - 18 [為Web通道建立互動式通信](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) 插入 **立即支付** 和 **訂閱** 互動式通訊的Web通道中的超連結。
