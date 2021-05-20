---
title: 「教學課程：建立互動式通訊「
seo-title: 建立用於打印和Web的互動式通信
description: 使用所有構成要素建立互動式通訊
seo-description: 使用所有構成要素建立互動式通訊
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: 互動式通訊
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---

# 教學課程：建立交互通信{#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

本教學課程是[建立第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md)系列中的步驟。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

在您為Web版本建立了所有構成塊（如表單資料模型、文檔片段、模板和主題）後，您就可以開始建立互動式通信。

互動式通訊可透過兩個通道提供：打印和Web。 您也可以建立以「打印」通道作為主資訊的互動式通信。 Web頻道的打印為主選項可確保從打印頻道派生Web頻道的內容、繼承和資料綁定。 它還確保在打印通道中所做的更改在Web通道中同步。 不過，互動式通訊作者可中斷網路通道中特定元件的繼承。

本教學課程會逐步帶您了解為列印和網頁頻道建立互動式通訊的步驟。 在本教學課程結束時，您將能夠：

* 為打印通道建立互動式通信
* 為Web通道建立互動式通信
* 以Print as Master建立打印和Web交互通信

## 建立不同步的打印和Web交互通信{#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 建立打印通道的交互通信{#create-interactive-communication-for-print-channel}

以下是本教學課程中已建立且在為列印管道建立互動式通訊時所需的資源清單：

**打印模板：** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**表單資料模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文檔片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**版面片段：** [table_lf](../../forms/using/create-templates-print-web.md)

**影像：** PayNow和ValueAddedServices

1. 登入AEM製作例項，並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 點選&#x200B;**Create**&#x200B;並選取&#x200B;**Interactive Communication**。 將顯示&#x200B;**建立交互通信**&#x200B;嚮導。
1. 在&#x200B;**Title**&#x200B;和&#x200B;**Name**&#x200B;欄位中指定&#x200B;**create_first_ic**。 選擇「**FDM_Create_First_IC**」作為「表單資料模型」，然後點選「**Next**」。
1. 在&#x200B;**通道**&#x200B;嚮導中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;作為「打印」模板，然後點選&#x200B;**選擇**。 確保未選中&#x200B;**使用打印作為Web通道的主版**&#x200B;複選框。

   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;資料夾> **Create_First_IC_Web_Template**&#x200B;作為Web模板，然後點選&#x200B;**Select**。

   1. 點選&#x200B;**建立**。

   將顯示一條確認消息，說明已成功建立互動式通信。

1. 點選&#x200B;**編輯**&#x200B;以開啟右窗格中的互動式通訊。
1. 前往&#x200B;**Assets**&#x200B;標籤，並套用篩選器以在左窗格中僅顯示檔案片段。
1. 在互動式通訊中，將下列檔案片段拖放至其目標區域：

   | 文件片段 | 目標區域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 客戶詳細資訊 |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | 費用 |

   ![互動式通訊的檔案片段](assets/create_first_ic_doc_fragments_new.png)

1. 點選「**Charts** 」目標區域，然後點選「 **+** 」以新增「 **Chart**」元件。
1. 點選圖表元件，然後選取![configure_icon](assets/configure_icon.png)（設定）。 圖表屬性顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 從&#x200B;**圖表類型**&#x200B;下拉清單中選擇&#x200B;**餅圖**。
   1. 從&#x200B;**X軸**&#x200B;區段的&#x200B;**calls**&#x200B;資料模型物件類型中，選取&#x200B;**calltype**&#x200B;屬性。 點選![done_icon](assets/done_icon.png)。
   1. 從&#x200B;**函式**&#x200B;下拉清單中選擇&#x200B;**頻率**。
   1. 在&#x200B;**Y軸**&#x200B;區段中，從&#x200B;**calls**&#x200B;資料模型物件類型中選取&#x200B;**calltype**&#x200B;屬性。 點選![done_icon](assets/done_icon.png)。
   1. 點選![done_icon](assets/done_icon.png)以儲存圖表屬性。

