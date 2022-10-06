---
title: 「教學課程：建立檔案片段」
seo-title: Create document fragments for Interactive Communication
description: 建立互動式通訊的檔案片段
seo-description: Create document fragments for Interactive Communication
uuid: 677d717e-e92e-434e-8266-6fbbf94f3867
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8ae97a21-83af-4615-9be3-61e2f8065081
docset: aem65
feature: Interactive Communication
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 2%

---

# 教學課程：建立檔案片段{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

本教學課程是 [建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md) 系列。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

文檔片段是用於構成互動式通信的通信的可重複使用的元件。 檔案片段的類型如下：

* 文字 — 文字資產是由一或多個文欄位落組成的內容片段。 段落可以是靜態的或動態的。
* 清單 — 清單是一組文檔片段，包括文本、清單、條件和影像。
* 條件 — 條件可讓您根據從表單資料模型收到的資料，定義互動式通訊中包含的內容。

本教學課程會逐步引導您了解如何根據 [規劃互動式通訊](/help/forms/using/planning-interactive-communications.md) 區段。 在本教學課程結束時，您將能夠：

* 建立檔案片段
* 建立變數
* 建立和套用規則

![text_document_fragments](assets/text_document_fragments.gif)

以下是在本教學課程中建立的檔案片段清單：

