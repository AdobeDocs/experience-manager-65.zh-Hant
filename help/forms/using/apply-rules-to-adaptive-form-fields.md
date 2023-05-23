---
title: 將規則應用於自適應表單域
seo-title: Apply rules to adaptive form fields
description: 建立規則，以將交互性、業務邏輯和智慧驗證添加到自適應表單。
seo-description: Create rules to add interactivity, business logic, and smart validations to an adaptive form.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
source-git-commit: 63bc43bba88a42d62fb574bc8ce42470ac61d693
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 0%

---

# 教程：將規則應用於自適應表單域 {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

本教程是 [建立第一個自適應窗體](/help/forms/using/create-your-first-adaptive-form.md) 的下界。 Adobe建議按時間順序按系列進行操作，以瞭解、執行和演示完整的教程使用案例。

## 關於教程 {#about-the-tutorial}

可以使用規則將交互性、業務邏輯和智慧驗證添加到自適應表單。 自適應表單具有內置規則編輯器。 規則編輯器提供拖放功能，類似於引導式導覽。 拖放方法是建立規則的最快、最簡便的方法。 規則編輯器還為有興趣測試其編碼技能或將規則帶到下一個級別的用戶提供代碼窗口。

您可以在以下位置瞭解有關規則編輯器的詳細資訊： [自適應Forms規則編輯器](/help/forms/using/rule-editor.md)。

在本教程結束時，您將學習建立規則以：

* 調用表單資料模型服務以從資料庫檢索資料
* 調用表單資料模型服務以向資料庫添加資料
* 運行驗證檢查並顯示錯誤消息

在本教程的每一部分末尾，互動式GIF影像可幫助您即時學習和驗證要構建的表單的功能。

## 步驟1:從資料庫檢索客戶記錄 {#retrieve-customer-record}

通過以下方式建立表單資料模型： [建立表單資料模型](/help/forms/using/create-form-data-model.md) 文章。 現在，您可以使用規則編輯器調用Forms資料模型服務來檢索和向資料庫添加資訊。

為每個客戶分配一個唯一的客戶ID號，這有助於識別資料庫中的相關客戶資料。 以下過程使用客戶ID從資料庫檢索資訊：

1. 開啟自適應表單進行編輯。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 點擊 **[!UICONTROL 客戶ID]** 點擊 **[!UICONTROL 編輯規則]** 表徵圖 將開啟「規則編輯器」(Rule Editor)窗口。
1. 點擊 **[!UICONTROL +建立]** 表徵圖以添加規則。 開啟可視編輯器。

   在可視編輯器中， **[!UICONTROL 時間]** 預設情況下，選擇語句。 另外，表單對象(在本例中， **[!UICONTROL 客戶ID]**)中的 **[!UICONTROL 時間]** 的雙曲餘切值。

1. 點擊 **[!UICONTROL 選擇狀態]** 下拉並選擇 **[!UICONTROL 已更改]**。

   ![更改客戶時](assets/whencustomeridischanged.png)

