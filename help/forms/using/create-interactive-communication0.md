---
title: 「教學課程：建立互動式通訊」
description: 使用所有建置區塊建立互動式通訊
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# 教學課程：建立互動式通訊 {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

此教學課程是[建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md)系列中的步驟。 建議您依照序列時間順序來瞭解、執行和示範完整的教學課程使用案例。

一旦您建立了Web版本的所有建置區塊（例如表單資料模型、檔案片段、範本和主題），您就可以開始建立互動式通訊。

互動式通訊可透過兩種通道提供：列印和網路。 您也可以建立以Print channel為主體的互動式通訊。 Web channel的「列印為主版」選項可確保Web channel的內容、繼承和資料繫結衍生自Print channel。 它也能確保在Print channel中所做的變更在Web channel中同步。 不過，互動式通訊作者可在Web channel中中斷特定元件的繼承。

本教學課程將逐步引導您完成為列印和Web管道建立互動式通訊的步驟。 在本教學課程結束時，您將能夠：

* 為列印管道建立互動式通訊
* 建立Web channel的互動式通訊
* 以Print as Master建立列印和Web互動式通訊

## 建立列印與網頁的互動式通訊，無需同步處理 {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 為列印管道建立互動式通訊 {#create-interactive-communication-for-print-channel}

以下是已在本教學課程中建立且在建立Print channel的互動式通訊時所需的資源清單：

