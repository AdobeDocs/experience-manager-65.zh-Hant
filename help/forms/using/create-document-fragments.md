---
title: 「教學課程：建立檔案片段」
description: 建立互動式通訊的檔案片段
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 3%

---

# 教學課程：建立檔案片段{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

此教學課程是[建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md)系列中的步驟。 Adobe建議您依照時間順序來瞭解、執行和示範完整的教學課程使用案例。

檔案片段是可重複使用的通訊元件，用於構成互動式通訊。 檔案片段屬於以下型別：

* 文字 — 文字資產是由一或多個文欄位落所組成的一段內容。 段落可以是靜態或動態的。
* 清單 — 清單是一組檔案片段，包括文字、清單、條件和影像。
* 條件 — 條件可讓您根據從表單資料模型收到的資料，定義要包含在互動式通訊中的內容。

本教學課程將逐步引導您根據[規劃互動式通訊](/help/forms/using/planning-interactive-communications.md)區段中提供的解剖來建立多個文字檔案片段。 在本教學課程結束時，您應該能夠進行下列操作：

* 建立檔案片段
* 建立變數
* 建立和套用規則

![text_document_fragments](assets/text_document_fragments.gif)

以下是本教學課程中建立的檔案片段清單：

* [帳單詳細資訊](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [客戶詳細資料](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [帳單摘要](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [費用摘要](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

每個檔案片段都包含具有靜態文字的欄位、從表單資料模型收到的資料，以及使用代理程式UI輸入的資料。 所有這些欄位已在[規劃互動式通訊](/help/forms/using/planning-interactive-communications.md)區段中描述。

在本教學課程中建立檔案片段時，會使用代理程式UI為接收資料的欄位建立變數。

在本教學課程中，使用&#x200B;**FDM_Create_First_IC** （如[建立表單資料模型](../../forms/using/create-form-data-model0.md)一節中所述）作為表單資料模型來建立檔案片段。

## 步驟1：建立帳單詳細資訊文字檔案片段 {#step-create-bill-details-text-document-fragment}

帳單詳細資料檔案片段包含下列欄位：

| 欄位 | 資料來源 |
|---|---|
| 發票號碼 | Agent UI |
| 帳單期間 | Agent UI |
| 記帳日期 | Agent UI |
| 您的計畫 | 表單資料模型 |

若要以代理程式UI作為資料來源為欄位建立變數、建立靜態文字，並在檔案片段中使用表單資料模型元素，請執行以下操作：

1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**。

1. 選取&#x200B;**建立** > **文字**。
1. 指定下列資訊：

   1. 在&#x200B;**Title**&#x200B;欄位中輸入&#x200B;**bill_details_first_ic**&#x200B;作為名稱。 標題會自動填入&#x200B;**名稱**&#x200B;欄位。

   1. 從&#x200B;**資料模型**&#x200B;區段中選取&#x200B;**表單資料模型**。

   1. 選取&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，並選取&#x200B;**選取**。

   1. 選取&#x200B;**「下一步」**。

1. 在左窗格中選取&#x200B;**變數**&#x200B;標籤，然後選取&#x200B;**建立**。
1. 在&#x200B;**建立變數**&#x200B;區段中：

   1. 輸入&#x200B;**Invoicenumber**&#x200B;作為變數的名稱。
   1. 選取&#x200B;**字串**&#x200B;作為型別。
   1. 選取「**建立**」。

   ![建立字串型別的變數](assets/variable_create_string_new.png)

   重複步驟4和5以建立下列變數：

   * 計費週期：字串型別
   * 帳單日期：日期型別

   ![帳單詳細資料](assets/variable_bill_details_new.png)

1. 使用右窗格為下列欄位建立靜態文字：

   * 發票號碼
   * 帳單期間
   * 記帳日期
   * 您的計畫

   ![靜態文字](assets/variable_bill_details_static_text_new.png)

1. 將游標放在&#x200B;**發票號碼**&#x200B;欄位旁，然後從&#x200B;**變數**&#x200B;索引標籤中連按兩下&#x200B;**發票號碼**&#x200B;變數。
1. 將游標放在&#x200B;**帳單期間**&#x200B;欄位旁邊，然後按兩下&#x200B;**帳單期間**&#x200B;變數。
1. 將游標放在&#x200B;**帳單日期**&#x200B;欄位旁邊，然後按兩下&#x200B;**帳單日期**&#x200B;變數。
1. 在左窗格中選取&#x200B;**資料模型物件**&#x200B;標籤。
1. 將游標放在&#x200B;**您的計畫**&#x200B;欄位旁邊，然後按兩下&#x200B;**customer** > **customerplan**&#x200B;屬性。

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. 按一下&#x200B;**儲存**&#x200B;以建立帳單詳細資訊文字檔案片段。

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

1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**。
1. 選取&#x200B;**建立** > **文字**。
1. 指定下列資訊：

   1. 在&#x200B;**Title**&#x200B;欄位中輸入&#x200B;**customer_details_first_ic**&#x200B;作為名稱。 標題會自動填入&#x200B;**名稱**&#x200B;欄位。

   1. 從&#x200B;**資料模型**&#x200B;區段中選取&#x200B;**表單資料模型**。

   1. 選取&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，並選取&#x200B;**選取**。

   1. 選取&#x200B;**「下一步」**。

1. 在左窗格中選取&#x200B;**變數**&#x200B;標籤，然後選取&#x200B;**建立**。
1. 在&#x200B;**建立變數**&#x200B;區段中：

   1. 輸入&#x200B;**Placessupply**&#x200B;作為變數的名稱。
   1. 選取&#x200B;**字串**&#x200B;作為型別。
   1. 選取「**建立**」。

   重複步驟4和5以建立下列變數：

   * Statecode：號碼型別
   * Numberconnections：數字型別

1. 選取&#x200B;**資料模型物件**&#x200B;標籤，將游標置於右窗格中，然後按兩下&#x200B;**customer** > **name**&#x200B;屬性。
1. 按Enter鍵將游標移至下一行，然後按兩下&#x200B;**customer** > **address**&#x200B;屬性。
1. 使用右窗格為下列欄位建立靜態文字：

   * 行動電話號碼
   * 備用連絡人號碼
   * 供應地點
   * 關係編號
   * 州代碼
   * 連線數目

   ![客戶詳細資料靜態文字](assets/customer_details_static_text_new.png)

1. 將游標放在&#x200B;**行動電話號碼**&#x200B;欄位旁邊，然後按兩下&#x200B;**客戶** > **行動電話號碼**&#x200B;屬性。
1. 將游標放在&#x200B;**備用聯絡電話號碼**&#x200B;欄位旁，然後按兩下** customer** > **alternatemobilenumber**&#x200B;屬性。
1. 將游標置於&#x200B;**關聯性編號**&#x200B;欄位旁邊，然後按兩下&#x200B;**客戶** > **關聯性編號**&#x200B;屬性。
1. 選取&#x200B;**變數**&#x200B;標籤，將游標放置在&#x200B;**供給位置**&#x200B;欄位旁邊，然後按兩下&#x200B;**Placessupply**&#x200B;變數。
1. 將游標放在&#x200B;**狀態碼**&#x200B;欄位旁邊，然後按兩下&#x200B;**狀態碼**&#x200B;變數。
1. 將游標置於&#x200B;**連線數目**&#x200B;欄位旁邊，然後按兩下&#x200B;**Numberconnections**&#x200B;變數。

   ![客戶詳細資料](assets/customer_details_df2_new.png)

1. 按一下「**儲存**」以建立客戶詳細資料文字檔案片段。

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

1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**。
1. 選取&#x200B;**建立** > **文字**。
1. 指定下列資訊：

   1. 在&#x200B;**Title**&#x200B;欄位中輸入&#x200B;**bill_summary_first_ic**&#x200B;作為名稱。 標題會自動填入&#x200B;**名稱**&#x200B;欄位。

   1. 從&#x200B;**資料模型**&#x200B;區段中選取&#x200B;**表單資料模型**。

   1. 選取&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，並選取&#x200B;**選取**。

   1. 選取&#x200B;**「下一步」**。

1. 在左窗格中選取&#x200B;**變數**&#x200B;標籤，然後選取&#x200B;**建立**。
1. 在&#x200B;**建立變數**&#x200B;區段中：

   1. 輸入&#x200B;**Previousbalance**&#x200B;作為變數名稱。
   1. 選取&#x200B;**數字**&#x200B;作為型別。
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

1. 將游標放在&#x200B;**Previous Balance**&#x200B;欄位旁邊，然後按兩下&#x200B;**Previousbalance**&#x200B;變數。
1. 將游標放在&#x200B;**付款**&#x200B;欄位旁邊，然後按兩下&#x200B;**付款**&#x200B;變數。
1. 將游標置於&#x200B;**調整**&#x200B;欄位旁邊，然後按兩下&#x200B;**調整**&#x200B;變數。
1. 將游標放在&#x200B;**到期金額**&#x200B;欄位旁邊，然後按兩下&#x200B;**到期金額**&#x200B;變數。
1. 將游標置於&#x200B;**到期日**&#x200B;欄位旁邊，然後按兩下&#x200B;**Duedate**&#x200B;變數。
1. 選取&#x200B;**資料模型物件**&#x200B;索引標籤，將游標放在右窗格中的&#x200B;**費用目前帳單期間**&#x200B;欄位旁，然後按兩下&#x200B;**帳單** > **使用費用**&#x200B;屬性。

   ![帳單摘要](assets/bill_summary_static_variables_new.png)

1. 按一下「**儲存**」以建立客戶詳細資料文字檔案片段。

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

1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**。
1. 選取&#x200B;**建立** > **文字**。
1. 指定下列資訊：

   1. 在&#x200B;**Title**&#x200B;欄位中輸入&#x200B;**summary_charges_first_ic**&#x200B;作為名稱。 標題會自動填入名稱欄位。

   1. 從&#x200B;**資料模型**&#x200B;區段中選取&#x200B;**表單資料模型**。

   1. 選取&#x200B;**FDM_Create_First_IC**&#x200B;作為表單資料模型，並選取&#x200B;**選取**。

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

   ![摘要費用](assets/summary_charges_static_new.png)

1. 選取&#x200B;**資料模型物件**&#x200B;標籤。
1. 將游標置於&#x200B;**通話費用**&#x200B;欄位旁，然後按兩下&#x200B;**帳單** > **通話費用**&#x200B;屬性。
1. 將游標放在&#x200B;**電話會議費用**&#x200B;欄位旁，然後按兩下&#x200B;**帳單** > **confcallcharges**&#x200B;屬性。
1. 將游標放在&#x200B;**SMS Charges**&#x200B;欄位旁邊，然後按兩下&#x200B;**bills** > **smscharges**&#x200B;屬性。
1. 將游標放在&#x200B;**行動網際網路費用**&#x200B;欄位旁邊，然後按兩下&#x200B;**帳單** > **網際網路費用**&#x200B;屬性。
1. 將游標放在&#x200B;**國家漫遊費用**&#x200B;欄位旁，然後按兩下&#x200B;**帳單** > **漫遊國家**&#x200B;屬性。
1. 將游標置於&#x200B;**國際漫遊費用**&#x200B;欄位旁邊，然後按兩下&#x200B;**帳單** > **roamingintnl**&#x200B;屬性。
1. 將游標放在&#x200B;**加值服務費用**&#x200B;欄位旁，然後按兩下&#x200B;**bills** > **vas**&#x200B;屬性。
1. 將游標放在&#x200B;**總費用**&#x200B;欄位旁邊，然後按兩下&#x200B;**帳單** > **使用費用**&#x200B;屬性。
1. 將游標放在&#x200B;**應付帳款總計**&#x200B;欄位旁邊，然後按兩下&#x200B;**帳單** > **使用費用**&#x200B;屬性。

   ![費用摘要](assets/summary_charges_static_fdm_new.png)

1. 選取&#x200B;**加值服務費用**&#x200B;列中的文字，並選取&#x200B;**建立規則**&#x200B;以建立條件，根據互動式通訊中顯示該列：
1. 在&#x200B;**建立規則**&#x200B;快顯視窗上：

   1. 選取&#x200B;**資料模型與變數**，然後選取&#x200B;**用料表** > **callcharges**。

   1. 選取&#x200B;**小於**&#x200B;作為運運算元。
   1. 選取&#x200B;**數字**&#x200B;並輸入值為&#x200B;**60**。

   根據此條件，只有在「通話費用」欄位的值小於60時，才會顯示「加值服務費用」列。

   ![create_rules_caption](assets/create_rules_caption.gif)

1. 按一下&#x200B;**儲存**&#x200B;以建立費用摘要文字檔案片段。
