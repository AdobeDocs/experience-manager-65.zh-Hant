---
title: 從適用性表單叫用表單資料模型服務的API
seo-title: API to invoke form data model service from adaptive forms
description: 說明可用來從適用性表單欄位中叫用在WSDL中寫入的Web服務的invokeWebServices API。
seo-description: Explains the invokeWebServices API that you can use to invoke web services written in WSDL from within an adaptive form field.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms
exl-id: cf037174-3153-486f-85b1-c974cd5a1ace
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 從適用性表單叫用表單資料模型服務的API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 概觀 {#overview}

AEM Forms可讓表單作者從最適化表單欄位中叫用在表單資料模型中設定的服務，進一步簡化並增強表單填寫體驗。 若要叫用資料模型服務，您可以在視覺編輯器中建立規則，或使用 `guidelib.dataIntegrationUtils.executeOperation` API(位於 [規則編輯器](/help/forms/using/rule-editor.md).

本檔案著重於使用 `guidelib.dataIntegrationUtils.executeOperation` 叫用服務的API。

## 使用API {#using-the-api}

此 `guidelib.dataIntegrationUtils.executeOperation` API從適用性表單欄位中叫用服務。 API語法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

的結構 `guidelib.dataIntegrationUtils.executeOperation` API指定服務操作的詳細資訊。 結構的語法如下。

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
   <td>根據服務操作的輸入參數返回值。 此為選用參數，用作回呼函式。<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>如果成功回呼函式無法根據輸入引數顯示輸出值，則顯示錯誤訊息。 此為選用參數，用作回呼函式。<br /> </td>
  </tr>
 </tbody>
</table>

## 叫用服務的範例指令碼 {#sample-script-to-invoke-a-service}

下列範例指令碼使用 `guidelib.dataIntegrationUtils.executeOperation` 叫用 `getAccountById` 在中配置的服務操作 `employeeAccount` 表單資料模型。

此 `getAccountById` 操作會採用 `employeeID` 表單欄位作為輸入 `empId` 參數和返回相應員工的員工名稱、帳號和帳戶餘額。 輸出值會填入指定的表單欄位中。 例如， `name` 引數會填入 `fullName` 表單元素和值 `accountNumber` 引數 `account` 表單元素。

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

## 使用API搭配回呼函式 {#using-the-api-callback}

您也可以使用 `guidelib.dataIntegrationUtils.executeOperation` 具有回撥函式的API。 API語法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

回叫函式可以 `success` 和 `failure` 回呼函式。

### 具有成功和失敗回呼函式的範例指令碼 {#callback-function-success-failure}

下列範例指令碼使用 `guidelib.dataIntegrationUtils.executeOperation` 叫用 `GETOrder` 在中配置的服務操作 `employeeOrder` 表單資料模型。

此 `GETOrder` 操作會採用 `Order ID` 表單欄位作為輸入 `orderId` 引數並傳回訂單數量值(位於 `success` 回呼函式。  若 `success` callback函式不會傳回訂購量， `failure` 回呼函式顯示 `Error occured` 訊息。

>[!NOTE]
>
>如果您使用 `success` 回撥函式，則輸出值不會填入指定的表單欄位中。

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