1. 前往&#x200B;**Assets**&#x200B;標籤，並套用篩選器以在左窗格中僅顯示版面片段。 拖放&#x200B;**table_lf**&#x200B;版面片段至&#x200B;**逐項呼叫**&#x200B;目標區域。
1. 選擇&#x200B;**Date**&#x200B;欄中的「文本欄位」，然後點選![configure_icon](assets/configure_icon.png)(Configure)。
1. 從&#x200B;**綁定類型**&#x200B;下拉清單中選擇&#x200B;**資料模型對象**，然後選擇&#x200B;**調用** > **調用**。 點選![done_icon](assets/done_icon.png)兩次以儲存屬性。

   同樣，為&#x200B;**Time**、**Number**、**callnumber**、**callduration**&#x200B;和&#x200B;**callcharges**&#x200B;中的文本欄位建立綁定，分別針對&#x200B;**Time**、**Number、** Duration **和&lt;a14/**&#x200B;列。

1. 點選&#x200B;**PayNow**&#x200B;目標區域，然後點選&#x200B;**+**&#x200B;以新增&#x200B;**Image**&#x200B;元件。
1. 點選「影像」元件，然後選取![configure_icon](assets/configure_icon.png)(Configure)。 影像屬性會顯示在左窗格中：

   1. 在&#x200B;**名稱**&#x200B;欄位中，將&#x200B;**PayNow**&#x200B;指定為影像名稱。
   1. 點選「**Upload**」，選取儲存在本機檔案系統上的影像，然後點選「**Open**」。
   1. 點選![done_icon](assets/done_icon.png)以儲存影像屬性。

1. 重複步驟13和14以將&#x200B;**ValueAddedServices**&#x200B;影像添加到&#x200B;**ValueAddedServices**&#x200B;目標區域。

### 為Web通道建立互動式通信{#create-interactive-communication-for-web-channel}

以下是本教學課程中已建立且為Web通道建立互動式通訊時所需的資源清單：

**Web模板：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**表單資料模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文檔片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**影像：** PayNowWeb和ValueAddedServicesWeb

1. 登入AEM製作例項，並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 點選&#x200B;**Create**&#x200B;並選取&#x200B;**Interactive Communication**。 將顯示&#x200B;**建立交互通信**&#x200B;嚮導。
1. 在&#x200B;**Title**&#x200B;和&#x200B;**Name**&#x200B;欄位中指定&#x200B;**create_first_ic**。 選擇「**FDM_Create_First_IC**」作為「表單資料模型」，然後點選「**Next**」。
1. 在&#x200B;**通道**&#x200B;嚮導中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;作為「打印」模板，然後點選&#x200B;**選擇**。 確保未選中&#x200B;**使用打印作為Web通道的主版**&#x200B;複選框。

   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;資料夾> **Create_First_IC_Web_Template**&#x200B;作為Web模板，然後點選&#x200B;**Select**。

   1. 點選&#x200B;**建立**。

   將顯示一條確認消息，說明已成功建立互動式通信。

1. 點選&#x200B;**編輯**&#x200B;以開啟右窗格中的互動式通訊。
1. 從左窗格點選&#x200B;**頻道**&#x200B;標籤，然後點選&#x200B;**Web**。
1. 前往&#x200B;**Assets**&#x200B;標籤，並套用篩選器以在左窗格中僅顯示檔案片段。
1. 在互動式通訊中，將下列檔案片段拖放至其目標區域：

   | 文件片段 | 目標區域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 客戶詳細資訊 |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | 費用 |

1. 點選「**費用摘要**」目標區域，然後點選「**+**」以新增「**Chart**」元件。
1. 點選圖表元件，然後選取![configure_icon](assets/configure_icon.png)（設定）。 圖表屬性顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 從&#x200B;**圖表類型**&#x200B;下拉清單中選擇&#x200B;**餅圖**。

   1. 從&#x200B;**X軸**&#x200B;區段的&#x200B;**calls**&#x200B;資料模型物件類型中，選取&#x200B;**calltype**&#x200B;屬性。 點選![done_icon](assets/done_icon.png)。

   1. 從&#x200B;**函式**&#x200B;下拉清單中選擇&#x200B;**頻率**。

   1. 在&#x200B;**Y軸**&#x200B;區段中，從&#x200B;**calls**&#x200B;資料模型物件類型中選取&#x200B;**calltype**&#x200B;屬性。 點選![done_icon](assets/done_icon.png)。

   1. 點選![done_icon](assets/done_icon.png)以儲存圖表屬性。