**列印範本：** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**表單資料模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**檔案片段：** [bill_details_first_ic， customer_details_first_ic， bill_summary_first_ic， summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**佈局片段：** [table_lf](../../forms/using/create-templates-print-web.md)

**影像：** PayNow與ValueAddedServices

1. 登入AEM作者執行個體並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。
1. 選取&#x200B;**建立**&#x200B;並選取&#x200B;**互動式通訊**。 顯示&#x200B;**建立互動式通訊**&#x200B;精靈。
1. 在&#x200B;**Title**&#x200B;和&#x200B;**Name**&#x200B;欄位中指定&#x200B;**create_first_ic**。 選取&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，並選取&#x200B;**下一步**。
1. 在&#x200B;**管道**&#x200B;精靈中：

   1. 將&#x200B;**create_first_ic_print_template**&#x200B;指定為列印範本，並選取&#x200B;**選取**。 確保未選取&#x200B;**Web Channel的[使用列印為主版]**&#x200B;核取方塊。

   1. 將&#x200B;**Create_First_IC_templates**&#x200B;資料夾> **Create_First_IC_Web_Template**&#x200B;指定為Web範本，並選取&#x200B;**選取**。

   1. 選取「**建立**」。

   系統會顯示確認訊息，指出已成功建立互動式通訊。

1. 選取&#x200B;**編輯**&#x200B;以在右窗格中開啟互動式通訊。
1. 移至&#x200B;**Assets**&#x200B;索引標籤並套用篩選，以在左窗格中僅顯示檔案片段。
1. 將下列檔案片段拖放至互動式通訊中的目標區域：

   | 文件片段 | 目標區域 |
   |---|---|
   | bill_details_first_ic | 帳單詳細資訊 |
   | customer_details_first_ic | 客戶詳細資料 |
   | bill_summary_first_ic | 帳單摘要 |
   | summary_charges_first_interactive_communication | 費用 |

   ![互動式通訊的檔案片段](assets/create_first_ic_doc_fragments_new.png)

1. 選取&#x200B;**圖表**&#x200B;目標區域，並選取&#x200B;**+**&#x200B;以新增&#x200B;**圖表**&#x200B;元件。
1. 選取圖表元件，然後選取![configure_icon](assets/configure_icon.png) （設定）。 圖表屬性會顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 從&#x200B;**圖表型別**&#x200B;下拉式清單中選取&#x200B;**圓形圖**。
   1. 從&#x200B;**X軸**&#x200B;區段中的&#x200B;**calls**&#x200B;資料模型物件型別中選取&#x200B;**calltype**&#x200B;屬性。 選取![完成圖示](assets/done_icon.png)。
   1. 從&#x200B;**函式**&#x200B;下拉式清單中選取&#x200B;**頻率**。
   1. 從&#x200B;**Y軸**&#x200B;區段中的&#x200B;**calls**&#x200B;資料模型物件型別中選取&#x200B;**calltype**&#x200B;屬性。 選取![完成圖示](assets/done_icon.png)。
   1. 選取![done_icon](assets/done_icon.png)以儲存圖表屬性。

1. 前往&#x200B;**Assets**&#x200B;索引標籤並套用篩選器，以在左窗格中僅顯示佈局片段。 將&#x200B;**table_lf**&#x200B;佈局片段拖放至&#x200B;**分項呼叫**&#x200B;目標區域。
1. 選取&#x200B;**Date**&#x200B;欄中的[文字欄位]並選取![configure_icon](assets/configure_icon.png) （設定）。
1. 從&#x200B;**繫結型別**&#x200B;下拉式清單中選取&#x200B;**資料模型物件**，然後選取&#x200B;**呼叫** > **呼叫日期**。 選取![done_icon](assets/done_icon.png)兩次，以儲存屬性。

   同樣地，針對&#x200B;**Time**、**Number**、**Duration**&#x200B;和&#x200B;**Charges**&#x200B;欄中的文字欄位，分別建立具有&#x200B;**calltime**、**callnumber**、**callduration**&#x200B;和&#x200B;**callcharges**&#x200B;的繫結。

1. 選取&#x200B;**PayNow**&#x200B;目標區域，並選取&#x200B;**+**&#x200B;以新增&#x200B;**Image**&#x200B;元件。
1. 選取影像元件，然後選取![configure_icon](assets/configure_icon.png) (Configure)。 影像屬性會顯示在左窗格中：

   1. 在&#x200B;**Name**&#x200B;欄位中指定&#x200B;**PayNow**&#x200B;作為影像的名稱。
   1. 選取&#x200B;**上傳**，選取儲存在本機檔案系統上的影像，然後選取&#x200B;**開啟**。
   1. 選取![done_icon](assets/done_icon.png)以儲存影像屬性。

1. 重複步驟13和14，將&#x200B;**ValueAddedServices**&#x200B;影像新增至&#x200B;**ValueAddedServices**&#x200B;目標區域。

### 建立Web channel的互動式通訊 {#create-interactive-communication-for-web-channel}

以下是已在本教學課程中建立且在建立Web channel的互動式通訊時所需的資源清單：

**網頁範本：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**表單資料模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**檔案片段：** [bill_details_first_ic， customer_details_first_ic， bill_summary_first_ic， summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**影像：** PayNowWeb和ValueAddedServicesWeb

1. 登入AEM作者執行個體並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。
1. 選取&#x200B;**建立**&#x200B;並選取&#x200B;**互動式通訊**。 顯示&#x200B;**建立互動式通訊**&#x200B;精靈。
1. 在&#x200B;**Title**&#x200B;和&#x200B;**Name**&#x200B;欄位中指定&#x200B;**create_first_ic**。 選取&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，並選取&#x200B;**下一步**。
1. 在&#x200B;**管道**&#x200B;精靈中：

   1. 將&#x200B;**create_first_ic_print_template**&#x200B;指定為列印範本，並選取&#x200B;**選取**。 確保未選取&#x200B;**Web Channel的[使用列印為主版]**&#x200B;核取方塊。

   1. 將&#x200B;**Create_First_IC_templates**&#x200B;資料夾> **Create_First_IC_Web_Template**&#x200B;指定為Web範本，並選取&#x200B;**選取**。

   1. 選取「**建立**」。

   系統會顯示確認訊息，指出已成功建立互動式通訊。

1. 選取&#x200B;**編輯**&#x200B;以在右窗格中開啟互動式通訊。
1. 從左窗格中選取&#x200B;**管道**&#x200B;標籤，然後選取&#x200B;**網頁**。
1. 移至&#x200B;**Assets**&#x200B;索引標籤並套用篩選，以在左窗格中僅顯示檔案片段。
1. 將下列檔案片段拖放至互動式通訊中的目標區域：

   | 文件片段 | 目標區域 |
   |---|---|
   | bill_details_first_ic | 帳單詳細資訊 |
   | customer_details_first_ic | 客戶詳細資料 |
   | bill_summary_first_ic | 帳單摘要 |
   | summary_charges_first_interactive_communication | 費用 |

1. 選取&#x200B;**費用摘要**&#x200B;目標區域，並選取&#x200B;**+**&#x200B;以新增&#x200B;**圖表**&#x200B;元件。
1. 選取圖表元件，然後選取![configure_icon](assets/configure_icon.png) （設定）。 圖表屬性會顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 從&#x200B;**圖表型別**&#x200B;下拉式清單中選取&#x200B;**圓形圖**。

   1. 從&#x200B;**X軸**&#x200B;區段中的&#x200B;**calls**&#x200B;資料模型物件型別中選取&#x200B;**calltype**&#x200B;屬性。 選取![完成圖示](assets/done_icon.png)。

   1. 從&#x200B;**函式**&#x200B;下拉式清單中選取&#x200B;**頻率**。

   1. 從&#x200B;**Y軸**&#x200B;區段中的&#x200B;**calls**&#x200B;資料模型物件型別中選取&#x200B;**calltype**&#x200B;屬性。 選取![完成圖示](assets/done_icon.png)。

   1. 選取![done_icon](assets/done_icon.png)以儲存圖表屬性。

1. 從左窗格選取&#x200B;**資料來源**&#x200B;標籤，並將&#x200B;**呼叫**&#x200B;資料模型物件拖放至&#x200B;**分項呼叫**&#x200B;目標區域。 **呼叫**&#x200B;資料模型物件中的所有屬性都會顯示為右窗格中&#x200B;**分項呼叫**&#x200B;目標區域中的資料表資料行。

   根據使用案例，您需要在表格中建立「通話日期」、「通話時間」、「通話號碼」、「通話持續時間」和「通話費用」欄。

   互動式通訊的![資料表](assets/table_ic_web_new.png)

1. 選取&#x200B;**Mobilenum**&#x200B;資料表資料行標題，然後選取&#x200B;**其他選項** > **刪除資料行**。 同樣地，刪除&#x200B;**Calltype**&#x200B;資料行。
1. 選取&#x200B;**Calldate**&#x200B;資料表資料行標題並選取![編輯](assets/edit.png) （編輯）以將文字重新命名為&#x200B;**呼叫日期**。 同樣地，重新命名表格中的其他欄標題。
1. 根據使用案例，在互動式通訊中插入&#x200B;**立即付款**&#x200B;按鈕，使用者可透過按一下按鈕選擇付款。 執行以下步驟來插入按鈕：

   1. 選取&#x200B;**立即付款**&#x200B;目標區域，並選取&#x200B;**+**&#x200B;以新增&#x200B;**文字**&#x200B;元件。

   1. 選取文字元件並選取![編輯](assets/edit.png) （編輯）。
   1. 將文字重新命名為&#x200B;**立即付款**。
   1. 選取文字並選取「超連結」圖示。
   1. 在&#x200B;**路徑**&#x200B;欄位中指定付款URL。
   1. 從&#x200B;**Target**&#x200B;下拉式清單中選取&#x200B;**新索引標籤**。

   1. 選取![done_icon](assets/done_icon.png)以儲存超連結屬性。

1. 從&#x200B;**預覽**&#x200B;選項旁的下拉式清單中選取&#x200B;**樣式**。

   ![選取互動式通訊的樣式模式](assets/select_style_ic_web_new.png)

1. 使用下列步驟，設定超連結文字的樣式，使其在互動式通訊中顯示為按鈕：

   1. 選取文字元件並選取![編輯](assets/edit.png) （編輯）。
   1. 在&#x200B;**邊框**&#x200B;區段中，將&#x200B;**1.5px**&#x200B;指定為&#x200B;**邊框寬度**，選取&#x200B;**實線**&#x200B;作為&#x200B;**邊框樣式**，並將&#x200B;**46px**&#x200B;指定為&#x200B;**邊框半徑**。

   1. 從&#x200B;**背景**&#x200B;區段中選取紅色作為按鈕的背景顏色。
   1. 在&#x200B;**Dimension與位置**&#x200B;區段的&#x200B;**邊界**&#x200B;欄位中，選取&#x200B;**同時編輯**&#x200B;圖示，並將&#x200B;**右側**&#x200B;邊界設定為&#x200B;**450px**。 「上」、「下」和「左」欄位會設為空白。

   ![在互動式通訊中插入超連結](assets/ic_web_hyperlink_new.png)

1. 選取&#x200B;**立即付款**&#x200B;目標區域，並選取&#x200B;**+**&#x200B;以新增&#x200B;**Image**&#x200B;元件。
1. 選取影像元件，然後選取![configure_icon](assets/configure_icon.png) (Configure)。 影像屬性會顯示在左窗格中：

   1. 在&#x200B;**Name**&#x200B;欄位中指定&#x200B;**PayNow**&#x200B;作為影像的名稱。

   1. 選取&#x200B;**上傳**，選取儲存在本機檔案系統上的&#x200B;**PayNowWeb**&#x200B;影像，然後選取&#x200B;**開啟**。

   1. 選取![done_icon](assets/done_icon.png)以儲存影像屬性。

1. 根據使用案例，在互動式通訊中插入&#x200B;**訂閱**&#x200B;按鈕，使用者可透過按一下按鈕選擇訂閱加值服務。

   重複步驟13至17，將&#x200B;**訂閱**&#x200B;按鈕新增至&#x200B;**加值服務**&#x200B;目標區域，並新增&#x200B;**ValueAddedServicesWeb**&#x200B;影像。

## 使用自動同步處理建立列印與Web的互動式通訊 {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

您也可以透過啟用列印和Web通道之間的自動同步來建立互動式通訊。 若要啟用自動同步化，請在建立互動式通訊時選取「列印為主版」選項。 選取「列印為主版」選項，可確保Web channel的內容、繼承和資料繫結衍生自Print channel。 它也能確保在列印管道中所做的變更反映在網頁管道中。

執行以下步驟，衍生使用Print channel的Web channel內容：

1. 登入AEM作者執行個體並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。
1. 選取&#x200B;**建立**&#x200B;並選取&#x200B;**互動式通訊**。 顯示&#x200B;**建立互動式通訊**&#x200B;精靈。
1. 在&#x200B;**Title**&#x200B;和&#x200B;**Name**&#x200B;欄位中指定&#x200B;**create_first_ic**。 選取&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，並選取&#x200B;**下一步**。
1. 在&#x200B;**管道**&#x200B;精靈中：

   1. 將&#x200B;**create_first_ic_print_template**&#x200B;指定為列印範本，並選取&#x200B;**選取**。

   1. 選取&#x200B;**使用Web Channel的[列印為主版]**&#x200B;核取方塊。
   1. 將&#x200B;**Create_First_IC_templates**&#x200B;資料夾> **Create_First_IC_Web_Template**&#x200B;指定為Web範本，並選取&#x200B;**選取**。

   1. 選取「**建立**」。

   系統會顯示確認訊息，指出已成功建立互動式通訊。

1. 選取&#x200B;**編輯**&#x200B;以在右窗格中開啟互動式通訊。
1. 執行[為列印通道](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel)區段建立互動式通訊的步驟6至15。
1. 從左窗格選取&#x200B;**管道**&#x200B;標籤，並選取&#x200B;**Web**&#x200B;以從Print channel自動產生Web channel的內容。
1. 由於已在步驟4中選取&#x200B;**使用Print as Master for Web Channel**&#x200B;核取方塊，因此內容和繫結會從Print channel自動產生Web channel。

   列印管道內容會插入Web channel範本內容下方。 若要修改已從列印管道自動產生的Web channel內容，您可以取消任何目標區域的繼承。

   將游標停留在Web Channel的相關目標區域上，並選取![取消繼承](assets/cancelinheritance.png) （取消繼承），然後在&#x200B;**取消繼承**&#x200B;對話方塊中，選取&#x200B;**是**。

   ![取消繼承](assets/cancel_inheritance_web_channel_new.png)

   如果您已取消元件的繼承，則可重新啟用它。 若要重新啟用繼承，請將游標停留在相關目標區域（包含元件）的邊界上，然後選取![reenableinheritance](assets/reenableinheritance.png)。

1. 在左窗格中選取&#x200B;**Content**&#x200B;標籤。
1. 使用內容樹將自動產生的Web channel內容拖放到Web範本中的現有面板。 以下是需要重新排列的元件清單：

   * 「用料表詳細資訊」面板的「用料表詳細資訊」元件
   * 「客戶詳細資料」面板的「客戶詳細資料」元件
   * 「用料表彙總」面板的「用料表彙總」元件
   * 「費用彙總」元件至「費用彙總」面板
   * 將片段（表格）配置到分項呼叫面板

   ![網頁內容樹狀結構](assets/ic_web_content_tree_new.png)

1. 重複步驟13 - 18 （共[個）建立Web管道的互動式通訊](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel)，以將&#x200B;**立即付款**&#x200B;和&#x200B;**訂閱**&#x200B;超連結插入互動式通訊的Web管道中。
