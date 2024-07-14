---
title: 將規則套用至最適化表單欄位
description: 建立規則，將互動性、商業邏輯和智慧型驗證新增至最適化表單。
page-status-flag: de-activated
products: SG_EXPERIENCEMANAGER/6.3/FORMS
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---

# 教學課程：將規則套用至最適化表單欄位 {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

本教學課程是[建立第一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md)系列中的步驟。 Adobe建議您依照時間順序進行序列學習，以瞭解、執行並示範完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

您可以使用規則將互動性、商業邏輯和智慧型驗證新增至最適化表單。 調適型表單有內建規則編輯器。 規則編輯器提供與引導式導覽類似的拖放功能。 拖放方法是最快速且最簡單的規則建立方法。 規則編輯器也會為有興趣測試其程式碼技能或將規則提升到更高層級的使用者提供程式碼視窗。

您可以在[最適化Forms規則編輯器](/help/forms/using/rule-editor.md)進一步瞭解規則編輯器。

在本教學課程結束時，您將學習如何建立規則以：

* 啟動表單資料模型服務，從資料庫擷取資料
* 啟動表單資料模型服務，將資料新增至資料庫
* 執行驗證檢查並顯示錯誤訊息

教學課程每個區段結尾的互動式GIF影像可協助您即時學習及驗證您所建置表單的功能。

## 步驟1：從資料庫擷取客戶記錄 {#retrieve-customer-record}

您已依照[建立表單資料模型](/help/forms/using/create-form-data-model.md)文章建立表單資料模型。 現在，您可以使用規則編輯器來叫用Forms資料模型服務，以擷取資訊並新增至資料庫。

每個客戶都會獲派一個唯一的客戶ID號碼，這有助於識別資料庫中的相關客戶資料。 下列程式使用客戶ID從資料庫擷取資訊：

1. 開啟最適化表單進行編輯。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 選取&#x200B;**[!UICONTROL 客戶識別碼]**&#x200B;欄位，並選取&#x200B;**[!UICONTROL 編輯規則]**&#x200B;圖示。 「規則編輯器」視窗隨即開啟。
1. 選取「**[!UICONTROL +建立]**」圖示以新增規則。 這會開啟視覺化編輯器。

   在視覺化編輯器中，預設會選取&#x200B;**[!UICONTROL WHEN]**&#x200B;陳述式。 此外，**[!UICONTROL WHEN]**&#x200B;陳述式中會指定您啟動規則編輯器的表單物件（在此案例中為&#x200B;**[!UICONTROL 客戶識別碼]**）。

1. 選取&#x200B;**[!UICONTROL 選取狀態]**&#x200B;下拉式清單，並選取&#x200B;**[!UICONTROL 已變更]**。

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

1. 在&#x200B;**[!UICONTROL THEN]**&#x200B;陳述式中，從&#x200B;**[!UICONTROL 選取動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 叫用服務]**。
1. 從&#x200B;**[!UICONTROL 選取]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 擷取送貨地址]**&#x200B;服務。
1. 從[表單物件]索引標籤將&#x200B;**[!UICONTROL 客戶識別碼]**&#x200B;欄位拖放到&#x200B;**[!UICONTROL 拖放物件，或在**[!UICONTROL &#x200B;輸入&#x200B;]**方塊中選取這裡]**&#x200B;欄位。

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 從[表單物件]索引標籤將&#x200B;**[!UICONTROL 客戶ID、名稱、送貨地址、狀態和郵遞區號]**&#x200B;欄位拖放到&#x200B;**[!UICONTROL 放置物件，或在**[!UICONTROL &#x200B;輸出&#x200B;]**方塊中選取這裡]**&#x200B;欄位。

   ![dropobjectstooutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存規則。 在規則編輯器視窗中，選取&#x200B;**[!UICONTROL 關閉]**。

1. 預覽最適化表單。 在&#x200B;**[!UICONTROL 客戶識別碼]**&#x200B;欄位中輸入ID。 該表單現在可以從資料庫擷取客戶詳細資訊。

   ![擷取資訊](assets/retrieve-information.gif)

## 步驟2：將更新的客戶地址新增至資料庫 {#updated-customer-address}

從資料庫擷取客戶詳細資料後，您可以更新送貨地址、州別和郵遞區號。 下列程式會叫用「表單資料模型」服務，將客戶資訊更新至資料庫：

1. 選取&#x200B;**[!UICONTROL 提交]**&#x200B;欄位並選取&#x200B;**[!UICONTROL 編輯規則]**&#x200B;圖示。 「規則編輯器」視窗隨即開啟。
1. 選取&#x200B;**[!UICONTROL 提交 — 按一下]**&#x200B;規則並選取&#x200B;**[!UICONTROL 編輯]**&#x200B;圖示。 編輯提交規則的選項隨即顯示。

   ![提交規則](assets/submit-rule.png)

   在WHEN選項中，已選取&#x200B;**[!UICONTROL 已點按]**&#x200B;及&#x200B;**[!UICONTROL 已點按]**&#x200B;選項。

   ![已點按](assets/submit-is-clicked.png)

1. 在&#x200B;**[!UICONTROL THEN]**&#x200B;選項中，選取&#x200B;**[!UICONTROL +新增陳述式]**&#x200B;選項。 從&#x200B;**[!UICONTROL 選取動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 啟動服務]**。
1. 從&#x200B;**[!UICONTROL 選取]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 更新送貨地址]**&#x200B;服務。

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. 從[!UICONTROL 表單物件]索引標籤將&#x200B;**[!UICONTROL 送貨地址、狀態和郵遞區號]**&#x200B;欄位拖放到&#x200B;**[!UICONTROL Drop物件的對應tablename .property （例如customerdetails .shippingAddress），或在**[!UICONTROL  INPUT ]**方塊中選取這裡]**&#x200B;欄位。 所有前置詞為tablename的欄位（例如，在此使用案例中為customerdetails）都會當作更新服務的輸入資料。 這些欄位中提供的所有內容都會在資料來源中更新。

   >[!NOTE]
   >
   >請勿將&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL 客戶ID]**&#x200B;欄位拖放至對應的tablename.property （例如customerdetails.name）。 它有助於避免錯誤地更新客戶的名稱和ID。