1. 從左窗格中選擇&#x200B;**Data Sources**&#x200B;標籤，並將&#x200B;**calls**&#x200B;資料模型物件拖放至&#x200B;**Itemized Calls**&#x200B;目標區域。 **calls**&#x200B;資料模型對象中的所有屬性在右窗格的&#x200B;**Itemized Calls**&#x200B;目標區域中顯示為表列。

   根據使用案例，您需要表中的「呼叫日期」、「呼叫時間」、「呼叫號碼」、「呼叫持續時間」和「呼叫費用」列。

   ![互動式通訊表格](assets/table_ic_web_new.png)

1. 選擇&#x200B;**Mobilenum**&#x200B;表列標題，然後選擇&#x200B;**更多選項** > **刪除列**。 同樣地，請刪除&#x200B;**Calltype**&#x200B;列。
1. 選擇&#x200B;**Calldate**&#x200B;表列標題，然後點選![edit](assets/edit.png)(Edit)，將文本更名為&#x200B;**Call Date**。 同樣地，更名表中的其他列標題。
1. 根據使用案例，在「交互通信」中插入&#x200B;**立即支付**&#x200B;按鈕，該按鈕通過按一下按鈕為用戶提供付款選項。 執行下列步驟以插入按鈕：

   1. 點選&#x200B;**立即付費**&#x200B;目標區域，然後點選&#x200B;**+**&#x200B;以新增&#x200B;**文字**&#x200B;元件。

   1. 點選文字元件，然後點選![edit](assets/edit.png)（編輯）。
   1. 將文字重新命名為&#x200B;**立即支付**。
   1. 選取文字，然後點選「超連結」圖示。
   1. 在&#x200B;**Path**&#x200B;欄位中指定付款URL。
   1. 從&#x200B;**Target**&#x200B;下拉式清單中選取&#x200B;**新增標籤**。

   1. 點選![done_icon](assets/done_icon.png)以儲存超連結屬性。

1. 從&#x200B;**預覽**&#x200B;選項旁的下拉清單中選擇&#x200B;**樣式**。

   ![選擇互動式通信的樣式模式](assets/select_style_ic_web_new.png)

1. 使用以下步驟設定超連結文本的樣式，以將其顯示為「互動式通信」中的按鈕：

   1. 點選文字元件並選取![edit](assets/edit.png)（編輯）。
   1. 在&#x200B;**邊框**&#x200B;部分中，將&#x200B;**1.5px**&#x200B;指定為&#x200B;**邊框寬度**，選擇&#x200B;**Solid**&#x200B;為&#x200B;**邊框樣式**，並將&#x200B;**46px**&#x200B;指定為&#x200B;**邊框半徑**。

   1. 從&#x200B;**Background**&#x200B;部分選擇紅色作為按鈕的背景顏色。
   1. 在&#x200B;**Margin**&#x200B;欄位(**Dimension與位置**)區段中，點選&#x200B;**Edit montiwle**&#x200B;圖示，並將&#x200B;**Right**&#x200B;邊界設為&#x200B;**450px**。 頂端、底部和左側欄位設為空白。

   ![在交互通信中插入超連結](assets/ic_web_hyperlink_new.png)

1. 點選&#x200B;**立即付費**&#x200B;目標區域，然後點選&#x200B;**+**&#x200B;以新增&#x200B;**影像**&#x200B;元件。
1. 點選「影像」元件，然後選取![configure_icon](assets/configure_icon.png)(Configure)。 影像屬性會顯示在左窗格中：

   1. 在&#x200B;**名稱**&#x200B;欄位中，將&#x200B;**PayNow**&#x200B;指定為影像名稱。

   1. 點選「**Upload**」，選取儲存在本機檔案系統上的「**PayNowWeb**」影像，然後點選「**Open**」。

   1. 點選![done_icon](assets/done_icon.png)以儲存影像屬性。

