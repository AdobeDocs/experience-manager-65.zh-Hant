---
title: 從自適應表單調用表單資料模型服務的API
seo-title: 從自適應表單調用表單資料模型服務的API
description: 說明可從最適化表單欄位中，用來叫用以WSDL編寫的Web服務的invokeWebServices API。
seo-description: 說明可從最適化表單欄位中，用來叫用以WSDL編寫的Web服務的invokeWebServices API。
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---


# 從自適應表單調用表單資料模型服務的API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 概覽 {#overview}

AEM Forms可讓表單作者從最適化表單欄位中叫用表單資料模型中設定的服務，進一步簡化並增強表單填寫體驗。 若要叫用資料模型服務，您可以在視覺化編輯器中建立規則，或在規則編輯器的程式碼編輯器中使用 `guidelib.dataIntegrationUtils.executeOperation` API指定 [JavaScript](/help/forms/using/rule-editor.md)。

本檔案著重於使用 `guidelib.dataIntegrationUtils.executeOperation` API來叫用服務來編寫JavaScript。

## 使用API {#using-the-api}

API `guidelib.dataIntegrationUtils.executeOperation` 從最適化表單欄位叫用服務。 API語法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

API的結構會指 `guidelib.dataIntegrationUtils.executeOperation` 定服務作業的詳細資訊。 結構的語法如下。

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

## 調用服務的示例指令碼 {#sample-script-to-invoke-a-service}

以下範例指令碼使用 `guidelib.dataIntegrationUtils.executeOperation` API來叫用表單資 `getAccountById` 料模型中設定的 `employeeAccount` 服務作業。

此操 `getAccountById` 作將表單欄位中的值作為參數的輸 `employeeID``empId` 入，並返回相應員工的員工姓名、帳戶編號和帳戶餘額。 輸出值會填入指定的表單欄位。 例如，參數中的值會 `name` 填入表單元素中， `fullName` 而表單元素中 `accountNumber` 的參數值 `account` 中。

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

## 使用API與回呼函式 {#using-the-api-callback}

您也可以使用具有回呼函式的 `guidelib.dataIntegrationUtils.executeOperation` API來叫用表單資料模型服務。 API語法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

回呼函式可以有回呼 `success` 函式 `failure` 和函式。

### 包含成功與失敗回呼函式的範例指令碼 {#callback-function-success-failure}

以下範例指令碼使用 `guidelib.dataIntegrationUtils.executeOperation` API來叫用表單資 `GETOrder` 料模型中設定的 `employeeOrder` 服務作業。

操 `GETOrder` 作將表單域中的值作 `Order ID` 為參數的輸入，並返回回 `orderId` 調函式中的訂單量 `success` 值。  如果回 `success` 調函式未傳回訂單量，則回 `failure` 調函式會顯示訊 `Error occured` 息。

>[!NOTE]
>
> 如果您使用 `success` 回呼函式，輸出值不會填入指定的表單欄位。

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
