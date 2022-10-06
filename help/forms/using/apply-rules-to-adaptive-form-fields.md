---
title: 將規則套用至最適化表單欄位
seo-title: Apply rules to adaptive form fields
description: 建立規則，將互動性、商業邏輯和智慧驗證新增至最適化表單。
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

# 教學課程：將規則套用至最適化表單欄位 {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

本教學課程是 [建立第一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md) 系列。 Adobe建議依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

您可以使用規則將互動性、商業邏輯和智慧驗證新增至最適化表單。 適用性表單有內建的規則編輯器。 規則編輯器提供拖放功能，類似於引導式導覽。 拖放方法是建立規則最快速且最簡單的方法。 規則編輯器還為有興趣測試其編碼技能或將規則提升到下一級的用戶提供一個代碼窗口。

如需規則編輯器的詳細資訊，請前往 [適用性Forms規則編輯器](/help/forms/using/rule-editor.md).

在教學課程結束前，您將學習如何建立規則，以：

* 調用表單資料模型服務以從資料庫中檢索資料
* 調用表單資料模型服務以將資料添加到資料庫
* 運行驗證檢查並顯示錯誤消息

教學課程每個區段結尾的互動式GIF影像可協助您即時學習及驗證您要建立的表單的功能。

## 步驟1:從資料庫中檢索客戶記錄 {#retrieve-customer-record}

您已建立表單資料模型，方法是遵循 [建立表單資料模型](/help/forms/using/create-form-data-model.md) 文章。 現在，您可以使用規則編輯器叫用Forms資料模型服務，以擷取資訊並新增至資料庫。

每個客戶都獲派一個唯一的客戶ID編號，這有助於識別資料庫中的相關客戶資料。 以下過程使用客戶ID從資料庫中檢索資訊：

1. 開啟最適化表單以進行編輯。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 點選 **[!UICONTROL 客戶ID]** 欄位並點選 **[!UICONTROL 編輯規則]** 表徵圖。 「規則編輯器」窗口隨即開啟。
1. 點選 **[!UICONTROL +建立]** 圖示來新增規則。 它會開啟視覺編輯器。

   在可視化編輯器中， **[!UICONTROL 當]** 預設情況下，會選取語句。 此外，表單物件(在此例中， **[!UICONTROL 客戶ID]**)，此時會在 **[!UICONTROL 當]** 語句。

1. 點選 **[!UICONTROL 選擇狀態]** 下拉式清單並選取 **[!UICONTROL 已變更]**.

   ![自訂變更時](assets/whencustomeridischanged.png)

