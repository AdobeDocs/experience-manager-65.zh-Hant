---
title: 「教學課程：建立互動式通訊"
seo-title: 建立適用於印刷品與網頁的互動式通訊
description: 使用所有建置區塊建立互動式通訊
seo-description: 使用所有建置區塊建立互動式通訊
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: 互動式通訊
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---


# 教學課程：建立互動式通信{#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

本教學課程是[建立您第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md)系列中的步驟。 建議依序依序依序排列，以瞭解、執行和展示完整的教學課程使用案例。

一旦您建立了Web版本的所有建置區塊，例如表單資料模型、檔案片段、範本和主題，就可以開始建立互動式通訊。

互動式通訊可透過兩個通道提供：印刷與網頁。 您也可以以主版的方式建立互動式的列印通訊管道。 列印為網頁頻道的主選項，可確保網頁頻道的內容、繼承和資料系結是從列印頻道衍生而來。 此外，還可確保在列印頻道中所做的變更在網頁頻道中同步。 不過，「互動式通訊」作者可以中斷Web頻道中特定元件的繼承。

本教學課程將逐步帶您建立適用於印刷和網路頻道的互動式通訊。 在本教學課程結束時，您將能夠：

* 建立適用於列印頻道的互動式通訊
* 建立適用於網路頻道的互動式通訊
* 以印刷為主的方式建立印刷與網路互動式通訊

## 建立用於打印和Web的互動式通信，而不進行同步{#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 建立適用於列印頻道的互動式通訊{#create-interactive-communication-for-print-channel}

以下是本教學課程中已建立且建立列印頻道互動式通訊時所需的資源清單：

