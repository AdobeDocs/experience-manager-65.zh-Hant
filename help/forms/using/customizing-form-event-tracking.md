---
title: 自訂表單事件追蹤
description: 如果使用者在欄位上花費超過60秒，則會觸發fieldvisit事件並將該欄位的詳細資訊傳送到Adobe SiteCatalyst。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# 自訂表單事件追蹤 {#customizing-form-event-tracking}

下列現成事件會在啟用Analytics的最適化表單中受到追蹤：

<table>
 <tbody>
  <tr>
   <th>事件</th>
   <th>可用變數</th>
  </tr>
  <tr>
   <td>轉譯</td>
   <td>formName， formTitle， formInstance， source</td>
  </tr>
  <tr>
   <td>捨棄</td>
   <td>formName、formTitle、formInstance、panelName、panelTitle</td>
  </tr>
  <tr>
   <td>儲存</td>
   <td>formName， formTitle， formInstance， panelName， source</td>
  </tr>
  <tr>
   <td>提交</td>
   <td>formName， formTitle， formInstance， source</td>
  </tr>
  <tr>
   <td>錯誤</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle</td>
  </tr>
  <tr>
   <td>說明</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelVisit</td>
   <td>formName， formTitle， panelName， panelTitle</td>
  </tr>
 </tbody>
</table>

## 自訂欄位造訪事件逾時 {#customizing-the-field-visit-event-timeout}

在預設AEM表單設定中，如果使用者在欄位上花費超過60秒，則 `fieldvisit` 事件會觸發，而欄位的詳細資訊會傳送至Adobe Analytics。 您可以在AEM設定控制檯(/system/console/configMgr)的AEM Forms Analytics設定下自訂欄位時間追蹤基準線，以增加或減少逾時限制。

## 自訂追蹤事件 {#customizing-the-tracking-events}

您可以修改 `trackEvent`中可用的函式 `/libs/afanalytics/js/custom.js` 檔案來自訂事件追蹤。 每當要追蹤的事件以最適化表單發生時， `trackEvent`呼叫函式。 此 `trackEvent` 函式接受兩個引數： `eventName`和 `variableValueMap`.

您可以評估下列專案的值： *事件名稱* 和 *variableValueMap* 引數來變更事件的追蹤行為。 例如，您可以選擇在發生特定數量的錯誤事件後，將資訊傳送至Analytics伺服器。 您也可以選擇執行下列任一自訂專案：

* 您可以在傳送事件前設定臨界值時間。
* 您可以維護狀態以決定動作，例如， *fieldVisit* 根據上一個事件的時間戳記推送一個虛擬事件。
* 您可以使用 `pushEvent` 將事件傳送至analytics伺服器的函式 *.*

* 您可以選擇完全不將事件推送至分析伺服器。

### 範例 {#sample}

在下列範例中， *錯誤* 每個的事件 *fieldName* 屬性已維護。 只有在再次發生錯誤時，才會將事件傳送至Analytics伺服器。

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## 自訂面板造訪事件 {#customizing-the-panelvisit-event}

在預設AEM Forms設定中，每60秒會檢查一次包含最適化表單的視窗是否處於作用中狀態。 如果視窗處於作用中狀態， `panelVisit`事件會觸發至Adobe Analytics。 這有助於確定檔案或表單是否作用中，以及計算在對應表單或檔案上所花費的時間。

>[!NOTE]
>
>用來保留活動和計算逗留時間的事件名稱為「panelVisit」。 此事件與上表所列之面板造訪事件不同。

您可以修改中可用的scheduleHeartBeatCheck函式 `/libs/afanalytics/js/custom.js` 以定期變更或停止傳送至Adobe Analytics的此事件。
