---
title: 從自適應表單調用表單資料模型服務的API
seo-title: 從自適應表單調用表單資料模型服務的API
description: 說明可從最適化表單欄位中，用來叫用以WSDL編寫的Web服務的invokeWebServices API。
seo-description: 說明可從最適化表單欄位中，用來叫用以WSDL編寫的Web服務的invokeWebServices API。
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: 適用性表單
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# 從最適化表單{#api-to-invoke-form-data-model-service-from-adaptive-forms}叫用表單資料模型服務的API

## 概覽 {#overview}

AEM Forms公司使表單作者能夠從自適應表單欄位中調用表單資料模型中配置的服務，從而進一步簡化並增強表單填寫體驗。 若要叫用資料模型服務，您可以在視覺編輯器中建立規則，或在[規則編輯器](/help/forms/using/rule-editor.md)的程式碼編輯器中使用`guidelib.dataIntegrationUtils.executeOperation` API指定JavaScript。

本檔案著重於使用`guidelib.dataIntegrationUtils.executeOperation` API來編寫JavaScript以叫用服務。

## 使用API {#using-the-api}

`guidelib.dataIntegrationUtils.executeOperation` API會從最適化表單欄位中叫用服務。 API語法如下：

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

API結構指定服務操作的以下詳細資訊。

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
   <td>將一個或多個表單對象映射到從服務操作輸出值以填充表單欄位<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>根據服務操作的輸入參數返回值。 它是用作回呼函式的可選參數。<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>如果成功回呼函式無法根據輸入參數顯示輸出值，則顯示錯誤消息。 它是用作回呼函式的可選參數。<br /> </td>
  </tr>
 </tbody>
</table>

## 調用服務{#sample-script-to-invoke-a-service}的示例指令碼

以下示例指令碼使用`guidelib.dataIntegrationUtils.executeOperation` API調用`employeeAccount`表單資料模型中配置的`getAccountById`服務操作。

`getAccountById`操作將`employeeID`表單欄位中的值作為`empId`參數的輸入，並返回相應員工的員工姓名、帳戶編號和帳戶餘額。 輸出值會填入指定的表單欄位。 例如，`name`參數中的值會填入`fullName`表單元素中，而`account`表單元素中`accountNumber`參數的值會填入。

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

## 將API與回呼函式{#using-the-api-callback}搭配使用

您也可以使用具有回呼函式的`guidelib.dataIntegrationUtils.executeOperation` API來叫用表單資料模型服務。 API語法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

回呼函式可以具有`success`和`failure`回呼函式。

### 包含成功和失敗回呼函式的示例指令碼{#callback-function-success-failure}

以下示例指令碼使用`guidelib.dataIntegrationUtils.executeOperation` API調用`employeeOrder`表單資料模型中配置的`GETOrder`服務操作。

`GETOrder`操作將`Order ID`表單欄位中的值作為`orderId`參數的輸入，並返回`success`回調函式中的訂單量值。  如果`success`回呼函式未傳回訂購量，`failure`回呼函式會顯示`Error occured`訊息。

>[!NOTE]
>
> 如果您使用`success`回呼函式，則輸出值不會填入指定的表單欄位。

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
