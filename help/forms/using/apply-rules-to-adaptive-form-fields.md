---
title: 「不要發佈教學課程：套用規則至最適化表單欄位」
seo-title: 將規則套用至最適化表單欄位
description: 建立規則，將互動功能、商業邏輯和智慧驗證新增至最適化表單。
seo-description: 建立規則，將互動功能、商業邏輯和智慧驗證新增至最適化表單。
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
translation-type: tm+mt
source-git-commit: e3ecf724cdfcd20ef4c089605e644ad10ef1221b
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# 教學課程：將規則套用至最適化表單欄位{#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

本教程是[建立第一個自適應表單](/help/forms/using/create-your-first-adaptive-form.md)系列中的一個步驟。 Adobe建議依序依時間順序執行系列，以瞭解、執行和展示完整的教學課程使用案例。

## 關於教學課程{#about-the-tutorial}

您可以使用規則將互動功能、商業邏輯和智慧驗證新增至最適化表單。 最適化表單有內建的規則編輯器。 規則編輯器提供拖放功能，類似於引導導覽。 拖放方法是建立規則最快速最簡單的方法。 規則編輯器也為有興趣測試其編碼技巧或將規則提升到新層次的使用者提供程式碼視窗。

您可在[最適化表單規則編輯器](/help/forms/using/rule-editor.md)中進一步瞭解規則編輯器。

在教學課程結束時，您將學習如何建立規則以：

* 調用表單資料模型服務以從資料庫中檢索資料
* 調用表單資料模型服務以向資料庫添加資料
* 運行驗證檢查並顯示錯誤消息

教學課程各節結尾的互動式GIF影像可協助您即時學習並驗證所建立表格的功能。

## 步驟1:從資料庫{#retrieve-customer-record}檢索客戶記錄

您遵循[建立表單資料模型](/help/forms/using/create-form-data-model.md)文章，建立表單資料模型。 現在，您可以使用規則編輯器來調用Forms Data Model Services以檢索資訊並將資訊添加到資料庫。

每個客戶都會獲得一個唯一的客戶ID號碼，有助於識別資料庫中的相關客戶資料。 以下過程使用客戶ID從資料庫中檢索資訊：

1. 開啟最適化表單以進行編輯。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 點選「**[!UICONTROL 客戶ID]**」欄位，然後點選「編輯規則&#x200B;]**」圖示。**[!UICONTROL 「規則編輯器」(Rule Editor)窗口隨即開啟。
1. 點選&#x200B;**[!UICONTROL + Create]**&#x200B;圖示以新增規則。 它會開啟視覺編輯器。

   在可視編輯器中，預設情況下選擇&#x200B;**[!UICONTROL WHEN]**&#x200B;語句。 此外，在&#x200B;**[!UICONTROL WHEN]**&#x200B;陳述式中，也會指定您啟動規則編輯器時的表單物件（在此例中為&#x200B;**[!UICONTROL 客戶ID]**）。

1. 點選「**[!UICONTROL 選擇狀態]**」下拉式清單，然後選取「**[!UICONTROL 變更]**」。

   ![when customdischanged](assets/whencustomeridischanged.png)