**列印範本：** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**表單資料模** [型：FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文檔片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**版面片段：** [table_lf](../../forms/using/create-templates-print-web.md)

**影像：** PayNow和ValueAddedServices

1. 登入作AEM者例項並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 點選「**建立**」並選取「互動式通訊&#x200B;**」。**&#x200B;將顯示&#x200B;**建立互動式通信**&#x200B;嚮導。
1. 在&#x200B;**Title**&#x200B;和&#x200B;**Name**&#x200B;欄位中指定&#x200B;**create_first_ic**。 選擇&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，然後按一下&#x200B;**Next**。
1. 在&#x200B;**頻道**&#x200B;精靈中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;為「列印」範本，然後點選&#x200B;**Select**。 確保未選中&#x200B;**使用打印作為Web Channel**&#x200B;複選框。

   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;資料夾> **Create_First_IC_Web_Template**&#x200B;作為Web範本，然後點選&#x200B;**Select**。

   1. 點選&#x200B;**Create**。

   將顯示一條確認消息，表明已成功建立互動式通信。

1. 點選「**編輯**」，在右窗格中開啟「互動式通訊」。
1. 前往&#x200B;**Assets**&#x200B;標籤，並套用篩選器，只顯示左側窗格中的檔案片段。
1. 在「互動式通訊」中將下列檔案片段拖放至其目標區域：

   | 文件片段 | 目標區域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 客戶詳細資訊 |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | 費用 |

   ![互動式通訊的檔案片段](assets/create_first_ic_doc_fragments_new.png)

1. 點選「**Charts**&#x200B;目標區域」，點選「**+**」以新增「Chart **」元件。**
1. 點選圖表元件並選取![configure_icon](assets/configure_icon.png)（設定）。 圖表屬性會顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 從&#x200B;**圖表類型**&#x200B;下拉式清單中選擇&#x200B;**餅圖**。
   1. 在&#x200B;**X軸**&#x200B;區段中，從&#x200B;**calls**&#x200B;資料模型對象類型中選擇&#x200B;**calltype**&#x200B;屬性。 點選![done_icon](assets/done_icon.png)。
   1. 從&#x200B;**函式**&#x200B;下拉式清單中選擇&#x200B;**頻率**。
   1. 在&#x200B;**Y軸**&#x200B;區段中，從&#x200B;**calls**&#x200B;資料模型對象類型中選擇&#x200B;**calltype**&#x200B;屬性。 點選![done_icon](assets/done_icon.png)。
   1. 點選![done_icon](assets/done_icon.png)以儲存圖表屬性。

1. 前往&#x200B;**Assets**&#x200B;標籤，並套用篩選條件，只顯示左側窗格中的版面片段。 將&#x200B;**table_lf**&#x200B;佈局片段拖放到&#x200B;**項目化呼叫**&#x200B;目標區域。
1. 在&#x200B;**Date**&#x200B;欄中選擇「文字欄位」，然後點選![configure_icon](assets/configure_icon.png)（設定）。
1. 從&#x200B;**綁定類型**&#x200B;下拉清單中選擇&#x200B;**資料模型對象**，並選擇&#x200B;**調用** >調用&#x200B;**調用日期**。 點選兩次![done_icon](assets/done_icon.png)以儲存屬性。

   同樣地，為&#x200B;**Time**、**Number**、**中的文本欄位建立與** calltime **、** callnumber **、** callduration **和** callcharges **綁定2/>持續時間**&#x200B;和&#x200B;**電荷**&#x200B;欄。

1. 點選&#x200B;**PayNow**&#x200B;目標區域，點選&#x200B;**+**&#x200B;以新增&#x200B;**Image**&#x200B;元件。
1. 點選影像元件並選取![configure_icon](assets/configure_icon.png)（設定）。 影像屬性會顯示在左窗格中：

   1. 在&#x200B;**名稱**&#x200B;欄位中，指定&#x200B;**PayNow**&#x200B;作為影像名稱。
   1. 點選「**上傳**」，選取儲存在本機檔案系統上的影像，然後點選「開啟&#x200B;**a3/>」。**
   1. 點選![done_icon](assets/done_icon.png)以儲存影像屬性。

1. 重複步驟13和14，將&#x200B;**ValueAddedServices**&#x200B;映像添加到&#x200B;**ValueAddedServices**&#x200B;目標區域。

### 建立適用於網路頻道的互動式通訊{#create-interactive-communication-for-web-channel}

以下是本教學課程中已建立的、在建立網路頻道互動式通訊時需要的資源清單：

**Web模板：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**表單資料模** [型：FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文檔片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**影像：** PayNowWeb和ValueAddedServicesWeb

1. 登入作AEM者例項並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 點選「**建立**」並選取「互動式通訊&#x200B;**」。**&#x200B;將顯示&#x200B;**建立互動式通信**&#x200B;嚮導。
1. 在&#x200B;**Title**&#x200B;和&#x200B;**Name**&#x200B;欄位中指定&#x200B;**create_first_ic**。 選擇&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，然後按一下&#x200B;**Next**。
1. 在&#x200B;**頻道**&#x200B;精靈中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;為「列印」範本，然後點選&#x200B;**Select**。 確保未選中&#x200B;**使用打印作為Web Channel**&#x200B;複選框。

   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;資料夾> **Create_First_IC_Web_Template**&#x200B;作為Web範本，然後點選&#x200B;**Select**。

   1. 點選&#x200B;**Create**。

   將顯示一條確認消息，表明已成功建立互動式通信。

1. 點選「**編輯**」，在右窗格中開啟「互動式通訊」。
1. 從左窗格點選「**頻道**」標籤，然後點選「**Web**」。
1. 前往&#x200B;**Assets**&#x200B;標籤，並套用篩選器，只顯示左側窗格中的檔案片段。
1. 在「互動式通訊」中將下列檔案片段拖放至其目標區域：

   | 文件片段 | 目標區域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 客戶詳細資訊 |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | 費用 |

1. 點選「**Summary of Charges**」目標區域，點選「**+**」以新增&#x200B;**Chart**&#x200B;元件。
1. 點選圖表元件並選取![configure_icon](assets/configure_icon.png)（設定）。 圖表屬性會顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 從&#x200B;**圖表類型**&#x200B;下拉式清單中選擇&#x200B;**餅圖**。

   1. 在&#x200B;**X軸**&#x200B;區段中，從&#x200B;**calls**&#x200B;資料模型對象類型中選擇&#x200B;**calltype**&#x200B;屬性。 點選![done_icon](assets/done_icon.png)。

   1. 從&#x200B;**函式**&#x200B;下拉式清單中選擇&#x200B;**頻率**。

   1. 在&#x200B;**Y軸**&#x200B;區段中，從&#x200B;**calls**&#x200B;資料模型對象類型中選擇&#x200B;**calltype**&#x200B;屬性。 點選![done_icon](assets/done_icon.png)。

   1. 點選![done_icon](assets/done_icon.png)以儲存圖表屬性。

1. 從左窗格選擇&#x200B;**Data Sources**&#x200B;標籤，並將&#x200B;**calls**&#x200B;資料模型物件拖放至&#x200B;**Itemized Calls**&#x200B;目標區域。 **calls**&#x200B;資料模型對象中的所有屬性在右窗格的&#x200B;**Itemized Calls**&#x200B;目標區域中顯示為表列。

   根據使用案例，您需要表格中的「呼叫日期」、「呼叫時間」、「呼叫號碼」、「呼叫持續時間」和「呼叫費用」欄。

   ![互動式通訊表格](assets/table_ic_web_new.png)

1. 選擇&#x200B;**Mobilenum**&#x200B;表列標題並選擇&#x200B;**更多選項** > **刪除列**。 同樣地，請刪除&#x200B;**Calltype**&#x200B;列。
1. 選擇&#x200B;**呼叫日期**&#x200B;表格欄標題，並點選![edit](assets/edit.png)（編輯），將文字重新命名為&#x200B;**呼叫日期**。 同樣地，請更名表中的其他列標題。
1. 根據使用案例，在「互動式通訊」中插入&#x200B;**立即付費**&#x200B;按鈕，讓使用者可以按一下按鈕來付款。 執行以下步驟以插入按鈕：

   1. 點選&#x200B;**立即付費**&#x200B;目標區域，點選&#x200B;**+**&#x200B;以新增&#x200B;**Text**&#x200B;元件。

   1. 點選文字元件並點選![edit](assets/edit.png)（編輯）。
   1. 將文本更名為&#x200B;**Pay Now**。
   1. 選取文字並點選「超連結」圖示。
   1. 在&#x200B;**路徑**&#x200B;欄位中指定付款URL。
   1. 從&#x200B;**Target**&#x200B;下拉式清單中選擇&#x200B;**新增標籤**。

   1. 點選![done_icon](assets/done_icon.png)以儲存超連結屬性。

1. 從&#x200B;**預覽**&#x200B;選項旁的下拉式清單中選擇&#x200B;**樣式**。

   ![選擇互動式通信的樣式模式](assets/select_style_ic_web_new.png)

1. 使用下列步驟，將超連結文字設為樣式，以便在互動式通訊中顯示為按鈕：

   1. 點選文字元件並選取![edit](assets/edit.png)（編輯）。
   1. 在&#x200B;**Border**&#x200B;區段中，將&#x200B;**1.5px**&#x200B;指定為&#x200B;**Border Width**，選擇&#x200B;**Solid**&#x200B;為&#x200B;**Border Style**，並將&#x200B;**46px**&#x200B;指定為&#x200B;**邊框半徑**。

   1. 從&#x200B;**Background**&#x200B;部分選擇紅色作為按鈕的背景顏色。
   1. 在&#x200B;**Dimension與位置**&#x200B;區段的&#x200B;**邊界**&#x200B;欄位中，點選&#x200B;**同時編輯**&#x200B;圖示，並將&#x200B;**右**&#x200B;邊界設為&#x200B;**450px**。 「頂端」、「底部」和「左側」欄位皆設為空白。

   ![在互動式通訊中插入超連結](assets/ic_web_hyperlink_new.png)

1. 點選&#x200B;**立即付費**&#x200B;目標區域，點選&#x200B;**+**&#x200B;以新增&#x200B;**影像**&#x200B;元件。
1. 點選影像元件並選取![configure_icon](assets/configure_icon.png)（設定）。 影像屬性會顯示在左窗格中：

   1. 在&#x200B;**名稱**&#x200B;欄位中，指定&#x200B;**PayNow**&#x200B;作為影像名稱。

   1. 點選「**上傳**」，選取儲存在本機檔案系統上的&#x200B;**PayNowWeb**&#x200B;影像，然後點選「開啟&#x200B;**a5/>」。**

   1. 點選![done_icon](assets/done_icon.png)以儲存影像屬性。

1. 根據使用案例，在「互動式通訊」中插入&#x200B;**訂閱**&#x200B;按鈕，讓使用者可以按一下按鈕來訂閱增值服務。

   重複步驟13 - 17，將&#x200B;**Subscribe**&#x200B;按鈕添加到&#x200B;**Value Added Services**&#x200B;目標區域並添加&#x200B;**ValueAddedServicesWeb**&#x200B;映像。

## 使用自動同步{#create-interactive-communications-for-print-and-web-with-auto-synchronization}建立用於打印和Web的互動式通信

您也可以啟用列印和網頁頻道之間的自動同步，以建立互動式通訊。 要啟用自動同步，請在建立交互通信時選擇「打印為主版」選項。 選擇「列印為主版」選項可確保從列印頻道衍生出網頁頻道的內容、繼承和資料系結。 此外，還可確保列印管道中所做的變更反映在網頁管道中。

執行下列步驟，使用列印頻道衍生網頁頻道內容：

1. 登入作AEM者例項並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 點選「**建立**」並選取「互動式通訊&#x200B;**」。**&#x200B;將顯示&#x200B;**建立互動式通信**&#x200B;嚮導。
1. 在&#x200B;**Title**&#x200B;和&#x200B;**Name**&#x200B;欄位中指定&#x200B;**create_first_ic**。 選擇&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，然後按一下&#x200B;**Next**。
1. 在&#x200B;**頻道**&#x200B;精靈中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;為「列印」範本，然後點選&#x200B;**Select**。

   1. 選中&#x200B;**使用打印作為Web通道的主程式**&#x200B;複選框。
   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;資料夾> **Create_First_IC_Web_Template**&#x200B;作為Web範本，然後點選&#x200B;**Select**。

   1. 點選&#x200B;**Create**。

   將顯示一條確認消息，表明已成功建立互動式通信。

1. 點選「**編輯**」，在右窗格中開啟「互動式通訊」。
1. 執行[「建立用於打印通道的互動式通信」部分的步驟6 - 15。](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel)
1. 從左窗格點選「**頻道**」標籤，點選「**Web**」，從「列印」頻道自動產生Web頻道的內容。
1. 在步驟4中選中了「使用打印作為Web頻道的主節點」複選框，從打印頻道自動為Web頻道生成內容和綁定。****

   列印頻道內容插入網頁頻道範本內容下方。 若要修改已自動從列印頻道產生的網頁頻道內容，您可以取消任何目標區域的繼承。

   將滑鼠指標暫留在網頁頻道的相關目標區域上，並選取![Cancelihenticate](assets/cancelinheritance.png)（取消繼承），然後在&#x200B;**Cancel Inheritance**&#x200B;對話方塊中，點選&#x200B;**Yes**。

   ![取消繼承](assets/cancel_inheritance_web_channel_new.png)

   如果已取消元件的繼承，可重新啟用它。 若要重新啟用繼承，請將滑鼠指標暫留在包含元件的相關目標區域的邊界上，然後點選![reenablehinetration](assets/reenableinheritance.png)。

1. 在左窗格中選擇&#x200B;**Content**&#x200B;標籤。
1. 使用內容樹狀結構，將自動產生的Web頻道內容拖放至Web範本中的現有面板。 以下是需要重新排列的元件清單：

   * 「清單詳細資訊」元件至「清單詳細資訊」面板
   * 客戶詳細資訊元件到客戶詳細資訊面板
   * 「清單匯總」元件至「清單匯總」面板
   * 「費用元件匯總」至「費用匯總」面板
   * 「項目化呼叫」面板的版面片段（表格）

   ![網頁內容樹狀結構](assets/ic_web_content_tree_new.png)

1. 重複[為Web通道](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel)建立互動式通信的步驟13 - 18，將&#x200B;**Pay Now**&#x200B;和&#x200B;**Subscribe**&#x200B;超連結插入互動式通信的Web通道中。