1. 在 **[!UICONTROL THEN]** 語句，選擇 **[!UICONTROL 調用服務]** 從 **[!UICONTROL 選擇操作]** 下拉式清單。
1. 選取 **[!UICONTROL 檢索發運地址]** 服務 **[!UICONTROL 選擇]** 下拉式清單。
1. 拖放 **[!UICONTROL 客戶ID]** 欄位(從「表單對象」頁簽到 **[!UICONTROL 拖放對象或在此處選擇]** 欄位 **[!UICONTROL 輸入]** 框。

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 拖放 **[!UICONTROL 客戶ID、名稱、運送地址、州和郵遞區號]** 欄位(從「表單對象」頁簽到 **[!UICONTROL 拖放對象或在此處選擇]** 欄位 **[!UICONTROL 輸出]** 框。

   ![dropobjectstooutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   點選 **[!UICONTROL 完成]** 來儲存規則。 在規則編輯器視窗上，點選 **[!UICONTROL 關閉]**.

1. 預覽最適化表單。 在 **[!UICONTROL 客戶ID]** 欄位。 表單現在可以從資料庫擷取客戶詳細資訊。

   ![檢索資訊](assets/retrieve-information.gif)

## 步驟2:將更新的客戶地址添加到資料庫 {#updated-customer-address}

從資料庫中擷取客戶詳細資訊後，您就可以更新運送地址、狀態和郵遞區號。 以下過程調用表單資料模型服務以將客戶資訊更新到資料庫：

1. 選取 **[!UICONTROL 提交]** 欄位並點選 **[!UICONTROL 編輯規則]** 表徵圖。 「規則編輯器」窗口隨即開啟。
1. 選取 **[!UICONTROL 提交 — 按一下]** 規則，並點選 **[!UICONTROL 編輯]** 表徵圖。 編輯提交規則的選項隨即出現。

   ![提交規則](assets/submit-rule.png)

   在WHEN選項中， **[!UICONTROL 提交]** 和 **[!UICONTROL 已點按]** 已選擇選項。

   ![submit-is-clicked](assets/submit-is-clicked.png)

1. 在 **[!UICONTROL THEN]** 選項，點選 **[!UICONTROL +添加語句]** 選項。 選擇 **[!UICONTROL 調用服務]** 從 **[!UICONTROL 選擇操作]** 下拉式清單。
1. 選取 **[!UICONTROL 更新發運地址]** 服務 **[!UICONTROL 選擇]** 下拉式清單。

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. 拖放 **[!UICONTROL 運送地址、州和郵遞區號]** 欄位 [!UICONTROL 表單物件] 頁簽至 **[!UICONTROL 拖放對象或在此處選擇]** 欄位 **[!UICONTROL 輸入]** 框。 所有以tablename為前置詞的欄位（例如，此使用案例中的customerdetails）都用作更新服務的輸入資料。 這些欄位中提供的所有內容都會在資料來源中更新。

   >[!NOTE]
   >
   >請勿拖放 **[!UICONTROL 名稱]** 和 **[!UICONTROL 客戶ID]** 欄位至對應的tablename.property（例如customerdetails.name）。 有助於避免錯誤更新客戶的名稱和ID。

1. 拖放 **[!UICONTROL 客戶ID]** 欄位 [!UICONTROL 表單物件] 標籤至 **[!UICONTROL 輸入]** 框。 不含前置詞tablename的欄位（例如，此使用案例中的customerdetails）可作為更新服務的搜尋參數。 此 **[!UICONTROL id]** 在此使用案例中，欄位可唯一識別  **customerdetails**  表格。
1. 點選 **[!UICONTROL 完成]** 來儲存規則。 在規則編輯器視窗上，點選 **[!UICONTROL 關閉]**.
1. 預覽最適化表單。 檢索客戶的詳細資訊、更新發運地址並提交表單。 當您再次檢索同一客戶的詳細資訊時，將顯示更新的發運地址。

## 步驟3:（額外章節）使用程式碼編輯器執行驗證並顯示錯誤訊息 {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

您應對表單執行驗證，以確保在表單中輸入的資料正確，並在資料不正確時顯示錯誤訊息。 例如，如果在表單中輸入了非現有客戶ID，則應會顯示錯誤訊息。

適用性表單提供數個內建驗證的元件，例如電子郵件和數值欄位，可用於常見使用案例。 對於高級使用案例，使用規則編輯器可在資料庫返回零(0)條記錄（無記錄）時顯示錯誤消息。

如果在表單中輸入的客戶ID不在資料庫中，則以下過程將說明如何建立規則以顯示錯誤消息。 規則也會將焦點引至並重設 **[!UICONTROL 客戶ID]** 欄位。 規則使用 [表單資料模型服務的dataIntegrationUtils API](/help/forms/using/invoke-form-data-model-services.md) 以檢查資料庫中是否存在客戶ID。

1. 點選 **[!UICONTROL 客戶ID]** 欄位並點選 `Edit Rules` 表徵圖。 此 [!UICONTROL 規則編輯器] 窗口。
1. 點選 **[!UICONTROL +建立]** 圖示來新增規則。 它會開啟視覺編輯器。

   在可視化編輯器中， **[!UICONTROL 當]** 預設情況下，會選取語句。 此外，表單物件(在此例中， **[!UICONTROL 客戶ID]**)，此時會在 **[!UICONTROL 當]** 語句。

1. 點選 **[!UICONTROL 選擇狀態]** 下拉式清單並選取 **[!UICONTROL 已變更]**.

   ![自訂變更時](assets/whencustomeridischanged.png)

   在 **[!UICONTROL THEN]** 語句，選擇 **[!UICONTROL 調用服務]** 從 **[!UICONTROL 選擇操作]** 下拉式清單。

1. 從 **[!UICONTROL 可視化編輯器]** to **[!UICONTROL 代碼編輯器]**. 開關控制項位於窗口的右側。 「代碼編輯器」隨即開啟，顯示類似下列的代碼：

   ![代碼編輯器](assets/code-editor.png)

1. 使用下列程式碼取代輸入變數區段：

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. 取代 `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` 區段及下列程式碼：

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

1. 預覽最適化表單。 輸入錯誤的客戶ID。 出現錯誤訊息。

   ![display-validation-error](assets/display-validation-error.gif)