1. 在 **[!UICONTROL 然後]** 語句，選擇 **[!UICONTROL 調用服務]** 從 **[!UICONTROL 選擇操作]** 下拉。
1. 選擇 **[!UICONTROL 檢索發運地址]** 服務 **[!UICONTROL 選擇]** 下拉。
1. 拖放 **[!UICONTROL 客戶ID]** 從「表單對象」頁籤到 **[!UICONTROL 刪除對象或選擇此處]** 的 **[!UICONTROL 輸入]** 框。

   ![dropobjectstoinputfield-retriedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 拖放 **[!UICONTROL 客戶ID、名稱、發運地址、狀態和郵遞區號]** 從「表單對象」頁籤到 **[!UICONTROL 刪除對象或選擇此處]** 的 **[!UICONTROL 輸出]** 框。

   ![dropobjectstooutputfield-retriedata](assets/dropobjectstooutputfield-retrievedata.png)

   點擊 **[!UICONTROL 完成]** 來保存規則。 在規則編輯器窗口中，按一下 **[!UICONTROL 關閉]**。

1. 預覽自適應窗體。 在 **[!UICONTROL 客戶ID]** 的子菜單。 現在，表單可以從資料庫中檢索客戶詳細資訊。

   ![檢索資訊](assets/retrieve-information.gif)

## 步驟2:將更新的客戶地址添加到資料庫 {#updated-customer-address}

從資料庫中檢索客戶詳細資訊後，您可以更新發運地址、狀態和郵遞區號。 以下過程調用表單資料模型服務以將客戶資訊更新到資料庫：

1. 選擇 **[!UICONTROL 提交]** 點擊 **[!UICONTROL 編輯規則]** 表徵圖 將開啟「規則編輯器」(Rule Editor)窗口。
1. 選擇 **[!UICONTROL 提交 — 按一下]** 規則並點擊 **[!UICONTROL 編輯]** 表徵圖 此時將顯示編輯「提交」規則的選項。

   ![提交規則](assets/submit-rule.png)

   在WHEN選項中， **[!UICONTROL 提交]** 和 **[!UICONTROL 按一下]** 選項。

   ![已按一下提交](assets/submit-is-clicked.png)

1. 在 **[!UICONTROL 然後]** 選項，按一下 **[!UICONTROL +添加語句]** 的雙曲餘切值。 選擇 **[!UICONTROL 調用服務]** 從 **[!UICONTROL 選擇操作]** 下拉。
1. 選擇 **[!UICONTROL 更新發運地址]** 服務 **[!UICONTROL 選擇]** 下拉。

   ![更新發運地址](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. 拖放 **[!UICONTROL 發運地址、省/自治區/直轄市和郵遞區號]** 的 [!UICONTROL 窗體對象] 的子目錄。 **[!UICONTROL 刪除對象或選擇此處]** 的 **[!UICONTROL 輸入]** 框。 所有以表名前置詞的欄位（例如，此用例中的customerdetails）都用作更新服務的輸入資料。 在資料源中更新這些欄位中提供的所有內容。

   >[!NOTE]
   >
   >不要拖放 **[!UICONTROL 名稱]** 和 **[!UICONTROL 客戶ID]** 欄位到相應的tablename.property（例如customerdetails.name）。 它有助於避免錯誤更新客戶的名稱和ID。

1. 拖放 **[!UICONTROL 客戶ID]** 的 [!UICONTROL 窗體對象] 頁籤 **[!UICONTROL 輸入]** 框。 沒有前置詞表名的欄位（例如，此使用情形中的customerdetails）用作更新服務的搜索參數。 的 **[!UICONTROL ID]** 此用例中的欄位唯一標識記錄  **customerdetails（客戶詳細資訊）**  的子菜單。
1. 點擊 **[!UICONTROL 完成]** 來保存規則。 在規則編輯器窗口中，按一下 **[!UICONTROL 關閉]**。
1. 預覽自適應窗體。 檢索客戶的詳細資訊、更新發運地址並提交表單。 當您再次檢索同一客戶的詳細資訊時，將顯示更新的發運地址。

## 第3步：（附加部分）使用代碼編輯器運行驗證並顯示錯誤消息 {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

您應對表單運行驗證，以確保在表單中輸入的資料正確，並在資料不正確時顯示錯誤消息。 例如，如果在表單中輸入了非現有客戶ID，則應顯示一條錯誤消息。

自適應表單提供了幾個具有內置驗證的元件，例如，電子郵件和數字欄位，您可以將這些欄位用於常用案例。 使用規則編輯器進行高級使用情形，例如，當資料庫返回零(0)條記錄（無記錄）時，顯示錯誤消息。

以下過程說明如何建立規則，以在資料庫中不存在在表單中輸入的客戶ID時顯示錯誤消息。 該規則還將焦點放在 **[!UICONTROL 客戶ID]** 的子菜單。 規則使用 [表單資料模型服務的dataIntegrationUtils API](/help/forms/using/invoke-form-data-model-services.md) 以檢查資料庫中是否存在客戶ID。

1. 點擊 **[!UICONTROL 客戶ID]** 點擊 `Edit Rules` 表徵圖 的 [!UICONTROL 規則編輯器] 的下界。
1. 點擊 **[!UICONTROL +建立]** 表徵圖以添加規則。 開啟可視編輯器。

   在可視編輯器中， **[!UICONTROL 時間]** 預設情況下，選擇語句。 另外，表單對象(在本例中， **[!UICONTROL 客戶ID]**)中的 **[!UICONTROL 時間]** 的雙曲餘切值。

1. 點擊 **[!UICONTROL 選擇狀態]** 下拉並選擇 **[!UICONTROL 已更改]**。

   ![更改客戶時](assets/whencustomeridischanged.png)

   在 **[!UICONTROL 然後]** 語句，選擇 **[!UICONTROL 調用服務]** 從 **[!UICONTROL 選擇操作]** 下拉。

1. 切換自 **[!UICONTROL 可視編輯器]** 至 **[!UICONTROL 代碼編輯器]**。 開關控制項位於窗口的右側。 「代碼編輯器」(Code Editor)開啟，顯示與以下內容類似的代碼：

   ![代碼編輯器](assets/code-editor.png)

1. 用以下代碼替換輸入變數部分：

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. 替換 `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` 下面的代碼：

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, function (result) {
     if (result) {
         result = JSON.parse(result);
       customer_Name.value = result.name;
       customer_Shipping_Address = result.shippingAddress;
     } else {
       if(window.confirm("Invalid Customer ID. Provide a valid customer ID")) {
             customer_Name.value = " ";
            guideBridge.setFocus(customer_ID);
       }
     }
   });
   ```

1. 預覽自適應窗體。 輸入不正確的客戶ID。 出現錯誤資訊。

   ![顯示驗證錯誤](assets/display-validation-error.gif)
