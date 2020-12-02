---
title: 「教學課程：建立檔案片段」
seo-title: 建立檔案片段以進行互動式通訊
description: 建立檔案片段以進行互動式通訊
seo-description: 建立檔案片段以進行互動式通訊
uuid: 677d717e-e92e-434e-8266-6fbbf94f3867
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8ae97a21-83af-4615-9be3-61e2f8065081
docset: aem65
translation-type: tm+mt
source-git-commit: e545fc5e2ea139bd8ebb7f84138ba68e03d71d19
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 2%

---


# 教學課程：建立檔案片段{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

本教學課程是[建立您第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md)系列中的步驟。 建議依序依序依序排列，以瞭解、執行和展示完整的教學課程使用案例。

文檔片段是用於構成互動式通信的通信的可重用元件。 檔案片段的類型如下：

* 文字——文字資產是由一或多個文欄位落組成的內容片段。 段落可以是靜態或動態。
* 清單——清單是一組檔案片段，包括文字、清單、條件和影像。
* 條件——條件可讓您根據從表單資料模型接收的資料，定義互動式通訊中包含的內容。

本教學課程將逐步帶您瞭解如何根據[規劃互動式通訊](/help/forms/using/planning-interactive-communications.md)章節中提供的解剖結構，建立多個文字檔案片段。 在本教學課程結束時，您將能夠：

* 建立檔案片段
* 建立變數
* 建立和套用規則

![text_document_fragments](assets/text_document_fragments.gif)

以下是在本教學課程中建立的檔案片段清單：

