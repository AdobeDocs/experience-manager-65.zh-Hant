---
title: 最適化表單的標準驗證錯誤訊息
seo-title: 最適化表單的標準驗證錯誤訊息
description: 使用自訂錯誤處理常式，將最適化表單的驗證錯誤訊息轉換為標準格式
seo-description: 使用自訂錯誤處理常式，將最適化表單的驗證錯誤訊息轉換為標準格式
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# 最適化表單{#standard-validation-error-messages}的標準驗證錯誤訊息

最適化表單會根據預先設定的驗證准則，驗證您在欄位中提供的輸入。 驗證准則參照最適化表單中欄位的可接受輸入值。 您可以根據與最適化表單搭配使用的資料來源來設定驗證准則。 例如，如果您使用REST風格的Web服務作為資料源，則可以在Swagger定義檔案中定義驗證標準。

如果輸入值符合驗證標準，則會將值提交至資料來源。 否則，最適化表單會顯示錯誤訊息。

與此方法類似，可調式表單現在可與自訂服務整合，以執行資料驗證。 如果輸入值不符合驗證標準，且伺服器傳回的驗證錯誤訊息為標準訊息格式，則錯誤訊息會在表單的欄位層級顯示。

如果輸入值不滿足驗證標準並且伺服器驗證錯誤消息不是標準消息格式，則自適應表單提供將驗證錯誤消息轉換為標準格式以便它們在表單的欄位級顯示的機制。 您可以使用下列兩種方法中的任一種，將錯誤訊息轉換為標準格式：

* 在最適化表單提交中新增自訂錯誤處理常式
* 使用規則編輯器將自訂處理常式新增至叫用服務動作

本文介紹了驗證錯誤消息的標準格式以及將錯誤消息從自定義格式轉換為標準格式的說明。

## 標準驗證錯誤消息格式{#standard-validation-message-format}

如果伺服器驗證錯誤消息採用以下標準格式，則自適應表單將在欄位級別顯示錯誤：

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
* `originCode` 包含外部服務傳回的錯誤碼
* `originMessage` 包含外部服務傳回的原始錯誤資料

## 配置自適應表單提交以添加自定義處理程式{#configure-adaptive-form-submission}

如果伺服器驗證錯誤消息未以標準格式顯示，則可以啟用非同步提交並在自適應表單提交中添加自定義錯誤處理程式，以將消息轉換為標準格式。

### 配置非同步自適應表單提交{#configure-asynchronous-adaptive-form-submission}

在新增自訂處理常式之前，您必須設定非同步提交的最適化表單。 執行下列步驟：

1. 在最適化表單製作模式中，選取「表單容器」物件，並點選![最適化表單屬性](assets/configure_icon.png)以開啟其屬性。
1. 在&#x200B;**[!UICONTROL Submission]**&#x200B;屬性區段中，啟用&#x200B;**[!UICONTROL 使用非同步提交]**。
1. 選擇&#x200B;**[!UICONTROL 重新驗證server]**&#x200B;以在提交之前驗證伺服器上的輸入欄位值。
1. 選擇提交操作：

   * 如果使用基於[表單資料模型](work-with-form-data-model.md)的REST風格Web服務作為資料源，請選擇&#x200B;**[!UICONTROL 使用表單資料模型]**&#x200B;提交並選擇相應的資料模型。
   * 如果您使用REST風格的Web服務作為資料源，請選擇&#x200B;**[!UICONTROL 提交到REST端點]**&#x200B;並指定&#x200B;**[!UICONTROL 重定向URL/路徑]**。

   ![自適應表單提交屬性](assets/af_submission_properties.png)

1. 點選![Save](assets/save_icon.png)以儲存屬性。

### 在最適化表單提交{#add-custom-error-handler-af-submission}中新增自訂錯誤處理常式

AEM Forms為表單提交提供現成可用的成功與錯誤處理常式。 處理常式是根據伺服器回應執行的用戶端函式。 當提交表單時，資料會傳送至伺服器進行驗證，而伺服器會傳回回應給用戶端，其中包含提交成功或錯誤事件的相關資訊。 這些資訊會作為參數傳遞給相關處理常式，以執行函式。

