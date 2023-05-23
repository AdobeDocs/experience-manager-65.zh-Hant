---
title: 從自適應表單調用表單資料模型服務的API
seo-title: API to invoke form data model service from adaptive forms
description: 說明可用於從自適應表單域中調用在WSDL中寫入的Web服務的invokeWebServices API。
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

# 從自適應表單調用表單資料模型服務的API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 概觀 {#overview}

AEM Forms使表單作者能夠通過從自適應表單域調用表單資料模型中配置的服務來進一步簡化和增強表單填充體驗。 要調用資料模型服務，可以在可視編輯器中建立規則或使用 `guidelib.dataIntegrationUtils.executeOperation` 代碼編輯器中的API [規則編輯器](/help/forms/using/rule-editor.md)。

本文檔重點介紹使用 `guidelib.dataIntegrationUtils.executeOperation` 調用服務的API。

## 使用API {#using-the-api}

的 `guidelib.dataIntegrationUtils.executeOperation` API從自適應表單域內調用服務。 API語法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

的結構 `guidelib.dataIntegrationUtils.executeOperation` API指定有關服務操作的詳細資訊。 結構的語法如下所示。

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

API結構指定有關服務操作的以下詳細資訊。

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
   <td>將一個或多個表單對象映射到從服務操作輸出值以填充表單域<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>根據服務操作的輸入參數返回值。 它是用作回調函式的可選參數。<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>如果成功回調函式無法基於輸入參數顯示輸出值，則顯示錯誤消息。 它是用作回調函式的可選參數。<br /> </td>
  </tr>
 </tbody>
</table>

## 調用服務的示例指令碼 {#sample-script-to-invoke-a-service}

以下示例指令碼使用 `guidelib.dataIntegrationUtils.executeOperation` 調用 `getAccountById` 在中配置的服務操作 `employeeAccount` 表單資料模型。

的 `getAccountById` 操作將在 `employeeID` 作為輸入的窗體欄位 `empId` 參數並返回相應員工的員工姓名、帳號和帳戶餘額。 輸出值將填充到指定的表單欄位中。 例如，中的值 `name` 參數填充在 `fullName` 窗體元素和值 `accountNumber` 參數 `account` 窗體元素。

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

## 將API與回調函式一起使用 {#using-the-api-callback}

您還可以使用 `guidelib.dataIntegrationUtils.executeOperation` 具有回調函式的API。 API語法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

回叫功能可以 `success` 和 `failure` 回調函式。

### 具有成功和失敗回調函式的示例指令碼 {#callback-function-success-failure}

以下示例指令碼使用 `guidelib.dataIntegrationUtils.executeOperation` 調用 `GETOrder` 在中配置的服務操作 `employeeOrder` 表單資料模型。

的 `GETOrder` 操作將在 `Order ID` 作為輸入的窗體欄位 `orderId` 參數和返回訂單數量值 `success` 回調函式。  如果 `success` 回調函式不返回訂單數量， `failure` 回調函式顯示 `Error occured` 。

>[!NOTE]
>
>如果使用 `success` 回調函式，輸出值不填充在指定的表單域中。

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
