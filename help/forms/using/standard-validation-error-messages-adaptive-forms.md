---
title: 適用性表單的標準驗證錯誤訊息
seo-title: Standard validation error messages for adaptive forms
description: 使用自訂錯誤處理常式，將適用性表單的驗證錯誤訊息轉換為標準格式
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
exl-id: 54a76d5c-d19b-4026-b71c-7b9e862874bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---

# 適用性表單的標準驗證錯誤訊息 {#standard-validation-error-messages}

適用性表單會根據預先設定的驗證標準，驗證您在欄位中提供的輸入。 驗證條件會參考最適化表單中欄位可接受的輸入值。 您可以根據與最適化表單搭配使用的資料來源來設定驗證條件。 例如，如果您使用RESTful Web服務作為資料源，則可以在Swagger定義檔案中定義驗證標準。

如果輸入值符合驗證標準，則值會提交至資料來源。 否則，適用性表單會顯示錯誤訊息。

與此方法類似，適用性表單現在可與自訂服務整合，以執行資料驗證。 如果輸入值不符合驗證標準，且伺服器返回的驗證錯誤消息為標準消息格式，則錯誤消息在表單的欄位級別顯示。

如果輸入值不符合驗證標準，並且伺服器驗證錯誤消息不是標準消息格式，則適用性表單提供將驗證錯誤消息轉換為標準格式的機制，以便它們在表單的欄位級顯示。 您可以使用下列兩種方法之一，將錯誤訊息轉換為標準格式：

* 在最適化表單提交上新增自訂錯誤處理常式
* 使用規則編輯器將自訂處理常式新增至叫用服務動作

本文說明驗證錯誤訊息的標準格式，以及將錯誤訊息從自訂格式轉換為標準格式的指示。

## 標準驗證錯誤消息格式 {#standard-validation-message-format}