1. 在&#x200B;**[!UICONTROL THEN]**&#x200B;語句中，從&#x200B;**[!UICONTROL 選擇操作]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL 調用服務]**。
1. 從&#x200B;**[!UICONTROL 選擇]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL 檢索發運地址]**&#x200B;服務。
1. 將「表單物件」標籤中的&#x200B;**[!UICONTROL 客戶ID]**&#x200B;欄位拖放至&#x200B;**[!UICONTROL 拖放物件，或在**[!UICONTROL  INPUT ]**方塊中選取此處]**&#x200B;欄位。

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 將「表單物件」標籤中的「**[!UICONTROL 客戶ID、名稱、運送地址、狀態和郵遞區號」欄位拖放至「**[!UICONTROL &#x200B;拖放」物件，或在「**[!UICONTROL OUTPUT]**」方塊中選取此處的「]**」欄位。]**

   ![dropobjectstoutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   點選&#x200B;**[!UICONTROL Done]**&#x200B;以儲存規則。 在規則編輯器窗口中，按一下&#x200B;**[!UICONTROL Close]**。

1. 預覽最適化表單。 在&#x200B;**[!UICONTROL 客戶ID]**&#x200B;欄位中輸入ID。 表單現在可以從資料庫擷取客戶詳細資訊。

   ![檢索資訊](assets/retrieve-information.gif)

## 步驟2:將更新的客戶地址添加到資料庫{#updated-customer-address}

從資料庫擷取客戶詳細資訊後，您就可以更新送貨地址、州和郵遞區號。 以下過程調用表單資料模型服務，將客戶資訊更新到資料庫：

1. 選擇&#x200B;**[!UICONTROL Submit]**&#x200B;欄位，然後點選&#x200B;**[!UICONTROL 編輯規則]**&#x200B;圖示。 「規則編輯器」(Rule Editor)窗口隨即開啟。
1. 選擇&#x200B;**[!UICONTROL 提交——按一下]**&#x200B;規則並點選&#x200B;**[!UICONTROL 編輯]**&#x200B;表徵圖。 此時會出現編輯「提交」規則的選項。

   ![submit-rule](assets/submit-rule.png)

   在WHEN選項中，已選擇&#x200B;**[!UICONTROL Submit]**&#x200B;和&#x200B;**[!UICONTROL 被按一下]**&#x200B;選項。

   ![submit-is-clicked](assets/submit-is-clicked.png)

1. 在&#x200B;**[!UICONTROL THEN]**&#x200B;選項中，點選&#x200B;**[!UICONTROL + Add Statement]**&#x200B;選項。 從&#x200B;**[!UICONTROL 選擇操作]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL 調用服務]**。
1. 從&#x200B;**[!UICONTROL 選擇]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL 更新送貨地址]**&#x200B;服務。

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. 將[!UICONTROL 表單物件]標籤中的&#x200B;**[!UICONTROL 運送位址、狀態和郵遞區號]**&#x200B;欄位拖放至&#x200B;**[!UICONTROL 拖曳物件的**[!UICONTROL &#x200B;對應標籤名稱。property（例如customerdetails .shippingAddress），或在&lt;a6/>INPUT&lt;a>中選取此處&#x200B;]**欄位7/>方塊。]**&#x200B;所有前置有tablename的欄位（例如，此使用案例中的customerdetails）都是更新服務的輸入資料。 這些欄位中提供的所有內容都會在資料來源中更新。

   >[!NOTE]
   >
   >請勿將&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Customer ID]**&#x200B;欄位拖放至對應的tablename.property（例如customerdetails.name）。 它有助於避免錯誤地更新客戶的名稱和ID。

1. 將[!UICONTROL 表單物件]標籤中的&#x200B;**[!UICONTROL 客戶ID]**&#x200B;欄位拖放至&#x200B;**[!UICONTROL INPUT]**&#x200B;方塊中的id欄位。 沒有前置詞表名的欄位（例如，此使用案例中的客戶詳細資訊）用作更新服務的搜索參數。 此使用案例中的&#x200B;**[!UICONTROL id]**&#x200B;欄位唯一標識&#x200B;**customerdetails**&#x200B;表中的記錄。
1. 點選&#x200B;**[!UICONTROL Done]**&#x200B;以儲存規則。 在規則編輯器窗口中，按一下&#x200B;**[!UICONTROL Close]**。
1. 預覽最適化表單。 擷取客戶的詳細資訊、更新運送地址並提交表單。 當您再次檢索同一客戶的詳細資訊時，將顯示更新的發運地址。

## 步驟3:（附加部分）使用代碼編輯器運行驗證並顯示錯誤消息{#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

您應對表單執行驗證，以確保在表單中輸入的資料正確無誤，並在資料不正確時顯示錯誤訊息。 例如，如果在表單中輸入了非現有的客戶ID，則應顯示錯誤訊息。

最適化表單提供多個內建驗證的元件，例如電子郵件和數值欄位，您可用於一般使用案例。 使用規則編輯器進行進階使用案例，例如，當資料庫傳回零(0)記錄（無記錄）時，顯示錯誤訊息。

以下過程說明如何建立規則以在表單中輸入的客戶ID不存在於資料庫中時顯示錯誤消息。 此規則也會將焦點引入並重設&#x200B;**[!UICONTROL 客戶ID]**&#x200B;欄位。 該規則使用[表單data model service](/help/forms/using/invoke-form-data-model-services.md)的dataIntegrationUtils API來檢查資料庫中是否存在客戶ID。

1. 點選&#x200B;**[!UICONTROL Customer ID]**&#x200B;欄位，然後點選`Edit Rules`圖示。 將開啟[!UICONTROL 規則編輯器]窗口。
1. 點選&#x200B;**[!UICONTROL + Create]**&#x200B;圖示以新增規則。 它會開啟視覺編輯器。

   在可視編輯器中，預設情況下選擇&#x200B;**[!UICONTROL WHEN]**&#x200B;語句。 此外，在&#x200B;**[!UICONTROL WHEN]**&#x200B;陳述式中，也會指定您啟動規則編輯器時的表單物件（在此例中為&#x200B;**[!UICONTROL 客戶ID]**）。

1. 點選「**[!UICONTROL 選擇狀態]**」下拉式清單，然後選取「**[!UICONTROL 變更]**」。

   ![when customdischanged](assets/whencustomeridischanged.png)

   在&#x200B;**[!UICONTROL THEN]**&#x200B;語句中，從&#x200B;**[!UICONTROL 選擇操作]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL 調用服務]**。

1. 從&#x200B;**[!UICONTROL 可視編輯器]**&#x200B;切換到&#x200B;**[!UICONTROL 代碼編輯器]**。 開關控制器位於窗口的右側。 程式碼編輯器隨即開啟，顯示類似下列的程式碼：

   ![程式碼編輯器](assets/code-editor.png)

1. 以下列程式碼取代輸入變數區段：

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

1. 預覽最適化表單。 輸入錯誤的客戶ID。 出現錯誤資訊。

   ![display-validation-error](assets/display-validation-error.gif)