執行下列步驟，在最適化表單提交上新增自訂錯誤處理常式：

1. 在編寫模式中開啟最適化表單，選取任何表單物件，然後點選<!--![Rule Editor](assets/af_edit_rules.png)-->以開啟規則編輯器。
1. 在「表單對象」樹中選擇「**[!UICONTROL 表單]**」，然後按一下「建立&#x200B;**[!UICONTROL 」。]**
1. 從「事件」下拉式清單中選擇「提交時出錯」。****
1. 撰寫規則，將自訂錯誤結構轉換為標準錯誤結構，並點選&#x200B;**[!UICONTROL Done]**&#x200B;以儲存規則。

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

`var som_map`列出了要轉換為標準格式的自適應表單欄位的SOM表達式。 通過點選該欄位並選擇「查看SOM表達式」(**[!UICONTROL View SOM Expression)]**，可以以自適應形式查看任何欄位的SOM表達式。

使用此自定義錯誤處理程式，最適化表單會將`var som_map`中列出的欄位轉換為標準錯誤消息格式。 因此，驗證錯誤訊息會以自適應表單的欄位層級顯示。

## 使用Invoke Service動作新增自訂處理常式

執行以下步驟，使用[規則編輯器的](rule-editor.md)叫用服務操作添加錯誤處理程式，將自定義錯誤結構轉換為標準錯誤結構：

1. 在編寫模式中開啟最適化表單，選取任何表單物件，然後點選「規則編輯器」以開啟規則編輯器。![](assets/rule_editor_icon.png)
1. 點選&#x200B;**[!UICONTROL Create]**。
1. 在規則的&#x200B;**[!UICONTROL When]**&#x200B;區段中建立條件。 例如，當欄位]的名稱變更時。 [從&#x200B;**[!UICONTROL 選擇狀態]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL 變更]**&#x200B;以達成此條件。
1. 在&#x200B;**[!UICONTROL Then]**&#x200B;區段中，從&#x200B;**[!UICONTROL 選擇操作]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL 調用服務]**。
1. 從&#x200B;**[!UICONTROL Input]**&#x200B;部分選擇Post服務及其相應的資料綁定。 例如，如果您想要驗證最適化形式的&#x200B;**Name**、**ID**&#x200B;和&#x200B;**Status**&#x200B;欄位，請選取貼文服務(pet)，然後在&#x200B;**[!UICONTROL Input]**&#x200B;區段中選取pet.name、pet.id和pet.status。

根據此規則，當步驟2中定義的欄位變更且您從表單中的欄位中跳出時，您為&#x200B;**Name**、**ID**&#x200B;和&#x200B;**Status**&#x200B;欄位輸入的值會立即生效。

1. 從模式選擇下拉清單中選擇&#x200B;**[!UICONTROL 代碼編輯器]**。
1. 點選&#x200B;**[!UICONTROL 編輯代碼]**。
1. 從現有代碼中刪除以下行：

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. 撰寫規則，將自訂錯誤結構轉換為標準錯誤結構，並點選&#x200B;**[!UICONTROL Done]**以儲存規則。
例如，在結尾加入下列范常式式碼，將自訂錯誤結構轉換為標準錯誤結構：

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

   `var som_map`列出了要轉換為標準格式的自適應表單欄位的SOM表達式。 通過點選該欄位並從&#x200B;**[!UICONTROL 更多選項]**(...)菜單中選擇&#x200B;**[!UICONTROL 查看SOM表達式]**，可以以自適應形式查看任何欄位的SOM表達式。

   請確定您將范常式式碼的下列行複製至自訂錯誤處理常式：

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   executeOperation API包含基於新自訂錯誤處理常式的`null`和`errorHandler`參數。

   使用此自定義錯誤處理程式，最適化表單會將`var som_map`中列出的欄位轉換為標準錯誤消息格式。 因此，驗證錯誤訊息會以自適應表單的欄位層級顯示。