如果伺服器驗證錯誤訊息採用下列標準格式，適用性表單會在欄位層級顯示錯誤：

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]

        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
}
```

其中：

* `errorCausedBy` 說明失敗的原因
* `errors` 提及未通過驗證標準的欄位的SOM表達式以及驗證錯誤消息
* `originCode` 包含外部服務傳回的錯誤代碼
* `originMessage` 包含外部服務傳回的原始錯誤資料

## 設定最適化表單提交以新增自訂處理常式 {#configure-adaptive-form-submission}

如果伺服器驗證錯誤訊息未以標準格式顯示，您可以啟用非同步提交，並在適用性表單提交時新增自訂錯誤處理常式，將訊息轉換為標準格式。

### 設定非同步最適化表單提交 {#configure-asynchronous-adaptive-form-submission}

新增自訂處理常式之前，您必須設定非同步提交的最適化表單。 執行下列步驟：

1. 在最適化表單製作模式中，選取「表單容器」物件並點選 ![適用性表單屬性](assets/configure_icon.png) 來開啟其屬性。
1. 在 **[!UICONTROL 提交]** 屬性部分，啟用 **[!UICONTROL 使用非同步提交]**.
1. 選擇 **[!UICONTROL 在伺服器上重新驗證]** 在提交之前驗證伺服器上的輸入欄位值。
1. 選擇提交操作：

   * 選擇 **[!UICONTROL 使用表單資料模型提交]** 並選擇適當的資料模型（如果使用基於RESTful Web服務） [表單資料模型](work-with-form-data-model.md) 作為資料來源。
   * 選擇 **[!UICONTROL 提交到REST端點]** 和指定 **[!UICONTROL 重新導向URL/路徑]**，以使用RESTful網站服務作為資料來源。

   ![適用性表單提交屬性](assets/af_submission_properties.png)

1. 點選 ![儲存](assets/save_icon.png) 以儲存屬性。

### 在最適化表單提交上新增自訂錯誤處理常式 {#add-custom-error-handler-af-submission}

AEM Forms為表單提交提供現成可用的成功和錯誤處理常式。 處理常式是根據伺服器回應執行的用戶端函式。 提交表單時，將資料發送到伺服器進行驗證，伺服器會向客戶端返回一個響應，其中包含有關提交成功或錯誤事件的資訊。 資訊會以參數形式傳遞至相關處理常式，以執行函式。

執行下列步驟，在適用性表單提交上新增自訂錯誤處理常式：

1. 在製作模式中開啟最適化表單、選取任何表單物件，然後點選 <!--![Rule Editor](assets/af_edit_rules.png)--> 來開啟規則編輯器。
1. 選擇 **[!UICONTROL 表單]** 在「表單對象」樹中，並點選 **[!UICONTROL 建立]**.
1. 選擇 **[!UICONTROL 提交錯誤]** 從「事件」下拉式清單中。
1. 編寫規則以將自定義錯誤結構轉換為標準錯誤結構並點選 **[!UICONTROL 完成]** 來儲存規則。

以下是將自訂錯誤結構轉換為標準錯誤結構的范常式式碼：

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

此 `var som_map` 列出要轉換為標準格式的最適化表單欄位的SOM表達式。 您可以點選欄位並選取，以在最適化表單中檢視任何欄位的SOM運算式 **[!UICONTROL 查看SOM表達式]**.

此自訂錯誤處理常式會轉換 `var som_map` 格式。 因此，驗證錯誤訊息會以最適化表單的欄位層級顯示。

## 使用Invoke Service操作添加自定義處理程式

執行下列步驟來新增錯誤處理常式，以使用將自訂錯誤結構轉換為標準錯誤結構 [規則編輯器的](rule-editor.md) 調用服務操作：

1. 在製作模式中開啟最適化表單、選取任何表單物件，然後點選 ![規則編輯器](assets/rule_editor_icon.png) 來開啟規則編輯器。
1. 點選 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 當]** 區段。 例如，當[欄位名稱] 已變更。 選擇 **[!UICONTROL 已變更]** 從 **[!UICONTROL 選擇狀態]** 下拉式清單來達成此條件。
1. 在 **[!UICONTROL 然後]** 部分，選擇 **[!UICONTROL 調用服務]** 從 **[!UICONTROL 選擇操作]** 下拉式清單。
1. 從 **[!UICONTROL 輸入]** 區段。 例如，如果您要驗證 **名稱**, **ID**，和 **狀態** 欄位，選取貼文服務(pet)，然後選取pet.name、pet.id和pet.status(位於 **[!UICONTROL 輸入]** 區段。

因為此規則，您為輸入的值 **名稱**, **ID**，和 **狀態** 當步驟2中定義的欄位變更，且您從表單中的欄位中取出索引標籤時，欄位即會經過驗證。

1. 選擇 **[!UICONTROL 代碼編輯器]** 從「模式選擇」下拉清單中。
1. 點選 **[!UICONTROL 編輯代碼]**.
1. 從現有程式碼中刪除下列行：

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. 編寫規則以將自定義錯誤結構轉換為標準錯誤結構並點選 **[!UICONTROL 完成]** 來儲存規則。
例如，在結尾處新增下列范常式式碼，以將自訂錯誤結構轉換為標準錯誤結構：

   ```javascript
   var errorHandler = function(jqXHR, data) {
   var som_map = {
       "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
       "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
       "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
   };
   
   
   var errorJson = {};
   errorJson.errors = [];
   
   if (data) {
       if (data.originMessage) {
           var errorData;
           try {
               errorData = JSON.parse(data.originMessage);
           } catch (err) {
               // not in json format
           }
   
           if (errorData) {
               Object.keys(errorData).forEach(function(key) {
                   var som_key = som_map[key];
                   if (som_key) {
                       var error = {};
                       error.somExpression = som_key;
                       error.errorMessage = errorData[key];
                       errorJson.errors.push(error);
                   }
               });
           }
           window.guideBridge.handleServerValidationError(errorJson);
       } else {
           window.guideBridge.handleServerValidationError(data);
       }
     }
   };
   
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   此 `var som_map` 列出要轉換為標準格式的最適化表單欄位的SOM表達式。 您可以點選欄位並選取，以在最適化表單中檢視任何欄位的SOM運算式 **[!UICONTROL 查看SOM表達式]** 從 **[!UICONTROL 更多選項]** (...)功能表。

   請確定您將下列程式碼範例行複製到自訂錯誤處理常式：

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   executeOperation API包含 `null` 和 `errorHandler` 參數（以新的自訂錯誤處理常式為基礎）。

   此自訂錯誤處理常式會轉換 `var som_map` 格式。 因此，驗證錯誤訊息會以最適化表單的欄位層級顯示。
