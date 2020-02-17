---
title: 自訂表單事件追蹤
seo-title: 自訂表單事件追蹤
description: 如果使用者在欄位上逗留超過60秒，則會觸發欄位瀏覽事件，並將欄位的詳細資訊傳送至Adobe SiteCatalyst。
seo-description: 如果使用者在欄位上逗留超過60秒，則會觸發欄位瀏覽事件，並將欄位的詳細資訊傳送至Adobe SiteCatalyst。
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
translation-type: tm+mt
source-git-commit: dfa983db4446cbb0cbdeb42297248aba55b3dffd

---


# 自訂表單事件追蹤 {#customizing-form-event-tracking}

立即可用的分析功能「最適化表單」會追蹤下列事件：

<table>
 <tbody>
  <tr>
   <th>事件</th>
   <th>可用變數</th>
  </tr>
  <tr>
   <td>渲染</td>
   <td>formName、formTitle、formInstance、source</td>
  </tr>
  <tr>
   <td>放棄</td>
   <td>formName、formTitle、formInstance、panelName、panelTitle</td>
  </tr>
  <tr>
   <td>儲存</td>
   <td>formName、formTitle、formInstance、panelName、source</td>
  </tr>
  <tr>
   <td>提交</td>
   <td>formName、formTitle、formInstance、source</td>
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
   <td>formName、formTitle、panelName、panelTitle</td>
  </tr>
 </tbody>
</table>

## 自訂欄位瀏覽事件逾時 {#customizing-the-field-visit-event-timeout}

在預設的AEM表單設定中，如果使用者在欄位上逗留超過60秒，則會觸發事件 `fieldvisit` ，並將欄位的詳細資訊傳送至Adobe Analytics。 您可以在AEM Configuration主控台(/system/console/configMgr)的「AEM Forms Analytics Configuration」（AEM Forms Analytics設定）下自訂欄位時間追蹤基準，以增加或減少逾時限制。

## 自訂追蹤事件 {#customizing-the-tracking-events}

您可以修改檔 `trackEvent`案中可用的 `/libs/afanalytics/js/custom.js` 函式，以自訂事件追蹤。 每當正在追蹤的事件以最適化形式發生時，就會 `trackEvent`呼叫函式。 函式 `trackEvent` 接受兩個參數： `eventName`和 `variableValueMap`。

您可以評估eventName *和variable* ValueMap ** 引數的值，以變更事件的追蹤行為。 例如，您可以選擇在發生特定數目的錯誤事件後，將資訊傳送至分析伺服器。 您也可以選擇執行下列任一自訂：

* 您可以在傳送事件之前設定臨界值時間。
* 您可以維護狀態以決定動作，例如 *fieldVisit* 根據上一個事件的時間戳記推送虛擬事件。
* 您可以使用函 `pushEvent` 數將事件傳送至分析伺服器 *。*

* 您可以選擇完全不將事件推送至分析伺服器。

### 範例 {#sample}

在下列範例中，會維 *護每個fieldName* 屬性的 ** error事件狀態。 事件只會在再次發生錯誤時傳送至分析伺服器。

```
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## 自訂panelvisit事件 {#customizing-the-panelvisit-event}

在預設的AEM Forms設定中，每60秒後，如果包含最適化表單的視窗處於活動狀態，就會勾選此設定。 如果視窗為作用中，則 `panelVisit`會觸發事件至Adobe Analytics。 它有助於確定文檔或表單是否處於活動狀態，並計算在相應表單或文檔上花費的時間。

>[!NOTE]
>
>用來取得活動和計算逗留時間的事件名稱為&quot;panelVisit&quot;。 此事件與上表所列的面板瀏覽事件不同。

您可以修改檔案中可用的scheduleHeartBeatCheck函式， `/libs/afanalytics/js/custom.js` 以定期間隔變更或停止傳送至Adobe Analytics的事件。
