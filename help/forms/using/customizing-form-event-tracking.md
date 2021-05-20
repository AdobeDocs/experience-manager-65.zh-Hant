---
title: 自訂表單事件追蹤
seo-title: 自訂表單事件追蹤
description: 如果使用者在欄位上逗留超過60秒，則會觸發欄位造訪事件，並將欄位的詳細資訊傳送至Adobe SiteCatalyst。
seo-description: 如果使用者在欄位上逗留超過60秒，則會觸發欄位造訪事件，並將欄位的詳細資訊傳送至Adobe SiteCatalyst。
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 自訂表單事件追蹤{#customizing-form-event-tracking}

以下事件會立即在啟用分析的適用性表單中追蹤：

<table>
 <tbody>
  <tr>
   <th>事件</th>
   <th>可用變數</th>
  </tr>
  <tr>
   <td>轉譯</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>放棄</td>
   <td>formName, formTitle, formInstance, panelName, panelTitle</td>
  </tr>
  <tr>
   <td>儲存</td>
   <td>formName, formTitle, formInstance, panelName, source</td>
  </tr>
  <tr>
   <td>提交</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>錯誤</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>說明</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelVisit</td>
   <td>formName, formTitle, panelName, panelTitle</td>
  </tr>
 </tbody>
</table>

## 自訂欄位造訪事件逾時{#customizing-the-field-visit-event-timeout}

在預設的AEM表單設定中，如果使用者在欄位上逗留超過60秒，則會觸發`fieldvisit`事件，並將欄位的詳細資料傳送至Adobe Analytics。 您可以在AEM設定主控台(/system/console/configMgr)的AEM Forms Analytics設定下自訂欄位時間追蹤基準，以增加或減少逾時限制。

## 自訂追蹤事件{#customizing-the-tracking-events}

您可以修改`/libs/afanalytics/js/custom.js`檔案中可用的`trackEvent`函式以自訂事件追蹤。 每當受追蹤的事件以最適化形式發生時，就會呼叫`trackEvent`函式。 `trackEvent`函式接受兩個參數：`eventName`和`variableValueMap`。

您可以評估&#x200B;*eventName*&#x200B;和&#x200B;*variableValueMap*&#x200B;引數的值，以變更事件的追蹤行為。 例如，您可以在發生特定數量的錯誤事件後，選擇將資訊傳送至分析伺服器。 您也可以選擇執行下列任一自訂：

* 您可以在傳送事件之前設定臨界值時間。
* 您可以維護狀態以決定動作，例如，*fieldVisit*&#x200B;根據上次事件的時間戳推送虛擬事件。
* 您可以使用`pushEvent`函式將事件傳送至分析伺服器&#x200B;*。*

* 您完全可以選擇不推送事件至分析伺服器。

### 範例 {#sample}

在以下範例中，維護每個&#x200B;*fieldName*&#x200B;屬性的&#x200B;*error*&#x200B;事件的狀態。 只有在再次發生錯誤時，才會將事件傳送至分析伺服器。

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## 自訂面板瀏覽事件{#customizing-the-panelvisit-event}

在預設的AEM Forms設定中，每60秒後，如果包含最適化表單的視窗處於作用中狀態，則會勾選此設定。 如果視窗處於作用中狀態，會對Adobe Analytics觸發`panelVisit`事件。 它有助於確定文檔或表單是否處於活動狀態，並計算在相應的表單或文檔上花費的時間。

>[!NOTE]
>
>用來擷取活動和計算逗留時間的事件名稱為「panelVisit」。 此事件與上表所列的面板造訪事件不同。

您可以修改`/libs/afanalytics/js/custom.js`檔案中可用的scheduleHeartBeatCheck函式，以定期間隔變更或停止傳送至Adobe Analytics的此事件。