1. 根據使用案例，在交互通信中插入&#x200B;**訂閱**&#x200B;按鈕，該按鈕通過按一下按鈕為用戶提供訂購增值服務的選項。

   重複步驟13 - 17，將&#x200B;**訂閱**&#x200B;按鈕添加到&#x200B;**增值服務**&#x200B;目標區域並添加&#x200B;**增值服務Web**&#x200B;影像。

## 使用自動同步{#create-interactive-communications-for-print-and-web-with-auto-synchronization}建立用於打印和Web的交互通信

您也可以啟用打印和Web通道之間的自動同步，以建立互動式通信。 要啟用自動同步，請在建立交互通信時選擇打印為主選項。 選擇「打印為主版」選項可確保從打印通道派生Web通道的內容、繼承和資料綁定。 它還可確保在「列印」管道中所做的變更反映在Web管道中。

執行下列步驟以衍生使用列印頻道的網頁頻道內容：

1. 登入AEM製作例項，並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 點選&#x200B;**Create**&#x200B;並選取&#x200B;**Interactive Communication**。 將顯示&#x200B;**建立交互通信**&#x200B;嚮導。
1. 在&#x200B;**Title**&#x200B;和&#x200B;**Name**&#x200B;欄位中指定&#x200B;**create_first_ic**。 選擇「**FDM_Create_First_IC**」作為「表單資料模型」，然後點選「**Next**」。
1. 在&#x200B;**通道**&#x200B;嚮導中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;作為「打印」模板，然後點選&#x200B;**選擇**。

   1. 選中&#x200B;**使用打印作為Web通道的主框**&#x200B;複選框。
   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;資料夾> **Create_First_IC_Web_Template**&#x200B;作為Web模板，然後點選&#x200B;**Select**。

   1. 點選&#x200B;**建立**。

   將顯示一條確認消息，說明已成功建立互動式通信。

1. 點選&#x200B;**編輯**&#x200B;以開啟右窗格中的互動式通訊。
1. 執行[建立用於打印通道的互動式通信部分的步驟6 - 15。](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel)
1. 從左窗格點選&#x200B;**頻道**&#x200B;標籤，然後點選&#x200B;**Web**&#x200B;以從列印頻道自動產生Web頻道的內容。
1. 由於在步驟4中選中了&#x200B;**使用打印作為Web頻道的主複選框**，因此從打印頻道自動為Web頻道生成內容和綁定。

   打印頻道內容插入到Web頻道模板內容的下方。 若要修改已從列印頻道自動產生的網頁頻道內容，您可以取消任何目標區域的繼承。

   暫留在Web通道中的相關目標區域上，選擇![取消繼承](assets/cancelinheritance.png)（取消繼承），然後在&#x200B;**取消繼承**&#x200B;對話方塊中，點選&#x200B;**是**。

   ![取消繼承](assets/cancel_inheritance_web_channel_new.png)

   如果已取消元件的繼承，則可重新啟用它。 若要重新啟用繼承，請將滑鼠移至包括元件的相關目標區域的邊界上，然後點選![重新啟用繼承](assets/reenableinheritance.png)。

1. 在左窗格中選擇&#x200B;**Content**&#x200B;頁簽。
1. 使用內容樹狀結構，將自動產生的網頁頻道內容拖放至網頁範本中的現有面板。 以下是需要重新排列的元件清單：

   * 清單詳細資訊元件至清單詳細資訊面板
   * 客戶詳細資訊元件至「客戶詳細資訊」面板
   * 清單匯總元件至清單匯總面板
   * 「費用匯總」元件至「費用匯總」面板
   * 配置片段（表格）至「分項呼叫」面板

   ![Web內容樹](assets/ic_web_content_tree_new.png)

1. 重複[為Web通道](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel)建立互動式通信的步驟13 - 18，以在互動式通信的Web通道中插入&#x200B;**立即支付**&#x200B;和&#x200B;**訂閱**&#x200B;超連結。