1. 將&#x200B;**[!UICONTROL 客戶ID]**&#x200B;欄位從[!UICONTROL 表單物件]標籤拖放至&#x200B;**[!UICONTROL 輸入]**&#x200B;方塊中的ID欄位。 沒有前置字元Tablename的欄位（例如，此使用案例中的Customerdetails）會作為更新服務的搜尋引數。 此使用案例中的&#x200B;**[!UICONTROL id]**&#x200B;欄位可唯一識別&#x200B;**customerdetails**&#x200B;資料表中的記錄。
1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存規則。 在規則編輯器視窗中，選取&#x200B;**[!UICONTROL 關閉]**。
1. 預覽最適化表單。 擷取客戶的詳細資料、更新送貨地址並提交表單。 當您再次擷取相同客戶的詳細資料時，會顯示更新的送貨地址。

## 步驟3： （額外區段）使用程式碼編輯器執行驗證並顯示錯誤訊息 {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

您應該對表單執行驗證，以確保在表單中輸入的資料正確無誤，並且在資料不正確時會顯示錯誤訊息。 例如，如果在表單中輸入不存在的客戶ID，則會顯示錯誤訊息。

調適型表單提供具備內建驗證的元件，例如電子郵件和數值欄位，您可將其用於常見使用案例。 針對進階使用案例，使用規則編輯器，例如在資料庫傳回零(0)筆記錄（無記錄）時，顯示錯誤訊息。

下列程式說明如果表單中輸入的客戶ID不存在於資料庫中，如何建立規則以顯示錯誤訊息。 此規則也會將焦點帶到&#x200B;**[!UICONTROL 客戶ID]**&#x200B;欄位並重設。 規則使用表單資料模型服務](/help/forms/using/invoke-form-data-model-services.md)的[dataIntegrationUtils API來檢查資料庫中是否有客戶ID。

1. 選取&#x200B;**[!UICONTROL 客戶識別碼]**&#x200B;欄位，並選取`Edit Rules`圖示。 [!UICONTROL 規則編輯器]視窗隨即開啟。
1. 選取「**[!UICONTROL +建立]**」圖示以新增規則。 這會開啟視覺化編輯器。

   在視覺化編輯器中，預設會選取&#x200B;**[!UICONTROL WHEN]**&#x200B;陳述式。 此外，**[!UICONTROL WHEN]**&#x200B;陳述式中會指定您啟動規則編輯器的表單物件（在此案例中為&#x200B;**[!UICONTROL 客戶識別碼]**）。

1. 選取&#x200B;**[!UICONTROL 選取狀態]**&#x200B;下拉式清單，並選取&#x200B;**[!UICONTROL 已變更]**。

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

   在&#x200B;**[!UICONTROL THEN]**&#x200B;陳述式中，從&#x200B;**[!UICONTROL 選取動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 叫用服務]**。

1. 從&#x200B;**[!UICONTROL 視覺化編輯器]**&#x200B;切換至&#x200B;**[!UICONTROL 程式碼編輯器]**。 切換器控制項位於視窗的右側。 程式碼編輯器隨即開啟，顯示類似下列的程式碼：

   ![程式碼編輯器](assets/code-editor.png)

1. 將輸入變數區段取代為下列程式碼：

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. 以下列程式碼取代`guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)`區段：

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

1. 預覽最適化表單。 輸入不正確的客戶ID。 出現錯誤訊息。

   ![display-validation-error](assets/display-validation-error.gif)
