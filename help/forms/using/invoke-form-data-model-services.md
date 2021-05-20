---
title: 從適用性表單叫用表單資料模型服務的API
seo-title: 從適用性表單叫用表單資料模型服務的API
description: 說明可用來從適用性表單欄位中叫用在WSDL中寫入的Web服務的invokeWebServices API。
seo-description: 說明可用來從適用性表單欄位中叫用在WSDL中寫入的Web服務的invokeWebServices API。
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: 適用性表單
exl-id: cf037174-3153-486f-85b1-c974cd5a1ace
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 從適用性表單叫用表單資料模型服務的API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 概覽 {#overview}

AEM Forms可讓表單作者從最適化表單欄位中叫用在表單資料模型中設定的服務，進一步簡化並增強表單填寫體驗。 若要叫用資料模型服務，您可以在可視化編輯器中建立規則，或使用[規則編輯器](/help/forms/using/rule-editor.md)的代碼編輯器中的`guidelib.dataIntegrationUtils.executeOperation` API指定JavaScript。

本檔案著重於使用`guidelib.dataIntegrationUtils.executeOperation` API來叫用服務來編寫JavaScript。

## 使用API {#using-the-api}

`guidelib.dataIntegrationUtils.executeOperation` API從適用性表單欄位內叫用服務。 API語法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

`guidelib.dataIntegrationUtils.executeOperation` API的結構指定了有關服務操作的詳細資訊。 結構的語法如下。

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API結構會指定服務操作的下列詳細資訊。

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>用於指定表單資料模型標識符、操作標題和操作名稱的結構</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>指定表單資料模型的儲存庫路徑，包括其名稱</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>指定要執行的服務操作的名稱</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>將一個或多個表單對象映射到服務操作的輸入參數</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>映射一個或多個表單對象以從服務操作輸出值以填充表單欄位<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>根據服務操作的輸入參數返回值。 這是用作回調函式的可選參數。<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>如果成功回呼函式無法根據輸入引數顯示輸出值，則顯示錯誤訊息。 這是用作回調函式的可選參數。<br /> </td>
  </tr>
 </tbody>
</table>

## 調用服務{#sample-script-to-invoke-a-service}的示例指令碼

以下示例指令碼使用`guidelib.dataIntegrationUtils.executeOperation` API調用`employeeAccount`表單資料模型中配置的`getAccountById`服務操作。

`getAccountById`操作將`employeeID`表單欄位中的值作為`empId`參數的輸入，並返回相應員工的員工名稱、帳號和帳戶餘額。 輸出值會填入指定的表單欄位中。 例如， `name`引數中的值會填入`fullName`表單元素中，以及`account`表單元素中`accountNumber`引數的值。

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## 使用API搭配回呼函式{#using-the-api-callback}

您也可以使用具有回撥函式的`guidelib.dataIntegrationUtils.executeOperation` API叫用表單資料模型服務。 API語法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

回呼函式可以有`success`和`failure`回呼函式。

### 具有成功和失敗回呼函式的指令碼示例{#callback-function-success-failure}

以下示例指令碼使用`guidelib.dataIntegrationUtils.executeOperation` API調用`employeeOrder`表單資料模型中配置的`GETOrder`服務操作。

`GETOrder`操作將`Order ID`表單欄位中的值作為`orderId`參數的輸入，並在`success`回調函式中返回訂單量值。  如果`success`回呼函式未傳回訂單量， `failure`回呼函式會顯示`Error occured`訊息。

>[!NOTE]
>
> 如果您使用`success`回呼函式，則輸出值不會填入指定的表單欄位中。

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
