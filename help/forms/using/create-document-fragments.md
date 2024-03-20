---
title: 「教學課程：建立檔案片段」
description: 建立互動式通訊的檔案片段
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 3%

---

# 教學課程：建立檔案片段{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

本教學課程是 [建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md) 數列。 Adobe建議您依照時間順序來瞭解、執行和示範完整的教學課程使用案例。

檔案片段是可重複使用的通訊元件，用於構成互動式通訊。 檔案片段屬於以下型別：

* 文字 — 文字資產是由一或多個文欄位落所組成的一段內容。 段落可以是靜態或動態的。
* 清單 — 清單是一組檔案片段，包括文字、清單、條件和影像。
* 條件 — 條件可讓您根據從表單資料模型收到的資料，定義要包含在互動式通訊中的內容。

本教學課程將逐步引導您根據中提供的解剖結構建立多個文字檔案片段 [規劃互動式通訊](/help/forms/using/planning-interactive-communications.md) 區段。 在本教學課程結束時，您應該能夠進行下列操作：

* 建立檔案片段
* 建立變數
* 建立和套用規則

![text_document_fragments](assets/text_document_fragments.gif)

以下是本教學課程中建立的檔案片段清單：

* [帳單詳細資訊](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [客戶詳細資料](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [帳單摘要](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [費用摘要](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

每個檔案片段都包含具有靜態文字的欄位、從表單資料模型收到的資料，以及使用代理程式UI輸入的資料。 以下欄位全部已描述於 [規劃互動式通訊](/help/forms/using/planning-interactive-communications.md) 區段。

在本教學課程中建立檔案片段時，會使用代理程式UI為接收資料的欄位建立變數。

使用 **FDM_Create_First_IC**，如 [建立表單資料模型](../../forms/using/create-form-data-model0.md) 區段，作為表單資料模型，以在本教學課程中建立檔案片段。

## 步驟1：建立帳單詳細資訊文字檔案片段 {#step-create-bill-details-text-document-fragment}

帳單詳細資料檔案片段包含下列欄位：

| 欄位 | 資料來源 |
|---|---|
| 發票號碼 | Agent UI |
| 帳單期間 | Agent UI |
| 記帳日期 | Agent UI |
| 您的計畫 | 表單資料模型 |

若要以代理程式UI作為資料來源為欄位建立變數、建立靜態文字，並在檔案片段中使用表單資料模型元素，請執行以下操作：

1. 選取 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.

1. 選取 **建立** > **文字**.
1. 指定下列資訊：

   1. 輸入 **bill_details_first_ic** 作為中的名稱 **標題** 欄位。 標題會自動填入 **名稱** 欄位。

   1. 選取 **表單資料模型** 從 **資料模型** 區段。

   1. 選取 **FDM_Create_First_IC** 作為表單資料模型，並選取 **選取**.

   1. 選取&#x200B;**「下一步」**。

1. 選取 **變數** 標籤並選取「 」 **建立**.
1. 在 **建立變數** 區段：

   1. 輸入 **發票號碼** 做為變數的名稱。
   1. 選取 **字串** 作為型別。
   1. 選取「**建立**」。

   ![建立字串型別的變數](assets/variable_create_string_new.png)

   重複步驟4和5以建立下列變數：

   * 計費週期：字串型別
   * 帳單日期：日期型別

   ![帳單詳細資訊](assets/variable_bill_details_new.png)

1. 使用右窗格為下列欄位建立靜態文字：

   * 發票號碼
   * 帳單期間
   * 記帳日期
   * 您的計畫

   ![靜態文字](assets/variable_bill_details_static_text_new.png)

1. 將游標放在 **發票號碼** 欄位並連按兩下 **發票號碼** 變數，來自 **變數** 標籤。
1. 將游標放在 **帳單期間** 欄位並連按兩下 **帳單期間** 變數中。
1. 將游標放在 **記帳日期** 欄位並連按兩下 **記帳日期** 變數中。
1. 選取 **資料模型物件** 標籤。
1. 將游標放在 **您的計畫** 欄位並連按兩下 **客戶** > **customerplan** 屬性。

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. 按一下 **儲存** 以建立帳單詳細資訊文字檔案片段。

## 步驟2：建立客戶詳細資料文字檔案片段 {#step-create-customer-details-text-document-fragment}

客戶詳細資料檔案片段包含下列欄位：

| 欄位 | 資料來源 |
|---|---|
| 客戶名稱 | 表單資料模型 |
| 地址 | 表單資料模型 |
| 供應地點 | Agent UI |
| 州代碼 | Agent UI |
| 行動電話號碼 | 表單資料模型 |
| 備用連絡人號碼 | 表單資料模型 |
| 關係編號 | 表單資料模型 |
| 連線數目 | Agent UI |

若要以代理程式UI作為資料來源為欄位建立變數、建立靜態文字，並在檔案片段中使用表單資料模型元素，請執行以下操作：

1. 選取 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.
1. 選取 **建立** > **文字**.
1. 指定下列資訊：

   1. 輸入 **customer_details_first_ic** 作為中的名稱 **標題** 欄位。 標題會自動填入 **名稱** 欄位。

   1. 選取 **表單資料模型** 從 **資料模型** 區段。

   1. 選取 **FDM_Create_First_IC** 作為表單資料模型，並選取 **選取**.

   1. 選取&#x200B;**「下一步」**。

1. 選取 **變數** 標籤並選取「 」 **建立**.
1. 在 **建立變數** 區段：

   1. 輸入 **Placesupply** 做為變數的名稱。
   1. 選取 **字串** 作為型別。
   1. 選取「**建立**」。

   重複步驟4和5以建立下列變數：

   * Statecode：號碼型別
   * Numberconnections：數字型別

1. 選取 **資料模型物件** 標籤，將游標置於右窗格中，然後按兩下 **客戶** > **名稱** 屬性。
1. 按Enter鍵將游標移至下一行，然後按兩下 **客戶** > **地址** 屬性。
1. 使用右窗格為下列欄位建立靜態文字：

   * 行動電話號碼
   * 備用連絡人號碼
   * 供應地點
   * 關係編號
   * 州代碼
   * 連線數目

   ![客戶詳細資料靜態文字](assets/customer_details_static_text_new.png)

1. 將游標放在 **行動電話號碼** 欄位並連按兩下 **客戶** > **mobilenum** 屬性。
1. 將游標放在 **備用連絡人號碼** 欄位並連按兩下** customer** > **alternatemobilenumber** 屬性。
1. 將游標放在 **關係編號** 欄位並連按兩下 **客戶** > **relationshipnumber** 屬性。
1. 選取 **變數** 標籤，將游標放置在 **供應地點** 欄位並連按兩下 **Placesupply** 變數中。
1. 將游標放在 **州代碼** 欄位並連按兩下 **狀態碼** 變數中。
1. 將游標放在 **連線數目** 欄位並連按兩下 **Numberconnections** 變數中。

   ![客戶詳細資料](assets/customer_details_df2_new.png)

1. 按一下 **儲存** 以建立客戶詳細資料文字檔案片段。

## 步驟3：建立帳單摘要文字檔案片段 {#step-create-bill-summary-text-document-fragment}

帳單摘要檔案片段包含下列欄位：

| 欄位 | 資料來源 |
|---|---|
| 上一個餘額 | Agent UI |
| 付款 | Agent UI |
| 調整 | Agent UI |
| 費用目前帳單期間 | 表單資料模型 |
| 應付金額 | Agent UI |
| 到期日期 | Agent UI |

若要以代理程式UI作為資料來源為欄位建立變數、建立靜態文字，並在檔案片段中使用表單資料模型元素，請執行以下操作：

1. 選取 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.
1. 選取 **建立** > **文字**.
1. 指定下列資訊：

   1. 輸入 **bill_summary_first_ic** 作為中的名稱 **標題** 欄位。 標題會自動填入 **名稱** 欄位。

   1. 選取 **表單資料模型** 從 **資料模型** 區段。

   1. 選取 **FDM_Create_First_IC** 作為表單資料模型，並選取 **選取**.

   1. 選取&#x200B;**「下一步」**。

1. 選取 **變數** 標籤並選取「 」 **建立**.
1. 在 **建立變數** 區段：

   1. 輸入 **先前平衡** 做為變數的名稱。
   1. 選取 **數字** 作為型別。
   1. 選取「**建立**」。

   重複步驟4和5以建立下列變數：

   * 付款：編號型別
   * 調整：數字型別
   * 金額：數字型別
   * 重複：日期型別

1. 使用右窗格為下列欄位建立靜態文字：

   * 上一個餘額
   * 付款
   * 調整
   * 費用目前帳單期間
   * 應付金額
   * 到期日期
   * 到期日之後的延遲付款費用為$ 20

   ![帳單摘要靜態文字](assets/bill_summary_static_new.png)

1. 將游標放在 **上一個餘額** 欄位並連按兩下 **先前平衡** 變數中。
1. 將游標放在 **付款** 欄位並連按兩下 **付款** 變數中。
1. 將游標放在 **調整** 欄位並連按兩下 **調整** 變數中。
1. 將游標放在 **應付金額** 欄位並連按兩下 **金額** 變數中。
1. 將游標放在 **到期日期** 欄位並連按兩下 **重複** 變數中。
1. 選取 **資料模型物件** 標籤，將游標放置在 **費用目前帳單期間** 欄位，然後按兩下 **帳單** > **使用費用** 屬性。

   ![帳單摘要](assets/bill_summary_static_variables_new.png)

1. 按一下 **儲存** 以建立客戶詳細資料文字檔案片段。

## 步驟4：建立費用摘要文字檔案片段 {#step-create-summary-of-charges-text-document-fragment}

「費用摘要檔案片段」包含下列欄位：

| 欄位 | 資料來源 |
|---|---|
| 通話費用 | 表單資料模型 |
| 電話會議費用 | 表單資料模型 |
| 簡訊費用 | 表單資料模型 |
| 行動網際網路費用 | 表單資料模型 |
| 國家漫遊費用 | 表單資料模型 |
| 國際漫遊費用 | 表單資料模型 |
| 增值服務費用 | 表單資料模型 |
| 總費用 | 表單資料模型 |
| 應付帳款總計 | 表單資料模型 |

若要建立靜態文字並在檔案片段中使用表單資料模型元素，請執行下列動作：

1. 選取 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.
1. 選取 **建立** > **文字**.
1. 指定下列資訊：

   1. 輸入 **summary_charges_first_ic** 作為中的名稱 **標題** 欄位。 標題會自動填入名稱欄位。

   1. 選取 **表單資料模型** 從 **資料模型** 區段。

   1. 選取 **FDM_Create_First_IC** 作為表單資料模型，並選取 **選取**.

   1. 選取&#x200B;**「下一步」**。

1. 使用右窗格為下列欄位建立靜態文字：

   * 通話費用
   * 電話會議費用
   * 簡訊費用
   * 行動網際網路費用
   * 國家漫遊費用
   * 國際漫遊費用
   * 增值服務費用
   * 總費用
   * 應付帳款總計

   ![彙總費用](assets/summary_charges_static_new.png)

1. 選取 **資料模型物件** 標籤。
1. 將游標放在 **通話費用** 欄位並連按兩下 **帳單** > **callcharges** 屬性。
1. 將游標放在 **電話會議費用** 欄位並連按兩下 **帳單** > **confcallcharges** 屬性。
1. 將游標放在 **簡訊費用** 欄位並連按兩下 **帳單** > **smscharges** 屬性。
1. 將游標放在 **行動網際網路費用** 欄位並連按兩下 **帳單** > **網際費用** 屬性。
1. 將游標放在 **國家漫遊費用** 欄位並連按兩下 **帳單** > **roamingnational** 屬性。
1. 將游標放在 **國際漫遊費用** 欄位並連按兩下 **帳單** > **roamingintel** 屬性。
1. 將游標放在 **增值服務費用** 欄位並連按兩下 **帳單** > **vas** 屬性。
1. 將游標放在 **總費用** 欄位並連按兩下 **帳單** > **使用費用** 屬性。
1. 將游標放在 **應付帳款總計** 欄位並連按兩下 **帳單** > **使用費用** 屬性。

   ![費用摘要](assets/summary_charges_static_fdm_new.png)

1. 選擇文字 **增值服務費用** 列並選取 **建立規則** 若要建立要在互動式通訊中顯示資料列的條件：
1. 在 **建立規則** 快顯視窗：

   1. 選取 **資料模型與變數** 然後 **帳單** > **callcharges**.

   1. 選取 **小於** 作為運運算元。
   1. 選取 **數字** 並輸入值，如下所示 **60**.

   根據此條件，只有在「通話費用」欄位的值小於60時，才會顯示「加值服務費用」列。

   ![create_rules_caption](assets/create_rules_caption.gif)

1. 按一下 **儲存** 以建立費用摘要文字檔案片段。