* [帳單詳細資訊](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [客戶詳細資訊](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [帳單摘要](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [費用匯總](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

每個檔案片段包含含靜態文字的欄位、從表單資料模型接收的資料，以及使用Agent UI輸入的資料。 [規劃互動式通信](/help/forms/using/planning-interactive-communications.md)部分中描述了這些欄位。

在本教學課程中建立檔案片段時，會為使用代理UI接收資料的欄位建立變數。

使用&#x200B;**FDM_Create_First_IC**（如[建立表單資料模型](../../forms/using/create-form-data-model0.md)部分所述）作為表單資料模型，以在本教程中建立文檔片段。

## 步驟1:建立清單詳細資訊文本文檔片段{#step-create-bill-details-text-document-fragment}

「清單詳細資訊」單據分段包含以下欄位：

| 欄位 | 資料來源 |
|---|---|
| 發票編號 | Agent UI |
| 帳單期間 | 代理UI |
| 帳單日期 | 代理UI |
| 您的計畫 | 表單資料模型 |

執行下列步驟，以建立以Agent UI為資料來源之欄位的變數、建立靜態文字，以及在檔案片段中使用表單資料模型元素：

1. 選擇「**[!UICONTROL Forms]** > **[!UICONTROL 文檔片段]**」。

1. 選擇&#x200B;**建立** > **文本**。
1. 指定下列資訊：

   1. 在&#x200B;**Title**&#x200B;欄位中輸入&#x200B;**bill_details_first_ic**&#x200B;作為名稱。 標題會自動填入&#x200B;**名稱**&#x200B;欄位中。

   1. 從&#x200B;**資料模型**&#x200B;部分選擇&#x200B;**表單資料模型**。

   1. 選擇&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，然後按一下&#x200B;**選擇**。

   1. 點選&#x200B;**Next**。

1. 在左窗格中選擇&#x200B;**變數**&#x200B;標籤，然後點選&#x200B;**建立**。
1. 在&#x200B;**建立變數**&#x200B;區段中：

   1. 輸入&#x200B;**發票編號**&#x200B;作為變數的名稱。
   1. 選擇&#x200B;**字串**&#x200B;作為類型。
   1. 點選&#x200B;**Create**。

   ![建立字串類型的變數](assets/variable_create_string_new.png)

   重複步驟4和5以建立下列變數：

   * 開單期間：字串類型
   * BillDate:日期類型

   ![帳單詳細資訊](assets/variable_bill_details_new.png)

1. 使用右窗格建立下列欄位的靜態文字：

   * 發票編號
   * 帳單期間
   * 帳單日期
   * 您的計畫

   ![靜態文字](assets/variable_bill_details_static_text_new.png)

1. 將游標置於&#x200B;**發票編號**&#x200B;欄位旁，並按兩下左窗格中&#x200B;**變數**&#x200B;標籤中的&#x200B;**InvoiceNumber**&#x200B;變數。
1. 將游標置於&#x200B;**帳單期間**&#x200B;欄位旁，並按兩下&#x200B;**帳單期間**&#x200B;變數。
1. 將游標置於&#x200B;**清單日期**&#x200B;欄位旁，並按兩下&#x200B;**清單日期**&#x200B;變數。
1. 在左窗格中選擇&#x200B;**資料模型對象**&#x200B;頁籤。
1. 將游標置於&#x200B;**Your Plan**&#x200B;欄位旁，按兩下&#x200B;**customer** > **customerplan**&#x200B;屬性。

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. 按一下&#x200B;**保存**&#x200B;以建立「清單詳細資訊」文本文檔片段。

## 步驟2:建立客戶詳細資訊文本文檔片段{#step-create-customer-details-text-document-fragment}

Customer Details文檔片段包含以下欄位：

| 欄位 | 資料來源 |
|---|---|
| 客戶名稱 | 表單資料模型 |
| 地址 | 表單資料模型 |
| 供應地點 | 代理UI |
| 州代碼 | 代理UI |
| 行動號碼 | 表單資料模型 |
| 備用聯繫人號碼 | 表單資料模型 |
| 關係編號 | 表單資料模型 |
| 連接數 | 代理UI |

執行下列步驟，以建立以Agent UI為資料來源之欄位的變數、建立靜態文字，以及在檔案片段中使用表單資料模型元素：

1. 選擇「**[!UICONTROL Forms]** > **[!UICONTROL 文檔片段]**」。
1. 選擇&#x200B;**建立** > **文本**。
1. 指定下列資訊：

   1. 在&#x200B;**Title**&#x200B;欄位中輸入&#x200B;**customer_details_first_ic**&#x200B;作為名稱。 標題會自動填入&#x200B;**名稱**&#x200B;欄位中。

   1. 從&#x200B;**資料模型**&#x200B;部分選擇&#x200B;**表單資料模型**。

   1. 選擇&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，然後按一下&#x200B;**選擇**。

   1. 點選&#x200B;**Next**。

1. 在左窗格中選擇&#x200B;**變數**&#x200B;標籤，然後點選&#x200B;**建立**。
1. 在&#x200B;**建立變數**&#x200B;區段中：

   1. 輸入&#x200B;**Placesupply**&#x200B;作為變數的名稱。
   1. 選擇&#x200B;**字串**&#x200B;作為類型。
   1. 點選&#x200B;**Create**。

   重複步驟4和5以建立下列變數：

   * 狀態碼：數字類型
   * 連接數：數字類型


1. 選擇&#x200B;**資料模型對象**&#x200B;頁籤，將游標置於右窗格中，然後按兩下&#x200B;**customer** > **name**&#x200B;屬性。
1. 按Enter鍵將游標移到下一行，然後按兩下&#x200B;**customer** > **address**&#x200B;屬性。
1. 使用右窗格建立下列欄位的靜態文字：

   * 行動號碼
   * 備用聯繫人號碼
   * 供應地點
   * 關係編號
   * 州代碼
   * 連接數

   ![客戶詳細資訊靜態文字](assets/customer_details_static_text_new.png)

1. 將游標置於&#x200B;**Mobile Number**&#x200B;欄位旁，按兩下&#x200B;**customer** > **mobilenum**&#x200B;屬性。
1. 將游標置於&#x200B;**備用聯繫人號碼**&#x200B;欄位旁，按兩下** customer** > **備用mobilenumber**&#x200B;屬性。
1. 將游標置於&#x200B;**關係編號**&#x200B;欄位旁，按兩下&#x200B;**customer** > **關係編號**&#x200B;屬性。
1. 選擇&#x200B;**變數**&#x200B;頁籤，將游標置於&#x200B;**供應地點**&#x200B;欄位旁，並按兩下&#x200B;**供應地點**&#x200B;變數。
1. 將游標置於&#x200B;**狀態代碼**&#x200B;欄位旁，按兩下&#x200B;**狀態代碼**&#x200B;變數。
1. 將游標置於&#x200B;**連接數**&#x200B;欄位旁，並按兩下&#x200B;**數字連接數**&#x200B;變數。

   ![客戶詳細資訊](assets/customer_details_df2_new.png)

1. 按一下&#x200B;**保存**&#x200B;以建立「客戶詳細資訊」文本文檔片段。

## 步驟3:建立清單匯總文本文檔片段{#step-create-bill-summary-text-document-fragment}

「清單匯總」單據片段包括以下欄位：

| 欄位 | 資料來源 |
|---|---|
| 上一餘額 | 代理UI |
| 付款 | 代理UI |
| 調整 | 代理UI |
| 當前帳單期間費用 | 表單資料模型 |
| 到期金額 | 代理UI |
| 到期日期 | 代理UI |

執行下列步驟，以建立以Agent UI為資料來源之欄位的變數、建立靜態文字，以及在檔案片段中使用表單資料模型元素：

1. 選擇「**[!UICONTROL Forms]** > **[!UICONTROL 文檔片段]**」。
1. 選擇&#x200B;**建立** > **文本**。
1. 指定下列資訊：

   1. 在&#x200B;**Title**&#x200B;欄位中輸入&#x200B;**bill_summary_first_ic**&#x200B;作為名稱。 標題會自動填入&#x200B;**名稱**&#x200B;欄位中。

   1. 從&#x200B;**資料模型**&#x200B;部分選擇&#x200B;**表單資料模型**。

   1. 選擇&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，然後按一下&#x200B;**選擇**。

   1. 點選&#x200B;**Next**。

1. 在左窗格中選擇&#x200B;**變數**&#x200B;標籤，然後點選&#x200B;**建立**。
1. 在&#x200B;**建立變數**&#x200B;區段中：

   1. 輸入&#x200B;**前置餘額**&#x200B;作為變數的名稱。
   1. 選擇&#x200B;**Number**&#x200B;作為類型。
   1. 點選&#x200B;**Create**。

   重複步驟4和5以建立下列變數：

   * 付款：數字類型
   * 調整：數字類型
   * 應付金額：數字類型
   * Duedate:日期類型


1. 使用右窗格建立下列欄位的靜態文字：

   * 上一餘額
   * 付款
   * 調整
   * 當前帳單期間費用
   * 到期金額
   * 到期日期
   * 到期日之後的延遲付款費用為$ 20

   ![清單摘要靜態文字](assets/bill_summary_static_new.png)

1. 將游標置於&#x200B;**Previous Balance**&#x200B;欄位旁，並按兩下&#x200B;**Previousbalance**&#x200B;變數。
1. 將游標置於&#x200B;**Payments**&#x200B;欄位旁，並按兩下&#x200B;**Payments**&#x200B;變數。
1. 將游標置於&#x200B;**Adjustments**&#x200B;欄位旁，按兩下&#x200B;**Adjustments**&#x200B;變數。
1. 將游標置於&#x200B;**到期金額**&#x200B;欄位旁，按兩下&#x200B;**到期金額**&#x200B;變數。
1. 將游標置於&#x200B;**到期日**&#x200B;欄位旁，並按兩下&#x200B;**Duedate**&#x200B;變數。
1. 選擇&#x200B;**資料模型對象**&#x200B;頁籤，將游標置於右窗格中的&#x200B;**費用當前開單期間**&#x200B;欄位旁邊，並按兩下&#x200B;**bills** > **usagecharges**&#x200B;屬性。

   ![帳單摘要](assets/bill_summary_static_variables_new.png)

1. 按一下&#x200B;**保存**&#x200B;以建立「客戶詳細資訊」文本文檔片段。

## 步驟4:建立費用摘要文本文檔片段{#step-create-summary-of-charges-text-document-fragment}

費用匯總單據片段包含以下欄位：

| 欄位 | 資料來源 |
|---|---|
| 通話費 | 表單資料模型 |
| 電話會議費用 | 表單資料模型 |
| 簡訊費 | 表單資料模型 |
| 行動網際網路收費 | 表單資料模型 |
| 國家漫遊費用 | 表單資料模型 |
| 國際漫遊費用 | 表單資料模型 |
| 增值服務費用 | 表單資料模型 |
| 費用合計 | 表單資料模型 |
| 應付總額 | 表單資料模型 |

執行以下步驟以建立靜態文本並在文檔片段中使用表單資料模型元素：

1. 選擇「**[!UICONTROL Forms]** > **[!UICONTROL 文檔片段]**」。
1. 選擇&#x200B;**建立** > **文本**。
1. 指定下列資訊：

   1. 在&#x200B;**Title**&#x200B;欄位中輸入&#x200B;**summary_charges_first_ic**&#x200B;作為名稱。 標題會自動填入「名稱」欄位。

   1. 從&#x200B;**資料模型**&#x200B;部分選擇&#x200B;**表單資料模型**。

   1. 選擇&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，然後按一下&#x200B;**選擇**。

   1. 點選&#x200B;**Next**。

1. 使用右窗格建立下列欄位的靜態文字：

   * 通話費
   * 電話會議費用
   * 簡訊費
   * 行動網際網路收費
   * 國家漫遊費用
   * 國際漫遊費用
   * 增值服務費用
   * 費用合計
   * 應付總額

   ![匯總費用](assets/summary_charges_static_new.png)

1. 選擇&#x200B;**資料模型對象**&#x200B;頁籤。
1. 將游標置於&#x200B;**呼叫費用**&#x200B;欄位旁，並按兩下&#x200B;**bills** > **呼叫費用**&#x200B;屬性。
1. 將游標置於&#x200B;**會議呼叫費用**&#x200B;欄位旁，並按兩下&#x200B;**bills** > **confcalcharges**&#x200B;屬性。
1. 將游標置於&#x200B;**SMS Charges**&#x200B;欄位旁，並按兩下&#x200B;**bills** > **smscharges**&#x200B;屬性。
1. 將游標置於&#x200B;**Mobile Internet Charges**&#x200B;欄位旁，並按兩下&#x200B;**bills** > **internetcharges**&#x200B;屬性。
1. 將游標置於&#x200B;**國家漫遊費用**&#x200B;欄位旁，並按兩下&#x200B;**bills** > **國家漫遊費用**&#x200B;屬性。
1. 將游標置於&#x200B;**國際漫遊費用**&#x200B;欄位旁，並按兩下&#x200B;**bills** > **roamingintnl**&#x200B;屬性。
1. 將游標置於&#x200B;**Value Added Services Charges**&#x200B;欄位旁邊，並按兩下&#x200B;**bills** > **vas**&#x200B;屬性。
1. 將游標置於&#x200B;**總費用**&#x200B;欄位旁，並按兩下&#x200B;**bills** > **usagecharges**&#x200B;屬性。
1. 將游標置於&#x200B;**TOTAL PAYABLE**&#x200B;欄位旁，並按兩下&#x200B;**bills** > **usagecharges**&#x200B;屬性。

   ![費用匯總](assets/summary_charges_static_fdm_new.png)

1. 選擇&#x200B;**Value Added Services Charges**&#x200B;行中的文本，並點選&#x200B;**Create Rule**&#x200B;以建立基於行在交互通信中顯示的條件：
1. 在&#x200B;**建立規則**&#x200B;快顯視窗中：

   1. 選擇&#x200B;**資料模型和變數**，然後選擇&#x200B;**bills** > **調用**。

   1. 選擇&#x200B;**小於**&#x200B;作為運算子。
   1. 選擇&#x200B;**Number**&#x200B;並輸入值為&#x200B;**60**。

   基於此條件，僅當「呼叫費用」欄位的值小於60時，才顯示「增值服務費用」行。

   ![create_rules_caption](assets/create_rules_caption.gif)

1. 按一下&#x200B;**保存**&#x200B;以建立費用摘要文本文檔片段。