* [帳單詳細資訊](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [客戶詳細資訊](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [清單匯總](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [費用匯總](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

每個檔案片段都包含含有靜態文字的欄位、從表單資料模型收到的資料，以及使用代理UI輸入的資料。 所有這些欄位都在 [規劃互動式通訊](/help/forms/using/planning-interactive-communications.md) 區段。

在本教學課程中建立檔案片段時，會使用代理UI為接收資料的欄位建立變數。

使用 **FDM_Create_First_IC**，如 [建立表單資料模型](../../forms/using/create-form-data-model0.md) 區段，作為本教學課程中建立檔案片段的表單資料模型。

## 步驟1:建立清單詳細資訊文本文檔片段 {#step-create-bill-details-text-document-fragment}

「清單詳細資訊」單據片段包括以下欄位：

| 欄位 | 資料來源 |
|---|---|
| 發票編號 | Agent UI |
| 帳單期間 | 代理UI |
| 帳單日期 | 代理UI |
| 您的計畫 | 表單資料模型 |

執行下列步驟為以Agent UI為資料源的欄位建立變數、建立靜態文本，以及在文檔片段中使用表單資料模型元素：

1. 選擇 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.

1. 選擇 **建立** > **文字**.
1. 指定下列資訊：

   1. 輸入 **bill_details_first_ic** 作為 **標題** 欄位。 標題會自動填入 **名稱** 欄位。

   1. 選擇 **表單資料模型** 從 **資料模型** 區段。

   1. 選擇 **FDM_Create_First_IC** 作為表單資料模型並點選 **選擇**.

   1. 點選 **下一個**.

1. 選取 **變數** 標籤，然後點選 **建立**.
1. 在 **建立變數** 小節：

   1. 輸入 **發票編號** 作為變數的名稱。
   1. 選擇 **字串** 。
   1. 點選 **建立**.

   ![建立字串類型的變數](assets/variable_create_string_new.png)

   重複步驟4和5以建立下列變數：

   * 計費週期：字串類型
   * 帳單日期：日期類型

   ![帳單詳細資訊](assets/variable_bill_details_new.png)

1. 使用右窗格建立以下欄位的靜態文本：

   * 發票編號
   * 帳單期間
   * 帳單日期
   * 您的計畫

   ![靜態文字](assets/variable_bill_details_static_text_new.png)

1. 將游標放在 **發票編號** 欄位並連按兩下 **發票編號** 變數 **變數** 頁簽。
1. 將游標放在 **帳單期間** 欄位並連按兩下 **帳單期間** 變數。
1. 將游標放在 **帳單日期** 欄位並連按兩下 **帳單日期** 變數。
1. 選取 **資料模型物件** 頁簽。
1. 將游標放在 **您的計畫** 欄位並連按兩下 **客戶** > **customerplan** 屬性。

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. 按一下 **儲存** 要建立「清單詳細資訊」文本文檔片段，請執行以下操作：

## 步驟2:建立客戶詳細資訊文本文檔片段 {#step-create-customer-details-text-document-fragment}

「客戶詳細資訊」檔案片段包含下列欄位：

| 欄位 | 資料來源 |
|---|---|
| 客戶名稱 | 表單資料模型 |
| 地址 | 表單資料模型 |
| 供應地 | 代理UI |
| 狀態代碼 | 代理UI |
| 行動號碼 | 表單資料模型 |
| 備用聯繫人號碼 | 表單資料模型 |
| 關係編號 | 表單資料模型 |
| 連接數 | 代理UI |

執行下列步驟為以Agent UI為資料源的欄位建立變數、建立靜態文本，以及在文檔片段中使用表單資料模型元素：

1. 選擇 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.
1. 選擇 **建立** > **文字**.
1. 指定下列資訊：

   1. 輸入 **customer_details_first_ic** 作為 **標題** 欄位。 標題會自動填入 **名稱** 欄位。

   1. 選擇 **表單資料模型** 從 **資料模型** 區段。

   1. 選擇 **FDM_Create_First_IC** 作為表單資料模型並點選 **選擇**.

   1. 點選 **下一個**.

1. 選取 **變數** 標籤，然後點選 **建立**.
1. 在 **建立變數** 小節：

   1. 輸入 **Placesupply** 作為變數的名稱。
   1. 選擇 **字串** 。
   1. 點選 **建立**.

   重複步驟4和5以建立下列變數：

   * 狀態代碼：數字類型
   * 數字連接：數字類型


1. 選取 **資料模型物件** 頁簽，將游標置於右窗格中，然後按兩下 **客戶** > **名稱** 屬性。
1. 按Enter鍵將游標移至下一行，然後按兩下 **客戶** > **地址** 屬性。
1. 使用右窗格建立以下欄位的靜態文本：

   * 行動號碼
   * 備用聯繫人號碼
   * 供應地
   * 關係編號
   * 狀態代碼
   * 連接數

   ![客戶詳細資訊靜態文字](assets/customer_details_static_text_new.png)

1. 將游標放在 **行動號碼** 欄位並連按兩下 **客戶** > **mobilenum** 屬性。
1. 將游標放在 **備用聯繫人號碼** 欄位，然後按兩下** customer** > **alternatemobilenumber** 屬性。
1. 將游標放在 **關係編號** 欄位並連按兩下 **客戶** > **關係編號** 屬性。
1. 選取 **變數** 標籤，將游標放在 **供應地** 欄位並連按兩下 **Placesupply** 變數。
1. 將游標放在 **狀態代碼** 欄位並連按兩下 **Statecode** 變數。
1. 將游標放在 **連接數** 欄位並連按兩下 **數字連接** 變數。

   ![客戶詳細資訊](assets/customer_details_df2_new.png)

1. 按一下 **儲存** 建立「客戶詳細資訊」文本文檔片段。

## 步驟3:建立清單匯總文本文檔片段 {#step-create-bill-summary-text-document-fragment}

「清單匯總」單據片段包括以下欄位：

| 欄位 | 資料來源 |
|---|---|
| 上一餘額 | 代理UI |
| 付款 | 代理UI |
| 調整 | 代理UI |
| 當前帳單期間費用 | 表單資料模型 |
| 到期金額 | 代理UI |
| 到期日期 | 代理UI |

執行下列步驟為以Agent UI為資料源的欄位建立變數、建立靜態文本，以及在文檔片段中使用表單資料模型元素：

1. 選擇 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.
1. 選擇 **建立** > **文字**.
1. 指定下列資訊：

   1. 輸入 **bill_summary_first_ic** 作為 **標題** 欄位。 標題會自動填入 **名稱** 欄位。

   1. 選擇 **表單資料模型** 從 **資料模型** 區段。

   1. 選擇 **FDM_Create_First_IC** 作為表單資料模型並點選 **選擇**.

   1. 點選 **下一個**.

1. 選取 **變數** 標籤，然後點選 **建立**.
1. 在 **建立變數** 小節：

   1. 輸入 **前期餘額** 作為變數的名稱。
   1. 選擇 **數字** 。
   1. 點選 **建立**.

   重複步驟4和5以建立下列變數：

   * 付款：數字類型
   * 調整：數字類型
   * 到期款項：數字類型
   * 重複：日期類型


1. 使用右窗格建立以下欄位的靜態文本：

   * 上一餘額
   * 付款
   * 調整
   * 當前帳單期間費用
   * 到期金額
   * 到期日期
   * 到期日後的延遲付款費用為$ 20

   ![清單摘要靜態文本](assets/bill_summary_static_new.png)

1. 將游標放在 **上一餘額** 欄位並連按兩下 **前期餘額** 變數。
1. 將游標放在 **付款** 欄位並連按兩下 **付款** 變數。
1. 將游標放在 **調整** 欄位並連按兩下 **調整** 變數。
1. 將游標放在 **到期金額** 欄位並連按兩下 **到期金額** 變數。
1. 將游標放在 **到期日** 欄位並連按兩下 **杜埃達特** 變數。
1. 選取 **資料模型物件** 標籤，將游標放在 **當前帳單期間費用** 欄位，然後按兩下 **票據** > **烏薩傑查爾熱** 屬性。

   ![清單匯總](assets/bill_summary_static_variables_new.png)

1. 按一下 **儲存** 建立「客戶詳細資訊」文本文檔片段。

## 步驟4:建立費用匯總文本文檔片段 {#step-create-summary-of-charges-text-document-fragment}

費用匯總文檔片段包括以下欄位：

| 欄位 | 資料來源 |
|---|---|
| 通話費 | 表單資料模型 |
| 電話會議費 | 表單資料模型 |
| 簡訊指控 | 表單資料模型 |
| 行動網際網路收費 | 表單資料模型 |
| 國家漫遊費 | 表單資料模型 |
| 國際漫遊費 | 表單資料模型 |
| 增值服務費 | 表單資料模型 |
| 總費用 | 表單資料模型 |
| 應付總額 | 表單資料模型 |

執行下列步驟以建立靜態文字，並在檔案片段中使用表單資料模型元素：

1. 選擇 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.
1. 選擇 **建立** > **文字**.
1. 指定下列資訊：

   1. 輸入 **summary_charges_first_ic** 作為 **標題** 欄位。 標題會自動填入「名稱」欄位中。

   1. 選擇 **表單資料模型** 從 **資料模型** 區段。

   1. 選擇 **FDM_Create_First_IC** 作為表單資料模型並點選 **選擇**.

   1. 點選 **下一個**.

1. 使用右窗格建立以下欄位的靜態文本：

   * 通話費
   * 電話會議費
   * 簡訊指控
   * 行動網際網路收費
   * 國家漫遊費
   * 國際漫遊費
   * 增值服務費
   * 總費用
   * 應付總額

   ![匯總費用](assets/summary_charges_static_new.png)

1. 選取 **資料模型物件** 標籤。
1. 將游標放在 **通話費** 欄位並連按兩下 **票據** > **呼叫費** 屬性。
1. 將游標放在 **電話會議費** 欄位並連按兩下 **票據** > **concallcarches** 屬性。
1. 將游標放在 **簡訊指控** 欄位並連按兩下 **票據** > **smcharges** 屬性。
1. 將游標放在 **行動網際網路收費** 欄位並連按兩下 **票據** > **internetcargeins** 屬性。
1. 將游標放在 **國家漫遊費** 欄位並連按兩下 **票據** > **羅明尼亞** 屬性。
1. 將游標放在 **國際漫遊費** 欄位並連按兩下 **票據** > **羅明寧** 屬性。
1. 將游標放在 **增值服務費** 欄位並連按兩下 **票據** > **vas** 屬性。
1. 將游標放在 **總費用** 欄位並連按兩下 **票據** > **烏薩傑查爾熱** 屬性。
1. 將游標放在 **應付總額** 欄位並連按兩下 **票據** > **烏薩傑查爾熱** 屬性。

   ![費用匯總](assets/summary_charges_static_fdm_new.png)

1. 選取 **增值服務費** 列和點選 **建立規則** 要建立條件，根據該條件在交互通信中顯示行：
1. 在 **建立規則** 彈出窗口：

   1. 選擇 **資料模型與變數** 然後 **票據** > **呼叫費**.

   1. 選擇 **小於** 作為運算子。
   1. 選擇 **數字** 並輸入值為 **60**.

   根據此條件，僅當「呼叫費用」欄位的值小於60時，才會顯示「增值服務費用」行。

   ![create_rules_caption](assets/create_rules_caption.gif)

1. 按一下 **儲存** 建立費用匯總文本文檔片段。
